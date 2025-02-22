---
title: Configurar el proveedor de servicios SAML
description: AEM Puede configurar el proveedor de servicios SAML para permitir que los usuarios inicien sesión y se autentiquen en los formularios de la a través de un proveedor de identidad de terceros (IDP) especificado.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# Configurar el proveedor de servicios SAML{#configure-saml-service-provider-settings}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

El lenguaje de marcado de aserción de seguridad (SAML) es una de las opciones que puede seleccionar al configurar la autorización de un dominio híbrido o empresarial. SAML se utiliza principalmente para admitir SSO en varios dominios. AEM Cuando SAML está configurado como su proveedor de autenticación, los usuarios inician sesión y se autentican en los formularios de la a través de un proveedor de identidad de terceros (IDP) especificado.

Para obtener una explicación de SAML, consulte [Descripción técnica del lenguaje de marcado de aserción de seguridad (SAML) V2.0](https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html).

1. En la consola de administración, haga clic en Configuración > User Management > Configuración > Configuración de Proveedor de servicio de SAML.
1. AEM En el cuadro ID de entidad de proveedor de servicios, escriba un ID único para utilizarlo como identificador para la implementación del proveedor de servicios de formularios de la aplicación de la entidad de proveedor de servicios de formularios de la. AEM También puede especificar este identificador único al configurar el IDP (por ejemplo, `um.lc.com`). También puede usar la URL que se usa para acceder a los formularios de la (por ejemplo, `https://AEMformsserver`).
1. En el cuadro Dirección URL base de Service Provider, escriba la dirección URL base del servidor de Forms (por ejemplo, `https://AEMformsserver:8080`).
1. AEM (Opcional) Para permitir que los formularios de envíen solicitudes de autenticación firmadas al IDP, realice las siguientes tareas:

   * Use el Administrador de confianza para importar una credencial en formato PKCS #12 con la credencial de firma de documento seleccionada como tipo de almacén de confianza. (Consulte [Administrar credenciales locales](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * En la lista Alias de clave de credencial de proveedor de servicios, seleccione el alias que asignó a la credencial en el almacén de confianza.
   * Haga clic en Exportar para guardar el contenido de la URL en un archivo y, a continuación, importar ese archivo en el IDP.

1. (Opcional) En la lista Política de ID de nombres de proveedores de servicios, seleccione el formato de nombre que utiliza el IDP para identificar al usuario en una afirmación de SAML. Las opciones son Sin especificar, Correo electrónico y Nombre completo del dominio de Windows.

   >[!NOTE]
   >
   >Los formatos de nombre no distinguen entre mayúsculas y minúsculas.

1. (Opcional) Seleccione Habilitar Mensaje De Autenticación Para Usuarios Locales. Cuando se selecciona esta opción, los usuarios ven dos vínculos:

   * un vínculo a la página de inicio de sesión del proveedor de identidad SAML de terceros, donde los usuarios que pertenecen a un dominio de Enterprise pueden autenticarse.
   * AEM un vínculo a la página de inicio de sesión de los formularios en la que los usuarios que pertenecen a un dominio local pueden autenticarse.

   Cuando esta opción no está seleccionada, los usuarios se dirigen directamente a la página de inicio de sesión del proveedor de identidad SAML de terceros, donde los usuarios que pertenecen a un dominio de Enterprise pueden autenticarse.

1. (Opcional) Seleccione Habilitar enlace de artefactos para habilitar la compatibilidad con enlaces de artefactos. De forma predeterminada, el enlace de POST se utiliza con SAML. Pero si ha configurado el enlace de artefactos, seleccione esta opción. Cuando se selecciona esta opción, la afirmación del usuario real no se pasa a través de la solicitud del explorador. En su lugar, se pasa un puntero a la aserción y esta se recupera mediante una llamada al servicio web back-end.
1. (Opcional) Seleccione Habilitar enlace de redireccionamiento para admitir enlaces SAML que utilicen redirecciones.
1. (Opcional) En Propiedades personalizadas, especifique propiedades adicionales. Las propiedades adicionales son pares nombre=valor separados por nuevas líneas.

   * AEM Puede configurar formularios para que emitan una aserción SAML durante un periodo de validez que coincida con el periodo de validez de una aserción de terceros. Para respetar el tiempo de espera de aserción de SAML de terceros, agregue la siguiente línea en Propiedades personalizadas:

     `saml.sp.honour.idp.assertion.expiry=true`

   * Agregue la siguiente propiedad personalizada para utilizar RelayState para determinar la dirección URL a la que se redirigirá al usuario después de la autenticación correcta.

     `saml.sp.use.relaystate=true`

   * Agregue la siguiente propiedad personalizada para poder configurar la dirección URL de las páginas de servidor Java™ (JSP) personalizadas, que se utilizan para procesar la lista registrada de proveedores de identidad. Si no ha implementado una aplicación web personalizada, se utiliza la página predeterminada Administración de usuarios para procesar la lista.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. Haga clic en Guardar.
