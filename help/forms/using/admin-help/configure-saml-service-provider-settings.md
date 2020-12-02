---
title: Configuración de la configuración del proveedor de servicio SAML
seo-title: Configuración de la configuración del proveedor de servicio SAML
description: Puede configurar la configuración del proveedor de servicio SAML para permitir que los usuarios inicien sesión y se autentiquen en AEM formularios a través de un proveedor de identidad de terceros (IDP) especificado.
seo-description: Puede configurar la configuración del proveedor de servicio SAML para permitir que los usuarios inicien sesión y se autentiquen en AEM formularios a través de un proveedor de identidad de terceros (IDP) especificado.
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---


# Configurar la configuración del proveedor de servicio SAML{#configure-saml-service-provider-settings}

El Lenguaje de marcado de aserción de seguridad (SAML) es una de las opciones que puede seleccionar al configurar la autorización para un dominio híbrido o empresarial. SAML se utiliza principalmente para admitir SSO en varios dominios. Cuando SAML está configurado como proveedor de autenticación, los usuarios inician sesión y se autentican en AEM formularios a través de un proveedor de identidad de terceros (IDP) especificado.

Para obtener una explicación de SAML, consulte [Security Assertion Markup Language (SAML) V2.0 Technical Overview](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configuración de Proveedor de servicio de SAML.
1. En el cuadro Id. de entidad de Proveedor de servicio, escriba un identificador único para utilizarlo como identificador para la implementación de proveedor de servicio de formularios AEM. También puede especificar este identificador único al configurar su IDP (por ejemplo, `um.lc.com`). También puede utilizar la dirección URL que se utiliza para acceder a AEM formularios (por ejemplo, `https://AEMformsserver`).
1. En el cuadro Dirección URL base del Proveedor de servicio, escriba la dirección URL base para el servidor de formularios (por ejemplo, `https://AEMformsserver:8080`).
1. (Opcional) Para permitir que los formularios AEM envíen solicitudes de autenticación firmadas al IDP, realice las siguientes tareas:

   * Utilice el Administrador de confianza para importar una credencial en formato PKCS #12 con la credencial de firma de Documento seleccionada como tipo de almacén de confianza. (Consulte [Administración de credenciales locales](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * En la lista Alias de clave de credencial de Proveedor de servicio, seleccione el alias asignado a las credenciales en el almacén de confianza.
   * Haga clic en Exportar para guardar el contenido de la URL en un archivo y, a continuación, importe dicho archivo en su IDP.

1. (Opcional) En la lista de directiva de ID de nombre de Proveedor de servicio, seleccione el formato de nombre que utiliza el IDP para identificar al usuario en una afirmación de SAML. Las opciones son No especificado, Correo electrónico y Nombre cualificado del dominio de Windows.

   >[!NOTE]
   >
   >Los formatos de nombre no distinguen entre mayúsculas y minúsculas.

1. (Opcional) Seleccione Activar el mensaje de autenticación para los usuarios locales. Cuando se selecciona esta opción, los usuarios verán dos vínculos:

   * vínculo a la página de inicio de sesión del proveedor de identidad SAML de terceros, donde los usuarios que pertenecen a un dominio Enterprise pueden autenticarse.
   * vínculo a la página de inicio de sesión de los formularios AEM, donde los usuarios que pertenecen a un dominio local pueden autenticarse.

   Cuando esta opción no está seleccionada, los usuarios serán llevados directamente a la página de inicio de sesión del proveedor de identidad SAML de terceros, donde los usuarios que pertenecen a un dominio Enterprise pueden autenticarse.

1. (Opcional) Seleccione Activar enlace de artefacto para activar la compatibilidad con enlace de artefacto. De forma predeterminada, el enlace de POST se utiliza con SAML. Sin embargo, si ha configurado Enlace de artefacto, seleccione esta opción. Cuando se selecciona esta opción, la afirmación del usuario real no se pasa a través de la solicitud del explorador. En su lugar, se pasa un puntero a la afirmación y ésta se recupera mediante una llamada de servicio web back-end.
1. (Opcional) Seleccione Activar enlace de redirección para admitir enlaces SAML que utilizan redirecciones.
1. (Opcional) En Propiedades personalizadas, especifique propiedades adicionales. Las propiedades adicionales son pares name=value separados por nuevas líneas.

   * Puede configurar formularios AEM para que emitan una afirmación SAML para un período de validez que coincida con el período de validez de una afirmación de terceros. Para respetar el tiempo de espera de afirmación de SAML de terceros, agregue la línea siguiente en Propiedades personalizadas:

      `saml.sp.honour.idp.assertion.expiry=true`

   * Añada la siguiente propiedad personalizada para usar RelayState para determinar la dirección URL a la que se redirigirá al usuario tras autenticarse correctamente.

      `saml.sp.use.relaystate=true`

   * Añada la siguiente propiedad personalizada para configurar la dirección URL de las páginas de servidor Java (JSP) personalizadas, que se utilizarán para representar la lista registrada de los proveedores de identidad. Si no ha implementado una aplicación web personalizada, utilizará la página Administración de usuarios predeterminada para procesar la lista.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. Haga clic en Guardar.

