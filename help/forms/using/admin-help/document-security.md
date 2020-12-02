---
title: 'Seguridad de documento '
seo-title: 'Seguridad de documento '
description: Descubra cómo puede crear, almacenar y aplicar parámetros de confidencialidad predefinidos, y distribuir su información de forma segura mediante la seguridad del documento.
seo-description: Descubra cómo puede crear, almacenar y aplicar parámetros de confidencialidad predefinidos, y distribuir su información de forma segura mediante la seguridad del documento.
uuid: e4fba2a4-f3c1-4b20-8e05-8e241b40ebd0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1820cb38-ba70-4cce-8895-290524bdd9bf
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '2546'
ht-degree: 0%

---


# Acerca de la seguridad de documento {#about-document-security}

La seguridad de documento garantiza que solo los usuarios autorizados puedan utilizar sus documentos. Con la seguridad de documento, puede distribuir con seguridad cualquier información que haya guardado en un formato compatible. Los formatos de archivo admitidos son:

* Archivos Adobe PDF
* Archivos de Microsoft® Word, Excel y PowerPoint

Para obtener más información sobre cómo las políticas protegen los tipos de archivo admitidos, consulte [Información de seguridad de documento adicional](https://www.adobe.com/go/learn_aemforms_doc_security_63).

Con la seguridad de documento, puede crear, almacenar y aplicar fácilmente parámetros de confidencialidad predefinidos a sus documentos. Para evitar que la información se extienda más allá de su alcance, también puede monitorear y controlar cómo los destinatarios utilizan sus documentos después de distribuirlos.

Puede proteger documentos mediante políticas. Una *directiva* es una recopilación de información que incluye parámetros de confidencialidad y una lista de usuarios autorizados. La configuración de confidencialidad que especifique en una política determinará cómo puede un destinatario utilizar un documento al que aplique la política. Por ejemplo, puede especificar si los destinatarios pueden imprimir o copiar texto, editar texto o agregar firmas y comentarios a documentos protegidos.

Los usuarios de seguridad de documento crean políticas a través de las páginas web del usuario final. Los administradores utilizan las páginas web de seguridad de documento para crear conjuntos de políticas que contengan directivas compartidas disponibles para todos los usuarios autorizados.

Aunque las directivas se almacenan en seguridad de documento, se aplican a los documentos a través de la aplicación cliente. La forma de aplicar políticas a documentos PDF se describe en detalle en *Ayuda de Acrobat*. La aplicación de políticas mediante otras aplicaciones, como Microsoft Office, se documenta en la *Ayuda de extensiones de Acrobat Reader DC* para la aplicación.

Cuando se aplica una política a un documento, la configuración de confidencialidad especificada en la política protege la información que contiene el documento. La configuración de confidencialidad también protege cualquier archivo (texto, audio o vídeo) dentro de un documento PDF. Puede distribuir el documento protegido por una política a destinatarios autorizados por la política.

**Control de acceso y auditoría de documentos**

El uso de una política para proteger un documento le permite controlar ese documento, incluso después de distribuirlo. Puede supervisar el documento, realizar cambios en la política, evitar que los usuarios sigan teniendo acceso al documento y cambiar la política aplicada al documento.

Mediante la seguridad de documento, puede supervisar documentos protegidos por políticas y rastrear eventos, como cuando un usuario autorizado o no autorizado intenta abrir el documento.

**Componentes**

La seguridad de documento consiste en un servidor y una interfaz de usuario:

**Servidor:** el componente central mediante el cual la seguridad de documento realiza transacciones como autenticación de usuarios, administración en tiempo real de políticas y aplicación de confidencialidad. El servidor también proporciona un repositorio central para directivas, registros de auditoría y otra información relacionada.

**Páginas Web:** la interfaz en la que se crean las políticas, se administran los documentos protegidos por políticas y se supervisan los eventos asociados a documentos protegidos por políticas. Los administradores también pueden configurar opciones globales como autenticación de usuarios, auditoría y mensajería para los usuarios invitados, y administrar las cuentas de usuario invitadas.

![rm_psworkflow](assets/rm_psworkflow.png)

Los pasos de la ilustración son los siguientes:

1. El propietario del documento crea directivas mediante las páginas web. Los propietarios de los documentos pueden crear políticas personales a las que solo puedan acceder. Los administradores y coordinadores de conjuntos de políticas pueden crear políticas compartidas dentro de conjuntos de políticas a las que los usuarios autorizados tengan acceso.
1. El propietario del documento aplica la política y, a continuación, guarda y distribuye el documento. El documento se puede distribuir por correo electrónico, a través de una carpeta de red o en un sitio web.
1. El destinatario abre el documento en la aplicación cliente adecuada. El destinatario puede utilizar el documento según su política.
1. El propietario del documento, el coordinador del conjunto de políticas o el administrador pueden rastrear documentos y modificar el acceso a ellos mediante las páginas web.

## Acerca de los usuarios de seguridad de documento {#about-document-security-users}

Varios tipos de usuarios trabajan con la seguridad de documento para lograr diferentes tareas:

* El administrador del sistema u otra persona de sistemas de información (IS) instala y configura la seguridad del documento. Esta persona también puede ser responsable de configurar la configuración global del servidor, las páginas web y las políticas y documentos.

   Esta configuración puede incluir, por ejemplo, una URL de seguridad de documento base, notificaciones de auditoría y privacidad, avisos de registro de usuarios invitados y períodos de concesión sin conexión predeterminados.

* Los administradores de seguridad de documento crean políticas y conjuntos de políticas, y administran documentos protegidos por políticas para los usuarios según sea necesario. También crean cuentas de usuario invitadas y supervisan el sistema, el documento, el usuario, la política, el conjunto de políticas y los eventos personalizados. También pueden ser responsables de configurar el servidor global, la página Web y la configuración de directivas junto con un administrador del sistema.

   Los administradores pueden asignar a los usuarios las siguientes funciones en el área Administración de usuarios de la consola de administración. Los usuarios asignados a estas funciones realizan sus tareas en el área de la interfaz de usuario de seguridad de documento de la consola de administración.

   **Superadministrador de seguridad de documento**

   Los usuarios con esta función tienen acceso a todas las configuraciones de seguridad de documento de la consola de administración. Estos permisos están asociados a la función:

   * Administrar configuración
   * Administrar directiva
   * Administrar conjuntos de políticas
   * Administrar documentos
   * Administrar editores de documento
   * Administrar usuarios invitados y locales
   * Eventos de vista
   * Delegar
   * Invitar a usuarios externos

   **Administrador de seguridad de documento**

   Los usuarios con esta función pueden configurar el servidor de seguridad de documento mediante la página Configuración de la sección Seguridad de documento de la consola de administración. Este permiso está asociado con la función Administrar configuración.

   >[!NOTE]
   >
   >Los usuarios con esta función también deben tener la función de usuario de la consola de administración para poder iniciar sesión en la consola de administración y editar cualquier configuración relacionada con la configuración.

   **Administrador del conjunto de directivas de seguridad de documento**

   Los usuarios con esta función pueden utilizar la sección de seguridad de documento de la consola de administración para editar las políticas de otros usuarios y para crear, editar y eliminar conjuntos de políticas. Cuando un administrador de conjuntos de directivas crea un conjunto de directivas, puede asignar un coordinador de conjuntos de directivas a ese conjunto de directivas. Estos permisos están asociados a la función:

   * Administrar directiva
   * Administrar conjuntos de políticas
   * Administrar documentos
   * Administrar editores de documento
   * Eventos de vista
   * Delegar

   >[!NOTE]
   >
   >Los usuarios con esta función también deben tener la función de usuario de la consola de administración para poder iniciar sesión en la consola de administración y editar cualquier configuración relacionada con la configuración.

   **Seguridad de documento gestiona los usuarios invitados y locales**

   Los usuarios con esta función pueden realizar tareas necesarias para administrar todos los usuarios invitados y locales en las páginas web de seguridad de documento relevantes. Estos permisos están asociados a la función:

   * Administrar usuarios invitados y locales
   * Invitar a usuarios externos
   * Acceso a las páginas web de los usuarios finales

   >[!NOTE]
   >
   >Los usuarios con esta función también deben tener la función de usuario de la consola de administración para poder iniciar sesión en la consola de administración y editar cualquier configuración relacionada con la configuración.

   **Usuario de invitación de seguridad de documento**

   Los usuarios con esta función pueden invitar a usuarios. Estos permisos están asociados a la función:

   * Invitar a usuarios externos
   * Acceso a las páginas web de los usuarios finales

   **Usuario final de seguridad de documento**

   Los usuarios con esta función pueden acceder a las páginas web del usuario final de documento Security. Esta función también se puede asignar a los administradores para que puedan crear políticas mediante las páginas de usuario final. Este permiso está asociado con la función Acceso a páginas web de usuarios finales.

* Los usuarios dentro de la organización que tienen cuentas de seguridad de documento válidas crean sus propias políticas, utilizan políticas para proteger documentos, rastrean y administran sus documentos protegidos por políticas y supervisan eventos relacionados con sus documentos.
* Los coordinadores de conjuntos de políticas administran documentos, eventos de vista y otros coordinadores de conjuntos de políticas (según sus permisos). Los administradores designan a los usuarios como coordinadores de conjuntos de políticas para conjuntos de políticas específicos.
* Los usuarios externos a su organización (por ejemplo, un socio comercial) pueden utilizar documentos protegidos por políticas si se encuentran en el directorio de seguridad del documento de seguridad de documento, si el administrador crea una cuenta para ellos o si se registran con seguridad de documento mediante un proceso automatizado de invitación por correo electrónico. Según cómo habilite el administrador la configuración de acceso, los usuarios invitados también pueden tener permiso para aplicar políticas a documentos, crear, modificar y eliminar sus políticas e invitar a otros usuarios externos a utilizar sus documentos protegidos por políticas.
* Los desarrolladores utilizan el SDK de formularios AEM para integrar aplicaciones personalizadas con seguridad de documento.

Los administradores de seguridad de documento pueden crear funciones personalizadas mediante los siguientes permisos en Administración de usuarios:

* Configuración de documento security Manage
* Seguridad de documento Administrar usuarios invitados y locales
* Seguridad de documento Administrar conjuntos de directivas
* Seguridad de documento Administrar conjuntos de directivas
* Eventos del servidor de Vista de seguridad de documento
* Propietario de la directiva de cambio de seguridad de documento

## Políticas y documentos protegidos por políticas {#policies-and-policy-protected-documents}

Una *directiva* define un conjunto de configuraciones de confidencialidad y usuarios que pueden acceder a un documento al que se aplica la directiva. Una directiva también permite cambiar dinámicamente los permisos de un documento. Proporciona a la persona que asegura el permiso del documento para cambiar los parámetros de confidencialidad para anular el acceso al documento o cambiar la política.

La protección de políticas se puede aplicar a un documento PDF mediante Adobe Acrobat® Pro y Acrobat Standard. La protección de políticas se puede aplicar a otros tipos de archivos, como archivos de Microsoft Word, Excel y PowerPoint, mediante la aplicación cliente con las extensiones de Acrobat Reader DC adecuadas instaladas.

### Cómo funcionan las políticas {#how-policies-work}

Las políticas contienen información sobre los usuarios autorizados y los parámetros de confidencialidad que se aplican a los documentos. Los usuarios pueden ser cualquiera en su organización, así como personas externas a su organización que tengan una cuenta. Si el administrador habilita la función de invitación de usuario, es posible agregar nuevos usuarios a las directivas, iniciando así un proceso de correo electrónico de invitación de registro.

La configuración de confidencialidad de una directiva determina cómo pueden utilizar el documento los destinatarios. Por ejemplo, puede especificar si los destinatarios pueden imprimir o copiar texto, realizar cambios o agregar firmas y comentarios a documentos protegidos. La misma directiva también puede especificar diferentes parámetros de confidencialidad para usuarios específicos.

>[!NOTE]
>
>La configuración de confidencialidad que se aplica mediante una política anula cualquier configuración que se haya aplicado a un documento PDF en Acrobat mediante las opciones de seguridad de certificado o contraseña. (Consulte la Ayuda de Acrobat para obtener más información).

Los usuarios y administradores crean políticas a través de las páginas web de seguridad de documento. Solo se puede aplicar una política a la vez a un documento. Puede aplicar una política mediante uno de estos métodos:

* Abra el documento en Acrobat u otra aplicación cliente y seleccione una política para proteger el documento.
* Enviar un documento como archivo adjunto de correo electrónico en Microsoft Outlook. En este caso, puede seleccionar una directiva de una lista de directivas o seleccionar una directiva generada automáticamente que Acrobat cree con un conjunto predeterminado de parámetros de confidencialidad para proteger el documento únicamente para los destinatarios de mensajes de correo electrónico.

Una directiva se puede eliminar de un documento mediante la aplicación cliente.

![rm_sonline_policy](assets/rm_psonline_policy.png)

Los pasos del diagrama son los siguientes:

1. El propietario del documento protege el documento de una aplicación cliente admitida con una política que permite el uso en línea.
1. La seguridad de documento crea una licencia de documento y claves de documento, y cifra la directiva. La licencia de documento, la directiva cifrada y la clave de documento se devuelven a la aplicación cliente.
1. El documento se cifra con la clave de documento y la clave de documento se descarta. El documento ahora incorpora la licencia y la política. Estas tareas se realizan en la aplicación cliente admitida.

Cuando se aplica una política a un documento, la información que contiene el documento, incluidos los archivos contenidos (texto, audio o vídeo) en los documentos PDF, está protegida por la configuración de confidencialidad especificada en la política. La seguridad de documento genera una licencia e información de cifrado que luego se incrusta en el documento. Al distribuir el documento, la seguridad de documento puede autenticar a los destinatarios que intentan abrir el documento y autorizar el acceso de acuerdo con los privilegios especificados en la política.

Si el uso sin conexión está activado, los destinatarios también pueden utilizar documentos protegidos por políticas sin conexión (sin una conexión activa a Internet o a la red) durante el período de tiempo especificado en la política.

### Cómo funcionan los documentos protegidos por políticas {#how-policy-protected-documents-work}

Para abrir y utilizar documentos protegidos por políticas, la política debe incluir su nombre como destinatario y debe tener una cuenta de seguridad de documento válida. Para documentos PDF, necesita Acrobat o Adobe Reader®. Para otros tipos de archivos, necesita la aplicación adecuada para el archivo con las extensiones de Acrobat Reader DC instaladas.

Al intentar abrir un documento protegido por una política, Acrobat, Adobe Reader o las extensiones de Acrobat Reader DC se conectan a la seguridad de documento para autenticarlo. A continuación, puede iniciar sesión. Si se está auditando el uso del documento, aparece un mensaje de notificación. Una vez que la seguridad de documento determina qué permisos de documento conceder, administra el descifrado del documento. A continuación, puede utilizar el documento según los parámetros de confidencialidad de la política.

![rm_psopen_online](assets/rm_psopen_online.png)

Los pasos del diagrama son los siguientes:

1. El usuario de documento abre el documento en una aplicación cliente admitida y se autentica con el servidor. El identificador de documento se envía al servidor de seguridad de documento.
1. La seguridad de documento autentica a los usuarios, comprueba la directiva para obtener autorización y crea una licencia. El asiento (que contiene la clave de documento y los permisos) se devuelve a la aplicación cliente.
1. El documento se descifra con la clave de documento y se descarta la clave de documento. El documento se puede utilizar de acuerdo con los parámetros de confidencialidad de la política. Estas tareas se realizan en la aplicación cliente admitida.

Puede seguir utilizando un documento en estas condiciones:

* Indefinidamente o para el período de validez especificado en la directiva
* Hasta que el administrador o la persona que aplicó la política anulen el acceso al documento o cambien la política

También puede utilizar documentos protegidos por políticas sin conexión (sin conexión a Internet o a la red) si la política permite el acceso sin conexión. Primero debe iniciar sesión en documento security para sincronizar el documento. A continuación, puede utilizar el documento durante el período de concesión sin conexión especificado en la política.

Cuando finaliza el período de concesión sin conexión, debe volver a sincronizar el documento con la seguridad de documento, ya sea conectándose y abriendo un documento protegido por una política o utilizando un comando en la aplicación cliente. (Consulte *Ayuda de Acrobat* o la *Ayuda de extensiones de Acrobat Reader DC* correspondiente para obtener más información).

Si guarda una copia de un documento protegido por una política mediante el comando de menú Guardar o Guardar como, la política se aplica automáticamente y se aplica para el nuevo documento. Eventos como los intentos de abrir el nuevo documento también se auditan y registran para el documento original.

## Conjuntos de directivas {#policy-sets}

*Los* conjuntos de políticas se utilizan para agrupar un conjunto de políticas que tienen un propósito comercial común. Estos conjuntos de políticas se ponen a disposición de un subconjunto de usuarios del sistema.

Cada conjunto de políticas puede tener uno o más coordinadores de conjuntos de políticas asociados. El coordinador de conjuntos de políticas es un administrador o un usuario que tiene permisos adicionales. El *coordinador de conjuntos de políticas* es normalmente un especialista de la organización que puede crear mejor las políticas en un conjunto de políticas en particular.

Los coordinadores de conjuntos de políticas pueden realizar las siguientes tareas:

* Crear nuevas directivas
* Editar y eliminar cualquier directiva del conjunto de directivas
* Editar la configuración del conjunto de directivas
* Añadir y eliminar coordinadores de conjuntos de políticas
* Eventos de política de vista y documento para cualquier política o documento dentro del conjunto de políticas
* Revocar acceso a documentos
* Cambiar directivas para el documento.

Los administradores y coordinadores de conjuntos de políticas que tienen permiso para hacerlo crean y eliminan conjuntos de políticas en las páginas web de la administración de seguridad de documento.

Los conjuntos de políticas generalmente están disponibles para un número limitado de usuarios al especificar qué usuarios o grupos dentro de un dominio pueden utilizar las políticas del conjunto de políticas para proteger documentos.

Cuando se instala la seguridad de documento, se crea un conjunto de directivas predeterminado denominado *Conjunto de directivas globales*. El administrador que instaló el software administra este conjunto de directivas.
