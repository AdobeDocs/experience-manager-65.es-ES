---
title: '"Tutorial: Crear modelo de datos de formulario"'
seo-title: Crear modelo de datos de formulario para comunicación interactiva
description: Crear modelo de datos de formulario para comunicación interactiva
seo-description: Crear modelo de datos de formulario para comunicación interactiva
uuid: b56d3dac-be54-4812-b958-38a085686218
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5413fb3-9d50-4f4f-9db8-7e53cd5145d5
docset: aem65
translation-type: tm+mt
source-git-commit: 709d8fe467f5449eb1e844a49126535a4a4a6e7a

---


# Tutorial: Create form data model{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Este tutorial es un paso en la [serie Crear una primera comunicación](/help/forms/using/create-your-first-interactive-communication.md) interactiva. Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

## Acerca del tutorial {#about-the-tutorial}

El módulo de integración de datos de AEM Forms le permite crear un modelo de datos de formulario a partir de orígenes de datos de back-end dispares, como perfil de usuario de AEM, servicios web RESTful, servicios web basados en SOAP, servicios OData y bases de datos relacionales. Puede configurar objetos y servicios de modelo de datos en un modelo de datos de formulario y asociarlo a un formulario adaptable. Los campos de formulario adaptables están enlazados a las propiedades del objeto del modelo de datos. Los servicios permiten rellenar previamente el formulario adaptable y escribir los datos del formulario enviados en el objeto del modelo de datos.

Para obtener más información sobre la integración de datos de formularios y el modelo de datos de formularios, consulte Integración [de datos de formularios de](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html)AEM.

Este tutorial lo acompaña a través de los pasos para preparar, crear, configurar y asociar un modelo de datos de formulario con una comunicación interactiva. Al final de este tutorial, podrá:

* [Configuración de la base de datos](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [Configurar la base de datos MySQL como fuente de datos](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [Crear modelo de datos de formulario](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [Configurar modelo de datos de formulario](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [Probar modelo de datos de formulario](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

El modelo de datos de formulario tiene un aspecto similar al siguiente:

![Modelo de datos de formulario](assets/form_data_model_callouts_new.png)

**********A. Fuentes de datos** B configuradas. Esquemas de fuentes de datos **C.** Servicios disponibles **D. Objetos del modelo de datos** E. Servicios configurados

## Requisitos previos {#prerequisites}

Antes de comenzar, asegúrese de que dispone de lo siguiente:

* Base de datos MySQL con datos de ejemplo como se indica en la sección [Configurar la base de datos](../../forms/using/create-form-data-model0.md#step-set-up-the-database) .
* Paquete OSGi para el controlador JDBC MySQL como se explica en [Compilación del controlador de base de datos JDBC](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)

## Paso 1: Configuración de la base de datos {#step-set-up-the-database}

Una base de datos es esencial para crear una comunicación interactiva. Este tutorial utiliza una base de datos para mostrar el modelo de datos de formulario y las capacidades de persistencia de las comunicaciones interactivas. Configure una base de datos que contenga tablas de cliente, facturas y llamadas.
La siguiente imagen ilustra los datos de muestra de la tabla de clientes:

![sample_data_cust](assets/sample_data_cust.png)

La tabla de llamadas incluye los detalles de la llamada, como la fecha de llamada, la hora de llamada, el número de llamada, la duración de la llamada y los cargos de la llamada. La tabla de cliente se vincula a la tabla de llamadas mediante el campo Número móvil (mobilenum). Por cada número de móvil que aparece en la tabla de clientes, hay varios registros en la tabla de llamadas. Por ejemplo, puede recuperar los detalles de la llamada del número móvil **1457892541** haciendo referencia a la tabla de llamadas.

La tabla de facturas incluye los detalles de la factura, como la fecha de facturación, el período de facturación, los cargos mensuales y los cargos de llamada. La tabla de cliente se vincula a la tabla de facturas mediante el campo Plan de facturas. Hay un plan asociado a cada cliente en la tabla del cliente. La tabla de facturas incluye los detalles de precios de todos los planes existentes. Por ejemplo, puede recuperar los detalles del plan de **Sarah** de la tabla de clientes y usarlos para recuperar los detalles de precios de la tabla de facturas.

## Paso 2: Configurar la base de datos MySQL como fuente de datos {#step-configure-mysql-database-as-data-source}

Puede configurar distintos tipos de orígenes de datos para crear un modelo de datos de formulario. Para este tutorial, usted configurará la base de datos MySQL que está configurada y llena con datos de muestra. Para obtener información sobre otras fuentes de datos admitidas y cómo configurarlas, consulte Integración [de datos de formularios](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html)AEM.

Haga lo siguiente para configurar su base de datos MySQL:

1. Instale el controlador JDBC para la base de datos MySQL como un paquete OSGi:

   1. Inicie sesión en la instancia de creación de AEM Forms como administrador y vaya a los paquetes de la consola web de AEM. La dirección URL predeterminada es [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).
   1. Toque **Instalar/Actualizar**. Aparece el cuadro de diálogo **Cargar e instalar paquetes** .

   1. Toque **Elegir archivo** para buscar y seleccionar el paquete OSGi del controlador JDBC de MySQL. Seleccione **Iniciar paquete** y **Actualizar paquetes**, y toque **Instalar** o **Actualizar**. Asegúrese de que el controlador JDBC de Oracle Corporation para MySQL está activo. El controlador está instalado.

1. Configure la base de datos MySQL como una fuente de datos:

   1. Vaya a la consola web de AEM en [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Localice la configuración de **Apache Sling Connection Pooled DataSource** . Toque para abrir la configuración en modo de edición.
   1. En el cuadro de diálogo de configuración, especifique los siguientes detalles:

      * **** Nombre del origen de datos: Puede especificar cualquier nombre. Por ejemplo, especifique **MySQL**.

      * **Nombre** de propiedad del servicio DataSource: Especifique el nombre de la propiedad de servicio que contiene el nombre de DataSource. Se especifica al registrar la instancia del origen de datos como servicio OSGi. Por ejemplo, **datasource.name**.

      * **Clase** de controlador JDBC: Especifique el nombre de clase Java del controlador JDBC. Para la base de datos MySQL, especifique **com.mysql.jdbc.Driver**.

      * **URI** de conexión JDBC: Especifique la dirección URL de conexión de la base de datos. Para la base de datos MySQL que se ejecuta en el puerto 3306 y en el esquema teleca, la dirección URL es: jdbc:mysql://[server]:3306/teleca?autoReconnect=true&amp;useUnicode=true&amp;characterEncoding=utf-8
      * **** Nombre de usuario: Nombre de usuario de la base de datos. Es necesario habilitar el controlador JDBC para establecer una conexión con la base de datos.
      * **** Contraseña: Contraseña de la base de datos. Es necesario habilitar el controlador JDBC para establecer una conexión con la base de datos.
      * **** Prueba a tomar prestado: Habilite la opción **Probar en préstamo** .

      * **** Prueba al regresar: Active la opción **Prueba al regresar** .

      * **** Consulta de validación: Especifique una consulta SQL SELECT para validar conexiones desde el grupo. La consulta debe devolver al menos una fila. Por ejemplo, **seleccione * del cliente**.

      * **Aislamiento** de transacciones: Establezca el valor en **READ_COMMITTED**.
   Deje otras propiedades con [los valores](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) predeterminados y toque **Guardar**.

   Se crea una configuración similar a la siguiente.

   ![Configuración de Apache](assets/apache_configuration_new.png)

## Step 3: Create form data model {#step-create-form-data-model}

AEM Forms proporciona una interfaz de usuario intuitiva para [crear un](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)modelo de datos de formulario a partir de orígenes de datos configurados. Puede utilizar varios orígenes de datos en un modelo de datos de formulario. Para el caso de uso en este tutorial, utilizará MySQL como fuente de datos.

Para crear el modelo de datos de formulario, haga lo siguiente:

1. En la instancia de creación de AEM, vaya a **Formularios** > Integraciones **de datos**.
1. Tap **Create** > **Form Data Model**.
1. En el asistente Crear modelo de datos de formulario, especifique un **nombre** para el modelo de datos de formulario. Por ejemplo, **FDM_Create_First_IC**. Puntee **Siguiente**.
1. La pantalla Seleccionar fuente de datos muestra todas las fuentes de datos configuradas. Seleccione el origen de datos **MySQL** y toque **Crear**.

   ![Origen de datos MYSQL](assets/fdm_mysql_data_source_new.png)

1. Haga clic en **Finalizado**. Se crea el modelo de datos de formulario **FDM_Create_First_IC** .

## Paso 4: Configurar modelo de datos de formulario {#step-configure-form-data-model}

La configuración del modelo de datos de formulario incluye:

* [adición de objetos y servicios del modelo de datos](#add-data-model-objects-and-services)
* [creación de propiedades secundarias calculadas para el objeto del modelo de datos](#create-computed-child-properties-for-data-model-object)
* [adición de asociaciones entre objetos de modelo de datos](#add-associations-between-data-model-objects)
* [edición de propiedades del objeto del modelo de datos](#edit-data-model-object-properties)
* [configuración de servicios para objetos de modelo de datos](#configure-services)

### Agregar objetos y servicios de modelos de datos {#add-data-model-objects-and-services}

1. En la instancia de creación de AEM, vaya a **Formularios** > Integraciones **de datos**. La dirección URL predeterminada es [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. El modelo de datos de formulario **FDM_Create_First_IC** que creó anteriormente se muestra aquí. Selecciónelo y toque **Editar**.

   La fuente de datos seleccionada **MySQL** se muestra en el panel Fuentes **** de datos.

   ![Origen de datos MYSQL para FDM](assets/mysql_fdm_new.png)

1. Expanda el árbol de fuentes de datos **MySQL** . Seleccione los siguientes objetos y servicios del modelo de datos del esquema de **telecomunicaciones** :

   * **Objetos** del modelo de datos:

      * facturas
      * llamadas
      * cliente
   * **Servicios:**

      * get
      * actualizar
   Toque **Agregar selección** para agregar objetos y servicios del modelo de datos seleccionado al modelo de datos de formulario.

   ![Seleccionar servicios de objetos del modelo de datos](assets/select_data_model_object_services_new.png)

   Los objetos de listas, llamadas y modelos de datos del cliente se muestran en el panel derecho de la ficha **Modelo** . Los servicios de obtención y actualización se muestran en la ficha **Servicios** .

   ![Objetos del modelo de datos](assets/data_model_objects_new.png)

### Crear propiedades secundarias calculadas para el objeto del modelo de datos {#create-computed-child-properties-for-data-model-object}

Una propiedad calculada es aquella cuyo valor se calcula en función de una regla o una expresión. Mediante una regla, puede establecer el valor de una propiedad calculada en una cadena literal, un número, un resultado de una expresión matemática o el valor de otra propiedad en el modelo de datos de formulario.

En función del caso de uso, cree la propiedad **usagecharges** secundario computed en el objeto del modelo de datos de **facturas** utilizando la siguiente expresión matemática:

* cargos por uso = cargos por llamada + cargos por llamada de conferencia + cargos por SMS + cargos por Internet móvil + roaming nacional + itinerancia internacional + VAS (todas estas propiedades existen en el objeto de modelo de datos de facturas)Para obtener más información sobre la propiedad **calculada de cobros** por uso, consulte [Plan the Interactive Communication](/help/forms/using/planning-interactive-communications.md).

Ejecute los siguientes pasos para crear propiedades secundarias calculadas para el objeto de modelo de datos de listas:

1. Seleccione la casilla de verificación situada en la parte superior del objeto del modelo de datos de **facturas** para seleccionarlo y tocar **Crear propiedad** secundaria.
1. En el panel **Crear propiedad** secundaria:

   1. Introduzca **usagecharges** como nombre de la propiedad secundaria.
   1. Habilitar **calculada**.
   1. Seleccione **Flotar** como tipo y toque **Listo** para agregar la propiedad secundaria al objeto del modelo de datos de **listas** .
   ![Crear propiedad secundaria](assets/create_child_property_new.png)

1. Toque **Editar regla** para abrir el Editor de reglas.
1. Toque **Crear**. Se abre la ventana **de regla Definir valor** .
1. En la lista desplegable Seleccionar opción, seleccione Expresión **** matemática.

   ![Editor de reglas de cargos de uso](assets/usage_charges_rule_editor_new.png)

1. En la expresión matemática, seleccione **callloads** y **confcallloads** como primer y segundo objeto, respectivamente. Seleccione **más** como operador. Toque dentro de la expresión matemática y **Ampliar expresión** para agregar **smsloads**, **internetfees**, **roamingnational**, **roamingintnl****** y objetos vas a la expresión.

   La siguiente imagen muestra la expresión matemática en el editor de reglas:

   ![Regla de cargos de uso](assets/usage_charges_rule_all_new.png)

1. Puntee **Listo**. La regla se crea en el Editor de reglas.
1. Toque **Cerrar** para cerrar la ventana Editor de reglas.

### Adición de asociaciones entre objetos de modelo de datos {#add-associations-between-data-model-objects}

Una vez definidos los objetos del modelo de datos, puede crear asociaciones entre ellos. La asociación puede ser uno a uno o uno a varios. Por ejemplo, puede haber varios dependientes asociados a un empleado. Se denomina asociación de uno a varios y se describe con 1:n en la línea que conecta objetos del modelo de datos asociados. Sin embargo, si una asociación devuelve un nombre de empleado único para un ID de empleado determinado, se denomina asociación uno a uno.

Cuando se agregan objetos de modelo de datos asociados en un origen de datos a un modelo de datos de formulario, sus asociaciones se conservan y se muestran como conectadas por líneas de flecha.

En función del caso de uso, cree las siguientes asociaciones entre los objetos del modelo de datos:

| Asociación | Objetos del modelo de datos |
|---|---|
| 1:n | cliente:llamadas (se pueden asociar varias llamadas con un cliente en una factura mensual) |
| 1:1 | cliente:facturas (una factura está asociada con un cliente durante un mes en particular) |

Realice los siguientes pasos para crear asociaciones entre objetos del modelo de datos:

1. Seleccione la casilla de verificación situada en la parte superior del objeto del modelo de datos del **cliente** para seleccionarlo y tocar **Agregar asociación**. Se abre el panel de propiedades **Agregar asociación** .
1. En el panel **Agregar asociación** :

   * Especifique un título para la asociación. Es un campo opcional.
   * Seleccione **Uno a Muchos** en la lista desplegable **Tipo** .

   * Seleccione **llamadas** en la lista desplegable Objeto **** modelo.

   * Seleccione **Obtener** en la lista desplegable **Servicio** .

   * Toque **Agregar** para vincular el objeto del modelo de datos del **cliente** al objeto del modelo de datos de **llamadas** mediante una propiedad. En función del caso de uso, el objeto del modelo de datos de llamadas debe estar vinculado a la propiedad de número móvil en el objeto del modelo de datos del cliente. Se abre el cuadro de diálogo **Agregar argumento** .
   ![Agregar asociación](assets/add_association_new.png)

1. En el cuadro de diálogo **Agregar argumento** :

   * Seleccione **mobilenum** en la lista desplegable **Nombre** . La propiedad mobile number es una propiedad común que está disponible en el cliente y llama a objetos del modelo de datos. Como resultado, se utiliza para crear una asociación entre el cliente y los objetos del modelo de datos de llamadas.
Para cada número móvil disponible en el objeto del modelo de datos del cliente, hay varios registros de llamadas disponibles en la tabla de llamadas.

   * Especifique un título y una descripción opcionales para el argumento.
   * Seleccione **cliente** en la lista desplegable **Enlace a** .

   * Seleccione **mobilenum** en la lista desplegable Valor **de** enlace.

   * Toque **Agregar**.
   ![Agregar asociación para un argumento](assets/add_association_argument_new.png)

   La propiedad mobilenum se muestra en la sección **Argumentos** .

   ![Agregar asociación de argumentos](assets/add_argument_association_new.png)

1. Puntee **Listo** para crear una asociación 1:n entre los objetos del modelo de datos de cliente y de llamada.

   Una vez que haya creado una asociación entre los objetos del modelo de datos cliente y las llamadas, cree una asociación 1:1 entre el cliente y los objetos del modelo de datos de facturación.

1. Seleccione la casilla de verificación situada en la parte superior del objeto del modelo de datos del **cliente** para seleccionarlo y tocar **Agregar asociación**. Se abre el panel de propiedades **Agregar asociación** .
1. En el panel **Agregar asociación** :

   * Especifique un título para la asociación. Es un campo opcional.
   * Seleccione **Uno a Uno** en la lista desplegable **Tipo** .

   * Seleccione **listas** en la lista desplegable Objeto **** modelo.

   * Seleccione **Obtener** en la lista desplegable **Servicio** . La propiedad **billplan** , que es la clave principal de la tabla de facturas, ya está disponible en la sección **Argumentos** .
Los objetos del modelo de datos de clientes y facturas se vinculan mediante las propiedades de plan de facturación (facturas) y plan del cliente (cliente), respectivamente. Cree un enlace entre estas propiedades para recuperar los detalles del plan de cualquier cliente disponible en la base de datos de MySQL.

   * Seleccione **cliente** en la lista desplegable **Enlace a** .

   * Seleccione **customerplan** en la lista desplegable Valor **de** enlace.

   * Puntee **Listo** para crear un enlace entre las propiedades de plan de facturación y plan del cliente.
   ![Agregar asociación para la factura de cliente](assets/add_association_customer_bills_new.png)

   La siguiente imagen muestra las asociaciones entre los objetos del modelo de datos y las propiedades utilizadas para crear asociaciones entre ellos:

   ![fdm_groups](assets/fdm_associations.gif)

### Editar propiedades del objeto del modelo de datos {#edit-data-model-object-properties}

Después de crear asociaciones entre el cliente y otros objetos del modelo de datos, edite las propiedades del cliente para definir la propiedad en función de la cual se recuperan los datos del objeto del modelo de datos. En función del caso de uso, el número móvil se utiliza como propiedad para recuperar datos del objeto del modelo de datos del cliente.

1. Seleccione la casilla de verificación situada en la parte superior del objeto del modelo de datos del **cliente** para seleccionarlo y tocar **Editar propiedades**. Se abre el panel **Editar propiedades** .
1. Especifique **cliente** como el objeto **Modelo de nivel** superior.
1. Seleccione **Obtener** en la lista desplegable Servicio **de** lectura.
1. En la sección **Argumentos** :

   * Seleccione **Solicitar atributo** en la lista desplegable **Enlace a** .

   * Especifique **mobilenum** como valor de enlace.

1. Seleccione **actualizar** en la lista desplegable Servicio de **escritura** .
1. En la sección **Argumentos** :

   * Para la propiedad **mobilenum** , seleccione **cliente** en la lista desplegable **Enlace a** .

   * Seleccione **mobilenum** en la lista desplegable Valor **de** enlace.

1. Toque **Listo** para guardar las propiedades.

   ![Configurar servicios](assets/configure_services_customer_new.png)

1. Seleccione la casilla de verificación situada en la parte superior del objeto del modelo de datos de **llamadas** para seleccionarlo y tocar **Editar propiedades**. Se abre el panel **Editar propiedades** .
1. Desactive el objeto **Modelo de nivel** superior para el objeto del modelo de datos de **llamadas** .
1. Puntee **Listo**.

   Repita los pasos 8 a 10 para configurar las propiedades del objeto del modelo de datos de **listas** .

### Configurar servicios {#configure-services}

1. Vaya a la ficha **Servicios** .
1. Seleccione el servicio **get** y toque **Editar propiedades**. Se abre el panel **Editar propiedades** .
1. En el panel **Editar propiedades** :

   * Introduzca un título y una descripción opcionales.
   * Seleccione **cliente** en la lista desplegable Objeto **del modelo de** salida.

   * Toque **Listo** para guardar las propiedades.
   ![Editar propiedades](assets/edit_properties_get_details_new.png)

1. Seleccione el servicio de **actualización** y toque **Editar propiedades**. Se abre el panel **Editar propiedades** .
1. En el panel **Editar propiedades** :

   * Introduzca un título y una descripción opcionales.
   * Seleccione **cliente** en la lista desplegable Objeto **del modelo de** entrada.

   * Puntee **Listo**.
   * Toque **Guardar** para guardar el modelo de datos de formulario.
   ![Actualizar propiedades del servicio](assets/update_service_properties_new.png)

## Paso 5: Probar el modelo y los servicios de datos de formulario {#step-test-form-data-model-and-services}

Puede probar el objeto y los servicios del modelo de datos para comprobar que el modelo de datos de formulario está configurado correctamente.

Para ejecutar la prueba, haga lo siguiente:

1. Vaya a la ficha **Modelo** , seleccione el objeto del modelo de datos del **cliente** y toque Objeto **del modelo de prueba**.
1. En la ventana **Probar modelo** de datos de formulario, seleccione **Leer objeto** de modelo en la lista desplegable **Seleccionar modelo/servicio** .
1. En la sección **Entrada** , especifique un valor para la propiedad **mobilenum** que existe en la base de datos MySQL configurada y toque **Prueba**.

   Los detalles del cliente asociados con la propiedad mobilenum especificada se recuperan y se muestran en la sección Salida, como se muestra a continuación. Cierre el cuadro de diálogo.

   ![Probar modelo de datos](assets/test_data_model_new.png)

1. Vaya a la ficha **Servicios** .
1. Seleccione el servicio **get** y toque Servicio **de pruebas.**
1. En la sección **Entrada** , especifique un valor para la propiedad **mobilenum** que existe en la base de datos MySQL configurada y toque **Prueba**.

   Los detalles del cliente asociados con la propiedad mobilenum especificada se recuperan y se muestran en la sección Salida, como se muestra a continuación. Cierre el cuadro de diálogo.

   ![Servicio de pruebas](assets/test_service_new.png)

### Editar y guardar datos de muestra {#edit-and-save-sample-data}

El editor del modelo de datos de formulario permite generar datos de ejemplo para todas las propiedades de objeto del modelo de datos, incluidas las propiedades calculadas, en un modelo de datos de formulario. Es un conjunto de valores aleatorios que cumplen el tipo de datos configurado para cada propiedad. También puede editar y guardar datos, que se conservan aunque vuelva a generar los datos de ejemplo.

Para generar, editar y guardar datos de ejemplo, haga lo siguiente:

1. En la página del modelo de datos de formulario, toque **Editar datos** de ejemplo. Genera y muestra los datos de ejemplo en la ventana Editar datos de muestra.

   ![Editar datos de muestra](assets/edit_sample_data_new.png)

1. En la ventana **Editar datos** de ejemplo, edite los datos según sea necesario y toque **Guardar**. Cierre la ventana.


