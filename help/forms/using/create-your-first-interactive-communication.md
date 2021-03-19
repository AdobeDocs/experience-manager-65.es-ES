---
title: 'Tutorial: Cree su primera comunicación interactiva'
seo-title: Cree su primera comunicación interactiva
description: Aprenda a crear su primera comunicación interactiva.
seo-description: Aprenda a crear su primera comunicación interactiva.
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
feature: Comunicación interactiva
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---


# Tutorial: Cree su primera comunicación interactiva {#tutorial-create-your-first-interactive-communication}

Aprenda a crear su primera comunicación interactiva.

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

Interactive Communications centraliza y administra la creación, el ensamblaje y la entrega de correspondencia segura, personalizada e interactiva, como correspondencia comercial, documentos, declaraciones, correos de marketing, facturas y kits de bienvenida. Interactive Communications puede entregarse mediante dos canales: Imprimir y Web. El canal Imprimir se utiliza para crear archivos PDF y comunicaciones en papel, mientras que el canal web se utiliza para ofrecer experiencias en línea.

Este tutorial proporciona un marco de trabajo completo para crear una comunicación interactiva. El tutorial está organizado en un caso de uso y en varias guías. Cada guía le ayuda a crear funciones que se utilizan como componentes básicos para crear una comunicación interactiva.

La siguiente imagen ilustra los componentes básicos necesarios para crear una comunicación interactiva.

![flujo de trabajo](assets/workflow.gif)

Al final de este tutorial, podrá:

* Crear bloques de creación (modelo de datos de formulario, fragmentos de documento y plantillas)
* Crear una comunicación interactiva
* Probar y publicar una comunicación interactiva

## Caso de uso {#use-case}

El recorrido comienza con el aprendizaje del caso de uso:

Un operador de telecomunicaciones envía facturas mensuales a los clientes por correo electrónico. El proyecto de ley es una comunicación interactiva. El correo electrónico incluye:

* Un PDF protegido mediante contraseña, denominado canal de impresión en este tutorial. Incluye detalles de clientes, detalles de facturas, resumen de cargos, modos prácticos de pagar la factura y detalles de uso.
* Un vínculo a la versión web de la lista, denominada canal web en este tutorial. La versión web de la ley, además de los detalles cubiertos en la versión PDF, proporciona una representación gráfica de los detalles de uso y las ofertas personalizadas basadas en Adobe Target. La versión web también contiene un formulario de pago en línea. Ayuda a realizar pagos en línea sin salir del IC.
* Un vínculo a servicios de valor agregado, como almacenamiento en línea, suscripciones de música y suscripciones de vídeo bajo demanda.

## Requisitos previos {#prerequisites}

* Configure una instancia de autor AEM.
* Instalar el [complemento de AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) en la instancia de autor
* Configuración de la base de datos MYSQL
* Obtenga el controlador de base de datos JDBC (archivo JAR) del proveedor de la base de datos. Algunos ejemplos del tutorial se basan en la base de datos MySQL y utilizan el [controlador de base de datos JDBC de MySQL](https://dev.mysql.com/downloads/connector/j/5.1.html) del Oracle.

## Paso 1: Planifique la comunicación interactiva {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

El primer paso en la planificación de una comunicación interactiva es finalizar el contenido de la comunicación interactiva. Una vez finalizado el contenido, debe analizarlo para identificar los distintos tipos de recursos necesarios para crear la comunicación interactiva.

**Objetivos:**

Para crear una anatomía para la comunicación interactiva con los siguientes modos de entrada de datos:

* Texto estático
* Modelo de datos de formulario
* IU del agente
* Datos condicionales
* Imágenes

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/planning-interactive-communications.md)

## Paso 2: Crear modelo de datos de formulario {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Un modelo de datos de formulario le permite conectar una comunicación interactiva a distintos orígenes de datos. Por ejemplo, AEM perfil de usuario, servicios web RESTful, servicios web basados en SOAP, servicios OData y bases de datos relacionales. Un modelo de datos de formulario es un esquema de representación de datos unificado de entidades y servicios empresariales disponibles en fuentes de datos conectadas. Puede utilizar el modelo de datos de formulario con una comunicación interactiva para recuperar datos de orígenes de datos conectados. Para obtener más información sobre el modelo de datos de formulario, consulte [AEM Forms Data Integration](/help/forms/using/data-integration.md).

