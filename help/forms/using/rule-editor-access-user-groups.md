---
title: Conceder acceso al editor de reglas a determinados grupos de usuarios
seo-title: Conceder acceso al editor de reglas a determinados grupos de usuarios
description: Conceder acceso restringido al editor de reglas para seleccionar grupos de usuarios.
seo-description: Conceder acceso restringido al editor de reglas para seleccionar grupos de usuarios.
uuid: efa2570a-20ac-4b43-8a0e-38247f84d02f
content-type: reference
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab694a93-00d2-44d7-8ded-68ab2ad50693
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Conceder acceso al editor de reglas a determinados grupos de usuarios{#grant-rule-editor-access-to-select-user-groups}

## Información general {#overview}

Es posible que tenga diferentes tipos de usuarios con diversas habilidades que trabajen con formularios adaptables. Aunque los usuarios expertos pueden tener los conocimientos adecuados para trabajar con secuencias de comandos y reglas complejas, puede haber usuarios de nivel básico que solo necesiten trabajar con la presentación y las propiedades básicas de los formularios adaptables.

AEM Forms permite limitar el acceso del editor de reglas a los usuarios en función de su función o función. En la configuración del servicio de configuración de formularios adaptables, puede especificar los grupos [de](/help/sites-administering/security.md) usuarios que pueden ver el editor de reglas y acceder a él.

## Especificar grupos de usuarios que pueden acceder al editor de reglas {#specify-user-groups-that-can-access-rule-editor}

1. Inicie sesión en AEM Forms como administrador.
1. En la instancia de autor, haga clic en ![](assets/adobeexperiencemanager.png)adobeexperimentencemanagerAdobe Experience Manager > ![Martillo](assets/hammer.png) de herramientas > Operaciones > Consola web. La consola web se abre en una ventana nueva.

   ![1-2](assets/1-2.png)

1. En la ventana de la consola web, ubique y haga clic en Servicio **** de configuración de formulario adaptable. **Aparece el cuadro de diálogo Servicio** de configuración de formulario adaptable. No cambie ningún valor y haga clic en **Guardar**.

   Crea un archivo /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config en el repositorio de CRX.

1. Inicie sesión en CRXDE como administrador. Abra el archivo /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config para editarlo.
1. Utilice la siguiente propiedad para especificar el nombre de un grupo que puede acceder al editor de reglas (por ejemplo, RuleEditorsUserGroup) y haga clic en **Guardar todo**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Para habilitar el acceso para varios grupos, especifique una lista de valores separados por comas:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Crear usuario](assets/create_user_new.png)

   Ahora, cuando un usuario que no forma parte de un grupo de usuarios especificado (aquí RuleEditorsUserGroup) toca un campo, el icono Editar regla ( ![edit-rules1](assets/edit-rules1.png)) no está disponible para él en la barra de herramientas de componentes:

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   Barra de herramientas de componentes visible para un usuario con acceso al editor de reglas

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   Barra de herramientas de componentes visible para un usuario sin acceso al editor de reglas

   Para obtener instrucciones sobre cómo agregar usuarios a grupos, consulte Administración [de usuarios y seguridad](/help/sites-administering/security.md).

