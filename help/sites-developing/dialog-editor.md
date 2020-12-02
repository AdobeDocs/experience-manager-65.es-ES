---
title: Editor de cuadros de diálogo
seo-title: Editor de cuadros de diálogo
description: El editor de cuadro de diálogo proporciona una interfaz gráfica para crear y editar fácilmente cuadros de diálogo y andamios
seo-description: El editor de cuadro de diálogo proporciona una interfaz gráfica para crear y editar fácilmente cuadros de diálogo y andamios
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# Editor de cuadros de diálogo{#dialog-editor}

El editor de cuadro de diálogo proporciona una interfaz gráfica para crear y editar fácilmente cuadros de diálogo y andamios.

Para ver cómo funciona, vaya al CRXDE Lite, abra el árbol del explorador en `/libs/foundation/components/chart` y haga clic en el doble en el nodo `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

El nodo de cuadro de diálogo se abrirá en el **editor de cuadro de diálogo**:

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## Información general de la interfaz de usuario {#user-interface-overview}

La interfaz del editor de cuadro de diálogo se compone de cuatro paneles:

* La **paleta**, en la esquina superior izquierda. Este panel contiene los widgets disponibles para crear un cuadro de diálogo, como paneles de fichas, campos de texto, listas de selección y botones. Puede expandir las diferentes categorías dentro de la paleta haciendo clic en la barra divisoria deseada.
* El panel **estructura**, en la esquina inferior izquierda. Este panel muestra la estructura jerárquica de los nodos que conforma la definición del cuadro de diálogo. Puede ver la misma estructura expandiendo el nodo de cuadro de diálogo en CRXDE Lite o en el Explorador de contenido de CRX.
* Panel **procesar**, en el centro de la ventana. Este panel muestra cómo la definición de cuadro de diálogo definida en el panel de estructura se procesará como un cuadro de diálogo real.
* El panel **propiedades**. Este panel muestra las propiedades del nodo que está resaltado en el panel de estructura.

### Uso del Editor de cuadros de diálogo {#using-the-dialog-editor}

Para crear un cuadro de diálogo, el usuario arrastra y coloca los elementos de la paleta en el panel de estructura en su posición dentro de la jerarquía de definición del cuadro de diálogo.

Una vez completada la estructura deseada, el usuario hace clic en **Guardar**, en la parte superior del panel de procesamiento.

>[!CAUTION]
>
>Tenga en cuenta que el editor de cuadro de diálogo está diseñado para la creación de diálogos relativamente simples y es posible que no pueda editar definiciones de cuadro de diálogo más complejas. En los casos en los que el editor de cuadro de diálogo no permita la edición de una estructura de cuadro de diálogo, la definición de cuadro de diálogo debe crearse y/o editarse manualmente editando directamente la estructura de nodos utilizando, por ejemplo, CRXDE Lite o CRX Content Explorer.

### Creación de un nuevo cuadro de diálogo {#creating-a-new-dialog}

Para crear un nuevo cuadro de diálogo debe seleccionar el componente requerido, haga clic en **Crear...** y luego **Crear cuadro de diálogo...**.

Introduzca los detalles requeridos y haga clic en **Guardar todo** - ahora puede hacer clic con el doble en el cuadro de diálogo para abrirlo con el editor.

### Uso del Editor de cuadros de diálogo para scaffolds {#using-the-dialog-editor-for-scaffolds}

Un scaffold es una página especial que contiene un formulario que se puede rellenar y enviar en un solo paso. Esto le permite crear rápidamente una página con el contenido introducido.

El formulario que forma un scaffold se define mediante una definición de cuadro de diálogo, al igual que un cuadro de diálogo normal, aunque aparece en la página de scaffolding de forma diferente. Dado que las definiciones de cuadro de diálogo se utilizan para definir scaffolds, los scaffolds se pueden diseñar con el editor de cuadro de diálogo. Tenga en cuenta que, al utilizar el editor de cuadro de diálogo de este modo, el panel de procesamiento seguirá mostrando la definición del cuadro de diálogo en forma de cuadro de diálogo y no como scaffold.

Consulte [Andamiaje](/help/sites-authoring/scaffolding.md) para obtener más información sobre cómo utilizar el editor de cuadro de diálogo para crear scaffolds.
