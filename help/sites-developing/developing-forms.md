---
title: Desarrollo de Forms (IU clásica)
seo-title: Developing Forms (Classic UI)
description: Aprenda a desarrollar formularios
seo-description: Learn how to develop forms
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 18%

---

# Desarrollo de Forms (IU clásica){#developing-forms-classic-ui}

La estructura básica de un formulario es:

* Inicio del formulario
* Elementos de formulario
* Final del formulario

Todas ellas se realizan con una serie de valores predeterminados [Componentes de formulario](/help/sites-authoring/default-components.md#form), disponible en una instalación de AEM estándar.

Además de [desarrollo de nuevos componentes](/help/sites-developing/developing-components-samples.md) para su uso en los formularios también puede:

* [Precargar el formulario con valores](#preloading-form-values)
* [Precargar (ciertos) campos con varios valores](#preloading-form-fields-with-multiple-values)
* [Desarrollar nuevas acciones](#developing-your-own-form-actions)
* [Desarrollar nuevas restricciones](#developing-your-own-form-constraints)
* [Mostrar u ocultar campos de formulario específicos](#showing-and-hiding-form-components)

[Uso de secuencias de comandos](#developing-scripts-for-use-with-forms) ampliar la funcionalidad cuando sea necesario.

>[!NOTE]
>
>Este documento se centra en el desarrollo de formularios utilizando la variable [Componentes básicos](/help/sites-authoring/default-components-foundation.md) en la IU clásica. Adobe recomienda aprovechar el nuevo [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) y [Ocultar condiciones](/help/sites-developing/hide-conditions.md) para el desarrollo de formularios en la IU táctil.

## Precarga de valores de formulario {#preloading-form-values}

El componente de inicio de formulario proporciona un campo para la variable **Ruta de carga**, una ruta opcional que apunta a un nodo en el repositorio.

La Ruta de carga es la ruta a las propiedades del nodo que se utiliza para cargar valores predefinidos en varios campos del formulario.

Se trata de un campo opcional que especifica la ruta a un nodo en el repositorio. Cuando este nodo cuenta con propiedades que coinciden con los nombres de campo, los campos apropiados del formulario se cargan previamente con el valor de estas propiedades. Si no existe coincidencia, el campo contiene el valor predeterminado.

>[!NOTE]
>
>A [acción del formulario](#developing-your-own-form-actions) también puede establecer el recurso desde el que cargar los valores iniciales. Esto se realiza mediante `FormsHelper#setFormLoadResource` interior `init.jsp`.
>
>Solo si no se ha establecido, el autor rellenará el formulario desde la ruta establecida en el componente del formulario de inicio.

### Precarga de campos de formulario con varios valores {#preloading-form-fields-with-multiple-values}

Varios campos de formulario también tienen la variable **Ruta de carga de elementos**, de nuevo una ruta opcional que señala a un nodo en el repositorio.

La variable **Ruta de carga de elementos** es la ruta a las propiedades del nodo que se utiliza para cargar valores predefinidos en ese campo específico del formulario, por ejemplo, un [lista desplegable](/help/sites-authoring/default-components-foundation.md#dropdown-list), [grupo de casillas de verificación](/help/sites-authoring/default-components-foundation.md#checkbox-group) o [grupo de radio](/help/sites-authoring/default-components-foundation.md#radio-group).

#### Ejemplo: Precarga de una lista desplegable con varios valores {#example-preloading-a-dropdown-list-with-multiple-values}

Se puede configurar una lista desplegable con el rango de valores para la selección.

La variable **Ruta de carga de elementos** se puede utilizar para acceder a una lista desde una carpeta del repositorio y precargarla en el campo :

1. Crear una nueva carpeta de sling ( `sling:Folder`), por ejemplo, `/etc/designs/<myDesign>/formlistvalues`

1. Añadir una nueva propiedad (por ejemplo, `myList`) de tipo cadena de varios valores ( `String[]`) para que contenga la lista de elementos desplegables. El contenido también se puede importar mediante un script, como con un script JSP o cURL en un script shell.

1. Utilice la ruta completa en la variable **Ruta de carga de elementos** campo: por ejemplo, `/etc/designs/geometrixx/formlistvalues/myList`

Tenga en cuenta que si los valores de la variable `String[]` son del formato siguiente:

* `AL=Alabama`
* `AK=Alaska`
* etc.

a continuación, AEM generará la lista como:

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

Esta función puede, por ejemplo, utilizarse en un ajuste de varios idiomas.

### Desarrollo de sus propias acciones de formulario {#developing-your-own-form-actions}

Un formulario necesita una acción. Una acción define la operación que se ejecuta cuando el formulario se envía con los datos del usuario.

Se proporcionan una serie de acciones con una instalación AEM estándar, que se pueden ver en:

`/libs/foundation/components/form/actions`

y en el **Tipo de acción** lista de **Formulario** componente:

![Chlimage_1-8](assets/chlimage_1-8.png)

Esta sección explica cómo desarrollar su propia acción de formulario para incluirla en esta lista.

Puede añadir su propia acción en `/apps` de la siguiente manera:

1. Crear un nodo de tipo `sling:Folder`. Especifique un nombre que refleje la acción que se va a implementar.

   Por ejemplo:

   `/apps/myProject/components/customFormAction`

1. En este nodo, defina las siguientes propiedades y haga clic en **Guardar todo** para mantener los cambios:

   * `sling:resourceType` - se configura como `foundation/components/form/action`

   * `componentGroup` - definir como `.hidden`

   * De forma opcional:

      * `jcr:title` - especifique un título de su elección; esto se mostrará en la lista de selección desplegable. Si no se configura, se muestra el nombre del nodo

      * `jcr:description` - introduzca una descripción de su elección

1. En la carpeta , cree un nodo de diálogo:

   1. Agregue campos para que el autor pueda editar el cuadro de diálogo de formularios una vez seleccionada la acción.

1. En la carpeta , cree:

   1. Una secuencia de comandos posterior.
El nombre de la secuencia de comandos es `post.POST.<extension>`, p. ej. `post.POST.jsp`
La secuencia de comandos posterior se invoca cuando se envía un formulario para procesarlo y contiene el código que gestiona los datos que llegan del formulario 
`POST`.

   1. Agregue una secuencia de comandos de reenvío que se invoque cuando se envíe el formulario.
El nombre de la secuencia de comandos es `forward.<extension`>, p. ej. `forward.jsp`
Esta secuencia de comandos puede definir una ruta. A continuación, la solicitud actual se reenvía a la ruta especificada.
   La llamada necesaria es `FormsHelper#setForwardPath` (2 variantes). Un caso típico es realizar alguna validación, o lógica, para encontrar la ruta de destino y luego reenviar a esa ruta, permitiendo que el servlet predeterminado del POST de Sling haga el almacenamiento real en JCR.

   También podría haber otro servlet que haga el procesamiento real, en tal caso la acción del formulario y la `forward.jsp` solo actuaría como el código &quot;pegado&quot;. Un ejemplo de esto es la acción de correo en `/libs/foundation/components/form/actions/mail`, que reenvía detalles a `<currentpath>.mail.html`donde se encuentra un servlet de correo.

   Así que:

   * a `post.POST.jsp` es útil para operaciones pequeñas que son totalmente realizadas por la propia acción
   * mientras que la variable `forward.jsp` es útil cuando solo se requiere la delegación.

   El orden de ejecución de las secuencias de comandos es:

   * Al procesar el formulario ( `GET`):

      1. `init.jsp`
      1. para todas las restricciones de campo: `clientvalidation.jsp`
      1. validación de formularioRT: `clientvalidation.jsp`
      1. el formulario se carga mediante el recurso de carga si se configura
      1. `addfields.jsp` while dentro de la renderización `<form></form>`
   * gestión de un formulario `POST`:

      1. `init.jsp`
      1. para todas las restricciones de campo: `servervalidation.jsp`
      1. validación de formularioRT: `servervalidation.jsp`
      1. `forward.jsp`
      1. si se estableció una ruta hacia adelante ( `FormsHelper.setForwardPath`), reenviar la solicitud y, a continuación, llamar a `cleanup.jsp`

      1. si no se estableció ninguna ruta de acceso hacia adelante, llame a `post.POST.jsp` (termina aquí, no `cleanup.jsp` llamado)




1. De nuevo en la carpeta, añada opcionalmente:

   1. Secuencia de comandos para agregar campos.
El nombre de la secuencia de comandos es `addfields.<extension>`, p. ej. `addfields.jsp`
Un 
`addfields` se invoca la secuencia de comandos inmediatamente después de escribir el HTML para el inicio del formulario. Esto permite que la acción agregue campos de entrada personalizados u otro HTML de este tipo dentro del formulario.

   1. Una secuencia de comandos de inicialización.
El nombre de la secuencia de comandos es `init.<extension>`, p. ej. `init.jsp`
Esta secuencia de comandos se invoca cuando se representa el formulario. Se puede utilizar para inicializar detalles de acciones.

   1. Un script de limpieza.
El nombre de la secuencia de comandos es `cleanup.<extension>`, p. ej. `cleanup.jsp`
Esta secuencia de comandos se puede utilizar para realizar la limpieza.

1. Utilice la variable **Forms** en un parsys. La variable **Tipo de acción** ahora incluirá la nueva acción.

   >[!NOTE]
   >
   >Para ver las acciones predeterminadas que forman parte del producto:
   >
   >
   >`/libs/foundation/components/form/actions`

### Desarrollar sus propias restricciones de formulario {#developing-your-own-form-constraints}

Las restricciones pueden imponerse en dos niveles:

* Para [campos individuales (consulte el procedimiento siguiente)](#constraints-for-individual-fields)
* Como [validación global de formularios](#form-global-constraints)

#### Restricciones para campos individuales {#constraints-for-individual-fields}

Puede añadir sus propias restricciones para un campo individual (en `/apps`) como se indica a continuación:

1. Crear un nodo de tipo `sling:Folder`. Especifique un nombre que refleje la restricción que se va a implementar.

   Por ejemplo:

   `/apps/myProject/components/customFormConstraint`

1. En este nodo, defina las siguientes propiedades y haga clic en **Guardar todo** para mantener los cambios:

   * `sling:resourceType` - se configura como `foundation/components/form/constraint`

   * `constraintMessage` : un mensaje personalizado que se muestra si el campo no es válido, según la restricción, cuando se envía el formulario

   * De forma opcional:

      * `jcr:title` - especifique un título de su elección, que se mostrará en la lista de selección. Si no se configura, se muestra el nombre del nodo
      * `hint` : información adicional, para el usuario, sobre cómo utilizar el campo

1. Dentro de esta carpeta, puede necesitar las siguientes secuencias de comandos:

   * Una secuencia de comandos de validación de cliente: El nombre de la secuencia de comandos es `clientvalidation.<extension>`, p. ej. `clientvalidation.jsp`
Esto se invoca cuando se procesa el campo de formulario. Se puede utilizar para crear javascript de cliente para validar el campo en el cliente.

   * Una secuencia de comandos de validación del servidor: El nombre de la secuencia de comandos es `servervalidation.<extension>`, p. ej. `servervalidation.jsp`
Esto se invoca cuando se envía el formulario. Se puede utilizar para validar el campo en el servidor después de enviarlo.

>[!NOTE]
>
>Las restricciones de muestra se pueden ver en:
>
>`/libs/foundation/components/form/constraints`

#### Restricciones globales de formulario {#form-global-constraints}

La validación global del formulario se especifica configurando un tipo de recurso en el componente del formulario de inicio ( `validationRT`). Por ejemplo:

`apps/myProject/components/form/validation`

A continuación, puede definir:

* a `clientvalidation.jsp` - insertado después de las secuencias de comandos de validación del cliente del campo
* y `servervalidation.jsp` - también se llama después de las validaciones individuales del servidor de campos en un `POST`.

### Mostrar y ocultar componentes del formulario {#showing-and-hiding-form-components}

Puede configurar el formulario para que muestre u oculte los componentes de formulario según el valor de otros campos del formulario.

Cambiar la visibilidad de un campo de formulario resulta útil cuando el campo es necesario sólo en condiciones concretas. Por ejemplo, en un formulario de recopilación de información, se pregunta al usuario si desea que la información del producto se le envíe por correo electrónico. Al seleccionar Sí, aparece el campo de texto para que el cliente pueda escribir su dirección de correo electrónico.

Utilice la variable **Editar Mostrar/ocultar reglas** para especificar las condiciones en las que se muestra u oculta un componente de formulario.

![showhideeditor](assets/showhideeditor.png)

Utilice los campos en la parte superior del cuadro de diálogo para especificar la siguiente información:

* Si va a especificar condiciones para ocultar o mostrar el componente.
* Si alguna o todas las condiciones deben ser verdaderas para mostrar u ocultar el componente.

Aparecen una o varias condiciones bajo estos campos. Una condición compara el valor de otro componente del formulario (en el mismo formulario) con un valor. Si el valor real del campo se ajusta a la condición, la condición evalúa en verdadero. Las condiciones incluyen la siguiente información:

* Título del campo de formulario que se va a probar.
* Operador.
* Valor frente al que se comprar el valor del campo.

Por ejemplo, un componente Grupo de opciones con el título `Receive email notifications?`* * * contiene `Yes` y `No` botones de opción. Un componente Campo de texto con el título de `Email Address` utiliza la siguiente condición para que sea visible si `Yes` está seleccionada:

![showhidecondition](assets/showhidecondition.png)

En Javascript, las condiciones utilizan el valor de la propiedad Nombre del elemento para hacer referencia a campos. En el ejemplo anterior, la propiedad Nombre de elemento del componente Grupo de opciones es `contact`. El siguiente código es el código Javascript equivalente para ese ejemplo:

`((contact == "Yes"))`

**Para mostrar u ocultar un componente de formulario:**

1. Edite el componente de formulario específico.

1. Select **Mostrar / Ocultar** para abrir el **Editar Mostrar / Ocultar reglas** diálogo:

   * En la primera lista desplegable, seleccione **Show** o **Ocultar** para especificar si las condiciones determinan si se muestra u oculta el componente.

   * En la lista desplegable situada al final de la línea superior, seleccione:

      * **all** - si todas las condiciones deben ser verdaderas para mostrar u ocultar el componente
      * **any** - si solo una o más condiciones deben ser verdaderas para mostrar u ocultar el componente
   * En la línea de condición (una se presenta como predeterminada), seleccione un componente, operador y, a continuación, especifique un valor.
   * Agregue más condiciones si es necesario haciendo clic en **Agregar condición**.

   Por ejemplo:

   ![Chlimage_1-9](assets/chlimage_1-9.png)

1. Haga clic en **OK** para guardar la definición.

1. Después de guardar la definición, se muestra una **Editar reglas** el vínculo aparece junto a la variable **Mostrar / Ocultar** en las propiedades del componente del formulario. Haga clic en este vínculo para abrir el **Editar Mostrar / Ocultar reglas** para realizar cambios.

   Haga clic en **OK** para guardar todos los cambios.

   ![imagen_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >Los efectos de las definiciones Mostrar / Ocultar se pueden ver y probar:
   >
   >* en **Vista previa** en el entorno de creación (es necesario volver a cargar la página al cambiar por primera vez a la vista previa)
   >
   >* en el entorno de publicación


#### Gestión de referencias de componentes rotas {#handling-broken-component-references}

Las condiciones de la función de mostrar y ocultar utilizan el valor de la propiedad Nombre de elemento para hacer referencia a otros componentes del formulario. La configuración Mostrar/Ocultar no es válida cuando cualquiera de las condiciones hace referencia a un componente que se elimina o cuya propiedad Nombre de elemento ha cambiado. Cuando se produce esta situación, se deben actualizar manualmente las condiciones o se producirá un error cuando se cargue el formulario.

Cuando la configuración de Mostrar/Ocultar no es válida, la configuración se proporciona solamente como código JavaScript. Edite el código para corregir los problemas. El código utilizará la propiedad Nombre de elemento utilizada originalmente para hacer referencia a los componentes.

### Desarrollo de secuencias de comandos para su uso con Forms {#developing-scripts-for-use-with-forms}

Para obtener más información sobre los elementos API que se pueden utilizar al escribir secuencias de comandos, consulte la [javadocs relacionados con formularios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

Puede utilizarlo para acciones como llamar a un servicio antes de que se envíe el formulario y cancelar el servicio si falla:

* Definición del tipo de recurso de validación
* Incluya una secuencia de comandos para la validación:

   * En JSP, llame al servicio web y cree un objeto `com.day.cq.wcm.foundation.forms.ValidationInfo` que contenga sus mensajes de error. Si hay errores, los datos del formulario no se publicarán.
