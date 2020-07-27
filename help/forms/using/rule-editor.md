---
title: Editor de reglas de formularios adaptables
seo-title: Editor de reglas de formularios adaptables
description: El editor de reglas de formularios adaptables permite agregar un comportamiento dinámico y generar una lógica compleja en los formularios sin necesidad de codificar ni utilizar secuencias de comandos.
seo-description: El editor de reglas de formularios adaptables permite agregar un comportamiento dinámico y generar una lógica compleja en los formularios sin necesidad de codificar ni utilizar secuencias de comandos.
uuid: c1b3d6e4-6f36-4352-ab57-9850d718e47c
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1b905e66-dc05-4f14-8025-62a78feef12a
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '6822'
ht-degree: 0%

---


# Editor de reglas de formularios adaptables{#adaptive-forms-rule-editor}

## Información general {#overview}

La función de editor de reglas de Adobe Experience Manager Forms permite a los usuarios y desarrolladores de formularios empresariales escribir reglas sobre objetos de formulario adaptables. Estas reglas definen acciones para activar objetos de formulario en función de condiciones preestablecidas, entradas de usuario y acciones de usuario en el formulario. Esto ayuda a optimizar aún más la experiencia de cumplimentación de formularios, asegurando la precisión y la velocidad.

El editor de reglas proporciona una interfaz de usuario intuitiva y simplificada para escribir reglas. El editor de reglas oferta un editor visual para todos los usuarios. Además, solo para usuarios con poder de formularios, el editor de reglas proporciona un editor de código para escribir reglas y secuencias de comandos. Algunas de las acciones clave que se pueden realizar con objetos de formulario adaptables mediante reglas son:

* Mostrar u ocultar un objeto
* Activar o desactivar un objeto
* Definición de un valor para un objeto
* Validar el valor de un objeto
* Ejecutar funciones para calcular el valor de un objeto
* Invocar un servicio de modelo de datos de formulario y realizar una operación
* Establecer propiedad de un objeto

El editor de reglas reemplaza las funciones de secuencias de comandos de AEM 6.1 Forms y versiones anteriores. Sin embargo, las secuencias de comandos existentes se conservan en el nuevo editor de reglas. Para obtener más información sobre cómo trabajar con secuencias de comandos existentes en el editor de reglas, consulte [Impacto del editor de reglas en secuencias de comandos](../../forms/using/rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p)existentes.

Los usuarios agregados al grupo de usuarios avanzados de formularios pueden crear nuevas secuencias de comandos y editar las existentes. Los usuarios del grupo de usuarios de formularios pueden utilizar las secuencias de comandos, pero no crearlas ni editarlas.

## Explicación de una regla {#understanding-a-rule}

Una regla es una combinación de acciones y condiciones. En el editor de reglas, las acciones incluyen actividades como ocultar, mostrar, habilitar, deshabilitar o calcular el valor de un objeto en un formulario. Las condiciones son expresiones booleanas que se evalúan realizando comprobaciones y operaciones en el estado, valor o propiedad de un objeto de formulario. Las acciones se realizan en función del valor ( `True` o `False`) devuelto mediante la evaluación de una condición.

El editor de reglas proporciona un conjunto de tipos de reglas predefinidos, como Cuándo, Mostrar, Ocultar, Habilitar, Deshabilitar, Definir valor de y Validar, para ayudarle a escribir reglas. Cada tipo de regla permite definir condiciones y acciones en una regla. El documento explica cada tipo de regla en detalle.

Una regla suele seguir una de las siguientes construcciones:

**Condición-Acción** En esta construcción, una regla primero define una condición seguida de una acción para activar. La construcción es comparable a la afirmación if-then en lenguajes de programación.

En el editor de reglas, el tipo de regla **Cuándo** fuerza la construcción de condición-acción.

**Condición** de acción En esta construcción, una regla primero define una acción que se activará seguida de condiciones para la evaluación. Otra variación de esta construcción es la acción alternativa-condición-acción, que también define una acción alternativa para activar si la condición devuelve False.

Los tipos de reglas Mostrar, Ocultar, Activar, Deshabilitar, Definir valor de y Validar del editor de reglas refuerzan la creación de reglas de condición de acción. De forma predeterminada, la acción alternativa para Mostrar es Ocultar y Activar es Deshabilitar, y viceversa. No se puede cambiar la acción alternativa predeterminada.

>[!NOTE]
>
>Los tipos de reglas disponibles, incluidas las condiciones y acciones que se definen en el editor de reglas, también dependen del tipo de objeto de formulario en el que se esté creando una regla. El editor de reglas solo muestra tipos de reglas y opciones válidos para escribir afirmaciones de condiciones y acciones para un tipo de objeto de formulario concreto. Por ejemplo, no se ven los tipos de reglas Validar, Definir valor de, Habilitar y Deshabilitar para un objeto de panel.

