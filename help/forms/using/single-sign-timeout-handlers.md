---
title: Inicio de sesión único y controladores de tiempo de espera
seo-title: Single Sign On and timeout handlers
description: Establecer el valor del tiempo de espera de la sesión para AEM Forms Workspace.
seo-description: How-to set the session timeout value for AEM Forms workspace.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 78%

---

# Inicio de sesión único y controladores de tiempo de espera {#single-sign-on-and-timeout-handlers}

El espacio de trabajo de AEM Forms está habilitado para SSO. Si un usuario ha iniciado sesión en una aplicación de AEM Forms como Forms Manager o la interfaz de usuario del PDF Generator y accede al espacio de trabajo de AEM Forms en la misma sesión del explorador, el usuario ha iniciado sesión en el espacio de trabajo de AEM Forms y a la inversa.

## Administrar el tiempo de espera del servidor en AEM Forms Workspace {#handling-server-timeout-in-nbsp-aem-forms-workspace}

El tiempo de espera de sesión de un usuario se puede configurar en la consola de administración.

Para establecer el tiempo de espera, inicie sesión en `https://'[server]:[port]'/adminui`, navegue hasta **Configuración > Administrar usuarios > Configuración > Configurar atributos avanzados del sistema** y realice la configuración que desee.

En AEM Forms, el tiempo de espera de espacio de trabajo se administra de la siguiente manera:

* La duración de la sesión de un usuario está disponible en respuesta a la llamada `initialize` que inicializa la sesión del usuario.
* Un cuadro de diálogo emergente notifica al usuario que la sesión está a punto de caducar, 15 segundos antes de que caduque la sesión.

En este cuadro de diálogo emergente:

* Haga clic en Aceptar para finalizar la sesión de usuario.
* Haga clic en Cancelar para reiniciar la sesión de usuario.

>[!NOTE]
>
>Si no se realiza ninguna acción, se cerrará la sesión del usuario de AEM Forms Workspace automáticamente tres segundos antes de la caducidad de la sesión.
