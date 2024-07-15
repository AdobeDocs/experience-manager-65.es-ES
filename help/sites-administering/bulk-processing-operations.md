---
title: Operaciones de procesamiento masivo
description: Nulo
page-status-flag: never-activated
contentOwner: sarchiz
docset: aem65
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 1%

---


# Operaciones de procesamiento masivo {#bulk-processing-operations}

## Introducción {#introduction}

Con la versión más reciente de Adobe Experience Manager AEM (), el botón Seleccionar todo se ha ampliado a todas las vistas: Lista, Columna y Vista de tarjeta. El botón Seleccionar todo ahora selecciona todo el contenido de una carpeta o colección determinada, y no solo el Assets y las páginas cargadas y visibles en el explorador del cliente.

Se han habilitado las acciones clave para la operación masiva: **Mover**, **Eliminar** y **Copiar**. Un nuevo cuadro de diálogo permite a los clientes saber cuáles son las acciones para las que no está disponible el procesamiento masivo.

## Cómo Usar {#how-to-use}

Se ha agregado un nuevo botón llamado **Seleccionar todo** a las vistas Tarjeta, Lista o Columna. Este botón se puede utilizar en cualquiera de las vistas para seleccionar todos los elementos del conjunto de datos.

AEM En las versiones anteriores de la aplicación, la selección estaba limitada a lo que se cargaba en el explorador del cliente. Este nuevo cambio se introdujo para evitar confusiones con respecto al número de elementos en los que se realiza una operación masiva.

Por ahora, se han añadido tres operaciones al procesamiento masivo:

* Mover
* Copiar
* Eliminar

En el futuro se agregará compatibilidad con más operaciones.
Para utilizar esta función, vaya a la carpeta o colección donde desee realizar una operación masiva en Páginas o en Assets.

A continuación, elija una de las vistas, como se muestra a continuación:

### Vista de tarjeta {#card-view}

![Vista de tarjeta que muestra imágenes en miniatura de diversos recursos de imagen.](assets/unu.png)

### Selección masiva en la vista de tarjeta {#bulk-selection-in-card-view}

Assets o Páginas se pueden seleccionar en lotes usando el botón **Seleccionar todo** de la parte superior derecha:

![Botón Seleccionar todo que se muestra en la esquina superior derecha de la vista de tarjeta.](assets/doi.png) ![Todas las imágenes en miniatura de los recursos de imagen en la vista de tarjeta se muestran como seleccionadas con marcas de verificación.](assets/trei.png)

### Vista de lista    {#list-view}

Lo mismo ocurre con la vista de lista:

![La opción Seleccionar todo de la esquina superior derecha de la vista de lista está resaltada.](assets/patru_modified.png)

### Selección masiva en la vista de lista {#bulk-selection-in-list-view}

En la vista de lista, use el botón **Seleccionar todo** o use la casilla de verificación de la izquierda para realizar una selección masiva.

![La vista en vivo que muestra miniaturas de imágenes de recursos de imagen se muestra en filas horizontales.](assets/cinci.png) ![Cuadro de lista que muestra miniaturas de imágenes de recursos de imagen y una casilla de verificación a la izquierda de Name.](assets/sase.png)

### Vista de columna {#column-view}

![Vista de columna que muestra imágenes en miniatura de recursos de imágenes mostrados en columnas verticales.](assets/sapte.png)

### Selección masiva en la vista de columna {#bulk-selection-in-column-view}

![Todas las imágenes en miniatura de los recursos de imagen en la vista de columna se muestran como seleccionadas con marcas de verificación.](assets/opt.png)

## Operaciones habilitadas por lotes {#bulk-enabled-operations}

Después de la selección, se puede realizar una de las tres acciones habilitadas por lotes: **Mover**, **Copiar** o **Eliminar**.

En este caso, la operación **Mover** se realiza en el Assets seleccionado anteriormente. En cualquiera de las vistas, esto hace que todos los Assets se muevan a la ubicación elegida y no solo a las que se cargan en la pantalla.

![Mover recursos que muestran una carpeta seleccionada en la vista de columna.](assets/noua.png)

Para otras operaciones que no están habilitadas por lotes, como **Descargar,**, se muestra una advertencia que indica que solo se incluyen en la operación los elementos cargados en el explorador.

![Vista de Assets que muestra los recursos de imagen seleccionados y el cuadro de diálogo emergente &quot;No se admite la acción en masa&quot;.](assets/zece.png)
