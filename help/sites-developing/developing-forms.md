---
title: Desarrollo de formularios (IU clásica)
seo-title: Desarrollo de formularios (IU clásica)
description: Aprenda a desarrollar formularios
seo-description: Aprenda a desarrollar formularios
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Desarrollo de formularios (IU clásica){#developing-forms-classic-ui}

La estructura básica de un formulario es:

* Inicio del formulario
* Elementos de formulario
* Fin del formulario

Todo esto se realiza con una serie de componentes [de](/help/sites-authoring/default-components.md#form)formulario predeterminados, disponibles en una instalación estándar de AEM.

Además de [desarrollar nuevos componentes](/help/sites-developing/developing-components-samples.md) para su uso en los formularios, también puede:

* [Carga previa del formulario con valores](#preloading-form-values)
* [Precargar (determinados) campos con varios valores
   ](#preloading-form-fields-with-multiple-values)
* [Desarrollar nuevas acciones](#developing-your-own-form-actions)
* [Desarrollar nuevas restricciones](#developing-your-own-form-constraints)
* [Mostrar u ocultar campos de formulario específicos](#showing-and-hiding-form-components)

[Uso de secuencias de comandos](#developing-scripts-for-use-with-forms) para ampliar la funcionalidad cuando sea necesario.

>[!NOTE]
>
>Este documento se centra en el desarrollo de formularios mediante los componentes [](/help/sites-authoring/default-components-foundation.md) de base en la IU clásica. Adobe recomienda aprovechar los nuevos componentes [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) principales y [ocultar condiciones](/help/sites-developing/hide-conditions.md) para el desarrollo de formularios en la IU táctil.

## Precargar valores de formulario {#preloading-form-values}

El componente de inicio de formulario proporciona un campo para la ruta de **carga**, una ruta opcional que apunta a un nodo del repositorio.

Ruta de carga es la ruta a las propiedades del nodo que se utiliza para cargar valores predefinidos en varios campos del formulario.

Se trata de un campo opcional que especifica la ruta a un nodo en el repositorio. Cuando este nodo cuenta con propiedades que coinciden con los nombres de campo, los campos apropiados del formulario se cargan previamente con el valor de estas propiedades. Si no existe coincidencia, el campo contiene el valor predeterminado.

>[!NOTE]
>
>Una acción [de](#developing-your-own-form-actions) formulario también puede establecer el recurso desde el que se cargarán los valores iniciales. Esto se hace usando `FormsHelper#setFormLoadResource` el interior `init.jsp`.
>
>Sólo si no se ha establecido, el autor rellenará el formulario desde la ruta definida en el componente de formulario de inicio.

### Preloading Form Fields with Multiple Values {#preloading-form-fields-with-multiple-values}

Varios campos de formulario también tienen la ruta **de carga de** elementos, otra vez una ruta opcional que apunta a un nodo del repositorio.

Ruta **de carga de** elementos es la ruta a las propiedades de nodo que se utiliza para cargar valores predefinidos en ese campo específico del formulario, por ejemplo, una lista [](/help/sites-authoring/default-components-foundation.md#dropdown-list)desplegable, un grupo [de](/help/sites-authoring/default-components-foundation.md#checkbox-group) casillas de verificación o un grupo [de](/help/sites-authoring/default-components-foundation.md#radio-group)radio.

#### Ejemplo: Precarga de una lista desplegable con varios valores {#example-preloading-a-dropdown-list-with-multiple-values}

Se puede configurar una lista desplegable con el rango de valores para la selección.

La ruta **de carga de** elementos se puede utilizar para acceder a una lista desde una carpeta del repositorio y precargarla en el campo:

1. Cree una nueva carpeta sling ( `sling:Folder`)por ejemplo, `/etc/designs/<myDesign>/formlistvalues`

1. Agregue una nueva propiedad (por ejemplo, `myList`) de tipo cadena de varios valores ( `String[]`) para contener la lista de elementos desplegables. El contenido también se puede importar mediante una secuencia de comandos, como con una secuencia de comandos JSP o cURL en una secuencia de comandos de shell.

1. Use the full path in the **Items Load Path** field:
for example, `/etc/designs/geometrixx/formlistvalues/myList`

Tenga en cuenta que si los valores de la `String[]` son del tipo de formato:

* `AL=Alabama`
* `AK=Alaska`
* *etc.*

AEM generará la lista como:

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

Esta función puede, por ejemplo, utilizarse bien en una configuración de varios idiomas.

### Desarrollo de sus propias acciones de formulario {#developing-your-own-form-actions}

Un formulario necesita una acción. Una acción define la operación que se ejecuta cuando el formulario se envía con los datos del usuario.

Se ofrece una serie de acciones con una instalación estándar de AEM, que se pueden ver en:

`/libs/foundation/components/form/actions`

y en la lista Tipo **de** acción del componente **Formulario** :

![chlimage_1-8](assets/chlimage_1-8.png)

Esta sección trata cómo desarrollar su propia acción de formulario para incluirla en esta lista.

Puede agregar su propia acción en `/apps` :

1. Cree un nodo de tipo `sling:Folder`. Especifique un nombre que refleje la acción que se va a implementar.

   Por ejemplo:

   `/apps/myProject/components/customFormAction`

1. En este nodo, defina las siguientes propiedades y, a continuación, haga clic en **Guardar todo** para mantener los cambios:

   * `sling:resourceType` - configurado como `foundation/components/form/action`

   * `componentGroup` - definir como `.hidden`

   * De forma opcional:

      * `jcr:title` - especifique un título de su elección; se mostrará en la lista desplegable de selección. Si no se establece, se muestra el nombre del nodo

      * `jcr:description` - escriba una descripción de su elección

1. En la carpeta, cree un nodo de cuadro de diálogo:

   1. Agregue campos para que el autor pueda editar el cuadro de diálogo de formularios una vez seleccionada la acción.

1. En la carpeta, cree una de las opciones siguientes:

   1. Un script de anuncio.
El nombre de la secuencia de comandos es `post.POST.<extension>`, por ejemplo: `post.POST.jsp`la secuencia de comandos de la publicación se invoca cuando se envía un formulario para procesarlo, contiene el código que controla los datos que llegan desde el formulario `POST`.

   1. Agregue una secuencia de comandos de reenvío que se invoque al enviar el formulario.
El nombre de la secuencia de comandos es `forward.<extension`>, por ejemplo: `forward.jsp`esta secuencia de comandos puede definir una ruta. La solicitud actual se reenvía a la ruta especificada.
   La llamada necesaria es `FormsHelper#setForwardPath` (2 variantes). Un caso típico es realizar alguna validación, o lógica, para encontrar la ruta de destino y luego reenviar a esa ruta, permitiendo que el servlet Sling POST predeterminado realice el almacenamiento real en JCR.

   También puede haber otro servlet que realice el procesamiento real, en tal caso la acción del formulario y el `forward.jsp` solo actuaría como el código &quot;pegado&quot;. Un ejemplo de esto es la acción de correo en `/libs/foundation/components/form/actions/mail`, que envía detalles `<currentpath>.mail.html`donde se encuentra un servlet de correo.

   Entonces:

   * a `post.POST.jsp` resulta útil para las operaciones pequeñas que se realizan plenamente mediante la propia acción
   * mientras que la `forward.jsp` es útil cuando sólo se requiere la delegación.
   El orden de ejecución de las secuencias de comandos es:

   * Al procesar el formulario ( `GET`):

      1. `init.jsp`
      1. para todas las restricciones de campo: `clientvalidation.jsp`
      1. validación del formularioRT: `clientvalidation.jsp`
      1. el formulario se carga mediante el recurso de carga si se configura
      1. `addfields.jsp` mientras se procesa dentro de la representación `<form></form>`
   * al administrar un formulario `POST`:

      1. `init.jsp`
      1. para todas las restricciones de campo: `servervalidation.jsp`
      1. validación del formularioRT: `servervalidation.jsp`
      1. `forward.jsp`
      1. si se ha establecido una ruta de avance ( `FormsHelper.setForwardPath`), reenvíe la solicitud y, a continuación, llame a `cleanup.jsp`

      1. si no se configuró ninguna ruta de avance, llame `post.POST.jsp` (termina aquí, sin `cleanup.jsp` llamar)




1. De nuevo en la carpeta, agregue de forma opcional:

   1. Secuencia de comandos para agregar campos.
El nombre de la secuencia de comandos es `addfields.<extension>`, por ejemplo: se invoca `addfields.jsp`una secuencia de comandos addfields inmediatamente después de escribir el código HTML para el inicio del formulario. Esto permite que la acción agregue campos de entrada personalizados u otro código HTML dentro del formulario.

   1. Una secuencia de comandos de inicialización.
El nombre de la secuencia de comandos es `init.<extension>`, por ejemplo: `init.jsp`esta secuencia de comandos se invoca cuando se procesa el formulario. Se puede utilizar para inicializar detalles específicos de acciones. &quot;

   1. Un script de limpieza.
El nombre de la secuencia de comandos es `cleanup.<extension>`, por ejemplo: `cleanup.jsp`esta secuencia de comandos se puede utilizar para realizar la limpieza.

1. Utilice el componente **Forms** en un parsys. La lista desplegable Tipo **de** acción ahora incluirá la nueva acción.

   >[!NOTE]
   >
   >Para ver las acciones predeterminadas que forman parte del producto:
   >
   >
   >`/libs/foundation/components/form/actions`

### Desarrollo de sus propias restricciones de formulario {#developing-your-own-form-constraints}

Las restricciones pueden imponerse en dos niveles:

* Para campos [individuales (consulte el procedimiento siguiente)](#constraints-for-individual-fields)
* Como validación [global de formularios](#form-global-constraints)

#### Restricciones para campos individuales {#constraints-for-individual-fields}

Puede agregar sus propias restricciones para un campo individual (debajo `/apps`) de la siguiente manera:

1. Cree un nodo de tipo `sling:Folder`. Especifique un nombre que refleje la restricción que se va a implementar.

   Por ejemplo:

   `/apps/myProject/components/customFormConstraint`

1. En este nodo, defina las siguientes propiedades y, a continuación, haga clic en **Guardar todo** para mantener los cambios:

   * `sling:resourceType` - configurado para `foundation/components/form/constraint`

   * `constraintMessage` - un mensaje personalizado que se mostrará si el campo no es válido, según la restricción, al enviar el formulario

   * De forma opcional:

      * `jcr:title` - especifique un título de su elección, se mostrará en la lista de selección. Si no se establece, se muestra el nombre del nodo
      * `hint` - información adicional, para el usuario, sobre cómo utilizar el campo

1. Dentro de esta carpeta, puede necesitar las siguientes secuencias de comandos:

   * Una secuencia de comandos de validación de cliente:
El nombre de la secuencia de comandos es `clientvalidation.<extension>`, por ejemplo: `clientvalidation.jsp`se invoca cuando se procesa el campo de formulario. Se puede utilizar para crear javascript de cliente para validar el campo en el cliente.

   * Secuencia de comandos de validación del servidor:
El nombre de la secuencia de comandos es `servervalidation.<extension>`, por ejemplo: `servervalidation.jsp`se invoca cuando se envía el formulario. Se puede utilizar para validar el campo en el servidor después de enviarlo.

>[!NOTE]
>
>En:
>
>`/libs/foundation/components/form/constraints`

#### Restricciones de formulario-globales {#form-global-constraints}

La validación global del formulario se especifica configurando un tipo de recurso en el componente de formulario de inicio ( `validationRT`). Por ejemplo:

`apps/myProject/components/form/validation`

A continuación, puede definir:

* a `clientvalidation.jsp` - insertado después de las secuencias de comandos de validación del cliente del campo
* y un `servervalidation.jsp` - también llamado después de las validaciones individuales del servidor de campo en un `POST`.

### Showing and Hiding Form Components {#showing-and-hiding-form-components}

Puede configurar el formulario para que muestre u oculte los componentes del formulario según el valor de otros campos del formulario.

Cambiar la visibilidad de un campo de formulario resulta útil cuando el campo es necesario sólo en condiciones concretas. Por ejemplo, en un formulario de recopilación de información, se pregunta al usuario si desea que la información del producto se le envíe por correo electrónico. Al seleccionar Sí, aparece el campo de texto para que el cliente pueda escribir su dirección de correo electrónico.

Use the **Edit Show/Hide Rules** dialog box to specify the conditions under which a form component is shown or hidden.

![showhideeditor](assets/showhideeditor.png)

Utilice los campos en la parte superior del cuadro de diálogo para especificar la siguiente información:

* Si va a especificar condiciones para ocultar o mostrar el componente.
* Si alguna o todas las condiciones deben ser verdaderas para mostrar u ocultar el componente.

Aparecen una o varias condiciones bajo estos campos. Una condición compara el valor de otro componente del formulario (en el mismo formulario) con un valor. Si el valor real del campo se ajusta a la condición, la condición evalúa en verdadero. Las condiciones incluyen la siguiente información:

* Título del campo de formulario que se va a probar.
* Operador.
* Valor frente al que se comprar el valor del campo.

Por ejemplo, un componente Grupo de radio con el título `Receive email notifications?`* * contiene `Yes` y `No` botones de opción. A Text Field component with the title of `Email Address` uses the following condition so that it is visible if `Yes` is selected:

![showhidecondición](assets/showhidecondition.png)

En Javascript, las condiciones utilizan el valor de la propiedad Nombre del elemento para hacer referencia a campos. In the previous example, the Element Name property of the Radio Group component is `contact`. El siguiente código es el código Javascript equivalente para ese ejemplo:

`((contact == "Yes"))`

**Para mostrar u ocultar un componente de formulario:**

1. Edite el componente de formulario específico.

1. Seleccione **Mostrar/Ocultar** para abrir el cuadro de diálogo **Editar reglas** de Mostrar/Ocultar:

   * En la primera lista desplegable, seleccione **Mostrar** u **Ocultar** para especificar si las condiciones determinan si se muestra u oculta el componente.

   * En la lista desplegable al final de la línea superior, seleccione:

      * **todo** : si todas las condiciones deben ser verdaderas para mostrar u ocultar el componente
      * **cualquiera** : si solo una o varias condiciones deben ser verdaderas para mostrar u ocultar el componente
   * En la línea de condición (una se presenta como predeterminada), seleccione un componente, operador y, a continuación, especifique un valor.
   * Agregue más condiciones si es necesario haciendo clic en **Agregar condición**.
   Por ejemplo:

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Click **OK** to save the definition.

1. After you saved your definition, an **Edit Rules** link appears next to the **Show / Hide** option in the form component properties. Click this link to open the **Edit Show / Hide Rules** dialog box to make changes.

   Click **OK** to save all changes.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >Se pueden ver y probar los efectos de las definiciones Mostrar/Ocultar:
   >
   >
   >
   >    * en el modo de **vista previa** en el entorno de creación (se necesita volver a cargar la página al cambiar por primera vez a la vista previa)
      >
      >    
   * en el entorno de publicación


#### Handling Broken Component References {#handling-broken-component-references}

Las condiciones de la función de mostrar y ocultar utilizan el valor de la propiedad Nombre de elemento para hacer referencia a otros componentes del formulario. La configuración Mostrar/Ocultar no es válida cuando cualquiera de las condiciones hace referencia a un componente que se elimina o cuya propiedad Nombre del elemento ha cambiado. Cuando se produce esta situación, se deben actualizar manualmente las condiciones o se producirá un error cuando se cargue el formulario.

Cuando la configuración Mostrar/Ocultar no es válida, la configuración se proporciona únicamente como código JavaScript. Edite el código para corregir los problemas. El código utilizará la propiedad Nombre de elemento utilizada originalmente para hacer referencia a los componentes.

### Desarrollo de secuencias de comandos para su uso con formularios {#developing-scripts-for-use-with-forms}

Para obtener más información sobre los elementos de API que se pueden utilizar al escribir secuencias de comandos, consulte los [javadocs relacionados con los formularios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

Esto se puede utilizar para acciones como llamar a un servicio antes de enviar el formulario y cancelar el servicio si se produce un error:

* Definir el tipo de recurso de validación
* Incluir una secuencia de comandos para validación:

   * En JSP, llame al servicio web y cree un objeto `com.day.cq.wcm.foundation.forms.ValidationInfo` que contenga sus mensajes de error. Si hay errores, los datos del formulario no se publicarán.
