---
title: Configuración de fuentes de datos
seo-title: Configure data sources
description: Aprenda a configurar diferentes tipos de fuentes de datos y aproveche para crear modelos de datos de formulario.
seo-description: Learn how to configure different types of data sources and leverage to create form data models.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
source-git-commit: 98854fa3b852f511cf95adc13b945c06b1afff96
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 1%

---

# Configuración de fuentes de datos{#configure-data-sources}

![](do-not-localize/data-integeration.png)

La integración de datos de AEM Forms le permite configurar y conectarse a fuentes de datos diferentes. Los siguientes tipos son compatibles de serie. Sin embargo, con poca personalización, también puede integrar otras fuentes de datos.

* Bases de datos relacionales: MySQL, Microsoft SQL Server, IBM DB2, Oracle RDBMS y Sybase
* AEM perfil de usuario
* Servicios web RESTful
* Servicios web basados en SOAP
* Servicios OData

La integración de datos es compatible con los tipos de autenticación OAuth2.0, Autenticación básica y API Key de serie, y permite implementar autenticación personalizada para acceder a servicios web. Mientras que los servicios RESTful, SOAP y OData están configurados en AEM Cloud Services, JDBC para bases de datos relacionales y conector para AEM perfil de usuario están configurados en AEM consola web.

## Configuración de la base de datos relacional {#configure-relational-database}

Puede configurar bases de datos relacionales mediante AEM Configuración de la consola web. Haga lo siguiente:

1. Vaya a AEM consola web en https://server:host/system/console/configMgr.
1. Buscar **[!UICONTROL Fuente de datos obtenida de una conexión Apache Sling]** configuración. Pulse para abrir la configuración en modo de edición.
1. En el cuadro de diálogo de configuración, especifique los detalles de la base de datos que desea configurar, como:

   * Nombre de la fuente de datos
   * Propiedad del servicio de fuente de datos que almacena el nombre del origen de datos
   * Nombre de clase Java para el controlador JDBC
   * URI de conexión JDBC
   * Nombre de usuario y contraseña para establecer conexión con el controlador JDBC

   >[!NOTE]
   >
   >Asegúrese de cifrar información confidencial como contraseñas antes de configurar el origen de datos. Para cifrar:
   >
   >    
   >    
   >    1. Vaya a https://&#39;[server]:[puerto]&#39;/system/console/crypto.
   >    1. En el **[!UICONTROL Texto sin formato]** , especifique la contraseña o cualquier cadena que desee cifrar y pulsar **[!UICONTROL Protect]**.

   >    
   >    
   >    
   >El texto cifrado aparece en el campo Texto protegido que puede especificar en la configuración.

1. Habilitar **[!UICONTROL Prueba a la vista previa]** o **[!UICONTROL Prueba a la vuelta]** para especificar que los objetos se validan antes de ser tomados en préstamo o devueltos al grupo, respectivamente.
1. Especifique una consulta SQL SELECT en la **[!UICONTROL Consulta de validación]** para validar conexiones desde el grupo. La consulta debe devolver al menos una fila. En función de la base de datos, especifique una de las siguientes opciones:

   * SELECT 1 (MySQL y MS SQL)
   * SELECT 1 from dual (Oracle)

1. Toque **[!UICONTROL Guardar]** para guardar la configuración.

## Configuración AEM perfil de usuario {#configure-aem-user-profile}

Puede configurar AEM perfil de usuario mediante la configuración del conector de perfil de usuario en AEM consola web. Haga lo siguiente:

1. Vaya a AEM consola web en https://&#39;[server]:[puerto]&#39;system/console/configMgr.
1. Buscar **[!UICONTROL Integraciones de datos de AEM Forms: configuración del conector de perfil de usuario]** y pulse para abrir la configuración en modo de edición.
1. En el cuadro de diálogo Configuración del conector de perfil de usuario, puede agregar, quitar o actualizar las propiedades del perfil de usuario. Las propiedades especificadas estarán disponibles para su uso en el modelo de datos de formulario. Utilice el siguiente formato para especificar las propiedades del perfil del usuario:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Ejemplos:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >La variable **&#42;** en el ejemplo anterior indica todos los nodos bajo la variable `profile/empLocation/` en AEM perfil de usuario en la estructura CRXDE. Significa que el modelo de datos de formulario puede acceder al `city` propiedad de tipo `string` presentes en cualquier nodo bajo el `profile/empLocation/` nodo . Sin embargo, los nodos que contienen la propiedad especificada deben seguir una estructura coherente.