**Objetivos:**

* Configurar la instancia de base de datos (base de datos MySQL) como fuente de datos
* Crear el modelo de datos de formulario utilizando la base de datos MySQL como origen de datos
* Agregar objetos del modelo de datos al modelo de datos de formulario
* Configuración de servicios de lectura y escritura para el modelo de datos de formulario
* Crear asociaciones entre los objetos del modelo de datos
* Ver datos de ejemplo generados automáticamente
* Editar datos de ejemplo
* Probar el modelo de datos de formulario y los servicios configurados con datos de prueba

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-form-data-model0.md)

## Paso 3: Crear fragmentos de documento {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Los fragmentos de documento son componentes reutilizables de una correspondencia que se utilizan para componer una comunicación interactiva. Los fragmentos del documento son de tipo: Texto, Lista y Condición.

**Objetivos:**

* Crear fragmentos de documento
* Crear variables
* Crear y aplicar reglas

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-document-fragments.md)

## Paso 4: Crear plantillas {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Para crear una comunicación interactiva, debe tener plantillas disponibles en el servidor de AEM para los canales web e impresos.

Las plantillas del canal Imprimir se crean en Adobe Forms Designer y se cargan en el servidor de AEM. Estas plantillas están disponibles para su uso durante la creación de una comunicación interactiva.

Las plantillas del canal web se crean en AEM. Los autores y administradores de plantillas pueden crear, editar y habilitar plantillas web. Una vez creadas y habilitadas, estas plantillas están disponibles para su uso durante la creación de una comunicación interactiva.

**Objetivos:**

* Creación de plantillas XDP para el canal de impresión mediante Adobe Forms Designer
* Cargar las plantillas XDP al servidor de AEM Forms
* Crear y habilitar plantillas para el canal web

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-templates-print-web.md)

## Paso 5: Crear una comunicación interactiva {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Una vez creados todos los componentes básicos, como el modelo de datos de formulario, los fragmentos de documento y las plantillas para la versión web, puede empezar a crear una comunicación interactiva.

Las comunicaciones interactivas se pueden entregar a través de dos canales: Imprimir y Web. También puede crear una comunicación interactiva con el canal de impresión como maestro. La opción Imprimir como principal del canal web garantiza que el contenido, la herencia y el enlace de datos del canal web se deriven del canal de impresión.

**Objetivos:**

* Crear comunicación interactiva para el canal de impresión
* Crear comunicación interactiva para el canal web
* Crear comunicaciones interactivas de impresión y web con Imprimir como maestro
* Crear una tabla dinámica en la versión web de la comunicación interactiva
* Crear un gráfico en la versión web de la comunicación interactiva
* Crear hipervínculos en la versión web de la comunicación interactiva

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-interactive-communication0.md)

## Paso 6: Pruebe la comunicación interactiva {#step-test-your-interactive-communication}

![11-test-your-adaptive-form](assets/11-test-your-adaptive-form.png)

Una vez creada una comunicación interactiva, es importante que pruebe cada cambio que realice en ellas. La prueba de cada campo de una comunicación interactiva es tediosa. AEM Forms proporciona un SDK (SDK de Calvin) para automatizar las pruebas de comunicaciones interactivas en el navegador web.

**Objetivos:**

* Crear grupo de pruebas
* Creación de casos de prueba
* Ejecutar los casos de prueba

## Paso 7: Publicar la comunicación interactiva {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

Una vez que haya creado y probado las comunicaciones interactivas mediante canales web e impresos, podrá publicar estos recursos. El caso de uso descrito en este tutorial se centra en la integración de estos recursos con un cliente de correo electrónico. El cliente de correo electrónico sirve como puente para enviar las comunicaciones interactivas a varias direcciones de correo electrónico.

**Objetivos:**

* Integrar las comunicaciones interactivas con un cliente de correo electrónico para poder enviar una comunicación a los clientes
* Incluir un documento PDF como archivo adjunto (Comunicación interactiva creada en el canal de impresión)
* Incluir un vínculo a la versión web de la comunicación interactiva

