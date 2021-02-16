---
title: 'Añadir y configurar usuarios '
seo-title: 'Añadir y configurar usuarios '
description: La configuración de Administración de usuarios de la consola de administración permite crear o eliminar usuarios y configurar otras opciones de usuario.
seo-description: La configuración de Administración de usuarios de la consola de administración permite crear o eliminar usuarios y configurar otras opciones de usuario.
uuid: fe650cdb-7d0d-4f38-9899-e5349559ed32
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
discoiquuid: 20ca99e3-4843-4254-b3e9-0255cc752363
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---


# Añadir y configurar usuarios {#adding-and-configuring-users}

La información de usuarios y grupos se mantiene en un sistema de almacenamiento de terceros, como un directorio LDAP. La Administración de usuarios no escribe en el sistema de almacenamiento de terceros. En su lugar, la Administración de usuarios sincroniza la información de usuarios y grupos con su propia base de datos

## Crear un usuario {#create-a-user}

Al crear usuarios, puede agregarlos a grupos y asignarles funciones.

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Usuarios y grupos]** y haga clic en **[!UICONTROL Nuevo usuario]**.
.
1. En **[!UICONTROL Configuración general]**, proporcione la información necesaria y haga clic en **[!UICONTROL Siguiente]**. Para obtener más información sobre la configuración, consulte [Configuración del usuario](adding-configuring-users.md#user-settings).
1. (Opcional) Para agregar el usuario a un grupo, haga clic en **[!UICONTROL Buscar grupos]** y realice las siguientes tareas:

   * En el cuadro **[!UICONTROL Buscar]**, escriba todo o parte del nombre del grupo.
   * Seleccione el dominio que desea buscar, seleccione el número de elementos que desea mostrar y haga clic en **[!UICONTROL Buscar]**.
   * (Opcional) Para vista de los detalles del grupo, seleccione el nombre del grupo y haga clic en **[!UICONTROL Aceptar]** para volver a la página de resultados de búsqueda.
   * Seleccione la casilla de verificación del grupo y haga clic en **[!UICONTROL Aceptar]**.
   * Haga clic en **[!UICONTROL Siguiente]**. 

1. (Opcional) Para asignar funciones al usuario, haga clic en **[!UICONTROL Buscar funciones]**, seleccione la casilla de verificación de las funciones que desea asignar y, a continuación, haga clic en **[!UICONTROL Aceptar]**.
1. Haga clic en **[!UICONTROL Finalizar]**.

   >[!NOTE]
   >
   >Si encuentra algún problema de inicio de sesión con el usuario, consulte [AEM Forms en JEE no puede iniciar sesión en AEM Forms en OSGi side](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## Configuración de usuario {#user-settings}

Especifique la siguiente configuración cuando cree o edite un usuario.

**Nombre canónico:**  (obligatorio) Identificador único del usuario. Cada usuario y grupo de un dominio debe tener un nombre canónico único. Seleccione la casilla Generado por el sistema para permitir que la Administración de usuarios asigne un valor único, o bien desactive la casilla de verificación y especifique un valor personalizado para el Nombre canónico.

Evite utilizar caracteres de subrayado (_) en nombres canónicos, por ejemplo, `sample_user`. Al buscar usuarios en función de su nombre canónico, no se devuelven los que contienen caracteres de subrayado.

**Nombre:**  (obligatorio) nombre del usuario

**Apellidos:** (obligatorio) nombre de la familia del usuario

**Nombre común:Nombre** completo o nombre para mostrar del usuario. Por ejemplo, si Nombre = Gloria y Apellido = Ríos, entonces Nombre común = Ríos de Gloria.

**Correo electrónico:dirección de correo electrónico del** usuario

**Teléfono:número de teléfono del** usuario

**Descripción:Descripción** opcional. Utilice este campo según las necesidades de su organización.

**Dirección:dirección de correo del** usuario

**Organización:** Organización a la que pertenece el usuario

**Alias de correo electrónico: alias de correo electrónico del** usuario. Separe los alias de correo electrónico con comas.

**Dominio:** Dominio al que pertenece el usuario

**Configuración regional:configuración regional ISO del** usuario

**Clave de calendario comercial:** le permite asignar un calendario comercial a un usuario, según el valor de esta configuración. Los calendarios comerciales definen los días laborables y no laborables. AEM formularios pueden utilizar calendarios comerciales para calcular fechas y horas futuras para eventos como recordatorios, plazos y escalaciones. La forma en que asigne claves de calendario empresarial a los usuarios dependerá de si utiliza un dominio empresarial, local o híbrido. (Consulte [Añadir dominios](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Si utiliza un dominio local o híbrido, la información sobre los usuarios se almacena únicamente en la base de datos de Administración de usuarios. Para estos usuarios, establezca la clave del calendario comercial en una cadena. A continuación, asigne la clave del calendario comercial (la cadena) a un calendario comercial en el flujo de trabajo de los formularios.

Si utiliza un dominio de empresa, la información sobre los usuarios reside en un sistema de almacenamiento de terceros, como un directorio LDAP. La Administración de usuarios sincroniza la información de usuario del directorio con la base de datos de Administración de usuarios. Esta función le permite asignar una clave de calendario comercial a un campo del directorio LDAP. Por ejemplo, imaginemos un escenario en el que cada registro de usuario del directorio contiene un campo de país y desea asignar calendarios comerciales basados en el país donde se encuentra el usuario. En este caso, debe especificar el nombre del campo de país como valor para la configuración de la clave del calendario comercial. A continuación, puede asignar las claves de calendario empresarial (los valores definidos para el campo de país en el directorio LDAP) a los calendarios comerciales en el flujo de trabajo de formularios.

Para obtener información adicional sobre los calendarios comerciales, incluida la asignación de claves de calendario empresarial a los calendarios comerciales, consulte [Configuración de calendarios comerciales](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Limite el nombre a menos de 53 caracteres. Un nombre más corto ayuda a evitar problemas al mostrar la clave del calendario comercial en las páginas de Administración de procesos de la consola de administración.

**ID de usuario:**  (obligatorio) ID de usuario que utiliza el usuario para iniciar sesión. El ID de usuario no distingue entre mayúsculas y minúsculas y debe ser único en todo el dominio.

En los dominios de empresa, utilice un atributo que no sea DN como ID de usuario porque el DN de un usuario puede cambiar si se mueve a otra parte de la organización. Esta configuración depende del servidor de directorio. El valor es `objectGUID` para Active Directory 2003, `nsuniqueID` para Sun™ One y `guid` para eDirectory.

Asegúrese de que el ID de usuario sea único. No utilice uno que se haya asignado a un usuario eliminado.

AEM formularios no pueden diferenciar entre cuentas de usuario que tienen ID de usuario y contraseñas idénticas pero que pertenecen a dominios diferentes. Para evitar este problema, no cree cuentas que tengan el mismo ID de usuario en varios dominios.

Cuando se utiliza SQL Server como base de datos, no se puede crear un ID de usuario que supere los 255 caracteres.

Al utilizar MySQL, el ID de usuario puede contener caracteres extendidos. Sin embargo, cuando se realiza una comparación entre dos cadenas, como abcde y âbcdè, se consideran las mismas. Por ejemplo, al sincronizar, si se ha agregado un nuevo usuario a la base de datos, se realiza una comparación para comprobar si existe un usuario con el mismo ID de usuario en la base de datos. Si el usuario *abcde* ya existe en la base de datos cuando se agrega el nuevo usuario *âbcdè*, la comparación no puede distinguir entre los dos nombres. Se da por hecho que el usuario ya existe en la base de datos y que el nuevo usuario se ignora y no se agrega.

Evite crear nombres de usuario que comiencen con un signo de número (#). Al realizar búsquedas de tarea no se obtienen resultados para esos nombres de usuario. (Consulte [Uso de tareas](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Contraseña y Confirmar contraseña:** Contraseña que utiliza el usuario para iniciar sesión. Debe tener un mínimo de ocho caracteres. No se requiere una contraseña para un usuario que forme parte de un dominio híbrido.

## Detalles de vista acerca de un usuario {#view-details-about-a-user}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. Especifique la información para reducir la búsqueda y, en la lista En, seleccione Usuarios y, a continuación, haga clic en Buscar. Los resultados de la búsqueda se enumeran en la parte inferior de la página. Puede ordenar la lista haciendo clic en cualquiera de los encabezados de columna.
1. Haga clic en el nombre del usuario para mostrar los detalles. La página Editar usuario muestra los siguientes detalles sobre el usuario:

   * Información general de identificación, como nombre, correo electrónico, dirección, dominio y organización
   * Funciones asignadas al usuario
   * Agrupa al usuario como miembro de

## Cambiar la contraseña de un usuario local {#change-the-password-for-a-local-user}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Usuarios y grupos]**.
1. Especifique la información para reducir la búsqueda de un usuario en particular y haga clic en **[!UICONTROL Buscar]**. Los resultados de la búsqueda se enumeran en la parte inferior de la página. Puede ordenar la lista haciendo clic en cualquiera de los encabezados de columna.
1. Haga clic en el nombre del usuario y, a continuación, haga clic en **[!UICONTROL Cambiar contraseña]**.
1. Escriba y confirme la nueva contraseña y, a continuación, haga clic en **[!UICONTROL Aceptar]**. La contraseña debe tener un mínimo de ocho caracteres.

## Editar las propiedades de un usuario {#edit-a-user-s-properties}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Usuarios y grupos]**.
1. Para buscar al usuario que editar, realice las siguientes tareas:

   * En el cuadro **[!UICONTROL Buscar]**, escriba los criterios de búsqueda.
   * En la lista **[!UICONTROL Utilizando]**, seleccione **[!UICONTROL Nombre]**, **[!UICONTROL Correo electrónico]** o **[!UICONTROL ID de usuario]**.
   * En la **[!UICONTROL lista]**, seleccione **[!UICONTROL Usuarios]**.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y, a continuación, haga clic en **[!UICONTROL Buscar]**.

1. Haga clic en el usuario para editar.
1. Para un usuario que forme parte de un dominio local o híbrido, en la ficha **[!UICONTROL Detalle]**, edite la **[!UICONTROL Configuración general]** y **[!UICONTROL Configuración de inicio de sesión]** y haga clic en **[!UICONTROL Guardar]**. Para obtener más información sobre la configuración, consulte [Configuración del usuario](adding-configuring-users.md#user-settings). No puede editar la configuración general y de inicio de sesión de un usuario que pertenece a un dominio de empresa.
1. Para editar la configuración del grupo para el usuario, haga clic en la ficha **[!UICONTROL Pertenencia al grupo]** y realice las siguientes tareas:

   * Haga clic en **[!UICONTROL Buscar grupo]** y complete la información de búsqueda.
   * Para agregar el usuario a un nuevo grupo, seleccione la casilla de verificación del grupo, haga clic en **[!UICONTROL Aceptar]** y, a continuación, haga clic en **[!UICONTROL Guardar]**.

   >[!NOTE]
   >
   >Los usuarios locales no se pueden agregar a los grupos de directorios. Sin embargo, los usuarios del directorio pueden agregarse a grupos locales.

   * Para eliminar el usuario de un grupo, seleccione la casilla de verificación del grupo, haga clic en **[!UICONTROL Eliminar]** y, a continuación, haga clic en **[!UICONTROL Guardar]**.


1. Para editar las funciones del usuario, haga clic en la ficha **[!UICONTROL Asignaciones de funciones]** y lleve a cabo estas tareas:

   * Para mostrar una lista de roles, haga clic en **[!UICONTROL Buscar roles]**.
   * Para agregar una función, seleccione la casilla de verificación de la función, haga clic en **[!UICONTROL Aceptar]** y, a continuación, haga clic en **[!UICONTROL Guardar]**.
   * Para quitar una función, seleccione la casilla de verificación de la función, haga clic en **[!UICONTROL Cancelar asignación]** y, a continuación, haga clic en **[!UICONTROL Guardar]**.

## Eliminar un usuario {#delete-a-user}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Usuarios y grupos]**.
1. Para buscar el usuario que desea eliminar, realice las siguientes tareas:

   * En el cuadro **[!UICONTROL Buscar]**, escriba los criterios de búsqueda.
   * En la lista **[!UICONTROL Utilizando]**, seleccione **[!UICONTROL Nombre]**, **[!UICONTROL Correo electrónico]** o **[!UICONTROL ID de usuario]**.
   * En la **[!UICONTROL lista]**, seleccione **[!UICONTROL Usuarios]**.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y, a continuación, haga clic en **[!UICONTROL Buscar]**.

1. Seleccione la casilla de verificación del usuario, haga clic en **[!UICONTROL Eliminar]** y, a continuación, haga clic en **[!UICONTROL Aceptar]**.

>[!NOTE]
>
>AEM Forms en JEE también permite que los usuarios del complemento de formularios AEM que se ejecutan en un OSGi se reconozcan como usuarios AEM. Esto es necesario para situaciones en las que se requiere el inicio de sesión único entre AEM Forms en JEE y AEM complemento de formularios que se ejecuta en un OSGi (por ejemplo, espacio de trabajo HTML). La operación de eliminación mencionada anteriormente elimina un usuario solo de AEM Forms en JEE. El usuario no se elimina del complemento de AEM Forms que se ejecuta en OSGi entorno. Sin embargo, se deniega cualquier intento de inicio de sesión que se realice después de eliminar el usuario (un intento de inicio de sesión en el servidor JEE del complemento de AEM Forms o en el complemento de AEM Forms en el entorno OSGi).

## Crear un controlador de error de inicio de sesión personalizado {#create-custom-login-error-handler}

Si un usuario sin los formularios de AEM y los permisos de CQ necesarios intenta iniciar sesión en las siguientes aplicaciones integradas en CQ, se le redirige a la página predeterminada de CQ 404 que contiene el seguimiento de errores:

* Solución de administración de correspondencia
* Área de trabajo de formularios AEM

   ***nota **: Flex Workspace está obsoleto para AEM versión de formularios.*

* administrador de formularios
* Informes de procesos

CQ proporciona un mecanismo para anular el jsp predeterminado del controlador 404.

Para obtener más información sobre cómo personalizar la página de administración de errores, consulte [Personalización de páginas mostradas por el controlador de errores](https://docs.adobe.com/docs/en/cq/current/developing/customizing_error_handler_pages.html) en la documentación de Adobe Experience Manager.
