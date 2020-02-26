---
title: '"Tutorial: Crear modelo de datos de formulario "'
seo-title: Tutorial de creación de modelo de datos de formulario
description: Crear modelo de datos de formulario
seo-description: Crear modelo de datos de formulario
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
translation-type: tm+mt
source-git-commit: 70350add185b932ee604e190aabaf972ff994ba2

---


# Tutorial: Create form data model {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Este tutorial es un paso de la serie [Crear su primer formulario](../../forms/using/create-your-first-adaptive-form.md) adaptable. Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

## Acerca del tutorial {#about-the-tutorial}

El módulo de integración de datos de AEM Forms le permite crear un modelo de datos de formulario a partir de orígenes de datos de back-end dispares, como perfil de usuario de AEM, servicios web RESTful, servicios web basados en SOAP, servicios OData y bases de datos relacionales. Puede configurar objetos y servicios de modelo de datos en un modelo de datos de formulario y asociarlo a un formulario adaptable. Los campos de formulario adaptables están enlazados a las propiedades del objeto del modelo de datos. Los servicios permiten rellenar previamente el formulario adaptable y escribir los datos del formulario enviados en el objeto del modelo de datos.

Para obtener más información sobre la integración de datos de formularios y el modelo de datos de formularios, consulte Integración [de datos de formularios de](../../forms/using/data-integration.md)AEM.

Este tutorial lo acompaña a través de los pasos para preparar, crear, configurar y asociar un modelo de datos de formulario con un formulario adaptable. Al final de este tutorial, podrá:

