---
title: Asignación de datos de componente con propiedades de Adobe Analytics
seo-title: Mapping Component Data with Adobe Analytics Properties
description: Obtenga información sobre cómo asignar datos de componentes con propiedades de SiteCatalyst.
seo-description: Learn how to map component data with SiteCatalyst properties.
uuid: b08ab37f-ad58-4c04-978f-8e21a3823ae8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6c1f8869-62d9-4fac-aa0d-b99bb0e86d6b
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
source-git-commit: 085e77b7b831d6be626a46d3de215aedb50f6178
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 0%

---

# Asignación de datos de componente con propiedades de Adobe Analytics{#mapping-component-data-with-adobe-analytics-properties}

Agregue componentes a la estructura que recopilen los datos para enviarlos a Adobe Analytics. Los componentes diseñados para recopilar datos de análisis almacenan los datos en los **Variable CQ**. Cuando se agrega un componente de este tipo a un marco, el marco muestra la lista de variables de CQ para que pueda dirigirse a las correspondientes **Variable de Analytics**.

![aa-11](assets/aa-11.png)

Cuando la variable **vista AEM** está abierta, las variables de Analytics aparecen en el buscador de contenido.

![aa-12](assets/aa-12.png)

Puede asignar varias variables de Analytics con el mismo **Variable CQ**.

![chlimage_1-68](assets/chlimage_1-68.png)

Los datos asignados se envían a Adobe Analytics cuando la página se carga y se cumplen las siguientes condiciones:

* La página está asociada a la estructura.
* La página utiliza los componentes que se agregan al marco.

Utilice el siguiente procedimiento para asignar variables de componentes de CQ con propiedades de informes de Adobe Analytics.

1. En el **vista AEM**, arrastre un componente de seguimiento de la barra de tareas al marco. Por ejemplo, arrastre el **Página** componente desde **General** categoría.

   ![aa-13](assets/aa-13.png)

   Existen varios grupos de componentes predeterminados: **General**, **Comercio**, **Comunidades**, **Search&amp;Promote** y **Otro**. La instancia de AEM puede configurarse para mostrar diferentes grupos y componentes.

1. Para asignar variables de Adobe Analytics con variables definidas en el componente, arrastre y **Variable de Analytics** desde el buscador de contenido a un campo del componente de seguimiento. Por ejemplo, arrastre `Page Name (pageName)` a `pagedata.title`.

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >El ID del grupo de informes (RSID) seleccionado para la estructura determina las variables de Adobe Analytics que aparecen en el buscador de contenido.

1. Repita los dos pasos anteriores para otros componentes y variables.

   >[!NOTE]
   >
   >Puede asignar varias variables de Analytics (p. ej. `props`, `eVars`, `events`) a la misma variable de CQ (p. ej. `pagedata.title`)

   >[!CAUTION]
   >
   >Se recomienda encarecidamente que:
   >
   >* `eVars` y `props` se asignan a variables de CQ que comienzan con `pagedata.X` o `eventdata.X`
   >* que los eventos deben asignarse a variables que comiencen por `eventdata.events.X`


1. Para que el marco esté disponible en la instancia de publicación del sitio, abra el **Página** de la barra de tareas y haga clic en **Activar marco.**

## Asignación de variables relacionadas con el producto {#mapping-product-related-variables}

AEM utiliza una convención para nombrar variables y eventos relacionados con el producto que están pensados para asignarse a propiedades relacionadas con el producto de Adobe Analytics:

| Variable CQ | Variable de Analytics | Descripción |
|--- |--- |--- |
| `product.category` | `product.category` (variable de conversión) | La categoría del producto. |
| `product.sku` | `product.sku` (variable de conversión) | El sku del producto. |
| `product.quantity` | `product.quantity` (variable de conversión) | Número de productos que se compran. |
| `product.price` | `product.price` (variable de conversión) | El precio del producto. |
| `product.events.<eventName>` | Los eventos de éxito que se asociarán con el producto en el informe. | `product.events` es el prefijo de los eventos asignados *eventName.* |
| `product.evars.<eVarName>` | Las variables de conversión ( `eVar`) para asociarlo al producto. | `product.evars` es el prefijo de las variables de eVar denominadas *eVarName.* |

