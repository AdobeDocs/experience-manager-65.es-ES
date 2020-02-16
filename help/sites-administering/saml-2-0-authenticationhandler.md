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
source-git-commit: a44d655871308dac34671f0af2c4a0017eba5793

---


# Controlador de autenticación SAML 2.0{#saml-authentication-handler}

AEM se envía con un controlador de autenticación [SAML](http://saml.xml.org/saml-specifications) . Este controlador proporciona compatibilidad con el protocolo de solicitud de autenticación [SAML](http://saml.xml.org/saml-specifications) 2.0 (perfil Web-SSO) mediante el `HTTP POST` enlace.

Admite:

* firma y cifrado de mensajes
* creación automática de usuarios
* sincronizar grupos con los existentes en AEM
* Autenticación iniciada por el proveedor de servicios y el proveedor de identidad

Este controlador almacena el mensaje de respuesta de SAML cifrado en el nodo de usuario ( `usernode/samlResponse`) para facilitar la comunicación con un proveedor de servicios de terceros.

>[!NOTE]
>
>Consulte [una demostración de la integración](https://helpx.adobe.com/cq/kb/saml-demo.html)de AEM y SAML.
>
>Para leer un artículo de comunidad de extremo a extremo, haga clic en: [Integración de SAML con Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/aem63_saml.html).

## Configuración del controlador de autenticación SAML 2.0 {#configuring-the-saml-authentication-handler}

La consola [](/help/sites-deploying/configuring-osgi.md) web proporciona acceso a la configuración del controlador de autenticación [SAML](http://saml.xml.org/saml-specifications) 2.0, denominado Controlador de autenticación **Adobe Granite SAML 2.0**. Se pueden establecer las siguientes propiedades.

>[!NOTE]
>
>El controlador de autenticación SAML 2.0 está deshabilitado de forma predeterminada. Debe establecer al menos una de las siguientes propiedades para habilitar el controlador:
>
>* Dirección URL POST del proveedor de identidad.
>* ID de entidad del proveedor de servicios.
>



>[!NOTE]
>
>Las aserciones SAML están firmadas y pueden cifrarse de forma opcional. Para que esto funcione, debe proporcionar al menos el certificado público del proveedor de identidad en TrustStore. Consulte [Adición del certificado de IdP a la sección TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) para obtener más información.

**Ruta** de acceso del repositorio para la cual Sling debe utilizar este controlador de autenticación. Si está vacío, el controlador de autenticación se desactivará.

**Valor de clasificación de servicios** OSGi Framework Service Ranking para indicar el orden en el que llamar a este servicio. Se trata de un valor entero en el que los valores más altos designan una prioridad mayor.

**Alias** de certificado de IDP El alias del certificado de IdP en el almacén de confianza global. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado. Consulte el capítulo &quot;Adición del certificado de IdP al almacén de confianza de AEM&quot; que aparece a continuación sobre cómo configurarlo.

**Dirección URL** del proveedor de identidad del IDP al que se debe enviar la solicitud de autenticación SAML. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado.

>[!CAUTION]
>
>El nombre de host del proveedor de identidad debe agregarse a la configuración OSGi del filtro **de referente de Sling de** Apache. Consulte la sección Consola [](/help/sites-deploying/configuring-osgi.md) web para obtener más información.

**ID** de entidad del proveedor de servicios que identifica exclusivamente a este proveedor de servicios con el proveedor de identidad. Si esta propiedad está vacía, el controlador de autenticación está deshabilitado.

**Redirección** predeterminada La ubicación predeterminada a la que se redirigirá después de autenticarse correctamente.

>[!NOTE]
>
>Esta ubicación solo se utiliza si no se ha establecido la `request-path` cookie. Si solicita cualquier página debajo de la ruta configurada sin un autentificador de inicio de sesión válido, la ruta solicitada se almacena en una cookie
>y el explorador se redirigirá a esta ubicación nuevamente después de autenticarse correctamente.

**Atributo** de ID de usuario El nombre del atributo que contiene el ID de usuario utilizado para autenticar y crear el usuario en el repositorio de CRX.

>[!NOTE]
>
>El ID de usuario no se tomará del `saml:Subject` nodo de la afirmación SAML sino de esto `saml:Attribute`.

**Usar cifrado** Indica si este controlador de autenticación espera o no afirmaciones de SAML cifradas.

**Crear automáticamente usuarios** de CRX Si desea o no crear automáticamente usuarios no existentes en el repositorio después de autenticarse correctamente.

>[!CAUTION]
>
>Si la creación automática de usuarios de CRX está deshabilitada, los usuarios deberán crearse manualmente.

**Agregar a grupos** Indica si un usuario debe agregarse automáticamente a los grupos de CRX después de autenticarse correctamente.

**Pertenencia** al grupo El nombre de saml:Attribute que contiene una lista de grupos de CRX a los que se debe agregar este usuario.

## Agregar el certificado de IdP al almacén de confianza de AEM {#add-the-idp-certificate-to-the-aem-truststore}

Las aserciones SAML están firmadas y pueden cifrarse de forma opcional. Para que esto funcione, debe proporcionar al menos el certificado público del IdP en el repositorio. Para ello, debe:

1. Vaya a *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. Pulse el vínculo **[!UICONTROL Crear almacén de confianza]**
1. Introduzca la contraseña de TrustStore y pulse **[!UICONTROL Guardar]**.
1. Haga clic en **[!UICONTROL Administrar TrustStore]**.
1. Cargue el certificado de IdP.
1. Tome nota del alias del certificado. El alias es **[!UICONTROL admin#1436172864930]** en el ejemplo siguiente.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## Adición de la cadena de certificados y la clave del proveedor de servicios al almacén de claves de AEM {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>Los pasos siguientes son obligatorios; de lo contrario, se generará la siguiente excepción: `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. Ir a: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. Edite el `authentication-service` usuario.
1. Para crear un almacén de claves, haga clic en **Crear almacén de claves** en Configuración **de cuenta**.

>[!NOTE]
>
>Los pasos siguientes solo son necesarios si el controlador debe poder firmar o descifrar mensajes.

1. Cargue el archivo de clave privada haciendo clic en **Seleccionar archivo** de clave privada. La clave debe estar en formato PKCS#8 con codificación DER.
1. Cargue el archivo de certificado haciendo clic en **Seleccionar archivos** de cadena de certificado.
1. Asignar un alias, como se muestra a continuación:

   ![chlimage_1-373](assets/chlimage_1-373.png)

## Configurar un registrador para SAML {#configure-a-logger-for-saml}

Puede configurar un registrador para depurar cualquier problema que pueda surgir al configurar mal SAML. Puede hacerlo mediante:

1. Ir a la consola web, en *http://localhost:4502/system/console/configMgr*
1. Busque y haga clic en la entrada denominada Configuración del registrador de registros **Apache Sling.**
1. Cree un registrador con la siguiente configuración:

   * **** Nivel de registro: Depurar
   * **** Archivo de registro: logs/saml.log
   * **** Registrador: com.adobe.granite.auth.saml

