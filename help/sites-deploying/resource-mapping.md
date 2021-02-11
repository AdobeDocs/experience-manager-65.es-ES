---
title: Asignación de recursos
seo-title: Asignación de recursos
description: Obtenga información sobre cómo definir redirecciones, direcciones URL personales y hosts virtuales para AEM mediante la asignación de recursos.
seo-description: Obtenga información sobre cómo definir redirecciones, direcciones URL personales y hosts virtuales para AEM mediante la asignación de recursos.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 1%

---


# Asignación de recursos{#resource-mapping}

La asignación de recursos se utiliza para definir redirecciones, direcciones URL personales y hosts virtuales para AEM.

Por ejemplo, puede utilizar estas asignaciones para:

* Pruebe todas las solicitudes con `/content` para que la estructura interna se oculte de los visitantes del sitio web.
* Defina un redireccionamiento para que todas las solicitudes a la página `/content/en/gateway` del sitio Web se redirijan a `https://gbiv.com/`.

Una posible asignación HTTP antepone todas las solicitudes a `localhost:4503` con `/content`. Una asignación como esta podría utilizarse para ocultar la estructura interna de los visitantes al sitio web, ya que permite:

`localhost:4503/content/we-retail/en/products.html`

para acceder a ellos mediante:

`localhost:4503/we-retail/en/products.html`

ya que la asignación agregará automáticamente el prefijo `/content` a `/we-retail/en/products.html`.

>[!CAUTION]
>
>Las direcciones URL de vanidad no admiten patrones regex.

>[!NOTE]
>
>Consulte la documentación de Sling y [Asignaciones para la resolución de recursos](https://sling.apache.org/site/resources.html) y [Recursos](https://sling.apache.org/site/mappings-for-resource-resolution.html) para obtener más información.

## Visualización de definiciones de asignación {#viewing-mapping-definitions}

Las asignaciones forman dos listas que el Resueltor de recursos JCR evalúa (de arriba abajo) para encontrar una coincidencia.

Estas listas se pueden ver (junto con la información de configuración) en la opción **JCR ResourceResolver** de la consola Felix; por ejemplo, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Configuración
Muestra la configuración actual (tal como se define para el [Resolver recurso sling de Apache](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* Prueba de configuración
Esto le permite introducir una dirección URL o ruta de recursos. Haga clic en **Resolver** o **Asignar** para confirmar cómo el sistema transformará la entrada.

* **Resolver**
entradas de mapaLa lista de entradas utilizadas por los métodos ResourceResolver.resolve para asignar direcciones URL a recursos.

* **Asignación de**
entradas de mapaLa lista de entradas que utilizan los métodos ResourceResolver.map para asignar rutas de recursos a direcciones URL.

Las dos listas muestran varias entradas, incluidas las definidas como predeterminadas por las aplicaciones. Estos suelen tener como objetivo simplificar las direcciones URL del usuario.

El par de listas **Patrón**, una expresión regular que coincide con la solicitud, con un **Reemplazo** que define la redirección que se va a imponer.

Por ejemplo:

**Patrón** `^[^/]+/[^/]+/welcome$`

déclencheur:

**Reemplazo** `/libs/cq/core/content/welcome.html`.

para redirigir una solicitud:

`https://localhost:4503/welcome` ``

hasta:

`https://localhost:4503/libs/cq/core/content/welcome.html`

Se crean nuevas definiciones de asignación dentro del repositorio.

>[!NOTE]
>
>Hay muchos recursos disponibles que ayudan a explicar cómo definir las expresiones ordinarias; por ejemplo [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Creación de definiciones de asignación en AEM {#creating-mapping-definitions-in-aem}

En una instalación estándar de AEM puede encontrar la carpeta:

`/etc/map/http`

Esta es la estructura que se utiliza al definir asignaciones para el protocolo HTTP. Se pueden crear otras carpetas ( `sling:Folder`) en `/etc/map` para cualquier otro protocolo que desee asignar.

#### Configuración de una redirección interna a /content {#configuring-an-internal-redirect-to-content}

Para crear la asignación que prefiera cualquier solicitud a https://localhost:4503/ con `/content`:

1. Con CRXDE vaya a `/etc/map/http`.

1. Crear un nuevo nodo:

   * **** `sling:Mapping`
TipoEste tipo de nodo está diseñado para estas asignaciones, aunque su uso no es obligatorio.

   * **Nombre** `localhost_any`

1. Haga clic en **Guardar todo**.
1. **** Se han agregado las siguientes propiedades a este nodo:

   * **Nombre** `sling:match`

      * **Tipo** `String`

      * **Valor** `localhost.4503/`
   * **Nombre** `sling:internalRedirect`

      * **Tipo** `String`

      * **Valor** `/content/`


1. Haga clic en **Guardar todo**.

Esto gestionará una solicitud como:
`localhost:4503/geometrixx/en/products.html`
como si:
`localhost:4503/content/geometrixx/en/products.html`
se ha solicitado.

>[!NOTE]
>
>Consulte [Recursos](https://sling.apache.org/site/mappings-for-resource-resolution.html) en la documentación de Sling para obtener más información sobre las propiedades de sling disponibles y cómo se pueden configurar.

>[!NOTE]
>
>Puede utilizar `/etc/map.publish` para mantener las configuraciones del entorno de publicación. A continuación, se deben replicar y configurar la nueva ubicación ( `/etc/map.publish`) para la **Ubicación de asignación** de la [Resolución de recursos de sling de Apache](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) del entorno de publicación.

