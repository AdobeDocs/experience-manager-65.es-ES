---
title: Conexión a Microsoft&reg; Traductor
description: Aprenda a conectar AEM a Microsoft&reg; Traductor.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 11%

---

# Conexión al traductor de Microsoft®{#connecting-to-microsoft-translator}

Cree una configuración para el servicio en la nube Microsoft® Translator para utilizar su cuenta de traducción de Microsoft® para traducir AEM contenido de la página, comunidad o recursos.

| Propiedad | Descripción |
|---|---|
| Etiqueta de traducción | El nombre para mostrar del servicio de traducción. |
| Atribución de traducción | (Opcional) Para el contenido generado por el usuario, la atribución que aparece junto al texto traducido, por ejemplo `Translations by Microsoft`. |
| ID del espacio de trabajo | (Opcional) El ID del motor de traducción personalizado de Microsoft® que debe utilizar. |
| Clave de suscripción | Su clave de suscripción Microsoft® para el traductor de Microsoft®. |

Después de crear la configuración, debe [actívelo](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

El siguiente procedimiento utiliza la IU táctil para crear una configuración de Microsoft® Translator.

1. En el carril, pulse o haga clic en Herramientas > Cloud Services.
1. En el área Microsoft® Translator, seleccione Mostrar configuraciones.
1. Haga clic en el vínculo + situado junto a Configuraciones disponibles.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Escriba un título para la configuración. El título identifica la configuración en la consola Cloud Services y en las listas desplegables de propiedades de página. El nombre predeterminado se basa en el título. De forma opcional, escriba un nombre para usar para el nodo del repositorio que almacena la configuración. Utilice el valor predeterminado para la propiedad Parent Configuration que es la ruta del nodo del repositorio.
1. Haga clic en Crear.
1. En el cuadro de diálogo que aparece, escriba los valores de las propiedades y haga clic en Aceptar.

## Ejemplo de configuraciones del Cloud Service del traductor Microsoft® {#sample-microsoft-translator-cloud-service-configurations}

Las siguientes configuraciones de servicio en la nube del conversor Microsoft® están instaladas con las muestras de Geometrixx. Algunas configuraciones de muestra utilizan una cuenta de traducción Microsoft® de prueba que permite un máximo de 2 000 000 caracteres traducidos gratuitos al mes.

### Licencia de prueba para el traductor Microsoft® {#microsoft-translator-trial-license}

La configuración de la licencia de prueba del traductor Microsoft® es una configuración de ejemplo que se instala con el paquete de muestra de Geometrixx Outdoors. Esta configuración utiliza una cuenta de Microsoft® Translator que tiene una suscripción gratuita que permite 2 000 000 caracteres traducidos al mes.

### Licencia de prueba del traductor Microsoft® - Geometrixx al aire libre {#microsoft-translator-trial-license-geometrixx-outdoors}

La licencia de prueba del traductor Microsoft®: la configuración de Geometrixx al aire libre es un ejemplo de configuración que se instala con los Geometrixx Outdoors. Esta configuración utiliza la misma cuenta gratuita de Microsoft® Translator que la configuración de la licencia de prueba del traductor de Microsoft®. La cuenta tiene una suscripción gratuita que permite 2 000 000 caracteres traducidos al mes.

Esta configuración de Microsoft® Translator está optimizada para su uso con el tipo de contenido del sitio de muestra de Geometrixx Outdoors.

### Actualización De La Configuración De La Licencia De Prueba De Microsoft® Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Las páginas de configuración de traducción de Microsoft® proporcionan un práctico vínculo al sitio web de Microsoft® para obtener una suscripción de cuenta adecuada para los sistemas de producción.

1. En el carril, pulse o haga clic en Herramientas > Operaciones > Nube > Cloud Services.
1. En el área Microsoft® Translator, toque o haga clic en Mostrar configuraciones y, a continuación, toque o haga clic en la licencia de prueba del traductor de Microsoft® (Configuración de traducción de Microsoft®).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. En la página de configuración, haga clic en Actualizar suscripción. Utilice la página web de Microsoft® que se abre para configurar su cuenta.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personalización del motor de traducción Microsoft® {#customizing-your-microsoft-translator-engine}

Las páginas de configuración de traducción de Microsoft® proporcionan un práctico vínculo al sitio web de Microsoft® para personalizar su motor de traducción de Microsoft®. ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/))

1. En el carril, pulse o haga clic en Herramientas > Operaciones > Nube > Cloud Services.
1. En el área Microsoft® Translator, toque o haga clic en Mostrar configuraciones y, a continuación, toque o haga clic en la configuración que desee personalizar.
1. En la página de configuración, haga clic en Personalizar traductor. Utilice la página web de Microsoft® que se abre para personalizar el servicio.

## Activación de las configuraciones del servicio de traducción {#activating-the-translator-service-configurations}

Para admitir contenido traducido que se replica en la instancia de publicación, active las configuraciones del servicio en la nube. Para activar los nodos del repositorio que almacenan las configuraciones de Microsoft® Translator o de servicio en la nube de terceros, utilice el método de [activación de una sección completa (árbol)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree). Los nodos se encuentran debajo de los siguientes nodos principales:

* Servicio de traducción de Microsoft®: /libs/settings/cloudconfigs/translation/msft-translation
* Traducción de terceros: /etc/cloudservices/machine-translation
