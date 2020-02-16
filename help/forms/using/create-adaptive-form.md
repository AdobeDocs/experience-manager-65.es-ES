---
title: '"Tutorial: Crear un formulario adaptable"'
seo-title: '"Crear un formulario adaptable"'
description: Aprenda a crear, diseñar y previsualizar un formulario adaptable. Además, aprenda a configurar acciones de envío.
seo-description: Aprenda a crear, diseñar y previsualizar un formulario adaptable. Además, aprenda a configurar acciones de envío.
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# Tutorial: Creación de un formulario adaptable {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Este tutorial es un paso de la serie [Crear su primer formulario](/help/forms/using/create-your-first-adaptive-form.md) adaptable. Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

## Acerca del tutorial {#about-the-tutorial}

Los formularios adaptables son formularios de nueva generación dinámicos y adaptables. Puede utilizar formularios adaptables para ofrecer experiencias personalizadas. También puede integrar formularios adaptables con Adobe Analytics para estadísticas de uso y Adobe Campaign para administración de campañas. Para obtener más información sobre las capacidades de los formularios adaptables, consulte [Introducción a la creación de formularios](/help/forms/using/introduction-forms-authoring.md)adaptables.

Es más fácil crear y administrar formularios cuando se sigue un proceso adecuado. En este artículo, aprenderá a:

