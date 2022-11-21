---
title: "Tutorial: Crear modelo de datos de formulario "
seo-title: Create Form Data Model Tutorial
description: Crear modelo de datos de formulario
seo-description: Create form data model
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: c3178eefb5aca3afea2f3df8381b52461247d6f3
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 2%

---

# Tutorial: Crear modelo de datos de formulario {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Este tutorial es un paso en la [Crear el primer formulario adaptable](../../forms/using/create-your-first-adaptive-form.md) serie. Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

## Acerca del tutorial {#about-the-tutorial}

AEM [!DNL Forms] el módulo de integración de datos le permite crear un modelo de datos de formulario a partir de fuentes de datos backend dispares, como AEM perfil de usuario, servicios web RESTful, servicios web basados en SOAP, servicios OData y bases de datos relacionales. Puede configurar objetos y servicios del modelo de datos en un modelo de datos de formulario y asociarlo a un formulario adaptable. Los campos de formulario adaptables están enlazados a las propiedades de objeto del modelo de datos. Los servicios permiten rellenar previamente el formulario adaptable y escribir los datos de formulario enviados en el objeto del modelo de datos.

Para obtener más información sobre la integración de datos de formulario y el modelo de datos de formulario, consulte [Integración de datos de AEM Forms](../../forms/using/data-integration.md).

Este tutorial lo acompaña durante los pasos para preparar, crear, configurar y asociar un modelo de datos de formulario con un formulario adaptable. Al final de este tutorial, podrá:

