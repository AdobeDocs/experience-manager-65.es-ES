---
title: Agregar fuentes para la representación gráfica
seo-title: Adding Fonts for Graphic-Rendering
description: AEM La permite generar gráficos que incorporen texto tomado dinámicamente del contenido
seo-description: AEM lets you generate graphics incorporating text dynamically taken from your content
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---

# Agregar fuentes para la representación gráfica{#adding-fonts-for-graphic-rendering}

AEM La opción permite generar gráficos que incorporen texto tomado dinámicamente del contenido.

Para ello, también puede cargar y utilizar sus propias fuentes.

Actualmente, todas las implementaciones de la plataforma Java son compatibles [TrueType](https://en.wikipedia.org/wiki/Truetype) fuentes.

1. Abra el CRXDE Lite y vaya a la carpeta de la aplicación del proyecto:

   `/apps/<your-project>/`

1. En `/apps/<your-project>/` cree un nuevo nodo:

   * **Nombre**: `fonts`
   * **Tipo**: `sling:Folder`

   Guarde todos los cambios.

1. Copie los archivos de fuente en esta carpeta; por ejemplo, mediante WebDAV.

   >[!NOTE]
   >
   >Los archivos de fuente del repositorio deben tener el sufijo `*.ttf` o `*.TTF`.

1. Actualice el [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) de [Ayuda de fuentes GFX de Day Commons](/help/sites-deploying/osgi-configuration-settings.md). Añada la ruta a la carpeta de fuentes; p. ej. `/apps/<your-project>/fonts`.

1. Volver a CRXDE Lite. Ahora debería ver una `.fontlist` nodo de la carpeta que contiene el nombre de las fuentes importadas.

   Estas fuentes ya están listas para utilizarse en la API de Java.

Para obtener más información sobre cómo utilizar las fuentes con la API de Java, consulte la [Documentación de la clase Font de la API de Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
