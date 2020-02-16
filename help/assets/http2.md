---
title: Envío de contenido HTTP2
description: HTTP/2 mejora la forma en que se comunican los exploradores y los servidores, lo que permite una transferencia de información más rápida y, al mismo tiempo, reduce la cantidad de potencia de procesamiento necesaria.
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Envío de contenido HTTP2 {#http-delivery-of-content}

Adobe se complace en anunciar la disponibilidad de la entrega de contenido HTTP/2 con la ventaja general de un rendimiento mejorado.

## ¿Qué es HTTP/2? {#what-is-http}

HTTP/2 mejora la forma en que se comunican los exploradores y los servidores, lo que permite una transferencia de información más rápida y, al mismo tiempo, reduce la cantidad de potencia de procesamiento necesaria.

El siguiente sitio web describe HTTP/2 y sus beneficios de una manera breve y simple:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## ¿Cuáles son las ventajas clave de pasar a HTTP/2 para la entrega de contenido? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

La mejora del rendimiento varía ampliamente en función de factores como el código del sitio web, el uso de Dynamic Media, el dispositivo, la pantalla y la ubicación del consumidor, etc.

Las propias pruebas de Adobe produjeron los siguientes resultados:

* En el caso de las imágenes, el tiempo de respuesta mejoró entre un 7% y un 28% en función del dispositivo y el explorador. Las mejoras de rendimiento más notables se produjeron en dispositivos iOS.
* Para los visores, el rendimiento del tiempo de carga ha mejorado un 15 %.

La siguiente demostración ilustra la diferencia entre la carga HTTP/1 y la carga HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## ¿Puedo cambiar a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para utilizar HTTP/2, debe cumplir los siguientes requisitos:

* Utilice HTTPS seguro para sus solicitudes de medios enriquecidos.
* Utilice la CDN (red de entrega de contenido) incluida en Adobe como parte de su licencia de Dynamic Media.
* Utilice un dominio dedicado (que no sea empresa-h.assetsadobe#.com).

   Si ya tiene un dominio dedicado, puede optar por la asistencia técnica.

   Si no tiene un dominio dedicado, Adobe programará la transición a HTTP/2 en 2018.

## ¿Cuál es el proceso para activar HTTP/2 en mi cuenta de Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

Debe iniciar la solicitud para cambiar a HTTP/2; no se hace automáticamente por usted.

1. Inicie una solicitud de asistencia técnica para cambiar a HTTP2. Consulte [Acceso al portal](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)de asistencia de AEM.

   1. Proporcione la siguiente información en su solicitud de asistencia:

      1. Nombre de contacto principal, correo electrónico, teléfono.
      1. Todos los dominios que se van a transferir a HTTP2.
      1. Compruebe que está utilizando HTTPS seguro para solicitudes de medios enriquecidos.
      1. Verifique que esté utilizando la CDN a través de Adobe y que no se administre con una relación directa.
      1. Compruebe que está utilizando un dominio dedicado. Si utiliza Dynamic Media, ya está utilizando un dominio dedicado.
   1. La asistencia técnica lo agregará a la lista de espera de clientes HTTP/2 en función del orden en que se enviaron las solicitudes.
   1. Cuando Adobe esté preparado para gestionar su solicitud, el servicio de asistencia técnica se pondrá en contacto con usted para coordinar la transición y establecer una fecha de destino.
   1. Se le notificará una vez finalizada la operación y podrá verificar la transición correcta a HTTP2.

      Dado que el navegador no indica este hecho, es necesario descargar una extensión.

      Para Firefox y Chrome hay una extensión denominada &quot;HTTP/2 e Indicador SPDY&quot;. Los navegadores solo admiten http/2 de forma segura, por lo que es necesario llamar a una URL con https para verificar. Si se admite http/2, esto se indica con la extensión en forma de símbolo Flash azul y con el encabezado &quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.


## ¿Cuándo puedo esperar que se realice la transición a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Las solicitudes se tramitarán en el orden en que sean recibidas por el servicio de asistencia técnica.

>[!NOTE]
>
>Puede haber un largo tiempo de espera porque la transición a HTTP/2 implica borrar la caché. Por lo tanto, solo se pueden gestionar algunas transiciones de cliente a la vez.

## ¿Cuáles son los riesgos de pasar a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transición a HTTP/2 borra la caché en la CDN porque implica el desplazamiento a una nueva configuración de CDN.

El contenido no almacenado en caché llega directamente a los servidores de origen de Adobe hasta que se vuelve a crear la caché. Debido a esto, Adobe tiene previsto gestionar algunas transiciones de clientes a la vez, de modo que se mantenga un rendimiento aceptable al extraer solicitudes de nuestro origen.

## ¿Cómo puede verificar si una dirección URL o un sitio web está activado con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Dado que el navegador no indica este hecho, es necesario descargar una extensión.

Para Firefox y Chrome hay una extensión denominada &quot;HTTP/2 e Indicador SPDY&quot;. Los navegadores solo admiten http/2 de forma segura, por lo que es necesario llamar a una URL con https para verificar. Si se admite http/2, esto se indica con la extensión en forma de símbolo Flash azul y con el encabezado &quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.
