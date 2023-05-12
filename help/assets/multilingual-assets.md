---
title: Recurso multilingüe
description: Aprenda a automatizar los flujos de trabajo para traducir recursos, incluidos binarios, metadatos y etiquetas a varios idiomas.
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: edccf23c-087e-4253-babb-dd4c6610517d
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 8%

---

# Recursos multilingües {#multilingual-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=en) |
| AEM 6.5 | Este artículo |

[!DNL Adobe Experience Manager Assets] permite automatizar los flujos de trabajo de traducción en recursos (incluidos binarios, metadatos y etiquetas) para generar recursos en otros idiomas y utilizarlos en proyectos multilingües.

Para automatizar los flujos de trabajo de traducción, debe integrar los proveedores de servicios de traducción con [!DNL Experience Manager] y crear proyectos para traducir recursos a varios idiomas. [!DNL Experience Manager] admite flujos de trabajo de traducción automática y humana.

Traducción humana: Los recursos traducidos se devuelven e importan en [!DNL Experience Manager]. Cuando el proveedor de traducción está integrado con [!DNL Experience Manager], los recursos se envían automáticamente entre [!DNL Experience Manager] y el proveedor de traducción.

Traducción automática: El servicio de traducción automática traduce inmediatamente los metadatos y las etiquetas de los recursos.

La traducción de recursos incluye lo siguiente:

1. [Conectar Experience Manager con el proveedor de servicios de traducción](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Crear configuraciones del marco de integración de traducción](/help/sites-administering/tc-tic.md)
1. [Preparación de recursos para su traducción](preparing-assets-for-translation.md)
1. [Aplicar servicios de nube de traducción a carpetas](transition-cloud-services.md)
1. [Crear proyectos de traducción](translation-projects.md)

Si su proveedor de servicios de traducción no proporciona un conector con el que integrarse [!DNL Experience Manager], use una [proceso alternativo](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Consulte también [Creación de proyectos de traducción para fragmentos de contenido](creating-translation-projects-for-content-fragments.md).
