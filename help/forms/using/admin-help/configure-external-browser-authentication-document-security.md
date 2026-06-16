---
title: Configurar la autenticación extendida desde un explorador externo para la seguridad de los documentos
description: Obtenga información sobre cómo configurar la autenticación de exploradores externos para que los usuarios puedan autenticarse en documentos de PDF protegidos por directivas en Acrobat o Reader mediante el explorador web predeterminado del sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: a452674c-aea0-45d6-88cd-438af539d355
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 89a07256cd5bb850aac19565ad86273322fa1f31
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# Configurar la autenticación extendida desde un explorador externo para la seguridad de los documentos {#configure-external-browser-authentication-document-security}

>[!NOTE]
>
> Asegúrese de tener privilegios de administrador para acceder a la consola de administración de AEM Forms.

La autenticación extendida desde un explorador externo permite a los usuarios autenticarse para documentos de PDF protegidos por directivas mediante el explorador web predeterminado del sistema (como Microsoft Edge o Google Chrome) en lugar del control de explorador incrustado en Acrobat o Reader. Esto habilita métodos de autenticación modernos, como PassKey, autenticación biométrica y otras características del proveedor de identidad (IDP) que requieren un explorador moderno.

Cuando se habilita, al abrir un documento protegido por una directiva en Acrobat o Reader se inicia la página de inicio de sesión de IDP en el explorador predeterminado del usuario. Después de la autenticación, se redirige automáticamente al usuario a Acrobat o Reader y el documento se desbloquea.

## Requisitos previos {#prerequisites}

Antes de configurar la autenticación de un explorador externo, asegúrese de que se cumplen los siguientes requisitos:

