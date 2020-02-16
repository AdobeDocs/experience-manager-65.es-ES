---
title: Configuración de calendarios comerciales
seo-title: Configuración de calendarios comerciales
description: Los calendarios comerciales definen los días laborables y no laborables de la organización. Obtenga información sobre cómo configurar los calendarios comerciales.
seo-description: Los calendarios comerciales definen los días laborables y no laborables de la organización. Obtenga información sobre cómo configurar los calendarios comerciales.
uuid: 0ba610b8-72a8-480c-8783-70d98cbe890a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7a85e13d-4800-47c4-812a-5c6e2355298a
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Configuración de calendarios comerciales {#configuring-business-calendars}

*Los calendarios* comerciales definen los días laborables y no laborables (por ejemplo, días festivos legales, fines de semana y días de cierre de la empresa) de la organización. Al utilizar calendarios comerciales, los formularios de AEM omiten los días no laborables al realizar determinados cálculos de fecha. En Workbench, puede especificar si desea utilizar calendarios comerciales para eventos asociados al usuario, como recordatorios de tareas, plazos y escalaciones, o para acciones no asociadas con usuarios, como Eventos de temporizador y Servicio de espera.

Por ejemplo, se configura un recordatorio de tareas para que se produzca tres días laborables después de que la tarea se asigne a un usuario. La tarea se asigna el jueves. Sin embargo, los siguientes tres días no son días laborables porque el viernes es feriado nacional y los siguientes dos días son días de fin de semana. Por lo tanto, el recordatorio se envía el miércoles de la semana siguiente.

>[!NOTE]
>
>Al calcular fechas y horas mediante calendarios comerciales, los formularios de AEM utilizan la fecha y la hora del servidor en el que se ejecutan y no se ajustan en función de la diferencia entre zonas horarias. Por ejemplo, si un recordatorio de tarea está programado para que se produzca a las 10:00 a.m. en un servidor que se ejecuta en Londres, pero el usuario que recibe el recordatorio está ubicado en Nueva York, el usuario recibirá el recordatorio a las 5:00 a.m., hora local.

## Uso del calendario comercial predeterminado {#using-the-default-business-calendar}

Los formularios AEM proporcionan un calendario comercial predeterminado (denominado calendario ** integrado) que designa los sábados y los domingos como días no laborables. Si todos los usuarios de su organización tienen los mismos días no laborables, puede actualizar el calendario comercial predeterminado para adaptarlo a su organización. Cuando se utiliza solamente el calendario comercial predeterminado, no es necesario habilitar los calendarios comerciales en Administración de usuarios ni proporcionar asignaciones. Cuando no se define ningún otro calendario empresarial, los formularios AEM utilizan el calendario comercial predeterminado.

## Configuración de varios calendarios comerciales {#setting-up-multiple-business-calendars}

Si algunos de los usuarios de su organización tienen diferentes días no laborables, puede definir varios calendarios comerciales y configurar asignaciones que permitan una resolución de tiempo de ejecución de un calendario comercial para un usuario.

### Definir varios calendarios comerciales {#define-multiple-business-calendars}

1. Decida cómo asociará el calendario comercial adecuado con un usuario. Existen dos maneras de asociar un calendario comercial con un usuario:

   **** Membresía del grupo: Puede asignar un calendario comercial a un usuario en función de su pertenencia a un grupo. En este caso, cada usuario del grupo utilizará el mismo calendario comercial.

   Si un usuario es miembro de dos grupos diferentes y dichos grupos están asignados a dos calendarios comerciales diferentes, los formularios de AEM utilizarán el primer calendario que encuentre en los resultados de búsqueda. En este caso, considere la posibilidad de utilizar claves de calendario empresarial para asociar usuarios con calendarios comerciales.

   **** Claves del calendario comercial: Puede asignar un calendario comercial a un usuario en función de una clave de calendario comercial, que es una configuración especificada en Administración de usuarios. A continuación, asigne la clave del calendario comercial a un calendario comercial en el flujo de trabajo de los formularios.

   La forma en que asigne claves de calendario empresarial a los usuarios dependerá de si utiliza un dominio empresarial, local o híbrido. Para obtener más información sobre la configuración de dominios, consulte [Adición de dominios](/help/forms/using/admin-help/adding-domains.md#adding-domains).

   Si utiliza un dominio local o híbrido, la información sobre los usuarios se almacena únicamente en la base de datos de Administración de usuarios. Para definir la clave del calendario comercial para estos usuarios, introduzca una cadena en el campo Clave del calendario comercial al agregar o editar un usuario en Administración de usuarios. (Consulte [Adición y configuración de usuarios](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users)). A continuación, asigne las claves de calendario empresarial (las cadenas) a los calendarios comerciales en el flujo de trabajo de los formularios. (Consulte [Asignación de usuarios y grupos a un calendario](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar)comercial).

   Si utiliza un dominio empresarial, la información sobre los usuarios reside en un sistema de almacenamiento de terceros, como un directorio LDAP, que la Administración de usuarios sincroniza con la base de datos de Administración de usuarios. Esto le permite asignar una clave de calendario comercial a un campo del directorio LDAP. Por ejemplo, si cada registro de usuario del directorio contiene un campo &quot;país&quot; y desea asignar calendarios comerciales en función del país en el que se encuentra el usuario, especifique el nombre de campo &quot;país&quot; en el campo Clave del calendario laboral al especificar la configuración de usuario del directorio. (Consulte [Configuración de directorios](/help/forms/using/admin-help/configuring-directories.md#configuring-directories)). A continuación, puede asignar las claves de calendario empresarial (los valores definidos para el campo &quot;país&quot; en el directorio LDAP) a los calendarios comerciales en el flujo de trabajo de formularios. (Consulte [Asignación de usuarios y grupos a un calendario](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar)comercial).

1. En el flujo de trabajo de formularios, defina un calendario para cada conjunto de usuarios que comparten los mismos días no laborables. (Consulte [Creación o actualización de un calendario](configuring-business-calendars.md#create-or-update-a-business-calendar)comercial).
1. En el flujo de trabajo de formularios, asigne las claves de calendario de trabajo o las pertenencias de grupo para cada calendario. (Consulte [Asignación de usuarios y grupos a un calendario](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar)comercial).
1. En Workbench, el desarrollador del proceso decide si desea utilizar calendarios comerciales para recordatorios, plazos y escalaciones. (Consulte la Ayuda [de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   Si el desarrollador del proceso decide utilizar calendarios comerciales, los formularios de AEM seleccionarán dinámicamente el calendario comercial adecuado en función de la configuración de Administración de usuarios y las asignaciones de calendario empresarial definidas en la Consola de administración, o bien, si no existen asignaciones, utilizarán el calendario predeterminado.

   Si el desarrollador del proceso no utiliza calendarios comerciales, el cálculo de la fecha del evento trata todos los días como un día hábil. Por ejemplo, una fecha límite de tarea se configura para que se produzca tres días después de que la tarea se asigne a un usuario. La tarea se asigna el jueves. La fecha límite de la tarea es el domingo, aunque sea un fin de semana.

## Crear o actualizar un calendario comercial {#create-or-update-a-business-calendar}

Si su organización contiene diferentes grupos de usuarios que tienen diferentes días no laborables, puede definir varios calendarios comerciales. También puede cambiar los calendarios existentes, incluido el calendario integrado predeterminado que se proporciona con los formularios AEM.

>[!NOTE]
>
>Si no crea un nuevo calendario comercial, se utilizará el calendario predeterminado.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Calendarios comerciales.
1. Para agregar un nuevo calendario comercial, haga clic en ![bus_cal_plus](assets/bus_cal_plus.png). El texto *Nuevo calendario* aparece en la lista desplegable. Seleccione el texto y escriba otro nombre para el calendario.

   Para editar un calendario comercial existente, selecciónelo en la lista desplegable.

1. En Días no laborables predeterminados, seleccione cualquier día no laborable semanal, como fines de semana.
1. [Opcional] Seleccione Usar horas laborables y especifique las horas de inicio y finalización de los días laborables.

   Si selecciona esta opción, un evento que se produce antes del intervalo de tiempo especificado se mueve al principio del intervalo de tiempo y un evento que se produce después del intervalo de tiempo se mueve a la hora de inicio del siguiente día hábil.

   Por ejemplo, considere una situación en la que se asigna una tarea a un usuario a las 2:00 de la mañana del martes y el recordatorio para esa tarea se establece en dos días hábiles. Sin horario laboral, el recordatorio se produciría a las 2:00 am del jueves. Si el horario laboral es de 8:00 a.m. a 5:00 p.m., el recordatorio se enviará a las 8:00 a.m. del jueves. Sin horario laboral, si se crea un evento de recordatorio a las 6:00 pm del martes, el recordatorio se producirá después del horario laboral del jueves. Con el horario de trabajo fijado a las 8:00 am a las 5:00 pm, el recordatorio ocurriría a las 8:00 am del viernes.

1. En el calendario de la izquierda, haga doble clic en cualquier otro día no laborable, como días festivos. No puede seleccionar días en el pasado. Los días no laborables que seleccione aparecerán en una lista a la derecha, con la fecha en una línea que aparecerá dos veces. Seleccione la fecha de la izquierda para escribir el nombre o la descripción del día no laborable.

   Para eliminar de la lista un día no laborable, haga clic en ![bus_cal_trash](assets/bus_cal_trash.png) al lado del día.

1. [Opcional] Si este calendario va a ser el calendario predeterminado, seleccione Calendario predeterminado. El calendario predeterminado se utiliza cuando no existe ninguna otra asignación de calendario para los eventos asociados al usuario o no se especifica ningún calendario comercial para el evento de temporizador o el servicio de espera. No se puede eliminar el calendario predeterminado.
1. Cuando haya terminado de definir los días no laborables, seleccione Calendario habilitado para activarlo y, a continuación, haga clic en Guardar.

   Si está actualizando un calendario existente, la nueva versión surte efecto inmediatamente y se utiliza para todos los cálculos del calendario comercial, incluso para las tareas que ya se están ejecutando.

   >[!NOTE]
   >
   >Si no habilita el calendario, se utilizará el calendario predeterminado.

## Asignación de usuarios y grupos a un calendario comercial {#mapping-users-and-groups-to-a-business-calendar}

Existen dos métodos que puede utilizar para asociar un calendario comercial con un usuario. Puede asignar calendarios comerciales a los usuarios en función de una clave de calendario comercial o del grupo de directorios al que pertenezca el usuario. La ficha Asignación se utiliza para especificar el método que utilizarán los formularios AEM, así como para asignar las claves y los grupos de calendario empresarial a los calendarios comerciales. Para obtener más información sobre la asociación de claves de calendario empresarial con usuarios, consulte [Configuración de varios calendarios](configuring-business-calendars.md#setting-up-multiple-business-calendars)comerciales.

### Asociación de calendarios comerciales con usuarios en función de las claves de calendario empresariales {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Calendarios de trabajo y, a continuación, haga clic en la ficha Asignación.
1. En la lista Uso del sistema, seleccione User Manager Business Calendar Key Resolution (Resolución de claves del calendario empresarial del administrador de usuarios).
1. Seleccione Mostrar la clave del calendario comercial del administrador de usuarios. Se muestra una lista que contiene un conjunto único de claves de calendario empresarial que se han definido en Administración de usuarios.

   Para dominios locales e híbridos, la lista muestra los valores introducidos en el campo Clave de calendario comercial en Administración de usuarios. En el caso de los dominios de empresa (LDAP), la lista muestra el conjunto único que se devuelve desde el campo LDAP (por ejemplo, &quot;país&quot;) configurado en la configuración del dominio LDAP.

   Si el administrador de administración de usuarios no ha definido ninguna clave de calendario comercial, la lista estará vacía.

1. Para cada elemento de la lista de claves del calendario empresarial de mensajería unificada, seleccione un calendario.
1. Haga clic en Guardar.

### Asociación de calendarios comerciales con usuarios y grupos en función de grupos de servicios de directorio {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Calendarios de trabajo y, a continuación, haga clic en la ficha Asignación.
1. En la lista Uso del sistema, seleccione Grupos definidos por el servidor de directorio.
1. En la ficha Asignación, seleccione Mostrar grupos de servicios de directorio. Se muestra una lista que contiene los grupos definidos en Administración de usuarios. (Consulte Configuración [del directorio](/help/forms/using/admin-help/configuring-directories.md#directory-settings)).

   >[!NOTE]
   >
   >En Workbench, si ha configurado un servicio de usuario para utilizar calendarios comerciales y el servicio está asignado a un grupo, los formularios de AEM utilizan las asignaciones de grupo especificadas aquí para resolver el calendario del grupo. Los formularios AEM siempre utilizan asignaciones de grupos para resolver el calendario de los grupos, incluso cuando se utilizan claves de calendario empresarial para resolver el calendario de los usuarios. Si no se encuentra ninguna asignación de grupos, se utilizará el calendario comercial predeterminado.

1. Para cada elemento de la lista Grupo de servicios de directorio, seleccione un Calendario.
1. Haga clic en Guardar.

## Exportación e importación de calendarios comerciales {#exporting-and-importing-business-calendars}

Los formularios AEM le permiten exportar e importar sus calendarios comerciales como archivos XML. Puede utilizar esta función para mover calendarios de un sistema de ensayo a un sistema de producción.

>[!NOTE]
>
>Esta función exporta e importa todos los calendarios comerciales definidos, incluido el calendario empresarial predeterminado que proporcionan los formularios AEM. Un calendario comercial importado con el mismo nombre que un calendario existente sobrescribirá el calendario existente.

### Exportar calendarios comerciales {#export-business-calendars}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Calendarios comerciales.
1. Haga clic en Exportar y guarde el archivo XML.

### Importar calendarios comerciales {#import-business-calendars}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Calendarios comerciales.
1. Haga clic en Importar.
1. Seleccione el archivo XML que contiene los calendarios comerciales exportados y haga clic en Abrir.

## Eliminar un calendario comercial {#delete-a-business-calendar}

Puede eliminar los calendarios comerciales que su organización ya no necesite. Si elimina un calendario comercial que aún está asignado a usuarios y grupos, se utilizará el calendario predeterminado.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Calendarios comerciales.
1. Seleccione el calendario.
1. Haga clic en Eliminar.

