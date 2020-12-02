---
title: Targeting de Adobe Campaign
seo-title: Targeting de Adobe Campaign
description: En la configuración de la segmentación se incluye la creación de segmentos, una marca, una campaña y experiencias.
seo-description: En la configuración de la segmentación se incluye la creación de segmentos, una marca, una campaña y experiencias.
uuid: 520cd006-0aa8-43f3-b754-efb7397bb92f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bbc2aac9-ccf1-40c3-be4f-d59c2d0d8a6c
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 73%

---


# Targeting de Adobe Campaign{#targeting-your-adobe-campaign}

Para el targeting de la newsletter de Adobe Campaign, primero debe configurar la segmentación, que solo está disponible en la IU clásica. Después, puede crear experiencias con objetivos para Adobe Campaign.

## Configuración de la segmentación en AEM {#setting-up-segmentation-in-aem}

En la configuración de la segmentación se incluye la creación de segmentos, una marca, una campaña y experiencias. Solo puede crear un segmento en la IU clásica. Puede crear marcas, campañas y experiencias en la IU táctil.

>[!NOTE]
>
>El ID del segmento se debe asignar al ID de Adobe Campaign.

### Creación de segmentos {#creating-segments}

Para crear segmentos:

1. Abra la [consola de segmentación](http://localhost:4502/miscadmin#/etc/segmentation) en **&lt;host>:&lt;puerto>/miscadmin#/etc/segmentation**.
1. Cree una nueva página e introduzca un título (por ejemplo, **Segmentos de CA**) y seleccione la plantilla **Segmento (Adobe Campaign)**.
1. Seleccione la página creada en la vista de árbol de la parte izquierda.
1. Cree un segmento, por ejemplo, dirigido a usuarios masculinos. Para ello, cree una nueva página en el segmento que ha creado llamado Masculino y seleccione la plantilla **Segmento (Adobe Campaign)**.
1. Abra la página de segmento creada, arrastre el segmento **ID del segmento** desde la barra de tareas y suéltelo en la página.
1. Haga clic con el botón doble en la característica, introduzca el ID que representa en este caso el segmento masculino definido en Adobe Campaign (por ejemplo, **MALE**) y haga clic en **Aceptar**. Debe aparecer el siguiente mensaje: `targetData.segmentCode == "MALE"`
1. Repita los pasos para otro segmento, por ejemplo, un segmento dirigido a usuarias femeninas.

### Creación de una marca {#creating-a-brand}

Para crear una marca:

1. En **Sitios**, vaya a la carpeta **Campañas** (por ejemplo, en We.Retail).
1. Haga clic en **Crear página** e introduzca un título para la página, como por ejemplo We.Retail Brand, y seleccione la plantilla **Marca**.

### Creación de una campaña {#creating-a-campaign}

Para crear una campaña:

1. Abra la página **Marca** que acaba de crear.
1. Haga clic en **Crear página** e introduzca un título para la página, como por ejemplo We.Retail Campaign, seleccione la plantilla **Campaña** y haga clic en **Crear**.

### Creación de experiencias  {#creating-experiences}

Para crear experiencias para los segmentos:

1. Abra la página **Campaña** que acaba de crear.
1. Cree experiencias para sus segmentos haciendo clic en **Crear página** e introduciendo un título para su página, por ejemplo, Hombre mientras crea una experiencia para el segmento Hombre, y seleccione la plantilla **Experiencia**.
1. Abra la página de la experiencia creada.
1. Haga clic en **Editar** y, debajo de Segmentos, haga clic en **Añadir elemento**.
1. Escriba la ruta de acceso al segmento masculino, por ejemplo `/etc/segmentation/ac-segments/male` y haga clic en **Aceptar**. Debe aparecer el siguiente mensaje: *La experiencia está dirigida a: Hombre*
1. Repita los pasos anteriores para crear una experiencia para todos los segmentos, como por ejemplo el segmento Femenino.

## Creación de una newsletter con contenido de destino  {#creating-a-newsletter-with-targeted-content}

Una vez que haya creado los segmentos, una marca, una campaña y una experiencia, puede crear una newsletter con contenido de destino. Después de crear la experiencia, vinculará estas a los segmentos.

Puede crear la newsletter con contenido de destino tanto en la interfaz de usuario clásica como en la táctil. Este documento describe el procedimiento para la IU táctil.

Para crear una newsletter con contenido de destino:

1. Cree una newsletter con contenido de destino: Debajo de Campañas de correo electrónico en Geometrixx Outdoors, toque o haga clic en **Crear** > **Página** y seleccione una de las plantillas de Adobe Campaign Mail.

   >[!NOTE]
   >
   >[Los ejemplos de correo electrónico solo están disponibles en Geometrixx](/help/sites-developing/we-retail.md#weretail). Descargue el contenido de ejemplo de Geometrixx de Uso compartido de paquetes.

1. En la newsletter, añada un componente de texto y personalización.
1. Añada texto en el componente de texto y personalización, como &quot;Este es el valor predeterminado&quot;.
1. Haga clic en la flecha junto a **Editar** y seleccione **Objetivo**.
1. Seleccione la marca del menú desplegable Marca y seleccione la campaña. (Se trata de la marca y la campaña que creó anteriormente).
1. Haga clic en **Iniciar Targeting**. Aparecerán los segmentos en el área Audiencias. La experiencia predeterminada se utiliza si ninguno de los segmentos definidos coincide.

   >[!NOTE]
   >
   >De forma predeterminada, los ejemplos de correo electrónico que se incluyen en AEM utilizan Adobe Campaign como motor de targeting. Para las newsletters personalizadas, es posible que tenga que seleccionar Adobe Campaign como motor de targeting. Durante el targeting, pulse o haga clic en + en la barra de herramientas, introduzca un título para la nueva actividad y seleccione **Adobe Campaign** como motor de targeting.

1. Haga clic en **Valor predeterminado** y luego en el componente de texto y personalización que ha añadido. Verá la diana con una flecha. Haga clic en el icono para dirigirse a este componente.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Vaya a otro segmento (Masculino), haga clic en **Agregar oferta** y luego haga clic en el icono del signo más (+). A continuación, edite la oferta.
1. Vaya a otro segmento (Femenino), haga clic en **Agregar oferta** y luego haga clic en el icono del signo más (+). A continuación, edite esta oferta.
1. Haga clic en **Siguiente** para ver Asignación, luego haga clic en **Siguiente** para ver Configuración, que no se aplica a Adobe Campaign, y haga clic en **Guardar**.

   AEM genera automáticamente el código de targeting correcto para Adobe Campaign cuando el contenido se utiliza en un envío en Adobe Campaign.

1. En Adobe Campaign, cree el envío: seleccione **Envío por correo electrónico con contenido de AEM**, seleccione la cuenta local de AEM, según corresponda, y confirme los cambios.

   En la vista HTML, las distintas experiencias de componentes de destino se incluyen en el código de targeting de Adobe Campaign.

   ![chlimage_1-166](assets/chlimage_1-166.png)

   >[!NOTE]
   >
   >Si también establece los segmentos en Adobe Campaign, al hacer clic en **Previsualizar**, aparecerá una lista con las experiencias para cada segmento.

