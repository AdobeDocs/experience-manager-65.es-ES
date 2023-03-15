---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 4%

---

# Instalar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-connector-install.html?lang=en) |

Un usuario con acceso de administrador en [!DNL Adobe Experience Manager] instala el conector mejorado. Antes de realizar la instalación, revise la compatibilidad con la plataforma y otros [requisitos previos del conector](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* El Adobe requiere la implementación y la configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con el Adobe.
>
>* El Adobe puede publicar actualizaciones en [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hacen que este conector sea redundante; si esto sucede, es posible que los clientes deban realizar la transición desde el uso de este conector.
>
>* El Adobe admite las versiones de conector mejoradas 1.7.4 y posteriores. No se admiten versiones preliminares ni versiones personalizadas anteriores. Para comprobar la versión mejorada del conector, vaya a `digital.hoodoo` grupo disponible en el panel izquierdo de [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es).
>
>* Consulte [Examen de certificación de socio para el conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener más información sobre el examen, consulte [Guía del examen](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


Para instalar el conector, siga estos pasos:

1. Descargue el conector desde [[!DNL Software Distribution] vincular](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [Configuración del cortafuegos](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. En el despachante, permita los encabezados HTTP llamados `authorization`, `username`, y `apikey`. Permitir `GET`, `POST`, y `PUT` solicitudes a `/bin/workfront-tools`.
1. Asegúrese de que las siguientes rutas no existan en [!DNL Experience Manager] repositorio:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Instalación del paquete utilizando [!UICONTROL Administrador de paquetes]. Para saber cómo instalar paquetes, consulte [Documentación del Administrador de paquetes](/help/sites-administering/package-manager.md).
1. Crear `wf-workfront-users` in [!DNL Experience Manager] Grupo de usuarios y asignar el permiso `jcr:all` hasta `/content/dam`.

Un usuario del sistema `workfront-tools` se crea automáticamente y los permisos necesarios se administran automáticamente. Todos los usuarios de [!DNL Workfront] los usuarios que utilizan el conector se añaden automáticamente como parte de este grupo.

## Configuración de la conexión entre [!DNL Experience Manager] y [!DNL Workfront] {#configure-connection}

Para crear una conexión con Workfront, siga estos pasos:

1. Entrada [!DNL Experience Manager], seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de herramientas de Workfront]**.

1. Seleccionar `workfront-tools` en el panel izquierdo y seleccione **[!UICONTROL Crear]** en el área superior derecha de la página.

1. En el **[!UICONTROL Conexión de Workfront]** diálogo, proporcione los detalles necesarios de su [!DNL Workfront] implementación y seleccione **[!UICONTROL Conectar con Workfront]** opción. Una vez que se haya conectado correctamente, la [!DNL Workfront] la integración personalizada de documentos se crea automáticamente en [!DNL Workfront] entorno.

   ![Connect [!DNL Experience Manager] y [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Para verificar la conexión, acceda a ella en [!DNL Workfront] y compruebe que la clave de API es la misma y que la conexión es **[!UICONTROL Habilitado]**. Para ello, seleccione **[!UICONTROL Configurar]** > **[!UICONTROL Documentos]** > **[!UICONTROL Integraciones personalizadas]** in [!DNL Workfront].

## Actualizar [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets le permite actualizar el [!DNL Workfront for Experience Manager enhanced connector] de una versión anterior a la última.

Para actualizar el [!DNL Workfront for Experience Manager enhanced connector] a la versión más reciente:

1. Descargue la última versión del conector mejorado desde [[!DNL Software Distribution] vincular](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. Instalación del paquete utilizando [!UICONTROL Administrador de paquetes]. Para saber cómo instalar paquetes, consulte [Documentación del Administrador de paquetes](/help/sites-administering/package-manager.md).
