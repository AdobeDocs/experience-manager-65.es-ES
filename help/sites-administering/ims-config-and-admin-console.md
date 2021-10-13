---
title: Autenticación IMS de Adobe y [!DNL Admin Console] compatibilidad con AEM Managed Services
seo-title: Adobe IMS Authentication and [!DNL Admin Console] Support for AEM Managed Services
description: Aprenda a utilizar el  [!DNL Admin Console] en AEM.
seo-description: Learn how to use the [!DNL Admin Console] in AEM.
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
source-git-commit: 1651fadeda0f2b37c90af2e1b2f84d74c118ccd9
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 11%

---

# Autenticación IMS de Adobe y [!DNL Admin Console] compatibilidad con AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>Tenga en cuenta que esta función solo está disponible para los clientes de Adobe Managed Services.

>[!NOTE]
>
>AEM no admite la asignación de grupos a perfiles.  Los usuarios deben agregarse individualmente en su lugar.

## Introducción {#introduction}

AEM 6.4.3.0 introduce compatibilidad con [!DNL Admin Console] instancias de AEM y autenticación basada en Adobe IMS (Identity Management System) para clientes de **AEM Managed Services**.

AEM incorporación a [!DNL Admin Console] permitirá a AEM clientes de Managed Services administrar todos los usuarios Experience Cloud en una consola. Los usuarios y grupos se pueden asignar a perfiles de producto asociados con instancias de AEM, lo que les permite iniciar sesión en una instancia específica.

## Puntos clave destacados {#key-highlights}

* AEM compatibilidad con la autenticación IMS solo es para autores, administradores o desarrolladores de AEM, no para usuarios finales externos del sitio del cliente como visitantes del sitio
* El [!DNL Admin Console] representará a AEM clientes de Managed Services como organizaciones de IMS y sus instancias como contextos de producto. Los administradores de sistemas de clientes y productos podrán administrar el acceso a las instancias
* AEM Managed Services sincronizará las topologías de los clientes con [!DNL Admin Console]. Habrá una instancia de AEM contexto de producto de Managed Services por instancia en [!DNL Admin Console].
* Los perfiles de producto de [!DNL Admin Console] determinarán a qué instancias puede acceder un usuario
* Se admite la autenticación federada utilizando los propios proveedores de identidad compatibles con SAML 2 de los clientes
* Solo se admitirán los Enterprise ID o Federated ID (para el inicio de sesión único del cliente), no los ID de Adobe personales.
* [!DNL User Management] (en Adobe  [!DNL Admin Console]) seguirá siendo propiedad de los administradores de clientes.

## Arquitectura {#architecture}

La autenticación IMS funciona mediante el protocolo OAuth entre AEM y el extremo IMS de Adobe. Una vez que se añade un usuario a IMS y tiene una identidad de Adobe, puede iniciar sesión en las instancias de AEM Managed Services con las credenciales de IMS.

El flujo de inicio de sesión del usuario se muestra a continuación; se redirige al usuario a IMS y, opcionalmente, al IDP del cliente para la validación de SSO y, a continuación, se le redirige de nuevo a AEM.

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## Cómo configurar {#how-to-set-up}

### Incorporación de organizaciones a [!DNL Admin Console] {#onboarding-organizations-to-admin-console}

La incorporación del cliente a [!DNL Admin Console] es un requisito previo para utilizar Adobe IMS para la autenticación AEM.

