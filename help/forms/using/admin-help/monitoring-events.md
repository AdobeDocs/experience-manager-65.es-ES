---
title: eventos de supervisión
seo-title: eventos de supervisión
description: Cuando la capacidad de auditoría está habilitada, la seguridad de documento le permite supervisar determinados tipos de eventos. Puede buscar y ordenar fácilmente la lista de eventos mediante la seguridad de documento.
seo-description: Cuando la capacidad de auditoría está habilitada, la seguridad de documento le permite supervisar determinados tipos de eventos. Puede buscar y ordenar fácilmente la lista de eventos mediante la seguridad de documento.
uuid: 22add6ff-536d-4cb9-8eac-b72cad5c3ecf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 379957bf-0634-4182-b269-1b010da4c90f
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# eventos de supervisión {#monitoring-events}

Cuando la capacidad de auditoría está habilitada, la seguridad de documento le permite supervisar determinados tipos de eventos. Los eventos que puede ver dependen de su función:

**Usuarios:** Puede vista de eventos auditados para sus documentos protegidos por políticas y para cualquier documentos protegido que reciban y utilicen.

**Coordinadores de conjuntos de políticas:** Puede vista de eventos auditados, incluidos eventos de documentos y políticas, para documentos protegidos por políticas de sus conjuntos de políticas.

**Administradores:** Puede vista de eventos auditados que estén relacionados con todos los documentos y usuarios protegidos por políticas. Los administradores también pueden realizar el seguimiento de otros tipos de eventos, incluidos los eventos de usuario, documento, política y sistema.

>[!NOTE]
>
>Los Eventos que se realizan en una copia de un documento protegido por una política también se rastrean como eventos en el documento protegido original.

(Consulte Opciones [de auditoría de](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options)Evento).

Se registra un evento fallido si un usuario no autorizado intenta realizar la vista de un documento o intenta iniciar sesión con un nombre de usuario o una contraseña incorrectos.

>[!NOTE]
>
>Se pueden registrar eventos de acceso anónimos fallidos para documentos si se edita una directiva para eliminar el acceso anónimo. Cuando un destinatario autorizado intenta acceder a un documento que protege la política editada, se sigue intentando acceder de forma anónima, pero se producirá un error.

Si una política permite el acceso de usuarios anónimos pero el administrador desactiva posteriormente el acceso anónimo para la seguridad de documento, el acceso anónimo fallará para los documentos protegidos con la política y el evento no se registrará.

## Habilitar auditoría de evento {#enable-event-auditing}

Estos requisitos de configuración deben cumplirse para que la auditoría de evento tenga lugar:

* El sistema o el administrador deben habilitar la capacidad de auditoría para el servidor.

   (Consulte [Configuración de auditoría de evento y configuración](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings)de privacidad).

* La directiva que utilice para proteger el documento debe tener habilitada la auditoría. (Consulte [Creación y edición de políticas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies)).

## Buscar un evento {#search-for-an-event}

Puede buscar en la lista de eventos y en la vista descripciones más detalladas sobre eventos. Las descripciones detalladas incluyen información como el ID de evento, la descripción, la dirección IP, la organización, la fecha y hora en que se produjo el evento, las actividades denegadas y los eventos sin conexión (cuando los usuarios intentan utilizar un documento cuando no están conectados a la seguridad de documento).

Puede buscar eventos en la página Eventos mediante una combinación de criterios de búsqueda de eventos y las fechas en que se produjeron los eventos. Los eventos que puede buscar dependen de su función:

**Usuarios:** Puede vista de eventos auditados para sus documentos protegidos por políticas y para cualquier documentos protegido que reciban y utilicen. Estas opciones de búsqueda están disponibles:

**Eventos relacionados conmigo:** Los usuarios pueden encontrar eventos para cualquier documento protegido por una política que hayan creado o recibido. Por ejemplo, si un usuario abre, vista o imprime un documento protegido por otra persona, solo verá estos eventos para ese documento.

**Eventos relacionados con mis documentos:** Los usuarios pueden encontrar todos los eventos relacionados con sus propios documentos protegidos por políticas. Los usuarios ven los eventos generados por cada persona que gestionó sus documentos.

**Coordinadores de conjuntos de políticas:** Puede vista de eventos auditados, incluidos eventos de documentos y políticas, para documentos protegidos por políticas de sus conjuntos de políticas. Las opciones disponibles son:

**eventos de Documento en los que soy un coordinador de conjunto de políticas:** Los coordinadores de conjuntos de políticas que tienen el permiso de evento de vista pueden encontrar eventos relacionados con documentos que protegen las políticas de sus conjuntos de políticas.

**eventos de política en los que soy coordinador de conjunto de políticas:** Los coordinadores de conjuntos de políticas que tienen el permiso eventos de vista pueden encontrar eventos relacionados con las políticas en sus conjuntos de políticas.

**Administradores:** Puede vista de eventos auditados que estén relacionados con todos los documentos y usuarios protegidos por políticas. Los administradores también pueden realizar el seguimiento de otros tipos. Además, los administradores pueden subdividir las búsquedas de evento según el tipo de usuario:

**Usuarios conocidos:** Los usuarios se encuentran en los directorios de origen o están registrados como usuarios externos.

**Usuarios anónimos:** Usuarios desconocidos que acceden a un documento protegido con una política que permite el acceso anónimo.

**Usuarios del sistema:** eventos iniciados por el servidor, como una sincronización de directorios.

1. En la página de seguridad de documento, haga clic en Eventos.
1. En la lista Buscar, seleccione los criterios de búsqueda que desee utilizar. Según la selección realizada en la lista Buscar, se muestra una segunda lista que proporciona criterios de búsqueda adicionales. Si corresponde, en el cuadro de texto, escriba los criterios de búsqueda.

   Para obtener más información sobre los tipos de evento específicos, consulte Opciones [de auditoría de](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options)Eventos.

1. En la lista Usuario, seleccione el tipo de usuario que realizó el evento:

   * Si selecciona Usuario conocido, se muestra un segundo cuadro de búsqueda, donde debe escribir el nombre de usuario o la dirección de correo electrónico del usuario.
   * Si no conoce estos valores, haga clic en el icono de búsqueda Libreta de direcciones para buscar al usuario por el nombre de usuario o la dirección de correo electrónico.

1. En la lista de fecha, seleccione una opción de intervalo de fechas. Si selecciona Fechas personalizadas, aparecerán cuadros en los que escriba la fecha con el formato aaaa/mm/dd, o puede utilizar el Selector de fecha para especificar el intervalo de fechas:

   * Haga clic en el calendario para abrir el Selector de fecha.
   * Utilice las flechas para buscar un año y un mes.
   * Haga clic en un día del mes en el calendario.
   * Haga clic en Aceptar para cerrar el Selector de fecha.

1. En la lista Mostrar, seleccione el número de resultados de búsqueda que se mostrarán por página.
1. Haga clic en Buscar.

   Los eventos fallidos se resaltan en la lista con un icono denegado.

1. Para vista de detalles sobre un evento, haga clic en la descripción del evento en la lista.

## Ordenar la lista de evento {#sort-the-event-list}

Puede ordenar la lista de eventos por encabezado de columna para encontrar eventos más fácilmente. Los iconos de triángulo junto al encabezado de la columna indican qué columna se utiliza actualmente para ordenar. Un triángulo que apunta hacia arriba indica el orden ascendente, mientras que un triángulo que apunta hacia abajo indica el orden descendente.

1. Haga clic en el encabezado de columna correspondiente.
1. Para cambiar el orden, vuelva a hacer clic en el encabezado de la columna.

