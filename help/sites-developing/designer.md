---
title: Diseños y el diseñador
seo-title: Designs and the Designer
description: AEM Tendrá que crear un diseño para su sitio web y, en la práctica, lo hace utilizando el diseñador de páginas web.
seo-description: You will need to create a design for your website and in AEM, you do so by using the Designer
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
source-git-commit: adbdff9ff5b5bd8f5f6b22fb724a0e5273072de2
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Diseños y el diseñador{#designs-and-the-designer}

>[!CAUTION]
>
>Este artículo describe cómo crear un sitio web basado en la IU clásica. El Adobe AEM recomienda aprovechar las últimas tecnologías de la para sus sitios web, tal como se describe en detalle en el artículo [Introducción al desarrollo de AEM Sites](/help/sites-developing/getting-started.md).

El Diseñador se utiliza para crear un diseño para el sitio web utilizando [IU clásica](/help/release-notes/touch-ui-features-status.md) AEM en la.

>[!NOTE]
>
>Para obtener más información sobre la accesibilidad Web, consulte [AEM Directrices de accesibilidad web de y](/help/managing/web-accessibility.md).

## Uso del diseñador {#using-the-designer}

Su diseño se puede definir en la **diseños** de la sección **Herramientas** pestaña:

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

Aquí puede crear la estructura necesaria para almacenar el diseño y, a continuación, cargar las hojas de estilo en cascada y las imágenes necesarias.

Los diseños se almacenan en `/apps/<your-project>`. La ruta al diseño que se va a utilizar para un sitio web se especifica mediante la variable `cq:designPath` propiedad del `jcr:content` nodo.

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>Todos los cambios realizados en una página en modo de diseño se mantienen debajo del nodo de diseño del sitio y se aplican automáticamente a todas las páginas que tienen el mismo diseño.

## Lo que necesita {#what-you-will-need}

Para realizar su diseño necesitará:

**CSS** : Las hojas de estilo en cascada definen los formatos de áreas específicas de las páginas.
**Imágenes** : cualquier imagen que utilice para funciones como fondos o botones.

### Consideraciones al diseñar el sitio web {#considerations-when-designing-your-website}

Al desarrollar un sitio web, es muy recomendable almacenar imágenes y archivos CSS en `/apps/<your-project>` por lo tanto, puede hacer referencia a los recursos en función del diseño actual como se describe en el siguiente fragmento de código.

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

El ejemplo anterior ofrece varios beneficios:

* Los componentes pueden tener un aspecto diferente en función de cada sitio y utilizar una ruta de diseño diferente.
* El rediseño del sitio web se puede hacer simplemente apuntando la ruta de diseño a un nodo diferente en la raíz del sitio desde `design/v1` hasta `design/v2.`

* `/etc/designs` y `/content` son las únicas direcciones URL externas que el explorador ve protegiéndolo de un usuario externo que siente curiosidad por saber qué hay debajo de su `/apps` árbol. Las ventajas de URL anteriores también ayudan al administrador del sistema a configurar una mejor seguridad, ya que limita la exposición de los recursos a unas pocas ubicaciones distintas.
