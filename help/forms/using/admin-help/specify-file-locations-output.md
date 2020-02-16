---
title: Especificar ubicaciones de archivos para Output
seo-title: Especificar ubicaciones de archivos para Output
description: Obtenga información sobre cómo especificar ubicaciones de archivos para Output.
seo-description: Obtenga información sobre cómo especificar ubicaciones de archivos para Output.
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Especificar ubicaciones de archivos para Output {#specify-file-locations-for-output}

Puede especificar las ubicaciones en las que Output busca determinados tipos de archivos que necesita.

1. En la consola de administración, haga clic en Servicios > salida.
1. En Ubicaciones, especifique las opciones correspondientes.
1. Haga clic en Guardar.

## Configuración de ubicaciones {#locations-settings}

**** URI de raíz de contenido: URI o ubicación absoluta del repositorio desde el que se recuperan los formularios. Este valor se combina con el parámetro sForm, especificado mediante la API, para construir la ruta absoluta al formulario que se recupera. Este valor puede hacer referencia a un directorio o a una ubicación web a la que se puede acceder mediante HTTP.

El valor predeterminado es una cadena vacía.

**** Archivo de configuración XCI: Ubicación relativa o absoluta del archivo de configuración XCI que utiliza el servicio Output para el procesamiento. Para un valor relativo, se supone que el archivo XCI reside en el archivo EAR implementable de formularios AEM.

El valor predeterminado es `com/adobe/formServer/PA/pa_output.xci`.

**** Ubicación de caché: Especifica la ubicación de la caché de disco de salida. Al cambiar esta configuración, se restablece toda la información de caché existente de la ubicación actual y se crea una nueva caché en la nueva ubicación. Seleccione una de las siguientes opciones:

**** Ubicación predeterminada: Ésta es la selección predeterminada. Cuando se selecciona esta opción, la caché se crea en una ubicación que depende del servidor de aplicaciones que esté utilizando:

* **** JBoss: `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **** WebLogic: `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[forms server name]\Output\Cache`
* **** WebSphere: `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**** Directorio temporal LC: La caché se crea en un subdirectorio del directorio temporal de formularios AEM, que se especifica en la consola de administración en Configuración > Configuración del sistema principal > Configuraciones > Ubicación del directorio temporal. El subdirectorio se denomina `adobeoutput_[servername]`.

>[!NOTE]
>
>Si está utilizando una utilidad de limpieza temporal, tenga en cuenta que si bien la eliminación de estos directorios no afecta a la funcionalidad, puede afectar significativamente al rendimiento durante un corto tiempo, hasta que se cree la nueva caché. Para evitar este problema, no elimine estos directorios mientras borra el directorio temporal de formularios AEM.

