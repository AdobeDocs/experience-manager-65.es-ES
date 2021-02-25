---
title: Activación de la protección de vínculos interactivos en Dynamic Media
description: Información sobre cómo activar la protección de vínculos interactivos en Dynamic Media.
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
translation-type: tm+mt
source-git-commit: 787f3b4cf5835b7e9b03e3f4e6f6597084adec8c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Activación de la protección de vínculos interactivos en Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

La vinculación interactiva se produce cuando un sitio web de terceros utiliza código HTML para mostrar una imagen del sitio web. Utilizan el ancho de banda cada vez que se solicita la imagen, ya que el navegador del visitante accede a ella directamente desde el servidor. Hotlink *protection* es un método para evitar que otros sitios Web se vinculen directamente a imágenes, css o JavaScript en sus páginas Web. Este tipo de escudo ayuda a reducir el uso innecesario del ancho de banda en su cuenta de Dynamic Media.

[Adobe ](https://helpx.adobe.com/support.html) Support puede configurar un filtro de remitente del reenvío en el nivel CDN (Red de Envío de contenido) para que el contenido de Dynamic Media solo se muestre en los sitios web de la lista de sitios web permitidos para el dominio.

>[!NOTE]
>
>Esta función requiere que utilice el CDN incorporado con Adobe Experience Manager Dynamic Media. Esta función no admite ningún otro CDN personalizado. Para activar la protección de vínculos interactivos, un administrador debe crear un ticket de asistencia técnica del Servicio de atención al cliente de Adobe para solicitar el cambio de configuración en su cuenta de Dynamic Media. No hay costo adicional para activar la protección de los vínculos interactivos.
