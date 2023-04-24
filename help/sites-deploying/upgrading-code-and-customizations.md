---
title: Actualización de código y personalizaciones
seo-title: Upgrading Code and Customizations
description: Obtenga más información sobre la actualización de código personalizado en AEM.
seo-description: Learn more about upgrading custom code in AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
source-git-commit: a296e459461973fc2dbd0641c6fdda1d89d8d524
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 0%

---

# Actualización de código y personalizaciones{#upgrading-code-and-customizations}

Al planificar una actualización, deben investigarse y abordarse las siguientes áreas de una implementación.

* [Actualizar la base de código](#upgrade-code-base)
* [Alinear con la estructura del repositorio 6.5](#align-repository-structure)
* [Personalizaciones de AEM](#aem-customizations)
* [Procedimiento de prueba](#testing-procedure)

## Información general {#overview}

1. **Detector de patrones** - Ejecute el detector de patrones tal como se describe en la planificación de actualizaciones y se describe detalladamente en [esta página](/help/sites-deploying/pattern-detector.md). Se obtiene un informe de detector de patrones que contiene más detalles sobre las áreas que se deben abordar, además de las API o paquetes no disponibles en la versión de AEM de Target. El informe Detección de patrones proporciona una indicación de cualquier incompatibilidad en el código. Si no existe ninguna, la implementación ya es compatible con la versión 6.5. Puede optar por hacer un nuevo desarrollo para utilizar la funcionalidad 6.5, pero no lo necesita solo para mantener la compatibilidad. Si se notifican incompatibilidades, puede elegir ejecutar en modo de compatibilidad y aplazar el desarrollo para nuevas funciones o compatibilidad con la versión 6.5. O bien, puede decidir realizar el desarrollo después de la actualización y pasar al paso 2. Consulte [Compatibilidad con versiones anteriores en AEM 6.5](/help/sites-deploying/backward-compatibility.md) para obtener más información.

1. **Desarrollar base de código para 6.5 **- Crear una rama o repositorio dedicado para la base de código para la versión de Target. Utilice la información de Compatibilidad previa a la actualización para planificar las áreas de código que se actualizarán.
1. **Compilar con 6.5 Uber jar **- Actualice los POMs de base de código para que apunten a 6.5 uber jar y compile código en su contra.
1. **Actualizar AEM personalizaciones*** - *Cualquier personalización o extensión de AEM debe actualizarse/validarse para funcionar en la versión 6.5 y añadirse a la base de código 6.5. Incluye Búsqueda de IU Forms, Personalizaciones de recursos, cualquier cosa que utilice /mnt/overlay

1. **Implementar en entorno 6.5** - Se debe instalar una instancia limpia de AEM 6.5 (Autor + Publicación) en un entorno de desarrollo/control de calidad. Se debe implementar una base de código actualizada y una muestra de contenido representativa (de la producción actual).
1. **Validación de control de calidad y corrección de errores** - El control de calidad debe validar la aplicación tanto en las instancias de Autor como de Publicación de la versión 6.5. Cualquier error encontrado debe corregirse y confirmarse en la base de código de la versión 6.5. Repita el ciclo de desarrollo según sea necesario hasta que se corrijan todos los errores.

Antes de continuar con una actualización, debe tener una base de código de aplicación estable que se haya probado a fondo con la versión de destino de AEM. Según las observaciones realizadas en las pruebas, podría haber maneras de optimizar el código personalizado. Por ejemplo, podría incluir refactorizar el código para evitar atravesar el repositorio, la indexación personalizada para optimizar la búsqueda o el uso de nodos no ordenados en JCR, entre otros.

Además de actualizar opcionalmente la base de código y las personalizaciones para que funcionen con la nueva versión de AEM, la versión 6.5 también ayuda a administrar las personalizaciones de forma más eficiente con la función Compatibilidad con versiones anteriores como se describe en [esta página](/help/sites-deploying/backward-compatibility.md).

Como se ha mencionado anteriormente y se muestra en el diagrama siguiente, al ejecutar el [Detector de patrones](/help/sites-deploying/pattern-detector.md) en el primer paso puede ayudarle a evaluar la complejidad general de la actualización. También puede ayudarle a decidir si desea ejecutar en modo de compatibilidad o actualizar sus personalizaciones para utilizar todas las nuevas funciones de AEM 6.5. Consulte la [Compatibilidad con versiones anteriores en AEM 6.5](/help/sites-deploying/backward-compatibility.md) para obtener más información.
[ ![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Actualizar la base de código {#upgrade-code-base}

### Crear una rama dedicada para el código 6.5 en el control de versiones {#create-a-dedicated-branch-for-6.5-code-in-version-control}

Todo el código y las configuraciones necesarias para la implementación de AEM se deben administrar con alguna forma de control de versiones. Se debe crear una rama dedicada en el control de versiones para administrar los cambios necesarios para la base de código en la versión de destino de AEM. En esta rama se administran pruebas iterativas del código base con la versión de destino de AEM y correcciones de errores posteriores.

### Actualización de la versión de AEM Uber Jar {#update-the-aem-uber-jar-version}

El AEM Uber jar incluye todas las API de AEM como una sola dependencia en el proyecto Maven `pom.xml`. Siempre es una práctica recomendada incluir Uber Jar como una dependencia única en lugar de incluir dependencias de API de AEM individuales. Al actualizar la base de código, cambie la versión de Uber Jar para que apunte a la versión de destino de AEM. Si el proyecto se desarrolló en una versión de AEM antes de la existencia de Uber Jar, elimine todas las dependencias individuales de API de AEM. Sustitúyalas por una sola inclusión de Uber Jar para la versión de destino de AEM. Recompile el código base con la nueva versión de Uber Jar. Actualice cualquier API o método obsoleto para que sea compatible con la versión de destino de AEM.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### Eliminación progresiva del uso de la resolución de recursos administrativos {#phase-out-use-of-administrative-resource-resolver}

El uso de una sesión administrativa mediante `SlingRepository.loginAdministrative()` y `ResourceResolverFactory.getAdministrativeResourceResolver()` era frecuente en las bases de código antes de AEM 6.0. Estos métodos han quedado obsoletos por motivos de seguridad, ya que ofrecen un nivel de acceso demasiado amplio. [En futuras versiones de Sling, estos métodos se eliminarán](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). Se recomienda refactorizar cualquier código para utilizar usuarios de servicios en su lugar. Más información sobre los usuarios de servicios y [cómo eliminar sesiones administrativas aquí](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### Consultas e índices de Oak {#queries-and-oak-indexes}

Cualquier uso de consultas en la base de código debe probarse exhaustivamente como parte de la actualización de la base de código. Para los clientes que actualizan desde Jackrabbit 2 (versiones de AEM anteriores a la 6.0), esta prueba es especialmente importante, ya que Oak no indexa el contenido automáticamente y se deben crear índices personalizados. Si se actualiza desde una versión AEM 6.x, las definiciones de índice Oak predeterminadas pueden haber cambiado y podrían afectar a las consultas existentes.

Las siguientes herramientas están disponibles para analizar e inspeccionar el rendimiento de las consultas:

* [Herramientas de índice de AEM](/help/sites-deploying/queries-and-indexing.md)

* [Herramientas de diagnóstico de operaciones - Rendimiento de la consulta](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### Creación de IU clásica {#classic-ui-authoring}

La creación de IU clásica sigue disponible en AEM 6.5, pero está en desuso. Encontrará más información [here](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). Si la aplicación se está ejecutando en el entorno de creación de la IU clásica, se recomienda actualizar a AEM 6.5 y seguir utilizando la IU clásica. La migración a la interfaz de usuario táctil se puede planificar como un proyecto independiente para completar varios ciclos de desarrollo. Para utilizar la IU clásica en AEM 6.5, se deben confirmar varias configuraciones de OSGi en la base de código. Encontrará más detalles sobre cómo realizar la configuración [here](/help/sites-administering/enable-classic-ui.md).

## Alinear con la estructura del repositorio 6.5 {#align-repository-structure}

Para facilitar las actualizaciones y garantizar que las configuraciones no se sobrescriban durante una actualización, el repositorio se reestructurará en la versión 6.4 para separar el contenido de la configuración.

Por lo tanto, se deben mover varias configuraciones para dejar de residir en `/etc` como en el pasado. Para revisar el conjunto completo de preocupaciones de reestructuración de repositorios que deben revisarse y tenerse en cuenta en la versión actualizada a la AEM 6.4, véase [Reestructuración de repositorios en AEM 6.4](/help/sites-deploying/repository-restructuring.md).

## Personalizaciones de AEM  {#aem-customizations}

Se deben identificar todas las personalizaciones del entorno de creación de AEM en la versión de origen de AEM. Una vez identificados, se recomienda almacenar cada personalización en el control de versiones o, como mínimo, en una copia de seguridad como parte de un paquete de contenido. Todas las personalizaciones deben implementarse y validarse en un entorno de control de calidad o ensayo que ejecute la versión de destino de AEM antes de una actualización de producción.

### Superposiciones en general {#overlays-in-general}

Es una práctica habitual ampliar AEM funcionalidad predeterminada superponiendo nodos y/o archivos bajo /libs con nodos adicionales bajo /apps. Estas superposiciones deben rastrearse en el control de versiones y probarse con la versión de destino de AEM. Si un archivo (como JS, JSP, HTL) está superpuesto, Adobe recomienda dejar un comentario sobre qué funcionalidad se aumentó para facilitar las pruebas de regresión en la versión de destino de AEM. Puede encontrar más información sobre las superposiciones en general [here](/help/sites-developing/overlays.md). A continuación se encuentran las instrucciones para superposiciones de AEM específicas.

### Actualización de Forms de búsqueda personalizada {#upgrading-custom-search-forms}

Las facetas de búsqueda personalizadas requieren algunos ajustes manuales después de la actualización para funcionar correctamente. Para obtener más información, consulte [Actualización de Forms de búsqueda personalizada](/help/sites-deploying/upgrading-custom-search-forms.md).

### Personalizaciones de la interfaz de usuario de Assets {#assets-ui-customizations}

>[!NOTE]
>
>Este procedimiento solo es necesario para las actualizaciones de versiones anteriores a la AEM 6.2.

Las instancias que tienen implementaciones personalizadas de Assets deben estar preparadas para la actualización. Esta acción es necesaria para garantizar que todo el contenido personalizado sea compatible con la nueva estructura de nodos 6.4.

Puede preparar las personalizaciones de la interfaz de usuario de Assets haciendo lo siguiente:

1. En la instancia que se está actualizando, abra el CRXDE Lite yendo a *https://server:port/crx/de/index.jsp*

1. Vaya al siguiente nodo:

   * `/apps/dam/content`

1. Cambie el nombre del nodo de contenido a **content_backup** haciendo clic con el botón derecho en el panel del explorador en el lado izquierdo de la ventana y seleccionando **Cambiar nombre**.

1. Una vez que se haya cambiado el nombre del nodo, cree un nodo denominado content en `/apps/dam` named **contenido** y establezca su tipo de nodo en **sling:Folder**.

1. Mover todos los nodos secundarios de **content_backup** al nodo de contenido recién creado haciendo clic con el botón derecho en cada nodo secundario del panel del explorador y seleccionando **Mover**.

1. Elimine el **content_backup** nodo .

1. Los nodos actualizados debajo de `/apps/dam` con el tipo de nodo correcto de `sling:Folder` idealmente debe guardarse en control de versiones e implementarse con el código base o con una copia de seguridad mínima como paquete de contenido.

### Generación de ID de recursos para recursos existentes {#generating-asset-ids-for-existing-assets}

Para generar ID de recursos para recursos existentes, actualice los recursos al actualizar la instancia de AEM para que se ejecute AEM 6.5. Este paso es necesario para habilitar la variable [Función de Assets Insights](/help/assets/asset-insights.md). Para obtener más información, consulte [Añadir código incrustado](/help/assets/use-page-tracker.md#add-embed-code).

Para actualizar recursos, configure el paquete Asociar ID de recursos en la consola JMX. En función del número de recursos del repositorio, `migrateAllAssets` puede tardar mucho tiempo. Las pruebas internas de Adobe estiman que aproximadamente una hora para 125000 activos en TarMK.

![1487758945977](assets/1487758945977.png)

Si necesita ID de recursos para un subconjunto de todos los recursos, use la variable `migrateAssetsAtPath` API.

Para todos los demás fines, utilice la variable `migrateAllAssets()` API.

### Personalizaciones de secuencias de comandos de InDesign {#indesign-script-customizations}

Adobe recomienda colocar scripts personalizados en `/apps/settings/dam/indesign/scripts` ubicación. Encontrará más información sobre las personalizaciones de las secuencias de comandos de InDesign [here](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Recuperación de las configuraciones de ContextHub {#recovering-contexthub-configurations}

Las configuraciones de ContextHub se ven afectadas por una actualización. Encontrará instrucciones sobre cómo recuperar las configuraciones existentes de ContextHub [here](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### Personalizaciones de flujo de trabajo {#workflow-customizations}

Es una práctica habitual editar flujos de trabajo listos para usar para añadir o eliminar funciones innecesarias. Un flujo de trabajo común personalizado es el [!UICONTROL Recurso de actualización DAM] flujo de trabajo. Todos los flujos de trabajo necesarios para una implementación personalizada deben realizarse copias de seguridad y almacenarse en el control de versiones, ya que se pueden sobrescribir durante una actualización.

### Plantillas editables {#editable-templates}

>[!NOTE]
>
>Este procedimiento solo es necesario para las actualizaciones de sitios que utilizan plantillas editables de AEM 6.2

La estructura de las plantillas editables ha cambiado entre AEM 6.2 y 6.3. Si actualiza desde 6.2 o versiones anteriores y si el contenido del sitio se crea con plantillas editables, debe usar la variable [Herramienta de limpieza de nodos interactivos](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). La herramienta está pensada para ejecutarse **after** una actualización para limpiar contenido. Ejecutarlo en los niveles Autor y Publicar .

### Cambios en la implementación del CUG {#cug-implementation-changes}

La implementación de Grupos de usuarios cerrados ha cambiado significativamente para abordar las limitaciones de rendimiento y escalabilidad en versiones anteriores de AEM. La versión anterior de CUG quedó obsoleta en la versión 6.3 y la nueva implementación solo es compatible con la interfaz de usuario táctil. Si está actualizando desde la versión 6.2 o anterior, puede encontrar instrucciones para migrar a la nueva implementación de CUG [here](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## Procedimiento de prueba {#testing-procedure}

Se debe preparar un plan de prueba completo para probar las actualizaciones. La prueba de la base de código y la aplicación actualizadas debe realizarse primero en entornos más bajos. Los errores encontrados deben corregirse de forma iterativa hasta que la base de código sea estable, solo entonces se deben actualizar los entornos de nivel superior.

### Prueba del procedimiento de actualización {#testing-the-upgrade-procedure}

El procedimiento de actualización como se describe aquí debe probarse en entornos de desarrollo y control de calidad como se documenta en su libro de ejecución personalizado (consulte [Planificación de la actualización](/help/sites-deploying/upgrade-planning.md)). El procedimiento de actualización debe repetirse hasta que todos los pasos estén documentados en el libro de ejecución de la actualización y el proceso de actualización sea fluido.

### Áreas de prueba de implementación  {#implementation-test-areas-}

A continuación, se muestran áreas críticas de cualquier implementación de AEM que debería incluirse en el plan de prueba una vez que el entorno se haya actualizado y se haya implementado la base de código actualizada.

<table>
 <tbody>
  <tr>
   <td><strong>Área de prueba funcional</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Sitios publicados</td>
   <td>Prueba de la implementación de AEM y el código asociado en el nivel de publicación<br /> a través de Dispatcher. Debe incluir criterios para las actualizaciones de página y<br /> invalidación de caché.</td>
  </tr>
  <tr>
   <td>Creación</td>
   <td>Prueba de la implementación de AEM y el código asociado en el nivel Autor. Debe incluir la creación de páginas, componentes y cuadros de diálogo.</td>
  </tr>
  <tr>
   <td>Integraciones con soluciones de Experience Cloud</td>
   <td>Validación de integraciones con productos como Analytics, DTM y Target.</td>
  </tr>
  <tr>
   <td>Integraciones con sistemas de terceros</td>
   <td>Valide las integraciones de terceros en los niveles Author y Publish .</td>
  </tr>
  <tr>
   <td>Autenticación, seguridad y permisos</td>
   <td>Cualquier mecanismo de autenticación como LDAP/SAML debe validarse.<br /> Los permisos y grupos deben probarse tanto en Autor como en Publicación<br /> niveles.</td>
  </tr>
  <tr>
   <td>Consultas</td>
   <td>Los índices personalizados y las consultas deben probarse junto con el rendimiento de la consulta.</td>
  </tr>
  <tr>
   <td>Personalizaciones de la interfaz de usuario</td>
   <td>Las extensiones o personalizaciones de la interfaz de usuario de AEM en el entorno de creación.</td>
  </tr>
  <tr>
   <td>Flujos de trabajo</td>
   <td>Flujos de trabajo y funciones personalizados y/o listos para usar.</td>
  </tr>
  <tr>
   <td>Pruebas de rendimiento</td>
   <td>Las pruebas de carga deben realizarse en los niveles Author y Publish que simulen escenarios reales.</td>
  </tr>
 </tbody>
</table>

### Plan y resultados de la prueba de documento {#document-test-plan-and-results}

Se debe crear un plan de prueba que cubra las áreas de prueba de implementación anteriores. A menudo tiene sentido separar el plan de prueba por listas de tareas Autor y Publicar . Este plan de prueba debe ejecutarse en los entornos Dev, QA y Stage antes de actualizar los entornos de producción. Los resultados de las pruebas y las métricas de rendimiento deben capturarse en entornos más bajos para proporcionar comparación al actualizar entornos de fase y producción.
