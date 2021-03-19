---
title: Configuración de las opciones de cliente y servidor
seo-title: Configuración de opciones de cliente y servidor
description: Obtenga información sobre cómo configurar las distintas opciones de cliente y servidor, como los ajustes de configuración del servidor, las funciones de seguridad de documentos y la auditoría de eventos.
seo-description: Obtenga información sobre cómo configurar las distintas opciones de cliente y servidor, como los ajustes de configuración del servidor, las funciones de seguridad de documentos y la auditoría de eventos.
uuid: 1f9f9886-726e-4fad-9ff8-0ff11eef653e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0f069fbc-10c2-403e-9419-5e9920035d75
feature: Seguridad de los documentos
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '10275'
ht-degree: 0%

---


# Configuración del servidor de seguridad de documentos {#configure-the-document-security-server}

1. En la consola de administración, haga clic en Servicios > seguridad del documento > Configuración > Configuración del servidor.
1. Configure los ajustes y haga clic en Aceptar.

## Ajustes de configuración del servidor {#server-configuration-settings}

**URL básica:** la URL de seguridad del documento base que contiene el nombre del servidor y el puerto. La información adjunta a la base crea direcciones URL de conexión. Por ejemplo, /edc/Main.do se adjunta para acceder a las páginas web. Los usuarios también responden a invitaciones de registro de usuarios externos a través de esta dirección URL.

Si utiliza IPv6, introduzca la URL base como nombre de equipo o nombre DNS. Si utiliza una dirección IP numérica, Acrobat no podrá abrir los archivos protegidos por políticas. Además, utilice la URL segura HTTP (HTTPS) para su servidor.

>[!NOTE]
>
>La URL base está incrustada en archivos protegidos por políticas. Las aplicaciones cliente utilizan la URL base para conectarse de nuevo al servidor. Los archivos seguros seguirán conteniendo la dirección URL base, incluso si se cambia más adelante. Si cambia la dirección URL base, la información de configuración deberá actualizarse para todos los clientes que se conecten.

**Período de arrendamiento sin conexión predeterminado:** el tiempo predeterminado que un usuario puede utilizar un documento protegido sin conexión. Esta configuración determina el valor inicial de la configuración del período de arrendamiento sin conexión automática al crear una directiva. (Consulte Creación y edición de directivas). Cuando caduca el periodo de arrendamiento, el destinatario debe sincronizar de nuevo el documento para seguir utilizándolo.

