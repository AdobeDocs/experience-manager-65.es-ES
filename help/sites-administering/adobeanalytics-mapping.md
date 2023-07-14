---
title: Asignación de datos de componente con propiedades de Adobe Analytics
description: Obtenga información sobre cómo asignar datos de componentes con propiedades de SiteCatalyst.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 1%

---

# Asignación de datos de componente con propiedades de Adobe Analytics{#mapping-component-data-with-adobe-analytics-properties}

Agregue componentes al marco de trabajo que recopilen los datos para enviarlos a Adobe Analytics. Los componentes diseñados para recopilar datos de análisis almacenan los datos en el repositorio adecuado **variable CQ**. Cuando se agrega un componente de este tipo a un marco de trabajo, el marco de trabajo muestra la lista de variables de CQ para que pueda establecer el vínculo con el entorno adecuado **Variable de Analytics**.

![aa-11](assets/aa-11.png)

Si la variable **AEM vista de** está abierto, las variables de Analytics aparecen en el buscador de contenido.

![aa-12](assets/aa-12.png)

Puede asignar varias variables de Analytics con el mismo **variable CQ**.

![chlimage_1-68](assets/chlimage_1-68.png)

Los datos asignados se envían a Adobe Analytics cuando se carga la página y se cumplen las siguientes condiciones:

* La página está asociada al marco de trabajo.
* La página utiliza los componentes que se añaden al marco de trabajo.

Utilice el siguiente procedimiento para asignar variables de componente CQ con propiedades de informe de Adobe Analytics.

1. En el **AEM vista de**, arrastre un componente de seguimiento desde la barra de tareas al marco de trabajo. Por ejemplo, arrastre el **Página** del componente de **General** categoría.

   ![aa-13](assets/aa-13.png)

   Hay varios grupos de componentes predeterminados: **General**, **Comercio**, **Communities**, y **Otros**. AEM La instancia se puede configurar para que muestre grupos y componentes diferentes.

1. Para asignar variables de Adobe Analytics con variables definidas en el componente, arrastre un **Variable de Analytics** desde el buscador de contenido a un campo en el componente de seguimiento. Por ejemplo, arrastre `Page Name (pageName)` hasta `pagedata.title`.

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >El ID del grupo de informes (RSID) seleccionado para el marco de trabajo determina las variables de Adobe Analytics que aparecen en el buscador de contenido.

1. Repita los dos pasos anteriores para otros componentes y variables.

   >[!NOTE]
   >
   >Puede asignar varias variables de Analytics (por ejemplo, `props`, `eVars`, `events`) a la misma variable de CQ (por ejemplo, `pagedata.title`)

   >[!CAUTION]
   >
   >Se recomienda encarecidamente que:
   >
   >* `eVars` y `props` están asignados a variables de CQ que comienzan por `pagedata.X` o `eventdata.X`
   >* que los eventos deben asignarse a variables que empiecen por `eventdata.events.X`

1. Para que el marco de trabajo esté disponible en la instancia de publicación del sitio, abra **Página** pestaña de la barra de tareas y haga clic en **Activar marco.**

## Asignación de variables relacionadas con el producto {#mapping-product-related-variables}

AEM utiliza una convención de nombres de variables y eventos relacionados con productos que están pensados para asignarse a propiedades relacionadas con productos de Adobe Analytics:

| Variable CQ | Variable de Analytics | Descripción |
|--- |--- |--- |
| `product.category` | `product.category` (variable de conversión) | La categoría del producto. |
| `product.sku` | `product.sku` (variable de conversión) | El SKU del producto. |
| `product.quantity` | `product.quantity` (variable de conversión) | Número de productos que se están comprando. |
| `product.price` | `product.price` (variable de conversión) | El precio del producto. |
| `product.events.<eventName>` | Los eventos de éxito que se asociarán con el producto en el informe. | `product.events` es el prefijo de los eventos llamados *eventName.* |
| `product.evars.<eVarName>` | Las variables de conversión ( `eVar`) para asociarlo al producto. | `product.evars` es el prefijo de las variables de eVar denominadas *eVarName.* |

