---
title: Condiciones de las comunicaciones interactivas
seo-title: Condiciones de las comunicaciones interactivas
description: 'Creación y edición de fragmentos de condición para su uso en Interactive Communications: la condición es uno de los cuatro tipos de fragmentos de documento utilizados para crear comunicaciones interactivas. Los otros tres son textos, listas y fragmentos de maquetación.'
seo-description: Creación y edición de condiciones para utilizar en Interactive Communications
uuid: c98f02d5-1769-46dd-ab35-6e8145a24939
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fe59d260-d392-4d6f-bb7e-2f2a1d701f51
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 0%

---


# Condiciones de Interactive Communications{#conditions-in-interactive-communications}

Creación y edición de fragmentos de condición para su uso en Interactive Communications: la condición es uno de los cuatro tipos de fragmentos de documento utilizados para crear comunicaciones interactivas. Los otros tres son textos, listas y fragmentos de maquetación.

## Información general {#overview}

Condición es un fragmento de documento que se puede incluir en una comunicación interactiva. Los demás fragmentos de documento son [texto](../../forms/using/texts-interactive-communications.md), lista y fragmento de diseño. Las condiciones permiten definir uno o varios recursos contextuales que se incluyen en una comunicación interactiva en función de los datos y las reglas suministrados.

Ejemplos:

* En un extracto de tarjeta de crédito, muestre la tarifa anual de la tarjeta de crédito y la imagen de la tarjeta de crédito en función del tipo de tarjeta de crédito del cliente.
* En un recordatorio de prima de seguro debida, se muestran cálculos de impuestos basados en los impuestos del estado del cliente.

Los recursos en las condiciones que se procesan según las reglas aplicadas y los valores pasados a la regla. Las reglas de las condiciones pueden comprobar los valores de los siguientes tipos de datos:

* Propiedad asociada del modelo de datos de formulario
* Todas las variables que cree en la condición
* Cadenas
* Números
* Expresiones matemáticas
* Fechas

## Crear condición {#createcondition}

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de Documento]**.
1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Condición]**.
1. Especifique la siguiente información:

   * **[!UICONTROL Título]**: (Opcional) Introduzca el título de la condición. Los títulos no tienen que ser únicos y pueden tener caracteres especiales y caracteres no ingleses. Las condiciones se remiten por sus títulos (cuando están disponibles), como en miniaturas y propiedades.
   * **[!UICONTROL Nombre]**: Nombre exclusivo de la condición, dentro de una carpeta. No pueden existir dos fragmentos de documento (texto, condición o lista) en ningún estado con el mismo nombre dentro de una carpeta. En el campo Nombre, solo puede introducir caracteres, números y guiones en inglés. El campo Nombre se rellena automáticamente según el campo Título. Los caracteres especiales, espacios, números y caracteres no ingleses introducidos en el campo Título se sustituyen por guiones en el campo Nombre. Aunque el valor del campo Título se copia automáticamente en el Nombre, puede editarlo.

   * **[!UICONTROL Descripción]**: Escriba una descripción del fragmento de documento.
   * **[!UICONTROL Modelo]** de datos de formulario: De forma opcional, seleccione el botón de opción Modelo de datos de formulario para crear la condición basada en un modelo de datos de formulario. Al seleccionar el botón de radio Modelo de datos de formulario, aparece el campo **[!UICONTROL Modelo de datos de formulario]**. Examine y seleccione un modelo de datos de formulario. Al crear una condición para una comunicación interactiva, asegúrese de utilizar el mismo modelo de datos que desea utilizar en la comunicación interactiva. Para obtener más información sobre el modelo de datos de formulario, consulte [Integración de datos](../../forms/using/data-integration.md).

   * **[!UICONTROL Etiquetas]**: De forma opcional, para crear una etiqueta personalizada, introduzca un valor en el campo de texto y toque Intro. Al guardar esta condición, se crean las etiquetas recientemente agregadas.

1. Toque **[!UICONTROL Siguiente]**.

   Aparece la página Crear condición.

   ![createcondition](assets/createcondition.png)