Para obtener más información sobre los tipos de reglas disponibles en el editor de reglas, consulte Tipos de reglas [disponibles en el editor](../../forms/using/rule-editor.md#p-available-rule-types-in-rule-editor-p)de reglas.

### Pautas para elegir una construcción de regla {#guidelines-for-choosing-a-rule-construct}

Aunque puede lograr la mayoría de los casos de uso utilizando cualquier construcción de regla, a continuación se presentan algunas directrices para elegir una construcción por encima de otra. Para obtener más información sobre las reglas disponibles en el editor de reglas, consulte Tipos de reglas [disponibles en el editor](../../forms/using/rule-editor.md#p-available-rule-types-in-rule-editor-p)de reglas.

* Una regla normal de la miniatura al crear una regla es pensarla en el contexto del objeto en el que se escribe una regla. Considere que desea ocultar o mostrar el campo B en función del valor especificado por un usuario en el campo A. En este caso, está evaluando una condición en el campo A y, en función del valor que devuelve, está activando una acción en el campo B.

   Por lo tanto, si está escribiendo una regla en el campo B (el objeto en el que está evaluando una condición), utilice la construcción de condición-acción o el tipo de regla Cuándo. Del mismo modo, utilice la construcción de condición de acción o Mostrar u Ocultar tipo de regla en el campo A.

* A veces, es necesario realizar varias acciones en función de una condición. En estos casos, se recomienda utilizar la construcción de condición-acción. En esta construcción, puede evaluar una condición una vez y especificar varias sentencias de acción.

   Por ejemplo, para ocultar los campos B, C y D en función de la condición que comprueba el valor especificado por un usuario en el campo A, escriba una regla con la creación de condición-acción o Cuando el tipo de regla en el campo A y especifique acciones para controlar la visibilidad de los campos B, C y D. De lo contrario, necesita tres reglas independientes en los campos B, C y D, donde cada regla comprueba la condición y muestra u oculta el campo correspondiente. En este ejemplo, es más eficaz escribir el tipo de regla Cuándo en un objeto en lugar de Mostrar u Ocultar tipo de regla en tres objetos.

* Para desencadenar una acción basada en varias condiciones, se recomienda utilizar la construcción de condición de acción. Por ejemplo, para mostrar y ocultar el campo A mediante la evaluación de condiciones en los campos B, C y D, utilice Mostrar u Ocultar tipo de regla en el campo A.
* Utilice la construcción de condición-acción o condición de acción si la regla contiene una acción para una condición.
* Si una regla comprueba la existencia de una condición y realiza una acción inmediatamente después de proporcionar un valor en un campo o de salir de un campo, se recomienda escribir una regla con la construcción de acción-condición o el tipo de regla Cuándo en el campo en el que se evalúa la condición.
* La condición de la regla Cuándo se evalúa cuando un usuario cambia el valor del objeto en el que se aplica la regla Cuándo. Sin embargo, si desea que la acción se active cuando el valor cambie en el servidor, como en el caso de rellenar previamente el valor, se recomienda escribir una regla de Cuándo que active la acción cuando se inicialice el campo.
* Al escribir reglas para objetos de listas desplegables, botones de opción o casillas de verificación, las opciones o valores de estos objetos de formulario en el formulario se rellenan previamente en el editor de reglas.

## Tipos de operadores y eventos disponibles en el editor de reglas {#available-operator-types-and-events-in-rule-editor}

El editor de reglas proporciona los siguientes operadores lógicos y eventos mediante los cuales puede crear reglas.

* **Es igual a**
* **No es igual a**
* **Inicios con**
* **Termina con**
* **Contiene**
* **Is Empty**
* **Is Not Empty**
* **Ha seleccionado:** Devuelve true cuando el usuario selecciona una opción concreta para un botón de opción, desplegable o de casilla de verificación.
* **Se Inicializa (evento):** Devuelve true cuando un objeto de formulario se procesa en el explorador.
* **Se ha cambiado (evento):** Devuelve true cuando el usuario cambia el valor introducido o la opción seleccionada para un objeto de formulario.

## Tipos de reglas disponibles en el editor de reglas {#available-rule-types-in-rule-editor}

El editor de reglas proporciona un conjunto de tipos de reglas predefinidos que puede utilizar para escribir reglas. Veamos cada tipo de regla en detalle. Para obtener más información sobre la escritura de reglas en el editor de reglas, consulte [Escribir reglas](../../forms/using/rule-editor.md#p-write-rules-p).

### Cuando {#whenruletype}

El tipo de regla **Cuándo** sigue la construcción de regla de acción **alternativa-acción-** condición o, a veces, solo la construcción de **condición-acción** . En este tipo de regla, primero debe especificar una condición para la evaluación seguida de una acción para activar si se cumple la condición ( `True`). Al utilizar el tipo de regla Cuándo, puede utilizar varios operadores Y y O para crear expresiones [](#nestedexpressions)anidadas.

Con el tipo de regla Cuándo, puede evaluar una condición en un objeto de formulario y realizar acciones en uno o varios objetos.

En palabras simples, una regla Cuándo típica está estructurada de la siguiente manera:

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

Acción 2 sobre el objeto B;
ANDAction 3 sobre el objeto C;

_

Cuando tiene un componente de varios valores, como botones de opción o lista, mientras crea una regla para ese componente, las opciones se recuperan automáticamente y se ponen a disposición del creador de reglas. No es necesario volver a escribir los valores de la opción.

Por ejemplo, una lista tiene cuatro opciones: Rojo, Azul, Verde y Amarillo. Al crear la regla, las opciones (botones de opción) se recuperan automáticamente y se ponen a disposición del creador de reglas de la siguiente manera:

![multivaluefcdisplaysoptions](assets/multivaluefcdisplaysoptions.png)

Al escribir una regla de Cuándo, puede activar la acción Borrar valor de acción. Borrar valor de acción borra el valor del objeto especificado. La opción Tener un valor claro de como en la instrucción When le permite crear condiciones complejas con varios campos.

![clearValue de](assets/clearvalueof.png)

**Ocultar** Oculta el objeto especificado.

**Mostrar** Muestra el objeto especificado.

**Habilitar** Habilita el objeto especificado.

**Deshabilitar** Deshabilita el objeto especificado.

**Invocar servicio** Invoca un servicio configurado en un modelo de datos de formulario. Al elegir la operación Invocar servicio, aparece un campo. Al tocar el campo, se muestran todos los servicios configurados en todos los modelos de datos de formulario de la instancia de AEM. Al elegir un servicio de modelo de datos de formulario, aparecen campos adicionales en los que se pueden asignar objetos de formulario con parámetros de entrada y salida para el servicio especificado. Consulte la regla de ejemplo para invocar servicios del modelo de datos de formulario.

Además del servicio de modelo de datos de formulario, puede especificar una URL WSDL directa para invocar un servicio Web. Sin embargo, un servicio de modelo de datos de formulario tiene muchas ventajas y el método recomendado para invocar un servicio.

Para obtener más información sobre la configuración de servicios en el modelo de datos de formulario, consulte Integración [de datos de](/help/forms/using/data-integration.md)AEM Forms.

**Establezca el valor de Calcula y establece el valor del** objeto especificado. Puede establecer el valor del objeto en una cadena, el valor de otro objeto, el valor calculado mediante una expresión o función matemática, el valor de una propiedad de un objeto o el valor de salida de un servicio de modelo de datos de formulario configurado. Al elegir la opción de servicio Web, se muestran todos los servicios configurados en todos los modelos de datos de formulario de la instancia de AEM. Al elegir un servicio de modelo de datos de formulario, aparecen campos adicionales en los que se pueden asignar objetos de formulario con parámetros de entrada y salida para el servicio especificado.

Para obtener más información sobre la configuración de servicios en el modelo de datos de formulario, consulte Integración [de datos de](/help/forms/using/data-integration.md)AEM Forms.

El tipo de regla **Set Property** permite establecer el valor de una propiedad del objeto especificado basándose en una acción de condición.

Permite definir reglas para agregar casillas de verificación dinámicamente al formulario adaptable. Puede utilizar una función personalizada, un objeto de formulario o una propiedad de objeto para definir una regla.

![Configurar propiedad](assets/set_property_rule_new.png)

Para definir una regla basada en una función personalizada, seleccione Salida **de** función en la lista desplegable y arrastre y suelte una función personalizada desde la ficha **Funciones** . Si se cumple la acción de condición, se agrega al formulario adaptable el número de casillas de verificación definidas en la función personalizada.

Para definir una regla basada en un objeto de formulario, seleccione Objeto **de formulario** en la lista desplegable y arrastre y suelte un objeto de formulario desde la ficha Objetos **de** formulario. Si se cumple la acción de condición, se agrega al formulario adaptable el número de casillas de verificación definidas en el objeto de formulario.

Una regla Set Property basada en una propiedad object permite agregar el número de casillas de verificación en un formulario adaptable basado en otra propiedad de objeto incluida en el formulario adaptable.

En la siguiente figura se muestra un ejemplo de cómo agregar casillas de verificación dinámicamente en función del número de listas desplegables del formulario adaptable:

![Propiedad de objeto](assets/object_property_set_property_new.png)

**Borrar valor de borra** el valor del objeto especificado.

**Definir el enfoque** de los conjuntos de enfoque en el objeto especificado.

**Guardar formulario** Guarda el formulario.

**Enviar formulario** Envía el formulario.

**Restablecer formulario** Restablece el formulario.

**Validar formulario** Valida el formulario.

**Añadir instancia** Añade una instancia del panel repetible o la fila de tabla especificados.

**Quitar instancia** Quita una instancia del panel repetible o la fila de tabla especificados.

**Vaya a** Navega a otras comunicaciones interactivas, formularios adaptables, otros recursos, como imágenes o fragmentos de documento, o a una dirección URL externa. Para obtener más información, consulte el botón [Añadir a la comunicación](../../forms/using/create-interactive-communication.md#addbuttontothewebchannel)interactiva.

### Valor definido de {#set-value-of}

El valor **[!UICONTROL definido del]** tipo de regla permite definir el valor de un objeto de formulario en función de si la condición especificada se cumple o no. El valor se puede establecer en un valor de otro objeto, una cadena literal, un valor derivado de una expresión matemática o una función, un valor de una propiedad de otro objeto o el resultado de un servicio de modelo de datos de formulario. Del mismo modo, puede comprobar si hay una condición en un componente, una cadena, una propiedad o valores derivados de una función o una expresión matemática.

Tenga en cuenta que el tipo de regla Definir valor de no está disponible para todos los objetos de formulario, como paneles y botones de la barra de herramientas. Una regla de valor de conjunto estándar tiene la siguiente estructura:



Definir el valor del objeto A como:

(cadena ABC) OR(propiedad de objeto X del objeto C) OR (valor de una función) OR (valor de una expresión matemática) OR (valor de salida de un servicio de modelo de datos o servicio Web);

Cuando (opcional):

(Condición 1 Y Condición 2 Y Condición 3) es TRUE;



El ejemplo siguiente toma el valor del `dependentid` campo como entrada y establece el valor del `Relation` campo en el resultado del `Relation` argumento del servicio del modelo de datos del `getDependent` formulario.

![set-value-web-service](assets/set-value-web-service.png)

Ejemplo de regla de valor establecido con el servicio de modelo de datos de formulario

>[!NOTE]
>
>Además, puede utilizar Definir valor de regla para rellenar todos los valores de un componente de lista desplegable desde el resultado de un servicio de modelo de datos de formulario o un servicio Web. Sin embargo, asegúrese de que el argumento de salida que elija sea de un tipo de matriz. Todos los valores devueltos en una matriz estarán disponibles en la lista desplegable especificada.

### Mostrar {#show}

Con el tipo de regla **Mostrar** , puede escribir una regla para mostrar u ocultar un objeto de formulario en función de si una condición se cumple o no. El tipo de regla Mostrar también activa la acción Ocultar en caso de que la condición no se cumpla o devuelva `False`.

Una regla Mostrar típica está estructurada de la siguiente manera:



`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`



### Ocultar {#hide}

De forma similar al tipo de regla Mostrar, puede utilizar el tipo de regla **Ocultar** para mostrar u ocultar un objeto de formulario en función de si una condición se cumple o no. El tipo de regla Ocultar también activa la acción Mostrar en caso de que la condición no se cumpla o devuelva `False`.

Una regla de Ocultar típica está estructurada de la siguiente manera:



`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`



### Habilitar {#enable}

El tipo de regla **Habilitar** permite habilitar o deshabilitar un objeto de formulario en función de si una condición se cumple o no. El tipo de regla Habilitar también activa la acción Deshabilitar en caso de que la condición no se cumpla o se devuelva `False`.

Una regla Habilitar típica está estructurada de la siguiente manera:



`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`



### Desactivar {#disable}

De forma similar al tipo de regla Habilitar, el tipo de regla **Deshabilitar** permite habilitar o deshabilitar un objeto de formulario en función de si una condición se cumple o no. El tipo de regla Deshabilitar también activa la acción Habilitar en caso de que la condición no se cumpla o se devuelva `False`.

Una regla de desactivación típica está estructurada de la siguiente manera:



`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### Validar {#validate}

El tipo de regla **Validar** valida el valor de un campo mediante una expresión. Por ejemplo, puede escribir una expresión para comprobar que el cuadro de texto para especificar el nombre no contenga caracteres o números especiales.

Una regla de validación típica está estructurada de la siguiente manera:

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>Si el valor especificado no cumple la regla Validar, puede mostrar un mensaje de validación al usuario. Puede especificar el mensaje en el campo Mensaje **[!UICONTROL de validación de]** secuencia de comandos de las propiedades de componente de la barra lateral.

![script-validation](assets/script-validation.png)

### Set Options Of {#setoptionsof}

El tipo **Definir opciones del** tipo de regla permite definir reglas para agregar casillas de verificación dinámicamente al formulario adaptable. Puede utilizar un modelo de datos de formulario o una función personalizada para definir la regla.

Para definir una regla basada en una función personalizada, seleccione Salida **de** función en la lista desplegable y arrastre y suelte una función personalizada desde la ficha **Funciones** . El número de casillas de verificación definidas en la función personalizada se agregan al formulario adaptable.

![Funciones personalizadas](assets/custom_functions_set_options_new.png)

Para crear una función personalizada, consulte Funciones [personalizadas en el editor](#custom-functions)de reglas.

Para definir una regla basada en un modelo de datos de formulario:

1. Seleccione Salida **de servicio** en la lista desplegable.
1. Seleccione el objeto del modelo de datos.
1. Seleccione una propiedad de objeto de modelo de datos en la lista desplegable **Mostrar valor** . El número de casillas de verificación del formulario adaptable se deriva del número de instancias definidas para esa propiedad en la base de datos.
1. Seleccione una propiedad de objeto de modelo de datos en la lista desplegable **Guardar valor** .

![Opciones de conjunto FDM](assets/fdm_set_options_new.png)

## Explicación de la interfaz de usuario del editor de reglas {#understanding-the-rule-editor-user-interface}

El editor de reglas proporciona una interfaz de usuario completa y sencilla para escribir y administrar reglas. Puede iniciar la interfaz de usuario del editor de reglas desde un formulario adaptable en modo de creación.

Para iniciar la interfaz de usuario del editor de reglas:

1. Abra un formulario adaptable en modo de creación.
1. Toque el objeto de formulario para el que desea escribir una regla y, en la barra de herramientas de componentes, toque ![edit-rules](assets/edit-rules.png). Aparece la interfaz de usuario del editor de reglas.

   ![create-rules](assets/create-rules.png)

   Todas las reglas existentes en los objetos de formulario seleccionados se muestran en esta vista. Para obtener información sobre la administración de reglas existentes, consulte [Administrar reglas](../../forms/using/rule-editor.md#p-manage-rules-p).

1. Toque **[!UICONTROL Crear]** para escribir una nueva regla. El editor visual de la interfaz de usuario del editor de reglas se abre de forma predeterminada cuando se inicia el editor de reglas por primera vez.
[ IU ![del editor de reglas](assets/rule-editor-ui.png)

   Haga clic para vista de la imagen ampliada

   ](assets/rule-editor-ui-1.png)Observemos en detalle cada componente de la interfaz de usuario del editor de reglas.

### A. Pantalla de regla de componente {#a-component-rule-display}

Muestra el título del objeto de formulario adaptable a través del cual se ha iniciado el editor de reglas y el tipo de regla seleccionado actualmente. En el ejemplo anterior, el editor de reglas se inicia desde un objeto de formulario adaptable denominado Salario y el tipo de regla seleccionado es Cuándo.

### B. Form objects and functions {#b-form-objects-and-functions-br}

El panel de la izquierda en la interfaz de usuario del editor de reglas incluye dos fichas: **[!UICONTROL Objetos]** y **[!UICONTROL funciones]** de formulario.

La ficha Objetos de formulario muestra una vista jerárquica de todos los objetos contenidos en el formulario adaptable. Muestra el título y el tipo de los objetos. Al escribir una regla, puede arrastrar y soltar objetos de formulario en el editor de reglas. Al crear o editar una regla cuando arrastra y suelta un objeto o función en un marcador de posición, el marcador de posición toma automáticamente el tipo de valor adecuado.

Los objetos de formulario que tienen una o varias reglas válidas aplicadas se marcan con un punto verde. Si alguna de las reglas aplicadas a un objeto de formulario no es válida, el objeto de formulario se marca con un punto amarillo.

La ficha Funciones incluye un conjunto de funciones integradas, como Suma de, Mínimo de, Máx de, Media de, Número de y Validar formulario. Puede utilizar estas funciones para calcular valores en paneles repetitivos y filas de tabla y usarlos en instrucciones de acción y condición al escribir reglas. Sin embargo, también puede crear funciones [](#custom-functions) personalizadas.

![Ficha Funciones](assets/functions.png)

>[!NOTE]
>
>Puede realizar búsquedas de texto en los nombres y títulos de objetos y funciones en las fichas Objetos y funciones de formulario.

En el árbol izquierdo de los objetos de formulario, puede tocar los objetos de formulario para mostrar las reglas aplicadas a cada uno de los objetos. No sólo puede desplazarse por las reglas de los distintos objetos de formulario, sino que también puede copiar y pegar reglas entre los objetos de formulario. Para obtener más información, consulte [Copiar y pegar reglas](../../forms/using/rule-editor.md#p-copy-paste-rules-p).

### C. Alternar objetos y funciones de formulario {#c-form-objects-and-functions-toggle-br}

Al tocar el botón de alternancia, se alternan los objetos de formulario y el panel de funciones.

### D. Editor de reglas visuales {#d-visual-rule-editor}

El editor de reglas visuales es el área en el modo de editor visual de la interfaz de usuario del editor de reglas donde se escriben las reglas. Le permite seleccionar un tipo de regla y definir las condiciones y las acciones correspondientes. Al definir condiciones y acciones en una regla, puede arrastrar y soltar objetos y funciones de formulario desde el panel Objetos y funciones de formulario.

Para obtener más información sobre el uso del editor de reglas visuales, consulte [Escribir reglas](../../forms/using/rule-editor.md#p-write-rules-p).

### E. Conmutador de editores de código visual {#e-visual-code-editors-switcher}

Los usuarios del grupo de usuarios avanzados de formularios pueden acceder al editor de código. Para otros usuarios, el editor de código no está disponible. Si tiene los derechos, puede cambiar del modo de editor visual al modo de editor de código del editor de reglas, y viceversa, con el conmutador situado justo encima del editor de reglas. Cuando se inicia el editor de reglas por primera vez, se abre en el modo de editor visual. Puede escribir reglas en el modo de editor visual o cambiar al modo de editor de código para escribir una secuencia de comandos de regla. Sin embargo, tenga en cuenta que si modifica una regla o escribe una regla en el editor de código, no podrá volver al editor visual de esa regla a menos que borre el editor de código.

Los AEM Forms realizan el seguimiento del modo de editor de reglas utilizado por última vez para escribir una regla. Cuando inicie el editor de reglas la próxima vez, se abrirá en ese modo. Sin embargo, también puede configurar un modo predeterminado para abrir el editor de reglas en el modo especificado. Para ello:

1. Vaya a la consola web de AEM en `https://[host]:[port]/system/console/configMgr`.
1. Haga clic para editar el servicio **[!UICONTROL de configuración de formularios]** adaptables.
1. seleccione Editor **** visual o Editor **** de código en la lista desplegable Modo **[!UICONTROL predeterminado para el editor]** de reglas

1. Haga clic en **[!UICONTROL Guardar]**.

### F. Botones Listo y Cancelar {#f-done-and-cancel-buttons}

El botón **[!UICONTROL Listo]** se utiliza para guardar una regla. Puede guardar una regla incompleta. Sin embargo, los incompletos no son válidos y no se ejecutan. Las reglas guardadas en un objeto de formulario se enumeran cuando se inicia el editor de reglas la próxima vez desde el mismo objeto de formulario. Puede administrar las reglas existentes en esa vista. Para obtener más información, consulte [Administrar reglas](../../forms/using/rule-editor.md#p-manage-rules-p).

El botón **[!UICONTROL Cancelar]** descarta los cambios realizados en una regla y cierra el editor de reglas.

## Reglas de escritura {#write-rules}

Puede escribir reglas mediante el editor de reglas visuales o el editor de código. Cuando se inicia el editor de reglas por primera vez, se abre en el modo de editor visual. Puede cambiar al modo de editor de código y escribir reglas. Sin embargo, tenga en cuenta que si escribe o modifica una regla en el editor de código, no puede cambiar al editor visual de esa regla a menos que borre el editor de código. Cuando inicie el editor de reglas la próxima vez, se abrirá en el modo que utilizó por última vez para crear la regla.

Analicemos primero cómo escribir reglas con un editor visual.

### Uso del editor visual {#using-visual-editor}

Vamos a comprender cómo crear una regla en un editor visual utilizando el siguiente formulario de ejemplo.

![create-rule-example](assets/create-rule-example.png)

La sección Requisitos de préstamo del formulario de solicitud de préstamo de ejemplo requiere que los solicitantes especifiquen su estado civil, su salario y, si están casados, el salario de su cónyuge. En función de las entradas del usuario, la regla calcula el importe de elegibilidad del préstamo y se muestra en el campo Elegibilidad del préstamo. Aplique las siguientes reglas para implementar el escenario:

* El campo Salario del cónyuge se muestra únicamente cuando el estado civil está casado.
* El monto de elegibilidad del préstamo es el 50% del salario total.

Realice los siguientes pasos para escribir reglas:

1. En primer lugar, escriba la regla para controlar la visibilidad del campo Salario del cónyuge en función de la opción que seleccione el usuario para el botón de opción Estado civil.

   Abra el formulario de solicitud de préstamo en modo de creación. Toque el componente Estado **** civil y ![edite las reglas](assets/edit-rules.png). A continuación, toque **[!UICONTROL Crear]** para iniciar el editor de reglas.

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   Al iniciar el editor de reglas, la regla Cuándo se selecciona de forma predeterminada. Además, el objeto de formulario (en este caso, Estado civil) desde el que se inició el editor de reglas se especifica en la instrucción When.

   Aunque no puede cambiar ni modificar el objeto seleccionado, puede utilizar la lista desplegable de reglas, como se muestra a continuación, para seleccionar otro tipo de regla. Si desea crear una regla en otro objeto, toque Cancelar para salir del editor de reglas y volver a iniciarla desde el objeto de formulario deseado.

1. Toque **[!UICONTROL Seleccionar estado]** en la lista desplegable y seleccione **[!UICONTROL es igual]**. Aparece el campo **[!UICONTROL Ingrese una cadena]** .

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   En el botón de radio Estado civil, las opciones **Casado** y **Soltero** se asignan a los valores **0** y **1** , respectivamente. Puede verificar los valores asignados en la ficha Título del cuadro de diálogo Editar botón de radio, como se muestra a continuación.

   ![Valores del botón de radio del editor de reglas](assets/radio-button-values.png)

1. En el campo **Introduzca una cadena** en la regla, especifique **0**.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   Ha definido la condición como `When Marital Status is equal to Married`. A continuación, defina la acción que se realizará si esta condición es True.

1. En la instrucción Entonces, seleccione **[!UICONTROL Mostrar]** en la lista desplegable **[!UICONTROL Seleccionar acción]** .

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. Arrastre y suelte el campo **Salario** del cónyuge desde la ficha Objetos de formulario del objeto **Colocar o seleccione aquí** . También puede tocar el objeto **Colocar o seleccionar aquí** y seleccionar el campo **Salario** del cónyuge en el menú emergente, que lista todos los objetos de formulario del formulario.

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   La regla aparece de la siguiente manera en el editor de reglas.

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

   Toque **Hecho** para guardar la regla.

1. Repita los pasos del 1 al 5 para definir otra regla que oculte el campo Salario del cónyuge si el estado civil es único. La regla aparece de la siguiente manera en el editor de reglas.

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >También puede escribir una regla Mostrar en el campo Salario del cónyuge, en lugar de dos reglas Cuándo en el campo Estado civil, para implementar el mismo comportamiento.

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. A continuación, escriba una regla para calcular el importe de elegibilidad del préstamo, que es el 50 % del salario total, y muéstrela en el campo Elegibilidad del préstamo. Para conseguirlo, cree **Establecer valor de las** reglas en el campo Elegibilidad de préstamo.

   En el modo de creación, toque el campo **[!UICONTROL Préstamo elegibilidad]** y ![edite las reglas](assets/edit-rules.png). A continuación, toque **[!UICONTROL Crear]** para iniciar el editor de reglas.

1. Seleccione **[!UICONTROL Definir valor de la regla desde]** la lista desplegable de reglas.

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. Toque **[!UICONTROL Seleccionar opción]** y seleccione Expresión **** matemática. Se abre un campo para escribir expresión matemática.

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. En el campo expresión:

   * Seleccione o arrastre y suelte desde la ficha Objeto de formulario el campo **Salario** del primer objeto **Colocar o seleccione aquí** .

   * Seleccione **Plus** en el campo **Seleccionar operador** .

   * Seleccione o arrastre y suelte desde la ficha Objeto de formulario el campo **Salario** del cónyuge del otro objeto **Colocar o seleccione aquí** .

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. A continuación, toque el área resaltada alrededor del campo de expresión y **Ampliar Expresión**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   En el campo expresión extendida, seleccione **dividido por** en el campo **Seleccionar operador** y **Número** del campo **Seleccionar opción** . A continuación, especifique **2** en el campo de número.

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >Puede crear expresiones complejas utilizando componentes, funciones, expresiones matemáticas y valores de propiedades desde el campo Seleccionar opción.

   A continuación, cree una condición que, cuando devuelva True, se ejecute la expresión.

1. Toque **Añadir condición** para agregar una instrucción When.

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   En la instrucción When:

   * Seleccione o arrastre y suelte desde la ficha Objeto de formulario el campo Estado **** civil del primer objeto **Colocar o seleccione aquí** .

   * Seleccionar **es igual** que en el campo **Seleccionar operador** .

   * Seleccione Cadena en el otro objeto **Colocar o seleccione aquí** y especifique **Casado** en el campo **Introducir una cadena** .

   La regla finalmente aparece como sigue en el editor de reglas.  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

   Toque **Hecho** para guardar la regla.

1. Repita los pasos del 7 al 12 para definir otra regla a fin de calcular la elegibilidad del préstamo si el estado civil es único. La regla aparece de la siguiente manera en el editor de reglas.

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>También puede utilizar la regla Definir valor de para calcular la elegibilidad del préstamo en la regla Cuándo que ha creado para mostrar y ocultar el campo Salario del cónyuge. La regla combinada resultante cuando Estado civil es único aparece de la siguiente manera en el editor de reglas.
>
>De manera similar, puede escribir una regla combinada para controlar la visibilidad del campo Salario del cónyuge y calcular la elegibilidad del préstamo cuando el Estado civil está casado.

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18.png)

### Uso del editor de código {#using-code-editor}

Los usuarios agregados al grupo de usuarios avanzados de formularios pueden utilizar el editor de código. El editor de reglas genera automáticamente el código JavaScript para cualquier regla que cree con el editor visual. Puede cambiar del editor visual al editor de código para la vista del código generado. Sin embargo, si modifica el código de regla en el editor de código, no podrá volver al editor visual. Si prefiere escribir reglas en un editor de código en lugar de en un editor visual, puede escribir reglas de nuevo en el editor de código. El conmutador de editores de código visual le ayuda a cambiar entre los dos modos.

JavaScript, editor de código, es el lenguaje de expresión de los formularios adaptables. Todas las expresiones son expresiones JavaScript válidas y utilizan API de modelos de secuencias de comandos de formularios adaptables. Estas expresiones devuelven valores de ciertos tipos. Para obtener la lista completa de clases de formularios adaptables, eventos, objetos y API públicas, consulte Referencia de la API de la biblioteca [JavaScript para formularios](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html)adaptables.

Para obtener más información sobre las directrices para escribir reglas en el editor de código, consulte Expresiones [de formularios](/help/forms/using/adaptive-form-expressions.md)adaptables.

Al escribir código JavaScript en el editor de reglas, las siguientes indicaciones visuales le ayudan con la estructura y la sintaxis:

* Resaltado de sintaxis
* Sangría automática
* Sugerencias y sugerencias para objetos, funciones y sus propiedades de formulario
* Finalización automática de los nombres de componentes de formulario y funciones comunes de JavaScript

![javascriptruleeditor](assets/javascriptruleeditor.png)

#### Funciones personalizadas en el editor de reglas {#custom-functions}

Aparte de las funciones integradas como *Suma de las* que se enumeran en Resultados de funciones, puede escribir funciones personalizadas que necesite con frecuencia. Asegúrese de que la función que escribe vaya acompañada de la `jsdoc` anterior.

Se `jsdoc` requiere la acompañamiento:

* Si desea una configuración y una descripción personalizadas.
* Debido a que hay varias formas de declarar una función en `JavaScript,` y los comentarios le permiten realizar un seguimiento de las funciones.

For more information, see [usejsdoc.org](https://usejsdoc.org/).

Etiquetas `jsdoc` admitidas:

* **Sintaxis privada**: 
Una función privada no se incluye como función personalizada.`@private`
Una función privada no se incluye como función personalizada.

* **Sintaxis del nombre**: 
También `@name funcName <Function Name>`puede `,` utilizar: `@function funcName <Function Name>` **o** `@func` `funcName <Function Name>`.
   `funcName` es el nombre de la función (no se permiten espacios).
   `<Function Name>` es el nombre para mostrar de la función.

* **Sintaxis del miembro**: 
Adjunta una Área de nombres a la función.`@memberof namespace`
Adjunta una Área de nombres a la función.

* **Sintaxis del parámetro**: 
También puede utilizar: `@param {type} name <Parameter Description>`
También puede utilizar: `@argument` `{type} name <Parameter Description>` **o** `@arg` `{type}` `name <Parameter Description>`.
Muestra los parámetros utilizados por la función. Una función puede tener varias etiquetas de parámetros, una etiqueta para cada parámetro en el orden de incidencia.
   `{type}` representa el tipo de parámetro. Los tipos de parámetro permitidos son:

   1. Cadena
   1. número
   1. boolean

   Todos los demás tipos de parámetros se categorizan bajo uno de los anteriores. No se admite ninguno. Asegúrese de seleccionar uno de los tipos anteriores. Los tipos no distinguen entre mayúsculas y minúsculas. No se permiten espacios en el parámetro `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **Sintaxis del tipo**de devolución: 
Como alternativa, puede usar `@return {type}`como opción `@returns {type}`.
Añade información sobre la función, como su objetivo.
{type} representa el tipo de devolución de la función. Los tipos de devolución permitidos son:

   1. Cadena
   1. número
   1. boolean

   Todos los demás tipos de devolución se clasifican en uno de los anteriores. No se admite ninguno. Asegúrese de seleccionar uno de los tipos anteriores. Los tipos de devolución no distinguen entre mayúsculas y minúsculas.

>[!NOTE]
>
>Los comentarios antes de la función personalizada se utilizan como resumen. El resumen puede extenderse a varias líneas hasta que se encuentre una etiqueta. Limite el tamaño a un único para una descripción concisa en el generador de reglas.

**Añadir una función personalizada**

Por ejemplo, desea agregar una función personalizada que calcule el área de un cuadrado. Longitud lateral es la entrada del usuario a la función personalizada, que se acepta mediante un cuadro numérico en el formulario. El resultado calculado se muestra en otro cuadro numérico del formulario. Para agregar una función personalizada, primero debe crear una biblioteca de cliente y luego agregarla al repositorio de CRX.

Realice los siguientes pasos para crear una biblioteca de cliente y agregarla al repositorio de CRX.

1. Cree una biblioteca de cliente. Para obtener más información, consulte [Uso de bibliotecas](/help/sites-developing/clientlibs.md)del lado del cliente.
1. En CRXDE, agregue una propiedad `categories`con un valor de tipo de cadena como `customfunction` a la `clientlib` carpeta.

   >[!NOTE]
   >
   >`customfunction`es una categoría de ejemplo. Puede elegir cualquier nombre para la categoría que cree en la `clientlib`carpeta.

Después de agregar la biblioteca de cliente en el repositorio de CRX, utilícela en el formulario adaptable. Permite utilizar la función personalizada como regla en el formulario. Realice los siguientes pasos para agregar la biblioteca del cliente en el formulario adaptable.

1. Abra el formulario en modo de edición.
Para abrir un formulario en modo de edición, seleccione un formulario y toque **Abrir**.
1. En el modo de edición, seleccione un componente, toque ![campo](assets/field-level.png) > Contenedor **de formulario** adaptable y, a continuación, toque ![cmppr](assets/cmppr.png).
1. En la barra lateral, en Nombre de la biblioteca de cliente, agregue la biblioteca de cliente. ( `customfunction` en el ejemplo.)

   ![Añadir la biblioteca del cliente de función personalizada](assets/clientlib.png)

1. Seleccione el cuadro numérico de entrada y toque ![edit-rules](assets/edit-rules.png) para abrir el editor de reglas.
1. Toque **Crear regla**. Mediante las opciones que se muestran a continuación, cree una regla para guardar el valor al cuadrado de la entrada en el campo Salida del formulario.
   [ ![Uso de funciones personalizadas para crear una](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)reglaToque **Listo**. Se ha agregado la función personalizada.

#### Tipos admitidos en la declaración de funciones {#function-declaration-supported-types}

**Instrucción de función**

```javascript
function area(len) {
    return len*len;
}
```

Esta función se incluye sin `jsdoc` comentarios.

**Expresión de funciones**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Expresión y declaración de funciones**

```
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Declaración de función como variable**

```
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitación: la función personalizada selecciona únicamente la primera declaración de función de la lista de variable, si está unida. Puede utilizar la expresión de funciones para cada función declarada.

**Declaración de función como objeto**

```
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>Asegúrese de utilizar `jsdoc` todas las funciones personalizadas. Aunque se recomiendan `jsdoc`comentarios, incluya un `jsdoc`comentario vacío para marcar la función como función personalizada. Permite el manejo predeterminado de la función personalizada.

## Administrar reglas {#manage-rules}

Cualquier regla existente en un objeto de formulario se muestra cuando toca el objeto y toca ![edit-rules1](assets/edit-rules1.png). Puede vista del título y una previsualización del resumen de reglas. Además, la interfaz de usuario le permite expandir y vista del resumen completo de reglas, cambiar el orden de las reglas, editar las reglas y eliminar reglas.

![Reglas de lista](assets/list-rules.png)

Puede realizar las siguientes acciones en reglas:

* **Expandir/Contraer**: La columna Contenido de la lista de regla muestra el contenido de la regla. Si todo el contenido de la regla no está visible en la vista predeterminada, toque ![expandir contenido](assets/expand-rule-content.png) de regla para expandirlo.

* **Reordenar**: Cualquier regla nueva que cree se apilará en la parte inferior de la lista de regla. Las reglas se ejecutan de arriba abajo. La regla en la parte superior se ejecuta primero seguida de otras reglas del mismo tipo. Por ejemplo, si tiene las reglas Cuándo, Mostrar, Activar y Cuándo en la primera, segunda, tercera y cuarta posiciones desde la parte superior, respectivamente, la regla Cuándo en la parte superior se ejecuta primero seguida de la regla Cuándo en la cuarta posición. A continuación, se ejecutarán las reglas Mostrar y Activar.
Puede cambiar el orden de una regla tocando las reglas ![de](assets/sort-rules.png) clasificación o arrastrándola y soltándola en el orden deseado en la lista.

* **Editar**: Para editar una regla, active la casilla de verificación situada junto al título de la regla. Aparecerán opciones adicionales para editar y eliminar la regla. Toque **Editar** para abrir la regla seleccionada en el editor de reglas en modo visual o de editor de código, según el modo utilizado para crear la regla.

* **Eliminar**: Para eliminar una regla, selecciónela y toque **Eliminar**.

* **Habilitar/Deshabilitar**: Es posible que tenga que suspender temporalmente el uso de una regla. Puede seleccionar una o varias reglas y tocar Deshabilitar en la barra de herramientas Acciones para deshabilitarlas. Si una regla está deshabilitada, no se ejecuta en tiempo de ejecución. Para habilitar una regla que está deshabilitada, puede seleccionarla y tocar Habilitar en la barra de herramientas de acciones. La columna de estado de la regla muestra si la regla está habilitada o deshabilitada.

![disablerule](assets/disablerule.png)

## Copiar y pegar reglas {#copy-paste-rules}

Puede copiar y pegar una regla de un campo a otros campos similares para ahorrar tiempo.

Para copiar y pegar reglas, haga lo siguiente:

1. Toque el objeto de formulario desde el que desea copiar una regla y, en la barra de herramientas del componente, toque ![Editar](assets/editrule.png). La interfaz de usuario del editor de reglas aparece con el objeto de formulario seleccionado y aparecen las reglas existentes.

   ![copyrule](assets/copyrule.png)

   Para obtener información sobre la administración de reglas existentes, consulte [Administrar reglas](../../forms/using/rule-editor.md#p-manage-rules-p).

1. Seleccione la casilla de verificación situada junto al título de la regla. Aparecerán opciones adicionales para administrar la regla. Pulse **Copiar**.

   ![copyrule2](assets/copyrule2.png)

1. Seleccione otro objeto de formulario en el que desee pegar la regla y toque **Pegar**. Además, puede editar la regla para realizar cambios en ella.

   >[!NOTE]
   >
   >Puede pegar una regla en otro objeto de formulario solo si dicho objeto de formulario admite el evento de la regla copiada. Por ejemplo, un botón admite el evento de clics. Puede pegar una regla con un evento de clic en un botón pero no en una casilla de verificación.

1. Toque **Hecho** para guardar la regla.

## expresiones anidadas {#nestedexpressions}

El editor de reglas permite utilizar varios operadores Y y O para crear reglas anidadas. Puede combinar varios operadores Y y O en las reglas.

A continuación se muestra un ejemplo de regla anidada que muestra un mensaje al usuario sobre la elegibilidad para la custodia de un niño cuando se cumplen las condiciones requeridas.

![complejexpresión](assets/complexexpression.png)

También puede arrastrar y soltar condiciones dentro de una regla para editarlas. Puntee y coloque el puntero sobre el controlador ( ![control](assets/handle.png)) antes de una condición. Una vez que el puntero se convierta en el símbolo de mano como se muestra a continuación, arrastre y suelte la condición en cualquier lugar dentro de la regla. La estructura de reglas cambia.

![arrastrar y soltar](assets/drag-and-drop.png)

## Condiciones de expresión de fecha {#dateexpression}

El editor de reglas permite usar comparaciones de fechas para crear condiciones.

A continuación se muestra una condición de ejemplo que muestra un objeto de texto estático si la hipoteca de la casa ya se ha tomado, lo que el usuario significa rellenando el campo de fecha.

Cuando la fecha de hipoteca de la propiedad tal como la ha rellenado el usuario es anterior, el formulario adaptable muestra una nota sobre el cálculo de ingresos. La regla siguiente compara la fecha rellenada por el usuario con la fecha actual y, si la fecha rellenada por el usuario es anterior a la fecha actual, el formulario muestra el mensaje de texto (denominado Ingresos).

![dateexpressioncondition](assets/dateexpressioncondition.png)

Cuando la fecha rellenada es anterior a la fecha actual, el formulario muestra el mensaje de texto (Ingresos) de la siguiente manera:

![dateexpressioncondition](assets/dateexpressionconditionmet.png)

## Condiciones de comparación de número {#number-comparison-conditions}

El editor de reglas permite crear condiciones que comparan dos números.

A continuación se muestra una condición de ejemplo que muestra un objeto de texto estático si el número de meses que un solicitante permanece en su dirección actual es inferior a 36.

![number ercomparisoncondition](assets/numbercomparisoncondition.png)

Cuando el usuario indica que ha vivido en su domicilio actual durante menos de 36 meses, el formulario muestra una notificación en la que se indica que se puede solicitar prueba adicional de residencia.

![additionalsolicitado](assets/additionalproofrequested.png)

## Impacto del editor de reglas en secuencias de comandos existentes {#impact-of-rule-editor-on-existing-scripts}

En las versiones de AEM Forms anteriores al paquete de funciones 1 de AEM 6.1 Forms, los creadores y desarrolladores de formularios solían escribir expresiones en la ficha Secuencias de comandos del cuadro de diálogo Editar componente para añadir un comportamiento dinámico a los formularios adaptables. La ficha Secuencias de comandos ahora se reemplaza por el editor de reglas.

Las secuencias de comandos o expresiones que debe haber escrito en la ficha Secuencias de comandos están disponibles en el editor de reglas. Aunque no puede realizar vistas ni editarlas en un editor visual, si forma parte del grupo de usuarios avanzados de formularios, puede editar las secuencias de comandos en el editor de código.

## Reglas de ejemplo {#example}

### Invoke form data model service {#invoke}

Considere un servicio Web `GetInterestRates` que toma el monto del préstamo, la tenencia y la calificación crediticia del solicitante como insumo y devuelve un plan de préstamo que incluye el importe del IME y el tipo de interés. Puede crear un modelo de datos de formulario utilizando el servicio Web como origen de datos. Los objetos del modelo de datos y un `get` servicio se agregan al modelo de formulario. El servicio aparece en la ficha Servicios del modelo de datos de formulario. A continuación, cree un formulario adaptable que incluya campos de objetos del modelo de datos para capturar las entradas del usuario para el importe del préstamo, la tenencia y la puntuación del crédito. Añada un botón que active el servicio Web para obtener los detalles del plan. El resultado se rellena en los campos correspondientes.

La regla siguiente muestra cómo configurará la acción del servicio Invocar para llevar a cabo el escenario de ejemplo.

![example-invoke-services](assets/example-invoke-services.png)

Invocar el servicio del modelo de datos de formulario mediante una regla de formulario adaptable

### Activación de varias acciones mediante la regla Cuándo {#triggering-multiple-actions-using-the-when-rule}

En un formulario de solicitud de préstamo, desea capturar si el solicitante del préstamo es un cliente existente o no. En función de la información que proporcione el usuario, el campo ID del cliente debe mostrarse u ocultarse. Además, si el usuario es un cliente existente, desea establecer el enfoque en el campo ID del cliente. El formulario de solicitud de préstamo tiene los siguientes componentes:

* Un botón de radio, **¿Es usted un cliente de Geometrixx existente?**, que proporciona las opciones Sí y No. El valor de Sí es **0** y No es **1**.

* Campo de texto, ID **de cliente de** Geometrixx, para especificar el ID de cliente.

Al escribir una regla de Cuándo en el botón de radio para implementar este comportamiento, la regla aparece de la siguiente manera en el editor de reglas visuales.  ![when-rule-example](assets/when-rule-example.png)

Regla en el editor visual

En la regla de ejemplo, la instrucción de la sección Cuándo es la condición, que cuando devuelve True, ejecuta las acciones especificadas en la sección Entonces.

La regla aparece de la siguiente manera en el editor de código.

![when-rule-example-code](assets/when-rule-example-code.png)

Regla en el editor de código

### Uso de una salida de función en una regla {#using-a-function-output-in-a-rule}

En un formulario de orden de compra, tiene la siguiente tabla, en la que los usuarios rellenarán sus pedidos. En esta tabla:

* La primera fila es repetible, por lo que los usuarios pueden solicitar varios productos y especificar diferentes cantidades. Su nombre de elemento es `Row1`.
* El título de la celda en la columna Cantidad del producto de la fila repetible es Cantidad. El nombre del elemento de esta celda es `productquantity`.
* La segunda fila de la tabla no se puede repetir y el título de la celda de la columna Cantidad de producto de esta fila es Cantidad total.

![example-function-table](assets/example-function-table.png)

**A.** Fila1 **B.** Cantidad **C.** Cantidad total

Ahora, desea agregar cantidades especificadas en la columna Cantidad del producto para todos los productos y mostrar la suma en la celda Cantidad total. Esto se puede lograr escribiendo una regla Definir valor de en la celda Cantidad total, como se muestra a continuación.

![example-function-output](assets/example-function-output.png)

Regla en el editor visual

La regla aparece de la siguiente manera en el editor de código.

![example-function-output-code](assets/example-function-output-code.png)

Regla en el editor de código

### Validación de un valor de campo mediante expresión {#validating-a-field-value-using-expression}

En el formulario de orden de compra explicado en el ejemplo anterior, desea restringir la posibilidad de que el usuario solicite más de una cantidad de cualquier producto cuyo precio sea superior a 10000. Para ello, puede escribir una regla de validación como se muestra a continuación.

![example-validate](assets/example-validate.png)

Regla en el editor visual

La regla aparece de la siguiente manera en el editor de código.

![example-validate-code](assets/example-validate-code.png)

Regla en el editor de código

