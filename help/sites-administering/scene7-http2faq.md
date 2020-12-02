---
title: Preguntas frecuentes sobre la entrega de contenido HTTP2
seo-title: Preguntas frecuentes sobre la entrega de contenido HTTP2
description: Obtenga información sobre el envío de contenido HTTP2.
seo-description: Obtenga información sobre el envío de contenido HTTP2.
uuid: e837c3e0-6e48-46f1-b510-847c9976807a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: afbe9f80-c2a3-4a46-b9d6-4c9406667d7f
translation-type: tm+mt
source-git-commit: 55f6517073ace72d468bb70853b745c2980b11f2
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 4%

---


# Preguntas frecuentes sobre la entrega de contenido HTTP2{#http-delivery-of-content-faq}

Adobe está emocionado de anunciar la disponibilidad del envío HTTP/2 del contenido. Al utilizar HTTP/2 notará un aumento general del rendimiento.

## ¿Qué es HTTP/2? {#what-is-http}

HTTP/2 mejora la forma en que se comunican los exploradores y los servidores, lo que permite una transferencia de información más rápida y, al mismo tiempo, reduce la cantidad de potencia de procesamiento necesaria.

El siguiente sitio web describe HTTP/2 y sus ventajas de una manera breve y sencilla:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## ¿Cuáles son las ventajas clave del cambio a HTTP/2 para el envío de contenido? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

La mejora del rendimiento varía ampliamente en función de factores como el código de su sitio web, el uso de Scene7, el dispositivo del consumidor, la pantalla y la ubicación, etc.

Las propias pruebas de Adobe dieron los siguientes resultados:

* En el caso de las imágenes, el tiempo de respuesta mejoró entre un 7% y un 28% en función del dispositivo y el explorador. Las mejoras de rendimiento más notables se produjeron en dispositivos iOS.
* Para los visores, el rendimiento del tiempo de carga ha mejorado un 15 %.

La siguiente demostración ilustra la diferencia entre la carga HTTP/1 y la carga HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## ¿Puedo cambiar a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para utilizar HTTP/2, debe cumplir los siguientes requisitos:

* Utilice HTTPS seguro para sus solicitudes de medios enriquecidos.
* Utilice la CDN (red de envío de contenido) incluida en el Adobe como parte de la licencia de Dynamic Media Classic.
* Utilice un dominio dedicado (es decir, `images.company.com` o `mycompany.scene7.com`), no un dominio genérico de Dynamic Media Classic (es decir, `s7d1.scene7.com`, `s7d2.scene7.com` o `s7d13.scene7.com`).

   Para encontrar los dominios, [inicie sesión en la instancia de Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) para cada cuenta de compañía.

   Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuracióngeneral.]** Busque el campo con la etiqueta Nombre **del servidor** publicado. Si actualmente está utilizando un dominio de Scene7 genérico, puede solicitar el traslado a su propio dominio personalizado como parte de esta transición.

## ¿Cuál es el proceso para activar HTTP/2 en mi cuenta de Dynamic Media Classic? {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. Debe [utilizar el Admin Console para crear un caso de soporte](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) y solicitar cambiar a HTTP/2; no se hace automáticamente por usted.
1. Proporcione la siguiente información en su caso de asistencia:

   * Nombre de contacto principal, correo electrónico y número de teléfono.
   * Todos los dominios que se van a transferir a HTTP2. Es decir, `images.company.com` o `mycompany.scene7.com`.

   Para encontrar los dominios, [inicie sesión en la instancia de Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) para cada cuenta de compañía.

   Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuracióngeneral.]** Busque el campo denominado Nombre del servidor  **[!UICONTROL publicado.]**

   * Compruebe que utiliza HTTPS seguro para solicitudes de medios enriquecidos.
   * Compruebe que está utilizando la CDN mediante Adobe y que no se administra con una relación directa.
   * Compruebe que está utilizando un dominio dedicado. Es decir, `images.company.com` o `mycompany.scene7.com`, no es un dominio de Scene7 genérico como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

   Para encontrar los dominios, [inicie sesión en la instancia de Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) para cada cuenta de compañía.

   Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuracióngeneral.]** Busque el campo denominado Nombre del servidor  **[!UICONTROL publicado.]** Si actualmente está utilizando un dominio de Scene7 genérico, puede solicitar el traslado a su propio dominio personalizado como parte de esta transición.

   1. La asistencia técnica le agrega a la lista de espera de clientes HTTP/2 en función del orden en que se enviaron las solicitudes.
   1. Cuando Adobe esté listo para gestionar su solicitud, el servicio de soporte técnico se pondrá en contacto con usted para coordinar la transición y establecer una fecha de destinatario.
   1. Se le notificará una vez finalizada la operación y podrá comprobar que la transición a HTTP2 se ha realizado correctamente.



## ¿Cuándo puedo esperar que se realice la transición a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Las solicitudes se procesan en el orden en que son recibidas por la asistencia técnica.

>[!NOTE]
>
>Puede haber un largo tiempo de espera porque la transición a HTTP/2 implica borrar la caché. Por lo tanto, sólo se pueden gestionar unas pocas transiciones de clientes a la vez.

## ¿Cuáles son los riesgos de pasar a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transición a HTTP/2 borra la caché en la CDN porque implica pasar a una nueva configuración de CDN.

El contenido no almacenado en caché entra directamente en los servidores origen del Adobe hasta que se vuelve a crear la caché. Debido a esto, Adobe planea manejar algunas transiciones de clientes a la vez para mantener un rendimiento aceptable al extraer solicitudes de nuestro origen.

## ¿Cómo puede verificar si una dirección URL o un sitio web está activado con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Debe descargar una externalización para utilizarla con el explorador Web. Para Firefox y Chrome hay una extensión denominada **[!UICONTROL HTTP/2 e Indicador SPDY.]** Los navegadores solo admiten HTTP/2 de forma segura, por lo que es necesario llamar a una URL con HTTPS para verificarla. Si se admite HTTP/2, esto se indica con la extensión en forma de símbolo de Flash azul y con el encabezado &quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.
