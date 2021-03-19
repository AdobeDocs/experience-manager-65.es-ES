---
title: Uso de gráficos en Interactive Communications
seo-title: Componente gráfico en Interactive Communications
description: Con los gráficos de una comunicación interactiva, puede condensar grandes cantidades de información en un formato visual fácil de analizar
seo-description: AEM Forms proporciona un componente de gráfico que puede utilizar para crear gráficos en la comunicación interactiva. Este documento explica las configuraciones básicas y de agente del componente de gráfico.
uuid: 978aa431-9a5b-4964-b37c-7bfa8c3f49b9
content-type: reference
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e21714ad-d445-4aff-b0db-d577061e0907
docset: aem65
feature: Comunicación interactiva
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2648'
ht-degree: 2%

---


# Uso de gráficos en Interactive Communications{#using-charts-in-interactive-communications}

Un gráfico o un gráfico es una representación visual de los datos. Condensa grandes cantidades de información en un formato visual fácil de entender, lo que permite a los destinatarios de la comunicación interactiva visualizar, interpretar y analizar mejor los datos complejos.

Mientras crea una comunicación interactiva, puede agregar gráficos para representar visualmente los datos bidimensionales del modelo de datos de formulario de la comunicación interactiva. El componente Gráfico permite añadir y configurar los siguientes tipos de gráficos: Circular, Columna, Anillo, Barra, Línea, Línea y Punto, Punto, Área y Cuadrante.

## Agregar y configurar un gráfico en una comunicación interactiva {#add-and-configure-chart-in-an-interactive-communication}

Realice los siguientes pasos para agregar y configurar un gráfico en una comunicación interactiva:

1. Pulse **Componentes** en la barra de tareas de la comunicación interactiva.
1. Arrastre y suelte el componente **Chart** en uno de los siguientes componentes:

   * Canal de impresión: Área de destino o campo de imagen
   * Canal web: Panel o área de destino

1. Pulse el componente de gráfico en el editor de comunicación interactiva y seleccione **[!UICONTROL Configurar (]** ![configurar_icono](assets/configure_icon.png)) en la barra de herramientas Componente.

   Las Propiedades del gráfico se muestran en el panel izquierdo.

   ![Propiedades básicas de un gráfico de tipo de línea en el canal de impresión](assets/chart_properties_print_new.png)

   Propiedades básicas de un gráfico de tipo de línea en el canal de impresión

   ![Propiedades básicas de un gráfico de tipo de línea en el canal web](assets/chart_properties_web_new.png)

   Propiedades básicas de un gráfico de tipo de línea en el canal web

