---
title: Configuración de atributos de sistema avanzados
seo-title: Configure advanced system attributes
description: Utilice la página Configurar Atributos del sistema avanzados para modificar ciertas opciones del archivo de configuración sin necesidad de exportar, editar e importar el archivo.
seo-description: Use the Configure Advanced System Attributes page to modify certain settings in the configuration file without the need to export, edit, and import the file.
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---

# Configuración de atributos de sistema avanzados {#configure-advanced-system-attributes}

Utilice la página Configurar Atributos del sistema avanzados para modificar ciertas opciones del archivo de configuración sin necesidad de exportar, editar e importar el archivo. (Consulte [Importación y exportación del archivo de configuración](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Configuración > Configurar atributos avanzados del sistema]**.
1. (Opcional) Cambie cualquiera de los siguientes atributos de sesión:

   **Límite de tiempo de espera de sesión (minutos):** Cantidad de tiempo, en minutos, antes de que se cierre la sesión de un usuario automáticamente en el sistema. De forma predeterminada, AEM componentes de formularios como Workbench exceden el tiempo de espera de dos horas, independientemente de la actividad o la inactividad, y el usuario debe volver a iniciar sesión. Los valores válidos son `1` a `1440`. El valor predeterminado es `120` (2 horas). Esta configuración actualiza el `SAML/Producer/assertionValidityInMinutes` clave de entrada en el archivo de configuración.

   >[!NOTE]
   >
   >No debe establecer el límite de tiempo de espera de sesión por debajo de los 10 minutos, ya que es posible que el sistema no se comporte correctamente. El valor recomendado es 10-120 (minutos).

   **Umbral de aserción (segundos):** Un tiempo de búfer para compensar los retrasos debido a las diferencias de tiempo del sistema entre AEM servidor de aplicaciones de formularios en un clúster. AEM formularios retrasa el tiempo de inicio de sesión de un usuario en la cantidad de tiempo (en segundos) especificada en esta propiedad. Los valores válidos son `0` a `3600`. El valor predeterminado es `60`. Esta configuración actualiza el `SAML/Producer/assertionThresholdInSeconds` clave de entrada en el archivo de configuración.

   **Máximo de renovaciones permitidas de una aserción:** Número máximo de veces que una sesión de usuario se puede renovar de forma transparente sin necesidad de iniciar sesión. Los valores válidos son `0` a `9999`. Un valor de `0` significa que las afirmaciones no se renuevan. El valor predeterminado es 10. Esta configuración actualiza el `SAML/Producer/maxAssertionRenewalCount` clave de entrada en el archivo de configuración.

1. (Opcional) Cambie cualquiera de los siguientes atributos de sincronización de directorios:

   **Registro de estadísticas de sincronización:** Especifica si Administración de usuarios registra estadísticas detalladas durante el proceso de sincronización. (Consulte [Habilitar o deshabilitar el registro detallado durante la sincronización](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization).)

   **Sinc. Expresiones de Cron del finizador de sincronización:** Intervalo en el cual Administración de usuarios reintenta realizar errores en las sincronizaciones. (Consulte [Configuración de la opción de reintento de sincronización de directorios](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option).)

   **Tiempo De Espera De Bloqueo De Trabajo De Clúster En Minutos:** Se utiliza en entornos agrupados. Si la sincronización en un nodo falla y el bloqueo del clúster no se libera, este valor especifica el número de minutos que otro nodo espera antes de adquirir el bloqueo por la fuerza. El valor predeterminado es `15` minutos. Los valores válidos son `1` a `1440` minutos.

1. (Opcional) Cambie los siguientes atributos y haga clic en **[!UICONTROL OK]**:

   **Auditoría de eventos del administrador de usuarios:** Seleccione esta opción para habilitar la auditoría de eventos de sincronización de directorios y de eventos de autenticación como éxito, error y bloqueo. De forma predeterminada, esta opción no está seleccionada a menos que haya instalado un componente que requiera auditoría, como Rights Management. Esta configuración actualiza el `APSAuditService` clave de entrada en el archivo de configuración.

   **Creación automática de grupos dinámicos:** Permite la creación automática de grupos dinámicos basados en dominios de correo electrónico. (Consulte [Crear un grupo dinámico](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group).)

También puede volver a la configuración original de Administración de usuarios haciendo clic en Recargar.