1. Toque **[!UICONTROL Guardar]** para guardar la configuración.

## Configuración de la carpeta para configuraciones de servicios en la nube {#cloud-folder}

>[!NOTE]
>
>La configuración de la carpeta de servicios de nube es necesaria para configurar los servicios de nube para los servicios RESTful, SOAP y OData.

Todas las configuraciones de servicios en la nube en AEM se consolidan en la variable `/conf` en AEM repositorio. De forma predeterminada, la variable `conf` La carpeta contiene el `global` carpeta donde puede crear configuraciones de servicios en la nube. Sin embargo, debe habilitarlo manualmente para las configuraciones de nube. También puede crear carpetas adicionales en `conf` para crear y organizar configuraciones de servicios en la nube.

Para configurar la carpeta para las configuraciones del servicio en la nube:

1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   * Consulte la [Explorador de configuración](/help/sites-administering/configurations.md) documentación para obtener más información.
1. Haga lo siguiente para habilitar la carpeta global para configuraciones de nube o omita este paso para crear y configurar otra carpeta para configuraciones de servicios de nube.

   1. En el **[!UICONTROL Explorador de configuración]**, seleccione `global` carpeta y toque **[!UICONTROL Propiedades]**.

   1. En el **[!UICONTROL Propiedades de configuración]** cuadro de diálogo, habilitar **[!UICONTROL Configuraciones de nube]**.

   1. Toque **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. En el **[!UICONTROL Explorador de configuración]**, toque **[!UICONTROL Crear]**.
1. En el **[!UICONTROL Crear configuración]** , especifique un título para la carpeta y habilite **[!UICONTROL Configuraciones de nube]**.
1. Toque **[!UICONTROL Crear]** para crear la carpeta habilitada para las configuraciones del servicio en la nube.

## Configuración de los servicios web de RESTful {#configure-restful-web-services}

