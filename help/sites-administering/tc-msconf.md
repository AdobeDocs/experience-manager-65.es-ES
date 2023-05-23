---
title: Conectando con Microsoft&reg; Translator
description: AEM Aprenda a conectarse a Microsoft&reg; Translator de forma.
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

# Conexión a Microsoft® Translator{#connecting-to-microsoft-translator}

Cree una configuración para el servicio en la nube de Microsoft® Translator y use su cuenta de MicrosoftAEM ® Translation para traducir contenido de página, contenido de la comunidad o recursos.

| Propiedad | Descripción |
|---|---|
| Etiqueta de traducción | El nombre para mostrar del servicio de traducción. |
| Atribución de traducción | (Opcional) Para el contenido generado por el usuario, la atribución que aparece junto al texto traducido, por ejemplo `Translations by Microsoft`. |
| ID del espacio de trabajo | (Opcional) El ID del motor personalizado de Microsoft® Translator que debe utilizar. |
| Clave de suscripción | Su clave de suscripción de Microsoft® para Microsoft® Translator. |

Después de crear la configuración, debe [activarlo](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

El siguiente procedimiento utiliza la interfaz de usuario táctil optimizada para crear una configuración de Microsoft® Translator.

1. En el carril, toque o haga clic en Herramientas > Cloud Services.
1. En el área de Microsoft® Translator, seleccione Mostrar configuraciones.
1. Haga clic en + junto a Configuraciones disponibles.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Escriba un título para la configuración. El título identifica la configuración en la consola Cloud Services y en las listas desplegables de propiedades de página. El nombre predeterminado se basa en el título. De forma opcional, escriba un nombre para usar para el nodo del repositorio que almacena la configuración. Utilice el valor predeterminado para la propiedad Parent Configuration, que es la ruta del nodo del repositorio.
1. Haga clic en Crear.
1. En el cuadro de diálogo que aparece, escriba los valores de las propiedades y, a continuación, haga clic en Aceptar.

## Ejemplo de configuraciones del Cloud Service de Microsoft® Translator {#sample-microsoft-translator-cloud-service-configurations}

Las siguientes configuraciones del servicio en la nube de Microsoft® Translator se instalan con los ejemplos de Geometrixx. Algunas configuraciones de muestra utilizan una cuenta de prueba de Microsoft® Translation que permite un máximo de 2 000 000 caracteres traducidos gratuitos al mes.

### Licencia de prueba de Microsoft® Translator {#microsoft-translator-trial-license}

La configuración de la licencia de prueba de Microsoft® Translator es una configuración de ejemplo que se instala con el paquete de muestra de Geometrixx Outdoors. Esta configuración utiliza una cuenta de Microsoft® Translator con una suscripción gratuita que permite 2 000 000 caracteres traducidos al mes.

### Licencia de prueba del traductor de Microsoft® - Geometrixx-al aire libre {#microsoft-translator-trial-license-geometrixx-outdoors}

La configuración de Microsoft® Translator Trial License - Geometrixx-outdoors es una configuración de ejemplo que se instala con los Geometrixx Outdoors. Esta configuración utiliza la misma cuenta gratuita de Microsoft® Translator que la configuración de la licencia de prueba de Microsoft® Translator. La cuenta tiene una suscripción gratuita que permite 2 000 000 caracteres traducidos al mes.

Esta configuración de Microsoft® Translator está optimizada para utilizarse con el tipo de contenido del sitio de muestra de Geometrixx Outdoors.

### Actualización De La Configuración De La Licencia De Prueba De Microsoft® Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Las páginas de configuración de Microsoft® Translation proporcionan un práctico vínculo al sitio web de Microsoft® para obtener una suscripción de cuenta adecuada para los sistemas de producción.

1. En el carril, toque o haga clic en Herramientas > Operaciones > Nube > Cloud Services.
1. En el área de Microsoft® Translator, toque o haga clic en Mostrar configuraciones y, a continuación, toque o haga clic en Licencia de prueba de Microsoft® Translator (Microsoft® Translation Configuration).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. En la página de configuración, haga clic en Actualizar suscripción. Utilice la página web de Microsoft® que se abre para configurar su cuenta de.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personalización del motor de Microsoft® Translator {#customizing-your-microsoft-translator-engine}

Las páginas de configuración de Microsoft® Translation proporcionan un práctico vínculo al sitio web de Microsoft® para personalizar el motor de Microsoft® Translator. ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/))

1. En el carril, toque o haga clic en Herramientas > Operaciones > Nube > Cloud Services.
1. En el área de Microsoft® Translator, toque o haga clic en Mostrar configuraciones y, a continuación, toque o haga clic en la configuración que desea personalizar.
1. En la página de configuración, haga clic en Personalizar traductor. Utilice la página web de Microsoft® que se abre para personalizar el servicio.

## Activación de las configuraciones del servicio de traducción {#activating-the-translator-service-configurations}

Para admitir contenido traducido que se duplique en la instancia de publicación, active las configuraciones del servicio en la nube. Para activar los nodos del repositorio que almacenan las configuraciones de Microsoft® Translator o servicios en la nube de terceros, utilice el método de [activación de una sección completa (árbol)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree). Los nodos se encuentran debajo de los siguientes nodos principales:

* Servicio de traducción de Microsoft®: /libs/settings/cloudconfigs/translation/msft-translation
* Traducción de terceros: /etc/cloudservices/machine-translation