1. Toque **[!UICONTROL Añadir recursos]**.

   Aparece la página Seleccionar recursos y muestra los textos, listas, condiciones e imágenes disponibles para agregar en la condición.

   >[!NOTE]
   >
   >En la página Seleccionar recursos solo aparecen los recursos basados en FDM y los nuevos creados basados en ninguno (creados con el mismo FDM que la condición que se está creando).

1. Toque los recursos correspondientes para seleccionarlos para incluirlos en la condición y, a continuación, toque **[!UICONTROL Listo]**.

   Aparece la página Crear condición y lista los recursos agregados.

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   Puede utilizar las siguientes opciones para administrar recursos en una condición:

   ![createconditionscreenassetsadadenotated](assets/createconditionscreenassetsaddedannotated.png)

   **[] AReject Change.** Toque este icono para rechazar los cambios que haya realizado en el recurso y en la regla de la condición.
   **[Cambio de ] BAccept.** Toque este icono para aceptar los cambios realizados en el recurso y la regla de la condición.
   **[Recurso ] CDuplicate.** Toque este icono para crear una copia del recurso junto con la regla aplicada, si la hay, en la condición. A continuación, puede continuar editando la regla y el recurso para el recurso duplicado. Duplicar un recurso resulta útil para crear reglas similares que muestren recursos alternativos basados en un contexto concreto.
   **[previsualización ] DShow.** Toque este icono para mostrar una previsualización del recurso en la página Crear/Editar condición.
   **Reordenar &#39;servidor&#39;.** Mantenga pulsado este icono para arrastrar y soltar recursos para reordenarlos dentro de una condición.

   Puede seleccionar las siguientes opciones para especificar el comportamiento de la condición en tiempo de ejecución:

   * **Se deshabilitó la evaluación de varios resultados\Se habilitó** la evaluación de varios resultados: Cuando esta opción está habilitada (aparece como &quot;Evaluación de resultados múltiples habilitada&quot;), se evalúan todas las reglas y el resultado es la suma de todas las reglas verdaderas. Si esta opción está deshabilitada (aparece como &quot;Evaluación de resultados múltiples deshabilitada&quot;), solo se evalúa la primera regla que se encuentre como verdadera y se convierte en el resultado de la condición.

   * **Salto** de página: Seleccione esta opción ( ![salto](assets/break.png)) para agregar un salto de página entre los recursos de las condiciones. Cuando esta opción no está seleccionada ( ![nobreak](assets/nobreak.png)), si una condición se está desbordando a la página siguiente en la salida de impresión, toda la condición se pasa a la página siguiente en lugar de saltarse la página entre los recursos de la condición.