* [Configurar la base de datos MySQL como fuente de datos](#config-database)
* [Crear un modelo de datos de formulario con la base de datos MySQL](#create-fdm)
* [Configurar modelo de datos de formulario](#config-fdm)
* [Probar modelo de datos de formulario](#test-fdm)

El modelo de datos de formulario tendrá un aspecto similar al siguiente:

![form-data-model_l](assets/form-data-model_l.png)

**********A. Fuentes de datos** B configuradas. Esquemas de fuentes de datos **C.** Servicios disponibles **D. Objetos del modelo de datos** E. Servicios configurados

## Requisitos previos {#prerequisites}

Antes de comenzar, asegúrese de que dispone de lo siguiente:

* Base de datos MySQL con datos de ejemplo como se indica en la sección Requisitos previos de [Crear el primer formulario adaptable](../../forms/using/create-your-first-adaptive-form.md)
* Paquete OSGi para el controlador JDBC MySQL como se explica en [Compilación del controlador de base de datos JDBC](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Formulario adaptable tal como se explica en el primer tutorial [Crear un formulario adaptable](/help/forms/using/create-adaptive-form.md)

## Paso 1: Configurar la base de datos MySQL como fuente de datos {#config-database}

Puede configurar distintos tipos de orígenes de datos para crear un modelo de datos de formulario. Para este tutorial, configuraremos la base de datos MySQL que configuró y llenó con datos de ejemplo. Para obtener información sobre otras fuentes de datos admitidas y cómo configurarlas, consulte Integración [de datos de formularios](../../forms/using/data-integration.md)AEM.

Haga lo siguiente para configurar su base de datos MySQL:

1. Instale el controlador JDBC para la base de datos MySQL como un paquete OSGi:

   1. Inicie sesión en la instancia de creación de AEM Forms como administrador y vaya a los paquetes de la consola web de AEM. La dirección URL predeterminada es [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Toque **Instalar/Actualizar**. Aparece el cuadro de diálogo **Cargar e instalar paquetes** .

   1. Toque **Elegir archivo** para buscar y seleccionar el paquete OSGi del controlador JDBC de MySQL. Seleccione **Iniciar paquete** y **Actualizar paquetes**, y toque **Instalar o Actualizar**. Asegúrese de que el controlador JDBC de Oracle Corporation para MySQL está activo. El controlador está instalado.

1. Configure la base de datos MySQL como una fuente de datos:

   1. Vaya a la consola web de AEM en [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Localice la configuración de **Apache Sling Connection Pooled DataSource** . Toque para abrir la configuración en modo de edición.
   1. En el cuadro de diálogo de configuración, especifique los siguientes detalles:

      * **** Nombre del origen de datos: Puede especificar cualquier nombre. Por ejemplo, especifique **WeRetailMySQL**.
      * **Nombre** de propiedad del servicio DataSource: Especifique el nombre de la propiedad de servicio que contiene el nombre de DataSource. Se especifica al registrar la instancia del origen de datos como servicio OSGi. Por ejemplo, **datasource.name**.
      * **Clase** de controlador JDBC: Especifique el nombre de clase Java del controlador JDBC. Para la base de datos MySQL, especifique **com.mysql.jdbc.Driver**.
      * **URI** de conexión JDBC: Especifique la dirección URL de conexión de la base de datos. Para la base de datos MySQL que se ejecuta en el puerto 3306 y el esquema weretail, la dirección URL es: `jdbc:mysql://[server]:3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **** Nombre de usuario: Nombre de usuario de la base de datos. Es necesario habilitar el controlador JDBC para establecer una conexión con la base de datos.
      * **** Contraseña: Contraseña de la base de datos. Es necesario habilitar el controlador JDBC para establecer una conexión con la base de datos.
      * **** Prueba a tomar prestado: Habilite la opción **Probar en préstamo** .
      * **** Prueba al regresar: Active la opción **Prueba al regresar** .
      * **** Consulta de validación: Especifique una consulta SQL SELECT para validar conexiones desde el grupo. La consulta debe devolver al menos una fila. Por ejemplo, **seleccione * en los detalles del cliente**.
      * **Aislamiento** de transacciones: Establezca el valor en **READ_COMMITTED**.
      Deje otras propiedades con [los valores](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) predeterminados y toque **Guardar**.
   Se crea una configuración similar a la siguiente.

   ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## Step 2: Create form data model {#create-fdm}

AEM Forms proporciona una interfaz de usuario intuitiva para [crear un](../../forms/using/data-integration.md#main-pars-header-1524967585)modelo de datos de formulario a partir de orígenes de datos configurados. Puede utilizar varios orígenes de datos en un modelo de datos de formulario. Para nuestro caso de uso, usaremos la fuente de datos MySQL configurada.

Para crear el modelo de datos de formulario, haga lo siguiente:

1. En la instancia de creación de AEM, vaya a **Formularios** > Integraciones **de datos**.
1. Tap **Create** > **Form Data Model**.
1. En el cuadro de diálogo Crear modelo de datos de formulario, especifique un **nombre** para el modelo de datos de formulario. Por ejemplo, **cliente-envío-facturación-detalles**. Puntee **Siguiente**.
1. La pantalla Seleccionar fuente de datos muestra todas las fuentes de datos configuradas. Seleccione la fuente de datos **WeRetailMySQL** y toque **Crear**.

   ![selección de fuente de datos](assets/data-source-selection.png)

Se crea el modelo de datos de formulario **cliente-envío-facturación-detalles** .

## Paso 3: Configurar modelo de datos de formulario {#config-fdm}

La configuración del modelo de datos de formulario implica:

* adición de objetos y servicios del modelo de datos
* configuración de servicios de lectura y escritura para objetos del modelo de datos

Para configurar el modelo de datos de formulario, haga lo siguiente:

1. En la instancia de creación de AEM, vaya a **Formularios** > Integraciones **de datos**. La dirección URL predeterminada es [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. El modelo de datos de formulario **cliente-envío-facturación-detalles** que ha creado anteriormente se muestra aquí. Ábralo en modo de edición.

   El origen de datos seleccionado **WeRetailMySQL** está configurado en el modelo de datos de formulario.

   ![default-fdm](assets/default-fdm.png)

1. Expanda el árbol de origen de datos WeRailMySQL. Seleccione los siguientes objetos y servicios del modelo de datos desde **weretail** > esquema de detalles del **cliente** al modelo de datos de formulario:

   * **Objetos** del modelo de datos:

      * id
      * name
      * ShippingAddress
      * ciudad
      * estado
      * zipcode
   * **Servicios:**

      * get
      * actualizar
   Toque **Agregar selección** para agregar objetos y servicios del modelo de datos seleccionado al modelo de datos de formulario.

   ![Esquema de WeRetail](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >Los servicios predeterminados de obtención, actualización e inserción de orígenes de datos JDBC se proporcionan de forma predeterminada con el modelo de datos de formulario.

1. Configure los servicios de lectura y escritura para el objeto del modelo de datos.

   1. Seleccione el objeto del modelo de datos **custom** details y toque **Editar propiedades**.
   1. Seleccione **Obtener** en la lista desplegable Servicio de lectura. El argumento **id** , que es la clave principal en el objeto del modelo de datos customDetails, se agrega automáticamente. Toque ![aem_6_3_edit](assets/aem_6_3_edit.png) y configure el argumento como se indica a continuación.

      ![read-default](assets/read-default.png)

   1. Del mismo modo, seleccione **actualizar** como servicio de escritura. El objeto **customerdetails** se agrega automáticamente como argumento. El argumento se configura de la siguiente manera.

      ![write-default](assets/write-default.png)

      Agregue y configure el argumento **id** de la siguiente manera.

      ![id-arg](assets/id-arg.png)

   1. Toque **Listo** para guardar las propiedades del objeto del modelo de datos. A continuación, toque **Guardar** para guardar el modelo de datos de formulario.

      Los servicios **get** y **update** se agregan como servicios predeterminados para el objeto del modelo de datos.

      ![data-model-object](assets/data-model-object.png)

1. Vaya a la ficha **Servicios** y configure **get** and **update** services.

   1. Seleccione el servicio **get** y toque **Editar propiedades**. Se abre el cuadro de diálogo de propiedades.
   1. Especifique lo siguiente en el cuadro de diálogo Editar propiedades:

      * **Título**: Especifique el título del servicio. Por ejemplo: Recuperar dirección de envío.
      * **Descripción**: Especifique una descripción que contenga el funcionamiento detallado del servicio. Por ejemplo:

         Este servicio recupera la dirección de envío y otros detalles del cliente de la base de datos MySQL

      * **Objeto** de modelo de salida: Seleccione el esquema que contiene los datos del cliente. Por ejemplo:

         esquema de detalles del cliente

      * **Matriz** de retorno: Desactive la opción **Volver matriz** .
      * **Argumentos**: Seleccione un argumento llamado **ID**.
      Puntee **Listo**. Servicio para recuperar los detalles del cliente de la base de datos MySQL está configurado.

      ![cambio de dirección-recuperación](assets/shiiping-address-retrieval.png)

   1. Seleccione el servicio de **actualización** y toque **Editar propiedades**. Se abre el cuadro de diálogo de propiedades.

   1. Especifique lo siguiente en el cuadro de diálogo Editar propiedades:

      * **Título**: Especifique el título del servicio. Por ejemplo, Actualizar dirección de envío.
      * **Descripción**: Especifique una descripción que contenga el funcionamiento detallado del servicio. Por ejemplo:

         Este servicio actualiza la dirección de envío y los campos relacionados en la base de datos MySQL

      * **Objeto** de modelo de entrada: Seleccione el esquema que contiene los datos del cliente. Por ejemplo:

         esquema de detalles del cliente

      * **Tipo** de salida: Seleccione **BOOLEAN**.

      * **Argumentos**: Seleccione un argumento denominado **ID** y detalles del **cliente**.
      Puntee **Listo**. Se ha configurado el servicio de **actualización** para actualizar los detalles del cliente en la base de datos de MySQL.

      ![shiiping-address-update](assets/shiiping-address-update.png)



Se configuran el objeto y los servicios del modelo de datos del formulario. Ahora puede probar el modelo de datos de formulario.

## Step 4: Test form data model {#test-fdm}

Puede probar el objeto y los servicios del modelo de datos para comprobar que el modelo de datos de formulario está configurado correctamente.

Para ejecutar la prueba, haga lo siguiente:

1. Vaya a la ficha **Modelo** , seleccione el objeto del modelo de datos detalles del **cliente** y toque Objeto **del modelo de prueba**.
1. En la ventana **Modelo de prueba/Servicio** , seleccione **Leer objeto** de modelo en la lista desplegable **Seleccionar modelo/servicio** .
1. En la sección **customerdetails** , especifique un valor para el argumento **id** que existe en la base de datos MySQL configurada y toque **Test**.

   Los detalles del cliente asociados con la ID especificada se recuperan y se muestran en la sección **Salida** como se muestra a continuación.

   ![test-read-model](assets/test-read-model.png)

1. Del mismo modo, puede probar el objeto y los servicios del modelo de escritura.

   En el siguiente ejemplo, el servicio de actualización actualiza correctamente los detalles de dirección del identificador 7102715 de la base de datos.

   ![test-write-model](assets/test-write-model.png)

   Ahora, si vuelve a probar el servicio de modelo de lectura para la identificación 7107215, recuperará y mostrará los detalles actualizados del cliente como se muestra a continuación.

   ![leído-actualizado](assets/read-updated.png)
