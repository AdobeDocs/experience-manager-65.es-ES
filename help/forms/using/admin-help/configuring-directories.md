---
title: Configuración de directorios
seo-title: Configuración de directorios
description: Obtenga información sobre cómo agregar, editar y eliminar directorios y configurar la administración de usuarios para utilizar la vista de lista virtual.
seo-description: Obtenga información sobre cómo agregar, editar y eliminar directorios y configurar la administración de usuarios para utilizar la vista de lista virtual.
uuid: 0bf1a8a7-c917-4248-9937-d24e31c5ba17
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1f15f028-aa81-478e-97eb-f83a4dc0418c
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# Configuración de directorios {#configuring-directories}

Para cada dominio de empresa que configure, especifique los directorios que el proveedor de autenticación consulta para obtener información del usuario. Puede configurar varios directorios para un dominio.

## Adición de directorios o SPI personalizados {#adding-directories-or-custom-spis}

Para cada dominio de empresa que configure, especifique los directorios que el proveedor de autenticación consulta para obtener información del usuario. Puede agregar un directorio a un dominio de empresa existente o a un nuevo dominio de empresa que esté agregando. Puede configurar varios directorios para un dominio. También puede configurar un dominio para que utilice una interfaz de proveedor de servicios (SPI) personalizada para la sincronización.

