---
title: Notas de la versión de Service Pack de AEM 6.5
description: Notas de versión específicas de Service Pack 4 de Adobe Experience Manager 6.5.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cc72581f0de6f47cd1d7e207f228e64ba7c9e842

---


# Notas de la versión de Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Información de la versión {#release-information}

| Productos | **Adobe Experience Manager 6.5** |
|---|---|
| Versión | 6.5.4.0 |
| Tipo | Versión de Service Pack |
| Fecha | 05 de marzo de 2020 |
| Descargar URL | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0), distribución [de software (Beta)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.4.zip) |

## Novedades de Adobe Experience Manager 6.5.4.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.4.0 es una actualización importante que incluye nuevas funciones, mejoras y rendimiento clave solicitados por el cliente, estabilidad y mejoras de seguridad, publicadas tras la disponibilidad general de la versión 6.5 en **abril de 2019**. Se puede instalar sobre Adobe Experience Manager (AEM) 6.5.

Algunas de las funciones y mejoras clave introducidas en AEM 6.5.4.0 son:

* Recursos AEM ahora se configura con Brand Portal a través de la consola de Adobe I/O.

* Ya hay disponible un nuevo paso [Generar salida](../forms/using/aem-forms-workflow-step-reference.md) imprimible para los flujos de trabajo de AEM Forms.

* [Compatibilidad](../forms/using/resize-using-layout-mode.md) con varias columnas para el modo de presentación de formularios adaptables y comunicaciones interactivas.

* Compatibilidad con texto [](../forms/using/designing-form-template.md) enriquecido en formularios HTML5.

