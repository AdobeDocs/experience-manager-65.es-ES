---
title: Habilitar la alternancia de funciones para integrar las funciones de pionero y prelanzamiento
description: AEM La opción de alternancia de funciones es una funcionalidad de la aplicación que permite a los administradores habilitar nuevas funciones en un entorno de tiempo de ejecución.
feature: Adaptive Forms, Foundation Components
role: User, Developer
hidefromtoc: true
source-git-commit: 794d93d890ba752f9036a85831f7cbc8391fb545
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 7%

---

# Alternancia de funciones en Adobe Experience Manager AEM () 6.5{#enable-feature-toggle-aem-forms-65}

AEM La opción de alternancia de funciones es una funcionalidad en la que los administradores pueden habilitar o deshabilitar de forma dinámica determinadas funciones. Esta funcionalidad es especialmente útil para administrar **las características de los primeros usuarios** y **las características de la versión preliminar** sin que sea necesario realizar implementaciones o cambios importantes en la base de código. AEM Garantiza la flexibilidad y el control sobre las funciones accesibles en un entorno de.

## Activar alternancia de función {#enable-feature-toggle-65}

AEM Se pueden configurar cambios de características para los usuarios que las adoptaron por primera vez o nuevas características a través de la **consola web de** siguiendo los pasos a continuación:

1. Inicie sesión en la instancia de AEM Forms.
2. Navegue hasta `http://<author-instance-url>:portnumber/system/console/configMgr`.
3. Busque **Adobe Granite Dynamic Toggle Provider** en el Administrador de configuración.
4. Haga clic en el icono ![icono-lápiz](assets/illustratorcc_penciltool_cur_edit_2_17.png).
5. En la sección [!UICONTROL Conmutadores habilitados], haga clic en ![icono de lápiz](assets/aem6forms_add.png).
6. Añada el ID de alternancia de función para la función como se muestra en la siguiente imagen.
   ![Agregar alternancia](assets/add_toggle_number_forms.png)

   >[!NOTE]
   >
   >Puede encontrar el ID de alternancia de funciones en el documento específico de las funciones que adoptaron por primera vez.

7. Haga clic en Guardar.

## Deshabilitar alternancia de funciones {#disable-feature-toggle-65}

Para desactivar las opciones de características para aquellas características cuyas opciones están activadas, siga los pasos a continuación:

1. Inicie sesión en la instancia de AEM Forms.
2. Navegue hasta `http://<author-instance-url>:portnumber/system/console/configMgr`.
3. Busque **Adobe Granite Dynamic Toggle Provider** en el Administrador de configuración.
4. Haga clic en el icono ![icono-lápiz](assets/illustratorcc_penciltool_cur_edit_2_17.png).
5. En la sección [!UICONTROL Conmutadores deshabilitados], haga clic en ![icono de lápiz](assets/aem6forms_add.png).
6. Añada el número de conmutador para que la función se desactive.
   ![Quitar alternancia](assets/remove_toggle_feature_forms.png)
7. Haga clic en Guardar.

## Consideración técnica

Las alternancias de funciones son específicas del entorno y se administran durante la ejecución, por lo que no requieren el reinicio del servidor. Sin embargo, algunas funciones pueden requerir la actualización de las páginas relevantes o la limpieza de la caché para reflejar los cambios.
Puede acceder a la lista de características habilitadas mediante la alternancia de características para su entorno mediante `http://<author-instance-url>:4502/etc.clientlibs/toggles.json`.