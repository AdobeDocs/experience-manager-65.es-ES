---
title: Ejemplo para integrar el componente de borradores y envíos con la base de datos
seo-title: Ejemplo para integrar el componente de borradores y envíos con la base de datos
description: Implementación de referencia de servicios personalizados de metadatos y datos para integrar borradores y componentes de envíos con una base de datos.
seo-description: Implementación de referencia de servicios personalizados de metadatos y datos para integrar borradores y componentes de envíos con una base de datos.
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 1%

---


# Ejemplo para integrar el componente de borradores y envíos con la base de datos {#sample-for-integrating-drafts-submissions-component-with-database}

## Información general de muestra {#sample-overview}

Los borradores y el componente de envíos del portal de AEM Forms permiten a los usuarios guardar los formularios como borradores y enviarlos posteriormente desde cualquier dispositivo. Además, los usuarios pueden vista los formularios enviados en el portal. Para habilitar esta funcionalidad, AEM Forms proporciona servicios de datos y metadatos para almacenar los datos rellenados por un usuario en el formulario y los metadatos del formulario asociados con borradores y formularios enviados. De forma predeterminada, estos datos se almacenan en el repositorio de CRX. Sin embargo, a medida que los usuarios interactúan con los formularios a través de AEM instancia de publicación, que generalmente está fuera del servidor de seguridad de la empresa, es posible que las organizaciones deseen personalizar el almacenamiento de datos para que sea más seguro y fiable.

La muestra, analizada en este documento, es una implementación de referencia de servicios personalizados de metadatos y datos para integrar borradores y componentes de envíos con una base de datos. La base de datos utilizada en la implementación de muestra es **MySQL 5.6.24**. Sin embargo, puede integrar el componente de borradores y envíos con cualquier base de datos que desee.

>[!NOTE]
>
>* Los ejemplos y las configuraciones explicadas en este documento son de acuerdo con MySQL 5.6.24 y usted debe sustituirlos apropiadamente por su sistema de base de datos.
>* Asegúrese de que ha instalado la versión más reciente del paquete de complementos de AEM Forms. Para ver la lista de los paquetes disponibles, consulte el artículo [AEM Forms releases](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html).
>* El paquete de muestra solo funciona con acciones de envío de Forms adaptable.


## Configure y configure el ejemplo {#set-up-and-configure-the-sample}

Realice los siguientes pasos, en todas las instancias de creación y publicación, para instalar y configurar el ejemplo:

1. Descargue el siguiente paquete **aem-fp-db-integration-sample-pkg-6.1.2.zip** en su sistema de archivos.

   Paquete de muestra para la integración de bases de datos

   [Obtener archivo](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Vaya a AEM administrador de paquetes en https://[*host*]:[*puerto*]/crx/packmgr/.
1. Haga clic en **[!UICONTROL Cargar paquete]**.

1. Busque y seleccione el paquete **aem-fp-db-integration-sample-pkg-6.1.2.zip** y haga clic en **[!UICONTROL Aceptar]**.
1. Haga clic en **[!UICONTROL Instalar]** al lado del paquete para instalar el paquete.
1. Vaya a **[!UICONTROL Configuración de la consola web de AEM]**
página en https://[*host*]:[*puerto*]/system/console/configMgr.
1. Haga clic para abrir **[!UICONTROL Forms Portal Draft and Submission Configuration]** en modo de edición.

1. Especifique los valores de las propiedades como se describe en la tabla siguiente:

   | **Propiedad** | **Descripción** | **Value** |
   |---|---|---|
   | Servicio de datos de borrador de Forms Portal | Identificador del servicio de datos de borrador | formsportal.sampledataservice |
   | Servicio de metadatos de borrador de Forms Portal | Identificador del servicio de metadatos de borrador | formsportal.samplemetadataservice |
   | Servicio de envío de datos de Forms Portal | Identificador para enviar el servicio de datos | formsportal.sampledataservice |
   | Servicio de envío de metadatos de Forms Portal | Identificador del servicio de metadatos de envío | formsportal.samplemetadataservice |
   | Servicio de datos de firma pendiente de Forms Portal | Identificador del servicio de datos de firma pendiente | formsportal.sampledataservice |
   | Servicio de metadatos de firma pendiente de Forms Portal | Identificador del servicio de metadatos Firma pendiente | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >Los servicios se resuelven con sus nombres mencionados como valor para la clave `aem.formsportal.impl.prop` de la siguiente manera:

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   Puede cambiar los nombres de las tablas de datos y metadatos.

   Para proporcionar un nombre diferente para la tabla de metadatos:

   * En Configuración de la consola web, busque y haga clic en Implementación de muestra del servicio de metadatos de Forms Portal. Puede cambiar los valores del origen de datos, los metadatos o el nombre de tabla de metadatos adicional.

   Para proporcionar un nombre diferente para la tabla de datos:

   * En Configuración de la consola web, busque y haga clic en Implementación de muestra del servicio de datos del portal de Forms. Puede cambiar los valores del origen de datos y el nombre de la tabla de datos.
   >[!NOTE]
   >
   >Si cambia los nombres de tabla, indíquelos en la configuración de Form Portal.

1. Deje otras configuraciones tal cual y haga clic en **[!UICONTROL Guardar]**.

1. La conexión a la base de datos se puede realizar a través de Apache Sling Connection Pooled Data Source.
1. Para la conexión Apache Sling, busque y haga clic para abrir **[!UICONTROL Apache Sling Connection Pooled DataSource]** en modo de edición en la Configuración de la consola web. Especifique los valores de las propiedades como se describe en la tabla siguiente:

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Value</strong></td>
  </tr>
  <tr>
   <td>Nombre del origen de datos</td>
   <td><p>Nombre de fuente de datos para filtrar controladores del grupo de fuentes de datos</p> <p><strong>Nota:  </strong><em>La implementación de ejemplo utiliza FormsPortal como nombre del origen de datos.</em></p> </td>
  </tr>
  <tr>
   <td>Clase de controlador JDBC</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>URI de conexión JDBC<br /> </td>
   <td>jdbc:mysql://[<em>host</em>]:[<em>puerto</em>]/[<em>nombre_esquema</em>]</td>
  </tr>
  <tr>
   <td>Nombre de usuario</td>
   <td>Un nombre de usuario para autenticar y realizar acciones en tablas de base de datos</td>
  </tr>
  <tr>
   <td>Contraseña</td>
   <td>Contraseña asociada al nombre de usuario</td>
  </tr>
  <tr>
   <td>Aislamiento de transacciones</td>
   <td>READ_COMMITTED</td>
  </tr>
  <tr>
   <td>Máximo de conexiones activas</td>
   <td>1000</td>
  </tr>
  <tr>
   <td>Máximo de conexiones inactivas</td>
   <td>100</td>
  </tr>
  <tr>
   <td>Conexiones mínimas inactivas</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Tamaño inicial</td>
   <td>10</td>
  </tr>
  <tr>
   <td>Espera máxima</td>
   <td>100 000</td>
  </tr>
  <tr>
   <td>Prueba a la vista previa</td>
   <td>Activados</td>
  </tr>
  <tr>
   <td>Probar mientras está inactivo</td>
   <td>Activados</td>
  </tr>
  <tr>
   <td>Consulta de validación</td>
   <td>Los valores de ejemplo son SELECT 1(mysql), select 1 from dual(oracle), SELECT 1(MS Sql Server) (validationQuery)</td>
  </tr>
  <tr>
   <td>Tiempo de espera de Consulta de validación</td>
   <td>10 000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> * El controlador JDBC para MySQL no se proporciona con el ejemplo. Asegúrese de haberla aprovisionado y proporcione la información necesaria para configurar el grupo de conexiones JDBC.
> * Elija las instancias de autor y publicación para utilizar la misma base de datos. El valor del campo URI de conexión JDBC debe ser el mismo para todas las instancias de creación y publicación.

>



1. Deje otras configuraciones tal cual y haga clic en **[!UICONTROL Guardar]**.

1. Si ya tiene una tabla en el esquema de la base de datos, vaya al paso siguiente.

   De lo contrario, si aún no tiene una tabla en el esquema de la base de datos, ejecute las siguientes sentencias SQL para crear tablas independientes para datos, metadatos y metadatos adicionales en el esquema de la base de datos:

   >[!NOTE]
   >
   >No se requieren bases de datos diferentes para las instancias de creación y publicación. Utilice la misma base de datos en todas las instancias de creación y publicación.

   **Instrucción SQL para tabla de datos**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Instrucción SQL para tabla de metadatos**

   ```sql
   CREATE TABLE `metadata` (
   `formPath` varchar(1000) DEFAULT NULL,
   `formType` varchar(100) DEFAULT NULL,
   `description` text,
   `formName` varchar(255) DEFAULT NULL,
   `owner` varchar(255) DEFAULT NULL,
   `enableAnonymousSave` varchar(45) DEFAULT NULL,
   `renderPath` varchar(1000) DEFAULT NULL,
   `nodeType` varchar(45) DEFAULT NULL,
   `charset` varchar(45) DEFAULT NULL,
   `userdataID` varchar(45) DEFAULT NULL,
   `status` varchar(45) DEFAULT NULL,
   `formmodel` varchar(45) DEFAULT NULL,
   `markedForDeletion` varchar(45) DEFAULT NULL,
   `showDorClass` varchar(255) DEFAULT NULL,
   `sling:resourceType` varchar(1000) DEFAULT NULL,
   `attachmentList` longtext,
   `draftID` varchar(45) DEFAULT NULL,
   `submitID` varchar(45) DEFAULT NULL,
   `id` varchar(60) NOT NULL,
   `profile` varchar(255) DEFAULT NULL,
   `submitUrl` varchar(1000) DEFAULT NULL,
   `xdpRef` varchar(1000) DEFAULT NULL,
   `agreementId` varchar(255) DEFAULT NULL,
   `nextSigners` varchar(255) DEFAULT NULL,
   `eSignStatus` varchar(45) DEFAULT NULL,
   `pendingSignID` varchar(45) DEFAULT NULL,
   `agreementDataId` varchar(255) DEFAULT NULL,
   `enablePortalSubmit` varchar(45) DEFAULT NULL,
   `submitType` varchar(45) DEFAULT NULL,
   `dataType` varchar(45) DEFAULT NULL,
   `jcr:lastModified` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`id`),
   UNIQUE KEY `ID_UNIQUE` (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Instrucción SQL para metadatos adicionales**

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **Instrucción SQL para tabla de comentarios**

   ```sql
   CREATE TABLE `commenttable` (
   `commentId` varchar(255) DEFAULT NULL,
   `comment` text DEFAULT NULL,
   `ID` varchar(255) DEFAULT NULL,
   `commentowner` varchar(255) DEFAULT NULL,
   `time` varchar(255) DEFAULT NULL);
   ```

1. Si ya tiene las tablas (datos, metadatos y metadatos adicionales) en el esquema de la base de datos, ejecute las siguientes consultas de tabla de modificación:

   **Instrucción SQL para modificar la tabla de datos**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **Instrucción SQL para modificar la tabla de metadatos**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >La consulta de adición de metadatos ALTER TABLE falla si ya la ha ejecutado y la columna markedforDelection está presente en la tabla.

   ```sql
   ALTER TABLE metadata add agreementId varchar(255) DEFAULT NULL,
   add nextSigners varchar(255) DEFAULT NULL,
   add eSignStatus varchar(45) DEFAULT NULL,
   add pendingSignID varchar(45) DEFAULT NULL,
   add agreementDataId varchar(255) DEFAULT NULL,
   add enablePortalSubmit varchar(45) DEFAULT NULL,
   add submitType varchar(45) DEFAULT NULL,
   add dataType varchar(45) DEFAULT NULL;
   ```

   ```sql
   ALTER TABLE `metadata` CHANGE `formPath` `formPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formType` `formType` VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `description` `description` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formName` `formName` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `renderPath` `renderPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `showDorClass` `showDorClass` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `sling:resourceType` `sling:resourceType` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `profile` `profile` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `submitUrl` `submitUrl` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `xdpRef` `xdpRef` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **Instrucción SQL para modificar la tabla adicional de metadatos**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

La implementación de muestra ya está configurada, que puede utilizar para lista de borradores y envíos mientras almacena todos los datos y metadatos en una base de datos. Ahora veremos cómo se configuran los servicios de metadatos y datos en el ejemplo.

## Instale el archivo mysql-Connector-java-5.1.39-bin.jar {#install-mysql-connector-java-bin-jar-file}

Realice los siguientes pasos, en todas las instancias de creación y publicación, para instalar el archivo mysql-Connector-java-5.1.39-bin.jar:

1. Vaya a `https://'[server]:[port]'/system/console/depfinder` y busque el paquete com.mysql.jdbc.
1. En la columna Exportado por, compruebe si el paquete lo exporta cualquier paquete.

   Proceda si el paquete no se exporta mediante ningún paquete.

1. Vaya a `https://'[server]:[port]'/system/console/bundles` y haga clic en **[!UICONTROL Instalar/Actualizar]**.
1. Haga clic en **[!UICONTROL Elija Archivo]** y busque para seleccionar el archivo mysql-Connector-java-5.1.39-bin.jar. Además, seleccione las casillas **[!UICONTROL Paquete de Inicio]** y **[!UICONTROL Actualizar paquetes]**.
1. Haga clic en **[!UICONTROL Instalar o Actualizar]**. Una vez finalizado, reinicie el servidor.
1. (*Solo Windows*) Desactive el cortafuegos del sistema para su sistema operativo.

## Código de ejemplo para el servicio de metadatos y datos del portal de formularios {#sample-code-for-forms-portal-data-and-metadata-service}

El siguiente zip contiene `FormsPortalSampleDataServiceImpl` y `FormsPortalSampleMetadataServiceImpl` (clases de implementación) para interfaces de servicio de datos y metadatos. Además, contiene todas las clases requeridas para la compilación de las clases de implementación antes mencionadas.

[Obtener archivo](assets/sample_package.zip)

## Verificar la longitud del nombre de archivo {#verify-length-of-the-file-name}

La implementación de la base de datos de Forms Portal utiliza una tabla de metadatos adicional. La tabla tiene una clave principal compuesta basada en las columnas Clave e ID de la tabla. MySQL permite claves primarias de hasta 255 caracteres. Puede utilizar la siguiente secuencia de comandos de validación del lado del cliente para comprobar la longitud del nombre de archivo adjunto al widget de archivo. La validación se ejecuta cuando se adjunta un archivo. La secuencia de comandos proporcionada en el siguiente procedimiento muestra un mensaje cuando el nombre del archivo es mayor que 150 (incluida la extensión). Puede modificar la secuencia de comandos para comprobar si hay un número diferente de caracteres.

Siga los pasos siguientes para crear [una biblioteca de cliente](/help/sites-developing/clientlibs.md) y utilizar la secuencia de comandos:

1. Inicie sesión en CRXDE y vaya a /etc/clientlibs/
1. Cree un nodo de tipo **cq:ClientLibraryFolder** y proporcione el nombre del nodo. Por ejemplo, `validation`.

   Haga clic en **[!UICONTROL Guardar todo]**.

1. Haga clic con el botón secundario en el nodo, haga clic en **[!UICONTROL crear un nuevo archivo]** y cree un archivo con la extensión .txt. Por ejemplo, `js.txt`Añada el siguiente código al archivo .txt recién creado y haga clic en **[!UICONTROL Guardar todo]**.

   ```javascript
   #base=util
    util.js
   ```

   En el código anterior, `util` es el nombre de la carpeta y `util.js` el nombre del archivo en la carpeta `util`. La carpeta `util` y el archivo `util.js` se crean en los pasos siguientes.

1. Haga clic con el botón derecho en el nodo `cq:ClientLibraryFolder` creado en el paso 2, seleccione Crear > Crear carpeta. Cree una carpeta con el nombre `util`. Haga clic en **[!UICONTROL Guardar todo]**. Haga clic con el botón derecho en la carpeta `util` y seleccione Crear > Crear archivo. Cree un archivo denominado `util.js`. Haga clic en **[!UICONTROL Guardar todo]**.

1. Añada el siguiente código al archivo util.js y haga clic en **[!UICONTROL Guardar todo]**. El código valida la longitud del nombre del archivo.

   ```javascript
   /*
    * ADOBE CONFIDENTIAL
    * ___________________
    *
    * Copyright 2016 Adobe Systems Incorporated
    * All Rights Reserved.
    *
    * NOTICE:  All information contained herein is, and remains
    * the property of Adobe Systems Incorporated and its suppliers,
    * if any.  The intellectual and technical concepts contained
    * herein are proprietary to Adobe Systems Incorporated and its
    * suppliers and may be covered by U.S. and Foreign Patents,
    * patents in process, and are protected by trade secret or copyright law.
    * Dissemination of this information or reproduction of this material
    * is strictly forbidden unless prior written permission is obtained
    * from Adobe Systems Incorporated.
    *
    */
   (function () {
       var connectWithGuideBridge = function (gb) {
           gb.connect(function () {
               //For first time load
               window.guideBridge.on("elementValueChanged" , function(event, payload) {
           var component = payload.target; // Field whose value has changed
                   if(component.name == 'fileAttachment' && component.parent) {
                       var fileItems = $('#'+payload.target.parent.id).find(".guide-fu-fileItem");
                       for (i = 0;i<fileItems.length;i++) {
                           var filename = $(fileItems[i]).find(".guide-fu-fileName").text();
                           //check whether it is previously attached file or a newly  attached one
                           if(filename.length > 150 && filename.indexOf("fp.attach.jsp") < 0) {
                               window.alert("filename is larger than 150 : "+filename);
                                $(fileItems[i]).find(".guide-fu-fileClose.close").click();
                           }
                       }
                   }
   
      });
           });
       };
   
       if (window.guideBridge) {
           connectWithGuideBridge(window.guideBridge);
       } else {
           window.addEventListener("bridgeInitializeStart", function (event) {
               connectWithGuideBridge(event.detail.guideBridge);
           });
       }
   })();
   ```

   >[!NOTE]
   >
   >La secuencia de comandos está diseñada para el componente del widget de datos adjuntos (OOTB) listo para usar. Si ha personalizado la utilidad de datos adjuntos OOTB, cambie la secuencia de comandos anterior para incorporar los cambios correspondientes.

1. Añada la siguiente propiedad a la carpeta creada en el paso 2 y haga clic en **[!UICONTROL Guardar todo]**.

   * **[!UICONTROL Nombre:]** categorías

   * **[!UICONTROL Tipo:]** Cadena

   * **[!UICONTROL Valor:]** fp.validation

   * **[!UICONTROL opción múltiple:]** activado

1. Vaya a `/libs/fd/af/runtime/clientlibs/guideRuntime`y anexe el valor `fp.validation` a la propiedad embed.

1. Vaya a /libs/fd/af/Runtime/clientlibs/guideRuntimeWithXFA y anexe el valor `fp.validation` a la propiedad embed.

   >[!NOTE]
   >
   >Si utiliza bibliotecas de cliente personalizadas en lugar de las bibliotecas de cliente guideRuntime y guideRuntimeWithXfa, utilice el nombre de categoría para incrustar la biblioteca de cliente creada en este procedimiento en las bibliotecas personalizadas cargadas durante la ejecución.

1. Haga clic en **[!UICONTROL Guardar todo.]** Ahora, cuando el nombre de archivo es mayor que 150 caracteres (incluida la extensión), se muestra un mensaje.

