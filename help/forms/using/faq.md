---
title: Preguntas más frecuentes para formularios HTML5
seo-title: Preguntas más frecuentes para formularios HTML5
description: Preguntas más frecuentes (FAQ) sobre el diseño, la compatibilidad con secuencias de comandos y el ámbito de los formularios HTML5.
seo-description: Preguntas más frecuentes (FAQ) sobre el diseño, la compatibilidad con secuencias de comandos y el ámbito de los formularios HTML5.
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
translation-type: tm+mt
source-git-commit: 19299fb5fc764d0e71c0ea3a5ec2286183dd6861

---


# Preguntas más frecuentes para formularios HTML5{#frequently-asked-questions-faq-for-html-forms}

Hay algunas preguntas más frecuentes (FAQ) sobre el diseño, la compatibilidad con secuencias de comandos y el ámbito de los formularios HTML5.

## Diseño {#layout}

1. ¿Por qué los códigos de barras y los campos de firma no aparecen en mi formulario?

   Respuesta: Los campos de códigos de barras y firmas no son relevantes en los escenarios HTML o móviles. Estos campos aparecen como un área no interactiva. Sin embargo, AEM Forms Designer proporciona un nuevo campo de creación de secuencias de comandos de firma que se puede utilizar en lugar de un campo de firma. También se puede agregar una utilidad [](../../forms/using/custom-widgets.md) personalizada para códigos de barras e integrarla.

1. ¿Se admite texto enriquecido para el campo de texto XFA?

   Respuesta: El campo XFA, que permite contenido enriquecido en AEM Forms Designer, no se admite y se procesa como texto normal sin que sea posible aplicar estilo al texto desde la interfaz de usuario. Además, los campos XFA con propiedad comb se muestran como un campo normal, aunque todavía hay restricciones en el número de caracteres permitidos según el valor de los dígitos comb.

1. ¿Existen limitaciones en cuanto al uso de subformularios repetibles?

   Respuesta: Los subformularios repetibles deben tener un recuento inicial de 1 o más. No se admiten los subformularios repetibles con un recuento inicial de cero. También puede elegir utilizar un subformulario repetible y no mostrarlo cuando se cargue el formulario. Para lograr el caso de uso:

   1. Establezca el recuento inicial del subformulario repetible en 1.

      ![recuento inicial](assets/intial-count.png)

   1. Utilice el suceso initialize del formulario para ocultar la instancia principal del subformulario. Por ejemplo, el código siguiente oculta la instancia principal del subformulario al inicializarlo. También verifica el tipo de aplicación para asegurarse de que la secuencia de comandos se ejecuta únicamente en el lado del cliente:

      ```
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. Abra la secuencia de comandos para agregar una instancia del subformulario para editarlo. Agregue el código siguiente para agregar una instancia de la secuencia de comandos de Subformulario.

      El código siguiente comprueba la instancia oculta del subformulario. Si se encuentra la instancia oculta del subformulario, elimine la instancia oculta del subformulario e inserte una nueva instancia del subformulario. Si no se encuentra la instancia oculta del subformulario, simplemente inserte una nueva instancia del subformulario.

      ```
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

   1. Abra la secuencia de comandos para quitar una instancia del subformulario para editarlo. Agregue el código siguiente para quitar una instancia de la secuencia de comandos de Subformulario.

      Recuento de comprobaciones de código de los subformularios. Si el recuento del subformulario alcanza 1, el código oculta el subformulario en lugar de eliminarlo.

      ```
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. Abra el suceso de envío previo del formulario para editarlo. Agregue la siguiente secuencia de comandos al suceso para eliminar la instancia oculta de la secuencia de comandos antes de editarla. Evita el envío de datos del subformulario oculto al enviarlo.

      ```
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. ¿Hay alguna limitación con respecto al uso de subformularios ocultos?

   Respuesta: Un subformulario oculto con una jerarquía compleja que se divide entre páginas causa problemas de presentación. Una solución consiste en marcar el subformulario inicialmente visible y, a continuación, ocultarlo en una secuencia de comandos de inicialización basada en alguna lógica o datos.

1. ¿Por qué parte del texto se trunca o se muestra incorrectamente en HTML5?

   Respuesta: Cuando no se ha dado espacio suficiente a un elemento de texto Dibujar o Rótulo para mostrar contenido, el texto aparece truncado en la representación de formularios móviles. Este truncamiento también está visible en la vista Diseño de AEM Forms Designer. Aunque este truncamiento se puede gestionar en los archivos PDF, no se puede gestionar en los formularios HTML5. Para evitar el problema, proporcione espacio suficiente para Dibujar o Texto de rótulo para que no se trunque en el modo de diseño de AEM Forms Designer.

1. Estoy observando problemas de diseño relacionados con la falta de contenido o la superposición de contenido. ¿Cuál es la razón?

   Respuesta: Si hay un elemento Dibujar texto o Dibujar imagen junto con otro elemento superpuesto en la misma posición (por ejemplo, un rectángulo), el contenido Dibujar texto no estará visible si se produce más adelante en el orden del documento (en la vista Jerarquía de AEM Forms Designer). PDF admite capas transparentes, pero los navegadores/HTML no admiten capas transparentes.

