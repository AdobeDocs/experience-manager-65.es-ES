---
title: Vista previa de activos 3D
description: Obtenga información sobre cómo previsualizar recursos 3D en Experience Manager.
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: User
exl-id: fdebbc2b-c04d-4cdd-b7c2-8e9a2a854e79
source-git-commit: aa45839c53cb2c0715c9163847351aa2391309e0
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 12%

---

# Vista previa de recursos 3D en Adobe Experience Manager {#previewing-3d-assets-aem}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/previewing-3d-assets.html?lang=en) |
| AEM 6.5 | Este artículo |

Experience Manager admite la carga, entrega y previsualización interactiva de recursos 3D como parte del proceso de creación.

El visor 3D interactivo está disponible en la página de detalles de recursos de Experience Manager. El visor incluye, entre otras cosas, una colección de controles de cámara interactivos que le permiten girar, ampliar o reducir y panoramizar el recurso 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Formatos admitidos para la vista previa 3D en el Experience Manager {#supported-3d-previewing-assets}

La vista previa 3D interactiva admite los siguientes formatos de archivo:

| Extensión de archivo 3D | Formato del archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria de GL | model/gltf-binary |  |
| GLTF | Formato de Transmisión GL | modelo/gltf+json | Consulte **Nota** más abajo. |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Esteroolitografía | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | Compatibilidad únicamente con la ingesta; vista previa no disponible. |
| USDZ | Archivo zip de descripción de escena universal | model/vnd.usdz+zip | Compatibilidad únicamente con la ingesta; vista previa no disponible. |

>[!NOTE]
>
>Si los materiales no se renderizan en la previsualización de un modelo gLTF, asegúrese de que tengan el nombre adecuado y en un `textures` en la misma carpeta raíz que el modelo, similar a lo siguiente:

    Recurso (carpeta)
    model.gltf
    model.bin
    texturas (carpeta)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Consideraciones de rendimiento al previsualizar recursos 3D en Experience Manager{#performance-3d-previewing-assets}

El tiempo que se tarda en abrir un recurso 3D en la página de vista de detalles del recurso depende de varios factores, como el ancho de banda, la complejidad de la imagen y las latencias del servidor.

Además, las capacidades del equipo cliente, como una estación de trabajo, un ordenador portátil o un dispositivo táctil móvil, también son importantes de tener en cuenta al manipular la cámara de forma interactiva. Un sistema razonablemente potente con buenas capacidades gráficas puede hacer que la experiencia de visualización interactiva en 3D sea más cómoda y agradable.

**Para previsualizar recursos 3D en el Experience Manager:**

1. Asegúrese de haber cargado recursos 3D en Experience Manager.
Consulte [Formatos compatibles con la vista previa 3D](#supported-3d-previewing-assets) y [Cargar recursos](/help/assets/manage-assets.md#uploading-assets).
1. Desde el Experience Manager, en el **[!UICONTROL Navegación]** página, seleccione **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]**.

   ![Página de navegación](/help/assets/assets-dm/navigation-assets.png)

1. Cerca de la esquina superior derecha de la página, en la lista desplegable Ver, seleccione **[!UICONTROL Vista de tarjeta]** y, a continuación, navegue hasta un recurso 3D cuya vista previa desee ver.

   ![Selección de tarjeta 3D](/help/assets/assets-dm/3d-card-select.png)
   _En Vista de tarjeta, seleccione la tarjeta del recurso 3D que desea previsualizar._

1. Seleccione la tarjeta del recurso 3D.

   ![Vista previa interactiva en 3D](/help/assets/assets-dm/3d-preview.png)
   _Vista previa interactiva de un recurso 3D en la página de vista de detalles del recurso._
1. En la página de vista de detalles del recurso para el recurso 3D, realice una de las acciones siguientes:

   | Ver | Descripción | Acción del ratón | Acción de pantalla táctil |
   | --- | --- | --- | --- |
   | **Gire la cámara** | Haga girar la vista alrededor de la escena 3D y de los objetos. | Haga clic y arrastre con el botón izquierdo. | Presione con un solo dedo y arrastre. |
   | **Panorámica de la cámara** | Desplace la vista hacia la izquierda, hacia la derecha, hacia arriba o hacia abajo. | Haga clic con el botón derecho y arrastre. | Presione con dos dedos y arrastre. |
   | **Ampliar la cámara** | Entrada y salida de áreas en la escena 3D. | Rueda de desplazamiento. | Pellizque con dos dedos. |
   | **Vuelva a introducir la cámara** | Vuelva a introducir la cámara en un punto de un objeto de la escena 3D. | Hacer doble clic. | Toque dos veces. |
   | **Restablecer** | Cerca de la esquina inferior derecha de la página, seleccione el icono Restablecer para restaurar el punto de destino de la vista al centro del recurso 3D. Restablecer también mueve la cámara más cerca o más lejos para mostrar el recurso en su totalidad y con un tamaño de visualización razonable. |  |  |
   | **Modo de pantalla completa** | Para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, seleccione el icono Pantalla completa . |  |  |

1. Cuando haya terminado, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Cerrar]**.