Como primer paso, los clientes deben tener una organización aprovisionada en Adobe IMS. Los clientes de Adobe Enterprise están representados como organizaciones de IMS en el [Adobe [!DNL Admin Console]](https://helpx.adobe.com/es/enterprise/using/admin-console.html).

AEM los clientes de Managed Services ya deben disponer de una organización aprovisionada y, como parte del aprovisionamiento de IMS, las instancias de cliente estarán disponibles en [!DNL Admin Console] para administrar las autorizaciones de usuario y el acceso.

El paso a IMS para la autenticación de usuarios será un esfuerzo conjunto entre AMS y los clientes, y cada uno de ellos tendrá que completar sus flujos de trabajo.

Una vez que un cliente existe como una organización de IMS y AMS se ha realizado con el aprovisionamiento del cliente para IMS, este es el resumen de los flujos de trabajo de configuración necesarios:

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. El administrador del sistema designado recibe una invitación para iniciar sesión en el [!DNL Admin Console]
1. El administrador del sistema reclama un dominio para confirmar la propiedad del dominio (en este ejemplo acme.com)
1. El administrador del sistema configura los directorios de usuario
1. El administrador del sistema configura el proveedor de identidad (IDP) en la [!DNL Admin Console] configuración de SSO.
1. El administrador de AEM administra los grupos locales, los permisos y los privilegios de la forma habitual. Consulte Sincronización de usuarios y grupos

>[!NOTE]
>
>Para obtener más información sobre los fundamentos de Identity Management de Adobe, incluida la configuración de IDP, consulte el artículo [esta página.](https://helpx.adobe.com/es/enterprise/using/set-up-identity.html)
>
>Para obtener más información sobre la Administración de Enterprise y [!DNL Admin Console] consulte el artículo [esta página](https://helpx.adobe.com/es/enterprise/managing/user-guide.html).

### Incorporación de usuarios a [!DNL Admin Console] {#onboarding-users-to-the-admin-console}

Existen tres formas de integrar a los usuarios en función del tamaño del cliente y de sus preferencias:

1. Crear manualmente usuarios y grupos en [!DNL Admin Console]
1. Cargar un archivo CSV con usuarios
1. Sincronice usuarios y grupos desde Active Directory empresarial del cliente.

#### Adición manual a través de la interfaz de usuario [!DNL Admin Console] {#manual-addition-through-admin-console-ui}

Los usuarios y grupos se pueden crear manualmente en la interfaz de usuario de [!DNL Admin Console]. Este método se puede utilizar si no tienen un gran número de usuarios que administrar. Por ejemplo, un número menor de 50 usuarios AEM.

Los usuarios también se pueden crear manualmente si el cliente ya está utilizando este método para administrar otros productos de Adobe como aplicaciones de Analytics, Target o Creative Cloud.

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Carga de archivos en la interfaz de usuario de [!DNL Admin Console] {#file-upload-in-the-admin-console-ui}

Para facilitar la gestión de la creación de usuarios, se puede cargar un archivo CSV para agregar usuarios de forma masiva:

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### Herramienta de sincronización de usuarios {#user-sync-tool}

La herramienta de sincronización de usuarios (UST en resumen) permite a los clientes empresariales crear o administrar usuarios de Adobe utilizando Active Directory u otros servicios de directorio OpenLDAP probados. Los usuarios de destino son administradores de identidad de TI (Enterprise Directory y administradores del sistema) que podrán instalar y configurar la herramienta. La herramienta de código abierto es personalizable para que los clientes puedan hacer que un desarrollador la modifique para adaptarla a sus propios requisitos particulares.

Cuando se ejecuta la sincronización de usuarios, se obtiene una lista de usuarios de Active Directory de la organización (o de cualquier otra fuente de datos compatible) y se compara con la lista de usuarios de [!DNL Admin Console]. A continuación, llama a la API de Adobe [!DNL User Management] para sincronizar el [!DNL Admin Console] con el directorio de la organización. El flujo de cambios es totalmente unidireccional; las ediciones realizadas en [!DNL Admin Console] no se insertan en el directorio.

La herramienta permite que el administrador del sistema asigne grupos de usuarios en el directorio del cliente con la configuración del producto y los grupos de usuarios en [!DNL Admin Console], la nueva versión del UST también permite la creación dinámica de grupos de usuarios en [!DNL Admin Console].

Para configurar la sincronización de usuarios, la organización debe crear un conjunto de credenciales de la misma manera que usaría la [[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

La sincronización de usuarios se distribuye a través del repositorio de GitHub de Adobe en esta ubicación:

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

Tenga en cuenta que la versión de prelanzamiento 2.4RC1 está disponible con compatibilidad para la creación de grupos dinámicos y se puede encontrar aquí: [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

Las principales características de esta versión son la capacidad de asignar dinámicamente nuevos grupos LDAP para la pertenencia de usuarios a [!DNL Admin Console], así como la creación dinámica de grupos de usuarios.

Puede encontrar más información sobre las nuevas funciones de grupo aquí:

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>Para obtener más información sobre la herramienta de sincronización de usuarios, consulte la [página de documentación](https://adobe-apiplatform.github.io/user-sync.py/es/).
>
>
>La herramienta de sincronización de usuarios debe registrarse como cliente de Adobe I/O UMAPI mediante el procedimiento descrito [aquí](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).
>
>La documentación de la consola Adobe I/O se encuentra [aquí](https://www.adobe.io/apis/cloudplatform/console.html).
>
>
>La API [!DNL User Management] que utiliza la herramienta de sincronización de usuarios se cubre en esta [ubicación](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

>[!NOTE]
>
>La configuración AEM de IMS la gestionará el equipo de Adobe Managed Services. Sin embargo, el administrador de clientes puede modificarlo según sus necesidades (por ejemplo, Pertenencia a grupos automática o Asignación de grupos). El cliente IMS también será registrado por su equipo de Managed Services.

## Usos {#how-to-use}

### Administración de productos y acceso de usuarios en [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

Cuando el administrador de productos del cliente inicia sesión en [!DNL Admin Console], verá varias instancias del contexto de producto de Managed Services de AEM como se muestra a continuación:

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

En este ejemplo, la organización *AEM-MS-Onboard* tiene 32 instancias que abarcan diferentes topologías y entornos como Stage, Prod, etc.

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

Los detalles de la instancia se pueden comprobar para identificar la instancia:

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

En cada instancia de contexto de producto, habrá un perfil de producto asociado. Este perfil de producto se utiliza para asignar acceso a usuarios y grupos.

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

Los usuarios y grupos agregados bajo este perfil de producto pueden iniciar sesión en esa instancia en , como se muestra en el ejemplo siguiente:

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### Iniciar sesión en AEM {#logging-into-aem}

#### Inicio de sesión de administrador local {#local-admin-login}

AEM seguir admitiendo los inicios de sesión locales para los usuarios administradores, ya que la pantalla de inicio de sesión tiene la opción de iniciar sesión localmente:

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### Inicio de sesión basado en IMS {#ims-based-login}

Para otros usuarios, el inicio de sesión basado en IMS se puede utilizar una vez que IMS esté configurado en la instancia. El usuario primero hará clic en el botón **Iniciar sesión con Adobe** como se muestra a continuación:

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

A continuación, se les redirigirá a la pantalla de inicio de sesión de IMS e introduzca sus credenciales:

![screen_shot_2018-09-17at15629pm](assets/screen_shot_2018-09-17at115629pm.png)

Si se configura un IDP federado durante la configuración inicial de [!DNL Admin Console], se redirigirá al usuario al IDP del cliente para SSO.

El IDP es Okta en el siguiente ejemplo:

![screen_shot_2018-09-17at15734pm](assets/screen_shot_2018-09-17at115734pm.png)

Una vez finalizada la autenticación, se redirige al usuario a AEM para iniciar sesión:

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### Migración de usuarios existentes {#migrating-existing-users}

Para las instancias de AEM existentes que utilizan otro método de autenticación y que ahora se están migrando a IMS, debe haber un paso de migración.

Los usuarios existentes en el repositorio de AEM (con origen local, a través de LDAP o SAML) se pueden migrar para que apunten a IMS como IDP con la Utilidad de migración de usuarios.

Su equipo de AMS ejecutará esta utilidad como parte del aprovisionamiento de IMS.

### Administración de permisos y ACL en AEM {#managing-permissions-and-acls-in-aem}

El control de acceso y los permisos se seguirán administrando en AEM, esto se puede lograr mediante la separación de los grupos de usuarios procedentes de IMS (por ejemplo, AEM-GRP-008 en el ejemplo siguiente) y los grupos locales donde se definen los permisos y el control de acceso. Los grupos de usuarios sincronizados con IMS se pueden asignar a grupos locales y heredar los permisos.

En el ejemplo siguiente, se añaden grupos sincronizados al grupo local *Dam_Users* como ejemplo.

En este caso, también se ha asignado un usuario a algunos grupos del [!DNL Admin Console]. ( Tenga en cuenta que los usuarios y grupos pueden sincronizarse desde LDAP mediante la herramienta de sincronización de usuarios o crearse localmente, consulte la sección **Incorporación de usuarios al[!DNL Admin Console]** anterior).

>[!NOTE]
>
>Los grupos de usuarios solo se sincronizan cuando los usuarios inician sesión en la instancia.

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

El usuario forma parte de los siguientes grupos en IMS:

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

Cuando el usuario inicia sesión, se sincronizan las suscripciones al grupo, como se muestra a continuación:

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

En AEM, los grupos de usuarios sincronizados con IMS se pueden agregar como miembros a grupos locales existentes, por ejemplo, usuarios de DAM.

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

Como se muestra a continuación, el grupo *AEM-GRP_008* hereda los permisos y privilegios de los usuarios de DAM. Esta es una forma eficaz de administrar permisos para grupos sincronizados y se utiliza comúnmente también en métodos de autenticación basados en LDAP.

![screen_shot_2018-09-17at10505pm](assets/screen_shot_2018-09-17at110505pm.png)
