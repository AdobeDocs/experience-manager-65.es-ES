---
title: Eliminación de los sitios de Geometrixx
description: Obtenga información sobre cómo eliminar el contenido de la Geometrixx de ejemplo.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Eliminación de los sitios de Geometrixx{#removing-the-geometrixx-sites}

AEM viene con un conjunto de sitios web de Geometrixx de ejemplo. Puede quitar este contenido de muestra mediante el **Administrador de paquetes**.

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

Para quitar un paquete individual, simplemente haga clic en **Desinstalar** en ese paquete.

También hay un súper paquete:

* `cq-geometrixx-all-pkg-5.6.12.zip`

Este paquete incluye todos los paquetes individuales anteriores. Para quitar todo el contenido relacionado con geometrixx a la vez, haz clic en **Desinstalar** en este paquete. El superpaquete pasa al estado desinstalado y todos los paquetes individuales desaparecen de la vista del Administrador de paquetes.

AEM Ahora tiene una instancia de &quot;vaciado&quot; sin ningún sitio de demostración.

>[!NOTE]
>
>Al actualizar, los sitios de Geometrixx se reinstalan automáticamente. Elimine los sitios web de Geometrixx después de la actualización si no desea estos ejemplos.

