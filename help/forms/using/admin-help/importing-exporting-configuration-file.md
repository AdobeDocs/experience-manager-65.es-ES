---
title: Importar y exportar archivos de configuración
description: AEM Obtenga información sobre cómo importar y exportar el archivo de configuración para editar las preferencias del servidor o configurar otra instancia de producto de formularios en la que se puede usar la plantilla de formularios de.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 4%

---

# Importar y exportar archivos de configuración {#importing-and-exporting-the-configuration-file}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Utilice la página Configuración Manual para descargar una copia de los ajustes de configuración en formato XML. La configuración de este archivo controla todas las preferencias del servidor. A continuación, puede editar el archivo y cargarlo de nuevo en el servidor. AEM También puede utilizar el archivo para configurar otra instancia de producto de formularios en formato.

Para evitar riesgos de seguridad, el valor de la contraseña de enlace para el servidor de directorios no se incluye en un archivo de configuración exportado. Actualice la contraseña en el archivo XML antes de importar el archivo a un nuevo sistema.

>[!NOTE]
>
>AEM La importación del archivo de configuración vuelve a configurar formularios de datos en función de la información del archivo de configuración. AEM Solamente un administrador del sistema o un consultor de servicios profesionales familiarizado con el producto de formularios de la y el XML debe considerar la posibilidad de modificar el archivo de configuración. Es posible que tengan que editar el archivo de configuración, por ejemplo, para volver a configurar una configuración dañada.

**Exportar la información de configuración**

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Exportar. Si utiliza Microsoft Internet Explorer, se le pedirá que especifique una ubicación para guardar el archivo. Si utiliza Firefox, el archivo se guardará en el escritorio.

**Importar la información de configuración**

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Examinar para buscar el archivo de configuración, haga clic en Importar y, a continuación, haga clic en Aceptar.
