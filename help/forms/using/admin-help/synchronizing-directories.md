---
title: Sincronización de directorios
seo-title: Sincronización de directorios
description: Obtenga información sobre cómo sincronizar la base de datos de Administración de usuarios con los cambios realizados en los servidores de directorio de origen mediante la sincronización manual o programada.
seo-description: Obtenga información sobre cómo sincronizar la base de datos de Administración de usuarios con los cambios realizados en los servidores de directorio de origen mediante la sincronización manual o programada.
uuid: 71cbc04d-6172-49b7-a490-ff3233c1b2bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7ec0698a-9e6e-48d4-bba2-5a6eee313900
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Sincronización de directorios {#synchronizing-directories}

Para sincronizar dominios, puede elegir realizar una sincronización manual o programada. Una sincronización ** manual sincroniza los dominios seleccionados. Una sincronización ** programada sincroniza todos los dominios.

La sincronización de directorios se utiliza para extraer detalles de los servidores de directorios especificados en la configuración de directorios en la base de datos de Administración de usuarios. Posteriormente, también puede realizar una sincronización manual si se producen cambios o actualizaciones en los servidores de directorio. Por ejemplo, puede realizar una sincronización manual si se agregan usuarios y grupos o si se realizan cambios en la cuenta de un usuario.

También puede configurar una programación de sincronización diaria para sincronizar automáticamente la base de datos de Administración de usuarios con cambios o actualizaciones en los servidores de directorio de origen. Sin embargo, tenga en cuenta que este proceso utiliza recursos de red y de servidor. Elija períodos de tiempo de bajo uso y evite programar sincronizaciones innecesarias que conecten los recursos del sistema y de la red. Para minimizar sincronizaciones innecesarias, utilice la opción de sincronización inmediata en su lugar.

También puede especificar si desea insertar información de usuarios y grupos en Adobe LiveCycle Content Services 9 (desaprobada) al sincronizar dominios.

>[!NOTE]
>
>No cree varios usuarios y grupos locales mientras esté en curso una sincronización de directorio LDAP. Intentar este proceso puede provocar errores.

>[!NOTE]
>
>Si se interrumpe el proceso de sincronización de dominios (por ejemplo, el servidor de aplicaciones se cierra durante el proceso), espere un poco antes de intentar sincronizar el dominio. Para evaluar el estado de la sincronización, consulte el estado. Si la Administración de usuarios adquirió un bloqueo antes del cierre, espere 10 minutos para que el bloqueo se libere después del reinicio del servidor. Si el estado de sincronización es &quot;En curso&quot; pero la sincronización se interrumpe o se detiene, la Administración de usuarios reintentará la sincronización pasados 3 minutos. Después de tres intentos fallidos, la Administración de usuarios declara que la sincronización ha fallado y libera el bloqueo.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsoleto) es un sistema de administración de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, monitorear y optimizar procesos centrados en el ser humano. La compatibilidad con Content Services (obsoleto) finaliza el 31/12/2014. Consulte el documento [de ciclo vital del producto de](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)Adobe. Para obtener información sobre la configuración de Content Services (obsoleto), consulte [Administración de Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

## Habilitar sincronización de directorio delta {#enable-delta-directory-synchronization}

La sincronización de directorios Delta mejora la eficacia de la sincronización de directorios. Cuando la sincronización de directorios delta está habilitada, Administración de usuarios sincroniza solo los usuarios y grupos que se han agregado o actualizado desde la última sincronización.

La Administración de usuarios realiza los siguientes pasos cuando la sincronización de directorios delta está habilitada:

* Recupere todos los usuarios de los servidores de directorio, pero actualice la base de datos de Administración de usuarios solo con los usuarios cuya marca de tiempo haya cambiado.
* Recupere todos los grupos pero actualice la base de datos de Administración de usuarios solo con los grupos cuya marca de tiempo haya cambiado.
* Recupere miembros del grupo únicamente para los grupos cuyas marcas de hora han cambiado y actualice la base de datos de Administración de usuarios con esa información.

>[!NOTE]
>
>Los usuarios y grupos que se eliminaron del directorio no se eliminarán de la base de datos de Administración de usuarios hasta que se realice una sincronización completa del directorio.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. En Sintaxis delta, active la casilla de verificación y haga clic en Guardar.
1. Edite la configuración del directorio para cada uno de los dominios de empresa que utilizarán la función de sincronización del directorio delta. En las páginas Configuración de usuario y Configuración de grupo, ubique la opción Modificar marca de hora y escriba `modify TimeStamp` como valor. Para obtener más información sobre la edición de dominios de empresa, consulte [Edición y conversión de dominios](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)existentes.

## Habilitar o deshabilitar el registro detallado durante la sincronización {#enable-or-disable-detailed-logging-during-synchronization}

De forma predeterminada, la Administración de usuarios registra estadísticas detalladas durante el proceso de sincronización.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configurar atributos avanzados del sistema.
1. En Sincronizar registro de estadísticas, anule la selección de la casilla de verificación para deshabilitar el registro detallado o selecciónelo para habilitar el registro y, a continuación, haga clic en Guardar.

## Configuración de la opción de reintento de sincronización de directorios {#configure-the-directory-synchronization-retry-option}

Puede configurar la Administración de usuarios para que compruebe periódicamente si hay algún intento fallido de sincronización de directorios. A continuación, la Administración de usuarios intenta completar las sincronizaciones fallidas.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configurar atributos avanzados del sistema.
1. En Synch Finisher Cron Expression (Expresión cron de Synch Finisher), introduzca una expresión cron que represente el intervalo en el que User Management reintenta las sincronizaciones fallidas. El uso de la expresión cron se basa en el sistema de programación de trabajos de código abierto Quartz, versión 1.4.0.

   El valor predeterminado es 0 0/13 &amp;ast; ?  &amp;ast; , lo que significa que la comprobación se realiza cada 13 minutos.

## Sincronizar directorios manualmente {#manually-synchronize-directories}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. (Opcional) Para insertar información de usuarios y grupos en Content Services (obsoleto), seleccione la opción Seleccionar esta opción para insertar usuarios y grupos en proveedores de almacenamiento externo registrados. Esta opción también se aplica al agregar usuarios y grupos nuevos a través de la página Usuarios y grupos.
1. Seleccione la casilla de verificación de cada dominio de empresa para sincronizar y haga clic en Sincronizar ahora.

   Si selecciona varios dominios, la sincronización de dominios para todos los dominios se puede ejecutar al mismo tiempo. Sin embargo, si selecciona los dominios por separado, solo se puede ejecutar una sincronización de dominios a la vez.

## Programar sincronización de directorios {#schedule-directory-synchronization}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Programar sincronización:

   * Para habilitar la sincronización automática diariamente, en Programador, seleccione Ocurrencias. Seleccione Diario en la lista y escriba la hora en el formato de 24 horas en el cuadro correspondiente. Al guardar la configuración, este valor se convierte en una expresión cron, que se muestra en el cuadro Expresión Cron.
   * Para programar la sincronización en un día concreto de la semana o mes, o en un mes concreto, seleccione Expresión crónica y escriba la expresión adecuada en el cuadro. Por ejemplo, sincronice a la 1:30 A.M. el último viernes del mes.

El uso de la expresión cron se basa en el sistema de programación de trabajos de código abierto Quartz, versión 1.4.0.

* Para desactivar la sincronización automática, seleccione Ocurrencias y Nunca en la lista.
* (Opcional) Para insertar información de usuarios y grupos en Content Services (obsoleto), seleccione la opción Seleccionar esta opción para insertar usuarios y grupos en proveedores de almacenamiento externo registrados. Esta opción también se aplica al agregar usuarios y grupos nuevos a través de la página Usuarios y grupos.
* Haga clic en Guardar.

## Detener todas las sincronizaciones de directorios en curso {#stop-all-directory-synchronizations-currently-in-progress}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Anular. Este botón solo se muestra mientras hay una sincronización de directorio en curso.

