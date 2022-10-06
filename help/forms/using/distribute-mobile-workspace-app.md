---
title: Distribuir aplicación de AEM Forms
seo-title: Distribute AEM Forms app
description: Utilice la administración de dispositivos móviles (MDM) para la implementación a gran escala de aplicaciones en dispositivos móviles.
seo-description: Use Mobile Device Management (MDM) for the large-scale deployment of apps on mobile devices.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Distribuir aplicación de AEM Forms {#distribute-aem-forms-app}

La administración de dispositivos móviles (MDM) permite la implementación a gran escala de aplicaciones en dispositivos móviles.

>[!NOTE]
>
>Esta distribución solo es aplicable a dispositivos iOS y Android.

## Funciones principales que generalmente proporcionan las soluciones MDM: {#main-features-generally-provided-by-mdm-solutions}

* Habilitar la inscripción de dispositivos en su entorno empresarial
* Permitir la configuración y actualización de la configuración del dispositivo
* Aplique el cumplimiento de la seguridad.
* Acceso móvil seguro a los recursos corporativos

Una solución MDM junto con la Administración de aplicaciones móviles, le permite administrar aplicaciones internas, públicas y compradas en todos los dispositivos móviles de su empresa.

El administrador de MDM puede cargar archivos ipa y apk al servidor de MDM y controlar a los usuarios que pueden acceder a los archivos ipa o apk. El administrador también puede controlar la configuración de perfil correspondiente a cada aplicación.

## Configuración de perfil que afecta a la aplicación de AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

La siguiente configuración de perfil de su dispositivo afectará al funcionamiento de la aplicación AEM Forms en su dispositivo:

* **Permitir el uso de la cámara** en el **Funcionalidad del dispositivo** sección

Si desactiva **Permitir el uso de la cámara**, la función de cámara del [Anotación fotográfica](/help/forms/using/add-attachments.md) no funcionará. Debe activar esta opción para utilizar la cámara en la aplicación.

* **Requerir código de paso en el dispositivo** en la sección Políticas de contraseñas

Para habilitar **cifrado de datos de aplicación**, se recomienda habilitar la variable **Código de paso** en su dispositivo. Si el código de paso no está establecido en el dispositivo, los datos de la aplicación almacenados en el dispositivo no se cifran.
