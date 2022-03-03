---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6,5
description: '"[!DNL Adobe Experience Manager] 6.5 notas que describen la información de la versión, las novedades, cómo instalar y listas de cambios detalladas."'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 37e7f2552ae712bc23eb3ce1af1b41808f4d1810
workflow-type: tm+mt
source-wordcount: '2644'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] 6.5 Últimas notas de la versión de Service Pack {#aem-service-pack-release-notes}

## Información de la versión {#release-information}

| Productos | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.12.0 |
| Tipo | Versión de Service Pack |
| Fecha | 24 de febrero de 2022 |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip) |

## ¿Qué incluye [!DNL Adobe Experience Manager] 6.5.12.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.12.0 incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras de rendimiento, estabilidad y seguridad, que se han publicado desde la publicación de la versión 6.5 en abril de 2019. El Service Pack está instalado en [!DNL Adobe Experience Manager] 6.5.

Las principales funciones y mejoras introducidas en [!DNL Adobe Experience Manager] 6.5.12.0 son:

* Después de configurar una conexión entre las implementaciones remotas de DAM y Sites, los recursos en DAM remoto están disponibles en la implementación de Sites. Ahora puede realizar las operaciones de actualización, eliminación, cambio de nombre y movimiento en los recursos o carpetas DAM remotos. Las actualizaciones, con algún retraso, están disponibles automáticamente en la implementación de Sites (NPR-37816).

* Ahora es posible, de forma predeterminada, desplegar un origen de Live Copy en varias Live Copies sin necesidad de una configuración de modelo (CQ-4259951).
* El estado de las operaciones asincrónicas en curso ahora se muestra en la interfaz de usuario para ayudar a evitar que los usuarios activen accidentalmente varias operaciones asincrónicas en la misma ruta (NPR-37611).
* Se proporciona compatibilidad con la autenticación basada en IMS para las API de Analytics 2.0 (CQ-4285474, NPR-37803, NPR-37701, NPR-37702, NPR-37703).
* Compatibilidad de API para fragmento de experiencia de tipo de oferta JSON (NPR-37796).
* La solicitud de oferta ahora se proporciona para la oferta de eliminación (API de fragmento de experiencia) en IMS (NPR-37668).
* El repositorio integrado (Apache Jackrabbit Oak) sigue en 1.22.9.

La siguiente es la lista de correcciones que se proporcionan en [!DNL Experience Manager] Versión 6.5.12.0.

### [!DNL Sites] {#sites-65120}

Los siguientes problemas se solucionan en [!DNL Sites]:

