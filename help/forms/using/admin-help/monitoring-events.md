---
title: Supervisión de eventos
seo-title: Supervisión de eventos
description: Cuando la capacidad de auditoría está habilitada, la seguridad de los documentos permite supervisar ciertos tipos de eventos. Puede buscar y ordenar fácilmente la lista de eventos mediante la seguridad del documento.
seo-description: Cuando la capacidad de auditoría está habilitada, la seguridad de los documentos permite supervisar ciertos tipos de eventos. Puede buscar y ordenar fácilmente la lista de eventos mediante la seguridad del documento.
uuid: 22add6ff-536d-4cb9-8eac-b72cad5c3ecf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 379957bf-0634-4182-b269-1b010da4c90f
feature: Seguridad de los documentos
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---


# Monitorización de eventos {#monitoring-events}

Cuando la capacidad de auditoría está habilitada, la seguridad de los documentos permite supervisar ciertos tipos de eventos. Los eventos que puede ver dependen de su función:

**Usuarios:** pueden ver eventos auditados para sus documentos protegidos por políticas y para cualquier documento protegido que reciban y utilicen.

**Coordinadores de conjuntos de políticas:** pueden ver eventos auditados, incluidos eventos de documentos y políticas, para documentos protegidos por políticas de sus conjuntos de políticas.

**Administradores:** pueden ver eventos auditados relacionados con todos los documentos y usuarios protegidos por políticas. Los administradores también pueden rastrear otros tipos de eventos, como eventos de usuario, documento, directiva y sistema.

>[!NOTE]
>
>Los eventos que se realizan en una copia de un documento protegido por políticas también se rastrean como eventos en el documento protegido original.

(Consulte [Opciones de auditoría de eventos](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options)).

Se registra un evento fallido si un usuario no autorizado intenta ver un documento o intenta iniciar sesión con un nombre de usuario o contraseña incorrectos.

>[!NOTE]
>
>Los eventos de acceso anónimos fallidos para los documentos se pueden registrar si se edita una directiva para eliminar el acceso anónimo. Cuando un destinatario autorizado intenta acceder a un documento que protege la directiva editada, se sigue intentando acceder de forma anónima, pero el acceso fallará.

Si una directiva permite el acceso de usuarios anónimos, pero el administrador desactiva posteriormente el acceso anónimo para la seguridad de documentos, el acceso anónimo fallará en los documentos protegidos con la directiva y el evento no se registrará.

## Habilitar la auditoría de eventos {#enable-event-auditing}

Estos requisitos de configuración deben cumplirse para que se realice la auditoría de eventos:

* El sistema o el administrador deben habilitar la capacidad de auditoría para el servidor.

   (Consulte [Configuración de auditoría de eventos y configuración de privacidad](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings)).

* La directiva que utilice para proteger el documento debe tener habilitada la auditoría. (Consulte [Creación y edición de directivas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies)).

## Buscar un evento {#search-for-an-event}

Puede buscar en la lista de eventos y ver descripciones más detalladas sobre los eventos. Las descripciones detalladas incluyen información como el ID del evento, la descripción, la dirección IP, la organización, la fecha y la hora en que se produjo el evento, las actividades denegadas y los eventos sin conexión (cuando los usuarios intentan utilizar un documento cuando no están conectados a la seguridad del documento).

Puede buscar eventos en la página Eventos mediante una combinación de criterios de búsqueda de eventos y fechas en las que se produjeron los eventos. Los eventos que puede buscar dependen de su función:

**Usuarios:** pueden ver eventos auditados para sus documentos protegidos por políticas y para cualquier documento protegido que reciban y utilicen. Estas opciones de búsqueda están disponibles:

**Eventos relacionados conmigo:** los usuarios pueden encontrar eventos para cualquier documento protegido por políticas que hayan creado o recibido. Por ejemplo, si un usuario abre, visualiza o imprime un documento protegido por otra persona, solo verá estos eventos para ese documento.

**Eventos relacionados con mis documentos:**  los usuarios pueden encontrar todos los eventos relacionados con sus propios documentos protegidos por políticas. Los usuarios ven los eventos generados por cada persona que manejó sus documentos.

**Coordinadores de conjuntos de políticas:** pueden ver eventos auditados, incluidos eventos de documentos y políticas, para documentos protegidos por políticas de sus conjuntos de políticas. Las opciones disponibles son:

**Documentar eventos donde soy un coordinador de conjuntos de políticas:**  los coordinadores de conjuntos de políticas que tienen el permiso de eventos de visualización pueden encontrar eventos relacionados con documentos que protegen las políticas de sus conjuntos de políticas.

**Eventos de política donde soy coordinador de conjuntos de políticas:**  Los coordinadores de conjuntos de políticas que tienen permiso para ver eventos pueden encontrar eventos relacionados con políticas desde sus conjuntos de políticas.

**Administradores:** pueden ver eventos auditados relacionados con todos los documentos y usuarios protegidos por políticas. Los administradores también pueden realizar el seguimiento de otros tipos. Además, los administradores pueden subdividir las búsquedas de eventos según el tipo de usuario:

**Usuarios conocidos:** Los usuarios se encuentran en los directorios de origen o están registrados como usuarios externos.

**Usuarios anónimos:** usuarios desconocidos que acceden a un documento protegido con una política que permita el acceso anónimo.

**Usuarios del sistema:** Eventos iniciados por el servidor, como la sincronización de directorios.

1. En la página de seguridad del documento, haga clic en Eventos.
1. En la lista Buscar, seleccione los criterios de búsqueda que desee utilizar. Según su selección en la lista Buscar, se muestra una segunda lista que proporciona criterios de búsqueda adicionales. Si corresponde, en el cuadro de texto, escriba los criterios de búsqueda.

   Para obtener más información sobre los tipos de eventos específicos, consulte [Opciones de auditoría de eventos](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).

1. En la lista Usuario, seleccione el tipo de usuario que realizó el evento:

   * Si selecciona Usuario conocido, se muestra un segundo cuadro de búsqueda, donde debe escribir el nombre de usuario o la dirección de correo electrónico del usuario.
   * Si no conoce estos valores, haga clic en el icono de búsqueda Libreta de direcciones para buscar al usuario por el nombre de usuario o la dirección de correo electrónico.

1. En la lista Fecha, seleccione una opción de intervalo de fechas. Si selecciona Fechas personalizadas, aparecerán cuadros en los que escribirá la fecha con el formato aaaa/mm/dd, o puede utilizar el Selector de fechas para especificar el intervalo de fechas:

   * Haga clic en el calendario para abrir el selector de fechas.
   * Utilice las flechas para encontrar un año y un mes.
   * Haga clic en un día del mes en el calendario.
   * Haga clic en Aceptar para cerrar el selector de fechas.

1. En la lista Mostrar, seleccione el número de resultados de búsqueda que se mostrarán por página.
1. Haga clic en Buscar.

   Los eventos fallidos se resaltan en la lista con un icono denegado.

1. Para ver los detalles de un evento, haga clic en la descripción del evento en la lista.

## Ordenar la lista de eventos {#sort-the-event-list}

Puede ordenar la lista de eventos por encabezado de columna para encontrar los eventos más fácilmente. Los iconos de triángulo junto al encabezado de la columna indican qué columna se utiliza actualmente para ordenar. Un triángulo que señala hacia arriba indica el orden ascendente, mientras que un triángulo que señala hacia abajo indica el orden descendente.

1. Haga clic en el encabezado de columna correspondiente.
1. Para cambiar el orden, vuelva a hacer clic en el encabezado de la columna.

