---
title: Habilitar la detección de recursos de duplicado
description: Obtenga información sobre cómo activar la detección de recursos de duplicado en AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Habilitar la detección de recursos de duplicado {#enable-detection-of-duplicate-assets}

Si intenta cargar un recurso que existe en Recursos Adobe Experience Manager (AEM), la función de detección de duplicado lo identifica como duplicado. La detección de Duplicados está deshabilitada de forma predeterminada. Para habilitar la función, realice los siguientes pasos:

1. Abra la página Configuración de la consola web de AEM accediendo a `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite la configuración del servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Seleccione la opción **[!UICONTROL Detectar duplicado]** y haga clic en **[!UICONTROL Guardar]**.

   ![Seleccione la opción Detectar duplicado en el servlet](assets/chlimage_1-377.png)

   *Figura: Seleccione la opción Detectar duplicado en el servlet*

La función de detección de duplicados ahora está activada en Recursos AEM. Cuando un usuario intenta cargar un recurso que existe en AEM, el sistema comprueba si hay conflictos e indica que hay conflictos. Los recursos se identifican mediante hash SHA-1 almacenado en `jcr:content/metadata/dam:sha1`, lo que significa que se detectan los recursos de duplicado independientemente de los nombres de archivo.

>[!MORELIKETHIS]
>
>* [Duplicado de recursos en un repositorio existente (un tutorial de un miembro de la comunidad)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

