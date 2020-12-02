---
title: Configurar orígenes de datos
seo-title: Configurar orígenes de datos
description: Obtenga información sobre cómo configurar distintos tipos de fuentes de datos y aprovechar para crear modelos de datos de formulario.
seo-description: Obtenga información sobre cómo configurar distintos tipos de fuentes de datos y aprovechar para crear modelos de datos de formulario.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 0%

---


# Configurar fuentes de datos{#configure-data-sources}

![](do-not-localize/data-integeration.png)

La integración de datos de AEM Forms le permite configurar y conectar fuentes de datos dispares. Los siguientes tipos son compatibles de forma predeterminada. Sin embargo, con poca personalización, también puede integrar otras fuentes de datos.

* Bases de datos relacionales: MySQL, Microsoft SQL Server, IBM DB2 y Oracle RDBMS
* perfil del usuario de AEM
* Servicios web RESTful
* Servicios Web basados en SOAP
* Servicios OData

La integración de datos admite los tipos de autenticación OAuth2.0, Basic Authentication y API Key predeterminados, y permite implementar la autenticación personalizada para acceder a los servicios Web. Mientras que los servicios RESTful, basados en SOAP y OData están configurados en los servicios de nube de AEM, JDBC para bases de datos relacionales y conector para AEM perfil de usuarios están configurados en AEM consola web.

## Configurar la base de datos relacional {#configure-relational-database}

Puede configurar bases de datos relacionales mediante AEM Configuración de consola web. Haga lo siguiente:

1. Vaya a AEM consola web en https://server:host/system/console/configMgr.
1. Busque la configuración de **[!UICONTROL Apache Sling Connection Pooled DataSource]**. Toque para abrir la configuración en modo de edición.
1. En el cuadro de diálogo de configuración, especifique los detalles de la base de datos que desea configurar, como:

   * Nombre del origen de datos
   * Propiedad del servicio de origen de datos que almacena el nombre del origen de datos
   * Nombre de clase Java para el controlador JDBC
   * URI de conexión JDBC
   * Nombre de usuario y contraseña para establecer la conexión con el controlador JDBC

   >[!NOTE]
   >
   >Asegúrese de cifrar información confidencial como contraseñas antes de configurar el origen de datos. Para cifrar:
   >
   >    
   >    
   >    1. Vaya a https://&#39;[server]:[port]&#39;/system/console/crypto.
   >    1. En el campo **[!UICONTROL Texto sin formato]**, especifique la contraseña o cualquier cadena que desee cifrar y toque **[!UICONTROL Protect]**.

   >    
   >    
   >    
   >El texto cifrado aparece en el campo Texto protegido que puede especificar en la configuración.

1. Habilite **[!UICONTROL Prueba en préstamo]** o **[!UICONTROL Prueba en devolución]** para especificar que los objetos se validen antes de ser tomados en préstamo o devueltos al grupo, respectivamente.
1. Especifique una consulta SQL SELECT en el campo **[!UICONTROL Consulta de validación]** para validar las conexiones del grupo. La consulta debe devolver al menos una fila. En función de la base de datos, especifique una de las siguientes opciones:

   * SELECT 1 (MySQL y MS SQL)
   * SELECT 1 from dual (Oracle)

1. Toque **[!UICONTROL Guardar]** para guardar la configuración.

## Configurar AEM perfil de usuario {#configure-aem-user-profile}

Puede configurar AEM perfil del usuario mediante la configuración del conector de Perfil del usuario en AEM consola web. Haga lo siguiente:

1. Vaya a AEM consola web en https://&#39;[server]:[port]&#39;system/console/configMgr.
1. Busque **[!UICONTROL AEM Forms Data Integrations - User Perfil Connector Configuration]** y toque para abrir la configuración en modo de edición.
1. En el cuadro de diálogo Configuración del conector de Perfil de usuario, puede agregar, quitar o actualizar las propiedades del perfil de usuario. Las propiedades especificadas estarán disponibles para su uso en el modelo de datos de formulario. Utilice el siguiente formato para especificar las propiedades de perfil del usuario:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Ejemplos:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >El ***** del ejemplo anterior indica todos los nodos bajo el nodo `profile/empLocation/` en AEM perfil de usuario en la estructura CRXDE. Significa que el modelo de datos de formulario puede acceder a la propiedad `city` de tipo `string` presente en cualquier nodo bajo el nodo `profile/empLocation/`. Sin embargo, los nodos que contienen la propiedad especificada deben seguir una estructura coherente.

1. Toque **[!UICONTROL Guardar]** para guardar la configuración.

## Configurar carpeta para configuraciones de servicios en la nube {#cloud-folder}

>[!NOTE]
La configuración de la carpeta de servicios en la nube es necesaria para configurar los servicios en la nube para los servicios RESTful, SOAP y OData.

