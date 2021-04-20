---
title: '"Tutorial: Crear modelo de datos de formulario"'
seo-title: Creación de un modelo de datos de formulario para la comunicación interactiva
description: Creación de un modelo de datos de formulario para la comunicación interactiva
seo-description: Creación de un modelo de datos de formulario para la comunicación interactiva
uuid: b56d3dac-be54-4812-b958-38a085686218
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5413fb3-9d50-4f4f-9db8-7e53cd5145d5
docset: aem65
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2749'
ht-degree: 0%

---


# Tutorial: Crear modelo de datos de formulario{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Este tutorial es un paso de la serie [Create your first Interactive Communication](/help/forms/using/create-your-first-interactive-communication.md) . Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

## Acerca del tutorial {#about-the-tutorial}

El módulo de integración de datos de AEM Forms le permite crear un modelo de datos de formulario a partir de fuentes de datos backend dispares, como AEM perfil de usuario, servicios web RESTful, servicios web basados en SOAP, servicios OData y bases de datos relacionales. Puede configurar objetos y servicios del modelo de datos en un modelo de datos de formulario y asociarlo a un formulario adaptable. Los campos de formulario adaptables están enlazados a las propiedades de objeto del modelo de datos. Los servicios permiten rellenar previamente el formulario adaptable y escribir los datos de formulario enviados en el objeto del modelo de datos.

