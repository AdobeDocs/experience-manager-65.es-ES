---
title: Especificar ubicaciones de archivos para la salida
description: Obtenga información sobre cómo especificar ubicaciones de archivos para la salida para determinados tipos de archivos, por ejemplo, URI raíz de contenido, archivo de configuración XCI, caché y predeterminado.
uuid: 3287274f-85b5-4811-8abb-d347a9b80947
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 460bbb31-8187-469c-8102-b310093b6c03
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 5%

---

# Especificar ubicaciones de archivos para la salida {#specify-file-locations-for-output}

Puede especificar las ubicaciones en las que Output busca determinados tipos de archivos que necesita.

1. En la consola de administración, haga clic en Servicios > Resultados.
1. En Ubicaciones, especifique las opciones adecuadas.
1. Haga clic en Guardar.

## Configuración de ubicaciones {#locations-settings}

**URI de raíz de contenido:** URI o ubicación absoluta del repositorio desde el que se recuperan los formularios. Este valor se combina con el parámetro sForm, especificado mediante la API, para construir la ruta absoluta al formulario que se recupera. Este valor puede hacer referencia a un directorio o a una ubicación web a la que se puede acceder mediante HTTP.

El valor predeterminado es una cadena vacía.

**Archivo de configuración XCI:** La ubicación relativa o absoluta del archivo de configuración XCI que el servicio Output utiliza para el procesamiento. AEM Para un valor relativo, se da por hecho que el archivo XCI reside en el archivo EAR implementable de formularios en el que se puede implementar el formulario de la.

El valor predeterminado es `com/adobe/formServer/PA/pa_output.xci`.

**Ubicación de caché:** Especifica la ubicación de la caché del disco de salida. Al cambiar esta configuración, se restablece toda la información de caché existente de la ubicación actual y se crea una nueva caché en la nueva ubicación. Seleccione una de las siguientes opciones:

**Ubicación predeterminada:** Esta es la selección predeterminada. Cuando se selecciona esta opción, la caché se crea en una ubicación que depende del servidor de aplicaciones que esté utilizando:

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[forms server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**Directorio temporal de LC:** AEM La caché se crea en un subdirectorio del directorio temporal de los formularios de la, que se especifica en la consola de administración en Configuración > Configuración del sistema principal > Configuraciones > Ubicación del directorio temporal. El nombre del subdirectorio es `adobeoutput_[servername]`.

>[!NOTE]
>
>Si utiliza una utilidad de limpieza temporal, tenga en cuenta que, aunque la eliminación de estos directorios no afecta a la funcionalidad, puede afectar significativamente al rendimiento durante un corto tiempo, hasta que se cree la nueva caché. AEM Para evitar este problema, no elimine estos directorios mientras borra el directorio temporal de los formularios de la.