1. Configure las [propiedades del gráfico](../../forms/using/chart-component-interactive-communications.md#configure-chart-properties) en función del tipo de canal.
1. (Solo canal de impresión) En **[!UICONTROL Configuración del agente]**, especifique si es obligatorio que el agente use este gráfico. Si la opción **[!UICONTROL t Is Mandatory For the Agent To Use This Chart]** no está seleccionada, el agente puede tocar el icono de ojo del gráfico en la pestaña **[!UICONTROL Content]** de la interfaz de usuario del agente para mostrar u ocultar el gráfico.

   ![chart_agentproperties](assets/chart_agentproperties.png)

1. Toque ![done_icon](assets/done_icon.png) para guardar las propiedades del gráfico.

   Toque **[!UICONTROL Preview]** para ver el aspecto y los datos asociados con el gráfico. Toque **[!UICONTROL Editar]** para reconfigurar las propiedades del gráfico.

## Configurar las propiedades del gráfico {#configure-chart-properties}

Configure las siguientes propiedades al crear gráficos para canales web e impresos:

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descripción</td>
   <td>Tipo de canal</td>
  </tr>
  <tr>
   <td>Nombre</td>
   <td>Identificador del elemento de gráfico. El nombre del gráfico especificado en este campo no está visible en el gráfico. Se utiliza al hacer referencia al elemento desde otros componentes, secuencias de comandos y expresiones SOM.</td>
   <td>Imprimir y Web</td>
  </tr>
  <tr>
   <td>Tipo de gráfico</td>
   <td>Tipo de gráfico que desea generar. Las opciones disponibles son circular, columna, anillo, barra, línea, línea y punto, punto y área.</td>
   <td>Imprimir y Web</td>
  </tr>
  <tr>
   <td>Serie &gt; Serie múltiple</td>
   <td>Seleccione esta opción para agregar varias series para los elementos de recopilación del modelo de datos de formulario trazados en el eje X y el eje Y.</td>
   <td>Imprimir y Web</td>
  </tr>
  <tr>
   <td>Serie &gt; Objeto de modelo de datos</td>
   <td>Nombre del elemento de recopilación del modelo de datos de formulario para agregar varias series al gráfico.<br /> Elija una propiedad de objeto del modelo de datos del formulario principal para las propiedades trazadas en el eje X y en el eje Y para formar una serie significativa. El objeto del modelo de datos que enlace debe ser de tipo Number, String o Date.</td>
   <td>Imprimir y Web</td>
  </tr>
  <tr>
   <td>Mostrar apilados</td>
   <td>Seleccione para apilar los valores de cada serie uno encima de otro.</td>
   <td>Imprimir y Web</td>
  </tr>
  <tr>
   <td>Eje X &gt; Título</td>
   <td>Título para el eje X.</td>
   <td>Imprimir y Web</td>
  </tr>
  <tr>
   <td>Eje X &gt; Objeto del modelo de datos</td>
   <td><p>Nombre del elemento de recopilación del modelo de datos de formulario que se va a trazar en el eje X.</p> <p>Elija dos propiedades de tipo colección/matriz del mismo objeto del modelo de datos principal que tengan sentido en relación mutua para trazar en el eje X e Y de un gráfico. El objeto del modelo de datos que enlace debe ser de tipo Number, String o Date.</p> </td>
   <td>Imprimir y Web</td>
  </tr>
  <tr>
   <td>Eje Y &gt; Título</td>
   <td>Título para el eje Y. </td>
   <td>Imprimir y Web</td>
  </tr>
  <tr>
   <td>Eje Y &gt; Objeto del modelo de datos</td>
   <td><p>Elemento de colección del modelo de datos de formulario que se va a trazar en el eje Y. En el canal Imprimir, el objeto del modelo de datos para el eje Y debe ser del tipo Número.</p> <p>Elija dos propiedades de tipo colección/matriz del mismo objeto del modelo de datos principal que tengan sentido en relación mutua para trazar en el eje X e Y de un gráfico. </p> </td>
   <td>Imprimir y Web</td>
  </tr>
  <tr>
   <td>Eje Y &gt; Función</td>
   <td>Función estadística/personalizada que se utilizará para calcular los valores en el eje Y.</td>
   <td>Imprimir y Web</td>
  </tr>
  <tr>
   <td>Ocultar objeto</td>
   <td>Seleccione para ocultar el gráfico en la salida final.</td>
   <td>Imprimir y Web</td>
  </tr>
  <tr>
   <td>Título</td>
   <td>Título del gráfico. </td>
   <td>Imprimir</td>
  </tr>
  <tr>
   <td>Altura</td>
   <td>Altura del gráfico en píxeles.</td>
   <td>Imprimir</td>
  </tr>
  <tr>
   <td>Anchura</td>
   <td>Anchura del gráfico en píxeles. Puede controlar la anchura del gráfico en el canal web mediante la capa de estilo o aplicando un tema.</td>
   <td>Imprimir</td>
  </tr>
  <tr>
   <td>Salto de página obligatorio antes de</td>
   <td>Seleccione para agregar un salto de página obligatorio antes del gráfico y coloque el gráfico sobre una nueva página. </td>
   <td>Imprimir</td>
  </tr>
  <tr>
   <td>Salto de página obligatorio después de</td>
   <td>Seleccione para agregar un salto de página obligatorio después del gráfico y coloque el contenido que sigue al gráfico en la parte superior de una nueva página. </td>
   <td>Imprimir</td>
  </tr>
  <tr>
   <td>Sangría</td>
   <td>Sangría del gráfico desde la izquierda de la página. </td>
   <td>Imprimir</td>
  </tr>
  <tr>
   <td>Información de objeto</td>
   <td><p>Formato en el que aparece la información del objeto al pasar el ratón sobre un punto de datos del gráfico en el canal web. El valor predeterminado es ${x}(${y}). Según el tipo de gráfico, cuando señala el ratón sobre un punto, barra o fracción del gráfico, las variables ${x} y ${y} se reemplazan dinámicamente con los valores correspondientes del eje X y del eje Y y se muestran en la información del objeto.</p> <p>Para desactivar la información del objeto, deje el campo <span class="uicontrol">Tooltip</code> en blanco. Esta opción no se aplica a los gráficos de líneas y áreas. Por ejemplo, consulte <a href="#chartoutputprintweb">Ejemplo 1: Salida de gráfico en impresión y Web</a>.</code></p> </td>
   <td>Web</td>
  </tr>
  <tr>
   <td>Configuraciones específicas de gráficos</td>
   <td><p>Además de las configuraciones comunes, están disponibles las siguientes configuraciones específicas del gráfico:</p>
    <ul>
     <li><strong>Mostrar leyenda:  </strong>Muestra una leyenda para el gráfico circular o circular cuando está habilitada.</li>
     <li><strong>Posición de la leyenda:  </strong>Especifica la posición del pie de ilustración con respecto al gráfico. Las opciones disponibles son Derecha, Izquierda, Superior e Inferior. Se recomienda utilizar la leyenda del lado derecho en el canal de impresión.</li>
     <li><strong>Radio interior</strong>: Disponible para gráficos circulares para especificar el radio (en píxeles) del círculo interior del gráfico.</li>
     <li><strong>Color</strong> de línea: Disponible para gráficos de líneas, líneas y puntos y áreas para especificar el color de la línea del gráfico.</li>
     <li><strong>Color</strong> de punto: Disponible para gráficos de puntos y líneas y puntos para especificar el color de los puntos del gráfico.<br /> </li>
     <li><strong>Color</strong> de área: Disponible para gráficos de área para especificar el color del área bajo la línea del gráfico.</li>
     <li><strong>Punto de referencia &gt; Tipo de enlace:  </strong>Disponible para gráficos de cuadrantes <strong> </strong>para especificar el tipo de enlace para el punto de referencia. Utilice la propiedad de objeto de texto estático o modelo de datos para definir el valor del punto de referencia.</li>
     <li><strong>Punto de referencia &gt; Eje X:  </strong>Disponible para gráficos de cuadrante si selecciona  <span class="uicontrol"></code> Estático en la lista desplegable Tipo de enlace para especificar el valor del eje X para el punto de referencia.</code></li>
     <li><strong>Punto de referencia &gt; Eje Y:  </strong>Disponible para gráficos de cuadrante si selecciona  <span class="uicontrol"></code> Estático en la lista desplegable Tipo de enlace para especificar el valor del eje Y para el punto de referencia.</code></li>
     <li><strong>Punto de referencia &gt; Objeto de modelo de datos para series:  </strong>Disponible para varios gráficos de cuadrantes de series si selecciona Objeto  <span class="uicontrol">de modelo de </code> datos en la lista desplegable Tipo de enlace . Defina la propiedad del objeto del modelo de datos de formulario para identificar la serie del punto de referencia. </code></li>
     <li><strong>Punto de referencia &gt; Valor del objeto del modelo de datos para series:  </strong>Disponible para varios gráficos de cuadrantes de series si selecciona Objeto  <span class="uicontrol">de modelo de </code> datos en la lista desplegable Tipo de enlace . Utilice la propiedad del objeto del modelo de datos de formulario para series y el valor definido en este campo para identificar la serie para el punto de referencia.</code></li>
     <li><strong>Punto de referencia &gt; Objeto de modelo de datos para punto de referencia:  </strong>Disponible para gráficos de cuadrantes si selecciona Objeto  <span class="uicontrol">de modelo de </code> datos en la lista desplegable Tipo de enlace . Defina una propiedad de objeto del modelo de datos de formulario que sea similar a las propiedades trazadas en los ejes X e Y. Además, para varias series, defina una propiedad de objeto del modelo de datos que sea una entidad secundaria de la propiedad de objeto del modelo de datos definida para la serie.</code></li>
     <li><strong>Punto de referencia &gt; Valor del objeto del modelo de datos para el punto de referencia:  </strong>Disponible para gráficos de cuadrantes si selecciona Objeto  <span class="uicontrol">de modelo de </code> datos en la lista desplegable Tipo de enlace . Utilice la propiedad del objeto del modelo de datos de formulario para el punto de referencia y el valor definido en este campo para identificar el punto de referencia del gráfico.<br /> <strong>Etiquetas de cuadrantes &gt; Superior izquierda: </strong> disponible para gráficos de cuadrantes para especificar el nombre del cuadrante superior izquierdo.</code></li>
     <li><strong>Etiquetas de cuadrantes &gt; Arriba a la derecha: </strong> disponible para gráficos de cuadrantes para especificar el nombre del cuadrante superior derecho.</li>
     <li><strong>Etiquetas de cuadrantes &gt; Abajo a la derecha:  </strong>Disponible para gráficos de cuadrantes para especificar el nombre del cuadrante inferior derecho.</li>
     <li><strong>Etiquetas de cuadrantes &gt; Abajo a la izquierda:  </strong>Disponible para gráficos de cuadrantes para especificar el nombre del cuadrante inferior izquierdo.</li>
    </ul> </td>
   <td>Imprimir y Web</td>
  </tr>
 </tbody>
</table>

## Uso de funciones en el gráfico {#use-functions-in-chart}

Puede configurar un gráfico para que utilice funciones estadísticas a fin de calcular los valores a partir de los datos de origen para trazar en el gráfico. Al aplicar funciones en un gráfico, se pueden representar datos que el modelo de datos de formulario no proporciona directamente.

![Funciones en gráficos](assets/functions_charts_new.png)

Aunque el componente Gráfico incluye algunas funciones integradas, puede escribir [funciones personalizadas](#customfunctionsweb) y ponerlas a disposición para su uso en la configuración de gráficos del canal web.

Las siguientes funciones están disponibles de forma predeterminada con el componente Gráfico :

**Media (Average)** Devuelve el promedio de los valores en el eje X o Y para un valor determinado en el otro eje.

**** SumDevuelve la suma de todos los valores del eje X o Y para un valor determinado del otro eje.

**** MaximumDevuelve el máximo de los valores en el eje X o Y para un valor determinado en el otro eje.

**** FrequencyDevuelve el número de valores en el eje X o Y para un valor determinado en el otro eje.

**** RangeDevuelve la diferencia entre el máximo y el mínimo de los valores en el eje X o Y para un valor determinado en el otro eje.

**** MedianaDevuelve el valor que separa los valores más altos e inferiores a la mitad en los ejes X o Y para un valor determinado en el otro eje.

**** MinimumDevuelve el mínimo de los valores del eje X o Y para un valor determinado del otro eje.

**** ModeDevuelve el valor con la mayoría de las incidencias en el eje X o Y para un valor determinado del otro eje.

Para obtener más información, consulte [Ejemplo 2: Aplicación de las funciones Suma y Frecuencia en un gráfico de líneas](#applicationsumfrequency).

### Funciones personalizadas en el canal web {#customfunctionsweb}

Además de utilizar las funciones predeterminadas en los gráficos, puede escribir funciones personalizadas en JavaScript™ y ponerlas a disposición en la lista de funciones del componente Gráfico para el canal web.

Una función toma una matriz o valores y un nombre de categoría como entradas y devuelve un valor. Por ejemplo:

```javascript
Multiply(valueArray, category) {
 var val = 1;
 _.each(valueArray, function(value) {
 val = val * value;
 });
 return val;
}
```

Una vez que haya escrito una función personalizada, haga lo siguiente para que esté disponible para usarla en la configuración del gráfico:

1. Añada la función personalizada en la biblioteca de cliente asociada a la comunicación interactiva correspondiente. Para obtener más información, consulte [Configuración de la acción de envío](/help/forms/using/configuring-submit-actions.md) y [Uso de bibliotecas del lado del cliente](/help/sites-developing/clientlibs.md).

1. Para mostrar la función personalizada en la lista desplegable Función, en CRXDe Lite, cree un nodo `nt:unstructured` en la carpeta de aplicaciones con las siguientes propiedades:

   * Agregue la propiedad `guideComponentType` con el valor `fd/af/reducer`. (obligatorio)

   * Agregue la propiedad `value` a un nombre completo de la función personalizada de JavaScript™. (obligatorio) y establezca su valor en el nombre de la función personalizada, como Multiply.
   * Agregue la propiedad `jcr:description` con el valor que desea mostrar como nombre de la función personalizada que aparece en la lista desplegable Función. Por ejemplo, **Multiply**.

   * Agregue la propiedad `qtip` con un valor que sea una breve descripción de la función personalizada. Aparece como información de objeto al pasar el puntero sobre el nombre de función en la lista desplegable **Function**.

1. Haga clic en **Guardar todo** para guardar la configuración.

La función ahora está disponible para su uso en el gráfico.

## Ejemplo 1: Salida de gráfico en impresión y Web {#chartoutputprintweb}

En la ficha Básico , se define el tipo de gráfico, las propiedades del modelo de datos del formulario de origen que contienen datos, las etiquetas que se van a trazar en el eje X y el eje Y del gráfico y, opcionalmente, la función estadística para calcular los valores para trazar en el gráfico.

Comprendamos en detalle la información mínima requerida en las propiedades básicas, con la ayuda de una declaración de tarjeta generada mediante una comunicación interactiva. Tenga en cuenta que desea generar un gráfico para mostrar la cantidad de gastos diferentes en el estado. Desea utilizar diferentes tipos de gráficos para la impresión y la salida web de la comunicación interactiva.

### Gráfico de columnas para Imprimir {#columnchartprint}

Para ello, especifique las siguientes propiedades:

* **[!UICONTROL Nombre]** : especifique el nombre del gráfico.
* **[!UICONTROL Tipo de gráfico]** : seleccione  **** Columna en la lista desplegable.
* **[!UICONTROL Título]** : especifique el tipo de gasto para el eje X y la cantidad de transacción para el eje Y.
* **[!UICONTROL Objetos del modelo de datos]** : seleccione las propiedades del objeto del modelo de datos para crear enlaces de datos para los ejes X (Tipo de gasto) y Y (Cantidad de transacción).

![Gráfico de columnas en el canal de impresión de una comunicación interactiva](assets/sample_chart_print_column_new.png)

Gráfico de columnas en el canal de impresión de una comunicación interactiva

### Gráfico de anillo para la web {#donutchartweb}

Para ello, especifique las siguientes propiedades:

* **[!UICONTROL Nombre]** : especifique el nombre del gráfico.
* **[!UICONTROL Tipo de gráfico]** : seleccione  **** Donuts en la lista desplegable.
* **[!UICONTROL Objetos del modelo de datos]** : seleccione las propiedades del objeto del modelo de datos para crear enlaces de datos para los ejes X (Tipo de gasto) y Y (Cantidad de transacción).
* **[!UICONTROL Radio interior]** : especifique el valor de Radio interior como 150 para especificar el radio (en píxeles) del círculo interior del gráfico.
* **[!UICONTROL Información del objeto]** : use el formato predeterminado ${x}(${y}) para mostrar la información del objeto. La información del objeto se muestra de la siguiente manera: Tipo de Gasto(Importe de Transacción). Ejemplo: Débito de bitcoin(10000).

![Gráfico circular en el canal web de una comunicación interactiva](assets/sample_chart_web_new.png)

Gráfico circular en el canal web de una comunicación interactiva

## Ejemplo 2: Aplicación de las funciones Suma y Frecuencia en un gráfico de líneas {#applicationsumfrequency}

Al aplicar funciones en un gráfico, se pueden representar datos que el modelo de datos de formulario no proporciona directamente. En este ejemplo, utilizamos un ejemplo de extracto de tarjetas de crédito para comprender cómo se pueden aplicar las funciones Suma y Frecuencia al gráfico.

![Gráfico de líneas sin una función con dos transacciones &quot;Debit for AirBnB&quot;](assets/line_chart_web_new.png)

Gráfico de líneas sin una función con dos transacciones &quot;Debit for AirBnB&quot;

### Función Sum {#sum-function}

Puede aplicar la función sum para agregar valores de varias instancias de la misma propiedad de datos y mostrarlos solo una vez. Por ejemplo, en el gráfico siguiente, la función Suma se aplica en el eje Y para sumar la cantidad de los dos Débito para transacciones AirBnB (2050 y 1050) y mostrar solo una transacción (3100).

La función Sum puede hacer que el gráfico sea más útil cuando desea recopilar y mostrar la suma para muchas instancias de la misma propiedad de datos.

![Suma de gráfico de líneas](assets/line_chart_web_sum_new.png)

### Función de frecuencia {#frequency-function}

La función Frequency devuelve el número de valores del eje Y para un valor determinado del otro eje. Con la aplicación de la función Frequency en el eje Y (Transaction Amount), el gráfico muestra que ha habido dos incidencias de Debit para transacciones AirBnB y una incidencia del resto de tipos de transacciones.

![Frecuencia del gráfico de líneas](assets/line_chart_web_functions_frequency_new.png)

## Ejemplo 3: Gráfico de cuadrantes de varias series en Web {#example-multi-series-quadrant-chart-in-web}

El gráfico representa la cantidad de transacciones realizadas en un intervalo de fechas determinado. El gráfico de cuadrantes permite dividir el área del gráfico en cuatro secciones etiquetadas. El gráfico utiliza un punto de referencia estático para el eje X y el eje Y. Utilice la función de varias series para separar los datos en función del nombre del banco.

Para ello, especifique las siguientes propiedades:

* **Nombre:** especifique el nombre del gráfico.
* **Tipo de gráfico:** seleccione  **** Cuadrante en la lista desplegable.

* Seleccione la casilla **Multiple Series**.
* **Objeto** Modelo de datos: Especifique la propiedad del objeto del modelo de datos para la serie. La propiedad del objeto del modelo de datos para el nombre del banco es una propiedad principal de las propiedades del objeto del modelo de datos trazadas en los ejes X e Y.
* **Objetos del modelo de datos:** seleccione las propiedades de objeto del modelo de datos para crear enlaces de datos para los ejes X (Fecha de transacción) y Y (Importe de transacción).
* En la sección **Reference Point**, seleccione **Static** como Tipo de enlace.

* Especifique los valores para los puntos de referencia del eje X y del eje Y.
* Especifique las etiquetas de cuadrante para los cuadrantes Superior izquierda, Superior derecha, Inferior derecha e Inferior izquierda.
* Seleccione la casilla **Show legends** para mostrar los códigos de color de los nombres de banco.

![Gráficos de cuadrante](assets/charts_quadrant_example_new.png)

