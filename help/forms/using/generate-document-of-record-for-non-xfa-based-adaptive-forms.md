---
title: Generar documento de registro para formularios adaptables
description: Explica cómo puede generar una plantilla para el documento de registro (DoR) de los formularios adaptables.
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms
exl-id: 7240897f-6b3a-427a-abc6-66310c2998f3
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '3544'
ht-degree: 96%

---

# Generar documento de registro para formularios adaptables{#generate-document-of-record-for-adaptive-forms}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo Forms adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [adición de Forms adaptable a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de Forms adaptable, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Forms adaptable mediante componentes de base. </span>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=es) |
| AEM 6.5 | Este artículo |


## Información general {#overview}

Después de enviar un formulario, normalmente los clientes desean guardar un registro —impreso o en formato de documento— de la información que han rellenado en el formulario para utilizarlo como referencia en el futuro. Este registro se denomina documento de registro.

Este artículo explica cómo generar un documento de registro para formularios adaptables.

>[!NOTE]
>
>La generación automática de documentos de registro no es compatible con los formularios adaptables basados en XFA. Sin embargo, puede utilizar el XDP utilizado para crear el formulario adaptable como documento de registro.

## Tipos de formularios adaptables y sus documentos de registro {#adaptive-form-types-and-their-documents-of-record}

Al crear un formulario adaptable, puede seleccionar un modelo de formulario. Las opciones son las siguientes:

