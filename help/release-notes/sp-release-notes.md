---
title: '[!DNL Experience Manager] Notas de la versión de service pack 6.5'
description: Notas de versión específicas de [!DNL Adobe Experience Manager] 6.5 service pack 9
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 68928e251203f67faef498dc22f6d57ea141e748
workflow-type: tm+mt
source-wordcount: '3389'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] Notas de la versión de service pack 6.5  {#aem-service-pack-release-notes}

## Información de la versión {#release-information}

| Productos | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.9.0 |
| Tipo | Versión de Service Pack |
| Fecha | 27 de mayo de 2021 |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## Qué incluye [!DNL Adobe Experience Manager] 6.5.9.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.9.0 incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras de rendimiento, estabilidad y seguridad, que se han publicado desde la publicación de la versión 6.5 en abril de 2019. El Service Pack se instala en [!DNL Adobe Experience Manager] 6.5.

Las funciones y mejoras clave introducidas en [!DNL Adobe Experience Manager] 6.5.9.0 son:

* El componente AEM Sites Dynamic Media Foundation ahora permite activar o desactivar la optimización para dispositivos de mayor resolución al utilizar ajustes preestablecidos de imagen o Recorte inteligente interactivos.

* Para mejorar el rendimiento, la condición hidden=false se mueve de la consulta JCR al evaluador QueryBuilder. Para comprobar que un predicado oculto funciona después del cambio, Adobe Experience Manager comprueba que no se muestra ninguna carpeta oculta en la interfaz.

* Posibilidad de restaurar páginas y árboles eliminados en una página [!DNL Experience Manager Sites].

* Compatibilidad para que un nuevo usuario actualice el token de acceso mediante un token de actualización para el servicio de configuración de correo.

* Compatibilidad con el mecanismo SMTP XOAUTH2 para el servicio de configuración de buzones.

* Las ocurrencias de nombres relacionados con Hong Kong, Macao y Taiwán se actualizan según las nuevas convenciones de nomenclatura para las regiones y configuraciones regionales chinas.

* Mejoras de accesibilidad en [!DNL Experience Manager] [Assets](#assets-accessibility-6590) y [Dynamic Media](#accessibility-dm-6590).

* El RGPD de imágenes inteligentes (proporción de píxeles de dispositivo) y la optimización del ancho de banda de la red le permiten ofrecer imágenes de la mejor calidad de forma eficaz; en dispositivos con pantallas de alta resolución y ancho de banda de red restringido. Para obtener más información, consulte [Preguntas frecuentes sobre imágenes inteligentes](/help/assets/imaging-faq.md).

   >[!NOTE]
   >
   >La cronología de versiones para las mejoras de imágenes inteligentes anteriores es:
   >
   >* América del Norte 24 de mayo de 2021 en NA,
      >
      >
   * Europa, Oriente Medio y África 25 de junio de 2021,
      >
      >
   * Asia-Pacífico 19 de julio de 2021.


* Se ha introducido compatibilidad con el formato de imagen de próxima generación AVIF en la entrega de Dynamic Media (modificador de URL fmt). Para obtener más información, consulte [servicio de imágenes y renderización de api fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html).

   >[!NOTE]
   >
   >El calendario de versiones para la compatibilidad con AVIF es:
   >
   >* Norteamérica, 10 de mayo de 2021,
      >
      >
   * Europa, Oriente Medio y África 24 de mayo de 2021,
      >
      >
   * Asia-Pacífico 24 de junio de 2021.


* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.22.7.

Para obtener una lista completa de las funciones y mejoras introducidas en [!DNL Experience Manager] 6.5.9.0, consulte [novedades en [!DNL Adobe Experience Manager] 6.5 Service Pack 9](new-features-latest-service-pack.md).

>[!NOTE]
>
>A partir de AEM Service Pack 9, los clientes [!DNL Experience Manager] pueden desarrollar y operar sus [!DNL Experience Manager] aplicaciones con distribuciones de las [!DNL Azul Zulu] compilaciones de OpenJDK, compatibles con los estándares de Java SE.
>El Adobe también proporciona soporte para los [!DNL Azul Zulu] JDK a los clientes [!DNL Experience Manager].
>Puede descargar las versiones relevantes de [!DNL Azul Zulu JDKs] desde [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
>Los derechos de uso de la tecnología Java de Oracle, tal como se distribuyen por Adobe, expirarán a finales de diciembre de 2022. [!DNL Experience Manager] se recomienda a los clientes que planifiquen e implementen el uso de para los  [!DNL Azul Zulu] JDK a más tardar para esta fecha. Para obtener más información sobre el uso de la tecnología [!DNL Oracle Java] y la tecnología [!DNL Azul Zulu], consulte las [preguntas frecuentes](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf?lang=en) asociadas.

La siguiente es la lista de correcciones que se proporcionan en la versión [!DNL Experience Manager] 6.5.9.0.

### [!DNL Sites] {#sites-6590}

* Las páginas publicadas con la propiedad Requisito de autenticación habilitada no redirigen a la página de inicio de sesión y devuelven el mensaje de error 404 (NPR-36354).

* Al crear un hipervínculo, la opción de buscar un vínculo no funciona en el componente de texto (NPR-35849).

* Se activa una consulta transversal al utilizar la API `com.day.cq.wcm.commons.ReferenceSearch`. Afecta al rendimiento del servidor [!DNL Experience Manager] (NPR-36407).

* El contenedor de diseño anidado que se encuentra dentro de otro contenedor de diseño cambiado de tamaño muestra un número incorrecto de columnas para sus componentes secundarios, lo que provoca que estos componentes no se alineen a la cuadrícula (NPR-36359).

* El Comprobador de vínculos externos muestra vínculos externos válidos como vínculos no válidos (NPR-36289).

* Después de mostrar las referencias durante algún tiempo, el panel de referencias comienza a mostrar un mensaje de error (NPR-36167).

* Al mover un componente, el parsys creado automáticamente no tiene el nodo `sling:resourceType` (NPR-36165).

* Cuando se intenta sincronizar una Live Copy (mientras se utilizan configuraciones de implementación [!UICONTROL Activar en modelo] y [!UICONTROL Desactivar en modelo]) si se elimina un componente en el maestro de Live Copy, la sincronización falla y se registra un `NullPointerException` (NPR-36127).

* Cuando un usuario escribe texto ad hoc para etiqueta (etiqueta que no existe en el sistema) y pulsa Intro, la etiqueta aparece debajo del campo pero cuando el fragmento de contenido se guarda y vuelve a abrir, la etiqueta ad hoc desaparece (NPR-36132).

* La bandeja de entrada no tiene la opción de mostrar el estado de las operaciones asincrónicas (NPR-36104).

* Se crea un componente duplicado después de restaurar la herencia (NPR-36000).

* Al utilizar `RemoteContentRenderingService`, la solicitud al `RemoteContentRendererRequestHandler.getRequest` siempre incluye la página raíz del `ComponentExporter`, pero no incluye la página solicitada si no se incluye con el modelo raíz en función de la profundidad de recorrido y las opciones de filtrado establecidas. La solicitud siempre debe incluir la página solicitada para que el SPA tenga suficiente información para presentar una respuesta (NPR-35961).

* Los elementos onTime/offTime no se activan/desactivan en el onTime/offTime esperado (NPR-35936).

* Cuando publica una página que contiene un fragmento de experiencia que no tiene la propiedad `cq:lastModified` , se produce un `NullPointerException` (NPR-35914).

* Cuando se intenta cambiar el tamaño de un componente dentro de un contenedor, no es posible volver a cambiar el tamaño al tamaño original. Cuando se reduce el tamaño del contenedor de componentes, no es posible volver a establecer el tamaño en el original (NPR-35809).

* En el cuadro de diálogo de lanzamiento, activado en el editor o desde la Información general de Live Copy, los iconos de estado para páginas separadas, suspendidas o no creadas son incorrectos (NPR-35691).

* Despliegue de Multi-Site Manager en propiedades de página de formato ignorar la página de despliegue y las subpáginas de la casilla de verificación (NPR-35634).

* Falta la funcionalidad Restaurar árbol, disponible en la IU clásica en la IU táctil (CQ-4315352, CQ-4309415).

* Problemas al revertir la herencia y desplegar la página en una página [!DNL Experience Manager Sites] (NPR-36033).

### [!DNL Assets] {#assets-6590}

[!DNL Adobe Experience Manager] 6.5.9.0  [!DNL Assets] corrige los siguientes problemas.

* Las etiquetas creadas dentro de un elemento de selección de etiquetas en un formulario [!UICONTROL Folder Metadata Schema] no se guardan (NPR-36119).

* Cuando se utiliza una elipse pequeña para anotar recursos, la elipse se superpone con el número de la anotación en la versión de impresión (NPR-36114).

* En la vista de columna, en algunos casos, [!DNL Experience Manager] no solicita conflictos de recursos duplicados cuando se carga un recurso duplicado (NPR-36048).

* El cuadro de diálogo Compartir vínculo no se cierra haciendo clic en el botón Cerrar si se abre y no se realiza ningún cambio (NPR-36030).

* Cuando se seleccionan varios recursos para actualizar las propiedades, a veces se produce un error o se actualizan las propiedades de un recurso no seleccionado (NPR-36002).

* Cuando en la carga de recursos se añaden espacios en blanco al principio o al final de los nombres de los archivos de recursos, con caracteres restantes iguales al nombre de un recurso existente en el repositorio, el recurso existente se reemplaza sin registrar ningún error (NPR-36001).

* Cuando el vídeo se reproduce en la página de detalles del recurso, las opciones de reproducción y pausa no funcionan (NPR-35999).

* Al cancelar la publicación de recursos de forma masiva, Brand Portal genera un error que sugiere que el URI de la solicitud es demasiado largo (NPR-35954).

* Cuando se imprime un recurso con texto de anotación largo, el texto de la anotación se recorta, incluso si hay espacio disponible (NPR-35948).

* La opción para desplazarse a la página siguiente está desactivada al seleccionar la página en la vista Plantillas seleccionada en la página Crear catálogo (CQ-4315462).

* Cuando se inicia el flujo de trabajo de actualización de recursos en el recurso de vídeo, la página se actualiza repetidamente (CQ-4313375).

* Las carpetas DAM no se pueden eliminar ni mover, y se registra una excepción (NPR-35942).

#### Mejoras en Assets {#assets-enhancements}

* Se ha introducido la opción [!UICONTROL None] en la tarjeta, columna y vista de perspectivas para ordenar los recursos en el orden en que se almacenan en el nodo JCR (NPR-36356).

* Se añade una opción para añadir el ID de correo electrónico en minúscula en la respuesta de API de Adobe Experience Manager (CQ-4317704).

#### Mejoras de accesibilidad en Assets {#assets-accessibility-6590}

[!DNL Adobe Experience Manager] 6.5.9.0  [!DNL Assets] proporciona las siguientes mejoras de accesibilidad.

Se mejora el contraste (con fondo) del siguiente texto e iconos, de modo que los usuarios con visión y percepción de color limitadas puedan comprender:

* título del recurso en la página [!UICONTROL Propiedades] (NPR-35967).
* iconos de clasificación por estrellas en las secciones [!UICONTROL Clasificación] en varios lugares (NPR-36009).
* texto en la vista de tarjeta de recursos y carpetas (NPR-35966).
* texto de marcador de posición en la vista [!UICONTROL Línea de tiempo] (NPR-35965).
* nombres de recursos en los resultados de búsqueda de recursos (NPR-35964).
* texto del marcador de posición en el cuadro de diálogo [!UICONTROL Uso compartido de vínculos] (NPR-35963).
* [!UICONTROL Metadatos],  [!UICONTROL estado] y   otro texto en la   lista, en el cuadro de diálogo  [!UICONTROL Ver ] configuración (NPR-35910).
*  Ubicación y  [!UICONTROL tipo para ] buscar textos de marcador de posición en búsqueda global (NPR-35909).
* expanda y contraiga los iconos en el [!UICONTROL Árbol de contenido] (NPR-35908).
* el texto [!UICONTROL Assets] en la página donde se muestran las carpetas de recursos (NPR-35905).
* en [!UICONTROL Metadatos de recursos], [!UICONTROL Estadísticas de uso] dentro de la opción [!UICONTROL Información general] en la página de detalles de recursos (NPR-35904).
* texto para teclas de método abreviado para las opciones [!UICONTROL properties] y [!UICONTROL editar] en la página de detalles del recurso (NPR-35904).

### [!DNL Dynamic Media] {#dynamic-media-6590}

Adobe Experience Manager 6.5.9.0 Assets corrige los siguientes problemas en [!DNL Dynamic Media]:

* Los ajustes preestablecidos de visualizador personalizados y CSS no se replican en [!DNL Dynamic Media] cuando [!DNL Dynamic Media] se activa de forma selectiva y se deshabilita por [default](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html?lang=en#troubleshoot-dm-config) (NPR-36232).

* Cuando se intenta obtener una vista previa de las representaciones de vídeo en la página de detalles del recurso, los vídeos se cargan lentamente (CQ-4320122).

* La página del explorador no responde y se ralentiza al cargar más de 200 activos con Duplicate Asset Detector habilitado (CQ-4319633).

* Cuando se añade un recurso de imagen panorámica en el componente de medios panorámicos de una página, se registra un error de referencia no capturada (CQ-4317666).

* Cuando se implementa un visualizador de medios interactivo con fragmento de experiencia, el fragmento de experiencia no se abre desde el editor y se registra un error (CQ-4317655).

* La opción Publicar en Dynamic Media no está disponible en Publicación rápida en la vista del editor de metadatos (CQ-4317199).

* Los autores de sitios con permisos de solo lectura pueden utilizar la funcionalidad de recorte inteligente en los recursos y editar las representaciones recortadas inteligentes. Sin embargo, los usuarios con permisos de solo lectura no deben poder editar las propiedades de los recursos en la instancia de desarrollo de sitios (CQ-4316450).

* Las anotaciones de vídeo no funcionan para rutas de carpeta en las que la configuración de Dynamic Media no está habilitada, aunque la instancia de AEM esté configurada en modo Dynamic Media (CQ-4314950).

* Cuando el título de los recursos tiene caracteres de doble byte, multibyte, ASCII alto, cirílico, par sustituto, hebreo, árabe y GB18030, al publicar en Dynamic Media el título del recurso tiene un signo de interrogación (?) (CQ-4311872).

#### Mejoras de accesibilidad en Dynamic Media {#accessibility-dm-6590}

[!DNL Adobe Experience Manager] 6.5.9.0  [!DNL Assets] proporciona las siguientes mejoras de accesibilidad en  [!DNL Dynamic Media].

* Cuando abra el cuadro de diálogo para agregar recursos mediante teclas de teclado en el editor de conjuntos de imágenes:
   * los lectores de pantalla narran que el cuadro de diálogo está abierto.
   * el foco del teclado se desplaza al cuadro de diálogo cuando se abre.
   * el enfoque del teclado vuelve a la opción Agregar recurso cuando se cierra el cuadro de diálogo (CQ-4312134).

* Ahora puede agregar y editar puntos interactivos en recursos utilizando teclas de teclado en el editor de puntos interactivos (CQ-4305965).

* Ahora puede colocar hipervínculos en puntos interactivos mediante la administración de puntos interactivos mediante teclas de teclado. El enfoque del lector de pantalla ahora se mueve al campo para editar la ruta de URL y la opción Abrir cuadro de diálogo de selección (CQ-4290735).

* Se mejora el contraste (con fondo) del texto y los controles en la página Editor de conjuntos de imágenes, de modo que los usuarios con visión y percepción limitadas del color puedan comprender (CQ-4290733).

* Ahora puede navegar a las opciones de uso compartido de recursos en el Editor de ajustes preestablecidos de visualizador y contraer la opción de uso compartido expandido mediante teclas de teclado (CQ-4290724).

* Ahora puede navegar y ver las informaciones de objeto en los iconos de información y los iconos de alerta en las pestañas Básico y Avanzado de la página Editar Codificación de Vídeo utilizando las teclas de teclado (CQ-4290722).

* Los lectores de pantalla ahora narran las instrucciones de varios campos en la pestaña Aspecto y Comportamiento del Editor de ajustes preestablecidos de visualizador (CQ-4290721).

* Al navegar por la página Editar ajuste preestablecido de imagen en el modo Formulario , el lector de pantalla narra el propósito y los nombres de varios campos y controles (CQ-4290717).

* Al navegar por la página de detalles de recursos, los lectores de pantalla ahora describen el propósito de varias opciones dentro de Visualizadores (CQ-4290716).

* Contraste (con fondo) del texto del marcador de posición Todas las representaciones en representaciones de la página de detalles del recurso se mejora, de modo que los usuarios con visión y percepción limitadas del color puedan comprenderlo (CQ-4290713).

* Ahora se proporciona un asterisco visual para indicar que el campo es obligatorio en el campo Título del recurso en el Editor de conjuntos de imágenes y los lectores de pantalla anuncian la información necesaria para el campo (CQ-4290712).

* Los lectores de pantalla ahora pueden acceder y narrar el propósito de varias opciones interactivas dentro de Visualizadores en la página de detalles de recursos (CQ-4290708).

### Plataforma {#platform-6590}

* Cuando se genera una miniatura para un modelo y se implementan los cambios en la Live Copy, la herencia de algunos campos no funciona (CQ-4319517).

* Cuando cree una carpeta, seleccione la propiedad Orderable y agregue más de 20 recursos a la carpeta. Al seleccionar todos los recursos de la carpeta, se muestra un recuento incorrecto (CQ-4316243).

* Al actualizar una página, la ordenación de carpetas o recursos no muestra los resultados adecuados (CQ-4316200).

* La biblioteca JavaScript de controladores se actualiza a la versión 4.7.7 (NPR-36375).

* Los paquetes personalizados no se actualizan al instalar un nuevo paquete de código mediante el Administrador de paquetes (NPR-35949).

* Un paquete Sling `resourceresolver` está causando que la consulta `Sling:alias` falle (NPR-35335).

* La ruta de contexto se elimina al configurar SSL en AEM (NPR-35294).

* La excepción `SegmentNotFound` se devuelve después de una sesión de larga duración (NPR-36405).

### Integraciones {#integrations-6590}

* No se pueden guardar las propiedades de la página con la herencia habilitada para los Cloud Services de fragmentos de experiencias (NPR-36107).

* La paginación de la interfaz de usuario IMS y la carga diferida no muestran los resultados adecuados (NPR-36046).

* Al crear la configuración de A4T Target y seleccionar la fuente de informes como [!DNL Adobe Analytics], no hay grupos de informes habilitados para Adobe Target disponibles en la lista desplegable (NPR-36006).

### Proyectos {#projects-6590}

* No se pueden guardar las propiedades de un proyecto porque la ruta JCR al proyecto no se ha resuelto debido a una barra diagonal adicional (/) anexada a la ruta del proyecto (NPR-36191).

### Pantallas {#screens-6590}

* [!DNL Experience Manager Screens] los reproductores no se pueden autenticar si se utiliza un controlador de autenticación 2FA personalizado (NPR-35854).

### Comercio {#commerce-6590}

* El asistente del [!UICONTROL Catálogo de comercio] no carga más de 40 elementos en la vista de columna (CQ-4318379).

### Proyectos de traducción {#translation-6590}

* Las opciones de actualización o sobrescritura no se muestran al retraducir una `es` a `es_es` página (NPR-36170).

* Cuando se selecciona la opción de aprobación automática para un proyecto con traducción humana, el estado del trabajo se muestra como `Unknown` (NPR-35981).

* Cuando traduce una página, la ruta de referencia de los fragmentos de experiencias no se actualiza a la ruta de referencia del fragmento de experiencias de destino (NPR-35911).

* Cuando se realizan cambios en las páginas principal y secundaria y se envía la página principal para su traducción, también se traducen incorrectamente las páginas secundarias (NPR-35896).

* Cuando hay varios proyectos de traducción simultáneos para una página seleccionada, la opción [!UICONTROL Ir a proyectos] no se vincula al último proyecto de traducción (NPR-35454).

* Cuando publica recursos en [!DNL Dynamic Media], [!DNL Experience Manager] muestra un mensaje incorrecto para etiquetas no publicadas (CQ-4315914, CQ-4315913).

* Cuando se abre un trabajo eliminado, [!DNL Experience Manager] muestra un mensaje incorrecto (CQ-4315910).

### Flujo de trabajo {#workflow-6590}

* Al hacer clic en Completar, Delegar o Abrir acciones para elementos disponibles en la Bandeja de entrada, no hay ninguna pista visual que indique la finalización de estas acciones (NPR-36317).

### [!DNL Communities] {#communities-6590}

* En el filtrado de correo no deseado, el sistema consume el 100% del espacio de memoria JAVA que baja el servidor de AEM (NPR-36316, NPR-36493).
* En los foros, los datos de las sesiones JCR procedentes de SearchCommentSocialComponentListProvider se filtran (NPR-36235).
* La apertura de un mensaje de bandeja de entrada específico refleja todos los mensajes con paginación incorrecta y otros problemas (NPR-35917).

### [!DNL Brand Portal] {#brandportal-6590}

* El indicador de la función de abastecimiento de recursos se habilita automáticamente al configurar [!DNL Experience Manager Assets] con [!DNL Brand Portal] (NPR-36010).

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>[!DNL Experience Manager Forms] lanza los paquetes de complementos una semana después de la fecha de lanzamiento programada del paquete de servicio de [!DNL Experience Manager].

Para obtener información sobre las actualizaciones de seguridad, consulte la [página de boletines de seguridad del Experience Manager](https://helpx.adobe.com/security/products/experience-manager.html).

## Instalar 6.5.9.0 {#install}

**Requisitos de configuración y más información**

* El Experience Manager 6.5.9.0 requiere el Experience Manager 6.5. Consulte [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas.
* La descarga del Service Pack está disponible en el Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* En una implementación con MongoDB y varias instancias, instale el Experience Manager 6.5.9.0 en una de las instancias de autor mediante el Administrador de paquetes.

>[!NOTE]
>
>Adobe no recomienda quitar o desinstalar el paquete [!DNL Adobe Experience Manager] 6.5.9.0.

### Instale el Service Pack {#install-service-pack}

Para instalar el Service Pack en una instancia [!DNL Adobe Experience Manager] 6.5, siga estos pasos:

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (y este es el caso cuando la instancia se actualizó desde una versión anterior). Adobe también recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de la instalación, tome una instantánea o una copia de seguridad nueva de su instancia [!DNL Experience Manager].

1. Descargue el Service Pack desde [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9.zip).

1. Abra Administrador de paquetes y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y haga clic en **[!UICONTROL Install]**.

1. Para actualizar el conector S3, detenga la instancia después de instalar el Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacenamiento de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del Administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que las instalaciones se realizan correctamente. Normalmente, esto sucede en [!DNL Safari] pero puede suceder de forma intermitente en cualquier explorador.

**Instalación automática**

Existen dos maneras de instalar automáticamente Adobe Experience Manager 6.5.9.0 en una instancia de trabajo:

A. Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.

B. Utilice la API [HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Utilice `cmd=install&recursive=true` para instalar los paquetes anidados.

>[!NOTE]
>
>Adobe Experience Manager 6.5.9.0 no es compatible con la instalación del Bootstrap.

**Validar la instalación**

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.9.0)` en [!UICONTROL Installed Products].

1. Todos los paquetes OSGi son **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.3 o posterior (utilice la consola web: `/system/console/bundles`).

Para saber cuáles son las plataformas certificadas para funcionar con esta versión, consulte los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

<!--

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>AEM 6.5.9.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to AEM 6.5.9.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.
-->

### UberJar {#uber-jar}

UberJar para Experience Manager 6.5.9.0 está disponible en el [repositorio Maven Central](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.9/).

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.9</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar y los otros artefactos relacionados están disponibles en el Repositorio Central de Maven en lugar del Repositorio de Maven Público de Adobe (`repo.adobe.com`). El nombre del archivo principal de UberJar cambia a `uber-jar-<version>.jar`. Por lo tanto, no hay `classifier`, con `apis` como valor, para la etiqueta `dependency`.

## Funciones en desuso {#removed-deprecated-features}

A continuación se muestra una lista de funciones y capacidades que están marcadas como obsoletas con [!DNL Experience Manager] 6.5.7.0. Las funciones se marcan como obsoletas inicialmente y luego se eliminan en una versión futura. Normalmente se proporciona una opción alternativa.

Revise si utiliza una función o una capacidad en una implementación. Además, planifique cambiar la implementación para utilizar una opción alternativa.

| Área | Función | Reemplazo |
|---|---|---|
| Integraciones | La pantalla de inclusión **[!UICONTROL AEM Cloud Services]** está en desuso. Con la integración de Experience Manager y Adobe Target actualizada en Experience Manager 6.5 para admitir la API de Adobe Target Standard, que utiliza la autenticación mediante IMS y E/S de Adobe, y el creciente papel de Launch de Adobe para instrumentar páginas de Experience Manager para el análisis y la personalización, el asistente de inclusión se ha vuelto funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y las integraciones [!DNL Adobe I/O] a través de los respectivos servicios de nube de Experience Manager. |
| Conectores | El conector JCR de Adobe para Microsoft SharePoint 2010 y Microsoft SharePoint 2013 está en desuso para Experience Manager 6.5. | N/D |

## Problemas conocidos {#known-issues}

* Si está actualizando la instancia [!DNL Experience Manager] de la versión 6.5 a la versión 6.5.9.0, puede ver `RRD4JReporter` excepciones en el archivo `error.log`. Reinicie la instancia para resolver el problema.

* Si instala [!DNL Experience Manager] 6.5 Service Pack 5 o un Service Pack anterior en [!DNL Experience Manager] 6.5, se eliminará la copia de tiempo de ejecución del modelo de flujo de trabajo personalizado de recursos (creado en `/var/workflow/models/dam`).
Para recuperar la copia de tiempo de ejecución, Adobe recomienda sincronizar la copia en tiempo de diseño del modelo de flujo de trabajo personalizado con su copia de tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Si se cambia el nombre de una carpeta de la jerarquía en [!DNL Experience Manager Assets] y la carpeta anidada que contiene un recurso se publica en [!DNL Brand Portal], el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el Explorador de propiedades. Si se selecciona para configurar otro campo del formulario adaptable en el mismo editor, se resuelve el problema.

* Durante la instalación del Experience Manager 6.5.x.x pueden aparecer los siguientes errores y mensajes de advertencia:
   * &quot;Cuando la integración de Adobe Target se configura en Experience Manager mediante la API de Target Standard (autenticación IMS), la exportación de fragmentos de experiencias a Target provoca la creación de tipos de ofertas incorrectos. En lugar de tener que escribir &quot;Fragmento de experiencias&quot;/origen &quot;Adobe Experience Manager&quot;, Destino, se crean varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor del formulario adaptable falla cuando se utilizan funciones agregadas como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al previsualizar el recurso mediante el visor de banners de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tiempo de espera de que el cambio de registro se complete sin registrar.

## Los paquetes OSGi y los paquetes de contenido están incluidos {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.9.0:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.9.0](assets/6590_bundles.txt)

* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.9.0](assets/6590_packages.txt)

## Sitios web restringidos {#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* Consulte [cómo ponerse en contacto con el Servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notas de la versión 6.5](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] página de producto](https://www.adobe.com/es/marketing/experience-manager.html)
* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)

