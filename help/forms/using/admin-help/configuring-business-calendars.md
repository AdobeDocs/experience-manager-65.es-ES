---
title: Configuración de calendarios comerciales
seo-title: Configuring Business Calendars
description: Los calendarios comerciales definen los días laborables y no laborables de su organización. Obtenga información sobre cómo configurar los calendarios empresariales.
seo-description: Business calendars define business and non-business days for your organization. Learn how to configure the business calendars.
uuid: 0ba610b8-72a8-480c-8783-70d98cbe890a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7a85e13d-4800-47c4-812a-5c6e2355298a
exl-id: 4282718a-41f1-411a-9cd7-8c470005107d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---

# Configuración de calendarios comerciales {#configuring-business-calendars}

*Calendarios empresariales* defina los días laborables y no laborables (por ejemplo, días festivos legales, fines de semana y días de cierre de la empresa) para su organización. Al utilizar calendarios empresariales, AEM formularios omite los días no laborables al realizar determinados cálculos de fechas. En Workbench, puede especificar si desea usar calendarios empresariales para eventos asociados al usuario, como recordatorios de tareas, plazos y escalaciones, o para acciones que no están asociadas con usuarios, como Eventos de temporizador y el servicio de espera.

Por ejemplo, se ha configurado un recordatorio de tareas para que se produzca tres días hábiles después de que la tarea se asigne a un usuario. La tarea se asigna el jueves. Sin embargo, los siguientes tres días no son días laborables porque el viernes es feriado nacional y los siguientes dos días son días de fin de semana. Por lo tanto, el recordatorio se envía el miércoles de la semana siguiente.

>[!NOTE]
>
>Al calcular fechas y horas utilizando calendarios empresariales, AEM formularios utiliza la fecha y la hora del servidor en el que se está ejecutando y no se ajusta para la diferencia entre zonas horarias. Por ejemplo, si está programado que se produzca un recordatorio de tarea a las 10:00 en un servidor que se ejecuta en Londres, pero el usuario que recibe el recordatorio está ubicado en Nueva York, el usuario recibirá el recordatorio a las 5:00 a.m., hora local.

## Uso del calendario empresarial predeterminado {#using-the-default-business-calendar}

AEM formularios proporciona un calendario empresarial predeterminado (con el nombre *Calendario integrado*) que designa los sábados y domingos como días no laborables. Si todos los usuarios de su organización tienen los mismos días no laborables, puede actualizar el calendario empresarial predeterminado para adaptarlo a su organización. Cuando utilice únicamente el calendario empresarial predeterminado, no es necesario habilitar los calendarios empresariales en Administración de usuarios ni proporcionar ninguna asignación. Cuando no se definen otros calendarios comerciales, AEM formularios utilizan el calendario empresarial predeterminado.

## Configuración de varios calendarios empresariales {#setting-up-multiple-business-calendars}

Si algunos de los usuarios de la organización tienen diferentes días no laborables, puede definir varios calendarios empresariales y configurar asignaciones que permitan una resolución de tiempo de ejecución de un calendario empresarial para un usuario.

### Definir varios calendarios empresariales {#define-multiple-business-calendars}

