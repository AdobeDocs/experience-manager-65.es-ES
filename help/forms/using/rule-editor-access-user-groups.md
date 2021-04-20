---
title: Conceder acceso al editor de reglas a determinados grupos de usuarios
seo-title: Conceder acceso al editor de reglas a determinados grupos de usuarios
description: Conceder acceso restringido al editor de reglas a grupos de usuarios seleccionados.
seo-description: Conceder acceso restringido al editor de reglas a grupos de usuarios seleccionados.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 8%

---


# Conceder acceso al editor de reglas a determinados grupos de usuarios{#grant-rule-editor-access-to-select-user-groups}

## Información general {#overview}

Puede tener diferentes tipos de usuarios con diversas habilidades que trabajan con Adaptive Forms. Aunque los usuarios expertos pueden tener los conocimientos adecuados para trabajar con secuencias de comandos y reglas complejas, puede haber usuarios de nivel básico que solo necesiten trabajar con la presentación y las propiedades básicas de los formularios adaptables.

AEM Forms le permite limitar el acceso al editor de reglas a los usuarios en función de su función o función. En la configuración del Servicio de configuración de Forms adaptable, puede especificar los [grupos de usuarios](/help/sites-administering/security.md) que pueden ver y acceder al editor de reglas.

## Especificar grupos de usuarios que pueden acceder al editor de reglas {#specify-user-groups-that-can-access-rule-editor}

1. Inicie sesión en AEM Forms como administrador.
1. En la instancia de autor, haga clic en ![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Herramientas ![martillo](assets/hammer.png) > Operaciones > Consola web. La consola web se abre en una nueva ventana.

   ![1-2](assets/1-2.png)

1. En la ventana de la consola web, localice y haga clic en **[!UICONTROL Configuración del canal web del formulario adaptable y la comunicación interactiva]**. **[!UICONTROL Aparece el cuadro de diálogo]** Configuración del canal web de formularios adaptables y comunicaciones interactivas. No cambie ningún valor y haga clic en **Guardar**.

   Crea un archivo /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config en el repositorio CRX.

1. Inicie sesión en CRXDE como administrador. Abra el archivo /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config para editarlo.
1. Utilice la siguiente propiedad para especificar el nombre de un grupo que puede acceder al editor de reglas (por ejemplo, RuleEditorsUserGroup) y haga clic en **Guardar todo**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Para habilitar el acceso para varios grupos, especifique una lista de valores separados por comas:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Crear usuario](assets/create_user_new.png)

   Ahora, cuando un usuario que no forma parte de un grupo de usuarios especificado (en este caso RuleEditorsUserGroup) toca un campo, el icono Editar regla ( ![edit-rules1](assets/edit-rules1.png)) no está disponible para él en la barra de herramientas de componentes:

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   Barra de herramientas de componentes visible para un usuario con acceso al editor de reglas

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   Barra de herramientas de componentes visible para el usuario sin acceso al editor de reglas

   Para obtener instrucciones sobre cómo agregar usuarios a grupos, consulte [Administración de usuarios y seguridad](/help/sites-administering/security.md).

