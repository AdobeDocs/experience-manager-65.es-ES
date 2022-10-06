---
title: Diseños y Designer
seo-title: Designs and the Designer
description: Deberá crear un diseño para el sitio web y, en AEM, hacerlo utilizando Designer
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

# Diseños y Designer{#designs-and-the-designer}

>[!CAUTION]
>
>Este artículo describe cómo crear un sitio web basado en la IU clásica. Adobe recomienda aprovechar las últimas tecnologías de AEM para sus sitios web como se describe detalladamente en el artículo [Introducción al desarrollo de AEM Sites](/help/sites-developing/getting-started.md).

El Diseñador se utiliza para crear un diseño para el sitio web mediante la [IU clásica](/help/release-notes/touch-ui-features-status.md) en AEM.

>[!NOTE]
>
>Para obtener más información sobre la accesibilidad web, consulte [AEM y las directrices de accesibilidad web](/help/managing/web-accessibility.md).

## Uso de Designer {#using-the-designer}

El diseño se puede definir en la variable **diseños** de la sección **Herramientas** pestaña:

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

Aquí puede crear la estructura necesaria para almacenar el diseño y, a continuación, cargar las hojas de estilo en cascada y las imágenes necesarias.

Los diseños se almacenan en `/apps/<your-project>`. La ruta al diseño que se utilizará para un sitio web se especifica mediante la variable `cq:designPath` propiedad de la variable `jcr:content` nodo .

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>Todos los cambios realizados en una página en modo de diseño se mantienen debajo del nodo de diseño del sitio y se aplican automáticamente a todas las páginas que tienen el mismo diseño.

## Lo que necesitará {#what-you-will-need}

Para realizar su diseño necesitará:

**CSS** - Las hojas de estilo en cascada definen los formatos de áreas específicas en sus páginas.
**Imágenes** - Imágenes que utilice para funciones como fondos, botones.

### Consideraciones Al Diseñar El Sitio Web {#considerations-when-designing-your-website}

Al desarrollar un sitio web, se recomienda encarecidamente almacenar imágenes y archivos CSS en `/apps/<your-project>` de este modo, puede hacer referencia a sus recursos en función del diseño actual, tal como se describe en el siguiente fragmento de código.

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

El ejemplo anterior ofrece varias ventajas:

* Los componentes pueden tener una apariencia diferente en función de cada sitio mediante una ruta de diseño diferente.
* El rediseño del sitio web se puede hacer simplemente señalando la ruta de diseño a un nodo diferente en la raíz del sitio desde `design/v1` a `design/v2.`

* `/etc/designs` y `/content` son las únicas direcciones URL externas que el navegador ve protegiéndole de un usuario externo que tiene curiosidad por saber qué hay debajo de su `/apps` árbol. Los beneficios de la URL anterior también ayudan al administrador del sistema a configurar una mejor seguridad, ya que limita la exposición de los recursos a unas pocas ubicaciones diferentes.
