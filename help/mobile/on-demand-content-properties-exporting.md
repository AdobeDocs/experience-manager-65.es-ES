---
title: Uso de las propiedades del contenido para exportar contenido
seo-title: Uso de las propiedades del contenido para exportar contenido
description: La página siguiente muestra Propiedades de la aplicación y Nodos.
seo-description: La página siguiente muestra Propiedades de la aplicación y Nodos.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 4%

---


# Uso de las propiedades del contenido para exportar contenido{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las aplicaciones se representan como *cq:Pages* en AEM.

Comparten las mismas propiedades comunes que se encuentran en cualquier *cq:Page* además de otras que se muestran a continuación y que representan las propiedades de soporte de la integración.

## Propiedades de la aplicación {#app-properties}

La siguiente tabla muestra **Propiedades y nodos de la aplicación**.

<table>
 <tbody>
  <tr>
   <td><strong>PropertyName</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>Cadena:Ruta</td>
   <td><p>Ruta a un Cloud Service de Mobile On-Demand configurado. Utilizado para acciones de AEM Mobile a Mobile On-Demand (invocación de API)</p> <p>Esta asociación se configura mediante el mosaico Administrar conexión cuando un autor elige un Cloud Service de Mobile On-Demand para asociar la aplicación.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>Cadena:Ruta</td>
   <td><p>Ruta a las configuraciones de exportación de la aplicación. La configuración de exportación es una carpeta con dos plantillas de configuración de exportación de ContentSync secundarias;</p> <p><i>dps-article</i>: Configuración de exportación de ContentSync para exportar el contenido del artículo</p> <p><i>dps-HTMLResources</i>: Configuración de exportación de ContentSync para exportar recursos compartidos de aplicaciones/artículos</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>Cadena</td>
   <td><p>Id/URI del proyecto de Mobile On-Demand al que está vinculada esta aplicación.</p> <p>Esta asociación se configura mediante el mosaico Administrar conexión cuando un autor elige el proyecto de una lista de proyectos disponibles para el Cloud Service de Mobile On-Demand asociado.</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>Cadena</td>
   <td>Título de la aplicación.</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>Cadena</td>
   <td>Tipo de contenido.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>Fecha</td>
   <td>Fecha de la última carga de recursos compartidos de AEM a AEM Mobile.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>Cadena:userid</td>
   <td>Id del usuario que realizó la última carga de la solicitud de recursos compartidos de AEM a AEM Mobile.</td>
  </tr>
  <tr>
   <td>page-panel-config</td>
   <td>Cadena:Ruta</td>
   <td>Ruta a una configuración de panel. La ruta se puede redirigir a una configuración de tablero personalizada según sea necesario.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>Cadena:Ruta</td>
   <td><p>Ruta a un componente cq:Component que es o extiende <i>mobileapps/core/components/instance.</i></p> <p>Esto proporciona la presencia y el procesamiento en el Catálogo de aplicaciones.</p> </td>
  </tr>
 </tbody>
</table>

Puede utilizar ***Propiedades del contenido*** para crear contenido. Consulte los siguientes recursos para crear y exportar artículos y recursos compartidos:

* [Propiedades del contenido](/help/mobile/content-properties.md)
* [Creación de la configuración de exportación de artículos](/help/mobile/creating-article-export-configuration.md)
* [Creación de la configuración de exportación de recursos compartidos](/help/mobile/creating-shared-resources-export-configuration.md)
