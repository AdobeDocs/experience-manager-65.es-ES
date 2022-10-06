---
title: Sincronización de directorios
seo-title: Synchronizing directories
description: Obtenga información sobre cómo sincronizar la base de datos de Administración de usuarios con los cambios realizados en los servidores de directorios de origen mediante la sincronización manual o programada.
seo-description: Learn how to synchronize the User Management database with changes to the source directory servers using manual or scheduled synchronization.
uuid: 71cbc04d-6172-49b7-a490-ff3233c1b2bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7ec0698a-9e6e-48d4-bba2-5a6eee313900
exl-id: cb642289-4137-4ba7-8bde-0e458c8c94fe
source-git-commit: 2a2f8538b6554540b546f4d345c0b3c0d3e706f3
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# Sincronización de directorios {#synchronizing-directories}

Para sincronizar dominios, puede elegir realizar una sincronización manual o programada. A *sincronización manual* sincroniza los dominios seleccionados. A *sincronización programada* sincroniza todos los dominios.

La sincronización de directorios se utiliza para extraer detalles de los servidores de directorios que especificó en la configuración de directorios a la base de datos de Administración de usuarios. Posteriormente, también puede realizar una sincronización manual si se producen cambios o actualizaciones en los servidores de directorios. Por ejemplo, puede realizar una sincronización manual si se agregan usuarios y grupos o si se realizan cambios en la cuenta de un usuario.

También puede establecer una programación de sincronización diaria para sincronizar automáticamente la base de datos de Administración de usuarios con cambios o actualizaciones en los servidores de directorios de origen. Sin embargo, tenga en cuenta que este proceso utiliza recursos de red y de servidor. Elija períodos de tiempo de bajo uso y evite programar sincronizaciones innecesarias que vinculen los recursos del sistema y de la red. Para minimizar las sincronizaciones innecesarias, utilice la opción de sincronización inmediata en su lugar.

También puede especificar si desea insertar información de usuarios y grupos en Adobe LiveCycle Content Services 9 (obsoleto) al sincronizar dominios.

>[!NOTE]
>
>No cree varios usuarios y grupos locales mientras haya una sincronización de directorios LDAP en curso. Si se intenta este proceso, pueden producirse errores.

>[!NOTE]
>
>Si se interrumpe el proceso de sincronización de dominios (por ejemplo, el servidor de aplicaciones se apaga durante el proceso), espere un tiempo antes de intentar sincronizar el dominio. Para evaluar el estado de la sincronización, consulte el estado . Si la Administración de usuarios adquirió un bloqueo antes del cierre, espere 10 minutos para que el bloqueo se libere después del reinicio del servidor. Si el estado de sincronización es &quot;En curso&quot; pero la sincronización se interrumpe o se detiene, la Administración de usuarios reintenta la sincronización después de 3 minutos. Después de tres intentos fallidos, la Administración de usuarios declara que la sincronización es un error y libera el bloqueo.

