---
title: Exportar a CSV
seo-title: Export to CSV
description: Exportar información sobre sus páginas a un archivo CSV en su sistema local
seo-description: Export information about your pages to a CSV file on your local system
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 75%

---

# Exportar a CSV  {#export-to-csv}

**Al crear un informe de CSV** puede exportar información sobre las páginas a un archivo CSV en el sistema local.

* El archivo descargado se llama `export.csv`.
* El contenido depende de las propiedades que seleccione.
* Puede definir la ruta de la exportación, así como la profundidad.

>[!NOTE]
>
>Se utiliza la función de descarga (y el destino predeterminado) de su navegador.

El **Crear exportación de CSV** El asistente le permite seleccionar:

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
   * Ruta principal
   * Solo elementos secundarios directos
   * Niveles adicionales de tareas secundarias
   * Niveles

El archivo `export.csv` resultante se puede abrir en Excel o en cualquier otra aplicación compatible.

![etc-01](assets/etc-01.png)

La creación de **Informe CSV** La opción está disponible al navegar por la **Sites** consola (en la vista de lista): es una opción del **Crear** menú desplegable:

![etc-02](assets/etc-02.png)

Para crear una exportación de CSV: 

1. Abra el **Sites** consola de, vaya a la ubicación requerida si es necesario.
1. Para abrir el asistente, en la barra de herramientas seleccione **Crear** y, a continuación, **Informe de CSV**:

   ![etc-03](assets/etc-03.png)

1. Seleccione las propiedades necesarias para exportar.
1. Seleccione **Crear**.
