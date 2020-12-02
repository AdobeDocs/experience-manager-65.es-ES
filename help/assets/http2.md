---
title: ENVÍO de contenido HTTP2
description: HTTP/2 mejora la forma en que se comunican los exploradores y los servidores, lo que permite una transferencia de información más rápida y, al mismo tiempo, reduce la cantidad de potencia de procesamiento necesaria.
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---


# ENVÍO HTTP2 del contenido {#http-delivery-of-content}

Adobe está emocionado de anunciar la disponibilidad del envío de contenido HTTP/2 con el beneficio general de mejorar el rendimiento.

## ¿Qué es HTTP/2? {#what-is-http}

HTTP/2 mejora la forma en que se comunican los exploradores y los servidores, lo que permite una transferencia de información más rápida y, al mismo tiempo, reduce la cantidad de potencia de procesamiento necesaria.

El siguiente sitio web describe HTTP/2 y sus beneficios de una manera breve y simple:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## ¿Cuáles son las ventajas clave del cambio a HTTP/2 para el envío de contenido? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

La mejora del rendimiento varía ampliamente en función de factores como el código del sitio web, el uso de Dynamic Media, el dispositivo, la pantalla y la ubicación del consumidor, etc.

Las propias pruebas de Adobe dieron los siguientes resultados:

* En el caso de las imágenes, el tiempo de respuesta mejoró entre un 7% y un 28% en función del dispositivo y el explorador. Las mejoras de rendimiento más notables se produjeron en dispositivos iOS.
* Para los visores, el rendimiento del tiempo de carga ha mejorado un 15 %.

La siguiente demostración ilustra la diferencia entre la carga HTTP/1 y la carga HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## ¿Puedo cambiar a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para utilizar HTTP/2, debe cumplir los siguientes requisitos:

* Utilice HTTPS seguro para sus solicitudes de medios enriquecidos.
* Utilice la CDN (red de envío de contenido) incluida en el Adobe como parte de su licencia de Dynamic Media.
* Utilice un dominio dedicado (que no sea compañía-h.assetsadobe#.com).

   Si ya tiene un dominio dedicado, puede optar por la asistencia técnica.

   Si no tiene un dominio dedicado, Adobe programará su transición a HTTP/2 en 2018.

## ¿Cuál es el proceso para activar HTTP/2 en mi cuenta de Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

Debe iniciar la solicitud para cambiar a HTTP/2; no se hace automáticamente por usted.

1. Inicie una solicitud de asistencia técnica para cambiar a HTTP2. Consulte [Acceso al portal de soporte de AEM](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html).

   1. Proporcione la siguiente información en su solicitud de asistencia:

      1. Nombre de contacto principal, correo electrónico, teléfono.
      1. Todos los dominios que se van a transferir a HTTP2.
      1. Compruebe que está utilizando HTTPS seguro para solicitudes de medios enriquecidos.
      1. Compruebe que está utilizando la CDN mediante Adobe y que no se administran con una relación directa.
      1. Compruebe que está utilizando un dominio dedicado. Si utiliza Dynamic Media, ya está utilizando un dominio dedicado.
   1. La asistencia técnica lo agregará a la lista de espera de clientes HTTP/2 en función del orden en que se enviaron las solicitudes.
   1. Cuando Adobe esté listo para gestionar su solicitud, el servicio de soporte técnico se pondrá en contacto con usted para coordinar la transición y establecer una fecha de destinatario.
   1. Se le notificará una vez finalizada la operación y podrá comprobar si la transición a HTTP2 ha sido correcta.

      Dado que el navegador no indica este hecho, es necesario descargar una extensión.

      Para Firefox y Chrome hay una extensión denominada &quot;HTTP/2 e Indicador SPDY&quot;. Los navegadores solo admiten http/2 de forma segura, por lo que es necesario llamar a una URL con https para verificar. Si se admite http/2, esto se indica con la extensión en forma de símbolo de Flash azul y con el encabezado &quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.


## ¿Cuándo puedo esperar que se realice la transición a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Las solicitudes se tramitarán en el orden en que sean recibidas por el servicio de asistencia técnica.

>[!NOTE]
>
>Puede haber un largo tiempo de espera porque la transición a HTTP/2 implica borrar la caché. Por lo tanto, sólo se pueden gestionar unas pocas transiciones de clientes a la vez.

## ¿Cuáles son los riesgos de pasar a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transición a HTTP/2 borra la caché en la CDN porque implica pasar a una nueva configuración de CDN.

El contenido no almacenado en caché entra directamente en los servidores origen del Adobe hasta que se vuelve a crear la caché. Debido a esto, Adobe planea manejar algunas transiciones de clientes a la vez para mantener un rendimiento aceptable al extraer solicitudes de nuestro origen.

## ¿Cómo puede verificar si una dirección URL o un sitio web está activado con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Dado que el navegador no indica este hecho, es necesario descargar una extensión.

Para Firefox y Chrome hay una extensión denominada &quot;HTTP/2 e Indicador SPDY&quot;. Los navegadores solo admiten http/2 de forma segura, por lo que es necesario llamar a una URL con https para verificar. Si se admite http/2, esto se indica con la extensión en forma de símbolo de Flash azul y con el encabezado &quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.