1. ¿Por qué se muestran algunas fuentes en el formulario HTML diferentes de las utilizadas al diseñar el formulario?

   Respuesta: Los formularios HTML5 no incrustan fuentes (a diferencia de los formularios PDF en los que las fuentes se incrustan dentro del formulario). Para que la versión HTML del formulario se represente según lo esperado, asegúrese de que las fuentes especificadas en XDP están disponibles en el servidor y en el ordenador cliente. Si las fuentes requeridas no están disponibles en el servidor, se utilizan fuentes de otoño. Además, si utiliza fuentes en la plantilla de formulario que no están disponibles en el dispositivo cliente, se utilizarán las fuentes predeterminadas del explorador para procesar el texto.

1. ¿Se admiten los atributos vAlign y hAlign en los formularios HTML?

   Sí, se admiten los atributos vAlign y hAlign. El atributo vAlign no se admite en Internet Explorer ni en los campos multilínea.

1. ¿Los formularios HTML5 admiten caracteres hebreos?

   Los formularios HTML5 admiten caracteres hebreos en todos los exploradores excepto en Microsoft Internet Explorer.

1. ¿Los formularios HTML5 tienen alguna limitación en los campos numéricos?

   Respuesta: Sí, los formularios HTML5 tienen algunas limitaciones. Si el número de dígitos es mayor que el recuento especificado en la cláusula de imagen, los números no se localizan y se muestran en la configuración regional de inglés.

1. ¿Por qué los formularios HTML tienen un tamaño mayor que los formularios PDF?

   Se requieren muchas estructuras de datos intermedias y objetos como el uso de formularios, el uso de datos y el uso de diseños para procesar un XDP en un formulario HTML.

   Para los formularios PDF, Adobe Acrobat tiene un motor XTG integrado para crear estructuras de datos y objetos intermedios. Acrobat también se ocupa del diseño y las secuencias de comandos.

   En el caso de los formularios HTML5, los exploradores no tienen un motor XTG integrado para crear estructuras de datos intermedias ni objetos a partir de bytes XDP sin procesar. Por lo tanto, para los formularios HTML5, las estructuras intermedias se generan en el servidor y se envían al cliente. En el cliente, la secuencia de comandos y el motor de diseño basados en javascript utilizan estas estructuras intermedias.

   El tamaño de la estructura intermedia depende del tamaño del XDP original y de los datos combinados con el XDP.

1. ¿Hay alguna limitación con respecto al uso de tablas en mi xdp?

   Respuesta: Las tablas complejas causan problemas en el procesamiento.

   * No se admite la sección (SubformSet) dentro de una tabla.
   * Las filas de encabezado o pie de página de algunas tablas se marcan para la repetición. La división de estas tablas en varias páginas puede causar algunos problemas.

1. ¿Existen limitaciones en las tablas accesibles?

   Respuesta: Sí, las tablas accesibles tienen las siguientes limitaciones:

   * No se admiten las tablas anidadas ni los subformularios dentro de una tabla.
   * Los encabezados solo se admiten para las columnas superior o izquierda de la tabla. Los encabezados no son compatibles con los elementos de la tabla intermedia. Puede aplicar encabezados a varios encabezados de columna y fila siempre que todas estas filas y columnas estén junto con la fila superior o la columna situada más a la izquierda de la tabla.
   * `Rowspan`y `colspan`desde una ubicación aleatoria dentro de la tabla no se admite.

   * No se puede agregar o quitar dinámicamente una instancia de filas que contenga elementos con un valor de envergadura mayor que 1.

1. ¿Cuál es el orden de lectura de la información del objeto y del rótulo para los lectores de pantalla?

   * Cuando están presentes tanto el rótulo como la información del objeto, se lee el único rótulo. Si el rótulo no está disponible, se lee la información del objeto. También puede especificar la prioridad de lectura en un XDP mediante el diseñador de formularios
   * Al pasar el ratón sobre un elemento, se muestra información del objeto. Si la información sobre herramientas no está disponible, se muestra texto de voz. Si el texto de voz no está disponible, se muestra el nombre del campo.

1. Al pasar el ratón sobre un campo, se muestra una información del objeto. ¿Cómo deshabilitarlo?

   Para desactivar la información del objeto al pasar el ratón por encima, seleccione ninguna en el panel de accesibilidad de Designer.

1. En Designer, un usuario puede configurar las propiedades de apariencia personalizadas del botón de radio y las casillas de verificación. ¿Los formularios HTML5 tienen en cuenta estas propiedades de aspecto personalizadas al procesar los formularios?

   Respuesta: Los formularios HTML5 omiten las propiedades de apariencia personalizadas del botón de radio y las casillas de verificación. Los botones de radio y las casillas de verificación aparecen según las especificaciones del navegador subyacente.

