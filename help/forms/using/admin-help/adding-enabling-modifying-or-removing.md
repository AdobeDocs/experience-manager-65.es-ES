---
title: Adición, activación, modificación o eliminación de puntos finales
seo-title: Adding, enabling, modifying, or removing endpoints
description: Aprenda a añadir, habilitar, modificar y eliminar puntos finales.
seo-description: Learn how to add, enable, modify and remove endpoints.
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Adición, activación, modificación o eliminación de puntos finales {#adding-enabling-modifying-or-removing-endpoints}

## Añadir un extremo a un servicio {#add-an-endpoint-to-a-service}

Los puntos de conexión solo se pueden agregar a servicios. Un punto final no puede existir solo; debe estar asociado a un servicio.

>[!NOTE]
>
>Se recomienda utilizar nombres únicos al añadir extremos.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios , haga clic en el servicio para configurarlo.
1. En la lista de la ficha Extremos , seleccione el tipo de extremo que desea agregar y haga clic en Agregar.
1. Dependiendo del tipo de extremo, configure ajustes de extremo adicionales.

[Configuración de extremo de carpeta vigilada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[Configuración de extremo de correo electrónico](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[Configuración de los extremos del Administrador de tareas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[Configuración de extremo remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. Haga clic en Agregar.

## Habilitar o deshabilitar un punto final {#enable-or-disable-an-endpoint}

De forma predeterminada, los nuevos extremos se activan automáticamente. Pero si ha deshabilitado un punto final, tendrá que habilitarlo para que funcione.

Si tiene problemas con los servicios, deshabilite los extremos asociados para solucionar mejor el problema. También es posible que desee deshabilitar los extremos durante el mantenimiento regular del sistema o al actualizar un servicio.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de extremos.
1. En la página Administración de puntos de conexión, active la casilla de verificación del punto final para habilitar o deshabilitar y haga clic en Habilitar o Deshabilitar.

## Modificación de un punto final {#modify-an-endpoint}

>[!NOTE]
>
>Los cambios que realice en una configuración de extremo mediante la consola de administración no se reflejarán en las copias en tiempo de diseño de las aplicaciones. Si vuelve a implementar una aplicación, se perderá cualquier cambio que haya realizado en sus puntos finales mediante la consola de administración.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de extremos.
1. En la página Administración de puntos finales , haga clic en el punto final para modificarlo.
1. En la página Actualizar extremo , modifique el nombre del extremo, la descripción y la configuración.

   >[!NOTE]
   >
   >No incluya un carácter &lt; en el nombre o la descripción porque truncará el nombre o la descripción mostrados en Workspace.

1. Para guardar los cambios, haga clic en Actualizar.

También puede realizar esta tarea desde la página Administración de servicios seleccionando un servicio y luego haciendo clic en la pestaña Puntos de conexión .

## Eliminar un punto final {#remove-an-endpoint}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de extremos.
1. En la página Administración de puntos de conexión, active la casilla de verificación del punto final que desea eliminar y haga clic en Quitar. El punto final ya no se muestra.
