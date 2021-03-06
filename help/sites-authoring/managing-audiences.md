---
title: Administrar audiencias
seo-title: Administrar audiencias
description: La consola de audiencias permite crear, organizar y administrar las audiencias de la cuenta de Adobe Target o administrar segmentos de ContextHub o Client Context
seo-description: La consola de audiencias permite crear, organizar y administrar las audiencias de la cuenta de Adobe Target o administrar segmentos de ContextHub o Client Context
uuid: 76408a8c-25db-4e9f-8a69-27e820a2a7cf
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9a7a31f9-aeb8-455f-a07e-7b1d1f0a88b6
docset: aem65
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 68%

---


# Administrar audiencias{#managing-audiences}

La consola de audiencias permite crear, organizar y administrar las audiencias de la cuenta de Adobe Target o administrar segmentos de ContextHub o Client Context:

* Añadir audiencias: audiencias de Adobe Target o segmentos de ContextHub.
* Administre audiencias.

Una Audiencia, denominada *segment* en ContextHub y Client Context, es una clase de visitantes definidos por criterios específicos, que luego determina quién ve una actividad de objetivo. Al segmentar una actividad, puede seleccionar la audiencia directamente en el proceso de segmentación o crear una nueva en la consola de audiencias.

En la consola de audiencias, las audiencias se organizan según la marca.

Las audiencias están disponibles en modo de objetivo para [crear contenido de destino](/help/sites-authoring/content-targeting-touch.md), donde también puede crear audiencias (pero necesita crear audiencias de Adobe Target en la consola Audiencias). Las audiencias creadas en el modo Segmentación aparecen en la consola de audiencias.

Las audiencias se muestran con una etiqueta que describe qué tipo de audiencia está definida:

* CH: segmento de ContextHub
* CC: segmento del contexto del cliente
* AT: audiencia de Adobe Target

## Crear un segmento de ContextHub en la consola de audiencias {#creating-a-contexthub-segment-in-the-audiences-console}

Puede crear un segmento de ContextHub en la consola de audiencias o durante el proceso de segmentación.

Para crear un segmento de ContextHub en la consola de audiencias:

1. En la consola de navegación, haga clic o pulse **Personalización**. Toque o haga clic en **Audiencias**.
1. Haga clic o pulse **Crear segmento de ContextHub**.

   ![screen-shot_2019-03-05at124034](assets/screen-shot_2019-03-05at124034.png)

1. En cuadro de diálogo **Nuevo segmento de ContextHub**, introduzca un título, ajuste el aumento y haga clic en **Crear**. El nuevo segmento de ContextHub aparece en la lista de audiencias.

   >[!NOTE]
   >
   >Puede ordenar la lista modificada pulsando o haciendo clic en **Modificado** para clasificar en orden descendente y ver las audiencias recién creadas.

Para obtener más información sobre cómo crear segmentos con ContextHub, consulte la documentación de [Configurar la segmentación con ContextHub](/help/sites-administering/segmentation.md).

## Crear una audiencia de Adobe Target mediante la consola de audiencias  {#creating-an-adobe-target-audience-using-the-audience-console}

Puede crear audiencias de Adobe Target directamente en AEM mediante la consola de audiencias.

Las audiencias se definen mediante reglas que determinan quién se incluye o excluye de una actividad de destino. Una definición de audiencia puede incluir varias reglas y cada regla puede incluir varios parámetros.

Al utilizar más de una regla, estas reglas se combinan según el operador booleano Y (AND), lo que significa que cualquier posible miembro de la audiencia debe cumplir todas las condiciones que se detallaron para ser incluido en la actividad. Por ejemplo, si define una regla de sistema operativo Y (AND) una regla de explorador, solo se incluyen en la actividad los visitantes que usan el sistema operativo definido Y (AND) el explorador definido.

>[!NOTE]
>
>Si no ve **Crear Audiencia de Destinatario **en el menú **Crear**, no tiene los permisos necesarios para crear una audiencia. Necesita permisos de escritura en **/etc/segmentation** para poder crear audiencias. Los autores de contenido del grupo tienen permisos de escritura de forma predeterminada.

Para crear una audiencia de Adobe Target:

1. En la consola de navegación, haga clic o pulse **Personalización**. Toque o haga clic en **Audiencias**.

   ![screen-shot_2019-03-05at124139](assets/screen-shot_2019-03-05at124139.png)

