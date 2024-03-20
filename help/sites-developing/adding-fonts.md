---
title: Agregar fuentes para la representación gráfica
description: AEM La permite generar gráficos que incorporen texto tomado dinámicamente del contenido
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Agregar fuentes para la representación gráfica{#adding-fonts-for-graphic-rendering}

AEM La opción permite generar gráficos que incorporen texto tomado dinámicamente del contenido.

Para ello, también puede cargar y utilizar sus propias fuentes.

Actualmente, todas las implementaciones de la plataforma Java son compatibles [TrueType](https://en.wikipedia.org/wiki/Truetype) fuentes.

1. Abra el CRXDE Lite y vaya a la carpeta de la aplicación del proyecto:

   `/apps/<your-project>/`

1. En `/apps/<your-project>/` cree un nodo:

   * **Nombre**: `fonts`
   * **Tipo**: `sling:Folder`

   Guarde todos los cambios.

1. Copie los archivos de fuente en esta carpeta; por ejemplo, mediante WebDAV.

   >[!NOTE]
   >
   >Los archivos de fuente del repositorio deben tener el sufijo `*.ttf` o `*.TTF`.

1. Actualice el [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) de [Ayuda de fuentes GFX de Day Commons](/help/sites-deploying/osgi-configuration-settings.md). Añada la ruta a la carpeta de fuentes; es decir, `/apps/<your-project>/fonts`.

1. Volver a CRXDE Lite. Ahora debería ver una `.fontlist` nodo de la carpeta que contiene el nombre de las fuentes importadas.

   Estas fuentes ya están listas para utilizarse en la API de Java.

Para obtener más información sobre cómo utilizar las fuentes con la API de Java, consulte la [Documentación de la clase Font de la API de Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
