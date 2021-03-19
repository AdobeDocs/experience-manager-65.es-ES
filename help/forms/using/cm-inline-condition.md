---
title: Condición y repetición en línea en Interactive Communications y letras
seo-title: Condición y repetición en línea en Interactive Communications y letras
description: Con las condiciones en línea y repetir en las comunicaciones interactivas y las letras, puede crear comunicaciones que sean muy contextuales y estén bien estructuradas.
seo-description: Con las condiciones en línea y repetir en las comunicaciones interactivas y las letras, puede crear comunicaciones que sean muy contextuales y estén bien estructuradas.
uuid: 32b48a8b-431d-4f9c-9f51-8e7e9ac624a0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: interactive-communications, correspondence-management
discoiquuid: bbaba39b-e15a-4143-b6fc-7789fa2917b4
docset: aem65
feature: Administración de correspondencia
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 0%

---


# Condición y repetición en línea en Interactive Communications and letters{#inline-condition-and-repeat-in-interactive-communications-and-letters}

## Condiciones en línea {#inline-conditions}

AEM Forms permite utilizar condiciones en línea en módulos de texto para automatizar la representación de texto que depende del contexto o los datos asociados con el modelo de datos de formulario (en comunicación interactiva) o el diccionario de datos (en letras). La condición en línea muestra contenido específico en función de que la evaluación de la condición sea verdadera o falsa.

Las condiciones realizan cálculos sobre los valores de datos proporcionados por el modelo de datos de formulario/el diccionario de datos o por los usuarios finales. Con las condiciones en línea, puede ahorrar tiempo y reducir los errores humanos, a la vez que crea comunicaciones/cartas interactivas altamente contextuales y personalizadas.

Para obtener más información, consulte:

* [Crear una comunicación interactiva](../../forms/using/create-interactive-communication.md)
* [Información general sobre la gestión de correspondencia](/help/forms/using/cm-overview.md)
* [Texto en comunicaciones interactivas](../../forms/using/texts-interactive-communications.md)

### Ejemplo: Uso de reglas para condicionalizar el texto en línea en la comunicación interactiva {#example-using-rules-to-conditionalize-inline-text-in-interactive-communication}

Para condicionalizar una frase, párrafo o cadena de texto en una comunicación interactiva, puede crear una regla en el fragmento de documento de texto correspondiente. El siguiente ejemplo utiliza una regla para mostrar un número gratuito solo a los destinatarios de EE. UU. de la comunicación interactiva.

Para obtener más información, consulte Crear regla en texto en [Textos en comunicaciones interactivas](../../forms/using/texts-interactive-communications.md).

Una vez que se incluye el fragmento de texto en una comunicación interactiva y el agente utiliza la interfaz de usuario del agente para preparar una comunicación interactiva, los datos (modelo de datos de formulario) de los destinatarios se evalúan y el texto solo se muestra a los destinatarios en Estados Unidos.

### Ejemplo: Uso de una condición en línea en una carta para representar la dirección adecuada {#example-using-inline-condition-in-a-letter-to-render-the-appropriate-address}

Puede insertar una condición en línea en una letra insertando la condición en línea en el módulo de texto correspondiente. El siguiente ejemplo utiliza dos condiciones para evaluar y mostrar la dirección adecuada, Sir o Ma&#39;am, en una carta basada en el elemento DD Gender. Con pasos similares, puede crear otras condiciones.

>[!NOTE]
>
>Si los recursos existentes incluyen expresiones antiguas/repetidas (anteriores a la versión 6.2 SP1 CFP4), los recursos muestran la sintaxis antigua de condición y se repiten. Sin embargo, la condición o repetición antigua funciona. Las expresiones de condición/repetición nuevas y antiguas son compatibles entre sí para crear una mezcla anidada de expresiones de condición/repetición antiguas y nuevas.

1. En el módulo de texto correspondiente, seleccione la parte del texto que desea condicionalizar y pulse **Condición**.

   ![1_selecttext](assets/1_selecttext.png)

   El cuadro de diálogo Condición aparece con una condición vacía.

   ![2_conditiondialog](assets/2_conditiondialog.png)

   >[!NOTE]
   >
   >No se puede guardar una expresión condicional vacía o no válida. Debe haber una expresión condicional válida dentro de `${}` para guardar la expresión.

1. Realice lo siguiente para construir una condición para evaluar si el texto seleccionado/condicional aparece en la carta y, a continuación, pulse la marca de verificación para guardar la expresión:

   Pulse dos veces un elemento DD para insertarlo en la condición. Inserte el operador adecuado y construya la siguiente condición en el cuadro de diálogo.

   ```javascript
   ${DD_creditcard_Gender=="Male"}
   ```

   Para obtener más información sobre la creación de la expresión, consulte **Creación de expresiones y funciones remotas con el generador de expresiones** en [Generador de expresiones](../../forms/using/expression-builder.md). El valor especificado en la expresión debe ser compatible con el elemento del diccionario de datos. Para obtener más información, consulte [Diccionario de datos](../../forms/using/data-dictionary.md).

   Una vez insertada la condición, puede situarse sobre el controlador de la izquierda de la condición para ver la condición. Puede pulsar el control para ver el menú emergente de la condición, que le permite editar o eliminar la condición.

   ![3_hoverhandle](assets/3_hoverhandle.png) ![4_editconditionremoveconditionpopup](assets/4_editconditionremoveconditionpopup.png)

