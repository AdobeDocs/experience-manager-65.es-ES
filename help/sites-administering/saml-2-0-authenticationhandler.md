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
source-git-commit: 6bc60122d2512a6f58c0204cd240a1b99a37ed93
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 1%

---

# Controlador de autenticación SAML 2.0{#saml-authentication-handler}

AEM se envía con un controlador de autenticación [SAML](http://saml.xml.org/saml-specifications). Este controlador proporciona soporte para el [SAML](http://saml.xml.org/saml-specifications) 2.0 Authentication Request Protocol (perfil Web-SSO) utilizando el enlace `HTTP POST`.

Admite:

* firma y cifrado de mensajes
* creación automática de usuarios
* sincronizar grupos con los existentes en AEM
* Autenticación iniciada por el proveedor de servicios y el proveedor de identidad

Este controlador almacena el mensaje de respuesta de SAML cifrado en el nodo de usuario ( `usernode/samlResponse`) para facilitar la comunicación con un proveedor de servicios de terceros.

>[!NOTE]
>
>Consulte [una demostración de la integración de AEM y SAML](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html).
>
>Para leer un artículo de la comunidad de principio a fin, haga clic en: [Integración de SAML con Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/aem63_saml.html).

## Configuración del gestor de autenticación SAML 2.0 {#configuring-the-saml-authentication-handler}

La [consola web](/help/sites-deploying/configuring-osgi.md) proporciona acceso a la configuración del [gestor de autenticación SAML](http://saml.xml.org/saml-specifications) 2.0 llamado **Controlador de autenticación de granito de Adobe SAML 2.0**. Se pueden establecer las siguientes propiedades.

>[!NOTE]
>
>El gestor de autenticación SAML 2.0 está deshabilitado de forma predeterminada. Debe establecer al menos una de las siguientes propiedades para habilitar el controlador:
>
>* La dirección URL del POST del proveedor de identidad.
>* El ID de entidad de proveedor de servicios.

>


>[!NOTE]
>
>Las aserciones SAML están firmadas y pueden ser cifradas opcionalmente. Para que esto funcione, debe proporcionar al menos el certificado público del proveedor de identidad en TrustStore. Consulte [Adición del certificado IdP a la sección TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) para obtener más información.

**** Ruta de acceso del repositorio para la cual Sling debe utilizar este controlador de autenticación. Si está vacío, se desactivará el controlador de autenticación.

**Ranking de** ServiciosOSGi Framework Valor de Clasificación de Servicios para indicar el orden en que se debe llamar a este servicio. Se trata de un valor entero en el que los valores superiores designan una prioridad mayor.

**Alias de certificado IDP** El alias del certificado de IdP en el almacén de confianza global. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado. Consulte el capítulo &quot;Añadir el certificado IdP al AEM TrustStore&quot; a continuación sobre cómo configurarlo.

**URL del proveedor de** identidad del IDP al que se debe enviar la solicitud de autenticación SAML. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado.

>[!CAUTION]
>
>El nombre de host del proveedor de identidad debe agregarse a la configuración OSGi **Apache Sling Referrer Filter**. Consulte la sección [Consola web](/help/sites-deploying/configuring-osgi.md) para obtener más información.

**ID de entidad de proveedor de servicios** que identifica de forma exclusiva a este proveedor de servicios con el proveedor de identidad. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado.

**Redireccionar** predeterminadoLa ubicación predeterminada a la que redirigir después de una autenticación correcta.

>[!NOTE]
>
>Esta ubicación solo se utiliza si no se ha establecido la cookie `request-path` . Si solicita cualquier página debajo de la ruta configurada sin un token de inicio de sesión válido, la ruta solicitada se almacena en una cookie
>y el explorador se redirigirá a esta ubicación de nuevo después de la autenticación correcta.

**Atributo de ID de usuario** El nombre del atributo que contiene el ID de usuario utilizado para autenticar y crear el usuario en el repositorio CRX.

>[!NOTE]
>
>El ID de usuario no se toma del nodo `saml:Subject` de la aserción SAML sino de esta `saml:Attribute`.

**Utilice** EncryptionIf o no este controlador de autenticación espera aserciones SAML cifradas.

**Crear automáticamente** usuarios de CRXEspecifica si se crean o no automáticamente usuarios no existentes en el repositorio después de la autenticación correcta.

>[!CAUTION]
>
>Si la creación automática de usuarios CRX está deshabilitada, los usuarios deberán crearse manualmente.

**Agregar a** gruposEspecifica si un usuario debe agregarse o no automáticamente a los grupos CRX después de la autenticación correcta.

**Pertenencia** al grupoEl nombre del saml:Attribute que contiene una lista de grupos CRX a los que este usuario debe añadirse.

## Añadir el certificado IdP a AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

Las aserciones SAML están firmadas y pueden ser cifradas opcionalmente. Para que esto funcione, debe proporcionar al menos el certificado público del IdP en el repositorio. Para ello, debe:

1. Vaya a *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Pulse el enlace **[!UICONTROL Create TrustStore]**
1. Introduzca la contraseña de TrustStore y pulse **[!UICONTROL Save]**.
1. Haga clic en **[!UICONTROL Administrar TrustStore]**.
1. Cargue el certificado IdP.
1. Tome nota del certificado Alias. El alias es **[!UICONTROL admin#1436172864930]** en el ejemplo siguiente.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Agregue la cadena de certificado y clave del Proveedor de servicios al almacén de claves de AEM {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>Los pasos siguientes son obligatorios; de lo contrario, se genera la siguiente excepción: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Vaya a: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Edite el usuario `authentication-service`.
1. Cree un KeyStore haciendo clic en **Crear KeyStore** en **Configuración de la cuenta**.

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
1. Busque y haga clic en la entrada denominada **Configuración del registrador de Sling de Apache**
1. Cree un registrador con la siguiente configuración:

   * **Nivel de registro:** depuración
   * **Archivo de registro:** logs/saml.log
   * **Registrador:** com.adobe.granite.auth.saml
