---
title: Preguntas más frecuentes para formularios HTML5
seo-title: Frequently asked questions (FAQ) for HTML5 forms
description: Preguntas más frecuentes sobre la presentación, la compatibilidad con secuencias de comandos y el ámbito de los formularios HTML5.
seo-description: Frequently Asked Questions (FAQ) about layout, scripting support, and scope of HTML5 forms.
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
feature: Mobile Forms
exl-id: 85c9315e-1bc8-44a9-937e-af6fc7cf54d1
source-git-commit: 99c9eddad7a2ec7eb23b3c374a1c0e65e141da20
workflow-type: tm+mt
source-wordcount: '2005'
ht-degree: 0%

---


# Preguntas más frecuentes para formularios HTML5{#frequently-asked-questions-faq-for-html-forms}

Hay algunas preguntas más frecuentes (FAQ) sobre la presentación, la compatibilidad con secuencias de comandos y el ámbito de los formularios HTML5.

## Diseño {#layout}

1. ¿Por qué los códigos de barras y los campos de firma no aparecen en mi formulario?

   Respuesta: Los campos Códigos de barras y firmas no son relevantes en los casos de HTML o móviles. Estos campos aparecen como un área no interactiva. Sin embargo, AEM Forms Designer proporciona un nuevo campo de anotaciones de firma que se puede utilizar en lugar de un campo de firma. También se puede agregar una [utilidad personalizada](../../forms/using/custom-widgets.md) para códigos de barras e integrarlos.

1. ¿Se admite texto enriquecido para el campo de texto XFA?

   Respuesta: El campo XFA, que permite contenido enriquecido en AEM Forms Designer, no es compatible y se representa como texto normal sin que sea posible aplicar estilo al texto desde la interfaz de usuario. Además, los campos XFA con propiedad comb se muestran como un campo normal, aunque sigue habiendo restricciones en el número de caracteres permitidos en función del valor de los dígitos comb.

