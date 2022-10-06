---
title: Configuración de ubicaciones para Forms
seo-title: Configuring locations for Forms
description: Obtenga información sobre cómo configurar la ubicación para Forms.
seo-description: Learn how to configure location for Forms.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---

# Configuración de ubicaciones para Forms {#configuring-locations-for-forms}

Puede especificar la dirección URL, el URI y las ubicaciones de archivo de atributos como la raíz web, la ubicación de los formularios que se van a recuperar, el archivo del PDF semilla que se utiliza en las transformaciones PDFForm y la ubicación de la caché.

1. En la consola de administración, haga clic en Servicios > Forms.
1. En Ubicaciones, especifique las opciones adecuadas. Las opciones se describen a continuación.
1. Haga clic en Guardar.

## Configuración de ubicaciones {#locations-settings}

**Dirección URL base:** Dirección URL base donde se encuentran los recursos de formulario, como imágenes y secuencias de comandos. Este valor es necesario para transformaciones de HTML que incluyen referencias HREF a dependencias externas, como imágenes o secuencias de comandos. Una de estas secuencias de comandos es xfasubset.js, que es necesaria para que los formularios de HTML realicen la inteligencia XFA. Este valor debe ser el equivalente HTTP del URI raíz de contenido.

>[!NOTE]
>
>La URL base solo admite protocolos HTTP o de repositorio. No admite protocolos como file:///. Si necesita acceder a un recurso como una CSS personalizada o un URI de firma digital, utilice el valor de parámetro de API apropiado para especificar la ubicación absoluta.

Cuando una ruta de dependencia es absoluta, se ignora el valor de la URL base. De lo contrario, la ruta de dependencia se combina con la dirección URL base.

El valor predeterminado es una cadena vacía.

El siguiente ejemplo apunta al mismo contenido (mediante el URI de raíz de contenido y la URL base):

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**URI raíz web de FS:** La URL de la aplicación web de Forms. Puede dejar este cuadro vacío si la aplicación web de Forms y la aplicación cliente están implementadas en el mismo servidor de aplicaciones; se utilizará la URL raíz web de la API de Forms.

Si la aplicación web de Forms y la aplicación cliente no están implementadas en el mismo servidor de aplicaciones, proporcione la URL para la aplicación web de Forms en este cuadro, como se muestra en este ejemplo:

`https://<host name>:<port>/FormServer`

Donde `host name`y `port` son el nombre del servidor y el número de puerto del servidor que aloja la aplicación web de Forms.

El valor predeterminado es una cadena vacía.

**URI raíz web:** La raíz web de la aplicación. Este valor se combina con el parámetro sTargetURL (cuando sTargetURL se proporciona como relativo), especificado mediante el SDK de AEM forms para construir una dirección URL absoluta para acceder al contenido web específico de la aplicación.

El valor predeterminado es una cadena vacía.

**URI raíz de contenido:** URI o ubicación absoluta desde la que se recuperan los formularios. Este valor se combina con el parámetro sFormQuery, especificado a través de la API, para construir la ruta absoluta al formulario que se recupera. Este valor puede hacer referencia a un directorio o a una ubicación web a la que se puede acceder mediante HTTP.

El valor predeterminado es una cadena vacía.

**URI de configuración XCI:** Ubicación relativa o absoluta en la que se encuentra el archivo XCI utilizado para la renderización. Para un valor relativo, se supone que el archivo XCI reside en el archivo EAR de formularios AEM implementables.

El valor predeterminado es `com/adobe/formServer/PA/pa.xci`.

**URI de mapa de fuente:** Ubicación relativa o absoluta del archivo de asignación de fuentes. Para un valor relativo, se da por hecho que este archivo reside en el archivo EAR de formularios AEM implementables.

El archivo de asignación de fuentes se utiliza para crear asignaciones de fuentes personalizadas para transformaciones de HTML en formularios, lo que le permite especificar qué fuente se sustituirá cuando una fuente no esté disponible en el equipo del cliente.

El valor predeterminado es `com/adobe/formServer/client-font-map.properties`.

La siguiente entrada es un ejemplo de una entrada en el archivo de asignación de fuentes:

`Arial=Arial,Helvetica,sans-serif`

**Archivo PDF semilla:** El archivo de PDF inicial que se utiliza en una transformación PDFForm para optimizar el envío. El archivo de PDF de semilla especifica un archivo de PDF personalizado (que solo contiene recursos de fuente, imagen y flujo XFA) que se anexa al diseño y los datos del formulario. El formulario se procesa mediante Acrobat 7 o versiones posteriores y se aplica a la transformación PDFForm.

El valor predeterminado es una cadena vacía.

**Ubicación de caché:** Especifica la ubicación de la caché de disco de Forms. Al cambiar esta configuración, se restablece toda la información de caché existente de la ubicación actual y se crea una nueva caché en la nueva ubicación. Seleccione una de las siguientes opciones:

**Ubicación predeterminada:** Esta es la selección predeterminada. Cuando se selecciona esta opción, la caché se crea en una ubicación que depende del servidor de aplicaciones que esté utilizando:

* **JBoss:** [Página principal de JBoss]\server\[tipo de instalación]\svcdata\FormServer\Cache
* **WebLogic:** [Página principal de WebLogic]\user_projects\domains\[nombre de dominio de aem-forms]\adobe\[nombre de servidor de formularios]\FormServer\Cache
* **WebSphere:** [Página principal de IBM]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**Directorio temporal LC:** La caché se crea en un subdirectorio del directorio temporal de formularios AEM, que se especifica en la consola de administración en Configuración > Configuración del sistema principal > Configuraciones > Ubicación del directorio temporal. El subdirectorio se denomina adobeform_[servername].

>[!NOTE]
>
>Si utiliza una utilidad de limpieza temporal, tenga en cuenta que, aunque la eliminación de estos directorios no afecta a la funcionalidad, puede afectar significativamente al rendimiento durante un breve periodo hasta que se cree la nueva caché. Para evitar este problema, no elimine estos directorios mientras borra el directorio temporal de formularios AEM.
