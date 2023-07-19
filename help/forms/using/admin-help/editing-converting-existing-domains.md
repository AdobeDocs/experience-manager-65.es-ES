---
title: Editar y convertir dominios existentes
seo-title: Editing and converting existing domains
description: Aprenda a cambiar la configuración de los dominios existentes desde la página Administración de dominios. Convertir un dominio de empresa existente en un dominio híbrido o a la inversa.
seo-description: Learn how to change the settings for existing domains from the Domain Management page. Convert an existing enterprise domain to a hybrid domain or conversely.
uuid: 4cc9547e-b4ec-4588-b1cf-18720f06149a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 44dec184-3ef7-4ba6-a87f-ad171d3cb188
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# Editar y convertir dominios existentes{#editing-and-converting-existing-domains}

Puede cambiar la configuración de los dominios existentes desde la página Administración de dominios. También puede convertir un dominio de empresa existente en un dominio híbrido.

## Editar un dominio existente {#edit-an-existing-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el nombre del dominio que desea editar.
1. Para cambiar el nombre de dominio, cambie el texto en el cuadro Nombre.
1. Para cambiar la información de autenticación de un dominio híbrido o empresarial, haga clic en el nombre de autenticación correspondiente en la parte inferior de la página. En la página Editar autenticación, cambie la configuración según sea necesario. (Consulte [Configuración de autenticación](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Para cambiar la información de directorio de un dominio de empresa, haga clic en el nombre de directorio correspondiente en la parte inferior de la página. En la página Editar directorio, cambie la configuración según sea necesario. (Consulte [Adición de directorios o SPI personalizados](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Cuando haya completado los cambios, haga clic en Aceptar.

## Conversión de un dominio de empresa en un dominio híbrido {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el nombre del dominio de empresa que desea convertir.
1. Haga clic en Convertir en dominio híbrido.
1. Revise la información que aparece con respecto a los datos de usuarios y grupos y la autenticación de usuarios, y haga clic en Aceptar.
1. Edite la configuración del dominio híbrido y haga clic en Aceptar.

>[!NOTE]
>
>Si el dominio de empresa que está convirtiendo no contiene la configuración de directorio, se perderá la configuración de autenticación LDAP.

## Conversión de un dominio híbrido en un dominio de empresa {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el nombre del dominio híbrido que desea convertir.
1. Haga clic en Convertir a dominio de empresa.
1. Revise la información que aparece con respecto a los datos de usuarios y grupos y la autenticación de usuarios, y haga clic en Aceptar.
1. Haga clic en Agregar directorio y configure la información de directorio necesaria. (Consulte [Adición de directorios o SPI personalizados](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
