---
title: Obtener información de página en formato JSON
description: Para obtener la información de la página, envíe una solicitud al servlet PageInfo para obtener los metadatos de la página en formato JSON
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 7c856e87-9f90-435d-aceb-994f10ea6f50
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 1%

---

# Obtener información de página en formato JSON{#obtaining-page-information-in-json-format}

Para obtener la información de la página, envíe una solicitud al servlet PageInfo para obtener los metadatos de la página en formato JSON.

El servlet PageInfo devuelve información sobre los recursos del repositorio. El servlet está enlazado a la dirección URL `https://<server>:<port>/libs/wcm/core/content/pageinfo.json` y utiliza el `path` para identificar el recurso. La siguiente URL de ejemplo devuelve información sobre `/content/we-retail/us/en` nodo:

```shell
http://localhost:4502/libs/wcm/core/content/pageinfo.json?path=/content/we-retail/us/en
```

>[!NOTE]
>
>AEM Si necesita información de la página en formato JSON para proporcionar la entrega de contenido a canales que no son páginas web tradicionales, como, por ejemplo:
>
>* Aplicaciones de una sola página
>* Aplicaciones móviles nativas
>* AEM Otros canales y puntos de contacto externos a los que se puede acceder mediante el uso de la
>
>Ver el documento [Exportador JSON para servicios de contenido](/help/sites-developing/json-exporter.md).

## Proveedores de información de página {#page-information-providers}

Los componentes de página se pueden asociar a uno o más `com.day.cq.wcm.api.PageInfoProvider` servicios que generan metadatos de página. El servlet PageInfo llama a cada servicio PageInfoProvider y agrega los metadatos:

1. El cliente HTTP envía una solicitud al servlet PageInfo, que incluye la dirección URL de la página.
1. El servlet PageInfo detecta qué componente procesa la página.
1. El servlet PageInfo llama a cada PageInfoProvider asociado al componente.
1. El servlet agrega los metadatos que devuelve cada PageInfoProvider y los agrega a la respuesta HTTP en un objeto JSON.

![chlimage_1-2](assets/chlimage_1-2a.png)

>[!NOTE]
>
>De forma similar a PageInfoProviders, utilice ListInfoProviders para actualizar listas de información en formato JSON. (Consulte [Personalización de la consola de administración de sitios web](/help/sites-developing/customizing-siteadmin.md).)

## Proveedores de información de página predeterminada {#default-page-information-providers}

El `/libs/foundation/components/page` está asociado con los siguientes servicios de PageInfoProvider:

* **Proveedor de estado de página predeterminado:** Información sobre el estado de página, como si está bloqueado, si la página es la carga útil de un flujo de trabajo activo y qué flujos de trabajo están disponibles para la página.
* **Proveedor de información de relación activa:** Información sobre Multi Site Management (MSM), como si la página forma parte de un modelo de impresión azul y si es una Live Copy.
* **Servlet de idioma de contenido:** El idioma de la página actual e información sobre cada idioma en el que está disponible la página.
* **Proveedor de estado de flujo de trabajo:** Información de estado sobre el flujo de trabajo en ejecución que tiene la página como carga útil.
* **Proveedor de información de paquete de flujo de trabajo:** Información sobre cada paquete de flujo de trabajo almacenado en el repositorio y si cada paquete contiene el recurso actual.
* **Proveedor de información del emulador:** Información acerca de los emuladores de dispositivos móviles disponibles para este recurso. Si el componente de página no procesa páginas móviles, no hay emuladores disponibles.
* **Proveedor de información de anotaciones:** Información sobre anotaciones que se encuentran en la página.

Por ejemplo, el servlet PageInfo devuelve la siguiente respuesta JSON para la variable `/content/we-retail/us/en` nodo:

```
{
   "status":{
      "path":"/content/we-retail/us/en",
      "isLocked":false,
      "lockOwner":"",
      "canUnlock":false,
      "lastModified":1467202845038,
      "lastModifiedBy":"admin",
      "timeUntilValid":0,
      "onTime":0,
      "offTime":0,
      "replication":{
         "numQueued":0
      },
      "isDesignable":true,
      "isDeveloper":true
   },
   "isPage":true,
   "pageResourceType":"weretail/components/structure/page",
   "enableFragmentIdentifier":false,
   "workflow":{
      "isRunning":false
   },
   "workflows":{
      "wcm":{
         "models":[
            {
               "wid":"/etc/workflow/models/dam/adddamsize/jcr:content/model",
               "label":"Add Asset Size",
               "label_xss":"Add Asset Size"
            },
            {
               "wid":"/etc/workflow/models/ac-newsletter-workflow-simple/jcr:content/model",
               "label":"Approve for Adobe Campaign",
               "label_xss":"Approve for Adobe Campaign"
            },
            {
               "wid":"/etc/workflow/models/dam/dam-autotag-assets/jcr:content/model",
               "label":"DAM Smart Tag Assets",
               "label_xss":"DAM Smart Tag Assets"
            },
            {
               "wid":"/etc/workflow/models/dam/update_asset/jcr:content/model",
               "label":"DAM Update Asset",
               "label_xss":"DAM Update Asset"
            },
            {
               "wid":"/etc/workflow/models/cloudservices/DTM_bundle_download/jcr:content/model",
               "label":"Default DTM Bundle Download",
               "label_xss":"Default DTM Bundle Download"
            },
            {
               "wid":"/etc/workflow/models/dam/dam_download_asset/jcr:content/model",
               "label":"Download Asset",
               "label_xss":"Download Asset"
            },
            {
               "wid":"/etc/workflow/models/dam/dynamic-media-video-thumbnail-replacement/jcr:content/model",
               "label":"Dynamic Media Video Thumbnail Replacement",
               "label_xss":"Dynamic Media Video Thumbnail Replacement"
            },
            {
               "wid":"/etc/workflow/models/dam/dynamic-media-video-user-uploaded-thumbnail/jcr:content/model",
               "label":"Dynamic Media Video User Uploaded Thumbnail Process",
               "label_xss":"Dynamic Media Video User Uploaded Thumbnail Process"
            },
            {
               "wid":"/etc/workflow/models/projects/approval_workflow/jcr:content/model",
               "label":"Project Approval Workflow",
               "label_xss":"Project Approval Workflow"
            },
            {
               "wid":"/etc/workflow/models/publish_example/jcr:content/model",
               "label":"Publish Example",
               "label_xss":"Publish Example"
            },
            {
               "wid":"/etc/workflow/models/publish_to_campaign/jcr:content/model",
               "label":"Publish to Adobe Campaign",
               "label_xss":"Publish to Adobe Campaign"
            },
            {
               "wid":"/etc/workflow/models/s7dam/request_to_publish_to_youtube/jcr:content/model",
               "label":"Publish to YouTube",
               "label_xss":"Publish to YouTube"
            },
            {
               "wid":"/etc/workflow/models/projects/request_copy/jcr:content/model",
               "label":"Request Copy",
               "label_xss":"Request Copy"
            },
            {
               "wid":"/etc/workflow/models/request_for_activation/jcr:content/model",
               "label":"Request for Activation",
               "label_xss":"Request for Activation"
            },
            {
               "wid":"/etc/workflow/models/request_for_deactivation/jcr:content/model",
               "label":"Request for Deactivation",
               "label_xss":"Request for Deactivation"
            },
            {
               "wid":"/etc/workflow/models/request_for_deletion/jcr:content/model",
               "label":"Request for Deletion",
               "label_xss":"Request for Deletion"
            },
            {
               "wid":"/etc/workflow/models/request_to_complete_move_operation/jcr:content/model",
               "label":"Request to complete Move operation",
               "label_xss":"Request to complete Move operation"
            },
            {
               "wid":"/etc/workflow/models/screens-update-asset/jcr:content/model",
               "label":"Screens Update Asset",
               "label_xss":"Screens Update Asset"
            },
            {
               "wid":"/etc/workflow/models/s7dam/request_to_remove_from_youtube/jcr:content/model",
               "label":"Unpublish from YouTube",
               "label_xss":"Unpublish from YouTube"
            },
            {
               "wid":"/etc/workflow/models/wcm-translation/create_language_copy/jcr:content/model",
               "label":"WCM: Create Language Copy",
               "label_xss":"WCM: Create Language Copy"
            },
            {
               "wid":"/etc/workflow/models/wcm-translation/prepare_translation_project/jcr:content/model",
               "label":"WCM: Prepare Translation Project",
               "label_xss":"WCM: Prepare Translation Project"
            },
            {
               "wid":"/etc/workflow/models/wcm-translation/translate-i18n-dictionary/jcr:content/model",
               "label":"WCM: Prepare and Translate I18n-Dictionary",
               "label_xss":"WCM: Prepare and Translate I18n-Dictionary"
            },
            {
               "wid":"/etc/workflow/models/wcm-translation/sync_translation_job/jcr:content/model",
               "label":"WCM: Sync Translation Job",
               "label_xss":"WCM: Sync Translation Job"
            },
            {
               "wid":"/etc/workflow/models/wcm-translation/update_language_copy/jcr:content/model",
               "label":"WCM: Update Language Copy",
               "label_xss":"WCM: Update Language Copy"
            }
         ]
      },
      "translation":{
         "models":[
            {
               "wid":"/etc/workflow/models/dam/adddamsize/jcr:content/model",
               "label":"Add Asset Size",
               "label_xss":"Add Asset Size"
            },
            {
               "wid":"/etc/workflow/models/ac-newsletter-workflow-simple/jcr:content/model",
               "label":"Approve for Adobe Campaign",
               "label_xss":"Approve for Adobe Campaign"
            },
            {
               "wid":"/etc/workflow/models/dam/dam-autotag-assets/jcr:content/model",
               "label":"DAM Smart Tag Assets",
               "label_xss":"DAM Smart Tag Assets"
            },
            {
               "wid":"/etc/workflow/models/cloudservices/DTM_bundle_download/jcr:content/model",
               "label":"Default DTM Bundle Download",
               "label_xss":"Default DTM Bundle Download"
            },
            {
               "wid":"/etc/workflow/models/dam/dam_download_asset/jcr:content/model",
               "label":"Download Asset",
               "label_xss":"Download Asset"
            },
            {
               "wid":"/etc/workflow/models/dam/dynamic-media-video-thumbnail-replacement/jcr:content/model",
               "label":"Dynamic Media Video Thumbnail Replacement",
               "label_xss":"Dynamic Media Video Thumbnail Replacement"
            },
            {
               "wid":"/etc/workflow/models/dam/dynamic-media-video-user-uploaded-thumbnail/jcr:content/model",
               "label":"Dynamic Media Video User Uploaded Thumbnail Process",
               "label_xss":"Dynamic Media Video User Uploaded Thumbnail Process"
            },
            {
               "wid":"/etc/workflow/models/projects/approval_workflow/jcr:content/model",
               "label":"Project Approval Workflow",
               "label_xss":"Project Approval Workflow"
            },
            {
               "wid":"/etc/workflow/models/publish_to_campaign/jcr:content/model",
               "label":"Publish to Adobe Campaign",
               "label_xss":"Publish to Adobe Campaign"
            },
            {
               "wid":"/etc/workflow/models/s7dam/request_to_publish_to_youtube/jcr:content/model",
               "label":"Publish to YouTube",
               "label_xss":"Publish to YouTube"
            },
            {
               "wid":"/etc/workflow/models/projects/request_copy/jcr:content/model",
               "label":"Request Copy",
               "label_xss":"Request Copy"
            },
            {
               "wid":"/etc/workflow/models/request_for_deletion/jcr:content/model",
               "label":"Request for Deletion",
               "label_xss":"Request for Deletion"
            },
            {
               "wid":"/etc/workflow/models/request_to_complete_move_operation/jcr:content/model",
               "label":"Request to complete Move operation",
               "label_xss":"Request to complete Move operation"
            },
            {
               "wid":"/etc/workflow/models/screens-update-asset/jcr:content/model",
               "label":"Screens Update Asset",
               "label_xss":"Screens Update Asset"
            },
            {
               "wid":"/etc/workflow/models/translation/jcr:content/model",
               "label":"Translation Prepare",
               "label_xss":"Translation Prepare"
            },
            {
               "wid":"/etc/workflow/models/s7dam/request_to_remove_from_youtube/jcr:content/model",
               "label":"Unpublish from YouTube",
               "label_xss":"Unpublish from YouTube"
            }
         ]
      }
   },
   "translation":{

   },
   "design":{
      "path":"/conf/we-retail/settings/wcm/templates/hero-page/policies",
      "lastModified":0
   },
   "componentsRef":"/libs/wcm/core/content/components.1497341312569.json",
   "editableTemplate":"/conf/we-retail/settings/wcm/templates/hero-page",
   "msm":{
      "msm:isLiveCopy":true,
      "msm:isInBlueprint":false,
      "msm:isSource":false
   },
   "launches":{
      "isLaunch":false,
      "isInLaunch":false
   },
   "language":"en",
   "languages":{
      "rows":[
         {
            "path":"/content/we-retail/us/en",
            "exists":true,
            "hasContent":true,
            "lastModified":0,
            "iso":"en",
            "country":"gb",
            "language":"English"
         },
         {
            "path":"/content/we-retail/us/es",
            "exists":true,
            "hasContent":true,
            "lastModified":0,
            "iso":"es",
            "country":"es",
            "language":"Spanish"
         }
      ]
   },
   "workflowInfo":{
      "isRunning":false
   },
   "workflowPackageInfo":{
      "workflowPackages":[

      ],
      "selectedWorkflowPackages":[

      ],
      "runningSelectedWorkflowPackages":[

      ]
   },
   "emulators":{
      "groups":{
         "responsive":{
            "title":"Responsive Devices",
            "description":"The devices in this group are able to display a website built using responsive design patterns.",
            "path":"/etc/mobile/groups/responsive",
            "galaxy5":{
               "text":"Galaxy S5",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/galaxy5",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":1080,
               "height":1920,
               "device-pixel-ratio":3
            },
            "ipad":{
               "text":"iPad",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/ios/ipad",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":768,
               "height":1024,
               "device-pixel-ratio":1
            },
            "iphone5":{
               "text":"iPhone 5",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/ios/iphone5",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":640,
               "height":1136,
               "device-pixel-ratio":2
            },
            "iphone6":{
               "text":"iPhone 6",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/ios/iphone6",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":750,
               "height":1334,
               "device-pixel-ratio":2
            },
            "iphone4":{
               "text":"iPhone 4",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/ios/iphone4",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":640,
               "height":960,
               "device-pixel-ratio":2
            },
            "iphone6plus":{
               "text":"iPhone 6 Plus",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/ios/iphone6plus",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":1080,
               "height":1920,
               "device-pixel-ratio":2.6
            },
            "nexuss":{
               "text":"Nexus S",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/nexuss",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":320,
               "height":533,
               "device-pixel-ratio":1
            }
         }
      }
   },
   "annotations":[

   ],
   "permissions":{
      "modify":true,
      "replicate":true,
      "read":true,
      "create":true,
      "delete":true,
      "acl_read":true,
      "acl_edit":true
   },
   "isTargetable":"true",
   "responsive":{
      "breakpoints":{
         "phone":{
            "width":650,
            "title":"Smaller Screen"
         },
         "tablet":{
            "width":1200,
            "title":"Tablet"
         }
      }
   }
}
```

