---
title: Uso de las páginas web de seguridad del documento
seo-title: Uso de las páginas web de seguridad del documento
description: Descubra cómo puede iniciar sesión, navegar y utilizar las páginas web de seguridad del documento.
seo-description: Descubra cómo puede iniciar sesión, navegar y utilizar las páginas web de seguridad del documento.
uuid: b4863343-cda5-474a-a101-a20e39b1f8c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2878b145-e6c0-48d3-810c-3540de13c826
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Uso de las páginas web de seguridad del documento {#using-the-document-security-webpages}

Los usuarios y administradores utilizan las páginas web de seguridad de documentos para crear y administrar políticas, administrar documentos protegidos por políticas y supervisar eventos asociados a documentos protegidos por políticas. Los administradores también utilizan las páginas web para crear conjuntos de políticas y designar coordinadores de conjuntos de políticas, configurar las opciones predeterminadas de seguridad de los documentos, administrar el registro y las cuentas de los usuarios invitados y supervisar y administrar los eventos relacionados con el servidor, la política, el usuario y los documentos.

>[!NOTE]
>
>También puede iniciar sesión para documentar la seguridad a través de Acrobat y otras aplicaciones cliente mediante su cuenta de inicio de sesión de usuario. (Consulte [Configuración del acceso a la seguridad de documentos desde aplicaciones](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications)cliente).

Para abrir las páginas web, necesita un navegador, la dirección URL y la información de inicio de sesión para garantizar la seguridad de los documentos. La dirección URL de los usuarios es diferente de la URL de los administradores.

Debido a que la seguridad de los documentos hace referencia a los directorios existentes de la organización para obtener información de usuario, la información de inicio de sesión de seguridad de los documentos puede ser la misma información que se utiliza para iniciar sesión en la red y en otras aplicaciones. Consulte con el administrador o administrador del sistema la información de su cuenta.

Para iniciar sesión como administrador, debe tener asignada la función de administrador. Puede utilizar la cuenta de superadministrador predeterminada que se crea durante el proceso de instalación.

## Inicie sesión en las páginas web {#log-in-to-the-web-pages}

Para iniciar sesión en las páginas web con un navegador, necesita la URL de seguridad del documento y una cuenta. La dirección URL de los usuarios es diferente de la URL de los administradores. Los administradores también pueden iniciar sesión en las páginas de usuario para crear políticas.

Si tiene acceso a más de una instalación de seguridad de documentos, necesita la URL para la instancia de seguridad de documentos a la que desea acceder. Consulte con el administrador si no tiene esta información. La dirección URL predeterminada para las páginas de usuario es https://*[host]*:*[port]*/edc. Es posible que en algunos casos no se requiera el número de puerto. Pida detalles al administrador.

La dirección URL predeterminada para administradores es https://*[host]*:*[port]*/adminui.

Para los administradores, se crea una cuenta de superadministrador predeterminada durante la instalación. Puede utilizar esta cuenta para iniciar sesión cuando se instale por primera vez Document Security.

>[!NOTE]
>
>También puede acceder a las páginas web desde Acrobat y otras aplicaciones cliente. Consulte la Ayuda de Acrobat o la Ayuda de las extensiones de Acrobat Reader DC correspondientes para obtener más información.

1. Escriba la dirección URL en el explorador:

   URL de seguridad del documento: `https://`*[host ]*`:`*[port]*`/edc`

   o URL de la Consola de administración: `https://`*[host ]*`:`*[port]*`/adminui`

1. En la ventana de inicio de sesión, escriba su nombre de usuario y contraseña y haga clic en Aceptar.
1. En la Consola de administración, haga clic en Servicios > seguridad de documentos.

>[!NOTE]
>
>Al trabajar con páginas web, evite utilizar los botones del navegador, como el botón Atrás, el botón Actualizar y las flechas Atrás y Avanzar, ya que esta acción puede causar problemas no deseados en la captura de datos y la visualización de datos.

## Navegación por las páginas Web {#navigating-the-web-pages}

Al iniciar sesión en las páginas web del usuario, verá vínculos a las páginas de usuario de Políticas, Documentos y Eventos.

Al iniciar sesión en la consola de administración y desplazarse a la página principal de seguridad del documento, también puede ver uno o dos vínculos adicionales, uno para la página Configuración y otro para la página Usuarios invitados y locales. La página Usuarios invitados y locales solo se muestra si está activado el registro de usuarios invitados.

Utilice estos vínculos para acceder a las distintas páginas, donde puede crear y administrar políticas y documentos protegidos por políticas.

**Mostrar una página**

1. Haga clic en el nombre de la página; como hacer clic en Directivas.

**Volver a la página anterior**

1. Haga clic en el vínculo de navegación en la parte superior de la página a la que desea volver.

**Actualizar el listado de datos en una página**

1. En la página principal, haga clic en el vínculo a la página que desee actualizar.

>[!NOTE]
>
>Al trabajar con páginas web, evite utilizar los botones del navegador, como el botón Atrás, el botón Actualizar y las flechas Atrás y Avanzar, ya que esta acción puede causar problemas no deseados en la captura de datos y la visualización de datos.

## Configuración del acceso a la seguridad de los documentos desde las aplicaciones cliente {#setting-up-access-to-document-security-from-client-applications}

Las aplicaciones cliente deben configurarse para conectarse a la seguridad de documentos a fin de proteger documentos, abrir documentos protegidos por políticas y conectarse a las páginas web de seguridad de documentos. Consulte la Ayuda *de* Acrobat o la Ayuda *correspondiente de* RightsManagementExtension para obtener información sobre la configuración de la conexión dentro de la aplicación cliente.

Se puede acceder a la seguridad del documento a través de la capa de conexión segura (SSL). Debe instalar el certificado del sitio web en el almacén de certificados para poder acceder a la seguridad de los documentos a través de las aplicaciones cliente.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

Estas instrucciones son específicas de Internet Explorer, pero puede instalar el certificado mediante cualquier navegador web compatible. Para obtener más información, consulte la Ayuda del explorador.

**Instalar el certificado del servidor mediante Internet Explorer**

1. Abra el explorador Web y escriba la dirección URL base para la seguridad del documento en el cuadro Dirección. For example, type `https://[host]:[port]`. Aparece un cuadro de diálogo Alerta de seguridad.
1. Haga clic en Ver certificado y, a continuación, en Instalar certificado y seleccione los valores predeterminados para la instalación. El certificado debe instalarse en las entidades emisoras de certificados raíz de confianza.
1. Cierre la sesión del explorador.
1. Abra otra ventana del explorador y escriba la misma dirección URL en el cuadro Dirección. No debería aparecer un cuadro de diálogo de alerta de seguridad. Esta prueba confirma que el certificado está correctamente instalado.

## Cerrar sesión en las páginas web {#log-out-of-the-web-pages}

Cierre la sesión cuando termine de utilizar las páginas web para que pueda utilizar el explorador web con seguridad para otros fines. Según la configuración de la seguridad del documento, es posible que deba cerrar el explorador para cerrar la sesión por completo.

1. En la esquina superior derecha de la página, haga clic en Cerrar sesión.
1. Si aparece un mensaje en la página Cerrar sesión, cierre la ventana del explorador para cerrar la sesión por completo. De lo contrario, puede utilizar el explorador para otros fines.