1. Inserte una condición similar seleccionando el texto `Ma'am`.

   ```javascript
   ${DD_creditcard_Gender == "Female"}
   ```

1. Previsualice la carta correspondiente y observe que el texto se procesa según la condición en línea. Puede introducir el valor del elemento DD Gender utilizando:

   * Archivo de datos XML de ejemplo creado en función del diccionario de datos pertinente mientras se previsualiza la carta con datos de ejemplo.
   * Archivo de datos XML adjunto al diccionario de datos pertinente.

   Para obtener más información, consulte [Diccionario de datos](../../forms/using/data-dictionary.md).

   ![5_letteroutput](assets/5_letteroutput.png)

## Repetir {#repeat}

Es posible que tenga información dinámica en la Comunicación/carta interactiva, como transacciones en un extracto de tarjeta de crédito, cuya instancia o incidencia puede seguir cambiando con cada carta generada. Si utiliza repetir, puede dar formato y estructurar esa información dinámica en el fragmento del documento de texto.

Además, puede especificar la regla/condición dentro de la construcción repetida para condicionalizar la información/entradas que se representan en la comunicación/carta interactiva.

### Ejemplo: Uso de repetir en una comunicación interactiva para dar formato, estructurar y mostrar una lista de transacciones de tarjeta de crédito {#example-using-repeat-in-an-interactive-communication-to-format-structure-and-display-a-list-of-credit-card-transactions}

El siguiente ejemplo le muestra los pasos para utilizar repetir para estructurar y procesar las transacciones de tarjetas de crédito en una comunicación interactiva.

1. En un fragmento de documento basado en modelos de datos de formulario, inserte los objetos correspondientes del modelo de datos de formulario (y el texto incrustado requerido para las etiquetas, como en este ejemplo):

   ![1_elementstext](assets/1_elementstext.png)

   >[!NOTE]
   >
   >El contenido repetible debe incluir al menos una propiedad del tipo Collection.

1. Seleccione el contenido en el que desea aplicar la repetición.

   ![2_selection](assets/2_selection.png)

1. Toque Repetir.

   Aparecerá el cuadro de diálogo Repetir.

   ![3_repetidialog](assets/3_repeatdialog.png)

1. Seleccione Salto de línea como separador y, si es necesario, pulse Añadir condición para crear una regla. También puede utilizar el texto como separador y especificar los caracteres de texto que se utilizarán como separadores.

   Aparecerá el cuadro de diálogo Crear regla .

1. Cree una regla para mostrar las transacciones con fecha posterior al 28 de febrero de 2018 a fin de incluir las transacciones solo para el mes de marzo en la Comunicación interactiva.

   >[!NOTE]
   >
   >En este ejemplo se supone que el agente creará la instrucción a finales de marzo de 2018. De lo contrario, puede crear otra regla para incluir las transacciones anteriores a 2018-04-01 para excluir las transacciones posteriores a marzo de 2018.

   ![4_createral](assets/4_createrule.png)

1. Guarde la condición/regla y, a continuación, guarde la repetición. La repetición condicional se aplica al contenido seleccionado.

   ![5_onmouseoverconditionrule](assets/5_onmouseoverconditionrule.png)

   Al pasar el ratón por encima, el fragmento del documento de texto muestra la condición y el separador utilizados en la repetición aplicada al contenido.

1. Guarde el fragmento del documento de texto y previsualice la comunicación interactiva correspondiente. Según los datos del modelo de datos del formulario, la repetición aplicada a los elementos procesa los detalles de transacción de forma similar a los siguientes en la vista previa:

   ![screen_shot_2018-03-09at155516copy](assets/screen_shot_2018-03-09at155516copy.png)

### Ejemplo: Utilizar repetir en una carta para dar formato, estructurar y mostrar una lista de transacciones de tarjeta de crédito {#example-using-repeat-in-a-letter-to-format-structure-and-display-a-list-of-credit-card-transactions}

En el siguiente ejemplo se proporcionan los pasos para utilizar repetir para estructurar y procesar las transacciones de tarjetas de crédito en una carta. Con pasos similares, puede utilizar repetir en un escenario diferente.

1. Abra (mientras edita o crea) un módulo de texto que tenga elementos DD que procesen datos repetidos/dinámicos e incorporen el texto requerido alrededor de los elementos DD. Por ejemplo, un módulo de texto tiene los siguientes elementos DD para crear un estado de transacciones en una tarjeta de crédito:

   ```javascript
   {^DD_creditcard_TransactionDate^} {^DD_creditcard_TransactionAmount^}
   {^DD_creditcard_TransactionType^}
   ```

   Estos elementos DD presentan una lista de las transacciones realizadas en la tarjeta de crédito con la siguiente información:

   Fecha de transacción, Cantidad de transacción y Tipo de transacción (débito o crédito)

