---
title: Configuración de OData de Microsoft Dynamics
seo-title: Configuración de ODtata de Microsoft Dynamics
description: Aproveche, integre y trabaje con los servicios de Microsoft Dynamics en línea y locales a través del modelo de datos de formulario.
seo-description: Obtenga información sobre cómo aprovechar la integración y el trabajo con los servicios de Microsoft Dynamics en línea y locales a través del modelo de datos de formulario.
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
translation-type: tm+mt
source-git-commit: 6a53f5d8a2f3428e4957f2b2a38a1183ef7333ed
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---


# Configuración de OData de Microsoft Dynamics{#microsoft-dynamics-odata-configuration}

![integración de datos](assets/data-integeration.png)

Microsoft Dynamics es un software de administración de la relación con los clientes (CRM) y de planificación de recursos empresariales (ERP) que proporciona soluciones empresariales para crear y administrar cuentas de clientes, contactos, posibles clientes, oportunidades y casos. [La ](../../forms/using/data-integration.md) integración de datos de AEM Forms proporciona una configuración de servicio en la nube OData para integrar Forms con el servidor en línea y en las instalaciones de Microsoft Dynamics. Permite crear un modelo de datos de formulario basado en las entidades, atributos y servicios definidos en el servicio Microsoft Dynamics. El modelo de datos de formulario se puede utilizar para crear formularios adaptables que interactúen con el servidor de Microsoft Dynamics para habilitar flujos de trabajo empresariales. Por ejemplo:

* Consulta de Microsoft Dynamics Server para datos y cumplimentación previa de formularios adaptables
* Escribir datos en Microsoft Dynamics en el envío de formularios adaptables
* Escribir datos en Microsoft Dynamics mediante entidades personalizadas definidas en el modelo de datos de formulario y viceversa

El paquete de complementos de AEM Forms también incluye la configuración OData de referencia que puede aprovechar para integrar rápidamente Microsoft Dynamics con AEM Forms.

Cuando se instala el paquete, las siguientes entidades y servicios están disponibles en la instancia de AEM Forms:

* Cloud Service de MS Dynamics OData (servicio OData)
* Modelo de datos de formulario con entidades y servicios preconfigurados de Microsoft Dynamics.

Las entidades y servicios preconfigurados de Microsoft Dynamics en un modelo de datos de formulario solo están disponibles en la instancia de AEM Forms si el modo de ejecución de la instancia de AEM está establecido como `samplecontent` (predeterminado). El Cloud Service de MS Dynamics OData (servicio OData) también está disponible con otros modos de ejecución. Para obtener más información sobre la configuración de modos de ejecución para una instancia de AEM, consulte [Modos de ejecución](/help/sites-deploying/configure-runmodes.md).

## Requisitos previos {#prerequisites}

Antes de comenzar a configurar y configurar Microsoft Dynamics, asegúrese de que:

* Se instaló el [paquete de complemento de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)
* Se ha configurado Microsoft Dynamics 365 en línea o se ha instalado una instancia de una de las siguientes versiones de Microsoft Dynamics:

   * Microsoft Dynamics 365 local
   * Microsoft Dynamics 2016 in situ

