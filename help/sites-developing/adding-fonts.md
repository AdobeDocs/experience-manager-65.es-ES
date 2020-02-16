---
title: Adición de fuentes para la representación gráfica
seo-title: Adición de fuentes para la representación gráfica
description: AEM le permite generar gráficos que incorporan texto tomado dinámicamente de su contenido
seo-description: AEM le permite generar gráficos que incorporan texto tomado dinámicamente de su contenido
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Adición de fuentes para la representación gráfica{#adding-fonts-for-graphic-rendering}

AEM le permite generar gráficos que incorporan texto tomado dinámicamente de su contenido.

Para ello, también puede cargar y utilizar sus propias fuentes.

Actualmente, todas las implementaciones de la plataforma Java admiten fuentes [TrueType](https://en.wikipedia.org/wiki/Truetype) .

1. Abra CRXDE Lite y vaya a la carpeta de la aplicación del proyecto:

   `/apps/<your-project>/`

1. En `/apps/<your-project>/` Crear un nuevo nodo:

   * **Nombre**: `fonts`
   * **Tipo**: `sling:Folder`
   Guarde todos los cambios.

1. Copie los archivos de fuente en esta carpeta; por ejemplo, mediante WebDAV.

   >[!NOTE]
   >
   >Los archivos de fuente del repositorio deben tener el sufijo `*.ttf` o `*.TTF`.

1. Actualice la configuración [](/help/sites-deploying/configuring-osgi.md) OSGi de [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). Agregue la ruta a la carpeta de fuentes; es decir, `/apps/<your-project>/fonts`.

1. Vuelva a CRXDE Lite. Ahora debe ver un `.fontlist` nodo en la carpeta que contenga el nombre de las fuentes importadas.

   Estas fuentes ya están listas para usarse en la API de Java.

Para obtener información detallada sobre cómo utilizar las fuentes con la API de Java, consulte la [documentación de la clase Font de la API](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)de Java.