Todas las configuraciones de servicios en la nube en AEM se consolidan en la carpeta `/conf` en AEM repositorio. De forma predeterminada, la carpeta `conf` contiene la carpeta `global` donde puede crear configuraciones de servicio en la nube. Sin embargo, debe habilitarlo manualmente para las configuraciones de nube. También puede crear carpetas adicionales en `conf` para crear y organizar configuraciones de servicio en la nube.

Para configurar la carpeta para las configuraciones del servicio en la nube:

1. Vaya a **[!UICONTROL Herramientas > General > Navegador de configuración]**.
   * Consulte la documentación de [Configuration Browser](/help/sites-administering/configurations.md) para obtener más información.
1. Haga lo siguiente para habilitar la carpeta global para las configuraciones de nube o omita este paso para crear y configurar otra carpeta para las configuraciones de servicio en la nube.

   1. En el **[!UICONTROL Explorador de configuración]**, seleccione la carpeta `global` y toque **[!UICONTROL Propiedades]**.

   1. En el cuadro de diálogo **[!UICONTROL Propiedades de configuración]**, habilite **[!UICONTROL Configuraciones de nube]**.

   1. Toque **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. En el **[!UICONTROL Explorador de configuración]**, toque **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un título para la carpeta y habilite **[!UICONTROL Configuraciones de nube]**.
1. Toque **[!UICONTROL Crear]** para crear la carpeta habilitada para las configuraciones de servicio en la nube.

## Configurar los servicios Web RESTful {#configure-restful-web-services}

