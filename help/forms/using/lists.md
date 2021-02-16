---
title: Fragmentos de documento
seo-title: Fragmentos de documento
description: Los fragmentos de documento, como los fragmentos de texto, listas, condiciones y diseño, en la gestión de correspondencia le permiten formar los componentes estáticos, dinámicos y repetibles de la correspondencia con los clientes.
seo-description: Los fragmentos de documento, como los fragmentos de texto, listas, condiciones y diseño, en la gestión de correspondencia le permiten formar los componentes estáticos, dinámicos y repetibles de la correspondencia con los clientes.
uuid: 4273323d-14f5-4b3b-8fed-80beef641efe
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d5436c6-1976-496c-b9a7-7dc6e830bb5d
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '6933'
ht-degree: 0%

---


# Fragmentos de documento{#document-fragments}

## Fragmentos de documento {#document-fragments-1}

Los fragmentos de documento son partes/componentes reutilizables de una correspondencia mediante los cuales se pueden componer cartas/correspondencia. Los fragmentos de documento son de los siguientes tipos:

* **Texto**: Un recurso de texto es un fragmento de contenido que consta de uno o varios párrafos de texto. Un párrafo puede ser estático o dinámico.
* **Lista**: Lista es un grupo de fragmentos de documento, incluidos texto, listas, condiciones e imágenes. El orden de los elementos de lista puede ser fijo o editable. Al crear una carta, puede utilizar algunos o todos los elementos de lista para replicar un patrón reutilizable de elementos.
* **Condición**: Las condiciones le permiten definir qué contenido se incluye en el momento de la creación de la correspondencia, en función de los datos suministrados. La condición se describe en términos de variables de control. Una variable de control puede ser un elemento de diccionario de datos o un marcador de posición.
* **Fragmento** de diseño: Un fragmento de diseño es un diseño que se puede utilizar en una o varias letras. Un fragmento de diseño se utiliza para crear patrones repetibles, especialmente tablas dinámicas. La presentación puede contener campos de formulario típicos como &quot;Dirección&quot; y &quot;Número de referencia&quot;. También contiene subformularios vacíos que denotan áreas de destinatario. Los diseños (XDP) se crean en Designer y, a continuación, se cargan en AEM Forms.

## Texto {#text}

Un recurso de texto es un fragmento de contenido que consta de uno o varios párrafos de texto. Un párrafo puede ser estático o dinámico. Un párrafo dinámico contiene referencias a elementos de datos, cuyos valores se suministran en tiempo de ejecución. Por ejemplo, el nombre del cliente en un saludo de letras podría ser un elemento de datos dinámico, con su valor disponible en tiempo de ejecución. Al cambiar estos valores, se puede utilizar la misma plantilla de letras para generar letras para distintos clientes.

La solución de administración de correspondencia admite dos tipos de elementos de datos dinámicos (datos variables):

* **Elementos** del diccionario de datos: Estos elementos están enlazados al diccionario de datos y obtienen sus valores del origen de datos proporcionado. Una variable de diccionario de datos puede estar protegida o desprotegida. Durante la creación de la correspondencia, el usuario puede modificar el valor predeterminado de las variables de diccionario de datos no protegidas, pero no puede modificar las que están protegidas.
* **Marcadores** de posición: Son variables que no están enlazadas a una fuente de datos back-end. Requieren que el usuario rellene un valor durante la creación de la correspondencia. Los marcadores de posición no están protegidos de forma predeterminada.

>[!NOTE]
>
>Las plantillas de Administración de correspondencia no obligan a crear nombres únicos al crear marcadores de posición. Si se crean dos marcadores de posición con el mismo nombre, como un texto y una condición, y se utilizan ambos en una plantilla de letras, los valores del último marcador de posición insertado se utilizan para ambos marcadores de posición. Si dos marcadores de posición tienen el mismo nombre, se comparan sus tipos. Si los tipos son diferentes, su tipo pasa a ser String. Sin embargo, dentro de un módulo no se pueden crear varios marcadores de posición con el mismo nombre.

### Crear texto {#create-text}

1. Seleccione **Forms** > **Fragmentos de Documento**.
1. Toque **Crear** > **Texto** O seleccione un recurso de texto y toque **Editar**.
1. Especifique la siguiente información para el texto:

   * **Título: (Opcional)** Introduzca el título del recurso de texto. Los títulos no tienen que ser únicos y pueden tener caracteres especiales y caracteres no ingleses. Los textos se remiten por sus títulos (cuando están disponibles), como en miniaturas y propiedades de recursos.
   * **Nombre:** el nombre único del recurso de texto. No pueden existir dos recursos (texto, condición o lista) en ningún estado con el mismo nombre. En el campo Nombre, solo puede introducir caracteres, números y guiones en inglés. El campo Nombre se rellena automáticamente según el campo Título. Los caracteres especiales, espacios, números y caracteres no ingleses introducidos en el campo Título se sustituyen por guiones en el campo Nombre. Aunque el valor del campo Título se copia automáticamente en el Nombre, puede editarlo.
   * **Descripción**: Escriba una descripción del recurso.
   * **Diccionario** de datos: De forma opcional, seleccione el diccionario de datos en el que desea realizar la asignación. Este atributo permite agregar referencias a elementos del diccionario de datos en el recurso de texto.
   * **Etiquetas**: De forma opcional, para crear un valor de introducción de etiquetas personalizado en el campo de texto y pulse Intro. Puede ver la etiqueta debajo del campo de texto de las etiquetas. Al guardar este texto, también se crean las etiquetas recientemente agregadas.

