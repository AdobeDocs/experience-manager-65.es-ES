---
title: Edición y conversión de dominios existentes
seo-title: Edición y conversión de dominios existentes
description: Obtenga información sobre cómo cambiar la configuración de los dominios existentes desde la página Administración de dominios. Convierta un dominio empresarial existente en un dominio híbrido o viceversa.
seo-description: Obtenga información sobre cómo cambiar la configuración de los dominios existentes desde la página Administración de dominios. Convierta un dominio empresarial existente en un dominio híbrido o viceversa.
uuid: 4cc9547e-b4ec-4588-b1cf-18720f06149a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 44dec184-3ef7-4ba6-a87f-ad171d3cb188
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Edición y conversión de dominios existentes{#editing-and-converting-existing-domains}

Puede cambiar la configuración de los dominios existentes desde la página Administración de dominios. También puede convertir un dominio empresarial existente en un dominio híbrido.

## Editar un dominio existente {#edit-an-existing-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el nombre del dominio que desea editar.
1. Para cambiar el nombre de dominio, cambie el texto en el cuadro Nombre.
1. Para cambiar la información de autenticación de un dominio empresarial o híbrido, haga clic en el nombre de autenticación correspondiente en la parte inferior de la página. En la página Editar autenticación, cambie la configuración según sea necesario. (Consulte Configuración [de autenticación](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)).
1. Para cambiar la información de directorio de un dominio de empresa, haga clic en el nombre de directorio correspondiente en la parte inferior de la página. En la página Editar directorio, cambie la configuración según sea necesario. (Consulte [Adición de directorios o SPIs](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)personalizados).
1. Cuando complete los cambios, haga clic en Aceptar.

## Convertir un dominio de empresa en un dominio híbrido {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el nombre del dominio de empresa que desea convertir.
1. Haga clic en Convertir a dominio híbrido.
1. Revise la información que aparece sobre los datos de usuarios y grupos y la autenticación de usuarios, y haga clic en Aceptar.
1. Edite la configuración del dominio híbrido y haga clic en Aceptar.

>[!NOTE]
>
>Si el dominio de empresa que está convirtiendo no contiene la configuración de directorio, se perderá cualquier configuración de autenticación LDAP.

## Convertir un dominio híbrido en un dominio de empresa {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el nombre del dominio híbrido que desea convertir.
1. Haga clic en Convertir a dominio empresarial.
1. Revise la información que aparece sobre los datos de usuarios y grupos y la autenticación de usuarios, y haga clic en Aceptar.
1. Haga clic en Agregar directorio y configure la información de directorio requerida. (Consulte [Adición de directorios o SPIs](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)personalizados).

