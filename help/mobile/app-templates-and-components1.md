---
title: Plantillas y componentes de aplicación
seo-title: App Templates and Components
description: Siga esta página para obtener más información sobre las plantillas y los componentes de la aplicación. Proporciona información detallada sobre la estructura de las plantillas.
seo-description: Follow this page to learn about App Templates and Components. It provides detailed information on the structure of templates.
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# Plantillas y componentes de aplicación{#app-templates-and-components}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Una plantilla se utiliza para crear una página y define qué componentes se pueden utilizar dentro del ámbito seleccionado. Una plantilla es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin contenido real.

Cada plantilla le presentará una selección de componentes disponibles para su uso.

* Las plantillas están creadas con [Componentes](/help/sites-developing/components.md);
* Los componentes utilizan utilidades y permiten el acceso a ellas, que se utilizan para representar el contenido.

>[!NOTE]
>
>Para obtener información sobre cómo desarrollar la aplicación de AEM con CRXDE Lite, consulte [Desarrollo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

Una plantilla es la base de una página.

Para crear una página, la plantilla debe copiarse (árbol de nodos) **/apps/&lt;myapp>/templates/&lt;mytemplate>**) a la posición correspondiente en el árbol de sitios: esto es lo que sucede si se crea una página con la variable **Sitios web** pestaña .

Esta acción de copia también proporciona a la página su contenido inicial (normalmente solo contenido de nivel superior) y la propiedad sling:resourceType, la ruta al componente de página que se utiliza para procesar la página (todo en el nodo secundario jcr:content).

## Estructura de una plantilla {#structure-of-a-template}

Hay dos aspectos que se deben tener en cuenta:

* la estructura de la plantilla
* la estructura del contenido producido al utilizar una plantilla

Una plantilla se crea bajo un nodo de tipo **cq:Template**.

Se pueden configurar varias propiedades, en particular:

* **jcr:title** - título de la plantilla; aparece en el cuadro de diálogo al crear una página.
* **jcr:description** - descripción de la plantilla; aparece en el cuadro de diálogo al crear una página.

Este nodo contiene *a jcr:content (cq:PageContent)* nodo que se utilizará como base para el nodo de contenido de las páginas resultantes; hace referencia a, usar *sling:resourceType*, el componente que se utilizará para procesar el contenido real de una página nueva.

>[!NOTE]
>
>Para conocer los conceptos básicos de las plantillas y los componentes de AEM, consulte los siguientes recursos:
>
>* [Plantillas](/help/sites-developing/templates.md)
>* [Componentes](/help/sites-developing/components.md)
>


Una vez que conozca las plantillas y los componentes, consulte los siguientes recursos:

* [Creación y adición de plantillas y componentes](/help/mobile/mobile-ondemand-app-templates.md)
* [Uso de las propiedades de contenido para exportar contenido](/help/mobile/on-demand-content-properties-exporting.md)
* [Prácticas recomendadas](/help/mobile/best-practices-aem-mobile.md)
* [Desarrollo de los servicios de contenido de AEM Mobile](/help/mobile/developing-content-services.md)

### Recursos adicionales {#additional-resources}

Para obtener más información sobre temas adicionales en aplicaciones móviles, consulte los vínculos siguientes:

* [Móvil con sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md)
* [Prueba de aplicaciones móviles](/help/mobile/develop-mobile-apps-testing.md)
