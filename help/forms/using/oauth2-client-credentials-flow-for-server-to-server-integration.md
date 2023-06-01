---
title: Integración de Salesforce con AEM Forms mediante el flujo de credenciales de cliente de OAuth 2.0
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: Pasos para integrar la integración de Salesforce con AEM Forms mediante el flujo de credenciales de cliente de OAuth 2.0
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
source-git-commit: cc0375f5b5616f82a73bd983a9da95225c51db99
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Integración de Salesforce con el flujo de credenciales de cliente de OAuth 2.0  {#configure-salesforce-with-ouath-2.0-client-credential}

Para integrar AEM Forms con la aplicación Salesforce, se utiliza el flujo de credenciales de cliente de OAuth 2.0. Es un método estandarizado y seguro para la comunicación directa sin la participación del usuario. AEM En este flujo, la aplicación cliente (formulario de la aplicación de cliente) intercambia las credenciales del cliente, definidas en la aplicación conectada de Salesforce, para obtener un token de acceso. Las credenciales de cliente requeridas incluyen la clave de consumidor y el secreto de consumidor.

## Ventajas de integrar Salesforce con AEM Forms mediante el flujo de credenciales de cliente de OAuth 2.0 {#advantages-of-integrating-saleforce-aemforms}

AEM Forms admite la integración de Salesforce con el flujo de código de autorización, además del flujo de credenciales de cliente de OAuth 2.0. En el flujo del código de autorización de OAuth 2.0, la aplicación cliente (AEM Forms) obtiene acceso a los recursos en nombre de un usuario de Salesforce, lo que tiene algunas limitaciones:

* Se permiten un máximo de cinco conexiones por usuario. Las conexiones adicionales revocan automáticamente las conexiones antiguas.
* AEM Si un usuario está desactivado, pierde el acceso o actualiza una contraseña, la configuración de la fuente de datos deja de funcionar, por lo que la configuración de la fuente de datos deja de funcionar.

## Requisitos previos {#prerequisites}

AEM Para recuperar datos entre los entornos de Salesforce y, se requieren ciertos requisitos previos antes de continuar:

+++ **Configurar una aplicación conectada de Salesforce con un flujo de credenciales de cliente y un usuario solo de API**

Es obligatorio crear una aplicación conectada de Salesforce con flujo de credenciales de cliente de OAuth 2.0 y un usuario solo de API para su organización. Para ver los pasos detallados, consulte el artículo [Flujo de credenciales de cliente de OAuth 2.0 para la integración de servidor a servidor](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5). Estos pasos le ayudan a obtener la clave del consumidor y el secreto del consumidor.

>[!NOTE]
>
> AEM Asegúrese de anotar la clave de consumidor y el secreto de consumidor, ya que son necesarios al crear una configuración de fuente de datos de la fuente de datos de la aplicación.

+++

+++ **Creación de un archivo Swagger**

Swagger es un conjunto de reglas, especificaciones y herramientas de código abierto para desarrollar y describir las API de RESTful. [Creación de un archivo swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) antes de integrar Salesforce con AEM Forms.

>[!NOTE]
>
> AEM La versión 6.5 solo admite especificaciones de archivo de Swagger 2.0.

+++

## Pasos para configurar Salesforce con el flujo de credenciales del cliente {#steps-to-create-aem-datasource-configuration}

1. Inicie sesión en la instancia de autor.
1. Ir a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fuentes de datos]**.
1. Seleccione la carpeta de configuración.
1. Clic **[!UICONTROL Crear]** y el **[!UICONTROL Crear configuración de fuente de datos]** aparece.
1. Especifique el **[!UICONTROL Título]** y seleccione la **[!UICONTROL Tipo de servicio]** as **[!UICONTROL Servicio RESTful]**.
1. Haga clic en **[!UICONTROL Siguiente]**.
1. Seleccione el **[!UICONTROL Origen de Swagger]** as **[!UICONTROL Archivo].**
   >[!NOTE]
   >
   > En cuanto se selecciona el archivo swagger, el esquema, el nombre del host y la ruta base se rellenan automáticamente.

1. Cargue el archivo swagger creado desde el equipo local haciendo clic en **[!UICONTROL Examinar]**.
1. Seleccione el **[!UICONTROL Tipo de autenticación]** as **[!UICONTROL OAuth 2.0]** y el **[!UICONTROL Configuración de autenticación]** aparece el panel.
1. Seleccione el **[!UICONTROL Tipo de concesión]** as **[!UICONTROL Credenciales del cliente]**.
1. Especifique el **[!UICONTROL ID de cliente]** y **[!UICONTROL Secreto del cliente]** obtenido de la aplicación conectada de Salesforce.
1. Especifique el **[!UICONTROL URL de token de acceso]** en formato
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Cada organización tiene su propio nombre de dominio específico.

1. Clic **[!UICONTROL Probar conexión]**.
1. Si la conexión se realiza correctamente, haga clic en **[!UICONTROL Crear]** botón.

Ahora, puede [crear el modelo de datos de formulario](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) para integrar la fuente de datos configurada con el formulario adaptable.


