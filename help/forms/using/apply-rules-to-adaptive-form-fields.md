---
title: '"NO PUBLIQUE EL Tutorial: Aplicar reglas a campos de formulario adaptables"'
seo-title: Aplicación de reglas a campos de formulario adaptables
description: Cree reglas para agregar interactividad, lógica empresarial y validaciones inteligentes a un formulario adaptable.
seo-description: Cree reglas para agregar interactividad, lógica empresarial y validaciones inteligentes a un formulario adaptable.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---


# Tutorial: Aplicación de reglas a campos de formulario adaptables {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

Este tutorial es un paso de la serie [Crear su primer formulario](/help/forms/using/create-your-first-adaptive-form.md) adaptable. Adobe recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

## Acerca del tutorial {#about-the-tutorial}

Puede utilizar reglas para agregar interactividad, lógica empresarial y validaciones inteligentes a un formulario adaptable. Los formularios adaptables tienen un editor de reglas integrado. El editor de reglas proporciona una funcionalidad de arrastrar y soltar, similar a las visitas guiadas. El método de arrastrar y soltar es el más rápido y sencillo para crear reglas. El editor de reglas también proporciona una ventana de código para los usuarios interesados en probar sus habilidades de codificación o llevar las reglas al siguiente nivel.

Puede obtener más información sobre el editor de reglas en el editor [de reglas de formularios](/help/forms/using/rule-editor.md)adaptables.

Al final del tutorial, aprenderá a crear reglas para:

* Invocar un servicio de modelo de datos de formulario para recuperar datos de la base de datos
* Invocar un servicio de modelo de datos de formulario para agregar datos a la base de datos
* Ejecutar una comprobación de validaciones y mostrar mensajes de error

Las imágenes GIF interactivas al final de cada sección del tutorial le ayudan a aprender y validar la funcionalidad del formulario que está creando sobre la marcha.

## Paso 1: Recuperar un registro de cliente de la base de datos {#retrieve-customer-record}

Ha creado un modelo de datos de formulario siguiendo el artículo [crear modelo](/help/forms/using/create-form-data-model.md) de datos de formulario. Ahora puede utilizar el editor de reglas para invocar los servicios del Modelo de datos de formularios para recuperar y agregar información a la base de datos.

A cada cliente se le asigna un número de ID de cliente único, que ayuda a identificar los datos relevantes del cliente en una base de datos. El procedimiento siguiente utiliza el ID de cliente para recuperar información de la base de datos:

1. Abra el formulario adaptable para editarlo.

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. Toque el campo ID **** del cliente y el icono **[!UICONTROL Editar reglas]** . Se abre la ventana Editor de reglas.
1. Toque el icono **[!UICONTROL + Crear]** para agregar una regla. Abre el Editor visual.

   En el Editor visual, la instrucción **[!UICONTROL WHEN]** está seleccionada de forma predeterminada. Además, el objeto de formulario (en este caso, ID **[!UICONTROL de]** cliente) desde el que se inició el editor de reglas se especifica en la instrucción **[!UICONTROL WHEN]** .

1. Toque la lista desplegable **[!UICONTROL Seleccionar estado]** y seleccione **[!UICONTROL se cambiará]**.

   ![whparticipstomeridischanged](assets/whencustomeridischanged.png)

