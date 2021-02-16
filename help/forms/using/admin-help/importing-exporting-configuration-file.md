---
title: Importación y exportación del archivo de configuración
seo-title: Importación y exportación del archivo de configuración
description: Obtenga información sobre cómo importar y exportar el archivo de configuración para editar las preferencias del servidor o configurar otra instancia de producto de AEM formularios.
seo-description: Obtenga información sobre cómo importar y exportar el archivo de configuración para editar las preferencias del servidor o configurar otra instancia de producto de AEM formularios.
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Importación y exportación del archivo de configuración {#importing-and-exporting-the-configuration-file}

Utilice la página Configuración manual para descargar una copia de la configuración en formato XML. La configuración de este archivo controla todas las preferencias del servidor. A continuación, puede editar el archivo y volverlo a cargar en el servidor. También puede utilizar el archivo para configurar otra instancia de producto de AEM formularios.

Para evitar riesgos de seguridad, el valor de la contraseña de enlace para el servidor de directorio no se incluye en un archivo de configuración exportado. Actualice la contraseña en el archivo XML antes de importar el archivo a un nuevo sistema.

>[!NOTE]
>
>La importación del archivo de configuración reconfigura AEM formularios en función de la información del archivo. Sólo un administrador del sistema o un consultor de servicios profesionales que esté familiarizado con el producto de formularios AEM y XML debe considerar la posibilidad de modificar el archivo de configuración. Es posible que necesiten editar el archivo de configuración, por ejemplo, para volver a configurar una configuración dañada.

**Exportar la información de configuración**

1. En la Consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Exportar. Si utiliza Microsoft Internet Explorer, se le pedirá que especifique una ubicación para guardar el archivo. Si utiliza Firefox, el archivo se guarda en el escritorio.

**Importar la información de configuración**

1. En la Consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Examinar para buscar el archivo de configuración, haga clic en Importar y, a continuación, en Aceptar.

