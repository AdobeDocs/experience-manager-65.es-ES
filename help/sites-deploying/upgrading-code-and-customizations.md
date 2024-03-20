---
title: Actualizar código y personalizaciones
description: AEM Obtenga más información sobre la actualización de código y personalizaciones en.
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2138'
ht-degree: 0%

---

# Actualizar código y personalizaciones{#upgrading-code-and-customizations}

Al planificar una actualización, se deben investigar y abordar las siguientes áreas de una implementación.

* [Actualizar la base de código](#upgrade-code-base)
* [Alinear con la estructura de repositorio de 6.5](#align-repository-structure)
* [AEM Personalizaciones de](#aem-customizations)
* [Procedimiento de prueba](#testing-procedure)

## Información general {#overview}

1. **Detector de patrones** : ejecute Pattern Detector como se describe en la planificación de la actualización y se describe en detalle en [esta página](/help/sites-deploying/pattern-detector.md). AEM Recibirá un informe de detector de patrones que contiene más detalles sobre las áreas que deben abordarse, además de las API o los paquetes no disponibles en la versión de Target de. El informe Detección de patrones le proporciona una indicación de cualquier incompatibilidad en el código. Si no existe, su implementación ya es compatible con la versión 6.5. Puede optar por realizar un nuevo desarrollo para utilizar la funcionalidad 6.5, pero no lo necesita solo para mantener la compatibilidad. Si se notifican incompatibilidades, puede elegir ejecutar en modo de compatibilidad y retrasar el desarrollo para nuevas funciones o compatibilidad de la versión 6.5. O bien, puede decidir realizar el desarrollo después de la actualización y pasar al paso 2. Consulte [AEM Compatibilidad con versiones anteriores en 6.5](/help/sites-deploying/backward-compatibility.md) para obtener más información.

1. **Desarrollar la base de código para 6.5 **: cree una rama o repositorio dedicado para la base de código de la versión de Target. Utilice la información de Compatibilidad previa a la actualización para planificar las áreas de código que desea actualizar.
1. **Compile con 6.5 Uber jar **- Actualice los POM base de código para que apunten a 6.5 Uber jar y compile el código con él.
1. **AEM Actualizar personalizaciones de** AEM * - * Todas las personalizaciones o extensiones para la deben actualizarse/validarse para que funcionen en 6.5 y agregarse a la base de código de 6.5. Incluye Forms de búsqueda de interfaz de usuario, personalizaciones de recursos, cualquier cosa que use /mnt/overlay

1. **Implementar en el entorno de 6.5** AEM : una instancia limpia de 6.5 (autor + publicación) debe plantearse en un entorno de desarrollo/control de calidad. Se debe implementar una base de código actualizada y una muestra representativa de contenido (de producción actual).
1. **Validación de control de calidad y corrección de errores** : el control de calidad debe validar la aplicación en las instancias de autor y publicación de 6.5. Los errores encontrados deben corregirse y confirmarse en la base de código de 6.5. Repita Dev-Cycle según sea necesario hasta que se corrijan todos los errores.

AEM Antes de continuar con la actualización, debe tener una base de código de aplicación estable que se haya probado exhaustivamente en relación con la versión de destino de la aplicación de destino de la que se ha realizado la actualización de la aplicación de la versión de la aplicación de destino. Según las observaciones realizadas en las pruebas, podría haber formas de optimizar el código personalizado. Por ejemplo, puede incluir la refactorización del código para evitar atravesar el repositorio, la indexación personalizada para optimizar la búsqueda o el uso de nodos sin ordenar en JCR, entre otros.

AEM Además de actualizar de forma opcional el código base y las personalizaciones para que funcionen con la nueva versión de la aplicación, la versión 6.5 también ayuda a administrar las personalizaciones de forma más eficaz con la función Compatibilidad con versiones anteriores, tal como se describe en [esta página](/help/sites-deploying/backward-compatibility.md).

Como se ha mencionado anteriormente y se muestra en el diagrama siguiente, la ejecución del [Detector de patrones](/help/sites-deploying/pattern-detector.md) en el primer paso puede ayudarle a evaluar la complejidad general de la actualización. AEM También puede ayudarle a decidir si desea ejecutar en modo de compatibilidad o actualizar las personalizaciones para utilizar todas las nuevas características de la versión 6.5 de la versión de. Consulte la [AEM Compatibilidad con versiones anteriores en 6.5](/help/sites-deploying/backward-compatibility.md) para obtener más información.
[![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Actualizar la base de código {#upgrade-code-base}

### Crear una rama dedicada para el código de 6.5 en el control de versiones {#create-a-dedicated-branch-for-6.5-code-in-version-control}

AEM Todo el código y las configuraciones necesarios para la implementación de la se deben administrar mediante algún tipo de control de versiones. AEM Se debe crear una rama dedicada en el control de versiones para administrar los cambios necesarios para el código base en la versión de destino de la versión de la aplicación de código de. AEM En esta rama se gestionan las pruebas iterativas del código base respecto a la versión de destino de la corrección de errores y las correcciones de errores subsiguientes.

### AEM Actualización de la versión de Jar de Uber de {#update-the-aem-uber-jar-version}

AEM AEM El JAR de Uber incluye todas las API de como una sola dependencia en el proyecto de Maven `pom.xml`. AEM Siempre es una práctica recomendada incluir Uber Jar como una sola dependencia en lugar de incluir dependencias de API de individuales. AEM Al actualizar el código base, cambie la versión de Uber Jar para que apunte a la versión de destino de la versión de la versión de la versión de la versión de la versión de la versión de la versión de la versión de la versión de la aplicación. AEM AEM Si su proyecto se desarrolló en una versión de antes de la existencia del Jar de Uber, elimine todas las dependencias de API individuales de la API de la. AEM Sustitúyalos por una sola inclusión de Uber Jar para la versión de destino de la versión de la versión de la versión de la versión de la aplicación de la versión de la versión de la aplicación de la versión de la aplicación. Recompile el código base con la nueva versión de Uber Jar. AEM Actualice las API o los métodos obsoletos para que sean compatibles con la versión de destino de la versión de la.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### Eliminación gradual del uso de la herramienta de resolución de recursos administrativos {#phase-out-use-of-administrative-resource-resolver}

El uso de una sesión administrativa mediante `SlingRepository.loginAdministrative()` y `ResourceResolverFactory.getAdministrativeResourceResolver()` AEM prevalecía en bases de código antes de la versión 6.0 de la. Estos métodos han quedado obsoletos por motivos de seguridad, ya que otorgan un nivel de acceso demasiado amplio. [En versiones futuras de Sling, estos métodos se eliminarán](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). Se recomienda encarecidamente refactorizar cualquier código para utilizar usuarios de servicio en su lugar. Más información sobre los Usuarios de servicio y [puede encontrar información sobre cómo eliminar las sesiones administrativas aquí](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### Consultas e índices de Oak {#queries-and-oak-indexes}

Cualquier uso de consultas en la base de código debe probarse a fondo como parte de la actualización de la base de código. AEM Para los clientes que actualizan desde Jackrabbit 2 (versiones de anteriores a 6.0), esta prueba es especialmente importante, ya que Oak no indexa contenido automáticamente y se deben crear índices personalizados. AEM Si se actualiza desde una versión de 6.x, las definiciones de índice de Oak listas para usar pueden haber cambiado y afectar a las consultas existentes.

Las siguientes herramientas están disponibles para analizar e inspeccionar el rendimiento de las consultas:

* [AEM Herramientas de índice](/help/sites-deploying/queries-and-indexing.md)

* [Herramientas de diagnóstico de operaciones: rendimiento de consultas](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### Creación de IU clásica {#classic-ui-authoring}

AEM La creación de IU clásica sigue estando disponible en la versión 6.5 de, pero está en desuso. Puede encontrar más información [aquí](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). AEM Si la aplicación se está ejecutando en el entorno de creación de la IU clásica, se recomienda actualizar a la versión 6.5 de la interfaz de usuario clásica y seguir usando la interfaz de usuario clásica. La migración a la IU táctil se puede planificar como un proyecto independiente para completarse en varios ciclos de desarrollo. AEM Para utilizar la IU clásica en 6.5, se deben confirmar varias configuraciones de OSGi en la base de código. Se pueden encontrar más detalles sobre cómo realizar la configuración [aquí](/help/sites-administering/enable-classic-ui.md).

## Alinear con la estructura de repositorio de 6.5 {#align-repository-structure}

Para facilitar las actualizaciones y garantizar que las configuraciones no se sobrescriban durante una actualización, el repositorio se reestructura en la versión 6.4 para separar el contenido de la configuración.

Por lo tanto, se deben mover varias configuraciones para que ya no residan en `/etc` como había ocurrido en el pasado. AEM Para revisar el conjunto completo de problemas de reestructuración de repositorios que deben revisarse y tenerse en cuenta en la actualización a la versión 6.4, véase el documento de trabajo de la Comisión sobre la reestructuración de los repositorios de las Naciones Unidas en el documento actualizado a la versión 6.40000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000000000000000000000 [AEM Reestructuración de repositorios en 6.4](/help/sites-deploying/repository-restructuring.md).

## AEM Personalizaciones de  {#aem-customizations}

AEM AEM Se deben identificar todas las personalizaciones del entorno de creación de la en la versión de origen de la aplicación Una vez identificadas, se recomienda almacenar cada personalización en el control de versiones o, como mínimo, hacer una copia de seguridad como parte de un paquete de contenido. AEM Todas las personalizaciones deben implementarse y validarse en un entorno de control de calidad o de ensayo que ejecute la versión de destino de las actualizaciones de la aplicación antes de una actualización de producción.

### Superposiciones en general {#overlays-in-general}

AEM Es una práctica común ampliar la funcionalidad de forma predeterminada superponiendo nodos o archivos en /libs con nodos adicionales en /apps. AEM Estas superposiciones deben rastrearse en el control de versiones y probarse con la versión de destino de la versión de la versión de la versión de la que se ha realizado el seguimiento Si un archivo (como JS, JSP, HTL) está superpuesto, Adobe AEM recomienda dejar un comentario sobre qué funcionalidad se aumentó para facilitar las pruebas de regresión en la versión de destino de la. Encontrará más información sobre las superposiciones en general [aquí](/help/sites-developing/overlays.md). AEM A continuación, se encuentran las instrucciones para superposiciones específicas de la.

### Actualización de Forms de búsqueda personalizada {#upgrading-custom-search-forms}

Las facetas de búsqueda personalizadas requieren algunos ajustes manuales después de la actualización para funcionar correctamente. Para obtener más información, consulte [Actualización de Forms de búsqueda personalizada](/help/sites-deploying/upgrading-custom-search-forms.md).

### Personalizaciones de IU de Assets {#assets-ui-customizations}

>[!NOTE]
>
>AEM Este procedimiento solo es necesario para las actualizaciones de versiones anteriores a la 6.2 de.

Las instancias que tienen implementaciones de recursos personalizadas deben estar preparadas para la actualización. Esta acción es necesaria para garantizar que todo el contenido personalizado sea compatible con la nueva estructura de nodos de 6.4.

Puede preparar las personalizaciones de la IU de Assets haciendo lo siguiente:

1. En la instancia que se está actualizando, abra el CRXDE Lite en *https://server:port/crx/de/index.jsp*

1. Vaya al siguiente nodo:

   * `/apps/dam/content`

1. Cambie el nombre del nodo de contenido a **content_backup** haciendo clic con el botón derecho en el panel del explorador, en el lado izquierdo de la ventana, y seleccionando **Cambiar nombre**.

1. Una vez que se haya cambiado el nombre del nodo, cree un nodo denominado content en `/apps/dam` nombrado **content** y establezca su tipo de nodo en **sling:Carpeta**.

1. Mover todos los nodos secundarios de **content_backup** al nodo de contenido recién creado haciendo clic con el botón derecho en cada nodo secundario del panel del explorador y seleccionando **Mover**.

1. Elimine el **content_backup** nodo.

1. Los nodos actualizados debajo de `/apps/dam` con el tipo de nodo correcto de `sling:Folder` Lo ideal es guardar en el control de versiones e implementarlo con el código base o, como mínimo, hacer una copia de seguridad como paquete de contenido.

### Generación de ID de recurso para recursos existentes {#generating-asset-ids-for-existing-assets}

AEM AEM Para generar los ID de recurso para los recursos existentes, actualice los recursos al actualizar la instancia de para que ejecute la versión 6.5. Este paso es necesario para habilitar el [Función Assets Insights](/help/assets/asset-insights.md). Para obtener más información, consulte [Añadir código incrustado](/help/assets/use-page-tracker.md#add-embed-code).

Para actualizar recursos, configure el paquete Associate Asset IDs en la consola JMX. Según el número de recursos del repositorio, `migrateAllAssets` puede llevar mucho tiempo. Las pruebas internas de Adobe estiman aproximadamente una hora para los activos 125000 en TarMK.

![1487758945977](assets/1487758945977.png)

Si necesita ID de recurso para un subconjunto de todos los recursos, utilice el `migrateAssetsAtPath` API.

Para todos los demás fines, utilice la variable `migrateAllAssets()` API.

### Personalizaciones de scripts de InDesign {#indesign-script-customizations}

El Adobe recomienda colocar los scripts personalizados en `/apps/settings/dam/indesign/scripts` ubicación. Puede encontrar más información sobre las personalizaciones de scripts de InDesign [aquí](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Recuperación de configuraciones de ContextHub {#recovering-contexthub-configurations}

Las configuraciones de ContextHub se ven afectadas por una actualización. Encontrará instrucciones sobre cómo recuperar las configuraciones de ContextHub existentes [aquí](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### Personalizaciones de flujo de trabajo {#workflow-customizations}

Es una práctica habitual editar flujos de trabajo predeterminados para añadir o quitar funciones innecesarias. Un flujo de trabajo personalizado común es [!UICONTROL Recurso de actualización DAM] flujo de trabajo. Se debe realizar una copia de seguridad de todos los flujos de trabajo necesarios para una implementación personalizada y almacenarlos en el sistema de control de versiones, ya que pueden sobrescribirse durante una actualización.

### Plantillas editables {#editable-templates}

>[!NOTE]
>
>AEM Este procedimiento solo es necesario para las actualizaciones de sitios que utilizan plantillas editables de la versión 6.2 de

AEM La estructura de las plantillas editables ha cambiado entre la versión 6.2 y la versión 6.3 de la. Si actualiza desde la versión 6.2 o anterior y el contenido del sitio se crea mediante plantillas editables, debe utilizar el complemento [Herramienta de limpieza de nodos adaptables](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). La herramienta está diseñada para ejecutarse **después** una actualización para limpiar el contenido. Ejecútelo tanto en el nivel de creación como en el de publicación.

### Cambios de implementación de CUG {#cug-implementation-changes}

AEM La implementación de Grupos de usuarios cerrados ha cambiado significativamente para hacer frente a las limitaciones de rendimiento y escalabilidad en versiones anteriores de los grupos de usuarios que no son de la lista de los más avanzados. La versión anterior de CUG estaba en desuso en la versión 6.3 y la nueva implementación solo es compatible con la IU táctil. Si actualiza desde la versión 6.2 o anterior, puede encontrar las instrucciones para migrar a la nueva implementación de CUG [aquí](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## Procedimiento de prueba {#testing-procedure}

Se debe preparar un plan de pruebas completo para probar las actualizaciones. La aplicación y la base de código actualizadas deben probarse primero en entornos más bajos. Los errores encontrados deben corregirse de forma iterativa hasta que la base de código sea estable, solo entonces deben actualizarse los entornos de nivel superior.

### Prueba del procedimiento de actualización {#testing-the-upgrade-procedure}

El procedimiento de actualización descrito aquí debe probarse en los entornos de desarrollo y control de calidad, tal como se documenta en el manual de ejecución personalizado (consulte [Planificación de la actualización](/help/sites-deploying/upgrade-planning.md)). El procedimiento de actualización debe repetirse hasta que todos los pasos estén documentados en el manual de ejecución de la actualización y el proceso de actualización sea fluido.

### Áreas de prueba de implementación  {#implementation-test-areas-}

AEM A continuación, se muestran áreas críticas de cualquier implementación de que deba incluirse en el plan de prueba una vez que se haya actualizado el entorno y se haya implementado la base de código actualizada.

<table>
 <tbody>
  <tr>
   <td><strong>Área de prueba funcional</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Sitios publicados</td>
   <td>AEM Prueba de la implementación de la y el código asociado en el nivel de publicación<br /> mediante Dispatcher. Debe incluir criterios para actualizaciones de página y<br /> invalidación de caché.</td>
  </tr>
  <tr>
   <td>Creación</td>
   <td>AEM Prueba de la implementación de la y el código asociado en el nivel de Author. Debe incluir la creación de páginas, componentes y cuadros de diálogo.</td>
  </tr>
  <tr>
   <td>Integraciones con soluciones de Experience Cloud</td>
   <td>Validación de integraciones con productos como Analytics, DTM y Target.</td>
  </tr>
  <tr>
   <td>Integraciones con sistemas de terceros</td>
   <td>Valide cualquier integración de terceros en los niveles de creación y publicación.</td>
  </tr>
  <tr>
   <td>Autenticación, seguridad y permisos</td>
   <td>Deben validarse todos los mecanismos de autenticación como LDAP/SAML.<br /> Los permisos y grupos deben probarse en Autor y Publish<br /> niveles.</td>
  </tr>
  <tr>
   <td>Consultas</td>
   <td>Los índices y consultas personalizados deben probarse junto con el rendimiento de las consultas.</td>
  </tr>
  <tr>
   <td>Personalizaciones de IU</td>
   <td>AEM Extensiones o personalizaciones de la IU de la en el entorno de creación.</td>
  </tr>
  <tr>
   <td>Flujos de trabajo</td>
   <td>Flujos de trabajo y funcionalidad personalizados o listos para usar.</td>
  </tr>
  <tr>
   <td>Pruebas de rendimiento</td>
   <td>Las pruebas de carga deben realizarse en los niveles Author y Publish que simulan escenarios reales.</td>
  </tr>
 </tbody>
</table>

### Documentar el plan y los resultados de prueba {#document-test-plan-and-results}

Debe crearse un plan de pruebas que cubra las áreas de prueba de implementación mencionadas anteriormente. A menudo, tiene sentido separar el plan de prueba por las listas de tareas Autor y Publicar. Este plan de prueba debe ejecutarse en los entornos de desarrollo, control de calidad y ensayo antes de actualizar los entornos de producción. Los resultados de las pruebas y las métricas de rendimiento deben capturarse en entornos inferiores para proporcionar una comparación al actualizar los entornos de ensayo y producción.
