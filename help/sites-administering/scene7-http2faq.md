---
title: Preguntas frecuentes sobre la entrega de contenido HTTP2
description: Obtenga información sobre la entrega de contenido HTTP2.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2428914c-5fb0-439e-a1ef-8ee30b890f58
source-git-commit: 1349d9929fc64ad46fc91f0d189bab54cca9de81
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 1%

---

# Preguntas frecuentes sobre la entrega de contenido HTTP2{#http-delivery-of-content-faq}

Adobe se complace en anunciar la disponibilidad de la entrega HTTP/2 de contenido. Al utilizar HTTP/2, se observa un aumento del rendimiento general.

## ¿Qué es HTTP/2? {#what-is-http}

HTTP/2 mejora la forma en que se comunican los exploradores y los servidores, lo que permite una transferencia de información más rápida y, al mismo tiempo, reduce la cantidad de potencia de procesamiento necesaria.

El siguiente sitio web describe HTTP/2 y sus ventajas de una manera breve y sencilla:

[Lo que debe saber sobre HTTP/2](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/).

## ¿Cuáles son las ventajas clave del paso a HTTP/2 para la entrega de contenido? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

La mejora del rendimiento varía ampliamente en función de factores como el código del sitio web, el uso de Dynamic Media, el dispositivo, la pantalla y la ubicación del cliente.

Las propias pruebas de Adobe dieron los siguientes resultados:

* En el caso de las imágenes, el tiempo de respuesta mejoró del 7 % al 28 % en función del dispositivo y el navegador. Las mejoras de rendimiento más notables se produjeron en dispositivos iOS.
* Para los visores, el rendimiento del tiempo de carga ha mejorado un 15%.

La siguiente demostración ilustra la diferencia entre la carga HTTP/1 y HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## ¿Puedo cambiar a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para utilizar HTTP/2, debe cumplir los siguientes requisitos:

* Utilice HTTPS seguro para sus solicitudes de medios enriquecidos.
* Utilice la CDN (red de entrega de contenido) incluida en la Adobe como parte de su licencia de Dynamic Media.
* Utilice un dominio dedicado (es decir, `images.company.com` o `mycompany.scene7.com`), no un dominio Dynamic Media genérico (es decir, `s7d1.scene7.com`, `s7d2.scene7.com` o `s7d13.scene7.com`).

   Para encontrar sus dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicie sesión en la cuenta o cuentas de su empresa. A continuación, pulse **[!UICONTROL Configuración > Configuración de la aplicación > Configuración general]**. Busque el campo denominado **Published Server Name**. Si está utilizando un dominio genérico de Dynamic Media, puede solicitar pasar a su propio dominio personalizado como parte de esta transición.

## ¿Cuál es el proceso para habilitar HTTP/2 para mi cuenta de Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. [Utilice el Admin Console para crear un caso de asistencia ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) y solicitar cambiar a HTTP/2; no se realiza automáticamente.
1. Proporcione la siguiente información en su caso de asistencia:

   * Nombre de contacto principal, correo electrónico y número de teléfono.
   * Todos los dominios que se van a transferir a HTTP2. Es decir, `images.company.com` o `mycompany.scene7.com`.

      Para encontrar sus dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicie sesión en la cuenta o cuentas de su empresa. A continuación, pulse **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo denominado **[!UICONTROL Published Server Name]**.

   * Compruebe que utiliza HTTPS seguro para solicitudes de medios enriquecidos.
   * Compruebe que está utilizando la CDN a través de la Adobe y que no se administra con una relación directa.
   * Compruebe que está utilizando un dominio dedicado. Es decir, `images.company.com` o `mycompany.scene7.com`, no es un dominio genérico de Dynamic Media como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Para encontrar sus dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicie sesión en la cuenta o cuentas de su empresa. A continuación, pulse **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo denominado **[!UICONTROL Published Server Name]**. Si está utilizando un dominio genérico de Dynamic Media, puede solicitar pasar a su propio dominio personalizado como parte de esta transición.

1. La asistencia técnica le añade a la lista de espera de clientes HTTP/2 en función del orden en que se enviaron las solicitudes.
1. Cuando el Adobe esté listo para gestionar su solicitud, el equipo de asistencia técnica se pondrá en contacto con usted para coordinar la transición y establecer una fecha objetivo.
1. Se le notificará una vez finalizada y podrá verificar que la transición a HTTP2 se ha realizado correctamente.

## ¿Cuándo puedo esperar que se pase a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Las solicitudes se procesan en el orden en que son recibidas por el servicio de asistencia técnica.

>[!NOTE]
>
>Hay un largo tiempo de espera porque la transición a HTTP/2 implica borrar la caché. Por lo tanto, solo se pueden gestionar algunas transiciones de cliente a la vez.

## ¿Cuáles son los riesgos de pasar a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transición a HTTP/2 borra la caché en la CDN porque implica pasar a una nueva configuración de CDN.

El contenido no almacenado en caché llega directamente a los servidores de origen del Adobe hasta que se vuelve a crear la caché. Debido a esta acción, Adobe planea gestionar algunas transiciones de cliente a la vez, de modo que se mantenga un rendimiento aceptable al extraer solicitudes del origen de Adobe.

## ¿Cómo se puede verificar si una URL o un sitio web está activado con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Descargue una extensión que puede utilizar con el explorador web. Para Firefox y Chrome, hay una extensión llamada **[!UICONTROL HTTP/2 e Indicador SPDY]**. Los navegadores solo admiten HTTP/2 de forma segura, por lo que es necesario llamar a una dirección URL con HTTPS para verificarlo. Si se admite HTTP/2, se indica con la extensión en forma de símbolo de Flash azul y con el encabezado &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.