* [Mejoras](new-features-latest-service-pack.md#accessibility-enhancements) de accesibilidad en Experience Manager Assets.

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.10.8.

Para obtener una lista completa de las funciones, los aspectos más destacados y las funciones clave introducidas en los Service Pack anteriores de AEM 6.5, consulte [Novedades de Adobe Experience Manager 6.5 Service Pack 4](new-features-latest-service-pack.md).

### Sites {#sites-fixes}

* Cuando una dirección URL de una página de AEM Sites contiene dos puntos (: ) o símbolo de porcentaje (%), el explorador subyacente deja de responder y los ciclos de CPU muestran un pico (NPR-32369, NPR-31918).

* Cuando se abre una página de AEM Sites para editarla y se copia un componente, la acción de pegado permanece indisponible para algunos marcadores de posición (NPR-32317).

* Cuando se abre el asistente Administrar publicación, un fragmento de experiencia vinculado a un componente principal no se muestra en las listas de referencias publicadas (NPR-32233).

* La descripción general de la Live Copy en la IU táctil tarda mucho más que la IU clásica en procesarse (NPR-32149).

* Cuando la hora del servidor y la hora del equipo están en diferentes zonas horarias, la hora de publicación programada muestra la hora del servidor en la IU táctil, mientras que en la IU clásica se muestra la hora del equipo (NPR-32077).

* AEM Sites no puede abrir una página con un sufijo en la URL (NPR-32072).

* Cuando un usuario edita un fragmento de contenido, se restaura una variación eliminada del fragmento de contenido (NPR-32062).

* Los usuarios pueden guardar un fragmento de contenido sin proporcionar información en los campos requeridos (NPR-31988).

* kernel.js y ui.js no se cumplimentan ni se almacenan en caché. Esto lleva a tiempo adicional en el procesamiento de páginas (NPR-31891).

* Cuando PageEventAuditListener está habilitado, la longitud de la cola de confirmación aumenta. Afecta al rendimiento de muchas operaciones, como la publicación masiva, la navegación y el movimiento masivo de recursos (NPR-31890).

* Cuando se arrastran fragmentos de experiencia, se observa un tiempo de respuesta alto (NPR-31878).

* Cuando selecciona la opción Arrastrar componente aquí en el marcador de posición de una cuadrícula adaptable, se envía una solicitud GET y la solicitud da como resultado un error HTTP 403 (NPR-31845).

* Al mover el contenido dentro de la misma carpeta, se desactiva la opción de mover la página (NPR-31840).

* En el modo de estructura de plantillas editables, la lista de componentes permitidos del contenedor de diseños muestra resultados incorrectos. En el contenedor de diseño (NPR-31816) solo se muestran los componentes con cuadro de diálogo de diseño.

* Cuando una página tiene permisos de solo lectura para un usuario, la opción Abrir propiedades está visible en sites.html pero no en editor.html (NPR-31770).

* Cuando un usuario hace clic en el botón Crear, la opción de página no está disponible (NPR-31756).

* No se puede sincronizar la campaña en la campaña de Adobe que contenga el componente importador de diseños OOTB (predeterminado) (NPR-31728).

* Cuando se intenta cambiar una lista de viñetas a una lista numerada, solo se cambian los dos primeros elementos de la lista (NPR-31636).

* Cuando se anula la creación de una página y se selecciona el nodo secundario, el cuadro de diálogo de selección aún muestra el nodo inicial. Cuando se crea la página y el usuario hace clic en Examinar, la página se redirige al nodo raíz en lugar del nodo creado (NPR-31618).

* El cuadro de diálogo de configuración de la vista no funciona correctamente para la función de flujo de trabajo de personalización de la Bandeja de entrada (NPR-32503 y NPR-32492).

* Aparece un mensaje de error al ver la información del flujo de trabajo mediante la Bandeja de entrada (CQ-4282168).

### Assets {#assets-6540-enhancements}

* El botón para activar el flujo de trabajo en la página de recopilación de recursos está desactivado (NPR-32471).

* Se crea una carpeta sin nombre en SPS (Scene7 Publishing System) mientras se mueve un recurso de una carpeta a otra en Experience Manager con la configuración de Dynamic Media Scene7 (NPR-32440).

* La acción para mover todos los recursos (mediante Seleccionar todo y, a continuación, mover) a una carpeta que contenga recursos publicados falla con error (NPR-32366).

* Error en la generación de representaciones para recursos con ${extension} (NPR-32294).

* Las direcciones URL del historial de versiones se muestran en el campo Referenciado por de la página de propiedades de recursos (NPR-31889).

* El archivo ZIP descargado de DAM no se puede abrir con WinZip (NPR-32293).

* Los permisos originales de una carpeta se actualizan cuando se abre la configuración de la carpeta para cambiar el título de la carpeta o la imagen en miniatura y, a continuación, se guardan (NPR-32292).

* El icono de calendario para la activación programada no se muestra en la columna Estado (en la IU clásica de la lista de recursos DAM) para los recursos cuya activación está programada para una fecha y hora posteriores (NPR-32291).

* La creación de fragmentos de código mediante plantillas de fragmento produce un error al buscar colecciones durante el proceso de creación de fragmentos (NPR-32290).

* Se activan varias consultas de búsqueda cuando se seleccionan varias etiquetas en el filtro de búsqueda (NPR-32143).

* La interfaz de usuario de Experience Manager Assets muestra nombres de archivo truncados cuando se cargan recursos con más de 50 caracteres en el nombre de archivo (NPR-32054).

* Todas las casillas de verificación del panel Filtro se desactivan cuando se desactivan la primera y la segunda casillas de verificación, cuando se seleccionan las casillas de verificación de nivel dos del árbol de casillas de verificación en Adobe Stock (NPR-31919).

* La búsqueda de archivos y carpetas mediante facetas de Omnisearch ofrece una excepción (NPR-31872).

* El resaltado de campos para la selección obligatoria de campos en el editor de metadatos no se elimina ni siquiera después de seleccionar el campo requerido, cuando las reglas de dependencia se establecen en el formulario de esquema de metadatos correspondiente (NPR-31834).

* Los nombres completos de las etiquetas de nivel de hoja (de la jerarquía de etiquetas) no se muestran en la página Propiedades del recurso (NPR-31820).

* El uso del comando posterior de la página Propiedades del recurso en el navegador Safari genera un error (NPR-31753).

* La página de resultados de la búsqueda por IU táctil (realizada a través de Omnisearch) se desplaza automáticamente hacia arriba y pierde la posición de desplazamiento del usuario (NPR-31307).

* La página de detalles de recursos de los recursos PDF no muestra botones de acción excepto los botones Para colección y Añadir representación en Experience Manager que se ejecutan en el modo de ejecución de Dynamic Media Scene7 (CQ-4286705).

* Los recursos buenos de más de 2 GB ahora se pueden cargar en Dynamic Media-Scene7 (CQ-4286561).

* Los recursos tardan demasiado en procesarse mediante el proceso de carga por lotes de Scene7 (CQ-4286445).

* El botón Guardar no importa el conjunto remoto cuando el usuario no ha realizado ningún cambio en el Editor de conjuntos en el cliente de medios dinámicos (CQ-4285690).

* La miniatura de un recurso 3D no es informativa cuando se ingesta un modelo 3D compatible en AEM (CQ-4283701).

* El estado sin procesar del ajuste preestablecido de visor de vídeo de recorte inteligente aparece dos veces en el texto de la pancarta junto con el nombre del ajuste preestablecido (CQ-4283517).

* En la página de detalles del recurso (CQ-4283309) se observa una altura incorrecta del contenedor de un modelo 3D cargado con vista previa en el visor 3D.

* El Editor de carrusel no se abre en IE 11 en el modo híbrido de Dynamic Media de Experience Manager (CQ-4255590).

* El enfoque del teclado se queda atascado en la lista desplegable Correo electrónico del cuadro de diálogo Descargar, en los navegadores Chrome y Safari (NPR-32067).

* La casilla de verificación Sincronizar todo el contenido no está habilitada de forma predeterminada al intentar agregar la configuración de nube de DM en AEM (CQ-4288533).

### Interfaz de usuario de Foundation {#foundation-ui-6540}

* El control del ratón cambia al campo de filtro anterior en lugar de permanecer en el campo de filtro existente al buscar recursos con el panel Filtro (NPR-32538).

* Etiquetado de plataforma: Para buscar etiquetas, escriba en los campos de etiqueta, se muestran las etiquetas que están fuera de los límites raíz y no se respeta la `rootPath` propiedad de los campos de etiqueta (NPR-31895).

* Interfaz de usuario de plataforma: El navegador de rutas se interrumpe si se agrega una ruta no válida en el campo de texto (NPR-31884).

* La notificación se oculta detrás de un menú adhesivo en la selección de página (NPR-31628).

### Plataforma {#platform-sling-6540}

* (HTL) Los caracteres de subrayado reemplazan los dos puntos en la sección de ruta de la dirección URL (NPR-32231).

### Proyectos {#projects-6540}

* El botón Crear no está visible para el usuario aunque éste tenga permiso para crear un proyecto en la subcarpeta (NPR-31832).

### Traducción de proyectos {#projects-translation-6540}

* La creación de proyectos de traducción interrumpe la interfaz de usuario cuando se activa la opción Recortar espacios en `Apache Sling JSP Script Handler` (NPR-32154).

* Se observa un error en la interfaz de usuario y una excepción de punto nulo en los registros de errores cuando se agrega cualquier etiqueta a un proyecto de traducción (NPR-31896).

### Integraciones {#integrations-6540}

* La generación de direcciones URL de la biblioteca de inicio se basa únicamente en `path` y `library_name` los valores de la API de inicio, y no se basa en el `library_path` valor (NPR-31550).

* Aparece un mensaje de error al procesar los elementos relacionados con LiveFile (FYR-12420).

### Editor de plantillas WCM {#wcm-template-editor-6540}

* En el modo de estructura de plantillas editables, la lista de componentes permitidos en el contenedor de diseños no muestra el componente de botón de vínculo (CQ-4282099).

### WCM Page Editor {#wcm-page-editor-6540}

* Se observa un error al seleccionar una superposición y, a continuación, seleccionar una cuadrícula adaptable Arrastre los componentes aquí (CQ-4283342).

### Campaign Targeting {#campaign-targeting-6540}

* La configuración de la nube de destino falla con el error al obtener la solicitud de mboxes (CQ-4279880).

### Brand Portal {#assets-brand-portal}

* Los valores desplegables del esquema de metadatos no están visibles en las propiedades del recurso (CQ-4283287).

* El subesquema de metadatos no muestra fichas basadas en mimetype en propiedades de recursos (CQ-4283288).

* El esquema de metadatos de cancelación de publicación rellena un mensaje de error, aunque el esquema se elimina al final.

* La imagen de vista previa no se muestra para un recurso publicado (CQ-4285886).

* El usuario no puede publicar ni cancelar la publicación de recursos que contengan una sola cotización en el nombre (CQ-4272686).

* Los términos y condiciones no se muestran al descargar varios recursos (CQ-4281224).

* Se han solucionado pequeñas vulnerabilidades de seguridad.

### Communities {#communities}

* El formulario Crear miembro se muestra como una página en blanco (NPR-31997).

* El usuario no puede ver el informe de Analytics en la instancia de autor (NPR-30913).

### Indexación de roble y consultas {#oak-indexing-6540}

* Los documentos de Microsoft Word y MS Excel, que contienen imágenes JPEG, cuando se analizan con el analizador Tika no se analizan y se observa un error de clase no encontrada (NPR-31952).

### Formularios {#forms-6530}

>[!NOTE]
>
>Service Pack de AEM no incluye correcciones para AEM Forms. Estas se entregan mediante un paquete independiente de complementos de Forms. Asimismo, se ha publicado un instalador acumulativo que incluye correcciones para AEM Forms en JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Administración de correspondencia: Las cartas muestran caracteres adicionales después del envío a los flujos de trabajo del proceso de publicación (NPR-32626).

* Administración de correspondencia: Las letras muestran un marcador de posición desplegable como un componente de texto después de enviarlo a flujos de trabajo posteriores al proceso (NPR-32539).

* Administración de correspondencia: Los valores predeterminados definidos en la plantilla de letras no se muestran en el modo de vista previa (NPR-32511).

* Formularios móviles: El botón de envío se muestra con un tamaño ampliado mientras se procesa un formulario XDP en una versión HTML (NPR-32514).

* Document Services: Problemas de acceso a URL para cartas y otras páginas después de aplicar Service Pack 2 (NPR-32508, NPR-32509).

* Document Services: Si el número de transacciones en un servidor supera un límite específico, la conversión de HTML a PDF falla y la configuración del tipo de archivo se elimina del servidor de AEM Forms (NPR-32204).

* Formularios adaptables: La herramienta de accesibilidad de navegadores informa de errores en formularios adaptables según las directrices WCAG2 de nivel AA (NPR-32312, NPR-32309, CQ-4285439).

* Formularios adaptables: La herramienta de accesibilidad del navegador Chrome informa de un error de práctica recomendada (NPR-32310).

* Formularios adaptables: Problemas de traducción al configurar un formulario adaptable incrustado en una página Sitios de AEM (NPR-32168).

* Área de trabajo: Aparece un mensaje de error al utilizar la operación Obtener propiedades de PDF para el servicio Utilidades de PDF (NPR-32150).

* Document Security: Un archivo PDF protegido no se puede abrir sin conexión con la opción DisableGlobalOfflineSynchronizationData establecida en True (NPR-32078).

* Designer: Si la opción de etiquetado está activada, el borde del subformulario desaparece en la salida PDF generada (NPR-32547, NPR-31983, NPR-31950).

* Designer: Si hay celdas combinadas en una tabla, la prueba de accesibilidad falla para el archivo PDF de salida convertido desde un formulario XDP mediante el servicio de salida (CQ-4285372).

* Foundation JEE: Si un servidor de AEM Forms está desconectado de un clúster, los problemas de almacenamiento en caché impiden que se vuelva a conectar al servidor (NPR-32412).

## Install 6.5.4.0 {#install}

**Requisitos de configuración**

* AEM 6.5.4.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* La descarga del Service Pack está disponible en la opción de uso compartido de paquetes de Adobe, a la que puede acceder directamente desde la instancia de AEM 6.5.
* En una implementación con MongoDB y varias instancias, instale AEM 6.5.4.0 en una de las instancias de creación mediante el Administrador de paquetes.
* Antes de instalar el paquete de servicio, asegúrese de disponer de una instantánea o una copia de seguridad nueva de su instancia de AEM.
* Reinicie la instancia antes de la instalación. Aunque esto solo es necesario cuando la instancia sigue en modo de actualización (y este es el caso cuando la instancia se actualizó desde una versión anterior), se recomienda si la instancia se ejecutó durante un período más largo.

>[!CAUTION]
>
>Adobe no recomienda quitar o desinstalar el paquete AEM 6.5.4.0.

### Instalación de la instancia de Service Pack mediante el uso compartido de paquetes {#install-service-pack-via-package-share}

Siga estos pasos para instalar el paquete de servicio en una instancia de AEM 6.5 existente:

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.4.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0).

