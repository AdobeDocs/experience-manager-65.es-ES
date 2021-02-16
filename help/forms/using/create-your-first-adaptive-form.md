---
title: '"Tutorial: Crear el primer formulario adaptable"'
seo-title: '"Tutorial: Crear el primer formulario adaptable"'
description: Aprenda a crear formularios interactivos, interactivos y adaptables de clase empresarial.
seo-description: Aprenda a crear formularios interactivos, interactivos y adaptables de clase empresarial.
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
translation-type: tm+mt
source-git-commit: 43c04a8b2f1e2e7f2067cec055d8737dfc7b3e84
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---


# Tutorial: Cree su primer formulario adaptable {#tutorial-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## Introducción {#introduction}

¿Busca una **experiencia de formularios** fácil de usar para dispositivos móviles que simplifique la inscripción, aumente la participación y reduzca el tiempo de respuesta, **los formularios adaptables** es una opción perfecta para usted. Los formularios adaptables proporcionan una experiencia de formularios móvil, de automatización y analítica. Puede crear fácilmente formularios que sean interactivos e interactivos, utilizar procesos automatizados para reducir las tareas administrativas y repetitivas y utilizar el análisis de datos para mejorar y personalizar la experiencia que los clientes tienen con los formularios.

Este tutorial proporciona un marco integral para crear un formulario adaptable. El tutorial está organizado en un caso de uso y en varias guías. Cada guía ayuda a conocer y agregar nuevas funciones al formulario adaptable que se crea en este tutorial. Tiene un formulario adaptable que funciona después de cada guía. La guía para crear un formulario adaptable está disponible. Las guías posteriores estarán disponibles pronto. Al final de este tutorial, podrá:

* Cree un formulario adaptable y un modelo de datos de formulario.
* Defina el estilo del formulario adaptable.
* Utilice el editor de reglas de formulario adaptable para crear reglas comerciales.
* Pruebe y publique un formulario adaptable.

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

El recorrido inicio con el aprendizaje del caso de uso:

Un sitio web oferta una gama de productos para diversos clientes. Los clientes exploran el portal, seleccionan y solicitan los productos. Cada cliente crea una cuenta y proporciona direcciones de envío y facturación. Una cliente existente, Sara Rose, está buscando agregar su dirección de envío al sitio web. El sitio web proporciona un formulario en línea para agregar y actualizar las direcciones de envío.

El sitio web se ejecuta en Adobe Experience Manager (AEM) y utiliza AEM [!DNL Forms] para capturar y procesar datos. El formulario de adición y actualización de direcciones es un formulario adaptable. El sitio web almacena los detalles del cliente en una base de datos. Utilizan el formulario de adición y actualización de direcciones para recuperar y mostrar las direcciones disponibles. También utilizan el formulario adaptable para aceptar direcciones nuevas y actualizadas.

### Requisitos previos {#prerequisite}

