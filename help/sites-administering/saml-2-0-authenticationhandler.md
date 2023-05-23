---
title: Controlador de autenticación SAML 2.0
seo-title: SAML 2.0 Authentication Handler
description: AEM Obtenga información acerca del controlador de autenticación SAML 2.0 en la documentación de.
seo-description: Learn about the SAML 2.0 Authentication Handler in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: 6fa3679429527e026313b22d953267503598d1a9
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 2%

---

# Controlador de autenticación SAML 2.0{#saml-authentication-handler}

AEM barcos con un a [SAML](https://saml.xml.org/saml-specifications) controlador de autenticación. Este controlador proporciona compatibilidad con [SAML](https://saml.xml.org/saml-specifications) Protocolo de solicitud de autenticación 2.0 (perfil Web-SSO) que utiliza el `HTTP POST` enlace.

Admite lo siguiente:

* firma y cifrado de mensajes
* creación automática de usuarios
* AEM sincronización de grupos con los existentes en la
* Autenticación iniciada por el proveedor de servicios y el proveedor de identidad

Este controlador almacena el mensaje de respuesta SAML cifrado en el nodo de usuario ( `usernode/samlResponse`) para facilitar la comunicación con un proveedor de servicios de terceros.

>[!NOTE]
>
>Consulte [AEM una demostración de la integración de SAML y de los servicios de INTEL](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17481.html?lang=es).

## Configuración del controlador de autenticación SAML 2.0 {#configuring-the-saml-authentication-handler}

El [consola web](/help/sites-deploying/configuring-osgi.md) proporciona acceso a la [SAML](https://saml.xml.org/saml-specifications) Configuración del controlador de autenticación 2.0 llamada **Controlador de autenticación de Adobe Granite SAML 2.0**. Se pueden configurar las siguientes propiedades.

>[!NOTE]
>
>El Controlador de autenticación SAML 2.0 está deshabilitado de forma predeterminada. Debe establecer al menos una de las siguientes propiedades para habilitar el controlador:
>
>* La URL del POST del proveedor de identidad o la URL del IDP.
>* El ID de entidad de Service Provider.
>


>[!NOTE]
>
>Las afirmaciones de SAML están firmadas y pueden cifrarse de forma opcional. Para que esto funcione, debe proporcionar al menos el certificado público del proveedor de identidad en el almacén de confianza. Consulte [Agregar el certificado IdP al almacén de confianza](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) para obtener más información.

**Ruta** Ruta de repositorio para la que Sling debe utilizar este controlador de autenticación. Si está vacío, el controlador de autenticación se deshabilitará.

**Clasificación de servicios** Valor de clasificación del servicio marco OSGi para indicar el orden en que se llama a este servicio. Es un valor entero en el que los valores más altos designan una prioridad mayor.

**Alias de certificado IDP** Alias del certificado del IdP en el almacén de confianza global. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado. AEM Consulte el capítulo &quot;Añadir el certificado IdP al almacén de confianza de&quot; a continuación sobre cómo configurarlo.

**URL de IDP** URL del IDP al que debe enviarse la solicitud de autenticación SAML. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado.

>[!CAUTION]
>
>El nombre de host del proveedor de identidad debe agregarse al **Filtro de referente de Apache Sling** Configuración de OSGi. Consulte la [consola web](/help/sites-deploying/configuring-osgi.md) para obtener más información.

**ID de entidad de Service Provider** ID que identifica de forma exclusiva a este proveedor de servicios con el proveedor de identidad. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado.

**Redirección predeterminada** La ubicación predeterminada a la que se redirigirá tras la autenticación correcta.

>[!NOTE]
>
>Esta ubicación solo se utiliza si la variable `request-path` no se ha establecido la cookie. Si solicita cualquier página por debajo de la ruta configurada sin un token de inicio de sesión válido, la ruta solicitada se almacenará en una cookie
>y el explorador se redirigirá a esta ubicación de nuevo después de la autenticación correcta.

**Atributo de ID de usuario** Nombre del atributo que contiene el ID de usuario utilizado para autenticar y crear el usuario en el repositorio CRX.

>[!NOTE]
>
>El ID de usuario no se toma de `saml:Subject` nodo de la aserción de SAML, pero desde esta `saml:Attribute`.

**Utilizar cifrado** Indica si este controlador de autenticación espera o no aserciones SAML cifradas.

**Crear automáticamente usuarios CRX** Indica si se crean o no automáticamente usuarios no existentes en el repositorio después de la autenticación correcta.

>[!CAUTION]
>
>Si la creación automática de usuarios CRX está deshabilitada, los usuarios deberán crearse manualmente.

**Añadir a grupos** Si un usuario debe agregarse automáticamente o no a los grupos CRX después de la autenticación correcta.

**Pertenencia a grupo** Nombre del saml: Attribute que contiene una lista de grupos CRX a los que debe agregarse este usuario.

## AEM Añadir el certificado IdP al almacén de confianza de la {#add-the-idp-certificate-to-the-aem-truststore}

Las afirmaciones de SAML están firmadas y pueden cifrarse de forma opcional. Para que esto funcione, debe proporcionar al menos el certificado público del IdP en el repositorio. Para ello, debe hacer lo siguiente:

1. Ir a *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Pulse el botón **[!UICONTROL Crear vínculo de TrustStore]**
1. Introduzca la contraseña de TrustStore y pulse **[!UICONTROL Guardar]**.
1. Haga clic en **[!UICONTROL Administrar TrustStore]**.
1. Cargue el certificado IdP.
1. Tome nota del alias del certificado. El alias es **[!UICONTROL admin#1436172864930]** en el ejemplo siguiente.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## AEM Agregue la cadena de certificado y la clave del proveedor de servicios al almacén de claves de la {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>Los pasos siguientes son obligatorios; de lo contrario, se generará la siguiente excepción: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Ir a: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Edite el `authentication-service` usuario.
1. Cree un almacén de claves haciendo clic en **Crear almacén de claves** bajo **Configuración de cuenta**.

>[!NOTE]
>
>Los siguientes pasos solo son necesarios si el controlador debe poder firmar o descifrar mensajes.

1. AEM Cree el certificado/par de claves para la. El comando para generarlo mediante openssl debe ser similar al ejemplo siguiente:

   `openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out certificate.crt -keyout key.pem`

1. Convertir la clave al formato PKCS#8 con codificación DER. AEM Este es el formato que requiere el almacén de claves de la.

   `openssl pkcs8 -topk8 -inform PEM -outform DER -in key.pem -out key.der -nocrypt`

1. Cargue el archivo de clave privada haciendo clic en **Seleccionar archivo de clave privada**.
1. Cargue el archivo de certificado haciendo clic en **Seleccionar archivos de cadena de certificados**.
1. Asigne un alias, como se muestra a continuación:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configuración de un registrador para SAML {#configure-a-logger-for-saml}

Puede configurar un registrador para depurar cualquier problema que pueda surgir por una configuración incorrecta de SAML. Para ello:

1. Vaya a la consola web en *http://localhost:4502/system/console/configMgr*
1. Busque y haga clic en la entrada llamada **Configuración del registrador de Apache Sling**
1. Cree un registrador con la siguiente configuración:

   * **Nivel de registro:** Depurar
   * **Archivo de registro:** logs/saml.log
   * **Registrador:** com.adobe.granite.auth.saml
