---
title: Aplicación de reglas a campos de formulario adaptables
seo-title: Aplicación de reglas a campos de formulario adaptables
description: Cree reglas para agregar interactividad, lógica empresarial y validaciones inteligentes a un formulario adaptable.
seo-description: Cree reglas para agregar interactividad, lógica empresarial y validaciones inteligentes a un formulario adaptable.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
source-git-commit: 63bc43bba88a42d62fb574bc8ce42470ac61d693
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 0%

---

# Tutorial: Aplicación de reglas a campos de formulario adaptables {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

Este tutorial es un paso de la serie [Create Your First Adaptive Form](/help/forms/using/create-your-first-adaptive-form.md). Adobe recomienda seguir la serie en secuencia cronológica para comprender, realizar y mostrar el caso de uso completo del tutorial.

## Acerca del tutorial {#about-the-tutorial}

Puede utilizar reglas para agregar interactividad, lógica empresarial y validaciones inteligentes a un formulario adaptable. Los formularios adaptables tienen un editor de reglas integrado. El editor de reglas proporciona una funcionalidad de arrastrar y soltar, similar a las visitas guiadas. El método de arrastrar y soltar es el más rápido y sencillo para crear reglas. El editor de reglas también proporciona una ventana de código para los usuarios interesados en probar sus habilidades de codificación o llevar las reglas al siguiente nivel.

Puede obtener más información sobre el editor de reglas en [Editor de reglas de Forms adaptable](/help/forms/using/rule-editor.md).

Al final del tutorial, aprenderá a crear reglas para:

* Invocar un servicio del Modelo de datos de formulario para recuperar datos de la base de datos
* Invocar un servicio del Modelo de datos de formulario para agregar datos a la base de datos
* Ejecutar una comprobación de validaciones y mostrar mensajes de error

Las imágenes GIF interactivas al final de cada sección del tutorial le ayudan a aprender y validar la funcionalidad del formulario que está creando sobre la marcha.

## Paso 1: Recuperar un registro de cliente de la base de datos {#retrieve-customer-record}

Ha creado un modelo de datos de formulario siguiendo el artículo [crear modelo de datos de formulario](/help/forms/using/create-form-data-model.md). Ahora, puede utilizar el editor de reglas para invocar los servicios del Modelo de datos de Forms para recuperar y agregar información a la base de datos.

A cada cliente se le asigna un número de ID de cliente único, que ayuda a identificar los datos de clientes relevantes en una base de datos. El procedimiento siguiente utiliza el ID de cliente para recuperar información de la base de datos:

1. Abra el formulario adaptable para editarlo.

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. Pulse el campo **[!UICONTROL Customer ID]** y pulse el icono **[!UICONTROL Editar reglas]**. Se abre la ventana Editor de reglas.
1. Pulse el icono **[!UICONTROL + Crear]** para añadir una regla. Abre el Editor visual.

   En el Editor visual, la instrucción **[!UICONTROL WHEN]** está seleccionada de forma predeterminada. Además, el objeto de formulario (en este caso, **[!UICONTROL Customer ID]**) desde el que inició el editor de reglas se especifica en la instrucción **[!UICONTROL WHEN]**.

1. Pulse la lista desplegable **[!UICONTROL Select State]** y seleccione **[!UICONTROL is changed]**.

   ![whcompromestomeridischanged](assets/whencustomeridischanged.png)

1. En la instrucción **[!UICONTROL THEN]**, seleccione **[!UICONTROL Invocar servicio]** en la lista desplegable **[!UICONTROL Seleccionar acción]**.
1. Seleccione el servicio **[!UICONTROL Retrieve Shipping Address]** en la lista desplegable **[!UICONTROL Select]**.
1. Arrastre y suelte el campo **[!UICONTROL Customer ID]** de la ficha Objetos de formulario al objeto **[!UICONTROL Soltar o seleccione aquí]** en el cuadro **[!UICONTROL ENTRADA]**.

   ![dropobjectstoinputfield-retrieve-data](assets/dropobjectstoinputfield-retrievedata.png)

1. Arrastre y suelte el campo **[!UICONTROL Customer ID, Name, Shipping Address, State y Zip Code]** de la ficha Objetos del formulario al objeto **[!UICONTROL Drop o seleccione aquí]** en el cuadro **[!UICONTROL OUTPUT]**.

   ![dropobjectstooutputfield-retrieve-data](assets/dropobjectstooutputfield-retrievedata.png)

   Toque **[!UICONTROL Listo]** para guardar la regla. En la ventana del editor de reglas, pulse **[!UICONTROL Cerrar]**.

1. Obtenga una vista previa del formulario adaptable. Introduzca un ID en el campo **[!UICONTROL Customer ID]**. El formulario ahora puede recuperar los detalles del cliente de la base de datos.

   ![retrieve-information](assets/retrieve-information.gif)

## Paso 2: Añadir la dirección de cliente actualizada a la base de datos {#updated-customer-address}

Una vez recuperados los detalles del cliente de la base de datos, puede actualizar la dirección de envío, el estado y el código postal. El procedimiento siguiente invoca un servicio del Modelo de datos de formulario para actualizar la información del cliente en la base de datos:

1. Seleccione el campo **[!UICONTROL Submit]** y pulse el icono **[!UICONTROL Editar reglas]**. Se abre la ventana Editor de reglas.
1. Seleccione la regla **[!UICONTROL Submit - Click]** y pulse el icono **[!UICONTROL Edit]**. Aparecerán las opciones para editar la regla Enviar.

   ![submit-rule](assets/submit-rule.png)

   En la opción WHEN , las opciones **[!UICONTROL Submit]** y **[!UICONTROL is clicked]** ya están seleccionadas.

   ![submit-is-clicked](assets/submit-is-clicked.png)

1. En la opción **[!UICONTROL THEN]**, pulse la opción **[!UICONTROL + Agregar instrucción]**. Seleccione **[!UICONTROL Invocar servicio]** en la lista desplegable **[!UICONTROL Seleccionar acción]**.
1. Seleccione el servicio **[!UICONTROL Update Shipping Address]** en la lista desplegable **[!UICONTROL Select]**.

   ![update-Shipping-address](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. Arrastre y suelte el campo **[!UICONTROL Dirección de envío, estado y código postal]** de la ficha [!UICONTROL Objetos de formulario] a la propiedad .nombre de tabla correspondiente (por ejemplo, detalles del cliente .ShippingAddress) del campo **[!UICONTROL Colocar o seleccione aquí]** en el cuadro **[!UICONTROL ENPUT]**. Todos los campos con el prefijo tablename (por ejemplo, los detalles del cliente en este caso de uso) sirven como datos de entrada para el servicio de actualización. Todo el contenido proporcionado en estos campos se actualiza en el origen de datos.

   >[!NOTE]
   >
   >No arrastre y suelte los campos **[!UICONTROL Name]** y **[!UICONTROL Customer ID]** en la propiedad correspondiente de nombre de tabla (por ejemplo, customerdetails.name). Ayuda a evitar actualizar el nombre y el ID del cliente por error.

1. Arrastre y suelte el campo **[!UICONTROL Customer ID]** de la pestaña [!UICONTROL Form Objects] al campo id del cuadro **[!UICONTROL INPUT]**. Los campos sin un nombre de tabla prefijado (por ejemplo, detalles del cliente en este caso de uso) sirven como parámetro de búsqueda para el servicio de actualización. El campo **[!UICONTROL id]** en este caso de uso identifica de forma exclusiva un registro de la tabla **customerdetails**.
1. Toque **[!UICONTROL Listo]** para guardar la regla. En la ventana del editor de reglas, pulse **[!UICONTROL Cerrar]**.
1. Obtenga una vista previa del formulario adaptable. Recupere detalles de un cliente, actualice la dirección de envío y envíe el formulario. Cuando recupere los detalles del mismo cliente de nuevo, se mostrará la dirección de envío actualizada.

## Paso 3: (Sección Bonus) Utilice el editor de código para ejecutar las validaciones y mostrar los mensajes de error {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

Debe ejecutar la validación en el formulario para asegurarse de que los datos introducidos en el formulario son correctos y se muestra un mensaje de error en caso de datos incorrectos. Por ejemplo, si se introduce un ID de cliente no existente en el formulario, se debería mostrar un mensaje de error.

Los formularios adaptables proporcionan varios componentes con validaciones integradas, por ejemplo, campos numéricos y de correo electrónico que se pueden utilizar para casos de uso comunes. Utilice el editor de reglas para casos de uso avanzados, por ejemplo, para mostrar un mensaje de error cuando la base de datos devuelve registros cero (0) (sin registros).

El siguiente procedimiento muestra cómo crear una regla para mostrar un mensaje de error si el ID de cliente introducido en el formulario no existe en la base de datos. La regla también lleva el foco al campo **[!UICONTROL Customer ID]** y lo restablece. La regla utiliza [la API dataIntegrationUtils del servicio del modelo de datos de formulario](/help/forms/using/invoke-form-data-model-services.md) para comprobar si existe el ID de cliente en la base de datos.

1. Pulse el campo **[!UICONTROL Customer ID]** y pulse el icono `Edit Rules`. Se abre la ventana [!UICONTROL Editor de reglas].
1. Pulse el icono **[!UICONTROL + Crear]** para añadir una regla. Abre el Editor visual.

   En el Editor visual, la instrucción **[!UICONTROL WHEN]** está seleccionada de forma predeterminada. Además, el objeto de formulario (en este caso, **[!UICONTROL Customer ID]**) desde el que inició el editor de reglas se especifica en la instrucción **[!UICONTROL WHEN]**.

1. Pulse la lista desplegable **[!UICONTROL Select State]** y seleccione **[!UICONTROL is changed]**.

   ![whcompromestomeridischanged](assets/whencustomeridischanged.png)

   En la instrucción **[!UICONTROL THEN]**, seleccione **[!UICONTROL Invocar servicio]** en la lista desplegable **[!UICONTROL Seleccionar acción]**.

1. Cambie de **[!UICONTROL Editor visual]** a **[!UICONTROL Editor de código]**. El control del interruptor se encuentra en el lado derecho de la ventana. Se abre el Editor de código, que muestra código similar al siguiente:

   ![code-editor](assets/code-editor.png)

1. Reemplace la sección de la variable de entrada con el siguiente código:

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. Reemplace la sección `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` con el siguiente código:

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
