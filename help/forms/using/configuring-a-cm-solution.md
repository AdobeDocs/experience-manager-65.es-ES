---
title: Configuración de una solución de administración de correspondencia
seo-title: Configuración de una solución de administración de correspondencia
description: nulo
seo-description: nulo
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# Configuración de una solución de administración de correspondencia {#configuring-a-correspondence-management-solution}

## Definición de la URL de instancia de autor para VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Siga los pasos siguientes para definir una URL de instancia de autor para la restauración de la versión de la instancia de autor:

1. Vaya a *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Inicie sesión con las credenciales de usuario de la Consola de administración OSGi. Las credenciales predeterminadas son admin/admin.
1. Busque y haga clic en el icono **[!UICONTROL Editar]** situado junto a la configuración de **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** .
1. En el campo URL **[!UICONTROL de creación de]** VersionRestoreManager, especifique la URL de la instancia de autor de VersionRestoreManager.

   **Cadena** URL:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Si hay varias instancias de autor (agrupadas) delante de un equilibrador de carga, especifique la dirección URL del equilibrador de carga en el campo URL **[!UICONTROL de creación de]** VersionRestoreManager.

1. Haga clic en **[!UICONTROL Guardar]**.

## Definición de la URL de instancia de publicación para ActivationManagerImpl (administrador de activación de instancia pública) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Siga estos pasos para definir la URL de instancia de Publish para el administrador de activación de instancias públicas:

1. Vaya a *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Inicie sesión con las credenciales de usuario de la Consola de administración OSGi. Las credenciales predeterminadas son admin/admin.
1. Busque y haga clic en el icono **[!UICONTROL Editar]** situado junto a la configuración de **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** .
1. En el campo URL **[!UICONTROL de publicación de]** ActivationManager, especifique la dirección URL para acceder a la instancia de publicación ActivationManager. Puede proporcionar las siguientes direcciones URL.

   * **URL del equilibrador de carga (recomendado)**: Proporcione la URL del equilibrador de carga si tiene un servidor web que actúa como equilibrador de carga frente al conjunto de servidores de publicación (varias instancias de publicación sin clúster).
   * **URL** de instancia de publicación: Proporcione cualquier URL de instancia de publicación. Si tiene una sola instancia de publicación o el servidor web que se encuentra delante del conjunto de servidores de publicación no es accesible desde el entorno de creación debido a restricciones. En caso de que la instancia de publicación especificada esté inactiva, hay un mecanismo de reserva con el que tratar en el autor.
   * **Cadena** URL:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Haga clic en **[!UICONTROL Guardar]**.

Para obtener más información sobre la configuración de la Administración de correspondencia, consulte Propiedades [de configuración de la Administración de](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html)correspondencia.