* [Configurar la base de datos MySQL como fuente de datos](#config-database)
* [Creación de un modelo de datos de formulario mediante la base de datos MySQL](#create-fdm)
* [Configuración del modelo de datos de formulario](#config-fdm)
* [Probar modelo de datos de formulario](#test-fdm)

El modelo de datos de formulario tendrá un aspecto similar al siguiente:

![form-data-model_l](assets/form-data-model_l.png)

**A.** Fuentes de datos configuradas **B.** Esquemas de fuentes de datos **C.** Servicios disponibles **D.** Objetos del modelo de datos **E.** Servicios configurados

## Requisitos previos {#prerequisites}

Antes de empezar, asegúrese de que dispone de lo siguiente:

* [!DNL MySQL] base de datos con datos de ejemplo como se indica en la sección Requisitos previos de [Cree su primer formulario adaptable](../../forms/using/create-your-first-adaptive-form.md)
* Paquete OSGi para [!DNL MySQL] Controlador JDBC tal como se explica en [Agrupación del controlador de base de datos JDBC](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Formulario adaptable, tal como se explica en el primer tutorial [Creación de un formulario adaptable](/help/forms/using/create-adaptive-form.md)

## Paso 1: Configurar la base de datos MySQL como fuente de datos {#config-database}

Puede configurar distintos tipos de orígenes de datos para crear un modelo de datos de formulario. Para este tutorial, configuraremos la base de datos MySQL que ha configurado y rellenado con datos de ejemplo. Para obtener información sobre otras fuentes de datos compatibles y cómo configurarlas, consulte [Integración de datos de AEM Forms](../../forms/using/data-integration.md).

Haga lo siguiente para configurar su [!DNL MySQL] base de datos:

1. Instale el controlador JDBC para [!DNL MySQL] base de datos como paquete OSGi:

   1. Descargar [[!DNL MySQL] Paquete OSGi del controlador JDBC](http://www.java2s.com/ref/jar/download-orgosgiservicejdbc100jar-file.html).
   1. Iniciar sesión en AEM [!DNL Forms] Instancia de autor como administrador y vaya a AEM paquetes de consola web. La dirección URL predeterminada es [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Toque **[!UICONTROL Instalar/actualizar]**. Un [!UICONTROL Cargar e instalar paquetes] se abre.

   1. Toque **[!UICONTROL Elegir archivo]** para buscar y seleccionar la variable [!DNL MySQL] Paquete OSGi del controlador JDBC. Select **[!UICONTROL Iniciar paquete]** y **[!UICONTROL Actualizar paquetes]** y toque **[!UICONTROL Instalar o actualizar]**. Asegúrese de que la variable [!DNL Oracle Corporation's] Controlador JDBC para [!DNL MySQL] está activa. El controlador está instalado.

1. Configurar [!DNL MySQL] base de datos como fuente de datos:

   1. Vaya a AEM consola web en [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Localizar **Fuente de datos obtenida de una conexión Apache Sling** configuración. Pulse para abrir la configuración en modo de edición.
   1. En el cuadro de diálogo de configuración, especifique los siguientes detalles:

      * **Nombre del origen de datos:** Puede especificar cualquier nombre. Por ejemplo, especifique **WeRetailMySQL**.
      * **Nombre de propiedad del servicio DataSource**: Especifique el nombre de la propiedad de servicio que contiene el nombre de DataSource. Se especifica al registrar la instancia de origen de datos como servicio OSGi. Por ejemplo, **datasource.name**.
      * **Clase de controlador JDBC**: Especifique el nombre de clase Java del controlador JDBC. Para [!DNL MySQL] base de datos, especificar **com.mysql.jdbc.Driver**.
      * **URI de conexión JDBC**: Especifique la dirección URL de conexión de la base de datos. Para [!DNL MySQL] base de datos que se ejecuta en el puerto 3306 y esquema weretail, la URL es: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`

      >[!NOTE]
      >
      > Cuando la variable [!DNL MySQL] la base de datos está detrás de un servidor de seguridad y el nombre de host de la base de datos no es un DNS público. La dirección IP de la base de datos debe agregarse en la */etc/hosts* del equipo host AEM.

      * **Nombre de usuario:** Nombre de usuario de la base de datos. Es necesario permitir que el controlador JDBC establezca una conexión con la base de datos.
      * **Contraseña:** Contraseña de la base de datos. Es necesario permitir que el controlador JDBC establezca una conexión con la base de datos.

      >[!NOTE]
      >
      >AEM Forms no admite la autenticación NT para [!DNL MySQL]. Vaya a AEM consola web en [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) y busque &quot;Fuente de datos agrupada de la conexión Apache Sling&quot;.Para &quot;URI de conexión JDBC&quot; valor de la propiedad &quot;integrationSecurity&quot; como False y utilice el nombre de usuario y la contraseña creados para conectarse con [!DNL MySQL] base de datos.

      * **Pruebas con prestatario:** Active la variable **[!UICONTROL Prueba a la vista previa]** .
      * **Prueba tras retorno:** Active la variable **[!UICONTROL Prueba a la vuelta]** .
      * **Consulta de validación:** Especifique una consulta SQL SELECT para validar conexiones desde el grupo. La consulta debe devolver al menos una fila. Por ejemplo, **select &#42; de detalles del cliente**.
      * **Aislamiento de transacciones**: Establezca el valor en **READ_COMMITTED**.

         Deje otras propiedades con el valor predeterminado [values](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) y toque **[!UICONTROL Guardar]**.

         Se crea una configuración similar a la siguiente.

         ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)



## Paso 2: Crear modelo de datos de formulario {#create-fdm}

AEM [!DNL Forms] proporciona una interfaz de usuario intuitiva para [crear un modelo de datos de formulario](data-integration.md) desde fuentes de datos configuradas. Puede utilizar varios orígenes de datos en un modelo de datos de formulario. Para nuestro caso de uso, utilizaremos la configuración [!DNL MySQL] fuente de datos.

Para crear el modelo de datos de formulario, haga lo siguiente:

1. En AEM instancia de autor, vaya a **[!UICONTROL Forms]** > **[!UICONTROL Integraciones de datos]**.
1. Toque **[!UICONTROL Crear]** > **[!UICONTROL Modelo de datos de formulario]**.
1. En el cuadro de diálogo Crear modelo de datos de formulario , especifique un **name** para el modelo de datos de formulario. Por ejemplo, **customer-Shipping-billing-details**. Pulse **[!UICONTROL Siguiente]**.
1. La pantalla seleccionar fuente de datos enumera todas las fuentes de datos configuradas. Select **WeRetailMySQL** fuente de datos y toque **[!UICONTROL Crear]**.

   ![selección de fuente de datos](assets/data-source-selection.png)

La variable **customer-Shipping-billing-details** se crea el modelo de datos de formulario.

## Paso 3: Configuración del modelo de datos de formulario {#config-fdm}

La configuración del modelo de datos de formulario implica:

* adición de objetos y servicios del modelo de datos
* configuración de servicios de lectura y escritura para objetos del modelo de datos

Para configurar el modelo de datos de formulario, haga lo siguiente:

1. En AEM instancia de autor, vaya a **[!UICONTROL Forms]** > **[!UICONTROL Integraciones de datos]**. La dirección URL predeterminada es [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. La variable **customer-Shipping-billing-details** el modelo de datos de formulario creado anteriormente se muestra aquí. Ábrala en modo de edición.

   La fuente de datos seleccionada **WeRetailMySQL** se configura en el modelo de datos de formulario.

   ![default-fdm](assets/default-fdm.png)

1. Expanda el árbol de fuentes de datos WeRailMySQL. Seleccione los siguientes objetos y servicios del modelo de datos **weretail** > **detalles del cliente** esquema para el modelo de datos de formulario:

   * **Objetos del modelo de datos**:

      * id
      * name
      * ShippingAddress
      * ciudad
      * estado
      * código postal
   * **Servicios:**

      * get
      * actualizar

   Toque **Agregar selección** para agregar objetos y servicios del modelo de datos seleccionado al modelo de datos de formulario.

   ![Esquema de WeRetail](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >Los servicios predeterminados de obtener, actualizar e insertar para orígenes de datos JDBC se proporcionan ya preparados con el modelo de datos de formulario .

1. Configure los servicios de lectura y escritura para el objeto del modelo de datos.

   1. Seleccione el **detalles del cliente** objeto del modelo de datos y toque **[!UICONTROL Editar propiedades]**.
   1. Select **[!UICONTROL get]** en la lista desplegable Servicio de lectura . La variable **id** , que es la clave principal del objeto del modelo de datos customerdetails, se agrega automáticamente. Toque ![aem_6_3_edit](assets/aem_6_3_edit.png) y configure el argumento como se indica a continuación.

      ![read-default](assets/read-default.png)

   1. Del mismo modo, seleccione **[!UICONTROL actualizar]** como servicio de escritura. La variable **detalles del cliente** se agrega automáticamente como argumento. El argumento se configura de la siguiente manera.

      ![write-default](assets/write-default.png)

      Agregue y configure la variable **id** como se indica a continuación.

      ![id-arg](assets/id-arg.png)

   1. Toque **[!UICONTROL Listo]** para guardar las propiedades del objeto del modelo de datos. A continuación, toque **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario.

      La variable **[!UICONTROL get]** y **[!UICONTROL actualizar]** los servicios se añaden como servicios predeterminados para el objeto del modelo de datos.

      ![data-model-object](assets/data-model-object.png)

1. Vaya a la **[!UICONTROL Servicios]** y configurar **[!UICONTROL get]** y **[!UICONTROL actualizar]** servicios.

   1. Seleccione el **[!UICONTROL get]** servicio y toque **[!UICONTROL Editar propiedades]**. Se abre el cuadro de diálogo de propiedades.
   1. Especifique lo siguiente en el cuadro de diálogo Editar propiedades:

      * **Título**: Especifique el título del servicio. Por ejemplo: Recupere la dirección de envío.
      * **Descripción**: Especifique la descripción que contiene el funcionamiento detallado del servicio. Por ejemplo:

         Este servicio recupera la dirección de envío y otros detalles del cliente de [!DNL MySQL] base de datos

      * **Objeto de modelo de salida**: Seleccione el esquema que contiene los datos del cliente. Por ejemplo:

         customerdetail schema

      * **Devolver matriz**: Desactive el **Devolver matriz** .
      * **Argumentos**: Seleccionar argumento llamado **ID**.

      Pulse **[!UICONTROL Listo]**. El servicio para recuperar los detalles del cliente de la base de datos MySQL está configurado.

      ![shiiping-address-retrieve](assets/shiiping-address-retrieval.png)

   1. Seleccione el **[!UICONTROL actualizar]** servicio y toque **[!UICONTROL Editar propiedades]**. Se abre el cuadro de diálogo de propiedades.

   1. Especifique lo siguiente en la [!UICONTROL Editar propiedades] diálogo:

      * **Título**: Especifique el título del servicio. Por ejemplo, Actualizar dirección de envío.
      * **Descripción**: Especifique la descripción que contiene el funcionamiento detallado del servicio. Por ejemplo:

         Este servicio actualiza la dirección de envío y los campos relacionados en la base de datos MySQL

      * **Objeto de modelo de entrada**: Seleccione el esquema que contiene los datos del cliente. Por ejemplo:

         customerdetail schema

      * **Tipo de salida**: Select **BOOLEANO**.

      * **Argumentos**: Seleccionar argumento llamado **ID** y **detalles del cliente**.
      Pulse **[!UICONTROL Listo]**. La variable **[!UICONTROL actualizar]** para actualizar los detalles del cliente en el [!DNL MySQL] base de datos configurada.

      ![shiiping-address-update](assets/shiiping-address-update.png)



Se configuran el objeto y los servicios del modelo de datos de formulario. Ahora puede probar el modelo de datos de formulario.

## Paso 4: Probar modelo de datos de formulario {#test-fdm}

Puede probar el objeto y los servicios del modelo de datos para comprobar que el modelo de datos del formulario está configurado correctamente.

Haga lo siguiente para ejecutar la prueba:

1. Vaya a la **[!UICONTROL Modelo]** , seleccione **detalles del cliente** objeto del modelo de datos y toque **[!UICONTROL Objeto de modelo de prueba]**.
1. En el [!UICONTROL Modelo/servicio de prueba] ventana, seleccione **[!UICONTROL Objeto de modelo de lectura]** de la variable **[!UICONTROL Seleccionar modelo/servicio]** lista desplegable.
1. En el **detalles del cliente** , especifique un valor para **id** argumento que existe en la configuración [!DNL MySQL] pulsar y definir base de datos **[!UICONTROL Prueba]**.

   Los detalles del cliente asociados con la ID especificada se recuperan y se muestran en la variable **[!UICONTROL Salida]** como se muestra a continuación.

   ![modelo test-read](assets/test-read-model.png)

1. Del mismo modo, puede probar el objeto y los servicios del modelo de escritura.

   En el siguiente ejemplo, el servicio de actualización actualiza correctamente los detalles de dirección del id 7102715 de la base de datos.

   ![test-write-model](assets/test-write-model.png)

   Ahora, si vuelve a probar el servicio de modelo de lectura para el id 7107215, recuperará y mostrará los detalles actualizados del cliente como se muestra a continuación.

   ![leído y actualizado](assets/read-updated.png)