* [Crear un formulario adaptable que permita al cliente agregar una dirección de envío](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [Campos de diseño de un formulario adaptable para mostrar y aceptar información de un cliente](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [Crear una acción de envío para enviar un correo electrónico con contenido de formulario](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [Vista previa y envío de un formulario adaptable](/help/forms/using/create-adaptive-form.md)

Al final del artículo tendrá un formulario similar al siguiente:\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## Paso 1: Creación del formulario adaptable {#step-create-the-adaptive-form}

1. Inicie sesión en la instancia de creación de AEM y vaya a **Adobe Experience Manager** > **Formularios** > **Formularios y documentos**. La dirección URL predeterminada es [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. Toque **Crear** y seleccione Formulario **** adaptable. Aparece una opción para seleccionar una plantilla. Toque la plantilla **en blanco** para seleccionarla y toque **Siguiente**.

1. Aparece una opción para **Agregar propiedades** . Los campos **Título** y **Nombre** son obligatorios:

   * **** Título: Especifique `Add new or update shipping address` en el campo Título. El campo de título especifica el nombre para mostrar del formulario. El título le ayuda a identificar el formulario en la interfaz de usuario de AEM Forms.
   * **** Nombre: Especifique `shipping-address-add-update-form` en el campo Nombre. El campo Nombre especifica el nombre del formulario. En el repositorio se crea un nodo con el nombre especificado. A medida que comienza a escribir un título, se genera automáticamente el valor del campo de nombre. Puede cambiar el valor sugerido. El campo de nombre solo puede incluir caracteres alfanuméricos, guiones y guiones bajos. Todas las entradas no válidas se reemplazan con un guión.

1. Toque **Crear**. Se crea un formulario adaptable y aparece un cuadro de diálogo para abrir el formulario y editarlo. Toque **Abrir** para abrir el formulario recién creado en una nueva ficha. El formulario se abre para su edición. También muestra la barra lateral para personalizar el formulario recién creado según las necesidades.

   Para obtener información sobre la interfaz de creación de formularios adaptables y los componentes disponibles, consulte [Introducción a la creación de formularios](/help/forms/using/creating-adaptive-form.md)adaptables.

   ![nuevo-formulario adaptable-creado](assets/newly-created-adaptive-form.png)

## Paso 2: Agregar encabezado y pie de página {#step-add-header-and-footer}

AEM Forms proporciona varios componentes para mostrar información en un formulario adaptable. Los componentes Encabezado y Pie de página ayudan a proporcionar un aspecto coherente a un formulario. Un encabezado suele incluir el logotipo de una empresa, el título del formulario y el resumen. Un pie de página suele incluir información de copyright y vínculos a otras páginas.

1. Toque ![toggle-side-panel](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png). Se abre el navegador de componentes. Arrastre el componente **Encabezado** desde el navegador de componentes al formulario adaptable.
1. Toque **Logotipo**. Aparece la barra de herramientas. Toque ![aem_6_3_edit](assets/aem_6_3_edit.png) en la barra de herramientas, escriba **We.Retail** y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. Toque Imagen. Aparece la barra de herramientas. Toque ![cmppr](assets/cmppr.png). El navegador de propiedades se abre a la izquierda de la pantalla. **Explore** y cargue la imagen del logotipo. Toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). La imagen aparece en el encabezado.

   Puede tocar Obtener archivo para descargar el logotipo utilizado en este artículo si no tiene uno.

   [Obtener archivo](assets/logo.png)

1. Arrastre el componente **Pie** de página de ![treeexpandall](assets/treeexpandall.png) al formulario adaptable. En este momento, el formulario tiene el siguiente aspecto:

   ![adaptable-form-with-headers-and-ada-ada](assets/adaptive-form-with-headers-and-footers.png)

## Paso 3: Agregar componentes para capturar y mostrar información {#step-add-components-to-capture-and-display-information}

Los componentes son componentes básicos de un formulario adaptable. AEM Forms proporciona varios componentes para capturar y mostrar información en un formulario adaptable. Puede arrastrar los componentes de ![treeexpandall](assets/treeexpandall.png) a un formulario. Para obtener más información sobre los componentes disponibles y la funcionalidad correspondiente, consulte [Introducción a la creación de formularios](/help/forms/using/introduction-forms-authoring.md)adaptables.

1. Arrastre el componente Cuadro numérico al formulario adaptable. Colóquelo antes del componente de pie de página. Abra las propiedades del componente, cambie el **Título** del componente a **`Customer ID`**, cambie el Nombre **del** elemento a **`customer_ID`**, habilite la opción Campo **** requerido, active la opción **Usar tipo** ![](assets/aem_6_3_forms_save.png)de entrada de número HTML5 y toque aem_6_3_forms_save.
1. Arrastre tres componentes de Cuadro de texto al formulario adaptable. Colóquelas antes del componente de pie de página. Defina las siguientes propiedades para estos cuadros de texto.:

<table> 
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Text Box 1<br /> </td> 
   <td>Text Box 2<br /> </td> 
   <td>Cuadro de texto 3</td> 
  </tr> 
  <tr> 
   <td>Título</td> 
   <td>Nombre<br /> </td> 
   <td>Dirección de envío</td> 
   <td>Estado</td> 
  </tr> 
  <tr> 
   <td>Nombre de elemento</td> 
   <td>customer_Name<br /> </td> 
   <td>customer_Shipping_Address</td> 
   <td>customer_State</td> 
  </tr> 
  <tr> 
   <td>Campo requerido</td> 
   <td>Activado</td> 
   <td>Activado</td> 
   <td>Activado</td> 
  </tr> 
  <tr> 
   <td>Allow multiple lines<br /> </td> 
   <td>Deshabilitado</td> 
   <td>Activado</td> 
   <td>Deshabilitado</td> 
  </tr> 
 </tbody> 
</table>

1. Arrastre un componente Cuadro **** numérico antes del componente de pie de página. Abra las propiedades del componente, defina los valores enumerados en la tabla siguiente, Toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propiedad | Value |
   |---|---|
   | Título | Código postal |
   | Nombre de elemento | customer_ZIPCode |
   | Número máximo de dígitos | 6 |
   | Campo requerido | Activado |
   | Tipo de patrón de visualización | Sin patrón |

1. Arrastre un componente **Correo electrónico** antes del componente de pie de página. Abra las propiedades del componente, defina los valores enumerados en la tabla siguiente y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propiedad | Value |
   |---|---|
   | Título | Correo electrónico |
   | Nombre de elemento | customer_Email |
   | Campo requerido | Activado |

1. Arrastre un componente **Archivo adjunto** antes del componente de pie de página. Abra las propiedades del componente, defina los valores enumerados en la tabla siguiente y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

<table> 
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Value</td> 
  </tr> 
  <tr> 
   <td>Título</td> 
   <td>Prueba de dirección aprobada por el gobierno<br /> </td> 
  </tr> 
  <tr> 
   <td>Nombre de elemento</td> 
   <td>customer_Address_Proof</td> 
  </tr> 
  <tr> 
   <td>Campo requerido</td> 
   <td>Activado</td> 
  </tr> 
 </tbody> 
</table>

1. Arrastre un componente Botón **de** envío al formulario adaptable. Colóquelo antes del componente de pie de página. Abra las propiedades del componente, cambie Nombre del elemento a **address_addin_submit**, toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). La presentación del formulario es completa y el formulario tiene el siguiente aspecto:

   ![adaptable-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## Paso 4: Configurar la acción de envío para el formulario adaptable {#step-configure-submit-action-for-the-adaptive-form}

Una acción de envío se activa cuando un usuario toca el botón Enviar en un formulario adaptable. Puede utilizar una acción de envío para guardar datos de formulario en el repositorio local, enviar datos de formulario a un extremo REST, enviar datos de formulario como correo electrónico, etc. Los formularios adaptables proporcionan algunas acciones de envío integradas más. Para obtener información detallada, consulte [Configuración de la acción](/help/forms/using/configuring-submit-actions.md)Enviar.

Mediante los siguientes pasos, puede configurar la acción de envío por correo electrónico y la acción de envío de demostración del formulario:

1. Configure el servidor de correo electrónico. Para obtener más información, consulte [Configuración de notificaciones](/help/sites-administering/notification.md)por correo electrónico.


1. Toque Contenedor **de** formulario en el navegador de contenido y toque ![cmppr](assets/cmppr.png). El navegador de propiedades se abre a la izquierda.
1. Vaya a **Envío** > **Enviar acción**. Seleccione **Enviar correo electrónico**. Especifique los siguientes valores y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Propiedad | Value |
   |--- |--- |
   | De | `donotreply@weretail.com` |
   | A | `${customer_Email}` |
   | Asunto | Reconocimiento: Ha agregado la dirección de envío en el sitio web de We.Retail. |
   | Plantilla de correo electrónico | Hola `${customer_Name}`, se agrega la siguiente dirección como dirección de envío de su cuenta: <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> Regalos, We.Retail |
   | Incluir datos adjuntos | Activado |

   El formulario está listo. Ahora puede obtener una vista previa del formulario y probar la funcionalidad. Si ha utilizado el nombre mencionado en el tutorial y ha accedido al formulario en el equipo que ejecuta el servidor de AEM Forms, el formulario estará disponible en [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## Paso 5: Vista previa y envío del formulario adaptable {#step-preview-and-submit-the-adaptive-form}

Puede utilizar la opción **** Vista previa para evaluar el aspecto y el comportamiento de un formulario. Puede enviar un formulario en modo de vista previa y también comprobar las validaciones aplicadas a un formulario. Por ejemplo, si se muestra un error cuando un campo obligatorio se deja vacío.

Los formularios adaptables también proporcionan una opción para emular la experiencia de un formulario para varios dispositivos. Por ejemplo, iPhone, iPad y Escritorio. Puede utilizar las opciones **Vista previa** y **Regla de** emulador ![en conjunto](assets/ruler.png) para obtener una vista previa de un formulario para dispositivos de diferentes tamaños de pantalla.

1. Puntee en la opción **Vista previa** en la parte derecha del editor de formularios. El formulario se abre en el modo de vista previa. Si ha utilizado el nombre mencionado en el tutorial, la dirección URL de vista previa del formulario es [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. Utilice la ![regla](assets/ruler.png) para ver el aspecto del formulario en varios dispositivos.
1. Rellene los campos del formulario y toque **Enviar**. El formulario se envía y se le redirige a la página de **agradecimiento** predeterminada. También puede especificar una página de agradecimiento personalizada. Para obtener más información, consulte [Configuración de la página](/help/forms/using/configuring-redirect-page.md)de redireccionamiento.

El formulario adaptable para agregar una dirección está listo. Si ha utilizado el nombre mencionado en el tutorial y ha accedido al formulario en el equipo que ejecuta el servidor de AEM Forms, el formulario estará disponible en [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
