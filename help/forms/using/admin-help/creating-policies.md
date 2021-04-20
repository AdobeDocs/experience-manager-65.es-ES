---
title: Creación y administración de políticas
seo-title: Creación y administración de políticas
description: Una directiva es un conjunto de configuraciones de confidencialidad y usuarios que pueden acceder a un documento al que se aplica la directiva. Puede crear y administrar varios tipos de políticas mediante AEM formularios.
seo-description: Una directiva es un conjunto de configuraciones de confidencialidad y usuarios que pueden acceder a un documento al que se aplica la directiva. Puede crear y administrar varios tipos de políticas mediante AEM formularios.
uuid: 72be06f3-3e90-495e-8425-72380d95704a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fa054d30-c7dc-4b64-acf1-cbcbe8827df5
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '4757'
ht-degree: 0%

---


# Creación y administración de directivas {#creating-and-managing-policies}

Una *directiva* define un conjunto de configuraciones de confidencialidad y usuarios que pueden acceder a un documento al que se aplica la directiva. Se utiliza un *conjunto de directivas* para agrupar un conjunto de directivas que tienen un propósito comercial común. Estos conjuntos de políticas se ponen a disposición de un subconjunto de usuarios del sistema. Para obtener más información sobre las políticas, consulte [Directivas y documentos protegidos por políticas](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents).

## Tipos de directivas {#types-of-policies}

La seguridad de los documentos proporciona los siguientes tipos de directivas.

**Políticas personales**

Los usuarios pueden crear, editar, copiar, eliminar y aplicar sus propias directivas con una configuración adecuada para una situación concreta. Solo la persona que crea una directiva y los administradores pueden acceder a ella. Las políticas personales aparecen en la ficha Mis políticas de la página Políticas.

Los usuarios invitados también pueden crear, editar, copiar y eliminar directivas personales si el administrador habilita esta capacidad.

**Políticas compartidas**

Los administradores y los coordinadores de conjuntos de políticas crean políticas compartidas basadas en los requisitos de confidencialidad que su organización identifica para diferentes tipos de documentos y usuarios. Las políticas compartidas están incluidas en conjuntos de políticas y están disponibles para todos los usuarios autorizados (editores de documentos, coordinadores de conjuntos de políticas y destinatarios de documentos) para un conjunto de políticas determinado. Los administradores y los coordinadores de conjuntos de políticas pueden habilitar y deshabilitar las directivas compartidas. Las políticas compartidas aparecen en los conjuntos de directivas en la ficha Conjuntos de directivas de la página Directivas.

Cuando instala por primera vez la seguridad del documento, contiene una directiva compartida, denominada *Restrict to All Principals*. Cuando esta directiva se aplica a un documento, cualquier usuario que pueda iniciar sesión en document security puede acceder al documento. Esta directiva se encuentra en el conjunto de directivas denominado *Conjunto de directivas globales*. De forma predeterminada, esta directiva no está habilitada. Puede habilitarlo si se adapta a las necesidades de su organización.

**Políticas autogeneradas de Microsoft Outlook**

