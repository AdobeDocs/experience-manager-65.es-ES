---
title: Configuración de la caché de formularios adaptables
seo-title: Configuración de la caché de formularios adaptables
description: 'La caché de formularios adaptables está diseñada específicamente para formularios y documentos adaptables. Almacena en caché formularios adaptables y documentos adaptables con el objetivo de reducir el tiempo necesario para presentar un formulario o documento adaptable en el cliente. '
seo-description: 'La caché de formularios adaptables está diseñada específicamente para formularios y documentos adaptables. Almacena en caché formularios adaptables y documentos adaptables con el objetivo de reducir el tiempo necesario para presentar un formulario o documento adaptable en el cliente. '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# Configuración de la caché de formularios adaptables{#configure-adaptive-forms-cache}

Una caché es un mecanismo para reducir los tiempos de acceso a los datos, reducir la latencia y mejorar las velocidades de entrada y salida (E/S). La caché de formularios adaptables almacena solo el contenido HTML y la estructura JSON de un formulario adaptable sin guardar datos precargados. Ayuda a reducir el tiempo necesario para procesar un formulario o documento adaptable en el cliente. Está diseñado específicamente para formularios adaptables y también admite documentos adaptables.

>[!NOTE]
>
>Cuando utilice la caché de formularios adaptables, utilice AEM Dispatcher para almacenar en caché las bibliotecas de cliente (CSS y JavaScript) de un formulario o documento adaptable.

>[!NOTE]
>
>Al desarrollar componentes personalizados, en el servidor utilizado para el desarrollo, mantenga deshabilitada la caché de formularios adaptables.

## Configurar la caché {#configure-the-cache}

Realice los siguientes pasos para configurar la caché de formularios adaptables:

1. Vaya al administrador de configuración de la consola web de AEM en https://[server]:[port]/system/console/configMgr.
1. Haga clic en Configuración **de canal web de comunicación interactiva y formulario** adaptable para editar sus valores de configuración.
1. En el cuadro de diálogo Editar valores de configuración, especifique el número máximo de formularios o documentos que una instancia del servidor de AEM Forms puede almacenar en caché en el campo **Número de formularios** adaptables. El valor predeterminado es 100.

   >[!NOTE]
   >
   >Para deshabilitar la caché, establezca el valor en **0** en el campo Número de formularios adaptables. La caché se restablece y todos los formularios y documentos se eliminan de la caché cuando se deshabilita o cambia la configuración de la caché.

   ![Cuadro de diálogo de configuración para la caché HTML de formularios adaptables](assets/cache-configuration-edit.png)

1. Click **Save** to save the configuration.

