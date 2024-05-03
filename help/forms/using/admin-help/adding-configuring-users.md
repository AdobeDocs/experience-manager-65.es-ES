---
title: Agregar y configurar usuarios
description: La configuración de Administración de usuarios en la consola de administración le permite crear o eliminar usuarios y configurar otras opciones de configuración de usuario.
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 1%

---

# Agregar y configurar usuarios {#adding-and-configuring-users}

La información de usuarios y grupos se mantiene en un sistema de almacenamiento de terceros, como un directorio LDAP. Administración de usuarios no escribe en el sistema de almacenamiento de terceros. En su lugar, Administración de usuarios sincroniza la información de usuarios y grupos con su propia base de datos

## Crear un usuario {#create-a-user}

Cuando cree usuarios, puede agregarlos a grupos y asignarles funciones.

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Usuarios y grupos]** y haga clic en **[!UICONTROL Nuevo usuario]**. .
1. En **[!UICONTROL Configuración general]**, proporcione la información necesaria y haga clic en **[!UICONTROL Siguiente]**. Para obtener más información sobre la configuración, consulte [Configuración de usuario](adding-configuring-users.md#user-settings).
1. (Opcional) Para agregar el usuario a un grupo, haga clic en **[!UICONTROL Buscar grupos]** y realice estas tareas:

   * En el **[!UICONTROL Buscar]** , escriba todo o parte del nombre del grupo.
   * Seleccione el dominio que desea buscar, seleccione el número de elementos que desea mostrar y haga clic en **[!UICONTROL Buscar]**.
   * (Opcional) Para ver los detalles del grupo, seleccione el nombre del grupo y haga clic en **[!UICONTROL OK]** para volver a la página de resultados de la búsqueda.
   * Seleccione la casilla del grupo y haga clic en **[!UICONTROL OK]**.
   * Haga clic en **[!UICONTROL Siguiente]**.

1. (Opcional) Para asignar funciones al usuario, haga clic en **[!UICONTROL Buscar roles]**, active la casilla de verificación de las funciones que desea asignar y haga clic en **[!UICONTROL OK]**.
1. Haga clic en **[!UICONTROL Finalizar]**.

   >[!NOTE]
   >
   >Si encuentra algún problema de inicio de sesión con el usuario, consulte [AEM Forms en JEE no puede iniciar sesión en AEM Forms en OSGi](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## Configuración de usuario {#user-settings}

Especifique la siguiente configuración cuando cree o edite un usuario.

**Nombre canónico:** (Obligatorio) Identificador único del usuario. Cada usuario y grupo de un dominio debe tener un nombre canónico único. Seleccione la casilla de verificación Generado por el sistema para permitir que la Administración de usuarios asigne un valor único o desmarque la casilla de verificación y especifique un valor personalizado para el Nombre canónico.

Evite utilizar caracteres de guion bajo (_) en nombres canónicos, por ejemplo, `sample_user`. Cuando busca usuarios en función de su nombre canónico, no se devuelven los que contienen caracteres de guion bajo.

**Nombre:** (Obligatorio) Nombre de pila del usuario

**Apellidos:** (Obligatorio) Apellido del usuario

**Nombre común:** Nombre completo o nombre para mostrar del usuario. Por ejemplo, si Nombre = Gloria y Apellidos = Ríos, Nombre común = Gloria Ríos.

**Correo electrónico:** Dirección de correo electrónico del usuario

**Teléfono:** Número de teléfono del usuario

**Descripción:** Descripción opcional. Utilice este campo según las necesidades de su organización.

**Dirección:** Dirección de correo del usuario

**Organización:** Organización a la que pertenece el usuario

**Alias de correo electrónico:** Alias de correo electrónico del usuario. Separe los alias de los correos electrónicos con comas.

**Dominio:** Dominio al que pertenece el usuario

**Configuración regional:** Configuración regional ISO del usuario

**Clave de calendario empresarial:** Permite asignar un calendario empresarial a un usuario, según el valor de esta configuración. Los calendarios comerciales definen días laborables y no laborables. AEM Los formularios de datos pueden utilizar calendarios comerciales al calcular las fechas y horas futuras para eventos como recordatorios, plazos y escalaciones. La forma de asignar claves de calendario empresarial a los usuarios depende de si utiliza un dominio empresarial, local o híbrido. (Consulte [Adición de dominios](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Si utiliza un dominio local o híbrido, la información sobre los usuarios se almacena únicamente en la base de datos de Administración de usuarios. Para estos usuarios, establezca la Clave del calendario empresarial en una cadena. A continuación, asigne la clave del calendario empresarial (la cadena) a un calendario empresarial en el flujo de trabajo de Forms.

Si utiliza un dominio de empresa, la información sobre los usuarios reside en un sistema de almacenamiento de terceros, como un directorio LDAP. Administración de usuarios sincroniza la información de usuario del directorio con la base de datos de Administración de usuarios. Esta función permite asignar una clave de calendario empresarial a un campo del directorio LDAP. Por ejemplo, imagine un escenario en el que cada registro de usuario del directorio contiene un campo de país y desea asignar calendarios comerciales basados en el país en el que se encuentra el usuario. En este caso, especifique el nombre del campo de país como valor para la configuración Clave del calendario empresarial. A continuación, puede asignar las claves del calendario empresarial (los valores definidos para el campo de país en el directorio LDAP) a los calendarios empresariales en el flujo de trabajo de Forms.

Para obtener información adicional sobre los calendarios comerciales, incluido cómo asignar claves de calendario empresarial a calendarios comerciales, consulte [Configurar calendarios comerciales](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Limite el nombre a menos de 53 caracteres. Un nombre más corto ayuda a evitar problemas al mostrar la clave del calendario empresarial en las páginas Administración de procesos de la consola de administración.

**ID de usuario:** (Obligatorio) ID de usuario que utiliza el usuario para iniciar sesión. El ID de usuario no distingue entre mayúsculas y minúsculas y debe ser único en todo el dominio.

En los dominios de empresa, utilice un atributo que no sea DN como ID de usuario, ya que el DN de un usuario puede cambiar si se desplaza a otra parte de la organización. Esta configuración depende del servidor de directorio. El valor es `objectGUID` para Active Directory 2003, `nsuniqueID` para Sun™ One y `guid` para eDirectory.

Asegúrese de que el ID de usuario sea único. No utilice uno que se haya asignado a un usuario eliminado.

AEM Los formularios no pueden diferenciar entre cuentas de usuario que tienen ID y contraseñas de usuario idénticos, pero que pertenecen a dominios diferentes. Para evitar este problema, no cree cuentas con el mismo ID de usuario en varios dominios.

Cuando se utiliza SQL Server como base de datos, no se puede crear un Id. de usuario que supere los 255 caracteres.

Al utilizar MySQL, el ID de usuario puede contener caracteres extendidos. Sin embargo, cuando se realiza una comparación entre dos cadenas, como abcde y âbcdè, se consideran iguales. Por ejemplo, al sincronizar, si se agregó un nuevo usuario a la base de datos, se realiza una comparación para comprobar si existe un usuario con el mismo ID de usuario en la base de datos. Si el usuario *abcde* existe en la base de datos cuando el nuevo usuario *âbcdè* , la comparación no puede distinguir entre los dos nombres. Se da por hecho que el usuario existe en la base de datos y que el nuevo usuario se ignora y no se añade.

Evite crear nombres de usuario que comiencen con un signo de número (#). Al realizar búsquedas de tareas, no se obtienen resultados para esos nombres de usuario. (Consulte [Trabajar con tareas](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Contraseña y confirmar contraseña:** Contraseña que utiliza el usuario para iniciar sesión. Debe tener un mínimo de ocho caracteres. No se requiere una contraseña para un usuario que forme parte de un dominio híbrido.

## Ver detalles de un usuario {#view-details-about-a-user}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. Especifique información para limitar la búsqueda y, en la lista En, seleccione Usuarios y, a continuación, haga clic en Buscar. Los resultados de la búsqueda se muestran en la parte inferior de la página. Puede ordenar la lista haciendo clic en cualquiera de los encabezados de columna.
1. Haga clic en el nombre del usuario para mostrar detalles sobre. La página Editar Usuario muestra estos detalles, como se muestra a continuación, sobre el usuario:

   * Información general de identificación, como nombre, correo electrónico, dirección, dominio y organización
   * Funciones asignadas al usuario
   * Grupos a los que pertenece el usuario

## Cambiar la contraseña de un usuario local {#change-the-password-for-a-local-user}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Usuarios y grupos]**.
1. Especifique información para restringir la búsqueda de un usuario en particular y haga clic en **[!UICONTROL Buscar]**. Los resultados de la búsqueda se muestran en la parte inferior de la página. Puede ordenar la lista haciendo clic en cualquiera de los encabezados de columna.
1. Haga clic en el nombre del usuario y luego en **[!UICONTROL Cambiar contraseña]**.
1. Escriba y confirme la nueva contraseña y haga clic en **[!UICONTROL OK]**. La contraseña debe tener un mínimo de ocho caracteres.

## Editar las propiedades de un usuario {#edit-a-user-s-properties}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Usuarios y grupos]**.
1. Para buscar el usuario que desea editar, realice estas tareas:

   * En el **[!UICONTROL Buscar]** , escriba los criterios de búsqueda.
   * En el **[!UICONTROL Uso de]** , seleccione **[!UICONTROL Nombre]**, **[!UICONTROL Correo electrónico]**, o **[!UICONTROL ID de usuario]**.
   * En el **[!UICONTROL En la lista]**, seleccione **[!UICONTROL Usuarios]**.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y haga clic en **[!UICONTROL Buscar]**.

1. Haga clic en el usuario para editarlo.
1. Para un usuario que forme parte de un dominio local o híbrido, en la **[!UICONTROL Detalle]** , edite la pestaña **[!UICONTROL Configuración general]** y **[!UICONTROL Configuración de inicio]** y haga clic en **[!UICONTROL Guardar]**. Para obtener más información sobre la configuración, consulte [Configuración de usuario](adding-configuring-users.md#user-settings). No puede editar la configuración general y de inicio de sesión de un usuario que pertenece a un dominio de empresa.
1. Para editar la configuración de grupo del usuario, haga clic en **[!UICONTROL Pertenencia a grupo]** y realice estas tareas:

   * Clic **[!UICONTROL Buscar grupo]** y complete la información de búsqueda.
   * Para agregar el usuario a un nuevo grupo, marque la casilla de verificación del grupo y haga clic en **[!UICONTROL OK]** y haga clic en **[!UICONTROL Guardar]**.

   >[!NOTE]
   >
   >Los usuarios locales no se pueden agregar a grupos de directorios. Sin embargo, los usuarios del directorio pueden agregarse a los grupos locales.

   * Para quitar el usuario de un grupo, marque la casilla del grupo y haga clic en **[!UICONTROL Eliminar]** y haga clic en **[!UICONTROL Guardar]**.

1. Para editar las funciones del usuario, haga clic en **[!UICONTROL Asignaciones de roles]** y realice estas tareas:

   * Para mostrar una lista de funciones, haga clic en **[!UICONTROL Buscar roles]**.
   * Para agregar un rol, active la casilla correspondiente y haga clic en **[!UICONTROL OK]** y haga clic en **[!UICONTROL Guardar]**.
   * Para quitar un rol, active la casilla correspondiente y haga clic en **[!UICONTROL Desasignar]** y haga clic en **[!UICONTROL Guardar]**.

## Eliminar un usuario {#delete-a-user}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Usuarios y grupos]**.
1. Para buscar el usuario que desea eliminar, realice estas tareas:

   * En el **[!UICONTROL Buscar]** , escriba los criterios de búsqueda.
   * En el **[!UICONTROL Uso de]** , seleccione **[!UICONTROL Nombre]**, **[!UICONTROL Correo electrónico]**, o **[!UICONTROL ID de usuario]**.
   * En el **[!UICONTROL En la lista]**, seleccione **[!UICONTROL Usuarios]**.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y haga clic en **[!UICONTROL Buscar]**.

1. Seleccione la casilla de verificación del usuario y haga clic en **[!UICONTROL Eliminar]** y haga clic en **[!UICONTROL OK]**.

>[!NOTE]
>
>AEM Forms AEM AEM en JEE también permite reconocer como usuarios a los usuarios del complemento de formularios en forma de que se ejecutan en un OSGi. Esto es necesario en los casos en los que se requiera el inicio de sesión único entre AEM Forms AEM en JEE y el complemento de formularios en el que se ejecuta en un OSGi (por ejemplo, en el espacio de trabajo del HTML). La operación de eliminación mencionada elimina un usuario solo de AEM Forms en JEE. El usuario no se elimina del complemento de AEM Forms que se ejecuta en el entorno OSGi. Sin embargo, cualquier intento de inicio de sesión realizado después de eliminar el usuario (un intento de inicio de sesión en el servidor JEE de complementos de AEM Forms o complementos de AEM Forms en el entorno OSGi) se deniega.

## Crear controlador de errores de inicio de sesión personalizado {#create-custom-login-error-handler}

AEM Si un usuario sin los formularios y los permisos de CQ necesarios intenta iniciar sesión en las siguientes aplicaciones incrustadas en CQ, se redirige al usuario a la página predeterminada de CQ 404 que contiene el seguimiento de errores:

* Solución de Administración de correspondencia
* AEM Espacio de trabajo de formularios

  ***nota **: Flex AEM Workspace está en desuso para la versión de formularios en la que se ha realizado el.*

* administrador de formularios
* Informes de procesos 

CQ proporciona un mecanismo para anular el controlador jsp 404 predeterminado.

Para obtener más información sobre cómo personalizar la página de gestión de errores, consulte [Personalizar páginas mostradas por el controlador de error](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=en) en la documentación de Adobe Experience Manager.