### Agregar un directorio {#add-a-directory}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio de empresa o seleccione un dominio de empresa existente.
1. Haga clic en Agregar directorio.
1. En el cuadro Nombre de perfil, escriba un nombre para distinguir este directorio y haga clic en Siguiente.
1. Configure la configuración del servidor de directorios. (Consulte Configuración [del directorio](configuring-directories.md#directory-settings)).
1. Para verificar que se puede establecer una conexión con el servidor LDAP, haga clic en Probar. Si la prueba falla, revise la excepción en el archivo de registro de Application Server para determinar la causa raíz del error. Haga clic en Cerrar y, a continuación, en Siguiente.
1. Seleccione Configuración de usuario y configure las opciones según sea necesario. (Consulte Configuración [del directorio](configuring-directories.md#directory-settings)).
1. Para verificar que el DN base y otros atributos configurados recopilan el lote correcto de usuarios, haga clic en Probar. LDAP intenta recuperar los primeros 200 registros mediante la configuración proporcionada (como el DN base, el filtro de búsqueda y todos los atributos).

   Si se devuelven usuarios, los resultados muestran los valores asignados a cada campo según el conjunto de atributos. Si la prueba falla debido a un nombre de servidor inexistente, información de autorización incorrecta o atributos incorrectos, aparece el siguiente mensaje de error: &quot;Los criterios de búsqueda especificados no devolvieron ningún resultado&quot;. Para determinar la causa raíz del error, revise la excepción en el archivo de registro de Application Server. Haga clic en Cerrar y, a continuación, en Siguiente.

1. Seleccione Configuración de grupo y configure los ajustes según sea necesario. (Consulte Configuración [del directorio](configuring-directories.md#directory-settings)).
1. Para verificar que el DN base y otros atributos configurados recopilan el lote correcto de grupos, haga clic en Probar. Si se devuelven grupos, los resultados muestran los valores asignados a cada campo según el conjunto de atributos. Haga clic en Cerrar.

### Agregar un SPI personalizado {#add-a-custom-spi}

Para obtener información sobre la creación de una SPI personalizada, consulte &quot;Desarrollo de SPI para formularios AEM&quot; en [Programación con formularios](https://www.adobe.com/go/learn_aemforms_programming_63)AEM. Para que un SPI personalizado recién implementado esté disponible para asociarse al dominio, reinicie el servidor.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio de empresa o seleccione un dominio de empresa existente.
1. Haga clic en Agregar directorio.
1. Escriba un nombre en el cuadro Nombre de perfil, seleccione Proveedor SPI personalizado y, a continuación, haga clic en Siguiente.
1. Seleccione un proveedor de usuario personalizado en la lista y haga clic en Siguiente.
1. Seleccione un proveedor de grupo personalizado en la lista y haga clic en Finalizar.

## Editar un directorio {#edit-a-directory}

Puede editar los detalles de un directorio que haya configurado anteriormente.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el dominio correspondiente de la lista y, en la página que aparece, seleccione el directorio apropiado de la lista.
1. Configure las opciones de directorio, usuario y grupo según sea necesario. (Consulte Configuración [del directorio](configuring-directories.md#directory-settings)).
1. Haga clic en Aceptar.

## Eliminar un directorio {#delete-a-directory}

Al sincronizar los dominios después de eliminar un directorio, todos los usuarios y grupos de ese directorio se marcan como obsoletos en la base de datos. No se devolverán en ninguna búsqueda desde la Consola de administración.

>[!NOTE]
>
>Los dominios de empresa requieren al menos un proveedor de autenticación y un proveedor de directorio.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el dominio correspondiente de la lista.
1. Seleccione la casilla de verificación del directorio correspondiente y haga clic en Eliminar.
1. Haga clic en Aceptar en la página de confirmación que aparece y vuelva a hacer clic en Aceptar.

## Ajustes del directorio {#directory-settings}

Cuando agregue un directorio a un dominio, especifique la siguiente configuración de directorio.

**** Servidor: (Obligatorio) Nombre de dominio completo (FQDN) del servidor de directorio. Por ejemplo, para un equipo llamado x en la red corp.adobe.com, el FQDN es x.corp.adobe.com. Se puede usar una dirección IP en lugar del nombre del servidor FQDN.

**** Puerto: (Obligatorio) El puerto que utiliza el servidor de directorios. Generalmente, 389 o 636 si se utiliza el protocolo Secure Sockets Layer (SSL) para enviar información de autenticación a través de la red.

**** SSL: (Obligatorio) Especifica si el servidor de directorio utiliza SSL al enviar datos a través de la red. El valor predeterminado es No. Cuando se establece en Sí, el entorno de tiempo de ejecución de Java™ (JRE) del servidor de aplicaciones debe confiar en el certificado de servidor LDAP correspondiente.

**Enlace** (obligatorio) Especifica cómo acceder al directorio.

**** Anónimo: No se requiere nombre de usuario ni contraseña. Es posible que un usuario anónimo solo pueda recuperar una cantidad limitada de datos. Esta opción puede resultar útil para la prueba inicial.

**** Usuario: Se requiere autenticación. En el cuadro Nombre, especifique el nombre del registro de usuario que puede acceder al directorio. Es mejor introducir el nombre de reconocimiento completo (DN) de la cuenta de usuario, como cn=Jane Doe, ou=user, dc=can, dc=com. En el cuadro Contraseña, especifique la contraseña asociada. Estas opciones de configuración son necesarias cuando selecciona Usuario como opción de enlace.

**** Nombre: Nombre que se puede utilizar para conectarse a la base de datos LDAP cuando el acceso anónimo no está habilitado. Especifique `[domain name]\[userid]`para Active Directory 2003. Para Sun™ One, eDirectory o IBM Tivoli Directory Server, especifique el nombre completo del usuario, como uid=lcuser,ou=it,o=company.com.

**** Contraseña: Contraseña que corresponde al nombre especificado para conectarse a la base de datos LDAP cuando el acceso anónimo no está habilitado.

**** Rellenar página con: Cuando se selecciona, rellena los atributos en las páginas de configuración de usuario y grupo con los valores predeterminados correspondientes de LDAP.

**** Recuperar DN base: Recupera los DN base y los muestra en la lista desplegable. Esta configuración resulta útil cuando tiene varios DN base y necesita seleccionar un valor.

**** Habilitar referencia: Esta configuración es aplicable cuando su organización utiliza varios dominios de Active Directory organizados en una estructura jerárquica y ha especificado la configuración de directorio sólo para el dominio principal. En este caso, cuando selecciona esta opción, la Administración de usuarios puede acceder a los detalles de usuarios y grupos de los dominios secundarios.

***Nota **: Haga clic en Probar para comprobar que se puede establecer una conexión con el servidor LDAP. Para determinar la causa raíz de cualquier error, revise la excepción en el archivo de registro de Application Server.*

### User settings {#user-settings}

**** Identificador único: (Obligatorio) Un atributo único y constante utilizado para identificar a los usuarios. Utilice un atributo que no sea DN como identificador único porque el DN de un usuario puede cambiar si se traslada a otra parte de la organización. Esta configuración depende del servidor de directorio. El valor es objectGUID para Active Directory 2003, nsuniqueID para Sun™ One y guid para eDirectory.

**Nota**: Asegúrese de introducir un atributo que esté garantizado que sea único en su organización. La introducción de un valor incorrecto puede causar graves problemas en el sistema. *

**** DN base: Se establece como punto de partida para sincronizar usuarios y grupos desde la jerarquía de LDAP. Es mejor especificar un DN base en el nivel más bajo de la jerarquía que incluya a todos los usuarios y grupos que necesitan sincronizarse para los servicios.

Si seleccionó la opción Habilitar referencia en la configuración del Directorio, establezca la opción DN base en la parte *dc* del DN. Para que la referencia funcione, el período de búsqueda debe incluir tanto dominios principales como secundarios.

***Nota **: No incluya el DN del usuario en esta configuración. Para sincronizar un usuario en particular, utilice la configuración Filtro de búsqueda.*

Aunque el DN base es una configuración obligatoria en la consola de administración, algunos servidores de directorio como IBM Domino Enterprise Server pueden requerir un BaseDN vacío. Para especificar un DN base vacío, exporte el archivo config.xml, edite la configuración en el archivo config.xml y vuelva a importarlo. (Consulte [Importación y exportación del archivo](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)de configuración.)

**** Filtro de búsqueda: (Obligatorio) Filtro de búsqueda que se usará para encontrar el registro asociado al usuario. Puede realizar una búsqueda de un nivel o una búsqueda de subnivel. (Consulte Sintaxis del filtro de búsqueda o RFC 2254.) Para obtener más información sobre el esquema de Microsoft AD, consulte Esquema de Active Directory.

**** Descripción: Atributo de esquema para la descripción del usuario

**** Nombre completo: (Obligatorio) Atributo de esquema para el nombre completo del usuario

**** ID de inicio de sesión: (Obligatorio) Atributo de esquema para el ID de inicio de sesión del usuario

**** Apellido: (Obligatorio) Atributo de esquema para el apellido del usuario

**** Nombre dado: (Obligatorio) Atributo de esquema para el nombre del usuario

**** Iniciales: Atributo de esquema para las iniciales del usuario

**** Calendario comercial: Le permite asignar un calendario comercial a un usuario, en función del valor de esta configuración (la clave del calendario comercial). Los calendarios comerciales definen los días laborables y no laborables. Los formularios AEM pueden utilizar calendarios comerciales para calcular las fechas y horas futuras de eventos como recordatorios, plazos y escalaciones. La manera en que asigne las claves de calendario empresarial a los usuarios dependerá de si utiliza un dominio empresarial, local o híbrido. (Consulte Configuración de calendarios comerciales).

Si utiliza un dominio de empresa, puede asignar la configuración del calendario de negocios a un campo del directorio LDAP. Por ejemplo, si cada registro de usuario del directorio contiene un campo de *país* y desea asignar calendarios comerciales en función del país en el que se encuentra el usuario, especifique el nombre del campo de *país* como valor para la configuración del calendario comercial. A continuación, puede asignar las claves de calendario empresarial (los valores definidos para el campo de *país* en el directorio LDAP) a los calendarios comerciales en el flujo de trabajo de formularios.

La cantidad de espacio que se utiliza para mostrar el nombre de la clave de calendario comercial en las páginas de flujo de trabajo de formularios es limitada. Limite el nombre de la clave del calendario comercial a menos de 53 caracteres para evitar que se trunque en esas páginas.

**** Modificar marca de hora: Para habilitar la sincronización de directorios delta, establezca este valor para modificar TimeStamp. (Consulte Activación de la sincronización de directorios delta).

**** Organización: Atributo de esquema para el nombre de la organización a la que pertenece el usuario.

**** Correo electrónico principal: Atributo de esquema para la dirección de correo electrónico principal del usuario.

**** Correo electrónico secundario: Atributo de esquema para la dirección de correo electrónico secundaria del usuario.

**** Teléfono: Atributo de esquema para el número de teléfono del usuario.

**** Dirección postal: Atributo de esquema para la dirección de correo del usuario.

**** Configuración regional: Atributo de esquema que contiene la información de configuración regional ISO. El valor es un código de idioma de dos letras o un código de idioma y de país.

**** Huso horario: Atributo de esquema que contiene la zona horaria donde se encuentra el usuario. El valor es una cadena como Ciudad/País.

**** Activar control de vista de lista virtual (VLV): Control LDAP que permite a los formularios AEM recuperar datos por lotes desde el servidor de directorios. Si está utilizando Sun One como directorio LDAP y el directorio contiene muchos usuarios, al habilitar VLV se crea un índice que la Administración de usuarios puede utilizar al buscar usuarios. Esta función resulta útil cuando se utiliza una cuenta de usuario normal que solo puede sincronizar una cantidad limitada de datos. También puede activar VLV para grupos. Si selecciona Activar control de vista de lista virtual (VLV), especifique un nombre en el cuadro Campo de ordenación.

***Nota **: Para habilitar VLV, configure Sun One. (Consulte[Configuración de la administración de usuarios para utilizar la vista de lista virtual (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv)).*

**** Campo de ordenación: Si seleccionó Activar control de vista de lista virtual (VLV), especifique el nombre del atributo utilizado para ordenar el índice. Este nombre de atributo (como uid) es el que especificó cuando creó un índice para VLV en el servidor de directorio.

### Configuración de grupo {#group-settings}

**** Identificador único: (Obligatorio) Un atributo único y constante utilizado para identificar grupos. Utilice un atributo que no sea DN como identificador único. Esta configuración depende del servidor de directorio. El valor es objectGUID para Active Directory 2003, nsuniqueID para Sun One y guid para eDirectory.

***Nota**: Asegúrese de introducir un atributo que esté garantizado que sea único en su organización. La introducción de un valor incorrecto puede causar graves problemas en el sistema. *

**** DN base: (Obligatorio) Nombre distintivo base del directorio.

Aunque el DN base es una configuración obligatoria en la consola de administración, algunos servidores de directorio como IBM Domino Enterprise Server requieren un BaseDN vacío. Para especificar un DN base vacío, exporte el archivo config.xml, edite la configuración en el archivo config.xml y vuelva a importarlo. (Consulte [Importación y exportación del archivo](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)de configuración.)

**** Filtro de búsqueda: (Obligatorio) Filtro de búsqueda que se usará para encontrar el registro asociado al grupo. Puede realizar una búsqueda de un nivel o una búsqueda de subnivel.

**** Descripción: Atributo de esquema para la descripción del grupo

**** Nombre completo: (Obligatorio) Atributo de esquema para el nombre completo del grupo

**** DN de miembro: (Obligatorio) Atributo de esquema para el nombre distintivo de los miembros dentro de un grupo

**** Identificador único de miembro: Identificador único de un usuario o grupo que es miembro del grupo seleccionado. Este valor depende del servidor de directorio. El valor es objectSID para AD2003, nsuniqueID para Sun One y guid para eDirectory.

Si se especifica un DN de miembro con un atributo que no es de DN, la Administración de usuarios utiliza el Identificador único de miembro para consultar LDAP para recopilar el DN del usuario, ya que corresponde a un valor de identificador único.

Si DN se especifica como identificador único, no es necesario configurar el identificador único de miembro.

**** Organización: Atributo de esquema para el nombre de la organización a la que pertenece el grupo

**** Correo electrónico principal: Atributo de esquema para la dirección de correo electrónico principal del grupo

**** Correo electrónico secundario: Atributo de esquema para la dirección de correo electrónico secundaria del grupo

**** Modificar marca de hora: Para habilitar la sincronización de directorios delta, establezca este valor para modificar TimeStamp. (Consulte Activación de la sincronización de directorios delta).

**** Activar control de vista de lista virtual (VLV): Control LDAP que permite a los formularios AEM recuperar datos por lotes desde el servidor de directorios. Si está utilizando Sun One como directorio LDAP y el directorio contiene muchos grupos, al habilitar VLV se crea un índice que la Administración de usuarios puede utilizar al buscar grupos. Esta función resulta útil cuando se utiliza una cuenta de usuario normal que solo puede sincronizar una cantidad limitada de datos. También puede habilitar VLV para los usuarios. Si selecciona Activar control de vista de lista virtual (VLV), especifique un nombre de campo de ordenación.

***Nota **: Para habilitar VLV, configure Sun One. (Consulte[Configuración de la administración de usuarios para utilizar la vista de lista virtual (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv)).*

**** Nombre del campo de ordenación: Si seleccionó Activar control de vista de lista virtual (VLV), especifique el nombre del atributo utilizado para ordenar el índice. Este nombre de atributo es el que especificó cuando creó un índice para VLV en el servidor de directorio.

***Nota **: Haga clic en Probar para verificar que la configuración de usuario y grupo se recopila en función del DN base y los criterios de búsqueda. Si se devuelven usuarios y grupos, los resultados muestran los valores asignados a cada campo según el conjunto de atributos.*

***Nota **: La Administración de usuarios no admite ID de usuario duplicados dentro de un dominio; solo se sincroniza un usuario con el ID de usuario.*

## Configuración de la administración de usuarios para utilizar la vista de lista virtual (VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

La sincronización de directorios es un requisito importante para la Administración de usuarios. Los usuarios y grupos se sincronizan desde un directorio de empresa a la base de datos de formularios de AEM para asignar funciones y permisos. El número de usuarios varía de 100 a 100000 o más según los requisitos, y supone un desafío de ingeniería para sincronizar los datos de manera eficiente.

El protocolo LDAP proporciona un mecanismo para consultar grandes conjuntos de datos de forma paginada mediante controles de solicitud. Al utilizar Microsoft Active Directory, la sincronización de bases de datos de formularios LDAP con AEM utiliza PagedResultsControl para recuperar datos en lotes de un tamaño concreto. Sun ONE Directory Server no admite este control. Para completar una consulta paginada con el servidor de directorio Sun ONE, utilice el control Vista de lista virtual (VLV). Este control implica tanto la configuración del lado del servidor del directorio como la implementación del lado del cliente.

>[!NOTE]
>
>En esta sección se describe el uso del control VLV para el servidor de directorio Sun ONE. Sin embargo, puede utilizar este control para cualquier servidor de directorio que admita el control VLV.

1. Al configurar el directorio, seleccione Activar control de vista de lista virtual (VLV) en la página Configuración de usuario y en la página Configuración de grupo. Al seleccionar la casilla de verificación, también debe especificar un nombre de ordenación en el cuadro Campo de ordenación. El valor predeterminado es uid. (Consulte [Adición de directorios o SPIs](configuring-directories.md#adding-directories-or-custom-spis) personalizados o [Edición de un directorio](configuring-directories.md#edit-a-directory)).
1. Utilice una consola de administración Sun ONE o un script de línea de comandos para crear las entradas LDAP VLV para usuarios y grupos. Si utiliza una secuencia de comandos de línea de comandos, puede utilizar los usuarios y grupos de ejemplo de archivos LDIF. (Consulte [Configuración del servidor de directorio Sun ONE para VLV](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv)).
1. Detenga el servidor y cree el índice requerido. (Consulte [Creación del índice del servidor de directorios para VLV](configuring-directories.md#create-the-directory-server-index-for-vlv)).

### Configuración del servidor de directorio Sun ONE para VLV {#configuring-the-sun-one-directory-server-for-vlv}

La creación de un VLV requiere un par de entradas que incluyen las clases `vlvSearch` y `vlvIndex` objeto. La entrada vlvSearch incluye una base de búsqueda y el `vlvFilter` atributo, que especifica la clase de objeto que contiene los atributos que se pretenden ordenar. La clase de `vlvIndex` objeto incluye el `vlvSort` atributo, que especifica uno o varios atributos para ordenar y el orden en que se ordenan. (El signo menos (-) indica el orden alfabético inverso). El uso de VLV con formularios AEM requiere entradas independientes para usuarios y grupos.

>[!NOTE]
>
>Las entradas de objeto se pueden crear mediante la interfaz gráfica de usuario (GUI) Sun ONE o mediante un script de línea de comandos. Para obtener instrucciones sobre cómo crear las entradas de objeto mediante la interfaz gráfica de usuario, consulte la documentación de Sun ONE.

Esta es una entrada LDIF de script de muestra para VLV para usuarios:

```as3
 dn: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 objectclass: top
 objectclass: vlvSearch
 cn: lcuser
 vlvBase: dc=corp,dc=adobe,dc=com
 vlvScope: 2
 vlvFilter: (&(objectclass=inetOrgPerson))
 aci: (target="ldap:///cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config")(targetattr="*")(version 3.0; acl "Config"
 ;allow(read,search,compare) userdn="ldap:///all"; )
 dn: cn=lcuser,cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 cn: lcuser
 vlvSort: cn
 objectclass: top
 objectclass: vlvIndex
```

**Creación de entradas de objeto mediante una secuencia de comandos**

1. La secuencia de comandos de ejemplo tiene una entrada LDAP denominada `lcuser`. Esta entrada es para la configuración relacionada con VLV para la sincronización de usuarios en formularios AEM. Modifique las siguientes propiedades según corresponda:

   **** Nombre de entrada: El nombre de entrada de este ejemplo es `lcuser`. Si `lcuser` se cambia, debe cambiarse en todas las áreas de la secuencia de comandos de ejemplo.

   **** vlvBase: DN base especificado en la página Configuración de usuario.

   **** vlvFilter: Filtro de búsqueda especificado en la página Configuración de usuario.

   **** vlvSort: Campo de ordenación especificado en la sección Configuración de VLV de la página Configuración de usuario. Un control VLV requiere que especifique un control de ordenación. Este campo se utiliza como parámetro de ordenación para el índice vlv creado.

   **** aci: El control de acceso especificado en la secuencia de comandos de ejemplo otorga a cualquier usuario autenticado el derecho de acceder a los índices VLV para operaciones de lectura, búsqueda y comparación. El administrador puede restringir el acceso a un usuario de enlace, que está configurado en la página Ajustes del servidor de directorio especificada en la interfaz de usuario de Administración de usuarios. Si no se otorgan permisos, la búsqueda de usuarios no puede utilizar el VLV y el servidor LDAP emite una excepción de permisos.

   >[!NOTE]
   >
   >Como convención, el nombre de la entrada vlvIndex también se establece en `lcuser`, pero puede darle un nombre diferente. Utilice el mismo nombre en la herramienta vlvindex. (Consulte [Creación del índice del servidor de directorios para VLV](configuring-directories.md#create-the-directory-server-index-for-vlv)*).*

1. Con la `ldapmodify` herramienta proporcionada con Sun ONE Server, cree una entrada similar para los grupos utilizando el DN base, el Filtro de búsqueda y el Campo de ordenación del grupo, respectivamente:

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   Por ejemplo, escriba el siguiente texto:

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### Creación del índice del servidor de directorios para VLV {#create-the-directory-server-index-for-vlv}

Después de configurar los ajustes del directorio y crear las entradas LDAP VLV para usuarios y grupos, detenga el servidor y cree el índice requerido.

1. Después de crear entradas de objeto, detenga el servidor Sun ONE.
1. Con la herramienta vlvindex, genere el índice escribiendo el siguiente texto:

   *instancia* del servidor de directorios `\vlvindex.bat -n userRoot -T lcuser`

   Se genera el siguiente resultado:

   ```as3
    D:\tools\ldap\sun\shared\bin>..\..\slapd-chetanmeh-xp3\vlvindex.bat -n userRoot -T livecycle
    [21/Nov/2007:16:47:26 +051800] - userRoot: Indexing VLV: livecycle
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 1000 entries (5%).
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 2000 entries (9%).
    ...
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 20000 entries (94%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 21000 entries (99%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Finished indexing.
   ```

   La herramienta vlvindex está presente en el directorio de instancias del servidor de directorio. Si Sun ONE Server tiene dos instancias que ejecutan server1 y server2, la herramienta vlvindex se encuentra en el directorio ** de servidor Sun ONE\server1. El valor del parámetro `-T` es el valor del `cn` atributo de la entrada vlvindex creada anteriormente en el LDIF de muestra. En este caso, lo es `lcuser`.

1. Si VLV también está habilitado para grupos, cree el índice correspondiente para los grupos. Compruebe si los índices se crean ejecutando el siguiente comando:

   *directorio* de servidor Sun `\shared\bin>ldapsearch -h`*nombre *de host`-p`*puerto no*`-s base -b "" objectclass=*`

   Se generan resultados como los siguientes datos de ejemplo:

   ```as3
    D:\tools\ldap\sun\shared\bin>ldapsearch.exe -h localhost -p 55850 -s base -b "" objectclass=*
    ldapsearch.exe: started Tue Nov 27 16:34:20 2007
    version: 1
    dn:
    objectClass: top
    namingContexts: dc=corp,dc=adobe,dc=com
    supportedExtension: 2.16.840.1.113730.3.5.7
    ...
    vlvsearch: cn=MCC ou=testdata dc=corp dc=adobe dc=com, cn=userRoot,cn=ldbm dat
        abase,cn=plugins,cn=config
    vlvsearch: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
    vlvsearch: cn=Browsing ou=testdata,cn=userRoot,cn=ldbm database,cn=plugins,cn=
        config
    1 matches
   ```

