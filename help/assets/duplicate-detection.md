---
title: Habilitar la detección de recursos duplicados
description: Obtenga información sobre cómo habilitar la detección de recursos duplicados en Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Habilitar la detección de recursos duplicados {#enable-detection-of-duplicate-assets}

Si intenta cargar un recurso que existe en [!DNL Adobe Experience Manager Assets], la función de detección de duplicados la identifica como duplicada. La detección de duplicados está desactivada de forma predeterminada. Para habilitar la función, siga estos pasos:

1. Abra el [!DNL Experience Manager] página de configuración de la consola web accediendo a `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite la configuración del servlet **[!UICONTROL Crear recurso de CQ DAM del día]**.
1. Seleccione el **[!UICONTROL detectar duplicados]** y haga clic en **[!UICONTROL Guardar]**.

   ![Seleccione la opción detectar duplicados en el servlet](assets/chlimage_1-377.png)

   *Imagen: seleccione la opción detectar duplicados en el servlet.*

La función de detección de duplicados ahora está habilitada en [!DNL Assets]. Cuando un usuario intenta cargar un recurso que existe en [!DNL Experience Manager], el sistema comprueba la existencia de conflictos y lo indica. Los recursos se identifican mediante un hash SHA-1 almacenado en `jcr:content/metadata/dam:sha1`, lo que significa que se detectan recursos duplicados independientemente de los nombres de archivo.

>[!MORELIKETHIS]
>
>* [Activos duplicados en el repositorio existente (un tutorial de un miembro de la comunidad)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [AEM Detección de recursos duplicados en la as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html)
