---
title: Notas de la versión de Service Pack de AEM 6.5
description: Notas de versión específicas de Service Pack 3 de Adobe Experience Manager 6.5.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: fdcd9173b02347a7a9527b292635d63e8aa9ce19

---


# Notas de la versión de Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Información de la versión {#release-information}

| Productos | **Adobe Experience Manager 6.5** |
|---|---|
| Versión | 6.5.3.0 |
| Tipo | Versión de Service Pack |
| Fecha | 12 de diciembre de 2019 |
| Descargar URL | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0), distribución [de software](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aem.html#package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.3.zip) |

## Novedades de Adobe Experience Manager 6.5.3.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.3.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of 6.5 release in **April 2019**. Se puede instalar sobre Adobe Experience Manager (AEM) 6.5.

Algunos aspectos destacados de esta versión del Service Pack son:

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.10.6.

* Experience Manager Assets ahora admite archivos ZIP creados con el algoritmo Deflate 64.

* Se ha añadido una nueva columna para la fecha de creación, que es ordenable, en la vista de lista DAM y en los resultados de búsqueda de recursos en la vista de lista.

* La clasificación de recursos basada en la columna Nombre se ha activado en la vista de lista.

* Los medios dinámicos ahora admiten recursos de vídeo de recorte inteligente. Smart Crop es una función de aprendizaje automático que vuelve a recortar un vídeo mientras mueve el fotograma para seguir el punto focal de la escena.

* Dynamic Media admite imágenes inteligentes.

* Posibilidad de [establecer preferencias fuera de Office](../forms/using/configure-out-of-office-settings.md) en flujos de trabajo de AEM.

* Posibilidad de [compartir elementos](../forms/using/configure-shared-queues-osgi.md) de bandeja de entrada o bandeja de entrada con otros usuarios en flujos de trabajo de AEM.

* Capacidad para [generar comunicaciones interactivas en modo](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)por lotes.

* Se ha actualizado la versión de jQuery incluida en ContextHub a 3.4.1.

### Lista de cambios {#list-of-changes}

#### Assets {#assets-6530-enhancements}

**Mejoras del producto**

* Experience Manager Assets ahora admite archivos ZIP creados con el algoritmo Deflate 64 (NPR-27573).

* Se ha agregado una nueva columna para la fecha de creación, que es ordenable, en la vista de lista DAM y en los resultados de búsqueda de recursos en la vista de lista (NPR-31312).

* La clasificación de recursos basada en la columna Nombre se permite en la vista de lista (NPR-31299).

* Los archivos de recursos GLB, GLTF, OBJ y STL admiten la vista previa de recursos en la página Detalles de recursos de DAM (CQ-4282277).

* El evento ReplicationOnModifyListener se activa para nodos de fragmento durante la carga de fragmentos en Dynamic Media (CQ-4281279).

* Los medios dinámicos ahora admiten recursos de vídeo de recorte inteligente. Smart Crop es una función de aprendizaje automático que vuelve a recortar un vídeo mientras mueve el fotograma para seguir el punto focal de la escena (CQ-4278995).

* Dynamic Media admite imágenes inteligentes (CQ-422249).

* La vista de búsqueda y exploración se ha configurado como vista predeterminada en el selector de base si se pasan parámetros de consulta en la solicitud (NPR-31601).

**Correcciones**

* Los metadatos de algunos documentos PDF no se actualizan ni guardan en el PDF al modificar su título (NPR-31629).

* El uso compartido de recursos no funciona para los recursos que tienen el carácter más &#39;+&#39; en sus nombres (NPR-31547).

* Las ediciones en el formulario de búsqueda predeterminado Administración de recursos * El carril de búsqueda no funciona de la forma esperada (NPR-31502).

* No se muestran sugerencias al utilizar Omniture en la vista Recursos para buscar recursos (NPR-31496).

* Las referencias de recursos dentro de las colecciones no se actualizan cuando los recursos a los que se hace referencia se mueven a otra ubicación, en casos en los que diferentes usuarios hacen referencia a los mismos recursos (NPR-31486).

* Se agregan etiquetas IPTC duplicadas a los metadatos de los recursos (NPR-31328).

* El recuento de resultados de búsqueda en la esquina superior derecha no se actualiza con precisión cuando la búsqueda se activa desde el carril de filtros (NPR-31316).

* Todas las casillas de verificación se desactivan al desactivar las casillas de verificación de segundo nivel en el filtro Tipo de archivo y el texto de la barra de búsqueda no está sincronizado con las propiedades seleccionadas o no seleccionadas (NPR-31287).

* No se pueden quitar todos los miembros (usuarios/grupos) de la sección Miembros de una carpeta; al intentar eliminar todos los usuarios, el usuario que ha iniciado sesión se agrega a la lista (NPR-31171).

* Los recursos con el símbolo más &#39;+&#39; en el nombre del archivo no se pueden eliminar (NPR-31162).

* El menú desplegable Crear, que está visible en el menú superior al seleccionar una carpeta, no muestra &#39;Carpeta&#39; como opción de creación (NPR-30877).

* Selección de carpetas Crear > Elemento de acción FileUpload falta cuando se aplica ACL para Deny jcr:removeChildNodes y jcr:removeNode en la ruta a un usuario (NPR-30840).

* Los flujos de trabajo DAM pasan a un estado antiguo cuando se cargan determinados recursos mp4, lo que provoca que todos los flujos de trabajo restantes pasen a un estado antiguo (NPR-30662).

* Error de memoria insuficiente cuando se carga un archivo PDF grande (de varios gigabytes) en DAM y se procesan sus subrecursos (NPR-30614).

* El movimiento masivo de recursos falla y muestra un mensaje de advertencia (NPR-30610).

* Los nombres de los recursos se cambian a minúsculas al mover recursos de una carpeta a otra en AEM que se ejecuta en el modo de ejecución de Dynamic Media Scene 7 (NPR-31630).

* Se observa un error al editar un conjunto de imágenes remoto para la imagen que reside en la carpeta con el mismo nombre que el nombre de empresa de Scene7 (NPR-31340).

* Los recursos de Dynamic Media que contienen referencias no se publican (NPR-31180).

* Las cargas del modo de ejecución de AEM Dynamic Media - Scene 7 a Scene7 tardan demasiado en completarse (NPR-31048).

* La zona interactiva añadida a un recurso de imagen no es visible a través del visor de imágenes interactivo en la página de detalles de recursos (NPR-30979).

* Se crean enormes trabajos de sling y vuelve a aparecer la pancarta de procesamiento cuando las acciones realizadas en recursos de AEM Assets se pasan a la escena 7 (NPR-30947).

* El conflicto se produce al crear una copia de idioma de los recursos y no se carga en Scene7 (NPR-30932).

* Las representaciones dinámicas descargadas de AEM que se ejecutan en el modo híbrido de Dynamic Media están dañadas (son de tipo de texto con contenido &quot;no se puede encontrar la imagen&quot; en lugar de contenido de imagen) (NPR-30876).

* El flujo de trabajo de codificación de vídeo de Dynamic Media no puede generar miniaturas para el vídeo que se migra de Scene7 al modo de ejecución Dynamic Media - Scene 7 (CQ-4282011).

* Se ha observado una excepción IpsApiException al migrar recursos de una instancia a otra mediante distintos ID de empresa de Scene7 (CQ-4280548).

* La miniatura de un recurso 3D no es informativa cuando se ingesta un modelo 3D compatible en AEM (CQ-4283701).

* Los botones de desplazamiento se muestran en el visor si un recurso 3D tiene pocas vistas de cámara (CQ-4283322).

* Altura incorrecta del contenedor de un modelo 3D cargado previsualizado en la página de detalles de recursos de Dimensional Viewer (CQ-4283309).

* Los vídeos no se pueden reproducir con SmartCropVideoViewer en Internet Explorer 11 y Safari (CQ-4281422).

* El uso del botón Mover para mover varios recursos, de una carpeta a otra, falla en AEM que se ejecuta en Dynamic Media - modo de ejecución scene7 (CQ-4280384).

* El vídeo distorsionado se ve en los detalles del recurso cuando el tipo MIME no es MP4 (CQ-4279704).

* Los vídeos recientemente ingestados en carpetas con perfil de vídeo permanecen en estado de procesamiento incluso después de que el porcentaje de codificación se complete al 100 % (CQ-4279389).

* Al mover recursos desde una carpeta, se crea un gran número de trabajos de sling (llamadas a la API de Scene7) que lo que se necesita de forma ideal (CQ-4278664).

* Los nombres del conjunto de imágenes se cambian a minúsculas en la escena 7, cuando se crea un conjunto de imágenes (o conjunto de medios) y se les asigna un nombre con la convención de nombres adecuada en DAM (CQ-4281112).

* El migrador de Scene7 establece el estado de publicación de forma incorrecta (CQ-4263492).

* La página de resultados de la búsqueda por IU táctil (realizada a través de Omniture) se desplaza automáticamente hacia arriba y pierde la posición de desplazamiento del usuario en los fragmentos de contenido (CQ-4282898).

* Los archivos PDF no se indexan y el contenido dentro de no se puede buscar (CQ-4278916).

* Error &quot;Grupo no enumerado por selector de usuario: &quot;se espera que false sea igual a true&quot; se observa al agregar un grupo de usuarios cerrado con diferente `principalName` y `authorizableId` (CQ-4278177).

* La vista de columna de la interfaz de usuario de recursos muestra todas las rutas, independientemente de la ruta raíz de la represa específica del inquilino (CQ-4278175).

* La búsqueda del selector de recursos no funciona correctamente (CQ-4275886).

* Los flujos de trabajo de representación fallan (CQ-4271928).

* Depuración de eventos DAM elimina los últimos datos del evento (maxSavedActivities) y contiene los datos creados anteriormente (NPR-31336).

* La página de resultados de la búsqueda por IU táctil (realizada a través de Omnisearch) se desplaza automáticamente hacia arriba y pierde la posición de desplazamiento del usuario (NPR-31307).

* La barra de acciones y el recuento de recursos no se actualizan al seleccionar todo y, a continuación, anular la selección de algunos elementos (carpetas/recursos individuales) en la IU táctil (NPR-31118).

* Se muestra una excepción en AEM mientras se sondea para obtener los detalles del trabajo de un recurso (CQ-4283569).

* Vulnerabilidad XSS en DAM (NPR-31654).

#### Sites {#sites}

* Si la herencia de LiveCopy está dañada, las páginas de Live Copy muestran vínculos de copia de idioma en lugar de vínculos de LiveCopy (NPR-30980).
* Para un nuevo modelo, si el número de registros es superior a 40, solo se muestran los primeros 40 registros. El modelo muestra líneas en blanco para el resto de los registros (NPR-31182).
* Cuando un usuario agrega caracteres japoneses o coreanos en la propiedad description de un menú, el menú muestra caracteres distorsionados para texto en japonés y coreano. (NPR-31331).
* El editor de texto enriquecido (RTE) no permite insertar una tabla incrustada como elemento de lista (NPR-30879).
* Fuera de la casilla, scaffolding Rich Text Editor (RTE). aplica tamaño de fuente en línea a los elementos de forma inesperada (NPR-31284).
* Cuando un usuario se centra en los campos del carril izquierdo y utiliza un método abreviado de teclado para pegar contenido, pega el contenido del portapapeles del editor de páginas en lugar del contenido copiado de los campos del carril izquierdo (NPR-31172).
* Cuando un usuario agrega un campo Carga de archivo a un campo múltiple, la ruta de la imagen se almacena en el nodo del componente en lugar del nodo de varios campos (NPR-30882).
* La API ResponsiveGridExporter no devuelve la interfaz com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter. El paquete com.day.cq.wcm.foundation.model.impl se declara como paquete privado (NPR-31398).
* Cuando se abre una página que contiene algunos fragmentos de experiencia en modo que no es de editor (ya sea en Autor sin el `editor.html` prefijo y `wcmmode=disabled`o en Editor), la solicitud termina en el código de error de estado HTTP 500 (NPR-30743).
* Los usuarios no pueden cambiar su contraseña ni acceder a su página de perfil (NPR-31161).
* En el servidor se genera un archivo JavaScript con datos de usuario (NPR-30822).
* La interfaz de usuario de creación de AEM permite la suplantación de identidad con contenido externo (NPR-29745).
* Vulnerabilidad de inyección de lenguaje de expresión en el editor de metadatos de AEM 6.5 (NPR-31017).

#### Búsqueda e interfaz de usuario {#search-ui-interface}

* Al pasar de la vista de tarjeta a la vista de lista en una página de resultados de búsqueda, hay un retraso antes de que se pueda desplazar la página (NPR-31286).

* La casilla de verificación Seleccionar todo está oculta en la vista de lista de la interfaz de usuario Sitios (NPR-31614).

* El recuento Seleccionar todo en una página de resultados de búsqueda es incorrecto (NPR-31120).

* El editor de metadatos muestra etiquetas que no existen (NPR-31119).

#### Traducción {#translation}

* Aparecen dos ventanas emergentes de calendario al seleccionar la opción Fecha de vencimiento en un trabajo de traducción (NPR-31270).

#### Plataforma {#platform}

* La opción Tipo de MIME en la consola web no funciona (NPR-31108).

* El certificado de cliente no se acepta al configurar el inicio de sesión único (NPR-31165).

* Las actualizaciones en la configuración del tamaño del búfer para el servicio HTTP basado en Jetty no se guardan (NPR-30925).

* QueryBuilder ahora admite pedidos ``fn:name()`` en consultas xpath (NPR-31322).

* Se crea un árbol de activación duplicado al actualizar desde AEM 6.3 (NPR-31513).

* Las solicitudes reenviadas no conservan los encabezados de respuesta establecidos durante la autenticación sling (NPR-30013).

* La búsqueda dentro de los componentes del selector no funciona (NPR-31692).

* Se muestra un error al adjuntar un archivo ZIP a una publicación de AEM Communities debido a diferentes versiones del paquete Apache POI y Apache Tika (NPR-31018).

* El ``org.apache.sling.distribution.api`` paquete está oculto en el administrador de configuración y, por lo tanto, no está disponible para paquetes personalizados (NPR-31720).

#### Proyectos {#projects}

* El cambio de vistas de calendario no funciona (NPR-31271).

#### Brand Portal {#assets-brand-portal}

**Mejoras del producto**

* El flujo de trabajo de importación de Asset Sourcing en Recursos AEM se ha modificado para recuperar solo los recursos recién creados de Brand Portal a AEM y omitir los recursos que ya existen en la nueva carpeta para evitar la replicación (CQ-4278527).

**Correcciones**

* Aparece un icono incorrecto al crear una nueva carpeta de contribución en la función de fuentes de recursos (CQ-4282825).
* Al crear una nueva carpeta Contribution, una o ambas subcarpetas (NUEVAS y COMPARTIDAS) no aparece dentro de la carpeta Contribution (CQ-4282424).
* El sistema genera una excepción si el usuario intenta volver a publicar la carpeta Contribution de AEM en Brand Portal después de recibir nuevos recursos en la carpeta Contribution desde Brand Portal end (CQ-4279740).
* La creación de la carpeta Contribution dentro de una carpeta Contribution (carpeta anidada) está prohibida para evitar la complejidad (CQ-4278391).
* El sistema emite una excepción al cargar la lista de usuarios de Brand Portal (archivo .csv) importada desde la Consola de administración de AEM. Solo son obligatorios los campos Correo electrónico, Nombre y Apellido del archivo .csv (CQ-4278390).

#### Communities {#communities}

**Correcciones**

* Los vínculos rápidos para administrar grupos (Abrir/Editar/Publicar/Eliminar grupos) no son visibles para los administradores de la comunidad (administrador del grupo/administrador del sitio) (NPR-31627).
* Un blog enviado no se muestra a menos que la página se actualice o recargue manualmente (NPR-31599).
* La consulta JCR utilizada por la función &quot;Menciones&quot; distingue entre mayúsculas y minúsculas y tarda demasiado en devolver resultados (NPR-31475).
* El archivo UberJar de AEM 6.5 emite una excepción, pero falta el paquete en el archivo UberJar de AEM 6.5 (NPR-31186). `cq-social-translation`
* Las bibliotecas del enlace de datos Jackson se actualizaron a la versión 2.9.9.3 para abordar nuevas vulnerabilidades (NPR-30967).
* Los títulos de las actividades y las notificaciones son incoherentes (NPR-30941).
* La paginación no funciona correctamente en los blogs de Communities (NPR-30914).
* Los informes de Analytics no se completan en el entorno de creación de AEM; aparece una página en blanco (NPR-30913).

#### Oak {#oak}

* Las actualizaciones del índice de Lucene hacen que el servidor de creación se ralentice (NPR-31548).

#### Formularios {#forms-6530}

>[!NOTE]
>
>Service Pack de AEM no incluye correcciones para AEM Forms. Estas se entregan mediante un paquete independiente de complementos de Forms. Asimismo, se ha publicado un instalador acumulativo que incluye correcciones para AEM Forms en JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

##### Paquete de complemento de Forms {#forms-add-on-package-6530}

**Formularios adaptables**

* Las cadenas contienen la clave del diccionario al localizar formularios adaptables (NPR-31110).

**Comunicación interactiva**

* **MissingNode.toString()** devuelve resultados inexactos después de actualizar las bibliotecas de Jackson a 2.10.0 (NPR-31549).

* El editor de texto elimina aleatoriamente los caracteres de espacio del texto copiado de Microsoft Word (NPR-31113).

**Administración de correspondencia**

* Los rótulos y la información sobre herramientas no se muestran al migrar letras de LiveCycle ES4SP1 a AEM 6.5 (NPR-31615).

* **El formato de flujo de texto ya no se muestra** en los mensajes de error al guardar las letras como borradores (NPR-30463).

**Flujo de trabajo**

* El flujo de trabajo de OSGi falla debido a la utilización del 100% de la CPU (NPR-31233).

**HTML5 Forms**

* Al generar la vista previa HTML5 de un formulario XDP, se muestra un parpadeo al agregar instancias de un subformulario (NPR-30909).

##### Forms on JEE installer {#forms-jee-installer-6530}

**Forms: servicios de documentos**

* El servicio web SOAP que utiliza MTOM en un proyecto .NET muestra excepciones para los métodos AssemblerServiceClient invoke y HtmlToPDF2 (NPR-4281771).

**Base JEE**

* La configuración de la acción no carga los nombres de proceso para la acción de envío Invocar un flujo de trabajo de formularios (NPR-31478).
* Los formularios de AEM en JEE detectan errores similares a los siguientes al importar archivos .lca o al configurar LDAP en la consola de administración:

   `com.ibm.ws.webcontainer.filter.FilterInstanceWrapper doFilter SRVE8109W: Uncaught exception thrown by filter um: java.lang.NoClassDefFoundError: org/apache/commons/io/IOUtils at org.apache.commons.fileupload.util.Streams.copy`

   `Error 500: javax.servlet.ServletException: java.lang.NoClassDefFoundError: org.apache.commons.io.IOUtils` (NPR-30931)


### Paquetes de funciones incluidos {#feature-packs-included-6530}

>[!NOTE]
>
>Para los clientes de AEM Forms, es esencial instalar el paquete de complementos de AEM Forms después de instalar cualquier paquete de servicio, paquete acumulativo o paquete de funciones de AEM.

#### Forms: base JEE {#forms-foundation-jee-feature}

* Compatibilidad de AEM Forms con Oracle 18c (NPR-29155).

## Install 6.5.3.0 {#install}

**Requisitos de configuración**

* AEM 6.5.3.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* La descarga del Service Pack está disponible en la opción de uso compartido de paquetes de Adobe, a la que puede acceder directamente desde la instancia de AEM 6.5.
* En una implementación con MongoDB y varias instancias, instale AEM 6.5.3.0 en una de las instancias de creación mediante el Administrador de paquetes.
* Antes de instalar el paquete de servicio, asegúrese de disponer de una instantánea o una copia de seguridad nueva de su instancia de AEM.
* Reinicie la instancia antes de la instalación. Aunque esto solo es necesario cuando la instancia sigue en modo de actualización (y este es el caso cuando la instancia se actualizó desde una versión anterior), se recomienda si la instancia se ejecutó durante un período más largo.

>[!CAUTION]
>
>Adobe no recomienda quitar o desinstalar el paquete AEM 6.5.3.0.

### Instalación de la instancia de Service Pack mediante el uso compartido de paquetes {#install-service-pack-via-package-share}

Siga estos pasos para instalar el paquete de servicio en una instancia de AEM 6.5 existente:

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.3.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0).

