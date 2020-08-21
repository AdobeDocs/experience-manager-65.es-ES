---
title: Actualización a la versión 6.5 de Comunidades de AEM
seo-title: Actualización a la versión 6.5 de Comunidades de AEM
description: Cómo actualizar desde una versión anterior a AEM 6.4 Communities
seo-description: Cómo actualizar desde una versión anterior a AEM 6.4 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---


# Actualización a la versión 6.5 de Comunidades de AEM {#upgrading-to-aem-communities}

Según la topología y las características de cada sitio, es posible que sean necesarias las siguientes acciones al actualizar a AEM Communities 6.5 o al instalar el paquete de funciones más reciente.

Esta sección es específica de Comunidades y complementa la información proporcionada en [Actualización a AEM 6.5](/help/sites-deploying/upgrade.md) (plataforma).

## Actualización desde AEM 6.1 o posterior {#upgrading-from-aem-or-later}

### Volver a indexar Solr {#reindex-solr}

Al instalar un nuevo paquete de funciones de Comunidades en una implementación configurada con MSRP, será necesario:

1. Instale el [último paquete](/help/communities/deploy-communities.md#latestfeaturepack)de funciones.
1. Instale los [últimos archivos](/help/communities/msrp.md#upgrading)de configuración de Solr.
1. Reindexar MSRPver sección [MSRP Herramienta](/help/communities/msrp.md#msrp-reindex-tool)de reindexación.

### Enablement 2.0 {#enablement}

A partir de AEM 6.3, las funciones de habilitación ya no almacenan información de sistema de informes en MySQL. La dependencia de MySQL sólo está ahí para rastrear contenido SCORM.

Póngase en contacto con [el servicio de atención](https://helpx.adobe.com/es/marketing-cloud/contact-support.html) al cliente para obtener ayuda en la migración de contenido desde Habilitación 1.0.

## Actualización desde AEM 6.0 {#upgrading-from-aem}

Si es necesario conservar UGC preexistente, los medios para hacerlo dependerán de si la implementación almacenó UGC [in situ](#on-premise-storage) o en la nube [de](#adobe-cloud-storage)Adobe.

### Almacenamiento de Adobe Cloud {#adobe-cloud-storage}

Si el sitio actualizado se configuró para utilizar el almacenamiento de nube de Adobe, puede aparecer (incorrectamente) como si todo el UGC se hubiera perdido, ya que los métodos SRP no podrán ubicar el UGC preexistente en la ubicación antigua.

Por lo tanto, existe la posibilidad de indicar a ASRP que utilice `AEM 6.0 compatability-mode` para acceder a UGC.

Para todas las instancias de creación y publicación de AEM 6.3:

* Inicie sesión con privilegios de administrador.
* Configure [ASRP](/help/communities/asrp.md).
* Siga estos pasos para hacer que UGC preexistente sea visible:

   * Vaya a la consola web:

      * Por ejemplo, [https://&lt;host>:&lt;puerto>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Busque la configuración de **AEM Communities Utilities** .
      * Seleccione esta opción para expandir el panel de configuración:

         * *Desmarcar* `Cloud Storage`

         * Seleccione **Guardar**

      ![utilidades](assets/utilities.png)


### Almacenamiento local {#on-premise-storage}

Si el sitio actualizado no utiliza almacenamiento en la nube, cualquier UGC preexistente debe convertirse para ajustarse a la nueva estructura introducida en las comunidades de AEM 6.1 en apoyo del almacén común.

Para ello, existe una herramienta de migración de código abierto en GitHub:
[Herramienta de migración UGC de AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### API de Java {#java-apis}

Al actualizar de comunidades sociales de AEM 6.0 a comunidades AEM 6.3, tenga en cuenta que muchas API se han reorganizado en diferentes paquetes. La mayoría de ellas deben resolverse fácilmente al utilizar un IDE para personalizar las funciones de Communities.

Para obtener más información sobre el paquete de SocialUtils obsoleto, visite Refactorización [de SocialUtils](/help/communities/socialutils.md).

Consulte también [Uso de Maven para comunidades](/help/communities/maven.md).

### Sin plantillas de componente JSP {#no-jsp-component-templates}

El marco [de componentes](/help/communities/scf.md) sociales (SCF) utiliza el lenguaje de plantilla [HandlebarsJS](https://www.handlebarsjs.com/) (HBS) en lugar de Java Server Pages (JSP) utilizado antes de AEM 6.0.

En AEM 6.0, los componentes JSP permanecieron junto con los nuevos componentes del marco HBS en la misma ubicación, con los componentes HBS ubicados normalmente en subcarpetas denominadas &quot;hbs&quot;.

A partir del AEM 6.1, los componentes de JSP se eliminaron completamente. En el caso de las comunidades, se recomienda reemplazar todo el uso de componentes JSP por componentes SCF.

## Herramienta de migración UGC de AEM Communities {#aem-communities-ugc-migration-tool}

La herramienta [de migración UGC de](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) AEM Communities es una herramienta de migración de código abierto, disponible en GitHub, que se puede personalizar para exportar UGC desde versiones anteriores de comunidades sociales AEM e importarla en AEM Communities 6.1 o posterior.

Además de mover UGC de versiones anteriores, también es posible utilizar la herramienta para mover UGC de un [SRP](/help/communities/working-with-srp.md) a otro, como del MSRP al DSRP.

## Actualización desde AEM 5.6.1 o anterior {#upgrading-from-aem-or-earlier}

Conceptualmente, hay tres generaciones de componentes de comunidades:

**Gen. 1**: Aproximadamente CQ 5.4 a AEM 5.6.0, estos son los componentes de **laboratorio** que almacenaban UGC en el repositorio local mediante replicación como medio de sincronizar UGC entre plataformas. Otras diferencias incluyen la implementación mediante Java Server Pages (JSP), así como la función de blog que consiste en la creación únicamente en el entorno de creación.

**Gen. 2**: De AEM 5.6.1 a AEM 6.1, se trata de una combinación de componentes **collab** y **sociales** . AEM 6.0 introdujo el nuevo marco [de componentes](/help/communities/scf.md) sociales (SCF) y AEM 6.2 introdujo un almacén [UGC](/help/communities/working-with-srp.md) común en el que se accede a UGC mediante un proveedor [de recursos de](/help/communities/srp.md) almacenamiento (SRP).

**Gen. 3**: A partir de AEM 6.2, solo hay componentes **sociales** , implementados en SCF como componentes de Handlebars (HBS) que requieren una elección de SRP para UGC.
