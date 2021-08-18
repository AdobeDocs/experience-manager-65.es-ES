---
title: Actualización a la versión 6.5 de Comunidades de AEM
seo-title: Actualización a la versión 6.5 de Comunidades de AEM
description: Actualización de una versión anterior a AEM 6.5 Communities
seo-description: Actualización de una versión anterior a AEM 6.5 Communities
uuid: 929c3892-1b3b-46a7-8e70-fa6864125911
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: abe5a998-bbe3-4a2b-bcf7-b490a8275219
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
source-git-commit: 07f8a9f629122102d30676926b225d57e542147d
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---

# Actualización a la versión 6.5 de Comunidades de AEM {#upgrading-to-aem-communities}

Dependiendo de la topología y las características de cada sitio, pueden ser necesarias las siguientes acciones al actualizar a AEM Communities 6.5 o al instalar el último paquete de funciones.

Esta sección es específica de Comunidades y complementa la información proporcionada en [Actualización a AEM 6.5](/help/sites-deploying/upgrade.md) (plataforma).

## Actualización desde AEM 6.1 o posterior {#upgrading-from-aem-or-later}

### Reindexar Solr {#reindex-solr}

Al instalar un nuevo paquete de funciones de Communities en una implementación configurada con MSRP, será necesario:

1. Instale el [paquete de funciones más reciente](/help/communities/deploy-communities.md#latestfeaturepack).
1. Instale los [últimos archivos de configuración de Solr](/help/communities/msrp.md#upgrading).
1. Reindexar MSRP
consulte la sección [Herramienta de reindexación de MSRP](/help/communities/msrp.md#msrp-reindex-tool).

### Habilitación 2.0 {#enablement}

A partir de AEM 6.3, las funciones de habilitación ya no almacenan información de informes en MySQL. La dependencia MySQL está ahí solamente para rastrear contenido SCORM.

Póngase en contacto con el [Servicio de atención al cliente](https://helpx.adobe.com/es/marketing-cloud/contact-support.html) para obtener ayuda sobre la migración de contenido desde la Habilitación 1.0.

## Actualización desde AEM 6.0 {#upgrading-from-aem}

Si es necesario conservar UGC preexistente, los medios para hacerlo dependen de si la implementación almacenó UGC [local](#on-premise-storage) o en [Adobe cloud](#adobe-cloud-storage).

### Almacenamiento en la nube de Adobe {#adobe-cloud-storage}

Si el sitio actualizado se configuró para utilizar el almacenamiento en la nube de Adobe, puede aparecer (incorrectamente) como si todos los UGC se hubieran perdido, ya que los métodos SRP no podrán localizar el UGC preexistente en la ubicación antigua.

Por lo tanto, existe la capacidad de indicar a ASRP que utilice `AEM 6.0 compatability-mode` para acceder a UGC.

Para todas las instancias de creación y publicación de AEM 6.3:

* Inicie sesión con privilegios de administrador.
* Configure [ASRP](/help/communities/asrp.md).
* Siga estos pasos para que el UGC preexistente sea visible :

   * Vaya a la consola web:

      * Por ejemplo, [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Busque la configuración **AEM Communities Utilities**.
      * Seleccione para expandir el panel de configuración:

         * *Desmarcar* `Cloud Storage`

         * Seleccione **Guardar**

      ![utilidades](assets/utilities.png)


### Almacenamiento On-Premise {#on-premise-storage}

Si el sitio actualizado no utiliza almacenamiento en la nube, cualquier UGC preexistente debe convertirse para ajustarse a la nueva estructura introducida en AEM comunidades 6.1 en apoyo del almacén común.

Para este fin, hay disponible una herramienta de migración de código abierto en GitHub:
[Herramienta de migración UGC de AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### API de Java {#java-apis}

Al actualizar de AEM comunidades sociales 6.0 a AEM 6.3 Communities, tenga en cuenta que muchas API se han reorganizado en paquetes diferentes. La mayoría debe resolverse fácilmente al utilizar un IDE para personalizar las funciones de Communities.

Para obtener más información sobre el paquete SocialUtils obsoleto, visite [SocialUtils Refactoring](/help/communities/socialutils.md).

Consulte también [Uso de Maven para Communities](/help/communities/maven.md).

### Sin plantillas de componente JSP {#no-jsp-component-templates}

El [marco de componentes sociales](/help/communities/scf.md) (SCF) utiliza el lenguaje de plantilla [HandlebarsJS](https://handlebarsjs.com/) (HBS) en lugar de las páginas del servidor Java (JSP) utilizadas antes de AEM 6.0.

En AEM 6.0, los componentes JSP permanecieron junto con los nuevos componentes del marco HBS en la misma ubicación, y los componentes HBS normalmente se encuentran en subcarpetas denominadas &quot;hbs&quot;.

A partir de AEM 6.1, los componentes JSP se eliminaron completamente. En el caso de las comunidades, se recomienda reemplazar todo uso de componentes JSP por componentes SCF.

## Herramienta de migración UGC de AEM Communities {#aem-communities-ugc-migration-tool}

La [herramienta de migración UGC de AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) es una herramienta de migración de código abierto disponible en GitHub que se puede personalizar para exportar UGC de versiones anteriores de AEM comunidades sociales e importarlo a AEM Communities 6.1 o posterior.

Además de mover UGC de versiones anteriores, también es posible utilizar la herramienta para mover UGC de un [SRP](/help/communities/working-with-srp.md) a otro, como de MSRP a DSRP.

## Actualización desde AEM 5.6.1 o anterior {#upgrading-from-aem-or-earlier}

Conceptualmente, hay tres generaciones de componentes de comunidades :

**Gen 1**: Aproximadamente CQ 5.4 a AEM 5.6.0, estos son los componentes de  **** colaboración que almacenaron UGC en el repositorio local utilizando la replicación como medio de sincronizar UGC entre plataformas. Otras diferencias incluyen la implementación mediante páginas de servidor Java (JSP), así como la función de blog que consiste en la creación solo en el entorno de creación.

**Gen 2**: De AEM 5.6.1 a AEM 6.1, se trata de una combinación de  **** componentes sociales y  **** de colaboración. AEM 6.0 introdujo el nuevo [marco de componentes sociales](/help/communities/scf.md) (SCF) y la AEM 6.2 introdujo un [almacén UGC común](/help/communities/working-with-srp.md) donde se accede a UGC mediante un [proveedor de recursos de almacenamiento](/help/communities/srp.md) (SRP).

**Gen 3**: A partir de AEM 6.2, sólo hay componentes  **** sociales, implementados en SCF como Handlebars (HBS), que requieren una elección de SRP para UGC.
