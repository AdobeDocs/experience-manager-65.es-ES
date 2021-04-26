---
title: Configuración de varias tiendas de comercio
description: Obtenga información sobre cómo asignar varias vistas de tienda de Magento a AEM. Esto permite que los proyectos admitan casos de uso multilingües y de inquilinos múltiples.
sub-product: Comercio
doc-type: technical-video
activity: setup
audience: administrator
feature: Marco de integración de Commerce
kt: 3046
thumbnail: 28952.jpg
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 83%

---

# Configuración de varias tiendas de comercio {#multi-store}

Los componentes principales del CIF de AEM se pueden utilizar en varias estructuras del sitio de AEM y la implementación de cliente de GraphQL subyacente se puede conectar a diferentes tiendas de Magento o vistas de la tienda. Esto permite que los proyectos implementen configuraciones complejas de varias tiendas y sitios.

Un tutorial en vídeo que detalla las opciones para integrar varias vistas de la tienda de Magento con Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Las funciones de administración de varios sitios de AEM de Live Copy y de copia de idioma se utilizan junto con Commerce Integration Framework para administrar globalmente los sitios en las regiones y las configuraciones regionales.

La configuración recomendada es utilizar una relación 1:1 entre el sitio de AEM y la vista de la tienda de Magento.

Siga los pasos a continuación para conectar un sitio de AEM y los componentes principales del CIF de AEM a una vista de tienda dedicada:

## Configuración {#configuration}

1. Configure varias tiendas y vistas de las tiendas según el patrón descrito en [sitios web, tiendas y vistas de Magento](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. Asegúrese de que funcione la conexión entre AEM y Magento.

3. Cree una configuración secundaria de la configuración del CIF de Cloud Service siguiendo estos pasos:

   * En AEM vaya a Herramientas -> General -> [Explorador de configuración](/help/sites-administering/configurations.md#using-configuration-browser)
   * Seleccione la configuración base que ha creado.
   * Cree una nueva configuración siguiendo los pasos descritos en el punto 2 anterior.

   Esta nueva configuración se creará como una configuración secundaria de la base. Ahora puede ir a Herramientas -> General -> Explorador de configuración y crear los ajustes de configuración.

   >[!TIP]
   >
   > Los catálogos comerciales se pueden abordar mediante el uso de ID o UID. Los UID se introdujeron en el Magento 2.4.2. Solo debe habilitarse si el servidor de comercio admite un esquema de GraphQL de la versión 2.4.2 o posterior.

4. Asigne la configuración secundaria a un sitio de AEM.

   * Vaya a la consola de AEM Sites.
   * Navegue hasta la región o la raíz de idioma de la estructura del sitio, por ejemplo: /content/venia/us _o_ /content/venia/us/es para la página de muestra de Venia.
   * Seleccione la página y abra las propiedades de la página.
   * Seleccione la pestaña Avanzadas.
   * En la sección `Configuration` seleccione la configuración que creó en el paso

## Recursos adicionales

* [Sitios web, tiendas y vistas de Magento](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [Componentes principales del CIF de AEM: configuración de varias tiendas y sitios](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [Uso del administrador de varios sitios](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Reutilización del contenido: administrador de varios sitios y Live Copy](/help/sites-administering/msm.md)
