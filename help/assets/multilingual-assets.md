---
title: Recursos multilingües y traducción de recursos
description: Obtenga información sobre cómo automatizar flujos de trabajo para traducir recursos, incluidos binarios, metadatos y etiquetas, a varios idiomas.
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: edccf23c-087e-4253-babb-dd4c6610517d
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 11%

---

# Recursos multilingües {#multilingual-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/multilingual-assets.html?lang=en) |

[!DNL Adobe Experience Manager Assets] permite automatizar los flujos de trabajo de traducción de recursos (binarios, metadatos y etiquetas incluidos) para generar recursos en otros idiomas y utilizarlos en proyectos multilingües.

Para automatizar los flujos de trabajo de traducción, se integran los proveedores de servicios de traducción con [!DNL Experience Manager] y cree proyectos para traducir recursos a varios idiomas. [!DNL Experience Manager] admite flujos de trabajo de traducción automática y humana.

Traducción humana: los recursos traducidos se devuelven e importan en [!DNL Experience Manager]. Cuando el proveedor de traducción esté integrado con [!DNL Experience Manager], los recursos se envían automáticamente entre [!DNL Experience Manager] y el proveedor de traducción.

Traducción automática: el servicio de traducción automática traduce inmediatamente los metadatos y las etiquetas de los recursos.

La traducción de recursos incluye lo siguiente:

1. [Conexión del Experience Manager con el proveedor de servicios de traducción](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Crear configuraciones del marco de trabajo de integración de traducciones](/help/sites-administering/tc-tic.md)
1. [Preparación de recursos para su traducción](preparing-assets-for-translation.md)
1. [Aplicación de servicios de nube de traducción a carpetas](transition-cloud-services.md)
1. [Creación de proyectos de traducción](translation-projects.md)

Si el proveedor de servicios de traducción no proporciona un conector con el que integrar [!DNL Experience Manager], use un [proceso alternativo](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Consulte también. [Creación de proyectos de traducción para fragmentos de contenido](creating-translation-projects-for-content-fragments.md).
