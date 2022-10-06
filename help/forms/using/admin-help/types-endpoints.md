---
title: Tipos de extremos
seo-title: Types of endpoints
description: Obtenga información sobre los distintos tipos de extremos.
seo-description: Learn about the different types of endpoints.
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Tipos de extremos {#types-of-endpoints}

Para poder utilizar un servicio, debe configurar y habilitar un punto final. Un punto final especifica cómo se va a invocar un servicio.

>[!NOTE]
>
>En Workbench, los extremos se denominan puntos de inicio.

Se pueden agregar los siguientes tipos de extremos a los servicios. No todos los servicios admiten todos los extremos:

**Correo electrónico:** Permite que un usuario invoque un servicio enviando un mensaje de correo electrónico con uno o más archivos adjuntos a una cuenta de correo electrónico especificada. Antes de configurar un extremo de correo electrónico, debe configurar las cuentas de correo electrónico necesarias. (Consulte Configuración de extremos de correo electrónico).

**Carpeta vigilada:** Permite que un usuario invoque un servicio colocando un archivo en una carpeta, que se analiza en un intervalo definido. (Consulte Configuración de los extremos de las carpetas vigiladas.)

**TaskManager:** Permite a un usuario de Workspace invocar el servicio.

**Remotando:** Habilita una aplicación creada con Flex para invocar el servicio mediante (obsoleto para AEM formularios) AEM Forms Remoting. Se crea automáticamente un punto final remoto para cada servicio activado. Se crea un destino de Flex que tiene el mismo nombre que el extremo y los clientes de Flex pueden crear objetos remotos que apunten a este destino para invocar operaciones en el servicio correspondiente.

**SOAP:** Permite que una aplicación cliente desarrollada mediante las API de programación de formularios AEM invoque el servicio mediante el modo SOAP. Se crea automáticamente un extremo SOAP para cada servicio activado.

**nota**: *La seguridad se puede eliminar de los documentos de seguridad de documentos cuando se utiliza el extremo SOAP al ver los documentos en Adobe Acrobat o Adobe Reader. Para obtener más información sobre cómo deshabilitar los puntos de conexión SOAP en los documentos LCRM, consulte [Desactivación de extremos SOAP para documentos de seguridad de documentos](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** Permite que una aplicación cliente desarrollada mediante las API de programación de formularios AEM invoque el servicio mediante el modo Enterprise JavaBeans (EJB). Se crea automáticamente un extremo EJB para cada servicio activado.

**WSDL:** Permite que una aplicación cliente desarrollada mediante las API de programación de formularios AEM invoque el servicio mediante el lenguaje de definición de servicio web (WSDL). La página Configuraciones principales contiene una opción para habilitar la generación de WSDL para todos los servicios que forman parte de AEM formularios. (Consulte Configuración general AEM la configuración de formularios).

**REST:** Los procesos creados en Workbench se pueden configurar para que pueda invocarlos mediante solicitudes de transferencia de estado representativo (REST). Las solicitudes REST se envían desde páginas de HTML. Es decir, puede invocar un proceso de formularios AEM directamente desde una página web mediante una solicitud REST.

Los extremos Correo electrónico, TaskManager, Carpeta vigilada y Remoting solo exponen una operación específica del servicio. La adición de estos extremos requiere un segundo paso de configuración para seleccionar un método para invocar el servicio, configurar parámetros de configuración y especificar asignaciones de parámetros de entrada y salida.