1. ¿Existen limitaciones en cuanto al uso de subformularios repetibles?

   Respuesta: Los subformularios repetibles deben tener un recuento inicial de 1 o más. Los subformularios repetibles con un recuento inicial de cero no son compatibles. También puede elegir utilizar un subformulario repetible y no mostrarlo cuando se carga el formulario. Para conseguir el caso de uso:

   1. Defina el recuento inicial del subformulario repetible en 1.

      ![Recuento inicial](assets/intial-count.png)

   1. Utilice el suceso initialize del formulario para ocultar la instancia principal del subformulario. Por ejemplo, el código siguiente oculta la instancia principal del subformulario al inicializarlo. También verifica el tipo de aplicación para garantizar que la secuencia de comandos se ejecute únicamente en el lado del cliente:

      ```javascript
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. Abra la secuencia de comandos para agregar una instancia del subformulario para editarlo. Agregue el código como se muestra a continuación para agregar una instancia de la secuencia de comandos del subformulario.

      El código siguiente comprueba la instancia oculta del subformulario. Si se encuentra la instancia oculta del subformulario, elimine la instancia oculta del subformulario e inserte una nueva instancia del subformulario. Si no se encuentra la instancia oculta del subformulario, simplemente inserte una nueva instancia del subformulario.

      ```javascript
      if (RepeatSubform.presence == "hidden")
      {
      RepeatSubform.instanceManager.insertInstance(0);
      RepeatSubform.instanceManager.removeInstance(1);
      }
      else
      {
      RepeatSubform.instanceManager.addInstance(1);
      }
      ```

   1. Abra la secuencia de comandos para quitar una instancia del subformulario y editarla. Agregue el código como se indica a continuación para quitar una instancia de la secuencia de comandos de subformulario.

      El código comprueba el recuento de los subformularios. Si el recuento del subformulario alcanza 1, el código oculta el subformulario en lugar de eliminarlo.

      ```javascript
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. Abra el suceso de envío previo del formulario para editarlo. Agregue la siguiente secuencia de comandos al suceso para eliminar la instancia oculta de la secuencia de comandos antes de editarla. Evita enviar datos del subformulario oculto al enviarlo.

      ```javascript
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. ¿Existen limitaciones en cuanto al uso de subformularios ocultos?

   Respuesta: Un subformulario oculto con una jerarquía compleja que se divide entre páginas causa problemas de presentación. Una solución consiste en marcar el subformulario inicialmente visible y luego ocultarlo en una secuencia de comandos initialize basada en alguna lógica o datos.

1. ¿Por qué parte del texto está truncado o se muestra incorrectamente en HTML5?

   Respuesta: Cuando no se ha dado espacio suficiente a un elemento de texto Dibujar o Rótulo para mostrar contenido, el texto aparece truncado en la representación de formularios móviles. Este truncamiento también está visible en la vista Diseño de AEM Forms Designer. Aunque este truncamiento se puede controlar en los PDF, no se puede gestionar en los formularios HTML5. Para evitar el problema, proporcione espacio suficiente para Dibujar o Texto de rótulo para que no se trunque en el modo de diseño del Diseñador de AEM Forms.

1. Estoy observando problemas de diseño relacionados con la falta de contenido o el contenido superpuesto. ¿Cuál es la razón?

   Respuesta: Si hay un elemento Dibujar texto o Dibujar imagen junto con otro elemento superpuesto en la misma posición (por ejemplo, un rectángulo), el contenido Dibujar texto no estará visible si se presenta más adelante en el orden del documento (en la vista Jerarquía de AEM Forms Designer). El PDF admite capas transparentes, pero los HTML/navegadores no admiten capas transparentes.

1. ¿Por qué algunas fuentes se muestran en el formulario del HTML de forma diferente a las utilizadas al diseñar el formulario?

   Respuesta: HTML5 Forms no permite incrustar fuentes (a diferencia de los PDF forms donde las fuentes están incrustadas dentro del formulario). Para que la versión HTML de un formulario se represente según lo esperado, asegúrese de que las fuentes estén disponibles en el repositorio CRX (repositorio de contenido AEM) de su servidor AEM Forms y en el equipo que tenga instalado AEM Designer. Cuando las fuentes no están disponibles en el repositorio CRX del servidor AEM Forms o en la ubicación donde está instalado AEM Designer, el formulario se procesa con fuentes de reserva.

1. ¿Se admiten los atributos vAlign y hAlign en los formularios HTML?

   Respuesta: Sí, se admiten los atributos vAlign y hAlign . El atributo vAlign no es compatible con Internet Explorer ni con los campos multilínea.

1. ¿Los formularios HTML5 admiten caracteres hebreos?

   Respuesta: Los formularios de HTML5 admiten caracteres hebreos en todos los navegadores excepto en Microsoft Internet Explorer.

1. ¿Los formularios HTML5 tienen limitaciones en los campos numéricos?

   Respuesta: Sí, los formularios HTML5 tienen algunas limitaciones. Si el número de dígitos es mayor que el recuento especificado en la cláusula de formato, los números no se localizan y se muestran en la configuración regional en inglés.

1. ¿Por qué los formularios HTML son más grandes que los PDF forms?

   Respuesta: Para procesar un XDP en un formulario de HTML, se requieren muchas estructuras de datos intermedias y objetos como dom de formulario, dom de datos y dom de presentación.

   Para los PDF forms, Adobe Acrobat tiene un motor XTG integrado para crear objetos y estructuras de datos intermedias. Acrobat también se encarga del diseño y las secuencias de comandos.

   Para los formularios HTML5, los navegadores no tienen un motor XTG incorporado para crear estructuras de datos intermedias y objetos a partir de bytes XDP sin procesar. Por lo tanto, para los formularios HTML5, las estructuras intermedias se generan en el servidor y se envían al cliente. En el cliente, el script basado en JavaScript y el motor de diseño utilizan estas estructuras intermedias.

   El tamaño de la estructura intermedia depende del tamaño del XDP original y de los datos combinados con el XDP.

1. ¿Hay alguna limitación con respecto al uso de tablas en mi xdp?

   Respuesta: Las tablas complejas causan problemas en la renderización.

   * No se admite la sección (SubformSet) dentro de una tabla.
   * Las filas de encabezado o pie de página de algunas tablas se marcan para repetición. Dividir estas tablas en varias páginas puede encontrar algunos problemas.

1. ¿Las tablas accesibles tienen limitaciones?

   Respuesta: Sí, las tablas accesibles tienen las siguientes limitaciones:

   * No se admiten tablas anidadas ni subformularios dentro de una tabla.
   * Los encabezados solo se admiten para las columnas superior o izquierda de la tabla. Los encabezados no son compatibles con los elementos de la tabla intermedia. Puede aplicar encabezados a varios encabezados de fila y columna siempre que se admitan todas estas filas y columnas junto con la fila superior o la columna situada más a la izquierda de la tabla.
   * `Rowspan`y `colspan`no se admite desde una ubicación aleatoria dentro de la tabla.

   * No se puede añadir ni eliminar dinámicamente la instancia de filas que contienen elementos con un valor de extensión bueno a 1.

1. ¿Cuál es el orden de lectura de la información del objeto y el rótulo para los lectores de pantalla?

   Respuesta:
   * Cuando están presentes tanto el rótulo como la información del objeto, se lee el único rótulo. Si el rótulo no está disponible, se lee la información del objeto. También puede especificar la prioridad para la lectura en un XDP mediante el diseñador de formularios
   * Cuando pasa el ratón por encima de un elemento, se muestra la información del objeto. Si la información del objeto no está disponible, se muestra texto de voz. Si el texto de voz no está disponible, se muestra el nombre del campo.

1. Cuando pasa el ratón por encima de un campo, se muestra la información del objeto. ¿Cómo desactivarlo?

   Respuesta: Para desactivar la información del objeto al pasar el cursor por encima, seleccione ninguna en el panel de accesibilidad de Designer.

1. En Designer, un usuario puede configurar las propiedades de aspecto personalizadas del botón de radio y las casillas de verificación. ¿Los formularios HTML5 tienen en cuenta estas propiedades de aspecto personalizadas al procesar los formularios?

   Respuesta: Los formularios HTML5 ignoran las propiedades de aspecto personalizadas del botón de radio y las casillas de verificación. Los botones de opción y las casillas de verificación aparecen según las especificaciones del navegador subyacente.

1. Cuando se abre un formulario de HTML5 en un explorador compatible, el borde de los campos colocados de forma adyacente no se alinea correctamente o los subformularios aparecen superpuestos. Cuando se obtiene una vista previa del mismo formulario HTML5 en Forms Designer, los campos y la presentación no aparecen mal alineados y los subformularios aparecen en la posición correcta. ¿Cómo solucionar el problema?

   Respuesta: Cuando un subformulario está configurado con una posición variable del contenido y el subformulario tiene un elemento de borde oculto, el borde de los campos colocados adyacentemente no se alinea correctamente o los subformularios parecen superpuestos. Para resolver el problema, puede quitar o comentar el objeto oculto &lt;border> elementos del XDP correspondiente. Por ejemplo: &lt;border> El elemento está marcado como comentario:

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. ¿Por qué los lectores de pantalla no funcionan correctamente con el objeto de campo de fecha y hora?

   Respuesta: Los lectores de pantalla no admiten campos de fecha y hora. Sin embargo, puede introducir manualmente la fecha y la hora en el campo para que el lector de pantalla lo lea. Utilice información del objeto o texto del lector de pantalla para indicar al usuario que seleccione manualmente la fecha y la hora del campo.

1. ¿Los formularios HTML5 admiten patrones de visualización para campos flotantes?

   Respuesta: Los formularios HTML5 no admiten patrones de visualización para campos flotantes.

1. ¿Cuál es el formato del campo Fecha en HTML5 Forms?

Respuesta: El campo Date acepta el formato ISO, AAAA-MM-DD. Si especifica una fecha en otro formato, el campo Fecha no aceptará el formato hasta que el usuario extraiga el campo del tabulador.

### Creación de secuencias de comandos {#scripting}

1. ¿Existen limitaciones en la implementación de JavaScript para HTML Forms?

   Respuesta:

   * La compatibilidad con el script xfa.connectionSet es limitada. Para connectionSet, solo se admite la invocación del servicio web en el lado del servidor. Para obtener información detallada, consulte [Compatibilidad con secuencias de comandos](/help/forms/using/scripting-support.md).
   * No se admiten $record y $data en scripts del lado del cliente. Sin embargo, si las secuencias de comandos se escriben en un bloque formReady, layoutReady , las secuencias de comandos siguen funcionando porque se ejecutan en el servidor.
   * No se admiten scripts específicos de elementos XFA Draw, como cambiar el texto de Dibujar (o el texto de Rótulo en el caso de campos).

1. ¿Hay alguna limitación en el uso de formCalc?

   Respuesta: Actualmente solo se está implementando un subconjunto de las secuencias de comandos formCalc. Para obtener información detallada, consulte [Compatibilidad con secuencias de comandos](/help/forms/using/scripting-support.md).

1. ¿Existe alguna convención de nombres recomendada y hay alguna palabra clave reservada que se pueda evitar?

   Respuesta:
   * En AEM Forms Designer, se recomienda no comenzar el nombre de un objeto (como un subformulario o un campo de texto) con un guión bajo (_). Para utilizar guiones bajos al principio del nombre, agregue un prefijo después del guión bajo._&lt;prefix>&lt;objectname>.
   * Todas las API de formularios de HTML5 son palabras clave reservadas. Para las API y funciones personalizadas, utilice un nombre que no sea idéntico al de [API de HTML5 forms](/help/forms/using/scripting-support.md).

1. ¿Los formularios HTML5 admiten campos flotantes?

   Respuesta: Sí, HTML5 Forms admite campos flotantes. Para habilitar los campos flotantes, agregue la siguiente propiedad al perfil de renderización:

   >[!NOTE]
   >
   >De forma predeterminada, los campos no están habilitados para flotar. Puede utilizar Forms Designer para establecer la propiedad flotante de los campos.

   1. Abra la lista CRXde y vaya a la `/content/xfaforms/profiles/default` nodo .
   1. Agregar una propiedad `mfDataDependentFloatingField`de tipo String y establezca el valor de la propiedad en `true`.
   1. Haga clic en **Guardar todo**. Ahora los campos flotantes están habilitados para el Forms de HTML mediante el perfil de renderización actualizado.

      >[!NOTE]
      >
      >Para habilitar campos flotantes para un formulario específico sin actualizar el perfil de renderización, pase la propiedad mfDataDependentFloatingField=true como parámetro de URL.

1. ¿Los formularios de HTML5 ejecutan la secuencia de comandos de inicialización y el suceso de formulario listo varias veces?

   Respuesta: Sí, las secuencias de comandos de inicialización y los sucesos preparados para el formulario se ejecutan varias veces, al menos una vez en el servidor y otra en el lado del cliente. Se recomienda escribir secuencias de comandos como sucesos initialize o form:ready basados en alguna lógica empresarial (datos de formulario o campo) para que la acción se realice en función del estado de los datos y del potencial idempotente (si los datos son iguales).

### Diseño de XDP {#designing-xdp}

1. ¿Hay alguna palabra clave reservada en los formularios HTML5?

   Respuesta: Todas las API de formularios de HTML5 son palabras clave reservadas. Para las API y funciones personalizadas, utilice un nombre que no sea idéntico al de [API de HTML5 forms](/help/forms/using/scripting-support.md). Aparte de las palabras clave reservadas, si utiliza nombres de objeto que comiencen con un guión bajo (_), se recomienda agregar un prefijo único después del guión bajo. Añadir un prefijo ayuda a evitar cualquier posible conflicto con las API internas de formularios de HTML5. Por ejemplo, `_fpField1`. 
