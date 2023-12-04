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
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Integración de páginas de destino con Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

AEM ha integrado la solución de páginas de aterrizaje de con [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) mediante los siguientes componentes de llamada a la acción (CTA):

1. Componente Clic
1. Componente Vínculo gráfico

Estos componentes exponen ciertos atributos que se pueden asignar a través de variables de Adobe Analytics (tráfico, variables de conversión) y eventos de éxito para enviar información a Adobe Analytics.

## Requisitos previos {#prerequisites}

El Adobe recomienda que revise las [AEM integración existente con Adobe Analytics](/help/sites-administering/adobeanalytics.md) para comprender cómo funciona esta integración.

## Componentes disponibles para asignación {#components-available-for-mapping}

AEM En el caso de los **Llamada a acción** componentes - **ClickThroughLink** y **GraphicalLink** : mostrado aquí en la barra de tareas, se puede asignar a variables de Adobe Analytics.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### Asignación de componentes de página de aterrizaje a Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

Para asignar componentes de página de aterrizaje a Adobe Analytics:

1. Después de crear la configuración de Adobe Analytics y de crear un marco de trabajo, seleccione el grupo de informes adecuado en el menú desplegable. Esto hace que se recuperen las variables de Adobe Analytics y se muestren en el buscador de contenido.
1. Arrastre y suelte los componentes de llamada a la acción (CTA) de la barra de tareas en el área de asignación situada en el centro de la página, según corresponda.

<table>
 <tbody>
  <tr>
   <td><strong>Nombre del componente</strong></td>
   <td><strong>Atributos expuestos</strong></td>
   <td><strong>Significado del atributo</strong></td>
  </tr>
  <tr>
   <td><strong>Vínculo de pulsación CTA</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>La etiqueta del vínculo o el texto del vínculo </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>El destino al que se le redirige al hacer clic en el vínculo </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>El evento de clic </td>
  </tr>
  <tr>
   <td><strong>Vínculo gráfico de CTA</strong></td>
   <td><i>eventdata.clicktroughImageLabel</i> <br /> </td>
   <td>El título de la imagen de CTA </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageTarget</i> <br /> </td>
   <td>El destino al que se le lleva al hacer clic en la imagen que contiene un vínculo</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageAsset</i> <br /> </td>
   <td>La ruta al recurso de imagen en el repositorio </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughImageClick</i> <br /> </td>
   <td>El evento de clic</td>
  </tr>
 </tbody>
</table>

1. Asigne estos atributos expuestos con cualquier variable de Adobe Analytics desde el buscador de contenido. El marco de trabajo ya está listo para usarse.
1. Ahora puede crear una página de aterrizaje o abrir una existente con componentes de CTA existentes y hacer clic en **Cloud Service** pestaña en **Propiedades de página** en la barra de tareas (en la IU táctil optimizada, seleccione **Abrir propiedades** y haga clic en **Cloud Service**) y configure el marco de trabajo para utilizarlo con la página de aterrizaje. Seleccione el marco de trabajo de la lista desplegable.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Después de configurar el marco de trabajo con la página de aterrizaje, ahora puede utilizar los componentes instrumentados y cualquier clic en CTA se registra en Adobe Analytics.