* Configure una instancia de autor AEM.
* Instale [AEM Forms Add-on](../../forms/using/installing-configuring-aem-forms-osgi.md) en la instancia de creación.
* Obtenga el controlador de base de datos JDBC (archivo JAR) del proveedor de base de datos. Los ejemplos del tutorial se basan en la base de datos [!DNL MySQL] y utilizan [!DNL Oracle's] [controlador de base de datos JDBC MySQL](https://dev.mysql.com/downloads/connector/j/5.1.html).

* Configure una base de datos que contenga datos de clientes con los campos que se muestran a continuación. Una base de datos no es esencial para crear un formulario adaptable. Este tutorial utiliza una base de datos para mostrar el modelo de datos de formulario y las capacidades de persistencia de AEM [!DNL Forms].

![adaptiveformdata](assets/adaptiveformdata.png)

## Paso 1: Crear un formulario adaptable {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Los formularios adaptables son de nueva generación, atractivos, interactivos, dinámicos y adaptables. Mediante formularios adaptables, puede ofrecer experiencias personalizadas y con objetivos definidos. AEM [!DNL Forms] proporciona un editor WYSIWYG de arrastrar y soltar para crear formularios adaptables. Para obtener más información sobre los formularios adaptables, consulte [Introducción a la creación de formularios adaptables](../../forms/using/introduction-forms-authoring.md).

Objetivos:

* Crear un formulario adaptable que permita al cliente agregar una dirección de envío
* Campos de diseño de un formulario adaptable para mostrar y aceptar información de un cliente
* Crear una acción de envío para enviar un correo electrónico con contenido de formulario
* Previsualización y envío de un formulario adaptable

[![Consulte la Guía](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## Paso 2: Crear modelo de datos de formulario {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Un modelo de datos de formulario permite conectar un formulario adaptable a orígenes de datos dispares. Por ejemplo, AEM perfil del usuario, servicios web RESTful, servicios web basados en SOAP, servicios OData y bases de datos relacionales. Un modelo de datos de formulario es un esquema de representación de datos unificado de las entidades comerciales y los servicios disponibles en las fuentes de datos conectadas. Puede utilizar el modelo de datos de formulario con un formulario adaptable para recuperar, actualizar, eliminar y agregar datos a orígenes de datos conectados.

Objetivos:

* Configure la instancia de base de datos del sitio web ([!DNL MySQL] base de datos) como fuentes de datos
* Crear el modelo de datos de formulario utilizando la base de datos [!DNL MySQL] como origen de datos
* Añadir objetos del modelo de datos en el modelo de datos de formulario
* Configuración de servicios de lectura y escritura para el modelo de datos de formulario
* Probar el modelo de datos de formulario y los servicios configurados con datos de prueba

[![Consulte la Guía](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## Paso 3: Aplicar reglas a campos de formulario adaptables {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Los formularios adaptables proporcionan un editor para escribir reglas en objetos de formulario adaptables. Estas reglas definen acciones para el déclencheur de objetos de formulario en función de condiciones preestablecidas, entradas del usuario y acciones del usuario en el formulario. Ayuda a garantizar la precisión y acelera la experiencia de cumplimentación de formularios.

Objetivos:

* Creación y aplicación de reglas a campos de formulario adaptables
* Usar reglas para déclencheur de servicios de modelos de datos de formularios para actualizar datos a la base de datos

[![Consulte la Guía](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## Paso 4: Defina el estilo del formulario adaptable {#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

Los formularios adaptables proporcionan temáticas y un [editor](../../forms/using/themes.md) para crear temáticas para los formularios adaptables. Un tema contiene detalles de estilo para componentes y paneles, y puede reutilizar un tema en diferentes formularios. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar el tema al formulario, el estilo especificado se refleja en los componentes correspondientes del formulario. Los formularios adaptables también admiten estilos en línea para estilos específicos de un formulario.

Objetivos:

* Aplicar un tema predefinido a un formulario adaptable
* Creación de un tema para un formulario adaptable mediante el editor de temas
* Uso de fuentes web en un tema personalizado

[![Consulte la Guía](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## Paso 5: Probar el formulario adaptable {#step-test-your-adaptive-form}

![11-test-your-adaptive-form](assets/11-test-your-adaptive-form.png)

Los formularios adaptables son esenciales para las interacciones con los clientes. Es importante probar los formularios adaptables con cada cambio que realice en ellos. Probar cada campo de un formulario es tedioso. AEM [!DNL Forms] proporciona un SDK (Calvin SDK) para automatizar la prueba de formularios adaptables. Calvin le permite automatizar la prueba de sus formularios adaptables en el navegador web.

Objetivos:

* Crear grupo de pruebas para el formulario adaptable
* Creación de casos de prueba para formularios adaptables
* Ejecutar los casos de prueba

[![Consulte la Guía](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](testing-your-adaptive-form.md)

## Paso 6: Publicar el formulario adaptable {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

Puede publicar formularios adaptables como un formulario independiente (aplicación de una sola página), incluir en AEM [Página de sitios](/help/forms/using/embed-adaptive-form-aem-sites.md) o lista en un AEM [!DNL Site] mediante [Forms Portal](../../forms/using/introduction-publishing-forms.md).

Objetivos:

* Publicar el formulario adaptable como una página AEM
* Incrustar el formulario adaptable en una página AEM [!DNL Sites]
* Incrustar el formulario adaptable en una página web externa (una página web no AEM alojada fuera de AEM)

[![Consulte la Guía](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)