El servicio web RESTful se puede describir mediante [Especificaciones de Swagger](https://swagger.io/specification/) en formato JSON o YAML en un archivo de definición Swagger. Para configurar el servicio web RESTful en los servicios en la nube de AEM, asegúrese de que tiene el archivo Swagger en el sistema de archivos o la URL donde está alojado el archivo.

Haga lo siguiente para configurar los servicios RESTful:

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Pulse para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configuración de la carpeta para configuraciones de servicios en la nube](../../forms/using/configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Toque **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente para la creación de la configuración de fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio RESTful]** de la variable **[!UICONTROL Tipo de servicio]** lista desplegable, opcionalmente puede examinar y seleccionar una imagen en miniatura para la configuración, y pulsar **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio RESTful:

   * Seleccione URL o Archivo en la lista desplegable Origen del intercambiador y, en consecuencia, especifique la URL del intercambiador al archivo de definición del intercambiador o cargue el archivo Swagger desde el sistema de archivos local.
   * En función de la entrada de origen de Swagger, los siguientes campos se rellenan previamente con valores:

      * Esquema: Los protocolos de transferencia utilizados por la API de REST. El número de tipos de esquema que se muestran en la lista desplegable depende de los esquemas definidos en el origen Swagger.
      * Host: El nombre de dominio o la dirección IP del host que sirve la API de REST. Es un campo obligatorio.
      * Ruta base: El prefijo URL de todas las rutas de API. Es un campo opcional.\
         Si es necesario, edite los valores rellenados previamente para estos campos.
   * Seleccione el tipo de autenticación (Ninguno, OAuth2.0, Autenticación básica, Clave de API, Autenticación personalizada o Autenticación mutua) para acceder al servicio RESTful y proporcione los detalles correspondientes para la autenticación.

   Si selecciona **[!UICONTROL Clave de API]** como tipo de autenticación, especifique el valor de la clave de API. La clave de API se puede enviar como encabezado de solicitud o como parámetro de consulta. Seleccione una de estas opciones en el **[!UICONTROL Ubicación]** lista desplegable y especifique el nombre del encabezado o el parámetro de consulta en la **[!UICONTROL Nombre del parámetro]** en consecuencia.

   Si selecciona **[!UICONTROL Autenticación mutua]** como tipo de autenticación, consulte [Autenticación mutua basada en certificados para servicios web RESTful y SOAP](#mutual-authentication).

1. Toque **[!UICONTROL Crear]** para crear la configuración de nube para el servicio RESTful.

### Modelo de datos de formulario Configuración del cliente HTTP para optimizar el rendimiento {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] modelo de datos de formulario al integrarse con los servicios web RESTful, ya que el origen de datos incluye configuraciones de cliente HTTP para la optimización del rendimiento.
Realice los siguientes pasos para configurar el cliente HTTP del modelo de datos de formulario:

1. Iniciar sesión en [!DNL Experience Manager Forms] Instancia de autor como administrador y vaya a [!DNL Experience Manager] paquetes de la consola web. La dirección URL predeterminada es [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Toque **[!UICONTROL Configuración del cliente HTTP del Modelo de datos de formulario para el origen de datos REST]**.

1. En el [!UICONTROL Configuración del cliente HTTP del Modelo de datos de formulario para el origen de datos REST] diálogo:

   * Especifique el número máximo de conexiones permitidas entre el modelo de datos de formulario y los servicios web RESTful en la variable **[!UICONTROL Límite de conexión en total]** campo . El valor predeterminado es 20 conexiones.

   * Especifique el número máximo de conexiones permitidas para cada ruta en la variable **[!UICONTROL Límite de conexión por ruta]** campo . El valor predeterminado es 2 conexiones.

   * Especifique la duración, durante la cual se mantiene activa una conexión HTTP persistente, en la variable **[!UICONTROL Mantener viva]** campo . El valor predeterminado es de 15 segundos.

   * Especifique la duración para la que [!DNL Experience Manager Forms] espera a que una conexión se establezca, en la variable **[!UICONTROL Tiempo de espera de la conexión]** campo . El valor predeterminado es de 10 segundos.

   * Especifique el período de tiempo máximo para la inactividad entre dos paquetes de datos en la variable **[!UICONTROL Tiempo de espera de socket]** campo . El valor predeterminado es de 30 segundos.


## Configuración de servicios web SOAP {#configure-soap-web-services}

Los servicios web basados en SOAP se describen utilizando [Especificaciones del lenguaje de descripción de servicios web (WSDL)](https://www.w3.org/TR/wsdl). Para configurar el servicio web basado en SOAP en los servicios en la nube de AEM, asegúrese de que dispone de la URL WSDL para el servicio web y haga lo siguiente:

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Pulse para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configuración de la carpeta para configuraciones de servicios en la nube](../../forms/using/configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Toque **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente para la creación de la configuración de fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio web SOAP]** de la variable **[!UICONTROL Tipo de servicio]** lista desplegable, opcionalmente puede examinar y seleccionar una imagen en miniatura para la configuración, y pulsar **[!UICONTROL Siguiente]**.
1. Especifique lo siguiente para el servicio web SOAP:

   * URL de WSDL para el servicio web.
   * Punto final de servicio. Especifique un valor en este campo para anular el extremo de servicio mencionado en WSDL.
   * Seleccione el tipo de autenticación (Ninguno, OAuth2.0, Autenticación básica, Autenticación personalizada, Token X509 o Autenticación mutua) para acceder al servicio SOAP y proporcione los detalles para la autenticación.

      Si selecciona **[!UICONTROL Token X509]** como tipo Autenticación, configure el certificado X509. Para obtener más información, consulte [Configuración de certificados](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Especifique el alias KeyStore para el certificado X509 en la variable **[!UICONTROL Alias de clave]** campo . Especifique el tiempo, en segundos, hasta que la solicitud de autenticación siga siendo válida en la variable **[!UICONTROL Tiempo de vida]** campo . De forma opcional, seleccione para firmar el cuerpo del mensaje, el encabezado de la marca de tiempo o ambos.

      Si selecciona **[!UICONTROL Autenticación mutua]** como tipo de autenticación, consulte [Autenticación mutua basada en certificados para servicios web RESTful y SOAP](#mutual-authentication).

1. Toque **[!UICONTROL Crear]** para crear la configuración de nube para el servicio web SOAP.

## Configuración de servicios OData {#config-odata}

Un servicio OData se identifica mediante su URL raíz de servicio. Para configurar un servicio OData en los servicios en la nube de AEM, asegúrese de que tiene una URL raíz de servicio para el servicio y haga lo siguiente:

>[!NOTE]
>
> El modelo de datos de formulario es compatible [OData versión 4](https://www.odata.org/documentation/).
>Para obtener una guía paso a paso sobre la configuración de Microsoft Dynamics 365, en línea o local, consulte [Configuración de OData de Microsoft Dynamics](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Pulse para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configuración de la carpeta para configuraciones de servicios en la nube](../../forms/using/configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Toque **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente para la creación de la configuración de fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio OData]** de la variable **[!UICONTROL Tipo de servicio]** lista desplegable, opcionalmente puede examinar y seleccionar una imagen en miniatura para la configuración, y pulsar **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio OData:

   * URL raíz del servicio para configurar el servicio OData.
   * Seleccione el tipo de autenticación (Ninguno, OAuth2.0, Autenticación básica o Autenticación personalizada) para acceder al servicio OData y proporcione los detalles para la autenticación.

   >[!NOTE]
   >
   >Debe seleccionar el tipo de autenticación de OAuth 2.0 para conectarse con los servicios de Microsoft Dynamics mediante el extremo OData como raíz del servicio.

1. Toque **Crear** para crear la configuración de nube para el servicio OData.

## Autenticación mutua basada en certificados para servicios web RESTful y SOAP {#mutual-authentication}

Cuando se habilita la autenticación mutua para el modelo de datos de formulario, tanto el origen de datos como AEM servidor que ejecuta el modelo de datos de formulario se autentican entre sí antes de compartir cualquier dato. Puede utilizar la autenticación mutua para conexiones basadas en REST y SOAP (fuentes de datos). Para configurar la autenticación mutua para un modelo de datos de formulario en su entorno AEM Forms:

1. Cargue la clave privada (certificado) en [!DNL AEM Forms] servidor. Para cargar la clave privada:
   1. Inicie sesión en su [!DNL AEM Forms] como administrador.
   1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**. Seleccione el `fd-cloudservice` usuario y toque **[!UICONTROL Propiedades]**.
   1. Abra el **[!UICONTROL Almacén de claves]** expanda la pestaña **[!UICONTROL Agregar clave privada desde el archivo KeyStore]** , cargue el archivo KeyStore, especifique los alias, las contraseñas y pulse **[!UICONTROL Submit]**. Se carga el certificado.  El alias de clave privada se menciona en el certificado y se establece al crear el certificado.
1. Cargar certificado de confianza a Global Trust Store. Para cargar el certificado:
   1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Almacén de confianza]**.
   1. Expanda el **[!UICONTROL Añadir certificado del archivo CER]** opción, toque **[!UICONTROL Seleccionar archivo de certificado]**, cargue el certificado y pulse **[!UICONTROL Submit]**.
1. Configurar [SOAP](#configure-soap-web-services) o [RESTful](#configure-restful-web-services) servicios web como fuente de datos y seleccione **[!UICONTROL Autenticación mutua]** como tipo de autenticación. Si configura varios certificados autofirmados para `fd-cloudservice` especifique el nombre del alias de clave para el certificado.

## Pasos siguientes {#next-steps}

Ha configurado las fuentes de datos. A continuación, puede crear un modelo de datos de formulario o, si ya ha creado un modelo de datos de formulario sin un origen de datos, puede asociarlo a los orígenes de datos que acaba de configurar. Consulte [Crear modelo de datos de formulario](/help/forms/using/create-form-data-models.md) para obtener más información.