Con Acrobat, puede aplicar directivas a documentos que envíe como archivos adjuntos de correo electrónico en Microsoft Outlook. En Outlook, puede proteger un documento utilizando una directiva existente o utilizando una directiva generada automáticamente que Acrobat genera con la configuración de confidencialidad predeterminada y se aplica al documento adjunto a un mensaje de correo electrónico. (Consulte *[Ayuda de Acrobat](https://help.adobe.com/en_US/acrobat/pro/using/index.html)*).

>[!NOTE]
>
>Para que una directiva esté disponible en Outlook, debe definirla como favorita en Acrobat. Todas las demás directivas, incluidas las que haya aplicado como Publicador, no se muestran en Outlook.

## Quién puede crear y administrar políticas y conjuntos de políticas {#who-can-create-and-manage-policies-and-policy-sets}

La forma en que interactúa con las políticas y los conjuntos de políticas depende de su función dentro de la organización:

**Usuarios:** los usuarios pueden crear, editar y eliminar sus políticas personales. Los usuarios invitados también pueden crear políticas personales si el administrador habilita esta capacidad.

**Coordinadores de conjuntos de políticas:**  Los coordinadores de conjuntos de políticas pueden crear y administrar políticas compartidas dentro de los conjuntos de políticas donde se les designa como coordinadores. Un coordinador de conjuntos de políticas suele ser un especialista de la organización que puede crear mejor las políticas en un conjunto de políticas determinado.

**Administradores:** los administradores pueden editar las políticas personales de cualquier usuario. Pueden crear políticas compartidas. También pueden crear, editar y eliminar conjuntos de políticas y designar coordinadores de conjuntos de políticas.

Para obtener más información sobre las distintas funciones de seguridad del documento, consulte [Acerca de los usuarios de seguridad del documento](/help/forms/using/admin-help/document-security.md#about-document-security-users).

## Creación y edición de directivas {#creating-and-editing-policies}

Los usuarios pueden crear o editar políticas personales para su propio uso. Los administradores y los coordinadores de conjuntos de políticas pueden crear o editar directivas compartidas para su organización.

### Consideraciones para editar directivas {#considerations-for-editing-policies}

Cuando edita una directiva, los cambios afectan a los documentos que la directiva protege actualmente, así como a los documentos que la directiva protege posteriormente. Por ejemplo, si elimina los destinatarios de una directiva que se aplica actualmente a un documento, los destinatarios ya no podrán abrir el documento.

El estado del documento determina cuándo tiene efecto el cambio:

* Si el documento está en línea, los cambios se aplican inmediatamente a menos que el usuario tenga el documento abierto. En este caso, el usuario debe cerrar el documento para que los cambios surtan efecto.
* Si un destinatario está utilizando el documento sin conexión (por ejemplo, en un equipo portátil), los cambios surten efecto la próxima vez que el destinatario ponga el documento en línea y se sincronice con la seguridad del documento abriendo cualquier documento protegido por políticas.

>[!NOTE]
>
>Las directivas que Acrobat genera automáticamente para los destinatarios de documentos adjuntos a mensajes de correo electrónico en Microsoft Outlook no aparecen en la lista de directivas. Para ver estas directivas, abra la página Detalles del documento del documento asociado.

Cuando edita las directivas, se aplican estas restricciones:

* Los usuarios invitados solo pueden editar directivas si el administrador habilita esta capacidad. Si no puede editar directivas, la opción Editar no estará disponible.
* Los coordinadores de conjuntos de políticas solo pueden editar directivas dentro de conjuntos de directivas si tienen los permisos correctos. El superusuario o el administrador del conjunto de directivas establecen estos permisos en la interfaz del administrador de seguridad de documentos.
* Si la directiva tiene una marca de agua configurada que el administrador eliminó desde que se creó la directiva, esta marca de agua ya no se aplicará a los documentos si edita y guarda la directiva. Las marcas de agua eliminadas siguen vigentes solo para las políticas existentes, siempre que no edite la directiva. Si edita la directiva, debe seleccionar otra marca de agua para reemplazar la eliminada.
* No se puede conceder acceso anónimo a un documento editando la directiva que se aplica actualmente. Si edita la directiva, los usuarios deben iniciar sesión para acceder al documento. Para aplicar acceso anónimo a este documento, primero elimine la directiva en la aplicación cliente y luego aplique otra directiva que permita el acceso anónimo.
* Las directivas que Acrobat genera automáticamente para los destinatarios de un documento que está adjunto a un mensaje de correo electrónico en Microsoft Outlook no aparecen en la lista de directivas. Para acceder a esta directiva, localice el documento en la página Documentos, abra la página Detalles del documento y haga clic en el nombre de la directiva en la lista de detalles del documento.

**Crear o editar una directiva**

1. En la página de seguridad del documento, haga clic en Directivas y, a continuación, haga clic en una de estas pestañas:

   * Para crear o editar una directiva personal, haga clic en la pestaña My Policy .
   * Para crear o editar una directiva compartida, si tiene permiso, haga clic en la ficha Conjuntos de políticas y en el nombre del conjunto de directivas correspondiente y, a continuación, haga clic en la ficha Directivas .

1. Haga clic en Nuevo o seleccione la política que desee editar en la lista.
1. En el cuadro Nombre, escriba un nombre que identifique la política de forma única. En el cuadro Descripción, describa lo que hace la política y cuándo utilizarla. Si la directiva se encuentra dentro de un conjunto de directivas, el nombre y la descripción aparecerán en la lista de directivas de todos los usuarios especificados. Las políticas personales solo están disponibles para el usuario y los administradores.

   No se pueden usar los caracteres siguientes en el nombre o la descripción:

   * Signo menor que (&lt;)
   * Signo bueno que (>)
   * y comercial (&amp;)
   * Comilla tipográfica simple (&#39;)
   * Comilla tipográfica doble (&quot;)
   * Barra invertida (\)
   * barra diagonal (/)

   Si utiliza el siguiente carácter en el nombre o la descripción, se convierten en espacios:

   * retorno de carro (carácter ASCII 13)
   * nueva línea (carácter ASCII 10).

   >[!NOTE]
   >
   >Puede crear un nombre de directiva que contenga caracteres extendidos; sin embargo, cuando se realiza una comparación entre dos cadenas, los caracteres acentuados y no acentuados como &quot;e&quot; y &quot;é&quot; se consideran iguales. Cuando alguien crea una directiva, se realiza una comparación para comprobar si ya existe una directiva con el mismo nombre. La comparación no puede distinguir entre nombres que sean iguales excepto para caracteres acentuados. Se da por hecho que la política ya se ha agregado a la base de datos y que la nueva no se ha añadido.

1. Agregue usuarios y grupos a la directiva y establezca los permisos adecuados. (Consulte [Usuarios y grupos](creating-policies.md#users-and-groups)).
1. En Configuración general, seleccione las opciones adecuadas. (Consulte [Configuración general](creating-policies.md#general-settings)).
1. (Opcional) Si corresponde, seleccione un proveedor de autorización externo y especifique sus propiedades. Si no desea utilizar un proveedor de autorización externo, haga clic en Quitar proveedor predeterminado.

   Un proveedor de autorización externo se utiliza para configurar propiedades dentro de la directiva y, cuando se selecciona, el proveedor de autorización externo utiliza esta información para evaluar la directiva. El administrador y la persona que instala el software configuran las propiedades disponibles.

1. En Configuración avanzada, seleccione las opciones adecuadas. (Consulte [Configuración avanzada](creating-policies.md#advanced-settings)).
1. En Configuración avanzada inmodificable, seleccione las opciones adecuadas. (Consulte [Configuración avanzada inmodificable](creating-policies.md#unchangeable-advanced-settings)).
1. Haga clic en Guardar. La directiva aparece en la lista de directivas. Al lado de la nueva directiva aparece un icono con un círculo rojo que indica que aún está desactivado.

   Para que la directiva esté disponible para los usuarios, actívela. (Consulte [Habilitar o deshabilitar directivas compartidas](creating-policies.md#enable-or-disable-shared-policies)).

### Usuarios y grupos {#users-and-groups}

En el área Usuarios y grupos , especifique los usuarios que tienen acceso a los documentos protegidos con la directiva. Para cada usuario o grupo que especifique, también debe establecer los privilegios de uso del documento.

>[!NOTE]
>
>El editor del documento es el usuario que protege el documento con la directiva. Este usuario siempre se incluye de forma predeterminada en una directiva, con derechos de acceso completos, incluidas las capacidades de revocación y conmutación de políticas. Sin embargo, los administradores pueden cambiar los derechos de acceso del editor del documento para las directivas compartidas. Por ejemplo, el administrador puede restringir el editor del documento para que no revoque el acceso al documento o cambie la directiva.

**Agregar usuario o grupo:** para agregar un usuario o grupo de usuarios, haga clic en Agregar usuario o grupo y, después, haga clic en Búsqueda avanzada para encontrar usuarios o grupos. Los usuarios incluyen a los usuarios internos de su organización y a los usuarios invitados que se han registrado con seguridad de documentos. Cuando selecciona esta opción, aparece la página Agregar usuario o grupo :

* En el cuadro Buscar, escriba el nombre de usuario o grupo o la dirección de correo electrónico.
* En la lista Uso, seleccione Nombre o Correo electrónico.
* En la lista Tipo, seleccione Usuario o Grupo.
* Seleccione el dominio que desea buscar en la lista En y haga clic en Buscar.
* Cuando devuelvan los resultados, seleccione el usuario o grupo que desee añadir y haga clic en Agregar.

>[!NOTE]
>
>Si introduce un nombre de usuario o una dirección de correo electrónico invitados correctos y no se devuelve ningún resultado, es posible que el usuario no se haya registrado aún o que la cuenta se elimine. Puede intentar agregar el usuario como un tipo de usuario invitado o ponerse en contacto con el administrador.

**Invitar nuevo usuario:** para agregar un usuario invitado, haga clic en Invitar nuevo usuario, escriba la dirección de correo electrónico del usuario en el cuadro que aparece y haga clic en Invitar. Esta opción solo está disponible si el administrador la ha activado. Cuando se añaden nuevos usuarios invitados a una directiva, document security envía un correo electrónico de invitación de registro si los usuarios no están invitados a registrarse. Los usuarios deben utilizar el vínculo del correo electrónico para crear una cuenta y luego deben activarla.

Después de registrarse, los usuarios invitados pueden utilizar documentos protegidos por políticas para los que tienen autorización. Según las capacidades que habilite el administrador, los usuarios externos pueden tener permiso para aplicar directivas a documentos, crear, editar y eliminar directivas, y agregar otros usuarios externos a directivas.

**Agregar usuario anónimo:** para permitir el acceso de usuarios anónimos, haga clic en Agregar usuario anónimo. Esta opción solo está disponible si el administrador ha habilitado el acceso de usuario anónimo para la seguridad de documentos. (Consulte Configuración del servidor de seguridad de documentos). Esta opción concede a todos el acceso a los documentos protegidos por esta directiva, independientemente de si tienen una cuenta de seguridad de documento. Si selecciona esta opción, no podrá agregar otros tipos de usuarios a la directiva.

>[!NOTE]
>
>Para permitir el acceso anónimo a un documento protegido por políticas que actualmente no lo tiene, elimine la política existente y luego aplique una política que permita el acceso anónimo. Si cambia o cambia la directiva existente, los usuarios deben iniciar sesión para acceder al documento.

#### Especifique los permisos del documento para usuarios y grupos {#specify-the-document-permissions-for-users-and-groups}

Puede especificar permisos de documento para un usuario o grupo a la vez, o puede seleccionar varios usuarios y grupos de la lista y cambiar sus permisos mediante las opciones del área de encabezados de columna.

De forma predeterminada, todos los documentos protegidos por políticas tienen un permiso que permite a los usuarios abrirlos mientras están en línea.

La ficha Permisos y opciones se muestra en seguridad del documento.

Estos permisos de documento están disponibles en la ficha Permisos. Puede aplicar estos permisos a archivos PDF, PTC Pro/E y Microsoft Office.

**Imprimir:** permite al usuario imprimir un documento protegido con esta directiva. Para los archivos Office y Pro/E, puede seleccionar la casilla de verificación Imprimir para permitir la impresión, o borrarla para evitar la impresión. Si selecciona la casilla de verificación Mostrar permisos personalizados para PDF, puede seleccionar una de estas opciones:

**No permitido:** el usuario no puede imprimir el PDF.

**Permitido:** el usuario puede imprimir el PDF.

**Baja resolución. solo:** El usuario puede imprimir el PDF a baja resolución.

**Modificar:** permite al usuario modificar un documento protegido con esta directiva. Para los archivos Office y Pro/E, puede seleccionar la casilla de verificación Modificar para permitir modificaciones o desactivarla para evitar modificaciones. Si selecciona la casilla de verificación Mostrar permisos personalizados para PDF, puede seleccionar una de estas opciones:

**No permitido:** el usuario no puede modificar el PDF.

**Cualquiera:** el usuario puede modificar el PDF.

**Colaborar:** el usuario puede colaborar con otros mediante las opciones Colaborar en Adobe Acrobat. Este permiso permite al usuario copiar datos de formulario incluso si el permiso Copiar no se proporciona explícitamente en la directiva.

**Modificar páginas:** el usuario puede agregar y eliminar páginas y editar contenido en el PDF.

**Fill &amp; Sign:** el usuario puede rellenar los campos del formulario en el PDF y firmarlo.

**Copiar:** permite al usuario copiar texto de un documento protegido con esta directiva.

**Reader de pantalla:** este permiso se muestra si selecciona la casilla de verificación Mostrar permisos personalizados para PDF. Cuando se selecciona esta opción, Adobe Acrobat tiene permiso para añadir etiquetas temporales al PDF para mejorar su legibilidad con un lector de pantalla.

Estos permisos de documento están disponibles en la ficha Opciones. Puede aplicar estos permisos a archivos PDF, PTC Pro/E y Microsoft Office:

**Sin conexión:** permite al usuario ver un documento sin conexión protegido con esta directiva.

**Validez de permisos:** seleccione Los permisos son siempre válidos o establezca un periodo de validez de permisos de documentos. Si selecciona un periodo de validez, haga clic en los iconos del calendario para seleccionar una fecha y utilice las flechas para especificar la hora en formato de 24 horas.

En el caso de las directivas compartidas, los administradores pueden desactivar los siguientes privilegios para el editor del documento (el usuario que aplica la directiva a un documento):

**Revocar:** permite que el editor del documento revoque los privilegios de acceso al documento.

**Cambiar:** permite que el editor del documento cambie de privilegios de directiva.

### Configuración general {#general-settings}

El área Configuración general contiene los siguientes ajustes:

**Periodo de validez:** periodo de tiempo durante el cual los destinatarios autorizados pueden acceder al documento protegido por políticas. Puede elegir entre estas opciones de periodo de validez:

**El documento no será válido después de:** el documento es accesible durante el número especificado de días desde el momento en que se protegió el documento.

**El documento no será válido después de esta fecha:** el documento es válido desde la fecha en que se aplica la política al documento hasta la fecha de finalización especificada.

**Válido de, a:** El documento es válido durante las fechas especificadas. Puede utilizar el calendario para seleccionar una fecha, si corresponde, haciendo clic en el icono de calendario.

**El documento siempre es válido:** el periodo de validez del documento no caduca.

>[!NOTE]
>
>Las fechas de validez se basan en la zona horaria del sistema de seguridad de documentos, no en la del equipo local.

**Auditoría:** habilite o deshabilite la auditoría de los eventos asociados a un documento protegido por políticas. Por ejemplo, la seguridad de los documentos puede registrar eventos como intentos de abrir un documento. Los eventos auditados aparecen en la lista de la página Eventos . Si no selecciona esta opción, document security no registra eventos para documentos asociados a la directiva.

>[!NOTE]
>
>El administrador también debe habilitar la auditoría del servidor en la página de configuración de Auditoría y Configuración de privacidad para que funcione la función de auditoría.

**Seguimiento de uso extendido:** habilite o deshabilite el seguimiento de uso extendido. la seguridad del documento admite el seguimiento de eventos de usuario asociados con diversas operaciones realizadas en un archivo PDF. Se puede acceder al objeto de seguridad del documento mediante un JavaScript. Un clic en un botón, un archivo multimedia que se está reproduciendo o el guardado de un archivo son algunos ejemplos de eventos que se pueden activar desde un PDF protegido por políticas. Con el objeto de seguridad del documento, también se puede recuperar información de usuario. El seguimiento de eventos puede habilitarse desde el servidor de seguridad de documentos a nivel global o a nivel de directiva.

**Periodo de arrendamiento sin conexión automática:** el número máximo de días que el destinatario puede utilizar el documento protegido por políticas sin conexión (sin una conexión activa a Internet o a la red). Cuando caduca el periodo de arrendamiento, el destinatario debe sincronizar de nuevo el documento para seguir utilizándolo.

### Proveedores de autorización externa {#external-authorization-providers}

Seleccione los proveedores de autenticación externos si ya ha configurado alguno. Se muestran los proveedores disponibles.

### Configuración de autenticación {#authentication-settings}

Puede anular la configuración de autenticación que configuró en el servidor y especificar las opciones de autenticación relevantes para esta directiva. Seleccione Omitir configuración de autenticación global y, a continuación, seleccione las opciones de autenticación relevantes para esta directiva. Estas son las opciones de autenticación disponibles:

**Permitir autenticación de contraseña de nombre de usuario:** seleccione esta opción para permitir que las aplicaciones cliente utilicen autenticación de nombre de usuario/contraseña al conectarse al servidor.

**Permitir autenticación Kerberos:** seleccione esta opción para permitir que las aplicaciones cliente utilicen autenticación Kerberos al conectarse al servidor.

**Permitir autenticación de certificado de cliente:** seleccione esta opción para permitir que las aplicaciones cliente utilicen autenticación de certificado al conectarse al servidor.

**Permitir** autenticación extendidaSeleccione esta opción para habilitar la autenticación extendida. Al seleccionar esta opción, las aplicaciones cliente pueden utilizar la autenticación extendida. La autenticación extendida proporciona procesos de autenticación personalizados y diferentes opciones de autenticación configuradas en el servidor de seguridad de documentos

Si anula la configuración de autenticación global, puede elegir las opciones de autenticación relevantes para esta directiva. Por ejemplo, si ha habilitado tres opciones de autenticación (nombre de usuario y contraseña, certificado de cliente y autenticación extendida) en el servidor, puede anular esa configuración global y seleccionar solo autenticación extendida para esta directiva. Debe asegurarse de que la opción de autenticación que selecciona aquí ya esté configurada en el servidor. En este ejemplo, no se puede seleccionar Kerberos como opción de autenticación porque no está configurada en el servidor.

>[!NOTE]
>
>La autenticación ampliada es compatible con Apple Mac OS X con Adobe Acrobat versión 11.0.6 y posteriores.

### Configuración avanzada {#advanced-settings}

El área Configuración avanzada contiene los siguientes ajustes:

**Marca de agua dinámica:** seleccione una marca de agua para que se muestre dinámicamente en las páginas de un documento (por ejemplo, cuando un destinatario imprime el documento). Las marcas de agua dinámicas identifican de forma exclusiva un documento, lo que contribuye a garantizar la confidencialidad del documento y a evitar la infracción de los derechos de autor. Por ejemplo, el administrador puede configurar una marca de agua dinámica que muestre la fecha actual, el nombre de usuario o el identificador de la persona que utiliza el documento o el nombre de la política utilizada para protegerlo. Una marca de agua también puede mostrar texto personalizado o elementos gráficos si está configurada. Los administradores configuran las opciones de marcas de agua, y los administradores y usuarios pueden aplicarlas a las políticas.

(Consulte [Configuración de marcas de agua dinámicas](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks)).

Si está editando una directiva y el administrador ha eliminado una marca de agua configurada que seleccionó anteriormente para esta directiva, aparecerá una nota en la página Editar directiva . En este caso, si está guardando el documento editado, seleccione una nueva marca de agua si desea que aparezca en el documento.

>[!NOTE]
>
>En el caso de las políticas que proporcionan acceso anónimo a los usuarios, el nombre de usuario y el identificador de un usuario anónimo no se muestran como marcas de agua aunque seleccione este tipo de marca de agua.

**Usar solo complementos certificados de Acrobat para PDF:**  cuando se selecciona una directiva, esta opción especifica que Acrobat 8.0 y posteriores deben ejecutarse en modo certificado al abrir documentos protegidos con la directiva. Cuando Acrobat se ejecuta en modo certificado, no carga ningún complemento de terceros.

Seleccione esta opción si le preocupa que un destinatario de un documento escriba un complemento que pueda eludir cualquiera de las protecciones de documento en Acrobat 8.0 y posteriores. No seleccione esta opción si los destinatarios del documento necesitan utilizar complementos de terceros en Acrobat para interactuar con documentos.

Esta opción solo habilita el modo certificado en Acrobat 8.0 o posterior; el administrador debe desactivar el acceso para Acrobat 7.0.

(Consulte [Configuración del servidor de seguridad de documentos](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server)).

Esta opción no se aplica a Adobe Reader.

**Mensaje de error de acceso denegado:** mensaje que aparece para cualquiera que intente abrir un documento protegido por políticas sin permiso. Este mensaje aparece en Acrobat. Los clientes que no pueden mostrar este mensaje muestran un mensaje predeterminado para indicar que se ha denegado el acceso.

### Configuración avanzada inmodificable {#unchangeable-advanced-settings}

El área Configuración avanzada inmodificable contiene las siguientes opciones de configuración. No puede cambiar esta configuración después de guardar la directiva.

**Algoritmo de codificación y longitud clave:**  se utiliza para proteger los documentos. Puede elegir entre estas opciones:

* AES de 128 bits
* AES de 256 bits. Solo Acrobat 9.0 y versiones posteriores admiten esta opción. Para utilizar el cifrado AES 256 para archivos PDF, obtenga e instale los archivos de la Extensión de criptografía Java (JCE) Unlimited Strength Jurisdiction Policy . Estos archivos reemplazan los archivos local_policy.jar y US_export_policy.jar en la carpeta [JAVE_HOME]/lib/security. Por ejemplo, si está utilizando Sun JDK 1.6, copie los archivos descargados en la carpeta [dep root]/Java/jdk1.6.0_26/lib/security. Puede descargar estos archivos desde [Java SE Downloads](https://java.sun.com/javase/downloads/index.jsp).
* Sin cifrado. Actualmente, Acrobat 9.0 y las versiones posteriores admiten esta opción. Si selecciona esta opción, las opciones de Restricciones del documento se desactivan. Esta opción puede resultar útil si desea utilizar la seguridad del documento para la auditoría de documentos o el control de versiones, pero no desea cifrar el documento.

**Restricciones del documento:** seleccione los componentes del documento PDF que desea codificar. Otras aplicaciones cliente cifran todo el documento, pero no los archivos vinculados o incrustados. Puede elegir entre estas opciones:

* Todo el documento, incluidos sus archivos adjuntos y metadatos. ** Metadatos muestra información sobre el documento y su contenido que puede ver en el cuadro de diálogo Propiedades del documento o en el menú Avanzadas de Acrobat. En Acrobat, puede adjuntar archivos de distintos tipos (por ejemplo, archivos de texto, audio y vídeo) a documentos PDF.
* El documento y sus archivos adjuntos, pero no los metadatos.
* El documento sólo se adjunta. Puede cifrar los archivos adjuntos en un archivo PDF sin cifrar el contenido del documento.

## Habilitar o deshabilitar directivas compartidas {#enable-or-disable-shared-policies}

Para que una directiva compartida esté disponible, el administrador o el coordinador del conjunto de políticas deben habilitarla. Puede habilitar directivas nuevas o directivas deshabilitadas anteriormente. Una directiva compartida que deshabilite seguirá aplicándose a los documentos protegidos con esa directiva.

Aparece una X roja junto a una directiva deshabilitada.

>[!NOTE]
>
>Los administradores no pueden deshabilitar las políticas personales y los usuarios no pueden habilitar ni deshabilitar sus propias políticas.

1. En la página de seguridad del documento, haga clic en Directivas y, a continuación, en la ficha Conjuntos de directivas.
1. Haga clic en el nombre del conjunto de directivas correspondiente y en la ficha Directivas .
1. Seleccione la casilla de verificación situada junto a la directiva adecuada, haga clic en Activar o Desactivar y, a continuación, haga clic en Aceptar.

## Ver información sobre una directiva {#view-information-about-a-policy}

Con la pestaña Mis políticas , puede buscar políticas personales.

Los conjuntos de directivas que crean los administradores se enumeran en la ficha Conjuntos de directivas de la página Directivas con información sobre el conjunto de directivas, incluido su nombre, la fecha de creación y modificación y una descripción. Haga clic en el nombre de un conjunto de directivas para ver sus detalles. Los coordinadores de conjuntos de políticas que tienen permiso para administrar políticas pueden crear políticas compartidas dentro de un conjunto de políticas en particular.

Cuando crea o edita una directiva, se muestra una página en la que puede configurar detalles como el nombre de la directiva, los niveles de permisos, la configuración de confidencialidad y los destinatarios que desea incluir en la directiva.

El administrador puede configurar las siguientes opciones de confidencialidad para una directiva:

* Opciones generales de confidencialidad de documentos, como el periodo de validez del documento y el periodo de arrendamiento sin conexión
* Los usuarios autorizados y las restricciones y privilegios de documento de cada uno de esos usuarios
* Opciones avanzadas de confidencialidad de documentos, incluidas las marcas de agua dinámicas y el cifrado de documentos

Los usuarios pueden ver las políticas que han creado y las políticas compartidas a las que tienen acceso. Los administradores pueden ver todas las directivas personales y compartidas que se encuentran en seguridad de documentos.

Puede ver información más detallada sobre una directiva que aparece en la lista, incluidos los usuarios o grupos que están incluidos en la directiva y la configuración de confidencialidad especificada para esos usuarios.

>[!NOTE]
>
>Las directivas que Acrobat genera automáticamente para los destinatarios de documentos adjuntos a mensajes de correo electrónico en Microsoft Outlook no aparecen en la lista de directivas. Para ver estas directivas, abra la página Detalles del documento del documento asociado.

1. En la página de seguridad del documento, haga clic en Directivas y, a continuación, en la ficha Mis políticas .
1. Complete la información de búsqueda para buscar políticas personales.
1. Seleccione la política adecuada en la lista.
1. En la página Detalle de la directiva, puede ver detalles sobre la directiva, editarla o ver eventos relacionados con ella.

## Buscar directivas {#search-for-policies}

Los administradores pueden buscar políticas compartidas y políticas personales creadas por otros usuarios.

1. Para buscar una directiva compartida, haga clic en Directivas y, a continuación, en la ficha Conjuntos de directivas . Haga clic en un conjunto de directivas de la lista y, a continuación, haga clic en la ficha Directivas .

   Para buscar una directiva personal, en la página de seguridad del documento, haga clic en Directivas y, a continuación, haga clic en la ficha Mis directivas .

1. En la lista Buscar, seleccione una de estas opciones:

   **ID de directiva:** el número de identificación de la directiva que se genera cuando el usuario crea la directiva. Debe escribir el ID exacto de la directiva.

   **Nombre de directiva:** el nombre de la directiva. Puede buscar parte o todo el nombre de la directiva.

1. En el cuadro de texto, escriba el valor correspondiente. Por ejemplo, si seleccionó Nombre de la directiva, escriba el nombre de la directiva que está buscando.
1. En la lista Mostrar, seleccione el número de resultados que desea mostrar y, a continuación, haga clic en Buscar. Se muestran los resultados de la búsqueda.
1. (Opcional) Para ver los detalles de la directiva, haga clic en ella.

## Copiar una directiva {#copy-a-policy}

Puede copiar una directiva existente y guardarla con un nombre y una descripción nuevos. Copiar directivas es una forma eficaz de crear nuevas directivas mediante la configuración existente.

Los usuarios externos solo pueden copiar directivas si el administrador habilita esta capacidad. Si no puede crear directivas, la opción Copiar no estará disponible.

1. En la página de seguridad del documento, haga clic en Directivas y, a continuación, haga clic en la ficha Mi directiva .
1. Seleccione la política adecuada en la lista.
1. En la página Detalles de directiva , haga clic en Copiar.
1. En el cuadro Nuevo nombre de directiva , escriba el nuevo nombre de la directiva. De forma opcional, escriba una nueva Descripción.

   No se pueden usar los caracteres siguientes en el nombre o la descripción:

   * Signo menor que (&lt;)
   * Signo bueno que (>)
   * y comercial (&amp;)
   * Comilla tipográfica simple (&#39;)
   * Comilla tipográfica doble (&quot;)
   * Barra invertida (\)
   * barra diagonal (/)

   Si utiliza el siguiente carácter en el nombre o la descripción, se convierten en espacios:

   * retorno de carro (carácter ASCII 13)
   * nueva línea (carácter ASCII 10).

   >[!NOTE]
   >
   >Puede crear un nombre de directiva que contenga caracteres extendidos; sin embargo, cuando se realiza una comparación entre dos cadenas, los caracteres acentuados y no acentuados como &quot;e&quot; y &quot;é&quot; se consideran iguales. Cuando alguien crea una directiva, se realiza una comparación para comprobar si ya existe una directiva con el mismo nombre. La comparación no puede distinguir entre nombres que sean iguales excepto para caracteres acentuados. Se da por hecho que la política ya se ha agregado a la base de datos y que la nueva no se ha añadido.

1. Haga clic en Aceptar.

## Eliminar una directiva {#delete-a-policy}

Puede eliminar directivas que haya creado. Los administradores pueden eliminar directivas que cualquier usuario haya creado. Los coordinadores de conjuntos de políticas pueden eliminar directivas en sus conjuntos de políticas. Una directiva que elimine seguirá aplicándose a los documentos protegidos con esa directiva. Puede eliminar varias directivas a la vez.

Los usuarios invitados solo pueden eliminar directivas si el administrador habilita esta capacidad. Si no puede eliminar directivas, la opción eliminar no estará disponible.

1. En la página de seguridad del documento, haga clic en Directivas.
1. Haga clic en la ficha Mi política .
1. Para eliminar una directiva compartida, haga clic en la ficha Conjuntos de directivas y haga clic en el nombre del conjunto de directivas correspondiente.
1. Seleccione la casilla de verificación situada junto a la política adecuada, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

>[!NOTE]
>
>Debe utilizar la aplicación cliente para eliminar directivas de documentos. (Consulte la Ayuda de Acrobat o la ayuda correspondiente sobre las extensiones de Acrobat Reader DC).

## Ordenar la lista de directivas {#sort-the-policy-list}

Puede ordenar la lista de directivas por encabezado de columna para encontrar las directivas más fácilmente. Un icono de triángulo junto al encabezado de la columna indica qué columna se utiliza actualmente para ordenar. Un triángulo que señala hacia arriba indica el orden ascendente, mientras que un triángulo que señala hacia abajo indica el orden descendente.

1. En la página de seguridad del documento, haga clic en Directivas y en la ficha Conjunto de directivas .
1. Seleccione un conjunto de directivas y, a continuación, haga clic en la ficha Directivas .
1. Haga clic en el encabezado de columna correspondiente.
1. Para cambiar el orden, vuelva a hacer clic en la columna .

