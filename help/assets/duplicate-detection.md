---
title: Habilitar la detección de recursos duplicados
description: Obtenga información sobre cómo habilitar la detección de recursos duplicados en Experience Manager.
contentOwner: AG
role: User, Admin
feature: Administración de activos,Informes de activos
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Habilitar la detección de recursos duplicados {#enable-detection-of-duplicate-assets}

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