Varios componentes AEM Commerce utilizan estos nombres de variables.

>[!NOTE]
>
>No asigne la propiedad Productos de Adobe Analytics a una variable de CQ. La configuración de asignaciones relacionadas con el producto como se describe en la tabla equivale a asignar la variable Productos.

### Comprobación de informes en Adobe Analytics {#checking-reports-on-adobe-analytics}

1. Inicie sesión en el sitio web de Adobe Analytics con las mismas credenciales que se proporcionan a AEM.
1. Asegúrese de que el RSID seleccionado sea el que se usó en los pasos anteriores.
1. En **Informes** (en el lado izquierdo de la página), seleccione **Conversión personalizada**, luego **Conversión personalizada 1-10** y seleccione la variable correspondiente a `eVar7`

1. En función de la versión de Adobe Analytics que utilice, debe esperar un promedio de 45 minutos para que el informe se actualice con el término de búsqueda utilizado; Por ejemplo, eggfactory en el ejemplo

## Uso del buscador de contenido (cf#) con marcos de Adobe Analytics {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

Inicialmente, cuando se abre un marco de Adobe Analytics, el buscador de contenido contiene variables predefinidas de Analytics en:

* Tráfico
* Conversión
* Sucesos

Cuando se selecciona un RSID, todas las variables que pertenecen a ese RSID se agregan a la lista.\
La variable `cf#` es necesario para asignar variables de Analytics a las variables de CQ presentes en los distintos componentes de seguimiento. Consulte Configuración de un marco para el seguimiento básico.

Según la vista seleccionada para la infraestructura, el buscador de contenido se rellenará con variables de Analytics (en AEM vista) o con variables de CQ (en la vista de Analytics).

La lista se puede manipular de las siguientes maneras:

1. Cuando **vista AEM**, la lista se puede filtrar según el tipo de variable que se seleccione con los 3 botones de filtro:

   * If *botón no* está seleccionado, la lista muestra la lista completa.
   * Si la variable **Tráfico** está seleccionado, la lista solo mostrará las variables que pertenecen a la sección Tráfico .
   * Si la variable **Conversión** está seleccionado, la lista solo muestra las variables que pertenecen a la sección Conversión .
   * Si la variable **Eventos** está seleccionado, la lista solo muestra las variables que pertenecen a la sección Eventos .

   >[!NOTE]
   >
   >Solo se puede activar un botón de filtro a la vez.

   >[!NOTE]
   >
   >Las variables de Search&amp;Promote también pertenecen a la sección Conversión .

   1. La lista también tiene una función de búsqueda, que filtra los elementos según el texto introducido en el campo de búsqueda.
   1. Si se activa una opción de filtro al buscar elementos en la lista, los resultados mostrados también se filtrarán según el botón activo.
   1. La lista se puede volver a cargar en cualquier momento con el botón de flechas giratorias.
   1. Si se seleccionan varios RSID en la infraestructura, todas las variables de la lista se mostrarán con todas las etiquetas utilizadas dentro de los RSID seleccionados.


