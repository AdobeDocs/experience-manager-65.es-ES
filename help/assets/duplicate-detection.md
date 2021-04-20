---
title: Habilitar la detección de recursos duplicados
description: Obtenga información sobre cómo habilitar la detección de recursos duplicados en Experience Manager.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Asset Management,Asset Reports
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Habilitar la detección de activos duplicados {#enable-detection-of-duplicate-assets}

Si intenta cargar un recurso que existe en [!DNL Adobe Experience Manager Assets], la función de detección de duplicados lo identificará como duplicado. La detección de duplicados está deshabilitada de forma predeterminada. Para habilitar la función, siga estos pasos:

1. Abra la página de configuración de la Consola Web [!DNL Experience Manager] accediendo a `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite la configuración del servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Seleccione la opción **[!UICONTROL detect duplicate]** y haga clic en **[!UICONTROL Save]**.

   ![Seleccione la opción Detectar duplicado en el servlet](assets/chlimage_1-377.png)

   *Figura: Seleccione la opción Detectar duplicado en el servlet.*

La función Detectar duplicado ahora está habilitada en [!DNL Assets]. Cuando un usuario intenta cargar un recurso que existe en [!DNL Experience Manager], el sistema comprueba si hay conflicto e lo indica. Los recursos se identifican utilizando el hash SHA-1 almacenado en `jcr:content/metadata/dam:sha1`, lo que significa que se detectan activos duplicados independientemente de los nombres de archivo.

>[!MORELIKETHIS]
>
>* [Duplicar recursos en un repositorio existente (un tutorial de un miembro de la comunidad)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

