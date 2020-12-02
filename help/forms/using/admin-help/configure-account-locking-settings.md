---
title: Configuración de la configuración del bloqueo de cuentas
seo-title: Configuración de la configuración del bloqueo de cuentas
description: Utilice la opción Activar bloqueo de cuenta para bloquear las cuentas de usuario después de un número especificado de errores de autenticación consecutivos.
seo-description: Utilice la opción Activar bloqueo de cuenta para bloquear las cuentas de usuario después de un número especificado de errores de autenticación consecutivos.
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 4%

---


# Configurar la configuración del bloqueo de cuentas {#configure-account-locking-settings}

Al agregar un dominio, especifique si desea habilitar el bloqueo de cuenta. Cuando se selecciona la opción Activar bloqueo de cuenta, las cuentas de usuario se bloquean después de un número especificado de errores de autenticación consecutivos. Después de un período de tiempo determinado, el usuario puede intentar autenticarse de nuevo. Esta función evita que los usuarios intenten distintas combinaciones de credenciales para acceder al sistema.

Utilice la configuración de la página Administración de dominios para especificar el número máximo de errores de autenticación y el período de tiempo que las cuentas se bloquean. Esta configuración se aplica a todos los dominios que tienen habilitado el bloqueo de cuentas.

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Administración de dominios]**.
1. En el cuadro Número máximo de errores de autenticación consecutiva, introduzca el número de veces consecutivas que un usuario puede intentar iniciar sesión sin éxito antes de que su cuenta esté bloqueada. El valor predeterminado es 20.
1. En el cuadro Desbloquear la cuenta después de (minutos), introduzca el número de minutos que la cuenta de usuario está bloqueada. Después del número especificado de minutos, el usuario puede intentar iniciar sesión de nuevo. El valor predeterminado es 30.
1. Haga clic en **[!UICONTROL Guardar]**.