1. En la vista Adobe Analytics, el Buscador de contenido muestra todas las variables de CQ que pertenecen a los componentes de seguimiento arrastrados en la vista CQ.

   * Por ejemplo, en caso de que la variable **Descargar componente** es la variable *solo uno arrastrado* en la vista CQ (que tiene dos variables asignables) *eventdata.downloadLink* y *eventdata.events.startDownload*), el buscador de contenido tendrá este aspecto al cambiar a la vista de Adobe Analytics:

   ![aa-22](assets/aa-22.png)

   * Las variables se pueden arrastrar y soltar en cualquier variable de Adobe Analytics que pertenezca a una de las tres secciones de variables (**Tráfico**, **Conversión** y **Eventos**).

   * Al arrastrar un nuevo componente de seguimiento al marco en la vista CQ, las variables CQ que pertenecen al componente se añaden automáticamente al Buscador de contenido (cf#) en la vista Adobe Analytics.
   >[!NOTE]
   >
   >Solo se puede asignar una variable CQ a una variable de Adobe Analytics en un momento determinado.

## Uso de la vista AEM y la vista de Analytics {#using-aem-view-and-analytics-view}

En un momento dado, los usuarios tienen la opción de cambiar entre dos formas de ver las asignaciones de Adobe Analytics en una página de marco. Las dos vistas proporcionan una mejor visión general de las asignaciones dentro del marco, desde dos perspectivas distintas.

### Vista AEM {#aem-view}

![aa-23](assets/aa-23.png)

Tomando como ejemplo la imagen anterior, la variable **vista AEM** tiene las siguientes propiedades:

1. Esta es la vista predeterminada cuando se abre el marco.
1. Lado izquierdo: el buscador de contenido (cf#) se rellena con variables de Adobe Analytics basadas en los RSID seleccionados.
1. Encabezados de tabulación (**vista AEM** y **Vista de Analytics**): utilice estos iconos para cambiar entre las dos vistas.

1. **Vista AEM**:

   1. Si la estructura tiene componentes que se heredan de su elemento principal, estos se enumerarán aquí, junto con las variables asignadas a los componentes.

      1. Los componentes heredados están bloqueados.
      1. Para desbloquear un componente heredado, haga doble clic en el cerrojo situado junto al nombre del componente
      1. Para revertir la herencia, debe eliminar el componente desbloqueado; después de lo cual recuperará su estado de bloqueo.
   1. **Arrastre los componentes aquí para incluirlos en el marco de análisis**: Los componentes se pueden arrastrar desde la barra de tareas y soltar aquí.
   1. Puede encontrar todos los componentes que están actualmente incluidos en el marco de análisis:

      1. Para añadir un componente, arrastre uno desde la ficha Componentes de la barra de tareas
      1. Para eliminar un componente y todas sus asignaciones, seleccione Eliminar en el menú contextual del componente y acepte la eliminación en el cuadro de diálogo de confirmación.
      1. Tenga en cuenta que un componente solo se puede eliminar del marco en el que se creó y no se puede eliminar de los marcos secundarios en el sentido tradicional (solo se puede sobrescribir).


### Vista de Analytics {#analytics-view}

![aa-24](assets/aa-24.png)

1. Para acceder a esta vista, cambie a la función **Vista de Analytics** en el marco.
1. Lado izquierdo: Buscador de contenido (cf#) rellenado por variables de CQ basadas en los componentes arrastrados al marco en la vista CQ.
1. Encabezados de tabulación (**vista AEM** y **Vista de Analytics**): utilice estos iconos para cambiar entre las dos vistas.

1. Las tres tablas (Tráfico, Conversión, Evento) enumeran todas las variables de Adobe Analytics disponibles. perteneciente a los RSID seleccionados. Las asignaciones que se muestran aquí deben ser las mismas que en la vista AEM:

   * **Tráfico**:

      * Variable de tráfico ( `prop1`) asignada a una variable de CQ ( `eventdata.downloadLink`)

      * Cuando el componente tiene un Padlock junto a él, significa que se hereda de un marco principal y, por lo tanto, no se puede editar
   * **Conversión**:

      * Variable de conversión ( `eVar1`) asignada a una variable de CQ ( `pagedata.title`)

      * Variable de conversión ( `eVar3`) asignada a una expresión de javascript añadida en línea haciendo doble clic en el campo de la variable CQ e introduciendo el código manualmente
   * **Evento**:

      * Variable de evento ( `event1`) asignado a un evento de CQ ( `eventdata.events.pageView`)



>[!NOTE]
>
>La columna de la variable CQ de cualquier tabla también se puede rellenar en línea, haciendo doble clic en el campo y agregándole texto. Estos campos aceptan javascript como entrada.
>
>Por ejemplo, junto a `prop3` puede agregar:
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
para enviar la variable *title* de una página concatenada con su *sitesection* using *:* (dos puntos) y el prefijo *Adobe* como `prop3`

>[!CAUTION]
Solo se puede asignar una variable CQ a una variable de Adobe Analytics en un momento determinado.
