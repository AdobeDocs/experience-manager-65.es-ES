---
title: Importación y exportación del archivo de configuración
seo-title: Importing and exporting the configuration file
description: Obtenga información sobre cómo importar y exportar el archivo de configuración para editar las preferencias del servidor o configurar otra instancia de producto de AEM forms.
seo-description: Learn how to import and export the configuration file in order to edit server preferences or configure another AEM forms product instance.
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Importación y exportación del archivo de configuración {#importing-and-exporting-the-configuration-file}

Utilice la página Configuración manual para descargar una copia de los ajustes de configuración en formato XML. La configuración de este archivo controla todas las preferencias del servidor. A continuación, puede editar el archivo y cargarlo de nuevo en el servidor. También puede utilizar el archivo para configurar otra instancia de producto de AEM forms.

Para evitar riesgos de seguridad, el valor de la contraseña de enlace del servidor de directorios no se incluye en un archivo de configuración exportado. Actualice la contraseña en el archivo XML antes de importar el archivo en un nuevo sistema.

>[!NOTE]
>
>La importación del archivo de configuración reconfigura AEM formularios en función de la información del archivo. Solo un administrador del sistema o un consultor de servicios profesional familiarizado con el producto de formularios AEM y XML deben considerar la posibilidad de modificar el archivo de configuración. Es posible que tengan que editar el archivo de configuración, por ejemplo, para reconfigurar una configuración dañada.

**Exportar la información de configuración**

1. En la Consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Exportar. Si utiliza Microsoft Internet Explorer, se le pedirá que especifique una ubicación para guardar el archivo. Si utiliza Firefox, el archivo se guarda en el escritorio.

**Importación de la información de configuración**

1. En la Consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Examinar para buscar el archivo de configuración, haga clic en Importar y, a continuación, haga clic en Aceptar.
