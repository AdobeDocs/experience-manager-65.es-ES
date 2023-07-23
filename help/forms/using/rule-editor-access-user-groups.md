---
title: Conceder acceso al Editor de reglas a determinados grupos de usuarios
seo-title: Grant rule editor access to select user groups
description: Conceder acceso restringido al editor de reglas para seleccionar grupos de usuarios.
seo-description: Grant restricted access to rule editor to select user groups.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
feature: Adaptive Forms
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 86%

---

# Conceder acceso al Editor de reglas a determinados grupos de usuarios{#grant-rule-editor-access-to-select-user-groups}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo Forms adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [adición de Forms adaptable a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de Forms adaptable, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Forms adaptable mediante componentes de base. </span>

## Información general {#overview}

Existen diferentes tipos de usuarios con diversas aptitudes que trabajan con formularios adaptables. Aunque es posible que los usuarios expertos tengan los conocimientos necesarios para trabajar con scripts y reglas complejas, puede haber usuarios de nivel básico que únicamente necesiten trabajar con el diseño y las propiedades básicas de los formularios adaptables.

AEM Forms permite limitar el acceso de los usuarios al Editor de reglas en función de su rol o función. En los ajustes del servicio de configuración de los formularios adaptables, puede especificar los [grupos de usuarios](/help/sites-administering/security.md) que pueden ver y acceder al Editor de reglas.

## Especificar qué grupos de usuarios pueden acceder al Editor de reglas {#specify-user-groups-that-can-access-rule-editor}

1. Inicie sesión en AEM Forms como administrador.
1. En la instancia de autor, haga clic en ![adobeexperiencemanager](assets/adobeexperiencemanager.png) Adobe Experience Manager > Herramientas ![hammer](assets/hammer.png) > Operaciones > Consola web. La consola web se abre en una nueva ventana.

   ![1-2](assets/1-2.png)

1. En la ventana de la consola web, busque y haga clic en **[!UICONTROL Configuración del canal Web de comunicaciones interactivas y formularios adaptables]**. La **[!UICONTROL Configuración del canal Web de comunicaciones interactivas y formularios adaptables]** se abre. No cambie ningún valor y haga clic en **Guardar**.

   Crea el archivo /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config en el repositorio CRX.

1. Inicie sesión en CRXDE como administrador. Abra el archivo /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config para editarlo.
1. Utilice la siguiente propiedad para especificar el nombre de un grupo que puede acceder al Editor de reglas (por ejemplo, RuleEditorsUserGroup) y haga clic en **Guardar todo**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Para habilitar el acceso para varios grupos, especifique una lista de valores separados por comas:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Crear usuario](assets/create_user_new.png)

   Ahora, cuando un usuario que no forma parte del grupo de usuarios especificado (aquí RuleEditorsUserGroup) pulse un campo, el icono Editar regla ( ![edit-rules1](assets/edit-rules1.png)) no estará disponible en la barra de herramientas Componentes:

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   Barra de herramientas de componentes visible para un usuario con acceso al Editor de reglas

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   Barra de herramientas de componentes visible para un usuario sin acceso al Editor de reglas

   Para obtener instrucciones sobre cómo agregar usuarios a grupos, consulte [Administración de usuarios y seguridad](/help/sites-administering/security.md).