Para obtener más información sobre la integración de datos de formulario y el modelo de datos de formulario, consulte [AEM Forms Data Integration](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

Este tutorial lo acompaña durante los pasos para preparar, crear, configurar y asociar un modelo de datos de formulario con una comunicación interactiva. Al final de este tutorial, podrá:

* [Configuración de la base de datos](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [Configurar la base de datos MySQL como fuente de datos](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [Crear modelo de datos de formulario](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [Configuración del modelo de datos de formulario](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [Probar modelo de datos de formulario](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

El modelo de datos de formulario tiene un aspecto similar al siguiente:

![Modelo de datos de formulario](assets/form_data_model_callouts_new.png)

**A.** Fuentes de datos configuradas  **B.** Esquemas de fuentes de datos  **C.** Servicios disponibles  **D.** Objetos de modelos de datos  **E.** Servicios configurados

## Requisitos previos {#prerequisites}

Antes de empezar, asegúrese de que dispone de lo siguiente:

* Base de datos MySQL con datos de ejemplo como se indica en la sección [Configure the database](../../forms/using/create-form-data-model0.md#step-set-up-the-database).
* Paquete OSGi para el controlador JDBC MySQL como se explica en [Agrupación del controlador de base de datos JDBC](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)

## Paso 1: Configuración de la base de datos {#step-set-up-the-database}

Una base de datos es esencial para crear una comunicación interactiva. Este tutorial utiliza una base de datos para mostrar el Modelo de datos de formulario y las capacidades de persistencia de las comunicaciones interactivas. Configure una base de datos que contenga tablas cliente, facturas y llamadas.
La siguiente imagen ilustra datos de ejemplo para la tabla de clientes:

![sample_data_cust](assets/sample_data_cust.png)

Utilice la siguiente instrucción DDL para crear la tabla **customer** en la base de datos.

```sql
CREATE TABLE `customer` (
   `mobilenum` int(11) NOT NULL,
   `name` varchar(45) NOT NULL,
   `address` varchar(45) NOT NULL,
   `alternatemobilenumber` int(11) DEFAULT NULL,
   `relationshipnumber` int(11) DEFAULT NULL,
   `customerplan` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`mobilenum`),
   UNIQUE KEY `mobilenum_UNIQUE` (`mobilenum`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

Utilice la siguiente instrucción DDL para crear la tabla **bill** en la base de datos.

```sql
CREATE TABLE `bills` (
   `billplan` varchar(45) NOT NULL,
   `latepayment` decimal(4,2) NOT NULL,
   `monthlycharges` decimal(4,2) NOT NULL,
   `billdate` date NOT NULL,
   `billperiod` varchar(45) NOT NULL,
   `prevbal` decimal(4,2) NOT NULL,
   `callcharges` decimal(4,2) NOT NULL,
   `confcallcharges` decimal(4,2) NOT NULL,
   `smscharges` decimal(4,2) NOT NULL,
   `internetcharges` decimal(4,2) NOT NULL,
   `roamingnational` decimal(4,2) NOT NULL,
   `roamingintnl` decimal(4,2) NOT NULL,
   `vas` decimal(4,2) NOT NULL,
   `discounts` decimal(4,2) NOT NULL,
   `tax` decimal(4,2) NOT NULL,
   PRIMARY KEY (`billplan`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

Utilice la siguiente instrucción DDL para crear la tabla **calls** en la base de datos.

```sql
CREATE TABLE `calls` (
   `mobilenum` int(11) DEFAULT NULL,
   `calldate` date DEFAULT NULL,
   `calltime` varchar(45) DEFAULT NULL,
   `callnumber` int(11) DEFAULT NULL,
   `callduration` varchar(45) DEFAULT NULL,
   `callcharges` decimal(4,2) DEFAULT NULL,
   `calltype` varchar(45) DEFAULT NULL
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

La tabla **llamadas** incluye los detalles de la llamada, como la fecha de llamada, la hora de llamada, el número de llamada, la duración de la llamada y los cargos por llamada. La tabla **customer** está vinculada a la tabla de llamadas mediante el campo Número móvil (mobilenum) . Para cada número de móvil enumerado en la tabla **customer**, hay varios registros en la tabla **calls**. Por ejemplo, puede recuperar los detalles de la llamada para el número de teléfono móvil **1457892541** haciendo referencia a la tabla **calls** .

La tabla **Billetes** incluye detalles de la factura como fecha de factura, período de factura, cargos mensuales y cargos por llamada. La tabla **customer** está vinculada a la tabla **bill** mediante el campo Plan de Facturación. Hay un plan asociado a cada cliente en la tabla **customer**. La tabla **bill** incluye los detalles de precios de todos los planes existentes. Por ejemplo, puede recuperar los detalles del plan para **Sarah** de la tabla **customer** y usarlos para recuperar los detalles de precios de la tabla **bill**.

## Paso 2: Configurar la base de datos MySQL como fuente de datos {#step-configure-mysql-database-as-data-source}

Puede configurar distintos tipos de orígenes de datos para crear un modelo de datos de formulario. Para este tutorial, configurará la base de datos MySQL que está configurada y llena con datos de ejemplo. Para obtener información sobre otras fuentes de datos compatibles y cómo configurarlas, consulte [AEM Forms Data Integration](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

Haga lo siguiente para configurar la base de datos MySQL:

1. Instale el controlador JDBC para la base de datos MySQL como un paquete OSGi:

   1. Inicie sesión en la instancia de autor de AEM Forms como administrador y vaya a AEM paquetes de consola web. La dirección URL predeterminada es [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).
   1. Pulse **Instalar/Actualizar**. Aparece un cuadro de diálogo **Cargar / Instalar paquetes**.

   1. Toque **Choose File** para buscar y seleccionar el paquete OSGi del controlador JDBC de MySQL. Seleccione **Iniciar paquete** y **Actualizar paquetes** y pulse **Instalar** o **Actualizar**. Asegúrese de que el controlador JDBC de Oracle Corporation para MySQL esté activo. El controlador está instalado.

1. Configure la base de datos MySQL como fuente de datos:

   1. Vaya a AEM consola web en [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Busque la configuración **Apache Sling Connection Pooled DataSource**. Pulse para abrir la configuración en modo de edición.
   1. En el cuadro de diálogo de configuración, especifique los siguientes detalles:

      * **Nombre del origen de datos:** puede especificar cualquier nombre. Por ejemplo, especifique **MySQL**.

      * **Nombre** de propiedad del servicio DataSource: Especifique el nombre de la propiedad de servicio que contiene el nombre de DataSource. Se especifica al registrar la instancia de origen de datos como servicio OSGi. Por ejemplo, **datasource.name**.

      * **Clase** de controlador JDBC: Especifique el nombre de clase Java del controlador JDBC. Para la base de datos MySQL, especifique **com.mysql.jdbc.Driver**.

      * **URI** de conexión JDBC: Especifique la dirección URL de conexión de la base de datos. Para la base de datos MySQL que se ejecuta en el puerto 3306 y en el esquema teleca, la URL es: `jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Nombre de usuario:** Nombre de usuario de la base de datos. Es necesario permitir que el controlador JDBC establezca una conexión con la base de datos.
      * **Contraseña:** Contraseña de la base de datos. Es necesario permitir que el controlador JDBC establezca una conexión con la base de datos.
      * **Probar en la toma de prestado:** active la opción  **Probar en** la toma de prestado.

      * **Probar al volver:** active la opción  **Probar al** volver.

      * **Consulta de validación:** especifique una consulta SQL SELECT para validar conexiones desde el grupo. La consulta debe devolver al menos una fila. Por ejemplo, **seleccione * del cliente**.

      * **Aislamiento** de transacciones: Establezca el valor en  **READ_COMMITTED**.
   Deje otras propiedades con [valores](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) predeterminados y pulse **Guardar**.

   Se crea una configuración similar a la siguiente.

   ![Configuración de Apache](assets/apache_configuration_new.png)

## Paso 3: Crear modelo de datos de formulario {#step-create-form-data-model}

AEM Forms proporciona una interfaz de usuario intuitiva para [crear un modo de datos de formulario](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)l a partir de orígenes de datos configurados. Puede utilizar varios orígenes de datos en un modelo de datos de formulario. Para el caso de uso de este tutorial, utilizará MySQL como fuente de datos.

Para crear el modelo de datos de formulario, haga lo siguiente:

1. En AEM instancia de autor, vaya a **Forms** > **Integraciones de datos**.
1. Pulse **Crear** > **Modelo de datos de formulario**.
1. En el asistente Crear modelo de datos de formulario, especifique un **nombre** para el modelo de datos de formulario. Por ejemplo, **FDM_Create_First_IC**. Toque **Siguiente**.
1. La pantalla seleccionar fuente de datos enumera todas las fuentes de datos configuradas. Seleccione la fuente de datos **MySQL** y pulse **Crear**.

   ![Fuente de datos de MYSQL](assets/fdm_mysql_data_source_new.png)

1. Haga clic en **Listo**. Se crea el modelo de datos de formulario **FDM_Create_First_IC**.

## Paso 4: Configurar el modelo de datos de formulario {#step-configure-form-data-model}

La configuración del modelo de datos de formulario incluye:

* [adición de objetos y servicios del modelo de datos](#add-data-model-objects-and-services)
* [creación de propiedades secundarias calculadas para el objeto del modelo de datos](#create-computed-child-properties-for-data-model-object)
* [adición de asociaciones entre objetos del modelo de datos](#add-associations-between-data-model-objects)
* [edición de propiedades de objeto del modelo de datos](#edit-data-model-object-properties)
* [configuración de servicios para objetos del modelo de datos](#configure-services)

### Agregar objetos y servicios del modelo de datos {#add-data-model-objects-and-services}

1. En AEM instancia de autor, vaya a **Forms** > **Integraciones de datos**. La dirección URL predeterminada es [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. El modelo de datos de formulario **FDM_Create_First_IC** que creó anteriormente se muestra aquí. Selecciónela y pulse **Editar**.

   La fuente de datos seleccionada **MySQL** se muestra en el panel **Fuentes de datos**.

   ![Fuente de datos MYSQL para FDM](assets/mysql_fdm_new.png)

1. Expanda el árbol de fuentes de datos **MySQL**. Seleccione los siguientes objetos y servicios del modelo de datos del esquema **teleca**:

   * **Objetos** del modelo de datos:

      * letras
      * llamadas
      * cliente
   * **Servicios:**

      * get
      * actualizar

   Toque **Agregar seleccionado** para agregar objetos y servicios del modelo de datos seleccionado al modelo de datos de formulario.

   ![Seleccionar servicios de objetos del modelo de datos](assets/select_data_model_object_services_new.png)

   Los objetos de listas, llamadas y modelos de datos de cliente se muestran en el panel derecho de la pestaña **Model**. Los servicios get y update se muestran en la pestaña **Services**.

   ![Objetos del modelo de datos](assets/data_model_objects_new.png)

### Crear propiedades secundarias calculadas para el objeto del modelo de datos {#create-computed-child-properties-for-data-model-object}

Una propiedad calculada es aquella cuyo valor se calcula en función de una regla o una expresión. Con una regla, puede establecer el valor de una propiedad calculada en una cadena literal, un número, el resultado de una expresión matemática o el valor de otra propiedad en el modelo de datos del formulario.

En función del caso de uso, cree la propiedad **usagecharges** secundaria calculada en el objeto del modelo de datos **bill** utilizando la siguiente expresión matemática:

* tarifas de uso = gastos de llamada + gastos de llamada de conferencia + gastos de SMS + gastos de internet móvil + itinerancia nacional + itinerancia internacional + VAS (todas estas propiedades existen en el objeto del modelo de datos de facturas)
Para obtener más información sobre la propiedad **usagecharges** secundaria calculada, consulte [Plan the Interactive Communication](/help/forms/using/planning-interactive-communications.md).

Ejecute los siguientes pasos para crear propiedades secundarias calculadas para el objeto del modelo de datos de listas:

1. Seleccione la casilla de verificación situada en la parte superior del objeto del modelo de datos **bill** para seleccionarlo y pulse **Crear propiedad secundaria**.
1. En el panel **Crear propiedad secundaria**:

   1. Introduzca **usagecharges** como nombre de la propiedad secundaria.
   1. Habilite **Computed**.
   1. Seleccione **Float** como tipo y pulse **Listo** para agregar la propiedad secundaria al objeto del modelo de datos **bill**.

   ![Crear propiedad secundaria](assets/create_child_property_new.png)

1. Toque **Editar regla** para abrir el Editor de reglas.
1. Toque **Crear**. Se abre la ventana de regla **Set Value**.
1. En la lista desplegable Seleccionar opción , seleccione **Expresión matemática**.

   ![Editor de reglas de cargos de uso](assets/usage_charges_rule_editor_new.png)

1. En la expresión matemática, seleccione **callcharge** y **conficallcharge** como primer y segundo objeto, respectivamente. Seleccione **plus** como operador. Pulse dentro de la expresión matemática y pulse **Extend Expression** para agregar **smscharge**, **internetfees**, **itineringnational**, **roamingintnl** y **&lt;a11 1/> objetos de la expresión.**

   La siguiente imagen representa la expresión matemática en el editor de reglas:

   ![Regla de cargos de uso](assets/usage_charges_rule_all_new.png)

1. Puntee **Listo**. La regla se crea en el Editor de reglas.
1. Toque **Cerrar** para cerrar la ventana del Editor de reglas.

### Añadir asociaciones entre objetos del modelo de datos {#add-associations-between-data-model-objects}

Una vez definidos los objetos del modelo de datos, puede crear asociaciones entre ellos. La asociación puede ser de uno a uno o de uno a varios. Por ejemplo, puede haber varios dependientes asociados a un empleado. Se denomina asociación &quot;uno a varios&quot; y se representa mediante 1:n en la línea que conecta los objetos del modelo de datos asociados. Sin embargo, si una asociación devuelve un nombre de empleado único para un ID de empleado determinado, se denomina asociación uno a uno.

Cuando se agregan objetos del modelo de datos asociados en un origen de datos a un modelo de datos de formulario, sus asociaciones se retienen y se muestran como conectadas mediante líneas de flecha.

En función del caso de uso, cree las siguientes asociaciones entre los objetos del modelo de datos:

| Asociación | Objetos del modelo de datos |
|---|---|
| 1:n | cliente:llamadas (se pueden asociar varias llamadas a un cliente en una factura mensual) |
| 1:1 | cliente:facturas (una factura está asociada a un cliente para un mes en particular) |

Siga estos pasos para crear asociaciones entre objetos del modelo de datos:

1. Seleccione la casilla de verificación situada en la parte superior del objeto del modelo de datos **customer** para seleccionarlo y pulse **Agregar asociación**. Se abre el panel de propiedades **Agregar asociación**.
1. En el panel **Agregar asociación**:

   * Especifique un título para la asociación. Es un campo opcional.
   * Seleccione **One to Many** en la lista desplegable **Type**.

   * Seleccione **calls** en la lista desplegable **Model Object**.

   * Seleccione **get** en la lista desplegable **Service**.

   * Toque **Add** para vincular el objeto del modelo de datos **customer** al objeto del modelo de datos **calls** mediante una propiedad. En función del caso de uso, el objeto del modelo de datos de llamadas debe estar vinculado a la propiedad número móvil del objeto del modelo de datos del cliente. Se abre el cuadro de diálogo **Agregar argumento**.

   ![Agregar asociación](assets/add_association_new.png)

1. En el cuadro de diálogo **Agregar argumento**:

   * Seleccione **mobilenum** en la lista desplegable **Name**. La propiedad mobile number es una propiedad común que está disponible en el cliente y llama a los objetos del modelo de datos. Como resultado, se utiliza para crear una asociación entre el cliente y los objetos del modelo de datos de llamadas.
Para cada número móvil disponible en el objeto del modelo de datos del cliente, hay varios registros de llamada disponibles en la tabla de llamadas.

   * Especifique un título y una descripción opcionales para el argumento.
   * Seleccione **customer** en la lista desplegable **Enlace a**.

   * Seleccione **mobilenum** en la lista desplegable **Valor de enlace**.

   * Toque **Agregar**.

   ![Agregar asociación para un argumento](assets/add_association_argument_new.png)

   La propiedad mobilenum se muestra en la sección **Argumentos**.

   ![Agregar asociación de argumentos](assets/add_argument_association_new.png)

1. Toque **Listo** para crear una asociación 1:n entre los objetos del modelo de datos del cliente y las llamadas.

   Una vez que haya creado una asociación entre los objetos del modelo de datos de cliente y de llamadas, cree una asociación 1:1 entre los objetos del modelo de datos del cliente y de la factura.

1. Seleccione la casilla de verificación situada en la parte superior del objeto del modelo de datos **customer** para seleccionarlo y pulse **Agregar asociación**. Se abre el panel de propiedades **Agregar asociación**.
1. En el panel **Agregar asociación**:

   * Especifique un título para la asociación. Es un campo opcional.
   * Seleccione **One to One** en la lista desplegable **Type**.

   * Seleccione **bill** en la lista desplegable **Model Object**.

   * Seleccione **get** en la lista desplegable **Service**. La propiedad **billplan**, que es la clave principal de la tabla de facturas, ya está disponible en la sección **Argumentos**.
Los objetos de los modelos de facturas y datos del cliente se vinculan mediante las propiedades plan de facturación (facturas) y plan del cliente (cliente), respectivamente. Cree un enlace entre estas propiedades para recuperar los detalles del plan para cualquier cliente disponible en la base de datos MySQL.

   * Seleccione **customer** en la lista desplegable **Enlace a**.

   * Seleccione **customerplan** en la lista desplegable **Valor de enlace**.

   * Toque **Listo** para crear un enlace entre las propiedades del plan de facturación y del plan del cliente.

   ![Agregar asociación a la lista de clientes](assets/add_association_customer_bills_new.png)

   La siguiente imagen muestra las asociaciones entre los objetos del modelo de datos y las propiedades utilizadas para crear asociaciones entre ellos:

   ![fdm_groups](assets/fdm_associations.gif)

### Editar propiedades de objeto del modelo de datos {#edit-data-model-object-properties}

Después de crear asociaciones entre el cliente y otros objetos del modelo de datos, edite las propiedades del cliente para definir la propiedad en función de la cual se recuperan los datos del objeto del modelo de datos. En función del caso de uso, el número móvil se utiliza como propiedad para recuperar datos del objeto del modelo de datos del cliente.

1. Seleccione la casilla de verificación situada en la parte superior del objeto del modelo de datos **customer** para seleccionarlo y pulse **Editar propiedades**. Se abre el panel **Editar propiedades**.
1. Especifique **customer** como **Top Level Model object**.
1. Seleccione **get** en la lista desplegable **Read Service**.
1. En la sección **Argumentos**:

   * Seleccione **Solicitar atributo** en la lista desplegable **Enlace a**.

   * Especifique **mobilenum** como valor de enlace.

1. Seleccione **update** en la lista desplegable **Write** Service.
1. En la sección **Argumentos**:

   * Para la propiedad **mobilenum**, seleccione **customer** en la lista desplegable **Enlace a**.

   * Seleccione **mobilenum** en la lista desplegable **Valor de enlace**.

1. Toque **Listo** para guardar las propiedades.

   ![Configurar servicios](assets/configure_services_customer_new.png)

1. Seleccione la casilla de verificación situada en la parte superior del objeto del modelo de datos **calls** para seleccionarlo y pulse **Editar propiedades**. Se abre el panel **Editar propiedades**.
1. Deshabilite el objeto **Top Level Model** para el objeto del modelo de datos **calls**.
1. Puntee **Listo**.

   Repita los pasos 8 a 10 para configurar las propiedades del objeto del modelo de datos **bill**.

### Configurar servicios {#configure-services}

1. Vaya a la pestaña **Services**.
1. Seleccione el servicio **get** y pulse **Editar propiedades**. Se abre el panel **Editar propiedades**.
1. En el panel **Editar propiedades**:

   * Introduzca un título y una descripción opcionales.
   * Seleccione **customer** en la lista desplegable **Output Model Object**.

   * Toque **Listo** para guardar las propiedades.

   ![Editar propiedades](assets/edit_properties_get_details_new.png)

1. Seleccione el servicio **update** y pulse **Editar propiedades**. Se abre el panel **Editar propiedades**.
1. En el panel **Editar propiedades**:

   * Introduzca un título y una descripción opcionales.
   * Seleccione **customer** en la lista desplegable **Input Model Object**.

   * Puntee **Listo**.
   * Toque **Guardar** para guardar el modelo de datos del formulario.

   ![Actualizar propiedades del servicio](assets/update_service_properties_new.png)

## Paso 5: Probar el modelo y los servicios de datos de formulario {#step-test-form-data-model-and-services}

Puede probar el objeto y los servicios del modelo de datos para comprobar que el modelo de datos del formulario está configurado correctamente.

Haga lo siguiente para ejecutar la prueba:

1. Vaya a la pestaña **Model**, seleccione el objeto del modelo de datos **customer** y pulse **Test Model Object**.
1. En la ventana **Test Form Data Model**, seleccione **Read model object** en la lista desplegable **Select Model/Service**.
1. En la sección **Input**, especifique un valor para la propiedad **mobilenum** que existe en la base de datos MySQL configurada y pulse **Test**.

   Los detalles del cliente asociados con la propiedad mobilenum especificada se recuperan y se muestran en la sección Salida como se muestra a continuación. Cierre el cuadro de diálogo.

   ![Modelo de datos de prueba](assets/test_data_model_new.png)

1. Vaya a la pestaña **Services**.
1. Seleccione el servicio **get** y pulse **Test Service.**
1. En la sección **Input**, especifique un valor para la propiedad **mobilenum** que existe en la base de datos MySQL configurada y pulse **Test**.

   Los detalles del cliente asociados con la propiedad mobilenum especificada se recuperan y se muestran en la sección Salida como se muestra a continuación. Cierre el cuadro de diálogo.

   ![Servicio de prueba](assets/test_service_new.png)

### Editar y guardar datos de ejemplo {#edit-and-save-sample-data}

El editor del modelo de datos de formulario permite generar datos de ejemplo para todas las propiedades de objetos del modelo de datos, incluidas las propiedades calculadas, en un modelo de datos de formulario. Es un conjunto de valores aleatorios que cumplen con el tipo de datos configurado para cada propiedad. También puede editar y guardar datos, que se conservan incluso si se regeneran los datos de ejemplo.

Para generar, editar y guardar datos de ejemplo, haga lo siguiente:

1. En la página del modelo de datos de formulario, pulse **Editar datos de ejemplo**. Genera y muestra los datos de ejemplo en la ventana Editar datos de ejemplo .

   ![Editar datos de ejemplo](assets/edit_sample_data_new.png)

1. En la ventana **Editar datos de ejemplo** , edite los datos según sea necesario y pulse **Guardar**. Cierre la ventana.


