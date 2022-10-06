---
title: Aplicación de reglas a campos de formulario adaptables
seo-title: Apply rules to adaptive form fields
description: Cree reglas para agregar interactividad, lógica empresarial y validaciones inteligentes a un formulario adaptable.
seo-description: Create rules to add interactivity, business logic, and smart validations to an adaptive form.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
source-git-commit: 63bc43bba88a42d62fb574bc8ce42470ac61d693
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 1%

---

# Tutorial: Aplicación de reglas a campos de formulario adaptables {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

Este tutorial es un paso en la [Crear el primer formulario adaptable](/help/forms/using/create-your-first-adaptive-form.md) serie. Adobe recomienda seguir la serie en secuencia cronológica para comprender, realizar y mostrar el caso de uso completo del tutorial.

## Acerca del tutorial {#about-the-tutorial}

Puede utilizar reglas para agregar interactividad, lógica empresarial y validaciones inteligentes a un formulario adaptable. Los formularios adaptables tienen un editor de reglas integrado. El editor de reglas proporciona una funcionalidad de arrastrar y soltar, similar a las visitas guiadas. El método de arrastrar y soltar es el más rápido y sencillo para crear reglas. El editor de reglas también proporciona una ventana de código para los usuarios interesados en probar sus habilidades de codificación o llevar las reglas al siguiente nivel.

Puede obtener más información sobre el editor de reglas en [Editor de reglas de Forms adaptable](/help/forms/using/rule-editor.md).

Al final del tutorial, aprenderá a crear reglas para:

* Invocar un servicio del Modelo de datos de formulario para recuperar datos de la base de datos
* Invocar un servicio del Modelo de datos de formulario para agregar datos a la base de datos
* Ejecutar una comprobación de validaciones y mostrar mensajes de error

Las imágenes interactivas de GIF al final de cada sección del tutorial le ayudan a aprender y validar la funcionalidad del formulario que está creando sobre la marcha.

## Paso 1: Recuperar un registro de cliente de la base de datos {#retrieve-customer-record}

Se ha creado un modelo de datos de formulario siguiendo las [crear modelo de datos de formulario](/help/forms/using/create-form-data-model.md) artículo. Ahora, puede utilizar el editor de reglas para invocar los servicios del Modelo de datos de Forms para recuperar y agregar información a la base de datos.

A cada cliente se le asigna un número de ID de cliente único, que ayuda a identificar los datos de clientes relevantes en una base de datos. El procedimiento siguiente utiliza el ID de cliente para recuperar información de la base de datos:

1. Abra el formulario adaptable para editarlo.

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. Toque . **[!UICONTROL ID de cliente]** toque el campo **[!UICONTROL Editar reglas]** icono. Se abre la ventana Editor de reglas.
1. Toque . **[!UICONTROL + Crear]** para agregar una regla. Abre el Editor visual.

   En el Editor visual, la variable **[!UICONTROL WHEN]** está seleccionada de forma predeterminada. Además, el objeto de formulario (en este caso, **[!UICONTROL ID de cliente]**) desde donde inició el editor de reglas se especifica en la sección **[!UICONTROL WHEN]** instrucción.

1. Toque . **[!UICONTROL Seleccionar estado]** y seleccione **[!UICONTROL se cambia]**.

   ![whcompromestomeridischanged](assets/whencustomeridischanged.png)

1. En el **[!UICONTROL ENTONCES]** , seleccione **[!UICONTROL Invocar servicio]** de la variable **[!UICONTROL Seleccionar acción]** lista desplegable.
1. Seleccione el **[!UICONTROL Recuperar dirección de envío]** del **[!UICONTROL Select]** lista desplegable.
1. Arrastre y suelte la **[!UICONTROL ID de cliente]** del campo de la ficha Objetos de formulario al **[!UICONTROL Colocar objeto o seleccionar aquí]** en el campo **[!UICONTROL ENTRADA]** en la ventana

   ![dropobjectstoinputfield-retrieve-data](assets/dropobjectstoinputfield-retrievedata.png)

1. Arrastre y suelte la **[!UICONTROL ID de cliente, nombre, dirección de envío, estado y código postal]** del campo de la ficha Objetos de formulario al **[!UICONTROL Colocar objeto o seleccionar aquí]** en el campo **[!UICONTROL SALIDA]** en la ventana

   ![dropobjectstooutputfield-retrieve-data](assets/dropobjectstooutputfield-retrievedata.png)

   Pulse **[!UICONTROL Listo]** para guardar la regla. En la ventana del editor de reglas, pulse **[!UICONTROL Cerrar]**.

1. Obtenga una vista previa del formulario adaptable. Introduzca un ID en la variable **[!UICONTROL ID de cliente]** campo . El formulario ahora puede recuperar los detalles del cliente de la base de datos.

   ![retrieve-information](assets/retrieve-information.gif)

## Paso 2: Añadir la dirección de cliente actualizada a la base de datos {#updated-customer-address}

Una vez recuperados los detalles del cliente de la base de datos, puede actualizar la dirección de envío, el estado y el código postal. El procedimiento siguiente invoca un servicio del Modelo de datos de formulario para actualizar la información del cliente en la base de datos:

1. Seleccione el **[!UICONTROL Submit]** toque el campo **[!UICONTROL Editar reglas]** icono. Se abre la ventana Editor de reglas.
1. Seleccione el **[!UICONTROL Enviar - Haga clic]** y pulse la **[!UICONTROL Editar]** icono. Aparecerán las opciones para editar la regla Enviar.

   ![submit-rule](assets/submit-rule.png)

   En la opción WHEN , la variable **[!UICONTROL Submit]** y **[!UICONTROL se hace clic]** ya están seleccionadas.

   ![submit-is-clicked](assets/submit-is-clicked.png)

1. En el **[!UICONTROL ENTONCES]** , pulse la opción **[!UICONTROL + Agregar instrucción]** . Select **[!UICONTROL Invocar servicio]** de la variable **[!UICONTROL Seleccionar acción]** lista desplegable.
1. Seleccione el **[!UICONTROL Actualizar dirección de envío]** del **[!UICONTROL Select]** lista desplegable.

   ![update-Shipping-address](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. Arrastre y suelte la **[!UICONTROL Dirección de envío, estado y código postal]** del campo [!UICONTROL Objetos de formulario] a la propiedad .property correspondiente del nombre de tabla (por ejemplo, customerdetails.ShippingAddress) del **[!UICONTROL Colocar objeto o seleccionar aquí]** en el campo **[!UICONTROL ENTRADA]** en la ventana Todos los campos con el prefijo tablename (por ejemplo, los detalles del cliente en este caso de uso) sirven como datos de entrada para el servicio de actualización. Todo el contenido proporcionado en estos campos se actualiza en el origen de datos.

   >[!NOTE]
   >
   >No arrastre y suelte la variable **[!UICONTROL Nombre]** y **[!UICONTROL ID de cliente]** a la propiedad tablename.property correspondiente (por ejemplo, customerdetails.name). Ayuda a evitar actualizar el nombre y el ID del cliente por error.

1. Arrastre y suelte la **[!UICONTROL ID de cliente]** del campo [!UICONTROL Objetos de formulario] a la pestaña id del campo **[!UICONTROL ENTRADA]** en la ventana Los campos sin un nombre de tabla prefijado (por ejemplo, detalles del cliente en este caso de uso) sirven como parámetro de búsqueda para el servicio de actualización. La variable **[!UICONTROL id]** en este caso de uso identifica de forma exclusiva un registro de la variable  **detalles del cliente**  tabla.
1. Pulse **[!UICONTROL Listo]** para guardar la regla. En la ventana del editor de reglas, pulse **[!UICONTROL Cerrar]**.
1. Obtenga una vista previa del formulario adaptable. Recupere detalles de un cliente, actualice la dirección de envío y envíe el formulario. Cuando recupere los detalles del mismo cliente de nuevo, se mostrará la dirección de envío actualizada.

## Paso 3: (Sección Bonus) Utilice el editor de código para ejecutar las validaciones y mostrar los mensajes de error {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

Debe ejecutar la validación en el formulario para asegurarse de que los datos introducidos en el formulario son correctos y se muestra un mensaje de error en caso de datos incorrectos. Por ejemplo, si se introduce un ID de cliente no existente en el formulario, se debería mostrar un mensaje de error.

Los formularios adaptables proporcionan varios componentes con validaciones integradas, por ejemplo, campos numéricos y de correo electrónico que se pueden utilizar para casos de uso comunes. Utilice el editor de reglas para casos de uso avanzados, por ejemplo, para mostrar un mensaje de error cuando la base de datos devuelve registros cero (0) (sin registros).

El siguiente procedimiento muestra cómo crear una regla para mostrar un mensaje de error si el ID de cliente introducido en el formulario no existe en la base de datos. La regla también lleva el foco a y restablece el **[!UICONTROL ID de cliente]** campo . La regla utiliza [la API dataIntegrationUtils del servicio del modelo de datos de formulario](/help/forms/using/invoke-form-data-model-services.md) para comprobar si el ID de cliente existe en la base de datos.

1. Toque . **[!UICONTROL ID de cliente]** toque el campo `Edit Rules` icono. La variable [!UICONTROL Editor de reglas] se abre.
1. Toque . **[!UICONTROL + Crear]** para agregar una regla. Abre el Editor visual.

   En el Editor visual, la variable **[!UICONTROL WHEN]** está seleccionada de forma predeterminada. Además, el objeto de formulario (en este caso, **[!UICONTROL ID de cliente]**) desde donde inició el editor de reglas se especifica en la sección **[!UICONTROL WHEN]** instrucción.

1. Toque . **[!UICONTROL Seleccionar estado]** y seleccione **[!UICONTROL se cambia]**.

   ![whcompromestomeridischanged](assets/whencustomeridischanged.png)

   En el **[!UICONTROL ENTONCES]** , seleccione **[!UICONTROL Invocar servicio]** de la variable **[!UICONTROL Seleccionar acción]** lista desplegable.

1. Cambiar desde **[!UICONTROL Editor visual]** a **[!UICONTROL Editor de código]**. El control del interruptor se encuentra en el lado derecho de la ventana. Se abre el Editor de código, que muestra código similar al siguiente:

   ![code-editor](assets/code-editor.png)

1. Reemplace la sección de la variable de entrada con el siguiente código:

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. Sustituya el `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` con el siguiente código:

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

1. Obtenga una vista previa del formulario adaptable. Introduzca un ID de cliente incorrecto. Aparece un mensaje de error.

   ![display-validation-error](assets/display-validation-error.gif)
