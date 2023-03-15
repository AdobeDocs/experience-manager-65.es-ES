---
title: Configurar el bloqueo de cuentas
seo-title: Configure account-locking settings
description: Utilice la opción Habilitar bloqueo de cuentas para bloquear las cuentas de usuario después de un número determinado de errores de autenticación consecutivos.
seo-description: Use the Enable Account Locking option to lock user accounts after a specified number of consecutive authentication failures.
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 8%

---

# Configurar el bloqueo de cuentas {#configure-account-locking-settings}

Cuando agregue un dominio, especifique si desea habilitar el bloqueo de cuentas. Cuando se selecciona la opción Habilitar bloqueo de cuentas, las cuentas de usuario se bloquean después de un número determinado de errores de autenticación consecutivos. Después de un período de tiempo especificado, el usuario puede intentar autenticarse de nuevo. Esta función evita que los usuarios intenten varias combinaciones de credenciales para acceder al sistema.

Use la configuración de la página Administración de dominios para especificar el número máximo de errores de autenticación y el período de tiempo que las cuentas están bloqueadas. Esta configuración se aplica a todos los dominios que tienen habilitado el bloqueo de cuentas.

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Administración de dominios]**.
1. En el cuadro Máximo de errores de autenticación consecutivos, escriba el número de veces consecutivas que un usuario puede intentar iniciar sesión sin éxito antes de que se bloquee su cuenta. El valor predeterminado es 20.
1. En el cuadro Desbloquear la cuenta después de (minutos), escriba el número de minutos que la cuenta de usuario está bloqueada. Después del número de minutos especificado, el usuario puede intentar iniciar sesión de nuevo. El valor predeterminado es 30.
1. Haga clic en **[!UICONTROL Guardar]**.
