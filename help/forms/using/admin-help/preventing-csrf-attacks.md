---
title: Prevención de ataques del CSRF
seo-title: Preventing CSRF attacks
description: Aprenda a evitar ataques de falsificación de solicitudes entre sitios (CSRF) y a evitar que los datos de los usuarios se vean comprometidos.
seo-description: Learn how to prevent Cross-site request forgery (CSRF) attacks and safeguard user data from being compromised.
uuid: f3553826-f5eb-40ea-aeb7-90e4ad30598c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a3cbffb7-c1d1-47c2-bcfd-70f1e2d81ac9
exl-id: e17fc114-eba5-4e1b-8e70-ad6af7008018
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# Prevención de ataques del CSRF {#preventing-csrf-attacks}

## Cómo funcionan los ataques de la CSRF {#how-csrf-attacks-work}

La falsificación de solicitudes entre sitios (CSRF) es una vulnerabilidad de sitio web en la que el explorador de un usuario válido se utiliza para enviar una solicitud maliciosa, posiblemente a través de un iFrame. Dado que el explorador envía cookies en función del dominio, si el usuario ha iniciado sesión en una aplicación, los datos del usuario pueden verse comprometidos.

Por ejemplo, imaginemos un escenario en el que ha iniciado sesión en la consola de administración en un explorador. Recibe un mensaje de correo electrónico que contiene un vínculo. Haga clic en el vínculo , que abre una nueva pestaña en el explorador. La página que abrió contiene un iFrame oculto que realiza una solicitud malintencionada al servidor de formularios mediante la cookie de la sesión de formularios AEM autenticados. Como Administración de usuarios recibe una cookie válida, pasa la solicitud.

## Términos relacionados con el RCSF {#csrf-related-terms}

**Referente:** La dirección de la página de origen desde la que proviene una solicitud. Por ejemplo, una página web en site1.com contiene un vínculo a site2.com. Al hacer clic en el vínculo, se envía una solicitud a site2.com. El referente de esta solicitud es site1.com porque la solicitud se realiza desde una página cuyo origen es site1.com.

**URI incluidos en la lista de permitidos:** Los URI identifican los recursos del servidor de formularios que se están solicitando, por ejemplo, /adminui o /contentspace. Algunos recursos pueden permitir que una solicitud entre en la aplicación desde sitios externos. Estos recursos se consideran URI incluidas en la lista de permitidos. El servidor de formularios nunca realiza una comprobación de referentes desde URI incluidos en la lista de permitidos.

**Referente nulo:** Cuando abra una nueva ventana o ficha del explorador, después escriba una dirección y pulse Intro, el referente será nulo. La solicitud es completamente nueva y no se origina en una página web principal; por lo tanto, no hay ningún referente para la solicitud. El servidor de formularios puede recibir un referente nulo de:

* solicitudes realizadas en extremos SOAP o REST desde Acrobat
* cualquier cliente de escritorio que realice una solicitud HTTP en un extremo SOAP o REST de formularios AEM
* cuando se abre una nueva ventana del explorador y se introduce la dirección URL de cualquier página de inicio de sesión de la aplicación web de formularios AEM

Permita un referente nulo en los extremos SOAP y REST. También permita un referente nulo en todas las páginas de inicio de sesión de URI como /adminui y /contentspace y sus recursos asignados correspondientes. Por ejemplo, el servlet asignado para /contentspace es /contentspace/faces/jsp/login.jsp, que debe ser una excepción de referente nulo. Esta excepción solo es necesaria si se habilita el filtrado de GET para la aplicación web. Las aplicaciones pueden especificar si se permiten referentes nulos. Consulte &quot;Protección contra ataques de falsificación de solicitudes entre sitios&quot; en [Endurecimiento y seguridad de los formularios AEM](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**Excepción de referente permitida:** La excepción de referente permitida es una sublista de la lista de referentes permitidos, desde la cual se bloquean las solicitudes. Las excepciones de referencia permitidas son específicas de una aplicación web. Si no se debe permitir que un subconjunto de los Referentes permitidos invoque una aplicación web concreta, se puede realizar la lista de bloqueados de los referentes a través de Excepciones de Referentes Permitidas. Las excepciones de referentes permitidas se especifican en el archivo web.xml de la aplicación. (Consulte &quot;Protección contra los ataques de falsificación de solicitudes entre sitios&quot; en Endurecimiento y seguridad para AEM formularios en la página Ayuda y Tutorials ).

## Funcionamiento de los referentes permitidos {#how-allowed-referers-work}

AEM formularios proporciona filtrado de referentes, que puede ayudar a prevenir ataques de CSRF. Así funciona el filtrado de referentes:

1. El servidor de formularios comprueba el método HTTP utilizado para la invocación:

   * Si es POST, el servidor de formularios realiza la comprobación del encabezado del referente.
   * Si es GET, el servidor de formularios evita la comprobación del remitente del reenvío, a menos que CSRF_CHECK_GETS esté establecido en true, en cuyo caso realiza la comprobación del encabezado del remitente. CSRF_CHECK_GETS se especifica en el archivo web.xml para su aplicación. (Consulte &quot;Protección contra ataques de falsificación de solicitudes entre sitios&quot; en [Guía de endurecimiento y seguridad](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. El servidor de formularios comprueba si el URI solicitado está incluido en la lista de permitidos:

   * Si el URI está incluido en la lista de permitidos, el servidor pasa la solicitud.
   * Si el URI solicitado no está incluido en la lista de permitidos, el servidor recupera el referente de la solicitud.

1. Si hay un referente en la solicitud, el servidor comprueba si es un referente permitido. Si está permitido, el servidor comprueba la existencia de una excepción de referente:

   * Si es una excepción, la solicitud se bloquea.
   * Si no es una excepción, se pasa la solicitud.

1. Si no hay ningún referente en la solicitud, el servidor comprueba si se permite un referente nulo.

   * Si se permite un referente nulo, se pasa la solicitud.
   * Si no se permite un referente nulo, el servidor comprueba si el URI solicitado es una excepción para el referente nulo y gestiona la solicitud en consecuencia.

## Configuración de los referentes permitidos {#configure-allowed-referers}

Cuando se ejecuta Configuration Manager, el host predeterminado y la dirección IP o el servidor de formularios se añaden a la lista de referentes permitidos . Puede editar esta lista en la consola de administración.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configurar URL de referente permitidas. La lista Referente permitido aparece en la parte inferior de la página.
1. Para agregar un referente permitido:

   * Escriba un nombre de host o una dirección IP en el cuadro Referentes permitidos . Para agregar más de un referente permitido a la vez, escriba cada nombre de host o dirección IP en una nueva línea.
   * En los cuadros Puerto HTTP y Puertos HTTPS, especifique qué puertos se permiten para HTTP, HTTPS o ambos. Si deja esas casillas vacías, se utilizan los puertos predeterminados (puerto 80 para HTTP y puerto 443 para HTTPS). Si introduce `0` (cero) en los cuadros, todos los puertos de ese servidor están habilitados. También puede introducir un número de puerto específico para habilitar solo ese puerto.
   * Haga clic en Agregar.

1. Para eliminar una entrada de la lista Referente permitido, seleccione el elemento de la lista y haga clic en Eliminar.

   Si la lista de referentes permitidos está vacía, la función CSRF deja de funcionar y el sistema se vuelve inseguro.

1. Después de cambiar la lista Referente permitido, reinicie el servidor de AEM forms.
