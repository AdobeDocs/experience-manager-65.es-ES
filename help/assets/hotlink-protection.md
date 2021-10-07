---
title: Activación de la protección de vínculos interactivos en Dynamic Media
description: Información sobre cómo activar la protección de vínculos interactivos en Dynamic Media.
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Activar la protección de los vínculos interactivos en Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

La vinculación activa se produce cuando un sitio web de terceros utiliza código de HTML para mostrar una imagen del sitio web. Utilizan su ancho de banda cada vez que se solicita la imagen porque el navegador del visitante está accediendo directamente desde su servidor. Hotlink *protection* es un método para evitar que otros sitios web se vinculen directamente a imágenes, CSS o JavaScript en sus páginas web. Este tipo de escudo ayuda a reducir el uso innecesario del ancho de banda en su cuenta de Dynamic Media.

[El servicio de ](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) asistencia al cliente de Experience Manager puede configurar un filtro de referente en el nivel CDN (red de entrega de contenido) para que el contenido de Dynamic Media solo se proporcione a los sitios web de la lista de sitios web permitidos para el dominio.

>[!NOTE]
>
>Esta función requiere que utilice la CDN predeterminada incluida con Adobe Experience Manager Dynamic Media. Esta función no admite ninguna otra CDN personalizada. Para activar la protección de vínculos interactivos, un administrador debe crear un ticket de asistencia al cliente de Adobe para solicitar el cambio de configuración en su cuenta de Dynamic Media. No existe ningún coste adicional para activar la protección de los vínculos interactivos.
