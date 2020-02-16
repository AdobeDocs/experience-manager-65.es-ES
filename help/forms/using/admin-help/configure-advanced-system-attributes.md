---
title: Configurar atributos avanzados del sistema
seo-title: Configurar atributos avanzados del sistema
description: Utilice la página Configurar Atributos Avanzados del Sistema para modificar determinados ajustes del archivo de configuración sin necesidad de exportar, editar e importar el archivo.
seo-description: Utilice la página Configurar Atributos Avanzados del Sistema para modificar determinados ajustes del archivo de configuración sin necesidad de exportar, editar e importar el archivo.
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurar atributos avanzados del sistema {#configure-advanced-system-attributes}

Utilice la página Configurar Atributos Avanzados del Sistema para modificar determinados ajustes del archivo de configuración sin necesidad de exportar, editar e importar el archivo. (Consulte [Importación y exportación del archivo](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)de configuración.)

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Configuración > Configurar atributos]** avanzados del sistema.
1. (Opcional) Cambie cualquiera de los atributos de sesión siguientes:

   **** Límite de tiempo de espera de sesión (minutos): Cantidad de tiempo, en minutos, antes de que un usuario cierre la sesión del sistema automáticamente. De forma predeterminada, los componentes de formularios AEM, como Workbench, agotan el tiempo de espera después de dos horas, independientemente de la actividad o inactividad, y el usuario debe volver a iniciar sesión. Los valores válidos son `1` para `1440`. El valor predeterminado es `120` (2 horas). Esta configuración actualiza la clave de entrada `SAML/Producer/assertionValidityInMinutes` en el archivo de configuración.

   >[!NOTE]
   >
   >No debe establecer el límite de tiempo de espera de sesión por debajo de 10 minutos, ya que es posible que el sistema no se comporte correctamente. El valor recomendado es 10-120 (minutos).

   **** Umbral de aserción (segundos): Tiempo de búfer para compensar los retrasos debido a las diferencias de tiempo del sistema entre los servidores de aplicaciones de formularios AEM en un clúster. Los formularios AEM antedatan el tiempo de inicio de sesión de un usuario en la cantidad de tiempo (en segundos) especificada en esta propiedad. Los valores válidos son `0` para `3600`. El valor predeterminado es `60`. Esta configuración actualiza la clave de entrada `SAML/Producer/assertionThresholdInSeconds` en el archivo de configuración.

   **** Máximo de renovaciones permitidas de una afirmación: El número máximo de veces que una sesión de usuario se puede renovar de forma transparente sin necesidad de iniciar sesión. Los valores válidos son `0` para `9999`. Un valor de `0` significa que las afirmaciones no se renuevan. El valor predeterminado es 10. Esta configuración actualiza la clave de entrada `SAML/Producer/maxAssertionRenewalCount` en el archivo de configuración.

1. (Opcional) Cambie cualquiera de los siguientes atributos de sincronización de directorios:

   **** Registro de estadísticas de sincronización: Especifica si la Administración de usuarios registra estadísticas detalladas durante el proceso de sincronización. (Consulte [Habilitar o deshabilitar el registro detallado durante la sincronización](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization)).

   **** Sinch Finisher Cron Expression: Intervalo en el que la Administración de usuarios reintenta las sincronizaciones fallidas. (Consulte [Configuración de la opción](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)de reintento de sincronización de directorios.)

   **** Tiempo De Espera De Bloqueo De Trabajo De Clúster En Minutos: Se utiliza en entornos agrupados. Si la sincronización en un nodo falla y no se libera el bloqueo del clúster, este valor especifica el número de minutos que otro nodo espera antes de adquirir el bloqueo por la fuerza. The default value is `15` minutes. Los valores válidos son de `1` a `1440` minutos.

1. (Opcional) Cambie los atributos siguientes y haga clic en **[!UICONTROL Aceptar]**:

   **** Auditoría de eventos del administrador de usuarios: Seleccione esta opción para habilitar la auditoría de los eventos de sincronización de directorios y de los eventos de autenticación, como los eventos de éxito, error y bloqueo. De forma predeterminada, esta opción no está seleccionada a menos que haya instalado un componente que requiera auditoría, como Rights Management. Esta configuración actualiza la clave de entrada `APSAuditService` en el archivo de configuración.

   **** Creación automática de grupos dinámicos: Habilita la creación automática de grupos dinámicos basados en dominios de correo electrónico. (Consulte [Creación de un grupo](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group)dinámico).

También puede volver a la configuración original de Administración de usuarios haciendo clic en Volver a cargar.