Para obtener más información sobre el funcionamiento del arrendamiento y la sincronización sin conexión, consulte [Manual on configuring offline leasing and synchronization](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**Período de sincronización sin conexión predeterminado:** el tiempo máximo que puede utilizarse un documento sin conexión desde el momento en que está protegido inicialmente.

**Tiempo de espera de sesión del cliente:** El tiempo, en minutos, transcurrido el cual la seguridad del documento se desconecta si un usuario que ha iniciado sesión mediante una aplicación cliente no interactúa con la seguridad del documento.

**Permitir acceso a usuarios anónimos:** seleccione esta opción para permitir la creación de políticas compartidas y personales que permitan a los usuarios anónimos abrir documentos protegidos por políticas. (Los usuarios que no tengan cuentas pueden acceder al documento, pero no pueden iniciar sesión en documentos de seguridad ni utilizar otros documentos protegidos por políticas).

**Deshabilitar acceso a clientes de la versión 7:** especifica si los usuarios pueden usar Acrobat o Reader 7.0 para conectarse al servidor. Cuando se selecciona esta opción, los usuarios deben utilizar Acrobat o Reader 8.0 y posterior para completar las operaciones de seguridad de los documentos en documentos PDF. Si las políticas requieren que Acrobat o Reader 8.0 y posterior se ejecuten en modo certificado al abrir documentos protegidos por políticas, debe desactivar el acceso a Acrobat o Reader 7. (Consulte Especificar los permisos del documento para usuarios y grupos).

**Permitir acceso sin conexión por** documentoSeleccione esta opción para especificar el acceso sin conexión por documento. Si esta configuración está habilitada, el usuario tendrá acceso sin conexión únicamente a los documentos que el usuario haya abierto en línea al menos una vez.

**Permitir autenticación de contraseña de nombre de usuario:** seleccione esta opción para permitir que las aplicaciones cliente utilicen autenticación de nombre de usuario/contraseña al conectarse al servidor.

**Permitir autenticación Kerberos:** seleccione esta opción para permitir que las aplicaciones cliente utilicen autenticación Kerberos al conectarse al servidor.

**Permitir autenticación de certificado de cliente:** seleccione esta opción para permitir que las aplicaciones cliente utilicen autenticación de certificado al conectarse al servidor.

**Permitir** autenticación extendidaSeleccione esta opción para habilitar la autenticación extendida y, a continuación, introduzca la URL de aterrizaje de autenticación extendida.

Al seleccionar esta opción, las aplicaciones cliente pueden utilizar la autenticación extendida. La autenticación extendida proporciona procesos de autenticación personalizados y distintas opciones de autenticación configuradas en el servidor de formularios AEM. Por ejemplo, los usuarios ahora pueden experimentar la autenticación basada en SAML en lugar de AEM nombre de usuario/contraseña de los formularios, desde Acrobat y el cliente de Reader. De forma predeterminada, la dirección URL de aterrizaje contiene *localhost* como nombre de servidor. Reemplace el nombre del servidor por un nombre de host completo. El nombre de host en la dirección URL de aterrizaje se rellena automáticamente desde la dirección URL base, si la autenticación ampliada aún no está habilitada. Consulte [Añadir el proveedor de autenticación extendido](configuring-client-server-options.md#add-the-extended-authentication-provider).

***nota **: La autenticación ampliada es compatible con Apple Mac OS X con Adobe Acrobat versión 11.0.6 y posteriores.*

**Ancho de control HTML preferido para la** autenticación extendidaEspecifique la anchura del cuadro de diálogo de autenticación extendida que se abre en Acrobat para introducir las credenciales de usuario.

**Altura de control HTML preferida para la** autenticación extendidaEspecifique la altura del cuadro de diálogo de autenticación extendida que se abre en Acrobat para introducir las credenciales de usuario.

***nota **: Los límites de anchura y altura de este cuadro de diálogo son los siguientes:*
Anchura: Mínimo = 400, máximo = 900

Altura: Mínimo = 450; máximo = 800

**Habilitar el almacenamiento en caché de credenciales del cliente:** seleccione esta opción para permitir que los usuarios almacenen en caché sus credenciales (nombre de usuario y contraseña). Cuando las credenciales de los usuarios se almacenan en caché, no tienen que introducir sus credenciales cada vez que abren un documento o cuando hacen clic en el botón Actualizar de la página Administrar políticas de seguridad de Adobe Acrobat. Puede especificar el número de días antes de que los usuarios deban proporcionar sus credenciales de nuevo. Si establece el número de días en 0, las credenciales se pueden almacenar en caché indefinidamente.

## Configuración de usuarios y administradores de seguridad de documentos {#configuring-document-security-users-and-administrators}

### Asignación de funciones de seguridad de documento a los administradores {#assigning-document-security-roles-to-administrators}

El entorno de AEM forms contiene uno o más usuarios administradores que tienen los privilegios adecuados para crear usuarios y grupos. Si su organización utiliza la seguridad de los documentos, al menos un administrador debe tener asignado el privilegio de administrar los usuarios invitados y locales.

Los administradores también deben tener la función de usuario de la consola de administración para acceder a la consola de administración. (Consulte [Creación y configuración de funciones](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)).

### Configuración de usuarios y grupos visibles {#configuring-visible-users-and-groups}

Para ver usuarios y grupos en dominios seleccionados durante las búsquedas de usuarios de directivas, un superadministrador o un administrador de conjuntos de directivas deben seleccionar y agregar dominios (creados en Administración de usuarios) a la lista de usuarios y grupos visible para cada conjunto de directivas.

La lista visible de usuarios y grupos es visible para el coordinador del conjunto de directivas y se utiliza para restringir los dominios que el usuario final puede examinar al elegir usuarios o grupos para agregar a directivas. Si no se realiza esta tarea, el coordinador del conjunto de políticas no encontrará ningún usuario o grupo que agregar a la directiva. Puede haber más de un coordinador de conjunto de políticas para un conjunto de políticas determinado.

1. Después de instalar y configurar el entorno de formularios AEM con seguridad de documentos, configure todos los dominios adecuados en Administración de usuarios. <!-- Fix broken link (See Setting up and managing domains) -->

   ***nota **: La creación de dominios debe realizarse antes de poder crear cualquier política.*

1. En la consola de administración, haga clic en Servicios > Administración de documentos > Directivas y, a continuación, haga clic en la ficha Conjuntos de políticas.
1. Seleccione Conjunto de directivas globales y, a continuación, haga clic en la ficha Usuarios y grupos visibles .
1. Haga clic en Añadir dominio y añada dominios existentes según sea necesario.
1. Vaya a Servicios > Seguridad del documento > Configuración > Mis políticas y haga clic en la ficha Usuarios y grupos visibles .
1. Haga clic en Añadir dominio y añada dominios existentes según sea necesario.

## Añadir el proveedor de autenticación extendido {#add-the-extended-authentication-provider}

AEM formularios proporciona una configuración de ejemplo que puede personalizar para su entorno. Siga estos pasos:

>[!NOTE]
>
>La autenticación ampliada es compatible con Apple Mac OS X con Adobe Acrobat versión 11.0.6 y posteriores.

1. Obtenga el archivo WAR de muestra para implementarlo. Consulte la guía de instalación adecuada para su servidor de aplicaciones.
1. Asegúrese de que el servidor de formularios tiene un nombre completo en lugar de direcciones IP como URL base y que es una URL HTTPS. Consulte [Ajustes de configuración del servidor](configuring-client-server-options.md#server-configuration-settings).
1. Habilite la autenticación extendida desde la página Configuración del servidor . Consulte [Ajustes de configuración del servidor](configuring-client-server-options.md#server-configuration-settings).
1. Añada las direcciones URL de redireccionamiento SSO necesarias en el archivo de configuración de Administración de usuarios . Consulte [Añadir direcciones URL de redireccionamiento SSO para la autenticación extendida](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### Añadir direcciones URL de redireccionamiento SSO para la autenticación extendida {#add-sso-redirect-urls-for-extended-authentication}

Con la autenticación extendida habilitada, los usuarios que abren un documento protegido por políticas en Acrobat XI o Reader XI obtienen un cuadro de diálogo para la autenticación. Este cuadro de diálogo carga la página HTML especificada como URL de aterrizaje de autenticación extendida en la configuración del servidor de seguridad del documento. Consulte [Ajustes de configuración del servidor](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>La autenticación ampliada es compatible con Apple Mac OS X con Adobe Acrobat versión 11.0.6 y posteriores.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Exportar y guarde el archivo de configuración en el disco.
1. Abra el archivo en un editor y busque el nodo AllowedUrls .
1. En el nodo `AllowedUrls`, agregue las siguientes líneas: `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Guarde el archivo y, a continuación, importe el archivo actualizado desde la página Configuración manual : En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.

## Configuración de la seguridad sin conexión {#configuring-offline-security}

document security permite utilizar documentos protegidos por políticas sin conexión a Internet o sin conexión de red. Esta capacidad requiere que la directiva permita el acceso sin conexión, como se describe en [Especifique los permisos de documento para usuarios y grupos](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Antes de poder utilizar un documento con una directiva de este tipo sin conexión, el destinatario debe abrir el documento en línea y habilitar el acceso sin conexión haciendo clic en Sí cuando se le solicite. También se puede solicitar al destinatario que autentique su identidad. El destinatario puede utilizar documentos sin conexión durante el periodo de arrendamiento sin conexión especificado en la directiva.

Cuando finaliza el periodo de arrendamiento sin conexión, el destinatario debe volver a sincronizarse con la seguridad del documento abriendo un documento en línea o utilizando un comando de menú Acrobat o Acrobat Reader DC Extensions para sincronizar. (Consulte *Ayuda de Acrobat* o la *Ayuda de extensiones de Acrobat Reader DC* correspondiente).

Dado que los documentos que permiten el acceso sin conexión requieren almacenar en caché material clave en el equipo en el que los archivos se almacenan sin conexión, el archivo puede verse comprometido si un usuario no autorizado puede obtener el material clave. Para compensar esta posibilidad, se proporcionan opciones de sustitución de claves programadas y manuales que se pueden configurar para evitar que una persona no autorizada utilice la clave para acceder al documento.

### Establecer un periodo de arrendamiento sin conexión predeterminado {#set-a-default-offline-lease-period}

Los destinatarios de los documentos protegidos por políticas pueden desconectar los documentos durante el número de días especificado en la directiva. Después de sincronizar inicialmente el documento con document security, el destinatario puede utilizarlo sin conexión hasta que caduque el periodo de arrendamiento sin conexión. Cuando caduca el periodo de arrendamiento, el destinatario debe poner el documento en línea e iniciar sesión para sincronizarse con la seguridad del documento y así seguir utilizando el documento.

Puede configurar un periodo de arrendamiento sin conexión predeterminado. El periodo de arrendamiento puede cambiarse del predeterminado cuando alguien crea o edita una directiva.

1. En la página de seguridad del documento, haga clic en Configuración > Configuración del servidor.
1. En el cuadro Periodo de arrendamiento sin conexión predeterminado, escriba el número de días para el periodo de arrendamiento sin conexión.
1. Haga clic en Aceptar.

### Administrar los roles clave {#manage-key-rollovers}

La seguridad de los documentos utiliza algoritmos de codificación y licencias para proteger los documentos. Cuando cifra un documento, la seguridad del documento genera y administra una clave de descifrado denominada *DocKey* que pasa a la aplicación cliente. Si la política que protege un documento permite el acceso sin conexión, también se genera una clave sin conexión denominada *principal* para cada usuario que tenga acceso al documento sin conexión.

>[!NOTE]
>
>Si no existe una clave principal, la seguridad del documento genera una para proteger un documento.

Para abrir un documento protegido por políticas sin conexión, el equipo del usuario debe tener la clave principal adecuada. El equipo obtiene la clave principal cuando el usuario se sincroniza con la seguridad del documento (abre un documento protegido en línea). Si esta clave principal se ve comprometida, cualquier documento al que el usuario tenga acceso sin conexión también podría verse comprometido.

Una manera de reducir la amenaza a los documentos sin conexión es evitar permitir el acceso sin conexión a documentos particularmente delicados. Otro método es pasar periódicamente las claves principales. Cuando la seguridad del documento coloca la clave sobre, las claves existentes ya no pueden acceder a los documentos protegidos por políticas. Por ejemplo, si un autor obtiene una clave principal de una laptop robada, esa clave no se puede utilizar para acceder a los documentos que están protegidos después de que se produce la prórroga. Si sospecha que una clave principal específica se ha visto comprometida, puede pasar manualmente la tecla.

Sin embargo, también debe tener en cuenta que un cambio de clave afecta a todas las claves principales, no solo a una. También reduce la escalabilidad del sistema porque los clientes deben almacenar más claves para el acceso sin conexión. La frecuencia de sustitución de claves predeterminada es de 20 días. Se recomienda no establecer este valor por debajo de los 14 días, ya que es posible que las personas no puedan ver documentos sin conexión y que el rendimiento del sistema se vea afectado.

En el siguiente ejemplo, Key1 es la más antigua de las dos claves principales y Key2 es la más reciente. Al hacer clic en el botón Rollover Keys Now la primera vez, Key1 pasa a ser no válida y se genera una clave principal más nueva y válida (Key3). Los usuarios obtendrán Key3 cuando se sincronicen con la seguridad del documento, normalmente abriendo un documento protegido en línea. Sin embargo, los usuarios no se ven obligados a sincronizarse con la seguridad de los documentos hasta que alcancen el período máximo de arrendamiento sin conexión especificado en una directiva. Después del primer cambio de clave, los usuarios que permanezcan sin conexión podrán abrir documentos sin conexión, incluidos los protegidos por Key3, hasta que alcancen el período máximo de arrendamiento sin conexión. Cuando hace clic en el botón Rollover Keys Now por segunda vez, Key2 deja de ser válido y se crea Key4. Los usuarios que permanezcan sin conexión durante los dos traslados clave no podrán abrir documentos protegidos con Key3 o Key4 hasta que se sincronicen con la seguridad del documento.

**Cambio de la frecuencia de sustitución de teclas**

Para fines de confidencialidad, cuando se utilizan documentos sin conexión, la seguridad de los documentos proporciona una opción de sustitución automática de claves con un periodo de frecuencia predeterminado de 20 días. Puede cambiar la frecuencia de prórroga; sin embargo, evite establecer un valor inferior a 14 días, ya que es posible que se impida a las personas ver documentos sin conexión y que el rendimiento del sistema se vea afectado.

1. En la página de seguridad del documento, haga clic en Configuración > Administración de claves.
1. En el cuadro Frecuencia de sustitución de claves , escriba el número de días para el período de prórroga.
1. Haga clic en Aceptar.

**Redondear manualmente las claves principales**

Para mantener la confidencialidad de los documentos sin conexión, puede pasar manualmente las claves principales. Es posible que necesite pasar manualmente el ratón por encima de una clave (por ejemplo, si la clave está comprometida por alguien que la obtiene de un equipo en el que se almacena en caché para habilitar el acceso sin conexión a un documento).

>[!NOTE]
>
>Evite utilizar con frecuencia el desplazamiento manual porque hace que todas las claves principales se pasen, no solo una, y puede evitar temporalmente que los usuarios vean nuevos documentos sin conexión.

Las claves principales deben redistribuirse dos veces antes de que las claves existentes anteriormente en los equipos cliente se invaliden. Los equipos cliente que tengan claves principales invalidadas deben volver a sincronizarse con el servicio de seguridad de documentos para adquirir las nuevas claves principales.

1. En la página de seguridad del documento, haga clic en Configuración > Administración de claves.
1. Haga clic en Combinar teclas ahora y, a continuación, haga clic en Aceptar.
1. Espere aproximadamente 10 minutos. El siguiente mensaje de registro aparece en el registro del servidor: `Done RightsManagement key rollover for`*N* `principals`. Donde *N* es el número de usuarios en el sistema de seguridad de documentos.
1. Haga clic en Combinar teclas ahora y, a continuación, haga clic en Aceptar.
1. Espere aproximadamente 10 minutos.

## Configuración de auditoría de eventos y configuración de privacidad {#configuring-event-auditing-and-privacy-settings}

La seguridad de los documentos puede auditar y registrar información sobre eventos relacionados con la interacción con documentos, políticas, administradores y servidores protegidos por políticas. Puede configurar la auditoría de eventos y especificar los tipos de eventos que desea auditar. Para auditar eventos para un documento en particular, también debe habilitarse la opción de auditoría de la directiva .

Cuando la auditoría está habilitada, puede ver detalles de los eventos auditados en la página Eventos . los usuarios de seguridad de documentos también pueden ver eventos relacionados específicamente con los documentos protegidos por políticas que utilizan o crean.

Puede seleccionar estos tipos de eventos para la auditoría:

* Eventos de documentos protegidos por políticas, como intentos de usuarios autorizados o no autorizados de abrir documentos
* Eventos de directiva, como la creación, el cambio, la eliminación, la activación y la desactivación de directivas
* Eventos de usuario, como invitaciones y registros de usuarios externos, cuentas de usuario activadas y desactivadas, cambios en las contraseñas de los usuarios y actualizaciones de perfil
* AEM eventos de formularios, como descoincidencias de versiones, proveedores de autorización y servidor de directorios no disponibles, y cambios de configuración del servidor

### Habilitar o deshabilitar la auditoría de eventos {#enable-or-disable-event-auditing}

Puede habilitar y deshabilitar la auditoría de eventos relacionados con el servidor, documentos protegidos por políticas, directivas, conjuntos de directivas y usuarios. Al habilitar la auditoría de eventos, puede elegir auditar todos los eventos posibles o seleccionar eventos específicos para auditarlos.

Cuando activa la auditoría del servidor, puede ver los eventos auditados en la página Eventos .

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Auditoría y configuración de privacidad.
1. Para configurar la auditoría del servidor, en Habilitar auditoría del servidor, seleccione Sí o No.
1. Si ha seleccionado Sí, en cada categoría de evento, realice una de las siguientes acciones para seleccionar las opciones que desea auditar:

   * Para auditar todos los eventos de la categoría , seleccione Todos.
   * Para auditar solo algunos eventos, anule la selección de Todos y, a continuación, active las casillas de verificación situadas junto a los eventos que desee auditar.

      (Consulte [Opciones de auditoría de eventos](configuring-client-server-options.md#event-auditing-options)).

1. Haga clic en Aceptar.

>[!NOTE]
>
>Al trabajar con las páginas web, evite utilizar los botones del explorador, como el botón Atrás, el botón Actualizar y la flecha Atrás o Adelante, ya que esta acción puede causar problemas no deseados en la captura de datos y la visualización de datos.

### Habilitar o deshabilitar la notificación de privacidad {#enable-or-disable-privacy-notification}

Puede activar y desactivar un mensaje de notificación de privacidad. Cuando activa la notificación de privacidad, aparece un mensaje cuando un destinatario intenta abrir un documento protegido por políticas. El aviso informa al usuario de que se está auditando el uso del documento. También puede especificar una dirección URL que el usuario pueda utilizar para ver la página de política de privacidad si hay una disponible.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Auditoría y configuración de privacidad.
1. Para configurar la notificación de privacidad, en Habilitar notificación de privacidad, seleccione Sí o No.

   Si la directiva adjunta a un documento permite el acceso de usuarios anónimos y la opción Habilitar aviso de privacidad está establecida en No, no se pedirá al usuario que inicie sesión y no se mostrará el mensaje de notificación de privacidad.

   Si la directiva adjunta a un documento no permite el acceso de usuarios anónimos, el usuario verá el mensaje de notificación de privacidad.

1. Si corresponde, en el cuadro URL de privacidad, escriba la dirección URL a la página de política de privacidad. Si el cuadro URL de privacidad se deja en blanco, se muestra la página de privacidad de adobe.com.
1. Haga clic en Aceptar.

>[!NOTE]
>
>Al desactivar el aviso de privacidad, no se desactiva la auditoría del uso del documento. Las acciones de auditoría y las acciones personalizadas integradas que se admiten mediante el seguimiento de uso extendido aún pueden recopilar información de comportamiento del usuario.

### Importar un tipo de evento de auditoría personalizado {#import-a-custom-audit-event-type}

Si utiliza una aplicación habilitada para la seguridad de documentos que admita la auditoría de eventos adicionales, como eventos específicos de un determinado tipo de archivo, un socio de Adobe puede proporcionarle eventos de auditoría personalizados que puede importar en la seguridad de documentos. Utilice esta función solo si un socio de Adobe le ha proporcionado tipos de eventos personalizados.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Gestión de eventos.
1. Haga clic en Examinar para ir al archivo XML que desea importar y haga clic en Importar.
1. La importación sobrescribe los tipos de eventos de auditoría personalizados existentes en el servidor si se encuentran combinaciones idénticas de código de evento y área de nombres.
1. Haga clic en Aceptar.

### Eliminar un tipo de evento de auditoría personalizado {#delete-a-custom-audit-event-type}

1. En la consola de administración, haga clic en Servicios > seguridad del documento > Configuración > Gestión de eventos.
1. Seleccione la casilla de verificación situada junto al tipo de evento de auditoría personalizado que desea eliminar y haga clic en Eliminar.
1. Haga clic en Aceptar.

### Exportar eventos de auditoría {#export-audit-events}

Puede exportar eventos de auditoría a un archivo para archivarlos.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Gestión de eventos.
1. Edite la configuración en Exportar eventos de auditoría según sea necesario. Puede especificar:

   * la edad mínima de los eventos de auditoría para exportar
   * el número máximo de eventos de auditoría que se incluirán en un solo archivo. El servidor genera uno o más archivos, según este valor.
   * la carpeta donde se creará el archivo. Esta carpeta se encuentra en el servidor de formularios. Si la ruta de la carpeta es relativa, entonces es relativa al directorio raíz del servidor de aplicaciones.
   * el prefijo de archivo que se utilizará para los archivos de eventos de auditoría
   * el formato del archivo, ya sea un archivo de valores separados por comas (CSV) compatible con Microsoft Excel o un archivo XML.

1. Haga clic en Exportar. Si desea cancelar la exportación, haga clic en Cancelar exportación. Si otro usuario ha programado una exportación, el botón Cancelar exportación no estará disponible hasta que se complete dicha exportación. El botón Cancelar exportación no está disponible si otro usuario ha programado una exportación. Para comprobar si se ha iniciado o finalizado una exportación o eliminación programada, haga clic en Actualizar.

### Eliminar eventos de auditoría {#delete-audit-events}

Puede eliminar los eventos de auditoría que tengan más de un número determinado de días.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Gestión de eventos.
1. En Eliminar eventos de auditoría, especifique el número de días en el cuadro Eliminar eventos de auditoría anteriores a
1. Haga clic en Eliminar. Haga clic en Exportar. Si desea cancelar la eliminación, haga clic en Cancelar eliminación. Si otro usuario ha programado una eliminación, el botón Cancelar eliminación no estará disponible hasta que se complete la exportación. El botón Cancelar eliminación no está disponible si otro usuario ha programado una exportación. Para comprobar si una eliminación programada ha comenzado o terminado, haga clic en Actualizar.

### Opciones de auditoría de eventos {#event-auditing-options}

Puede habilitar y deshabilitar la auditoría de eventos y especificar los tipos de eventos que se van a auditar.

**Eventos de documento**

**Ver documento:** un destinatario ve un documento protegido por políticas.

**Cerrar documento:** un destinatario cierra un documento protegido por políticas.

**Imprimir baja** resoluciónUn destinatario imprime un documento protegido por políticas con la opción de baja resolución especificada.

**Imprimir alta resolución:** un destinatario imprime un documento protegido por políticas con opción de alta resolución especificada.

**Agregar anotación al documento:** un destinatario agrega una anotación a un documento PDF.

**Revocar documento:** un usuario o administrador revoca el acceso a un documento protegido por políticas.

**Documento sin revocar:** un usuario o administrador restablece el acceso a un documento protegido por políticas.

**Rellenado de formulario:** un destinatario introduce información en un documento PDF que se puede rellenar.

**Política eliminada:** un editor elimina una directiva de un documento para retirar las protecciones de seguridad.

**Cambiar URL de revocación de documento:**  una llamada desde el nivel de API cambia la URL de revocación especificada para acceder a un nuevo documento que reemplaza a un documento revocado.

**Modificar documento:** un destinatario cambia el contenido de un documento protegido por políticas.

**Firmar documento:** un destinatario firma un documento.

**Asegurar un nuevo documento:** un usuario aplica una directiva para proteger un documento.

**Cambiar directiva en documento:** un usuario o administrador cambia la directiva adjunta a un documento.

**Publicar documento como:** se registra en el servidor un nuevo documento cuyo documentName y licencia sean idénticos a un documento existente y los documentos no tienen una relación principal-secundario. Este suceso se puede activar con el SDK de AEM forms.

**Iterar documento:** un nuevo documento cuyo documentName y licencia son idénticos a un documento existente se registra en el servidor y los documentos tienen una relación padre-hijo. Este suceso se puede activar con el SDK de AEM forms.

**Eventos de política**

**Directiva creada:** un usuario o administrador crea una directiva.

**Política habilitada:** un administrador hace que una directiva esté disponible.

**Directiva modificada:** un usuario o administrador cambia una directiva.

**Directiva deshabilitada:** un administrador impide que una directiva esté disponible.

**Directiva eliminada:** un usuario o administrador elimina una directiva.

**Cambiar propietario de directiva:** una llamada desde el nivel de API cambia el propietario de la directiva.

**Eventos de usuario**

**Usuario eliminado:** un administrador elimina una cuenta de usuario.

**Registrar usuario invitado:** un usuario externo se registra con la seguridad del documento.

**Inicio de sesión correcto:** intentos de inicio de sesión correctos por parte de administradores o usuarios.

**Usuarios invitados:** la seguridad de los documentos invita al usuario a registrarse.

**Usuarios activados:** los usuarios externos activan sus cuentas utilizando la dirección URL del correo electrónico de activación o un administrador habilita una cuenta.

**Cambiar contraseña:** los usuarios invitados cambian sus contraseñas o un administrador restablece una contraseña para un usuario local.

**Error de inicio de sesión:** errores en los intentos de inicio de sesión de administradores o usuarios.

**Usuarios desactivados:** un administrador desactiva una cuenta de usuario local.

**Actualización de perfil:** los usuarios invitados cambian su nombre, nombre de organización y contraseña.

**Cuenta bloqueada:** un administrador bloquea una cuenta.

**Eventos de conjuntos de políticas**

**Conjunto de directivas creado:** un administrador o coordinador de conjuntos de directivas crea un conjunto de directivas.

**Conjunto de directivas eliminado:** un administrador o un coordinador de conjuntos de directivas elimina un conjunto de directivas.

**Conjunto de directivas modificado:** un administrador o un coordinador de conjuntos de directivas cambian un conjunto de directivas.

**Eventos del sistema**

**Sincronización de directorios finalizada:**  esta información no está disponible en la página Eventos. La información de sincronización de directorios actual, incluido el estado de sincronización actual y la hora de la última sincronización, se muestra en la página Administración de dominios . Para acceder a la página Administración de dominios en la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.

**Acceso sin conexión de cliente:** acceso sin conexión habilitado por el usuario a documentos protegidos contra el servidor en el equipo del usuario.

**La aplicación** ClientClient sincronizada debe sincronizar la información con el servidor para permitir el acceso sin conexión.

**Discordancia de versión:** una versión del SDK de AEM forms incompatible con el servidor que intenta conectarse al servidor.

**Información de sincronización de directorios:** esta información no está disponible en la página Eventos. La información de sincronización de directorios actual, incluido el estado de sincronización actual y la hora de la última sincronización, se muestra en la página Administración de dominios . Para acceder a la página Administración de dominios en la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.

**Cambio en la configuración del servidor:** los cambios en la configuración del servidor que se realizan a través de las páginas web o manualmente mediante la importación de un archivo config.xml. Esto incluye cambios en la dirección URL base, tiempos de espera de sesión, bloqueos de inicio de sesión, configuración de directorios, rebotes de claves, configuración del servidor SMTP para registro externo, configuración de marcas de agua, opciones de visualización, etc.

## Configuración del seguimiento de uso extendido {#configuring-extended-usage-tracking}

La seguridad de los documentos puede rastrear varios eventos personalizados que se pueden realizar en un documento protegido. Puede habilitar el seguimiento de eventos desde el servidor de seguridad de documentos a nivel global o a nivel de directiva. A continuación, puede configurar un JavaScript para capturar acciones específicas realizadas dentro del documento PDF protegido, como hacer clic en un botón o guardar el documento. Estos datos de uso se envían como archivo XML en pares de clave-valor, que se pueden utilizar para un análisis más detallado. Los usuarios finales que accedan a los documentos protegidos pueden permitir o rechazar dicho seguimiento desde la aplicación cliente.

Si el seguimiento está habilitado a nivel global, puede anular esta configuración a nivel de directiva y deshabilitarla para una directiva en particular. La anulación a nivel de directiva no es posible si el seguimiento está deshabilitado a nivel global. La lista de eventos rastreados se inserta automáticamente en el servidor cuando el recuento de eventos alcanza los 25 o cuando se cierra el documento. También puede configurar la secuencia de comandos para que inserte explícitamente la lista de eventos según sus necesidades. Puede personalizar el seguimiento de eventos accediendo a las propiedades y los métodos del objeto de seguridad del documento.

Después de habilitar el seguimiento, todas las directivas que se creen posteriormente tendrán activado el seguimiento de forma predeterminada. Las directivas creadas antes de habilitar el seguimiento en el servidor necesitarán actualizaciones manuales.

### Habilitar o deshabilitar el seguimiento de uso extendido {#enable-or-disable-extended-usage-tracking}

Antes de comenzar, asegúrese de que la auditoría del servidor está habilitada. Consulte [Configuración de auditoría de eventos y configuración de privacidad](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) para obtener más información sobre la auditoría.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Auditoría y configuración de privacidad.
1. Para configurar el seguimiento de uso extendido, en Habilitar seguimiento, seleccione Sí o No.
1. Para establecer la selección de la casilla de verificación Permitir la recopilación de datos de uso detallados en la página de inicio de sesión, en Habilitar seguimiento predeterminado, seleccione Sí o No.

Para ver los eventos rastreados, puede usar el filtro Eventos de documento en la página Eventos . Los eventos rastreados con JavaScript se etiquetan como Seguimiento de uso detallado. Consulte [Monitorización de eventos](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) para obtener más información sobre los eventos.

## Configurar la configuración de visualización de seguridad del documento {#configure-document-security-display-settings}

1. En la consola de administración, haga clic en Servicios > seguridad del documento > Configuración > Opciones de visualización.
1. Configure los ajustes y haga clic en Aceptar.

### Mostrar configuración {#display-settings}

**Filas para mostrar los resultados de la búsqueda:** Número de filas que aparecen en una página cuando se realizan búsquedas.

**Personalización para el cuadro de diálogo de inicio de sesión del cliente**

Esta configuración controla el texto mostrado en el mensaje de inicio de sesión que aparece cuando un usuario inicia sesión en la seguridad del documento a través de una aplicación cliente.

**Texto de bienvenida:** el texto del mensaje de bienvenida, como &quot;Por favor, inicia sesión con tu nombre de usuario y contraseña&quot;. El texto del mensaje de bienvenida debe contener información sobre cómo iniciar sesión para documentar la seguridad y cómo ponerse en contacto con un administrador u otra persona de asistencia designada en su organización para obtener ayuda. Por ejemplo, es posible que los usuarios externos tengan que ponerse en contacto con un administrador si olvidan sus contraseñas o necesitan asistencia en el proceso de registro o inicio de sesión. La longitud máxima del texto de bienvenida es de 512 caracteres.

**Texto de nombre de usuario:** etiqueta de texto para el cuadro de nombre de usuario.

**Texto de contraseña:** la etiqueta de texto del cuadro de contraseña.

**Personalización para el cuadro de diálogo de autenticación de certificado de cliente**

Esta configuración controla el texto mostrado en el cuadro de diálogo de autenticación de certificado.

**Elegir tipo de autenticación Texto:** el texto mostrado para dirigir a un usuario a seleccionar un tipo de autenticación.

**Elegir texto del certificado:** el texto mostrado para dirigir a un usuario para que seleccione un tipo de certificado.

**Texto de error Certificados no disponibles:**  Mensaje de hasta 512 caracteres que se mostrarán cuando el certificado seleccionado no esté disponible.

**Personalización para la visualización de certificados de cliente**

**Mostrar solo los emisores de credenciales de confianza:** cuando se selecciona esta opción, la aplicación cliente presenta al usuario únicamente certificados de los emisores de credenciales en los que AEM formulario está configurado para confiar (consulte Administración de certificados y credenciales). Cuando no se selecciona esta opción, se presenta al usuario una lista de todos los certificados del sistema del usuario.

## Configuración de marcas de agua dinámicas {#configure-dynamic-watermarks}

Con la seguridad del documento, puede configurar los ajustes predeterminados de la opción de marca de agua dinámica que puede aplicar al crear directivas. Una *marca de agua* es una imagen superpuesta sobre el texto del documento. Resulta útil para rastrear el contenido de un documento y puede ayudar a identificar el uso ilegal del contenido.

Una marca de agua dinámica puede consistir en texto compuesto por variables definidas, como el ID de usuario y la fecha y el texto personalizado, o en contenido enriquecido dentro de un PDF. Puede configurar marcas de agua con varios elementos cada uno con su propio posicionamiento y formato.

Las marcas de agua no son editables y, por lo tanto, constituyen un método más seguro para garantizar la confidencialidad del contenido del documento. Las marcas de agua dinámicas también garantizan que una marca de agua muestre suficiente información específica del usuario como elemento disuasorio para distribuir más el documento.

La marca de agua que especifica una política aparece en el documento protegido por políticas cuando un destinatario visualiza o imprime el documento. A diferencia de las marcas de agua permanentes, las marcas de agua dinámicas nunca se guardan en el documento, lo que proporciona la flexibilidad necesaria al implementar un documento en un entorno de intranet para garantizar que la aplicación de visualización muestre la identidad del usuario específico. Además, si un documento tiene varios usuarios, el uso de la marca de agua dinámica significa que puede utilizar un documento en lugar de varias versiones, cada una con una marca de agua diferente. La marca de agua que aparece refleja la identidad del usuario actual.

Tenga en cuenta que las marcas de agua dinámicas son diferentes de las marcas de agua que los usuarios pueden agregar directamente al documento en Acrobat. El resultado es que puede tener dos marcas de agua en un documento protegido por políticas.

### Consideraciones al crear marcas de agua {#considerations-when-creating-watermarks}

Puede crear marcas de agua dinámicas con varios elementos de marca de agua y cada elemento especificado como texto o PDF. Se pueden incluir hasta cinco elementos en una marca de agua.

Si elige una marca de agua basada en texto, puede especificar varios elementos dentro de la marca de agua con varias entradas de texto y especificar la posición de cada elemento. Asigne nombres significativos a estos elementos, como encabezado, pie de página, etc.

Por ejemplo, si desea especificar un texto distinto en el encabezado, pie de página, en los márgenes y en todo el documento como marca de agua, cree varios elementos de marca de agua y especifique sus posiciones. Si desea que el ID de usuario del usuario y la fecha actual de acceso al documento aparezcan en el encabezado, que el nombre de la política en el margen derecho y el texto personalizado &quot;CONFIDENCIAL&quot; aparezcan en diagonal en todo el documento, debe definir elementos de marca de agua independientes con texto como tipo y especificar su formato y posición. Cuando se aplica la marca de agua a un documento, todos los elementos de la marca de agua se aplican al documento al mismo tiempo, en el orden en que se añaden a la marca de agua.

Normalmente, se utilizan marcas de agua basadas en PDF para incluir contenido gráfico, como logotipos o símbolos especiales, como copyright o marca registrada.

Puede cambiar los límites en el número de elementos de marca de agua y el tamaño del archivo PDF modificando el archivo de configuración de seguridad del documento. Consulte [Cambiar los parámetros de configuración de marca de agua](configuring-client-server-options.md#change-the-watermark-configuration-parameters).

Tenga en cuenta lo siguiente cuando configure marcas de agua:

* No se puede usar un documento PDF protegido con contraseña como elemento de marca de agua. Sin embargo, si la marca de agua que crea contiene otros elementos que no están protegidos por contraseña, se aplicarán como parte de la marca de agua.
* Puede cambiar el tamaño máximo del archivo PDF que desea utilizar como elemento de marca de agua. Sin embargo, los documentos PDF de gran tamaño utilizados como marcas de agua degradan el rendimiento durante la sincronización sin conexión de los documentos aplicados con dichas marcas de agua. Consulte [Cambiar los parámetros de configuración de marca de agua](configuring-client-server-options.md#change-the-watermark-configuration-parameters).
* Solo se utiliza como marca de agua la primera página del PDF seleccionado. Asegúrese de que la información que desea que aparezca como marca de agua esté disponible en la primera página.
* Aunque puede especificar la escala del documento PDF, tenga en cuenta el tamaño y la presentación de la página del PDF si desea utilizarla como marca de agua en el encabezado, pie de página o márgenes.
* Cuando especifique el nombre de la fuente, escriba el nombre correctamente. AEM formularios sustituye la fuente especificada si no está presente en el equipo cliente donde se abre el documento.
* Si seleccionó texto como contenido de marca de agua, especificar la opción de escalado como Ajustar a página no funciona para páginas con anchura diferente.
* Cuando especifique el posicionamiento de los elementos de marca de agua, asegúrese de que no haya más de un elemento con la misma posición. Si dos elementos de marca de agua tienen la misma posición, como el centro, aparecen superpuestos en el documento y en el orden en que se añadieron a la marca de agua.
* Al especificar el tamaño y el tipo de fuente, asegúrese de que la longitud del texto sea completamente visible dentro de la página. El contenido del texto se desplaza a nuevas líneas, por lo que el contenido de marca de agua que pretendía estar presente en los márgenes puede superponerse en las áreas de contenido de las páginas. Sin embargo, si el documento se abre en Acrobat 9, el texto que va más allá de la línea única se trunca.

### Limitaciones de las marcas de agua dinámicas {#limitations-of-dynamic-watermarks}

Es posible que algunas aplicaciones cliente no admitan marcas de agua dinámicas. Consulte la Ayuda de las extensiones de Acrobat Reader DC correspondientes. Además, tenga en cuenta lo siguiente sobre las versiones de Acrobat que admiten marcas de agua dinámicas:

* No se puede usar un documento PDF protegido con contraseña como elemento de marca de agua.
* Las versiones anteriores a la 10 de Acrobat y Adobe Reader no admiten las siguientes funciones de marca de agua:

   * Marcas de agua PDF
   * Varios elementos de la marca de agua (Texto/PDF)
   * Opciones avanzadas, como el intervalo de páginas o las opciones de visualización
   * Opciones de formato de texto, como fuente especificada, nombre de fuente y color. Sin embargo, las versiones anteriores de Acrobat y Reader mostrarán el contenido del texto en la fuente y el color predeterminados.

* Acrobat 9.0 y versiones anteriores: Acrobat 9.0 y versiones anteriores no admiten nombres de políticas en marcas de agua dinámicas. Si Acrobat 9.0 abre un documento protegido por políticas con una marca de agua dinámica que incluye un nombre de política y otros datos dinámicos, la marca de agua se muestra sin el nombre de la política. Si la marca de agua dinámica solo incluye el nombre de la directiva, Acrobat muestra un mensaje de error

### Agregar una plantilla de marca de agua dinámica {#add-a-dynamic-watermark-template}

Puede crear plantillas de marca de agua dinámicas. Estas plantillas siguen estando disponibles como opción de configuración para las políticas que crean los administradores o los usuarios.

>[!NOTE]
>
>La información de configuración de las marcas de agua dinámicas no se captura con el resto de la información de configuración al exportar un archivo de configuración.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Marcas de agua.
1. Haga clic en Nuevo.
1. En el cuadro Nombre, escriba un nombre para la nueva marca de agua.

   ***nota **: No se pueden utilizar algunos caracteres especiales en los nombres o descripciones de marcas de agua o elementos de marcas de agua. Consulte las restricciones enumeradas en [Consideraciones para editar directivas](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. En Nombre, junto al signo más, escriba un nombre significativo para el elemento de marca de agua como Encabezado, añada una descripción y expanda el signo más para mostrar las opciones.
1. En Origen, seleccione el tipo de marca de agua como Texto o PDF.
1. Si ha seleccionado Texto, haga lo siguiente:

   * Seleccione los tipos de marca de agua que desea incluir. Si selecciona Texto personalizado, en el cuadro adyacente, escriba el texto que se mostrará para la marca de agua. Tenga en cuenta la longitud del texto que aparecerá como marca de agua.
   * Especifique las propiedades de formato del texto, como el nombre de la fuente, el tamaño de la fuente, el color de primer plano y el color de fondo para el contenido del texto de la marca de agua. Especifique el color de primer y segundo plano como valores hexadecimales.

      ***nota **: Si selecciona la opción de escalado como Ajustar a página, la propiedad tamaño de fuente no estará disponible para edición.*

1. Si seleccionó PDF para opciones de marca de agua enriquecida, haga clic en **Examinar** junto a Seleccionar PDF de marca de agua para seleccionar el documento PDF que desea utilizar como marca de agua.

   ***nota **: No utilice un documento PDF protegido por contraseña. Si especifica un PDF protegido con contraseña como elemento de marca de agua, la marca de agua no se aplicará.*

1. En Utilizar como fondo, seleccione Sí o No.

   **nota**: Actualmente, la marca de agua aparece en primer plano independientemente de esta configuración.

1. Para controlar dónde se muestra la marca de agua en el documento, configure las opciones Alineación vertical y Alineación horizontal.
1. Seleccione Ajustar a página o seleccione % y escriba un porcentaje en el cuadro. El valor debe ser un número entero, no una fracción. Para configurar el tamaño de la marca de agua, puede utilizar un valor que sea el porcentaje de la página o establecer la marca de agua para que se ajuste al tamaño de la página.
1. En el cuadro Rotación, escriba los grados que girarán la marca de agua. El rango es de -180 a 180. Utilice un valor negativo para girar la marca de agua en sentido contrario al de las agujas del reloj. El valor debe ser un número entero, no una fracción.
1. En el cuadro Opacidad, escriba un porcentaje. Utilice un número entero, no una fracción.
1. En Opciones avanzadas, configure lo siguiente:

   **Opciones de rango de página**

   Defina el rango de páginas donde se debe mostrar la marca de agua. Escriba la página de inicio como 1 y la página final como -1 para que todas las páginas estén marcadas con la marca de agua.

   **Opciones de visualización**

   Seleccione dónde desea que aparezca la marca de agua. De forma predeterminada, la marca de agua aparece tanto en la copia en pantalla (en línea) como en la copia impresa (impresa).

1. Haga clic en **Nuevo** en Elementos de marca de agua para agregar más elementos de marca de agua si es necesario.
1. Haga clic en Aceptar.

### Editar una plantilla de marca de agua dinámica {#edit-a-dynamic-watermark-template}

1. En la consola de administración, haga clic en Servicios > seguridad del documento > Configuración > Marcas de agua.
1. Haga clic en la marca de agua adecuada de la lista.
1. En la página Editar marcas de agua , cambie la configuración según sea necesario.
1. Haga clic en Aceptar.

### Eliminar una plantilla de marca de agua dinámica {#delete-a-dynamic-watermark-template}

Cuando elimine una marca de agua dinámica, ya no estará disponible para agregarla a una política nueva. Sin embargo, la marca de agua permanece en las políticas existentes que la utilizan actualmente, y los documentos que la política protege actualmente siguen mostrando la marca de agua dinámica hasta que usted o un usuario editen la política que contiene la marca de agua eliminada. Una vez editada la directiva, ya no se aplica la marca de agua. Aparece un mensaje que indica que la marca de agua existente se elimina en la directiva y que el usuario puede seleccionar otra para reemplazarla.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Marcas de agua.
1. Seleccione la casilla de verificación situada junto a la marca de agua correspondiente y haga clic en Eliminar.
1. Haga clic en Aceptar.

## Configuración del registro de usuario invitado {#configuring-invited-user-registration}

Los usuarios externos a su organización pueden registrarse con seguridad de documentos. Los usuarios invitados que se registran y activan sus cuentas pueden iniciar sesión en el documento de seguridad utilizando su dirección de correo electrónico y la contraseña que crean cuando se registran. Los usuarios invitados registrados pueden utilizar documentos protegidos por políticas a los que tienen permisos.

Cuando se activan los usuarios invitados, se convierten en usuarios locales. Los usuarios locales se pueden configurar y administrar utilizando el área Usuarios invitados y locales . (Consulte [Administración de cuentas de usuario locales e invitadas](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts)).

Según las capacidades que habilite para los usuarios invitados, también pueden utilizar estas funciones de seguridad de documentos:

* Aplicar directivas a documentos
* Crear políticas
* Agregar usuarios invitados a las directivas

La seguridad del documento genera automáticamente un correo electrónico de invitación de registro cuando se producen los siguientes eventos a menos que el usuario ya esté en el directorio LDAP de origen o se le haya invitado previamente a registrarse:

* Un usuario existente agrega un usuario invitado a una directiva
* Un administrador añade una cuenta de usuario invitada en la página Registro de usuarios invitados .

El correo electrónico de registro contiene un vínculo a una página de registro e información sobre cómo registrarse. Una vez que el usuario invitado se registre, documente los problemas de seguridad mediante un correo electrónico de activación con un vínculo a una página de activación. Cuando se activa, la cuenta permanece válida hasta que la desactive o elimine.

Si habilita el registro integrado, solo una vez especifica el servidor SMTP, los detalles del correo electrónico de registro, las capacidades de acceso y restablece la información de correo electrónico de contraseña. Antes de habilitar el registro integrado, asegúrese de que ha creado un dominio local en Administración de usuarios y ha asignado la función &quot;Usuario invitado de seguridad de documentos&quot; a los usuarios y grupos adecuados de su organización. (Consulte [Añadir un dominio local](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) y [Creación y configuración de funciones](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)). Si no utiliza el registro integrado, debe tener su propio sistema de registro de usuario creado con el SDK de AEM forms. Consulte la ayuda sobre &quot;Desarrollo de SPI para formularios AEM&quot; en [Programación con formularios AEM](https://www.adobe.com/go/learn-aemforms-programming-63). Si no utiliza la opción Registro integrado , se recomienda configurar un mensaje en el correo electrónico de activación y en la pantalla de inicio de sesión del cliente para notificar a los usuarios cómo ponerse en contacto con el administrador para obtener una contraseña nueva o para obtener otra información.

**Habilitar y configurar el registro de usuario invitado**

De forma predeterminada, el proceso de registro de usuarios invitados está desactivado. Puede habilitar y deshabilitar el registro de usuarios invitados para la seguridad de documentos, según sea necesario.

1. En la consola de administración, haga clic en Servicios > seguridad del documento > Configuración > Registro de usuarios invitados.
1. Seleccione Activar registro de usuario invitado.
1. (Opcional) Actualice la configuración de registro del usuario invitado como sea necesario:

   * [Excluir o incluir un usuario o grupo externo](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Parámetros de cuenta de registro y servidor](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Configuración de correo electrónico de invitación de registro](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Configuración del correo electrónico de activación](configuring-client-server-options.md#activation-email-settings)
   * [Configuración de un correo electrónico de restablecimiento de contraseña](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Opcional) En Registro integrado, seleccione Sí para activar esta opción. Si no habilita el registro integrado, debe configurar su propio sistema de registro de usuario.
1. Haga clic en Aceptar.

### Excluir o incluir un usuario o grupo externo {#exclude-or-include-an-external-user-or-group}

Puede restringir el registro con seguridad de documento para determinados usuarios o grupos de usuarios externos. Esta opción es útil, por ejemplo, para permitir el acceso a un determinado grupo de usuarios, pero excluir personas específicas que forman parte del grupo.

Las siguientes opciones de configuración se encuentran en el área Filtro de restricción de correo electrónico de la página Registro de usuarios invitados .

**Exclusión:** escriba la dirección de correo electrónico de un usuario o grupo para excluir. Para excluir varios usuarios o grupos, escriba cada dirección de correo electrónico en una nueva línea. Para excluir a todos los usuarios que pertenecen a un dominio en particular, introduzca un comodín y el nombre de dominio. Por ejemplo, para excluir a todos los usuarios del dominio example.com, escriba &amp;ast;.example.com.

**Inclusión:** escriba la dirección de correo electrónico de un usuario o grupo para incluir. Para incluir varios usuarios o grupos, escriba cada dirección de correo electrónico en una nueva línea. Para incluir a todos los usuarios que pertenecen a un dominio en particular, introduzca un comodín y el nombre de dominio. Por ejemplo, para incluir a todos los usuarios en el dominio example.com, escriba &amp;ast;.example.com.

### Parámetros de cuenta de registro y servidor {#server-and-registration-account-parameters}

Las siguientes opciones de configuración se encuentran en el área Configuración general de la página Registro de usuarios invitados .

**Host SMTP:** el nombre de host del servidor SMTP. El servidor SMTP administra los avisos de correo electrónico salientes para registrar y activar las cuentas de usuario invitadas.

Si el host SMTP lo requiere, escriba la información necesaria en los cuadros Nombre de cuenta del servidor SMTP y Contraseña de cuenta del servidor SMTP para conectarse al servidor SMTP. Algunas organizaciones no aplican este requisito. Si necesita información, consulte con el administrador del sistema.

**Nombre de clase del socket del servidor SMTP:** Nombre de clase de socket para el servidor SMTP. Por ejemplo, javax.net.ssl.SSLSocketFactory.

**Tipo de contenido de correo electrónico:** tipo MIME aceptado como text/plain o text/html.

**Codificación de correo electrónico:**  formato de codificación que se utiliza al enviar mensajes de correo electrónico. Puede especificar cualquier codificación, por ejemplo, UTF-8 para Unicode o ISO-8859-1 para latín. El valor predeterminado es UTF-8.

**Dirección de correo electrónico de redirección:** cuando especifica una dirección de correo electrónico para esta configuración, cualquier invitación nueva se envía a la dirección proporcionada. Esta configuración puede resultar útil para realizar pruebas.

**Usar dominios locales:** seleccione el dominio correspondiente. En una nueva instalación, asegúrese de que ha creado el dominio mediante Administración de usuarios. Si se trata de una actualización, se creó un dominio de usuario externo durante la actualización y se puede utilizar.

**Usar SSL para servidor SMTP:** seleccione esta opción para habilitar SSL para el servidor SMTP.

**Mostrar vínculo de inicio de sesión en la página de registro:** muestra un vínculo de inicio de sesión en la página de registro que muestran los usuarios invitados.

**Para habilitar Seguridad de capa de transporte (TLS) para el servidor SMTP**

1. Abra la consola de administración.

   La ubicación predeterminada de la consola de administración es `https://<server>:<port>/adminui`.

1. Vaya a Inicio > Servicios > Seguridad de documentos > Configuración > Registro de usuarios invitados.
1. En Registro de usuarios invitados, especifique todos los ajustes de configuración y haga clic en Aceptar.

   >[!NOTE]
   >
   >Si utiliza Microsoft Office 365 como servidor SMTP para enviar las invitaciones para el registro de usuarios, use la siguiente configuración:
   >
   >**Host SMTP:** smtp.office365.com
   >**Puerto:** 587

1. A continuación, debe actualizar el archivo config.xml. Consulte [Configuración para habilitar SMTP para Seguridad de capa de transporte (TLS)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>Si realiza cambios en las opciones de Registro de usuarios invitados, el archivo config.xml se sobrescribe y TLS se desactiva. Si sobrescribe los cambios, debe realizar el paso anterior para reactivar la compatibilidad con TLS para el registro de usuarios invitados.

### Configuración de correo electrónico de invitación de registro {#registration-invitation-email-settings}

La seguridad de los documentos envía automáticamente un correo electrónico de invitación de registro cuando se crea una nueva cuenta de usuario invitada o cuando un usuario existente agrega un destinatario externo que no se ha registrado previamente o al que se ha invitado a registrarse en una directiva. El correo electrónico contiene un vínculo que el destinatario puede utilizar para acceder a la página de registro e introducir información de cuenta personal, incluidos el nombre de usuario y la contraseña. La contraseña puede ser cualquier combinación de ocho caracteres.

Cuando el destinatario activa la cuenta, el usuario se convierte en un usuario local.

Los siguientes ajustes se encuentran en el área Configuración de correo electrónico de invitación de la página Registro de usuarios invitados .

**De:** la dirección de correo electrónico desde la que se envía el correo electrónico de invitación. El formato predeterminado de la dirección de correo electrónico De es postmaster@[your_installation_domain].com.

**Asunto:** Asunto predeterminado del mensaje de correo electrónico de invitación.

**Tiempo de espera:** el número de días después de los cuales caduca la invitación de registro si el usuario externo no se registra. El valor predeterminado es 30 días.

**Mensaje:** texto que aparece en el cuerpo del mensaje invitando al usuario a registrarse.

### Configuración del correo electrónico de activación {#activation-email-settings}

Una vez que los usuarios invitados se registran, la seguridad del documento envía un correo electrónico de activación. El correo electrónico de activación contiene un vínculo a la página de activación de la cuenta donde los usuarios pueden activar su cuenta. Cuando se activan las cuentas, los usuarios pueden iniciar sesión en un documento de seguridad utilizando su dirección de correo electrónico y la contraseña que crearon cuando se registraron.

Cuando el destinatario activa la cuenta de usuario, el usuario se convierte en un usuario local.

Los siguientes ajustes se encuentran en el área Configuración de correo electrónico de activación de la página Registro de usuarios invitados .

>[!NOTE]
>
>También se recomienda configurar un mensaje en la pantalla de inicio de sesión para aconsejar a los usuarios externos cómo ponerse en contacto con su administrador para obtener una contraseña nueva o para obtener otra información.

**De:** la dirección de correo electrónico desde la que se envía el correo electrónico de activación. Esta dirección de correo electrónico recibe notificaciones de entrega fallidas del host de correo electrónico del registrador y también cualquier mensaje que el destinatario envíe en respuesta al correo electrónico de registro. El formato predeterminado de la dirección de correo electrónico De es postmaster@[your_installation_domain].com.

**Asunto:** Asunto predeterminado del mensaje de correo electrónico de activación.

**Tiempo de espera:** el número de días después de los cuales caduca la invitación de activación si el usuario no activa la cuenta. El valor predeterminado es 30 días.

**Mensaje:** El texto que aparece en el cuerpo del mensaje es un mensaje que indica que la cuenta de usuario del destinatario debe activarse. También es posible que desee incluir información como cómo ponerse en contacto con un administrador para obtener una nueva contraseña.

### Configurar un correo electrónico de restablecimiento de contraseña {#configure-a-password-reset-email}

Si tiene que restablecer la contraseña de un usuario invitado, se genera un correo electrónico de confirmación que invita al usuario a elegir una nueva contraseña. No se puede determinar la contraseña de un usuario; si el usuario lo olvida, debe restablecerlo.

Las siguientes opciones de configuración se encuentran en el área Restablecer correo electrónico de contraseña de la página Registro de usuarios invitados .

**De:** la dirección de correo electrónico desde la que se envía el correo electrónico de restablecimiento de contraseña. El formato predeterminado de la dirección de correo electrónico De es postmaster@[your_installation_domain].com.

**Asunto:** Asunto predeterminado para el mensaje de correo electrónico de restablecimiento.

**Mensaje:** El texto que aparece en el cuerpo del mensaje es un mensaje que indica que se restablece la contraseña de usuario externa del destinatario.

## Permitir que los usuarios y grupos creen directivas {#enable-users-and-groups-to-create-policies}

La página Configuración tiene un vínculo a la página Mis políticas, donde especifica qué usuarios finales pueden crear mis políticas y qué usuarios y grupos son visibles en los resultados de búsqueda. La página Mis políticas tiene dos pestañas:

**Ficha Crear políticas:** utilice para configurar los permisos de usuario para crear políticas personalizadas.

**Pestaña Usuarios y grupos visibles:**  permite controlar qué usuarios y grupos son visibles en los resultados de búsqueda de los usuarios. El superusuario o administrador del conjunto de directivas es necesario para seleccionar y agregar dominios, creados en Administración de usuarios, al usuario y grupo visibles para cada conjunto de directivas. Esta lista es visible para el coordinador de conjuntos de políticas y se utiliza para poner límites en los dominios que el coordinador de conjuntos de políticas puede examinar al elegir usuarios para agregar a políticas.

Antes de conceder permiso a los usuarios para crear políticas personalizadas, considere cuánto acceso o control desea que tengan los usuarios individuales. Además, tenga en cuenta la exposición que desea que tengan sus usuarios y grupos cuando los haga visibles a las búsquedas.

### Especifique usuarios y grupos que puedan crear directivas {#specify-users-and-groups-who-can-create-policies}

Como administrador, especifique qué usuarios y grupos pueden crear directivas personalizadas. Este permiso se puede establecer a nivel de usuario y grupo. La funcionalidad de búsqueda busca usuarios y grupos en la base de datos de Administración de usuarios.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Configuración > Mis directivas.
1. En la página Mis políticas, haga clic en la ficha Crear políticas y, después, en Agregar usuarios y grupos.
1. En el cuadro Buscar, escriba el nombre de usuario o la dirección de correo electrónico del usuario o grupo que está buscando. Si no dispone de esta información, deje vacía la casilla . También puede escribir un nombre parcial o una dirección de correo electrónico, como cuando solo conoce las dos primeras letras de un nombre de usuario.
1. En la lista Uso, seleccione los parámetros de búsqueda Nombre o Correo electrónico.
1. En la lista Tipo, seleccione Grupo o Usuario para limitar la búsqueda.
1. En la lista En , seleccione el dominio en el que desea buscar. Si no conoce el dominio del usuario o grupo, seleccione Todos los dominios.
1. En la lista Mostrar, especifique el número de resultados de búsqueda que se mostrarán por página y, a continuación, haga clic en Buscar.
1. Para agregar usuarios y grupos de Mis directivas, seleccione la casilla de verificación de cada usuario y grupo que desee agregar.
1. Haga clic en Agregar y, a continuación, en Aceptar.

Los usuarios y grupos seleccionados ahora tienen permiso para crear políticas personalizadas.

### Elimine el permiso crear políticas personalizadas de un usuario o grupo {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. En la página de seguridad del documento, haga clic en Configuración > Mis directivas.
1. En la página Mis políticas, haga clic en la ficha Crear políticas . Se muestran los usuarios y grupos con permisos para crear políticas personalizadas.
1. Seleccione la casilla de verificación situada junto a los usuarios y grupos que desea quitar de este permiso.
1. Haga clic en Eliminar y, a continuación, en Aceptar.

### Especificar usuarios y grupos que sean visibles en las búsquedas {#specify-users-and-groups-that-are-visible-in-searches}

Cuando los usuarios administran sus políticas personalizadas, pueden buscar usuarios y grupos para agregarlos a sus políticas. Debe especificar los dominios desde los cuales los usuarios y grupos están visibles en estas búsquedas.

1. En la página de seguridad del documento, haga clic en Configuración > Mis directivas.
1. En la página Mis políticas, haga clic en la ficha Usuarios y grupos visibles .
1. Para que los usuarios y grupos de un dominio estén visibles, haga clic en Añadir dominios, seleccione los dominios y haga clic en Agregar. Para quitar un dominio, active la casilla situada junto al nombre de dominio y haga clic en Eliminar.

## Edición manual del archivo de configuración de seguridad del documento {#manually-editing-the-document-security-configuration-file}

Puede importar y exportar la información de configuración almacenada en la base de datos de seguridad del documento. Por ejemplo, es posible que desee realizar una copia de seguridad de la información de configuración cuando pase de un entorno de ensayo a un entorno de producción, o que desee editar las opciones avanzadas que solo se pueden configurar para editar este archivo.

Puede realizar los siguientes cambios utilizando el archivo de configuración:

[Mostrar permisos de CATIA al crear y editar políticas](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Especificación de un período de tiempo de espera para la sincronización sin conexión](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Denegación de servicios de seguridad de documentos para aplicaciones específicas](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Cambiar los parámetros de configuración de marca de agua](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Desactivación de vínculos externos](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>Al importar el archivo de configuración, se reconfigura el sistema según la información del archivo. Las excepciones son la configuración dinámica de marcas de agua y la información de eventos personalizados, que no se guardan con el archivo de configuración exportado. Debe configurar esta información manualmente en el nuevo sistema. Solo un administrador del sistema o un consultor de servicios profesionales que estén familiarizados con la seguridad de documentos y XML deben modificar el contenido de un archivo de configuración, como para reconfigurar una configuración dañada o ajustar parámetros para un escenario de implementación empresarial en particular.

**Exportación de un archivo de configuración**

1. En la consola de administración, haga clic en Servicios > seguridad del documento 11 > Configuración > Configuración manual.
1. Haga clic en Exportar y guarde el archivo de configuración en otra ubicación. El nombre de archivo predeterminado es config.xml.
1. Haga clic en Aceptar.
1. Antes de cambiar el archivo de configuración, realice una copia de seguridad en caso de que necesite revertir.

**Importar un archivo de configuración**

1. En la consola de administración, haga clic en Servicios > seguridad del documento 11 > Configuración > Configuración manual.
1. Haga clic en Examinar para ir al archivo de configuración y, a continuación, haga clic en Importar. No se puede escribir la ruta directamente en el cuadro Nombre de archivo.
1. Haga clic en Aceptar.

### Especifique un período de tiempo de espera para la sincronización sin conexión {#specify-a-timeout-period-for-offline-synchronization}

La seguridad de los documentos permite a los usuarios abrir y utilizar documentos protegidos cuando no están conectados al servidor de seguridad de documentos. La aplicación cliente del usuario debe sincronizarse regularmente con el servidor para mantener los documentos válidos para su uso sin conexión. La primera vez que los usuarios abren un documento protegido, se les pregunta si su equipo debe estar autorizado para realizar la sincronización periódica del cliente.

De forma predeterminada, la sincronización se produce automáticamente cada cuatro horas y según sea necesario cuando un usuario está conectado al servidor de seguridad de documentos. Si el periodo sin conexión de un documento caduca mientras el usuario está sin conexión, el usuario debe volver a conectarse al servidor para permitir que la aplicación cliente se sincronice con el servidor.

En el archivo de configuración de seguridad del documento, puede especificar la frecuencia predeterminada de la sincronización en segundo plano automática. Esta configuración actúa como la aplicación cliente del periodo de espera predeterminado, a menos que el cliente establezca explícitamente su propio valor de tiempo de espera.

1. Exporte el archivo de configuración de seguridad del documento. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Abra el archivo de configuración en un editor y busque el nodo `PolicyServer` . Bajo ese nodo, busque el nodo `ServerSettings`.
1. En el nodo `ServerSettings`, agregue esta entrada siguiente y, a continuación, guarde el archivo:

   `<entry key="BackgroundSyncFrequency" value="`*time* `"/>`

   donde *time* es el número de segundos entre las sincronizaciones automáticas de fondo. Si ha enviado este valor a `0`, la sincronización siempre se produce. El valor predeterminado es `14400` segundos (cada cuatro horas).

1. Importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

### Denegación de servicios de seguridad de documentos para aplicaciones específicas {#denying-document-security-services-for-specific-applications}

Puede configurar la seguridad del documento para denegar servicios a aplicaciones que cumplan criterios específicos. Los criterios pueden especificar un único atributo, como un nombre de plataforma, o varios conjuntos de atributos. Esta función puede ayudarle a controlar las solicitudes que debe gestionar la seguridad del documento. Estas son algunas aplicaciones de esta función:

* **Protección de ingresos:** es posible que desee denegar el acceso a cualquier aplicación cliente que no admita sus convenciones de ingresos.
* **Compatibilidad de aplicaciones:** Algunas aplicaciones pueden ser incompatibles con las políticas o el comportamiento del servidor de seguridad de documentos.

Cuando las aplicaciones cliente intentan establecer un vínculo con la seguridad del documento, proporcionan información sobre la aplicación, la versión y la plataforma. La seguridad de los documentos compara esta información con las opciones de Denials que obtiene del archivo de configuración de seguridad del documento.

La configuración de denegación puede contener varios conjuntos de condiciones de denegación. Si todos los atributos de cualquier conjunto coinciden, se deniega a la aplicación solicitante el acceso a los servicios de seguridad de documentos.

La función de denegación de servicio requiere que las aplicaciones cliente utilicen la seguridad del documento C++ Client SDK versión 8.2 o posterior. Los siguientes productos de Adobe proporcionan información de producto al solicitar servicios de seguridad de documentos:

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard y versiones posteriores
* Adobe Reader 9.0 y versiones posteriores
* Extensiones de Acrobat Reader DC para Microsoft Office 8.2 y posterior

Las aplicaciones cliente utilizan la API de cliente del SDK de cliente C++ de seguridad de documento para solicitar servicios de seguridad de documentos. Las solicitudes de API de cliente incluyen información de la plataforma y la versión del SDK (precompilada en la API de cliente) e información del producto obtenida de la aplicación cliente.

Las aplicaciones o complementos de cliente proporcionan información de producto en la implementación de una función de llamada de retorno. La aplicación proporciona la siguiente información:

* Nombre del integrador
* Versión de Integrator
* Familia de aplicaciones
* Nombre de la aplicación
* Versión de la aplicación

Si alguna información no es aplicable, la aplicación cliente deja el campo correspondiente en blanco.

Varias aplicaciones de Adobe incluyen información de producto al solicitar servicios de seguridad de documentos, incluidas Acrobat, Adobe Reader y extensiones de Acrobat Reader DC para Microsoft Office.

**Acrobat y Adobe Reader**

Cuando Acrobat o Adobe Reader solicitan un servicio desde la seguridad de documentos, proporcionan la siguiente información del producto:

* **Integrador:** Adobe Systems, Inc.
* **Versión de integrador:** 1.0
* **Familia de aplicaciones:** Acrobat
* **Nombre de la aplicación:** Acrobat
* **Versión de la aplicación:** 9.0.0

**Extensiones de Acrobat Reader DC para Microsoft Office**

Las extensiones de Acrobat Reader DC para Microsoft Office son un complemento que se utiliza con los productos de Microsoft Office Microsoft Word, Microsoft Excel y Microsoft PowerPoint. Cuando solicita un servicio, proporciona la siguiente información:

* **Integrador:** Adobe Systems Incorporated
* **Versión de integrador:** 8.2
* **Familia de aplicaciones:** Extensiones de Acrobat Reader DC para Microsoft Office
* **Nombre de la aplicación:** Microsoft Word, Microsoft Excel o Microsoft PowerPoint
* **Versión de la aplicación:** 2003 o 2007

**Configure la seguridad de documentos para denegar servicios para aplicaciones específicas**

1. Exporte el archivo de configuración de seguridad del documento. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Abra el archivo de configuración en un editor y busque el nodo `PolicyServer` . Agregue un nodo `ClientVersionRules` como secundario inmediato del nodo `PolicyServer`, si no existe:

   ```xml
    <node name="ClientVersionRules">
        <map>
            <entry key="infoURL" value="URL"/>
        </map>
        <node name="Denials">
            <map/>
            <node name="MyEntryName">
                <map>
                    <entry key="SDKPlatforms" value="platforms"/>
                    <entry key="SDKVersions" value="versions"/>
                    <entry key="AppFamilies" value="families"/>
                    <entry key="AppNames" value="names"/>
                    <entry key="AppVersions" value="versions"/>
                    <entry key="Integrators" value="integrators"/>
                    <entry key="IntegratorVersions" value="versions"/>
                </map>
            </node>
            <node name="MyOtherEntryName"
                <map>
                    [...]
                </map>
            </node>
            [...]
        </node>
    </node>
   ```

   donde:

   `SDKPlatforms` especifica la plataforma que aloja la aplicación cliente. Los valores posibles son:

   * Microsoft Windows
   * Apple OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` especifica la versión de la API de cliente C++ de seguridad de documento que utiliza la aplicación cliente. Por ejemplo, `"8.2"`.

   `APPFamilies` está definido por la API de cliente.

   `AppName`especifica el nombre de la aplicación cliente. Las comas se utilizan como separadores de nombres. Para incluir una coma en un nombre, escapa con una barra invertida (\). Por ejemplo, *&quot;Adobe Systems\, Inc.&quot;*.

   `AppVersions` especifica la versión de la aplicación cliente.

   `Integrators` especifica el nombre de la empresa o grupo que desarrolló el complemento o la aplicación integrada.

   `IntegratorVersions` es la versión del complemento o la aplicación integrada.

1. Para cada conjunto adicional de datos de denegación, agregue otro elemento *MyEntryName*.
1. Guarde el archivo de configuración.
1. Importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

**Ejemplos**

En este ejemplo, se deniega el acceso a todos los clientes de Windows.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://www.dont.use/windows.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="SDKPlatforms" value="Microsoft Windows"/>
             </map>
         </node>
     </node>
 </node>
```

En este ejemplo, My Application versión 3.0 y My Other Application versión 2.0 no tienen acceso. Se utiliza la misma URL de información de denegación independientemente del motivo de la denegación.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value=”https://get.a.new/version.html”/>
     </map>
     <node name="Denials">
         <map/>
         <node name="FirstDenialSettings">
             <map>
                 <entry key="AppNames" value="My Application"/>
                 <entry key="AppVersions" value="3.0"/>
             </map>
         </node>
         <node name="SecondDenialSettings">
             <map>
                 <entry key="AppNames" value="My Other Application"/>
                 <entry key="AppVersions" value="2.0"/>
             </map>
         </node>
     </node>
 </node>
```

En este ejemplo, se deniegan todas las solicitudes de instalación de extensiones de Acrobat Reader DC de Microsoft PowerPoint 2007 o Microsoft PowerPoint 2010 para Microsoft Office.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value=”https://get.a.new/version.html”/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="AppFamilies" value=
     "document security Extension for Microsoft Office"/>
                 <entry key="AppNames" value= "Microsoft PowerPoint"/>
                 <entry key="AppVersions" value="2007,2010"/>
             </map>
         </node>
     </node>
 </node
```

### Cambiar los parámetros de configuración de marca de agua {#change-the-watermark-configuration-parameters}

De forma predeterminada, puede especificar un máximo de cinco elementos en una marca de agua. Además, el tamaño máximo del archivo del documento PDF que desea utilizar como marca de agua está limitado a 100 KB. Puede cambiar estos parámetros en el archivo config.xml.

***nota **: Debe cambiar estos parámetros con precaución.*

1. Exporte el archivo de configuración de seguridad del documento. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Abra el archivo de configuración en un editor y busque el nodo `ServerSettings` .
1. En el nodo `ServerSettings`, agregue las siguientes entradas y, a continuación, guarde el archivo: `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   La primera entrada, *max file size* es el tamaño máximo del archivo (en KB) permitido para un elemento de marca de agua PDF. El valor predeterminado es 100 KB.

   La segunda entrada, *max elements* es el número máximo de elementos permitidos en una marca de agua. El valor predeterminado es 5.

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

### Desactivación de vínculos externos {#disabling-external-links}

Muchos usuarios de seguridad de documentos no tienen acceso a vínculos externos como **www.adobe.com** mientras utilizan las interfaces de usuario de Administración correcta:

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

Los siguientes cambios en config.xml desactivan todos los vínculos externos desde las interfaces de usuario de Administración de derechos.

1. Exporte el archivo de configuración de seguridad del documento. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Abra el archivo de configuración en un editor y busque el nodo `DisplaySettings` .
1. Para desactivar todos los vínculos externos, en el nodo `DisplaySettings`, agregue la siguiente entrada y guarde el archivo: `<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

### Configuración para habilitar SMTP para Seguridad de capa de transporte (TLS) {#configuration-to-enable-smtp-for-transport-layer-security-tls}

Los siguientes cambios en config.xml habilitan la compatibilidad con TLS para la función Registro de usuarios invitados .

1. Exporte el archivo de configuración de seguridad del documento. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Abra el archivo de configuración en un editor y busque el nodo `DisplaySettings` .
1. Busque el nodo siguiente: `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. Establezca el valor de la clave `SmtpUseTls` en el nodo `ExternalUser` en **true**.
1. Establezca el valor de la clave `SmtpUseSsl` en el nodo `ExternalUser` en **false**.
1. Guarde el `config.xml`.
1. Importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

### Desactivación de extremos SOAP para documentos de Seguridad de documentos {#disable-soap-endpoints-for-document-security-documents}

Los siguientes cambios en config.xml para deshabilitar los extremos SOAP para documentos de seguridad de documentos.

1. Exporte el archivo de configuración de seguridad del documento. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Abra el archivo de configuración en un editor y busque el siguiente nodo: `<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. En el nodo DRM, busque el nodo `entry`:

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. Para deshabilitar los extremos SOAP para documentos de seguridad del documento, establezca el atributo value en **false**.

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. Guarde el `config.xml`.
1. Importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

### Aumento de la escalabilidad del servidor de seguridad de documentos {#increasingscalability}

De forma predeterminada, mientras se sincroniza un documento para su uso sin conexión, junto con la información del documento actual, los clientes de seguridad del documento recuperan información de directivas, marcas de agua, licencias y actualizaciones de revocación para todos los demás documentos a los que el usuario tiene acceso. Si estas actualizaciones e información no se sincronizan con el cliente, un documento abierto en modo sin conexión puede seguir abriéndose con información de revocación, marca de agua y directiva anterior.

Puede aumentar la escalabilidad del servidor de seguridad de documentos limitando la información que se envía al cliente. La reducción de la cantidad de información enviada al cliente mejora la escalabilidad, reduce el tiempo de respuesta y mejora el rendimiento del servidor. Siga estos pasos para aumentar la escalabilidad:

1. Exporte el archivo de configuración de seguridad del documento. (Consulte [Edición manual del archivo de configuración de seguridad del documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).
1. Abra el archivo de configuración en un editor y busque el nodo ServerSettings .
1. En el nodo ServerSettings, establezca el valor de la propiedad `DisableGlobalOfflineSynchronizationData`en `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Cuando se establece en true, el servidor de seguridad de documentos envía información solamente para el documento actual y la información para el resto de documentos (a los demás documentos a los que tiene acceso un usuario) no se envía al cliente.

   >[!NOTE]
   >
   >De forma predeterminada, el valor de la clave `DisableGlobalOfflineSynchronizationData`está establecido en `false`.

1. Guarde e importe el archivo de configuración. (Consulte [Edición manual del archivo de configuración de seguridad del documento](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)).

