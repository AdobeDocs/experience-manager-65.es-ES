---
title: Generar documento de registro para formularios adaptables
seo-title: Generar documento de registro para formularios adaptables
description: Explica cómo se puede generar una plantilla para un documento de registro (DoR) para formularios adaptables.
seo-description: Explica cómo se puede generar una plantilla para un documento de registro (DoR) para formularios adaptables.
uuid: 2dc7e0de-fff9-43fa-9426-e9b047eb2595
content-type: reference
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ce65cb5f-94ec-4423-9fa9-d617e9703091
docset: aem65
translation-type: tm+mt
source-git-commit: 14975f409a0e17183b3da6bdc5a42c8073080108

---


# Generar documento de registro para formularios adaptables{#generate-document-of-record-for-adaptive-forms}

## Información general {#overview}

Después de enviar un formulario, los clientes generalmente desean mantener un registro, impreso o en formato de documento, de la información que han rellenado en el formulario para su futura referencia. Esto se denomina documento de registro.

En este artículo se explica cómo generar un documento de registro para formularios adaptables.

>[!NOTE]
>
>La generación automática de documentos de registro no es compatible con formularios adaptables basados en XFA. Sin embargo, puede utilizar el XDP utilizado para crear el formulario adaptable como documento de registro.

## Tipos de formularios adaptables y sus documentos de registro {#adaptive-form-types-and-their-documents-of-record}

Cuando se crea un formulario adaptable, se puede seleccionar un modelo de formulario. Sus opciones son:

* [Plantillas](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)de formularioPermite seleccionar una plantilla XFA para el formulario adaptable. Al seleccionar una plantilla XFA, puede utilizar el archivo XDP asociado para el documento de registro como se describe anteriormente.

* [Esquema](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)XML Permite seleccionar una definición de esquema XML para el formulario adaptable. Al seleccionar un esquema XML para el formulario adaptable, puede:

   * Asocie una plantilla XFA para el documento de registro. Asegúrese de que la plantilla XFA asociada utiliza el mismo esquema XML que el formulario adaptable
   * Generar automáticamente documento de registro

* NingunoPermite crear un formulario adaptable sin un modelo de formulario. El documento de registro se genera automáticamente para el formulario adaptable.