1. Instale el paquete descargado mediante el Administrador de paquetes.

>[!NOTE]
>
>**El cuadro de diálogo en la IU del administrador de paquetes a veces se cierra de forma precipitada durante la instalación de 6.5.3.0**
>
>Por lo tanto, se recomienda esperar a que los registros de errores se estabilicen antes de acceder a la instancia. El usuario tiene que esperar a que se produzcan registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que las instalaciones se realizan correctamente. Suele suceder en Safari, pero puede suceder de forma intermitente en cualquier navegador.

**Instalación automática**

Existen dos formas de instalar automáticamente AEM 6.5.3.0 en una instancia en ejecución:

A. Coloque el paquete en ..*carpeta /crx-quickstart/install* mientras el servidor está disponible en línea. El paquete se instala automáticamente.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.3.0 no admite la instalación de Bootstrap.

**Validar la instalación**

1. La página Información del producto (/system/console/ productinfo) muestra la cadena de versión actualizada `Adobe Experience Manager, Version 6.5.3.0` en Productos instalados.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. El paquete OSGI org.apache.jackrabbit.oak-core está en la versión 1.10.6 o superior (utilice la consola web: /system/console/buncles).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms. Las correcciones en AEM Forms se entregan mediante un paquete de complementos independiente.

>[!NOTE]
>
>AEM 6.5.3.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). Si utiliza una versión anterior del paquete de compatibilidad de AEM Forms y la actualiza a AEM 6.5.3.0, instale la versión más reciente del paquete de compatibilidad de AEM Forms después de la instalación del paquete de complemento de Forms.

