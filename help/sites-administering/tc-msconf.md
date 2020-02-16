---
title: Conexión a Microsoft Translator
seo-title: Conexión a Microsoft Translator
description: Obtenga información sobre cómo conectar AEM a Microsoft Translator.
seo-description: Obtenga información sobre cómo conectar AEM a Microsoft Translator.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Conexión a Microsoft Translator{#connecting-to-microsoft-translator}

Cree una configuración para el servicio en la nube de Microsoft Translator a fin de utilizar su cuenta de Microsoft Translation para traducir el contenido de la página de AEM, el contenido de la comunidad o los recursos.

| Propiedad | Descripción |
|---|---|
| Etiqueta de traducción | Nombre para mostrar del servicio de traducción. |
| Atribución de traducción | (Opcional) Para el contenido generado por el usuario, la atribución que aparece junto al texto traducido, por ejemplo `Translations by Microsoft`. |
| ID del espacio de trabajo | (Opcional) El ID del motor de Microsoft Translator personalizado que se va a utilizar. |
| Clave de suscripción | La clave de suscripción de Microsoft para Microsoft Translator. |

Después de crear la configuración, debe [activarla](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

El siguiente procedimiento utiliza la IU táctil para crear una configuración de Microsoft Translator.

1. En el carril, toque o haga clic en Herramientas > Servicios de nube.
1. En el área Microsoft Translator, toque o haga clic en Mostrar configuraciones.
1. Haga clic en el vínculo + junto a Configuraciones disponibles.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Escriba un título para la configuración. El título identifica la configuración en la consola de Cloud Services, así como en las listas desplegables de propiedad de página. El nombre predeterminado se basa en el título. Opcionalmente, escriba un nombre para utilizarlo para el nodo del repositorio que almacena la configuración. Debe utilizar el valor predeterminado para la propiedad Parent Configuration, que es la ruta del nodo del repositorio.
1. Haga clic en Crear.
1. En el cuadro de diálogo que aparece, escriba los valores de las propiedades y haga clic en Aceptar.

## Ejemplo de las configuraciones del servicio de nube de Microsoft Translator {#sample-microsoft-translator-cloud-service-configurations}

Las siguientes configuraciones del servicio en la nube de Microsoft Translator están instaladas con los ejemplos de Geometrixx. Algunas configuraciones de muestra utilizan una cuenta de Microsoft Translation de prueba que permite un máximo de 2 000 000 caracteres gratuitos traducidos al mes.

### Licencia de la versión de prueba de Microsoft Translator {#microsoft-translator-trial-license}

La configuración de la licencia de prueba de Microsoft Translator es una configuración de muestra que se instala con el paquete de muestra de Geometrixx Outdoors. Esta configuración utiliza una cuenta de Microsoft Translator que tiene una suscripción gratuita que permite 2 000 000 caracteres traducidos al mes.

### Microsoft Translator Trial License - Geometrixx-outdoors {#microsoft-translator-trial-license-geometrixx-outdoors}

La configuración de Microsoft Translator Trial License - Geometrixx-outdoors es una configuración de muestra que se instala con Geometrixx Outdoors. Esta configuración utiliza la misma cuenta gratuita de Microsoft Translator que la configuración de la licencia de prueba de Microsoft Translator. La cuenta tiene una suscripción gratuita que permite 2 000 000 caracteres traducidos al mes.

Esta configuración de Microsoft Translator está optimizada para su uso con el tipo de contenido del sitio de muestra de Geometrixx Outdoors.

### Actualización De La Configuración De Licencias De Prueba De Microsoft Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Las páginas de configuración de traducción de Microsoft proporcionan un vínculo práctico al sitio web de Microsoft para obtener una suscripción de cuenta adecuada para los sistemas de producción.

1. En el carril, toque o haga clic en Herramientas > Operaciones > Nube > Servicios de nube.
1. En el área Microsoft Translator, toque o haga clic en Mostrar configuraciones y, a continuación, toque o haga clic en Microsoft Translator Trial License (Microsoft Translation Configuration).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. En la página de configuración, haga clic en Actualizar suscripción. Utilice la página web de Microsoft que se abre para configurar su cuenta.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personalización del motor de traducción de Microsoft {#customizing-your-microsoft-translator-engine}

Las páginas de configuración de Microsoft Translation proporcionan un vínculo práctico al sitio web de Microsoft para personalizar el motor de Microsoft Translator. ([https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/))

1. En el carril, toque o haga clic en Herramientas > Operaciones > Nube > Servicios de nube.
1. En el área Microsoft Translator, toque o haga clic en Mostrar configuraciones y, a continuación, toque o haga clic en la configuración que desee personalizar.
1. En la página de configuración, haga clic en Personalizar traductor. Utilice la página web de Microsoft que se abre para personalizar el servicio.

## Activación de las configuraciones del servicio Traductor {#activating-the-translator-service-configurations}

Debe activar las configuraciones de servicio en la nube para admitir el contenido traducido que se replica en la instancia de publicación. Utilice el método de [activar una sección completa (árbol)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree) para activar los nodos del repositorio que almacenan las configuraciones de Microsoft Translator o de servicio en la nube de terceros. Los nodos se encuentran debajo de los siguientes nodos principales:

* Servicio de traducción de Microsoft: /etc/cloudservices/msft-translate
* Traducción de terceros: /etc/cloudservices/machine-Translation