1. Toque **[!UICONTROL Crear regla]** para agregar reglas para mostrar u ocultar los recursos, según sea necesario. Para utilizar variables en las reglas, consulte [creación de variables](#variables). Para obtener más información, consulte [Añadir reglas a condición](#ruleeditor).

   Las reglas creadas aparecen en la columna REGLA de la pantalla Crear condición.

   ![createconditionscrelesadded](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >Puede insertar recursos en la condición que ya tengan reglas o que se repitan.

1. Toque **[!UICONTROL Guardar]**.

   Se crea la condición. Ahora puede usar la condición como un bloque de creación al crear una comunicación interactiva.

   >[!NOTE]
   >
   >Para guardar una condición nueva o editada, debe tener al menos una regla para cada uno de los recursos agregados en la condición.

## Editar una condición {#edit-a-condition}

Puede editar una condición siguiendo los pasos siguientes. También puede elegir editar una condición desde una comunicación interactiva seleccionando Editar fragmento en el menú emergente.

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos de Documento]**.
1. Vaya a la condición y selecciónela.
1. Toque **[!UICONTROL Editar]**.
1. Realice los cambios necesarios en la condición. Para obtener más información sobre la información que puede cambiar en una condición, consulte [Crear condición](#createcondition).
1. Toque **[!UICONTROL Guardar]** y luego toque **[!UICONTROL Cerrar]**.

## Crear reglas en condición {#ruleeditor}

Con el editor de reglas en una condición, puede crear reglas para mostrar u ocultar recursos en función de **condiciones preestablecidas**. Estas condiciones pueden construirse sobre la base de:

* Cadenas
* Números
* Expresiones matemáticas
* Fechas
* Propiedades del modelo de datos de formulario asociado
* Cualquier [variable](#variables) que pueda haber creado

### Crear regla en condición {#create-rule-in-condition}

1. Mientras crea o edita una condición, toque el icono ![ruleeditoricon](assets/ruleeditoricon.png) (Editor de reglas) para el recurso relevante.

   Aparecerá el cuadro de diálogo Crear regla. Además de la cadena, el número, la expresión matemática y la fecha, en el Editor de reglas también se encuentran disponibles las siguientes opciones para crear instrucciones de las reglas:

   * Propiedades del modelo de datos de formulario asociado
   * Cualquier [variable](#variables) que pueda haber creado.

   ![createruledialog](assets/createruledialog.png)

   Seleccione la opción adecuada para evaluar.

   >[!NOTE]
   >
   >La propiedad Collection no se admite para crear reglas para mostrar recursos.

1. Seleccione el operador apropiado para evaluar la regla, como Es igual a, Contiene y Inicios con.
1. Inserte la expresión, cadena, propiedad del modelo de datos, variable o fecha de evaluación.

   ![Regla para mostrar un recurso cuando el tipo de directiva es estándar](assets/ruleincondition.png)

   Regla para mostrar un recurso cuando el tipo de directiva es estándar

   * Al crear o editar una regla, también puede tocar ![icon_resize](assets/icon_resize.png) (Cambiar tamaño) para expandir el cuadro de diálogo Crear regla/Editar regla. El cuadro de diálogo ampliado de ventana completa le permite crear [variables](#variables) para construir reglas. Vuelva a tocar Cambiar tamaño para volver al cuadro de diálogo Crear regla.

   * También puede crear varias condiciones en una regla.

1. Puntee **[!UICONTROL Listo]**.

   La regla se aplica al recurso.

## Creación y uso de variables en una condición {#variables}

Al crear o editar una regla en una condición, puede tocar ![icon_resize](assets/icon_resize.png) (Cambiar tamaño) para expandir el cuadro de diálogo Crear regla\Editar regla. El cuadro de diálogo ampliado con ventana completa le permite:

* Crear y utilizar variables en la regla
* Arrastrar y soltar las propiedades y variables del modelo de datos de formulario en la regla

Vuelva a tocar Cambiar tamaño para volver al cuadro de diálogo Crear regla\Editar regla.

### Crear variables {#create-variables}

1. Al crear o editar una regla en una condición, puede tocar ![icon_resize](assets/icon_resize.png) (Cambiar tamaño) para expandir el cuadro de diálogo Crear regla\Editar regla.

   Aparece el cuadro de diálogo Ampliado y ventana completa.

   ![expandeditruledialog](assets/expandededitruledialog.png)

1. En el panel izquierdo, toque **[!UICONTROL Variables]**.

   Aparece el panel Variables.

   ![expandeditrulevariables](assets/expandededitrulevariables.png)

1. Toque **[!UICONTROL Crear]**.

   Aparece el panel Crear variables.

1. Introduzca la siguiente información y toque **[!UICONTROL Crear]**:

   * **[!UICONTROL Nombre]**: Nombre de la variable.
   * **[!UICONTROL Descripción]**: De forma opcional, introduzca una descripción de la variable.
   * **[!UICONTROL Tipo]**: Seleccione un tipo de variable: Cadena, Número, Booleano o Fecha.
   * **[!UICONTROL Permitir sólo]** valores específicos: En el caso de las variables String y Number, puede asegurarse de que el agente elige entre un conjunto específico de valores para un marcador de posición en la interfaz de usuario del agente. Para especificar el conjunto de valores, seleccione esta opción y, a continuación, especifique los valores separados por comas que se permiten en el campo **[!UICONTROL Valores]**.

1. Toque **[!UICONTROL Crear]**.

   La variable se crea y se enumera en el panel Variables.

1. Para insertar una variable en la regla, arrastre y suelte la variable en un marcador de posición para una opción de la regla.
1. Después de crear una regla válida, toque **[!UICONTROL Listo]**.

   Proceda a realizar más cambios, si es necesario, en la condición y guardarla.

