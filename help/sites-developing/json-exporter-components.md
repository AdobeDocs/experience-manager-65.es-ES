---
title: Activación de la exportación de JSON para un componente
seo-title: Enabling JSON Export for a Component
description: Los componentes se pueden adaptar para generar la exportación JSON de su contenido en función de un marco de modelos.
seo-description: Components can be adapted to generate JSON export of their content based on a modeler framework.
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 8%

---

# Activación de la exportación de JSON para un componente{#enabling-json-export-for-a-component}

Los componentes se pueden adaptar para generar la exportación JSON de su contenido en función de un marco de modelos.

## Información general {#overview}

La exportación de JSON se basa en [Modelos de Sling](https://sling.apache.org/documentation/bundles/models.html), y en el [Exportador de modelo Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) marco (que en sí mismo se basa en [Anotaciones de Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Esto significa que el componente debe tener un modelo de Sling si necesita exportar JSON. Por lo tanto, debe seguir estos dos pasos para habilitar la exportación de JSON en cualquier componente.

* [Definir un modelo de Sling para el componente](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Anotar la interfaz del modelo Sling](#annotate-the-sling-model-interface)

## Definir un modelo de Sling para el componente {#define-a-sling-model-for-the-component}

Primero debe definirse un modelo de Sling para el componente.

>[!NOTE]
>
>Para ver un ejemplo del uso de modelos Sling, consulte el artículo [Desarrollo de exportadores de modelos de Sling en AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html).

La clase de implementación del modelo de Sling debe estar anotada con lo siguiente:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Esto garantiza que el componente se pueda exportar por su cuenta, utilizando la variable `.model` y `.json` extensión.

Además, esto especifica que la clase del Modelo Sling se puede adaptar a la `ComponentExporter` interfaz.

>[!NOTE]
>
>Las anotaciones Jackson no suelen especificarse en el nivel de clase del Modelo Sling, sino en el nivel de interfaz del Modelo. Esto sirve para garantizar que la exportación de JSON se considere parte de la API de componente.

>[!NOTE]
>
>La variable `ExporterConstants` y `ComponentExporter` las clases provienen de `com.adobe.cq.export.json` paquete.

### Uso de varios selectores {#multiple-selectors}

Aunque no es un caso de uso estándar, es posible configurar varios selectores además del `model` selector.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

Sin embargo, en tal caso, el `model` debe ser el primer selector y la extensión debe ser `.json`.

## Anotar la interfaz del modelo Sling {#annotate-the-sling-model-interface}

Para que el marco del exportador JSON lo tenga en cuenta, la interfaz del modelo debe implementar la variable `ComponentExporter` interfaz (o `ContainerExporter`, en el caso de un componente contenedor).

La interfaz del modelo de Sling correspondiente ( `MyComponent`) se anotaría usando [Anotaciones de Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir cómo se debe exportar (serializado).

La interfaz del modelo debe estar debidamente anotada para definir qué métodos deben serializarse. De forma predeterminada, todos los métodos que respetan la convención de nombres habitual para los captadores se serializarán y derivarán sus nombres de propiedades JSON de forma natural de los nombres de los captadores. Esto se puede evitar o anular utilizando `@JsonIgnore` o `@JsonProperty` para cambiar el nombre de la propiedad JSON.

## Ejemplo {#example}

Los componentes principales son compatibles con la exportación de JSON desde la versión [1.1.0 de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) y pueden utilizarse como referencia.

Para ver un ejemplo, consulte la implementación del modelo Sling del componente principal de imagen y su interfaz anotada.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto aem-core-wcm-components en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## Documentación relacionada {#related-documentation}

Para obtener más información, consulte:

* La variable [Tema Fragmentos de contenido en la guía del usuario de Assets](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
* [Creación con fragmentos de contenido](/help/sites-authoring/content-fragments.md)
* [Exportador JSON para servicios de contenido](/help/sites-developing/json-exporter.md)
* [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) y [Componente Fragmento de contenido](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