* [Plantillas de formulario](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
Permite seleccionar una plantilla XFA para el formulario adaptable. Al seleccionar una plantilla XFA, puede utilizar el archivo XDP asociado para el documento de registro como se ha descrito anteriormente.

* [Esquema XML](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
Permite seleccionar una definición de esquema XML para el formulario adaptable. Al seleccionar un esquema XML para el formulario adaptable, puede:

   * Asociar una plantilla XFA al documento de registro. Asegúrese de que la plantilla XFA asociada utiliza el mismo esquema XML que el formulario adaptable
   * Generar automáticamente un documento de registro

* Ninguno
Permite crear un formulario adaptable sin un modelo de formulario. El documento de registro se genera automáticamente para el formulario adaptable.

Cuando seleccione un modelo de formulario, configure el documento de registro mediante las opciones disponibles en Configuración de la plantilla de un documento de registro. [Configuración de la plantilla de un documento de registro.](#document-of-record-template-configuration)

## Documento de registro generado automáticamente {#automatically-generated-document-of-record}

Un documento de registro permite a los clientes conservar una copia del formulario enviado para su impresión. Cuando se genera automáticamente un documento de registro, este se actualiza inmediatamente cada vez que se modifica el formulario. Por ejemplo, se elimina el campo de edad de los clientes que seleccionan Estados Unidos de América como país. Cuando estos clientes generan un documento de registro, el campo de edad no es visible para ellos en el documento.

Un documento de registro generado automáticamente tiene las siguientes ventajas:

* Se encarga del enlace de datos.
* Oculta automáticamente los campos marcados que se excluirán del documento de registro en el momento del envío. No se requiere ningún esfuerzo adicional.
* Permite ahorrar tiempo a la hora de diseñar la plantilla del documento de registro.
* Permite probar diferentes estilos y apariencias utilizando diferentes plantillas base y elegir el mejor estilo y la mejor apariencia para el documento de registro. La apariencia de cada estilo es opcional y, si no se especifica el estilo, el sistema de estilos se establece de forma predeterminada.
* Permite garantizar que cualquier cambio realizado en el formulario se verá reflejado inmediatamente en el documento de registro.

## Componentes para generar automáticamente un documento de registro {#components-to-automatically-generate-a-document-of-record}

Para generar el documento de registro de un formularios adaptable, son necesarios los siguientes componentes:

**Formulario adaptable**: el formulario adaptable para el que se desea generar un documento de registro.

**Plantilla base (recomendada)**: la plantilla XFA (archivo XDP) creada en AEM Designer. La plantilla base se utiliza para especificar la información de estilo y de personalización de marca de la plantilla del documento de registro.

Consulte [Plantilla base de un documento de registro](#base-template-of-a-document-of-record)

>[!NOTE]
>
>La plantilla base de un documento de registro también se denomina metaplantilla del documento de registro.

**Documento de plantilla de registro**: la plantilla XFA (archivo XDP) generada a partir de un formulario adaptable.

[Configuración de la plantilla de un documento de registro.](#document-of-record-template-configuration)

**Datos de formulario**: la información que rellena un usuario en el formulario adaptable. Se combina con la plantilla del documento de registro para generar el documento de registro.

## Asignación de elementos de formulario adaptable {#mapping-of-adaptive-form-elements}

Las siguientes secciones describen cómo se muestran los elementos de formulario adaptable en el documento de registro.

### Campos {#fields}

<table>
 <tbody>
  <tr>
   <th>Componente de formulario adaptable</th>
   <th>Componente XFA correspondiente</th>
   <th>¿Se incluye de forma predeterminada en la plantilla del documento de registro?</th>
   <th>Notas</th>
  </tr>
  <tr>
   <td>Botón</td>
   <td>Botón</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Casilla de verificación</td>
   <td>Casilla de verificación</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Selector de fecha</td>
   <td>Campo de fecha y hora</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Lista desplegable</td>
   <td>Lista desplegable</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Firma manuscrita</td>
   <td>Firma manuscrita</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Cuadro numérico</td>
   <td>Campo numérico</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Cuadro de contraseña</td>
   <td>Campo de contraseña</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Botón de opción</td>
   <td>Botón de opción</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Cuadro de texto</td>
   <td>Campo de texto</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Botón Restablecer</td>
   <td>Botón Restablecer</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Botón Enviar</td>
   <td><p>Botón Enviar correo electrónico</p> <p>Botón Enviar HTTP</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Términos y condiciones</td>
   <td> </td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Archivo adjunto</td>
   <td> </td>
   <td>false</td>
   <td>No disponible en la plantilla del documento de registro. Solo disponible en el documento de registro mediante archivos adjuntos.</td>
  </tr>
 </tbody>
</table>

### Contenedores {#containers}

<table>
 <tbody>
  <tr>
   <th>Componente de formulario adaptable</th>
   <th>Componente XFA correspondiente</th>
   <th>Notas</th>
  </tr>
  <tr>
   <td>Panel<br /> </td>
   <td>Subformulario<br /> </td>
   <td>El panel repetible se asigna a un subformulario repetible.</td>
  </tr>
 </tbody>
</table>

### Componentes estáticos {#static-components}

| Componente de formulario adaptable | Componente XFA correspondiente | Notas |
|---|---|---|
| Imagen | Imagen | Los componentes TextDraw e Image, estén enlazados o no, siempre aparecen en el documento de registro de un formulario adaptable basado en XSD, a menos que se excluyan en la configuración del documento de registro. |
| Texto | Texto  |

>[!NOTE]
>
>En la IU clásica, se muestran diferentes pestañas para editar las propiedades de los campos.

### Tablas {#tables}

Los componentes de las tablas de formularios adaptables, como el encabezado, el pie de página y la fila, se asignan a los componentes XFA correspondientes. Puede asignar paneles repetibles a tablas en el documento de registro.

## Plantilla base de un documento de registro {#base-template-of-a-document-of-record}

La plantilla base proporciona al documento de registro información relativa al estilo y la apariencia. Permite personalizar el aspecto predeterminado del documento de registro generado automáticamente. Por ejemplo, puede utilizar la plantilla base para agregar el logotipo de su compañía en el encabezado y la información de copyright en el pie de página del documento de registro. La página maestra de la plantilla base se utiliza como página maestra de la plantilla del documento de registro. La página maestra puede incluir información como el encabezado de página, el pie de página y el número de página que puede aplicar al documento de registro. Puede aplicar dicha información al documento de registro mediante la plantilla base para generar automáticamente el documento de registro. El uso de una plantilla base permite cambiar las propiedades predeterminadas de los campos.

Asegúrese de seguir [Convenciones de plantilla base](#base-template-conventions) al diseñar una plantilla base.

## Convenciones de plantilla base {#base-template-conventions}

Se utiliza una plantilla base para definir el encabezado, el pie de página, el estilo y la apariencia de un documento de registro. El encabezado y pie de página pueden incluir información como el logotipo de la compañía y la información de copyright. La primera página maestra de la plantilla base se copia y se utiliza como página maestra del documento de registro, la cual contiene el encabezado, el pie de página, el número de página o cualquier otro tipo de información que deba aparecer en todas las páginas del documento. Si utiliza una plantilla base que no se ajusta a las convenciones de plantilla base, la primera página maestra de la plantilla se seguirá utilizando en la plantilla del documento de registro. Se recomienda encarecidamente que diseñe la plantilla base según sus convenciones y que la utilice para generar automáticamente el documento de registro.

**Convenciones de la página maestra**

* En la plantilla base, asigne el nombre `AF_METATEMPLATE` al subformulario raíz y el nombre `AF_MASTERPAGE` a la página maestra.

* La página maestra con el nombre `AF_MASTERPAGE` que se encuentra en el subformulario raíz `AF_METATEMPLATE` tiene preferencia a la hora de extraer la información de encabezado, pie de página y estilo.

* Si `AF_MASTERPAGE` no existe, se utiliza la primera página maestra presente en la plantilla base.

**Convenciones de estilo para campos**

* Para aplicar un estilo a los campos del documento de registro, la plantilla base proporciona campos en la variable `AF_FIELDSSUBFORM` subformulario en `AF_METATEMPLATE` subformulario raíz.

* Las propiedades de estos campos se aplican a los campos del documento de registro. Estos campos deben seguir la convención de nomenclatura de `AF_<name of field in all caps>_XFO`. Por ejemplo, el nombre de campo de la casilla de verificación debe ser `AF_CHECKBOX_XFO`.

Para crear una plantilla base, siga los siguientes pasos en AEM Designer.

1. Haga clic en **Archivo > Nuevo**.
1. Seleccione la opción **Basado en una plantilla**.

1. Seleccione la categoría **Formulario - Documento de registro**.
1. Seleccione **Plantilla base de documento de registro**.
1. Haga clic en **Siguiente** y proporcione la información requerida.

1. (Opcional) Modifique el estilo y el aspecto de los campos que desea aplicar en los campos del documento de registro.
1. Guarde el formulario.

Ahora puede utilizar el formulario guardado como plantilla base para el documento de registro.
No modifique ni elimine ningún script presente en la plantilla base.

**Modificación de la plantilla base**

* Si no se aplica ningún estilo a los campos de la plantilla base, es aconsejable quitar esos campos de la plantilla para que todas las actualizaciones en esta se reflejen automáticamente.
* Al modificar la plantilla base, no elimine, agregue ni modifique scripts.

>[!NOTE]
>
>Diseñe una plantilla base utilizando las convenciones y siguiendo estrictamente los pasos anteriores.

## Configuración de la plantilla de un documento de registro {#document-of-record-template-configuration}

Configure la plantilla del documento de registro del formulario para que sus clientes puedan descargar una copia del formulario enviado fácil de imprimir. Un archivo XDP sirve como plantilla del documento de registro. El documento de registro que descargan los clientes de tiene un formato coherente el diseño especificado en el archivo XDP.

Siga los siguientes pasos para configurar un documento de registro para formularios adaptables:

1. En la instancia de autor de AEM, haga clic en **Forms > Formularios y documentos.**
1. Seleccione un formulario y haga clic en **Ver propiedades**.
1. En la ventana Propiedades, pulse **Modelo de formulario**.
También puede seleccionar un modelo de formulario al crear un formulario.

   >[!NOTE]
   >
   >En la pestaña Modelo de formulario, asegúrese de seleccionar **Esquema** o **Ninguno** en la lista desplegable **Seleccionar de**. **[!UICONTROL El documento de registro no es compatible con los formularios adaptables o basados en XFA con una plantilla de formulario como modelo de formulario.]**

1. En la sección Configuración de la plantilla de un documento de registro de la pestaña Modelo de formulario, seleccione una de las siguientes opciones.

   **Ninguno**: seleccione esta opción si no desea configurar el documento de registro del formulario.

   **Asociar plantilla de formulario como plantilla de documento de registro**: seleccione esta opción si tiene un archivo XDP que desea utilizar como plantilla para el documento de registro. Al seleccionar esta opción, se muestran todos los archivos XDP disponibles en el repositorio de AEM Forms. Seleccione el archivo apropiado.

   El archivo XDP seleccionado se asocia con el formulario adaptable.

   **Generar documento de registro**: seleccione esta opción para utilizar un archivo XDP como plantilla base para definir el estilo y la apariencia del documento de registro. Al seleccionar esta opción, se muestran todos los archivos XDP disponibles en el repositorio de AEM Forms. Seleccione el archivo apropiado.

   >[!NOTE]
   >
   >Asegúrese de que el esquema utilizado para crear un formulario adaptable y el esquema (esquema de datos) del formulario XFA sea el mismo en los siguientes casos:
   >
   >
   >
   >    * El formulario adaptable se basa en esquemas.
   >    * Utiliza la opción **Asociar plantilla de formulario como plantilla de documento de registro** para el documento de registro.
   >
   >

1. Haga clic en **Listo.**

## Personalizar la información de marca en el documento de registro {#customize-the-branding-information-in-document-of-record}

Al generar un documento de registro, puede cambiar la información de marca del documento de registro en la pestaña Documento de registro. La pestaña Documento de registro incluye opciones como logotipo, apariencia, diseño, encabezado y pie de página, exención de responsabilidad legal, y si desea incluir o no opciones de casillas de verificación y botones de opción no seleccionados.

Para localizar la información de marca indicada en la pestaña Documento de registro, asegúrese de que ha establecido correctamente la configuración regional del explorador. Para personalizar la información de marca del documento de registro, siga estos pasos:

1. Seleccione un panel (panel raíz) en el documento de registro y, a continuación, pulse ![configurar](assets/configure.png).
1. Pulse ![dortab](/help/forms/using/assets/dortab.png). Aparecerá la pestaña Documento de registro.
1. Seleccione la plantilla predeterminada o una plantilla personalizada para procesar el documento de registro. Si selecciona la plantilla predeterminada, aparece una vista previa en miniatura del documento de registro debajo de la lista desplegable Plantilla.

   ![plantilla_personalización_de_marca](/help/forms/using/assets/brandingtemplate.png)

   Si elige una plantilla personalizada, busque y seleccione un XDP en el servidor de AEM Forms. Si desea utilizar una plantilla que no esté ya en el servidor de AEM Forms, primero debe cargar el XDP en el servidor.

1. En función de si selecciona una plantilla predeterminada o personalizada, la pestaña Documento de registro muestra algunas o todas las propiedades que aparecen a continuación. Especifíquelas correctamente:

   * **Imagen del logotipo**: puede elegir usar la imagen del logotipo en el formulario adaptable, elegir una de DAM o cargar una desde el equipo.
   * **Título del formulario**
   * **Texto de encabezado**
   * **Etiqueta de la exención de responsabilidad**
   * **Exención de responsabilidad**
   * **Texto de la exención de responsabilidad**
   * **Color de énfasis**: el color en el que se representa el texto del encabezado y las líneas de separación en el documento o registro PDF.
   * **Familia de fuentes**: la familia de fuentes del texto del documento de registro PDF.
   * **Para componentes de casilla de verificación y botones de radio, mostrar solo los valores seleccionados**
   * **Separador para varios valores seleccionados**
   * **Incluir objetos de formulario que no están enlazados al modelo de datos**
   * **Excluir los campos ocultos del documento de registro**
   * **Ocultar descripción de paneles**

   Si la plantilla XDP personalizada que selecciona incluye varias páginas maestras, las propiedades de esas páginas aparecerán en la sección **[!UICONTROL Contenido]** de la pestaña **[!UICONTROL Documento de registro]**.

   ![Propiedades de página maestra](assets/master-page-properties.png)

   Las propiedades de la página maestra incluyen Imagen de logotipo, Texto de encabezado, Título del formulario, Etiqueta de exención de responsabilidad legal y Texto de exención de responsabilidad legal. Puede aplicar propiedades de formulario adaptable o de plantilla XDP al documento de registro. AEM Forms aplica las propiedades de la plantilla al documento de registro de forma predeterminada. También puede definir valores personalizados para las propiedades de la página maestra. Para obtener información sobre cómo aplicar varias páginas maestras en un documento de registro, consulte [Aplicar varias páginas maestras a un documento de registro](#apply-multiple-master-pages-dor).

   >[!NOTE]
   >
   >Si está utilizando una plantilla de formulario adaptable creada con una versión de Designer anterior a la 6.3, para que las propiedades Color de énfasis y Familia de fuentes funcionen, asegúrese de que los siguientes elementos están presentes en el subformulario raíz de la plantilla de formulario adaptable:

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```

1. Para guardar los cambios de personalización de marca, pulse Listo.

## Diseños de tablas y columnas para paneles del documento de registro {#table-and-column-layouts-for-panels-in-document-of-record}

El formulario adaptable puede ser largo y tener varios campos de formulario. Es posible que no desee guardar un documento de registro como una copia exacta del formulario adaptable. Ahora puede elegir un diseño de tabla o columna para guardar uno o más paneles de formulario adaptable en el documento de registro PDF.

Antes de generar un documento de registro, establezca el Diseño del documento de registro de cada panel como Tabla o Columna en la configuración de ese panel. Los campos del panel se organizan en consecuencia en el documento de registro.

![Los campos de un panel se representan en forma de tabla en el documento de registro](assets/dortablelayout.png)

Los campos de un panel se representan en forma de tabla en el documento de registro

![Los campos de un panel se representan en forma de columna en el documento de registro](assets/dorcolumnlayout.png)

Los campos de un panel se representan en forma de columna en el documento de registro

## Configuración del documento de registro {#document-of-record-settings}

La configuración del documento de registro le permite elegir las opciones que desea incluir en dicho documento. Por ejemplo, un banco acepta el nombre, la edad, el número de la seguridad social y el número de teléfono en un formulario. El formulario genera un número de cuenta bancaria y detalles de sucursal. Puede elegir mostrar únicamente el nombre, el número de la seguridad social, la cuenta bancaria y los detalles de la sucursal en el documento de registro.

La configuración de del documento de registro de cada componente está disponible en sus propiedades. Para acceder a las propiedades de un componente, seleccione el componente y haga clic en ![cmppr](assets/cmppr.png) en la superposición. Las propiedades se enumeran en la barra lateral y puede encontrar la siguiente configuración en ella.

**Configuración del nivel de campo**

* **Excluir del documento de registro**: al establecer la propiedad en True, se excluye el campo del documento de registro. Se trata de una propiedad que puede ser script y que se llama `excludeFromDoR`. Su comportamiento depende de la propiedad de nivel de formulario **Excluir campos del documento de registro si están ocultos**.

* **Mostrar panel como tabla:** al establecer la propiedad, se muestra el panel como tabla en el documento de registro si el panel contiene menos de 6 campos. Solo aplicable para paneles.
* **Excluir título del documento de registro:** al establecer la propiedad, se excluye el título del panel o la tabla del documento de registro. Aplicable solo para paneles y tablas.
* **Excluir descripción del documento de registro:** al establecer la propiedad, se excluye la descripción del panel o la tabla del documento de registro. Aplicable solo para paneles y tablas.
* **[!UICONTROL Paginación]** > **[!UICONTROL Posición]**: determina la posición seleccionada para el panel.
   * **[!UICONTROL Posición]** > **[!UICONTROL Después del anterior]**: coloca el panel después del objeto anterior en el panel principal.
   * **[!UICONTROL Posición]** > **[!UICONTROL En el área de contenido]** > Nombre del área de contenido: coloca el panel en el área de contenido especificada.
   * **[!UICONTROL Posición]** > **[!UICONTROL Parte superior de la siguiente área de contenido]**: coloca el panel en la parte superior de la siguiente área de contenido.
   * **[!UICONTROL Posición]** > **[!UICONTROL Parte superior del área de contenido]** > Nombre del área de contenido: coloca el panel en la parte superior del área de contenido especificada.
   * **[!UICONTROL Posición]** > **[!UICONTROL En la página]** > Nombre de la página maestra: coloca el panel en la página especificada. Si no se inserta automáticamente un salto de página, [!DNL AEM Forms] añade uno.
   * **[!UICONTROL Posición]** > **[!UICONTROL Parte superior de la siguiente página]**: coloca el panel en la parte superior de la siguiente página. Si no se inserta automáticamente un salto de página, [!DNL AEM Forms] añade uno.
   * **[!UICONTROL Posición]** > **[!UICONTROL Parte superior de la página]** > Nombre de la página maestra: coloca el panel en la parte superior de la página cuando se representa la página especificada. Si no se inserta automáticamente un salto de página, [!DNL AEM Forms] añade uno.
* **[!UICONTROL Paginación]** > **[!UICONTROL Después]**: determina qué área se rellenará después de colocar un panel. Los campos siguientes están disponibles en la sección **[!UICONTROL Después]**:
   * **[!UICONTROL Después]** > **[!UICONTROL Continuar relleno principal]**: continúa combinando los datos de todos los objetos que quedan por rellenar en el panel principal.
   * **[!UICONTROL Después]** > **[!UICONTROL Ir a la siguiente área de contenido]**: comienza a rellenar la siguiente área de contenido después de colocar el panel.
   * **[!UICONTROL Después]** > **[!UICONTROL Ir al área de contenido]** > Nombre del área de contenido: comienza a rellenar el área de contenido especificada después de colocar el panel.
   * **[!UICONTROL Después]** > **[!UICONTROL Ir a la página siguiente]**: comienza a rellenar la página siguiente después de colocar el panel.
   * **[!UICONTROL Después]** > **[!UICONTROL Ir a la página]** > Nombre de la página: comienza a rellenar la página especificada después de colocar el panel.
* **[!UICONTROL Paginación]** > **[!UICONTROL Desbordamiento]**: define el desbordamiento de un panel o una tabla que ocupa varias páginas. Los campos siguientes están disponibles en la sección **[!UICONTROL Desbordamiento]**:
   * **[!UICONTROL Desbordamiento]** > **[!UICONTROL Ninguno]**: comienza a rellenar la página siguiente. Si no se inserta automáticamente un salto de página, [!DNL AEM Forms] añade uno.
   * **[!UICONTROL Desbordamiento]** > **[!UICONTROL Ir al área de contenido]** > Nombre del área de contenido: comienza a rellenar el área de contenido especificada.
   * **[!UICONTROL Desbordamiento]** > **[!UICONTROL Ir a la página]** > Nombre de la página: comienza a rellenar la página especificada.

Para obtener información sobre cómo aplicar saltos de página y aplicar varias páginas maestras en un documento de registro, consulte [Aplicar un salto de página en un documento de registro](#apply-page-breaks-in-dor) y [Aplicar varias páginas maestras a un documento de registro](#apply-multiple-master-pages-dor).

**Configuración del nivel de formulario**

* **Incluir campos no enlazados en el documento de registro:** al establecer la propiedad, se incluyen los campos no enlazados del formulario adaptable basado en esquema en el documento de registro. De forma predeterminada, es True.
* **Excluir campos de DoR si están ocultos:**[!UICONTROL  establezca la propiedad para excluir los campos ocultos del documento de registro al enviar el formulario. ] Al activar [Revalidar en el servidor](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form)[!UICONTROL , el servidor vuelve a calcular los campos ocultos antes de excluir dichos campos del documento de registro].

## Aplicar un salto de página en un documento de registro {#apply-page-breaks-in-dor}

Puede aplicar saltos de página en un documento de registro utilizando varios métodos.

Para aplicar un salto de página a un documento de registro:

1. Pulse el panel y seleccione ![Configurar](/help/forms/using/assets/configure.png)
1. Expanda **[!UICONTROL Documento de registro]** para ver las propiedades.

1. En la sección **[!UICONTROL Paginación]**, pulse ![Carpeta](/help/forms/using/assets/folder-icon.png) en el campo **[!UICONTROL Posición]**.
1. Pulse **[!UICONTROL Parte superior de la siguiente página]** y luego pulse **[!UICONTROL Seleccionar]**. También puede pulsar **[!UICONTROL Parte superior de la página]**, seleccionar la página maestra y pulsar **[!UICONTROL Seleccionar]** para aplicar el salto de página.
1. Pulse ![Guardar](/help/forms/using/assets/save_icon.png) para guardar las propiedades.

El panel seleccionado se traslada a la página siguiente.

## Aplicar varias páginas maestras a un documento de registro {#apply-multiple-master-pages-dor}

Si la plantilla XDP personalizada que selecciona incluye varias páginas maestras, las propiedades de esas páginas aparecerán en la sección [!UICONTROL Contenido] de la pestaña [!UICONTROL Documento de registro]. Para obtener más información, consulte [Personalizar la información de marca en el documento de registro](#customize-the-branding-information-in-document-of-record).

Puede aplicar varias páginas maestras a un documento de registro aplicando diferentes páginas maestras a los componentes de un formulario adaptable. Utilice la sección [Paginación](#document-of-record-settings) de las propiedades del documento de registro para aplicar varias páginas maestras.

A continuación, se muestra un ejemplo de cómo aplicar varias páginas maestras a un documento de registro:
Carga una plantilla XDP que incluye cuatro páginas maestras en el servidor de [!DNL AEM Forms]. [!DNL AEM Forms] aplica las propiedades de la plantilla al documento de registro de forma predeterminada. [!DNL AEM Forms] también aplica las primeras propiedades de la página maestra de la plantilla al documento de registro.

Para aplicar las propiedades de la segunda página maestra a un panel y las propiedades de la tercera página maestra a los paneles siguientes, ejecute los pasos que aparecen a continuación:

1. Pulse el panel para aplicar la segunda página maestra y seleccione ![Configurar](assets/cmppr.png).
1. En la sección **[!UICONTROL Paginación]**, pulse ![Carpeta](/help/forms/using/assets/folder-icon.png) en el campo **[!UICONTROL Posición]**.
1. Pulse **[!UICONTROL En la página]**, seleccione la segunda página maestra y pulse **[!UICONTROL Seleccionar]**.
AEM Forms aplica la segunda página maestra al panel y a todos los paneles posteriores del formulario adaptable.
1. En la sección **[!UICONTROL Paginación]**, pulse ![Carpeta](/help/forms/using/assets/folder-icon.png) en el campo **[!UICONTROL Después]**.
1. Pulse **[!UICONTROL Ir a la página]**, seleccione la tercera página maestra y luego pulse **[!UICONTROL Seleccionar]**.
1. Pulse ![Guardar](/help/forms/using/assets/save_icon.png) para guardar las propiedades.
AEM Forms aplica la tercera página maestra al panel y a todos los paneles posteriores del formulario adaptable.


## Consideraciones clave al trabajar con el documento de registro {#key-considerations-when-working-with-document-of-record}

Tenga en cuenta las siguientes consideraciones y limitaciones al trabajar en el documento de registro de los formularios adaptables.

* Las plantillas de documento de registro no admiten texto enriquecido. Por lo tanto, todo el texto enriquecido del formulario adaptable estático o de la información rellenada por el usuario final aparece como texto sin formato en el documento de registro.
* Los fragmentos de documento de un formulario adaptable no aparecen en el documento de registro. Sin embargo, sí se admiten fragmentos de formularios adaptables.
* No se admiten enlaces de contenido en los documentos de registro generados para formularios adaptables basados en el esquema XML.
* La versión localizada del documento de registro se crea bajo demanda para una configuración regional cuando el usuario solicita la representación del documento de registro. La localización del documento de registro se realiza de forma paralela a la localización del formulario adaptable. Para obtener más información sobre la localización de documentos de registro y formularios adaptables, consulte [Usar el flujo de trabajo de traducción de AEM para localizar formularios adaptables y documentos de registro](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).