* El diseño del fragmento de contenido Propiedades se rompe porque las pestañas Básico y Avanzado no tienen márgenes a la izquierda (SITES-4484).
* La opción de cerrar el banner en los fragmentos de contenido, a los que se hace referencia en varias páginas del sitio, no funciona. Este banner informa a los usuarios de que se hace referencia al fragmento de contenido en una o más páginas (SITES-4173).
* Las casillas de verificación no están alineadas en el cuadro de diálogo Revertir herencia (SITES-3514).
* La página de plantilla de sitios web y wknd está dañada, ya que los componentes no se cargan y la opción de estructura no está disponible, ya que el servlet pageinfo.json está atascado en LaunchManagerImpl.getLaunchStream (SITES-3489).
* La publicación de nodos de usuario desde el entorno Autor a Publicación no funciona (NPR-38005).
* El intento de crear un fragmento de experiencia con una plantilla editada no muestra las ediciones realizadas en las propiedades de página iniciales (NPR-37962).
* La operación de movimiento de página en el Experience Manager es lenta (NPR-37961).
* La traducción de fragmentos de experiencias no actualiza las referencias a rutas de copia de idioma (NPR-37953).
* Los usuarios sin permisos de replicación no pueden eliminar ni mover páginas, aunque estas no estén activadas (NPR-37936).
* Los errores Random org.apache.felix.mettype se observan en el servidor (NPR-37935).
* Las referencias en la interfaz de usuario táctil del administrador de Sites no muestran correctamente los vínculos entrantes (NPR-37934).
* La ruta de inicio para añadir nuevas páginas o recursos no está disponible al seleccionar páginas en un trabajo de traducción (NPR-37912).
* Las páginas de referencia en un componente de lista añadido en fragmentos de experiencia no se actualizan a la página de destino al promocionar el lanzamiento (NPR-37886).
* El entorno de creación tiene problemas con la interfaz de usuario, como el modo de edición, el título de la página no está centrado y el selector de componentes permitido en el editor de directivas: la casilla de verificación del grupo toma todo el ancho del contenedor, por lo que la etiqueta se representa en la siguiente línea (NPR-37878).
* [Plataforma] El número de versión de xmlns:mettype en el archivo mettype.xml de commons-httpclient es &quot;http://www.osgi.org/xmlns/metatype/v1.0.0&quot; en lugar de &quot;http://www.osgi.org/xmlns/metatype/v1.2.0&quot; (NPR-37865).
* Se observan errores y las páginas no se mueven al intentar desplazarse a una página (NPR-37864).
* [Editor de texto enriquecido] La imagen no se renderiza en la interfaz de usuario clásica al añadir la imagen como un elemento de lista en el Editor de texto enriquecido (NPR-37835).
* Los autores pueden aplicar etiquetas que están fuera de la ruta raíz configurada al utilizar el campo de etiqueta en un cuadro de diálogo (NPR-37834).
* Multifield no se representa correctamente en el contenedor de diseño y da error (NPR-37811).
* El intento de cambiar el tamaño del diseño del componente en el editor de páginas no funciona en el diseño móvil (NPR-37805).
* La traducción de fragmentos de experiencias no actualiza las referencias cíclicas a las rutas de copia de idioma (NPR-37745).
* El uso de campos de texto enriquecido bloqueables para cq-msm en las propiedades de página no desactiva el campo al desplegar la página y los autores pueden modificarlo (NPR-37714).
* Al activar un fragmento de experiencia, el editor envía muchas solicitudes de activación a Dispatcher (NPR-37707).
* Al cambiar la topología, el trabajo de Sling para el procesamiento de recursos se restablece, lo que provoca que los trabajos que están en curso en el momento del cambio de topología se ignoren (NPR-37706).
* Las comillas, las cruzadas y los guiones no se exportan a CSV cuando los usuarios de MacOS exportan sitios y URL de recursos (NPR-37698).
* El contenedor de diseño de SPA plantilla de página no puede registrar las clases CSS personalizadas definidas en la directiva de plantilla al ejecutar páginas de reacción SPA (NPR-37697).
* La imagen de fondo no está visible cuando el usuario selecciona la segmentación en un fragmento de experiencia que tiene fondo en el contenedor (NPR-37662).
* El trabajo de traducción en un fragmento de experiencia no está traduciendo todos los componentes de ese fragmento de experiencia (NPR-37660).
* La traducción de fragmentos de experiencia y la página que contiene el fragmento de experiencia no actualizan la ruta de inicio en el vínculo del fragmento de experiencia (NPR-37659).
* El widget de carga de archivos no muestra el nombre del archivo, cuando se carga un archivo y se guarda el cuadro de diálogo (NPR-37634).
* La activación programada (publicación) del recurso no tiene déclencheur en la hora programada si se mueve la carpeta que contiene ese recurso (NPR-37621).
* [Plataforma] El panel del verificador de enlaces externo no procesa los resultados en [!DNL Adobe Experience Manager] WCM (NPR-37614).
* El editor de fragmentos de contenido no funciona correctamente cuando se utilizan mayúsculas y minúsculas en los nombres de etiquetas al editar etiquetas en el editor (NPR-37601).
* El editor de interfaz de usuario clásico no aparece marcado como en la vista comparada de la interfaz de usuario táctil (NPR-37588).
* El error 500 intermitente se registra al añadir un fragmento de experiencia a los trabajos de traducción (NPR-37587).
* Los autores pueden seleccionar y utilizar la fecha del selector de fechas incluso en el selector de fechas desactivado (NPR-37583).
* [Foundation] Los autores no pueden introducir algunos valores decimales en el tipo de recurso de campo numérico en una estructura de diálogo de componente para la interfaz de usuario táctil (NPR-37059).
* Las rutas de la carpeta libs se eliminan al instalar los service packs anteriores (NPR-36815).
* [Comercio] La desactivación de una carpeta raíz no cambia el estado de desactivación de los productos secundarios en [!DNL Experience Manager Commerce] consola; además, el recuento de carpetas secundarias de una carpeta raíz en el momento de la desactivación se muestra incorrectamente en la interfaz de usuario (CQ-4338261).
* [Flujo de trabajo de localización] El contenido para la personalización de columnas y marcas no está localizado en el cuadro de diálogo Control de administración (al seleccionar el icono debajo del icono de perfil en [!DNL Adobe Experience Manager] bandeja de entrada (CQ-4334864).
* [Comunidades] No se puede hacer clic en el contenido de la tabla para los miembros del grupo (CQ-4334404).
* [Oak] El proceso de sincronización en espera pasiva no funciona y está registrando un error (CQ-4333868).
* [Interfaz de usuario de Platform Foundation] [!DNL Experience Manager] la página de inicio vuelve a aparecer cuando el usuario selecciona [!DNL Adobe Experience Manager] ya se encuentra en la página de inicio (CQ-4317409).

### [!DNL Assets] {#assets-65120}

<!--
The following accessibility enhancements are available in [!DNL Assets]:

* enhancement 1
-->

Los siguientes problemas se solucionan en [!DNL Assets]:

* Al añadir un recurso o una carpeta (contiene `single quote` en el nombre) de Recursos conectados, la ruta de referencia falla y resulta como una excepción (NPR-37712).
* Al agregar una marca de agua a un recurso, la marca de agua siempre se muestra en color negro independientemente del color definido por el usuario (NPR-37720).
* Cuando se utilizan recursos conectados, un usuario no administrador puede buscar un recurso aunque los usuarios no administradores estén restringidos para acceder al repositorio DAM (NPR-37644).
* Al actualizar los metadatos de recursos mediante la edición masiva, los cambios aplicados a los campos desplegables no se guardan y se restablecen a los valores predeterminados (NPR-37345).
* Al eliminar una carpeta, se tarda demasiado tiempo, lo que afecta al rendimiento general (NPR-37107).
* Al aplicar reglas en el esquema de metadatos, el usuario no puede ver el valor completo de la lista desplegable `Field Value` y `Field Choices` si el valor es mayor que el cuadro de texto (CQ-4338074).
* Después de actualizar a la versión 6.5.10.0, la página de propiedades del recurso refleja un mensaje de procesamiento de HTML innecesario (CQ-4336994).
* Clasificación de los recursos en `List View` no funciona de forma eficaz (CQ-4335298).
* Al compartir recursos mediante el vínculo de uso compartido, los recursos se descargan en carpetas independientes (CQ-4335000).
* Al verificar el [!DNL Experience Manager] `Inbox` configuración, la variable `Share` y `Out of office` las pestañas reflejan el contenido no traducido (CQ-4334858).

* Las siguientes correcciones están relacionadas con los metadatos en cascada de las propiedades de los recursos.
   * Un menú desplegable obligatorio refleja varios mensajes de error para cada selección del campo multivalor (NPR-37859).
   * Solo la última selección del campo principal se guarda para el campo dependiente no editable (NPR-37858).
   * La lista desplegable dependiente (campo multivalor) refleja el valor predeterminado de forma intermitente para la lista desplegable principal seleccionada (NPR-37791).


### [!DNL Dynamic Media] {#dynamic-media-65120}

Los siguientes problemas se solucionan en [!DNL Dynamic Media]:

* Los recursos de una carpeta que contienen `renditions` en el nombre de la carpeta no se sincronizan en `Dynamic Media` (CQ-4338428).
* Al crear un ajuste preestablecido de imagen en `tiff` , se crea el ajuste preestablecido, pero el formato cambia a `jpeg` (CQ-4335985).
* Al modificar el `Progressive JPEG Scan` en el Editor de ajustes preestablecidos de imagen, el valor desplegable siempre se restablece como `auto`(CQ-4335971).
* Los metadatos de vídeo no están visibles para la variable `mxf` vídeos en la página de propiedades de recursos (CQ-4335499).
* Al reprocesar los recursos de vídeo, se cancela la publicación de AVS (Conjunto de vídeos adaptables) y de las representaciones de vídeo desde el servidor de publicación (CQ-4335461).
* Las miniaturas de PDF generadas son diferentes de la primera página del PDF real. Faltan algunas partes de la imagen en la miniatura (CQ-4315554).
* La invalidación de CDN falla con una respuesta URL incorrecta si la variable `companyName` y `companyRoot` son diferentes (CQ-4339896).

### Flujos de trabajo {#workflows-65120}

* El desplazamiento no funciona como se espera si aplica el filtro en los elementos de la bandeja de entrada (CQ-433594).


### [!DNL Forms] {#forms-65120}


>[!NOTE]
>
>* [!DNL Experience Manager Forms] lanza los paquetes de complementos una semana después de la fecha de lanzamiento programada del paquete de servicio de [!DNL Experience Manager].


<!--

**Adaptive Forms**

* Accessibility – When you set the `Wizard` layout for a panel in an adaptive form, the navigation buttons do not have Aria labels and role (NPR-37613).

* Validations on a date field in an adaptive form does not work, as expected (NPR-37556).

* When the label text for the Checkbox and Radio Button components is long, the text does not fit appropriately (NPR-37294).

* When you apply styling changes to the Thank You message of the AEM Forms Container component, the changes do not replicate in the source adaptive form (NPR-37284).

* Differences in the value of the `Switch` component on the user interface and in the backend (NPR-37268).

* When you use the keyboard keys to navigate to the `Submit` option and press the `Enter` key, you can submit the adaptive form multiple times (CQ-4333993).

* The Remove operation for the File Attachment component does not work, as expected (NPR-37376).

* When a label for a field exceeds 1000 characters in an adaptive form that translates to various languages, the dictionary fails to retrieve the translation of the label (CQ-4329290).

**Document Services**

* An error displays while using the Assembler service (NPR-37606):

  ```TXT
    500 Internal Server Error
  ```

* When the document attachments are passed to the Assembler service, the following exception displays (NPR-37582):

  ```TXT
    com.adobe.livecycle.assembler.client.ProcessingException: ⁪: Failed to execute the DDX
  ```

* Missing closing parenthesis from data after converting a PDF document to a PDF-A/1B PDF document (NPR-37608).

**HTML5 Forms**

* When you install AEM 6.5.10.0, the HTML preview for an XDP form does not work (NPR-37503, CQ-4331926).

* Text overlapping issues while migrating the PDF forms to HTML 5 forms in various languages (NPR-37173).

**Letters**

* When you submit a letter and reopen it in HTML view, the position of text document fragments does not remain the same (NPR-37307).

**Forms Workflow**

* In case of embedded container workflow, you get multiple workflow completion emails even after selecting the `Notify on Complete of Container Workflow` option (NPR-37280).

**Foundation JEE**

* After installing AEM 6.5 Forms Service Pack 9, the CRX repository URLs are no longer available (NPR-37592).

**Issues fixed in AEM Forms 6.5.11.1**

>[!NOTE]
>
>If you have not upgraded to AEM 6.5.11.0 Forms, install the AEM Forms 6.5.11.1 add-on package directly. If you have installed AEM 6.5.11.0 Forms, Adobe recommends to upgrade to AEM 6.5.11.1 Forms.

* Submit actions, Send Email and Invoke an AEM Workflow stop working after installing the Forms 6.5.11.0 add-on package.
* CreatePDF operation stops converting Microsoft Word documents to PDF documents after installing the Forms 6.5.11.0 add-on package.
* (JEE Only) Critical security vulnerabilities (CVE-2021-44228 and CVE-2021-45046) reported for Apache Log4j2.
* (JEE only) Assembler DSC in 6.5.11.0 patch contains incorrect metainfo like specification version and impl version.

-->


Para obtener información sobre las actualizaciones de seguridad, consulte [[!DNL Experience Manager] página boletines de seguridad](https://helpx.adobe.com/security/products/experience-manager.html).

## Instalar 6.5.12.0 {#install}

**Requisitos de configuración y más información**

* El Experience Manager 6.5.12.0 requiere el Experience Manager 6.5. Consulte [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas.
* La descarga del Service Pack está disponible en Adobe [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).
* En una implementación con MongoDB y varias instancias, instale el Experience Manager 6.5.12.0 en una de las instancias de creación mediante el Administrador de paquetes.

>[!NOTE]
>
>El Adobe no recomienda quitar o desinstalar el [!DNL Adobe Experience Manager] Paquete 6.5.12.0.

### Instalación del Service Pack {#install-service-pack}

Para instalar el Service Pack en un [!DNL Adobe Experience Manager] 6.5, siga estos pasos:

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se actualizó desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de la instalación, tome una instantánea o una copia de seguridad nueva de su [!DNL Experience Manager] instancia.

1. Descargue el Service Pack desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip).

1. Abra Administrador de paquetes y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de instalar el Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacenamiento de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del Administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que las instalaciones se realizan correctamente. Normalmente, este problema ocurre en [!DNL Safari] pero puede ocurrir de forma intermitente en cualquier explorador.

**Instalación automática**

Hay dos maneras de instalar automáticamente [!DNL Experience Manager] 6.5.12.0 en un caso de trabajo:

A. Coloque el paquete en `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.

B. Utilice la variable [API HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para que se instalen los paquetes anidados.

>[!NOTE]
>
>Adobe Experience Manager 6.5.12.0 no es compatible con la instalación del Bootstrap.

**Validar la instalación**

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.12.0)` under [!UICONTROL Productos instalados].

1. Todos los paquetes OSGi son: **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.3 o posterior (utilice la consola web: `/system/console/bundles`).

Para saber cuáles son las plataformas certificadas para funcionar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

<!-- 

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

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

El UberJar para Experience Manager 6.5.12.0 está disponible en el [Repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.12/).

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.12</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar y los otros artefactos relacionados están disponibles en el Repositorio Central de Maven en lugar del Repositorio de Maven Público de Adobe (`repo.adobe.com`). Se cambia el nombre del archivo UberJar principal a `uber-jar-<version>.jar`. Así que no hay `classifier`, con `apis` como valor, para la variable `dependency` etiqueta.

## Funciones en desuso {#removed-deprecated-features}

A continuación se muestra una lista de funciones y capacidades que están marcadas como obsoletas con [!DNL Experience Manager] 6.5.7.0. Las funciones se marcan como obsoletas inicialmente y después se eliminan en una versión futura. Se proporciona una opción alternativa.

Revise si utiliza una función o una capacidad en una implementación. Además, planifique cambiar la implementación para utilizar una opción alternativa.

| Área | Función | Reemplazo |
|---|---|---|
| Integraciones | La variable **[!UICONTROL Inclusión de AEM Cloud Services]** ya que la función [!DNL Experience Manager] y [!DNL Adobe Target] se ha actualizado en Experience Manager 6.5. La integración es compatible con la API de Adobe Target Standard. La API utiliza la autenticación mediante Adobe IMS y [!DNL Adobe I/O] y apoya el papel cada vez más importante que desempeña Adobe Launch en la instrumentación [!DNL Experience Manager] páginas para analytics y personalización, el asistente de inclusión es funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y [!DNL Adobe I/O] integraciones a través de las [!DNL Experience Manager] servicios en la nube. |
| Conectores | El conector JCR de Adobe para Microsoft® SharePoint 2010 y Microsoft® SharePoint 2013 está obsoleto para el Experience Manager 6.5. | N/D |

## Problemas conocidos {#known-issues}

* Si utiliza fragmentos de contenido y GraphQL, se recomienda instalar los siguientes paquetes sobre la versión 6.5.12.0:

   * [AEM 6.5.12 HotFix-NPR-38144](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip)

   * [AEM fragmento de contenido con el paquete de índice 1.0.4 de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.4.zip)

* Como [!DNL Microsoft Windows Server 2019] no es compatible [!DNL MySQL 5.7] y [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] no admite instalaciones llave en mano para [!DNL AEM Forms 6.5.10.0].

* Si actualiza su [!DNL Experience Manager] de la versión 6.5 a la versión 6.5.10.0, puede ver `RRD4JReporter` las excepciones de `error.log` archivo. Para resolver el problema, reinicie la instancia.

* Si instala [!DNL Experience Manager] 6.5 Service Pack 10 o un Service Pack anterior en [!DNL Experience Manager] 6.5, la copia en tiempo de ejecución del modelo de flujo de trabajo personalizado de recursos (creado en `/var/workflow/models/dam`).
Para recuperar la copia de tiempo de ejecución, Adobe recomienda sincronizar la copia en tiempo de diseño del modelo de flujo de trabajo personalizado con su copia de tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Los usuarios pueden cambiar el nombre de una carpeta de una jerarquía [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el Explorador de propiedades. Si se selecciona para configurar otro campo del formulario adaptable en el mismo editor, se resuelve el problema.

* Durante la instalación del Experience Manager 6.5.x.x pueden aparecer los siguientes errores y mensajes de advertencia:
   * &quot;Cuando la integración de Adobe Target se configura en Experience Manager mediante la API de Target Standard (autenticación IMS), la exportación de fragmentos de experiencias a Target provoca la creación de tipos de ofertas incorrectos. En lugar de tener que escribir &quot;Fragmento de experiencias&quot;/origen &quot;Adobe Experience Manager&quot;, Destino, se crean varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor del formulario adaptable falla cuando se utilizan funciones agregadas como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al previsualizar el recurso mediante el visor de banners de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tiempo de espera de que el cambio de registro se complete sin registrar.

* Al intentar mover, eliminar o publicar fragmentos de contenido o sitios o páginas, hay un problema cuando se recuperan referencias de fragmentos de contenido, ya que la consulta en segundo plano falla; es decir, la funcionalidad no funciona.
Para garantizar la operación correcta, debe añadir las siguientes propiedades al nodo de definición de índice `/oak:index/damAssetLucene` (no se requiere reindexación) :

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Paquetes de contenido y paquetes OSGi incluidos {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.12.0:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.12.0](assets/65120_bundles.txt)

* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.12.0](assets/65120_packages.txt)

## Sitios web restringidos {#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* Consulte [cómo ponerse en contacto con el servicio de asistencia al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
>* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)

