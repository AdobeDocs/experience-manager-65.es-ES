---
title: Resolución de problemas de la aplicación AEM Forms
seo-title: Troubleshoot AEM Forms app
description: Obtenga información sobre problemas comunes con la aplicación de AEM Forms y cómo solucionarlos.
seo-description: Learn about common issues with AEM Forms app and how to troubleshoot them.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
exl-id: caec5fc3-db52-4bf5-8eb2-17e5189ab819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 2%

---

# Resolución de problemas de la aplicación AEM Forms {#troubleshoot-aem-forms-app}

Este artículo describe los mensajes de error que se pueden mostrar al crear la aplicación de AEM Forms y los pasos para resolverlos.

Las secciones de este artículo incluyen:

* [Pérdida de archivos adjuntos para usuarios de iOS](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Los borradores de formulario de HTML5 enviados por los usuarios del espacio de trabajo no están visibles en el portal](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [Los formularios de HTML 5 (no en caché) no se pueden cargar en la aplicación de AEM Forms](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms no se sincroniza en Windows](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Versión no admitida de Gradle](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Problemas de compatibilidad de complementos de Gradle y Android Gradle](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Pérdida de archivos adjuntos para usuarios de iOS {#attachment-loss-for-ios-users}

La aplicación de AEM Forms para iOS configurada para sincronizarse con AEM Forms en OSGi solo admite archivos adjuntos de nivel de campo. Todos los archivos adjuntos deben tener nombres únicos. Si varios archivos adjuntos tienen un nombre idéntico, solo se conserva un archivo adjunto y se pierden todos los demás que tengan un nombre idéntico. Siga estos pasos para evitar que los usuarios de dispositivos iOS pierdan datos:

1. En el servidor conectado, vaya a **Adobe Experience Manager > Herramientas > Operaciones > Consola web**.
1. Busque y haga clic en **[!UICONTROL Configuración del canal web de comunicaciones interactivas y formularios adaptables]**.
1. En el [!UICONTROL Configuración del canal web de comunicaciones interactivas y formularios adaptables] cuadro de diálogo, habilitar **Hacer únicos los nombres de archivo**.

   If **Hacer únicos los nombres de archivo** está desactivada, los usuarios pierden datos si intentan enviar formularios adaptables con varios archivos adjuntos.

1. Haga clic en **Guardar**.

## Los borradores de formulario de HTML5 enviados por los usuarios del espacio de trabajo no están visibles en el portal {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

Para formularios HTML5 activados en la aplicación AEM Forms con **Guardar como borrador** Perfil de procesamiento de HTML, los borradores guardados no son visibles para los usuarios del espacio de trabajo. Para ver los borradores guardados de los formularios de HTML5 enviados por los usuarios del espacio de trabajo en el portal, realice los siguientes pasos:

1. Abra CRXDE e inicie sesión con credenciales de administrador.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. En la ruta raíz del CRXDE, en la Lista de control de acceso en Control de acceso, haga clic en **+**.
1. En el **Agregar nueva entrada** , haga clic en el botón de búsqueda de grupo del campo Principal .
1. En el campo Nombre del cuadro de diálogo Seleccionar principal, escriba `PERM_WORKSPACE_USER` y haga clic en **Buscar**.
1. Select `PERM_WORKSPACE_USER` en el cuadro de diálogo Seleccionar principal y haga clic en **OK**.
1. En el cuadro de diálogo Agregar nueva entrada , `PERM_WORKSPACE_USER` grupo está seleccionado en el campo Principal.

   Habilitar `jcr:read` privilegios para el grupo de usuarios.

1. Haga clic en **Aceptar**.

## Los formularios de HTML 5 (no en caché) no se pueden cargar en la aplicación de AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Cuando la aplicación de AEM Forms está conectada a una versión anterior del servidor de AEM Forms, los formularios HTML5 no almacenados en caché no se cargan en la aplicación de AEM Forms.

Siga estos pasos para resolver el problema:

1. En la instancia de autor, vaya a **Adobe Experience Manager > Herramientas > Configurar el servicio sin conexión de la aplicación de Workspace > Configurar ahora**.
1. En **Servicio sin conexión de la aplicación de Workspace** página, haga clic en **Caché de recursos manual**.

   URL: https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. En el **Caché de recursos manual** , haga clic en la pestaña **+** para añadir una ruta CRX.
1. En el **Agregar un nuevo recurso** campo, tipo: /etc.clientlibs/fd/xfaforms/I18N/en_US.js y haga clic en **Agregar**.
1. Haga clic en **Guardar**.

## AEM Forms no se sincroniza en Windows {#aem-forms-do-not-sync-on-windows}

En la aplicación de AEM Forms en Windows, un formulario no se sincroniza con el servidor conectado si la ruta del formulario o cualquiera de sus recursos contiene buenos o iguales a 256 caracteres.

Modifique la ruta del formulario y sus recursos para reducir el número de caracteres a menos de 256 caracteres.

## Versión no admitida de Gradle {#unsupported-version-of-gradle}

**Mensaje de error:** El proyecto utiliza una versión no compatible de Gradle.

El mensaje de error se muestra al crear la aplicación de AEM Forms en Android Studio. El problema se debe a que la versión de Gradle no es compatible con el sistema.

**Resolución:** Haga clic en **Corregir el envoltorio de Gradle y volver a importar el proyecto** para resolver el problema.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Problemas de compatibilidad de complementos de Gradle y Android Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**Mensaje de error:** Las versiones del complemento Android Gradle y Gradle no son compatibles.

El mensaje de error se muestra al seleccionar **Generar APK** de la **Generar** en la interfaz de usuario de Android Studio.

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**Resolución:** Apertura **Secuencias de comandos de cuadrícula** > **gradle-wrapper.properties** y edite el **distributionUrl** propiedad.

Por ejemplo, la consola de Android Studio recomienda reducir la versión de Gradle a 3.5. Edite la versión en **distributionUrl** de **gradle-wrapper.properties** archivo.

Select **Generar** > **Generar APK** para resolver el error y generar el archivo .apk.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
