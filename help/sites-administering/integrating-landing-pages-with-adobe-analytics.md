---
title: Integración de Páginas de aterrizaje con Adobe Analytics
seo-title: Integración de Páginas de aterrizaje con Adobe Analytics
description: Aprenda a integrar páginas de aterrizaje con Adobe Analytics.
seo-description: Aprenda a integrar páginas de aterrizaje con Adobe Analytics.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 24%

---


# Integración de Páginas de aterrizaje con Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

AEM ha integrado la solución páginas de aterrizaje con [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) mediante los siguientes componentes de llamada a acción (CTA):

1. Componente de pulsaciones
1. Componente de vínculo gráfico

Estos componentes exponen determinados atributos que se pueden asignar mediante variables de Adobe Analytics (tráfico, variables de conversión) y eventos de éxito para enviar información a Adobe Analytics.

## Requisitos previos {#prerequisites}

Adobe recomienda que consulte la [integración existente de AEM-Adobe Analytics](/help/sites-administering/adobeanalytics.md) para comprender cómo funciona esta integración.

## Componentes que se pueden asignar {#components-available-for-mapping}

En AEM, los componentes **Llamada a acción** - **ClickThroughLink** y **GraphicalLink** - mostrados aquí en la barra de tareas, se pueden asignar a variables de Adobe Analytics.

![chlimage_1-29](assets/chlimage_1-21a.jpeg)

### Asignación de componentes de Página de aterrizaje a Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

Para asignar componentes de página de aterrizaje a Adobe Analytics:

1. Después de crear la configuración de Adobe Analytics y crear una nueva estructura, seleccione el grupo de sistemas de informes adecuado en el menú desplegable. Esto resulta en recuperar las variables de Adobe Analytics y mostrarlas en el buscador de contenido.
1. Arrastre los componentes de llamada a acción de la barra de tareas y suéltelos en el área de asignación situada en la parte central de la página, como convenga.

<table>
 <tbody>
  <tr>
   <td><strong>Nombre del componente</strong></td>
   <td><strong>Atributos expuestos</strong></td>
   <td><strong>Significado del atributo</strong></td>
  </tr>
  <tr>
   <td><strong>Llamada a acción: vínculo de pulsaciones</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>La etiqueta en el vínculo o el texto del vínculo </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>El destino al que se dirigirá cuando haga clic en el vínculo </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.eventos.clickthroughLinkClick</i> <br /> </td>
   <td>Evento de clic </td>
  </tr>
  <tr>
   <td><strong>Llamada a acción: vínculo gráfico</strong></td>
   <td><i>eventdata.clicktroughImageLabel</i> <br /> </td>
   <td>Título de la imagen de llamada a acción </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageTarget</i> <br /> </td>
   <td>Destino al que se dirigirá el usuario cuando haga clic en la imagen que contenga un vínculo</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clicktroughImageAsset</i> <br /> </td>
   <td>Ruta al recurso de imagen en el repositorio </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.eventos.clicktroughImageClick</i> <br /> </td>
   <td>Evento de clic</td>
  </tr>
 </tbody>
</table>

1. Asigne estos atributos expuestos a cualquier variable de Adobe Analytics desde Content Finder. El marco está listo para usarse.
1. Ahora puede crear una nueva página de aterrizaje o abrir una página de aterrizaje existente con componentes de llamada a acción existentes, hacer clic en la ficha **Cloud Services** de **Propiedades de la página** de la barra de tareas (en la IU táctil, seleccione **Propiedades abiertas** y haga clic en **Cloud Services**) y configurar la estructura que se utilizará con página de aterrizaje. Seleccione la estructura de la lista desplegable.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Después de configurar la estructura con la página de aterrizaje, ahora puede utilizar los componentes instrumentados y cualquier clic en CTA se registra en Adobe Analytics.