## Filtrado de información de paquetes de flujo de trabajo {#filtering-workflow-package-information}

Configure el servicio Proveedor de información del paquete del flujo de trabajo de CQ WCM diario para que devuelva información solo sobre los paquetes de flujo de trabajo en los que esté interesado. De forma predeterminada, el servicio Proveedor de información del paquete de flujo de trabajo devuelve información sobre cada paquete de flujo de trabajo del repositorio. La iteración en un subconjunto de paquetes de flujo de trabajo utiliza menos recursos de servidor.

>[!NOTE]
>
>La pestaña Workflow del Sidekick utiliza el servlet PageInfo para obtener una lista de paquetes de flujo de trabajo. En la lista, puede seleccionar el paquete al que desea agregar la página actual. Los filtros que cree afectarán a esta lista.
>

El ID del servicio es `com.day.cq.wcm.workflow.impl.WorkflowPackageInfoProvider`. Para crear un filtro, especifique un valor para una `workflowpackageinfoprovider.filter` propiedad.

Los valores de propiedad llevan el prefijo + o - seguido de la ruta del paquete:

* La ruta es la ruta del nodo raíz del paquete de flujo de trabajo. La ruta utiliza la sintaxis de FileVault.
* Para incluir un paquete, utilice el prefijo +.
* Para excluir un paquete, utilice el prefijo -.

