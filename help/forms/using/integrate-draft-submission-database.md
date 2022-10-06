---
title: Ejemplo para integrar el componente Borradores y envíos con la base de datos
seo-title: Sample for integrating drafts & submissions component with database
description: Implementación de referencia de servicios personalizados de metadatos y datos para integrar borradores y componentes de envío con una base de datos.
seo-description: Reference implementation of customized data and metadata services to integrate drafts and submissions component with a database.
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
exl-id: 2e4f8f51-df02-4bbb-99bb-30181facd1e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1467'
ht-degree: 2%

---

# Ejemplo para integrar el componente Borradores y envíos con la base de datos {#sample-for-integrating-drafts-submissions-component-with-database}

## Información general de muestra {#sample-overview}

Los borradores y el componente de envíos del portal de AEM Forms permiten a los usuarios guardar sus formularios como borradores y enviarlos más tarde desde cualquier dispositivo. Además, los usuarios pueden ver los formularios enviados en el portal. Para habilitar esta funcionalidad, AEM Forms proporciona servicios de metadatos y datos para almacenar los datos rellenados por un usuario en el formulario y los metadatos de formulario asociados a borradores y formularios enviados. De forma predeterminada, estos datos se almacenan en el repositorio CRX. Sin embargo, a medida que los usuarios interactúan con los formularios a través de AEM instancia de publicación, que generalmente está fuera del firewall de la empresa, es posible que las organizaciones deseen personalizar el almacenamiento de datos para que sea más seguro y fiable.

El ejemplo, que se analiza en este documento, es una implementación de referencia de servicios personalizados de metadatos y datos para integrar borradores y componentes de presentaciones con una base de datos. La base de datos utilizada en la implementación de muestra es **MySQL 5.6.24**. Sin embargo, puede integrar el componente de borradores y envíos con cualquier base de datos de su elección.

>[!NOTE]
>
>* Los ejemplos y configuraciones explicados en este documento son de acuerdo con MySQL 5.6.24 y debe sustituirlos adecuadamente por su sistema de base de datos.
>* Asegúrese de que ha instalado la última versión del paquete de complementos de AEM Forms. Para obtener la lista de paquetes disponibles, consulte la [Versiones de AEM Forms](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) artículo.
>* El paquete de muestra solo funciona con las acciones de envío de Forms adaptable.


## Configuración del ejemplo {#set-up-and-configure-the-sample}

Realice los siguientes pasos, en todas las instancias de autor y publicación, para instalar y configurar el ejemplo:

1. Descargue lo siguiente **aem-fp-db-integration-sample-pkg-6.1.2.zip** al sistema de archivos.

   Paquete de muestra para la integración de bases de datos