* AEM Forms 6.5 en JEE con Service Pack 6.5.25.0 implementado o Service Pack 6.5.24.0 con la revisión de revisión JEE aplicable instalada en un servidor de aplicaciones compatible (JBoss, WebLogic o WebSphere). Consulte [Vínculos de distribución de software para la revisión JEE de AEM Forms2 6.5.24.0](#software-distribution-links).
* La autenticación extendida (autenticación de terceros) ya está habilitada y funciona con un IDP. Consulte [Configuración del servidor](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings) y [Agregar el proveedor de autenticación extendida](/help/forms/using/admin-help/configuring-client-server-options.md#add-the-extended-authentication-provider).
* Adobe Acrobat Pro o Adobe Acrobat Reader (64 bits) instalados en el equipo cliente Windows con la última actualización.

>[!NOTE]
>
> La autenticación de explorador externo requiere una versión compatible de Adobe Acrobat o Adobe Acrobat Reader en el cliente. Consulte las [Notas de la versión de Acrobat (seguimiento continuo de marzo de 2026)](https://www.adobe.com/devnet-docs/acrobatetk/tools/ReleaseNotesDC/continuous/dccontinuousmarch2026.html#dccontinuousmarchtwentytwentysix) para obtener detalles y actualizaciones de la versión.

### Vínculos de distribución de software para la revisión 2 de AEM Forms JEE 6.5.24.0 {#software-distribution-links}

La autenticación de explorador externo está disponible en AEM Forms en el paquete de servicio JEE 6.5.25.0 y versiones posteriores.

Si está utilizando AEM Forms con el paquete de servicio JEE 6.5.24.0 o una versión anterior, realice una de las siguientes acciones:

* Actualizar a [AEM Forms en el paquete de servicio JEE 6.5.25.0](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip).
* Instale el parche de la revisión JEE de AEM Forms 6.5.24.0 para su servidor de aplicaciones y plataforma mediante los vínculos siguientes.

Descargue e instale el parche de la revisión JEE de AEM Forms 6.5.24.0 para su plataforma desde [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html):

**JBoss**

* Windows: [revisión para el paquete de servicio 6.5.24.0 de AEM en el servidor JEE de Windows para JBoss](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-jboss.zip)
* Linux: [Revisión para el paquete de servicio 6.5.24.0 de AEM en Linux para el servidor JEE de JBoss](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-jboss.tar.gz)

**WebSphere**

* Windows: [revisión para el Service Pack de AEM 6.5.24.0 en el servidor JEE de Windows para WebSphere](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-websphere.zip)
* Linux: [Revisión para el paquete de servicio 6.5.24.0 de AEM en Linux para el servidor JEE de WebSphere](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-websphere.tar.gz)

**WebLogic**

* Windows: [revisión para el paquete de servicio 6.5.24.0 de AEM en el servidor JEE de Windows para WebLogic](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-weblogic.zip)
* Linux: [revisión para el paquete de servicio 6.5.24.0 de AEM en Linux para el servidor JEE de WebLogic](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-weblogic.tar.gz)

Para obtener instrucciones de instalación, consulte [Instalar un parche JEE](/help/release-notes/jee-patch-installer-65.md).

## Habilitar la autenticación de explorador externo {#enable-external-browser-authentication}

Este vídeo muestra cómo habilitar la autenticación de explorador externo en el servidor de AEM Forms Document Security.

>[!VIDEO](https://video.tv.adobe.com/v/3492357/)

1. En la consola de administración, haga clic en **Servicios** > **Seguridad de documentos** > **Configuración** > **Configuración del servidor**.
1. Busque la sección **Permitir autenticación extendida desde el explorador externo para aplicaciones cliente de Adobe**.
1. Seleccione la casilla de verificación de cada plataforma de cliente de Adobe que desee habilitar:
   * **Adobe Acrobat y Reader (64 bits) - Escritorio**
   * **Adobe Acrobat Reader (32 bits) - Escritorio**
1. Haga clic en **OK**.

Para ver la descripción de la configuración del servidor, consulte [Configuración del servidor](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings).

<!--
## Client configuration (Acrobat / Reader) {#client-configuration}

External browser authentication is enabled by default in Acrobat and Reader. No client-side configuration is needed for most deployments. When the server is configured to allow external browser authentication, the client uses it automatically.

To disable external browser authentication on specific client machines (forcing the embedded browser fallback), set the following registry value:

`HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Adobe\Adobe Acrobat\<product_branch>\FeatureLockDown\EDC`

| Setting | Value |
| ------- | ----- |
| Value name | `TPExternalBrowserAuthAdmin` |
| Value type | `REG_DWORD` |
| Value data | `0` (to disable) |

>[!NOTE]
>
> Both the server-side setting and the client-side preference must be enabled for external browser authentication to work. If either is disabled, the client falls back to the embedded browser.
-->

## de verificación {#verification}

Este vídeo muestra cómo comprobar la autenticación de un explorador externo: abra un PDF protegido por directivas en Acrobat, inicie sesión a través del explorador predeterminado y confirme que el documento se desbloquea después de la autenticación.

>[!VIDEO](https://video.tv.adobe.com/v/3492356/)

1. Cree un documento de PDF protegido por políticas mediante el servidor de Document Security.
1. En un equipo cliente de Windows, abra el PDF protegido en Acrobat Pro o Acrobat Reader.
1. Aparecerá un cuadro de diálogo de consentimiento en Acrobat. Haga clic en **Iniciar sesión**.
1. Compruebe que el navegador predeterminado del sistema se abre con la página de inicio de sesión de IDP.
1. Autenticación completa.
1. Compruebe que el documento protegido se abre correctamente.

## Resolución de problemas {#troubleshooting}

### Se abre el explorador incrustado en lugar del explorador del sistema {#embedded-browser-opens-instead-of-system-browser}

* Compruebe que el servidor tiene habilitada la autenticación de explorador externo. Consulte [Habilitar la autenticación de explorador externo](#enable-external-browser-authentication).
* Confirme que la versión de Acrobat o Reader admite esta función. Ver [Acrobat](#acrobat).

### La autenticación se realiza correctamente en el explorador, pero el documento no se desbloquea {#authentication-succeeds-but-document-does-not-unlock}

* Asegúrese de que Acrobat o Reader se estén ejecutando y no estén bloqueados por software de seguridad o cortafuegos.
* Si el problema persiste, reinstale o repare la instalación de Acrobat o Reader para restaurar el registro del controlador de protocolo.

### Aparece el mensaje &quot;No hemos podido iniciar sesión&quot; en Acrobat {#we-couldnt-sign-you-in-message}

* Es posible que el usuario haya tardado demasiado en completar la autenticación. Inténtelo de nuevo.
* Compruebe la conectividad de red entre el explorador y el servidor de AEM Forms.

### La opción Autenticación no aparece en la página de inicio de sesión {#authentication-option-does-not-appear}

* Los métodos y opciones de autenticación los configura el IDP, no AEM Forms ni Acrobat. Asegúrese de que el IDP sea compatible con el método de autenticación que desee utilizar.
* Compruebe que la página de inicio de sesión se está cargando en el explorador del sistema (no en el explorador integrado).
