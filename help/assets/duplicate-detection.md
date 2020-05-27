---
title: Habilitar la detección de recursos de duplicado
description: Obtenga información sobre cómo activar la detección de recursos de duplicado en Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# Habilitar la detección de recursos de duplicado {#enable-detection-of-duplicate-assets}

Si intenta cargar un recurso que existe en Recursos Adobe Experience Manager, la función de detección de duplicados lo identifica como duplicado. La detección de Duplicados está deshabilitada de forma predeterminada. Para habilitar la función, realice los siguientes pasos:

1. Para abrir la página de configuración de la consola web de Experience Manager, acceda a `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite la configuración del servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Seleccione la opción **[!UICONTROL Detectar duplicado]** y haga clic en **[!UICONTROL Guardar]**.

   ![Seleccione la opción Detectar duplicado en el servlet](assets/chlimage_1-377.png)

   *Figura: Seleccione la opción Detectar duplicado en el servlet*

La función de detección de duplicado ahora está activada en Recursos. Cuando un usuario intenta cargar un recurso que existe en Experience Manager, el sistema comprueba si hay conflictos y lo indica. Los recursos se identifican mediante hash SHA-1 almacenado en `jcr:content/metadata/dam:sha1`, lo que significa que se detectan los recursos de duplicado independientemente de los nombres de archivo.

>[!MORELIKETHIS]
>
>* [Duplicado de recursos en un repositorio existente (un tutorial de un miembro de la comunidad)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

