---
title: Adición de fuentes para la renderización gráfica
seo-title: Adding Fonts for Graphic-Rendering
description: AEM le permite generar gráficos que incorporen texto tomado dinámicamente del contenido
seo-description: AEM allows you to generate graphics incorporating text dynamically taken from your content
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---

# Adición de fuentes para la renderización gráfica{#adding-fonts-for-graphic-rendering}

AEM permite generar gráficos que incorporen texto de forma dinámica tomado del contenido.

Para ello, también puede cargar y utilizar sus propias fuentes.

Actualmente, todas las implementaciones de la plataforma Java son compatibles [TrueType](https://en.wikipedia.org/wiki/Truetype) fuentes.

1. Abra el CRXDE Lite y vaya a la carpeta de la aplicación del proyecto:

   `/apps/<your-project>/`

1. En `/apps/<your-project>/` cree un nuevo nodo:

   * **Nombre**: `fonts`
   * **Tipo**: `sling:Folder`

   Guarde todos los cambios.

1. Copie los archivos de fuente en esta carpeta; por ejemplo, usando WebDAV.

   >[!NOTE]
   >
   >Los archivos de fuente del repositorio deben tener el sufijo `*.ttf` o `*.TTF`.

1. Actualice el [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) de [Ayudante de fuentes GFX de Day Commons](/help/sites-deploying/osgi-configuration-settings.md). Añada la ruta a la carpeta de fuentes; es decir, `/apps/<your-project>/fonts`.

1. Vuelva al CRXDE Lite. Ahora debería ver un `.fontlist` en la carpeta que contiene el nombre de las fuentes importadas.

   Estas fuentes ya están listas para utilizarse en la API de Java.

Para obtener más información sobre cómo utilizar las fuentes con la API de Java, consulte la [documentación para la clase Font de la API Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
