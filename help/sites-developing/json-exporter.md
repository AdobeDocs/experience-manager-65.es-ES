---
title: JSON Exporter for Content Services
seo-title: JSON Exporter for Content Services
description: Los servicios de contenido de AEM están diseñados para generalizar la descripción y el envío del contenido desde/hacia AEM más allá del enfoque en las páginas web. Proporcionan el envío de contenido a canales que no son páginas web AEM tradicionales, utilizando métodos estandarizados que pueden ser consumidos por cualquier cliente.
seo-description: Los servicios de contenido de AEM están diseñados para generalizar la descripción y el envío del contenido desde/hacia AEM más allá del enfoque en las páginas web. Proporcionan el envío de contenido a canales que no son páginas web AEM tradicionales, utilizando métodos estandarizados que pueden ser consumidos por cualquier cliente.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 4%

---


# Exportador JSON para servicios de contenido{#json-exporter-for-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y el envío del contenido desde/hacia AEM más allá del enfoque en las páginas web.

Proporcionan el envío de contenido a canales que no son páginas web AEM tradicionales, utilizando métodos estandarizados que pueden ser consumidos por cualquier cliente. Estos canales pueden incluir:

* [Aplicaciones de una sola página](spa-walkthrough.md)
* Aplicaciones móviles nativas
* otros canales y puntos de contacto externos a AEM

Con los fragmentos de contenido que utilizan contenido estructurado, puede proporcionar servicios de contenido mediante el exportador JSON para entregar el contenido de una página AEM en formato de modelo de datos JSON. Esto puede ser consumido por sus propias aplicaciones.

>[!NOTE]
>
>La funcionalidad descrita aquí está disponible para todos los componentes principales desde la [versión 1.1.0 de los componentes principales](https://docs.adobe.com/content/docs/en/core-components/v1.html).

## Exportador JSON con componentes principales de fragmento de contenido {#json-exporter-with-content-fragment-core-components}

Con el exportador JSON de AEM puede entregar el contenido de una(y) página AEM en formato de modelo de datos JSON. Esto puede ser consumido por sus propias aplicaciones.

Dentro de AEM el envío se logra mediante la extensión `model` y `.json` del selector.

`.model.json`

1. Por ejemplo, una dirección URL como:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. Entregará contenido como:

   ![chlimage_1-112](assets/chlimage_1-192.png)

También puede ofrecer el contenido de un fragmento de contenido estructurado segmentándolo específicamente.

Esto se realiza mediante la ruta completa del fragmento (mediante `jcr:content`); por ejemplo, con un sufijo como.

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

La página puede contener un solo fragmento de contenido o varios componentes de distintos tipos. También puede utilizar mecanismos como componentes de lista para buscar automáticamente contenido relevante.

* Por ejemplo, una dirección URL como:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* Entregará contenido como:

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >Puede [adaptar sus propios componentes](/help/sites-developing/json-exporter-components.md) para acceder y utilizar estos datos.

   >[!NOTE]
   >
   >Aunque no es una implementación estándar, [se admiten varios selectores,](json-exporter-components.md#multiple-selectors) pero `model` debe ser el primero.

### Información adicional {#further-information}

Consulte también:

* API de HTTP de Assets

   * [API de HTTP de Assets](/help/assets/mac-api-assets.md)

* Modelos Sling:

   * [Modelos Sling: Asociación de una clase model con un tipo de recurso desde 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM con JSON:

   * [Obtención de información de la página en formato JSON](/help/sites-developing/pageinfo.md)

## Documentación relacionada {#related-documentation}

Para obtener más información, consulte:

* El tema [Fragmentos de contenido en la guía del usuario de Recursos](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
* [Creación con fragmentos de contenido](/help/sites-authoring/content-fragments.md)
* [Activación de la exportación de JSON para un componente](/help/sites-developing/json-exporter-components.md)

* [Componentes principales ](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) y el componente Fragmento  [de contenido](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

