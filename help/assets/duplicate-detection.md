---
title: Habilitar la detección de recursos duplicados
description: Obtenga información sobre cómo activar la detección de recursos duplicados en AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 07c1a4102539ba4678c55dee3a4882101e39864f

---


# Habilitar la detección de recursos duplicados {#enable-detection-of-duplicate-assets}

Si intenta cargar un recurso que existe en Recursos Adobe Experience Manager (AEM), la función de detección de duplicados lo identificará como duplicado. La detección de duplicados está deshabilitada de forma predeterminada. Para habilitar la función, realice los siguientes pasos:

1. Abra la página Configuración de la consola web de AEM accediendo a `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite la configuración del servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Seleccione la opción **[!UICONTROL Detectar duplicados]** y toque o haga clic en **[!UICONTROL Guardar]**.

   ![Seleccione la opción detectar duplicados en el servlet](assets/chlimage_1-377.png)


   *Figura:Seleccione la opción detectar duplicados en el servlet*

La función de detección de duplicados ahora está activada en Recursos AEM. Cuando un usuario intenta cargar un recurso que existe en AEM, el sistema comprueba si hay conflictos e indica que hay conflictos. Los recursos se identifican mediante hash SHA-1 almacenado en `jcr:content/metadata/dam:sha1`, lo que significa que se detectan recursos duplicados independientemente de los nombres de archivo.

>[!MORELIKETHIS]
>
>* [Duplicar recursos en un repositorio existente (un tutorial de un miembro de la comunidad)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

