---
title: Compatibilidad con token encapsulado
seo-title: Compatibilidad con token encapsulado
description: Obtenga información sobre la compatibilidad con el token encapsulado en AEM.
seo-description: Obtenga información sobre la compatibilidad con el token encapsulado en AEM.
uuid: a7c6f269-bb5a-49ba-abef-ea029202ab6d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 2c263c0d-2521-49df-88ba-f304a25af8ab
translation-type: tm+mt
source-git-commit: 29328ff7fde4ed0e7f9728af1be911133259dc6c

---


# Compatibilidad con token encapsulado{#encapsulated-token-support}

## Introducción {#introduction}

De forma predeterminada, AEM utiliza el controlador de autentificación de testigos para autenticar cada solicitud. Sin embargo, para poder enviar solicitudes de autenticación, el Controlador de autentificación de autentificador requiere acceso al repositorio para cada solicitud. Esto sucede porque las cookies se utilizan para mantener el estado de autenticación. Lógicamente, el estado debe persistir en el repositorio para validar las solicitudes posteriores. De hecho, esto significa que el mecanismo de autenticación tiene estado.

Esto es especialmente importante para la escalabilidad horizontal. En una configuración de varias instancias como la granja de publicaciones que se muestra a continuación, el equilibrio de carga no se puede lograr de forma óptima. Con la autenticación con estado, el estado de autenticación persistente solo estará disponible en la instancia en la que el usuario se autentique por primera vez.

![chlimage_1-33](assets/chlimage_1-33a.png)

Veamos el siguiente escenario como ejemplo:

Un usuario puede autenticarse en la instancia de publicación uno, pero si una solicitud subsiguiente va a la instancia de publicación dos, esa instancia no tiene ese estado de autenticación persistente, porque ese estado se mantuvo en el repositorio de la publicación uno y la publicación dos tiene su propio repositorio.

La solución para esto es configurar las conexiones adhesivas en el nivel de equilibrador de carga. Con las conexiones adhesivas, un usuario siempre se dirigiría a la misma instancia de publicación. Como consecuencia, no es posible un equilibrio de carga realmente óptimo.

Si una instancia de publicación deja de estar disponible, todos los usuarios autenticados en esa instancia perderán su sesión. Esto se debe a que se necesita acceso al repositorio para validar la cookie de autenticación.

## Autenticación sin estado con el token encapsulado {#stateless-authentication-with-the-encapsulated-token}

La solución para la escalabilidad horizontal es la autenticación sin estado con el uso de la nueva compatibilidad con Token encapsulado en AEM.

El autentificador encapsulado es un fragmento de criptografía que permite a AEM crear y validar de forma segura la información de autenticación sin conexión, sin tener acceso al repositorio. De este modo, puede producirse una solicitud de autenticación en todas las instancias de publicación y sin necesidad de conexiones adhesivas. También tiene la ventaja de mejorar el rendimiento de la autenticación, ya que no es necesario acceder al repositorio para cada solicitud de autenticación.

Puede ver cómo funciona esto en una implementación distribuida geográficamente con los autores de MongoMK y las instancias de publicación de TarMK a continuación:

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>Tenga en cuenta que el autentificador encapsulado trata de la autenticación. Garantiza que la cookie se pueda validar sin tener que acceder al repositorio. Sin embargo, sigue siendo necesario que el usuario exista en todas las instancias y que todas las instancias tengan acceso a la información almacenada en ese usuario.
>
>Por ejemplo, si se crea un nuevo usuario en la instancia de publicación número uno, debido al funcionamiento del token encapsulado, se autenticará correctamente en la publicación número dos. Si el usuario no existe en la segunda instancia de publicación, la solicitud no se realizará correctamente.


## Configuración del token encapsulado {#configuring-the-encapsulated-token}

Hay algunas cosas que debe tener en cuenta al configurar el token encapsulado:

1. Debido a la criptografía involucrada, todas las instancias necesitan tener la misma clave HMAC. Desde AEM 6.3, el material clave ya no se almacena en el repositorio, sino en el sistema de archivos real. Con esto en mente, la mejor manera de replicar las claves es copiarlas del sistema de archivos de la instancia de origen a la de las instancias de destino a las que desee replicar las claves. Ver más información debajo de &quot;Replicando la clave HMAC&quot;.
1. El token encapsulado debe estar habilitado. Esto se puede realizar a través de la consola web.

### Replicar la clave HMAC {#replicating-the-hmac-key}

La clave HMAC está presente como una propiedad binaria de `/etc/key` en el repositorio. Puede descargarlo por separado pulsando el vínculo de **visualización** que hay junto a él:

![chlimage_1-35](assets/chlimage_1-35a.png)

Para replicar la clave entre instancias, debe:

1. Acceda a la instancia de AEM, que suele ser una instancia de autor, que contiene el material clave que copiar;
1. Busque el `com.adobe.granite.crypto.file` paquete en el sistema de archivos local. Por ejemplo, en esta ruta:

   * &lt;author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21
   El `bundle.info` archivo dentro de cada carpeta identificará el nombre del paquete.

1. Vaya a la carpeta de datos. Por ejemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copie los archivos principales y HMAC.
1. A continuación, vaya a la instancia de destino en la que desee duplicar la clave HMAC y navegue a la carpeta de datos. Por ejemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Pegue los dos archivos que copió anteriormente.
1. [Actualice el paquete](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) de cifrado si la instancia de destino ya se está ejecutando.

1. Repita los pasos anteriores para todas las instancias en las que desee replicar la clave.

#### Activación del token encapsulado {#enabling-the-encapsulated-token}

Una vez replicada la clave HMAC, puede habilitar el token encapsulado mediante la consola web:

1. Elija el explorador para `https://serveraddress:port/system/console/configMgr`
1. Busque una entrada denominada Controlador **de autentificación de autentificador CRX de** día y haga clic en ella.
1. En la siguiente ventana, marque la casilla **Activar compatibilidad** con token encapsulado y pulse **Guardar**.