1. En la consola Audiencias, toque o haga clic en **Crear** y, a continuación** Crear Audiencia de Destinatario**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. En el cuadro de diálogo **Configuración de Adobe Target**, seleccione la configuración de destino y haga clic o pulse **Aceptar**.
1. En el área de la Regla n.º 1, haga clic o pulse el tipo de atributo e introduzca la información de atributo en los campos que están disponibles. Cuando termine, seleccione la marca de verificación situada a la derecha del atributo para guardarlo. Consulte [Atributos y sus opciones](#attributes-and-their-options) para obtener más información acerca de todos los atributos.
1. Haga clic en **Agregar regla** para añadir otra regla. Escriba tantas reglas como sea necesario. Las reglas se combinan con el operador booleano Y, lo que significa que la audiencia debe cumplir todos los requisitos de cada regla para poder optar a una actividad.
1. Haga clic o pulse **Siguiente**.
1. Especifique un nombre para la audiencia y haga clic o pulse **Guardar**.
1. Toque o haga clic en **Guardar**. La audiencia se enumera en la lista de audiencias.

### Atributos y sus opciones  {#attributes-and-their-options}

Puede crear reglas de segmentación para cada uno de los atributos siguientes:

| **Atributo** | **Descripción** | **Para obtener más información** |
|---|---|---|
| **Móvil** | Destinatario los dispositivos móviles en función de parámetros como dispositivos móviles, tipo de dispositivo, proveedor de dispositivos, dimensiones de pantalla (en píxeles), etc. | Consulte [Documentación de dispositivos móviles](https://docs.adobe.com/content/help/en/target/using/audiences/create-audiences/categories-audiences/mobile.html) en Adobe Target. |
| **Personalizado** | Los parámetros personalizados son parámetros de mbox. Si pasa algún parámetro mbox a mboxes, o usa la función targetPageParams, ese parámetro aparece aquí para su uso en audiencias. | Consulte [Documentación de parámetros personalizados](https://docs.adobe.com/content/help/en/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) en Adobe Target. |
| **SO** | Puede destinatario visitantes que utilicen un sistema operativo determinado. | Usuarios de Target que usen Linux, Macintosh o Windows. |
| **Páginas del sitio** | Visitantes de destinatario que se encuentran en una página específica o que tienen un parámetro de mbox específico. | Consulte la [documentación de las páginas del sitio](https://docs.adobe.com/content/help/en/target/using/audiences/create-audiences/categories-audiences/site-pages.html) en Adobe Target. |
| **Explorador** | Puede asignar destinatarios a los usuarios que utilicen un explorador específico o opciones específicas del explorador cuando visiten la página. | Consulte [Documentación de opciones del explorador](https://docs.adobe.com/help/en/target/using/audiences/create-audiences/categories-audiences/browser.html)en Adobe Target. |
| **Perfil del visitante** | Visitantes de destinatario que cumplen parámetros de perfil específicos. | Consulte [documentación de Perfil de Visitante](https://docs.adobe.com/content/help/en/target/using/audiences/visitor-profiles/visitor-profile.html) en Adobe Target. |
| **Fuentes de tráfico** | Visitantes de destinatario basados en el motor de búsqueda o la página de aterrizaje que los remite a su sitio. | Consulte [Documentación de fuentes de tráfico](https://docs.adobe.com/content/help/en/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) en Adobe Target. |

## Modificar una audiencia en la consola de audiencias {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>Solo puede editar las audiencias de Adobe Target que se crearon en la misma instancia de AEM en la cual realizó las modificaciones. Las audiencias de destino que se crearon en diferentes entornos de AEM no se pueden editar.

Puede editar cualquier audiencia de ContextHub o Client Context desde la consola de audiencias. Asimismo, también puede editar audiencias de Adobe Target, pero solo aquellos que se hayan creado en AEM:

1. En la consola de navegación, haga clic o pulse **Personalización**. Toque o haga clic en **Audiencias**.
1. Haga clic o pulse el icono que está al lado del segmento de ContextHub o Client Context que desea editar, y haga clic o pulse **Editar**.
1. Haga los cambios necesarios en el editor de segmentos. Consulte la documentación de [Client Context](/help/sites-administering/campaign-segmentation.md) o [ContextHub](/help/sites-developing/ch-configuring.md).