1. Decida cómo va a asociar el calendario empresarial apropiado con un usuario. Existen dos maneras de asociar un calendario empresarial con un usuario:

   **Pertenencia al grupo:** Puede asignar un calendario empresarial a un usuario en función de su pertenencia a un grupo. En este caso, cada usuario del grupo utilizará el mismo calendario comercial.

   Si un usuario es miembro de dos grupos diferentes y esos grupos están asignados a dos calendarios empresariales diferentes, AEM formularios utilizarán el primer calendario que encuentre en sus resultados de búsqueda. En este caso, considere la posibilidad de utilizar claves de calendario empresarial para asociar usuarios con calendarios empresariales.

   **Claves del calendario empresarial:** Puede asignar un calendario empresarial a un usuario en función de una clave de calendario empresarial, que es una configuración especificada en Administración de usuarios. A continuación, asigne la clave de calendario empresarial a un calendario empresarial en el flujo de trabajo de los formularios.

   La forma en que asigne claves de calendario empresarial a los usuarios dependerá de si utiliza un dominio empresarial, local o híbrido. Para obtener más información sobre la configuración de dominios, consulte [Adición de dominios](/help/forms/using/admin-help/adding-domains.md#adding-domains).

   Si utiliza un dominio local o híbrido, la información sobre los usuarios solo se almacena en la base de datos de Administración de usuarios. Para definir la clave del calendario empresarial para estos usuarios, introduzca una cadena en el campo Clave del calendario empresarial al agregar o editar un usuario en Administración de usuarios. (Consulte [Adición y configuración de usuarios](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users).) A continuación, asigne las claves del calendario empresarial (las cadenas) a los calendarios empresariales en el flujo de trabajo de los formularios. (Consulte [Asignación de usuarios y grupos a un calendario empresarial](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

   Si utiliza un dominio empresarial, la información sobre los usuarios reside en un sistema de almacenamiento de terceros, como un directorio LDAP, que la Administración de usuarios sincroniza con la base de datos de Administración de usuarios. Esto le permite asignar una clave de calendario empresarial a un campo del directorio LDAP. Por ejemplo, si cada registro de usuario del directorio contiene un campo &quot;país&quot; y desea asignar calendarios empresariales en función del país donde se encuentre el usuario, especifique el nombre del campo &quot;país&quot; en el campo Clave del calendario empresarial al especificar la configuración de usuario del directorio. (Consulte [Configuración de directorios](/help/forms/using/admin-help/configuring-directories.md#configuring-directories).) A continuación, puede asignar las claves del calendario empresarial (los valores definidos para el campo &quot;country&quot; en el directorio LDAP) a los calendarios comerciales en el flujo de trabajo de formularios. (Consulte [Asignación de usuarios y grupos a un calendario empresarial](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

1. En el flujo de trabajo de formularios, defina un calendario para cada conjunto de usuarios que compartan los mismos días no laborables. (Consulte [Crear o actualizar un calendario empresarial](configuring-business-calendars.md#create-or-update-a-business-calendar).)
1. En el flujo de trabajo de formularios, asigne las claves del calendario empresarial o las suscripciones a grupos para cada calendario. (Consulte [Asignación de usuarios y grupos a un calendario empresarial](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)
1. En Workbench, el desarrollador del proceso elige si usar calendarios empresariales para recordatorios, plazos y escalaciones. (Consulte [Ayuda de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   Si el desarrollador del proceso decide utilizar calendarios empresariales, AEM formularios seleccionarán dinámicamente el calendario empresarial adecuado en función de la configuración de Administración de usuarios y las asignaciones de calendario empresarial definidas en la Consola de administración o, si no existen asignaciones, utilizará el calendario predeterminado.

   Si el desarrollador del proceso no utiliza calendarios empresariales, el cálculo de fechas del evento trata cada día como un día laborable. Por ejemplo, se configura una fecha límite de una tarea para que se produzca tres días después de que la tarea se asigne a un usuario. La tarea se asigna el jueves. La fecha límite de la tarea es domingo, aunque sea un fin de semana.

## Crear o actualizar un calendario empresarial {#create-or-update-a-business-calendar}

Si su organización contiene diferentes conjuntos de usuarios que tienen diferentes días no laborables, puede definir varios calendarios comerciales. También puede cambiar los calendarios existentes, incluido el calendario integrado predeterminado que se proporciona con AEM formularios.

>[!NOTE]
>
>Si no crea un nuevo calendario comercial, se utilizará el calendario predeterminado.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Calendarios empresariales.
1. Para agregar un nuevo calendario comercial, haga clic en ![bus_cal_plus](assets/bus_cal_plus.png). El texto *Nuevo calendario* aparece en la lista desplegable. Seleccione el texto y escriba otro nombre para el calendario.

   Para editar un calendario empresarial existente, selecciónelo en la lista desplegable.

1. En Días no laborables predeterminados, seleccione cualquier día semanal que no sea laboral, como los fines de semana.
1. [Opcional] Seleccione Usar horas laborables y especifique las horas de inicio y finalización de los días laborables.

   Si selecciona esta opción, un evento que se produzca antes del intervalo de tiempo especificado se moverá al principio del intervalo de tiempo y un evento que se produzca después del intervalo de tiempo se moverá a la hora de inicio del siguiente día laborable.

   Por ejemplo, imaginemos una situación en la que a un usuario se le asigna una tarea a las 2 de la mañana de un martes y el recordatorio para esa tarea se establece en dos días hábiles. Sin horario laboral, el recordatorio se produciría a las 2:00 am del jueves. Si el horario laboral es de 8:00 a.m. a 5:00 p.m., el recordatorio se pospondrá hasta las 8:00 a.m. del jueves. Sin horario laboral, si se creó un evento de recordatorio a las 6:00 pm del martes, el recordatorio se produciría después del horario laboral del jueves. Con el horario laboral fijado en 8:00 am a 5:00 pm, el recordatorio se produciría a las 8:00 am del viernes.

1. En el calendario de la izquierda, haga doble clic en cualquier otro día no laborable, como días festivos. No puede seleccionar días en el pasado. Los días no laborables que seleccione aparecerán en una lista de la derecha, con la fecha que aparecerá dos veces en una línea. Seleccione la fecha de la izquierda para escribir el nombre o la descripción del día no laborable.

   Para eliminar de la lista un día no laborable, haga clic en ![bus_cal_trash](assets/bus_cal_trash.png) al lado del día.

1. [Opcional] Si este calendario debe ser el calendario predeterminado, seleccione Calendario predeterminado. El calendario predeterminado se utiliza cuando no existe ninguna otra asignación de calendario para los eventos asociados al usuario o no se especifica ningún calendario empresarial para el Evento de temporizador o el Servicio de espera. No se puede eliminar el calendario predeterminado.
1. Cuando haya terminado de definir los días que no son laborables, seleccione Calendario habilitado para activarlo y, a continuación, haga clic en Guardar.

   Si está actualizando un calendario existente, la nueva versión surte efecto inmediatamente y se utiliza para todos los cálculos del calendario empresarial, incluidas las tareas que ya se estén ejecutando.

   >[!NOTE]
   >
   >Si no habilita el calendario, se utilizará el calendario predeterminado.

## Asignación de usuarios y grupos a un calendario empresarial {#mapping-users-and-groups-to-a-business-calendar}

Existen dos métodos que puede utilizar para asociar un calendario empresarial a un usuario. Puede asignar calendarios empresariales a los usuarios en función de una clave de calendario empresarial o del grupo de directorios al que pertenezca el usuario. La ficha Asignación se utiliza para especificar el método que AEM los formularios utilizarán y también para asignar las claves y los grupos de calendario empresarial a los calendarios de empresa. Para obtener más información sobre cómo asociar claves de calendario empresarial con usuarios, consulte [Configuración de varios calendarios empresariales](configuring-business-calendars.md#setting-up-multiple-business-calendars).

### Asociar calendarios empresariales con usuarios en función de claves de calendario empresariales {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Calendarios empresariales y, a continuación, haga clic en la ficha Asignación.
1. En la lista System Will Use (El sistema usará), seleccione User Manager Business Calendar Key Resolution (Resolución de claves del calendario de negocios del administrador de usuarios).
1. Seleccione Mostrar clave del calendario comercial de User Manager. Se muestra una lista que contiene un conjunto único de claves de calendario empresarial que se han definido en Administración de usuarios.

   Para dominios locales e híbridos, la lista muestra los valores introducidos en el campo Clave de calendario empresarial en Administración de usuarios . Para los dominios empresariales (LDAP), la lista muestra el conjunto único que se devuelve desde el campo LDAP (por ejemplo, &quot;country&quot;) configurado en la configuración del dominio LDAP.

   Si el administrador de administración de usuarios no ha definido ninguna clave de calendario empresarial, la lista estará vacía.

1. Para cada elemento de la lista Clave del calendario empresarial de mensajería unificada, seleccione un calendario.
1. Haga clic en Guardar.

### Asociar calendarios empresariales con usuarios y grupos basados en grupos de servicios de directorios {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Calendarios empresariales y, a continuación, haga clic en la ficha Asignación.
1. En la lista Usar sistema, seleccione Grupos Definidos por el Servidor de Directorios.
1. En la ficha Asignación, seleccione Mostrar grupos de servicio de directorio. Se muestra una lista que contiene los grupos definidos en Administración de usuarios. (Consulte [Configuración de directorio](/help/forms/using/admin-help/configuring-directories.md#directory-settings).)

   >[!NOTE]
   >
   >En Workbench, si ha configurado un servicio de usuario para utilizar calendarios empresariales y el servicio está asignado a un grupo, AEM formularios utiliza las asignaciones de grupo especificadas aquí para resolver el calendario del grupo. AEM formularios siempre utiliza asignaciones de grupos para resolver el calendario de los grupos, incluso cuando utiliza claves de calendario empresarial para resolver el calendario de los usuarios. Si no se encuentra ninguna asignación de grupos, se utilizará el calendario empresarial predeterminado.

1. Para cada elemento de la lista Grupo de Servicios de Directorio, seleccione un Calendario.
1. Haga clic en Guardar.

## Exportación e importación de calendarios comerciales {#exporting-and-importing-business-calendars}

AEM formularios le permite exportar e importar sus calendarios empresariales como archivos XML. Puede utilizar esta función para mover calendarios de un sistema de ensayo a un sistema de producción.

>[!NOTE]
>
>Esta función exporta e importa todos los calendarios empresariales definidos, incluido el calendario empresarial predeterminado proporcionado por AEM formularios. Un calendario comercial importado con el mismo nombre que un calendario existente sobrescribirá el calendario existente.

### Exportar calendarios empresariales {#export-business-calendars}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Calendarios empresariales.
1. Haga clic en Exportar y guarde el archivo XML.

### Importar calendarios empresariales {#import-business-calendars}

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de formularios > Calendarios empresariales.
1. Haga clic en Importar.
1. Seleccione el archivo XML que contiene los calendarios empresariales exportados y haga clic en Abrir.

## Eliminar un calendario empresarial {#delete-a-business-calendar}

Puede eliminar cualquier calendario empresarial que su organización ya no necesite. Si elimina un calendario empresarial que aún esté asignado a usuarios y grupos, se utilizará el calendario predeterminado.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Calendarios empresariales.
1. Seleccione el calendario.
1. Haga clic en Eliminar.
