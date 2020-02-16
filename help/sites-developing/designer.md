---
title: Diseños y el diseñador
seo-title: Diseños y el diseñador
description: Deberá crear un diseño para el sitio web y, en AEM, hacerlo mediante el uso de Designer
seo-description: Deberá crear un diseño para el sitio web y, en AEM, hacerlo mediante el uso de Designer
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# Diseños y el diseñador{#designs-and-the-designer}

>[!CAUTION]
>
>En este artículo se describe cómo crear un sitio web basado en la IU clásica. Adobe recomienda aprovechar las últimas tecnologías de AEM para sus sitios web, tal como se describe en detalle en el artículo [Introducción al desarrollo de sitios](/help/sites-developing/getting-started.md)de AEM.

Deberá crear un diseño para el sitio web y, en AEM, hacerlo mediante Designer.

>[!NOTE]
>
>Para obtener más información sobre la accesibilidad web, consulte [AEM y las Directrices](/help/managing/web-accessibility.md)de accesibilidad web.

## Uso de Designer {#using-the-designer}

El diseño se puede definir en la sección de **diseños** de la ficha **Herramientas** :

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

Aquí puede crear la estructura necesaria para almacenar el diseño y, a continuación, cargar las hojas de estilo en cascada y las imágenes necesarias.

Los diseños se almacenan en `/etc/designs`. La ruta al diseño que se va a utilizar para un sitio web se especifica mediante la `cq:designPath` propiedad del `jcr:content` nodo.

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>Todos los cambios realizados en una página en modo de diseño se mantienen debajo del nodo de diseño del sitio y se aplican automáticamente a todas las páginas que tengan el mismo diseño.

## Qué necesitará {#what-you-will-need}

Para realizar el diseño, necesitará:

**CSS** : las hojas de estilo en cascada definen los formatos de áreas específicas de las páginas.
**Imágenes** : cualquier imagen que utilice para funciones como fondos o botones.

### Consideraciones Al Diseñar El Sitio Web {#considerations-when-designing-your-website}

Al desarrollar un sitio web, se recomienda almacenar imágenes y archivos CSS en `/etc/design/<project>` para poder hacer referencia a los recursos en función del diseño actual, como se describe en el siguiente fragmento de código.

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

El ejemplo anterior ofrece varias ventajas:

* Los componentes pueden tener un aspecto diferente en función de cada sitio mediante una ruta de diseño diferente.
* El rediseño del sitio web se puede realizar simplemente señalando la ruta de diseño a un nodo diferente en la raíz del sitio, de `design/v1` a `design/v2.`

* `/etc/designs` y `/content` son las únicas direcciones URL externas que el explorador ve protegerle de un usuario externo que se está curioso sobre lo que hay debajo del `/apps` árbol. Las ventajas de la URL anterior también ayudan al administrador del sistema a configurar una mejor seguridad, ya que está limitando la exposición de los recursos a unas pocas ubicaciones distintas.

