---
title: Segmentación de Adobe Campaign
description: La configuración de la segmentación incluye la creación de segmentos, una marca, una campaña y experiencias.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: e56986b2-397e-4802-992b-05a9ea7b2e36
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# Segmentación de Adobe Campaign{#targeting-your-adobe-campaign}

Para dirigirse al boletín informativo de Adobe Campaign, primero debe configurar la segmentación, que solo está disponible en la IU clásica. Después, puede crear experiencias segmentadas para Adobe Campaign.

## AEM Configuración de la segmentación en las {#setting-up-segmentation-in-aem}

La configuración de la segmentación incluye la creación de segmentos, una marca, una campaña y experiencias. Solo puede crear un segmento en la IU clásica. Puede crear marcas, campañas y experiencias en la interfaz de usuario táctil.

>[!NOTE]
>
>El ID del segmento debe asignarse al del lado de Adobe Campaign.

### Creación de segmentos {#creating-segments}

Para crear segmentos:

1. Abra el [consola de segmentación](http://localhost:4502/miscadmin#/etc/segmentation) en **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. Cree una página e introduzca un título; por ejemplo, **Segmentos de CA** - y seleccione el **Segmento (Adobe Campaign)** plantilla.
1. Seleccione la página creada en la vista de árbol de la izquierda.
1. Cree un segmento, por ejemplo, dirigido a usuarios hombres, creando una página en el segmento que ha creado llamada Hombre y seleccione **Segmento (Adobe Campaign)** plantilla.
1. Abra la página de segmentos creada y arrastre y suelte un **ID del segmento** de la barra de tareas a la página.
1. Haga doble clic en la característica e introduzca el ID que representa, en este caso, el segmento masculino definido en Adobe Campaign; por ejemplo, **MASCULINO** - y haga clic en **OK**. Debe aparecer el siguiente mensaje: `targetData.segmentCode == "MALE"`
1. Repita los pasos para otro segmento, por ejemplo, un segmento dirigido a mujeres.

### Creación de una marca {#creating-a-brand}

Para crear una marca:

1. Entrada **Sites**, vaya al **Campañas** (por ejemplo, en We.Retail).
1. Clic **Crear página** y escriba un título para la página, por ejemplo, Marca We.Retail, y seleccione **Marca** plantilla.

### Creación de una campaña {#creating-a-campaign}

Para crear una campaña:

1. Abra el **Marca** página que ha creado.
1. Clic **Crear página** y escriba un título para su página, por ejemplo, We.Retail Campaign, y seleccione **Campaign** y haga clic en **Crear**.

### Creación de experiencias {#creating-experiences}

Para crear experiencias para segmentos:

1. Abra el **Campaign** página que ha creado.
1. Cree experiencias para sus segmentos haciendo clic en **Crear página** y escriba un título para su página, por ejemplo, Hombre mientras crea una experiencia para el segmento Hombre, y seleccione **Experiencia** plantilla.
1. Abra la página de experiencia creada.
1. Clic **Editar**, a continuación, haga clic en Segmentos **Agregar elemento**.
1. Introduzca la ruta al segmento masculino, por ejemplo, `/etc/segmentation/ac-segments/male` y haga clic en **OK**. Debe aparecer el siguiente mensaje: *La experiencia se dirige a: Hombre*
1. Repita los pasos anteriores para crear una experiencia para todos los segmentos, por ejemplo, el segmento femenino.

## Creación de una newsletter con contenido de destino {#creating-a-newsletter-with-targeted-content}

Después de crear segmentos, una marca, una campaña y una experiencia, puede crear una newsletter con contenido de destino. Después de crear la experiencia, las vincula a sus segmentos.

Puede crear la newsletter con contenido de destino en la interfaz de usuario táctil y clásica. Este documento describe el procedimiento para la IU táctil.

Para crear una newsletter con contenido de destino:

1. Cree una newsletter con contenido de destino: debajo de Campañas de correo electrónico en Geometrixx Outdoors, toque o haga clic en **Crear** > **Página** y seleccione una de las plantillas de correo de Adobe Campaign.

   >[!NOTE]
   >
   >[Los ejemplos de correo electrónico solo están disponibles en Geometrixx](/help/sites-developing/we-retail.md#weretail). Descargar contenido de Geometrixx de muestra desde Package Share.

1. En la newsletter, añada un componente Texto y personalización.
1. Agregue texto al componente Texto y personalización, como &quot;Este es el predeterminado&quot;.
1. Haga clic en la flecha situada junto a **Editar** y seleccione **Segmentación**.
1. Seleccione la marca en el menú desplegable Marca y seleccione la Campaña. (Esta es la marca y la campaña que creó anteriormente).
1. Clic **Iniciar segmentación**. Verá sus segmentos aparecer en el área Audiencias. La experiencia predeterminada se utiliza si ninguno de los segmentos definidos coincide.

   >[!NOTE]
   >
   >AEM De forma predeterminada, los ejemplos de correo electrónico incluidos con el uso de Adobe Campaign como motor de segmentación de datos utilizan el. Para los boletines personalizados, es posible que tenga que seleccionar Adobe Campaign como motor de segmentación. Al segmentar, toque o haga clic en + en la barra de herramientas, introduzca un título para la nueva actividad y seleccione **Adobe Campaign** como motor de segmentación.

1. Clic **Predeterminado** y luego el componente Texto y personalización que agregó, y verá la diana con una flecha en ella. Haga clic en el icono para orientar este componente.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Vaya a otro segmento (Hombre) y haga clic en **Añadir oferta** y haga clic en el icono +. A continuación, edite la oferta.
1. Vaya a otro segmento (femenino) y haga clic en **Añadir oferta** y el icono +. Luego edite esta oferta.
1. Clic **Siguiente** para ver la Asignación, haga clic en **Siguiente** para ver la Configuración, que no se aplica a Adobe Campaign, y haga clic en **Guardar**.

   AEM El genera automáticamente el código de segmentación correcto para Adobe Campaign cuando el contenido se utiliza en una entrega dentro de Adobe Campaign

1. En Adobe Campaign, cree su entrega: seleccione **AEM Envío de correo electrónico con contenido de** AEM y seleccione la cuenta de la cuenta local de, según corresponda, y confirme los cambios.

   En la vista de HTML, las diferentes experiencias de los componentes segmentados se incluyen en el código de segmentación de Adobe Campaign.

   ![chlimage_1-166](assets/chlimage_1-166.png)

   >[!NOTE]
   >
   >Si también configura los segmentos en Adobe Campaign, haga clic en **Previsualizar** le mostrará las experiencias de cada segmento.