1. Cuando se abre un formulario HTML5 en un navegador compatible, el borde de los campos colocados adyacentemente no se alinea correctamente o los subformularios aparecen superpuestos. Cuando se obtiene una vista previa del mismo formulario HTML5 en Forms Designer, los campos y la presentación no aparecen desalineados y los subformularios aparecen en la posición correcta. ¿Cómo solucionar el problema?

   Cuando un subformulario se define en posición variable y el subformulario tiene un elemento de borde oculto, el borde de los campos colocados adyacentemente no se alinea correctamente o los subformularios aparecen superpuestos. Para resolver el problema, puede eliminar o comentar los elementos ocultos &lt;border> del XDP correspondiente. Por ejemplo, el siguiente elemento &lt;border> está marcado como comentario:

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. ¿Por qué los lectores de pantalla no funcionan correctamente con el objeto de campo Fecha y hora?

   Los lectores de pantalla no admiten campos de fecha y hora. Sin embargo, puede introducir manualmente la fecha y hora en el campo para que el lector de pantalla lo lea. Utilice la información del objeto o el texto del lector de pantalla para indicar al usuario que seleccione manualmente la fecha y hora del campo.

### Creación de secuencias de comandos {#scripting}

1. ¿Hay alguna limitación en la implementación de JavaScript para formularios HTML?

   Respuesta:

   * La compatibilidad con la secuencia de comandos xfa.connectionSet es limitada. Para connectionSet, solo se admite la invocación del servicio Web por parte del servidor. Para obtener información detallada, consulte Compatibilidad con [secuencias de comandos](/help/forms/using/scripting-support.md).
   * No se admite $record y $data en scripts del lado del cliente. Sin embargo, si las secuencias de comandos se escriben en un bloque formReady, layoutReady, las secuencias de comandos seguirán funcionando porque estos sucesos se ejecutan en el servidor.
   * No se admiten secuencias de comandos específicas de elementos XFA Draw, como cambiar el texto Dibujar (o el texto Rótulo en caso de campos).

1. ¿Hay alguna limitación en el uso de formCalc?

   Respuesta: Actualmente solo se implementa un subconjunto de las secuencias de comandos formCalc. Para obtener información detallada, consulte Compatibilidad con [secuencias de comandos](/help/forms/using/scripting-support.md).

1. ¿Existe alguna convención de nombres recomendada y hay palabras clave reservadas que evitar?

   * En AEM Forms Designer, se recomienda no empezar el nombre de un objeto (como un subformulario o un campo de texto) con un subrayado (_). Para utilizar subrayado al principio del nombre, agregue un prefijo después del subrayado, _&lt;prefix>&lt;objectname>.
   *  Todas las API de formularios HTML5 son palabras clave reservadas. Para las funciones o API personalizadas, utilice un nombre que no sea idéntico a las API de formularios [HTML5](/help/forms/using/scripting-support.md).

1. ¿Los formularios HTML5 admiten campos flotantes?

   Sí, los formularios HTML5 admiten campos flotantes. Para habilitar los campos flotantes, agregue la siguiente propiedad al perfil de procesamiento:

   >[!NOTE]
   >
   >De forma predeterminada, los campos no están habilitados para flotar. Puede utilizar Forms Designer para establecer la propiedad flotante de los campos.

   1. Abra la lista CRXde y navegue hasta el `/content/xfaforms/profiles/default` nodo.
   1. Agregue una propiedad `mfDataDependentFloatingField`de tipo String y defina el valor de la propiedad en `true`.
   1. Haga clic en **Guardar todo**. Ahora los campos flotantes están activados para los formularios HTML mediante el perfil de procesamiento actualizado.

      >[!NOTE]
      >
      >Para habilitar campos flotantes para un formulario específico sin actualizar el perfil de procesamiento, pase la propiedad mfDataDependentFloatingField=true como parámetro de URL.

1. ¿Ejecutan los formularios HTML5 la secuencia de comandos de inicialización y el suceso de formulario listo varias veces?

   Sí, las secuencias de comandos de inicialización y los sucesos preparados para el formulario se ejecutan varias veces, al menos una vez en el servidor y otra en el cliente. Se recomienda escribir secuencias de comandos como sucesos initialize o form:ready basados en alguna lógica empresarial (datos de campo o formulario) para que la acción se realice en función del estado de los datos y del potencial (si los datos son los mismos).

### Diseño de XDP {#designing-xdp}

1. ¿Hay palabras clave reservadas en los formularios HTML5?

   Respuesta: Todas las API de formularios HTML5 son palabras clave reservadas. Para las funciones o API personalizadas, utilice un nombre que no sea idéntico a las API de formularios [HTML5](/help/forms/using/scripting-support.md). Aparte de las palabras clave reservadas, si utiliza nombres de objeto que comienzan con un guion bajo (_), se recomienda agregar un prefijo único después del guion bajo. La adición de un prefijo ayuda a evitar cualquier posible conflicto con las API internas de formularios HTML5. Por ejemplo, `_fpField1`

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
