---
title: Tipos de extremos
description: Obtenga información acerca de los distintos tipos de extremos. Se pueden agregar diferentes tipos de extremos a los servicios, como correo electrónico, carpeta inspeccionada y muchos más.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# Tipos de extremos {#types-of-endpoints}

Para poder utilizar un servicio, debe configurar y habilitar un extremo. Un extremo especifica cómo se va a invocar un servicio.

>[!NOTE]
>
>En Workbench, los puntos finales se denominan puntos iniciales.

Se pueden agregar los siguientes tipos de extremos a los servicios. No todos los servicios admiten todos los extremos:

**Correo electrónico:** Permite que un usuario invoque un servicio enviando un mensaje de correo electrónico con uno o más archivos adjuntos a una cuenta de correo electrónico especificada. Antes de configurar un extremo de correo electrónico, debe configurar las cuentas de correo electrónico necesarias. (Consulte Configuración de puntos finales de correo electrónico).

**Carpeta inspeccionada:** Permite que un usuario invoque un servicio colocando un archivo en una carpeta, que se analiza a un intervalo definido. (Consulte Configuración de puntos finales de carpetas vigiladas).

**Administrador de tareas:** Permite que un usuario de Workspace invoque el servicio.

**Remoting:** Habilita una aplicación creada con Flex AEM AEM para invocar el servicio mediante (obsoleto para formularios de la versión de la aplicación en tiempo de ejecución) la comunicación remota de formularios de la aplicación de formularios. Se crea automáticamente un extremo remoto para cada servicio activado. Se crea un destino de Flex con el mismo nombre que el extremo y los clientes de Flex pueden crear objetos remotos que apunten a este destino para invocar operaciones en el servicio correspondiente.

**SOAP:** AEM Habilita una aplicación cliente desarrollada mediante las API de programación de formularios de la aplicación para invocar el servicio mediante el modo SOAP. Se crea automáticamente un punto final SOAP para cada servicio activado.

**nota**: *La seguridad se puede quitar de los documentos de seguridad del documento cuando se utiliza el extremo SOAP mientras se visualizan los documentos en Adobe Acrobat o Adobe Reader. Para obtener más información sobre cómo deshabilitar los extremos SOAP en los documentos de CRM, consulte [Deshabilitar extremos SOAP para documentos de Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** AEM Habilita una aplicación cliente desarrollada mediante las API de programación de formularios de la aplicación para invocar el servicio mediante Enterprise JavaBeans (EJB). Se crea automáticamente un extremo de EJB para cada servicio activado.

**WSDL:** AEM Habilita una aplicación cliente desarrollada mediante las API de programación de formularios de la aplicación para invocar el servicio mediante el Lenguaje de definición de servicios web (WSDL). AEM La página Configuraciones principales contiene una opción para habilitar la generación de WSDL para todos los servicios que forman parte de los formularios de. AEM (Consulte Configuración general de los formularios de ).

**REST:** Los procesos creados en Workbench se pueden configurar para que se puedan invocar a través de solicitudes de transferencia de estado representacional (REST). Las solicitudes REST se envían desde páginas del HTML. AEM Es decir, puede invocar un proceso de formularios de la aplicación de la forma directa desde una página web utilizando una petición REST.

Los extremos Correo electrónico, TaskManager, Carpeta inspeccionada y Remoting exponen únicamente una operación específica del servicio. Para agregar estos extremos, es necesario realizar un segundo paso de configuración para seleccionar un método para invocar el servicio, establecer parámetros de configuración y especificar asignaciones de parámetros de entrada y salida.
