---
title: Operaciones de procesamiento masivo
seo-title: Bulk Processing Operations
description: nulo
seo-description: null
page-status-flag: never-activated
uuid: 62a6c379-a460-4f8f-a909-03d04fa8944b
contentOwner: sarchiz
discoiquuid: 47c2a80f-78ac-4372-86b4-06351a1dd58f
docset: aem65
source-git-commit: d045fc1ac408f992d594a4cb68d1c4eeae2b0de1
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 2%

---


# Operaciones de procesamiento masivo {#bulk-processing-operations}

## Introducción {#introduction}

AEM Con la versión más reciente de la aplicación, el botón Seleccionar todo se ha ampliado a todas las vistas: Lista, Columna y Vista de tarjeta. El botón Seleccionar todo ahora selecciona todo el contenido de una carpeta o colección determinada, y no solo los recursos y las páginas cargados y visibles en el explorador del cliente.

Se han habilitado acciones clave para la operación masiva: **Mover**, **Eliminar** y **Copiar**. Un nuevo cuadro de diálogo permitirá a los clientes saber cuáles son las acciones para las que no está disponible el procesamiento masivo.

## Cómo Usar {#how-to-use}

Un nuevo botón llamado **Seleccionar todo** se ha agregado a las vistas Tarjeta, Lista o Columna. Este botón se puede utilizar en cualquiera de las vistas para seleccionar todos los elementos del conjunto de datos.

AEM En las versiones anteriores de la aplicación, la selección estaba limitada a lo que se cargaba en el explorador del cliente. Estos nuevos cambios se han introducido para evitar confusiones con respecto al número de elementos en los que se realiza una operación masiva.

Por ahora, se han añadido tres operaciones al procesamiento masivo:

* Mover
* Copiar
* Eliminar

En el futuro se agregará compatibilidad con más operaciones.
Para utilizar esta función, debe desplazarse a la carpeta o colección en la que desea realizar una operación masiva en páginas o recursos.

A continuación, elija una de las vistas, como se muestra a continuación:

### Vista de tarjeta {#card-view}

![Vista de tarjeta que muestra imágenes en miniatura de diversos recursos de imagen.](assets/unu.png)

### Selección masiva en la vista de tarjeta {#bulk-selection-in-card-view}

Los recursos o las páginas se pueden seleccionar de forma masiva mediante las opciones **Seleccionar todo** botón en la parte superior derecha:

![Seleccione el botón Todos que aparece en la esquina superior derecha de la vista de tarjeta.](assets/doi.png) ![Todas las imágenes en miniatura de los recursos de imagen en la vista de tarjeta se muestran como seleccionadas con marcas de verificación.](assets/trei.png)

### Vista de lista    {#list-view}

Lo mismo ocurre con la vista de lista:

![La opción Seleccionar todo está resaltada en la esquina superior derecha de la vista de lista.](assets/patru_modified.png)

### Selección masiva en la vista de lista {#bulk-selection-in-list-view}

En la vista de lista, utilice la variable **Seleccionar todo** o utilice la casilla de verificación de la izquierda para la selección masiva.

![La vista en vivo que muestra miniaturas de imágenes de recursos de imagen se muestra en filas horizontales.](assets/cinci.png) ![Cuadro de lista que muestra miniaturas de imágenes de recursos de imagen y una casilla de verificación a la izquierda de Nombre.](assets/sase.png)

### Vista de columna {#column-view}

![Vista de columna que muestra imágenes en miniatura de recursos de imágenes mostrados en columnas verticales.](assets/sapte.png)

### Selección masiva en la vista de columna {#bulk-selection-in-column-view}

![Todas las imágenes en miniatura de los recursos de imagen en la vista de columna se muestran como seleccionadas con marcas de verificación.](assets/opt.png)

## Operaciones habilitadas por lotes {#bulk-enabled-operations}

Después de la selección, se puede realizar una de las tres acciones activadas de forma masiva: **Mover**, **Copiar** o **Eliminar**.

Aquí, **Mover** Esta operación se realiza en los recursos seleccionados anteriormente. En cualquiera de las vistas, esto hará que todos los recursos se muevan a la ubicación elegida y no solo a los que se cargan en la pantalla.

![Mueva los recursos que muestran una carpeta seleccionada en la Vista de columna.](assets/noua.png)

Para otras operaciones que no se activan por lotes, como **Descargar,** aparecerá una advertencia que indica que solo se incluirán en la operación los elementos cargados en el explorador.

![Vista de recursos que muestra los recursos de imagen seleccionados y el cuadro de diálogo emergente &quot;Acción masiva no admitida&quot;.](assets/zece.png)
