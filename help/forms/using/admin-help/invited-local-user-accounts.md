---
title: Administración de cuentas de usuario invitadas y locales
seo-title: Administración de cuentas de usuario invitadas y locales
description: Con la seguridad de los documentos, puede buscar, ver, editar, bloquear, desbloquear y eliminar cuentas de usuario locales e invitadas.
seo-description: Con la seguridad de los documentos, puede buscar, ver, editar, bloquear, desbloquear y eliminar cuentas de usuario locales e invitadas.
uuid: 0d0c717a-6e6e-4e42-96eb-3a7166e215ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 65720eed-ab06-463f-9567-2fdc468b6219
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 0%

---


# Administración de cuentas de usuario invitadas y locales {#managing-invited-and-local-user-accounts}

Utilice la página Usuarios invitados y locales para administrar los usuarios invitados y locales. Esta página solo se muestra si se cumplen los siguientes requisitos:

* Es un administrador al que se le asigna la función de seguridad del documento Administrar usuarios invitados y locales y la función de usuario de la consola de administración. (Consulte [Creación y configuración de funciones](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)).
* El registro de usuario invitado está habilitado. (Consulte [Configuración del registro de usuario invitado](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration)).

La página Usuarios invitados y locales contiene dos pestañas que puede utilizar para buscar, ver, editar, bloquear, desbloquear y eliminar cuentas de usuario locales e invitadas.

También puede enviar manualmente correos electrónicos de registro a los usuarios invitados. Puede que desee hacer esto, por ejemplo, si el periodo de registro que finaliza el correo electrónico autorizado y el usuario no puede utilizar la URL para registrarse. En este caso, puede reenviar un correo electrónico de registro al usuario invitado. Cuando el usuario invitado se registra y activa la cuenta, se convierte en un usuario local.

>[!NOTE]
>
>Los usuarios invitados también pueden agregarse directamente a través del directorio LDAP en el que se documentan las referencias de seguridad, o cuando un usuario o administrador invita a un nuevo usuario a la hora de crear o editar una directiva, iniciando así un correo electrónico de invitación de registro. Los usuarios pueden agregar nuevos usuarios invitados a directivas si activa la opción Habilitar registro de usuario invitado en la página Registro de usuario invitado .

## Agregar un usuario invitado {#add-an-invited-user}

Puede agregar una o más cuentas de usuario invitadas para documentar la seguridad a la vez. Para añadir una cuenta de usuario invitada, necesita la dirección de correo electrónico del usuario. Cuando agrega un usuario, document security envía un correo electrónico de registro en el que se invita al usuario a registrarse.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Usuarios invitados y locales y, a continuación, haga clic en Invitar nuevo usuario.
1. Escriba las direcciones de correo electrónico de los usuarios que desea invitar. Introduzca varias direcciones en una línea, separadas por una coma.

   El mensaje que creó al habilitar el registro de usuario invitado se envía a los usuarios. (Consulte [Configuración del registro de usuario invitado](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration)).

1. Haga clic en Aceptar.

## Ver información sobre un usuario local {#view-information-about-a-local-user}

Puede ver información sobre los usuarios locales, como el nombre, la dirección de correo electrónico, la organización, el estado de registro y el dominio.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Usuarios invitados y locales y, a continuación, haga clic en Invitar nuevo usuario.
1. Haga clic en la ficha Usuarios locales y, en la página Administrar usuarios locales , haga clic en la dirección de correo electrónico del usuario que desee ver.

   Se muestran los detalles del usuario y puede restablecer su contraseña y desactivarla.

## Enviar un correo electrónico a un usuario externo no registrado {#send-an-email-to-an-unregistered-external-user}

Cuando se añade un usuario invitado, la seguridad de los documentos envía automáticamente al usuario una solicitud de correo electrónico de registro. También puede generar manualmente un correo electrónico de registro para enviarlo a un usuario invitado que aún no se haya registrado. Puede que desee hacer esto, por ejemplo, para enviar una nueva invitación si caduca el correo electrónico de registro de un usuario invitado.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Usuarios invitados y locales.
1. En la lista de usuarios, seleccione la casilla de verificación de cada usuario para enviar un correo electrónico de registro a y, a continuación, haga clic en Reenviar correo electrónico de invitación.
1. Revise la lista de usuarios seleccionados y haga clic en Aceptar.

## Restablecer una contraseña de usuario local {#reset-a-local-user-password}

Puede restablecer las contraseñas de los usuarios invitados activados que se registraron con seguridad de documento pero olvidaron su contraseña. Cuando restablece una contraseña, se genera un correo electrónico que contiene una nueva contraseña temporal para el usuario.