>[!NOTE]
>
>Adobe® Content Services ES (obsoleto) es un sistema de administración de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, monitorear y optimizar procesos centrados en el ser humano. La compatibilidad con los servicios de contenido (obsoletos) finaliza el 31/12/2014. Consulte [Documento de ciclo de vida del producto de Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

## Habilitar la sincronización de directorios delta {#enable-delta-directory-synchronization}

La sincronización de directorios Delta mejora la eficacia de la sincronización de directorios. Cuando la sincronización de directorios delta está habilitada, Administración de usuarios sincroniza solo los usuarios y grupos que se han agregado o actualizado desde la última sincronización.

La Administración de usuarios realiza los siguientes pasos cuando la sincronización de directorios delta está habilitada:

* Recupere todos los usuarios de los servidores de directorios, pero actualice la base de datos de Administración de usuarios solo con los usuarios cuya marca de tiempo haya cambiado.
* Recupere todos los grupos, pero actualice la base de datos de Administración de usuarios solo con los grupos cuya marca de tiempo haya cambiado.
* Recupere miembros del grupo solo para los grupos cuyas marcas de tiempo han cambiado y actualice la base de datos de Administración de usuarios con esa información.

>[!NOTE]
>
>Los usuarios y grupos que se eliminaron del directorio no se eliminarán de la base de datos de Administración de usuarios hasta que realice una sincronización de directorios completa.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. En Sintaxis delta, seleccione la casilla de verificación y haga clic en Guardar.
1. Edite la configuración de directorio de cada uno de los dominios de empresa que utilizarán la función de sincronización de directorios delta. En las páginas Configuración de usuario y Configuración de grupo , busque el ajuste Modificar marca de tiempo e introduzca `modify TimeStamp` como valor. Para obtener más información sobre la edición de dominios empresariales, consulte [Edición y conversión de dominios existentes](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## Habilitar o deshabilitar el registro detallado durante la sincronización {#enable-or-disable-detailed-logging-during-synchronization}

De forma predeterminada, Administración de usuarios registra estadísticas detalladas durante el proceso de sincronización.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configurar atributos avanzados del sistema.
1. En Registro de estadísticas de sincronización, anule la selección de la casilla de verificación para desactivar el registro detallado o selecciónelo para habilitar el registro y, a continuación, haga clic en Guardar.

## Configuración de la opción de reintento de sincronización de directorios {#configure-the-directory-synchronization-retry-option}

Puede configurar la Administración de usuarios para que compruebe periódicamente si hay algún intento fallido de sincronización de directorios. A continuación, Administración de usuarios intenta completar las sincronizaciones fallidas.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configurar atributos avanzados del sistema.
1. En Synch Finisher Cron Expression, introduzca una expresión cron que represente el intervalo en el que User Management reintenta las sincronizaciones fallidas. El uso de la expresión cron se basa en el sistema de programación de trabajos de código abierto de Quartz, versión 1.4.0.

   El valor predeterminado es 0 0/13 &amp;ast; ? &amp;ast; , lo que significa que la comprobación se realiza cada 13 minutos.

## Sincronizar directorios manualmente {#manually-synchronize-directories}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. (Opcional) Para insertar información de usuarios y grupos en los servicios de contenido (obsoleto), seleccione la opción Seleccionar esta opción para insertar usuarios y grupos en proveedores de almacenamiento principales externos registrados . Esta opción también se aplica cuando se agregan nuevos usuarios y grupos a través de la página Usuarios y grupos .
1. Seleccione la casilla de verificación de cada dominio de empresa para sincronizar y haga clic en Sincronizar ahora.

   Si selecciona varios dominios, la sincronización de dominios para todos los dominios se puede ejecutar al mismo tiempo. Sin embargo, si selecciona los dominios por separado, solo se puede ejecutar una sincronización de dominios a la vez.

## Programar sincronización de directorios {#schedule-directory-synchronization}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Programar sincronización:

   * Para habilitar la sincronización automática diariamente, en Programador, seleccione Ocurrencias. Seleccione Diario en la lista y escriba la hora en el formato de 24 horas en el cuadro correspondiente. Al guardar la configuración, este valor se convierte en una expresión cron, que se muestra en el cuadro Expresión Cron.
   * Para programar la sincronización en un día concreto de la semana o mes, o en un mes concreto, seleccione Expresión Cron y escriba la expresión adecuada en el cuadro. Por ejemplo, sincronice a la 1:30 a.m. del último viernes del mes.

El uso de la expresión cron se basa en el sistema de programación de trabajos de código abierto de Quartz, versión 1.4.0.

* Para desactivar la sincronización automática, seleccione Ocurrencias y elija Nunca en la lista.
* (Opcional) Para insertar información de usuarios y grupos en los servicios de contenido (obsoleto), seleccione la opción Seleccionar esta opción para insertar usuarios y grupos en proveedores de almacenamiento principales externos registrados . Esta opción también se aplica cuando se agregan nuevos usuarios y grupos a través de la página Usuarios y grupos .
* Haga clic en Guardar.

## Detener todas las sincronizaciones de directorios en curso {#stop-all-directory-synchronizations-currently-in-progress}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Anular. Este botón solo se muestra mientras hay una sincronización de directorios en curso.