El servicio aplica el resultado acumulado de todos los filtros. Por ejemplo, los siguientes valores de filtro excluyen todos los paquetes de flujo de trabajo excepto los de la carpeta Editions:

```
-/etc/workflow/packages(/.*)?
+/etc/workflow/packages/Editions(/.&ast;)?
```

>[!NOTE]
>
>AEM Al trabajar con los servicios de configuración, existen varios métodos para administrar los parámetros de configuración de dichos servicios. Consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener información detallada.

Por ejemplo, para configurar el servicio con CRXDE Lite:

1. Abrir CRXDE Lite ([http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. En la carpeta config de la aplicación, cree un nodo:

   * Nombre: `com.day.cq.wcm.workflow.impl.WorkflowPackageInfoProvider`
   * Tipo: `sling:OsgiConfig`

1. Seleccione el nodo y agregue una propiedad:

   * Nombre: `workflowpackageinfoprovider.filter`
   * Tipo: `String[]`
   * Valor: La ruta al paquete de flujo de trabajo con el formato correcto.

1. Haga clic en Guardar todo.

Para configurar el servicio en el origen del proyecto:

1. AEM Busque o cree la carpeta de configuración para la aplicación de en el origen del proyecto.

   Por ejemplo, si ha utilizado el arquetipo multimodule del complemento Maven del paquete de contenido para crear el proyecto, la ruta de la carpeta es `<projectroot>/content/src/ for example, content/src/main/content/jcr_root/apps/<appname>/config`.
1. En la carpeta de configuración, cree un archivo de texto llamado com.day.cq.wcm.workflow.impl.WorkflowPackageInfoProvider.xml
1. Copie el siguiente texto en el archivo:

   ```
   <?xml version="1.0" encoding="UTF-8"?>
    <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="https://www.jcp.org/jcr/1.0"
    jcr:primaryType="sling:OsgiConfig"
    workflowpackageinfoprovider.filter="[]"/>
   ```

1. Dentro de los corchetes (`[]`) que rodean al `workflowpackageinfoprovider.filter` , escriba una lista de valores de filtro separados por comas similar al siguiente ejemplo:

   `workflowpackageinfoprovider.filter="[-/etc/workflow/packages(/.*)?,+/etc/workflow/packages/Editions(/.*)?]"/>`

1. Guarde el archivo.

## Creación de un proveedor de información de página {#creating-a-page-information-provider}

Cree un servicio de proveedor de información de página personalizado para agregar metadatos de página que la aplicación pueda obtener fácilmente.

1. Implementación de `com.day.cq.wcm.api.PageInfoProvider` interfaz.
1. Agrupe e implemente la clase como un servicio OSGi.
1. Cree un componente de página en la aplicación. Uso `foundation/components/page` como el valor de `sling:resourceSuperType` propiedad.

1. Añada un nodo debajo del nodo de componente denominado `cq:infoProviders`.
1. Debajo de `cq:infoProviders` , agregue un nodo para el servicio PageInfoProvider. Puede especificar cualquier nombre para el nodo.
1. Agregue la siguiente propiedad al nodo PageInfoProvider:

   * Nombre: className
   * Tipo: cadena
   * Valor: PID del servicio PageInfoProvider.

Para recursos que utilizan el componente de página de la aplicación como `sling:resourceType`, el servlet PageInfo devuelve los metadatos personalizados de PageInfoProvider además de los metadatos predeterminados de PageInfoProvider.

### Ejemplo de implementación de PageInfoProvider {#example-pageinfoprovider-implementation}

La siguiente clase Java implementa [PageInfoProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) y devuelve la URL publicada del recurso de página actual.

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.ReferenceCardinality;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;

import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;

import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;

import com.day.cq.wcm.api.Page;
import com.day.cq.wcm.api.PageInfoProvider;

@Component(metatype = false)
@Properties({
 @Property(name="service.description", value="Returns the public URL of a resource.")
})
@Service
public class PageUrlInfoProvider implements PageInfoProvider {

 @Reference(cardinality = ReferenceCardinality.OPTIONAL_UNARY)
 private com.day.cq.commons.Externalizer externalizer;

 private String fetchExternalUrl(ResourceResolver rr, String path) {
  return externalizer.publishLink(rr, path);
 }

 public void updatePageInfo(SlingHttpServletRequest request, JSONObject info, Resource resource)
   throws JSONException {

  Page page = resource.adaptTo(Page.class);
  JSONObject urlinfo = new JSONObject();
  urlinfo.put("publishURL", fetchExternalUrl(null,page.getPath()));
  info.put("URLs",urlinfo);
 }
}
```

El siguiente ejemplo, en CRXDE Lite, muestra el componente de página configurado para utilizar el servicio PageUrlInfoProvider:

![chlimage_1-3](assets/chlimage_1-3a.png)

El servicio PageUrlInfoProvider devuelve los siguientes datos para la variable `/content/we-retail/us/en` nodo:

```xml
"URLs": {
    "publishURL": "http://localhost:4503/content/we-retail/us/en"
}
```
