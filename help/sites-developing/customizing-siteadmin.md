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
source-git-commit: 4d47310ebf9d450de52c925642978ba92ef9c1d4

---


# Personalización de la consola Sitios web (IU clásica){#customizing-the-websites-console-classic-ui}

## Adición de una columna personalizada a la consola Siteadmin (Siteadmin) {#adding-a-custom-column-to-the-websites-siteadmin-console}

La consola Administración de sitios web se puede ampliar para mostrar columnas personalizadas. La consola se basa en un objeto JSON que se puede ampliar creando un servicio OSGI que implemente la `ListInfoProvider` interfaz. Este servicio modifica el objeto JSON que se envía al cliente para crear la consola.

Este tutorial paso a paso explica cómo mostrar una nueva columna en la consola Administración de sitios web implementando la `ListInfoProvider` interfaz. Consiste en los siguientes pasos:

1. [Creación del servicio](#creating-the-osgi-service) OSGI e implementación del paquete que lo contiene en el servidor AEM.
1. (opcional) [Prueba del nuevo servicio](#testing-the-new-service) mediante la emisión de una llamada JSON para solicitar el objeto JSON que se utiliza para crear la consola.
1. [Mostrar la nueva columna](#displaying-the-new-column) extendiendo la estructura de nodos de la consola en el repositorio.

>[!NOTE]
>
>Este tutorial también se puede utilizar para ampliar las siguientes consolas de administración:
>
>* la consola Recursos digitales
>* la consola Community
>



### Creación del servicio OSGI {#creating-the-osgi-service}

La `ListInfoProvider` interfaz define dos métodos:

* `updateListGlobalInfo`, para actualizar las propiedades globales de la lista,
* `updateListItemInfo`, para actualizar un solo elemento de lista.

Los argumentos para ambos métodos son:

* `request`, el objeto de solicitud Sling HTTP asociado,
* `info`, el objeto JSON que se va a actualizar, que es, respectivamente, la lista global o el elemento de lista actual,
* `resource`, un recurso de Sling.

La implementación de muestra a continuación:

* Agrega una propiedad *estelar* para cada elemento, que es `true` si el nombre de la página comienza con un *e* y `false` no lo hace.

* Agrega una *propiedad starredCount* , que es global para la lista y contiene el número de elementos de la lista con estrellas.

Para crear el servicio OSGI:

1. En CRXDE Lite, [cree un paquete](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. Agregue el código de muestra siguiente.
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
>* Si la `ListInfoProvider` implementación define una propiedad que ya existe en el objeto de respuesta, su valor será sobrescrito por el que proporcione.
   >  Puede utilizar [la clasificación](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) del servicio para administrar el orden de ejecución de varias `ListInfoProvider` implementaciones.
>



### Prueba del nuevo servicio {#testing-the-new-service}

Cuando abre la consola Administración de sitios web y navega por el sitio, el explorador emite una llamada ajax para obtener el objeto JSON que se utiliza para crear la consola. Por ejemplo, cuando se desplaza a la `/content/geometrixx` carpeta, se envía la siguiente solicitud al servidor AEM para crear la consola:

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&limit=30&predicate=siteadmin)

Para asegurarse de que el nuevo servicio se está ejecutando después de haber implementado el paquete que lo contiene:

1. Seleccione la siguiente dirección URL en el navegador:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&limit=30&predicate=siteadmin)

1. La respuesta debe mostrar las nuevas propiedades de la siguiente manera:

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### Visualización de la nueva columna {#displaying-the-new-column}

El último paso consiste en adaptar la estructura de nodos de la consola Administración de sitios web para mostrar la nueva propiedad de todas las páginas de Geometrixx superponiendo `/libs/wcm/core/content/siteadmin`. Proceda de la siguiente manera:

1. En CRXDE Lite, cree la estructura de nodos `/apps/wcm/core/content` con nodos de tipo `sling:Folder` para reflejar la estructura `/libs/wcm/core/content`.

1. Copie el nodo `/libs/wcm/core/content/siteadmin` y péguelo debajo `/apps/wcm/core/content`.

1. Copie el nodo `/apps/wcm/core/content/siteadmin/grid/assets` a `/apps/wcm/core/content/siteadmin/grid/geometrixx` y cambie sus propiedades:

   * Eliminar **pageText**

   * Establecer **pathRegex** en `/content/geometrixx(/.*)?`Esto hará que la configuración de cuadrícula esté activa para todos los sitios web de geometrixx.

   * Establecer **storeProxySuffix** en `.pages.json`

   * Edite la propiedad multivalor **storeReaderFields** y agregue el `starred` valor.

   * Para activar la funcionalidad MSM, agregue los siguientes parámetros MSM a la propiedad multi-String **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. Agregue un `starred` nodo (de tipo **nt:unstructure**) a continuación `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` con las siguientes propiedades:

   * **dataIndex**: `starred` de tipo Cadena

   * **header**: `Starred` de tipo Cadena

   * **xtype**: `gridcolumn` de tipo Cadena

1. (opcional) Suelte las columnas que no desee mostrar en `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` es una ruta de vanidad a la que, de forma predeterminada, apunta `/libs/wcm/core/content/siteadmin`.
Para redirigir esto a su versión de siteadmin `/apps/wcm/core/content/siteadmin` defina la propiedad `sling:vanityOrder` para que tenga un valor superior al definido en `/libs/wcm/core/content/siteadmin`. El valor predeterminado es 300, por lo que es adecuado cualquier valor superior.

1. Vaya a la consola Administración de sitios web y vaya al sitio de Geometrixx:
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. La nueva columna denominada **Estrella** está disponible y muestra la información personalizada de la siguiente manera:

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>Si varias configuraciones de cuadrícula coinciden con la ruta solicitada definida por la propiedad **pathRegex** , se utilizará la primera y no la más específica, lo que significa que el orden de las configuraciones es importante.

### Paquete de muestra {#sample-package}

El resultado de este tutorial está disponible en [Personalización del paquete de la Consola](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) de administración de sitios web en Uso compartido de paquetes.
