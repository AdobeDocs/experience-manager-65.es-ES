---
title: Habilitar la detección de recursos duplicados
description: Obtenga información sobre cómo habilitar la detección de recursos duplicados en Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# Habilitar la detección de recursos duplicados {#enable-detection-of-duplicate-assets}

Si intenta cargar un recurso que exista en [!DNL Adobe Experience Manager Assets], la función de detección de duplicados la identifica como duplicada. La detección de duplicados está deshabilitada de forma predeterminada. Para habilitar la función, siga estos pasos:

1. Abra el [!DNL Experience Manager] página de configuración de la consola web accediendo a `https://[aem_server]:[port]/system/console/configMgr`.
1. Editar la configuración del servlet **[!UICONTROL Recurso de creación de DAM CQ de día]**.
1. Seleccione el **[!UICONTROL detectar duplicado]** y haga clic en **[!UICONTROL Guardar]**.

   ![Seleccione la opción Detectar duplicado en el servlet](assets/chlimage_1-377.png)

   *Figura: Seleccione la opción Detectar duplicado en el servlet.*

La función Detectar duplicado está ahora habilitada en [!DNL Assets]. Cuando un usuario intenta cargar un recurso que existe en [!DNL Experience Manager], el sistema comprueba si hay conflicto y lo indica. Los recursos se identifican utilizando el hash SHA-1 almacenado en `jcr:content/metadata/dam:sha1`, lo que significa que los recursos duplicados se detectan independientemente de los nombres de archivo.

>[!MORELIKETHIS]
>
>* [Duplicar recursos en un repositorio existente (un tutorial de un miembro de la comunidad)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