El servicio web RESTful se puede describir usando [especificaciones de Swagger](https://swagger.io/specification/) en formato JSON o YAML en un archivo de definición Swagger. Para configurar el servicio web RESTful en los servicios en la nube de AEM, asegúrese de que dispone del archivo Swagger en el sistema de archivos o de la URL en la que se aloja el archivo.

Para configurar los servicios RESTful, haga lo siguiente:

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Toque para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpeta para configuraciones de servicios en la nube](../../forms/using/configure-data-sources.md#cloud-folder) para obtener información sobre cómo crear y configurar una carpeta para configuraciones de servicios en la nube.

1. Toque **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente para crear la configuración de fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio RESTful]** en la lista desplegable **[!UICONTROL Tipo de servicio]**, si lo desea, busque y seleccione una imagen en miniatura para la configuración y toque **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio RESTful:

   * Seleccione URL o archivo en el menú desplegable Origen de Swagger y, en consecuencia, especifique la URL de Swagger en el archivo de definición Swagger o cargue el archivo Swagger desde el sistema de archivos local.
   * En función de la entrada de Origen de intervalo, los siguientes campos se rellenan previamente con valores:

      * Esquema: Los protocolos de transferencia utilizados por la API de REST. El número de tipos de esquema que se muestran en la lista desplegable depende de los esquemas definidos en el origen Swagger.
      * Host: El nombre de dominio o la dirección IP del host que sirve la API de REST. Es un campo obligatorio.
      * Ruta base: Prefijo de URL para todas las rutas de API. Es un campo opcional.\
         Si es necesario, edite los valores rellenados previamente para estos campos.
   * Seleccione el tipo de autenticación — Ninguno, OAuth2.0, Autenticación básica, Clave de API, Autenticación personalizada o Autenticación mutua — para acceder al servicio RESTful y, en consecuencia, proporcionar detalles para la autenticación.

   Si selecciona **[!UICONTROL Clave de API]** como tipo de autenticación, especifique el valor de la clave de API. La clave de API se puede enviar como encabezado de solicitud o como parámetro de consulta. Seleccione una de estas opciones en la lista desplegable **[!UICONTROL Ubicación]** y especifique el nombre del encabezado o el parámetro de consulta en el campo **[!UICONTROL Nombre del parámetro]** según corresponda.

   Si selecciona **[!UICONTROL Autenticación mutua]** como tipo de autenticación, consulte [Autenticación mutua basada en certificados para servicios Web RESTful y SOAP](#mutual-authentication).

1. Toque **[!UICONTROL Crear]** para crear la configuración de nube para el servicio RESTful.

## Configurar servicios Web SOAP {#configure-soap-web-services}

Los servicios Web basados en SOAP se describen mediante [especificaciones del lenguaje de descripción de servicios Web (WSDL)](https://www.w3.org/TR/wsdl). Para configurar el servicio web basado en SOAP en los servicios de nube de AEM, asegúrese de que dispone de la URL WSDL para el servicio web y haga lo siguiente:

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Toque para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpeta para configuraciones de servicios en la nube](../../forms/using/configure-data-sources.md#cloud-folder) para obtener información sobre cómo crear y configurar una carpeta para configuraciones de servicios en la nube.

1. Toque **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente para crear la configuración de fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio Web SOAP]** en la lista desplegable **[!UICONTROL Tipo de servicio]**, si lo desea, busque y seleccione una imagen en miniatura para la configuración y toque **[!UICONTROL Siguiente]**.
1. Especifique lo siguiente para el servicio web SOAP:

   * URL WSDL para el servicio Web.
   * Punto final de servicio. Especifique un valor en este campo para anular el extremo de servicio mencionado en WSDL.
   * Seleccione el tipo de autenticación — Ninguno, OAuth2.0, Autenticación básica, Autenticación personalizada, Token X509 o Autenticación mutua — para acceder al servicio SOAP y, en consecuencia, proporcionar los detalles para la autenticación.

      Si selecciona **[!UICONTROL Token X509]** como tipo de autenticación, configure el certificado X509. Para obtener más información, consulte [Configuración de certificados](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Especifique el alias KeyStore para el certificado X509 en el campo **[!UICONTROL Alias de clave]**. Especifique el tiempo, en segundos, hasta que la solicitud de autenticación siga siendo válida en el campo **[!UICONTROL Tiempo de vida]**. Si lo desea, seleccione firmar el encabezado de la marca de tiempo o el cuerpo del mensaje o ambos.

      Si selecciona **[!UICONTROL Autenticación mutua]** como tipo de autenticación, consulte [Autenticación mutua basada en certificados para servicios Web RESTful y SOAP](#mutual-authentication).

1. Toque **[!UICONTROL Crear]** para crear la configuración de nube para el servicio Web SOAP.

## Configurar servicios OData {#config-odata}

Un servicio OData se identifica mediante su URL raíz de servicio. Para configurar un servicio OData en los servicios en la nube de AEM, asegúrese de que dispone de una URL raíz de servicio para el servicio y haga lo siguiente:

>[!NOTE]
Para obtener una guía paso a paso para configurar Microsoft Dynamics 365, en línea o en las instalaciones, consulte [Configuración de OData de Microsoft Dynamics](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Toque para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpeta para configuraciones de servicios en la nube](../../forms/using/configure-data-sources.md#cloud-folder) para obtener información sobre cómo crear y configurar una carpeta para configuraciones de servicios en la nube.

1. Toque **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente para crear la configuración de fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio OData]** en la lista desplegable **[!UICONTROL Tipo de servicio]**, si lo desea, busque y seleccione una imagen en miniatura para la configuración y toque **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio OData:

   * URL de raíz de servicio para el servicio OData que se va a configurar.
   * Seleccione el tipo de autenticación — Ninguno, OAuth2.0, Autenticación básica o Autenticación personalizada — para acceder al servicio OData y, en consecuencia, proporcionar los detalles para la autenticación.

   >[!NOTE]
   Debe seleccionar el tipo de autenticación OAuth 2.0 para conectarse con los servicios de Microsoft Dynamics mediante el extremo OData como raíz del servicio.

1. Toque **Crear** para crear la configuración de nube para el servicio OData.

## Autenticación mutua basada en certificados para servicios Web RESTful y SOAP {#mutual-authentication}

Cuando se habilita la autenticación mutua para el modelo de datos de formulario, tanto el origen de datos como AEM servidor que ejecuta el modelo de datos de formulario se autentican mutuamente antes de compartir datos. Puede utilizar la autenticación mutua para conexiones basadas en REST y SOAP (fuentes de datos). Para configurar la autenticación mutua para un modelo de datos de formulario en su entorno AEM Forms:

1. Cargue la clave privada (certificado) en el servidor [!DNL AEM Forms]. Para cargar la clave privada:
   1. Inicie sesión en el servidor [!DNL AEM Forms] como administrador.
   1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**. Seleccione el usuario `fd-cloudservice` y toque **[!UICONTROL Propiedades]**.
   1. Abra la ficha **[!UICONTROL Keystore]**, expanda la opción **[!UICONTROL Añadir clave privada del archivo KeyStore]**, cargue el archivo KeyStore, especifique los alias, las contraseñas y toque **[!UICONTROL Enviar]**. Se cargará el certificado.  El alias de clave privada se menciona en el certificado y se establece durante la creación del certificado.
1. Cargar certificado de confianza en el almacén de confianza global. Para cargar el certificado:
   1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Almacén de confianza]**.
   1. Expanda la opción **[!UICONTROL Añadir certificado del archivo CER]**, toque **[!UICONTROL Seleccionar archivo de certificado]**, cargue el certificado y toque **[!UICONTROL Enviar]**.
1. Configure los servicios Web [SOAP](#configure-soap-web-services) o [RESTful](#configure-restful-web-services) como fuente de datos y seleccione **[!UICONTROL Autenticación mutua]** como tipo de autenticación. Si configura varios certificados con firma automática para `fd-cloudservice` usuario, especifique el nombre del alias de clave para el certificado.

## Próximos pasos {#next-steps}

Ha configurado las fuentes de datos. A continuación, puede crear un modelo de datos de formulario o, si ya ha creado un modelo de datos de formulario sin un origen de datos, puede asociarlo a los orígenes de datos que acaba de configurar. Consulte [Crear modelo de datos de formulario](/help/forms/using/create-form-data-models.md) para obtener más información.