AEM Varios componentes de comercio de utilizan estos nombres de variable.

>[!NOTE]
>
>No asigne la propiedad Productos de Adobe Analytics a una variable de CQ. La configuración de asignaciones relacionadas con productos como se describe en la tabla es equivalente a la asignación de la variable Products.

### Comprobación de informes en Adobe Analytics {#checking-reports-on-adobe-analytics}

1. Inicie sesión en el sitio web de Adobe Analytics AEM con las mismas credenciales proporcionadas a los usuarios de la plataforma de inicio de sesión de la plataforma de.
1. Asegúrese de que el RSID seleccionado sea el utilizado en los pasos anteriores.
1. Entrada **Informes** (en el lado izquierdo de la página) seleccione **Conversión personalizada**, entonces **Conversión personalizada 1-10** y seleccione la variable correspondiente a `eVar7`

1. Según la versión de Adobe Analytics que utilice, debe esperar una media de 45 minutos para que el informe se actualice con el término de búsqueda utilizado; por ejemplo, berenjena en el ejemplo

## Uso del buscador de contenido (cf#) con marcos de trabajo de Adobe Analytics {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

Inicialmente, cuando se abre un marco de trabajo de Adobe Analytics, el buscador de contenido contiene variables de Analytics predefinidas en:

* Tráfico
* Conversión
* Eventos

Cuando se selecciona un RSID, todas las variables que pertenecen a ese RSID se agregan a la lista.\
El `cf#` es necesario para asignar variables de Analytics a las variables de CQ presentes en los distintos componentes de seguimiento. Consulte Configuración de un marco de trabajo para el seguimiento básico.

AEM Según la vista seleccionada para el marco de trabajo, el buscador de contenido se rellenará con variables de Analytics (en la vista de) o con variables de CQ (en la vista de Analytics).

La lista se puede manipular de las siguientes maneras:

1. En **AEM vista de** Por lo tanto, la lista se puede filtrar según el tipo de variable seleccionada mediante los tres botones de filtro:

   * If *sin botón* está seleccionado, la lista muestra la lista completa.
   * Si la variable **Tráfico** cuando se selecciona el botón, la lista solo muestra las variables que pertenecen a la sección Tráfico.
   * Si la variable **Conversión** Cuando se selecciona este botón, la lista solo muestra las variables que pertenecen a la sección Conversión.
   * Si la variable **Eventos** Cuando se selecciona este botón, la lista solo muestra las variables que pertenecen a la sección Eventos.

   >[!NOTE]
   >
   >Solo puede haber un botón de filtro activo a la vez.

   1. La lista también tiene una función de búsqueda que filtra los elementos según el texto introducido en el campo de búsqueda.
   1. Si se activa una opción de filtro al buscar elementos en la lista, los resultados mostrados se filtrarán también según el botón activo.
   1. La lista se puede volver a cargar en cualquier momento con el botón de flechas giratorias.
   1. Si se seleccionan varios RSID en el marco de trabajo, todas las variables de la lista se mostrarán con todas las etiquetas utilizadas dentro de los RSID seleccionados.

