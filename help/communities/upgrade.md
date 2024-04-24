---
title: AEM Actualización a comunidades de 6.5
description: AEM Cómo actualizar desde una versión anterior a comunidades de la versión 6.5 de la
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: ea41d35c-967c-4606-b4ec-377e817902e4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# AEM Actualización a comunidades de 6.5 {#upgrading-to-aem-communities}

Según la topología y las características de cada sitio, pueden ser necesarias las siguientes acciones al actualizar a AEM Communities 6.5 o instalar el último paquete de funciones.

Esta sección es específica de Communities y complementa la información proporcionada en [AEM Actualización a 6.5](/help/sites-deploying/upgrade.md) (plataforma).

## AEM Actualización desde la versión 6.1 o posterior de {#upgrading-from-aem-or-later}

### Reindexar Solr {#reindex-solr}

Al instalar un nuevo paquete de funciones de Communities en una implementación configurada con MSRP, será necesario:

1. Instale el [último paquete de funciones](/help/communities/deploy-communities.md#latestfeaturepack).
1. Instale el [últimos archivos de configuración de Solr](/help/communities/msrp.md#upgrading).
1. Reindexar MSRP, consulte la sección [Herramienta de reindexación MSRP](/help/communities/msrp.md#msrp-reindex-tool).

## AEM Actualización desde la versión 6.0 de {#upgrading-from-aem}

Si es necesario conservar el UGC preexistente, los medios para hacerlo dependen de si la implementación almacenó el UGC [on-premise](#on-premise-storage) o en el [nube de Adobe](#adobe-cloud-storage).

### Almacenamiento de Adobe Cloud {#adobe-cloud-storage}

Si el sitio actualizado se configuró para utilizar el almacenamiento en la nube de Adobe, puede aparecer (incorrectamente) como si se hubieran perdido todos los UGC, ya que los métodos SRP no podrán localizar el UGC preexistente en la ubicación antigua.

Por lo tanto, existe la capacidad de indicar a ASRP que utilice `AEM 6.0 compatability-mode` para acceder a UGC.

AEM Para todas las instancias de autor y publicación de la versión 6.3 de:

* Iniciar sesión con privilegios de administrador.
* Configurar [ASRP](/help/communities/asrp.md).
* Siga estos pasos para hacer visible el UGC preexistente:

   * Vaya a la consola web:

      * Por ejemplo, [https://&lt;host>:&lt;port>/system/console/configMgr](https://localhost:4502/system/console/configMgr)

      * Localizar **Utilidades de AEM Communities** configuración.
      * Seleccione para expandir el panel de configuración:

         * *Desmarcar* `Cloud Storage`

         * Seleccionar **Guardar**

     ![utilidades](assets/utilities.png)

### Almacenamiento On-Premise {#on-premise-storage}

AEM Si el sitio actualizado no utiliza el almacenamiento en la nube, cualquier UGC preexistente debe convertirse para ajustarse a la nueva estructura introducida en las comunidades de la versión 6.1 de en apoyo del almacén común.

Para ello, hay disponible una herramienta de migración de código abierto en GitHub:
[Herramienta de migración de UGC para AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

### API de Java {#java-apis}

AEM AEM Al actualizar de comunidades sociales de la versión 6.0 de la a comunidades de la versión 6.3, muchas API se han reorganizado en paquetes diferentes. La mayoría de los problemas se deben resolver fácilmente al usar un IDE para personalizar las características de Communities.

Para obtener más información sobre el paquete obsoleto de SocialUtils, visite [Refactorización de SocialUtils](/help/communities/socialutils.md).

Consulte también [Uso de Maven para comunidades](/help/communities/maven.md).

### No hay plantillas de componentes JSP {#no-jsp-component-templates}

El [marco de componentes sociales](/help/communities/scf.md) (SCF) utiliza el [HandlebarsJS](https://handlebarsjs.com/) AEM (HBS) lenguaje de plantilla en lugar de las páginas de servidor Java (JSP) utilizadas antes de la versión 6.0 de la versión 6.0.

AEM En la versión 6.0, los componentes de JSP permanecieron junto a los nuevos componentes del marco de HBS en la misma ubicación, y los componentes de HBS normalmente en subcarpetas denominadas &quot;hbs&quot;.

AEM A partir de la versión 6.1, los componentes de JSP se eliminaron por completo. En el caso de las comunidades, se recomienda reemplazar todo el uso de componentes JSP por componentes SCF.

## Herramienta de migración de UGC para AEM Communities {#aem-communities-ugc-migration-tool}

El [Herramienta de migración de UGC para AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration) AEM es una herramienta de migración de código abierto, disponible en GitHub, que se puede personalizar para exportar UGC desde versiones anteriores de comunidades sociales de e importarlos en AEM Communities 6.1 o posterior.

Además de mover UGC de versiones anteriores, también es posible utilizar la herramienta para mover UGC de una [SRP](/help/communities/working-with-srp.md) a otro, como del MSRP al DSRP.

## AEM Actualización de la versión 5.6.1 o anterior de la {#upgrading-from-aem-or-earlier}

Conceptualmente, hay tres generaciones de componentes de las comunidades:

**Gen 1** AEM : Aproximadamente CQ 5.4 a 5.6.0, estos son los siguientes: **collab** componentes que almacenan UGC en el repositorio local mediante replicación como medio para sincronizar UGC entre plataformas. Otras diferencias implican la implementación mediante Java Server Pages (JSP) y la función de blog que consiste en crear solo en el entorno de creación.

**Gen 2** AEM AEM : De la versión 5.6.1 a la versión 6.1 de la, se trata de una combinación de **collab** y **social** componentes. AEM.0 presentó el nuevo [marco de componentes sociales](/help/communities/scf.md) AEM (SCF) y la versión 6.2 de la introdujeron un [almacén de UGC común](/help/communities/working-with-srp.md) donde se accede a UGC mediante una [proveedor de recursos de almacenamiento](/help/communities/srp.md) (SRP).

**Gen 3** AEM : A partir de la versión 6.2, solo hay **social** componentes, implementados en SCF como componentes Handlebars (HBS), que requieren una opción de SRP para UGC.