1. En la instrucción **[!UICONTROL ENTONCES]** , seleccione **[!UICONTROL Invocar servicio]** en la lista desplegable **[!UICONTROL Seleccionar acción]** .
1. Seleccione el servicio **[!UICONTROL Recuperar dirección]** de envío en la lista desplegable **[!UICONTROL Seleccionar]** .
1. Arrastre y suelte el campo ID **[!UICONTROL del]** cliente desde la ficha Objetos de formulario al objeto **[!UICONTROL Colocar o seleccione aquí]** en el cuadro **[!UICONTROL ENTRADA]** .

   ![dropobjectstoinputfield-Retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. Arrastre y suelte los campos ID de **[!UICONTROL cliente, Nombre, Dirección de envío, Estado y Código]** postal desde la ficha Objetos de formulario al objeto **[!UICONTROL Colocar o seleccione este]** campo en el **[!UICONTROL cuadro RESULTADO]** .

   ![dropobjectstooutputfield-Retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   Toque **[!UICONTROL Hecho]** para guardar la regla. En la ventana del editor de reglas, toque **[!UICONTROL Cerrar]**.

1. Previsualización del formulario adaptable. Introduzca un ID en el campo ID **[!UICONTROL del]** cliente. El formulario ahora puede recuperar los detalles del cliente de la base de datos.

   ![recuperar-información](assets/retrieve-information.gif)

## Paso 2: Añadir la dirección de cliente actualizada a la base de datos {#updated-customer-address}

Una vez recuperados los detalles del cliente de la base de datos, puede actualizar la dirección de envío, el estado y el código postal. El procedimiento siguiente invoca un servicio del Modelo de datos de formulario para actualizar la información del cliente a la base de datos:

1. Seleccione el campo **[!UICONTROL Enviar]** y toque el icono **[!UICONTROL Editar reglas]** . Se abre la ventana Editor de reglas.
1. Seleccione **[!UICONTROL Enviar: haga clic]** en la regla y toque el icono **[!UICONTROL Editar]** . Aparecerán las opciones para editar la regla Enviar.

   ![submit-rule](assets/submit-rule.png)

   En la opción WHEN, las opciones **[!UICONTROL Enviar]** y **[!UICONTROL se hace clic]** ya están seleccionadas.

   ![submit-is-clicked](assets/submit-is-clicked.png)

1. En la opción **[!UICONTROL ENTONCES]** , toque la opción **[!UICONTROL + Añadir instrucción]** . Seleccione **[!UICONTROL Invocar servicio]** en la lista desplegable **[!UICONTROL Seleccionar acción]** .
1. Seleccione el servicio **[!UICONTROL Actualizar dirección]** de envío en la lista desplegable **[!UICONTROL Seleccionar]** .

   ![update-Shipping-address](assets/update-shipping-address.png)

1. ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

   Arrastre y suelte los campos Dirección de **[!UICONTROL envío, Estado y Código]** postal desde la ficha Objetos de formulario hasta la correspondiente propiedad .property (por ejemplo, customerdetails.ShippingAddress) del objeto **[!UICONTROL Drop o seleccione este]** campo en el cuadro **[!UICONTROL ENTRADA]** . Todos los campos con el prefijo tablename (por ejemplo, detalles del cliente en este caso de uso) sirven como datos de entrada para el servicio de actualización. Todo el contenido proporcionado en estos campos se actualiza en el origen de datos.

   >[!NOTE]
   >
   >No arrastre y suelte los campos **[!UICONTROL Nombre]** e ID **[!UICONTROL del]** cliente en la propiedad correspondiente tablename.property (por ejemplo, customerdetails.name). Ayuda a evitar actualizar el nombre y la ID del cliente por error.

1. Arrastre y suelte el campo ID **[!UICONTROL del]** cliente desde la ficha Objetos del formulario hasta el campo id del cuadro **[!UICONTROL ENTRADA]** . Los campos sin un nombre de tabla preestablecido (por ejemplo, detalles del cliente en este caso de uso) sirven como parámetro de búsqueda para el servicio de actualización. El campo **[!UICONTROL id]** en este caso de uso identifica de forma exclusiva un registro en la tabla de detalles del cliente.
1. Toque **[!UICONTROL Hecho]** para guardar la regla. En la ventana del editor de reglas, toque **[!UICONTROL Cerrar]**.
1. Previsualización del formulario adaptable. Recupere los detalles de un cliente, actualice la dirección de envío y envíe el formulario. Al recuperar los detalles del mismo cliente de nuevo, se muestra la dirección de envío actualizada.

## Paso 3: (Sección de bonificación) Utilice el editor de código para ejecutar validaciones y mostrar mensajes de error {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

Debe ejecutar la validación en el formulario para asegurarse de que los datos introducidos en el formulario son correctos y se muestra un mensaje de error en caso de datos incorrectos. Por ejemplo, si se introduce un ID de cliente no existente en el formulario, se mostrará un mensaje de error.

Los formularios adaptables proporcionan varios componentes con validaciones integradas, por ejemplo, campos numéricos y de correo electrónico que se pueden utilizar para casos de uso comunes. Utilice el editor de reglas para casos de uso avanzados, por ejemplo, para mostrar un mensaje de error cuando la base de datos devuelve cero (0) registros (sin registros).

El siguiente procedimiento muestra cómo crear una regla para mostrar un mensaje de error si el ID de cliente introducido en el formulario no existe en la base de datos. La regla también centra la atención en el campo ID de cliente y lo restablece. La regla utiliza [la API dataIntegrationUtils del servicio](/help/forms/using/invoke-form-data-model-services.md) del modelo de datos de formulario para comprobar si el ID de cliente existe en la base de datos.

1. Puntee en el campo ID **[!UICONTROL del]** cliente y toque el `Edit Rules` icono. Se abre la ventana Editor de reglas.
1. Toque el icono **[!UICONTROL + Crear]** para agregar una regla. Abre el Editor visual.

   En el Editor visual, la instrucción **[!UICONTROL WHEN]** está seleccionada de forma predeterminada. Además, el objeto de formulario (en este caso, ID **[!UICONTROL de]** cliente) desde el que se inició el editor de reglas se especifica en la instrucción **[!UICONTROL WHEN]** .

1. Toque la lista desplegable **[!UICONTROL Seleccionar estado]** y seleccione **[!UICONTROL se cambiará]**.

   ![whparticipstomeridischanged](assets/whencustomeridischanged.png)

   En la instrucción **[!UICONTROL ENTONCES]** , seleccione **[!UICONTROL Invocar servicio]** en la lista desplegable **[!UICONTROL Seleccionar acción]** .

1. Cambie del Editor **** visual al Editor **** de código. El control del interruptor se encuentra en el lado derecho de la ventana. Se abre el Editor de código, que muestra código similar al siguiente:

   ![code-editor](assets/code-editor.png)

1. Reemplace la sección de variables de entrada con el siguiente código:

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. Reemplace la sección guía lib.dataIntegrationUtils.executeOperation (operationInfo, entradas, salidas) con el siguiente código:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, function (result) {
     if (result) {
         result = JSON.parse(result);
       customer_Name.value = result.name;
       customer_Shipping_Address = result.shippingAddress;
     } else {
       if(window.confirm("Invalid Customer ID. Provide a valid customer ID")) {
             customer_Name.value = " ";
            guideBridge.setFocus(customer_ID);
       }
     }
   });
   ```

1. Previsualización del formulario adaptable. Introduzca un ID de cliente incorrecto. Aparece un mensaje de error.

   ![display-validation-error](assets/display-validation-error.gif)

