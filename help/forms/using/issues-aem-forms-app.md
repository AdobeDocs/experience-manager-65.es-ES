---
title: Solución de problemas de la aplicación de AEM Forms
seo-title: Solución de problemas de la aplicación de AEM Forms
description: Obtenga información sobre los problemas comunes de la aplicación de AEM Forms y cómo solucionarlos.
seo-description: Obtenga información sobre los problemas comunes de la aplicación de AEM Forms y cómo solucionarlos.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Solución de problemas de la aplicación de AEM Forms {#troubleshoot-aem-forms-app}

En este artículo se describen los mensajes de error que se pueden mostrar al crear la aplicación de AEM Forms y los pasos para resolverlos.

Las secciones de este artículo incluyen:

* [Pérdida de datos adjuntos para usuarios de iOS](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Los borradores de formulario HTML5 enviados por los usuarios del espacio de trabajo no están visibles en el portal](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [Los formularios HTML5 (no en caché) no se pueden cargar en la aplicación de AEM Forms](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms no se sincroniza en Windows](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Versión no admitida de Gradle](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Problemas de compatibilidad de complementos de Gradle y Android Gradle](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Pérdida de datos adjuntos para usuarios de iOS {#attachment-loss-for-ios-users}

La aplicación de AEM Forms para iOS configurada para sincronizarse con AEM Forms en OSGi solo admite archivos adjuntos de campo. Todos los archivos adjuntos deben tener nombres únicos. Si varios datos adjuntos tienen un nombre idéntico, solo se conservará un dato adjunto y se perderán todos los demás datos con el mismo nombre. Realice los siguientes pasos para evitar que los usuarios de dispositivos iOS sufran pérdida de datos:

1. En el servidor conectado, vaya a **Adobe Experience Manager > Herramientas > Operaciones > Consola** web.
1. Busque y haga clic en **Servicio** de configuración de formularios adaptable.
1. En el cuadro de diálogo Servicio de configuración de formulario adaptable, habilite **Convertir nombres de archivo en únicos**.

   Si **la opción Convertir nombres de archivo en únicos** está desactivada, los usuarios pierden datos si intentan enviar formularios adaptables con varios archivos adjuntos.

1. Haga clic en **Guardar**.

## Los borradores de formulario HTML5 enviados por los usuarios del espacio de trabajo no están visibles en el portal {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

Para los formularios HTML5 activados en la aplicación de AEM Forms con **Guardar como perfil de procesamiento HTML de borrador** , los borradores guardados no son visibles para los usuarios del espacio de trabajo. Para ver los borradores guardados de formularios HTML5 enviados por los usuarios del espacio de trabajo en el portal, lleve a cabo los siguientes pasos:

1. Abra CRXDE e inicie sesión con las credenciales del administrador.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. En la ruta raíz de CRXDE, en la lista de control de acceso bajo Control de acceso, haga clic en **+**.
1. En el cuadro de diálogo **Agregar nueva entrada** , haga clic en el botón de búsqueda de grupo en el campo Principal.
1. En el campo Nombre del cuadro de diálogo Seleccionar entidad de seguridad, escriba `PERM_WORKSPACE_USER` y haga clic en **Buscar**.
1. Seleccione `PERM_WORKSPACE_USER` el grupo en el cuadro de diálogo Seleccionar entidad de seguridad y haga clic en **Aceptar**.
1. En el cuadro de diálogo Agregar nueva entrada, `PERM_WORKSPACE_USER` el grupo está seleccionado en el campo Principal.

   Habilite `jcr:read` privilegios para el grupo de usuarios.

1. Haga clic en **Aceptar**.

## Los formularios HTML5 (no en caché) no se pueden cargar en la aplicación de AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Cuando la aplicación de AEM Forms está conectada a una versión anterior del servidor de AEM Forms, los formularios HTML5 no almacenados en caché no se cargan en la aplicación de AEM Forms.

Siga los pasos siguientes para resolver el problema:

1. En la instancia de autor, vaya a **Adobe Experience Manager > Herramientas > Configurar el servicio sin conexión de la aplicación de Workspace > Configurar ahora**.
1. En la página Servicio **sin conexión de la aplicación de** Workspace, haga clic en Caché **de recursos** manual.

   URL: https://&lt;servidor>:&lt;puerto>/libs/fd/workspace-offline/content/config.html

1. En la ficha Caché **de recursos** manual, haga clic en el botón **+** para agregar una ruta CRX.
1. En el campo **Agregar un nuevo recurso** , escriba: /etc.clientlibs/fd/xfaforms/I18N/en_US.js y haga clic en **Agregar**.
1. Haga clic en **Guardar**.

## AEM Forms no se sincroniza en Windows {#aem-forms-do-not-sync-on-windows}

En la aplicación de AEM Forms en Windows, un formulario no se sincroniza con el servidor conectado si la ruta del formulario o de cualquiera de sus recursos contiene más o menos 256 caracteres.

Modifique la ruta del formulario y sus recursos para reducir el número de caracteres a menos de 256 caracteres.

## Versión no admitida de Gradle {#unsupported-version-of-gradle}

**** Mensaje de error: El proyecto está utilizando una versión no admitida de Gradle.

El mensaje de error se muestra al crear una aplicación de AEM Forms en Android Studio. El problema se debe a que la versión de Gradle no es compatible con el sistema.

**** Resolución: Haga clic en **Corregir contenedor de degradado y vuelva a importar el proyecto** para resolver el problema.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Problemas de compatibilidad de complementos de Gradle y Android Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**** Mensaje de error: Las versiones de los complementos y la base de Android Gradle no son compatibles.

El mensaje de error se muestra cuando selecciona la opción **Generar APK** en el menú **Generar** de la interfaz de usuario de Android Studio.

![gradle_plugin_Compatibility](assets/gradle_plugin_compatibility.png)

**** Resolución: Abra **Secuencias de comandos** de degradado > archivo **gradle-wrapper.properties** y edite la propiedad **distributionUrl** .

Por ejemplo, la consola de Android Studio recomienda reducir la versión de Gradle a 3.5. Edite la versión en **distributionUrl** del **archivo gradle-wrapper.properties** .

Seleccione **Generar** > **Generar APK** de nuevo para resolver el error y generar el archivo .apk.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)

