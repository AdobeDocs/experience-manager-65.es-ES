---
title: Configuración de la configuración del proveedor de servicios SAML
seo-title: Configure SAML service provider settings
description: Puede configurar la configuración del proveedor de servicios SAML para permitir que los usuarios inicien sesión y se autentiquen en AEM formularios a través de un proveedor de identidad de terceros (IDP) especificado.
seo-description: You can configure SAML service provider settings to allow users to login and authenticate to AEM forms via a specified third-party identity provider (IDP).
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---

# Configuración de la configuración del proveedor de servicios SAML{#configure-saml-service-provider-settings}

El lenguaje de marcado de aserción de seguridad (SAML) es una de las opciones que puede seleccionar al configurar la autorización para un dominio híbrido o empresarial. SAML se utiliza principalmente para admitir SSO en varios dominios. Cuando SAML está configurado como proveedor de autenticación, los usuarios inician sesión y se autentican en AEM formularios a través de un proveedor de identidad de terceros (IDP) especificado.

Para una explicación de SAML, consulte [Información general técnica sobre el lenguaje de marcado de aserción de seguridad (SAML) V2.0](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configuración del proveedor de servicios SAML.
1. En el cuadro ID de entidad proveedor de servicios, escriba un ID único para utilizarlo como identificador para la implementación del proveedor de servicios de formularios AEM. También especifica este ID único al configurar su IDP (por ejemplo, `um.lc.com`.) También puede utilizar la dirección URL que se utiliza para acceder a AEM formularios (por ejemplo, `https://AEMformsserver`).
1. En el cuadro URL base del proveedor de servicios, escriba la URL base para el servidor de formularios (por ejemplo, `https://AEMformsserver:8080`).
1. (Opcional) Para permitir que AEM formularios envíen solicitudes de autenticación firmadas al IDP, realice las siguientes tareas:

   * Utilice Trust Manager para importar una credencial en formato PKCS #12 con Credencial de firma de documento seleccionado como Tipo de almacén de confianza. (Consulte [Administración de credenciales locales](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * En la lista Alias de clave de credencial de proveedor de servicios , seleccione el alias que asignó a la credencial en el Almacén de confianza.
   * Haga clic en Exportar para guardar el contenido de la URL en un archivo y, a continuación, importe el archivo en su IDP.

1. (Opcional) En la lista Directiva de ID de nombre de proveedor de servicios, seleccione el formato de nombre que utiliza el IDP para identificar al usuario en una afirmación SAML. Las opciones son No especificado, Correo electrónico y Nombre cualificado del dominio de Windows.

   >[!NOTE]
   >
   >Los formatos de nombre no distinguen entre mayúsculas y minúsculas.

1. (Opcional) Seleccione Habilitar Mensaje De Autenticación Para Usuarios Locales. Cuando se selecciona esta opción, los usuarios ven dos vínculos:

   * un vínculo a la página de inicio de sesión del proveedor de identidad SAML de terceros, donde los usuarios que pertenecen a un dominio de Enterprise pueden autenticarse.
   * un vínculo a la página de inicio de sesión de AEM forms, en la que los usuarios pertenecientes a un dominio local pueden autenticarse.

   Cuando no se selecciona esta opción, los usuarios son llevados directamente a la página de inicio de sesión del proveedor de identidad SAML de terceros, donde los usuarios que pertenecen a un dominio de Enterprise pueden autenticarse.

1. (Opcional) Seleccione Habilitar enlace de artefactos para habilitar la compatibilidad con enlace de artefactos. De forma predeterminada, el enlace del POST se utiliza con SAML. Pero si ha configurado el enlace de artefactos, seleccione esta opción. Cuando se selecciona esta opción, la afirmación del usuario real no se pasa a través de la solicitud del explorador. En su lugar, se pasa un puntero a la afirmación y la afirmación se recupera mediante una llamada de servicio web back-end.
1. (Opcional) Seleccione Habilitar el enlace de redireccionamiento para admitir enlaces SAML que usen redirecciones.
1. (Opcional) En Propiedades personalizadas, especifique propiedades adicionales. Las propiedades adicionales son pares name=value separados por nuevas líneas.

   * Puede configurar AEM formularios para que emitan una afirmación SAML durante un periodo de validez que coincida con el periodo de validez de una afirmación de terceros. Para cumplir el tiempo de espera de afirmación de SAML de terceros, agregue la línea siguiente en Propiedades personalizadas:

      `saml.sp.honour.idp.assertion.expiry=true`

   * Agregue la siguiente propiedad personalizada para usar RelayState para determinar la dirección URL a la que se redirigirá al usuario después de la autenticación correcta.

      `saml.sp.use.relaystate=true`

   * Agregue la siguiente propiedad personalizada para configurar la URL de las páginas de servidor Java (JSP) personalizadas, que se utilizará para procesar la lista registrada de proveedores de identidad. Si no ha implementado una aplicación web personalizada, utilizará la página Administración de usuarios predeterminada para procesar la lista.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. Haga clic en Guardar.