[Obtener archivo](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. Vaya a AEM gestor de paquetes en https://[*host*]:[*puerto*]/crx/packmgr/.
1. Haga clic en **[!UICONTROL Cargar paquete]**.

1. Busque y seleccione **aem-fp-db-integration-sample-pkg-6.1.2.zip** paquete y haga clic en **[!UICONTROL OK]**.
1. Haga clic en **[!UICONTROL Instalar]** junto al paquete para instalar el paquete.
1. Vaya a **[!UICONTROL Configuración de AEM consola web]**
página en https://[*host*]:[*puerto*]/system/console/configMgr.
1. Haga clic para abrir **[!UICONTROL Borrador y configuración de envío del portal de Forms]** en modo de edición.

1. Especifique los valores de las propiedades tal como se describe en la tabla siguiente:

   | **Propiedad** | **Descripción** | **Valor** |
   |---|---|---|
   | Servicio de datos borrador del portal de Forms | Identificador del servicio de datos de borrador | formsportal.sampledataservice |
   | Servicio de metadatos de borrador del portal de Forms | Identificador del servicio de metadatos de borrador | formsportal.samplemetadataservice |
   | Servicio de envío de datos del portal de Forms | Identificador del servicio de envío de datos | formsportal.sampledataservice |
   | Servicio de envío de metadatos del portal de Forms | Identificador del servicio de envío de metadatos | formsportal.samplemetadataservice |
   | Servicio de datos de firma pendiente de Forms Portal | Identificador del servicio de datos de Firma pendiente | formsportal.sampledataservice |
   | Servicio de metadatos de firma pendiente de Forms Portal | Identificador del servicio de metadatos de firma pendiente | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >Los servicios se resuelven con sus nombres mencionados como valor para la variable `aem.formsportal.impl.prop` clave como se indica a continuación:

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   Puede cambiar los nombres de las tablas de datos y metadatos.

   Para proporcionar un nombre diferente para la tabla de metadatos:

   * En la Configuración de la consola web, busque y haga clic en Implementación de muestra del servicio de metadatos del portal de Forms . Puede cambiar los valores del origen de datos, los metadatos o el nombre de tabla de metadatos adicional.

   Para proporcionar un nombre diferente para la tabla de datos:

   * En la Configuración de la consola web, busque y haga clic en Implementación de muestra del servicio de datos del portal de Forms . Puede cambiar los valores del origen de datos y el nombre de la tabla de datos.
   >[!NOTE]
   >
   >Si cambia los nombres de las tablas, proporciónelos en la configuración de Form Portal.

1. Deje otras configuraciones tal cual y haga clic en **[!UICONTROL Guardar]**.

1. La conexión a la base de datos se puede realizar mediante la fuente de datos agrupada de la conexión Apache Sling.
1. Para la conexión Apache Sling, busque y haga clic para abrir **[!UICONTROL Fuente de datos obtenida de una conexión Apache Sling]** en modo de edición en la configuración de la consola web. Especifique los valores de las propiedades tal como se describe en la tabla siguiente:

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Valor</strong></td>
  </tr>
  <tr>
   <td>Nombre de la fuente de datos</td>
   <td><p>Un nombre de fuente de datos para filtrar controladores del grupo de fuentes de datos</p> <p><strong>Nota: </strong><em>La implementación de ejemplo utiliza FormsPortal como nombre de la fuente de datos.</em></p> </td>
  </tr>
  <tr>
   <td>Clase de controlador JDBC</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>URI de conexión JDBC<br /> </td>
   <td>jdbc:mysql://[<em>host</em>]:[<em>puerto</em>]/[<em>schema_name</em>]</td>
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
   <td>Conexiones máximas inactivas</td>
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
   <td>Comprobado</td>
  </tr>
  <tr>
   <td>Prueba mientras está inactiva</td>
   <td>Comprobado</td>
  </tr>
  <tr>
   <td>Consulta de validación</td>
   <td>Los valores de ejemplo son SELECT 1(mysql), select 1 from dual(oracle), SELECT 1(MS Sql Server) (validationQuery)</td>
  </tr>
  <tr>
   <td>Tiempo de espera de consulta de validación</td>
   <td>10 000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> * El controlador JDBC para MySQL no se proporciona con el ejemplo. Asegúrese de que lo ha aprovisionado y proporcione la información necesaria para configurar el grupo de conexiones JDBC.
> * Asigne instancias de autor y publicación para utilizar la misma base de datos. El valor del campo URI de conexión JDBC debe ser el mismo para todas las instancias de autor y publicación.
   >


1. Deje otras configuraciones tal cual y haga clic en **[!UICONTROL Guardar]**.

1. Si ya tiene una tabla en el esquema de la base de datos, vaya al paso siguiente.

   De lo contrario, si aún no tiene una tabla en el esquema de la base de datos, ejecute las siguientes instrucciones SQL para crear tablas independientes para datos, metadatos y metadatos adicionales en el esquema de la base de datos:

   >[!NOTE]
   >
   >No necesita bases de datos diferentes para las instancias de autor y publicación. Utilice la misma base de datos en todas las instancias de autor y publicación.

   **Instrucción SQL para la tabla de datos**

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

1. Si ya tiene las tablas (datos, metadatos y metadatos adicionales) en el esquema de base de datos, ejecute las siguientes consultas alter table:

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
   >La consulta ALTER TABLE metadata add falla si ya la ha ejecutado y la columna markedforDeletion está presente en la tabla.

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

   **Instrucción SQL para alterar la tabla de metadatos adicional**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

La implementación de muestra ya está configurada, que puede utilizar para enumerar los borradores y los envíos mientras almacena todos los datos y metadatos en una base de datos. Ahora veamos cómo se configuran los servicios de metadatos y datos en el ejemplo.

## Instale el archivo mysql-connector-java-5.1.39-bin.jar {#install-mysql-connector-java-bin-jar-file}

Realice los siguientes pasos, en todas las instancias de autor y publicación, para instalar el archivo mysql-connector-java-5.1.39-bin.jar:

1. Vaya a `https://'[server]:[port]'/system/console/depfinder` y busque el paquete com.mysql.jdbc.
1. En la columna Exportado por , compruebe si el paquete lo exporta algún paquete.

   Continúe si el paquete no se exporta mediante ningún paquete.

1. Vaya a `https://'[server]:[port]'/system/console/bundles` y haga clic en **[!UICONTROL Instalar/actualizar]**.
1. Haga clic en **[!UICONTROL Elegir archivo]** y busque para seleccionar el archivo mysql-connector-java-5.1.39-bin.jar . También, seleccione **[!UICONTROL Iniciar paquete]** y **[!UICONTROL Actualizar paquetes]** casillas de verificación.
1. Haga clic en **[!UICONTROL Instalar o actualizar]**. Una vez finalizado, reinicie el servidor.
1. (*Solo Windows*) Desactive el cortafuegos del sistema para su sistema operativo.

## Código de ejemplo para el servicio de metadatos y datos del portal de formularios {#sample-code-for-forms-portal-data-and-metadata-service}

El siguiente zip contiene `FormsPortalSampleDataServiceImpl` y `FormsPortalSampleMetadataServiceImpl` (clases de implementación) para interfaces de servicio de metadatos y datos. Además, contiene todas las clases necesarias para compilar las clases de implementación mencionadas anteriormente.

[Obtener archivo](assets/sample_package.zip)

## Comprobar la longitud del nombre del archivo  {#verify-length-of-the-file-name}

La implementación de la base de datos de Forms Portal utiliza tablas de metadatos adicionales. La tabla tiene una clave principal compuesta basada en las columnas Clave e ID de la tabla. MySQL permite claves principales de hasta 255 caracteres. Puede utilizar la siguiente secuencia de comandos de validación del lado del cliente para verificar la longitud del nombre de archivo adjunto al widget de archivos. La validación se ejecuta cuando se adjunta un archivo. La secuencia de comandos proporcionada en el siguiente procedimiento muestra un mensaje cuando el nombre del archivo es mayor que 150 (incluida la extensión). Se puede modificar la secuencia de comandos para comprobar si hay un número diferente de caracteres.

Siga los siguientes pasos para crear [una biblioteca cliente](/help/sites-developing/clientlibs.md) y utilice el script:

1. Inicie sesión en CRXDE y vaya a /etc/clientlibs/
1. Crear un nodo de tipo **cq:ClientLibraryFolder** y proporcione el nombre del nodo. Por ejemplo, `validation`.

   Haga clic en **[!UICONTROL Guardar todo]**.

1. Haga clic con el botón derecho en el nodo y haga clic en **[!UICONTROL crear nuevo archivo]** y cree un archivo con la extensión .txt. Por ejemplo, `js.txt`Agregue el siguiente código al archivo .txt recién creado y haga clic en **[!UICONTROL Guardar todo]**.

   ```javascript
   #base=util
    util.js
   ```

   En el código anterior, `util` es el nombre de la carpeta y `util.js` nombre del archivo en la variable `util` carpeta. La variable `util` carpeta y `util.js` se crean en pasos sucesivos.

1. Haga clic con el botón derecho en el `cq:ClientLibraryFolder` creado en el paso 2, seleccione Crear > Crear carpeta. Crear una carpeta con el nombre `util`. Haga clic en **[!UICONTROL Guardar todo]**. Haga clic con el botón derecho en el `util` , seleccione Crear > Crear archivo. Crear un archivo con el nombre `util.js`. Haga clic en **[!UICONTROL Guardar todo]**.

1. Agregue el siguiente código al archivo util.js y haga clic en **[!UICONTROL Guardar todo]**. El código valida la longitud del nombre del archivo.

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
   >La secuencia de comandos está diseñada para el componente del widget de archivos adjuntos predeterminado (OOTB). Si ha personalizado el widget de archivos adjuntos OOTB, cambie el script anterior para incorporar los cambios correspondientes.

1. Añada la siguiente propiedad a la carpeta creada en el paso 2 y haga clic en **[!UICONTROL Guardar todo]**.

   * **[!UICONTROL Nombre:]** categories

   * **[!UICONTROL Tipo:]** Cadena

   * **[!UICONTROL Valor:]** fp.validation

   * **[!UICONTROL multiopción:]** Habilitado

1. Vaya a `/libs/fd/af/runtime/clientlibs/guideRuntime`y añada la variable `fp.validation` a la propiedad embed .

1. Vaya a /libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA y añada la variable `fp.validation` para incrustar la propiedad.

   >[!NOTE]
   >
   >Si está utilizando bibliotecas de cliente personalizadas en lugar de las bibliotecas de cliente guideRuntime y guideRuntimeWithXfa, utilice el nombre de categoría para incrustar la biblioteca de cliente creada en este procedimiento en las bibliotecas personalizadas cargadas durante la ejecución.

1. Haga clic en **[!UICONTROL Guardar todo.]** Ahora, cuando el nombre de archivo tiene más de 150 caracteres (incluyendo la extensión), se muestra un mensaje.
