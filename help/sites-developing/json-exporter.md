---
title: Exportador JSON para servicios de contenido
description: Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido desde o hacia AEM, más allá del enfoque en las páginas web. Proporcionan la entrega de contenido a canales que no son páginas web de AEM tradicionales, mediante métodos estandarizados que cualquier cliente puede consumir.
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
exl-id: 647395c0-f392-427d-a998-e9ddf722b9f9
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 36%

---

# Exportador JSON para servicios de contenido{#json-exporter-for-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido desde o hacia AEM, más allá del enfoque en las páginas web.

Proporcionan la entrega de contenido a canales que no son páginas web de AEM tradicionales, mediante métodos estandarizados que cualquier cliente puede consumir. Estos canales pueden incluir lo siguiente:

* [Aplicaciones de una sola página](spa-walkthrough.md)
* Aplicaciones móviles nativas
* Otros canales y puntos de contacto externos a AEM

AEM Con los fragmentos de contenido que utilizan contenido estructurado, puede proporcionar servicios de contenido mediante el exportador JSON para entregar el contenido de cualquier página de la página en formato de modelo de datos JSON. Este método lo pueden consumir sus propias aplicaciones.

>[!NOTE]
>
>La funcionalidad descrita aquí está disponible para todos los componentes principales desde [versión 1.1.0 de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es).

## Exportador JSON con componentes principales de fragmentos de contenido {#json-exporter-with-content-fragment-core-components}

AEM AEM Con el exportador de JSON de, puede enviar el contenido de cualquier página de la página de la aplicación en formato de modelo de datos JSON de la página de la aplicación. Este método lo pueden consumir sus propias aplicaciones.

AEM Dentro de, la entrega se logra usando el selector de `model` y `.json` extensión.

`.model.json`

1. Por ejemplo, una dirección URL como:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. Ofrece contenido como:

   ![chlimage_1-192](assets/chlimage_1-192.png)

Como alternativa, puede entregar el contenido de un fragmento de contenido estructurado segmentándolo específicamente.

Utilice la ruta completa al fragmento (a través del `jcr:content`); por ejemplo, con un sufijo como.

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

La página puede contener un solo fragmento de contenido o varios componentes de varios tipos. También puede utilizar mecanismos como componentes de lista para buscar automáticamente contenido relevante.

* Por ejemplo, una dirección URL como:

  ```shell
  http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
  ```

* Ofrece contenido como:

  ![chlimage_1-193](assets/chlimage_1-193.png)

  >[!NOTE]
  >
  >Puede [adaptar sus propios componentes](/help/sites-developing/json-exporter-components.md) para acceder y utilizar estos datos.

  >[!NOTE]
  >
  >Aunque no es una implementación estándar, [se admiten varios selectores,](json-exporter-components.md#multiple-selectors) pero `model` debe ser el primero.

### Información adicional {#further-information}

Consulte también lo siguiente:

* API HTTP de recursos

   * [API HTTP de recursos](/help/assets/mac-api-assets.md)

* Modelos Sling:

   * [Modelos Sling: asociación de una clase de modelo con un tipo de recurso desde 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM con JSON:

   * [Obtener información de página en formato JSON](/help/sites-developing/pageinfo.md)

## Documentación relacionada {#related-documentation}

Para obtener más información, consulte:

* El [Tema Fragmentos de contenido en la guía del usuario de Assets](/help/assets/content-fragments/content-fragments.md)

* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
* [Creación con fragmentos de contenido](/help/sites-authoring/content-fragments.md)
* [Activación de la exportación de JSON para un componente](/help/sites-developing/json-exporter-components.md)

* [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) y el [Componente Fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=en)