1. Toque **Siguiente**. La Administración de correspondencia muestra la página Editor, donde puede agregar párrafos de texto y elementos de datos al texto.

   El corrector ortográfico predeterminado del navegador comprueba la ortografía en el editor de texto. Para administrar la revisión ortográfica y gramatical, puede editar la configuración del corrector ortográfico del navegador o instalar complementos del navegador para revisar la ortografía y la gramática.

   También puede utilizar los distintos métodos abreviados de teclado del editor de texto para administrar, editar y dar formato al texto. Para obtener más información acerca de los [atajos de teclado del Editor de texto](/help/forms/using/keyboard-shortcuts.md#p-formatting-p) en Atajos de teclado de Correspondence Management.

1. Se abre un editor de texto, introduzca el texto. Utilice la barra de herramientas situada en la parte superior de la página para dar formato al texto, insertar condiciones, vínculos y saltos de página.

   ![Barra de herramientas](assets/advancedediting.png)

   * **Vínculo**: Inserte un  [](#insert-hyperlink) hipervínculo en el texto.
   * **Repetir**: Repita el elemento de recopilación de impresiones en el diccionario de datos con un delimitador.
   * **Condición**: Toque para insertar una condición. Inserte texto basado en una condición. Si la condición es verdadera, el texto está visible en letra; de lo contrario, no.
   * **Añadir descripción**: Añada la anotación en un fragmento de texto. Se trata de metadatos visibles para el autor, pero no de una parte de la carta que se crea.
   * **Salto** de página: Si establece el atributo de salto de página de un módulo de texto en false, el módulo de texto no se divide entre las páginas.

   Se abre un editor de texto. Escriba el texto. La barra de herramientas cambia según el tipo de edición que elija: Párrafo, alineación o Lista:

   ![Seleccionar tipo de barra de herramientas](assets/toolbarselection.png)

   Seleccionar tipo de barra de herramientas: Párrafo, alineación o lista

   ![Barra de herramientas Párrafo](assets/fonteditingtoolbar.png)

   Barra de herramientas Párrafo
   [ ![Alineación, ](assets/paragrapheditingtoolbar.png)](assets/paragrapheditingtoolbar-1.png)barra de herramientasBarra de herramientas Alineación

   ![Lista, barra de herramientas](assets/bulleteditingtoolbar.png)

   Barra de herramientas Lista (haga clic para abrir una imagen de tamaño completo)

1. Para reutilizar uno o varios párrafos de texto que existen en otra aplicación, como desde páginas de MS Word o HTML, copie y pegue el texto en el editor de texto. El formato del texto copiado se conserva en el editor de texto.

   Puede copiar y pegar uno o varios párrafos de texto en un módulo de texto editable. Por ejemplo, puede tener un documento de MS Word con una lista con viñetas de pruebas de residencia aceptables, como por ejemplo:

   ![pastetextmsword-1](assets/pastetextmsword-1.png)

   Puede copiar y pegar directamente el texto del documento de MS Word en un módulo de texto editable. El formato, como la lista con viñetas, la fuente y el color del texto, se conserva en el módulo de texto.

   ![pastetexttextmodule](assets/pastetexttextmodule.png)

   >[!NOTE]
   >
   >Sin embargo, el formato del texto pegado tiene algunas [limitaciones](https://helpx.adobe.com/aem-forms/kb/cm-copy-paste-text-limitations.html).

1. Si es necesario, inserte caracteres especiales en el fragmento de documento. Por ejemplo, puede utilizar la paleta Caracteres especiales para insertar:

   * Símbolos monetarios como €, ¥y £
   * Matemáticas como la adrenalina, el rey, el rey, el rey y el símbolo ^
   * Símbolos de puntuación como ‟ y&quot;

   ![caracteres especiales-1](assets/specialcharacters-1.png)

   Correspondence Management ha incorporado compatibilidad con 210 caracteres especiales. El administrador puede [agregar compatibilidad con más caracteres especiales personalizados personalizándolos](/help/forms/using/custom-special-characters.md).

1. Para resaltar o resaltar partes del texto en un módulo en línea editable, seleccione el texto y toque Color de resaltado.

   ![textbackcoloreado aplicado](assets/textbackgroundcolorapplied.png)

   Puede tocar directamente un color básico `**[A]**` presente en la paleta Colores básicos o tocar **Seleccionar** después de usar el deslizador `**[B]**` para elegir la sombra adecuada del color.

   Opcionalmente, también puede ir a la ficha Avanzado para seleccionar el tono, la luminosidad y la saturación correspondientes `**[C]**` para crear el color preciso y, a continuación, tocar Seleccionar `**[D]**` para aplicar el color y resaltar el texto.

   ![textbackground-color-1](assets/textbackgroundcolor-1.png)

1. En el panel de datos, arrastre y suelte los elementos del diccionario de datos y los elementos del marcador de posición al texto.

   A:

   * Añada un elemento de diccionario de datos en el texto, seleccione un elemento de datos de la lista y toque Insertar ( ![insertar](assets/insert.png)). Si selecciona Protegido, el elemento del diccionario de datos es de solo lectura y aparece en el editor de letras, pero no en la interfaz de usuario Crear correspondencia o Creador de correspondencia.
   * Añada un elemento de marcador de posición en el texto, en el panel Elementos de datos toque Crear nuevo, introduzca los detalles del nuevo elemento de datos y toque Crear para agregar el nuevo elemento a la lista. El nuevo marcador de posición se puede insertar en el texto del mismo modo que el elemento del diccionario de datos. Para editar un marcador de posición, selecciónelo y toque Editar.

   ![Elementos de marcador de posición](assets/placeholder_elements_in_xmldata.png)

   Elementos de marcador de posición como se especifica en el archivo de datos de ejemplo de un diccionario de datos

   ![Elementos de marcador de posición en letra](assets/placeholder_elements_in_text.png)

   Los valores de los elementos de marcador de posición en la vista CCR se rellenan desde las variables de diccionario de datos, tal como se especifica en el archivo de datos de ejemplo

   También puede utilizar el símbolo @ para buscar y agregar elementos de diccionario de datos y marcador de posición al editor de texto. Coloque el cursor donde desee insertar el elemento. Escriba @ seguido de la cadena de búsqueda. El editor de texto realiza la operación de búsqueda en todos los elementos del diccionario de datos y del marcador de posición disponibles en el fragmento de documento de texto. La operación de búsqueda recupera y muestra los elementos que contienen la cadena de búsqueda como una lista desplegable. Navegue por los resultados de búsqueda y haga clic en el elemento que desee insertar en la ubicación del cursor. Pulse Esc para ocultar los resultados de la búsqueda.

1. Puede usar condiciones en línea y repetir para hacer que su carta sea muy contextual y esté bien estructurada. Para obtener más información sobre las condiciones en línea y repetir, consulte [Condiciones en línea y repita en letras](/help/forms/using/cm-inline-condition.md).
1. Toque **Guardar**.

#### Insertar hipervínculo en un texto {#insert-hyperlink}

Siga los pasos siguientes para crear un hipervínculo en un recurso de texto:

1. Seleccione el texto o el objeto del modelo de datos en el editor de texto.

2. Toque **[!UICONTROL Vínculo]**. Toque el campo **[!UICONTROL Texto alternativo]** para quitar el nombre o texto del objeto del modelo de datos existente.

3. Especifique la dirección URL y toque ![Guardar](assets/save_icon.svg).

![Crear hipervínculo en un recurso de texto](assets/text-create-hyperlink.png)

#### Búsqueda y reemplazo de texto {#searching-and-replacing-text}

Cuando se trabaja con elementos de texto que contienen un gran cuerpo de texto, es necesario buscar una cadena de texto específica. También es posible que tenga que reemplazar una cadena de texto específica por una cadena alternativa.

La función Buscar y reemplazar permite buscar (y reemplazar) cualquier cadena de texto en un elemento de texto. La función también incluye una potente búsqueda de expresión regular.

#### Para buscar texto en un módulo de texto {#to-search-text-in-a-text-module}

1. Abra el módulo de texto en el editor de texto.

1. Toque Buscar y reemplazar.
1. Introduzca el texto que desea buscar en el cuadro de texto Buscar y pulse Buscar. El texto de búsqueda se resalta en el módulo de texto.
1. Para buscar la siguiente instancia del texto, vuelva a pulsar Buscar.

   Si continúa presionando el botón Buscar, la búsqueda continúa hacia abajo en la página. Después de encontrar la última instancia del texto, el mensaje **Se llegó al final del módulo** indica que no se encontraron más resultados de búsqueda.

   Sin embargo, si no se encuentra ninguna instancia del texto de búsqueda en el módulo de texto, el mensaje mostrado es: **Coincidencia no encontrada**.

1. Si vuelve a pulsar Buscar, la búsqueda continúa en la parte superior de la página.

#### Opciones de búsqueda {#search-options}

**Coincidir mayúsculas y minúsculas:** la búsqueda devuelve resultados con el mismo caso solamente.

**Palabra completa:** Buscar solo devuelve palabras completas.

>[!NOTE]
>
>Si introduce caracteres especiales en el cuadro de texto Buscar, se desactivará la opción Palabra completa.

**Reg, por ejemplo:** Buscar con expresiones regulares. Por ejemplo, la siguiente expresión regular busca direcciones de correo electrónico en un módulo de texto:

`[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}`

#### Para buscar y reemplazar texto en un módulo de texto {#to-search-and-replace-text-in-a-text-module}

1. Abra el módulo de texto en el editor de texto.
1. Toque Buscar y reemplazar.
1. Introduzca el texto que desea buscar en el cuadro de texto Buscar y el texto con el que desea reemplazar el texto de búsqueda y pulse Reemplazar.
1. Si se encuentra el texto de búsqueda, el texto se reemplaza por el texto Reemplazar.

   * Si se encuentra otra instancia del texto de búsqueda, esa instancia se resalta en el módulo de texto. Si vuelve a pulsar Reemplazar, se reemplaza la instancia resaltada y el cursor se mueve hacia adelante, si se encuentra una tercera instancia.
   * Si no se encuentra otra instancia, el cursor se detiene en la última instancia reemplazada.

1. Si vuelve a pulsar Buscar, la búsqueda continúa en la parte superior de la página.

   Utilice la opción Reemplazar todo para reemplazar todas las instancias de un texto en el módulo de texto. Al hacerlo &quot;, el número de reemplazos se muestra como un mensaje en el cuadro de diálogo Buscar y reemplazar.

#### Prácticas recomendadas, sugerencias y trucos para módulos de texto {#best-practices-tips-and-tricks-for-text-modules}

* Utilice una convención de nombres coherente para evitar duplicaciones.
* Utilice el enlace de diccionario de datos adecuado en los módulos de texto.
* Las siguientes reglas se aplican al utilizar el Editor de texto al cambiar un recurso de texto:

   * **Adición de variable:** Permitida
   * **Eliminación de variable:** permitido
   * **Actualización de propiedades:** Permitida
   * **Cambio del diccionario de datos:** Permitido hasta que no se utilice el elemento del diccionario de datos. No se puede cambiar el diccionario de datos al actualizar.

## Lista {#list}

Una lista es un grupo de fragmentos de documento, incluido texto, (otros) listas, condiciones e imágenes. El orden de los elementos de lista puede ser fijo o editable. Al crear una carta, puede utilizar algunos o todos los elementos de lista para replicar un patrón reutilizable de elementos. Las listas se comportan básicamente como destinatarios que pueden anidarse dentro de otros destinatarios.

### Implementación de listas {#implementing-lists}

La implementación de listas consta de dos pasos:

1. Definición de propiedades principales como nombre, descripción o diccionario de datos.
1. Sección del contenido que forma parte de la lista y, a continuación, establecer propiedades como orden de bloqueo y acceso a la biblioteca para la lista.

### Crear una lista {#create-a-list}

Una lista es un grupo de contenido relacionado que se puede utilizar en una plantilla de carta como una sola unidad. Se puede agregar cualquier tipo de contenido a una lista. También se pueden anidar listas. Los módulos de lista pueden especificarse como:

* **ORDENADO**: El orden no se puede cambiar en el tiempo de ejecución Crear correspondencia.
* **Acceso** a biblioteca: Los usuarios pueden agregar módulos a la lista. Este indicador especifica si el acceso a la biblioteca está habilitado. Si está activada (abierta), el usuario puede agregar módulos a la lista mientras previsualiza la letra.
* Al crear una lista, puede especificar un tipo, como:
* **Sin formato**: No se aplica ningún formato de estilo adicional a la lista.
* **Con viñetas**: Lista con formato de viñeta simple.
* **Numerado**: Una lista numérica con la elección de números estándar (1,2,...), romanos superiores (I, II, ...) y romanos inferiores (i, ii,...).
* **Escritos**: Una lista alfabética con la elección de letras en minúsculas (a,b,...) y mayúsculas (A,B,...).
* **Personalizado**: Puede crear cualquier tipo Numerado/Escrito y los valores de prefijo y sufijo que desee.

1. Seleccione **Forms** > **Fragmentos de Documento**.

1. Seleccione **Crear** > **Lista**.

1. Especifique la siguiente información para la lista:

   * **Título (opcional):** Escriba el título de la lista. El título no tiene que ser único y puede tener caracteres especiales y caracteres no ingleses. Las listas se remiten por sus títulos (cuando están disponibles), como en miniaturas y propiedades de recursos.
   * **Nombre:** el nombre único de la lista. No pueden existir dos recursos (texto, condición o lista) en ningún estado con el mismo nombre. En el campo Nombre, solo puede introducir caracteres, números y guiones en inglés. El campo Nombre se rellena automáticamente con el valor en el campo Título. Los caracteres especiales, espacios, números y caracteres no ingleses introducidos en el campo Título se sustituyen por guiones en el campo Nombre. Aunque el valor del campo Título se copia automáticamente en el Nombre, puede editarlo.
   * **Descripción (opcional)**: Escriba una descripción del recurso.
   * **Diccionario de datos (opcional)**: De forma opcional, seleccione el diccionario de datos al que desea conectarse. Solo se pueden agregar a la lista recursos que utilicen el mismo diccionario de datos que la lista o recursos que no tengan asignado ningún diccionario de datos. Asignar un diccionario de datos a una lista facilita que la persona que crea una plantilla de letras encuentre la lista adecuada.
   * **Etiquetas (opcional)**: Seleccione las etiquetas que desee aplicar. También puede escribir el nombre de una nueva etiqueta y crearla. (La nueva etiqueta se crea al tocar **Guardar**).

1. Toque **Siguiente**.
1. Toque **Añadir recurso**.
1. Para agregar recursos a la lista, selecciónelos en la página Seleccionar recursos y toque **Listo**.

   ![Seleccionar recursos para agregar a la lista](assets/selectassets.png)

1. Los recursos se agregan a la página Elementos de Lista.
Para cambiar el orden de los recursos dentro de la lista, toque y mantenga presionadas las flechas ( ![arrastrar y soltar](assets/dragndrop.png) ) y arrastre y suelte. Cuando el usuario abre una plantilla de carta en la interfaz de usuario Crear correspondencia, el contenido se ensambla en el orden definido aquí.

   ![Reordenar y configurar recursos en una lista](assets/listitems.png)

1. Puede seleccionar las siguientes opciones para especificar el comportamiento de la lista en la interfaz de usuario de CCR:

   * **Acceso** a biblioteca: Para habilitar el acceso a la biblioteca para agregar recursos, toque Acceso a la biblioteca. Cuando se habilita el Acceso a biblioteca, el ajustador de notificaciones puede agregar más contenido a la lista. De lo contrario, el ajuste de solicitudes se limita al contenido que haya definido para la lista.
   * **Orden** de bloqueo: Para bloquear el orden de los recursos en la lista de modo que el ajuste de reclamaciones no pueda cambiar el orden, toque Bloquear orden. Si no selecciona esta opción, el ajuste de solicitudes puede cambiar el orden de los artículos de lista.

   * **Añadir viñetas**: Utilice esta opción para aplicar una viñeta o un estilo de numeración al módulo. Puede utilizar un estilo de lista prediseñado o uno personalizado. También puede especificar el texto que se mostrará antes y después de cada uno de los elementos de lista.
   * **Salto** de página: Seleccione esta opción ( ![salto](assets/break.png)) para agregar un salto de página entre el contenido de la lista. Cuando no se selecciona esta opción ( ![nobreak](assets/nobreak.png)), si el contenido de la lista se desborda a la página siguiente, toda la lista se desplaza a la página siguiente en lugar de saltarse la página entre la lista.

   * **Configuración** de asignación: Utilice esta opción para especificar el número mínimo y máximo de recursos que se pueden agregar a la lista.

1. Puede seleccionar las siguientes opciones para especificar el comportamiento de cada recurso en la lista durante la ejecución:

   * **Editable:** cuando se selecciona esta opción, el contenido se puede editar en la interfaz de usuario Crear correspondencia. (Esta opción no está disponible para los módulos de Lista e imagen).
   * **Obligatorio:** cuando se selecciona esta opción, el contenido es obligatorio en la interfaz de usuario Crear correspondencia.
   * **Seleccionado:** cuando se selecciona esta opción, el contenido se preselecciona en la interfaz de usuario Crear correspondencia.
   * **Estilo de omisión:** cuando se selecciona esta opción, el contenido omite las viñetas y la numeración en la interfaz de usuario Crear correspondencia. (Esta opción no está disponible para los módulos de imagen. Además, entre Omitir estilo, Compuesto e Ignorar estilo de Lista, solo se puede aplicar una de las opciones a un módulo. Una de estas opciones se puede utilizar para un módulo cuando se selecciona Añadir viñetas para un módulo).
   * **Sangría:** puede cambiar el nivel de sangría de cada módulo o contenido seleccionado como parte de la Lista. La sangría se especifica en términos de Niveles (empezando por cero), de modo que cada nivel de sangría corresponde a un relleno de 36 puntos.
   * **Compuesto:** cuando se selecciona, la numeración compuesta se aplica como una combinación del estilo de la Lista exterior (principal) y su propio estilo. La numeración compuesta de esta Lista anidada se basa en el orden en que esta Lista anidada aparece en la Lista exterior.
   * **Ignorar estilo de lista:** si la opción Numeración compuesta no está seleccionada, la opción Ignorar estilo de Lista está activada. Esta selección ignora el estilo de la Lista anidada y la numeración continúa desde la Lista exterior. Por lo tanto, los módulos de la lista anidada se tratan como parte de la propia lista exterior, sin tener en cuenta los estilos especificados en la Lista anidada. Si la opción Ignorar estilo de Lista no está seleccionada para una Lista anidada, los módulos que forman parte de esa Lista anidada tienen su propio estilo de numeración.
   * **Mantener con siguiente:** establece el salto de página para los recursos contenidos en una lista. Si establece la propiedad Mantener con siguiente de un recurso de una lista en **Activado**, ese recurso y el siguiente permanecerán en la misma página. Esto implica que el contenido del recurso seleccionado y el siguiente no se dividirán en las páginas.

1. Toque **Guardar**.

### Prácticas recomendadas, sugerencias y trucos {#best-practices-tips-and-tricks}

* Utilice una convención de nombres coherente para evitar duplicaciones.
* Usar enlace de diccionario de datos adecuado
* Las siguientes reglas se aplican al utilizar el Editor de Listas para cambiar una lista:

   * Actualización de propiedades: Permitido
   * **Cambio de diccionario de datos:** permitido hasta que no se asocie ningún elemento que utilice el diccionario de datos. No se puede cambiar el diccionario de datos al actualizar.

## Condiciones {#conditions}

Las condiciones le permiten definir qué contenido se incluye en el tiempo de creación de correspondencia o carta, en función de los datos suministrados. La condición se describe en términos de variables de control. Al agregar una condición, puede elegir incluir un recurso en función del valor que tenga la variable de control.

En función de las opciones que elija, solo se evalúa la primera expresión que se encuentre como verdadera, en función de la variable de condición actual o de toda la condición. Al rellenar la carta en Crear correspondencia (CCR), las condiciones se comportan como &quot;cuadros blancos&quot;. Si una condición resulta en una lista, se muestran todos los elementos obligatorios y preseleccionados de la lista. Si alguno de estos elementos son condiciones o listas en sí, su contenido resultante también se genera, en orden ascendente y profundo, como una lista plana de texto y contenido de imagen. Los resultados de la condición pueden ser de cualquier tipo (texto, lista, condición o imagen).

### Condiciones de implementación {#implementing-conditions}

El Editor de condiciones incluye una interfaz de usuario [Generador de Expresiones](/help/forms/using/expression-builder.md) que admite la creación de expresiones mediante varios marcadores de posición y elementos del diccionario de datos. Puede utilizar operandos comunes y funciones locales/globales en dichas expresiones. Cada expresión se puede asociar con cierto contenido y, opcionalmente, podría haber una sección predeterminada si ninguna de las expresiones se evalúa como verdadera. Todas las expresiones se evalúan en la secuencia en la que están definidas y se seleccionan las primeras expresiones que devuelven true y ese módulo condicional devuelve su contenido asociado.

Por ejemplo, si el texto de términos y condiciones de una carta difiere según el estado en que se encuentre el cliente y el diccionario de datos contenga un elemento llamado &quot;state&quot;, podría agregar la condición de la siguiente manera:
・ state = NY, seleccione el párrafo de texto T&amp;C_NY
・ state = NC, seleccione el párrafo de texto T&amp;C_NC

El editor Condición permite especificar una condición predeterminada. Si el valor de las variables de control no coincide con ninguna de las condiciones, se utiliza el contenido asociado con la condición predeterminada. Siguiendo el ejemplo anterior, puede agregar esta fila de condición:
・ Predeterminado, seleccione T&amp;C_Rest

### Crear una condición {#create-a-condition}

1. Seleccione **Forms** > **Fragmentos de Documento**.
1. Seleccione **Crear > Condición**.
1. Especifique la siguiente información para la lista:

   * **Título (opcional):** introduzca el título de la condición. El título no tiene que ser único y puede tener caracteres especiales y caracteres no ingleses. Las condiciones se remiten por sus títulos (cuando están disponibles), como en miniaturas y propiedades de recursos.
   * **Nombre:** el nombre único de la condición. No pueden existir dos recursos (texto, condición o lista) en ningún estado con el mismo nombre. En el campo Nombre, solo puede introducir caracteres, números y guiones en inglés. El campo Nombre se rellena automáticamente según el campo Título. Los caracteres especiales, espacios, números y caracteres no ingleses introducidos en el campo Título se sustituyen por guiones en el campo Nombre. Aunque el valor del campo Título se copia automáticamente en el Nombre, puede editarlo.
   * **Descripción (Opcional)** Escriba una descripción de la condición.
   * **Diccionario de datos (opcional)**: De forma opcional, seleccione el diccionario de datos al que desea conectarse. Solo se pueden agregar a la lista recursos que utilicen el mismo diccionario de datos que la condición o recursos que no tengan asignado ningún diccionario de datos. Asignar un diccionario de datos a una lista facilita que la persona que crea una plantilla de letras encuentre la condición adecuada.
   * **Etiquetas (opcional)**: De forma opcional, seleccione las etiquetas que desee aplicar. También puede escribir el nombre de una nueva etiqueta y crearla. (La nueva etiqueta se crea al tocar **Guardar**).

1. Toque **Siguiente**.
1. Toque **Añadir recurso**.
1. Para agregar un recurso a la condición, selecciónelo en la página Seleccionar recursos y toque **Listo**. Los recursos se agregan al panel Expresión.
1. Puede seleccionar las siguientes opciones para especificar el comportamiento de la condición en tiempo de ejecución:

   * **Deshabilitar la evaluación de varios resultados\Habilitar la evaluación** de varios resultados: Cuando esta opción está habilitada (aparece como &quot;Habilitar varios...&quot;), se evalúan todas las condiciones y el resultado es la suma de todas las condiciones reales. Si esta opción está deshabilitada (aparece como &quot;Deshabilitar varios...&quot;), solo se evalúa la primera condición que se encuentra como verdadera y se convierte en el resultado de la condición.
   * **Salto** de página: Seleccione esta opción ( ![salto](assets/break.png)) para agregar un salto de página entre los módulos de las condiciones. Cuando esta opción no está seleccionada ( ![nobreak](assets/nobreak.png)), si una condición se está desbordando a la página siguiente, toda la condición se cambia a la página siguiente en lugar de saltarse la página entre la condición.

1. Para cambiar el orden de los recursos dentro de la condición, toque y mantenga presionadas las flechas ( ![arrastrar y soltar](assets/dragndrop.png) ) y arrastre y suelte. Cuando el usuario abre una plantilla de carta en la interfaz de usuario Crear correspondencia, el contenido se ensambla en el orden definido aquí.
1. Toque **Eliminar** para eliminar la fila. Si toca Eliminar para la fila predeterminada, solo se borra la información del recurso.
1. Toque **Copiar** para duplicado de una fila.
1. Toque **Editar** para cambiar el recurso o editar la expresión.

   Además:

   * Para actualizar el recurso, toque el icono de la carpeta en la columna Recurso.
   * Para abrir el Generador de Expresiones e insertar una expresión, toque el icono de la carpeta situado debajo de la columna Expresión. Para obtener más información sobre el Generador de Expresiones, consulte [Generador de Expresiones](/help/forms/using/expression-builder.md).

### Prácticas recomendadas, sugerencias y trucos {#best-practices-tips-and-tricks-1}

* Utilice una convención de nombres uniforme para facilitar la búsqueda y evitar duplicaciones.
* Las condiciones se comportan como afirmaciones de caso, por lo que el orden de las condiciones es importante. Se devuelve la primera coincidencia.
* Usar enlace de diccionario de datos adecuado
* Las siguientes reglas se aplican al usar el Editor de condiciones para editar una condición:

   * **Adición de variable:** Permitida
   * **Eliminación de variable:** permitido
   * **Actualización de propiedades:** Permitida
   * **Cambio del diccionario de datos:** Permitido hasta que no se utilice el elemento del diccionario de datos.

## Fragmentos de diseños {#layoutfragments}

Un fragmento de diseño se basa en XDP creados en Designer. Para crear fragmentos de diseño, debe crear los XDP y [cargarlos en AEM Forms](/help/forms/using/import-export-forms-templates.md).

Uno o más fragmentos de diseño pueden formar partes de una letra y definir el diseño gráfico de dichos fragmentos. Un fragmento de diseño puede contener campos de formulario típicos, como Dirección y Número de referencia, y subformularios vacíos que denotan áreas de destinatario. Además, los fragmentos de diseño permiten crear tablas e insertarlas en letras.

Un caso de uso común es localizar patrones de diseño reutilizables en Cartas y crear fragmentos de diseño para ellos. Por ejemplo, la parte de saludo, dirección y asunto de la carta, que aparece en el mismo orden con varias letras. Otro ejemplo podría ser una tabla con un número similar de filas y columnas utilizadas en varias letras.

Puede crear un fragmento de diseño basado en un XDP existente. Un fragmento de diseño puede estar formado por campos y áreas de destinatario o por una o varias tablas. Las tablas de un diseño pueden ser estáticas o dinámicas. Se crea un XDP en Designer y [se carga en AEM Forms](/help/forms/using/import-export-forms-templates.md). Un XDP puede formar la estructura de un fragmento de diseño o de una letra. Más información sobre [Diseño de diseño](/help/forms/using/layout-design-details.md).

El uso de fragmentos enlazados a áreas de destinatario permite cambiar la letra en el momento de la creación. Se puede crear un fragmento de diseño con diferentes dimensiones y el fragmento adecuado se puede enlazar al área de destinatario. Los fragmentos de diseño también permiten personalizar algunas de las propiedades de la tabla:

1. Puede aumentar el recuento de filas y columnas.
1. Puede especificar el texto del encabezado y pie de página para más filas y columnas.
1. Puede definir la proporción del ancho de columna de la tabla. En tiempo de ejecución, se cambia el tamaño de las columnas de la tabla según la proporción definida y el espacio disponible. La suma de la relación de anchura debe ser 100. De lo contrario, no es aplicable.
1. Si una tabla es un marcador de posición (solo contiene una celda en blanco), puede definir el tipo (área/campo de destinatario) de las columnas nuevas.
1. Puede ocultar las filas de encabezado y pie de página.

Antes de realizar este procedimiento, cree un fragmento XFA con Designer. El fragmento puede contener tablas para organizar campos y áreas de destinatario. Designer permite la creación de dos tipos de tablas: estático y dinámico. Las tablas estáticas contienen un número fijo de filas. Las tablas estáticas pueden contener campos y áreas de destinatario. Estos campos y área de destinatario no se pueden enlazar a DDEs repetitivos. Una tabla dinámica también puede tener una sola fila. Los datos enlazados a las celdas de la tabla determinan el número de filas para las tablas dinámicas. Una tabla dinámica sólo puede contener campos. Los DDE pueden ser repetitivos o no repetitivos.

Tenga en cuenta los siguientes puntos al diseñar tablas:

1. Las tablas se pueden personalizar en el momento de crear el fragmento de diseño. Sin embargo, la opción de personalización solo se activa cuando se ajusta el subformulario principal de la tabla.
1. Para las tablas dinámicas, todos los campos, las filas y las tablas que se pueden repetir utilizan el enlace &quot;use name&quot; para que los datos se combinen correctamente.
1. En las tablas dinámicas, todos los DDE repetitivos enlazados a los campos de tabla forman parte de la misma jerarquía. En el caso de los DDE no repetitivos, no existe tal restricción.
1. Cuando se combina un fragmento de diseño en tablas de área de destinatario principal, se cambia el tamaño según el espacio disponible, aunque el cambio de tamaño solo se produce cuando el fragmento de diseño no contiene ningún área de destinatario o campo directamente dentro del subformulario de nivel superior. Se permiten el área de destinatario y los campos dentro de la tabla.
1. Puede crear tablas de marcador de posición. Las tablas de marcador de posición tienen una sola celda en blanco.

* En el caso de las tablas de marcadores de posición, puede personalizar las siguientes propiedades en el momento de la creación del fragmento.

   * recuento de filas
   * recuento de columnas
   * encabezado y pie de página para cada columna
   * tipo (área/campo de destinatario) de cada columna
   * relación de anchura para cada columna

* Para una tabla que no es un marcador de posición, puede personalizar las siguientes propiedades:

   * recuento de filas
   * recuento de columnas
   * encabezado y pie de página para una columna adicional
   * relación de anchura para cada columna

Puede anidar fragmentos en una carta. Esto implica que puede agregar un fragmento dentro de un fragmento. La solución Administración de correspondencia admite hasta cuatro niveles de anidación dentro de una carta: **Carta**->**Fragmento**->**Fragmento**->**Fragmento**->**Fragmento**

Para ver un ejemplo detallado del uso de tablas estáticas y dinámicas en fragmentos de diseño, consulte [Ejemplo con archivos de ejemplo: utilizando tablas estáticas y dinámicas en una letra](#examplewithsamplefiles).

### Creación de un fragmento de diseño {#creating-a-layout-fragment}

1. Seleccione **Crear** > **Fragmento de diseño**.
1. La Administración de correspondencia muestra los XDP disponibles. Seleccione el XDP en el que desea basar el fragmento de diseño y toque **Siguiente**.
1. Especifique la siguiente información para el diseño:

   * **Título (opcional):** introduzca el título del fragmento de diseño. El título no tiene que ser único y puede tener caracteres especiales y caracteres no ingleses. Los fragmentos de diseño se remiten por sus títulos (cuando están disponibles), como en miniaturas y propiedades de recursos.
   * **Nombre:** el nombre único del fragmento de diseño. No pueden existir dos recursos (texto, condición o lista) en ningún estado con el mismo nombre. En el campo Nombre, solo puede introducir caracteres, números y guiones en inglés. El campo Nombre se rellena automáticamente según el campo Título. Los caracteres especiales, espacios, números y caracteres no ingleses introducidos en el campo Título se sustituyen por guiones en el campo Nombre. Aunque el valor del campo Título se copia automáticamente en el Nombre, puede editarlo. Este nombre aparece en la lista de la interfaz de usuario Administrar recursos.
   * **Descripción (opcional)**: Descripción que aparece en la lista en la interfaz de usuario Administrar recursos.
   * **Etiquetas (opcional)**: De forma opcional, seleccione las etiquetas que desee aplicar a la condición. También puede escribir el nombre de una nueva etiqueta y crearla.

1. Toque la ficha **Tabla** y especifique la siguiente información para el diseño:

   * **Configuración para**: Seleccione la tabla que se está configurando.Como sufijo del nombre de la tabla en el menú desplegable es (Estático) si la tabla es estática o (Dinámica) si la tabla es dinámica. Las tablas estáticas contienen un número fijo de filas. Las tablas estáticas pueden contener campos y áreas de destinatario. Estos campos y área de destinatario no se pueden enlazar a DDEs repetitivos. Los datos enlazados a las celdas de la tabla determinan el número de filas para las tablas dinámicas.

   * **Filas**: Seleccione el número de filas para el diseño. El recuento de filas configurado debe ser bueno o igual al recuento de filas original.
   * **Columnas**: seleccione el número de columnas para el diseño. El recuento de columnas configurado debe ser bueno o igual al recuento de columnas original.

   Para cada columna se requieren los siguientes detalles:

   * **Encabezado**: texto para mostrar en el encabezado
   * **Pie de página**: texto para mostrar para el pie de página
   * **Tipo**: tipo de columna adicional. Campo o Área de Destinatario. El tipo está habilitado para tablas de marcador de posición estático. El tipo se puede definir en el nivel de columna y no en el nivel de celda. Todas las celdas de una columna extendida serían del mismo tipo. Para una tabla dinámica, todas las columnas son del tipo Campo. Para las tablas que no son marcadores de posición, no se puede definir el tipo de columnas adicionales. En este caso, el tipo de celdas adicionales en la columna extendida es el mismo que el tipo de la última columna de esa fila; y el tipo de celda en fila adicional es el mismo que el tipo de última celda de esa columna.
   * **Proporción de anchura:** proporción de los anchos de columna de la tabla.

   Para ver un ejemplo detallado del uso de tablas estáticas y dinámicas en fragmentos de diseño, consulte [Ejemplo con archivos de ejemplo: utilizando tablas estáticas y dinámicas en una letra](#examplewithsamplefiles).

1. Toque **Guardar**.

### Cargar un XDP en la administración de correspondencia {#upload-an-xdp-to-correspondence-management}

Para obtener instrucciones sobre cómo cargar/importar un XDP a la administración de correspondencia, consulte [Importación y exportación de recursos a AEM Forms](/help/forms/using/import-export-forms-templates.md).

### Prácticas recomendadas, sugerencias y trucos {#best-practices-tips-and-tricks-2}

#### Establecer el enlace predeterminado de subformulario {#set-the-default-subform-binding}

Al crear áreas de destinatario en Designer, ayuda a establecer el enlace predeterminado para todos los subformularios nuevos en &quot;ninguno&quot;.

Para definir el enlace predeterminado:

1. En Designer, toque **Herramientas** > **Opciones** > **Enlaces de datos** > **Enlace de subformularios**.

1. En la lista Enlace predeterminado para nuevos subformularios, seleccione **Ningún enlace de datos**.

Esto garantiza que los subformularios insertados mediante el comando Insertar > Subformulario o mediante la función de arrastrar y soltar desde la paleta Objeto tengan un enlace de &quot;ninguno&quot; de forma predeterminada. Esto significa que, de forma predeterminada, cualquier subformulario nuevo es un área de destinatario a menos que se le agregue contenido, se cambie su configuración de enlace o se asigne un nombre al subformulario con el sufijo &quot;_int&quot;.

#### Cumplimiento de la sección 508 {#section-compliance}

Si la carta final creada en la interfaz de usuario Crear correspondencia se utiliza para rellenar un flujo de trabajo posterior. Siga estas recomendaciones relacionadas con la Sección 508 al crear el diseño. De lo contrario, la letra PDF se muestra y puede omitir estas recomendaciones:

* Todos los subformularios de área de destinatario y todos los campos de una presentación tienen un orden de tabulación.
* Los campos con rótulos son compatibles con 508 de forma predeterminada. El atributo /field/help/speak@priority del campo se establece en &quot;custom&quot; de forma predeterminada, lo que significa que, a menos que se proporcione texto personalizado del lector de pantalla, el lector de pantalla lee el rótulo del campo.
* Los campos sin rótulos especifican una información del objeto e indican que los lectores de pantalla leen la información del objeto configurando

`/field/assist/speak@priority="toolTip"` y especificar texto de información del objeto en  `/field/assist/toolTip`.

#### Formatos de fecha en Designer y Asset Configuration Manager {#date-formats-in-designer-and-asset-configuration-manager}

Al diseñar un diseño en Designer, asegúrese de que los formatos de los campos de fecha coinciden con los formatos de fecha especificados en Formatos de visualización de datos en [Propiedades de configuración de la administración de correspondencia](/help/forms/using/cm-configuration-properties.md). Para obtener más información, consulte &quot;Formato de valores de campo y uso de patrones&quot; en la Ayuda de Designer.

#### Captura de intervalos de fechas {#capturing-date-ranges}

Cuando se trata de una combinación de fechas, como startDate - endDate, se utiliza un solo subformulario para garantizar la alineación correcta en la carta final y para minimizar el número de campos.

#### Configuración del enlace de nivel de formulario {#setting-form-level-binding}

Cuando una presentación contenga muchos campos y áreas de destinatario que estén asignados a elementos XML únicos, utilice el enlace de nivel de formulario y cree un nodo independiente para cada elemento. Los campos enlazados en el nivel de formulario se omiten al asignar datos en Administración de correspondencia.

#### No utilizar áreas de destinatario de subformulario en una página de formato {#do-not-use-subform-target-areas-in-a-master-page}

Las áreas de destinatarios de subformulario de una página de formato no están visibles en la interfaz de usuario de Administrar recursos y no se pueden asignar datos a ellas.

#### Elección de posiciones y tipos adecuados para áreas de destinatario {#choosing-appropriate-positions-and-types-for-target-areas}

Al diseñar la presentación, tenga cuidado al elegir subformularios. Si la presentación contiene un solo subformulario, puede ser de tipo variable. Una vez colocados los campos en el subformulario, puede ajustarlos en otro subformulario para que el subformulario ajustado también tenga posición variable y la presentación no se vea alterada.

#### Colocación de campos en páginas de formato {#placing-fields-on-master-pages}

Tenga en cuenta lo siguiente cuando coloque un campo en una página de formato:

* Definir el enlace de los campos de la página de formato como Usar datos globales
* No coloque el campo directamente debajo del área de página raíz de la página de formato.
* Ajuste el campo en un subformulario con nombre y asegúrese de que el enlace del subformulario con nombre está definido como Usar nombre.

## Creación de tablas mediante fragmentos de diseño {#creating-tables-using-layout-fragments}

Muchas plantillas de letras contienen tablas. Las tablas pueden ser estáticas, como una tabla de términos y condiciones, donde cada fila representa una condición y cada pieza se muestra en una columna separada. Las tablas también pueden ser dinámicas, como la información de la cuenta, que contiene información como el nombre del cliente, la identificación de la cuenta, el número de transacción y el importe de la transacción.

* **Tablas** estáticas: A veces, las tablas se crean con filas que tienen un número diferente de columnas, como para una tabla de términos y condiciones. Cada fila representa una condición y cada condición puede tener diferentes subpartes. Cada pieza se muestra en una columna separada.
* **Tablas** dinámicas: Los fragmentos de diseño permiten enlazar los campos de una tabla dinámica a los DDE de recopilación. En el momento de la generación de letras, las filas de la tabla se generan según el tamaño de los DDE de recopilación.

El DD tiene un elemento de recopilación Nominee_details que tiene un elemento compuesto con tres elementos primitivos: Nominee_name, Nominee_address y Nominee_gender.
El XDP dinámico también tiene los mismos encabezados. De este modo, puede asignar los campos XDP dinámicos con los campos de DD mencionados anteriormente.

### Ejemplo con archivos de ejemplo: Uso de tablas estáticas y dinámicas en una letra {#examplewithsamplefiles}

En este ejemplo se muestra cómo crear una tabla dinámica y una tabla estática, enlazar la tabla dinámica a DDE y, a continuación, crear una letra que incluya estas dos tablas. Al trabajar con este ejemplo, puede crear archivos desde cero o utilizar los archivos de entrada que se indican en los pasos.

1. Cree un diccionario de datos (DD) que desee utilizar en el ejemplo, tal como se representa en el gráfico.

   A continuación, seleccione DD y exporte datos de ejemplo. El archivo XML que obtiene contiene datos de Empleado y tres instancias de Nominee_details (de forma predeterminada, se descargan 3 instancias). Puede agregar o eliminar según sus necesidades). Actualice los valores y, a continuación, importe los datos de prueba en DD. El archivo CMP es el paquete y contiene el DD. Por lo tanto, importe el DD en Gestión de Correspondencia.

   Para obtener más información sobre cómo trabajar con el diccionario de datos y los datos de prueba, consulte [Diccionario de datos](/help/forms/using/data-dictionary.md#p-working-with-test-data-p).

   ![Estructura del diccionario de datos](assets/dd.jpeg)

   [Obtener archivo](assets/exportpackage_1431709897770.cmp.zip)

1. En Designer, cree dos XDP (fragmentos de diseño): una tabla dinámica y una tabla estática. Para ambos diseños:

   * Añada el subformulario a la columna de tabla. Asegúrese de cambiar la presentación del subformulario principal de la tabla a una posición variable y de quitar los enlaces del subformulario en la tabla.
   * Añada un subformulario a la celda de la tabla. Asegúrese de cambiar la presentación del subformulario principal de la tabla a una posición variable y de quitar los enlaces del subformulario en la tabla.

   O bien, utilice los XDP estáticos y dinámicos adjuntos a este paso.

   Para obtener más información sobre cómo trabajar con fragmentos de diseño, consulte [Fragmentos de diseño](#layoutfragments).
Para obtener más información sobre el diseño de diseños, consulte [Ayuda de Designer](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/).

   [Obtener archivo](assets/static.xdp.zip)

   [Obtener archivo](assets/dynamic.xdp.zip)

1. Cargue los XDP en AEM Forms.
1. Cree un fragmento de diseño basado en el XDP dinámico. La ficha Tabla de las propiedades muestra que la tabla es dinámica (campo Configuración para). El número de filas (1) y columnas (3) proviene del fragmento XDP/Layout.

   Los campos de este diseño se enlazan posteriormente al DD importado y, en la letra, el número de filas se crea dinámicamente en función del número de registros en el archivo de datos de prueba (el archivo de datos XML adjunto al DD).

   ![Creación de una pantalla de fragmento de diseño](assets/dynamictableproperties.png)

   Haga clic para abrir una imagen de tamaño completo

1. Cree un fragmento de diseño basado en el XDP estático. La ficha Tabla de las propiedades muestra que la tabla es estática (campo Configuración para). El número de filas (1) y columnas (3) proviene del fragmento XDP/Layout.

   Aquí puede cambiar el número de columnas y filas. Según lo que elija en esta pantalla, el número de filas y columnas de una tabla estática permanece fijo en la letra que se crea con esta presentación.
   [ ![Creación de una pantalla de fragmento de diseño](assets/statictableproperties.png)](assets/statictableproperties-1.png)

1. Cree una carta utilizando ambos fragmentos de diseño. Cuando inserte el XDP dinámico en la carta, establezca el enlace de sus campos a los elementos de recopilación del diccionario de datos.

   Para obtener más información sobre la creación de plantillas de letras y letras, consulte [Crear carta](/help/forms/using/create-letter.md).

1. Guarde la carta y previsualización. Cuando previsualización la carta, los valores del diccionario de datos se muestran en la carta. Para la tabla dinámica, hay tres filas. Esto se debe a que los datos de prueba tienen tres registros para estas filas.

   Para la tabla estática, hay tantas filas y columnas como especificó al crear el fragmento de diseño.

   ![Tabla estática en la letra](assets/statictableletter.png)

   Para la tabla dinámica, las tres filas aparecen según el número de registros en el archivo de datos de prueba. Esto ocurría porque, al agregar el diseño a la carta, se creaba un enlace entre los campos de la tabla dinámica y los elementos de recopilación del diccionario de datos. Los valores Nombre, Dirección y Sexo se rellenan a partir del archivo de datos de prueba utilizado.

   ![Tabla dinámica en la letra](assets/dynamictableletter.png)

## Crear una copia de un fragmento de documento {#create-a-copy-of-a-document-fragment}

Para crear rápidamente un fragmento de documento con propiedades y contenido similar a un fragmento de documento existente, puede copiarlo y pegarlo.

1. En la lista de fragmentos de documento, seleccione uno o varios fragmentos de documento. La interfaz de usuario muestra el icono Copiar.
1. Pulse Copiar. La interfaz de usuario muestra el icono Pegar. También puede elegir ir dentro de una carpeta antes de pegarla. Las distintas carpetas pueden contener recursos con los mismos nombres. Para obtener más información sobre las carpetas, consulte [Carpetas y organización de recursos](/help/forms/using/import-export-forms-templates.md#folders-and-organizing-assets).
1. Toque Pegar. Aparecerá el cuadro de diálogo Pegar. Si está copiando y pegando los fragmentos de documento en el mismo lugar, el sistema asigna automáticamente nombres y títulos a las nuevas copias de letras, pero puede editar los títulos y nombres de las letras.
1. Si es necesario, edite el Título y el Nombre con los que desea guardar la copia del fragmento de documento.
1. Toque Pegar. Se crea la copia del fragmento de documento.

