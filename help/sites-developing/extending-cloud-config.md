---
title: Configuraciones de Cloud Service
seo-title: Cloud Service Configurations
description: Puede ampliar las instancias existentes para crear sus propias configuraciones
seo-description: You can extend the existing instances to create your own configurations
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 4%

---

# Configuraciones de Cloud Service{#cloud-service-configurations}

Las configuraciones están diseñadas para proporcionar la lógica y estructura para almacenar configuraciones de servicio.

Puede ampliar las instancias existentes para crear sus propias configuraciones.

## Conceptos  {#concepts}

Los principios utilizados en el desarrollo de las configuraciones se han basado en los siguientes conceptos:

* Los servicios/adaptadores se utilizan para recuperar las configuraciones.
* Las configuraciones (p. ej., propiedades/párrafos) se heredan de los elementos principales.
* Se hace referencia desde los nodos de análisis por ruta.
* Fácilmente extensible.
* Tiene la flexibilidad para adaptarse a configuraciones más complejas, como [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* Compatibilidad con dependencias (p. ej. [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) los complementos necesitan una [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) configuración).

## Estructura {#structure}

La ruta base de las configuraciones es:

`/etc/cloudservices`.

Para cada tipo de configuración se proporcionará una plantilla y un componente.Esto permite tener plantillas de configuración que puedan satisfacer la mayoría de las necesidades después de personalizarse.

Para proporcionar una configuración para un nuevo servicio, debe:

* cree una página de servicio en

   `/etc/cloudservices`

* en esta sección:

   * una plantilla de configuración
   * un componente de configuración

La plantilla y el componente deben heredar el `sling:resourceSuperType` de la plantilla base:

`cq/cloudserviceconfigs/templates/configpage`

o componente base respectivamente

`cq/cloudserviceconfigs/components/configpage`

El proveedor de servicios también debe proporcionar la página de servicio:

`/etc/cloudservices/<service-name>`

### Plantilla {#template}

La plantilla amplía la plantilla base:

`cq/cloudserviceconfigs/templates/configpage`

y defina una `resourceType` que señala al componente personalizado.

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

Después de configurar la plantilla y el componente, puede añadir la configuración añadiendo subpáginas en:

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

Las configuraciones se almacenan bajo el subnodo `jcr:content`.

* Las propiedades fijas definidas en un cuadro de diálogo deben almacenarse en la variable `jcr:node` directamente.
* Elementos dinámicos (mediante `parsys` o `iparsys`) utilice un subnodo para almacenar los datos del componente.

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

### Integración AEM {#aem-integration}

Los servicios disponibles se enumeran en la sección **Cloud Services** de la pestaña **Propiedades de página** cuadro de diálogo (de cualquier página que herede de `foundation/components/page` o `wcm/mobile/components/page`).

La pestaña también proporciona:

* un vínculo a la ubicación en la que puede activar el servicio
* elegir una configuración (subnodo del servicio) de un campo de ruta

#### Cifrado de contraseña {#password-encryption}

Al almacenar las credenciales de usuario para el servicio, todas las contraseñas deben cifrarse.

Para conseguirlo, agregue un campo de formulario oculto. Este campo debe tener la anotación `@Encrypted` en el nombre de la propiedad; es decir, para la variable `password` field el nombre se escribirá como:

`password@Encrypted`

A continuación, la propiedad se cifrará automáticamente (utilizando la variable `CryptoSupport` por el `EncryptionPostProcessor`.

>[!NOTE]
>
>Esto es similar al estándar ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` anotaciones.

>[!NOTE]
>
>De forma predeterminada, la variable `EcryptionPostProcessor` solo cifra `POST` solicitudes realizadas `/etc/cloudservices`.

#### Propiedades adicionales para la página de servicio jcr:nodos de contenido {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>Ruta de referencia a un componente que se incluirá automáticamente en la página.<br /> Se utiliza para funciones adicionales e inclusiones de JS.<br /> Esto incluye el componente en la página donde<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> se incluye (normalmente antes de <code>body</code> ).<br /> En caso de que el de Analytics y Target lo use para incluir funcionalidades adicionales, como llamadas de JavaScript para rastrear el comportamiento de los visitantes.</td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>Descripción breve del servicio.<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>Descripción extendida del servicio.</td>
  </tr>
  <tr>
   <td>clasificación</td>
   <td>Clasificación del servicio para su uso en anuncios.</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>Filtro para mostrar configuraciones en el cuadro de diálogo de propiedades de página.</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>Dirección URL del sitio web del servicio.</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>Etiqueta de la URL del servicio.</td>
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

* [Fragmentos de rastreador](/help/sites-administering/external-providers.md) (Google, WebTrends, etc.)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)

<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>Consulte también [Creación de un Cloud Service personalizado](/help/sites-developing/extending-cloud-config-custom-cloud.md).
