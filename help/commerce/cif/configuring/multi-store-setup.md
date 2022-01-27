---
title: Configuración de varias tiendas de comercio
description: Obtenga información sobre cómo asignar varias vistas de tiendas de Adobe Commerce a AEM. Esto permite que los proyectos admitan casos de uso multilingües y de inquilinos múltiples.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 1d4e9b7b-848b-4007-b884-dd48682d62e8
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 44%

---

# Configuración de varias tiendas de comercio {#multi-store}

Los componentes principales del CIF de AEM se pueden utilizar en varias estructuras de sitio AEM y la implementación de cliente de GraphQL subyacente se puede conectar a diferentes tiendas de Adobe Commerce o vistas de la tienda. Esto permite que los proyectos implementen configuraciones complejas de varias tiendas y sitios.

Un tutorial en vídeo que detalla las opciones para integrar varias vistas de la tienda de Adobe Commerce con Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Las funciones de administración de varios sitios de AEM de Live Copy y de copia de idioma se utilizan junto con Commerce Integration Framework para administrar globalmente los sitios en las regiones y las configuraciones regionales.

La configuración recomendada es utilizar una relación 1:1 entre AEM sitio y la vista de la tienda de Adobe Commerce.

Para conectar un sitio AEM y AEM los componentes principales del CIF a una vista de tienda dedicada, siga los pasos a continuación:

## Configuración {#configuration}

1. Configure varias tiendas y vistas de tiendas según el patrón descrito en [Sitios web, tiendas y vistas de Adobe Commerce](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. Asegúrese de que la conexión entre AEM y Adobe Commerce funcione.

3. Cree una configuración secundaria de la configuración del CIF de Cloud Service siguiendo estos pasos:

   * En AEM vaya a Herramientas -> General -> [Explorador de configuración](/help/sites-administering/configurations.md#using-configuration-browser)
   * Seleccione la configuración base que ha creado.
   * Cree una nueva configuración siguiendo los pasos descritos en el punto 2 anterior.

   Esta nueva configuración se creará como una configuración secundaria de la base. Ahora puede ir a Herramientas -> General -> Explorador de configuración y crear los ajustes de configuración.

   >[!TIP]
   >
   > Los catálogos comerciales se pueden abordar mediante el uso de ID o UID. Los UID se introdujeron en Adobe Commerce 2.4.2. Solo debe habilitarse si el servidor de comercio es compatible con un esquema de GraphQL de la versión 2.4.2 o posterior.

4. Asigne la configuración secundaria a un sitio de AEM.

   * Vaya a la consola de AEM Sites.
   * Vaya a la región o a la raíz de idioma de la estructura del sitio, por ejemplo /content/venia/us _o_ /content/venia/us/es para la página de muestra de Venia
   * Seleccione la página y abra las propiedades de la página.
   * Seleccione la pestaña Avanzadas.
   * En la sección `Configuration` seleccione la configuración que creó en el paso

## Recursos adicionales

* [Sitios web, tiendas y vistas de Adobe Commerce](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [Componentes principales del CIF de AEM: configuración de varias tiendas y sitios](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [Uso del administrador de varios sitios](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Reutilización del contenido: administrador de varios sitios y Live Copy](/help/sites-administering/msm.md)
