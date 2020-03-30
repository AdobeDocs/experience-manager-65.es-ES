---
title: Configuración de las opciones de cliente y servidor
seo-title: Configuración de las opciones de cliente y servidor
description: Descubra cómo puede configurar las distintas opciones de cliente y servidor, como la configuración del servidor, las funciones de seguridad de documento y la auditoría de eventos.
seo-description: Descubra cómo puede configurar las distintas opciones de cliente y servidor, como la configuración del servidor, las funciones de seguridad de documento y la auditoría de eventos.
uuid: 1f9f9886-726e-4fad-9ff8-0ff11eef653e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0f069fbc-10c2-403e-9419-5e9920035d75
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configuración del servidor de seguridad de documento {#configure-the-document-security-server}

1. En la consola de administración, haga clic en Servicios > Seguridad de documento > Configuración > Configuración del servidor.
1. Configure los ajustes y haga clic en Aceptar.

## Ajustes de configuración del servidor {#server-configuration-settings}

**Dirección URL base:** Dirección URL de seguridad del documento base, que contiene el nombre del servidor y el puerto. La información anexada a la base crea direcciones URL de conexión. Por ejemplo, /edc/Main.do se adjunta para acceder a las páginas web. Los usuarios también responden a las invitaciones de registro de usuarios externos a través de esta URL.

Si utiliza IPv6, introduzca la URL base como nombre de equipo o nombre DNS. Si utiliza una dirección IP numérica, Acrobat no podrá abrir los archivos protegidos por políticas. También puede utilizar URL HTTP segura (HTTPS) para el servidor.

***Nota **: La dirección URL base está incrustada en los archivos protegidos por políticas. Las aplicaciones cliente utilizan la dirección URL base para volver a conectarse al servidor. Los archivos protegidos seguirán conteniendo la dirección URL base, aunque se cambie más tarde. Si cambia la dirección URL base, la información de configuración deberá actualizarse para todos los clientes que se conecten.*

**Período de arrendamiento sin conexión predeterminado:** El período de tiempo predeterminado que un usuario puede utilizar un documento protegido sin conexión. Esta configuración determina el valor inicial del período de concesión sin conexión automática al crear una política. (Consulte Creación y edición de políticas). Cuando caduca el período de concesión, el destinatario debe volver a sincronizar el documento para continuar utilizándolo.

Para obtener información sobre el funcionamiento de la concesión y sincronización sin conexión, consulte [Manual sobre la configuración de la concesión y la sincronización](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html)sin conexión.

**Período de sincronización sin conexión predeterminado:** El tiempo máximo que se puede utilizar cualquier documento sin conexión desde el momento en que se protege inicialmente.

**Tiempo de espera de sesión del cliente:** Duración, en minutos, después de la cual la seguridad de documento se desconecta si un usuario que ha iniciado sesión a través de una aplicación cliente no interactúa con la seguridad de documento.

**Permitir acceso de usuarios anónimos:** Seleccione esta opción para habilitar la capacidad de crear políticas personales y compartidas que permitan a los usuarios anónimos abrir documentos protegidos por políticas. (Los usuarios que no tienen cuentas pueden acceder al documento, pero no pueden iniciar sesión en seguridad de documento ni utilizar otros documentos protegidos por políticas).

**Deshabilitar el acceso a los clientes de la versión 7:** Especifica si los usuarios pueden utilizar Acrobat o Reader 7.0 para conectarse al servidor. Cuando se selecciona esta opción, los usuarios deben utilizar Acrobat o Reader 8.0 y posterior para completar las operaciones de seguridad de documento en documentos PDF. Si las políticas requieren que Acrobat o Reader 8.0 y posterior se ejecuten en modo certificado al abrir documentos protegidos por políticas, debe desactivar el acceso a Acrobat o Reader 7. (Consulte Especificación de los permisos de documento para usuarios y grupos).

**Permitir acceso sin conexión por documento** Seleccione esta opción para especificar el acceso sin conexión por documento. Si esta configuración está habilitada, el usuario tendrá acceso sin conexión solo a los documentos que el usuario haya abierto en línea al menos una vez.

**Permitir autenticación de contraseña de nombre de usuario:** Seleccione esta opción para permitir que las aplicaciones cliente utilicen la autenticación de nombre de usuario y contraseña al conectarse al servidor.

**Permitir autenticación Kerberos:** Seleccione esta opción para permitir que las aplicaciones cliente utilicen la autenticación Kerberos al conectarse al servidor.

**Permitir autenticación de certificado de cliente:** Seleccione esta opción para permitir que las aplicaciones cliente utilicen la autenticación de certificados al conectarse al servidor.

**Permitir autenticación** extendida Seleccione esta opción para habilitar la autenticación extendida y, a continuación, introduzca la URL de aterrizaje de autenticación extendida.

Al seleccionar esta opción, las aplicaciones cliente pueden utilizar la autenticación extendida. La autenticación extendida proporciona procesos de autenticación personalizados y diferentes opciones de autenticación configuradas en el servidor de formularios AEM. Por ejemplo, ahora los usuarios pueden experimentar la autenticación basada en SAML en lugar de la contraseña/nombre de usuario de los formularios AEM, desde Acrobat y Reader Client. De forma predeterminada, la URL de aterrizaje contiene *localhost* como nombre de servidor. Reemplace el nombre del servidor con un nombre de host completo. El nombre de host en la dirección URL de aterrizaje se rellena automáticamente desde la dirección URL base, si aún no se ha habilitado la autenticación extendida. Consulte [Añadir el proveedor](configuring-client-server-options.md#add-the-extended-authentication-provider)de autenticación ampliado.

***nota **: La autenticación extendida es compatible con Apple Mac OS X con Adobe Acrobat versión 11.0.6 y posterior.*

**Ancho de control HTML preferido para la autenticación** extendida Especifique la anchura del cuadro de diálogo de autenticación extendida que se abre en Acrobat para introducir las credenciales de usuario.

**Alto de control HTML preferido para autenticación** extendida Especifique la altura del cuadro de diálogo de autenticación extendida que se abre en Acrobat para introducir las credenciales de usuario.

***nota **: Los límites de anchura y altura de este cuadro de diálogo son los siguientes:*Ancho: Mínimo = 400, máximo = 900

Altura: Mínimo = 450; máximo = 800

**Habilitar el almacenamiento en caché de credenciales del cliente:** Seleccione esta opción para permitir que los usuarios almacenen en caché sus credenciales (nombre de usuario y contraseña). Cuando las credenciales de los usuarios se almacenan en caché, no tienen que introducir sus credenciales cada vez que abren un documento o cuando hacen clic en el botón Actualizar de la página Administrar políticas de seguridad de Adobe Acrobat. Puede especificar el número de días antes de que los usuarios deban volver a proporcionar sus credenciales. Si se establece el número de días en 0, las credenciales se pueden almacenar en caché indefinidamente.

## Configuración de los usuarios y administradores de seguridad de documento {#configuring-document-security-users-and-administrators}

### Asignación de funciones de seguridad de documento a los administradores {#assigning-document-security-roles-to-administrators}

El entorno de formularios AEM contiene uno o varios usuarios administradores que tienen los privilegios adecuados para crear usuarios y grupos. Si su organización utiliza seguridad de documento, al menos un administrador debe tener asignado el privilegio de administrar los usuarios invitados y locales.

Los administradores también deben tener la función de usuario de la consola de administración para acceder a la consola de administración. (Consulte [Creación y configuración de funciones](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)).

### Configuración de usuarios y grupos visibles {#configuring-visible-users-and-groups}

Para vista de usuarios y grupos en dominios seleccionados durante las búsquedas de usuarios de directivas, un superadministrador o un administrador de conjuntos de directivas debe seleccionar y agregar dominios (creados en Administración de usuarios) a la lista visible de usuarios y grupos para cada conjunto de directivas.

La lista visible de usuario y grupo es visible para el coordinador de conjuntos de políticas y se utiliza para restringir los dominios que el usuario final puede examinar al elegir usuarios o grupos para agregar a las políticas. Si no se realiza esta tarea, el coordinador de conjuntos de políticas no encontrará usuarios ni grupos para agregar a la política. Puede haber más de un coordinador de conjunto de políticas para un conjunto de políticas determinado.

1. Después de instalar y configurar el entorno de formularios de AEM con seguridad de documento, configure todos los dominios adecuados en Administración de usuarios. <!-- Fix broken link (See Setting up and managing domains) -->

   ***nota **: La creación de dominios debe realizarse antes de poder crear políticas.*

1. En la consola de administración, haga clic en Servicios > Administración de Documentos > Directivas y, a continuación, haga clic en la ficha Conjuntos de directivas.
1. Seleccione Conjunto de directivas globales y, a continuación, haga clic en la ficha Usuarios y grupos visibles.
1. Haga clic en Añadir dominios y agregue los dominios existentes según sea necesario.
1. Vaya a Servicios > Seguridad de documento > Configuración > Mis políticas y haga clic en la ficha Usuarios y grupos visibles.
1. Haga clic en Añadir dominios y agregue los dominios existentes según sea necesario.

## Añadir el proveedor de autenticación extendido {#add-the-extended-authentication-provider}

Los formularios AEM proporcionan una configuración de muestra que puede personalizar para su entorno. Siga estos pasos:

>[!NOTE]
>
>La autenticación extendida es compatible con Apple Mac OS X con Adobe Acrobat versión 11.0.6 y posterior.

1. Obtenga el archivo WAR de muestra para implementarlo. Consulte la guía de instalación adecuada para el servidor de aplicaciones.
1. Asegúrese de que el servidor de formularios tiene un nombre completo en lugar de direcciones IP como dirección URL base y de que es una dirección URL HTTPS. Consulte Configuración [del servidor](configuring-client-server-options.md#server-configuration-settings).
1. Habilite Autenticación extendida desde la página Configuración del servidor. Consulte Configuración [del servidor](configuring-client-server-options.md#server-configuration-settings).
1. Añada las direcciones URL de redireccionamiento SSO necesarias en el archivo de configuración de Administración de usuarios. Consulte [Añadir direcciones URL de redireccionamiento de SSO para una autenticación](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication)extendida.

### Añadir direcciones URL de redireccionamiento de SSO para autenticación extendida {#add-sso-redirect-urls-for-extended-authentication}

Con la autenticación extendida activada, los usuarios que abren un documento protegido por una política en Acrobat XI o Reader XI obtienen un cuadro de diálogo para la autenticación. Este cuadro de diálogo carga la página HTML especificada como URL de aterrizaje de autenticación extendida en la configuración del servidor de seguridad de documento. Consulte Configuración [del servidor](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>La autenticación extendida es compatible con Apple Mac OS X con Adobe Acrobat versión 11.0.6 y posterior.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Exportar y guarde el archivo de configuración en el disco.
1. Abra el archivo en un editor y busque el nodo AllowedUrls.
1. En el `AllowedUrls` nodo, agregue las líneas siguientes: `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```as3
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Guarde el archivo y, a continuación, importe el archivo actualizado desde la página Configuración manual: En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.

## Configuración de la seguridad sin conexión {#configuring-offline-security}

La seguridad de documento permite utilizar documentos protegidos por políticas sin conexión a Internet o a la red. Esta capacidad requiere que la directiva permita el acceso sin conexión, como se describe en [Especificar los permisos de documento para usuarios y grupos](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Antes de que un documento que tenga una política de este tipo pueda utilizarse sin conexión, el destinatario debe abrir el documento mientras está en línea y habilitar el acceso sin conexión, haciendo clic en Sí cuando se le solicite. También se podrá pedir al destinatario que autentique su identidad. El destinatario puede utilizar documentos sin conexión durante el período de concesión sin conexión especificado en la política.

Cuando finaliza el período de concesión sin conexión, el destinatario debe volver a sincronizarse con la seguridad de documento abriendo un documento en línea o utilizando un comando de menú de extensiones de Acrobat o Acrobat Reader DC para sincronizarlo. (Consulte la Ayuda *de* Acrobat o la Ayuda *correspondiente de extensiones de* Acrobat Reader DC).

Dado que los documentos que permiten el acceso sin conexión requieren almacenar en caché material clave en el equipo en el que los archivos se almacenan sin conexión, el archivo puede verse comprometido si un usuario no autorizado puede obtener el material clave. Para compensar esta posibilidad, se proporcionan opciones de rollover de claves programadas y manuales que puede configurar para evitar que una persona no autorizada utilice la clave para acceder al documento.

### Establecer un período de concesión sin conexión predeterminado {#set-a-default-offline-lease-period}

Destinatarios de documentos protegidos por políticas pueden desconectar los documentos durante el número de días especificado en la política. Después de sincronizar inicialmente el documento con la seguridad de documento, el destinatario puede utilizarlo sin conexión hasta que caduque el período de concesión sin conexión. Cuando caduque el período de concesión, el destinatario debe poner el documento en línea e iniciar sesión para sincronizar con la seguridad de documento a fin de continuar utilizando el documento.

Puede configurar un período de concesión sin conexión predeterminado. El período de concesión se puede cambiar del valor predeterminado cuando alguien cree o edite una política.

1. En la página de seguridad de documento, haga clic en Configuración > Configuración del servidor.
1. En el cuadro Período de arrendamiento sin conexión predeterminado, escriba el número de días para el período de concesión sin conexión.
1. Haga clic en Aceptar.

### Administrar rollovers clave {#manage-key-rollovers}

La seguridad de Documento utiliza algoritmos de codificación y licencias para proteger documentos. Cuando cifra un documento, la seguridad de documento genera y administra una clave de descifrado denominada *DocKey* que pasa a la aplicación cliente. Si la política que protege un documento permite el acceso sin conexión, también se genera una clave sin conexión denominada clave ** principal para cada usuario que tenga acceso sin conexión al documento.

>[!NOTE]
>
>Si no existe una clave principal, la seguridad de documento genera una para proteger un documento.

Para abrir un documento protegido por una política sin conexión, el equipo del usuario debe tener la clave principal adecuada. El equipo obtiene la clave principal cuando el usuario se sincroniza con la seguridad de documento (abre un documento protegido en línea). Si esta clave principal está comprometida, cualquier documento al que el usuario tenga acceso sin conexión también podría verse comprometido.

Una manera de reducir la amenaza a los documentos sin conexión es evitar permitir el acceso sin conexión a documentos particularmente sensibles. Otro método es pasar periódicamente las claves principales. Cuando la seguridad de documento pasa la clave por encima, las claves existentes ya no pueden acceder a los documentos protegidos por políticas. Por ejemplo, si un autor obtiene una clave principal de una laptop robada, esa clave no se puede utilizar para acceder a los documentos protegidos después de que se produzca el rollover. Si sospecha que una clave principal específica se ha visto comprometida, puede pasar el cursor sobre la clave manualmente.

Sin embargo, también debe tener en cuenta que un rollover de clave afecta a todas las claves principales, no solo a una. También reduce la escalabilidad del sistema porque los clientes deben almacenar más claves para el acceso sin conexión. La frecuencia de rollover de clave predeterminada es de 20 días. Se recomienda no establecer este valor por debajo de los 14 días, ya que es posible que se impida a las personas ver documentos sin conexión y que el rendimiento del sistema se vea afectado.

En el siguiente ejemplo, Key1 es la más antigua de las dos claves principales y Key2 es la más reciente. Al hacer clic en el botón Rollover Keys Now la primera vez, Key1 pasa a ser no válida y se genera una clave principal (Key3) nueva y válida. Los usuarios obtendrán Key3 cuando se sincronicen con la seguridad de documento, generalmente abriendo un documento protegido en línea. Sin embargo, los usuarios no se ven obligados a sincronizar con la seguridad de documento hasta que alcancen el máximo período de concesión sin conexión especificado en una política. Después del primer rollover de clave, los usuarios que permanezcan sin conexión podrán seguir abriendo documentos sin conexión, incluidos los protegidos por Key3, hasta que alcancen el máximo período de concesión sin conexión. Al hacer clic en el botón Rollover Keys Now por segunda vez, Key2 pasa a ser no válido y se crea Key4. Los usuarios que permanezcan sin conexión durante los dos rollovers clave no podrán abrir documentos protegidos con Key3 o Key4 hasta que se sincronicen con la seguridad de documento.

**Cambiar la frecuencia de rollover clave**

Por motivos de confidencialidad, cuando se utilizan documentos sin conexión, la seguridad de documento proporciona una opción de rollover de clave automática con un período de frecuencia predeterminado de 20 días. Puede cambiar la frecuencia de rollover; sin embargo, evite establecer un valor inferior a 14 días, ya que es posible que se impida a las personas ver documentos sin conexión y que el rendimiento del sistema se vea afectado.

1. En la página de seguridad de documento, haga clic en Configuración > Administración de claves.
1. En el cuadro Frecuencia de rollover clave, escriba el número de días para el período de rollover.
1. Haga clic en Aceptar.

**Deslizar manualmente las claves principales**

Para mantener la confidencialidad de los documentos sin conexión, puede pasar manualmente las claves principales. Es posible que necesite pasar el cursor manualmente sobre una clave (por ejemplo, si la clave está en peligro por alguien que la obtiene de un equipo en el que se almacena en caché para habilitar el acceso sin conexión a un documento).

>[!NOTE]
>
>Evite el uso frecuente de rollover manual porque hace que todas las claves principales se roden, no solo una, y puede evitar temporalmente que los usuarios vean nuevos documentos sin conexión.

Las claves principales deben revertirse dos veces antes de que se invaliden las claves existentes anteriormente en los equipos cliente. Los equipos cliente que tengan claves principales invalidadas deben volver a sincronizarse con el servicio de seguridad de documento para adquirir las nuevas claves principales.

1. En la página de seguridad de documento, haga clic en Configuración > Administración de claves.
1. Haga clic en Teclas de rollover ahora y, a continuación, haga clic en Aceptar.
1. Espere aproximadamente 10 minutos. El siguiente mensaje de registro aparece en el registro del servidor: `Done RightsManagement key rollover for`*N *`principals`. Donde* N *es el número de usuarios en el sistema de seguridad de documento.
1. Haga clic en Teclas de rollover ahora y, a continuación, haga clic en Aceptar.
1. Espere aproximadamente 10 minutos.

## Configuración de la auditoría de evento y la configuración de privacidad {#configuring-event-auditing-and-privacy-settings}

La seguridad de Documento puede auditar y registrar información sobre eventos relacionados con la interacción con documentos, políticas, administradores y servidores protegidos por políticas. Puede configurar la auditoría de evento y especificar los tipos de eventos que se auditarán. Para auditar eventos de un documento en particular, también debe habilitarse la opción de auditoría de la política.

Cuando la auditoría está habilitada, puede vista los detalles de los eventos auditados en la página Eventos. Los usuarios de seguridad de documento también pueden realizar vistas de eventos relacionados específicamente con los documentos protegidos por políticas que utilizan o crean.

Puede seleccionar estos tipos de eventos para la auditoría:

* eventos de documento protegidos por políticas, como intentos de usuarios autorizados o no autorizados de abrir documentos
* eventos de políticas, como crear, cambiar, eliminar, habilitar y deshabilitar políticas
* eventos de usuario, como invitaciones y registros de usuarios externos, cuentas de usuario activadas y desactivadas, cambios en las contraseñas de los usuarios y actualizaciones de perfil
* eventos de formularios AEM, como faltas de coincidencia de versiones, proveedores de autorización y servidor de directorios no disponibles y cambios en la configuración del servidor

### Habilitar o deshabilitar la auditoría de evento {#enable-or-disable-event-auditing}

Puede habilitar y deshabilitar la auditoría de eventos relacionados con el servidor, documentos protegidos por políticas, políticas, conjuntos de políticas y usuarios. Al habilitar la auditoría de evento, puede elegir auditar todos los eventos posibles o seleccionar eventos específicos para auditar.

Al habilitar la auditoría del servidor, puede realizar la vista de los eventos auditados en la página Eventos.

1. En la consola de administración, haga clic en Servicios > Seguridad de Documento > Configuración > Auditoría y configuración de privacidad.
1. Para configurar la auditoría del servidor, en Habilitar auditoría del servidor, seleccione Sí o No.
1. Si seleccionó Sí, en cada categoría de evento, realice una de las siguientes acciones para seleccionar las opciones de auditoría:

   * Para auditar todos los eventos de la categoría, seleccione Todos.
   * Para auditar solo algunos eventos, anule la selección de Todos y, a continuación, active las casillas de verificación situadas junto a los eventos que desee auditar.

      (Consulte Opciones [de auditoría de](configuring-client-server-options.md#event-auditing-options)Evento).

1. Haga clic en Aceptar.

>[!NOTE]
>
>Cuando trabaje con páginas web, evite utilizar los botones del navegador, como el botón Atrás, el botón Actualizar y la flecha Atrás o Avanzar, ya que esta acción puede causar problemas no deseados en la captura de datos y la visualización de datos.

### Habilitar o deshabilitar la notificación de privacidad {#enable-or-disable-privacy-notification}

Puede activar y desactivar un mensaje de notificación de privacidad. Cuando activa la notificación de privacidad, aparece un mensaje cuando un destinatario intenta abrir un documento protegido por una política. El aviso informa al usuario de que se está auditando el uso del documento. También puede especificar una URL que el usuario pueda utilizar para vista de la página de la política de privacidad si hay una disponible.

1. En la consola de administración, haga clic en Servicios > Seguridad de Documento > Configuración > Auditoría y configuración de privacidad.
1. Para configurar la notificación de privacidad, en Activar aviso de privacidad, seleccione Sí o No.

   Si la directiva adjunta a un documento permite el acceso de usuarios anónimos y Activar aviso de privacidad está establecida en No, no se solicita al usuario que inicie sesión y no se muestra el mensaje de notificación de privacidad.

   Si la directiva adjunta a un documento no permite el acceso anónimo de un usuario, el usuario verá el mensaje de notificación de privacidad.

1. Si corresponde, en el cuadro URL de privacidad, escriba la URL en la página de política de privacidad. Si el cuadro URL de privacidad se deja en blanco, se muestra la página de privacidad de adobe.com.
1. Haga clic en Aceptar.

>[!NOTE]
>
>Al desactivar el aviso de privacidad, no se deshabilita la auditoría del uso de documentos. Las acciones de auditoría integradas y las acciones personalizadas admitidas a través del seguimiento de uso extendido pueden recopilar información sobre el comportamiento del usuario.

### Importar un tipo de evento de auditoría personalizado {#import-a-custom-audit-event-type}

Si utiliza una aplicación con seguridad de documento que admite la auditoría de eventos adicionales, como eventos específicos de un determinado tipo de archivo, un socio de Adobe puede proporcionarle eventos de auditoría personalizados que puede importar en seguridad de documento. Utilice esta función solo si un socio de Adobe le ha proporcionado tipos de evento personalizados.

1. En la consola de administración, haga clic en Servicios > Seguridad de Documento > Configuración > Administración de Eventos.
1. Haga clic en Examinar para ir al archivo XML que desea importar y haga clic en Importar.
1. La importación sobrescribe los tipos de evento de auditoría personalizados existentes en el servidor si se encuentran idénticas combinaciones de código de evento y Área de nombres.
1. Haga clic en Aceptar.

### Eliminar un tipo de evento de auditoría personalizado {#delete-a-custom-audit-event-type}

1. En la consola de administración, haga clic en Servicios > Seguridad de documento > Configuración > Administración de Eventos.
1. Seleccione la casilla de verificación situada junto al tipo de evento de auditoría personalizado que desee eliminar y haga clic en Eliminar.
1. Haga clic en Aceptar.

### Exportar eventos de auditoría {#export-audit-events}

Puede exportar eventos de auditoría a un archivo para archivarlos.

1. En la consola de administración, haga clic en Servicios > Seguridad de Documento > Configuración > Administración de Eventos.
1. Edite la configuración en Exportar Eventos de auditoría según sea necesario. Puede especificar:

   * la edad mínima de los eventos de auditoría para exportar
   * el número máximo de eventos de auditoría que se incluirán en un solo archivo. El servidor genera uno o más archivos, según este valor.
   * la carpeta en la que se creará el archivo. Esta carpeta se encuentra en el servidor de formularios. Si la ruta de la carpeta es relativa, entonces es relativa al directorio raíz del servidor de aplicaciones.
   * el prefijo de archivo que se usará para los archivos de eventos de auditoría
   * el formato del archivo, ya sea un archivo de valores separados por comas (CSV) compatible con Microsoft Excel o un archivo XML.

1. Haga clic en Exportar. Si desea cancelar la exportación, haga clic en Cancelar exportación. Si otro usuario ha programado una exportación, el botón Cancelar exportación no estará disponible hasta que se complete dicha exportación. El botón Cancelar exportación no está disponible si otro usuario ha programado una exportación. Para comprobar si se ha iniciado o finalizado una exportación o eliminación programada, haga clic en Actualizar.

### Eliminar eventos de auditoría {#delete-audit-events}

Puede eliminar eventos de auditoría que tengan más de un número especificado de días.

1. En la consola de administración, haga clic en Servicios > Seguridad de Documento > Configuración > Administración de Eventos.
1. En Eliminar Eventos de auditoría, especifique el número de días en el cuadro Eliminar Eventos de auditoría anteriores a.
1. Haga clic en Eliminar. Haga clic en Exportar. Si desea cancelar la eliminación, haga clic en Cancelar eliminación. Si otro usuario ha programado la eliminación, el botón Cancelar eliminación no estará disponible hasta que se complete la exportación. El botón Cancelar eliminación no está disponible si otro usuario ha programado una exportación. Para comprobar si se ha iniciado o finalizado una eliminación programada, haga clic en Actualizar.

### Opciones de auditoría de Evento {#event-auditing-options}

Puede habilitar y deshabilitar la auditoría de evento y especificar los tipos de eventos que se van a auditar.

**eventos Documento**

**Documento de Vista:** Un destinatario vista un documento protegido por una política.

**Cerrar Documento:** Un destinatario cierra un documento protegido por una política.

**Imprimir baja resolución** Un destinatario imprime un documento protegido por una política con la opción de baja resolución especificada.

**Imprimir alta resolución:** Un destinatario imprime un documento protegido por una política con la opción de alta resolución especificada.

**Añadir anotación en Documento:** Un destinatario agrega una anotación a un documento PDF.

**Revocar Documento:** Un usuario o administrador anula el acceso a un documento protegido por una política.

**Documento sin revocar:** Un usuario o administrador restablece el acceso a un documento protegido por una política.

**Rellenado de formularios:** Un destinatario introduce información en un documento PDF que es un formulario rellenable.

**Directiva eliminada:** Un editor elimina una política de un documento para retirar las protecciones de seguridad.

**Cambiar URL de revocación de Documento:** Una llamada desde el nivel de API cambia la dirección URL de revocación especificada para acceder a un nuevo documento que reemplaza a un documento revocado.

**Modificar Documento:** Un destinatario cambia el contenido de un documento protegido por una política.

**Documento de firma:** Un destinatario firma un documento.

**Asegurar un nuevo Documento:** Un usuario aplica una política para proteger un documento.

**Cambiar directiva en Documento:** Un usuario o administrador cambia la directiva adjunta a un documento.

**Publicar Documento como:** Un nuevo documento cuyo documentName y licencia son idénticos a un documento existente está registrado en el servidor y los documentos no tienen una relación principal-secundario. Este evento se puede activar con el SDK de formularios de AEM.

**Iterar Documento:** Un nuevo documento cuyo documentName y licencia son idénticos a un documento existente está registrado en el servidor y los documentos tienen una relación principal-secundario. Este evento se puede activar con el SDK de formularios de AEM.

**eventos de políticas**

**Directiva creada:** Un usuario o administrador crea una directiva.

**Directiva habilitada:** Un administrador pone a disposición una directiva.

**Directiva modificada:** Un usuario o administrador cambia una directiva.

**Directiva deshabilitada:** Un administrador impide que una directiva esté disponible.

**Directiva eliminada:** Un usuario o administrador elimina una directiva.

**Cambiar propietario de directiva:** Una llamada desde el nivel de API cambia el propietario de la directiva.

**eventos del usuario**

**Usuario eliminado:** Un administrador elimina una cuenta de usuario.

**Registrar usuario invitado:** Un usuario externo se registra con seguridad de documento.

**Inicio de sesión satisfactorio:** Los administradores o usuarios intentaron iniciar sesión correctamente.

**Usuarios invitados:** La seguridad de Documento invita al usuario a registrarse.

**Usuarios activados:** Los usuarios externos activan sus cuentas mediante la dirección URL del correo electrónico de activación o un administrador habilita una cuenta.

**Cambiar contraseña:** Los usuarios invitados cambian sus contraseñas o un administrador restablece una contraseña para un usuario local.

**Inicio de sesión fallido:** Errores en los intentos de inicio de sesión de administradores o usuarios.

**Usuarios desactivados:** Un administrador desactiva una cuenta de usuario local.

**Actualización de Perfil:** Los usuarios invitados cambian su nombre, nombre de organización y contraseña.

**Cuenta bloqueada:** Un administrador bloquea una cuenta.

**Eventos de conjuntos de directivas**

**Conjunto de directivas de creación:** Un administrador o coordinador de conjuntos de políticas crea un conjunto de directivas.

**Conjunto de directivas eliminado:** Un administrador o coordinador de conjuntos de directivas elimina un conjunto de directivas.

**Conjunto de directivas modificado:** Un administrador o coordinador de conjuntos de políticas cambia un conjunto de directivas.

**eventos del sistema**

**Se completó la sincronización de directorios:** Esta información no está disponible en la página Eventos. La información de sincronización de directorios actual, incluido el estado de sincronización actual y la hora de la última sincronización, se muestra en la página Administración de dominios. Para acceder a la página Administración de dominios en la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.

**Acceso sin conexión del cliente:** Acceso sin conexión activado por el usuario a documentos protegidos contra el servidor en el equipo del usuario.

**La aplicación cliente** sincronizada debe sincronizar la información con el servidor para permitir el acceso sin conexión.

**No coincide la versión:** Una versión del SDK de formularios AEM incompatible con el servidor ha intentado conectarse al servidor.

**Información de sincronización de directorios:** Esta información no está disponible en la página Eventos. La información de sincronización de directorios actual, incluido el estado de sincronización actual y la hora de la última sincronización, se muestra en la página Administración de dominios. Para acceder a la página Administración de dominios en la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.

**Cambio de configuración del servidor:** Cambios en la configuración del servidor que se realizan a través de las páginas web o manualmente importando un archivo config.xml. Esto incluye cambios en la dirección URL base, los tiempos de espera de sesión, los bloqueos de inicio de sesión, la configuración del directorio, los rollovers de claves, la configuración del servidor SMTP para el registro externo, la configuración de marca de agua, las opciones de visualización, etc.

## Configuración del seguimiento de uso extendido {#configuring-extended-usage-tracking}

La seguridad de Documento puede rastrear varios eventos personalizados que se pueden realizar en un documento protegido. Puede habilitar el seguimiento de eventos desde el servidor de seguridad de documento a nivel global o a nivel de directiva. A continuación, puede configurar un JavaScript para capturar acciones específicas realizadas dentro del documento PDF protegido, como hacer clic en un botón o guardar el documento. Estos datos de uso se envían como un archivo XML en pares de clave-valor, que puede utilizar para una mayor análisis. Los usuarios finales que acceden a los documentos protegidos pueden permitir o rechazar dicho seguimiento desde la aplicación cliente.

Si el seguimiento está habilitado en el nivel global, puede anular esta configuración en el nivel de directiva y deshabilitarla para una directiva en particular. La anulación de nivel de directiva no es posible si el seguimiento está deshabilitado a nivel global. La lista de eventos rastreados se envía automáticamente al servidor cuando el recuento de eventos alcanza los 25 o cuando se cierra el documento. También puede configurar la secuencia de comandos para insertar explícitamente la lista de evento según sus necesidades. Puede personalizar el seguimiento de eventos accediendo a las propiedades y los métodos del objeto de seguridad de documento.

Después de habilitar el seguimiento, todas las directivas que se creen posteriormente tendrán activado el seguimiento de forma predeterminada. Las directivas creadas antes de habilitar el seguimiento en el servidor necesitarán actualizaciones manuales.

### Habilitar o deshabilitar el seguimiento de uso extendido {#enable-or-disable-extended-usage-tracking}

Antes de comenzar, asegúrese de que la auditoría del servidor está habilitada. Consulte [Configuración de auditoría de evento y configuración](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) de privacidad para obtener más información sobre la auditoría.

1. En la consola de administración, haga clic en Servicios > Seguridad de Documento > Configuración > Auditoría y configuración de privacidad.
1. Para configurar el seguimiento de uso extendido, en Habilitar seguimiento, seleccione Sí o No.
1. Para establecer la selección de la casilla de verificación Permitir la recopilación de datos de uso detallados en la página de inicio de sesión, en Habilitar seguimiento predeterminado, seleccione Sí o No.

Para vista de los eventos rastreados, puede utilizar el filtro Eventos de Documento en la página Eventos. Los eventos rastreados con JavaScript se etiquetan como Seguimiento detallado del uso. Consulte eventos [de](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) supervisión para obtener más información sobre eventos.

## Configuración de la pantalla de seguridad de documento {#configure-document-security-display-settings}

1. En la consola de administración, haga clic en Servicios > Seguridad de documento > Configuración > Opciones de visualización.
1. Configure los ajustes y haga clic en Aceptar.

### Display settings {#display-settings}

**Filas para mostrar en los resultados de búsqueda:** Número de filas que aparecen en una página cuando se realizan las búsquedas.

**Cuadro de diálogo Personalización para inicio de sesión de cliente**

Esta configuración controla el texto mostrado en el mensaje de inicio de sesión que aparece cuando un usuario inicia sesión en la seguridad de documento a través de una aplicación cliente.

**Texto de bienvenida:** El texto del mensaje de bienvenida, como &quot;Por favor, inicia sesión con tu nombre de usuario y contraseña&quot;. El texto del mensaje de bienvenida debe contener información sobre cómo iniciar sesión en documento security y cómo comunicarse con un administrador u otra persona de soporte designado de su organización para obtener ayuda. Por ejemplo, es posible que los usuarios externos necesiten ponerse en contacto con un administrador si olvidan sus contraseñas o necesitan asistencia en el proceso de registro o inicio de sesión. La longitud máxima del texto de bienvenida es de 512 caracteres.

**Texto de nombre de usuario:** Etiqueta de texto del cuadro de nombre de usuario.

**Texto de contraseña:** Etiqueta de texto del cuadro de contraseña.

**Personalización para cuadro de diálogo de autenticación de certificado de cliente**

Esta configuración controla el texto mostrado en el cuadro de diálogo de autenticación de certificados.

**Texto de tipo ChooseAuthentication:** Texto que se muestra para indicar al usuario que seleccione un tipo de autenticación.

**Elegir texto del certificado:** Texto que se muestra para indicar al usuario que seleccione un tipo de certificado.

**Texto de error de certificados no disponibles:** Mensaje de hasta 512 caracteres para mostrar cuando el certificado seleccionado no está disponible.

**Personalización para la visualización de certificados de cliente**

**Mostrar solo los emisores de credenciales de confianza:** Cuando se selecciona esta opción, la aplicación cliente presenta al usuario únicamente certificados de emisores de credenciales en los que los formularios AEM están configurados para confiar (consulte Administración de certificados y credenciales). Cuando esta opción no está seleccionada, se presenta al usuario una lista de todos los certificados del sistema del usuario.

## Configurar marcas de agua dinámicas {#configure-dynamic-watermarks}

Con la seguridad de documento, puede configurar los valores predeterminados de la opción de marca de agua dinámica que puede aplicar al crear políticas. Una *marca de agua* es una imagen que se superpone sobre el texto del documento. Es útil para rastrear el contenido de un documento y puede ayudar a identificar el uso ilegal del contenido.

Una marca de agua dinámica puede consistir en texto compuesto por variables definidas como ID de usuario y fecha y texto personalizado, o contenido enriquecido dentro de un PDF. Puede configurar marcas de agua con varios elementos, cada uno con su propio posicionamiento y formato.

Las marcas de agua no son editables y, por lo tanto, constituyen un método más seguro para garantizar la confidencialidad del contenido del documento. Las marcas de agua dinámicas también garantizan que las marcas de agua muestren suficiente información específica del usuario para disuadir de seguir distribuyendo el documento.

La marca de agua especificada por una política aparece en el documento protegido por una política cuando un destinatario realiza una vista o imprime el documento. A diferencia de las marcas de agua permanentes, una marca de agua dinámica nunca se guarda en el documento, lo que proporciona la flexibilidad necesaria al implementar un documento en un entorno de intranet para garantizar que la aplicación de visualización muestre la identidad del usuario específico. Además, si un documento tiene varios usuarios, el uso de la marca de agua dinámica significa que puede utilizar un documento en lugar de varias versiones, cada una con una marca de agua diferente. La marca de agua que aparece refleja la identidad del usuario actual.

Tenga en cuenta que las marcas de agua dinámicas son diferentes de las marcas de agua que los usuarios pueden agregar directamente al documento en Acrobat. El resultado es que puede tener dos marcas de agua en un documento protegido por una política.

### Consideraciones al crear marcas de agua {#considerations-when-creating-watermarks}

Puede crear marcas de agua dinámicas con varios elementos de marca de agua con cada elemento especificado como texto o PDF. Puede incluir hasta cinco elementos en una marca de agua.

Si elige una marca de agua basada en texto, puede especificar varios elementos dentro de la marca de agua con varias entradas de texto y especificar la posición de cada elemento. Asigne nombres significativos a estos elementos, como encabezado, pie de página, etc.

Por ejemplo, si desea especificar un texto diferente en el encabezado, pie de página, en los márgenes y en todo el documento como marca de agua, cree varios elementos de marca de agua y especifique sus posiciones. Si desea que el ID de usuario del usuario y la fecha actual de acceso al documento aparezcan en el encabezado, que el nombre de la política en el margen derecho y el texto personalizado &quot;CONFIDENCIAL&quot; aparezcan en diagonal en el documento, debe definir elementos de marca de agua independientes con texto como tipo y especificar su formato y posición. Cuando la marca de agua se aplica a un documento, todos los elementos de la marca de agua se aplican al documento al mismo tiempo, en el orden en que se añaden a la marca de agua.

Normalmente, las marcas de agua basadas en PDF se utilizan para incluir contenido gráfico como logotipos o símbolos especiales como copyright o marca comercial registrada.

Puede cambiar los límites del número de elementos de marca de agua y del tamaño del archivo PDF modificando el archivo de configuración de seguridad de documento. Consulte [Cambio de los parámetros](configuring-client-server-options.md#change-the-watermark-configuration-parameters)de configuración de marca de agua.

Tenga en cuenta lo siguiente al configurar las marcas de agua:

* No puede utilizar un documento PDF protegido con contraseña como elemento de marca de agua. Sin embargo, si la marca de agua que crea contiene otros elementos que no están protegidos con contraseña, se aplicarán como parte de la marca de agua.
* Puede cambiar el tamaño máximo del archivo PDF que desea utilizar como elemento de marca de agua. Sin embargo, los grandes documentos PDF utilizados como marcas de agua degradan el rendimiento durante la sincronización sin conexión de documentos aplicados con dichas marcas de agua. Consulte [Cambio de los parámetros](configuring-client-server-options.md#change-the-watermark-configuration-parameters)de configuración de marca de agua.
* Solo se utiliza como marca de agua la primera página del PDF seleccionado. Asegúrese de que la información que desea que aparezca como marca de agua esté disponible en la primera página.
* Aunque puede especificar la escala del documento PDF, tenga en cuenta el tamaño y la presentación de la página del PDF si desea utilizarla como marca de agua en el encabezado, pie de página o márgenes.
* Al especificar el nombre de la fuente, introduzca el nombre correctamente. Los formularios AEM sustituyen la fuente especificada si no está presente en el ordenador cliente en el que se abre el documento.
* Si ha seleccionado el texto como contenido de marca de agua, la especificación de la opción de escala como Ajustar a página no funciona para las páginas con un ancho diferente.
* Cuando especifique la posición de los elementos de marca de agua, asegúrese de que no haya más de un elemento con la misma posición. Si dos elementos de marca de agua tienen la misma posición, como el centro, aparecen superpuestos en el documento y, en el orden en que se añadieron a la marca de agua.
* Al especificar el tamaño y el tipo de fuente, asegúrese de que la longitud del texto sea completamente visible dentro de la página. El contenido del texto se desplaza a nuevas líneas, por lo que el contenido de la marca de agua que pretendía estar presente en los márgenes podría superponerse en las áreas de contenido de las páginas. Sin embargo, si el documento se abre en Acrobat 9, el texto que va más allá de la línea única se trunca.

### Limitaciones de las marcas de agua dinámicas {#limitations-of-dynamic-watermarks}

Es posible que algunas aplicaciones cliente no admitan marcas de agua dinámicas. Consulte la Ayuda correspondiente de las extensiones de Acrobat Reader DC. Además, tenga en cuenta lo siguiente sobre las versiones de Acrobat que admiten marcas de agua dinámicas:

* No puede utilizar un documento PDF protegido con contraseña como elemento de marca de agua.
* Las versiones anteriores a 10 de Acrobat y Adobe Reader no admiten las siguientes funciones de marca de agua:

   * Marcas de agua PDF
   * Varios elementos en la marca de agua (Texto/PDF)
   * Opciones avanzadas como el rango de páginas o las opciones de visualización
   * Opciones de formato de texto como fuente, nombre de fuente y color especificados. Sin embargo, las versiones anteriores de Acrobat y Reader mostrarán el contenido del texto en la fuente y el color predeterminados.

* Acrobat 9.0 y versiones anteriores: Acrobat 9.0 y versiones anteriores no admite nombres de políticas en marcas de agua dinámicas. Si Acrobat 9.0 abre un documento protegido por una política con una marca de agua dinámica que incluye un nombre de política y otros datos dinámicos, la marca de agua se muestra sin el nombre de la política. Si la marca de agua dinámica solo incluye el nombre de la política, Acrobat muestra un mensaje de error

### Añadir una plantilla de marca de agua dinámica {#add-a-dynamic-watermark-template}

Puede crear plantillas de marca de agua dinámicas. Estas plantillas siguen estando disponibles como opción de configuración para las directivas que crean los administradores o los usuarios.

>[!NOTE]
>
>La información de configuración de marca de agua dinámica no se captura con la otra información de configuración al exportar un archivo de configuración.

1. En la consola de administración, haga clic en Servicios > Seguridad de Documento > Configuración > Marcas de agua.
1. Haga clic en Nuevo.
1. En el cuadro Nombre, escriba un nombre para la nueva marca de agua.

   ***nota **: No se pueden usar algunos caracteres especiales en los nombres o descripciones de marcas de agua o elementos de marcas de agua. Consulte las restricciones enumeradas en[Consideraciones para editar directivas](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. En Nombre, junto al signo más, introduzca un nombre significativo para el elemento de marca de agua como Encabezado, agregue una descripción y expanda el signo más para mostrar las opciones.
1. En Origen, seleccione el tipo de marca de agua como Texto o PDF.
1. Si seleccionó Texto, haga lo siguiente:

   * Seleccione los tipos de marcas de agua que desea incluir. Si selecciona Texto personalizado, en el cuadro adyacente, escriba el texto que desea mostrar para la marca de agua. Tenga en cuenta la longitud del texto que aparecerá como marca de agua.
   * Especifique las propiedades de formato de texto, como el nombre de fuente, el tamaño de fuente, el color de primer plano y el color de fondo para el contenido de texto del texto de la marca de agua. Especifique el color de primer plano y de fondo como valores hexadecimales.

      ***nota **: Si selecciona la opción de escala como Ajustar a página, la propiedad de tamaño de fuente no estará disponible para la edición.*

1. Si seleccionó PDF para opciones de marca de agua enriquecida, haga clic en **Examinar** junto a Seleccionar archivo PDF de marca de agua para seleccionar el documento PDF que desea utilizar como marca de agua.

   ***nota **: No utilice un documento PDF protegido con contraseña. Si especifica un PDF protegido con contraseña como elemento de marca de agua, la marca de agua no se aplicará.*

1. En Usar como fondo, seleccione Sí o No.

   **nota**: Actualmente, la marca de agua aparece en primer plano independientemente de esta configuración.

1. Para controlar dónde se muestra la marca de agua en el documento, configure las opciones Alineación vertical y Alineación horizontal.
1. Seleccione Ajustar a página o seleccione % y escriba un porcentaje en el cuadro. El valor debe ser un número entero, no una fracción. Para configurar el tamaño de la marca de agua, puede utilizar un valor que sea el porcentaje de la página o establecer la marca de agua para que se ajuste al tamaño de la página.
1. En el cuadro Rotación, escriba los grados que se deben girar para rotar la marca de agua. El intervalo es de -180 a 180. Utilice un valor negativo para rotar la marca de agua en sentido contrario a las agujas del reloj. El valor debe ser un número entero, no una fracción.
1. En el cuadro Opacidad, escriba un porcentaje. Utilice un número entero, no una fracción.
1. En Opciones avanzadas, establezca lo siguiente:

   **Opciones de intervalo de páginas**

   Configure el rango de páginas en las que se debe mostrar la marca de agua. Introduzca la página de inicio como 1 y la página final como -1 para que todas las páginas estén marcadas con la marca de agua.

   **Opciones de visualización**

   Seleccione dónde desea que aparezca la marca de agua. De forma predeterminada, la marca de agua aparece tanto en la copia en pantalla (en línea) como en la copia impresa (impresa).

1. Haga clic en **Nuevo** en Elementos de marca de agua para agregar más elementos de marca de agua si es necesario.
1. Haga clic en Aceptar.

### Edición de una plantilla de marca de agua dinámica {#edit-a-dynamic-watermark-template}

1. En la consola de administración, haga clic en Servicios > Seguridad de documento > Configuración > Marcas de agua.
1. Haga clic en la marca de agua adecuada en la lista.
1. En la página Editar marcas de agua, cambie la configuración según sea necesario.
1. Haga clic en Aceptar.

### Eliminar una plantilla de marca de agua dinámica {#delete-a-dynamic-watermark-template}

Al eliminar una marca de agua dinámica, ya no está disponible para agregarla a una nueva directiva. Sin embargo, la marca de agua permanece en las políticas existentes que la utilizan actualmente y los documentos que la política protege actualmente siguen mostrando la marca de agua dinámica hasta que usted o un usuario editen la política que contiene la marca de agua eliminada. Una vez editada la política, ya no se aplica la marca de agua. Aparece un mensaje que indica que la marca de agua existente se elimina en la directiva y que el usuario puede seleccionar otra para reemplazarla.

1. En la consola de administración, haga clic en Servicios > Seguridad de Documento > Configuración > Marcas de agua.
1. Seleccione la casilla de verificación situada junto a la marca de agua correspondiente y haga clic en Eliminar.
1. Haga clic en Aceptar.

## Configuración del registro de usuarios invitados {#configuring-invited-user-registration}

Los usuarios externos a su organización pueden registrarse con seguridad de documento. Los usuarios invitados que se registren y activen sus cuentas pueden iniciar sesión en documento security utilizando su dirección de correo electrónico y la contraseña que crean al registrarse. Los usuarios invitados registrados pueden utilizar documentos protegidos por políticas a los que tienen permisos.

Cuando se activan los usuarios invitados, se convierten en usuarios locales. Los usuarios locales pueden configurarse y administrarse mediante el área Usuarios invitados y locales. (Consulte [Administración de cuentas](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts)de usuario invitadas y locales.)

En función de las funciones que habilite para los usuarios invitados, también podrán utilizar estas funciones de seguridad de documento:

* Aplicar directivas a documentos
* Crear políticas
* Añadir usuarios invitados a directivas

Documento security genera automáticamente un correo electrónico de invitación de registro cuando se producen los siguientes eventos, a menos que el usuario ya se encuentre en el directorio LDAP de origen o se le haya invitado previamente a registrarse:

* Un usuario existente agrega un usuario invitado a una directiva
* Un administrador agrega una cuenta de usuario invitado a la página Registro de usuarios invitados

El correo electrónico de registro contiene un vínculo a una página de registro e información sobre cómo registrarse. Una vez que el usuario invitado se registra, la seguridad de documento envía un correo electrónico de activación con un vínculo a una página de Activación. Cuando se activa, la cuenta permanece válida hasta que la desactive o elimine.

Si habilita el registro integrado, debe especificar el servidor SMTP, los detalles del correo electrónico de registro, las funciones de acceso y restablecer la información de correo electrónico de contraseña una sola vez. Antes de habilitar el registro integrado, asegúrese de que ha creado un dominio local en Administración de usuarios y ha asignado la función &quot;Documento security Invite a usuario&quot; a los usuarios y grupos adecuados de su organización. (Consulte [Añadir un dominio](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) local y [Crear y configurar funciones](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)). Si no utiliza el registro integrado, debe tener su propio sistema de registro de usuario creado con el SDK de formularios de AEM. Consulte la ayuda sobre &quot;Desarrollo de SPI para formularios AEM&quot; en [Programación con formularios](https://www.adobe.com/go/learn-aemforms-programming-63)AEM. Si no utiliza la opción Registro integrado, se recomienda configurar un mensaje en el correo electrónico de activación y en la pantalla de inicio de sesión del cliente para notificar a los usuarios cómo comunicarse con el administrador para obtener una contraseña nueva o para obtener más información.

**Habilitar y configurar el registro de usuarios invitados**

De forma predeterminada, el proceso de registro del usuario invitado está desactivado. Puede habilitar y deshabilitar el registro de usuarios invitados para la seguridad de documento, según sea necesario.

1. En la consola de administración, haga clic en Servicios > Seguridad de documento > Configuración > Registro de usuarios invitados.
1. Seleccione Activar registro de usuario invitado.
1. (Opcional) Actualice la configuración de registro del usuario invitado según sea necesario:

   * [Excluir o incluir un usuario o grupo externo](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Parámetros de servidor y cuenta de registro](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Configuración de correo electrónico de invitación de registro](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Configuración de correo electrónico de Activación](configuring-client-server-options.md#activation-email-settings)
   * [Configurar un correo electrónico de restablecimiento de contraseña](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Opcional) En Registro integrado, seleccione Sí para activar esta opción. Si no habilita el registro integrado, debe configurar su propio sistema de registro de usuarios.
1. Haga clic en Aceptar.

### Excluir o incluir un usuario o grupo externo {#exclude-or-include-an-external-user-or-group}

Puede restringir el registro con seguridad de documento para determinados usuarios o grupos de usuarios externos. Esta opción es útil, por ejemplo, para permitir el acceso a un grupo de usuarios determinado pero excluir a personas específicas que forman parte del grupo.

La siguiente configuración se encuentra en el área Filtro de restricción de correo electrónico de la página Registro de usuarios invitados.

**Exclusión:** Escriba la dirección de correo electrónico de un usuario o grupo para excluir. Para excluir varios usuarios o grupos, escriba cada dirección de correo electrónico en una nueva línea. Para excluir a todos los usuarios que pertenecen a un dominio en particular, introduzca un comodín y el nombre de dominio. Por ejemplo, para excluir todos los usuarios del dominio example.com, escriba &amp;ast;.example.com.

**Inclusión:** Escriba la dirección de correo electrónico de un usuario o grupo para incluir. Para incluir varios usuarios o grupos, escriba cada dirección de correo electrónico en una nueva línea. Para incluir a todos los usuarios que pertenecen a un dominio en particular, introduzca un comodín y el nombre de dominio. Por ejemplo, para incluir todos los usuarios en el dominio example.com, escriba &amp;ast;.example.com.

### Parámetros de servidor y cuenta de registro {#server-and-registration-account-parameters}

La siguiente configuración se encuentra en el área Configuración general de la página Registro de usuarios invitados.

**Host SMTP:** El nombre de host del servidor SMTP. El servidor SMTP administra los avisos de correo electrónico salientes para registrar y activar las cuentas de usuario invitadas.

Si el host SMTP lo requiere, escriba la información necesaria en los cuadros Nombre de cuenta del servidor SMTP y Contraseña de cuenta del servidor SMTP para conectarse al servidor SMTP. Algunas organizaciones no aplican este requisito. Si necesita información, póngase en contacto con el administrador del sistema.

**Nombre de clase de socket del servidor SMTP:** Nombre de clase de socket para el servidor SMTP. Por ejemplo, javax.net.ssl.SSLSocketFactory.

**Tipo de contenido de correo electrónico:** Tipo MIME aceptado como text/plain o text/html.

**Codificación de correo electrónico:** Formato de codificación que se utilizará al enviar mensajes de correo electrónico. Puede especificar cualquier codificación, por ejemplo, UTF-8 para Unicode o ISO-8859-1 para latín. El valor predeterminado es UTF-8.

**Dirección de correo electrónico de redirección:** Al especificar una dirección de correo electrónico para esta configuración, se envía cualquier nueva invitación a la dirección proporcionada. Esta configuración puede resultar útil para realizar pruebas.

**Usar dominios locales:** Seleccione el dominio apropiado. En una nueva instalación, asegúrese de que ha creado el dominio mediante Administración de usuarios. Si se trata de una actualización, se creó un dominio de usuario externo durante la actualización y se puede utilizar.

**Usar SSL para el servidor SMTP:** Seleccione esta opción para habilitar SSL para el servidor SMTP.

**Mostrar vínculo de inicio de sesión en la página de registro:** Muestra un vínculo de inicio de sesión en la página de registro que se muestra para los usuarios invitados.

**Para habilitar Transport Layer Security (TLS) para el servidor SMTP**

1. Abra la consola de administración.

   La ubicación predeterminada de la consola de administración es `https://<server>:<port>/adminui`.

1. Vaya a Inicio > Servicios > Seguridad de Documento > Configuración > Registro de usuarios invitados.
1. En Registro de usuarios invitados, especifique todos los ajustes de configuración y, a continuación, haga clic en Aceptar.

   >[!NOTE]
   >
   >Si utiliza Microsoft Office 365 como servidor SMTP para enviar las invitaciones para el registro de usuarios, use la siguiente configuración:
   >
   >**Host SMTP:** smtp.office365.com
   >**Puerto:** 587

1. A continuación, debe actualizar el archivo config.xml. Consulte [Configuración para habilitar SMTP para Seguridad de la capa de transporte (TLS)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>Si realiza cambios en las opciones de Registro de usuarios invitados, se sobrescribe el archivo config.xml y se desactiva TLS. Si sobrescribe los cambios, debe realizar el paso anterior para volver a activar la compatibilidad TLS para el registro de usuarios invitados.

### Configuración de correo electrónico de invitación de registro {#registration-invitation-email-settings}

Documento Security envía automáticamente un correo electrónico de invitación para el registro al crear una nueva cuenta de usuario invitado o cuando un usuario existente agrega un destinatario externo que no se ha registrado previamente o se le ha invitado a registrarse en una política. El correo electrónico contiene un vínculo que el destinatario puede utilizar para acceder a la página de registro e introducir información personal de la cuenta, incluido el nombre de usuario y la contraseña. La contraseña puede ser cualquier combinación de ocho caracteres.

Cuando el destinatario activa la cuenta, el usuario se convierte en un usuario local.

La siguiente configuración se encuentra en el área Configuración de correo electrónico de invitación de la página Registro de usuarios invitados.

**Desde:** La dirección de correo electrónico desde la que se envía el correo electrónico de invitación. El formato predeterminado de la dirección de correo electrónico De es postmaster@[your_installation_domain].com.

**Asunto:** Asunto predeterminado para el mensaje de correo electrónico de invitación.

**Tiempo de espera:** Número de días después de los cuales caduca la invitación de registro si el usuario externo no se registra. El valor predeterminado es 30 días.

**Mensaje:** Texto que aparece en el cuerpo del mensaje invitando al usuario a registrarse.

### Configuración de correo electrónico de Activación {#activation-email-settings}

Después de que los usuarios invitados se registren, documento Security envía un correo electrónico de activación. El correo electrónico de activación contiene un vínculo a la página de activación de la cuenta donde los usuarios pueden activar su cuenta. Cuando las cuentas están activadas, los usuarios pueden iniciar sesión en documento security utilizando su dirección de correo electrónico y la contraseña que crearon cuando se registraron.

Cuando el destinatario activa la cuenta de usuario, el usuario se convierte en un usuario local.

La siguiente configuración se encuentra en el área Configuración de correo electrónico de Activación de la página Registro de usuarios invitados.

>[!NOTE]
>
>También se recomienda configurar un mensaje en la pantalla de inicio de sesión para avisar a los usuarios externos sobre cómo ponerse en contacto con el administrador para obtener una contraseña nueva o para obtener más información.

**Desde:** La dirección de correo electrónico desde la que se envía el correo electrónico de activación. Esta dirección de correo electrónico recibe avisos de envío fallidos del host de correo electrónico del registrado y también cualquier mensaje que el destinatario envíe en respuesta al correo electrónico de registro. El formato predeterminado de la dirección de correo electrónico De es postmaster@[your_installation_domain].com.

**Asunto:** Asunto predeterminado para el mensaje de correo electrónico de activación.

**Tiempo de espera:** Número de días después de los cuales caduca la invitación de activación si el usuario no activa la cuenta. El valor predeterminado es 30 días.

**Mensaje:** El texto que aparece en el cuerpo del mensaje es un mensaje que indica que es necesario activar la cuenta de usuario del destinatario. También puede incluir información como cómo comunicarse con un administrador para obtener una nueva contraseña.

### Configurar un correo electrónico de restablecimiento de contraseña {#configure-a-password-reset-email}

Si tiene que restablecer la contraseña de un usuario invitado, se genera un mensaje de correo electrónico de confirmación que invita al usuario a elegir una nueva contraseña. No se puede determinar la contraseña de un usuario; si el usuario lo olvida, debe restablecerlo.

La siguiente configuración se encuentra en el área Restaurar correo electrónico de contraseña de la página Registro de usuarios invitados.

**Desde:** Dirección de correo electrónico desde la que se envía el correo electrónico de restablecimiento de contraseña. El formato predeterminado de la dirección de correo electrónico De es postmaster@[your_installation_domain].com.

**Asunto:** Asunto predeterminado para el mensaje de correo electrónico de restablecimiento.

**Mensaje:** El texto que aparece en el cuerpo del mensaje es un mensaje que indica que se restablece la contraseña de usuario externa del destinatario.

## Permitir que los usuarios y grupos creen directivas {#enable-users-and-groups-to-create-policies}

La página Configuración tiene un vínculo a la página Mis políticas, donde puede especificar qué usuarios finales pueden crear mis políticas y qué usuarios y grupos son visibles en los resultados de búsqueda. La página Mis políticas tiene dos fichas:

**Ficha Crear directivas:** Se utiliza para configurar los permisos de usuario para crear políticas personalizadas.

**Ficha Usuarios y grupos visibles:** Se utiliza para controlar qué usuarios y grupos son visibles en los resultados de búsqueda de usuarios. El superusuario o el administrador del conjunto de directivas es necesario para seleccionar y agregar dominios, creados en Administración de usuarios, al usuario y grupo visibles para cada conjunto de directivas. Esta lista es visible para el coordinador de conjuntos de políticas y se utiliza para poner límites en los dominios que el coordinador de conjuntos de políticas puede examinar al elegir usuarios para agregar a las políticas.

Antes de conceder permiso a los usuarios para crear políticas personalizadas, considere cuánto acceso o control desea que tengan los usuarios individuales. Además, tenga en cuenta la exposición que desea que estén los usuarios y grupos al hacerlos visibles para las búsquedas.

### Especificar usuarios y grupos que pueden crear directivas {#specify-users-and-groups-who-can-create-policies}

Como administrador, especifique qué usuarios y grupos pueden crear políticas personalizadas. Este permiso se puede establecer a nivel de usuario y grupo. La funcionalidad de búsqueda busca usuarios y grupos en la base de datos de Administración de usuarios.

1. En la consola de administración, haga clic en Servicios > Seguridad de Documento > Configuración > Mis políticas.
1. En la página Mis políticas, haga clic en la ficha Crear políticas y luego en Añadir usuarios y grupos.
1. En el cuadro Buscar, escriba el nombre de usuario o la dirección de correo electrónico del usuario o grupo que está buscando. Si no dispone de esta información, deje el cuadro vacío. También puede escribir un nombre parcial o una dirección de correo electrónico, por ejemplo, cuando solo conoce las dos primeras letras de un nombre de usuario.
1. En la lista Uso, seleccione los parámetros de búsqueda Nombre o Correo electrónico.
1. En la lista Tipo, seleccione Grupo o Usuario para limitar la búsqueda.
1. En la lista En, seleccione el dominio en el que desea realizar la búsqueda. Si no conoce el dominio del usuario o grupo, seleccione Todos los dominios.
1. En la lista Mostrar, especifique el número de resultados de búsqueda que se mostrarán por página y, a continuación, haga clic en Buscar.
1. Para agregar usuarios y grupos de Mis directivas, seleccione la casilla de verificación de cada usuario y grupo que desee agregar.
1. Haga clic en Añadir y, a continuación, en Aceptar.

Los usuarios y grupos seleccionados ahora tienen permiso para crear políticas personalizadas.

### Quitar los permisos de creación de directivas personalizadas de un usuario o grupo {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. En la página de seguridad de documento, haga clic en Configuración > Mis políticas.
1. En la página Mis políticas, haga clic en la ficha Crear políticas. Se muestran los usuarios y grupos con permisos para crear políticas personalizadas.
1. Seleccione la casilla de verificación situada junto a los usuarios y grupos que desea quitar de este permiso.
1. Haga clic en Eliminar y, a continuación, en Aceptar.

### Especificar usuarios y grupos visibles en las búsquedas {#specify-users-and-groups-that-are-visible-in-searches}

Cuando los usuarios administran sus políticas personalizadas, pueden buscar usuarios y grupos para agregarlos a sus políticas. Debe especificar los dominios desde los cuales los usuarios y grupos están visibles en estas búsquedas.

1. En la página de seguridad de documento, haga clic en Configuración > Mis políticas.
1. En la página Mis políticas, haga clic en la ficha Usuarios y grupos visibles.
1. Para hacer visibles los usuarios y grupos de un dominio, haga clic en Añadir dominios, seleccione los dominios y haga clic en Añadir. Para eliminar un dominio, seleccione la casilla de verificación situada junto al nombre del dominio y haga clic en Eliminar.

## Edición manual del archivo de configuración de seguridad de documento {#manually-editing-the-document-security-configuration-file}

Puede importar y exportar la información de configuración almacenada en la base de datos de seguridad de documento. Por ejemplo, puede que desee hacer una copia de seguridad de la información de configuración cuando pase de un ensayo a un entorno de producción, o puede que desee editar opciones avanzadas que sólo se pueden configurar para editar este archivo.

Puede realizar los siguientes cambios con el archivo de configuración:

[Mostrar permisos de CATIA al crear y editar políticas](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Especificación de un período de tiempo de espera para la sincronización sin conexión](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Denegación de servicios de seguridad de documento para aplicaciones específicas](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Cambiar los parámetros de configuración de marca de agua](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Desactivación de vínculos externos](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>La importación del archivo de configuración reconfigura el sistema según la información del archivo. Las excepciones son la configuración dinámica de marca de agua y la información de eventos personalizados, que no se guardan con el archivo de configuración exportado. Debe configurar esta información manualmente en el nuevo sistema. Solo un administrador del sistema o un consultor de servicios profesionales que esté familiarizado con la seguridad de documento y XML debe modificar el contenido de un archivo de configuración, como para reconfigurar una configuración dañada o para ajustar los parámetros de un escenario de implementación empresarial concreto.

**Exportación de un archivo de configuración**

1. En la consola de administración, haga clic en Servicios > Seguridad de documento 11 > Configuración > Configuración manual.
1. Haga clic en Exportar y guarde el archivo de configuración en otra ubicación. El nombre de archivo predeterminado es config.xml.
1. Haga clic en Aceptar.
1. Antes de cambiar el archivo de configuración, realice una copia de seguridad en caso de que necesite revertir.

**Importar un archivo de configuración**

1. En la consola de administración, haga clic en Servicios > Seguridad de documento 11 > Configuración > Configuración manual.
1. Haga clic en Examinar para ir al archivo de configuración y, a continuación, haga clic en Importar. No puede escribir la ruta directamente en el cuadro Nombre de archivo.
1. Haga clic en Aceptar.

### Especificación de un período de tiempo de espera para la sincronización sin conexión {#specify-a-timeout-period-for-offline-synchronization}

La seguridad de Documento permite a los usuarios abrir y utilizar documento protegido cuando no están conectados al servidor de seguridad de documento. La aplicación cliente del usuario debe sincronizarse regularmente con el servidor para mantener la validez de los documentos para su uso sin conexión. La primera vez que los usuarios abren un documento protegido, se les preguntará si su equipo debe estar autorizado para realizar la sincronización periódica con el cliente.

De forma predeterminada, la sincronización se realiza automáticamente cada cuatro horas y según sea necesario cuando un usuario está conectado al servidor de seguridad de documento. Si el período sin conexión de un documento caduca mientras el usuario está sin conexión, el usuario debe volver a conectarse al servidor para permitir que la aplicación cliente se sincronice con el servidor.

En el archivo de configuración de seguridad de documento, puede especificar la frecuencia predeterminada de la sincronización automática en segundo plano. Esta configuración actúa como la aplicación cliente del período de tiempo de espera predeterminado, a menos que el cliente establezca explícitamente su propio valor de tiempo de espera.

1. Exporte el archivo de configuración de seguridad de documento. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).
1. Abra el archivo de configuración en un editor y busque el `PolicyServer` nodo. Bajo ese nodo, busque el `ServerSettings` nodo.
1. En el `ServerSettings` nodo, agregue esta entrada siguiente y, a continuación, guarde el archivo:

   `<entry key="BackgroundSyncFrequency" value="`*time *`"/>`

   donde *time* es el número de segundos entre sincronizaciones en segundo plano automáticas. Si envía este valor a `0`, la sincronización siempre se produce. El valor predeterminado es `14400` segundos (cada cuatro horas).

1. Importe el archivo de configuración. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).

### Denegación de servicios de seguridad de documento para aplicaciones específicas {#denying-document-security-services-for-specific-applications}

Puede configurar la seguridad de documento para denegar servicios a aplicaciones que cumplan criterios específicos. Los criterios pueden especificar un único atributo, como un nombre de plataforma, o bien varios conjuntos de atributos. Esta función puede ayudarle a controlar las solicitudes que debe gestionar la seguridad del documento. Estas son algunas de las aplicaciones de esta función:

* **Protección de ingresos:** Es posible que desee denegar el acceso a cualquier aplicación cliente que no admita sus convenciones de ingresos.
* **Compatibilidad de aplicaciones:** Algunas aplicaciones pueden ser incompatibles con las políticas o el comportamiento del servidor de seguridad de documento.

Cuando las aplicaciones cliente intentan establecer un vínculo con seguridad de documento, suministran información sobre aplicaciones, versiones y plataformas. La seguridad de Documento compara esta información con la configuración de Negaciones que obtiene del archivo de configuración de seguridad de documento.

La configuración de Negaciones puede contener varios conjuntos de condiciones de denegación. Si todos los atributos de un conjunto coinciden, se deniega a la aplicación solicitante el acceso a los servicios de seguridad de documento.

La función de denegación de servicio requiere que las aplicaciones cliente utilicen la versión 8.2 o posterior del SDK de cliente C++ de seguridad de documento. Los siguientes productos de Adobe proporcionan información del producto al solicitar servicios de seguridad de documento:

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard y posterior
* Adobe Reader 9.0 y posterior
* Extensiones de Acrobat Reader DC para Microsoft Office 8.2 y posterior

Las aplicaciones cliente utilizan la API de cliente del SDK de cliente C++ de seguridad de documento para solicitar servicios de seguridad de documento. Las solicitudes de la API de cliente incluyen información sobre la plataforma y la versión del SDK (precompilada en la API de cliente) e información del producto obtenida de la aplicación cliente.

Las aplicaciones o complementos del cliente proporcionan información sobre el producto en la implementación de una función de llamada de retorno. La aplicación proporciona la siguiente información:

* Nombre del integrador
* Versión integradora
* Familia de aplicaciones
* Nombre de la aplicación
* Versión de la aplicación

Si no se aplica ninguna información, la aplicación cliente deja el campo correspondiente en blanco.

Varias aplicaciones de Adobe incluyen información del producto al solicitar servicios de seguridad de documento, incluidas las extensiones de Acrobat, Adobe Reader y Acrobat Reader DC para Microsoft Office.

**Acrobat y Adobe Reader**

Cuando Acrobat o Adobe Reader solicitan un servicio de seguridad de documento, proporciona la siguiente información del producto:

* **Integrador:** Adobe Systems, Inc.
* **Versión integradora:** 1.0
* **Familia de aplicaciones:** Acrobat
* **Nombre de la aplicación:** Acrobat
* **Versión de la aplicación:** 9.0.0

**Extensiones de Acrobat Reader DC para Microsoft Office**

Las extensiones de Acrobat Reader DC para Microsoft Office son un complemento que se utiliza con los productos de Microsoft Office Microsoft Word, Microsoft Excel y Microsoft PowerPoint. Cuando solicita un servicio, proporciona la siguiente información:

* **Integrador:** Adobe Systems Incorporated
* **Versión integradora:** 8.2
* **Familia de aplicaciones:** Extensiones de Acrobat Reader DC para Microsoft Office
* **Nombre de la aplicación:** Microsoft Word, Microsoft Excel o Microsoft PowerPoint
* **Versión de la aplicación:** 2003 o 2007

**Configurar la seguridad de documento para denegar servicios para aplicaciones específicas**

1. Exporte el archivo de configuración de seguridad de documento. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).
1. Abra el archivo de configuración en un editor y busque el `PolicyServer` nodo. Añada un `ClientVersionRules` nodo como un nodo secundario inmediato del `PolicyServer` nodo, si no existe:

   ```as3
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
   `SDKVersions` especifica la versión de la API de cliente C++ de seguridad de documento utilizada por la aplicación cliente. Por ejemplo, `"8.2"`.

   `APPFamilies` está definida por la API de cliente.

   `AppName`especifica el nombre de la aplicación cliente. Las comas se utilizan como separadores de nombres. Para incluir una coma en un nombre, escape con un carácter de barra invertida (\). Por ejemplo, *&quot;Adobe Systems\, Inc.&quot;*.

   `AppVersions` especifica la versión de la aplicación cliente.

   `Integrators` especifica el nombre de la compañía o grupo que desarrolló el complemento o la aplicación integrada.

   `IntegratorVersions` es la versión del complemento o la aplicación integrada.

1. Para cada conjunto adicional de datos de denegación, agregue otro elemento *MyEntryName* .
1. Guarde el archivo de configuración.
1. Importe el archivo de configuración. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).

**Ejemplos**

En este ejemplo, se deniega el acceso a todos los clientes de Windows.

```as3
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

En este ejemplo, se deniega el acceso a Mi aplicación versión 3.0 y a Mi otra aplicación versión 2.0. La misma URL de información de denegación se utiliza independientemente del motivo de la denegación.

```as3
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

En este ejemplo, se deniegan todas las solicitudes de una instalación de Microsoft PowerPoint 2007 o Microsoft PowerPoint 2010 de extensiones de Acrobat Reader DC para Microsoft Office.

```as3
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

De forma predeterminada, puede especificar un máximo de cinco elementos en una marca de agua. Además, el tamaño máximo de archivo del documento PDF que desea utilizar como marca de agua está limitado a 100 KB. Puede cambiar estos parámetros en el archivo config.xml.

***nota **: Debe cambiar estos parámetros con precaución.*

1. Exporte el archivo de configuración de seguridad de documento. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).
1. Abra el archivo de configuración en un editor y busque el `ServerSettings` nodo.
1. En el `ServerSettings` nodo, agregue las entradas siguientes y, a continuación, guarde el archivo: `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   El tamaño *máximo del archivo de la primera entrada,* máximo, es el tamaño máximo de archivo (en KB) permitido para un elemento de marca de agua PDF. El valor predeterminado es 100 KB.

   La segunda entrada, *max elements* , es el número máximo de elementos permitidos en una marca de agua. El valor predeterminado es 5.

   ```as3
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importe el archivo de configuración. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).

### Desactivación de vínculos externos {#disabling-external-links}

Muchos usuarios de seguridad de documento no tienen acceso a vínculos externos como **www.adobe.com** mientras utilizan las interfaces de usuario de Administración de derechos:

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

Los siguientes cambios en config.xml desactivan todos los vínculos externos desde las interfaces de usuario de Administración de derechos.

1. Exporte el archivo de configuración de seguridad de documento. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).
1. Abra el archivo de configuración en un editor y busque el `DisplaySettings` nodo.
1. Para deshabilitar todos los vínculos externos, en el `DisplaySettings` nodo, agregue la siguiente entrada y guarde el archivo: `<entry key="ExternalLinksAllowed" value="false"/>`

   ```as3
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importe el archivo de configuración. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).

### Configuración para habilitar SMTP para Seguridad de la capa de transporte (TLS) {#configuration-to-enable-smtp-for-transport-layer-security-tls}

Los siguientes cambios en config.xml habilitan la compatibilidad TLS para la función Registro de usuarios invitados.

1. Exporte el archivo de configuración de seguridad de documento. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).
1. Abra el archivo de configuración en un editor y busque el `DisplaySettings` nodo.
1. Busque el nodo siguiente: `<node name="ExternalUser">`

   ```as3
   <node name="ExternalUser">
   ```

1. Establezca el valor de la `SmtpUseTls` clave en el `ExternalUser` nodo en **true**.
1. Establezca el valor de la `SmtpUseSsl` clave en el `ExternalUser` nodo en **false**.
1. Guarde el `config.xml`.
1. Importe el archivo de configuración. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).

### Deshabilitar los extremos de SOAP para documentos de seguridad de Documento {#disable-soap-endpoints-for-document-security-documents}

Los siguientes cambios en config.xml para deshabilitar los extremos SOAP para documentos de seguridad de documento.

1. Exporte el archivo de configuración de seguridad de documento. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).
1. Abra el archivo de configuración en un editor y busque el nodo siguiente: `<node name="DRM">`

   ```as3
   <node name="DRM">
   ```

1. En el nodo DRM, busque el `entry` nodo:

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. Para deshabilitar los extremos SOAP para documentos de seguridad de documento, establezca el atributo value en **false**.

   ```as3
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. Guarde el `config.xml`.
1. Importe el archivo de configuración. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).

### Aumento de la escalabilidad del servidor de seguridad de documento {#increasingscalability}

De forma predeterminada, mientras sincroniza un documento para su uso sin conexión, junto con la información del documento actual, los clientes de seguridad de documento obtienen información de actualizaciones de directivas, marcas de agua, licencias y revocación para todos los demás documentos a los que el usuario tiene acceso. Si estas actualizaciones e información no se sincronizan con el cliente, es posible que un documento abierto en modo sin conexión se siga abriendo con información de política, marca de agua y revocación más antigua.

Puede aumentar la escalabilidad del servidor de seguridad de documento limitando la información que se envía al cliente. La reducción de la cantidad de información enviada al cliente mejora la escalabilidad, reduce el tiempo de respuesta y mejora el rendimiento del servidor. Realice los siguientes pasos para aumentar la escalabilidad:

1. Exporte el archivo de configuración de seguridad de documento. (Consulte Edición [manual del archivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).
1. Abra el archivo de configuración en un editor y busque el nodo ServerSettings.
1. En el nodo ServerSettings, establezca el valor de la `DisableGlobalOfflineSynchronizationData`propiedad en `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Cuando se establece en true, el servidor de seguridad de documento envía información únicamente para el documento actual y la información para el resto de documentos (los demás documentos a los que tiene acceso un usuario) no se envía al cliente.

   >[!NOTE]
   >
   >De forma predeterminada, el valor de la `DisableGlobalOfflineSynchronizationData`clave se establece en `false`.

1. Guarde e importe el archivo de configuración. (Consulte Edición [manual del archivo](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuración de seguridad de documento).

