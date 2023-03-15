---
title: Prevenir ataques CSRF
seo-title: Preventing CSRF attacks
description: Aprenda a evitar ataques de falsificación de solicitudes entre sitios (CSRF) y a salvaguardar los datos de usuario de verse comprometidos.
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
ht-degree: 5%

---

# Prevenir ataques CSRF {#preventing-csrf-attacks}

## Cómo funcionan los ataques CSRF {#how-csrf-attacks-work}

La falsificación de solicitudes entre sitios (CSRF) es una vulnerabilidad del sitio web en la que se utiliza el explorador de un usuario válido para enviar una solicitud maliciosa, posiblemente a través de un iFrame. Dado que el explorador envía cookies en función del dominio, si el usuario ha iniciado sesión en una aplicación, los datos del usuario pueden verse comprometidos.

Por ejemplo, imagine un escenario en el que ha iniciado sesión en la consola de administración en un explorador. Recibirá un mensaje de correo electrónico que contiene un vínculo. Hace clic en el vínculo, que abre una nueva pestaña en el explorador. AEM La página que ha abierto contiene un iFrame oculto que realiza una solicitud malintencionada al servidor de Forms mediante la cookie de la sesión de formularios autenticados del usuario. Como Administración de usuarios recibe una cookie válida, pasa la solicitud.

## Términos relacionados con CSRF {#csrf-related-terms}

**Referer:** La dirección de la página de origen de la que proviene una solicitud. Por ejemplo, una página web en site1.com contiene un vínculo a site2.com. Al hacer clic en el vínculo, se publica una solicitud en site2.com. El referente de esta solicitud es site1.com porque la solicitud se realiza desde una página cuyo origen es site1.com.

**URI incluidos en la lista de permitidos:** Los URI identifican recursos del servidor de Forms que se solicitan, por ejemplo, /adminui o /contentspace. Algunos recursos pueden permitir que una solicitud entre en la aplicación desde sitios externos. Estos recursos se consideran URI incluidos en la lista de permitidos. El servidor de Forms nunca realiza una comprobación del referente desde URI incluidos en la lista de permitidos.

**Referente nulo:** Al abrir una nueva ventana o ficha del explorador, escribir una dirección y pulsar Entrar, el referente es nulo. La solicitud es completamente nueva y no se origina desde una página web principal; por lo tanto, no hay ningún referente para la solicitud. El servidor de Forms puede recibir un referente nulo de:

* solicitudes realizadas en puntos finales SOAP o REST desde Acrobat
* AEM cualquier cliente de escritorio que realice una solicitud HTTP en un extremo SOAP o REST de formularios
* AEM cuando se abre una nueva ventana del explorador y se introduce la dirección URL de cualquier página de inicio de sesión de la aplicación web de formularios en la que se haya creado la aplicación de la aplicación

Permitir un referente nulo en los extremos SOAP y REST. También permita un referente nulo en todas las páginas de inicio de sesión de URI como /adminui y /contentspace y sus recursos asignados correspondientes. Por ejemplo, el servlet asignado para /contentspace es /contentspace/faces/jsp/login.jsp, que debería ser una excepción de referente nulo. Esta excepción solo es necesaria si habilita el filtrado de GET para la aplicación web. Las aplicaciones pueden especificar si se permiten referentes nulos. Consulte &quot;Protección frente a ataques de falsificación de solicitud en sitios múltiples&quot; en [AEM Protección y seguridad para formularios de](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**Excepción de referente permitido:** Excepción de referente permitida es una sublista de la lista de referentes permitidos, desde los que se bloquean las solicitudes. Las excepciones de referencia permitidas son específicas de una aplicación web. Si no se debe permitir que un subconjunto de los referentes permitidos invoque una aplicación web determinada, se puede realizar la lista de bloqueados de los referentes a través de Excepciones de referentes permitidos. Las excepciones de referentes permitidos se especifican en el archivo web.xml de la aplicación. AEM (Consulte &quot;Protección frente a ataques de falsificación de solicitud en sitios múltiples&quot; en Protección y seguridad para formularios en forma de en la página Ayuda y Tutorials ).

## Funcionamiento de los referentes permitidos {#how-allowed-referers-work}

AEM Los formularios de proporcionan un filtrado de referentes, que puede ayudar a evitar ataques de CSRF. Funciona el filtrado de referentes de la siguiente manera:

1. El servidor de Forms comprueba el método HTTP utilizado para la invocación:

   * Si es el POST, el servidor de Forms realiza la comprobación del encabezado del referente.
   * Si es GET, el servidor de Forms omite la comprobación del referente, a menos que CSRF_CHECK_GETS esté establecido en true, en cuyo caso realiza la comprobación del encabezado del referente. CSRF_CHECK_GETS se especifica en el archivo web.xml de la aplicación. (Consulte &quot;Protección frente a ataques de falsificación de solicitud en sitios múltiples&quot; en [Guía de seguridad y protección](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).)

1. El servidor de Forms comprueba si el URI solicitado está incluido en la lista de permitidos:

   * Si el URI está incluido en la lista de permitidos, el servidor pasa la solicitud.
   * Si el URI solicitado no está incluido en la lista de permitidos, el servidor recupera el referente de la solicitud.

1. Si hay un referente en la solicitud, el servidor comprueba si es un referente permitido. Si está permitido, el servidor comprueba la existencia de una excepción de referente:

   * Si existe una excepción, la solicitud se bloquea.
   * Si hay ninguna excepción, se pasa la solicitud.

1. Si no hay ningún referente en la solicitud, el servidor comprueba si se permite un referente nulo.

   * Si se permite un referente nulo, se pasa la solicitud.
   * Si no se permite un referente nulo, el servidor comprueba si el URI solicitado es una excepción para el referente nulo y gestiona la solicitud en consecuencia.

## Configuración de referentes permitidos {#configure-allowed-referers}

Al ejecutar el Administrador de configuración, el host predeterminado y la dirección IP o el servidor de Forms se agregan a la lista Referentes permitidos. Puede editar esta lista en la consola de administración.

1. En la consola de administración, haga clic en Configuración > User Management > Configuración > Configurar direcciones URL de referentes permitidos. La lista Referente permitidos aparece en la parte inferior de la página.
1. Para agregar un referente permitido:

   * Escriba un nombre de host o una dirección IP en el cuadro Referentes permitidos. Para agregar varios referentes permitidos a la vez, escriba cada nombre de host o dirección IP en una nueva línea.
   * En los cuadros Puerto HTTP y Puertos HTTPS, especifique qué puertos permiten HTTP, HTTPS o ambos. Si deja esas casillas vacías, se usan los puertos predeterminados (puerto 80 para HTTP y puerto 443 para HTTPS). Si introduce `0` (cero) en los cuadros, todos los puertos de ese servidor están habilitados. También puede especificar un número de puerto específico para habilitar sólo ese puerto.
   * Haga clic en Agregar.

1. Para quitar una entrada de la lista Referente permitidos, seleccione el elemento de la lista y haga clic en Eliminar.

   Si la Lista de referentes permitidos está vacía, la función CSRF deja de funcionar y el sistema se vuelve inseguro.

1. AEM Después de cambiar la lista Referente permitidos, reinicie el servidor de Forms de la.
