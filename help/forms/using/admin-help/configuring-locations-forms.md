---
title: Configurar ubicaciones para Forms
description: AEM Obtenga información sobre cómo configurar la ubicación del formulario. Puede especificar las ubicaciones de archivo del atributo, la ubicación del formulario, el archivo del PDF semilla y la ubicación de la caché.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
source-git-commit: e2a3470784beb04c2179958ac6cb98861acfaa71
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 2%

---

# Configurar ubicaciones para Forms {#configuring-locations-for-forms}

Puede especificar la dirección URL, el URI y las ubicaciones de los archivos de atributos como la raíz web, la ubicación de los formularios que se van a recuperar, el archivo PDF semilla que se utiliza en las transformaciones del formulario PDF y la ubicación de la memoria caché.

1. En la consola de administración, haga clic en Servicios > Forms.
1. En Ubicaciones, especifique las opciones adecuadas. Las opciones se describen a continuación.
1. Haga clic en Guardar.

## Configuración de ubicaciones {#locations-settings}

**URL básica:** Dirección URL base donde se encuentran los recursos de formulario, como imágenes y scripts. Este valor es necesario para las transformaciones de HTML que incluyen referencias HREF a dependencias externas, como imágenes o secuencias de comandos. Uno de estos scripts es xfasubset.js, que es necesario para que los formularios de HTML realicen inteligencia XFA. Este valor debe ser el equivalente HTTP del URI de raíz de contenido.

>[!NOTE]
>
>La dirección URL base solo admite protocolos HTTP o del repositorio. No admite protocolos como file:///. Si necesita acceder a un recurso como un CSS personalizado o un URI de firma digital, utilice el valor de parámetro de API adecuado para especificar la ubicación absoluta.

Cuando una ruta de dependencia es absoluta, se omite el valor de la dirección URL base. De lo contrario, la ruta de dependencia se combina con la dirección URL base.

El valor predeterminado es una cadena vacía.

El siguiente ejemplo apunta al mismo contenido (con el URI raíz del contenido y la URL base):

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**URI raíz web de FS:** La URL de la aplicación web de Forms. Puede dejar este cuadro vacío si la aplicación web de Forms y la aplicación cliente se implementan en el mismo servidor de aplicaciones; se utiliza la URL raíz web de la API de Forms.

Si la aplicación web de Forms y la aplicación cliente no se implementan en el mismo servidor de aplicaciones, proporcione la URL de la aplicación web de Forms en este cuadro, como se muestra en este ejemplo:

`https://<host name>:<port>/FormServer`

Donde `host name`y `port` son el nombre del servidor y el número de puerto del servidor que aloja la aplicación web de Forms.

El valor predeterminado es una cadena vacía.

**URI de raíz web:** Raíz web de la aplicación. AEM Este valor se combina con el parámetro sTargetURL (cuando sTargetURL se proporciona como relativo), especificado mediante el SDK de formularios de la aplicación, para construir una URL absoluta para acceder al contenido web específico de la aplicación.

El valor predeterminado es una cadena vacía.

**URI de raíz de contenido:** URI o ubicación absoluta desde la que se recuperan los formularios. Este valor se combina con el parámetro sFormQuery, especificado mediante la API, para construir la ruta absoluta al formulario recuperado. Este valor puede hacer referencia a un directorio o a una ubicación web a la que se puede acceder mediante HTTP.

El valor predeterminado es una cadena vacía.

**URI de configuración de XCI:** La ubicación relativa o absoluta en la que se encuentra el archivo XCI utilizado para la representación. AEM Para un valor relativo, se da por hecho que el archivo XCI reside en el archivo EAR de formularios implementable de la aplicación de formularios de la aplicación de datos.

El valor predeterminado es `com/adobe/formServer/PA/pa.xci`.

**URI de mapa de fuente:** Ubicación relativa o absoluta del archivo de asignación de fuentes. AEM Para un valor relativo, se da por hecho que este archivo reside en el archivo EAR de formularios implementable que se puede implementar en el formulario de la aplicación.

El archivo de asignación de fuentes se utiliza para crear asignaciones de fuentes personalizadas para las transformaciones de HTML en formularios, lo que le permite especificar qué fuente se sustituirá cuando una fuente no esté disponible en el equipo del cliente.

El valor predeterminado es `com/adobe/formServer/client-font-map.properties`.

La siguiente entrada es un ejemplo de una entrada en el archivo de asignación de fuentes:

`Arial=Arial,Helvetica,sans-serif`

**Archivo de PDF semilla:** El archivo PDF inicial que se utiliza en la transformación de un formulario PDF para optimizar la entrega. El archivo del PDF semilla especifica un archivo de PDF personalizado (que contiene únicamente recursos de fuente, imagen y flujo XFA) que se anexa al diseño de formulario y a los datos. Acrobat 7 o posterior procesa el formulario y se aplica a la transformación de PDF Forms.

El valor predeterminado es una cadena vacía.

**Ubicación de caché:** Especifica la ubicación de la caché de disco de Forms. Al cambiar esta configuración, se restablece toda la información de caché existente de la ubicación actual y se crea una nueva caché en la nueva ubicación. Seleccione una de las siguientes opciones:

**Ubicación predeterminada:** Esta es la selección predeterminada. Cuando se selecciona esta opción, la caché se crea en una ubicación que depende del servidor de aplicaciones que esté utilizando:

* **JBoss:** [Inicio de JBoss]\server\[tipo de instalación]\svcdata\FormServer\Cache
* **WebLogic:** [Inicio de WebLogic]\user_projects\domains\[nombre de dominio de aem-forms]\adobe\[nombre de servidor de Forms]\FormServer\Cache
* **WebSphere:** [Inicio de IBM]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**Directorio temporal de LC:** AEM La caché se crea en un subdirectorio del directorio temporal de los formularios de la, que se especifica en la consola de administración en Configuración > Configuración del sistema principal > Configuraciones > Ubicación del directorio temporal. El subdirectorio se denomina adobeform_[servername].

>[!NOTE]
>
>Si utiliza una utilidad de limpieza temporal, mientras que la eliminación de estos directorios no afecta a la funcionalidad, puede afectar significativamente al rendimiento durante un corto tiempo hasta que se cree la nueva caché. AEM Para evitar este problema, no elimine estos directorios mientras borra el directorio temporal de los formularios de la.