* [Se registró la aplicación para el servicio en línea de Microsoft Dynamics con Microsoft Azure Active Directory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Tome nota de los valores del ID de cliente (también denominado ID de aplicación) y del secreto de cliente para el servicio registrado. Estos valores se utilizan mientras [configura el servicio en la nube para el servicio de Microsoft Dynamics](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## Establecer URL de respuesta para la aplicación registrada de Microsoft Dynamics {#set-reply-url-for-registered-microsoft-dynamics-application}

Para establecer la URL de respuesta para la aplicación registrada de Microsoft Dynamics, haga lo siguiente:

>[!NOTE]
>
>Utilice este procedimiento únicamente al integrar AEM Forms con el servidor en línea de Microsoft Dynamics.

1. Vaya a la cuenta de Microsoft Azure Active Directory y agregue la siguiente URL de configuración del servicio en la **URL de respuesta** configuración de la aplicación registrada:

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Directorio de Azure](assets/azure_directory_new.png)

1. Guarde la configuración.

## Configurar Microsoft Dynamics para IFD {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics utiliza la autenticación basada en notificaciones para proporcionar acceso a los datos del servidor de Microsoft Dynamics CRM a los usuarios externos. Para habilitarlo, haga lo siguiente para configurar Microsoft Dynamics para la implementación con conexión a Internet (IFD) y configurar las notificaciones.

>[!NOTE]
>
>Utilice este procedimiento únicamente al integrar AEM Forms con el servidor local de Microsoft Dynamics.

1. Configure la instancia local de Microsoft Dynamics para IFD como se describe en [Configurar IFD para Microsoft Dynamics](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Ejecute los siguientes comandos con Windows PowerShell para configurar la configuración de notificaciones en Microsoft Dynamics habilitada para IFD:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Consulte [Registro de aplicaciones para CRM local (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) para obtener más información.

## Configurar el cliente OAuth en el equipo de AD FS {#configure-oauth-client-on-ad-fs-machine}

Haga lo siguiente para registrar un cliente OAuth en el equipo de Servicios de federación de Active Directory (AD FS) y conceder acceso en el equipo de AD FS:

>[!NOTE]
>
>Utilice este procedimiento únicamente al integrar AEM Forms con el servidor local de Microsoft Dynamics.

1. Ejecute el siguiente comando:

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Donde:

   * `Client-ID` es un ID de cliente que puede generar con cualquier generador GUID.
   * `redirect-uri` es la dirección URL del servicio en la nube de Microsoft Dynamics OData en AEM Forms. El servicio de nube predeterminado instalado con el paquete de AEM Forms se implementa en la siguiente dirección URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Ejecute el siguiente comando para conceder acceso en el equipo de AD FS:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   Donde:

   * `resource` es la dirección URL de la organización de Microsoft Dynamics.

1. Microsoft Dynamics utiliza el protocolo HTTPS. Para invocar extremos de AD FS desde el servidor de Forms, instale el certificado de sitio de Microsoft Dynamics en el almacén de certificados de Java mediante el comando `keytool` en el equipo que ejecuta AEM Forms.

## Configurar el servicio en la nube para su servicio de Microsoft Dynamics {#configure-cloud-service-for-your-microsoft-dynamics-service}

La configuración **Cloud Service OData de MS Dynamics (servicio OData)** viene con la configuración OData predeterminada. Para configurarlo para conectarse con su servicio de Microsoft Dynamics, haga lo siguiente.

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]** y toque la carpeta de configuración `global`.
1. Seleccione la configuración **Cloud Service OData de MS Dynamics (servicio OData)** y toque **[!UICONTROL Propiedades]**. Se abre el cuadro de diálogo de la propiedad de configuración del servicio en la nube.

   En la ficha **Configuración de autenticación**:

   1. Introduzca el valor del campo **Raíz del servicio**. Vaya a la instancia de Dynamics y vaya a **Recursos para desarrolladores** para vista del valor del campo Raíz del servicio. Por ejemplo: https://&lt;nombre_inquilino>/api/data/v9.1/

   1. Reemplace los valores predeterminados en **ID de cliente** (también denominado **ID de aplicación**), **Secreto de cliente**, **URL de OAuth**, **Actualizar URL de token**, **URL de Token de acceso**. campos> y **Recurso** con valores de la configuración del servicio de Microsoft Dynamics. Es obligatorio especificar la dirección URL de la instancia de dinámica en el campo **Recurso** para configurar Microsoft Dynamics con un modelo de datos de formulario. Utilice la URL de la raíz del servicio para derivar la URL de la instancia de dinámica. Por ejemplo, [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Especifique **open** en el campo **Ámbito de autorización** para el proceso de autorización en Microsoft Dynamics.

   ![Configuración de autenticación](assets/dynamics_authentication_settings_new.png)

1. Haga clic en **[!UICONTROL Conectar con OAuth]**. Se le redirige a la página de inicio de sesión de Microsoft Dynamics.
1. Inicie sesión con sus credenciales de Microsoft Dynamics y acepte permitir que la configuración del servicio en la nube se conecte al servicio de Microsoft Dynamics. Es una tarea única para establecer la conexión entre el servicio en la nube y el servicio.

   A continuación, se le redirige a la página de configuración del servicio en la nube, que muestra un mensaje que indica que la configuración de OData se ha guardado correctamente.

El servicio en la nube de MS Dynamics OData Cloud Service (servicio OData) está configurado y conectado con su servicio Dynamics.

## Crear modelo de datos de formulario {#create-form-data-model}

Al instalar el paquete de AEM Forms, se implementa un modelo de datos de formulario,**Microsoft Dynamics FDM**, en la instancia de AEM. De forma predeterminada, el modelo de datos de formulario utiliza el servicio Microsoft Dynamics configurado en el Cloud Service MS Dynamics OData (servicio OData) como su origen de datos.

Al abrir el modelo de datos de formulario por primera vez, se conecta al servicio configurado de Microsoft Dynamics y obtiene entidades de la instancia de Microsoft Dynamics. Las entidades &quot;contact&quot; y &quot;lead&quot; de Microsoft Dynamics ya se han agregado en el modelo de datos de formulario.

Para revisar el modelo de datos de formulario, vaya a **[!UICONTROL Forms > Integraciones de datos]**. Seleccione **Microsoft Dynamics FDM** y haga clic en **Editar** para abrir el modelo de datos de formulario en modo de edición. También puede abrir el modelo de datos de formulario directamente desde la siguiente URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

A continuación, puede crear un formulario adaptable basado en el modelo de datos de formulario y utilizarlo en varios casos de uso de formularios adaptables, como:

* Rellene el formulario adaptable consultando información de entidades y servicios de Microsoft Dynamics
* Invocar operaciones de servidor de Microsoft Dynamics definidas en un modelo de datos de formulario mediante reglas de formulario adaptables
* Escribir datos de formulario enviados a entidades de Microsoft Dynamics

Se recomienda crear una copia del modelo de datos de formulario proporcionado con el paquete de AEM Forms y configurar los modelos y servicios de datos según sus necesidades. Garantizará que las futuras actualizaciones del paquete no sobrescriban el modelo de datos de formulario.

Para obtener más información sobre cómo crear y utilizar el modelo de datos de formulario en flujos de trabajo comerciales, consulte [Integración de datos](../../forms/using/data-integration.md).
