---
title: Adición, activación, modificación o eliminación de puntos finales
seo-title: Adición, activación, modificación o eliminación de puntos finales
description: Obtenga información sobre cómo agregar, habilitar, modificar y eliminar puntos finales.
seo-description: Obtenga información sobre cómo agregar, habilitar, modificar y eliminar puntos finales.
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Adición, activación, modificación o eliminación de puntos finales {#adding-enabling-modifying-or-removing-endpoints}

## Agregar un extremo a un servicio {#add-an-endpoint-to-a-service}

Los extremos solo se pueden agregar a los servicios. Un punto final no puede existir solo; debe estar asociado a un servicio.

>[!NOTE]
>
>Se recomienda utilizar nombres únicos al agregar extremos.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en el servicio que desea configurar.
1. En la lista de la ficha Extremos, seleccione el tipo de extremo que desee agregar y haga clic en Agregar.
1. En función del tipo de extremo, configure parámetros de extremo adicionales.

   [Ajustes del extremo de la carpeta vigilada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

   [Configuración de extremo de correo electrónico](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

   [Configuración de los extremos del Administrador de tareas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

   [Configuración de punto final remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. Haga clic en Agregar.

## Habilitar o deshabilitar un punto final {#enable-or-disable-an-endpoint}

De forma predeterminada, los nuevos extremos se activan automáticamente. Pero si deshabilitó un punto final, deberá habilitarlo para que funcione.

Si tiene problemas con los servicios, deshabilite los extremos asociados para solucionar mejor el problema. También es posible que desee deshabilitar los extremos durante el mantenimiento regular del sistema o al actualizar un servicio.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de extremos.
1. En la página Administración de extremos, active la casilla de verificación del punto final que desea habilitar o deshabilitar y haga clic en Habilitar o Deshabilitar.

## Modificar un punto final {#modify-an-endpoint}

>[!NOTE]
>
>Los cambios realizados en una configuración de extremo mediante la consola de administración no se reflejan en las copias de las aplicaciones en tiempo de diseño. Si vuelve a implementar una aplicación, se perderá cualquier cambio que haya realizado en los extremos mediante la consola de administración.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de extremos.
1. En la página Administración de extremos, haga clic en el punto final que desee modificar.
1. En la página Actualizar extremo, modifique el nombre del extremo, la descripción y la configuración.

   >[!NOTE]
   >
   >No incluya un carácter &lt; en el nombre o la descripción porque truncará el nombre o la descripción mostrados en Workspace.

1. Para guardar los cambios, haga clic en Actualizar.

También puede realizar esta tarea desde la página Administración de servicios seleccionando un servicio y luego haciendo clic en la ficha Extremos.

## Eliminar un punto final {#remove-an-endpoint}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de extremos.
1. En la página Administración de extremos, active la casilla de verificación del punto final que desea eliminar y haga clic en Eliminar. El punto final ya no se muestra.

