---
title: Exportar a CSV
seo-title: Exportar a CSV
description: Permite exportar información sobre las páginas a un archivo CSV en el sistema local
seo-description: Permite exportar información sobre las páginas a un archivo CSV en el sistema local
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# Exportar a CSV{#export-to-csv}

**Al crear un informe de CSV** puede exportar información sobre las páginas a un archivo CSV en el sistema local.

* El archivo descargado se llama `export.csv`.
* El contenido depende de las propiedades que seleccione.
* Puede definir la ruta de la exportación, así como la profundidad.

>[!NOTE]
>
>Se utiliza la función de descarga (y el destino predeterminado) de su navegador.

El asistente para **crear exportaciones de CSV** permite seleccionar lo siguiente:

* Propiedades para exportar
   * Metadatos
      * Nombre
      * Modificado
      * Publicado
      * Plantilla
      * Flujo de trabajo
   * Traducción
      * Traducido
   * Análisis
      * Vistas de la página
      * Visitantes únicos
      * Tiempo empleado en la página
* Profundidad
   * Ruta de acceso principal
   * Solo elementos secundarios directos
   * Niveles adicionales de elementos secundarios
   * Niveles

El archivo `export.csv` resultante se puede abrir en Excel o en cualquier otra aplicación compatible.

![]() ![etc-01](assets/etc-01.png)

The create **CSV Report** option is available when browsing the **Sites** console (in List view): it is an option of the **Create** drop down menu:

![etc-02](assets/etc-02.png)

Para crear una exportación de CSV: 

1. Abra la consola **Sitios** y vaya hasta la ubicación deseada.
1. From the toolbar, select **Create** then **CSV Report** to open the wizard:

   ![etc-03](assets/etc-03.png)

1. Seleccione las propiedades oportunas para la exportación.
1. Seleccione **Crear**.
