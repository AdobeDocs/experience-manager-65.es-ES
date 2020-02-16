---
title: Tipos de extremos
seo-title: Tipos de extremos
description: Obtenga información sobre los distintos tipos de extremos.
seo-description: Obtenga información sobre los distintos tipos de extremos.
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Tipos de extremos {#types-of-endpoints}

Antes de utilizar un servicio, debe configurar y habilitar un punto final. Un punto final especifica cómo se va a invocar un servicio.

>[!NOTE]
>
>En Workbench, los puntos finales se denominan puntos de inicio.

Los siguientes tipos de extremos se pueden agregar a los servicios. No todos los servicios admiten todos los extremos:

**** Correo electrónico: Permite que un usuario invoque un servicio enviando un mensaje de correo electrónico con uno o varios archivos adjuntos a una cuenta de correo electrónico específica. Antes de configurar un extremo de correo electrónico, debe configurar las cuentas de correo electrónico necesarias. (Consulte Configuración de los extremos de correo electrónico).

**** Carpeta vigilada: Permite que un usuario invoque un servicio colocando un archivo en una carpeta, que se analiza a un intervalo definido. (Consulte Configuración de los extremos de carpeta observados).

**** Administrador de tareas: Permite que un usuario de Workspace invoque el servicio.

**** Remoting: Permite que una aplicación creada con Flex invoque el servicio mediante AEM forms Remoting (obsoleto para formularios AEM). Se crea automáticamente un extremo remoto para cada servicio activado. Se crea un destino de Flex con el mismo nombre que el extremo y los clientes de Flex pueden crear objetos remotos que apunten a este destino para invocar operaciones en el servicio correspondiente.

**** SOAP: Permite que una aplicación cliente desarrollada mediante las API de programación de formularios AEM invoque el servicio mediante el modo SOAP. Se crea automáticamente un extremo SOAP para cada servicio activado.

**nota**: La *seguridad se puede eliminar de los documentos de seguridad cuando se utiliza el extremo SOAP al ver los documentos en Adobe Acrobat o Adobe Reader. Para obtener más información sobre cómo deshabilitar los puntos finales SOAP en los documentos LCRM, consulte[Deshabilitar los puntos finales SOAP para documentos de seguridad de documentos](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**** EJB: Permite que una aplicación cliente desarrollada mediante las API de programación de formularios AEM invoque el servicio mediante el modo de JavaBeans (EJB) empresarial. Se crea automáticamente un punto final de EJB para cada servicio activado.

**** WSDL: Permite que una aplicación cliente desarrollada mediante las API de programación de formularios AEM invoque el servicio mediante el lenguaje de definición de servicio Web (WSDL). La página Configuraciones principales contiene una opción para habilitar la generación de WSDL para todos los servicios que forman parte de formularios AEM. (Consulte Configuración general de formularios AEM).

**** REST:Los procesos creados en Workbench se pueden configurar para que pueda invocarlos mediante solicitudes de transferencia de estado representativa (REST). Las solicitudes REST se envían desde páginas HTML. Es decir, puede invocar un proceso de formularios AEM directamente desde una página web mediante una solicitud REST.

Los extremos Correo electrónico, TaskManager, Carpeta vigilada y Remoting solo exponen una operación específica del servicio. La adición de estos extremos requiere un segundo paso de configuración para seleccionar un método para invocar el servicio, configurar parámetros de configuración y especificar asignaciones de parámetros de entrada y salida.
