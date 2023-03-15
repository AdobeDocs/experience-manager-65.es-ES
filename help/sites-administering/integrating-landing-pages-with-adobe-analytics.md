---
title: Integración de páginas de destino con Adobe Analytics
seo-title: Integrating Landing Pages with Adobe Analytics
description: Aprenda a integrar páginas de aterrizaje con Adobe Analytics.
seo-description: Learn how to integrate landing pages with Adobe Analytics.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 25%

---

# Integración de páginas de destino con Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

AEM ha integrado la solución de páginas de aterrizaje de con [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) mediante los siguientes componentes de llamada a la acción (CTA):

1. Componente de pulsaciones
1. Componente de vínculo gráfico

Estos componentes exponen ciertos atributos que se pueden asignar a través de variables de Adobe Analytics (tráfico, variables de conversión) y eventos de éxito para enviar información a Adobe Analytics.

## Requisitos previos {#prerequisites}

El Adobe recomienda que revise las [AEM integración existente con Adobe Analytics](/help/sites-administering/adobeanalytics.md) para comprender cómo funciona esta integración.

## Componentes que se pueden asignar {#components-available-for-mapping}

AEM En el caso de los **Llamada a acción** componentes - **ClickThroughLink** y **GraphicalLink** : mostrado aquí en la barra de tareas, se puede asignar a variables de Adobe Analytics.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### Asignación de componentes de página de aterrizaje a Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

Para asignar componentes de página de aterrizaje a Adobe Analytics:

1. Después de crear la configuración de Adobe Analytics y de crear una nueva estructura, seleccione el grupo de informes adecuado en el menú desplegable. Esto hace que se recuperen las variables de Adobe Analytics y se muestren en el buscador de contenido.
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
   <td>El destino al que se le redirige cuando hace clic en el vínculo </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>Evento de clic </td>
  </tr>
  <tr>
   <td><strong>Llamada a acción: vínculo gráfico</strong></td>
   <td><i>eventdata.clicktroughImageLabel</i> <br /> </td>
   <td>El título de la imagen de CTA </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageTarget</i> <br /> </td>
   <td>Destino al que se dirigirá el usuario cuando haga clic en la imagen que contenga un vínculo</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageAsset</i> <br /> </td>
   <td>Ruta al recurso de imagen en el repositorio </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughImageClick</i> <br /> </td>
   <td>Evento de clic</td>
  </tr>
 </tbody>
</table>

1. Asigne estos atributos expuestos con cualquier variable de Adobe Analytics desde el buscador de contenido. El marco de trabajo ya está listo para usarse.
1. Ahora puede crear una nueva página de aterrizaje o abrir una existente con componentes de CTA existentes y hacer clic en **Cloud Services** pestaña en **Propiedades de página** en la barra de tareas (en la IU táctil optimizada, seleccione **Abrir propiedades** y haga clic en **Cloud Services**) y configure el marco de trabajo para utilizarlo con la página de aterrizaje. Seleccione la estructura de la lista desplegable.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Después de configurar el marco de trabajo con la página de aterrizaje, ahora puede utilizar los componentes instrumentados y cualquier clic en CTA se registra en Adobe Analytics.