1. En la vista Adobe Analytics, el Buscador de contenido muestra todas las variables de CQ que pertenecen a los componentes de seguimiento arrastrados en la vista CQ.

   * Por ejemplo, en el caso de que la variable **Descargar componente** es el *solo uno arrastrado* en la vista CQ (que tiene dos variables asignables) *eventdata.downloadLink* y *eventdata.events.startDownload*), el buscador de contenido tendrá este aspecto al cambiar a la vista de Adobe Analytics:

   ![aa-22](assets/aa-22.png)

   * Las variables se pueden arrastrar y soltar en cualquier variable de Adobe Analytics que pertenezca a una de las tres secciones de variables (**Tráfico**, **Conversión** y **Eventos**).

   * Al arrastrar un nuevo componente de seguimiento al marco de trabajo en la vista CQ, las variables CQ que pertenecen al componente se agregan automáticamente al Buscador de contenido (cf#) en la vista Adobe Analytics.

   >[!NOTE]
   >
   >Solo se puede asignar una variable de CQ a una variable de Adobe Analytics en un momento dado.

## AEM Uso de la vista de y Analytics {#using-aem-view-and-analytics-view}

En cualquier momento dado, los usuarios pueden cambiar entre dos formas de ver las asignaciones de Adobe Analytics en una página de marco de trabajo. Las dos vistas proporcionan una mejor visión general de las asignaciones dentro del marco, desde dos perspectivas distintas.

### AEM Vista de {#aem-view}

![aa-23](assets/aa-23.png)

Tomando la imagen anterior como ejemplo, la variable **AEM vista de** tiene las siguientes propiedades:

1. Esta es la vista predeterminada cuando se abre el marco de trabajo.
1. Izquierda: el buscador de contenido (cf#) se rellena con variables de Adobe Analytics basadas en los RSID seleccionados.
1. Encabezados de pestañas (**AEM vista de** y **Vista de Analytics**): utilícelos para cambiar entre las dos vistas.

1. **Vista AEM**:

   1. Si el marco de trabajo tiene componentes heredados de su elemento principal, se enumerarán aquí, junto con las variables asignadas a los componentes.

      1. Los componentes heredados están bloqueados.
      1. Para desbloquear un componente heredado, haga doble clic en el candado situado junto al nombre del componente
      1. Para revertir la herencia, elimine el componente desbloqueado; después, recuperará su estado de bloqueado.

   1. **Arrastre los componentes aquí para incluirlos en el marco de análisis**: los componentes se pueden arrastrar desde el Sidekick y soltar aquí.
   1. Puede encontrar todos los componentes que están incluidos actualmente en el marco de Analytics:

      1. Para agregar un componente, arrastre uno desde la pestaña Componentes de la barra de tareas
      1. Para eliminar un componente y todas sus asignaciones, seleccione Eliminar en el menú contextual del componente y, a continuación, acepte la eliminación en el cuadro de diálogo de confirmación.
      1. Tenga en cuenta que un componente solo se puede eliminar del marco en el que se creó y no se puede eliminar de los marcos secundarios en el sentido tradicional (solo se pueden sobrescribir).

### Vista de Analytics {#analytics-view}

![aa-24](assets/aa-24.png)

1. Se puede acceder a esta vista cambiando a **Vista de Analytics** en el marco de trabajo.
1. Izquierda: el buscador de contenido (cf#) se rellena con variables CQ basadas en los componentes arrastrados al marco de trabajo en la vista CQ.
1. Encabezados de pestañas (**AEM vista de** y **Vista de Analytics**): utilícelos para cambiar entre las dos vistas.

1. Las tres tablas (Tráfico, Conversión, Evento) enumeran todas las variables de Adobe Analytics disponibles. pertenecen a los RSID seleccionados. AEM Las asignaciones que se muestran aquí deben ser las mismas que en la vista de la:

   * **Tráfico**:

      * Variable de tráfico ( `prop1`) asignado a una variable de CQ ( `eventdata.downloadLink`)

      * Cuando el componente tiene un candado junto a él, significa que se hereda de un marco principal y, por lo tanto, no se puede editar

   * **Conversión**:

      * Variable de conversión ( `eVar1`) asignado a una variable de CQ ( `pagedata.title`)

      * Variable de conversión ( `eVar3`) asignado a una expresión JavaScript agregada en línea al hacer doble clic en el campo de la variable CQ e introducir el código manualmente

   * **Evento**:

      * Variable de evento ( `event1`) asignado a un evento CQ ( `eventdata.events.pageView`)

>[!NOTE]
>
>La columna de variable CQ de cualquier tabla también se puede rellenar en línea, haciendo doble clic en el campo y agregándole texto. Estos campos aceptan JavaScript como entrada.
>
>Por ejemplo, junto a `prop3` puede agregar lo siguiente:
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
para enviar el *title* de una página concatenada con su *sección del sitio* usando *:* (dos puntos) y con el prefijo *Adobe* as `prop3`
>

>[!CAUTION]
>
Solo se puede asignar una variable de CQ a una variable de Adobe Analytics en un momento dado.
