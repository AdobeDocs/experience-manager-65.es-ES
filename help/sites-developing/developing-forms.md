---
title: Desarrollo de Forms (IU clásica)
seo-title: Desarrollo de Forms (IU clásica)
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
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 18%

---


# Desarrollo de Forms (IU clásica){#developing-forms-classic-ui}

La estructura básica de un formulario es:

* Inicio de formulario
* Elementos de formulario
* Fin del formulario

Todos estos componentes se realizan con una serie de [componentes de formulario](/help/sites-authoring/default-components.md#form) predeterminados, disponibles en una instalación de AEM estándar.

Además de [desarrollar nuevos componentes](/help/sites-developing/developing-components-samples.md) para su uso en los formularios, también puede:

* [Carga previa del formulario con valores](#preloading-form-values)
* [Precargar (determinados) campos con varios valores](#preloading-form-fields-with-multiple-values)
* [Desarrollar nuevas acciones](#developing-your-own-form-actions)
* [Desarrollar nuevas restricciones](#developing-your-own-form-constraints)
* [Mostrar u ocultar campos de formulario específicos](#showing-and-hiding-form-components)

[Uso de ](#developing-scripts-for-use-with-forms) secuencias de comandos para ampliar la funcionalidad cuando sea necesario.

>[!NOTE]
>
>Este documento se centra en el desarrollo de formularios mediante [Foundation Components](/help/sites-authoring/default-components-foundation.md) en la IU clásica. Adobe recomienda aprovechar los nuevos [Componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) y [Ocultar condiciones](/help/sites-developing/hide-conditions.md) para el desarrollo de formularios en la IU táctil.

## Precarga de valores de formulario {#preloading-form-values}

El componente inicio de formulario proporciona un campo para la **Ruta de carga**, una ruta opcional que apunta a un nodo del repositorio.

Ruta de carga es la ruta a las propiedades del nodo que se utiliza para cargar valores predefinidos en varios campos del formulario.

Se trata de un campo opcional que especifica la ruta a un nodo en el repositorio. Cuando este nodo cuenta con propiedades que coinciden con los nombres de campo, los campos apropiados del formulario se cargan previamente con el valor de estas propiedades. Si no existe coincidencia, el campo contiene el valor predeterminado.

>[!NOTE]
>
>Una [acción de formulario](#developing-your-own-form-actions) también puede establecer el recurso desde el cual cargar los valores iniciales. Esto se realiza utilizando `FormsHelper#setFormLoadResource` dentro de `init.jsp`.
>
>Sólo si no se ha establecido, el autor rellenará el formulario desde la ruta definida en el componente de formulario de inicio.

### Precarga de campos de formulario con varios valores {#preloading-form-fields-with-multiple-values}

Varios campos de formulario también tienen la **Ruta de carga de elementos**, otra vez una ruta opcional que apunta a un nodo en el repositorio.

La **Ruta de carga de elementos** es la ruta a las propiedades del nodo que se utiliza para cargar valores predefinidos en ese campo específico del formulario; por ejemplo, una [lista desplegable](/help/sites-authoring/default-components-foundation.md#dropdown-list), [grupo de casillas de verificación](/help/sites-authoring/default-components-foundation.md#checkbox-group) o [grupo de radio](/help/sites-authoring/default-components-foundation.md#radio-group).

#### Ejemplo: Precarga de una Lista desplegable con varios valores {#example-preloading-a-dropdown-list-with-multiple-values}

Se puede configurar una lista desplegable con el rango de valores para la selección.

La **Ruta de carga de elementos** puede utilizarse para acceder a una lista desde una carpeta del repositorio y precargarla en el campo:

1. Crear una nueva carpeta sling ( `sling:Folder`)
por ejemplo, `/etc/designs/<myDesign>/formlistvalues`

1. Añada una nueva propiedad (por ejemplo, `myList`) de tipo cadena de varios valores ( `String[]`) para contener la lista de elementos desplegables. El contenido también se puede importar mediante una secuencia de comandos, como con una secuencia de comandos JSP o cURL en una secuencia de comandos de shell.

1. Utilice la ruta completa en el campo **Ruta de carga de elementos**:
por ejemplo, `/etc/designs/geometrixx/formlistvalues/myList`

Tenga en cuenta que si los valores de `String[]` tienen el formato siguiente:

* `AL=Alabama`
* `AK=Alaska`
* *etc.*

aem generará la lista como:

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

Esta función puede, por ejemplo, utilizarse bien en una configuración de varios idiomas.

### Desarrollar sus propias acciones de formulario {#developing-your-own-form-actions}

Un formulario necesita una acción. Una acción define la operación que se ejecuta cuando el formulario se envía con los datos del usuario.

Se proporciona una serie de acciones con una instalación AEM estándar, que se pueden ver en:

`/libs/foundation/components/form/actions`

y en la lista **Tipo de acción** del componente **Formulario**:

![chlimage_1-8](assets/chlimage_1-8.png)

Esta sección trata cómo desarrollar su propia acción de formulario para incluirla en esta lista.

Puede agregar su propia acción en `/apps` de la siguiente manera:

1. Cree un nodo de tipo `sling:Folder`. Especifique un nombre que refleje la acción que se va a implementar.

   Por ejemplo:

   `/apps/myProject/components/customFormAction`

1. En este nodo, defina las siguientes propiedades y haga clic en **Guardar todo** para mantener los cambios:

   * `sling:resourceType` - configurado como  `foundation/components/form/action`

   * `componentGroup` - definir como  `.hidden`

   * De forma opcional:

      * `jcr:title` - especifique un título de su elección, esto se mostrará en la lista de selección desplegable. Si no se establece, se muestra el nombre del nodo

      * `jcr:description` - escriba una descripción de su elección

1. En la carpeta, cree un nodo de cuadro de diálogo:

   1. Añada los campos para que el autor pueda editar el cuadro de diálogo de formularios una vez seleccionada la acción.

1. En la carpeta, cree una de las opciones siguientes:

   1. Un script de anuncio.
El nombre de la secuencia de comandos es `post.POST.<extension>`, por ejemplo: `post.POST.jsp`
La secuencia de comandos posterior se invoca cuando se envía un formulario para procesarlo, contiene el código que controla los datos que llegan desde el formulario 
`POST`.

   1. Añada una secuencia de comandos hacia delante que se invoque al enviar el formulario.
El nombre de la secuencia de comandos es `forward.<extension`, por ejemplo: `forward.jsp`
Esta secuencia de comandos puede definir una ruta. La solicitud actual se reenvía a la ruta especificada.
   La llamada necesaria es `FormsHelper#setForwardPath` (2 variantes). Un caso típico es realizar alguna validación, o lógica, para encontrar la ruta de destinatario y luego avanzar a esa ruta, permitiendo que el servlet predeterminado del POST Sling haga el almacenamiento real en JCR.

   También puede haber otro servlet que realice el procesamiento real, en tal caso la acción del formulario y `forward.jsp` sólo actuaría como el código &quot;pegado&quot;. Un ejemplo de esto es la acción de correo en `/libs/foundation/components/form/actions/mail`, que envía los detalles a `<currentpath>.mail.html`donde se encuentra un servlet de correo.

   Entonces:

   * una `post.POST.jsp` es útil para pequeñas operaciones que se realizan completamente por la propia acción
   * mientras que el `forward.jsp` es útil cuando solo se requiere la delegación.

   El orden de ejecución de las secuencias de comandos es:

   * Al procesar el formulario ( `GET`):

      1. `init.jsp`
      1. para todas las restricciones de campo: `clientvalidation.jsp`
      1. validación del formularioRT: `clientvalidation.jsp`
      1. el formulario se carga mediante el recurso de carga si se configura
      1. `addfields.jsp` mientras se procesa dentro de la representación  `<form></form>`
   * al administrar un formulario `POST`:

      1. `init.jsp`
      1. para todas las restricciones de campo: `servervalidation.jsp`
      1. validación del formularioRT: `servervalidation.jsp`
      1. `forward.jsp`
      1. si se configuró una ruta de avance ( `FormsHelper.setForwardPath`), reenvíe la solicitud y, a continuación, llame a `cleanup.jsp`

      1. si no se configuró ninguna ruta de avance, llame a `post.POST.jsp` (termina aquí, no se llama a `cleanup.jsp`)




1. De nuevo en la carpeta, agregue de forma opcional:

   1. Secuencia de comandos para agregar campos.
El nombre de la secuencia de comandos es `addfields.<extension>`, por ejemplo: `addfields.jsp`
Se invoca una secuencia de comandos addfields inmediatamente después de escribir el HTML para el inicio de formulario. Esto permite que la acción agregue campos de entrada personalizados u otro código HTML dentro del formulario.

   1. Una secuencia de comandos de inicialización.
El nombre de la secuencia de comandos es `init.<extension>`, por ejemplo: `init.jsp`
Esta secuencia de comandos se invoca cuando se procesa el formulario. Se puede utilizar para inicializar detalles específicos de acciones. &quot;

   1. Un script de limpieza.
El nombre de la secuencia de comandos es `cleanup.<extension>`, por ejemplo: `cleanup.jsp`
Esta secuencia de comandos se puede utilizar para realizar la limpieza.

1. Utilice el componente **Forms** en un parámetro. La lista desplegable **Tipo de acción** ahora incluirá la nueva acción.

   >[!NOTE]
   >
   >Para ver las acciones predeterminadas que forman parte del producto:
   >
   >
   >`/libs/foundation/components/form/actions`

### Desarrollar sus propias restricciones de formulario {#developing-your-own-form-constraints}

Las restricciones pueden imponerse en dos niveles:

* Para [campos individuales (consulte el siguiente procedimiento)](#constraints-for-individual-fields)
* Como [validación global de formulario](#form-global-constraints)

#### Restricciones para campos individuales {#constraints-for-individual-fields}

Puede agregar sus propias restricciones para un campo individual (en `/apps`) de la siguiente manera:

1. Cree un nodo de tipo `sling:Folder`. Especifique un nombre que refleje la restricción que se va a implementar.

   Por ejemplo:

   `/apps/myProject/components/customFormConstraint`

1. En este nodo, defina las siguientes propiedades y haga clic en **Guardar todo** para mantener los cambios:

   * `sling:resourceType` - configurado para  `foundation/components/form/constraint`

   * `constraintMessage` - un mensaje personalizado que se mostrará si el campo no es válido, según la restricción, al enviar el formulario

   * De forma opcional:

      * `jcr:title` - especifique un título de su elección, esto se mostrará en la lista de selección. Si no se establece, se muestra el nombre del nodo
      * `hint` - información adicional, para el usuario, sobre cómo utilizar el campo

1. Dentro de esta carpeta, puede necesitar las siguientes secuencias de comandos:

   * Una secuencia de comandos de validación de cliente:
El nombre de la secuencia de comandos es `clientvalidation.<extension>`, por ejemplo: `clientvalidation.jsp`
Esto se invoca cuando se procesa el campo de formulario. Se puede utilizar para crear javascript de cliente para validar el campo en el cliente.

   * Secuencia de comandos de validación del servidor:
El nombre de la secuencia de comandos es `servervalidation.<extension>`, por ejemplo: `servervalidation.jsp`
Esto se invoca cuando se envía el formulario. Se puede utilizar para validar el campo en el servidor después de enviarlo.

>[!NOTE]
>
>En:
>
>`/libs/foundation/components/form/constraints`

#### Restricciones de Form-Global {#form-global-constraints}

La validación global del formulario se especifica configurando un tipo de recurso en el componente de formulario de inicio ( `validationRT`). Por ejemplo:

`apps/myProject/components/form/validation`

A continuación, puede definir:

* a `clientvalidation.jsp` - insertado después de las secuencias de comandos de validación del cliente del campo
* y un `servervalidation.jsp` - también llamado después de las validaciones del servidor de campo individual en un `POST`.

### Visualización y ocultación de componentes de formulario {#showing-and-hiding-form-components}

Puede configurar el formulario para que muestre u oculte los componentes del formulario según el valor de otros campos del formulario.

Cambiar la visibilidad de un campo de formulario resulta útil cuando el campo es necesario sólo en condiciones concretas. Por ejemplo, en un formulario de recopilación de información, se pregunta al usuario si desea que la información del producto se le envíe por correo electrónico. Al seleccionar Sí, aparece el campo de texto para que el cliente pueda escribir su dirección de correo electrónico.

Utilice el cuadro de diálogo **Editar Mostrar/Ocultar reglas** para especificar las condiciones en las que se muestra u oculta un componente de formulario.

![showhideeditor](assets/showhideeditor.png)

Utilice los campos en la parte superior del cuadro de diálogo para especificar la siguiente información:

* Si va a especificar condiciones para ocultar o mostrar el componente.
* Si alguna o todas las condiciones deben ser verdaderas para mostrar u ocultar el componente.

Aparecen una o varias condiciones bajo estos campos. Una condición compara el valor de otro componente del formulario (en el mismo formulario) con un valor. Si el valor real del campo se ajusta a la condición, la condición evalúa en verdadero. Las condiciones incluyen la siguiente información:

* Título del campo de formulario que se va a probar.
* Operador.
* Valor frente al que se comprar el valor del campo.

Por ejemplo, un componente Grupo de radio con el título `Receive email notifications?`* * contiene los botones de radio `Yes` y `No`. Un componente Campo de texto con el título `Email Address` utiliza la siguiente condición para que sea visible si se selecciona `Yes`:

![showhidecondición](assets/showhidecondition.png)

En Javascript, las condiciones utilizan el valor de la propiedad Nombre del elemento para hacer referencia a campos. En el ejemplo anterior, la propiedad Nombre de elemento del componente Grupo de radio es `contact`. El siguiente código es el código Javascript equivalente para ese ejemplo:

`((contact == "Yes"))`

**Para mostrar u ocultar un componente de formulario:**

1. Edite el componente de formulario específico.

1. Seleccione **Mostrar / Ocultar** para abrir el cuadro de diálogo **Editar Mostrar / Ocultar reglas**:

   * En la primera lista desplegable, seleccione **Mostrar** o **Ocultar** para especificar si las condiciones determinan si se muestra u oculta el componente.

   * En la lista desplegable al final de la línea superior, seleccione:

      * **all** - si todas las condiciones deben ser verdaderas para mostrar u ocultar el componente
      * **cualquiera** : si solo una o varias condiciones deben ser verdaderas para mostrar u ocultar el componente
   * En la línea de condición (una se presenta como predeterminada), seleccione un componente, operador y, a continuación, especifique un valor.
   * Añada más condiciones si es necesario haciendo clic en **Añadir condición**.

   Por ejemplo:

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Haga clic en **Aceptar** para guardar la definición.

1. Después de guardar la definición, aparece un vínculo **Editar reglas** junto a la opción **Mostrar / Ocultar** en las propiedades del componente del formulario. Haga clic en este vínculo para abrir el cuadro de diálogo **Editar Mostrar / Ocultar reglas** para realizar cambios.

   Haga clic en **Aceptar** para guardar todos los cambios.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >Se pueden ver y probar los efectos de las definiciones Mostrar/Ocultar:
   >
   >
   >
   >    * en el modo **Previsualización** en el entorno de creación (necesita una recarga de página al cambiar por primera vez a previsualización)
      >
      >    
   * en el entorno de publicación


#### Gestión de referencias de componentes rotas {#handling-broken-component-references}

Las condiciones de la función de mostrar y ocultar utilizan el valor de la propiedad Nombre de elemento para hacer referencia a otros componentes del formulario. La configuración Mostrar/Ocultar no es válida cuando cualquiera de las condiciones hace referencia a un componente que se elimina o cuya propiedad Nombre del elemento ha cambiado. Cuando se produce esta situación, se deben actualizar manualmente las condiciones o se producirá un error cuando se cargue el formulario.

Cuando la configuración Mostrar/Ocultar no es válida, la configuración se proporciona únicamente como código JavaScript. Edite el código para corregir los problemas. El código utilizará la propiedad Nombre de elemento utilizada originalmente para hacer referencia a los componentes.

### Desarrollo de secuencias de comandos para su uso con Forms {#developing-scripts-for-use-with-forms}

Para obtener más información sobre los elementos de API que se pueden utilizar al escribir secuencias de comandos, consulte los [javadocs relacionados con los formularios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

Esto se puede utilizar para acciones como llamar a un servicio antes de enviar el formulario y cancelar el servicio si se produce un error:

* Definir el tipo de recurso de validación
* Incluir una secuencia de comandos para validación:

   * En JSP, llame al servicio web y cree un objeto `com.day.cq.wcm.foundation.forms.ValidationInfo` que contenga sus mensajes de error. Si hay errores, los datos del formulario no se publicarán.
