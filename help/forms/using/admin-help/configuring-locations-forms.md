---
title: Configuración de ubicaciones para formularios
seo-title: Configuración de ubicaciones para formularios
description: Obtenga información sobre cómo configurar la ubicación de Forms.
seo-description: Obtenga información sobre cómo configurar la ubicación de Forms.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de ubicaciones para formularios {#configuring-locations-for-forms}

Puede especificar la dirección URL, el URI y las ubicaciones de archivos de atributos como la raíz web, la ubicación de los formularios que se van a recuperar, el archivo PDF raíz que se utiliza en las transformaciones PDFForm y la ubicación de la caché.

1. En la consola de administración, haga clic en Servicios > Formularios.
1. En Ubicaciones, especifique las opciones correspondientes. Las opciones se describen a continuación.
1. Haga clic en Guardar.

## Configuración de ubicaciones {#locations-settings}

**** Dirección URL base: Dirección URL base donde se encuentran los recursos de formulario, como imágenes y secuencias de comandos. Este valor es necesario para transformaciones HTML que incluyen referencias HREF a dependencias externas, como imágenes o secuencias de comandos. Una de estas secuencias de comandos es xfasubset.js, que es necesaria para que los formularios HTML realicen la inteligencia XFA. Este valor debe ser el equivalente HTTP del URI raíz de contenido.

***Nota **: La dirección URL base solo admite protocolos HTTP o de repositorio. No admite protocolos como file:///. Si necesita acceder a un recurso como una CSS personalizada o un URI de firma digital, utilice el valor de parámetro de API adecuado para especificar la ubicación absoluta.*

Cuando una ruta de dependencia es absoluta, se ignora el valor de la URL base. De lo contrario, la ruta de dependencia se combina con la dirección URL base.

El valor predeterminado es una cadena vacía.

El ejemplo siguiente apunta al mismo contenido (mediante URI de raíz de contenido y URL base):

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**** URI raíz web de FS: Dirección URL de la aplicación web Forms. Puede dejar este cuadro vacío si la aplicación web Forms y la aplicación cliente están implementadas en el mismo servidor de aplicaciones; se utilizará la URL raíz web de la API de formulario.

Si la aplicación web Forms y la aplicación cliente no están implementadas en el mismo servidor de aplicaciones, proporcione la URL de la aplicación web Forms en este cuadro, como se muestra en este ejemplo:

`https://<host name>:<port>/FormServer`

Dónde `host name`y `port` son el nombre del servidor y el número de puerto del servidor que aloja la aplicación web Forms.

El valor predeterminado es una cadena vacía.

**** URI raíz web: La raíz web de la aplicación. Este valor se combina con el parámetro sTargetURL (cuando sTargetURL se proporciona como relativo), especificado mediante el SDK de formularios AEM para construir una dirección URL absoluta para acceder al contenido web específico de la aplicación.

El valor predeterminado es una cadena vacía.

**** URI de raíz de contenido: URI o ubicación absoluta desde la que se recuperan los formularios. Este valor se combina con el parámetro sFormQuery, especificado mediante la API, para construir la ruta absoluta al formulario que se recupera. Este valor puede hacer referencia a un directorio o a una ubicación web a la que se puede acceder mediante HTTP.

El valor predeterminado es una cadena vacía.

**** URI de configuración XCI: Ubicación relativa o absoluta en la que se encuentra el archivo XCI utilizado para la representación. Para un valor relativo, se supone que el archivo XCI reside en el archivo EAR de formularios AEM implementable.

El valor predeterminado es `com/adobe/formServer/PA/pa.xci`.

**** URI de mapa de fuente: Ubicación relativa o absoluta del archivo de asignación de fuentes. Para un valor relativo, se da por hecho que este archivo reside en el archivo EAR de formularios AEM implementable.

El archivo de asignación de fuentes se utiliza para crear asignaciones de fuentes personalizadas para transformaciones HTML en formularios, lo que permite especificar qué fuente se sustituirá cuando una fuente no esté disponible en el equipo del cliente.

El valor predeterminado es `com/adobe/formServer/client-font-map.properties`.

La entrada siguiente es un ejemplo de una entrada en el archivo de asignación de fuentes:

`Arial=Arial,Helvetica,sans-serif`

**** Archivo PDF de inicialización: El archivo PDF inicial que se utiliza en una transformación PDFForm para optimizar la entrega. El archivo PDF de raíz especifica un archivo PDF personalizado (que solo contiene flujo XFA, imagen y recursos de fuente) que se anexa al diseño y los datos del formulario. El formulario se procesa con Acrobat 7 o posterior y se aplica a la transformación PDFForm.

El valor predeterminado es una cadena vacía.

**** Ubicación de caché: Especifica la ubicación de la caché de disco de Forms. Al cambiar esta configuración, se restablece toda la información de caché existente de la ubicación actual y se crea una nueva caché en la nueva ubicación. Seleccione una de las siguientes opciones:

**** Ubicación predeterminada: Ésta es la selección predeterminada. Cuando se selecciona esta opción, la caché se crea en una ubicación que depende del servidor de aplicaciones que esté utilizando:

* **** JBoss: Página de inicio [de JBoss]\server\[tipo de instalación]\svcdata\FormServer\Cache
* **** WebLogic: Inicio [WebLogic]\user_projects\domains\[nombre de dominio de aem-forms]\adobe\[nombre de servidor de formularios]\FormServer\Cache
* **** WebSphere: [IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**** Directorio temporal LC: La caché se crea en un subdirectorio del directorio temporal de formularios AEM, que se especifica en la consola de administración en Configuración > Configuración del sistema principal > Configuraciones > Ubicación del directorio temporal. El subdirectorio se denomina adobeform_[servername].

>[!NOTE]
>
>Si está utilizando una utilidad de limpieza temporal, tenga en cuenta que si bien la eliminación de estos directorios no afecta a la funcionalidad, puede afectar significativamente al rendimiento durante un corto tiempo hasta que se cree la nueva caché. Para evitar este problema, no elimine estos directorios mientras borra el directorio temporal de formularios AEM.

