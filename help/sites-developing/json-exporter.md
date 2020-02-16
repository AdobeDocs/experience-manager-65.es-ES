---
title: JSON Exporter for Content Services
seo-title: JSON Exporter for Content Services
description: Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido de AEM desde y hacia AEM más allá del enfoque en las páginas web. Proporcionan la entrega de contenido a canales que no son páginas web tradicionales de AEM, utilizando métodos estandarizados que cualquier cliente puede consumir.
seo-description: Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido de AEM desde y hacia AEM más allá del enfoque en las páginas web. Proporcionan la entrega de contenido a canales que no son páginas web tradicionales de AEM, utilizando métodos estandarizados que cualquier cliente puede consumir.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# JSON Exporter for Content Services{#json-exporter-for-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido de AEM desde y hacia AEM más allá del enfoque en las páginas web.

Proporcionan la entrega de contenido a canales que no son páginas web tradicionales de AEM, utilizando métodos estandarizados que cualquier cliente puede consumir. Estos canales pueden incluir:

* Aplicaciones de una sola página
* Aplicaciones móviles nativas
* otros canales y puntos de contacto externos a AEM

Con los fragmentos de contenido que utilizan contenido estructurado, puede proporcionar servicios de contenido mediante el exportador JSON para entregar el contenido de una página AEM en formato de modelo de datos JSON. Esto puede ser consumido por sus propias aplicaciones.

>[!NOTE]
>
>La funcionalidad descrita aquí está disponible para todos los componentes principales desde la [versión 1.1.0 de los componentes](https://docs.adobe.com/content/docs/en/core-components/v1.html)principales.

## Exportador JSON con componentes principales de fragmento de contenido {#json-exporter-with-content-fragment-core-components}

Con el exportador JSON de AEM, puede entregar el contenido de una(y) página AEM en formato de modelo de datos JSON. Esto puede ser consumido por sus propias aplicaciones.

Dentro de AEM, la entrega se logra mediante el sufijo

`.model.json`

1. Por ejemplo, una dirección URL como:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. Entregará contenido como:

   ![chlimage_1-192](assets/chlimage_1-192.png)

También puede ofrecer el contenido de un fragmento de contenido estructurado segmentándolo específicamente.

Esto se realiza utilizando toda la ruta del fragmento (a través del `jcr:content`); por ejemplo, con un sufijo como.

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
   >Puede [adaptar sus propios componentes](/help/sites-developing/json-exporter-components.md) para acceder a estos datos y utilizarlos.

### Información adicional {#further-information}

Consulte también:

* API HTTP de recursos

   * [API HTTP de recursos](/help/assets/mac-api-assets.md)

* Modelos Sling:

   * [Modelos Sling: Asociación de una clase model con un tipo de recurso desde 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM con JSON:

   * [Obtención de información de la página en formato JSON](/help/sites-developing/pageinfo.md)

## Related Documentation {#related-documentation}

Para obtener más información, consulte:

* Tema Fragmentos [de contenido en la guía del usuario Recursos](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelos de fragmento de contenido](/help/assets/content-fragments-models.md)
* [Creación con fragmentos de contenido](/help/sites-authoring/content-fragments.md)
* [Activación de la exportación de JSON para un componente](/help/sites-developing/json-exporter-components.md)

* [Componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) principales y el componente Fragmento [de contenido](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

