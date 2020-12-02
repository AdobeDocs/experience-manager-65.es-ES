---
title: Prevención de los ataques de las Fuerzas Centrales de Seguridad
seo-title: Prevención de los ataques de las Fuerzas Centrales de Seguridad
description: Aprenda a evitar ataques de falsificación de solicitudes entre sitios (CSRF) y a evitar que los datos de los usuarios se vean comprometidos.
seo-description: Aprenda a evitar ataques de falsificación de solicitudes entre sitios (CSRF) y a evitar que los datos de los usuarios se vean comprometidos.
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---


# Prevención de ataques de CSRF {#preventing-csrf-attacks}

## Cómo funcionan los ataques de CSRF {#how-csrf-attacks-work}

La falsificación de solicitudes entre sitios (CSRF) es una vulnerabilidad de sitio web en la que el navegador de un usuario válido se utiliza para enviar una solicitud maliciosa, posiblemente a través de un iFrame. Debido a que el explorador envía cookies por dominio, si el usuario ha iniciado sesión en una aplicación, los datos del usuario pueden verse comprometidos.

Por ejemplo, considere un escenario en el que haya iniciado sesión en la consola de administración en un navegador. Recibirá un mensaje de correo electrónico con un vínculo. Haga clic en el vínculo, que abre una nueva ficha en el explorador. La página que abrió contiene un iFrame oculto que realiza una solicitud malintencionada al servidor de formularios mediante la cookie de la sesión de formularios AEM autenticados. Dado que la Administración de usuarios recibe una cookie válida, pasa la solicitud.

## Términos relacionados con el CSRF {#csrf-related-terms}

**Referente:** la dirección de la página de origen desde la que proviene una solicitud. Por ejemplo: una página web en site1.com contiene un vínculo a site2.com. Al hacer clic en el vínculo, se envía una solicitud a site2.com. El referente de esta solicitud es site1.com porque la solicitud se realiza desde una página cuyo origen es site1.com.

**URI incluidos en la lista de permitidos:** URIs identifican recursos en el servidor de formularios que se solicitan, por ejemplo, /adminui o /contentspace. Algunos recursos pueden permitir que una solicitud entre en la aplicación desde sitios externos. Estos recursos se consideran URI incluidos en la lista de permitidos. El servidor de formularios nunca realiza una comprobación de referente desde URI incluidos en la lista de permitidos.

**Referente nulo:** cuando se abre una nueva ventana o ficha del explorador, después se escribe una dirección y se pulsa Intro, el referente es nulo. La solicitud es totalmente nueva y no procede de una página web principal; por lo tanto, no hay ningún referente para la solicitud. El servidor de formularios puede recibir un referente nulo de:

* solicitudes realizadas en puntos finales SOAP o REST desde Acrobat
* cualquier cliente de escritorio que realice una solicitud HTTP en un extremo SOAP o REST de formularios AEM
* cuando se abre una nueva ventana del explorador y se introduce la dirección URL de cualquier página de inicio de sesión de la aplicación Web de formularios AEM

Permitir un referente nulo en los extremos SOAP y REST. También permita un referente nulo en todas las páginas de inicio de sesión de URI como /adminui y /contentspace y sus correspondientes recursos asignados. Por ejemplo, el servlet asignado para /contentspace es /contentspace/faces/jsp/login.jsp, que debe ser una excepción de referente nulo. Esta excepción solo es necesaria si se activa el filtrado de GET para la aplicación web. Las aplicaciones pueden especificar si se permiten referentes nulos. Consulte &quot;Protección contra los ataques de falsificación de solicitudes entre sitios&quot; en [Endurecimiento y seguridad para formularios AEM](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**Excepción de referente permitida:Excepción de referente** permitida es una sublista de la lista de referentes permitidos, desde la cual se bloquean las solicitudes. Las excepciones de referencia permitidas son específicas de una aplicación web. Si no se debe permitir que un subconjunto de los referentes permitidos invoque una aplicación web concreta, puede realizar listas de bloqueados de los referentes mediante Excepciones de referentes permitidas. Las excepciones de referente permitidas se especifican en el archivo web.xml para la aplicación. (Consulte &quot;Protección contra los ataques de falsificación de solicitudes entre sitios&quot; en Endurecimiento y seguridad para formularios AEM en la página Ayuda y Tutorials).

## Cómo funcionan los referentes permitidos {#how-allowed-referers-work}

AEM formularios proporcionan un filtro de referentes que puede ayudar a evitar ataques de CSRF. Así funciona el filtrado de referentes:

1. El servidor de formularios comprueba el método HTTP utilizado para la invocación:

   * Si es POST, el servidor de formularios realiza la comprobación del encabezado del referente.
   * Si es GET, el servidor de formularios omite la comprobación del referente, a menos que CSRF_CHECK_GETS se establezca en true, en cuyo caso realiza la comprobación del encabezado del referente. CSRF_CHECK_GETS se especifica en el archivo web.xml de la aplicación. (Consulte &quot;Protección contra los ataques de falsificación de solicitudes entre sitios&quot; en [Guía de seguridad y endurecimiento](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. El servidor de formularios comprueba si el URI solicitado está incluido en la lista de permitidos:

   * Si el URI está incluido en la lista de permitidos, el servidor pasa la solicitud.
   * Si el URI solicitado no está incluido en la lista de permitidos, el servidor recupera el referente de la solicitud.

1. Si hay un referente en la solicitud, el servidor comprueba si es un referente permitido. Si está permitido, el servidor comprueba la existencia de una excepción de referente:

   * Si se trata de una excepción, la solicitud se bloquea.
   * Si no es una excepción, se pasa la solicitud.

1. Si no hay ningún referente en la solicitud, el servidor comprueba si se permite un referente nulo.

   * Si se permite un referente nulo, se pasa la solicitud.
   * Si no se permite un referente nulo, el servidor comprueba si el URI solicitado es una excepción para el referente nulo y gestiona la solicitud en consecuencia.

## Configurar los referentes permitidos {#configure-allowed-referers}

Al ejecutar Configuration Manager, el host predeterminado y la dirección IP o el servidor de formularios se agregan a la lista Referente permitido. Puede editar esta lista en la consola de administración.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configurar URL de referente permitidas. La lista Referente permitido aparece en la parte inferior de la página.
1. Para agregar un referente permitido:

   * Escriba un nombre de host o una dirección IP en el cuadro Referentes permitidos. Para agregar más de un referente permitido a la vez, escriba cada nombre de host o dirección IP en una línea nueva.
   * En los cuadros Puerto HTTP y Puertos HTTPS, especifique qué puertos se permiten para HTTP, HTTPS o ambos. Si deja estas casillas vacías, se utilizarán los puertos predeterminados (puerto 80 para HTTP y puerto 443 para HTTPS). Si introduce `0` (cero) en los cuadros, todos los puertos de ese servidor estarán habilitados. También puede introducir un número de puerto específico para habilitar solo ese puerto.
   * Haga clic en Agregar.

1. Para eliminar la entrada de la lista Referente permitido, seleccione el elemento en la lista y haga clic en Eliminar.

   Si la Lista Referente permitido está vacía, la función CSRF deja de funcionar y el sistema se vuelve inseguro.

1. Después de cambiar la lista Referente permitido, reinicie el servidor de formularios AEM.

