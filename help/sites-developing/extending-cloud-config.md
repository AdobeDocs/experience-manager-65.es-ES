---
title: Configuraciones de Cloud Service
seo-title: Configuraciones de Cloud Service
description: Puede ampliar las instancias existentes para crear sus propias configuraciones
seo-description: Puede ampliar las instancias existentes para crear sus propias configuraciones
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 4%

---


# Configuraciones de Cloud Service{#cloud-service-configurations}

Las configuraciones están diseñadas para proporcionar la lógica y la estructura para almacenar configuraciones de servicio.

Puede ampliar las instancias existentes para crear sus propias configuraciones.

## Conceptos {#concepts}

Los principios utilizados para desarrollar las configuraciones se han basado en los siguientes conceptos:

* Los servicios y adaptadores se utilizan para recuperar las configuraciones.
* Las configuraciones (por ejemplo, propiedades o párrafos) se heredan de los elementos principales.
* Se hace referencia desde los nodos de análisis por ruta.
* Fácilmente extensible.
* Tiene la flexibilidad de adaptarse a configuraciones más complejas, como [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* Compatibilidad con dependencias (p. ej. [Los complementos de Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) necesitan una [configuración de Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)).

## Estructura {#structure}

La ruta de acceso base de las configuraciones es:

`/etc/cloudservices`.

Para cada tipo de configuración se proporcionará una plantilla y un componente.Esto permite tener plantillas de configuración que puedan satisfacer la mayoría de las necesidades después de personalizarlas.

Para proporcionar una configuración para un nuevo servicio, debe:

* crear una página de servicios en

   `/etc/cloudservices`

* en este contexto:

   * una plantilla de configuración
   * un componente de configuración

La plantilla y el componente deben heredar `sling:resourceSuperType` de la plantilla base:

`cq/cloudserviceconfigs/templates/configpage`

o componente base respectivamente

`cq/cloudserviceconfigs/components/configpage`

El proveedor de servicio también debe proporcionar la página de servicio:

`/etc/cloudservices/<service-name>`

### Plantilla {#template}

La plantilla extenderá la plantilla base:

`cq/cloudserviceconfigs/templates/configpage`

y defina un `resourceType` que apunte al componente personalizado.

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### Componentes {#components}

El componente debe ampliar el componente base:

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

Después de configurar la plantilla y el componente, puede agregar la configuración agregando subpáginas en:

`/etc/cloudservices/<service-name>`

### Modelo de contenido {#content-model}

El modelo de contenido se almacena como `cq:Page` en:

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

Las configuraciones se almacenan en el subnodo `jcr:content`.

* Las propiedades fijas, definidas en un cuadro de diálogo, deben almacenarse directamente en `jcr:node`.
* Los elementos dinámicos (mediante `parsys` o `iparsys`) utilizan un subnodo para almacenar los datos del componente.

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

Para obtener documentación de referencia sobre la API, consulte [com.day.cq.wcm.webservicesupport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html).

### Integración de AEM {#aem-integration}

Los servicios disponibles se enumeran en la ficha **Cloud Services** del cuadro de diálogo **Propiedades de la página** (de cualquier página que herede de `foundation/components/page` o `wcm/mobile/components/page`).

La ficha también proporciona:

* un vínculo a la ubicación donde puede habilitar el servicio
* elija una configuración (subnodo del servicio) de un campo de ruta

#### Cifrado de contraseña {#password-encryption}

Al almacenar las credenciales de usuario para el servicio, todas las contraseñas deben cifrarse.

Esto se puede lograr agregando un campo de formulario oculto. Este campo debe tener la anotación `@Encrypted` en el nombre de la propiedad; Es decir, para el campo `password` el nombre se escribiría como:

`password@Encrypted`

La propiedad será cifrada automáticamente (mediante el servicio `CryptoSupport`) por el `EncryptionPostProcessor`.

>[!NOTE]
>
>Esto es similar a las ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` anotaciones estándar.

>[!NOTE]
>
>De manera predeterminada, `EcryptionPostProcessor` sólo cifra `POST` las solicitudes realizadas a `/etc/cloudservices`.

#### Propiedades adicionales para la página de servicio jcr:nodos de contenido {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>Ruta de referencia a un componente que se incluirá automáticamente en la página.<br /> Se utiliza para funcionalidad adicional e inclusiones de JS.<br /> Esto incluye el componente en la página <br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> donde se incluye (normalmente antes de la  <code>body</code> etiqueta).<br /> En el caso de que el uso de Analytics y Destinatario lo utilice para incluir funcionalidad adicional, como llamadas de JavaScript para rastrear el comportamiento del visitante.</td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>Descripción breve del servicio.<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>Descripción ampliada del servicio.</td>
  </tr>
  <tr>
   <td>clasificación</td>
   <td>Clasificación de servicio para su uso en anuncios.</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>Filtro para mostrar configuraciones en el cuadro de diálogo de propiedades de página.</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>Dirección URL del sitio web de servicio.</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>Etiqueta para la dirección URL del servicio.</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>Ruta a la miniatura del servicio.</td>
  </tr>
  <tr>
   <td>visible</td>
   <td>Visibilidad en el cuadro de diálogo de propiedades de página; visible de forma predeterminada (opcional)</td>
  </tr>
 </tbody>
</table>

### Casos de uso {#use-cases}

Estos servicios se proporcionan de forma predeterminada:

* [Recortes](/help/sites-administering/external-providers.md)  de rastreadores (Google, WebTrends, etc.)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
* [Search&amp;Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote)
* [Scene7](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>Consulte también [Creación de un Cloud Service personalizado](/help/sites-developing/extending-cloud-config-custom-cloud.md).

