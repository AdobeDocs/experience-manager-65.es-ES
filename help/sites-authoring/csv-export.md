---
title: Exportar a CSV
description: Exportar información sobre sus páginas a un archivo CSV en su sistema local
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 74%

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
