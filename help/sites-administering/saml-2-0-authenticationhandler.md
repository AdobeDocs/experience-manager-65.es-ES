---
title: Controlador de autenticación SAML 2.0
seo-title: SAML 2.0 Authentication Handler
description: Obtenga información sobre el gestor de autenticación SAML 2.0 en AEM.
seo-description: Learn about the SAML 2.0 Authentication Handler in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: c73d39a1c88c914cd63bc08fe8daf0ff37b4bf7c
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 1%

---

# Controlador de autenticación SAML 2.0{#saml-authentication-handler}

AEM buques con un [SAML](https://saml.xml.org/saml-specifications) controlador de autenticación. Este controlador proporciona soporte para la variable [SAML](https://saml.xml.org/saml-specifications) 2.0 Protocolo de solicitud de autenticación (perfil Web-SSO) que utiliza la variable `HTTP POST` enlace.

Admite:

* firma y cifrado de mensajes
* creación automática de usuarios
* sincronizar grupos con los existentes en AEM
* Autenticación iniciada por el proveedor de servicios y el proveedor de identidad

Este controlador almacena el mensaje de respuesta de SAML cifrado en el nodo de usuario ( `usernode/samlResponse`) para facilitar la comunicación con un proveedor de servicios de terceros.

>[!NOTE]
>
>Para leer un artículo de la comunidad de principio a fin, haga clic en: [Integración de SAML con Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/aem63_saml.html).

## Configuración del gestor de autenticación SAML 2.0 {#configuring-the-saml-authentication-handler}

La variable [Consola web](/help/sites-deploying/configuring-osgi.md) proporciona acceso al [SAML](https://saml.xml.org/saml-specifications) Configuración del gestor de autenticación 2.0 llamada **Controlador de autenticación de Adobe Granite SAML 2.0**. Se pueden establecer las siguientes propiedades.

>[!NOTE]
>
>El gestor de autenticación SAML 2.0 está deshabilitado de forma predeterminada. Debe establecer al menos una de las siguientes propiedades para habilitar el controlador:
>
>* La dirección URL del POST del proveedor de identidad o la dirección URL de IDP.
>* El ID de entidad de proveedor de servicios.
>


>[!NOTE]
>
>Las aserciones SAML están firmadas y pueden ser cifradas opcionalmente. Para que esto funcione, debe proporcionar al menos el certificado público del proveedor de identidad en TrustStore. Consulte [Añadir el certificado IdP al TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) para obtener más información.

**Ruta** Ruta del repositorio para la cual Sling debe utilizar este controlador de autenticación. Si está vacío, se desactivará el controlador de autenticación.

**Clasificación de servicios** Valor de clasificación de servicios de OSGi Framework para indicar el orden en que se debe llamar a este servicio. Se trata de un valor entero en el que los valores superiores designan una prioridad mayor.

**Alias de certificado IDP** alias del certificado de IdP en el almacén de confianza global. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado. Consulte el capítulo &quot;Añadir el certificado IdP al AEM TrustStore&quot; a continuación sobre cómo configurarlo.

**URL de IDP** URL del IDP donde se debe enviar la solicitud de autenticación SAML. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado.

>[!CAUTION]
>
>El nombre de host del proveedor de identidad debe agregarse al **Filtro de referente de Apache Sling** Configuración de OSGi. Consulte la [Consola web](/help/sites-deploying/configuring-osgi.md) para obtener más información.

**ID de entidad de proveedor de servicios** ID que identifica de forma exclusiva a este proveedor de servicios con el proveedor de identidad. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado.

**Redirección predeterminada** La ubicación predeterminada a la que redirigir después de una autenticación correcta.

>[!NOTE]
>
>Esta ubicación solo se utiliza si la variable `request-path` no está configurada. Si solicita cualquier página debajo de la ruta configurada sin un token de inicio de sesión válido, la ruta solicitada se almacena en una cookie
>y el explorador se redirigirá a esta ubicación de nuevo después de la autenticación correcta.

**Atributo User-ID** Nombre del atributo que contiene el ID de usuario utilizado para autenticar y crear el usuario en el repositorio CRX.

>[!NOTE]
>
>El ID de usuario no se toma del `saml:Subject` nodo de la aserción SAML pero a partir de este `saml:Attribute`.

**Usar codificación** Indica si este controlador de autenticación espera o no aserciones SAML cifradas.

**Creación automática de usuarios de CRX** Si se crean o no automáticamente usuarios no existentes en el repositorio después de una autenticación correcta.

>[!CAUTION]
>
>Si la creación automática de usuarios CRX está deshabilitada, los usuarios deberán crearse manualmente.

**Agregar a grupos** Indica si un usuario debe agregarse o no automáticamente a los grupos CRX después de la autenticación correcta.

**Pertenencia a grupos** El nombre del saml:Attribute que contiene una lista de grupos CRX a los que se debe agregar este usuario.

## Añadir el certificado IdP a AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

Las aserciones SAML están firmadas y pueden ser cifradas opcionalmente. Para que esto funcione, debe proporcionar al menos el certificado público del IdP en el repositorio. Para ello, debe:

1. Vaya a *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Pulse el botón **[!UICONTROL Crear vínculo de TrustStore]**
1. Introduzca la contraseña de TrustStore y pulse **[!UICONTROL Guardar]**.
1. Haga clic en **[!UICONTROL Administrar TrustStore]**.
1. Cargue el certificado IdP.
1. Tome nota del certificado Alias. El alias es **[!UICONTROL admin#1436172864930]** en el ejemplo siguiente.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Agregue la cadena de certificado y clave del Proveedor de servicios al almacén de claves de AEM {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>Los pasos siguientes son obligatorios; de lo contrario, se genera la siguiente excepción: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Vaya a: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Edite el `authentication-service` usuario.
1. Cree un almacén de claves haciendo clic en **Crear KeyStore** under **Configuración de la cuenta**.

>[!NOTE]
>
>Los pasos siguientes solo son necesarios si el controlador debe poder firmar o descifrar mensajes.

1. Cargue el archivo de clave privada haciendo clic en **Seleccionar archivo de clave privada**. La clave debe estar en formato PKCS#8 con codificación DER.
1. Cargue el archivo de certificado haciendo clic en **Seleccionar archivos de cadena de certificado**.
1. Asigne un alias, como se muestra a continuación:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configuración de un registrador para SAML {#configure-a-logger-for-saml}

Puede configurar un Registrador para depurar cualquier problema que pueda surgir de la configuración incorrecta de SAML. Para ello:

1. Accediendo a la consola web, en *http://localhost:4502/system/console/configMgr*
1. Busque y haga clic en la entrada denominada **Configuración del registrador de Apache Sling**
1. Cree un registrador con la siguiente configuración:

   * **Nivel de registro:** Depuración
   * **Archivo de registro:** logs/saml.log
   * **Registrador:** com.adobe.granite.auth.saml
