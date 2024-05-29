---
title: AEM Configuración de integraciones de IMS para la
description: AEM Obtenga información sobre cómo configurar integraciones de IMS para la
source-git-commit: 8540b1af3c0779f692f829d4c61112d36bd81a00
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 90%

---


# AEM Configuración de integraciones de IMS para la {#setting-up-ims-integrations-for-aem}

<!--

>[!NOTE]
>
>Adobe customers use [Adobe Developer Console](https://developer.adobe.com/console) to generate credentials that enable access to various APIs. Customers select from various credential types ranging from OAuth Server-to-Server to Single-Page App. One of those credential types, Service Account (JWT) credentials, has been deprecated in favor of the OAuth Server-to-Server credentials with Service Pack 20. This change can be back ported to older Service Packs, starting with Service Pack 11 up to Service Pack 20 with the use of a hotfix that you can download here. -->

Adobe Experience Manager AEM () se puede integrar con muchas otras soluciones de Adobe. Por ejemplo, Adobe Target y Adobe Analytics, entre otras.

Las integraciones utilizan una integración de IMS configurada con S2S OAuth.

* Una vez que haya creado lo siguiente:

   * [las credenciales en Developer Console](#credentials-in-the-developer-console)

* Puede avanzar con lo siguiente:

   * Crear una (nueva) [Configuración de OAuth](#creating-oauth-configuration)

   * [Migrar una configuración JWT existente a una configuración de OAuth.](#migrating-existing-JWT-configuration-to-oauth)

>[!CAUTION]
>
>Anteriormente, las configuraciones se hacían con las [credenciales JWT que ahora están en desuso en Adobe Developer Console](/help/sites-administering/jwt-credentials-deprecation-in-adobe-developer-console.md).
>
>Estas configuraciones ya no se pueden crear ni actualizar, pero sí migrar a las configuraciones de OAuth.

## Credenciales en Developer Console {#credentials-in-the-developer-console}

Como primer paso, debe configurar las credenciales de OAuth en Adobe Developer Console.

Para obtener detalles sobre cómo hacer esto, consulte la documentación de Developer Console, según lo que necesite:

* Información general:

   * [Autenticación de servidor a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

* Creación de una nueva credencial de OAuth:

   * [Guía de implementación de credenciales de servidor a servidor de OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)

* Migración de una credencial JWT existente a una credencial de OAuth:

   * [Migración de una credencial de cuenta de servicio (JWT) a una credencial de servidor a servidor de OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)

Por ejemplo:

![Credencial de OAuth en Developer Console](assets/ims-configuration-developer-console.png)

## Creación de una configuración de OAuth {#creating-oauth-configuration}

Para crear una nueva integración de Adobe IMS con OAuth, haga lo siguiente:

1. En AEM, navegue hasta **Herramientas**, **Seguridad**, **Integración de IMS de Adobe**.

1. Seleccione **Crear**.

1. Complete la configuración en función de los detalles de [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/). Por ejemplo:

   ![Crear configuración de OAuth](assets/ims-create-oauth-configuration.png)

1. **Guarde** los cambios.

## Migración de una configuración JWT existente a una configuración de OAuth {#migrating-existing-JWT-configuration-to-oauth}

Para migrar una integración de IMS de Adobe existente basada en las credenciales de JWT, haga lo siguiente:

>[!NOTE]
>
>Este ejemplo muestra una configuración de IMS de Launch.

1. En AEM, navegue hasta **Herramientas**, **Seguridad**, **Integración de IMS de Adobe**.

1. Seleccione la configuración JWT que debe migrarse. Las configuraciones JWT se marcan con la advertencia **Credenciales de JWT (en desuso)**.

1. Seleccione **Propiedades**.

   ![Seleccione la configuración de JWT](assets/ims-migrate-jwt-select-configuration.png)

1. La configuración se abre como de solo lectura:

   ![Propiedades de configuración: solo lectura](assets/ims-migrate-jwt-properties-read-only.png)

1. Seleccione **OAuth** en la lista desplegable **Tipo de autenticación**:

   ![Seleccione Tipo de autenticación](assets/ims-migrate-jwt-authentication-type.png)

1. Se actualizarán las propiedades disponibles. Utilice los detalles de Developer Console para completarlos:

   ![Complete los detalles de OAuth](assets/ims-migrate-jwt-complete-oauth-details.png)

1. Use **Guardar y cerrar** para conservar las actualizaciones.
Cuando vuelva a la consola, la advertencia **Credenciales de JWT (en desuso)** habrá desaparecido.