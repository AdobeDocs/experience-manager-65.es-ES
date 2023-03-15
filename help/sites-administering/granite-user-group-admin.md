---
title: 'Operaciones de Granite: administración de usuarios y grupos'
seo-title: Granite Operations - User and Group Administration
description: Obtenga información sobre la administración de usuarios y grupos de Granite.
seo-description: Learn about Granite user and group administration.
uuid: 7b6b7767-712c-4cc8-8d90-36f26280d6e3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 95ab2e54-0f8d-49e0-ad20-774875f6f80a
exl-id: f3477d21-7e9a-4588-94e8-496bc42434a8
feature: Security
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 4%

---

# Operaciones de Granite: administración de usuarios y grupos{#granite-operations-user-and-group-administration}

Como Granite incorpora la implementación del repositorio CRX de la especificación de la API de JCR, tiene su propia administración de usuarios y grupos.

Estas cuentas son la base subyacente de la [AEM cuentas de](/help/sites-administering/security.md) y cualquier cambio de cuenta realizado con la administración de Granite se reflejará si/cuando se accede a las cuentas desde el [AEM Consola de usuarios](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console) (p. ej., `http://localhost:4502/useradmin`). AEM AEM Desde la consola Usuarios de la también puede administrar los privilegios y otros detalles de la.

Las consolas de administración de grupos y usuarios de Granite están disponibles en el **[Herramientas](/help/sites-administering/tools-consoles.md)** consola de la IU táctil optimizada:

![chlimage_1-72](assets/chlimage_1-72a.png)

Elección de una **Usuarios** o **Grupos** desde la consola Herramientas se abrirá la consola adecuada. En ambos, puede realizar acciones utilizando el cuadro de clic y luego las acciones de la barra de herramientas, o abriendo los detalles de la cuenta mediante el vínculo en **Nombre**.

