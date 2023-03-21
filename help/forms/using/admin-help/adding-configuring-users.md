---
title: Agregar y configurar usuarios
seo-title: Adding and configuring users
description: La configuración Administración de usuarios de la consola de administración permite crear o eliminar usuarios y configurar otras opciones de usuario.
seo-description: The User Management settings in the administration console allow you to create or delete users  and configure other user settings.
uuid: fe650cdb-7d0d-4f38-9899-e5349559ed32
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
discoiquuid: 20ca99e3-4843-4254-b3e9-0255cc752363
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 1%

---

# Agregar y configurar usuarios {#adding-and-configuring-users}

La información de usuarios y grupos se mantiene en un sistema de almacenamiento de terceros, como un directorio LDAP. Administración de usuarios no escribe en el sistema de almacenamiento de terceros. En su lugar, Administración de usuarios sincroniza la información de usuarios y grupos con su propia base de datos

## Crear un usuario {#create-a-user}

Al crear usuarios, puede agregarlos a grupos y asignarles funciones.

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Usuarios y grupos]** y haga clic en **[!UICONTROL Nuevo usuario]**. .
1. En **[!UICONTROL Configuración general]**, proporcione la información necesaria y haga clic en **[!UICONTROL Siguiente]**. Para obtener más información sobre la configuración, consulte [Configuración de usuario](adding-configuring-users.md#user-settings).
1. (Opcional) Para agregar el usuario a un grupo, haga clic en **[!UICONTROL Buscar grupos]** y haga lo siguiente:

   * En el **[!UICONTROL Buscar]** , escriba todo o parte del nombre del grupo.
   * Seleccione el dominio en el que buscar, seleccione el número de elementos que desea mostrar y haga clic en **[!UICONTROL Buscar]**.
   * (Opcional) Para ver los detalles del grupo, seleccione el nombre del grupo y haga clic en **[!UICONTROL OK]** para volver a la página de resultados de la búsqueda.
   * Seleccione la casilla de verificación del grupo y haga clic en **[!UICONTROL OK]**.
   * Haga clic en **[!UICONTROL Siguiente]**.

1. (Opcional) Para asignar funciones al usuario, haga clic en **[!UICONTROL Buscar funciones]**, seleccione la casilla de verificación de las funciones que desea asignar y, a continuación, haga clic en **[!UICONTROL OK]**.
1. Haga clic en **[!UICONTROL Finalizar]**.

   >[!NOTE]
   >
   >Si encuentra algún problema de inicio de sesión con el usuario, consulte [El usuario de AEM Forms en JEE no puede iniciar sesión en AEM Forms en OSGi](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## Configuración de usuario {#user-settings}

Especifique las siguientes opciones cuando cree o edite un usuario.

**Nombre canónico:** (Obligatorio) Identificador único del usuario. Cada usuario y grupo de un dominio debe tener un nombre canónico único. Active la casilla Generado por el sistema para permitir que la Administración de usuarios asigne un valor único, o bien desactive la casilla de verificación y especifique un valor personalizado para el Nombre canónico.

Evite utilizar caracteres de subrayado (_) en nombres canónicos, por ejemplo, `sample_user`. Cuando busca usuarios en función de su nombre canónico, no devuelve los que contienen caracteres subrayados.

**Nombre:** (Obligatorio) Nombre dado del usuario

**Apellidos:** (Obligatorio) Nombre de la familia del usuario

**Nombre común:** Nombre completo o nombre para mostrar para el usuario. Por ejemplo, si Nombre = Gloria y Apellido = Ríos, Nombre común = Gloria Ríos.

**Correo electrónico:** Dirección de correo electrónico del usuario

**Teléfono:** Número de teléfono del usuario

**Descripción:** Descripción opcional. Utilice este campo según las necesidades de su organización.

**Dirección:** Dirección de correo del usuario

**Organización:** Organización a la que pertenece el usuario

**Alias de correo electrónico:** Alias de correo electrónico del usuario. Separe los alias de correo electrónico con comas.

**Dominio:** Dominio al que pertenece el usuario

**Configuración regional:** Configuración regional ISO del usuario

**Clave del calendario comercial:** Permite asignar un calendario empresarial a un usuario según el valor de esta configuración. Los calendarios comerciales definen los días laborables y no laborables. AEM formularios pueden utilizar calendarios empresariales para calcular fechas y horas futuras en el caso de eventos como recordatorios, plazos y escalaciones. La forma en que asigne claves de calendario empresarial a los usuarios dependerá de si utiliza un dominio empresarial, local o híbrido. (Consulte [Adición de dominios](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Si utiliza un dominio local o híbrido, la información sobre los usuarios solo se almacena en la base de datos de Administración de usuarios. Para estos usuarios, establezca la clave del calendario empresarial en una cadena. A continuación, asigne la clave del calendario empresarial (la cadena) a un calendario empresarial en el flujo de trabajo de los formularios.

Si utiliza un dominio empresarial, la información sobre los usuarios reside en un sistema de almacenamiento de terceros, como un directorio LDAP. La Administración de usuarios sincroniza la información de usuario del directorio con la base de datos de Administración de usuarios. Esta función le permite asignar una clave de calendario empresarial a un campo del directorio LDAP. Por ejemplo, imaginemos un escenario en el que cada registro de usuario del directorio contiene un campo de país y desea asignar calendarios comerciales basados en el país en el que se encuentra el usuario. En este caso, especifique el nombre del campo de país como valor para la configuración Clave de calendario de negocio . A continuación, puede asignar las claves del calendario empresarial (los valores definidos para el campo de país en el directorio LDAP) a los calendarios comerciales en el flujo de trabajo de formularios.

Para obtener información adicional sobre los calendarios empresariales, incluido cómo asignar claves de calendario empresarial a los calendarios empresariales, consulte [Configuración de calendarios comerciales](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Limite el nombre a menos de 53 caracteres. Un nombre más corto ayuda a evitar problemas al mostrar la clave del calendario empresarial en las páginas de Administración de procesos en la consola de administración.

**ID de usuario:** (Obligatorio) ID de usuario que el usuario utiliza para iniciar sesión. El ID de usuario no distingue entre mayúsculas y minúsculas y debe ser único en todo el dominio.

En los dominios empresariales, utilice un atributo que no sea de DN como ID de usuario, ya que el DN de un usuario puede cambiar si se traslada a otra parte de la organización. Esta configuración depende del servidor de directorios. El valor es `objectGUID` para Active Directory 2003, `nsuniqueID` para Sun™ One, y `guid` para eDirectory.

Asegúrese de que el ID de usuario sea único. No utilice una que se haya asignado a un usuario eliminado.

AEM formularios no pueden diferenciar entre cuentas de usuario que tienen ID de usuario y contraseñas idénticos pero que pertenecen a dominios diferentes. Para evitar este problema, no cree cuentas que tengan el mismo ID de usuario en varios dominios.

Al usar SQL Server como base de datos, no se puede crear un ID de usuario que supere los 255 caracteres.

Al utilizar MySQL, el ID de usuario puede contener caracteres extendidos. Sin embargo, cuando se realiza una comparación entre dos cadenas, como abcde y âbcdè, se consideran iguales. Por ejemplo, al sincronizar, si se ha agregado un nuevo usuario a la base de datos, se realiza una comparación para comprobar si existe un usuario con el mismo ID de usuario en la base de datos. Si el usuario *abcode* existe en la base de datos cuando el nuevo usuario *âbcdè* se añade, la comparación no puede distinguir entre los dos nombres. Se da por hecho que el usuario existe en la base de datos y se ignora y no se añade el nuevo usuario.

Evite crear nombres de usuario que empiecen por un signo de número (#). Al realizar búsquedas de tareas, no se devuelven resultados para esos nombres de usuario. (Consulte [Trabajo con tareas](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Contraseña y confirmar contraseña:** Contraseña que el usuario utiliza para iniciar sesión. Debe tener un mínimo de ocho caracteres. No se requiere una contraseña para un usuario que forma parte de un dominio híbrido.

## Ver detalles de un usuario {#view-details-about-a-user}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. Especifique la información para limitar la búsqueda y, en la lista En, seleccione Usuarios y, a continuación, haga clic en Buscar. Los resultados de la búsqueda se enumeran en la parte inferior de la página. Puede ordenar la lista haciendo clic en cualquiera de los encabezados de columna.
1. Haga clic en el nombre del usuario para mostrar los detalles sobre . La página Editar usuario muestra los siguientes detalles sobre el usuario:

   * Información general de identificación, como nombre, correo electrónico, dirección, dominio y organización
   * Funciones asignadas al usuario
   * Grupos de los que es miembro el usuario

## Cambiar la contraseña de un usuario local {#change-the-password-for-a-local-user}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Usuarios y grupos]**.
1. Especifique la información para restringir la búsqueda de un usuario en particular y haga clic en **[!UICONTROL Buscar]**. Los resultados de la búsqueda se enumeran en la parte inferior de la página. Puede ordenar la lista haciendo clic en cualquiera de los encabezados de columna.
1. Haga clic en el nombre del usuario y, a continuación, haga clic en **[!UICONTROL Cambiar contraseña]**.
1. Escriba y confirme la nueva contraseña y, a continuación, haga clic en **[!UICONTROL OK]**. La contraseña debe tener un mínimo de ocho caracteres.

## Edición de las propiedades de un usuario {#edit-a-user-s-properties}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Usuarios y grupos]**.
1. Para buscar el usuario que desea editar, haga lo siguiente:

   * En el **[!UICONTROL Buscar]** , escriba los criterios de búsqueda.
   * En el **[!UICONTROL Uso]** lista, seleccionar **[!UICONTROL Nombre]**, **[!UICONTROL Correo electrónico]** o **[!UICONTROL ID de usuario]**.
   * En el **[!UICONTROL En la lista]**, seleccione **[!UICONTROL Usuarios]**.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y, a continuación, haga clic en **[!UICONTROL Buscar]**.

1. Haga clic en el usuario para editarlo.
1. Para un usuario que forma parte de un dominio local o híbrido, en la variable **[!UICONTROL Detalle]** , edite la **[!UICONTROL Configuración general]** y **[!UICONTROL Configuración de inicio de sesión]** y haga clic en **[!UICONTROL Guardar]**. Para obtener más información sobre la configuración, consulte [Configuración de usuario](adding-configuring-users.md#user-settings). No puede editar la configuración general y de inicio de sesión de un usuario que pertenece a un dominio de empresa.
1. Para editar la configuración del grupo para el usuario, haga clic en el botón **[!UICONTROL Pertenencia a grupos]** y haga lo siguiente:

   * Haga clic en **[!UICONTROL Buscar grupo]** y complete la información de búsqueda.
   * Para agregar el usuario a un nuevo grupo, seleccione la casilla de verificación del grupo y haga clic en **[!UICONTROL OK]** y, a continuación, haga clic en **[!UICONTROL Guardar]**.

   >[!NOTE]
   >
   >Los usuarios locales no se pueden agregar a grupos de directorios. Sin embargo, los usuarios del directorio se pueden agregar a grupos locales.

   * Para quitar el usuario de un grupo, seleccione la casilla de verificación del grupo y haga clic en **[!UICONTROL Eliminar]** y, a continuación, haga clic en **[!UICONTROL Guardar]**.


1. Para editar las funciones del usuario, haga clic en el botón **[!UICONTROL Asignaciones de funciones]** y haga lo siguiente:

   * Para mostrar una lista de funciones, haga clic en **[!UICONTROL Buscar funciones]**.
   * Para agregar una función, seleccione la casilla de verificación de la función y haga clic en **[!UICONTROL OK]** y, a continuación, haga clic en **[!UICONTROL Guardar]**.
   * Para quitar una función, seleccione la casilla de verificación de la función y haga clic en **[!UICONTROL Anulación de asignación]** y, a continuación, haga clic en **[!UICONTROL Guardar]**.

## Eliminar un usuario {#delete-a-user}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Usuarios y grupos]**.
1. Para buscar el usuario que desea eliminar, haga lo siguiente:

   * En el **[!UICONTROL Buscar]** , escriba los criterios de búsqueda.
   * En el **[!UICONTROL Uso]** lista, seleccionar **[!UICONTROL Nombre]**, **[!UICONTROL Correo electrónico]** o **[!UICONTROL ID de usuario]**.
   * En el **[!UICONTROL En la lista]**, seleccione **[!UICONTROL Usuarios]**.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y, a continuación, haga clic en **[!UICONTROL Buscar]**.

1. Seleccione la casilla de verificación del usuario y haga clic en **[!UICONTROL Eliminar]** y, a continuación, haga clic en **[!UICONTROL OK]**.

>[!NOTE]
>
>AEM Forms en JEE también permite que los usuarios del complemento de formularios AEM que se ejecuta en un OSGi sean reconocidos como usuarios AEM. Esto es necesario en escenarios en los que se requiere el inicio de sesión único entre AEM Forms en JEE y el complemento de formularios AEM que se ejecuta en un OSGi (por ejemplo, en el espacio de trabajo de HTML). La operación de eliminación mencionada anteriormente elimina a un usuario solo de AEM Forms en JEE. El usuario no se elimina del complemento de AEM Forms que se ejecuta en un entorno OSGi. Sin embargo, cualquier intento de inicio de sesión realizado después de eliminar el usuario (un intento de inicio de sesión en el servidor JEE de complemento de AEM Forms o en el complemento de AEM Forms en el entorno OSGi) se niega.

## Crear un controlador de error de inicio de sesión personalizado {#create-custom-login-error-handler}

Si un usuario sin los formularios de AEM y los permisos de CQ necesarios intenta iniciar sesión en las siguientes aplicaciones incrustadas en CQ, se redirige al usuario a la página predeterminada de CQ 404 que contiene el seguimiento de errores:

* Solución de gestión de correspondencia
* AEM forms Workspace

   ***nota **: Flex Workspace está en desuso para AEM versión de formularios.*

* administrador de formularios
* Informes de procesos 

CQ proporciona un mecanismo para anular el jsp de controlador 404 predeterminado.

Para obtener más información sobre cómo personalizar la página de administración de errores, consulte [Personalización de páginas que muestra el Controlador de errores](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=en) en la documentación de Adobe Experience Manager.
