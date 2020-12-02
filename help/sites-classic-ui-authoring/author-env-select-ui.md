---
title: Selección de la IU
seo-title: Seleccionar la IU
description: Para facilitar la labor de los usuarios que crean contenido, la IU táctil permite cambiar a la IU clásica en caso necesario.
seo-description: Para facilitar la labor de los usuarios que crean contenido, la IU táctil permite cambiar a la IU clásica en caso necesario.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 60%

---


# Seleccionar la IU{#selecting-your-ui}

Dado que la IU táctil sustituye a la IU clásica, el usuario o administrador de la instancia de AEM debe tomar una decisión activa para continuar utilizando la IU clásica. Dado que la IU clásica ya no se mantiene, el usuario creador no puede cambiar de la IU clásica al equivalente en la IU táctil.

Para facilitar la labor de los usuarios que crean contenido, la IU táctil permite cambiar a la IU clásica en caso necesario. Consulte [Seleccionar la IU](/help/sites-authoring/select-ui.md) en la documentación de creación estándar para obtener más detalles.

>[!NOTE]
>
>Las instancias actualizadas de una versión anterior conservarán la IU clásica para la creación de páginas.
>
>Después de la actualización, la creación de páginas no cambiará automáticamente a la IU táctil, pero puede configurarla con la configuración[OSGi](/help/sites-deploying/configuring-osgi.md) del **servicio de modo de IU de creación de WCM** ( `AuthoringUIMode` servicio). Consulte [Omisiones de IU del editor](#uioverridesfortheeditor).

## Configurar la IU predeterminada para su instancia {#configuring-the-default-ui-for-your-instance}

Los administradores del sistema pueden configurar la IU que se ve al principio y en el inicio de sesión utilizando la [asignación raíz](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Las opciones predeterminadas del usuario o la configuración de la sesión pueden anular estos ajustes.
