---
title: Actualización del código y las personalizaciones
seo-title: Actualización del código y las personalizaciones
description: Obtenga más información sobre la actualización del código personalizado en AEM.
seo-description: Obtenga más información sobre la actualización del código personalizado en AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: 5035c9630b5e861f4386e1b5ab4f4ae7a8d26149

---


# Actualización del código y las personalizaciones{#upgrading-code-and-customizations}

Cuando se planifica una actualización, es necesario investigar y abordar las siguientes áreas de una implementación.

* [Actualizar la base de código](#upgrade-code-base)
* [Alinear con la estructura de repositorio 6.5](#align-repository-structure)
* [Personalizaciones de AEM](#aem-customizations)
* [Procedimiento de prueba](#testing-procedure)

## Información general {#overview}

1. **Detector** de patrones: ejecute el detector de patrones tal como se describe en la planificación de actualizaciones y se describe en detalle en [esta página](/help/sites-deploying/pattern-detector.md) para obtener un informe de detector de patrones que contenga más detalles sobre las áreas que deben abordarse además de las API y los paquetes no disponibles en la versión de Target de AEM. El informe Detección de patrones debe proporcionarle una indicación de cualquier incompatibilidad en el código. Si no hay ninguna, entonces la implementación ya es compatible con la versión 6.5, aún puede elegir realizar un nuevo desarrollo para utilizar la funcionalidad 6.5, pero no la necesita sólo para mantener la compatibilidad. Si hay incompatibilidades notificadas, puede elegir entre: a) Ejecutar en modo de compatibilidad y postergar el desarrollo para nuevas características de 6.5 o compatibilidad, b) Decidir realizar el desarrollo después de la actualización y pasar al paso 2. Consulte Compatibilidad [con versiones anteriores en AEM 6.5](/help/sites-deploying/backward-compatibility.md) para obtener más información.

1. **Desarrollar base de código para 6.5 **- Crear una rama o repositorio dedicado para la base de código para la versión de Target. Utilice la información de Compatibilidad previa a la actualización para planificar las áreas de código que se van a actualizar.
1. **Compile con 6.5 Uber jar **- Actualice los POM base de código para que señalen a 6.5 uber jar y compile código en contra de esto.
1. **Actualizar personalizaciones** de AEM*: *Cualquier personalización o extensión de AEM debe actualizarse o validarse para que funcione en la versión 6.5 y agregarse a la base de código 6.5. Incluye formularios de búsqueda de interfaz de usuario, personalización de recursos, cualquier cosa que utilice /mnt/overlay

1. **Implementar en entorno** 6.5: una instancia limpia de AEM 6.5 (Autor + Publicar) debe estar en un entorno Dev/QA. Se debe implementar una base de código actualizada y una muestra representativa de contenido (de la producción actual).
1. **Validación de control de calidad y corrección** de errores: el control de calidad debe validar la aplicación en instancias de autor y publicación de 6.5. Los errores encontrados deben corregirse y confirmarse en la base de código 6.5. Repita Dev-Cycle según sea necesario hasta que se corrijan todos los errores.

Antes de proceder con una actualización, debe disponer de una base de código de aplicación estable que se haya probado a fondo con la versión de destino de AEM. Según las observaciones realizadas en las pruebas, podría haber maneras de optimizar el código personalizado. Esto podría incluir refactorizar el código para evitar atravesar el repositorio, indexar a medida para optimizar la búsqueda o usar nodos no ordenados en JCR, entre otros.

Además de la opción de actualizar la base de código y las personalizaciones para trabajar con la nueva versión de AEM, 6.5 también ayuda a administrar sus personalizaciones de forma más eficaz con la función Compatibilidad con versiones anteriores, tal como se describe en [esta página](/help/sites-deploying/backward-compatibility.md).

Como se ha mencionado anteriormente y se muestra en el diagrama siguiente, la ejecución del [detector](/help/sites-deploying/pattern-detector.md) de patrones en el primer paso le ayudará a evaluar la complejidad general de la actualización y si desea ejecutar en modo de compatibilidad o actualizar sus personalizaciones para utilizar todas las nuevas funciones de AEM 6.5. Para obtener más información, consulte la página Compatibilidad con [versiones anteriores de AEM 6.5](/help/sites-deploying/backward-compatibility.md) .
[ ![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Actualizar la base de código {#upgrade-code-base}

### Crear una rama dedicada para el código 6.5 en el control de versiones {#create-a-dedicated-branch-for-6.5-code-in-version-control}

Todo el código y las configuraciones necesarias para la implementación de AEM se deben administrar con alguna forma de control de versiones. Se debe crear una rama dedicada en el control de versiones para administrar los cambios necesarios para la base de código en la versión de destino de AEM. En esta ramificación se gestionarán pruebas iterativas de la base de código con respecto a la versión de destino de AEM y posteriores correcciones de errores.

### Actualización de la versión de AEM Uber Jar {#update-the-aem-uber-jar-version}

El tarro de AEM Uber incluye todas las API de AEM como una única dependencia en el proyecto de Maven `pom.xml`. Siempre es recomendable incluir Uber Jar como una dependencia única en lugar de incluir dependencias de API de AEM individuales. Al actualizar la base de código, se debe cambiar la versión de Uber Jar para que señale a la versión de destino de AEM. Si el proyecto se desarrolló en una versión de AEM anterior a la existencia de Uber Jar, todas las dependencias individuales de la API de AEM deberían eliminarse y reemplazarse por una sola inclusión de Uber Jar para la versión de destino de AEM. La base de código debe recompilarse con la nueva versión de Uber Jar. Cualquier API o método obsoleto debe actualizarse para que sea compatible con la versión de destino de AEM.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### Eliminación del uso de Resolver recursos administrativos {#phase-out-use-of-administrative-resource-resolver}

El uso de una sesión administrativa a través de `SlingRepository.loginAdministrative()` y `ResourceResolverFactory.getAdministrativeResourceResolver()` fue bastante frecuente en las bases de códigos anteriores a AEM 6.0. Estos métodos han quedado obsoletos por motivos de seguridad, ya que ofrecen un nivel de acceso demasiado amplio. [En futuras versiones de Sling, estos métodos se eliminarán](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). Se recomienda redimensionar cualquier código para utilizar usuarios de servicios. Encontrará más información sobre los usuarios de servicios y [cómo eliminar gradualmente las sesiones administrativas aquí](/help/sites-administering/security-service-users.md#how to delete out admin session).

### Consultas e índices Oak {#queries-and-oak-indexes}

Cualquier uso de consultas en la base de código debe probarse a fondo como parte de la actualización de la base de código. Para los clientes que se actualizan desde Jackrabbit 2 (versiones de AEM anteriores a 6.0) esto es especialmente importante, ya que Oak no indexa el contenido automáticamente y es posible que sea necesario crear índices personalizados. Si se actualiza desde una versión de AEM 6.x, las definiciones de índice Oak predeterminadas pueden haber cambiado y podrían afectar a las consultas existentes.

Existen varias herramientas para analizar e inspeccionar el rendimiento de las consultas:

* [Herramientas de índice de AEM](/help/sites-deploying/queries-and-indexing.md)

* [Herramientas de diagnóstico de operaciones: rendimiento de la consulta](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

* [Utils](https://oakutils.appspot.com/)de roble. Se trata de una herramienta de código abierto que Adobe no mantiene.

### Classic UI Authoring {#classic-ui-authoring}

La creación de IU clásica aún está disponible en AEM 6.5, pero ya no se utiliza. Puede encontrar más información [aquí](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). Si la aplicación se está ejecutando en el entorno de creación de la IU clásica, se recomienda actualizar a AEM 6.5 y seguir usando la IU clásica. La migración a la IU táctil se puede planificar como un proyecto independiente que se completará en varios ciclos de desarrollo. Para utilizar la IU clásica en AEM 6.5, es necesario que varias configuraciones de OSGi se confirmen en la base de código. Puede encontrar más detalles sobre cómo configurar esto [aquí](/help/sites-administering/enable-classic-ui.md).

## Alinear con la estructura de repositorio 6.5 {#align-repository-structure}

Para facilitar las actualizaciones y garantizar que las configuraciones no se sobrescriban durante una actualización, el repositorio se reestructura en 6.4 para separar el contenido de la configuración.

Por lo tanto, se debe mover una serie de configuraciones para que ya no residan en `/etc` el país, como en el pasado. Para revisar el conjunto completo de problemas de reestructuración de repositorios que deben revisarse y adaptarse en la actualización a AEM 6.4, consulte Reestructuración [de repositorios en AEM 6.4](/help/sites-deploying/repository-restructuring.md).

## Personalizaciones de AEM {#aem-customizations}

Es necesario identificar todas las personalizaciones del entorno de creación de AEM en la versión de origen de AEM. Una vez identificadas, se recomienda almacenar cada personalización en el control de versiones o, como mínimo, en una copia de seguridad como parte de un paquete de contenido. Todas las personalizaciones deben implementarse y validarse en un entorno de control de calidad o ensayo que ejecute la versión de destino de AEM antes de una actualización de producción.

### Superposiciones en general {#overlays-in-general}

Es una práctica habitual extender AEM fuera de la funcionalidad del equipo superponiendo nodos o archivos en /libs con nodos adicionales en /apps. Estas superposiciones deben rastrearse en el control de versiones y probarse con la versión de destino de AEM. Si un archivo (ya sea JS, JSP, HTL) está superpuesto, se recomienda dejar un comentario sobre qué funcionalidad se ha aumentado para facilitar las pruebas de regresión en la versión de destino de AEM. Puede encontrar más información sobre las superposiciones en general [aquí](/help/sites-developing/overlays.md). A continuación encontrará instrucciones para superposiciones específicas de AEM.

### Actualización de formularios de búsqueda personalizados {#upgrading-custom-search-forms}

Las facetas de búsqueda personalizadas requieren algunos ajustes manuales después de la actualización para funcionar correctamente. Para obtener más información, consulte [Actualización de formularios](/help/sites-deploying/upgrading-custom-search-forms.md)de búsqueda personalizados.

### Personalizaciones de la interfaz de usuario de Recursos {#assets-ui-customizations}

>[!NOTE]
>
>Este procedimiento solo es necesario para las actualizaciones de versiones anteriores a AEM 6.2.

Las instancias que tienen implementaciones personalizadas de Recursos deben estar preparadas para la actualización. Esto es necesario para garantizar que todo el contenido personalizado sea compatible con la nueva estructura de nodos 6.4.

Puede preparar las personalizaciones de la interfaz de usuario de Recursos de la siguiente manera:

1. En la instancia que debe actualizarse, abra CRXDE Lite en *https://server:port/crx/de/index.jsp*

1. Vaya al nodo siguiente:

   * `/apps/dam/content`

1. Cambie el nombre del nodo de contenido a **content_backup**. Para ello, haga clic con el botón derecho en el panel del explorador en el lado izquierdo de la ventana y seleccione **Cambiar nombre**.

1. Una vez que se haya cambiado el nombre del nodo, cree un nuevo nodo denominado content en `/apps/dam` denominado **content** y defina su tipo de nodo en **sling:Folder**.

1. Mueva todos los nodos secundarios de **content_backup** al nodo de contenido recién creado. Para ello, haga clic con el botón derecho en cada nodo secundario del panel del explorador y seleccione **Mover**.

1. Elimine el nodo **content_backup** .

1. Los nodos actualizados debajo `/apps/dam` del tipo de nodo correcto de `sling:Folder` deberían guardarse en control de versiones e implementarse con la base de código o, como mínimo, con una copia de seguridad como paquete de contenido.

### Generación de ID de recursos para recursos existentes {#generating-asset-ids-for-existing-assets}

Para generar ID de recursos para recursos existentes, actualice los recursos al actualizar la instancia de AEM para ejecutar AEM 6.5. Esto es necesario para habilitar la función [de](/help/assets/touch-ui-asset-insights.md)perspectivas de recursos. Para obtener más información, consulte [Agregar código](/help/assets/touch-ui-using-page-tracker.md#add-embed-code)incrustado.

Para actualizar recursos, configure el paquete de ID de recursos asociados en la consola JMX. Según el número de recursos del repositorio, `migrateAllAssets` puede tardar mucho tiempo. Nuestras pruebas internas estiman aproximadamente una hora para 125 mil activos en TarMK.

![1487758945977](assets/1487758945977.png)

Si necesita ID de recursos para un subconjunto de todos los recursos, utilice la `migrateAssetsAtPath` API.

Para todos los demás fines, utilice la `migrateAllAssets()` API.

### Personalizaciones de secuencias de comandos de InDesign {#indesign-script-customizations}

Adobe recomienda colocar las secuencias de comandos personalizadas en la `/apps/settings/dam/indesign/scripts` ubicación. Encontrará más información sobre las personalizaciones de InDesign Script [aquí](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Recuperación de configuraciones de ContextHub {#recovering-contexthub-configurations}

Las configuraciones de ContextHub se realizan mediante una actualización. Encontrará instrucciones sobre cómo recuperar las configuraciones existentes de ContextHub [aquí](/help/sites-administering/contexthub-config.md#recupera configuraciones de contexto después de la actualización).

### Personalizaciones del flujo de trabajo {#workflow-customizations}

Es una práctica común actualizar los flujos de trabajo de modificación inmediata para agregar o eliminar funciones no necesarias. Un flujo de trabajo común personalizado es el flujo de trabajo de recursos de actualización de DAM. Todos los flujos de trabajo necesarios para una implementación personalizada deben respaldarse y almacenarse en el control de versiones, ya que se pueden sobrescribir durante una actualización.

### Plantillas editables {#editable-templates}

>[!NOTE]
>
>Este procedimiento solo es necesario para las actualizaciones de sitios mediante plantillas editables de AEM 6.2

La estructura de las plantillas editables ha cambiado entre AEM 6.2 y 6.3. Si está actualizando desde la versión 6.2 o anterior y si el contenido del sitio se crea con plantillas editables, deberá utilizar la herramienta [de limpieza de nodos](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration)interactivos. La herramienta está pensada para ejecutarse **después** de una actualización para limpiar el contenido. Tendrá que ejecutarse tanto en los niveles de autor como de publicación.

### Cambios en la implementación de CUG {#cug-implementation-changes}

La implementación de Grupos cerrados de usuarios ha cambiado significativamente para abordar las limitaciones de rendimiento y escalabilidad en versiones anteriores de AEM. La versión anterior de CUG quedó obsoleta en 6.3 y la nueva implementación solo se admite en la IU táctil. Si está actualizando desde 6.2 o anterior, [aquí](/help/sites-administering/closed-user-groups.md#upgradetoaem63)encontrará instrucciones para migrar a la nueva implementación de CUG.

## Procedimiento de prueba {#testing-procedure}

Debe prepararse un plan de pruebas completo para realizar pruebas de actualización. La prueba de la base de código y la aplicación actualizadas deberá realizarse primero en entornos más bajos. Los errores encontrados deben corregirse de forma iterativa hasta que la base de código sea estable, solo entonces se deben actualizar los entornos de nivel superior.

### Prueba del procedimiento de actualización {#testing-the-upgrade-procedure}

El procedimiento de actualización descrito aquí debe probarse en los entornos Dev y QA tal como se documenta en el libro de ejecución personalizado (consulte [Planificación de la actualización](/help/sites-deploying/upgrade-planning.md)). El procedimiento de actualización debe repetirse hasta que todos los pasos se documenten en el libro de ejecución de la actualización y el proceso de actualización sea fluido.

### Áreas de prueba de implementación {#implementation-test-areas-}

A continuación se indican las áreas críticas de cualquier implementación de AEM que debería cubrir su plan de prueba una vez que se haya actualizado el entorno y se haya implementado la base de código actualizada.

<table>
 <tbody>
  <tr>
   <td><strong>Área de prueba funcional</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Sitios publicados</td>
   <td>Prueba de la implementación de AEM y del código asociado en el nivel<br /> de publicación mediante el despachante. Debe incluir criterios para las actualizaciones de página y la invalidación de la caché<br /> .</td>
  </tr>
  <tr>
   <td>Creación  </td>
   <td>Prueba de la implementación de AEM y del código asociado en el nivel Autor. Debe incluir la creación de páginas, componentes y cuadros de diálogo.</td>
  </tr>
  <tr>
   <td>Integraciones con soluciones de Marketing Cloud</td>
   <td>Validación de integraciones con productos como Analytics, DTM y Target.</td>
  </tr>
  <tr>
   <td>Integraciones con sistemas de terceros</td>
   <td>Todas las integraciones de terceros deben validarse en los niveles Autor y Publicación.</td>
  </tr>
  <tr>
   <td>Autenticación, seguridad y permisos</td>
   <td>Se deben validar todos los mecanismos de autenticación como LDAP/SAML.<br /> Los permisos y los grupos deben probarse en los niveles de autor y publicación<br /> .</td>
  </tr>
  <tr>
   <td>Consultas</td>
   <td>Los índices personalizados y las consultas deben probarse junto con el rendimiento de la consulta.</td>
  </tr>
  <tr>
   <td>Personalizaciones de la interfaz de usuario</td>
   <td>Cualquier extensión o personalización de la interfaz de usuario de AEM en el entorno de creación.</td>
  </tr>
  <tr>
   <td>Flujos de trabajo</td>
   <td>Flujos de trabajo y funcionalidades personalizados y/o listos para usar.</td>
  </tr>
  <tr>
   <td>Prueba de rendimiento</td>
   <td>Las pruebas de carga deben realizarse en los niveles Autor y Publicación que simulan escenarios reales.</td>
  </tr>
 </tbody>
</table>

### Plan y resultados de la prueba del documento {#document-test-plan-and-results}

Debe crearse un plan de prueba que abarque las áreas de prueba de implementación mencionadas. En muchos casos, tiene sentido separar el plan de prueba por listas de tareas Autor y Publicar. Este plan de prueba debe ejecutarse en entornos Dev, QA y Stage antes de actualizar los entornos de producción. Los resultados de las pruebas y las métricas de rendimiento deben capturarse en entornos más bajos para proporcionar una comparación al actualizar entornos de fase y producción.
