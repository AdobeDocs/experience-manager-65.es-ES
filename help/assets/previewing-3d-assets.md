---
title: Vista previa de recursos 3D
description: Obtenga información sobre cómo previsualizar recursos 3D
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 16%

---


# Vista previa de recursos 3D en AEM{#previewing-3d-assets-aem}

Adobe Experience Manager admite la carga, entrega y previsualización interactiva de recursos 3D como parte del proceso de creación.

El visor interactivo 3D está disponible en la página de información de recursos de AEM. El visor incluye, entre otras cosas, una colección de controles de cámara interactivos que le permiten girar, ampliar o reducir y panoramizar el recurso 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Formatos compatibles con la vista previa 3D en AEM {#supported-3d-previewing-assets}

La vista previa 3D interactiva admite los siguientes formatos de archivo:

| Extensión de archivo 3D | Formato del archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria de GL | model/gltf-binary |  |
| GLTF | Formato de Transmisión GL | modelo/gltf+json | Consulte **Nota** a continuación. |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Esteroolitografía | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | Compatibilidad únicamente con la ingesta; vista previa no disponible. |
| USDZ | Archivo zip de descripción de escena universal | model/vnd.usdz+zip | Compatibilidad únicamente con la ingesta; vista previa no disponible. |

**Nota**: Si los materiales no se representan en la vista previa de un modelo gLTF, asegúrese de que tengan el nombre adecuado y se encuentren en una  `textures` carpeta de la misma carpeta raíz que el modelo, similar a lo siguiente:

    Recurso (carpeta)
    modelo.
    gltfmodel.
    bintextures (carpeta)
    material_0_baseColor.
    jpegmaterial_0_normal.jpeg

## Consideraciones de rendimiento al previsualizar recursos 3D en AEM{#performance-3d-previewing-assets}

El tiempo que se tarda en abrir un recurso 3D en la página de vista de detalles del recurso depende de varios factores, como el ancho de banda, la complejidad de la imagen y las latencias del servidor.

Además, las capacidades del equipo cliente (como una estación de trabajo, un portátil o un dispositivo táctil móvil) también son importantes de tener en cuenta al manipular la cámara de forma interactiva. Un sistema razonablemente potente con buenas capacidades gráficas puede hacer que la experiencia de visualización interactiva en 3D sea más cómoda y agradable.

**Para previsualizar recursos 3D en AEM**

1. Asegúrese de que ha cargado los recursos 3D en AEM.
Consulte [Formatos admitidos para la vista previa 3D](#supported-3d-previewing-assets) y [Carga de recursos](/help/assets/manage-assets.md#uploading-assets).
1. Desde AEM, en la página **[!UICONTROL Navegación]**, pulse **[!UICONTROL Assets > Archivos.]**

   ![Página de navegación](/help/assets/assets-dm/navigation-assets.png)

1. Cerca de la esquina superior derecha de la página, en la lista desplegable Ver, pulse **[!UICONTROL Vista de tarjeta]** y, a continuación, desplácese hasta un recurso 3D que quiera previsualizar.

   ![Selección de tarjeta 3D](/help/assets/assets-dm/3d-card-select.png)
   _En Vista de tarjeta, pulse la tarjeta del recurso 3D que desea previsualizar._

1. Pulse la tarjeta del recurso 3D para abrirlo en la página de vista de detalles del recurso.

   ![Vista previa interactiva en 3D](/help/assets/assets-dm/3d-preview.png)
   _Vista previa interactiva de un recurso 3D en la página de vista de detalles del recurso._
1. En la página de vista de detalles del recurso para el recurso 3D, realice una de las acciones siguientes:
   * **Girar la cámara**: permite girar la vista alrededor de la escena y los objetos 3D.
      * _Mouse_: Haga clic y arrastre con el botón izquierdo.
      * _Pantalla_ táctil: Presione con un solo dedo y arrastre.
   * **Panorre la cámara**: desplace la vista hacia la izquierda, hacia la derecha, hacia arriba o hacia abajo.
      * _Mouse_: Haga clic con el botón derecho y arrastre.
      * _Pantalla_ táctil: Presione con dos dedos y arrastre.
   * **Zoom de la cámara**: permite hacer zoom en la cámara para que se mueva dentro y fuera de las áreas de la escena 3D.
      * _Mouse_: Rueda de desplazamiento.
      * _Pantalla_ táctil: Pellizque con dos dedos.
   * **Vuelva a introducir la cámara**: vuelva a introducir la cámara en un punto de un objeto de la escena 3D.
      * _Mouse_: Haga doble clic en .
      * _Pantalla_ táctil: Toque dos veces.
   * **Restablecer**: cerca de la esquina inferior derecha de la página, pulse el icono Restablecer para restaurar el punto de destino de la vista al centro del recurso 3D. Restablecer también mueve la cámara más cerca o más lejos para mostrar el recurso en su totalidad y con un tamaño de visualización razonable.
   * **Modo** de pantalla completa (Full screen mode): para entrar al modo de pantalla completa, en la esquina inferior derecha de la página, pulse el icono de pantalla completa (Fullscreen).

1. Cuando haya terminado, pulse **[!UICONTROL Cerrar.]** cerca de la esquina superior derecha de la página
