---
title: Plantillas y componentes de aplicación
description: Siga esta página para obtener más información sobre las plantillas y los componentes de la aplicación. Proporciona información detallada sobre la estructura de las plantillas.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 1%

---

# Plantillas y componentes de aplicación{#app-templates-and-components}

{{ue-over-mobile}}

Se utiliza una plantilla para crear una página y define qué componentes se pueden utilizar dentro del ámbito seleccionado. Una plantilla es una jerarquía de nodos que tiene la misma estructura que la página que se va a crear, pero sin contenido real.

Cada plantilla le presenta una selección de componentes disponibles para su uso.

* Las plantillas están compuestas por [Componentes](/help/sites-developing/components.md);
* Los componentes utilizan los widgets y permiten el acceso a ellos, y se utilizan para procesar el contenido.

>[!NOTE]
>
>Para obtener información sobre cómo desarrollar la aplicación de Adobe Experience Manager AEM () mediante CRXDE Lite, consulte [Desarrollo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

Una plantilla es la base de una página.

Para crear una página, la plantilla debe copiarse (node-tree **/apps/&lt;myapp>/templates/&lt;mytemplate>**) a la posición correspondiente en el árbol del sitio: esto es lo que sucede si se crea una página con la pestaña **Sitios web**.

Esta acción de copia también proporciona a la página su contenido inicial (normalmente solo contenido de nivel superior) y la propiedad sling:resourceType, la ruta al componente de página que se utiliza para procesar la página (todo en el nodo secundario jcr:content).

## Estructura de una plantilla {#structure-of-a-template}

Hay dos aspectos que hay que tener en cuenta:

* la estructura de la propia plantilla
* la estructura del contenido producido cuando se utiliza una plantilla

Se crea una plantilla en un nodo de tipo **cq:Template**.

Se pueden configurar varias propiedades, en particular:

* **jcr:title** - título de la plantilla; aparece en el cuadro de diálogo al crear una página.
* **jcr:description**: descripción de la plantilla; aparece en el cuadro de diálogo al crear una página.

Este nodo contiene *un nodo jcr:content (cq:PageContent)* que se usa como base para el nodo de contenido de las páginas resultantes. Esto hace referencia, usando *sling:resourceType*, al componente que se va a usar para procesar el contenido real de una nueva página.

>[!NOTE]
>
>AEM Para conocer los conceptos básicos de las plantillas y los componentes en las plantillas de, consulte los recursos que aparecen a continuación:
>
>* [Plantillas](/help/sites-developing/templates.md)
>* [Componentes](/help/sites-developing/components.md)
>

Una vez que tenga la comprensión básica de las plantillas y los componentes, consulte los siguientes recursos:

* [Crear y agregar plantillas y componentes](/help/mobile/mobile-ondemand-app-templates.md)
* [Uso de propiedades de contenido para exportar contenido](/help/mobile/on-demand-content-properties-exporting.md)
* [Prácticas recomendadas](/help/mobile/best-practices-aem-mobile.md)
* [Desarrollo de AEM Mobile Content Services](/help/mobile/developing-content-services.md)

### Recursos adicionales {#additional-resources}

Para obtener más información sobre temas adicionales de las aplicaciones móviles, consulte los vínculos siguientes:

* [Móvil con sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md)
* [Prueba de aplicaciones móviles](/help/mobile/develop-mobile-apps-testing.md)
