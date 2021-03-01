---
title: Introducción a la creación de formularios adaptables
seo-title: Introducción a la creación de formularios adaptables
description: AEM Forms proporciona una interfaz fácil de usar pero potente para la creación de formularios adaptables. Proporciona una serie de componentes y herramientas que puede utilizar para crear formularios.
seo-description: AEM Forms proporciona una interfaz fácil de usar pero potente para la creación de formularios adaptables. Proporciona una serie de componentes y herramientas que puede utilizar para crear formularios.
uuid: 3b150507-41b9-47c2-a94c-f85b903b2274
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction, author
discoiquuid: ba70921e-db7e-43f6-902c-1065d3b13aef
docset: aem65
translation-type: tm+mt
source-git-commit: 103468b8e6e5bdf870156f85b7f547f190044561
workflow-type: tm+mt
source-wordcount: '3169'
ht-degree: 2%

---


# Introducción a la creación de formularios adaptables {#introduction-to-authoring-adaptive-forms}

## Información general {#overview}

Los formularios adaptables le permiten crear formularios atractivos, interactivos, dinámicos y adaptables. AEM Forms proporciona una interfaz de usuario intuitiva y componentes integrados para crear y trabajar con formularios adaptables. Puede elegir crear un formulario adaptable basado en un modelo o esquema de formulario o sin un modelo de formulario. Es importante elegir cuidadosamente el modelo de formulario que no solo se adapte a sus necesidades, sino que amplíe sus inversiones y recursos de infraestructura existentes. Puede elegir entre las siguientes opciones para crear un formulario adaptable:

* **Uso de un modelo de datos de formulario**
   [La ](../../forms/using/data-integration.md) integración de datos permite integrar entidades y servicios de distintos orígenes de datos en un modelo de datos de formulario que se puede utilizar para crear formularios adaptables. Elija el modelo de datos de formulario si el formulario adaptable que está creando implica recuperar y escribir datos desde y hacia múltiples fuentes de datos.

* **Uso de una**
plantilla de formulario XDPSe trata de un modelo de formulario ideal si tiene inversiones en formularios XFA o XDP. Proporciona una forma directa de convertir los formularios basados en XFA en formularios adaptables. Cualquier regla XFA existente se conserva en los formularios adaptables asociados. Los formularios adaptables resultantes admiten construcciones XFA, como validaciones, eventos, propiedades y patrones.

* **El uso de una definición de esquema XML (XSD) o de esquemas JSON**
SchemaXML y JSON representa la estructura en la que el sistema back-end de su organización produce o consume datos. Puede asociar el esquema a un formulario adaptable y utilizar sus elementos para agregar contenido dinámico al formulario adaptable. Los elementos del esquema estarán disponibles para su uso en la ficha Objetos del modelo de datos del navegador de contenido al crear formularios adaptables.

* **Uso de ninguno o sin un**
modelo de formularioLos formularios adaptables creados con esta opción no utilizan ningún modelo de formulario. El XML de datos generado a partir de estos formularios tiene una estructura plana con campos y valores correspondientes.

Para obtener más información sobre la creación de un formulario adaptable, consulte [Creación de un formulario adaptable](../../forms/using/creating-adaptive-form.md).

## IU de creación de formularios adaptable {#adaptive-form-authoring-ui}

La IU táctil para la creación de formularios adaptables es intuitiva y proporciona:

* Funcionalidad de arrastrar y soltar
* Componentes de formulario estándar
* Repositorio integrado para recursos

Al crear un formulario adaptable nuevo o editar uno existente, se utilizan los siguientes elementos de la interfaz de usuario:

* [Barra lateral](#sidebar)
* [Barra de herramientas de página](#page-toolbar)
* [Barra de herramientas de componentes](#component-toolbar)
* [Página de formulario adaptable](#af-page)

![IU de creación de formularios adaptable](assets/formeditor.png)

**A.** Barra lateral  **B.** Barra de herramientas de página  **C.** Página de formulario adaptable

### Barra lateral {#sidebar}

La barra lateral le permite

* Consulte el contenido del formulario, como paneles, componentes, campos y presentación.
* Edite las propiedades del componente.
* Busque, vea y utilice recursos en su repositorio de AEM Digital Asset Management (DAM).
* Añada componentes al formulario.

![Barra lateral](assets/sidebar-comps.png)

**A.** Explorador de contenido  **B.** Explorador de propiedades  **C.** Explorador de recursos  **D.** Navegador de componentes

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

La barra lateral consta de los siguientes navegadores:

* **Navegador de**
contenidoEn el navegador de contenido, puede ver

   * **Objetos de**
formularioMuestra la jerarquía de objetos del formulario. El autor puede desplazarse a un componente de formulario específico tocando ese elemento en el árbol de objetos del formulario. El autor puede buscar objetos y reorganizarlos desde este árbol.

   * **Objetos del modelo de**
datosPermite ver la jerarquía del modelo de formulario.
Permite arrastrar y soltar elementos de modelo de formulario en el formulario adaptable. Los elementos añadidos se convierten automáticamente en componentes de formulario conservando sus propiedades originales. Puede ver objetos del modelo de datos cuando el formulario utiliza un esquema XML, un esquema JSON o una plantilla XDP.

* **Explorador de propiedades**

   Permite editar las propiedades de un componente. Las propiedades cambian según un componente. Para ver las propiedades del contenedor de formulario adaptable:

   Seleccione un componente y, a continuación, pulse ![nivel de campo](assets/field-level.png) > **[!UICONTROL Contenedor de formulario adaptable]** y, a continuación, pulse ![cmppr](assets/cmppr.png).

* **Navegador de recursos**

   Segmenta contenido de distintos tipos, como imágenes, documentos, páginas, películas, etc.

* **Navegador de componentes**

   Incluye componentes que se pueden utilizar para crear un formulario adaptable. Puede arrastrar componentes desde al formulario adaptable para agregar elementos de formulario y configurar elementos agregados según los requisitos. En la tabla siguiente se describen los componentes enumerados en el navegador de componentes.

<table>
 <tbody>
  <tr>
   <th><strong>Componente</strong></th>
   <th><strong>Funcionalidad</strong></th>
  </tr>
  <tr>
   <td>Bloque de Adobe Sign</td>
   <td>Agrega un bloque de texto con marcadores de posición para que los campos se rellenen al firmar con Adobe Sign.</td>
  </tr>
  <tr>
   <td>Botón</td>
   <td>Agrega un botón, que puede configurar para realizar acciones como guardar, restablecer, ir a continuación, ir anterior, etc.</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>Agrega validación de CAPTCHA mediante el servicio Google reCAPTCHA. Para obtener más información, consulte <a href="../../forms/using/captcha-adaptive-forms.md" target="_blank">Uso de CAPTCHA en formularios adaptables</a>.</td>
  </tr>
  <tr>
   <td>Gráfico</td>
   <td>Agrega un gráfico que puede usar en formularios y documentos adaptables para la representación visual de datos bidimensionales en paneles repetibles y filas de tabla.</td>
  </tr>
  <tr>
   <td>Casilla de verificación</td>
   <td>Agrega una casilla de verificación.</td>
  </tr>
  <tr>
   <td>Campo de introducción de fecha</td>
   <td>Utilice el componente Campo de entrada de fecha en el formulario para permitir a los clientes rellenar los campos de día, mes y año por separado en tres cuadros. Puede personalizar el aspecto del componente y cambiar el formato de fecha. Por ejemplo, puede permitir que sus clientes introduzcan fechas en formato MM/DD/AAAA o DD/MM/AAAA .</td>
  </tr>
  <tr>
   <td>Selector de fecha</td>
   <td>Agrega un campo de calendario para elegir una fecha.</td>
  </tr>
  <tr>
   <td>Fragmento de documento</td>
   <td>Permite añadir componentes reutilizables de una correspondencia.</td>
  </tr>
  <tr>
   <td>Grupo de fragmentos de documento</td>
   <td>Permite agregar un grupo de fragmentos de documento relacionados que se pueden usar en una plantilla de carta como una sola unidad.</td>
  </tr>
  <tr>
   <td>Lista desplegable</td>
   <td>Añade una lista desplegable: selección única o múltiple</td>
  </tr>
  <tr>
   <td>Correo electrónico</td>
   <td><p>Agrega un campo para capturar la dirección de correo electrónico. El componente Correo electrónico, de forma predeterminada, valida las direcciones de correo electrónico con la siguiente expresión regular.</p> <p><code>^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>Adjuntar archivo</td>
   <td><p>Agrega un botón que permite a los usuarios examinar y adjuntar documentos de apoyo a un formulario. Puede adjuntar varios archivos a un componente Archivo adjunto. También puede especificar el **[!UICONTROL Tamaño máximo de archivo]** y **[!UICONTROL Tipos de archivo compatibles]** para los archivos adjuntos en el navegador de propiedades del componente. </p> <p><strong> Nota: </strong><ul> <li> El componente no admite adjuntar archivos con un nombre de archivo que empiece por caracteres (.), que contengan caracteres \ / : * ? " &lt; &gt; | ; % $, o que contiene nombres de archivo especiales reservados para el sistema operativo Windows como nul, prn, con, lpt o com. </li> <li> Para adjuntar varios archivos a un componente de archivo adjunto abierto en el explorador Apple Safari, seleccione y adjunte archivos uno a uno. No puede seleccionar y adjuntar varios archivos a la vez.</li> <li>El componente Archivo adjunto es compatible con un conjunto predefinido de formatos de archivo en formularios adaptables habilitados para Adobe Sign. Para obtener más información, consulte <a href="https://helpx.adobe.com/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">Formatos de archivo compatibles</a>. </li></ul></p> </td>
  </tr>
  <tr>
   <td>Lista de archivos adjuntos</td>
   <td>Agrega un campo que enumera todos los archivos adjuntos cargados mediante el componente Archivo adjunto.</td>
  </tr>
  <tr>
   <td>Encabezado<br /> </td>
   <td>Agrega el encabezado de página que generalmente incluye el logotipo de una corporación, el título del formulario y el resumen.<br /> </td>
  </tr>
  <tr>
   <td>Pie de página</td>
   <td>Agrega el pie de página que generalmente incluye información de copyright y vínculos a otras páginas. </td>
  </tr>
  <tr>
   <td>Imagen</td>
   <td>Permite insertar una imagen.</td>
  </tr>
  <tr>
   <td>Opción de imagen</td>
   <td>Permite a los clientes seleccionar una imagen para proporcionar información. Puede utilizar la información para proporcionar servicios personalizados a sus clientes.</td>
  </tr>
  <tr>
   <td>Botón Siguiente</td>
   <td>Agrega un botón para desplazarse al panel siguiente de un formulario.</td>
  </tr>
  <tr>
   <td>Cuadro numérico</td>
   <td>Añade un campo para capturar valores numéricos</td>
  </tr>
  <tr>
   <td>Stepper numérico</td>
   <td>Utilice Numeric Stepper en el formulario para permitir que los clientes introduzcan un valor numérico, que puede aumentar o disminuir en función de un paso predefinido.</td>
  </tr>
  <tr>
   <td>Panel</td>
   <td><p>Agrega un panel o subpanel.</p> <p>También puede agregar un componente de panel desde la barra de herramientas del panel principal con el botón <span class="uicontrol">Agregar panel secundario</code>. Del mismo modo, puede agregar una barra de herramientas específica del panel mediante el botón <span class="uicontrol">Agregar barra de herramientas del panel</code>. Puede configurar la posición de la barra de herramientas del panel mediante el cuadro de diálogo Editar panel.</code></code></p> </td>
  </tr>
  <tr>
   <td>Cuadro de contraseña</td>
   <td>Agrega un campo para capturar una contraseña.</td>
  </tr>
  <tr>
   <td>Botón Anterior</td>
   <td>Agrega un botón que los usuarios necesitan para volver a la página o panel anterior.</td>
  </tr>
  <tr>
   <td>Botón de opción</td>
   <td>Agrega botones de opción.</td>
  </tr>
  <tr>
   <td>Botón Restablecer</td>
   <td>Agrega un botón para restablecer los campos del formulario.</td>
  </tr>
  <tr>
   <td>Botón Guardar</td>
   <td>Agrega un botón para guardar los datos del formulario.</td>
  </tr>
  <tr>
   <td>Firma manuscrita</td>
   <td>Agrega un campo para capturar firmas de garabatos.</td>
  </tr>
  <tr>
   <td>Separador</td>
   <td>Permite la segregación visual de paneles en el formulario.</td>
  </tr>
  <tr>
   <td>Paso de firma</td>
   <td>Muestra la información proporcionada en el formulario y los campos de firma para que el usuario verifique y firme el formulario.</td>
  </tr>
  <tr>
   <td>Texto</td>
   <td>Permite especificar texto estático.</td>
  </tr>
  <tr>
   <td>Botón de envío</td>
   <td>Agrega un botón de envío para enviar el formulario a la acción de envío configurada.</td>
  </tr>
  <tr>
   <td>Paso de resumen</td>
   <td>Envía el formulario y muestra el texto de resumen que especifican los autores tras enviarlo. </td>
  </tr>
  <tr>
   <td>Cambiar</td>
   <td>Agrega un conmutador que realiza una acción de alternancia o de activación/desactivación. No se pueden agregar más de dos opciones en el componente Conmutar. Dado que un conmutador solo puede tener dos valores: On o Off, obligatorio no es aplicable. Se guarda al menos un valor independientemente de la entrada del usuario. <br /> </td>
  </tr>
  <tr>
   <td>Tabla</td>
   <td>Agrega una tabla que le permite organizar los datos en filas y columnas. </td>
  </tr>
  <tr>
   <td>Teléfono</td>
   <td><p>Agrega un campo para capturar el número de teléfono. El componente Teléfono permite a los autores configurar uno de los siguientes tipos de números de teléfono. Cada tipo está asociado con una expresión regular predeterminada para la validación.</p>
    <ul>
     <li>El tipo internacional está validado por <code>^[+][0-9]{0,14}$</code>.</li>
     <li>El tipo USPhoneNumber está validado por <code>{'+1 ('999') '999-9999}</code>.</li>
     <li>El tipo UKPhoneNumber está validado por <code>text{'+'99 999 999 9999}</code>.</li>
     <li>Tipo Personalizado no proporciona un patrón de validación predeterminado. Toma el valor del último tipo de número de teléfono seleccionado. También puede especificar su propio patrón de validación personalizado.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Términos y condiciones<br /> </td>
   <td>Agrega un campo que los autores pueden utilizar para especificar los términos y condiciones que deben revisar los usuarios antes de rellenar el formulario.</td>
  </tr>
  <tr>
   <td>Cuadro de texto </td>
   <td><p>Agrega un cuadro de texto en el que un usuario puede especificar la información necesaria. </p> <p>De forma predeterminada, el componente Cuadro de texto solo acepta texto sin formato. Puede habilitar un componente Cuadro de texto para que acepte Texto enriquecido. Un componente de texto Texto enriquecido habilitado proporciona opciones para agregar encabezados, cambiar estilos de caracteres (negrita, cursiva, subrayado de caracteres), crear listas ordenadas y sin ordenar, cambiar el fondo del texto y el color del texto y agregar hipervínculos. Para habilitar el texto enriquecido para un cuadro de texto, habilite la opción<strong> Permitir texto enriquecido</strong> en las propiedades del componente.</p> </td>
  </tr>
  <tr>
   <td>Título</td>
   <td>Especifica un título para el formulario adaptable.</td>
  </tr>
  <tr>
   <td>Paso de verificación</td>
   <td><p>Agrega un marcador de posición para mostrar el formulario rellenado para que el usuario lo compruebe.</p> <p><strong>Nota</strong>: El formulario adaptable que contiene el componente Verificar no admite usuarios anónimos. Además, no se recomienda utilizar el componente Verificar en un fragmento de formulario adaptable.</p> </td>
  </tr>
 </tbody>
</table>

#### Prácticas recomendadas para trabajar con componentes {#best-practices}

A continuación se indican algunas prácticas recomendadas y puntos clave que deben tenerse en cuenta al trabajar con componentes de formulario adaptables:

* Cada componente tiene propiedades asociadas que controlan su aspecto y funcionalidad. Para configurar las propiedades de un componente, pulse el componente y pulse ![cmppr](assets/cmppr.png) para abrir las propiedades del componente en el navegador Propiedades.
* Un componente se identifica con su nombre de elemento. Al pulsar ![cmppr](assets/cmppr.png), puede cambiar el nombre del componente cambiando el valor del campo **[!UICONTROL Nombre del elemento]** en el navegador de propiedades. El campo Nombre de elemento solo acepta letras, números, guiones (-) y guiones bajos (_). No se permiten otros caracteres especiales y el nombre del elemento debe comenzar con una letra.

* Puede modificar la propiedad Título de un componente de formulario adaptable en línea en el editor de formularios sin abrir el explorador Propiedades siempre que el título esté visible en el formulario. Para ello:

   1. Pulse para seleccionar un componente que tenga una propiedad **[!UICONTROL Title]** y cuya propiedad **[!UICONTROL Hide title]** esté deshabilitada.

   1. Toque ![aem_6_3_edit](assets/aem_6_3_edit.png) para que el título sea editable.

   1. Modifique el título y pulse la tecla Retorno o pulse cualquier lugar fuera del componente para guardar los cambios. Pulse la tecla Esc para descartar los cambios.

* Algunos componentes de formulario adaptables, como Correo electrónico y Teléfono, incluyen patrones de validación predeterminados. Sin embargo, puede especificar la validación personalizada actualizando el campo **[!UICONTROL Patrón de validación]** en el acordeón Patrones de las propiedades del componente. Consulte las descripciones de componentes de la tabla anterior para obtener más información sobre las validaciones predeterminadas.

* Los campos de formularios adaptables, como Cuadro numérico y Correo electrónico, se pueden configurar para incluir tipos de entrada HTML5 especializados. Cuando estos campos están enfocados en dispositivos móviles y tabletas, el teclado muestra el alfabeto, los números y los caracteres específicos por adelantado que normalmente se utilizan para introducir información en los campos. Ayuda a los usuarios a introducir la información rápidamente sin tener que alternar entre conjuntos de caracteres en el teclado. Para permitir entradas especializadas para un componente, active la casilla **[!UICONTROL Usar número de tipo HTML]** en sus propiedades de componente.

* Puede habilitar un componente Cuadro de texto para que acepte Texto enriquecido. Para habilitar el texto enriquecido para un cuadro de texto, active la casilla **[!UICONTROL Permitir texto enriquecido]** en las propiedades del componente.

* Puede activar los componentes Cuadro de texto, Correo electrónico y Teléfono para rellenar automáticamente los valores de campos como nombre, dirección, tarjeta de crédito, teléfono y correo electrónico a partir de la información almacenada en la configuración de relleno automático del explorador. Para habilitar esta función, seleccione **[!UICONTROL Enable Autofill]** en las propiedades del componente y seleccione un **[!UICONTROL Autofill Attribute]**. Cuando un usuario rellena un formulario adaptable, los valores se sugieren desde el perfil de relleno automático del explorador o se basan en los valores rellenados anteriormente por el usuario. Tenga en cuenta que el llenado automático funciona si la configuración de llenado automático está activada en el explorador del usuario.

* Especifique valores para los elementos de Botón de opción y Casilla de verificación en formato `{value}={text}` en las propiedades de los componentes.
* El componente Archivo adjunto, de forma predeterminada, permite al usuario adjuntar un solo archivo. Sin embargo, puede configurar las propiedades del componente para que admitan varios archivos adjuntos. Además, si un usuario adjunta varios archivos con el mismo nombre de archivo, los archivos adjuntos pueden causar algunos problemas. Por lo tanto, se recomienda asociar un identificador único para cada archivo adjunto enviado en el envío del formulario. Para ello:

   1. En el servidor de AEM Forms, vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
   1. Busque y pulse **[!UICONTROL Adaptive Forms Configuration Service]**.
   1. En el cuadro de diálogo Servicio de configuración de formularios adaptables, habilite **[!UICONTROL Convertir nombres de archivo en únicos]**. De forma predeterminada, está desactivado.

* Para permitir que los usuarios adjunten un PDF utilizando el explorador Safari, asegúrese de que **application/pdf** se agrega a la propiedad Tipos de archivo compatibles del componente Archivo adjunto. Los formularios adaptables creados con la versión anterior de AEM Forms pueden contener **.pdf** en lugar de **application/pdf** en la propiedad Tipos de archivo compatibles.

Para conocer las prácticas recomendadas en los formularios adaptables, consulte [Prácticas recomendadas para trabajar con formularios adaptables](/help/forms/using/adaptive-forms-best-practices.md).

>[!NOTE]
>
>Los componentes de formulario adaptables no admiten los lenguajes de derecha a izquierda (RTL). Por ejemplo, hebreo.

### Barra de herramientas de página {#page-toolbar}

La barra de herramientas de la página de la parte superior ofrece opciones que permiten obtener una vista previa del formulario, cambiar las propiedades del formulario y editar la presentación del formulario. Puede obtener una vista previa del formulario cuando lo crea y realizar los cambios correspondientes. En la barra de herramientas de la página, verá:

* **Alternar panel lateral del** ![panel lateral](assets/toggle-side-panel.png): Permite mostrar u ocultar la barra lateral.

* **Información de la** ![página, temas-opciones](assets/theme-options.png): Permite ver las propiedades de página, publicar o cancelar la publicación de un formulario, iniciar un flujo de trabajo de formulario y abrir el formulario en la IU clásica.

* **** ![Regla de emulación](assets/ruler.png): Permite emular el aspecto del formulario para diferentes tamaños de visualización, como tabletas y teléfonos.

* **Editar**: Permite seleccionar otros modos, como:  **[!UICONTROL Editar]**,  **[!UICONTROL Estilo]**,  **[!UICONTROL Desarrollador]** y  **[!UICONTROL Diseño]**.

   * **Editar**: Permite editar las propiedades del formulario y sus componentes. Por ejemplo, añadir un componente, soltar una imagen y especificar campos obligatorios.
   * **Estilo**: Permite aplicar estilo al aspecto de los componentes del formulario. Por ejemplo, en el modo de estilo, puede seleccionar un panel y especificar su color de fondo.

   * **Desarrollador**: Permite a un desarrollador:

      * Descubra de qué formularios se componen.
      * Depurar lo que está sucediendo donde y cuando, lo que a su vez ayuda a resolver problemas.
   * **Diseño**. Permite habilitar o deshabilitar componentes personalizados o componentes integrados que no aparecen en la barra lateral.


* **Vista previa**: Permite obtener una vista previa del aspecto del formulario cuando se publica.

### Barra de herramientas de componentes {#component-toolbar}

![Barra de herramientas de componentes en la IU táctil](assets/component-toolbar.png)

Al seleccionar un componente, aparece una barra de herramientas que le permite trabajar con él. Puede obtener opciones para cortar, pegar, mover y especificar propiedades de los componentes. Las opciones son:

A.**Configurar**: Al pulsar **[!UICONTROL Configurar]**, las propiedades de los componentes se pueden ver en la barra lateral. La configuración de estas propiedades permite personalizar la experiencia de captura de datos. Puede cambiar el nombre del elemento del componente, especificar el texto de la etiqueta en el campo Título del componente. El nombre del elemento permite capturar los valores que introducen los usuarios mediante el componente. En las propiedades del componente, se especifica el comportamiento del componente y se administran los datos introducidos por el usuario. Configure las propiedades en la barra lateral para capturar los datos de usuario y utilizarlos para un procesamiento posterior. Las propiedades del contenedor de formulario adaptable permiten especificar la configuración de bibliotecas de cliente, diseños, temas, documento de registro, configuración de guardado, configuración de envío y metadatos.

B.**Copiar**: Puede utilizar la opción de copia para copiar un componente y pegarlo en otros lugares del formulario. Al pegar un componente, el componente pegado obtiene un nuevo nombre de elemento, pero conserva las propiedades del componente copiado.

C.**Cortar**: Puede utilizar la opción de corte para mover un componente de un lugar a otro en el formulario adaptable.

D. **Eliminar**: Permite eliminar el componente del formulario.

E. **Insertar**: Permite insertar un componente sobre el componente seleccionado.

F. **Pegar**: Permite pegar el componente cortado o copiado mediante las opciones descritas anteriormente.

G. **Editar reglas**: Permite abrir el editor de reglas. Para obtener más información, consulte [Editor de reglas](../../forms/using/rule-editor.md).

H. **Grupo**: Permite seleccionar varios componentes si desea cortar, copiar o pegar más de un componente juntos.

I. **Principal**: Permite seleccionar el elemento principal de un componente. Por ejemplo, un campo de texto se encuentra dentro de una subsección, que reside en una sección. La sección se encuentra en el panel raíz de la guía y el contenedor de formulario adaptable es el principal de un panel raíz de guía. Para un componente, puede ver todas las opciones con la jerarquía ordenada en la parte inferior.

Por ejemplo, si toca **[!UICONTROL Principal]** para un cuadro de texto, puede ver:

* Subsección
* Sección
* guideRootPanel
* Contenedor de formulario adaptable

J. **Otros**: Proporciona más opciones para trabajar con el componente seleccionado.

* Ver expresión SOM
* Guardar un panel como fragmento (solo para paneles)
* Agregar panel secundario (solo para paneles)
* Agregar barra de herramientas del panel (solo para paneles)
* Reemplazar (no para paneles)

### Página de formulario adaptable {#af-page}

La página de formulario adaptable es el formulario real. Es como cualquier otra página WCM modelada como el componente WCM `cq:Page`. La imagen siguiente muestra la estructura de contenido de un formulario adaptable típico.

![Estructura de contenido de una página WCM de forma adaptable](assets/afstructure.png)

La estructura de contenido suele contener los siguientes componentes principales:

* **guideContainer**: La raíz de un formulario adaptable, que se marca como  **[!UICONTROL Inicio del]** formulario adaptable en la interfaz de usuario del formulario adaptable. En este componente, puede especificar:

   * *Diseño móvil del formulario* adaptable: Define el aspecto del formulario en los dispositivos móviles.
   * *Página de agradecimiento*: Define la página a la que se redirige al usuario después de enviar el formulario.
   * *Enviar acción*: Define cómo se procesa el formulario en el servidor una vez que el usuario lo envía.
   * *Estilo*: Especifica la ruta al archivo CSS utilizado para personalizar el aspecto del formulario.

* **rootPanel:** panel raíz de un formulario adaptable. Puede contener subpaneles bajo el nodo elementos . Cada panel, incluido el panel raíz, puede tener un diseño asociado. La presentación del panel dicta cómo se coloca el formulario. Por ejemplo, en la presentación Acordeón, sus elementos se muestran como pasos de Acordeón.

* **barra de herramientas:** un contenedor de formulario adaptable tiene asociada una barra de herramientas global que es global para el formulario. Esta barra de herramientas se puede agregar mediante la acción **[!UICONTROL Agregar barra de herramientas]** de la barra de edición, que permite a los autores agregar acciones como Enviar, Guardar, Restablecer, etc.

* **recursos:** este nodo contiene información adicional que se utiliza para la creación de formularios. Por ejemplo, detalles del modelo de formulario, detalles de localización, etc.).

