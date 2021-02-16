---
title: Plantillas y componentes de aplicación
seo-title: Plantillas y componentes de aplicación
description: Siga esta página para conocer las plantillas y los componentes de la aplicación. Proporciona información detallada sobre la estructura de las plantillas.
seo-description: Siga esta página para conocer las plantillas y los componentes de la aplicación. Proporciona información detallada sobre la estructura de las plantillas.
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
translation-type: tm+mt
source-git-commit: a876a1a8d4aeb9e9a94c93a16742a4058307b0a8
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 1%

---


# Plantillas y componentes de aplicación{#app-templates-and-components}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Se utiliza una plantilla para crear una página y define qué componentes se pueden utilizar dentro del ámbito seleccionado. Una plantilla es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin ningún contenido real.

Cada plantilla le presentará una selección de componentes disponibles para su uso.

* Las plantillas están compuestas de [Componentes](/help/sites-developing/components.md);
* Los componentes utilizan y permiten el acceso a los widgets y se utilizan para representar el contenido.

>[!NOTE]
>
>Para obtener información sobre cómo desarrollar su aplicación AEM con CRXDE Lite, consulte [Desarrollo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

Una plantilla es la base de una página.

Para crear una página, la plantilla debe copiarse (node-tree **/apps/&lt;myapp>/templates/&lt;mytemplate>**) en la posición correspondiente del árbol del sitio: esto es lo que sucede si se crea una página con la ficha **Sitios web**.

Esta acción de copia también proporciona a la página su contenido inicial (generalmente solo contenido de nivel superior) y la propiedad sling:resourceType, la ruta al componente de página que se utiliza para representar la página (todo en el nodo secundario jcr:content).

## Estructura de una plantilla {#structure-of-a-template}

Hay dos aspectos que deben considerarse:

* la estructura de la plantilla misma
* la estructura del contenido producido al utilizar una plantilla

Se crea una plantilla bajo un nodo de tipo **cq:Template**.

Se pueden definir varias propiedades, en particular:

* **jcr:title** - título de la plantilla; aparece en el cuadro de diálogo al crear una página.
* **jcr:description** - descripción de la plantilla; aparece en el cuadro de diálogo al crear una página.

Este nodo contiene *un nodo jcr:content (cq:PageContent)* que se utilizará como base para el nodo de contenido de las páginas resultantes; esto hace referencia, utilizando *sling:resourceType*, al componente que se utilizará para procesar el contenido real de una nueva página.

>[!NOTE]
>
>Para obtener información básica sobre plantillas y componentes en AEM, consulte los recursos siguientes:
>
>* [Plantillas](/help/sites-developing/templates.md)
>* [Componentes](/help/sites-developing/components.md)

>



Una vez que conozca las plantillas y los componentes de forma básica, consulte los siguientes recursos:

* [Creación y Añade de plantillas y componentes](/help/mobile/mobile-ondemand-app-templates.md)
* [Uso de las propiedades del contenido para exportar contenido](/help/mobile/on-demand-content-properties-exporting.md)
* [Prácticas recomendadas  ](/help/mobile/best-practices-aem-mobile.md)
* [Desarrollo de AEM Mobile Content Services](/help/mobile/developing-content-services.md)

### Recursos adicionales {#additional-resources}

Para obtener más información sobre temas adicionales en aplicaciones móviles, consulte los vínculos siguientes:

* [Móvil con sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md)
* [Prueba de aplicaciones móviles](/help/mobile/develop-mobile-apps-testing.md)

