---
title: Uso de propiedades de contenido para exportar contenido
seo-title: Using Content Properties to Export Content
description: La siguiente página muestra los nodos y las propiedades de la aplicación.
seo-description: The following page shows App Properties and Nodes.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 5%

---

# Uso de propiedades de contenido para exportar contenido{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las aplicaciones se representan como *cq:Páginas* AEM en la.

Comparten las mismas propiedades comunes encontradas en cualquier *cq:Page* además de otros que se muestran a continuación y que representan propiedades de compatibilidad con la integración.

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
   <td><p>Ruta a un Cloud Service de Mobile On-Demand configurado. Se utiliza para acciones de AEM Mobile a Mobile On-Demand (invocación de API)</p> <p>Esta asociación se configura mediante el mosaico Administrar conexión cuando un autor elige un Cloud Service de Mobile On-Demand al que asociar la aplicación.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>Cadena:Ruta</td>
   <td><p>Ruta a las configuraciones de exportación de la aplicación. La configuración de exportación es una carpeta con 2 plantillas de configuración de exportación de ContentSync secundarias;</p> <p><i>dps-article</i>: Configuración de exportación de ContentSync para exportar el contenido del artículo</p> <p><i>dps-HTMLResources</i>: Configuración de exportación de ContentSync para exportar recursos compartidos de aplicaciones/artículos</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>Cadena</td>
   <td><p>ID/URI del proyecto de Mobile On-Demand al que está vinculada esta aplicación o enlazada.</p> <p>Esta asociación se configura mediante el mosaico Administrar conexión cuando un autor elige el proyecto de una lista de proyectos disponibles para el Cloud Service de Mobile On-Demand asociado.</p> </td>
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
   <td>AEM Fecha de la última carga de recursos compartidos desde el servidor de recursos compartidos a AEM Mobile.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String:id de usuario</td>
   <td>AEM El ID del usuario que realizó la última carga de la solicitud de recursos compartidos de los recursos compartidos de los usuarios de la red de distribución de datos de a AEM Mobile.</td>
  </tr>
  <tr>
   <td>page-dashboard-config</td>
   <td>Cadena:Ruta</td>
   <td>Ruta a una configuración de panel. La ruta se puede redirigir a una configuración de panel personalizada según sea necesario.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>Cadena:Ruta</td>
   <td><p>Ruta a un cq:Component que es o extiende <i>mobileapps/core/components/instance.</i></p> <p>Esto proporciona la presencia y el procesamiento en el catálogo de aplicaciones.</p> </td>
  </tr>
 </tbody>
</table>

Puede utilizar ***Propiedades del contenido*** para crear contenido. Consulte los siguientes recursos para crear y exportar artículos y recursos compartidos:

* [Propiedades del contenido](/help/mobile/content-properties.md)
* [Creando configuración de exportación del artículo](/help/mobile/creating-article-export-configuration.md)
* [Creación de la configuración de exportación de recursos compartidos](/help/mobile/creating-shared-resources-export-configuration.md)
