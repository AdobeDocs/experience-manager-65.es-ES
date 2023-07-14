---
title: Asignación de recursos
description: Obtenga información sobre cómo definir redirecciones, URL mnemónicas y hosts virtuales para Adobe Experience Manager mediante la asignación de recursos.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 4%

---

# Asignación de recursos{#resource-mapping}

La asignación de recursos se utiliza para definir redirecciones, URL de vanidad y hosts virtuales para Adobe Experience Manager AEM ().

Por ejemplo, puede utilizar estas asignaciones para lo siguiente:

* Agregue a todas las solicitudes el prefijo `/content` para que la estructura interna se oculte a los visitantes del sitio web.
* Defina una redirección para que todas las solicitudes a `/content/en/gateway` de su sitio web se redirigen a `https://gbiv.com/`.

Una posible asignación HTTP prefija todas las solicitudes a `localhost:4503` con `/content`. Una asignación como esta podría utilizarse para ocultar la estructura interna de los visitantes del sitio web, ya que permite lo siguiente:

`localhost:4503/content/we-retail/en/products.html`

Para acceder a él, utilice:

`localhost:4503/we-retail/en/products.html`

Como la asignación añade automáticamente el prefijo `/content` hasta `/we-retail/en/products.html`.

>[!CAUTION]
>
>Las URL mnemónicas no admiten patrones de regex.

>[!NOTE]
>
>Consulte la documentación de Sling y [Asignaciones para la resolución de recursos](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) y [Recursos](https://sling.apache.org/documentation/the-sling-engine/resources.html) para obtener más información.

## Visualización de definiciones de asignación {#viewing-mapping-definitions}

Las asignaciones de dos listas que evalúa el JCR Resource Resolver (de arriba a abajo) para encontrar una coincidencia.

Estas listas se pueden ver (junto con la información de configuración) en la **ResourceResolver de JCR** de la consola Felix; por ejemplo, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Configuración Muestra la configuración actual (tal como se define para la variable [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* Prueba de configuración Permite introducir una dirección URL o una ruta de recursos. Clic **Resolver** o **Mapa** para confirmar cómo transformará el sistema la entrada.

* **Entradas de mapa de resolución**
La lista de entradas utilizadas por los métodos ResourceResolver.resolve para asignar direcciones URL a recursos.

* **Entradas de mapa de asignación**
La lista de entradas utilizadas por los métodos ResourceResolver.map para asignar rutas de recursos a las direcciones URL.

Las dos listas muestran varias entradas, incluidas las definidas como predeterminadas por las aplicaciones. Normalmente, pretenden simplificar las direcciones URL del usuario.

El par de listas a **Patrón**, una expresión regular coincidente con la solicitud, con un **Sustitución** que define la redirección que se va a imponer.

Por ejemplo, el:

**Patrón** `^[^/]+/[^/]+/welcome$`

Almacenará en déclencheur:

**Sustitución** `/libs/cq/core/content/welcome.html`.

Para redirigir una solicitud:

`https://localhost:4503/welcome` ``

A:

`https://localhost:4503/libs/cq/core/content/welcome.html`

Se crean nuevas definiciones de asignación dentro del repositorio.

>[!NOTE]
>
>Hay muchos recursos disponibles para explicar cómo definir las expresiones regulares. Por ejemplo, [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### AEM Creación de Definiciones de Asignación en el {#creating-mapping-definitions-in-aem}

AEM En una instalación estándar de la carpeta de carpetas, puede encontrar la siguiente carpeta:

`/etc/map/http`

Esta es la estructura que se utiliza al definir asignaciones para el protocolo HTTP. Otras carpetas ( `sling:Folder`) se puede crear en `/etc/map` para cualquier otro protocolo que desee asignar.

#### Configuración de una redirección interna a /content {#configuring-an-internal-redirect-to-content}

Para crear la asignación que prefija cualquier solicitud a https://localhost:4503/ con `/content`:

1. Uso de CRXDE para desplazarse a `/etc/map/http`.

1. Cree un nodo:

   * **Tipo** `sling:Mapping`
Este tipo de nodo está diseñado para este tipo de asignaciones, aunque su uso no es obligatorio.

   * **Nombre** `localhost_any`

1. Haga clic en **Guardar todo**.
1. **Añadir** Agregue las siguientes propiedades a este nodo:

   * **Nombre** `sling:match`

      * **Tipo** `String`

      * **Valor** `localhost.4503/`

   * **Nombre** `sling:internalRedirect`

      * **Tipo** `String[]`

      * **Valor** `/content/`

1. Haga clic en **Guardar todo**.

Esto administra una solicitud como:
`localhost:4503/geometrixx/en/products.html`
como si:
`localhost:4503/content/geometrixx/en/products.html`
se ha solicitado.

>[!NOTE]
>
>Consulte [Recursos](https://sling.apache.org/documentation/the-sling-engine/resources.html) en la Documentación de Sling para obtener más información sobre las propiedades de Sling disponibles y cómo se pueden configurar.

>[!NOTE]
>
>Puede utilizar `/etc/map.publish` para guardar las configuraciones del entorno de publicación. Se deben replicar, y la nueva ubicación ( `/etc/map.publish`) configurado para **Ubicación de asignación** de la [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) del entorno de publicación
