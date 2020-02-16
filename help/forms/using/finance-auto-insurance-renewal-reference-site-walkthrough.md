---
title: Recorrido por el sitio de referencia de la renovación automática de seguros de We.Finance
seo-title: Recorrido por el sitio de referencia de la renovación automática de seguros de We.Finance
description: nulo
seo-description: nulo
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
translation-type: tm+mt
source-git-commit: b2fd6e0412ee0dacf7b68f4a0b219804dd4a6150

---


# Recorrido por el sitio de referencia de la renovación automática de seguros de We.Finance{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## Requisitos previos {#pre-requisites}

Configure el sitio de referencia tal como se describe en [Configuración y configure el sitio](../../forms/using/setup-reference-sites.md)de referencia de formularios AEM.

## Escenario de sitio de referencia de We.Finance {#we-finance-reference-site-scenario}

El sitio Web de We.Finance es un sitio de servicios financieros diseñado para ayudarle a aprender las capacidades de comunicación interactiva de AEM Forms.

Lea el tutorial detallado del caso de uso de We.Finance Auto Insurance, que muestra cómo los formularios AEM y su integración con Microsoft Dynamics ayudan a personalizar la experiencia del cliente en una empresa de servicios financieros. El tutorial interactivo está diseñado para facilitar la implementación de transacciones digitales complejas y la comunicación con los clientes en una empresa financiera.

**El viaje comienza con el caso de uso:**

Sarah Rose es una cliente existente de We.Finance y ha adquirido una póliza de seguro de automóviles. Ahora es el momento del año para la renovación de su póliza de seguro. Gloria Rios, agente de seguros, We.Finance envía un recordatorio a Sarah sobre la renovación de su política. Sarah sigue las instrucciones proporcionadas en el correo electrónico y completa el proceso con éxito.

## Recorrido de solicitudes de seguros automáticos {#auto-insurance-application-walkthrough}

El escenario de la aplicación de seguros automáticos We.Finance es una narración visual para el usuario y se basa en dos personalidades:

* Sarah Rose, una cliente de We.Finance
* Gloria Rios, agente de seguros, We.Finance

### Gloria envía una comunicación de renovación de pólizas de seguros desde We.Finance {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria inicia sesión en la instancia de AEM, hace clic en Renovación **automática de seguros y,** a continuación, hace clic en **Abrir interfaz de usuario del agente.** El clic se muestra como prefijo en el documento de seguro con los detalles de la póliza de Sarah Rose. Gloria hace clic **en Enviar** y aparece un mensaje en la pantalla &quot;Envío iniciado&quot; y, a continuación, en pocos segundos &quot;Enviado correctamente&quot;.

Sarah recibe un correo electrónico con el asunto &quot;Su renovación automática del seguro&quot;.

![IU del agente](assets/agent_ui_email_new.png)

#### Véalo usted mismo {#see-it-yourself}

Vaya a **Adobe Experience Manager** > **Formularios** > **Formularios y documentos** > **We.Finance** > **Auto Insurance**. Seleccione la comunicación **** interactiva Renovación automática de seguros y haga clic en **Abrir interfaz de usuario** del agente. La comunicación interactiva se abre en la interfaz de usuario del agente. Introduzca una dirección de correo electrónico válida para recibir el correo electrónico con el documento de directiva adjunto y haga clic en Enviar.

Puede acceder a la comunicación interactiva Renovación automática de seguros y revisarla directamente desde `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah recibe una comunicación de renovación de pólizas de seguros de We.Finance y decide renovar la póliza {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah recibe un correo electrónico con un archivo adjunto de We.Finance que le recuerda que su póliza de Seguro Automático está a punto de caducar. El archivo adjunto es la versión impresa de su carta de seguro automático.

Sarah hace clic en **Renovar ahora** y se dirige a la versión web de su carta de seguro automático. Además de esta carta, Sarah encuentra la cantidad de días que le quedan a su política para que caduque. La página proporciona a Sarah una visión general básica de los detalles de su póliza de seguro, como el número de póliza, el importe adeudado y otra información como ofertas de descuento y recompensas por lealtad. Sarah de nuevo hace clic en **Renovar ahora** en la parte inferior de la política.

![ref1](assets/ref1.png)

#### Cómo funciona {#how-it-works}

La salida web y de impresión de la carta de Seguros automáticos se crean utilizando las capacidades multicanal de Comunicaciones interactivas.

El botón Renovar ahora del correo electrónico está vinculado a la aplicación Renovación automática de seguros, que es una comunicación interactiva en una instancia de publicación.

#### Véalo usted mismo {#see-it-yourself-1}

Debe haber recibido un correo electrónico con un PDF adjunto. El PDF es una versión impresa de la carta de seguro automático. Haga clic en **Renovar ahora** para acceder a la versión web de la directiva. Compruebe su información personal y los detalles de las políticas y haga clic en **Renovar ahora** , que lo lleva a otra comunicación interactiva.

El botón **Renovar ahora** del correo electrónico dirige a Sarah a la versión web de la política. Puede visitar la siguiente dirección URL:

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

Puede consultar el resumen detallado de la renovación automática del seguro y hacer clic en **Renovar ahora** en la parte inferior de la página.

### Sarah llega a la página de pago {#sarah-reaches-the-payment-page}

We.Finance lleva a Sarah a la página de pago. Sarah vuelve a comprobar su número de política y su fecha de caducidad con sus registros. En el lado derecho de la página, comprueba el Resumen de Pago de su renovación con un descuento del 10% sobre la cantidad total.

#### Cómo funciona {#how-it-works-1}

El botón Renovar ahora dirige a Sarah a la página de pago. La página de pago es un formulario adaptable.

#### Véalo usted mismo {#see-it-yourself-2}

Haga clic en **Renovar ahora** para acceder a la página Pago. Rellene la información de su tarjeta de crédito y haga clic en **Realizar pago**.

Puede acceder a la página de pago en la instancia de creación en

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah hace el pago y completa el proceso {#sarah-makes-the-payment-and-completes-the-process}

Sarah rellena los detalles de su tarjeta de crédito y hace clic en **Realizar pago**.

#### Cómo funciona {#how-it-works-2}

Cuando Sarah rellena los detalles de la tarjeta de crédito y hace clic en Enviar, se procesa el pago con tarjeta de crédito y aparece en pantalla un mensaje de agradecimiento configurado en el formulario adaptable.

#### Véalo usted mismo {#see-it-yourself-3}

Puede ver el mensaje de confirmación después de hacer clic en Realizar pago en

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
