---
title: Compatibilidad con tokens encapsulados
seo-title: Encapsulated Token Support
description: Obtenga información sobre la compatibilidad con Token encapsulado en AEM.
seo-description: Learn about the Encapsulated Token support in AEM.
uuid: a7c6f269-bb5a-49ba-abef-ea029202ab6d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 2c263c0d-2521-49df-88ba-f304a25af8ab
exl-id: e24d815c-83e2-4639-8273-b4c0a6bb008a
source-git-commit: 32e2a30d9f3327d26b81a07730ace04e4e68b0d1
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# Compatibilidad con tokens encapsulados{#encapsulated-token-support}

## Introducción {#introduction}

De forma predeterminada, AEM utiliza el controlador de autenticación de tokens para autenticar cada solicitud. Sin embargo, para servir solicitudes de autenticación, el gestor de autenticación de tokens requiere acceso al repositorio para cada solicitud. Esto sucede porque las cookies se utilizan para mantener el estado de autenticación. Lógicamente, el estado debe persistir en el repositorio para validar las solicitudes posteriores. De hecho, esto significa que el mecanismo de autenticación tiene estado.

Esto es de particular importancia para la escalabilidad horizontal. En una configuración de varias instancias como la granja de servidores de publicación que se muestra a continuación, el equilibrio de carga no se puede lograr de una manera óptima. Con la autenticación mediante estado, el estado de autenticación persistente solo estará disponible en la instancia en la que el usuario se autentique por primera vez.

![chlimage_1-33](assets/chlimage_1-33a.png)

Veamos el siguiente escenario como ejemplo:

Un usuario puede autenticarse en la instancia de publicación uno, pero si una solicitud posterior va a publicar la instancia dos, esa instancia no tiene ese estado de autenticación persistente, porque ese estado se persistió en el repositorio de publicación uno y la publicación dos tiene su propio repositorio.

La solución para esto es configurar las conexiones duraderas en el nivel de equilibrador de carga. Con conexiones duraderas, un usuario siempre sería dirigido a la misma instancia de publicación. Como consecuencia, no es posible un equilibrio de carga realmente óptimo.

Si una instancia de publicación deja de estar disponible, todos los usuarios autenticados en esa instancia perderán su sesión. Esto se debe a que se necesita acceso al repositorio para validar la cookie de autenticación.

## Autenticación sin estado con el token encapsulado {#stateless-authentication-with-the-encapsulated-token}

La solución para la escalabilidad horizontal es la autenticación sin estado con el uso del nuevo soporte de Token Encapsulado en AEM.

El Token encapsulado es un trozo de criptografía que permite AEM crear y validar de forma segura la información de autenticación sin conexión, sin acceder al repositorio. De este modo, puede producirse una solicitud de autenticación en todas las instancias de publicación y sin necesidad de conexiones duraderas. También tiene la ventaja de mejorar el rendimiento de la autenticación, ya que no es necesario acceder al repositorio para cada solicitud de autenticación.

Puede ver cómo funciona esto en una implementación distribuida geográficamente con los autores de MongoMK y las instancias de publicación de TarMK a continuación:

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>Tenga en cuenta que el token encapsulado se refiere a la autenticación. Garantiza que la cookie se pueda validar sin tener que acceder al repositorio. Sin embargo, sigue siendo necesario que el usuario exista en todas las instancias y que todas las instancias puedan acceder a la información almacenada debajo de ese usuario.
>
>Por ejemplo, si se crea un nuevo usuario en la instancia de publicación número uno, debido al modo en que funciona el token encapsulado, se autenticará correctamente en la publicación número dos. Si el usuario no existe en la segunda instancia de publicación, la solicitud seguirá sin tener éxito.

## Configuración del token encapsulado {#configuring-the-encapsulated-token}

>[!NOTE]
>Todos los controladores de autenticación que sincronizan usuarios y dependen de la autenticación de tokens (como SAML y OAuth) solo funcionarán con tokens encapsulados si:
>
>* Las sesiones adhesivas están habilitadas o
>
>* Los usuarios ya se han creado en AEM al iniciarse la sincronización. Esto significa que los tokens encapsulados no se admitirán en situaciones en las que los controladores **create** usuarios durante el proceso de sincronización.


Hay algunas cosas que debe tener en cuenta al configurar el token encapsulado:

1. Debido a la criptografía involucrada, todas las instancias necesitan tener la misma clave HMAC. Desde AEM 6.3, el material clave ya no se almacena en el repositorio, sino en el sistema de archivos real. Con esto en mente, la mejor manera de replicar las claves es copiarlas del sistema de archivos de la instancia de origen a la de las instancias de destino a las que desee replicar las claves. Vea más información en &quot;Replicando la clave HMAC&quot; a continuación.
1. El token encapsulado debe estar habilitado. Esto se puede hacer a través de la Consola Web.

### Duplicación de la clave HMAC {#replicating-the-hmac-key}

La clave HMAC está presente como una propiedad binaria de `/etc/key` en el repositorio. Puede descargarlo por separado pulsando el enlace **view** situado junto a él:

![chlimage_1-35](assets/chlimage_1-35a.png)

Para poder replicar la clave entre instancias, debe:

1. Acceda a la instancia de AEM, normalmente una instancia de autor, que contiene el material clave que se va a copiar;
1. Busque el paquete `com.adobe.granite.crypto.file` en el sistema de archivos local. Por ejemplo, en esta ruta:

   * &lt;author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21

   El archivo `bundle.info` dentro de cada carpeta identificará el nombre del paquete.

1. Vaya a la carpeta de datos. Por ejemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copie los archivos HMAC y maestro.
1. A continuación, vaya a la instancia de destino a la que desee duplicar la clave HMAC y vaya a la carpeta de datos. Por ejemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Pegue los dos archivos que ha copiado anteriormente.
1. [Actualice Crypto ](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) Bundlesi la instancia de destino ya se está ejecutando.

1. Repita los pasos anteriores para todas las instancias en las que desee replicar la clave.

#### Activación del token encapsulado {#enabling-the-encapsulated-token}

Una vez replicada la clave HMAC, puede habilitar el token encapsulado a través de la consola web:

1. Apunte el navegador a `https://serveraddress:port/system/console/configMgr`
1. Busque una entrada denominada **Adobe Granite Token Authentication Handler** y haga clic en ella.
1. En la siguiente ventana, marque la casilla **Enable encapsulated token support** y presione **Save**.
