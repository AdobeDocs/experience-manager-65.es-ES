---
title: 'Exportar a CSV  '
seo-title: 'Exportar a CSV  '
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
source-git-commit: 317093bce043ff2aaa5b5ceb8499f057fa9fa24b
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 86%

---


# Exportar a CSV  {#export-to-csv}

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

![etc-01](assets/etc-01.png)

La opción Crear **informe CSV** está disponible al explorar la consola **Sitios** (en vista de Lista): es una opción del menú desplegable **Crear**:

![etc-02](assets/etc-02.png)

Para crear una exportación de CSV: 

1. Abra la consola **Sitios** y vaya hasta la ubicación deseada.
1. Para abrir el asistente, en la barra de herramientas seleccione **Crear** y, a continuación, **Informe de CSV**:

   ![etc-03](assets/etc-03.png)

1. Seleccione las propiedades oportunas para la exportación.
1. Seleccione **Crear**.
