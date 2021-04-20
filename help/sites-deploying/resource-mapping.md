---
title: Asignación de recursos
seo-title: Asignación de recursos
description: Aprenda a definir redirecciones, direcciones URL de vanidad y hosts virtuales para AEM mediante la asignación de recursos.
seo-description: Aprenda a definir redirecciones, direcciones URL de vanidad y hosts virtuales para AEM mediante la asignación de recursos.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# Asignación de recursos{#resource-mapping}

La asignación de recursos se utiliza para definir redirecciones, direcciones URL de vanidad y hosts virtuales para AEM.

Por ejemplo, puede utilizar estas asignaciones para:

* Agregue a todas las solicitudes el prefijo `/content` para que la estructura interna esté oculta para los visitantes del sitio web.
* Defina un redireccionamiento para que todas las solicitudes a la página `/content/en/gateway` del sitio web se redirijan a `https://gbiv.com/`.

Una posible asignación HTTP antepone todas las solicitudes a `localhost:4503` con `/content`. Una asignación como esta podría utilizarse para ocultar la estructura interna de los visitantes al sitio web, ya que permite:

`localhost:4503/content/we-retail/en/products.html`

para acceder a través de:

`localhost:4503/we-retail/en/products.html`

ya que la asignación agregará automáticamente el prefijo `/content` a `/we-retail/en/products.html`.

>[!CAUTION]
>
>Las URL mnemónicas no admiten patrones regex.

>[!NOTE]
>
>Consulte la documentación de Sling y [Asignaciones para la resolución de recursos](https://sling.apache.org/site/resources.html) y [Recursos](https://sling.apache.org/site/mappings-for-resource-resolution.html) para obtener más información.

## Visualización de definiciones de asignación {#viewing-mapping-definitions}

Las asignaciones forman dos listas que el JCR Resource Resolver evalúa (de arriba abajo) para encontrar una coincidencia.

Estas listas se pueden ver (junto con la información de configuración) en la opción **JCR ResourceResolver** de la consola Felix; por ejemplo, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Configuración
Muestra la configuración actual (tal como se define para el [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* Prueba de configuración
Esto le permite introducir una dirección URL o una ruta de recurso. Haga clic en **Resolver** o **Mapa** para confirmar cómo el sistema transformará la entrada.

* **Resuelva**
Entradas de mapaLa lista de entradas que usan los métodos ResourceResolver.resolve para asignar direcciones URL a los recursos.

* **Asignación de**
Entradas de mapaLa lista de entradas que usan los métodos ResourceResolver.map para asignar las rutas de recursos a las URL.

Las dos listas muestran varias entradas, incluidas las definidas como predeterminadas por las aplicaciones. A menudo tienen como objetivo simplificar las direcciones URL del usuario.

Las listas emparejan un **Pattern**, una expresión regular que coincide con la solicitud, con un **Replace** que define la redirección que se va a imponer.

Por ejemplo, el:

**Patrón** `^[^/]+/[^/]+/welcome$`

déclencheur de:

**Reemplazo** `/libs/cq/core/content/welcome.html`.

para redirigir una solicitud:

`https://localhost:4503/welcome` ``

hasta:

`https://localhost:4503/libs/cq/core/content/welcome.html`

Se crean nuevas definiciones de asignación dentro del repositorio.

>[!NOTE]
>
>Hay muchos recursos disponibles que ayudan a explicar cómo definir expresiones regulares; por ejemplo [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Creación de definiciones de asignación en AEM {#creating-mapping-definitions-in-aem}

En una instalación estándar de AEM puede encontrar la carpeta :

`/etc/map/http`

Esta es la estructura que se utiliza al definir asignaciones para el protocolo HTTP. Se pueden crear otras carpetas ( `sling:Folder`) en `/etc/map` para cualquier otro protocolo que desee asignar.

#### Configuración de una redirección interna a /content {#configuring-an-internal-redirect-to-content}

Para crear la asignación que prefiere cualquier solicitud a https://localhost:4503/ con `/content`:

1. Con CRXDE, vaya a `/etc/map/http`.

1. Cree un nuevo nodo:

   * **** `sling:Mapping`
Tipo: este tipo de nodo está diseñado para estas asignaciones, aunque su uso no es obligatorio.

   * **Nombre** `localhost_any`

1. Haga clic en **Guardar todo**.
1. **** Añada las siguientes propiedades a este nodo:

   * **Nombre** `sling:match`

      * **Tipo** `String`

      * **Valor** `localhost.4503/`
   * **Nombre** `sling:internalRedirect`

      * **Tipo** `String`

      * **Valor** `/content/`


1. Haga clic en **Guardar todo**.

Esto administrará una solicitud como:
`localhost:4503/geometrixx/en/products.html`
como si:
`localhost:4503/content/geometrixx/en/products.html`
se ha solicitado.

>[!NOTE]
>
>Consulte [Resources](https://sling.apache.org/site/mappings-for-resource-resolution.html) en la documentación de Sling para obtener más información sobre las propiedades de Sling disponibles y cómo se pueden configurar.

>[!NOTE]
>
>Puede utilizar `/etc/map.publish` para guardar las configuraciones del entorno de publicación. A continuación, se deben replicar y la nueva ubicación ( `/etc/map.publish`) se debe configurar para la **Ubicación de asignación** del [resolver recursos de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) del entorno de publicación.