Cuando habilitó el proceso de registro de usuarios invitados, creó un mensaje de correo electrónico que se enviará a los usuarios pidiéndoles que restablezcan sus contraseñas. (Consulte [Configuración del registro de usuario invitado](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration)).

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Usuarios invitados y locales y, a continuación, haga clic en la ficha Usuarios locales .
1. En la lista de usuarios, seleccione el usuario correspondiente.
1. En la página Administrar usuario local , haga clic en Restablecer contraseña y en Aceptar. Se envía al usuario un correo electrónico de contraseña de restablecimiento que contiene la nueva contraseña.

## Habilitar o deshabilitar una cuenta de usuario {#enable-or-disable-a-user-account}

Puede deshabilitar las cuentas de usuario locales para restringir temporalmente el inicio de sesión de un usuario a la seguridad del documento. Cuando deshabilita la cuenta, el usuario no puede usar documentos protegidos por políticas ni crear ni aplicar políticas.

Puede habilitar una cuenta de usuario local que esté deshabilitada actualmente. No puede habilitar una cuenta de usuario invitado que aparezca como registrada. El estado de registro indica que el usuario invitado está registrado pero aún no ha activado la cuenta mediante el vínculo en el correo electrónico de activación.

**Restringir una cuenta de usuario**

1. En la Consola de administración, haga clic en Servicios > seguridad del documento > Usuarios invitados y locales y haga clic en la ficha Usuarios locales .
1. En la lista de usuarios, seleccione el usuario correspondiente.
1. En la página Detalle de usuario local, haga clic en Deshabilitar cuenta.

**Restablecer una cuenta de usuario**

1. Haga clic en Usuarios invitados y locales y, a continuación, en la ficha Usuarios locales .
1. En la lista de usuarios, seleccione el usuario correspondiente.
1. En la página Detalle de usuario local, haga clic en Activar cuenta.

## Eliminar una cuenta de usuario invitada {#remove-an-invited-user-account}

Puede eliminar las cuentas de usuario invitadas de la seguridad de documentos. Puede que desee eliminar una cuenta, por ejemplo, cuando un usuario cambia su información personal de cuenta de correo electrónico.

Si elimina una cuenta de usuario, solo usted u otro administrador puede restablecer la cuenta seleccionando la opción Agregar usuario invitado en la página Usuarios invitados . Los usuarios no pueden agregar la cuenta de usuario eliminada a una directiva y ese método no puede iniciar ningún proceso de invitación.

>[!NOTE]
>
>Los usuarios invitados que se eliminaron a través de la interfaz de Administración de usuarios de formularios AEM no se pueden volver a invitar hasta que se hayan eliminado de nuevo mediante el siguiente procedimiento.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Usuarios invitados y locales y, a continuación, haga clic en la ficha Usuarios invitados .
1. Seleccione la casilla de verificación situada junto a uno o varios usuarios, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

## Buscar una cuenta de usuario {#search-for-an-invited-user-account} invitada

Puede buscar cuentas de usuario invitadas mediante una dirección de correo electrónico.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Usuarios invitados y locales.
1. En el cuadro Buscar correo electrónico, escriba la dirección de correo electrónico del usuario y haga clic en Buscar.

## Buscar una cuenta de usuario local {#search-for-a-local-user-account}

Puede buscar un usuario local utilizando la dirección de correo electrónico o el nombre y el dominio del usuario.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Usuarios invitados y locales y, a continuación, haga clic en la ficha Usuarios locales .
1. Escriba los criterios de búsqueda en el cuadro Buscar, seleccione Nombre o Correo electrónico y, a continuación, haga clic en Buscar.

## Eliminar una cuenta de usuario local {#remove-a-local-user-account}

Puede eliminar las cuentas de usuario locales de la seguridad de documentos. Puede que desee eliminar cuentas, por ejemplo, cuando los usuarios cambien su información personal de cuenta de correo electrónico.

1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Usuarios invitados y locales y, a continuación, haga clic en la ficha Usuarios locales .
1. Seleccione la casilla de verificación situada junto a uno o varios usuarios, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

## Ordenar la lista de usuarios {#sort-the-user-list}

Puede encontrar usuarios más fácilmente ordenando la lista de usuarios por encabezado de columna. Los iconos de triángulo junto al encabezado de la columna indican qué columna se utiliza actualmente para ordenar:

* Un triángulo que señala hacia arriba indica el orden ascendente.
* Un triángulo que señala hacia abajo indica un orden descendente.

   1. En la consola de administración, haga clic en Servicios > Seguridad de documentos > Usuarios invitados y locales.
   1. Para ordenar los usuarios invitados, haga clic en la ficha Usuarios invitados y haga clic en el encabezado de columna correspondiente.
   1. Para ordenar los usuarios locales, haga clic en la ficha Usuarios locales y luego en el encabezado de columna correspondiente.

