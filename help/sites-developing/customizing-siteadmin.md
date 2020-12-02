---
title: Personalización de la consola Sitios web (IU clásica)
seo-title: Personalización de la consola Sitios web (IU clásica)
description: La consola Administración de sitios web se puede ampliar para mostrar columnas personalizadas
seo-description: La consola Administración de sitios web se puede ampliar para mostrar columnas personalizadas
uuid: 9163fdff-5351-477d-b91c-8a74f8b41d34
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: aeb37103-541d-4235-8a78-980b78c8de66
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# Personalización de la consola Sitios web (IU clásica){#customizing-the-websites-console-classic-ui}

## Añadir una columna personalizada en la consola Siteadmin (siteadmin) {#adding-a-custom-column-to-the-websites-siteadmin-console}

La consola Administración de sitios web se puede ampliar para mostrar columnas personalizadas. La consola se basa en un objeto JSON que se puede ampliar creando un servicio OSGI que implemente la interfaz `ListInfoProvider`. Este servicio modifica el objeto JSON que se envía al cliente para crear la consola.

Este tutorial paso a paso explica cómo mostrar una nueva columna en la consola Administración de sitios web implementando la interfaz `ListInfoProvider`. Consiste en los siguientes pasos:

1. [Creación del ](#creating-the-osgi-service) servicio OSGI e implementación del paquete que lo contiene en el servidor AEM.
1. (opcional) [Prueba del nuevo servicio](#testing-the-new-service) mediante la emisión de una llamada JSON para solicitar el objeto JSON que se utiliza para crear la consola.
1. [Mostrar la nueva ](#displaying-the-new-column) columna extendiendo la estructura de nodos de la consola en el repositorio.

>[!NOTE]
>
>Este tutorial también se puede utilizar para ampliar las siguientes consolas de administración:
>
>* la consola Recursos digitales
>* la consola Community

>



### Creación del servicio OSGI {#creating-the-osgi-service}

La interfaz `ListInfoProvider` define dos métodos:

* `updateListGlobalInfo`, para actualizar las propiedades globales de la lista,
* `updateListItemInfo`, para actualizar un solo elemento de lista.

Los argumentos para ambos métodos son:

* `request`, el objeto de solicitud Sling HTTP asociado,
* `info`, el objeto JSON que se va a actualizar, que es, respectivamente, la lista global o el elemento de lista actual,
* `resource`, un recurso de Sling.

La implementación de muestra a continuación:

* Añade una propiedad *starred* para cada elemento, que es `true` si el nombre de página inicio con un *e* y `false` en caso contrario.

* Añade una propiedad *starredCount*, que es global para la lista y contiene el número de elementos de lista con estrella.

Para crear el servicio OSGI:

1. En CRXDE Lite, [cree un paquete](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. Añada el código de muestra siguiente.
1. Cree el paquete.

El nuevo servicio está en funcionamiento.

```java
package com.test;

import com.day.cq.commons.ListInfoProvider;
import com.day.cq.i18n.I18n;
import com.day.cq.wcm.api.Page;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;

@Component(metatype = false)
@Service(value = ListInfoProvider.class)
public class StarredListInfoProvider implements ListInfoProvider {

    private int count = 0;

    public void updateListGlobalInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        info.put("starredCount", count);
        count = 0; // reset for next execution
    }

    public void updateListItemInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        Page page = resource.adaptTo(Page.class);
        if (page != null) {
            // Consider starred if page name starts with 'e'
            boolean starred = page.getName().startsWith("e");
            if (starred) {
                count++;
            }
            I18n i18n = new I18n(request);
            info.put("starred", starred ? i18n.get("Yes") : i18n.get("No"));
        }
    }

}
```

>[!CAUTION]
>
>* La implementación debe decidir, en función de la solicitud y/o el recurso proporcionados, si debe agregar o no la información al objeto JSON.
>* Si la implementación `ListInfoProvider` define una propiedad que ya existe en el objeto de respuesta, su valor será sobrescrito por el que proporcione.

>
>  
Puede utilizar [clasificación de servicio](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) para administrar el orden de ejecución de varias `ListInfoProvider` implementaciones.

### Prueba del nuevo servicio {#testing-the-new-service}

Cuando abre la consola Administración de sitios web y navega por el sitio, el explorador emite una llamada ajax para obtener el objeto JSON que se utiliza para crear la consola. Por ejemplo, cuando se desplaza a la carpeta `/content/geometrixx`, se envía la siguiente solicitud al servidor de AEM para crear la consola:

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

Para asegurarse de que el nuevo servicio se está ejecutando después de haber implementado el paquete que lo contiene:

1. Seleccione la siguiente dirección URL en el navegador:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. La respuesta debe mostrar las nuevas propiedades de la siguiente manera:

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### Visualización de la nueva columna {#displaying-the-new-column}

El último paso consiste en adaptar la estructura de nodos de la consola Administración de sitios web para mostrar la nueva propiedad de todas las páginas de Geometrixx mediante la superposición de `/libs/wcm/core/content/siteadmin`. Proceda de la siguiente manera:

1. En CRXDE Lite, cree la estructura de nodos `/apps/wcm/core/content` con nodos de tipo `sling:Folder` para reflejar la estructura `/libs/wcm/core/content`.

1. Copie el nodo `/libs/wcm/core/content/siteadmin` y péguelo debajo de `/apps/wcm/core/content`.

1. Copie el nodo `/apps/wcm/core/content/siteadmin/grid/assets` en `/apps/wcm/core/content/siteadmin/grid/geometrixx` y cambie sus propiedades:

   * Eliminar **pageText**

   * Establezca **pathRegex** en `/content/geometrixx(/.*)?`
Esto hará que la configuración de cuadrícula esté activa para todos los sitios web de Geometrixx.

   * Establezca **storeProxySuffix** en `.pages.json`

   * Edite la propiedad multivalor **storeReaderFields** y agregue el valor `starred`.

   * Para activar la funcionalidad de MSM, agregue los siguientes parámetros de MSM a la propiedad de varias cadenas **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. Añada un nodo `starred` (de tipo **nt:unestructure**) debajo de `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` con las siguientes propiedades:

   * **dataIndex**:  `starred` de tipo String

   * **header**:  `Starred` de tipo String

   * **xtype**:  `gridcolumn` de tipo String

1. (opcional) Suelte las columnas que no desee mostrar en `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` es una ruta de vanidad a la que, de forma predeterminada, apunta  `/libs/wcm/core/content/siteadmin`.
Para redirigir esto a su versión de siteadmin en `/apps/wcm/core/content/siteadmin` defina la propiedad `sling:vanityOrder` para que tenga un valor mayor que el definido en `/libs/wcm/core/content/siteadmin`. El valor predeterminado es 300, por lo que es adecuado cualquier valor superior.

1. Vaya a la consola Administración de sitios web y vaya al sitio de Geometrixx:
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. La nueva columna llamada **Starred** está disponible y muestra la información personalizada de la siguiente manera:

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>Si varias configuraciones de cuadrícula coinciden con la ruta solicitada definida por la propiedad **pathRegex**, se utilizará la primera, y no la más específica, lo que significa que el orden de las configuraciones es importante.

### Paquete de muestra {#sample-package}

El resultado de este tutorial está disponible en el paquete [Personalización de la Consola de administración de sitios web](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) en Package Share.
