---
title: Agregar fuentes para la representación gráfica
description: AEM La permite generar gráficos que incorporen texto tomado dinámicamente del contenido
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Agregar fuentes para la representación gráfica{#adding-fonts-for-graphic-rendering}

AEM La opción permite generar gráficos que incorporen texto tomado dinámicamente del contenido.

Para ello, también puede cargar y utilizar sus propias fuentes.

Actualmente todas las implementaciones de la plataforma Java admiten [TrueType](https://en.wikipedia.org/wiki/Truetype) fuentes.

1. Abra el CRXDE Lite y vaya a la carpeta de la aplicación del proyecto:

   `/apps/<your-project>/`

1. En `/apps/<your-project>/`, cree un nodo:

   * **Nombre**: `fonts`
   * **Tipo**: `sling:Folder`

   Guarde todos los cambios.

1. Copie los archivos de fuente en esta carpeta; por ejemplo, mediante WebDAV.

   >[!NOTE]
   >
   >Los archivos de fuente del repositorio deben tener el sufijo `*.ttf` o `*.TTF`.

1. Actualice la [configuración de OSGi](/help/sites-deploying/configuring-osgi.md) de [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). Agregue la ruta a la carpeta de fuentes; es decir, `/apps/<your-project>/fonts`.

1. Volver a CRXDE Lite. Ahora debería ver un nodo `.fontlist` en la carpeta que contiene el nombre de las fuentes importadas.

   Estas fuentes ya están listas para utilizarse en la API de Java.

Para obtener información detallada sobre cómo usar las fuentes con la API de Java, consulte la [documentación de la clase Font de la API de Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