1. Incruste el texto dentro de los elementos DD para que la declaración sea más legible, como por ejemplo:

   ![1_repeat](assets/1_repeat.png)

   ```javascript
   Date: {^DD_creditcard_TransactionDate^} Amount (USD): {^DD_creditcard_TransactionAmount^} Transaction Type: {^DD_creditcard_TransactionType^}
   ```

   Sin embargo, el trabajo de renderizar una instrucción con buen formato aún no ha finalizado. Si procesa una carta basada en el trabajo realizado hasta el momento, aparece de la siguiente manera:

   ![1_1renderwithoutrepeat](assets/1_1renderwithoutrepeat.png)

   Para repetir el texto estático junto con los elementos DD, debe aplicar repetir como se explica en los pasos adicionales.

1. Seleccione el texto estático así como los elementos DD que desee repetir, como se muestra a continuación:

   ![2_repeat_selecttext](assets/2_repeat_selecttext.png)

1. Toque **Repetir**. El cuadro de diálogo Repetir aparece con una condición en línea vacía.

   ![3_repeat_dialog](assets/3_repeat_dialog.png)

1. Si es necesario, inserte una condición para procesar selectivamente las transacciones, como para representar importes de transacciones superiores a 50 centavos:

   ```javascript
   ${DD_creditcard_TransactionAmount > 0.5}
   ```

   De lo contrario, si no necesita procesar la información (aquí transacciones) de forma selectiva, mantenga la condición vacía eliminando lo siguiente en el cuadro de diálogo: `${}`. Guardar una expresión repetida se habilita cuando la ventana de expresiones repetidas está vacía (sin ${} cuando no se necesita repetir) o cuando contiene una condición válida para repetir.

1. Seleccione un separador para dar formato al texto dinámico y pulse la marca de verificación para guardar:

   * **Salto** de línea: Inserta un salto de línea después de cada entrada de transacción en la carta de salida.
   * **Texto**: Inserta el carácter de texto especificado después de cada entrada de transacción en la carta de salida.

   Una vez insertada la condición, el texto con repetición se resalta en rojo y aparece un controlador a la izquierda. Puede situarse sobre el controlador de la izquierda de la repetición para ver la construcción de repetición.

   ![4_Repeat_hoverdetail](assets/4_repeat_hoverdetail.png)

   Puede pulsar el control para ver el menú emergente de la repetición, que le permite editar o eliminar la construcción repetida.

   ![5_repetieditremove](assets/5_repeateditremove.png)

1. Previsualice la carta correspondiente y observe que el texto se representa según se repita. Puede introducir el valor de los elementos DD utilizando:

   * Archivo de datos XML de ejemplo creado en función del diccionario de datos pertinente mientras se previsualiza la carta con datos de ejemplo.
   * Archivo de datos XML adjunto al diccionario de datos pertinente.

   Para obtener más información, consulte [Diccionario de datos](https://helpx.adobe.com/aem-forms/6-2/data-dictionary.html).

   ![6_repetioutputpreview](assets/6_repeatoutputpreview.png)

   El texto estático se repite con los detalles de la transacción. La repetición de texto estático se facilita con la repetición aplicada al texto en este procedimiento. La condición, ${DD_creditcard_TransactionAmount > 0,5}, garantiza que las transacciones por debajo de USD .5 no se muestren en la carta.

   >[!NOTE]
   >
   >Puede insertar una condición y repetirla solo mientras crea o edita el módulo de texto correspondiente. Al previsualizar la carta, aunque puede realizar modificaciones en el módulo de texto, no puede insertar condición ni repetir.

## Uso de condiciones en línea y repetición - algunos casos de uso {#using-inline-condition-and-repeat-some-use-cases}

### Repetir dentro de la condición {#repeat-within-condition}

Es posible que deba utilizar repetir dentro de una condición. La gestión de correspondencia le permite utilizar la repetición dentro de una construcción de condiciones en línea.

Por ejemplo, a continuación se repite (con formato de rojo) dentro de una condición (con formato de verde).

Mientras que la repetición procesa las transacciones de tarjetas de crédito, la condición ${DD_creditcard_nooftransactions > 0} garantiza que la construcción repetida se represente solo si hay al menos una transacción.

![repetiwitincondition](assets/repeatwitincondition.png)

Del mismo modo, según sus necesidades, puede crear:

* Una o más condiciones dentro de una condición
* Una o más condiciones dentro de una repetición
* Combinación de condiciones y repetición dentro de una condición o repetición

### Condición en línea vacía {#empty-inline-condition}

Es posible que deba insertar condiciones en línea vacías e incrustar texto y elementos DD más adelante. La gestión de correspondencia le permite hacer eso.

![condición de vacío](assets/emptycondition.png)

Sin embargo, se recomienda que, si es posible, inserte primero el texto y los elementos DD en el módulo de texto con el formato deseado, como las viñetas, y aplique después una condición en línea.