1. Instale el paquete descargado mediante el Administrador de paquetes.

>[!NOTE]
>
>**El cuadro de diálogo en la IU del administrador de paquetes a veces se cierra de forma precipitada durante la instalación de 6.5.4.0**
>
>Por lo tanto, se recomienda esperar a que los registros de errores se estabilicen antes de acceder a la instancia. El usuario tiene que esperar a que se produzcan registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que las instalaciones se realizan correctamente. Suele suceder en Safari, pero puede suceder de forma intermitente en cualquier navegador.

**Instalación automática**

Existen dos formas de instalar automáticamente AEM 6.5.4.0 en una instancia en ejecución:

A. Coloque el paquete en ..*carpeta /crx-quickstart/install* mientras el servidor está disponible en línea. El paquete se instala automáticamente.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.4.0 no admite la instalación de Bootstrap.

**Validar la instalación**

1. La página Información del producto (/system/console/ productinfo) muestra la cadena de versión actualizada `Adobe Experience Manager, Version 6.5.4.0` en Productos instalados.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. El paquete OSGI org.apache.jackrabbit.oak-core está en la versión 1.10.6 o superior (utilice la consola web: /system/console/buncles).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms. Las correcciones en AEM Forms se entregan mediante un paquete de complementos independiente.

>[!NOTE]
>
>AEM 6.5.4.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). Si utiliza una versión anterior del paquete de compatibilidad de AEM Forms y la actualiza a AEM 6.5.4.0, instale la versión más reciente del paquete de compatibilidad de AEM Forms después de la instalación del paquete de complemento de Forms.

