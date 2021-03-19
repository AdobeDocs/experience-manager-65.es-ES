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
feature: Seguridad de los documentos
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# Uso de las páginas web de seguridad del documento {#using-the-document-security-webpages}

Los usuarios y administradores utilizan las páginas web de seguridad de documentos para crear y administrar políticas, administrar documentos protegidos por políticas y supervisar eventos asociados con documentos protegidos por políticas. Los administradores también utilizan las páginas web para crear conjuntos de directivas y designar coordinadores de conjuntos de directivas, configurar la configuración predeterminada de seguridad de documentos, administrar el registro y las cuentas de usuarios invitados y supervisar y administrar eventos relacionados con servidores, políticas, usuarios y documentos.

>[!NOTE]
>
>También puede iniciar sesión para documentar la seguridad a través de Acrobat y otras aplicaciones cliente utilizando su cuenta de inicio de sesión de usuario. (Consulte [Configuración del acceso a la seguridad de documentos desde aplicaciones cliente](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications)).

Para abrir las páginas web, necesita un explorador, la dirección URL y la información de inicio de sesión para garantizar la seguridad del documento. La dirección URL de los usuarios es diferente de la dirección URL de los administradores.

Debido a que la seguridad de los documentos hace referencia a los directorios existentes de su organización para la información del usuario, la información de inicio de sesión de seguridad de los documentos puede ser la misma que se utiliza para iniciar sesión en la red y en otras aplicaciones. Consulte con el administrador o administrador del sistema la información de su cuenta.

Para iniciar sesión como administrador, debe tener la función de administrador asignada. Puede utilizar la cuenta de superadministrador predeterminada que se crea durante el proceso de instalación.

## Inicie sesión en las páginas web {#log-in-to-the-web-pages}

Para iniciar sesión en las páginas web mediante un explorador, necesita la dirección URL de seguridad del documento y una cuenta. La dirección URL de los usuarios es diferente de la dirección URL de los administradores. Los administradores también pueden iniciar sesión en las páginas de usuario para crear políticas.

Si tiene acceso a más de una instalación de seguridad de documentos, necesita la URL para la instancia de seguridad de documentos a la que desea acceder. Consulte con el administrador si no dispone de esta información. La dirección URL predeterminada para las páginas de usuario es `https://[host]:[port]/edc`. Es posible que el número de puerto no sea necesario en algunos casos. Solicite detalles al administrador.

La dirección URL predeterminada para los administradores es `https://[host]:[port]/adminui`.

Para los administradores, se crea una cuenta de superadministrador predeterminada durante la instalación. Puede utilizar esta cuenta para iniciar sesión cuando se instale por primera vez document security.

>[!NOTE]
>
>También puede acceder a las páginas web desde Acrobat y otras aplicaciones cliente. Consulte la Ayuda de Acrobat o la ayuda de las extensiones de Acrobat Reader DC correspondientes para obtener más información.

1. Escriba la dirección URL en el explorador:

   URL de seguridad de documento: `https://[host]:[port]/edc`

   o URL de la Consola de administración: `https://[host]:[port]/adminui`

1. En la ventana de inicio de sesión, escriba su nombre de usuario y contraseña y haga clic en Aceptar.
1. En la Consola de administración, haga clic en Servicios > seguridad del documento.

>[!NOTE]
>
>Al trabajar con las páginas web, evite utilizar los botones del explorador, como el botón Atrás, el botón Actualizar y las flechas Atrás y Adelante, ya que esta acción puede causar problemas no deseados en la captura de datos y la visualización de datos.

## Desplazamiento por las páginas web {#navigating-the-web-pages}

Cuando inicie sesión en las páginas web del usuario, verá vínculos a las páginas de usuario Directivas, Documentos y Eventos.

Cuando inicie sesión en la consola de administración y vaya a la página principal de seguridad del documento, también verá uno o dos vínculos adicionales, uno para la página Configuración y otro para la página Usuarios invitados y locales . La página Usuarios locales y invitados solo se muestra si está habilitado el registro de usuarios invitados.

Utilice estos vínculos para acceder a las distintas páginas, donde crea y administra políticas y documentos protegidos por políticas.

**Mostrar una página**

1. Haga clic en el nombre de la página; por ejemplo, haga clic en Directivas.

**Volver a la página anterior**

1. Haga clic en el vínculo de navegación en la parte superior de la página de la página a la que desee volver.

**Actualizar el listado de datos en una página**

1. En la página principal, haga clic en el vínculo a la página que desee actualizar.

>[!NOTE]
>
>Al trabajar con las páginas web, evite utilizar los botones del explorador, como el botón Atrás, el botón Actualizar y las flechas Atrás y Adelante, ya que esta acción puede causar problemas no deseados en la captura de datos y la visualización de datos.

## Configuración del acceso a la seguridad de documentos desde aplicaciones cliente {#setting-up-access-to-document-security-from-client-applications}

Las aplicaciones cliente deben configurarse para conectarse a la seguridad de los documentos a fin de proteger los documentos, abrir documentos protegidos por políticas y conectarse a las páginas web de seguridad de los documentos. Consulte *Ayuda de Acrobat* o la *Ayuda de RightsManagementExtension* apropiada para obtener información sobre cómo configurar la conexión dentro de la aplicación cliente.

Se accede a la seguridad de los documentos a través de Secure Sockets Layer (SSL). Debe instalar el certificado del sitio web en el almacén de certificados para poder acceder a la seguridad de los documentos a través de las aplicaciones cliente.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

Estas instrucciones son específicas de Internet Explorer, pero puede instalar el certificado utilizando cualquier explorador web compatible. Para obtener más información, consulte la Ayuda del explorador.

**Instalación del certificado del servidor mediante Internet Explorer**

1. Abra el explorador web y escriba la URL base para la seguridad del documento en el cuadro Dirección. Por ejemplo, escriba `https://[host]:[port]`. Aparecerá un cuadro de diálogo Alerta de seguridad.
1. Haga clic en Ver certificado y, a continuación, haga clic en Instalar certificado y seleccione los valores predeterminados para la instalación. El certificado debe estar instalado en las Entidades de certificación raíz de confianza.
1. Cierre la sesión del explorador.
1. Abra otra ventana del explorador y escriba la misma dirección URL en el cuadro Dirección. No debería aparecer un cuadro de diálogo Alerta de seguridad. Esta prueba confirma que el certificado está correctamente instalado.

## Cierre la sesión de las páginas web {#log-out-of-the-web-pages}

Cierre la sesión cuando termine de utilizar las páginas web para que pueda utilizar el explorador web con seguridad para otros fines. Según la configuración de la seguridad del documento, es posible que deba cerrar el explorador para cerrar la sesión por completo.

1. En la esquina superior derecha de la página, haga clic en Cerrar sesión.
1. Si aparece un mensaje en la página Cerrar sesión , cierre la ventana del explorador para cerrar la sesión por completo. De lo contrario, puede utilizar el explorador para otros fines.

