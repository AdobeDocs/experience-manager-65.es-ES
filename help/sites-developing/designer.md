---
title: Diseños y Designer
description: AEM Aprenda a crear un diseño para su sitio web y a crear un diseño en mediante el uso de Designer.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Diseños y Designer{#designs-and-the-designer}

>[!CAUTION]
>
>Este artículo describe cómo crear un sitio web basado en la IU clásica. El Adobe AEM recomienda usar las últimas tecnologías de la para sus sitios web, tal como se describe en detalle en el artículo [Introducción al desarrollo de AEM Sites](/help/sites-developing/getting-started.md).

El Designer AEM se usa para crear un diseño para tu sitio web usando la [IU clásica](/help/release-notes/touch-ui-features-status.md) en la interfaz de usuario de la aplicación .

>[!NOTE]
>
>AEM Para obtener más información acerca de la accesibilidad Web, vea [y las Directrices de accesibilidad Web](/help/managing/web-accessibility.md).

## Uso de Designer {#using-the-designer}

Su diseño se puede definir en la sección **designs** de la pestaña **Tools**:

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

Aquí puede crear la estructura necesaria para almacenar el diseño y, a continuación, cargar las hojas de estilo en cascada y las imágenes necesarias.

Los diseños se almacenan en `/apps/<your-project>`. La ruta de acceso al diseño que se utilizará para un sitio web se especifica mediante la propiedad `cq:designPath` del nodo `jcr:content`.

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>Todos los cambios realizados en una página en modo de diseño se mantienen debajo del nodo de diseño del sitio y se aplican automáticamente a todas las páginas que tienen el mismo diseño.

## Lo que necesita {#what-you-will-need}

Para realizar su diseño necesitará:

**CSS**: las hojas de estilo en cascada definen los formatos de áreas específicas de las páginas.
**Imágenes**: todas las imágenes que use para características como fondos o botones.

### Consideraciones al diseñar el sitio web {#considerations-when-designing-your-website}

Al desarrollar un sitio web, se recomienda encarecidamente almacenar imágenes y archivos CSS en `/apps/<your-project>` para poder hacer referencia a los recursos en función del diseño actual como se describe en el siguiente fragmento de código.

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

El ejemplo anterior ofrece varios beneficios:

* Los componentes pueden tener un aspecto diferente en función de cada sitio y utilizar una ruta de diseño diferente.
* El rediseño del sitio web se puede realizar simplemente señalando la ruta de diseño a un nodo diferente en la raíz del sitio de `design/v1` a `design/v2.`

* `/etc/designs` y `/content` son las únicas direcciones URL externas que el explorador ve protegiéndolo de un usuario externo que siente curiosidad por saber qué hay debajo de su árbol `/apps`. Las ventajas de URL anteriores también ayudan al administrador del sistema a configurar una mejor seguridad, ya que limita la exposición de los recursos a unas pocas ubicaciones distintas.
