---
title: Envío de recursos de Dynamic Media
description: Obtenga información sobre cómo distribuir recursos de Dynamic Media
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
role: Profesional empresarial, administrador
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 9%

---


# Envío de recursos de Dynamic Media{#delivering-dynamic-media-assets}

El modo de distribuir los recursos de Dynamic Media (vídeos e imágenes) depende de cómo se implemente el sitio web.

Con Dynamic Media dispone de varias opciones:

* Si el sitio web está alojado en AEM, quiere agregar los recursos de Dynamic Media directamente a la página.
* Si el sitio web no está AEM, puede elegir una de las opciones siguientes:

   * Incrustar el vídeo o la imagen en el sitio web.
   * Vincule las URL a la aplicación web. Utilice la vinculación cuando desee enviar un reproductor de vídeo como ventana emergente o modal.
   * Si el sitio es interactivo, puede [entregar imágenes optimizadas.](/help/assets/responsive-site.md)

>[!NOTE]
>
>Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del explorador. Consulte [Imágenes inteligentes](/help/assets/imaging-faq.md) para obtener más información.

Para obtener más información, consulte los temas siguientes:

* [Adición de recursos de Dynamic Media a páginas web](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Incrustación del visualizador de imágenes o vídeos en una página web](/help/assets/embed-code.md)
* [Activar la protección de los vínculos interactivos de Dynamic Media](hotlink-protection.md)
* [Vinculación de URL a la aplicación web](/help/assets/linking-urls-to-yourwebapplication.md)
* [Entrega de imágenes optimizadas para un sitio interactivo](/help/assets/responsive-site.md)
* [Entrega HTTP2 de contenido](/help/assets/http2.md)
* [Invalidación de la caché de CDN mediante Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [Uso de conjuntos de reglas para transformar direcciones URL](/help/assets/using-rulesets-to-transform-urls.md)


## Entrega HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ahora admite la entrega de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, una URL publicada o un código incrustado para la imagen o el vídeo están disponibles para integrarse con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega mediante el protocolo HTTP/2. Este método de envío mejora la forma en que se comunican los exploradores y los servidores, lo que permite mejorar los tiempos de respuesta y carga de todos los recursos de Dynamic Media.

Consulte [HTTP/2 Entrega de contenido preguntas más frecuentes](/help/sites-administering/scene7-http2faq.md) para obtener más información.
