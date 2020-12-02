---
title: Eliminación de sitios de Geometrixx
seo-title: Eliminación de sitios de Geometrixx
description: Obtenga información sobre cómo eliminar el contenido de muestra de Geometrixx.
seo-description: Obtenga información sobre cómo eliminar el contenido de muestra de Geometrixx.
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Eliminación de sitios de Geometrixx{#removing-the-geometrixx-sites}

AEM incluye un conjunto de sitios web de muestra de Geometrixx. Puede eliminar este contenido de muestra a través del **Administrador de paquetes**.

Los paquetes individuales relacionados con geometrixx son:

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

Para eliminar un paquete individual, haga clic en **Desinstalar** en ese paquete.

También hay un súper paquete:

* `cq-geometrixx-all-pkg-5.6.12.zip`

Este paquete incluye todos los paquetes individuales anteriores. Para eliminar todo el contenido relacionado con geometrixx a la vez, haga clic en **Desinstalar** en este paquete. El súper-paquete pasará al estado desinstalado, y todos los paquetes individuales desaparecerán de la vista del administrador de paquetes.

Ahora tiene una instancia de AEM &quot;vacía&quot; sin ningún sitio de demostración.

>[!NOTE]
>
>Al actualizar, los sitios de geometrixx se vuelven a instalar automáticamente. Es posible que tenga que eliminar los sitios web de geometrixx después de la actualización si no desea estos ejemplos.

