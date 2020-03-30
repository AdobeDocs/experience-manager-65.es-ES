---
title: Inicio de sesión único y controladores de tiempo de espera
seo-title: Inicio de sesión único y controladores de tiempo de espera
description: Cómo establecer el valor de tiempo de espera de sesión para el espacio de trabajo de AEM Forms.
seo-description: Cómo establecer el valor de tiempo de espera de sesión para el espacio de trabajo de AEM Forms.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Inicio de sesión único y controladores de tiempo de espera {#single-sign-on-and-timeout-handlers}

El espacio de trabajo de AEM Forms está habilitado para SSO. Si un usuario ha iniciado sesión en una aplicación de AEM Forms como Forms Manager o la interfaz de usuario de PDF Generator y accede al espacio de trabajo de AEM Forms en la misma sesión del explorador, el usuario ha iniciado sesión en el espacio de trabajo de AEM Forms y viceversa.

## Gestión del tiempo de espera del servidor en el espacio de trabajo de AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

El tiempo de espera de sesión de un usuario se puede configurar en la Consola de administración.

Para establecer el tiempo de espera, inicie sesión en `https://'[server]:[port]'/adminui`, vaya a **Configuración > Administración de usuarios > Configuración > Configurar atributos** avanzados del sistema y realice los ajustes que desee.

En el espacio de trabajo de AEM Forms, el tiempo de espera se gestiona de la siguiente manera:

* La duración de la sesión de un usuario está disponible como respuesta a una `initialize` llamada que inicializa la sesión del usuario.
* Un cuadro de diálogo emergente notifica al usuario que la sesión está a punto de caducar, 15 segundos antes de que caduque la sesión.

En este cuadro de diálogo emergente:

* Haga clic en Aceptar para finalizar la sesión de usuario.
* Haga clic en Cancelar para reinicializar la sesión de usuario.

>[!NOTE]
>
>Si no se realiza ninguna acción, se cierra automáticamente la sesión del usuario en el espacio de trabajo de AEM Forms tres segundos antes de que caduque la sesión.

**[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)**
