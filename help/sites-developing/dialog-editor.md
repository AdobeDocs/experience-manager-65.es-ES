---
title: Editor de diálogos
seo-title: Dialog Editor
description: El editor de diálogos proporciona una interfaz gráfica para crear y editar fácilmente cuadros de diálogo y andamios
seo-description: The dialog editor provides a graphical interface for easily creating and editing dialog boxes and scaffolds
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Editor de diálogos{#dialog-editor}

El editor de diálogos proporciona una interfaz gráfica para crear y editar fácilmente cuadros de diálogo y andamios.

Para ver cómo funciona, vaya a CRXDE Lite y abra el árbol del explorador para `/libs/foundation/components/chart` y haga doble clic en el nodo `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

El nodo de diálogo se abrirá en **editor de diálogos**:

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## Resumen de interfaz de usuario {#user-interface-overview}

La interfaz del editor de diálogos se compone de cuatro paneles:

* El **paleta**, en la esquina superior izquierda. Este panel contiene los widgets disponibles para crear un cuadro de diálogo, como paneles de pestañas, campos de texto, listas de selección y botones. Puede expandir las diferentes categorías dentro de la paleta haciendo clic en la barra divisoria deseada.
* El **estructura** panel, en la esquina inferior izquierda. Este panel muestra la estructura jerárquica de nodos que conforman la definición del cuadro de diálogo. Puede ver la misma estructura expandiendo el nodo de diálogo en CRXDE Lite o en Explorador de contenido CRX.
* El **render** panel, en el centro de la ventana. Este panel muestra cómo se representará la definición de cuadro de diálogo definida en el panel de estructura como un cuadro de diálogo real.
* El **propiedades** panel. Este panel muestra las propiedades del nodo resaltado actualmente en el panel de estructura.

### Uso del Editor de diálogos {#using-the-dialog-editor}

Para crear un cuadro de diálogo, el usuario arrastra y suelta los elementos desde la paleta hasta el panel de estructura y los coloca en su posición dentro de la jerarquía de definición del cuadro de diálogo.

Una vez completada la estructura deseada, el usuario hace clic en **Guardar**, en la parte superior del panel de procesamiento.

>[!CAUTION]
>
>Tenga en cuenta que el editor de diálogos está diseñado para la creación de diálogos relativamente simples y es posible que no pueda editar definiciones de diálogo más complejas. En los casos en los que el editor de diálogos no permite la edición de una estructura de diálogo, la definición del diálogo debe crearse o editarse manualmente editando directamente la estructura del nodo utilizando, por ejemplo, el CRXDE Lite o el Explorador de contenido CRX.

### Creación de un nuevo cuadro de diálogo {#creating-a-new-dialog}

Para crear un nuevo cuadro de diálogo, debe seleccionar el componente necesario y hacer clic en **Crear...** y luego **Crear diálogo...**.

Introduzca los detalles necesarios y haga clic en **Guardar todo** - ahora puede hacer doble clic en el diálogo para abrirlo con el editor.

### Uso del Editor de cuadros de diálogo para andamios {#using-the-dialog-editor-for-scaffolds}

Un andamio es una página especial que contiene un formulario que se puede rellenar y enviar en un solo paso. Esto le permite crear rápidamente una página utilizando el contenido introducido.

El formulario que constituye un andamio se define mediante una definición de cuadro de diálogo, como un cuadro de diálogo normal, aunque aparece en la página de andamiaje de un formulario diferente. Dado que las definiciones de cuadros de diálogo se utilizan para definir andamios, estos se pueden diseñar con el editor de cuadros de diálogo. Tenga en cuenta que cuando utilice el editor de diálogos de esta manera, el panel de procesamiento seguirá mostrando la definición del cuadro de diálogo en forma de cuadro de diálogo, no como un andamio.

Consulte [Andamiaje](/help/sites-authoring/scaffolding.md) para obtener más información sobre el uso del editor de diálogos para crear andamios.