Al seleccionar un modelo de formulario, configure el documento de registro mediante las opciones disponibles en Documento de configuración de plantilla de registro. See [Document of Record Template Configuration](#document-of-record-template-configuration).

## Documento de registro generado automáticamente {#automatically-generated-document-of-record}

Un documento de registro permite a los clientes conservar una copia del formulario enviado para su impresión. Cuando se genera automáticamente un documento de registro, cada vez que se cambia el formulario, el documento de registro se actualiza inmediatamente. Por ejemplo, se quita el campo de edad para los clientes que seleccionan Estados Unidos de América como su país. Cuando estos clientes generan un documento de registro, el campo de edad no es visible para ellos en el documento de registro.

El documento de registro generado automáticamente tiene las siguientes ventajas:

* Se encarga del enlace de datos.
* Oculta automáticamente los campos marcados como excluir del documento de registro en el momento del envío. No se requiere esfuerzo adicional.
* Ahorra tiempo para diseñar el documento de la plantilla de registro.
* Le permite probar diferentes estilos y apariencia utilizando diferentes plantillas base y elegir el mejor estilo y apariencia para el documento de registro. Las apariencias de estilo son opcionales y, si no especifica estilo, los estilos del sistema se definen como predeterminados.
* Garantiza que cualquier cambio en la forma se refleje inmediatamente en el documento de registro.

## Componentes para generar automáticamente un documento de registro {#components-to-automatically-generate-a-document-of-record}

Para generar un documento de registro para formularios adaptables, necesita los siguientes componentes:

**Formulario** adaptable Formulario adaptable para el que desea generar un documento de registro.

**Plantilla base (recomendada)** Plantilla XFA (archivo XDP) creada en AEM Designer. La plantilla base se utiliza para especificar información de estilo y marca para la plantilla de documento de registro.

Consulte Plantilla [base de un documento de registro](#base-template-of-a-document-of-record)

>[!NOTE]
>
>La plantilla base de un documento de registro también se denomina metaplantilla de un documento de registro.

**Documento de plantilla** de registro XFA (archivo XDP) generada a partir de un formulario adaptable.

See [Document of Record Template Configuration](#document-of-record-template-configuration).

**Información de datos** de formulario rellenada por un usuario en el formulario adaptable. Se combina con el documento de la plantilla de registro para generar el documento del registro.

## Asignación de elementos de formulario adaptables {#mapping-of-adaptive-form-elements}

Las siguientes secciones describen cómo aparecen los elementos de formulario adaptables en el documento de registro.

### Fields {#fields}

<table>
 <tbody>
  <tr>
   <th>Componente de formulario adaptable</th>
   <th>Componente XFA correspondiente</th>
   <th>¿Se incluye de forma predeterminada en el documento de plantilla de registro?</th>
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
   <td>verdadero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Selector de fecha</td>
   <td>Campo de fecha y hora</td>
   <td>verdadero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Lista desplegable</td>
   <td>Lista desplegable</td>
   <td>verdadero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Firma a mano alzada</td>
   <td>Secuencia de comandos de firma</td>
   <td>verdadero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Cuadro numérico</td>
   <td>Campo numérico</td>
   <td>verdadero</td>
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
   <td>verdadero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Cuadro de texto</td>
   <td>Campo de texto</td>
   <td>verdadero</td>
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
   <td><p>Botón de envío por correo electrónico</p> <p>Botón Enviar HTTP</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Términos y condiciones</td>
   <td> </td>
   <td>verdadero</td>
   <td> </td>
  </tr>
  <tr>
   <td>Archivo adjunto</td>
   <td> </td>
   <td>false</td>
   <td>No disponible en el documento de la plantilla de registro. Sólo disponible en documento de registro mediante datos adjuntos.</td>
  </tr>
 </tbody>
</table>

### Containers {#containers}

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
| Imagen | Imagen | Los componentes TextDraw e Image, tanto enlazados como no enlazados, siempre aparecen en el documento de registro de un formulario adaptable basado en XSD, a menos que se excluyan con la configuración del documento de registro. |
| Texto | Texto |

>[!NOTE]
>
>En la IU clásica, se obtienen diferentes fichas para editar las propiedades de los campos.

### Tablas {#tables}

Los componentes de tabla de formularios adaptables, como encabezado, pie de página y asignación de fila, se asignan a los componentes XFA correspondientes. Puede asignar paneles repetibles a tablas en el documento de registro.

## Plantilla base de un documento de registro {#base-template-of-a-document-of-record}

La plantilla base proporciona información de estilo y apariencia al documento de registro. Permite personalizar la apariencia predeterminada del documento de registro generado automáticamente. Por ejemplo, desea agregar el logotipo de su empresa en el encabezado y la información de copyright en el pie de página del documento del registro. La página de formato de la plantilla base se utiliza como página de formato para la plantilla de documento de registro. La página de formato puede tener información como encabezado de página, pie de página y número de página que puede aplicar al documento de registro. Puede aplicar dicha información al documento de registro mediante la plantilla base para generar automáticamente el documento de registro. El uso de una plantilla base permite cambiar las propiedades predeterminadas de los campos.

Siga las convenciones [de plantilla](#base-template-conventions) base al diseñar la plantilla base.

## Convenciones de plantilla base {#base-template-conventions}

Se utiliza una plantilla base para definir el encabezado, pie de página, estilo y apariencia de un documento de registro. El encabezado y el pie de página pueden incluir información como el logotipo de la empresa y el texto de copyright. La primera página de formato de la plantilla base se copia y utiliza como página de formato para el documento del registro, que contiene el encabezado, el pie de página, el número de página o cualquier otra información que deba aparecer en todas las páginas del documento del registro. Si utiliza una plantilla base que no se ajusta a las convenciones de plantilla base, la primera página de formato de la plantilla base se seguirá utilizando en el documento de plantilla de registro. Se recomienda encarecidamente que diseñe la plantilla base según sus convenciones y la utilice para la generación automática de documentos de registro.

**Convenciones de página de formato**

* En la plantilla base, debe asignar un nombre al subformulario raíz como `AF_METATEMPLATE` y a la página de formato como `AF_MASTERPAGE`.

* Se da preferencia a la página de formato con el nombre `AF_MASTERPAGE` ubicado debajo del subformulario `AF_METATEMPLATE` raíz para extraer información de encabezado, pie de página y estilo.

* Si `AF_MASTERPAGE` está ausente, se utiliza la primera página de formato presente en la plantilla base.

**Convenciones de estilo para campos**

* Para aplicar estilo a los campos del documento de registro, la plantilla base proporciona campos ubicados en el subformulario `AF_FIELDSSUBFORM` debajo del subformulario `AF_METATEMPLATE` raíz.

* Las propiedades de estos campos se aplican a los campos del documento de registro. Estos campos deben seguir la convención de `AF_<name of field in all caps>_XFO` nomenclatura. Por ejemplo, el nombre de campo de la casilla de verificación debe ser `AF_CHECKBOX_XFO`.

Para crear una plantilla base, haga lo siguiente en AEM Designer.

1. Haga clic en **Archivo > Nuevo**.
1. Seleccione la opción **Basado en una plantilla** .

1. Seleccione la categoría **Formularios - Documento de registro** .
1. Seleccione **Plantilla** base de DoR.
1. Haga clic en **Siguiente** y proporcione la información requerida.

1. (Opcional) Modifique el estilo y el aspecto de los campos que desea aplicar a los campos del documento de registro.
1. Guarde el formulario.

Ahora puede utilizar el formulario guardado como plantilla base para el documento de registro.
No modifique ni elimine las secuencias de comandos presentes en la plantilla base.

**Modificación de la plantilla base**

* Si no aplica ningún estilo sobre los campos de la plantilla base, es aconsejable quitar esos campos de la plantilla base para que las actualizaciones de la plantilla base se recojan automáticamente.
* Al modificar la plantilla base, no elimine, agregue ni modifique las secuencias de comandos.

>[!NOTE]
>
>Diseñe una plantilla base utilizando convenciones y siguiendo estrictamente los pasos anteriores.

## Configuración del documento de plantilla de registro {#document-of-record-template-configuration}

Configure el documento de la plantilla de registro del formulario para que los clientes puedan descargar una copia del formulario enviado que sea más fácil de imprimir. Un archivo XDP sirve como documento de la plantilla de registro. El documento de la descarga del registro de clientes se formatea según la presentación especificada en el archivo XDP.

Realice los siguientes pasos para configurar un documento de registro para formularios adaptables:

1. En la instancia de autor de AEM, haga clic en **Formularios > Formularios y documentos.**
1. Seleccione un formulario y haga clic en **Ver propiedades**.
1. En la ventana Propiedades, toque Modelo **de formulario**.
También puede seleccionar un modelo de formulario al crear un formulario.

   >[!NOTE]
   >
   >En la ficha Modelo de formulario, asegúrese de seleccionar **Esquema** o **Ninguno** en la lista desplegable **Seleccionar desde** . **[!UICONTROL El documento de registro no es compatible con formularios basados en XFA o adaptables con la plantilla de formulario como modelo de formulario.]**

1. En la sección Configuración del documento de plantilla de registro de la ficha Modelo de formulario, seleccione una de las siguientes opciones.

   **Ninguno** Seleccione esta opción si no desea configurar el documento de registro para el formulario.

   **Asociar plantilla de formulario como documento de plantilla** de registro Seleccione esta opción si tiene un archivo XDP que desea utilizar como plantilla para el documento de registro. Al seleccionar esta opción, se muestran todos los archivos XDP disponibles en el repositorio de AEM Forms. Seleccione el archivo adecuado.

   El archivo XDP seleccionado se asocia al formulario adaptable.

   **Generar documento de registro** Seleccione esta opción para utilizar un archivo XDP como plantilla base para definir el estilo y la apariencia del documento de registro. Al seleccionar esta opción, se muestran todos los archivos XDP disponibles en el repositorio de AEM Forms. Seleccione el archivo adecuado.

   **[!UICONTROL Seleccione esta opción para utilizar un archivo XDP como plantilla base para definir el estilo y la apariencia del documento de registro. Al seleccionar esta opción, se muestran todos los archivos XDP disponibles en el repositorio de AEM Forms. Seleccione el archivo adecuado.]**

   **Seleccione Plantilla de formulario como plantilla base para generar el documento de registro** Seleccione esta opción para utilizar un archivo XDP como plantilla base para definir el estilo y la apariencia del documento de registro. Al seleccionar esta opción, se muestran todos los archivos XDP disponibles en el repositorio de AEM Forms. Seleccione el archivo adecuado.

   >[!NOTE]
   >
   >Asegúrese de que el esquema utilizado para crear formularios y esquemas adaptables (esquema de datos) del formulario XFA sea el mismo si:
   >
   >
   >
   >    * El formulario adaptable está basado en esquemas
   >    * Utiliza la opción **Asociar plantilla de formulario como documento de plantilla** de registro para el documento del registro


1. Haga clic en **Finalizado.**

## Personalización de la información de marca en el documento de registro {#customize-the-branding-information-in-document-of-record}

Al generar un documento de registro, puede cambiar la información de marca del documento de registro en la ficha Documento de registro. La ficha Documento de registro incluye opciones como logotipo, apariencia, diseño, encabezado y pie de página, renuncia de responsabilidad y si desea incluir o no las opciones de casilla de verificación y botón de radio sin seleccionar.

Para localizar la información de marca que especifica en la ficha Documento de registro, debe asegurarse de que la configuración regional del explorador se establece correctamente. Para personalizar la información de marca del documento de registro, complete los siguientes pasos:

1. Seleccione un panel (panel raíz) en el documento del registro y toque ![Configurar](assets/configure.png).
1. Toque ![dortab](assets/dortab.png). Aparece la ficha Documento de registro.
1. Seleccione la plantilla predeterminada o una plantilla personalizada para procesar el documento del registro. Si selecciona la plantilla predeterminada, aparece una vista previa en miniatura del documento del registro debajo de la lista desplegable Plantilla.

   ![plantilla de marca](assets/brandingtemplate.png)

   Si elige seleccionar una plantilla personalizada, busque un archivo XDP en el servidor de AEM Forms. Si desea utilizar una plantilla que aún no se encuentra en el servidor de AEM Forms, primero debe cargar el XDP en el servidor de AEM Forms.

1. En función de si selecciona una plantilla predeterminada o personalizada, algunas o todas las siguientes propiedades aparecen en la ficha Documento de registro. Especifique estos datos correctamente:

   * **Imagen** del logotipo: Puede elegir entre usar la imagen del logotipo desde el formulario adaptable, elegir uno desde DAM o cargar uno desde el equipo.
   * **Título del formulario**
   * **Texto de encabezado**
   * **Etiqueta de la exención de responsabilidad**
   * **Exención de responsabilidad**
   * **Texto de la exención de responsabilidad**
   * **Color** de énfasis: El color en el que se representan las líneas separadoras y el texto del encabezado en el documento o en el archivo PDF
   * **Familia** de fuentes: Familia de fuentes del texto del documento del archivo PDF
   * **En los componentes Casilla de verificación y Botón de radio, mostrar solo los valores seleccionados**
   * **Separador para varios valores seleccionados**
   * **Incluir objetos de formulario que no estén enlazados al modelo de datos**
   * **Excluir campos ocultos del documento del registro**
   * **Ocultar descripción de paneles**
   >[!NOTE]
   >
   >Si utiliza una plantilla de formulario adaptable creada con una versión de Designer anterior a la 6.3 para que funcionen las propiedades Color de énfasis y Familia de fuentes, asegúrese de que lo siguiente está presente en la plantilla de formulario adaptable en el subformulario raíz:

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

1. Para guardar los cambios de marca, toque Finalizado.

## Diseños de tabla y columna para paneles en Documento de registro {#table-and-column-layouts-for-panels-in-document-of-record}

El formulario adaptable puede ser largo con varios campos de formulario. Es posible que no desee guardar un documento de registro como una copia exacta del formulario adaptable. Ahora puede elegir una presentación de tabla o columna para guardar uno o varios paneles de formulario adaptables en el documento de PDF de registro.

Antes de generar un documento de registro, en la configuración de un panel, seleccione Presentación para el documento de registro de ese panel como Tabla o Columna. Los campos del panel se organizan en consecuencia en el documento de registro.

![Campos de un panel procesados en una presentación de tabla en el documento de registro](assets/dortablelayout.png)

Campos de un panel procesados en una presentación de tabla en el documento de registro

![Campos de un panel procesados en una presentación de columna en el documento del registro](assets/dorcolumnlayout.png)

Campos de un panel procesados en una presentación de columna en el documento del registro

## Configuración de documento de registro {#document-of-record-settings}

La configuración del documento de registro permite elegir las opciones que desea incluir en el documento de registro. Por ejemplo, un banco acepta el nombre, la edad, el número de la seguridad social y el número de teléfono en un formulario. El formulario genera un número de cuenta bancaria y detalles de sucursal. Puede elegir mostrar únicamente el nombre, el número de la seguridad social, la cuenta bancaria y los detalles de sucursal en el documento de registro.

El documento de la configuración de registro de un componente está disponible en sus propiedades. Para acceder a las propiedades de un componente, selecciónelo y haga clic en ![cmppr](assets/cmppr.png) en la superposición. Las propiedades se enumeran en la barra lateral y se pueden encontrar los siguientes ajustes.

**Configuración de nivel de campo**

* **Excluir del documento de registro**: Al establecer la propiedad true, se excluye el campo del documento del registro. Se trata de una propiedad con nombre `excludeFromDoR`. Su comportamiento depende de la propiedad **Excluir campos de DoR si está oculta** en el nivel de formulario.

* **** Mostrar panel como tabla: Al establecer la propiedad, se muestra el panel como tabla en el documento de registro si el panel tiene menos de 6 campos. Aplicable solo para panel.
* **** Excluir título del documento de registro: Al establecer la propiedad, se excluye el título del panel o la tabla del documento de registro. Aplicable solo para panel y tabla.
* **** Excluir descripción del documento de registro: Al establecer la propiedad, se excluye la descripción del panel o la tabla del documento de registro. Aplicable solo para panel y tabla.

**Configuración del nivel de formulario**

* **** Incluir campos no enlazados en DoR: La configuración de la propiedad incluye campos independientes de un formulario adaptable basado en esquema en el documento de registro. De forma predeterminada, es true.
* **** Excluir campos de DoR si están ocultos: Al establecer la propiedad se anula el comportamiento de la propiedad de nivel de campo &quot;Excluir del documento de registro&quot; cuando no es true. Si los campos están ocultos en el momento del envío del formulario, se excluirán del documento de registro si la propiedad se establece como true, siempre que no se establezca la propiedad &quot;Excluir del documento de registro&quot;.

## Consideraciones clave al trabajar con el documento de registro {#key-considerations-when-working-with-document-of-record}

Tenga en cuenta las siguientes consideraciones y limitaciones al trabajar en un documento de registro para formularios adaptables.

* El documento de las plantillas de registro no admite texto enriquecido. Por lo tanto, cualquier texto enriquecido del formulario adaptable estático o de la información rellenada por el usuario final aparece como texto sin formato en el documento de registro.
* Los fragmentos de documento de un formulario adaptable no aparecen en el documento de registro. Sin embargo, se admiten fragmentos de formulario adaptables.
* el documento de registro se utiliza únicamente para imprimir.
* No se admite el enlace de contenido en el documento de registro generado para el formulario adaptable basado en esquemas XML.
* No se admite el enlace de contenido en el documento de registro generado para el formulario adaptable basado en esquemas XML.
* La versión localizada del documento del registro se crea a petición de una configuración regional cuando el usuario solicita la representación del documento del registro. La localización del documento de registro se produce junto con la localización del formulario adaptable. Para obtener más información sobre la localización de documentos de registro y formularios adaptables, consulte [Uso del flujo de trabajo de traducción de AEM para localizar formularios adaptables y documentos de registro](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

