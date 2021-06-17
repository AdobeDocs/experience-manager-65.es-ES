---
title: Configuración de los complementos del Editor de texto enriquecido
description: Aprenda a configurar los complementos del Editor de texto enriquecido de Adobe Experience Manager para habilitar funcionalidades individuales.
contentOwner: AG
exl-id: 6bfd6caa-a68a-40ba-9826-4ba02cd1dbfb
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '4395'
ht-degree: 3%

---

# Configurar los complementos del Editor de texto enriquecido {#configure-the-rich-text-editor-plug-ins}

Las funcionalidades de RTE están disponibles a través de una serie de complementos, cada uno con propiedad de características. Puede configurar la propiedad de funciones para habilitar o deshabilitar, una o más características de RTE. Este artículo describe cómo configurar específicamente los complementos RTE.

Para obtener más información sobre las otras configuraciones de RTE, consulte [Configuración del editor de texto enriquecido](/help/sites-administering/rich-text-editor.md).

>[!NOTE]
>
>Cuando trabaje con CRXDE Lite, se recomienda guardar los cambios con regularidad mediante la opción [!UICONTROL Guardar todo].

## Activar un complemento y configurar la propiedad de funciones {#activateplugin}

Para activar un complemento, siga estos pasos. Algunos pasos solo son necesarios cuando configura un complemento por primera vez, ya que los nodos correspondientes no existen.

De forma predeterminada, los complementos `format`, `link`, `list`, `justify` y `control` y todas sus características están activados en RTE.

>[!NOTE]
>
>El nodo `rtePlugins` correspondiente se denomina `<rtePlugins-node>` para evitar la duplicación en este artículo.

1. Con el CRXDE Lite , busque el componente de texto del proyecto.
1. Cree el nodo principal de `<rtePlugins-node>` si no existe, antes de configurar cualquier complemento RTE:

   * Según el componente, los nodos principales son:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * un nodo de configuración alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * Son del tipo: **jcr:primaryType** `cq:Widget`
   * Ambas tienen la siguiente propiedad:

      * **Nombre** `name`
      * **Tipo** `String`
      * **Valor** `./text`


1. Según la interfaz para la que esté configurando, cree un nodo `<rtePlugins-node>`, si no existe:

   * **Nombre** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. A continuación, cree un nodo para cada complemento que desee activar:

   * **Tipo** `nt:unstructured`
   * **** Asigne un nombre al ID del complemento requerido.

Después de activar un complemento, siga estas directrices para configurar la propiedad `features`.

|  | Habilitar todas las funciones | Habilitar algunas funciones específicas | Deshabilitar todas las funciones |
|---|---|---|---|
| Nombre | características | características | características |
| Tipo | Cadena | String[] (multi-string; establezca Type en String y haga clic en Multi in CRXDE Lite) | Cadena |
| Value | `*` (un asterisco) | se establece en uno o varios valores de función | - |

## Comprender el complemento Findreplace {#findreplace}

El complemento `findreplace` no necesita ninguna configuración. Funciona de forma predeterminada.

Al utilizar la funcionalidad de reemplazo, la cadena de reemplazo que se va a reemplazar debe introducirse al mismo tiempo que la cadena de búsqueda. Sin embargo, puede hacer clic en Buscar para buscar la cadena antes de reemplazarla. Si se introduce la cadena de reemplazo después de hacer clic en Buscar, la búsqueda se restablece al principio del texto.

El cuadro de diálogo buscar y reemplazar se vuelve transparente cuando se hace clic en buscar y se vuelve opaco cuando se hace clic en reemplazar. Esto permite al autor revisar el texto que reemplazará el autor. Si los usuarios hacen clic en reemplazar todo, el cuadro de diálogo se cerrará y mostrará el número de reemplazos realizados.

## Configurar los modos de pegado {#paste-modes}

Al utilizar RTE, los autores pueden pegar contenido en uno de los tres modos siguientes:

* **Modo** del explorador: Pegue texto con la implementación de pegado predeterminada del explorador. No es un método recomendado, ya que puede introducir marcas no deseadas.

* **Modo** de texto sin formato: Pegue el contenido del portapapeles como texto sin formato. Elimina todos los elementos de estilo y formato del contenido copiado antes de insertarlos en el componente [!DNL Experience Manager].

* **Modo** MS Word: Pegue el texto, incluidas las tablas, con formato al copiar desde MS Word. No se admite la copia y el pegado de texto desde otro origen, como una página web o MS Excel, y solo se conserva el formato parcial.

### Configurar las opciones de pegado disponibles en la barra de herramientas de RTE {#configure-paste-options-available-on-the-rte-toolbar}

Puede proporcionar algunos, todos o ninguno de estos tres iconos a sus autores en la barra de herramientas de RTE:

* **[!UICONTROL Pegar (Ctrl+V)]**: Se puede preconfigurar para que se corresponda con uno de los tres modos de pegado anteriores.

* **[!UICONTROL Pegar como texto]**: Proporciona funcionalidad de modo de texto sin formato.

* **[!UICONTROL Pegar desde Word]**: Proporciona funcionalidad de modo MS Word.

Para configurar RTE para que muestre los iconos necesarios, siga estos pasos.

1. Vaya al componente, por ejemplo `/apps/<myProject>/components/text`.
1. Vaya al nodo `rtePlugins/edit`. Consulte [activar un complemento](#activateplugin) si el nodo no existe.
1. Cree la propiedad `features` en el nodo `edit` y agregue una o más de las funciones. Guarde todos los cambios.

### Configure el comportamiento del icono Pegar (Ctrl+V) y el acceso directo {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Puede preconfigurar el comportamiento del icono **[!UICONTROL Pegar (Ctrl+V)]** siguiendo estos pasos. Esta configuración también define el comportamiento del método abreviado de teclado Ctrl+V que utilizan los autores para pegar contenido.

La configuración permite los tres tipos de casos de uso siguientes:

* Pegue texto con la implementación de pegado predeterminada del explorador. No es un método recomendado, ya que puede introducir marcas no deseadas. Configurado con `browser` a continuación.

* Pegue el contenido del portapapeles como texto sin formato. Elimina todos los elementos de estilo y formato del contenido copiado antes de insertarlos en AEM componente. Configurado con `plaintext` a continuación.

* Pegue el texto, incluidas las tablas, con formato al copiar desde MS Word. No se admite la copia y el pegado de texto desde otro origen, como una página web o MS Excel, y solo se conserva el formato parcial. Configurado con `wordhtml` a continuación.

1. En el componente, vaya al nodo `<rtePlugins-node>/edit`. Cree los nodos si no existen. Para obtener más información, consulte [activación de un complemento](#activateplugin).
1. En el nodo `edit` cree una propiedad con los siguientes detalles:

   * **Nombre** `defaultPasteMode`
   * **Tipo** `String`
   * **** ValorUno de los modos de pegado  `browser`,  `plaintext` o  `wordhtml` necesarios.

### Configurar los formatos permitidos al pegar contenido {#pasteformats}

El modo pegar como Microsoft Word (`paste-wordhtml`) se puede configurar aún más para que pueda definir explícitamente qué estilos se permiten al pegar en AEM desde otro programa, como Microsoft Word.

Por ejemplo, si solo se deben permitir formatos y listas en negrita al pegar en AEM, puede filtrar los demás formatos. Esto se denomina filtrado de pegado configurable, que se puede hacer para ambos:

* [Texto](#paste-modes)
* [Vínculos](#linkstyles)

Para los vínculos, también puede definir los protocolos que se aceptan automáticamente.

Para configurar qué formatos se permiten al pegar texto en AEM desde otro programa:

1. En el componente, vaya al nodo `<rtePlugins-node>/edit`. Cree los nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. Cree un nodo en el nodo `edit` para guardar las reglas de pegado HTML:

   * **Nombre** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Cree un nodo en `htmlPasteRules` para incluir detalles de los formatos básicos permitidos:

   * **Nombre** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Para controlar los formatos individuales aceptados, cree una o más de las siguientes propiedades en el nodo `allowBasics`:

   * **Nombre** `bold`
   * **Nombre** `italic`
   * **Nombre** `underline`
   * **Nombre** `anchor`  (para vínculos y anclajes con nombre)
   * **Nombre** `image`

   Todas las propiedades son de **Type** `Boolean`, por lo que en el **Value** correspondiente puede seleccionar o quitar la marca de verificación para habilitar o deshabilitar la funcionalidad.

   >[!NOTE]
   >
   >Si no se define explícitamente, se utiliza el valor predeterminado de true y se acepta el formato .

1. También se pueden definir otros formatos utilizando una serie de otras propiedades o nodos, aplicados también al nodo `htmlPasteRules`:

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>allowBlockTags</td>
   <td>Cadena[]</td>
   <td><p>Define la lista de etiquetas de bloque permitidas.</p> <p>Algunas etiquetas de bloque posibles son:</p>
    <ul>
     <li>encabezados (h1, h2, h3)</li>
     <li>párrafos p)</li>
     <li>listas (ol, ul)</li>
     <li>tablas (tabla)</li>
    </ul> </td>
  </tr>
  <tr>
   <td>fallbackBlockTag</td>
   <td>Cadena</td>
   <td><p>Define la etiqueta de bloque utilizada para cualquier bloque que tenga una etiqueta de bloque no incluida en allowBlockTags.</p> <p> p es suficiente en la mayoría de los casos.</p> </td>
  </tr>
  <tr>
   <td>tabla</td>
   <td>nt:unstructured</td>
   <td><p>Define el comportamiento al pegar tablas.<br /> </p> <p>Este nodo debe tener la propiedad <code>allow</code> (type <code>Boolean</code>) para definir si se permite pegar tablas.</p> <p>Si <code>allow</code> está establecido en <code>false</code>, debe especificar la propiedad <code>ignoreMode</code> (type<code> String</code>) para definir cómo se gestiona el contenido de la tabla pegada. Los valores válidos para <code>ignoreMode</code> son:</p>
    <ul>
     <li><code>remove</code>: Quita el contenido de la tabla.</li>
     <li><code>paragraph</code>: Convierte celdas de tabla en párrafos.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>list</td>
   <td>nt:unstructured</td>
   <td><p>Define el comportamiento al pegar listas.<br /> </p> <p>Debe tener la propiedad <code>allow</code> (type <code>Boolean</code>) para definir si se permite el pegado de listas.</p> <p>Si <code>allow</code> está establecido en <code>false</code>, debe especificar la propiedad <code>ignoreMode</code> (type <code>String</code>) para definir cómo administrar el contenido de la lista pegado. Los valores válidos para <code>ignoreMode</code> son:</p>
    <ul>
     <li><code>remove</code>: Elimina el contenido de la lista.</li>
     <li><code>paragraph</code>: Convierte los elementos de la lista en párrafos.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Ejemplo de una estructura `htmlPasteRules` válida:

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

1. Guarde todos los cambios.

## Configuración de estilos de texto {#textstyles}

Los autores pueden aplicar Estilos para cambiar el aspecto de una parte del texto. Los estilos se basan en clases CSS predefinidas en la hoja de estilos CSS. El contenido estilizado se incluye en etiquetas `span` utilizando el atributo `class` para hacer referencia a la clase CSS. Por ejemplo:

`<span class=monospaced>Monospaced Text Here</span>`

Cuando el complemento Estilos está habilitado por primera vez, no hay estilos predeterminados disponibles. La lista emergente está vacía. Para proporcionar a los autores estilos, haga lo siguiente:

* Habilite el selector desplegable Estilo .
* Especifique la ubicación de las hojas de estilo.
* Especifique los estilos individuales que se pueden seleccionar en la lista desplegable Estilo .

Para las configuraciones posteriores (re-), por ejemplo, para añadir más estilos, siga solo las instrucciones para hacer referencia a una nueva hoja de estilo y especificar los estilos adicionales.

>[!NOTE]
>
>Los estilos también se pueden definir para [tablas o celdas de tabla](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles). Estas configuraciones requieren procedimientos separados.

### Habilitar la lista de selector desplegable Estilo {#styleselectorlist}

Esto se hace habilitando el complemento de estilos.

1. En el componente, vaya al nodo `<rtePlugins-node>/styles`. Cree los nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. Cree la propiedad `features` en el nodo `styles`:

   * **Nombre** `features`
   * **Tipo** `String`
   * **Valor** `*`  (asterisco)

1. Guarde todos los cambios.

>[!NOTE]
>
>Una vez habilitado el complemento Estilos, la lista desplegable Estilo se muestra en el cuadro de diálogo de edición. Sin embargo, la lista está vacía ya que no se ha configurado ningún estilo.

### Especificar la ubicación de la hoja de estilo {#locationofstylesheet}

A continuación, especifique la ubicación de las hojas de estilo a las que desea hacer referencia:

1. Vaya al nodo raíz del componente de texto, por ejemplo `/apps/<myProject>/components/text`.
1. Agregue la propiedad `externalStyleSheets` al nodo principal de `<rtePlugins-node>`:

   * **Nombre** `externalStyleSheets`
   * **Tipo** `String[]`  (varias cadenas; haga clic en  **** Multiin CRXDE)
   * **Valores** La ruta y el nombre de archivo de cada hoja de estilo que desea incluir. Utilice rutas de repositorio.

   >[!NOTE]
   >
   >Puede agregar referencias a hojas de estilo adicionales más adelante.

1. Guarde todos los cambios.

>[!NOTE]
>
>Al utilizar RTE en un cuadro de diálogo (IU clásica), es posible que desee especificar las hojas de estilo optimizadas para la edición de texto enriquecido. Debido a restricciones técnicas, el contexto de CSS se pierde en el editor, por lo que puede que desee emular este contexto para mejorar la experiencia WYSIWYG.
>
>El Editor de texto enriquecido utiliza un elemento DOM de contenedor con un ID de `CQrte` que puede utilizarse para proporcionar distintos estilos para ver y editar:
>
>
```
>#CQ td {
> // defines the style for viewing
> }
>```
>
>
```
>#CQrte td {
> // defines the style for editing
> }
>```

### Especifique los estilos disponibles en la lista emergente {#stylesindropdown}

1. En la definición del componente, vaya al nodo `<rtePlugins-node>/styles`, tal como se ha creado en [Activación del selector desplegable de estilos](#styleselectorlist).
1. En el nodo `styles`, cree un nuevo nodo (también denominado `styles`) para mantener la lista disponible:

   * **Nombre** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Cree un nuevo nodo bajo el nodo `styles` para representar un estilo individual:

   * **Nombre**, puede especificar el nombre, pero debería ser adecuado para el estilo
   * **Tipo** `nt:unstructured`

1. Agregue la propiedad `cssName` a este nodo para hacer referencia a la clase CSS:

   * **Nombre** `cssName`
   * **Tipo** `String`
   * **** ValorEl nombre de la clase CSS (sin un &#39;.&#39; anterior); por ejemplo, `cssClass` en lugar de `.cssClass`)

1. Agregue la propiedad `text` al mismo nodo; esto define el texto mostrado en el cuadro de selección:

   * **Nombre** `text`
   * **Tipo** `String`
   * **** ValueDescription del estilo; aparece en el cuadro de selección desplegable Estilo .

1. Guarde los cambios.

   Repita los pasos anteriores para cada estilo necesario.

### Configurar RTE para saltos de palabras óptimos en japonés {#jpwordwrap}

Los autores que utilizan AEM para crear contenido en japonés pueden aplicar un estilo a los caracteres para evitar un salto de línea cuando no sea necesario un salto. Esto permite a los autores dejar que las frases rompan en la posición deseada. El estilo de esta funcionalidad se basa en la clase CSS predefinida en la hoja de estilos CSS.

>[!NOTE]
>
>Esta función requiere al menos AEM 6.5 Service Pack 1.

Para crear el estilo que los autores pueden aplicar al texto en japonés, siga estos pasos:

1. Cree un nuevo nodo en el nodo de estilos. Consulte [especificar un nuevo estilo](#stylesindropdown).
   * Nombre: `jpn-word-wrap`
   * Tipo: `nt:unstructure`

1. Agregue la propiedad `cssName` al nodo para hacer referencia a la clase CSS. Este nombre de clase es un nombre reservado para la función de ajuste de palabras en japonés.
   * Nombre: `cssName`
   * Tipo: `String`
   * Valor: `jpn-word-wrap` (sin un `.` anterior)

1. Agregue el texto de la propiedad al mismo nodo. El valor es el nombre del estilo que los autores ven al seleccionar el estilo.
   * Nombre: `text`
*Tipo: 
`String`
   * Value: `Japanese word-wrap`

1. Cree una hoja de estilo y especifique su ruta. Consulte [especificar la ubicación de la hoja de estilo](#locationofstylesheet). Agregue el siguiente contenido a la hoja de estilo. Cambie el color de fondo como desee.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Hoja de estilo para que la función de ajuste de palabras en japonés esté disponible para los autores](assets/rte_jpwordwrap_stylesheet.jpg)

## Configuración de los formatos de párrafo {#paraformats}

Cualquier texto creado en RTE se coloca dentro de una etiqueta de bloque, siendo el valor predeterminado `<p>`. Al habilitar el complemento `paraformat`, se especifican etiquetas de bloque adicionales que se pueden asignar a los párrafos mediante una lista desplegable de selección. Los formatos de párrafo determinan el tipo de párrafo asignando la etiqueta de bloque correcta. El autor puede seleccionarlos y asignarlos mediante el selector de formato. Las etiquetas de bloque de ejemplo incluyen, entre otras, el párrafo estándar &lt;p> y los encabezados &lt;h1>, &lt;h2>, entre otros.

>[!CAUTION]
>
>Este complemento no es adecuado para contenido con estructura compleja, como listas o tablas.

>[!NOTE]
>
>Si una etiqueta de bloque, por ejemplo una etiqueta &lt;hr> , no se puede asignar a un párrafo, no es un caso de uso válido para un complemento de formato.

Cuando el complemento Formatos de párrafo está habilitado por primera vez, no hay disponibles formatos de párrafo predeterminados. La lista emergente está vacía. Para proporcionar a los autores formatos de párrafo, haga lo siguiente:

* Active la lista de selector desplegable Formato .
* Especifique las etiquetas de bloque que se pueden seleccionar como formatos de párrafo desde la lista desplegable.

Para las configuraciones posteriores (re-), digamos para añadir más formatos, siga solamente la parte relevante de las instrucciones.

### Activación del selector desplegable Formato {#formatselectorlist}

Primero habilite el complemento paraformat :

1. En el componente, vaya al nodo `<rtePlugins-node>/paraformat`. Cree los nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. Cree la propiedad `features` en el nodo `paraformat`:

   * **Nombre** `features`
   * **Tipo** `String`
   * **Valor** `*`  (asterisco)

>[!NOTE]
Si el complemento no está configurado, se habilitan los siguientes formatos predeterminados:
* Párrafo ( `<p>`)
* Encabezado 1 ( `<h1>`)
* Encabezado 2 ( `<h2>`)
* Encabezado 3 ( `<h3>`)



>[!CAUTION]
Al configurar los formatos de párrafo de RTE, no elimine la etiqueta de párrafo &lt;p> como opción de formato. Si se elimina la etiqueta `<p>` , el autor del contenido no puede seleccionar la opción **Paragraph format** aunque haya otros formatos configurados.

### Especificar los formatos de párrafo disponibles {#paraformatsindropdown}

Los formatos de párrafo pueden seleccionarse mediante:

1. En la definición del componente, vaya al nodo `<rtePlugins-node>/paraformat`, tal como se ha creado en [Activación del selector desplegable de formato](#styleselectorlist).
1. En el nodo `paraformat` cree un nuevo nodo para incluir la lista de formatos:

   * **Nombre** `formats`
   * **Tipo** `cq:WidgetCollection`

1. Cree un nuevo nodo bajo el nodo `formats`, que contiene detalles de un formato individual:

   * **Nombre**, puede especificar el nombre, pero debería ser adecuado para el formato (por ejemplo, myParagraph, myheader1).
   * **Tipo** `nt:unstructured`

1. A este nodo, añada la propiedad para definir la etiqueta de bloque utilizada:

   * **Nombre** `tag`
   * **Tipo** `String`
   * **** ValueEtiqueta de bloque para el formato; por ejemplo: p, h1, h2, etc.

      No es necesario introducir los corchetes angulares delimitadores.

1. Al mismo nodo agregue otra propiedad para que el texto descriptivo aparezca en la lista desplegable:

   * **Nombre** `description`
   * **Tipo** `String`
   * **** ValorTexto descriptivo para este formato; por ejemplo, Párrafo, Encabezado 1, Encabezado 2, etc. Este texto se muestra en la lista de selección Formato.

1. Guarde los cambios.

   Repita los pasos para cada formato necesario.

>[!CAUTION]
Si define formatos personalizados, se eliminarán los formatos predeterminados (`<p>`, `<h1>`, `<h2>` y `<h3>`). Vuelva a crear el formato `<p>` porque es el formato predeterminado.

## Configuración de caracteres especiales {#spchar}

En una instalación de AEM estándar, cuando el complemento `misctools` está habilitado para caracteres especiales (`specialchars`), inmediatamente se puede utilizar una selección predeterminada; por ejemplo, los símbolos copyright y marca comercial.

Puede configurar el RTE para que su propia selección de caracteres esté disponible; definiendo caracteres distintos o una secuencia completa.

>[!CAUTION]
Al añadir sus propios caracteres especiales, se anula la selección predeterminada. Si es necesario, (vuelva a)definir estos caracteres en su propia selección.

### Definir un solo carácter {#definesinglechar}

1. En el componente, vaya al nodo `<rtePlugins-node>/misctools`. Cree los nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. Cree la propiedad `features` en el nodo `misctools`:

   * **Nombre** `features`
   * **Tipo** `String[]`
   * **Valor** `specialchars`

          (o `String / *` si se aplican todas las funciones para este complemento)

1. En `misctools` cree un nodo para mantener las configuraciones de caracteres especiales:

   * **Nombre** `specialCharsConfig`
   * **Tipo** `nt:unstructured`

1. En `specialCharsConfig` cree otro nodo para guardar la lista de caracteres:

   * **Nombre** `chars`
   * **Tipo** `nt:unstructured`

1. En `chars` agregue un nuevo nodo para contener una definición de carácter individual:

   * **** Nombre: puede especificar el nombre, pero debe reflejar el carácter. por ejemplo, la mitad.
   * **Tipo** `nt:unstructured`

1. A este nodo agregue la siguiente propiedad:

   * **Nombre** `entity`
   * **Tipo** `String`
   * **** Valore la representación HTML del carácter requerido; por ejemplo,  `&189;` para la fracción una mitad.

1. Guarde los cambios.

En CRXDE, una vez guardada la propiedad, se muestra el carácter representado. Consulte a continuación el ejemplo de la mitad. Repita los pasos anteriores para que los autores tengan más caracteres especiales disponibles.

![En CRXDE, añada un solo carácter para que esté disponible en la ](assets/chlimage_1-106.png "barra de herramientas RTE. En CRXDE, añada un solo carácter para que esté disponible en la barra de herramientas RTE")

### Definir un rango de caracteres {#definerangechar}

1. Utilice los pasos del 1 al 3 desde [Definición de un solo carácter](#definesinglechar).
1. En `chars` agregue un nuevo nodo para mantener la definición del intervalo de caracteres:

   * **** Nombre: puede especificar el nombre, pero debe reflejar el intervalo de caracteres; por ejemplo, lápices.
   * **Tipo** `nt:unstructured`

1. Bajo este nodo (cuyo nombre depende del rango de caracteres especial), agregue las dos propiedades siguientes:

   * **Nombre** `rangeStart`

      **Tipo** `Long`
      **** Valore la presentación  [](https://unicode.org/) Unicode (decimal) del primer carácter del rango

   * **Nombre** `rangeEnd`

      **Tipo** `Long`
      **** Valore la presentación  [](https://unicode.org/) Unicode (decimal) del último carácter del rango

1. Guarde los cambios.

   Por ejemplo, si define un intervalo de 9998 a 1000, obtendrá los siguientes caracteres.

   ![En CRXDE, defina un rango de caracteres para que estén disponibles en RTE](assets/chlimage_1-107.png)

   *Figura: En CRXDE, defina un rango de caracteres para que estén disponibles en RTE*

   ![Los caracteres especiales disponibles en RTE se muestran a los autores en una ](assets/rtepencil.png "ventana emergenteLos caracteres especiales disponibles en RTE se muestran a los autores en una ventana emergente")

## Configuración de estilos de tabla {#tablestyles}

Los estilos se suelen aplicar al texto, pero también se puede aplicar un conjunto independiente de estilos en una tabla o en unas pocas celdas de la tabla. Estos estilos están disponibles para los autores del cuadro de selector Estilo de las propiedades Celda o Propiedades de tabla. Los estilos están disponibles al editar una tabla dentro de un componente de texto (o derivado) y no en el componente de tabla estándar.

>[!NOTE]
Puede definir estilos para tablas y celdas solo para la IU clásica.

>[!NOTE]
Copiar y pegar tablas en o desde el componente RTE depende del explorador. No es compatible de serie para todos los exploradores. Puede obtener resultados variados según la estructura de la tabla y el navegador. Por ejemplo, cuando copia y pega una tabla en un componente RTE en Mozilla Firefox en la IU clásica y la IU táctil, no se conserva el diseño de la tabla.

1. Dentro del componente, vaya al nodo `<rtePlugins-node>/table`. Cree los nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. Cree la propiedad `features` en el nodo `table`:

   * **Nombre** `features`
   * **Tipo** `String`
   * **Valor** `*`

   >[!NOTE]
   Si no desea habilitar todas las funciones de la tabla, puede crear la propiedad `features` como:
   * **Tipo** `String[]`

   * **Los valores** son uno o ambos, de los siguientes, según sea necesario:
      * `table` permitir la edición de las propiedades de la tabla; incluidos los estilos.
      * `cellprops` para permitir la edición de propiedades de celda, incluidos los estilos.


1. Defina la ubicación de las hojas de estilo CSS para consultarlas. Consulte [Especificación de la ubicación de la hoja de estilo](#locationofstylesheet) ya que es la misma que al definir [estilos para texto](#textstyles). La ubicación se puede definir si ha definido otros estilos.
1. En el nodo `table` cree los siguientes nodos nuevos (según sea necesario):

   * Para definir estilos para toda la tabla (disponible en **Table properties**):

      * **Nombre** `tableStyles`
      * **Tipo** `cq:WidgetCollection`
   * Para definir estilos para celdas individuales (disponibles en **Cell properties**):

      * **Nombre** `cellStyles`
      * **Tipo** `cq:WidgetCollection`


1. Cree un nuevo nodo (en el nodo `tableStyles` o `cellStyles` según corresponda) para representar un estilo individual:

   * **** Nombre, puede especificar el nombre, pero debe reflejar el estilo.
   * **Tipo** `nt:unstructured`

1. En este nodo, cree las propiedades:

   * Definición del estilo CSS al que se hace referencia

      * **Nombre** `cssName`
      * **Tipo** `String`
      * **** Valore el nombre de la clase CSS (sin un precedente  `.`, por ejemplo,  `cssClass` en lugar de  `.cssClass`)
   * Definición de un texto descriptivo para que aparezca en el selector desplegable

      * **Nombre** `text`
      * **Tipo** `String`
      * **** Valore el texto que aparece en la lista de selección


1. Guarde todos los cambios.

Repita los pasos anteriores para cada estilo necesario.

### Configuración de encabezados ocultos en tablas para accesibilidad {#hiddenheader}

A veces, puede crear tablas de datos sin texto visual en el encabezado de una columna suponiendo que el propósito del encabezado esté implícito en la relación visual de la columna con otras columnas. En este caso, es necesario proporcionar texto interno oculto dentro de la celda en la celda del encabezado para permitir que los lectores de pantalla y otras tecnologías de asistencia ayuden a los lectores con distintas necesidades a comprender el propósito de la columna.

Para mejorar la accesibilidad en estos escenarios, RTE admite celdas de encabezado ocultas. Además, proporciona ajustes de configuración relacionados con encabezados ocultos en tablas. Esta configuración le permite aplicar estilos CSS en encabezados ocultos en los modos de edición y previsualización. Para ayudar a los autores a identificar encabezados ocultos en el modo de edición, incluya los siguientes parámetros en el código:

* `hiddenHeaderEditingCSS`: Especifica el nombre de la clase CSS que se aplica en la celda de encabezado oculto, cuando se edita RTE.
* `hiddenHeaderEditingStyle`: Especifica una cadena de estilo que se aplica en la celda de encabezado oculto cuando se edita RTE.

Si especifica la CSS y la cadena Estilo en el código, la clase CSS tiene prioridad sobre la cadena de estilo y puede sobrescribir cualquier cambio de configuración que realice la cadena Estilo.

Para ayudar a los autores a aplicar CSS en encabezados ocultos en el modo de vista previa, puede incluir los siguientes parámetros en el código:

* `hiddenHeaderClassName`: Especifica el nombre de la clase CSS que se aplica en la celda de encabezado oculto en el modo de vista previa.
* `hiddenHeaderStyle`: Especifica una cadena Style que se aplica a la celda de encabezado oculto en el modo de vista previa.

Si especifica la CSS y la cadena Estilo en el código, la clase CSS tiene prioridad sobre la cadena de estilo y puede sobrescribir cualquier cambio de configuración que realice la cadena Estilo.

## Agregar diccionarios para el corrector ortográfico {#adddict}

Cuando se activa el complemento de revisión ortográfica, el RTE utiliza diccionarios para cada idioma adecuado. A continuación, se seleccionan según el idioma del sitio web tomando la propiedad de idioma del subárbol o extrayendo el idioma de la dirección URL; por ejemplo. la rama `/en/` se marca como inglés y la rama `/de/` como alemán.

>[!NOTE]
El mensaje `Spell checking failed` se ve si se intenta comprobar un idioma que no está instalado. Los diccionarios estándar se encuentran en `/libs/cq/spellchecker/dictionaries`, junto con los archivos Léame correspondientes. No modifique los archivos.

Una instalación de AEM estándar incluye los diccionarios para inglés americano (`en_us`) e inglés británico (`en_gb`). Para agregar más diccionarios, siga estos pasos.

1. Vaya a la página [https://extensions.openoffice.org/](https://extensions.openoffice.org/).

1. Realice una de las siguientes acciones para encontrar el diccionario que elija:

   * Busque el diccionario de su elección de idioma. En la página de diccionario, busque el vínculo a la página web del autor o la fuente original. Busque los archivos de diccionario para v2.x en una página de este tipo.
   * Busque archivos de diccionario v2.x en [https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries](https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries).

1. Descargue el archivo con las definiciones ortográficas. Extraiga el contenido del archivo en su sistema de archivos.

   >[!CAUTION]
   Solo se admiten los diccionarios con el formato `MySpell` para OpenOffice.org v2.0.1 o anterior. Como los diccionarios ahora son archivos de archivo, se recomienda que verifique el archivo después de descargarlo.

1. Busque los archivos .aff y .dic . Mantener nombre de archivo en minúsculas. Por ejemplo, `de_de.aff` y `de_de.dic`.
1. Cargue los archivos .aff y .dic en el repositorio en `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
El corrector ortográfico RTE está disponible bajo demanda. No se ejecuta automáticamente cuando empieza a escribir texto. Para ejecutar el corrector ortográfico, haga clic en [!UICONTROL Corrector ortográfico] en la barra de herramientas. RTE comprueba la ortografía de las palabras y resalta las palabras mal escritas.
Si incorpora cualquier cambio que sugiera el corrector ortográfico, el estado del texto cambia y las palabras mal escritas ya no se resaltan. Para ejecutar el corrector ortográfico, toque o haga clic de nuevo en el botón corrector ortográfico.

## Configurar el tamaño del historial para acciones de deshacer y rehacer {#undohistory}

RTE permite a los autores deshacer o rehacer algunas de las últimas ediciones. De forma predeterminada, se almacenan 50 ediciones en el historial. Puede configurar este valor según sea necesario.

1. Dentro del componente, vaya al nodo `<rtePlugins-node>/undo`. Cree estos nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. En el nodo `undo` cree la propiedad:

   * **Nombre** `maxUndoSteps`
   * **Tipo** `Long`
   * **** Valore el número de pasos de deshacer que desea guardar en el historial. El valor predeterminado es 50. Utilice `0` para desactivar/rehacer completamente.

1. Guarde los cambios.

## Configuración del tamaño de la pestaña {#tabsize}

Cuando se presiona el carácter de tabulación dentro de cualquier texto, se inserta un número predefinido de espacios. de forma predeterminada, se trata de tres espacios de no separación y un espacio.

Para definir el tamaño de la pestaña:

1. En el componente, vaya al nodo `<rtePlugins-node>/keys`. Cree los nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. En el nodo `keys` cree la propiedad:

   * **Nombre** `tabSize`
   * **Tipo** `String`
   * **** Valore el número de caracteres de espacio que se utilizarán en la tabulación.

1. Guarde los cambios.

## Definir margen de sangría {#indentmargin}

Cuando la sangría está activada (opción predeterminada), puede definir el tamaño de la sangría:

>[!NOTE]
Este tamaño de guión solo se aplica a los párrafos (bloques) del texto; no afecta a la sangría de listas reales.

1. Dentro del componente, vaya al nodo `<rtePlugins-node>/lists`. Cree estos nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. En el nodo `lists` cree el parámetro `identSize`:

   * **Nombre**: `identSize`
   * **Tipo**: `Long`
   * **Valor**: número de píxeles necesarios para el margen de sangría.

## Configuración de la altura del espacio editable {#editablespace}

>[!NOTE]
Esto solo es aplicable cuando se utiliza el RTE en un cuadro de diálogo (no la edición in situ en la IU clásica).

Puede definir la altura del espacio editable que se muestra en el cuadro de diálogo del componente:

1. En el nodo `../items/text` de la definición del cuadro de diálogo para el componente, cree una nueva propiedad:

   * **Nombre** `height`
   * **Tipo** `Long`
   * **** Valore la altura del lienzo de edición en píxeles.

   >[!NOTE]
   Esto no cambia la altura de la ventana de diálogo.

1. Guarde los cambios.

## Configuración de estilos y protocolos para vínculos {#linkstyles}

Al agregar vínculos en AEM, puede definir:

* Los estilos CSS que se van a utilizar
* Los protocolos aceptados automáticamente

Para configurar cómo se agregan vínculos en AEM desde otro programa, defina las reglas HTML.

1. Con el CRXDE Lite , busque el componente de texto del proyecto.
1. Cree un nuevo nodo en el mismo nivel que `<rtePlugins-node>`, es decir, cree el nodo en el nodo principal de `<rtePlugins-node>`:

   * **Nombre** `htmlRules`
   * **Tipo** `nt:unstructured`

   >[!NOTE]
   El nodo `../items/text` tiene la propiedad :
   * **Nombre** `xtype`
   * **Tipo** `String`
   * **Valor** `richtext`

   La ubicación del nodo `../items/text` puede variar, según la estructura del cuadro de diálogo; dos ejemplos son:
   * `/apps/myProject>/components/text/dialog/items/text`
   * `/apps/<myProject>/components/text/dialog/items/panel/items/text`


1. En `htmlRules`, cree un nuevo nodo.

   * **Nombre** `links`
   * **Tipo** `nt:unstructured`

1. En el nodo `links` defina las propiedades como sea necesario:

   * Estilo CSS para vínculos internos:

      * **Nombre** `cssInternal`
      * **Tipo** `String`
      * **** Valore el nombre de la clase CSS (sin un &#39;.&#39; anterior); por ejemplo, `cssClass` en lugar de `.cssClass`)
   * Estilo CSS para vínculos externos

      * **Nombre** `cssExternal`
      * **Tipo** `String`
      * **** Valore el nombre de la clase CSS (sin un &#39;.&#39; anterior); por ejemplo, `cssClass` en lugar de `.cssClass`)
   * Matriz de **protocolos** válidos. Los protocolos admitidos son `http://`, `https://`, `file://` y `mailto:`.

      * **Nombre** `protocols`
      * **Tipo** `String[]`
      * **Valores**: uno o más protocolos
   * **defaultProtocol**  (propiedad del tipo  **String**): Protocolo que se utilizará si el usuario no especificó uno explícitamente.

      * **Nombre** `defaultProtocol`
      * **Tipo** `String`
      * **Valor**: uno o más protocolos predeterminados
   * Definición de cómo gestionar el atributo target de un vínculo. Cree un nuevo nodo:

      * **Nombre** `targetConfig`
      * **Tipo** `nt:unstructured`

      En el nodo `targetConfig`: defina las propiedades requeridas:

      * Especifique el modo de destino:

         * **Nombre** `mode`
         * **Tipo** `String`)
         * **Valores** :

            * `auto`: significa que se elige un objetivo automático

               (especificado por la propiedad `targetExternal` para vínculos externos o `targetInternal` para vínculos internos).

            * `manual`: no aplicable en este contexto
            * `blank`: no aplicable en este contexto
      * El objetivo para los vínculos internos:

         * **Nombre** `targetInternal`
         * **Tipo** `String`
         * **** Valore el objetivo para los vínculos internos (solo se usa cuando el modo es  `auto`)
      * El destino de los vínculos externos:

         * **Nombre** `targetExternal`
         * **Tipo** `String`
         * **** Valore el objetivo para los vínculos externos (solo se utiliza cuando el modo es  `auto`).








1. Guarde todos los cambios.
