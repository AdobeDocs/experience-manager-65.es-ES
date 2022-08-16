---
title: Asignación de recursos
seo-title: Resource Mapping
description: Aprenda a definir redirecciones, direcciones URL de vanidad y hosts virtuales para AEM mediante la asignación de recursos.
seo-description: Learn how to define redirects, vanity URLs and virtual hosts for AEM by using resource mapping.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
source-git-commit: 7c24379c01f247f5ad45e3ecd40f3edef4ac3cfb
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 3%

---

# Asignación de recursos{#resource-mapping}

La asignación de recursos se utiliza para definir redirecciones, direcciones URL de vanidad y hosts virtuales para AEM.

Por ejemplo, puede utilizar estas asignaciones para:

* Agregue a todas las solicitudes el prefijo `/content` de modo que la estructura interna se oculte a los visitantes del sitio web.
* Defina una redirección para que todas las solicitudes a la variable `/content/en/gateway` se redireccionan a `https://gbiv.com/`.

Una posible asignación HTTP fija como prefijo todas las solicitudes a `localhost:4503` con `/content`. Una asignación como esta podría utilizarse para ocultar la estructura interna de los visitantes al sitio web, ya que permite:

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

Estas listas se pueden ver (junto con la información de configuración) en la sección **JCR ResourceResolver** de la consola Felix; por ejemplo, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Configuración Muestra la configuración actual (tal como se define en la [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* Prueba de configuración Esta opción le permite introducir una dirección URL o una ruta de acceso a un recurso. Haga clic en **Resolver** o **Mapa** para confirmar cómo el sistema transformará la entrada.

* **Resolver entradas de mapa**
La lista de entradas que utilizan los métodos ResourceResolver.resolve para asignar direcciones URL a los recursos.

* **Asignación de entradas de mapa**
Lista de entradas que utilizan los métodos ResourceResolver.map para asignar rutas de recursos a direcciones URL.

Las dos listas muestran varias entradas, incluidas las definidas como predeterminadas por las aplicaciones. A menudo tienen como objetivo simplificar las direcciones URL del usuario.

El par de listas a **Patrón**, una expresión regular que coincide con la solicitud, con un **Sustitución** que define la redirección que se va a imponer.

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

Esta es la estructura que se utiliza al definir asignaciones para el protocolo HTTP. Otras carpetas ( `sling:Folder`) se puede crear en `/etc/map` para cualquier otro protocolo que desee asignar.

#### Configuración de una redirección interna a /content {#configuring-an-internal-redirect-to-content}

Para crear la asignación que prefiere cualquier solicitud a https://localhost:4503/ con `/content`:

1. Con CRXDE, vaya a `/etc/map/http`.

1. Cree un nuevo nodo:

   * **Tipo** `sling:Mapping`
Este tipo de nodo está diseñado para estas asignaciones, aunque su uso no es obligatorio.

   * **Nombre** `localhost_any`

1. Haga clic en **Guardar todo**.
1. **Agregar** las siguientes propiedades para este nodo:

   * **Nombre** `sling:match`

      * **Tipo** `String`

      * **Valor** `localhost.4503/`
   * **Nombre** `sling:internalRedirect`

      * **Tipo** `String[]`

      * **Valor** `/content/`


1. Haga clic en **Guardar todo**.

Esto administrará una solicitud como:
`localhost:4503/geometrixx/en/products.html`
como si:
`localhost:4503/content/geometrixx/en/products.html`
se ha solicitado.

>[!NOTE]
>
>Consulte [Recursos](https://sling.apache.org/site/mappings-for-resource-resolution.html) en la documentación de Sling para obtener más información sobre las propiedades de Sling disponibles y cómo se pueden configurar.

>[!NOTE]
>
>Puede usar `/etc/map.publish` para guardar las configuraciones del entorno de publicación. Estos deben replicarse y la nueva ubicación ( `/etc/map.publish`) configurado para la variable **Ubicación de asignación** del [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) del entorno de publicación.