1. Asegúrese de que ha instalado el Service Pack de AEM.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms en JEE. Las correcciones en AEM Forms en JEE se entregan a través de un instalador independiente.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0007](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0007.html).

#### Instalador de Workbench

Como es un instalador completo, el tamaño del archivo es mayor que el de la versión del parche. Desinstale la versión anterior de Workbench antes de instalar la nueva.

## UberJar {#uber-jar}

The UberJar for AEM 6.5.3.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.3/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.3.0</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Funciones en desuso {#removed-deprecated-features}

Esta sección enumera las funciones y funciones que se han marcado como obsoletas con AEM 6.5.3.0. Las funciones que se planea eliminar en una versión futura se definen como obsoletas en primer lugar, con una opción alternativa para su uso.

Se aconseja a los clientes que revisen si utilizan la función o la capacidad en su implementación actual y que planifiquen cambiar su implementación para utilizar la opción alternativa.

| Área | Función | Reemplazo |
|---|---|---|
| Integraciones | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. Con la integración de AEM y Target actualizada en AEM 6.5 para admitir la API de Target Standard, que utiliza la autenticación mediante Adobe IMS y E/S, y el creciente papel de Adobe Launch en la instrumentación de páginas de AEM para el análisis y la personalización, el asistente para la selección de contenido se ha vuelto funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y las integraciones de Adobe E/S a través de los respectivos servicios de nube de AEM |

## Problemas conocidos {#known-issues}

* Si **el asistente para la configuración** de recursos conectados devuelve un mensaje de error 404 después de instalar AEM 6.5.3.0, vuelva a instalar manualmente los paquetes **cq-remotedam-client-ui-content** y **cq-remotedam-client-ui-components** mediante el Administrador de paquetes.
* Durante la instalación de AEM 6.5.x.x pueden aparecer los siguientes errores y mensajes de advertencia:
   * &quot;Cuando la integración de Target se configura en AEM mediante la API de Target Standard (autenticación IMS), la exportación de fragmentos de experiencia a Target provoca la creación de tipos de ofertas incorrectos. En lugar de tener que escribir &quot;Fragmento de experiencias&quot;/origen &quot;Adobe Experience Manager&quot;, Destino, se crean varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * com.adobe.granite.maintenance.impl.TaskScheduler: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor de Formulario adaptable falla cuando se utilizan funciones de agregado como SUM, MAX y MIN. CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al obtener una vista previa del recurso a través del visor de banners a la venta.

## Paquetes de contenido y paquetes OSGi incluidos {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en AEM 6.5.3.0

Lista de paquetes OSGi incluidos en AEM 6.5.3.0

[Obtener archivo](assets/6530_bundles.txt)

Lista de paquetes de contenido incluidos en AEM 6.5.3.0

[Obtener archivo](assets/sp_6530_packages.txt)

## Helpful Resources {#helpful-resources}

* [Notas de la versión de AEM 6.5](/help/release-notes/release-notes.md)
* [Página de productos AEM](https://www.adobe.com/solutions/web-experience-management.html)
* [Asistencia para desarrolladores de AEM](https://docs.adobe.com/content/ddc/en.html)
* [Documentación de AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html)
* Subscribe to [Adobe Priority Product Updates](https://docs.adobe.com/content/help/en/release-notes/experience-cloud/current.html)

## Sitios restringidos {#restricted-sites}

Estos sitios solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con el servicio de asistencia](https://daycare.day.com/public/contact.html)al cliente Para obtener más información sobre el acceso al portal de asistencia técnica, consulte [Acceso al portal](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)de asistencia técnica.
