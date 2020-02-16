---
title: Elementos esenciales de SRP y UGC
seo-title: Elementos esenciales de SRP y UGC
description: Visión general del proveedor de recursos de almacenamiento y del contenido generado por el usuario
seo-description: Visión general del proveedor de recursos de almacenamiento y del contenido generado por el usuario
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Elementos esenciales de SRP y UGC {#srp-and-ugc-essentials}

## Introducción {#introduction}

Si no está familiarizado con el proveedor de recursos de almacenamiento (SRP) y su relación con el contenido generado por el usuario (UGC), visite Información general sobre el proveedor [de recursos de almacenamiento y almacenamiento](working-with-srp.md) de contenido [de la comunidad](srp.md).

En esta sección de la documentación se proporciona información esencial sobre SRP y UGC.

## API de StorageResourceProvider {#storageresourceprovider-api}

La API de SocialResourceProvider (SRP API) es una extensión de varias API de proveedores de recursos de Sling. Incluye soporte para paginación e incremento atómico (útil para contar y anotar).

Las consultas son necesarias para los componentes de SCF, ya que es necesario ordenar por fecha, utilidad, número de votos, etc. Todas las opciones de SRP tienen mecanismos de consulta flexibles que no dependen del agrupamiento.

La ubicación de almacenamiento SRP incorpora la ruta del componente. La API de SRP siempre debe utilizarse para acceder a UGC, ya que la ruta de acceso raíz depende de la opción de SRP seleccionada, como ASRP, MSRP o JSRP.

La API de SRP no es una clase abstracta, es una interfaz. Una implementación personalizada no debería realizarse a la ligera, ya que las ventajas de futuras mejoras en las implementaciones internas se perderían al actualizar a una nueva versión.

Los medios para utilizar la API de SRP son a través de las utilidades proporcionadas, como las que se encuentran en el paquete SocialResourceUtilities.

Al actualizar desde AEM 6.0 o anterior, será necesario migrar UGC para todos los SRP, para los que hay una herramienta de código abierto disponible. See [Upgrading to AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>Históricamente, las utilidades para acceder a UGC se encontraban en el paquete SocialUtils, que ya no existe.
>
>Para ver las utilidades de reemplazo, consulte Refactorización de [SocialUtils](socialutils.md).

## Método de utilidad para acceder a UGC {#utility-method-to-access-ugc}

Para acceder a UGC, utilice un método del paquete SocialResourceUtilities que devuelve una ruta adecuada para acceder a UGC desde SRP y reemplace el método obsoleto que se encuentra en el paquete SocialUtils.

A continuación se muestra un ejemplo mínimo de uso del método resourceToUGCStoragePath() en un servlet:

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

Para otras sustituciones de SocialUtils, consulte Refactorización de [SocialUtils](socialutils.md).

Para obtener instrucciones de codificación, visite [Acceso a UGC con SRP](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>El path resourceToUGCStoragePath() devuelve *no es *adecuado para la comprobación [](srp.md#for-access-control-acls)ACL.

## Método de utilidad para acceder a las ACL {#utility-method-to-access-acls}

Algunas implementaciones de SRP, como ASRP y MSRP, almacenan contenido comunitario en bases de datos que no proporcionan verificación de ACL. Los nodos de sombra proporcionan una ubicación en el repositorio local a la que se pueden aplicar las ACL.

Mediante la API de SRP, todas las opciones de SRP realizan la misma comprobación de la ubicación de sombra antes de todas las operaciones de CRUD.

Para comprobar las ACL, utilice un método que devuelva una ruta adecuada para comprobar los permisos aplicados al UGC del recurso.

A continuación se muestra un ejemplo sencillo de uso del método resourceToACLPath() en un servlet:

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
>La ruta devuelta por resourceToACLPath() *no es *adecuada para [acceder al UGC](#utility-method-to-access-acls) mismo.

## Ubicaciones de almacenamiento de información relacionadas con UGC {#ugc-related-storage-locations}

Las siguientes descripciones de la ubicación de almacenamiento pueden ser de ayuda cuando se desarrolla con JSRP o tal vez MSRP. Actualmente no hay ninguna interfaz de usuario para acceder a UGC almacenada en ASRP, ya que existe para JSRP ([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)) y MSRP (herramientas MongoDB).

**ubicación del componente**

Cuando un miembro entra en UGC en el entorno de publicación, interactúa con un componente como parte de un sitio de AEM.

Un ejemplo de este componente es el componente [de](http://localhost:4502/content/community-components/en/comments.html) comentarios que existe en el sitio de la Guía [de componentes de la](components-guide.md) comunidad. La ruta al nodo de comentarios en el repositorio local es:

* Ruta del componente = */content/community-components/es/comments/jcr:content/content/inclusible/comments*

**ubicación del nodo de sombra**

La creación de UGC también crea un nodo [de](srp.md#about-shadow-nodes-in-jcr) sombra al que se aplican las ACL necesarias. La ruta al nodo de sombra correspondiente en el repositorio local es el resultado de anteponer la ruta raíz del nodo de sombra a la ruta del componente:

* Ruta de acceso raíz = /content/usergenerate
* Nodo de sombra de comentario = /content/usergenerate/content/community-components/es/comments/jcr:content/content/inclusible/comments

**Ubicación de UGC**

El UGC se crea en ninguna de estas ubicaciones y solo se debe acceder a él mediante un método [de](#utility-method-to-access-ugc) utilidad que invoque la API de SRP.

* Ruta raíz = /content/usergenerate/asi/srp-choice
* Nodo UGC para JSRP = /content/usergenerate/asi/jcr/content/community-components/en/comments/jcr:content/content/inclusible/comments/srzd-let_it_be_

*Tenga en cuenta* que para JSRP, el nodo UGC *solo* estará presente en la instancia de AEM (autor o publicación) en la que se introdujo. Si se introduce en una instancia de publicación, la moderación no será posible desde la consola de moderación del autor.

## Información relacionada {#related-information}

* [Información general](srp.md) del proveedor de recursos de almacenamiento de información: Introducción y uso del repositorio
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) : directrices de codificación
* [Refactorización](socialutils.md) de SocialUtils: asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales

