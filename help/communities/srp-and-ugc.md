---
title: SRP y UGC Essentials
description: Resumen del proveedor de recursos de almacenamiento y del contenido generado por el usuario
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# SRP y UGC Essentials {#srp-and-ugc-essentials}

## Introducción {#introduction}

Si no está familiarizado con el proveedor de recursos de almacenamiento (SRP) y su relación con el contenido generado por el usuario (UGC), visite [Almacenamiento de contenido de comunidad](working-with-srp.md) y [Resumen del proveedor de recursos de almacenamiento](srp.md).

Esta sección de la documentación proporciona información esencial sobre SRP y UGC.

## API StorageResourceProvider {#storageresourceprovider-api}

La API de SocialResourceProvider (API de SRP) es una extensión de varias API de proveedor de recursos de Sling. Incluye soporte para paginación e incremento atómico (útil para recuento y puntuación).

Las consultas son necesarias para los componentes de SCF, ya que es necesario ordenar por fecha, utilidad, número de votos, etc. Todas las opciones de SRP tienen mecanismos de consulta flexibles que no dependen del agrupamiento.

La ubicación de almacenamiento SRP incorpora la ruta del componente. La API de SRP siempre debe utilizarse para acceder a UGC, ya que la ruta raíz depende de la opción de SRP seleccionada, como ASRP, MSRP o JSRP.

La API de SRP no es una clase abstracta, es una interfaz. Una implementación personalizada no debería llevarse a cabo a la ligera, ya que los beneficios de las futuras mejoras en las implementaciones internas se perderían al actualizar a una nueva versión.

Los medios para utilizar la API de SRP son a través de las utilidades proporcionadas, como las que se encuentran en el paquete SocialResourceUtilities.

AEM Al actualizar desde la versión 6.0 o anterior, será necesario migrar el UGC para todos los SRP, para los que hay disponible una herramienta de código abierto. Consulte [Actualización a AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Históricamente, las utilidades para acceder a UGC se encontraban en el paquete SocialUtils, que ya no existe.
>
>Para ver las utilidades de reemplazo, consulte [Refactorización de SocialUtils](socialutils.md).

## Método de utilidad para acceder a UGC {#utility-method-to-access-ugc}

Para acceder a UGC, utilice un método del paquete SocialResourceUtilities que devuelva una ruta adecuada para acceder a UGC desde SRP y sustituya el método obsoleto que se encuentra en el paquete SocialUtils.

A continuación se muestra un ejemplo mínimo del uso del método resourceToUGCStoragePath() en un servlet:

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String ugcPath = socialResourceUtilities.resourceToUGCStoragePath(request.getResource());
  // rest of servlet
}
```

Para ver otros reemplazos de SocialUtils, consulte [Refactorización de SocialUtils](socialutils.md).

Para ver las directrices de codificación, visite [Acceso a UGC con SRP](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>La ruta resourceToUGCStoragePath() devuelve el valor es *no* adecuado para [Comprobación de ACL](srp.md#for-access-control-acls).

## Método de utilidad para acceder a ACL {#utility-method-to-access-acls}

Algunas implementaciones de SRP, como ASRP y MSRP, almacenan contenido de la comunidad en bases de datos que no proporcionan verificación de ACL. Los nodos sombreados proporcionan una ubicación en el repositorio local a la que se pueden aplicar las ACL.

Con la API de SRP, todas las opciones de SRP realizan la misma comprobación de la ubicación en la sombra antes de todas las operaciones de CRUD.

Para comprobar las ACL, utilice un método que devuelva una ruta adecuada para comprobar los permisos aplicados al UGC del recurso.

A continuación se muestra un ejemplo sencillo de cómo utilizar el método resourceToACLPath() en un servlet:

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String aclPath = socialResourceUtilities.resourceToACLPath(request.getResource());
  // rest of servlet
}
```

>[!CAUTION]
>
>La ruta devuelta por resourceToACLPath() es *no* adecuado para [acceso a UGC](#utility-method-to-access-acls) sí mismo.

## Ubicaciones de almacenamiento relacionadas con UGC {#ugc-related-storage-locations}

Las siguientes descripciones de la ubicación de almacenamiento pueden ser de ayuda al desarrollar con JSRP o quizás MSRP. Actualmente no hay ninguna interfaz de usuario que acceda a UGC almacenada en ASRP, como sí la hay para JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) y MSRP (herramientas MongoDB).

**Ubicación del componente**

AEM Cuando un miembro introduce UGC en el entorno de publicación, está interactuando con un componente como parte de un sitio de.

Un ejemplo de este componente es el [componente comentarios](http://localhost:4502/content/community-components/en/comments.html) que existe en el [Guía de componentes de la comunidad](components-guide.md) sitio. La ruta al nodo de comentarios del repositorio local es la siguiente:

* Ruta del componente = `/content/community-components/en/comments/jcr:content/content/includable/comments`

**Ubicación del nodo de sombra**

La creación de UGC también crea un [nodo de sombra](srp.md#about-shadow-nodes-in-jcr) a la que se aplican las ACL necesarias. La ruta al nodo central correspondiente del repositorio local es el resultado de anteponer la ruta raíz del nodo central a la ruta del componente:

* Ruta raíz = `/content/usergenerated`
* Nodo de sombra de comentario = `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**Ubicación de UGC**

El UGC se creará en ninguna de estas ubicaciones y solo se debe acceder a él mediante una [método de utilidad](#utility-method-to-access-ugc) que invoca la API de SRP.

* Ruta raíz = `/content/usergenerated/asi/srp-choice`
* Nodo UGC para JSRP = `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*Tenga en cuenta*, para JSRP, el nodo UGC *solamente* AEM estar presente en la instancia de (ya sea de autor o publicación) en la que se introdujo. Si se introduce en una instancia de publicación, la moderación no será posible desde la consola de moderación del autor.

## Información relacionada {#related-information}

* [Resumen del proveedor de recursos de almacenamiento](srp.md) - Introducción y descripción general del uso del repositorio.
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) - Directrices de codificación.
* [Refactorización de SocialUtils](socialutils.md) : Asignación de métodos de utilidad obsoletos a los métodos de utilidad SRP actuales.
