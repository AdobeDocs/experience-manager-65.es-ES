---
title: Habilitar la alternancia de funciones para integrar las funciones de pionero y prelanzamiento
description: La alternancia de funciones es una funcionalidad de AEM que permite a los administradores habilitar nuevas funciones en un entorno de tiempo de ejecución.
feature: Adaptive Forms, Foundation Components
role: User, Developer
hidefromtoc: true
exl-id: 08815c2b-23b3-4545-a3ab-ba47ba1c3c55
source-git-commit: 0915f8a65b1a9697eaca95be3ef9a786a1071fe5
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 6%

---

# Alternancia de funciones en Adobe Experience Manager (AEM) 6.5{#enable-feature-toggle-aem-forms-65}

La alternancia de funciones es una funcionalidad de AEM que permite a los administradores habilitar o deshabilitar funciones específicas de forma dinámica. Esta funcionalidad es especialmente útil para administrar **las características de los primeros usuarios** y **las características de la versión preliminar** sin que sea necesario realizar implementaciones o cambios importantes en la base de código. Garantiza flexibilidad y control sobre las funciones accesibles en un entorno de AEM.

## ¿Por qué utilizar las alternancias de funciones en una configuración de AEM 6.5?

Al trabajar con una configuración de AEM 6.5, la función activa o desactiva la ayuda en lo siguiente:

* Prueba de características experimentales de forma segura.

* Despliegue de nuevos componentes por fases.

* Mantener un único código base en varios entornos.

* Reducción del riesgo durante las implementaciones y actualizaciones.

## Consideración

A partir de AEM 6.5 SP23, no es necesario realizar los pasos de Requisitos previos, ya que el paquete [com.adobe.granite.toggle.impl.dev](http://com.adobe.granite.toggle.impl.dev/) ya está instalado con el complemento de Forms.

## Requisitos previos

Antes de habilitar los conmutadores de funciones en la configuración de AEM 6.5, asegúrese de lo siguiente:

* El usuario es miembro del grupo `forms-users`.

* Vaya a `http://<author-instance-url>:portnumber/system/console/bundles` y compruebe si el paquete **(com.adobe.granite.toggle.impl.dev-1.1.8.jar)** está presente o no. En caso de que no esté presente, [descargue el paquete desde el vínculo](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fcom.adobe.granite.toggle.impl.dev-1.1.8.jar).

![Alternar característica](/help/forms/using/assets/feature-toggle-1.1.8.png)

## Activar conmutador de función {#enable-feature-toggle-65}

Se pueden configurar cambios de características para los usuarios que las adoptaron por primera vez o nuevas características a través de la **consola web de AEM** siguiendo los pasos a continuación:

1. Inicie sesión en la instancia de AEM Forms.
2. Navegue hasta `http://<author-instance-url>:portnumber/system/console/configMgr`.
3. Busque **Proveedor de alternancia dinámica de Adobe Granite** en el Administrador de configuración.
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
3. Busque **Proveedor de alternancia dinámica de Adobe Granite** en el Administrador de configuración.
4. Haga clic en el icono ![icono-lápiz](assets/illustratorcc_penciltool_cur_edit_2_17.png).
5. En la sección [!UICONTROL Conmutadores deshabilitados], haga clic en ![icono de lápiz](assets/aem6forms_add.png).
6. Añada el número de conmutador para que la función se desactive.
   ![Quitar alternancia](assets/remove_toggle_feature_forms.png)
7. Haga clic en Guardar.

## Consideración técnica

Las alternancias de funciones son específicas del entorno y se administran durante la ejecución, por lo que no requieren el reinicio del servidor. Sin embargo, algunas funciones pueden requerir la actualización de las páginas relevantes o la limpieza de la caché para reflejar los cambios.
Puede acceder a la lista de características habilitadas mediante la alternancia de características para su entorno mediante `http://<author-instance-url>:4502/etc.clientlibs/toggles.json`.
