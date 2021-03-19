---
title: Conexión a Microsoft Translator
seo-title: Conexión a Microsoft Translator
description: Aprenda a conectar AEM a Microsoft Translator.
seo-description: Aprenda a conectar AEM a Microsoft Translator.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Copiar idioma
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---


# Conexión a Microsoft Translator{#connecting-to-microsoft-translator}

Cree una configuración para el servicio en la nube de Microsoft Translator para usar su cuenta de Microsoft Translation para traducir AEM contenido de la página, contenido de la comunidad o recursos.

| Propiedad | Descripción |
|---|---|
| Etiqueta de traducción | Nombre para mostrar del servicio de traducción. |
| Atribución de traducción | (Opcional) Para el contenido generado por el usuario, la atribución que aparece junto al texto traducido, por ejemplo `Translations by Microsoft`. |
| ID del espacio de trabajo | (Opcional) El ID del motor de Microsoft Translator personalizado que debe utilizar. |
| Clave de suscripción | La clave de suscripción de Microsoft para Microsoft Translator. |

Después de crear la configuración, debe [activarla](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

El siguiente procedimiento utiliza la IU táctil para crear una configuración de Microsoft Translator.

1. En el carril, pulse o haga clic en Herramientas > Cloud Services.
1. En el área de Microsoft Translator, toque o haga clic en Mostrar configuraciones.
1. Haga clic en el vínculo + situado junto a Configuraciones disponibles.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Escriba un título para la configuración. El título identifica la configuración en la consola Cloud Services, así como en las listas desplegables de propiedades de página. El nombre predeterminado se basa en el título. Opcionalmente, escriba un nombre para usar para el nodo del repositorio que almacena la configuración. Debe utilizar el valor predeterminado de la propiedad Parent Configuration , que es la ruta del nodo del repositorio.
1. Haga clic en Crear.
1. En el cuadro de diálogo que aparece, escriba los valores de las propiedades y haga clic en Aceptar.

## Ejemplo de Configuraciones del Cloud Service del traductor de Microsoft {#sample-microsoft-translator-cloud-service-configurations}

Las siguientes configuraciones de servicio en la nube de Microsoft Translator están instaladas con los ejemplos de Geometrixx. Algunas configuraciones de ejemplo utilizan una cuenta de Microsoft Translation de prueba que permite un máximo de 2 000 000 caracteres traducidos gratuitos al mes.

### Licencia de la versión de prueba de Microsoft Translator {#microsoft-translator-trial-license}

La configuración de la licencia de prueba de Microsoft Translator es una configuración de ejemplo que se instala con el paquete de muestra de Geometrixx Outdoors. Esta configuración utiliza una cuenta de Microsoft Translator que tiene una suscripción gratuita que permite 2 000 000 caracteres traducidos al mes.

### Licencia de prueba de Microsoft Translator: Geometrixx al aire libre {#microsoft-translator-trial-license-geometrixx-outdoors}

La licencia de prueba de Microsoft Translator: la configuración de Geometrixx al aire libre es un ejemplo de configuración que se instala con los Geometrixx Outdoors. Esta configuración utiliza la misma cuenta gratuita de Microsoft Translator que la configuración de la licencia de prueba de Microsoft Translator. La cuenta tiene una suscripción gratuita que permite 2 000 000 caracteres traducidos al mes.

Esta configuración de Microsoft Translator está optimizada para su uso con el tipo de contenido del sitio de muestra de Geometrixx Outdoors.

### Actualización de la configuración de licencia de prueba de Microsoft Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Las páginas de configuración de Microsoft Translation proporcionan un práctico vínculo al sitio web de Microsoft para obtener una suscripción de cuenta adecuada para los sistemas de producción.

1. En el carril, pulse o haga clic en Herramientas > Operaciones > Nube > Cloud Services.
1. En el área de Microsoft Translator, pulse o haga clic en Mostrar configuraciones y, a continuación, pulse o haga clic en Licencia de prueba de Microsoft Translator (Configuración de traducción de Microsoft).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. En la página de configuración, haga clic en Actualizar suscripción. Utilice la página web de Microsoft que se abre para configurar su cuenta.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personalización del motor de traducción de Microsoft {#customizing-your-microsoft-translator-engine}

Las páginas de configuración de Microsoft Translation proporcionan un práctico vínculo al sitio web de Microsoft para personalizar el motor de Microsoft Translator. ([https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/))

1. En el carril, pulse o haga clic en Herramientas > Operaciones > Nube > Cloud Services.
1. En el área de Microsoft Translator, toque o haga clic en Mostrar configuraciones y, a continuación, toque o haga clic en la configuración que desee personalizar.
1. En la página de configuración, haga clic en Personalizar traductor. Utilice la página web de Microsoft que se abre para personalizar el servicio.

## Activación de las configuraciones del servicio de traducción {#activating-the-translator-service-configurations}

Debe activar las configuraciones del servicio en la nube para que admitan el contenido traducido que se replica en la instancia de publicación. Utilice el método de [activación de una sección completa (árbol)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree) para activar los nodos del repositorio que almacenan las configuraciones de servicio en la nube de Microsoft Translator o de terceros. Los nodos se encuentran debajo de los siguientes nodos principales:

* Servicio de traducción de Microsoft: /libs/settings/cloudconfigs/translation/msft-translation
* Traducción de terceros: /etc/cloudservices/machine-translation