* [Administración de usuarios](#user-administration)

   ![chlimage_1-73](assets/chlimage_1-73a.png)

   El **Usuarios** listas de la consola:

   * el nombre de usuario
   * el nombre de inicio de sesión del usuario (nombre de cuenta)
   * cualquier título que se haya dado a la cuenta

* [Administración de grupos](#group-administration)

   ![chlimage_1-74](assets/chlimage_1-74a.png)

   El **Grupos** listas de la consola:

   * el nombre del grupo
   * la descripción del grupo
   * el número de usuarios/grupos del grupo

## Administración de usuarios {#user-administration}

### Adición de un nuevo usuario {#adding-a-new-user}

1. Utilice el **Añadir usuario** icono:

   ![](do-not-localize/chlimage_1-1.png)

1. El **Crear usuario** se abrirá el formulario:

   ![chlimage_1-75](assets/chlimage_1-75a.png)

   Aquí puede introducir los detalles del usuario de la cuenta (la mayoría son estándar y explicativos):

   * **ID**

      Esta es la identificación única de la cuenta de usuario. Es obligatorio y no puede contener espacios.

   * **Dirección de correo electrónico**
   * **Contraseña**

      Es obligatorio introducir una contraseña.

   * **Repetir contraseña**

      Esto es obligatorio, ya que es necesario para confirmar la contraseña.

   * **Nombre**
   * **Apellidos**
   * **Número telefónico**
   * **Puesto de trabajo**
   * **Calle**
   * **Móvil**
   * **Ciudad**
   * **Código postal**
   * **País**
   * **Estado**
   * **Título**
   * **Sexo**
   * **Acerca de**
   * **Configuración de la cuenta**

      * **Estado**
Puede marcar la cuenta como 
**activo** o **inactivo**.
   * **Fotografía**

      Aquí puede cargar una foto para utilizarla como avatar.

      Tipos de archivo admitidos: `.jpg .png .tif .gif`

      Tamaño preferido: `240x240px`

   * **Añadir usuario a los grupos**

      Utilice la lista desplegable de selección para seleccionar los grupos a los que debe pertenecer el usuario. Una vez seleccionada, utilice el **X** por el nombre para anular la selección antes de guardar.

   * **Grupos**

      Una lista de los grupos de los que el usuario es miembro actualmente. Utilice el **X** por el nombre para anular la selección antes de guardar.


1. Una vez definida la cuenta de usuario, utilice:

   * **Cancelar** para anular el registro.
   * **Guardar** para completar el registro. La creación de la cuenta de usuario se confirmará con un mensaje.

### Edición de un usuario existente {#editing-an-existing-user}

1. Acceda a los detalles del usuario desde el vínculo bajo el nombre de usuario en la consola Usuarios.

1. Ahora puede editar los detalles como en [Adición de un nuevo usuario](#adding-a-new-user).

1. Acceda a los detalles del usuario desde el vínculo bajo el nombre de usuario en la consola Usuarios.

1. Ahora puede editar los detalles como en [Adición de un nuevo usuario](#adding-a-new-user).

### Cambio de la contraseña de un usuario existente {#changing-the-password-for-an-existing-user}

1. Acceda a los detalles del usuario desde el vínculo bajo el nombre de usuario en la consola Usuarios.

1. Ahora puede editar los detalles como en [Adición de un nuevo usuario](#adding-a-new-user). En **Configuración de cuenta** hay un vínculo para **Cambiar contraseña**.

   ![chlimage_1-76](assets/chlimage_1-76a.png)

1. El **Cambiar contraseña** se abrirá. Introduzca y vuelva a escribir la nueva contraseña, junto con la suya. Uso **OK** para confirmar los cambios.

   ![chlimage_1-77](assets/chlimage_1-77a.png)

   Un mensaje confirmará que la contraseña se ha cambiado.

### Asignación rápida de grupos {#quick-group-assignment}

1. Utilice la casilla de verificación para marcar uno o varios usuarios.
1. Utilice el **Grupos** icono:

   ![](do-not-localize/chlimage_1-2.png)

   Para abrir la lista desplegable de selección de grupo:

   ![chlimage_1-78](assets/chlimage_1-78a.png)

1. En el cuadro de selección puede seleccionar o anular la selección de los grupos a los que debe pertenecer la cuenta de usuario.

1. Cuando haya asignado o desasignado los grupos según sea necesario, utilice:

   * **Cancelar** para anular los cambios
   * **Guardar** para confirmar los cambios

### Eliminación de detalles del usuario existente {#deleting-existing-user-details}

1. Utilice la casilla de verificación para marcar uno o varios usuarios.
1. Utilice el **Eliminar** icono para eliminar los detalles del usuario:

   ![](do-not-localize/chlimage_1-3.png)

1. Se le pedirá que confirme la eliminación y un mensaje confirmará que la eliminación real se ha realizado.

## Administración de grupos {#group-administration}

### Adición de un nuevo grupo {#adding-a-new-group}

1. Utilice el icono Añadir grupo:

   ![](do-not-localize/chlimage_1-4.png)

1. El **Crear grupo** se abrirá el formulario:

   ![chlimage_1-79](assets/chlimage_1-79a.png)

   Aquí puede introducir los detalles del grupo:

   * **ID**

      Es un identificador único del grupo. Es obligatorio y no puede contener espacios.

   * **Nombre**

      Un nombre para el grupo; se mostrará en la consola Grupos.

   * **Descripción**

      Una descripción del grupo.

   * **Añadir miembros al grupo**

      Utilice la lista desplegable de selección para seleccionar los usuarios que desea añadir al grupo. Una vez seleccionada, utilice el **X** por el nombre para anular la selección antes de guardar.

   * **Miembros del grupo**

      Una lista de los usuarios del grupo. Utilice el **X** por el nombre para anular la selección antes de guardar.

1. Cuando haya definido el grupo, utilice:

   * **Cancelar** para anular el registro.
   * **Guardar** para completar el registro. La creación del grupo se confirmará con un mensaje.

### Edición de un grupo existente {#editing-an-existing-group}

1. Acceda a los detalles del grupo desde el vínculo bajo el nombre del grupo en la consola Grupos.

1. Ahora puede editar y guardar los detalles como en [Adición de un nuevo grupo](#adding-a-new-group).

### Copia de un grupo existente {#copying-an-existing-group}

1. Utilice la casilla para marcar un grupo.
1. Utilice el **Copiar** para copiar los detalles del grupo:

   ![](do-not-localize/chlimage_1-5.png)

1. El **Editar configuración de grupo** se abrirá el formulario.

   El ID de grupo es el mismo que el original, pero con el prefijo `Copy of`. Debe editarlo, ya que el ID no puede contener espacios. Todos los demás detalles serán los mismos que el original.

   Ahora puede editar y guardar los detalles como en [Adición de un nuevo grupo](#adding-a-new-group).

### Eliminación de un grupo existente {#deleting-an-existing-group}

1. Utilice el cuadro de diálogo para marcar uno o más grupos.
1. Utilice el **Eliminar** icono para eliminar los detalles del grupo:

   ![](do-not-localize/chlimage_1-6.png)

1. Se le pedirá que confirme la eliminación y un mensaje confirmará que la eliminación real se ha realizado.