1. Asegúrese de que ha instalado el Service Pack de AEM.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms en JEE. Las correcciones en AEM Forms en JEE se entregan a través de un instalador independiente.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0011](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0011.html).

#### Instalador de Workbench

Como es un instalador completo, el tamaño del archivo es mayor que el de la versión del parche. Desinstale la versión anterior de Workbench antes de instalar la nueva.

### UberJar {#uber-jar}

The UberJar for AEM 6.5.4.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.4</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Funciones en desuso {#removed-deprecated-features}

Esta sección enumera las funciones y funciones que se han marcado como obsoletas con AEM 6.5.4.0. Las funciones que se planea eliminar en una versión futura se definen como obsoletas en primer lugar, con una opción alternativa para su uso.

Se aconseja a los clientes que revisen si utilizan la función o la capacidad en su implementación actual y que planifiquen cambiar su implementación para utilizar la opción alternativa.

| Área | Función | Reemplazo |
|---|---|---|
| Integraciones | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. Con la integración de AEM y Target actualizada en AEM 6.5 para admitir la API de Target Standard, que utiliza la autenticación mediante Adobe IMS y E/S, y el creciente papel de Adobe Launch en la instrumentación de páginas de AEM para el análisis y la personalización, el asistente para la selección de contenido se ha vuelto funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y las integraciones de Adobe E/S a través de los respectivos servicios de nube de AEM |

## Problemas conocidos {#known-issues}

* Si **el asistente para configuración** de recursos conectados devuelve un mensaje de error 404 después de la instalación, vuelva a instalar manualmente los paquetes **cq-remotedam-client-ui-content** y **cq-remotedam-client-ui-components** mediante el Administrador de paquetes.
* Durante la instalación de AEM 6.5.x.x pueden aparecer los siguientes errores y mensajes de advertencia:
   * &quot;Cuando la integración de Target se configura en AEM mediante la API de Target Standard (autenticación IMS), la exportación de fragmentos de experiencia a Target provoca la creación de tipos de ofertas incorrectos. En lugar de tener que escribir &quot;Fragmento de experiencias&quot;/origen &quot;Adobe Experience Manager&quot;, Destino, se crean varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * com.adobe.granite.maintenance.impl.TaskScheduler: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor de Formulario adaptable falla cuando se utilizan funciones de agregado como SUM, MAX y MIN. CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al obtener una vista previa del recurso a través del visor de banners a la venta.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en AEM 6.5.4.0

Lista de paquetes OSGi incluidos en AEM 6.5.4.0

[Obtener archivo](assets/6540_bundles.txt)

Lista de paquetes de contenido incluidos en AEM 6.5.4.0

[Obtener archivo](assets/6540_packages.txt)

## Restricted sites {#restricted-sites}

Estos sitios solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con el servicio de asistencia](https://daycare.day.com/public/contact.html)al cliente Para obtener más información sobre el acceso al portal de asistencia técnica, consulte [Acceso al portal](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)de asistencia técnica.

>[!MORE COMO ESTO]
>
>* [Notas de la versión de AEM 6.5](/help/release-notes/release-notes.md)
>* [Página de productos AEM](https://www.adobe.com/solutions/web-experience-management.html)
>* [Documentación de AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

