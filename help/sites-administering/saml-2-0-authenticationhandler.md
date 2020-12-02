---
title: Controlador de autenticación SAML 2.0
seo-title: Controlador de autenticación SAML 2.0
description: Obtenga información sobre el controlador de autenticación SAML 2.0 en AEM.
seo-description: Obtenga información sobre el controlador de autenticación SAML 2.0 en AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
translation-type: tm+mt
source-git-commit: d559a15e3c1c65c39e38935691835146f54a356e
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---


# Controlador de autenticación SAML 2.0{#saml-authentication-handler}

AEM incluye un controlador de autenticación [SAML](http://saml.xml.org/saml-specifications). Este controlador proporciona compatibilidad con el protocolo de solicitud de autenticación [SAML](http://saml.xml.org/saml-specifications) 2.0 (perfil Web-SSO) mediante el enlace `HTTP POST`.

Admite:

* firma y cifrado de mensajes
* creación automática de usuarios
* sincronizar grupos con los existentes en AEM
* Autenticación iniciada por proveedor de servicio y proveedor de identidad

Este controlador almacena el mensaje de respuesta de SAML cifrado en el nodo de usuario ( `usernode/samlResponse`) para facilitar la comunicación con un Proveedor de servicio de terceros.

>[!NOTE]
>
>Consulte [una demostración de la integración de AEM y SAML](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html).
>
>Para leer un artículo de comunidad de extremo a extremo, haga clic en: [Integración de SAML con Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/aem63_saml.html).

## Configuración del controlador de autenticación SAML 2.0 {#configuring-the-saml-authentication-handler}

La [consola web](/help/sites-deploying/configuring-osgi.md) proporciona acceso a la configuración del controlador de autenticación [SAML](http://saml.xml.org/saml-specifications) 2.0 denominado **Controlador de autenticación de granito de Adobe SAML 2.0**. Se pueden establecer las siguientes propiedades.

>[!NOTE]
>
>El controlador de autenticación SAML 2.0 está deshabilitado de forma predeterminada. Debe establecer al menos una de las siguientes propiedades para habilitar el controlador:
>
>* Dirección URL del POST del proveedor de identidad.
>* ID de entidad de Proveedor de servicio.

>



>[!NOTE]
>
>Las aserciones SAML están firmadas y pueden cifrarse de forma opcional. Para que esto funcione, debe proporcionar al menos el certificado público del proveedor de identidad en TrustStore. Consulte [Añadir el certificado IdP a la sección TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) para obtener más información.

**Ruta** PathRepository para la cual Sling debe utilizar este controlador de autenticación. Si está vacío, el controlador de autenticación se desactivará.

**Clasificación** de serviciosValor de clasificación de servicios de OSGi Framework para indicar el orden en que se llama a este servicio. Se trata de un valor entero en el que los valores más altos designan una prioridad mayor.

**Alias de certificado** de IDPalias del certificado de IdP en el almacén de confianza global. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado. Consulte el capítulo &quot;Añadir el certificado de IdP al almacén de confianza de AEM&quot; a continuación sobre cómo configurarlo.

**URL del proveedor de identidad** del IDP al que se debe enviar la solicitud de autenticación SAML. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado.

>[!CAUTION]
>
>El nombre de host del proveedor de identidad debe agregarse a la configuración OSGi del **Filtro de Remitente del reenvío Sling de Apache**. Consulte la sección [Consola Web](/help/sites-deploying/configuring-osgi.md) para obtener más información.

**Identificador** IDID de entidad proveedor de servicio que identifica exclusivamente a este proveedor de servicio con el proveedor de identidad. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado.

**Redirección** predeterminadaUbicación predeterminada a la que se redirigirá después de autenticarse correctamente.

>[!NOTE]
>
>Esta ubicación solo se utiliza si la cookie `request-path` no está configurada. Si solicita cualquier página debajo de la ruta configurada sin un autentificador de inicio de sesión válido, la ruta solicitada se almacena en una cookie
>y el explorador se redirigirá a esta ubicación nuevamente después de autenticarse correctamente.

**Atributo de ID de usuario** El nombre del atributo que contiene el ID de usuario utilizado para autenticar y crear el usuario en el repositorio de CRX.

>[!NOTE]
>
>El ID de usuario no se obtendrá del nodo `saml:Subject` de la afirmación SAML, sino de este `saml:Attribute`.

**Usar** cifradoIndependientemente de si este controlador de autenticación espera o no aserciones de SAML cifradas.

**Crear automáticamente** usuarios de CRXntroduzca o no automáticamente los usuarios no existentes en el repositorio después de autenticarse correctamente.

>[!CAUTION]
>
>Si la creación automática de usuarios de CRX está deshabilitada, los usuarios deberán crearse manualmente.

**Añadir a** gruposIndica si un usuario debe agregarse automáticamente a los grupos de CRX después de autenticarse correctamente.

**Pertenencia** al grupoNombre del saml:Attribute que contiene una lista de grupos CRX a los que se debe agregar este usuario.

## Añadir el certificado de IdP a AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}

Las aserciones SAML están firmadas y pueden cifrarse de forma opcional. Para que esto funcione, debe proporcionar al menos el certificado público del IdP en el repositorio. Para ello, debe:

1. Vaya a *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Presione el vínculo **[!UICONTROL Crear TrustStore]**
1. Introduzca la contraseña de TrustStore y pulse **[!UICONTROL Guardar]**.
1. Haga clic en **[!UICONTROL Administrar TrustStore]**.
1. Cargue el certificado de IdP.
1. Tome nota del alias del certificado. El alias es **[!UICONTROL admin#1436172864930]** en el ejemplo siguiente.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Añada la cadena de certificado y clave de Proveedor de servicio al almacén de claves de AEM {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>Los pasos siguientes son obligatorios; de lo contrario, se generará la siguiente excepción: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Ir a: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Edite el usuario `authentication-service`.
1. Cree un KeyStore haciendo clic en **Crear KeyStore** en **Configuración de la cuenta**.

>[!NOTE]
>
>Los pasos siguientes solo son necesarios si el controlador debe poder firmar o descifrar mensajes.

1. Cargue el archivo de clave privada haciendo clic en **Seleccionar archivo de clave privada**. La clave debe estar en formato PKCS#8 con codificación DER.
1. Cargue el archivo de certificado haciendo clic en **Seleccionar archivos de cadena de certificado**.
1. Asignar un alias, como se muestra a continuación:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configurar un registrador para SAML {#configure-a-logger-for-saml}

Puede configurar un registrador para depurar cualquier problema que pueda surgir al configurar mal SAML. Puede hacerlo mediante:

1. Accediendo a la consola web, en *http://localhost:4502/system/console/configMgr*
1. Busque y haga clic en la entrada denominada **Configuración del registrador de registros de Apache Sling**
1. Cree un registrador con la siguiente configuración:

   * **Nivel de registro:** Depuración
   * **Archivo de registro:** logs/saml.log
   * **Logger:** com.adobe.granite.auth.saml

