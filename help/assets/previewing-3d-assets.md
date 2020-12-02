---
title: Vista previa de recursos 3D
description: Aprenda a previsualización de recursos 3D
contentOwner: Rick Brough
docset: aem65
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 15%

---


# Vista previa de recursos 3D en AEM{#previewing-3d-assets-aem}

Adobe Experience Manager admite la carga, el envío y la previsualización interactiva de recursos 3D como parte del proceso de creación.

El visor interactivo 3D está disponible en la página de información de recursos de AEM. El visor incluye, entre otras cosas, una colección de controles de cámara interactivos que le permiten girar, ampliar o reducir y panoramizar el recurso 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Formatos admitidos para la previsualización 3D en AEM {#supported-3d-previewing-assets}

La previsualización 3D interactiva admite los siguientes formatos de archivo:

| Extensión de archivo 3D | Formato de archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria de GL | model/gltf-binary |  |
| GLTF | Formato de transmisión de GL | modelo/gltf+json | Consulte **Nota** a continuación. |
| OBJ | Archivo de objeto WaveFront 3D | application/x-tgif |  |
| STL | Esteroolitografía | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | Apoyo a la ingestión únicamente; previsualización no disponible. |
| USDZ | Archivo zip de descripción de escena universal | model/vnd.usdz+zip | Apoyo a la ingestión únicamente; previsualización no disponible. |

**Nota**: Si los materiales no se representan en previsualización de un modelo gLTF, asegúrese de que su nombre sea correcto y se encuentren en una  `textures` carpeta de la misma carpeta raíz que el modelo, de forma similar a la siguiente:

    Recurso (carpeta)
    modelo.
    gltfmodel.
    bintextures (carpeta)
    material_0_baseColor.
    jpegmaterial_0_normal.jpeg

## Consideraciones de rendimiento al previsualización de recursos 3D en AEM{#performance-3d-previewing-assets}

El tiempo que tarda en abrir un recurso 3D en la página de vista de detalles del recurso depende de varios factores, como el ancho de banda, la complejidad de la imagen y las latencias del servidor.

Además, las capacidades del ordenador cliente, como una estación de trabajo, un portátil o un dispositivo táctil móvil, también son importantes para tener en cuenta al manipular la cámara de forma interactiva. Un sistema razonablemente potente con buenas capacidades gráficas puede hacer que la experiencia de visualización interactiva en 3D sea más cómoda y agradable.

**Previsualización de recursos 3D en AEM**

1. Asegúrese de que ha cargado los recursos 3D en AEM.
Consulte [Formatos admitidos para previsualización 3D](#supported-3d-previewing-assets) y [Carga de recursos](/help/assets/manage-assets.md#uploading-assets).
1. Desde AEM, en la página **[!UICONTROL Navegación]**, toque **[!UICONTROL Recursos > Archivos.]**

   ![Página de navegación](/help/assets/assets-dm/navigation-assets.png)

1. Cerca de la esquina superior derecha de la página, en la lista desplegable Ver, pulse **[!UICONTROL Vista de tarjeta]** y, a continuación, desplácese hasta un recurso 3D que quiera previsualizar.

   ![Selección de tarjeta 3D](/help/assets/assets-dm/3d-card-select.png)
   _En Vista de tarjetas, toque la tarjeta del recurso 3D que desea previsualización._

1. Toque la tarjeta del recurso 3D para abrirla en la página de vista de detalles del recurso.

   ![Previsualización 3D interactiva](/help/assets/assets-dm/3d-preview.png)
   _Previsualización interactiva de un recurso 3D en la página de vista de detalles del recurso._
1. En la página de vista de detalles de recursos para el recurso 3D, realice una de las siguientes acciones:
   * **Gire la cámara**: ordene la vista alrededor de la escena y los objetos 3D.
      * _Ratón_: Haga clic y arrastre.
      * _Pantalla_ táctil: Presione con un solo dedo y arrastre.
   * **Recorra la cámara**: desplace la vista hacia la izquierda, hacia la derecha, hacia arriba o hacia abajo.
      * _Ratón_: Haga clic con el botón derecho y arrastre.
      * _Pantalla_ táctil: Presione dos dedos y arrastre.
   * **Zoom en la cámara**: haga zoom en la cámara para entrar y salir de áreas de la escena 3D.
      * _Ratón_: Rueda de desplazamiento.
      * _Pantalla_ táctil: Pellizque con dos dedos.
   * **Volver a introducir la cámara**: vuelva a introducir la cámara en un punto de la escena 3D.
      * _Ratón_: Haga clic con el doble.
      * _Pantalla_ táctil: Toque el doble.
   * **Restaurar**: cerca de la esquina inferior derecha de la página, toque el icono Restablecer para restaurar el punto de destinatario de vista al centro del recurso 3D. El reinicio también hace que la cámara se acerque o se aleje para mostrar el recurso en su totalidad y con un tamaño de visualización razonable.
   * **Modo** de pantalla completa: para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, toque el icono de pantalla completa.

1. Cuando haya terminado, toque **[!UICONTROL Cerrar cerca de la esquina superior derecha de la página.]**
