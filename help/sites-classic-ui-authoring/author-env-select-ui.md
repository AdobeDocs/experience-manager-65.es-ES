---
title: Seleccionar la IU
seo-title: Selecting your UI
description: Para facilitar la labor de los usuarios que crean contenido, la IU táctil permite cambiar a la IU clásica en caso necesario.
seo-description: For convenience to authoring users, the touch-enabled UI does allow for switching to the classic UI when necessary.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 55%

---

# Seleccionar la IU{#selecting-your-ui}

AEM Dado que la IU táctil reemplaza a la IU clásica, el usuario o administrador de la instancia de la instancia de la debe tomar una decisión activa para seguir utilizando la IU clásica. Dado que la IU clásica ya no se mantiene, no hay forma de que el usuario autor simplemente cambie de la IU clásica a la equivalente en la IU táctil.

Para facilitar la labor de los usuarios que crean contenido, la IU táctil permite cambiar a la IU clásica en caso necesario. Consulte [Seleccionar la IU](/help/sites-authoring/select-ui.md) en la documentación de creación estándar para obtener más detalles.

>[!NOTE]
>
>Las instancias actualizadas de una versión anterior conservarán la IU clásica para la creación de páginas.
>
>Después de la actualización, la creación de páginas no se cambiará automáticamente a la IU táctil, pero puede configurarla con el[Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) de la **Servicio de modo de IU de creación de WCM** ( `AuthoringUIMode` service). Consulte [Omisiones de IU del editor](#uioverridesfortheeditor).

## Configurar la IU predeterminada para su instancia {#configuring-the-default-ui-for-your-instance}

Los administradores del sistema pueden configurar la IU que se ve al principio y en el inicio de sesión utilizando la [asignación raíz](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Las opciones predeterminadas del usuario o la configuración de la sesión pueden anular estos ajustes.
