---
title: Actualización de código y personalizaciones
seo-title: Actualización de código y personalizaciones
description: Obtenga más información sobre la actualización de código personalizado en AEM.
seo-description: Obtenga más información sobre la actualización de código personalizado en AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
feature: Actualización
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2205'
ht-degree: 0%

---


# Actualización de código y personalizaciones{#upgrading-code-and-customizations}

Al planificar una actualización, es necesario investigar y abordar las siguientes áreas de una implementación.

* [Actualizar la base de código](#upgrade-code-base)
* [Alinear con la estructura del repositorio 6.5](#align-repository-structure)
* [Personalizaciones de AEM](#aem-customizations)
* [Procedimiento de prueba](#testing-procedure)

## Información general {#overview}

1. **Detector de patrones** : ejecute el detector de patrones tal como se describe en la planificación de actualizaciones y se describe detalladamente en  [esta ](/help/sites-deploying/pattern-detector.md) página para obtener un informe detector de patrones que contenga más detalles sobre las áreas que deben abordarse además de las API o paquetes no disponibles en la versión de AEM de Target. El informe Detección de patrones debería darle una indicación de cualquier incompatibilidad en su código. Si no hay ninguna, entonces la implementación ya es compatible con la versión 6.5, puede optar por hacer un nuevo desarrollo para utilizar la funcionalidad 6.5, pero no lo necesita solo para mantener la compatibilidad. Si se notifican incompatibilidades, puede elegir entre: a) Ejecutar en modo de compatibilidad y aplazar el desarrollo para nuevas funciones de 6.5 o compatibilidad, b) Decidir hacer desarrollo después de la actualización y pasar al paso 2. Consulte la [Compatibilidad con versiones anteriores en AEM 6.5](/help/sites-deploying/backward-compatibility.md) para obtener más información.

1. **Desarrollar base de código para 6.5 **- Crear una rama o repositorio dedicado para la base de código para la versión de Target. Utilice la información de Compatibilidad previa a la actualización para planificar las áreas de código que se actualizarán.
1. **Compilar con 6.5 Uber jar **- Actualice los POMs de base de código para que apunten a 6.5 uber jar y compile código en contra de esto.
1. **Actualización AEM personalizaciones*** : *Cualquier personalización o extensión que AEM debe actualizarse o validarse para que funcione en la versión 6.5 y agregarse a la base de código 6.5. Incluye Búsqueda de IU Forms, Personalizaciones de recursos, cualquier cosa que utilice /mnt/overlay

1. **Implementar en entorno 6.5** : Se debe instalar una instancia limpia de AEM 6.5 (Autor + Publicación) en un entorno de desarrollo/control de calidad. Se debe implementar una base de código actualizada y una muestra de contenido representativa (de la producción actual).
1. **Validación de control de calidad y corrección de errores** : el control de calidad debe validar la aplicación tanto en la instancia de autor como en la de publicación de 6.5. Cualquier error encontrado debe corregirse y confirmarse en la base de código de 6.5. Repita el ciclo de desarrollo según sea necesario hasta que se corrijan todos los errores.

Antes de continuar con una actualización, debe tener una base de código de aplicación estable que se haya probado a fondo con la versión de destino de AEM. En función de las observaciones realizadas en las pruebas, podría haber maneras de optimizar el código personalizado. Esto podría incluir refactorizar el código para evitar atravesar el repositorio, la indexación personalizada para optimizar la búsqueda, o el uso de nodos no ordenados en JCR, entre otros.

Además de la opción de actualizar la base de código y las personalizaciones para que funcionen con la nueva versión de AEM, 6.5 también ayuda a administrar las personalizaciones de forma más eficiente con la función Compatibilidad con versiones anteriores como se describe en [esta página](/help/sites-deploying/backward-compatibility.md).

Como se menciona más arriba y se muestra en el diagrama siguiente, ejecutar [Pattern Detector](/help/sites-deploying/pattern-detector.md) en el primer paso le ayudará a evaluar la complejidad general de la actualización y si desea ejecutar en modo de compatibilidad o actualizar sus personalizaciones para utilizar todas las nuevas funciones de AEM 6.5. Consulte la [Compatibilidad con versiones anteriores en AEM página 6.5](/help/sites-deploying/backward-compatibility.md) para obtener más información.
[ ![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Actualizar la base de código {#upgrade-code-base}

### Crear una rama dedicada para el código 6.5 en el control de versiones {#create-a-dedicated-branch-for-6.5-code-in-version-control}

Todo el código y las configuraciones necesarias para la implementación de AEM se deben administrar con alguna forma de control de versiones. Se debe crear una rama dedicada en el control de versiones para administrar los cambios necesarios para la base de código en la versión de destino de AEM. En esta rama se gestionarán pruebas iterativas del código base con respecto a la versión de destino de AEM y correcciones de errores posteriores.

### Actualizar la versión de AEM Uber Jar {#update-the-aem-uber-jar-version}

El AEM Uber jar incluye todas las API de AEM como una sola dependencia en el `pom.xml` de su proyecto Maven. Siempre es una práctica recomendada incluir Uber Jar como una dependencia única en lugar de incluir dependencias de API de AEM individuales. Al actualizar la base de código, la versión de Uber Jar debe cambiarse para que apunte a la versión de destino de AEM. Si el proyecto se desarrolló en una versión de AEM antes de la existencia de Uber Jar, todas las dependencias individuales de la API de AEM deben eliminarse y reemplazarse por una sola inclusión de Uber Jar para la versión de destino de AEM. La base de código debe recompilarse con la nueva versión de Uber Jar. Cualquier API o método obsoleto debe actualizarse para que sea compatible con la versión de destino de AEM.

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

El uso de una sesión administrativa a través de `SlingRepository.loginAdministrative()` y `ResourceResolverFactory.getAdministrativeResourceResolver()` era bastante frecuente en las bases de código antes de AEM 6.0. Estos métodos han quedado obsoletos por motivos de seguridad, ya que ofrecen un nivel de acceso demasiado amplio. [En futuras versiones de Sling, se eliminarán](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication) estos métodos. Se recomienda refactorizar cualquier código para utilizar usuarios de servicios en su lugar. Puede encontrar más información sobre los usuarios de servicios y [cómo eliminar sesiones administrativas aquí](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### Consultas e índices Oak {#queries-and-oak-indexes}

Cualquier uso de consultas en la base de código debe probarse exhaustivamente como parte de la actualización de la base de código. Para los clientes que actualizan desde Jackrabbit 2 (versiones de AEM anteriores a la 6.0) esto es especialmente importante, ya que Oak no indexa el contenido automáticamente y es posible que se deban crear índices personalizados. Si se actualiza desde una versión AEM 6.x, las definiciones de índice Oak pueden haber cambiado y podrían afectar a las consultas existentes.

Hay varias herramientas disponibles para analizar e inspeccionar el rendimiento de las consultas:

* [Herramientas de índice de AEM](/help/sites-deploying/queries-and-indexing.md)

* [Herramientas de diagnóstico de operaciones - Rendimiento de la consulta](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

* [Utils Oak](https://oakutils.appspot.com/). Se trata de una herramienta de código abierto que no mantiene el Adobe.

### Creación de IU clásica {#classic-ui-authoring}

La creación de IU clásica sigue disponible en AEM 6.5, pero está en desuso. Puede encontrar más información [aquí](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). Si la aplicación se está ejecutando en el entorno de creación de la IU clásica, se recomienda actualizar a AEM 6.5 y seguir utilizando la IU clásica. La migración a la interfaz de usuario táctil se puede planificar como proyecto independiente para completarlo en varios ciclos de desarrollo. Para utilizar la IU clásica en AEM 6.5, es necesario confirmar varias configuraciones de OSGi en la base de código. Puede encontrar más detalles sobre cómo configurar esto [aquí](/help/sites-administering/enable-classic-ui.md).

## Alinear con la estructura del repositorio 6.5 {#align-repository-structure}

Para facilitar las actualizaciones y garantizar que las configuraciones no se sobrescriban durante una actualización, el repositorio se reestructurará en la versión 6.4 para separar el contenido de la configuración.

Por lo tanto, se debe mover una serie de configuraciones para dejar de residir en `/etc` como había sido el caso en el pasado. Para revisar el conjunto completo de preocupaciones de reestructuración de repositorios que deben revisarse y adaptarse en la versión actualizada a la AEM 6.4, consulte [Reestructuración de repositorios en la AEM 6.4](/help/sites-deploying/repository-restructuring.md).

## Personalizaciones de AEM {#aem-customizations}

Es necesario identificar todas las personalizaciones del entorno de creación de AEM en la versión de origen de AEM. Una vez identificados, se recomienda almacenar cada personalización en el control de versiones o, como mínimo, en una copia de seguridad como parte de un paquete de contenido. Todas las personalizaciones deben implementarse y validarse en un entorno de control de calidad o ensayo que ejecute la versión de destino de AEM antes de una actualización de producción.

### Superposiciones en general {#overlays-in-general}

Es una práctica habitual ampliar AEM funcionalidad predeterminada superponiendo nodos y/o archivos bajo /libs con nodos adicionales bajo /apps. Estas superposiciones deben rastrearse en el control de versiones y probarse con la versión de destino de AEM. Si se superpone un archivo (ya sea JS, JSP, HTL), se recomienda dejar un comentario sobre qué funcionalidad se ha aumentado para facilitar las pruebas de regresión en la versión de AEM de destino. Puede encontrar más información sobre las superposiciones en general [aquí](/help/sites-developing/overlays.md). A continuación se encuentran las instrucciones para superposiciones de AEM específicas.

### Actualización de Forms de búsqueda personalizada {#upgrading-custom-search-forms}

Las facetas de búsqueda personalizadas requieren algunos ajustes manuales después de la actualización para funcionar correctamente. Para obtener más información, consulte [Actualización de Forms de búsqueda personalizada](/help/sites-deploying/upgrading-custom-search-forms.md).

### Personalizaciones de la interfaz de usuario de Assets {#assets-ui-customizations}

>[!NOTE]
>
>Este procedimiento solo es necesario para las actualizaciones de versiones anteriores a la AEM 6.2.

Las instancias que tienen implementaciones personalizadas de Assets deben estar preparadas para la actualización. Esto es necesario para garantizar que todo el contenido personalizado sea compatible con la nueva estructura de nodos 6.4.

Puede preparar las personalizaciones de la interfaz de usuario de Assets haciendo lo siguiente:

1. En la instancia que debe actualizarse, abra el CRXDE Lite en *https://server:port/crx/de/index.jsp*

1. Vaya al siguiente nodo:

   * `/apps/dam/content`

1. Cambie el nombre del nodo de contenido a **content_backup**. Para ello, haga clic con el botón derecho en el panel del explorador en el lado izquierdo de la ventana y elija **Cambiar nombre**.

1. Una vez que se haya cambiado el nombre del nodo, cree un nuevo nodo denominado content en `/apps/dam` denominado **content** y establezca su tipo de nodo en **sling:Folder**.

1. Mueva todos los nodos secundarios de **content_backup** al nodo de contenido recién creado. Para ello, haga clic con el botón derecho en cada nodo secundario del panel del explorador y seleccione **Mover**.

1. Elimine el nodo **content_backup**.

1. Los nodos actualizados debajo de `/apps/dam` con el tipo de nodo correcto de `sling:Folder` idealmente deben guardarse en el control de versiones e implementarse con el código base o con una copia de seguridad mínima como paquete de contenido.

### Generación de ID de recursos para recursos existentes {#generating-asset-ids-for-existing-assets}

Para generar ID de recursos para recursos existentes, actualice los recursos cuando actualice la instancia de AEM para ejecutar AEM 6.5. Esto es necesario para habilitar la función [Assets Insights](/help/assets/asset-insights.md). Para obtener más información, consulte [Agregar código incrustado](/help/assets/use-page-tracker.md#add-embed-code).

Para actualizar recursos, configure el paquete Asociar ID de recursos en la consola JMX. Dependiendo del número de recursos en el repositorio, `migrateAllAssets` puede tardar mucho tiempo. Nuestras pruebas internas estiman aproximadamente una hora para 125 mil activos en TarMK.

![1487758945977](assets/1487758945977.png)

Si necesita ID de recursos para un subconjunto de todos los recursos, utilice la API `migrateAssetsAtPath` .

Para cualquier otro propósito, utilice la API `migrateAllAssets()`.

### Personalizaciones de scripts de InDesign {#indesign-script-customizations}

Adobe recomienda colocar scripts personalizados en la ubicación `/apps/settings/dam/indesign/scripts` . Puede encontrar más información sobre las personalizaciones de los scripts de InDesign [aquí](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Recuperación de las configuraciones de ContextHub {#recovering-contexthub-configurations}

Las configuraciones de ContextHub se ven afectadas por una actualización. Las instrucciones sobre cómo recuperar las configuraciones existentes de ContextHub se encuentran [aquí](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### Personalizaciones de flujo de trabajo {#workflow-customizations}

Es una práctica habitual actualizar los flujos de trabajo de modificación para añadir o eliminar funciones que no son necesarias. Un flujo de trabajo común personalizado es el flujo de trabajo [!UICONTROL DAM Update Asset]. Todos los flujos de trabajo necesarios para una implementación personalizada deben realizarse copias de seguridad y almacenarse en el control de versiones, ya que se pueden sobrescribir durante una actualización.

### Plantillas editables {#editable-templates}

>[!NOTE]
>
>Este procedimiento solo es necesario para las actualizaciones de sitios que utilizan plantillas editables de AEM 6.2

La estructura de las plantillas editables cambió entre AEM 6.2 y 6.3. Si actualiza desde 6.2 o versiones anteriores y el contenido del sitio se crea con plantillas editables, deberá utilizar la [Herramienta de limpieza de nodos interactivos](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). La herramienta está diseñada para ejecutar **después** una actualización para limpiar el contenido. Tendrá que ejecutarse tanto en el nivel de Author como en el de Publish.

### Cambios en la implementación de CUG {#cug-implementation-changes}

La implementación de Grupos de usuarios cerrados ha cambiado significativamente para abordar las limitaciones de rendimiento y escalabilidad en versiones anteriores de AEM. La versión anterior de CUG quedó obsoleta en la versión 6.3 y la nueva implementación solo es compatible con la interfaz de usuario táctil. Si está actualizando desde la versión 6.2 o anterior, las instrucciones para migrar a la nueva implementación de CUG se encuentran [aquí](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## Procedimiento de prueba {#testing-procedure}

Se debe preparar un plan de prueba completo para probar las actualizaciones. La prueba de la base de código y la aplicación actualizados deberán realizarse primero en entornos más bajos. Los errores encontrados deben corregirse de forma iterativa hasta que la base de código sea estable, solo entonces se deben actualizar los entornos de nivel superior.

### Prueba del procedimiento de actualización {#testing-the-upgrade-procedure}

El procedimiento de actualización descrito aquí debe probarse en entornos de desarrollo y control de calidad tal como se documenta en su libro de ejecución personalizado (consulte [Planificación de la actualización](/help/sites-deploying/upgrade-planning.md)). El procedimiento de actualización debe repetirse hasta que todos los pasos estén documentados en el libro de ejecución de la actualización y el proceso de actualización sea fluido.

### Áreas de prueba de implementación {#implementation-test-areas-}

A continuación, se muestran áreas críticas de cualquier implementación de AEM que debería incluirse en el plan de prueba una vez que el entorno se haya actualizado y se haya implementado la base de código actualizada.

<table>
 <tbody>
  <tr>
   <td><strong>Área de prueba funcional</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Sitios publicados</td>
   <td>Prueba de la implementación de AEM y el código asociado en el nivel de publicación<br /> a través de Dispatcher. Debe incluir criterios para las actualizaciones de página y la invalidación de caché <br />.</td>
  </tr>
  <tr>
   <td>Creación  </td>
   <td>Prueba de la implementación de AEM y el código asociado en el nivel Autor. Debe incluir la creación de páginas, componentes y cuadros de diálogo.</td>
  </tr>
  <tr>
   <td>Integraciones con soluciones de Marketing Cloud</td>
   <td>Validación de integraciones con productos como Analytics, DTM y Target.</td>
  </tr>
  <tr>
   <td>Integraciones con sistemas de terceros</td>
   <td>Las integraciones de terceros deben validarse en los niveles Author y Publish .</td>
  </tr>
  <tr>
   <td>Autenticación, seguridad y permisos</td>
   <td>Cualquier mecanismo de autenticación como LDAP/SAML debe validarse.<br /> Los permisos y grupos deben probarse tanto en Autor como en <br /> Publicadores.</td>
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

### Plan y resultados de prueba de documento {#document-test-plan-and-results}

Se debe crear un plan de prueba que cubra las áreas de prueba de implementación anteriores. En muchos casos, tendrá sentido separar el plan de prueba por listas de tareas Autor y Publicación . Este plan de prueba debe ejecutarse en los entornos Dev, QA y Stage antes de actualizar los entornos de producción. Los resultados de las pruebas y las métricas de rendimiento deben capturarse en entornos más bajos para proporcionar comparación al actualizar entornos de fase y producción.
