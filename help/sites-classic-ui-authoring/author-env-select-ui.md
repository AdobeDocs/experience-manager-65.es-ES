---
title: Selección de la IU
description: Para facilitar la labor de los usuarios que crean contenido, la IU táctil permite cambiar a la IU clásica cuando es necesario.
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Selección de la IU{#selecting-your-ui}

Dado que la IU táctil sustituye a la IU clásica, el usuario o administrador de la instancia de AEM debe tomar una decisión activa para continuar utilizando la IU clásica. Como la IU clásica ya no se mantiene, no hay forma de que el usuario autor cambie de la IU clásica al equivalente en la IU táctil.

Para facilitar la labor de los usuarios que crean contenido, la IU táctil permite cambiar a la IU clásica cuando es necesario. Consulte la [Selección de la IU](/help/sites-authoring/select-ui.md) en la documentación de creación estándar para obtener más información.

>[!NOTE]
>
>Las instancias actualizadas desde una versión anterior conservarán la IU clásica para la creación de páginas.
>
>Después de la actualización, la creación de páginas no cambiará automáticamente a la IU táctil, pero puede configurar esta opción mediante la función[Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) del **Servicio de modo de IU de creación WCM** ( `AuthoringUIMode` ). Consulte [Omisiones de IU del editor](#uioverridesfortheeditor).

## Configuración de la IU predeterminada para su instancia {#configuring-the-default-ui-for-your-instance}

Un administrador del sistema puede configurar la IU que se ve al inicio y al iniciar sesión mediante [Asignación de raíz](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Esto puede anularse por los valores predeterminados del usuario o por la configuración de la sesión.
