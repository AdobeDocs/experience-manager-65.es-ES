---
title: Configuraciones y el navegador de configuración
description: Comprender AEM configuraciones y cómo administran la configuración del espacio de trabajo en AEM.
translation-type: tm+mt
source-git-commit: 8f5159d92f64b218d9e2e72d119e6de9d3e01ce6
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---


# Configuraciones y el navegador de configuración {#configuration-browser}

AEM configuraciones sirven para administrar la configuración en AEM y servir como espacios de trabajo.

## ¿Qué es una configuración? {#what-is-a-configuration}

Se puede considerar una configuración desde dos puntos de vista diferentes.

* [Un administrador](#configurations-administrator) utiliza configuraciones como espacios de trabajo dentro de AEM para definir y administrar grupos de configuraciones.
* [Un desarrollador](#configurations-developer) utiliza el mecanismo de configuración subyacente que implementa las configuraciones para persistir y buscar los ajustes en AEM.

En resumen: desde el punto de vista del administrador, las configuraciones son la forma en que se crean los espacios de trabajo para administrar la configuración en AEM, mientras que el desarrollador debe comprender cómo AEM utiliza y administra estas configuraciones dentro del repositorio.

Independientemente de su perspectiva, las configuraciones tienen dos propósitos principales en AEM:

* Las configuraciones habilitan ciertas funciones para determinados grupos de usuarios.
* Las configuraciones definen los derechos de acceso para esas funciones.

## Configuraciones como administrador {#configurations-administrator}

Tanto el administrador de AEM como los autores pueden considerar las configuraciones como espacios de trabajo. Estos espacios de trabajo se pueden utilizar para reunir grupos de configuraciones, así como el contenido asociado, con fines organizativos, mediante la implementación de derechos de acceso para dichas funciones.

Se pueden crear configuraciones para muchas funciones distintas dentro de AEM.

* [Configuraciones de nube](/help/sites-administering/configurations.md)
* [Segmentos de Context Hub](/help/sites-administering/segmentation.md)
* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
* [Plantillas editables](/help/sites-authoring/templates.md)

### Ejemplo {#administrator-example}

Por ejemplo, un administrador puede crear dos configuraciones para Plantillas editables.

* WKND-General
* WKND-Magazine

A continuación, el administrador puede crear plantillas de página generales mediante la configuración de WKND-General y, a continuación, plantillas específicas de la revista en WKND-Magazine.

El administrador puede luego asociar el WKND-General con todo el contenido del sitio WKND. Sin embargo, la configuración de WKND-Magazine solo se asociaría con el sitio de la revista.

Haciendo esto:

* Cuando un autor de contenido crea una nueva página para la revista, puede elegir entre plantillas generales (WKND-General) o plantillas de revista (WKND-Magazine).
* Cuando un autor de contenido crea una nueva página para otra parte del sitio que no es la revista, solo puede elegir entre las plantillas generales (WKND-General).

Se pueden realizar configuraciones similares no solo para plantillas editables, sino también para configuraciones de nube, segmentos de ContextHub y modelos de fragmentos de contenido.

### Uso del navegador de configuración {#using-configuration-browser}

El navegador de configuración permite a un administrador crear, administrar y configurar fácilmente los derechos de acceso a las configuraciones en AEM.

>[!NOTE]
>
>Solo es posible crear configuraciones mediante el navegador de configuración si el usuario tiene `admin` derechos. `admin` también se requieren derechos para asignar derechos de acceso a la configuración o para modificar una configuración.

#### Creación de una configuración {#creating-a-configuration}

Es muy sencillo crear una nueva configuración en AEM mediante el navegador de configuración.

1. Inicie sesión en AEM como Cloud Service y, en el menú principal, seleccione **Herramientas** -> **General** -> Navegador **** de configuración.
1. Haga clic o pulse **Crear**.
1. Proporcione un **Título** y un **Nombre** para la configuración.

   ![Crear configuración](assets/configuration-create.png)

   * El **Título** debe ser descriptivo.
   * El **nombre** se convertirá en el nombre del nodo en el repositorio.
      * Se generará automáticamente en función del título y se ajustará según las convenciones de nombres [AEM.](/help/sites-developing/naming-conventions.md)
      * Puede ajustarse si es necesario.
1. Compruebe el tipo de configuraciones que desea permitir.
   * [Configuraciones de nube](/help/sites-administering/configurations.md)
   * [Segmentos de Context Hub](/help/sites-administering/segmentation.md)
   * [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
   * [Plantillas editables](/help/sites-authoring/templates.md)
1. Haga clic o pulse **Crear**.

>[!TIP]
>
>Las configuraciones se pueden anidar.

#### Edición de configuraciones y sus derechos de acceso {#access-rights}

Si considera que las configuraciones son espacios de trabajo, se pueden establecer derechos de acceso en esas configuraciones para imponer quién puede acceder a esos espacios de trabajo y quién no.

1. Inicie sesión en AEM como Cloud Service y, en el menú principal, seleccione **Herramientas** -> **General** -> Navegador **** de configuración.
1. Seleccione la configuración que desee modificar y toque o haga clic en **Propiedades** en la barra de herramientas.
1. Seleccione las funciones adicionales que desee agregar a la configuración
   >[!NOTE]
   >
   >Una vez creada la configuración, no es posible anular la selección de una función.
1. Utilice el botón Permisos **** efectivos para la vista de una matriz de funciones y los permisos que se conceden actualmente a las configuraciones.
   ![Ventana de permisos efectivos](assets/configuration-effective-permissions.png)
1. Para asignar nuevos permisos, introduzca el nombre de usuario o grupo en el campo **Seleccionar usuario o grupo** de la sección **Añadir nuevos permisos** .
   * El campo **Seleccionar usuario o grupo** oferta la finalización automática en función de los usuarios y las funciones existentes.
1. Seleccione el usuario o la función correspondiente en los resultados de autocompletar.
   * Puede seleccionar más de un usuario o función.
1. Compruebe las opciones de acceso que deben tener los usuarios o roles seleccionados y haga clic en **Añadir**.
   ![Añadir derechos de acceso a una configuración](assets/configuration-edit.png)
1. Repita los pasos para seleccionar usuarios o funciones y asignar derechos de acceso adicionales según sea necesario.
1. Toque o haga clic en **Guardar y cerrar** cuando termine.

## Configuraciones como desarrollador {#configurations-developer}

Como desarrollador, es importante saber cómo AEM como Cloud Service trabaja con las configuraciones y cómo procesa la resolución de la configuración.

### Separación de configuración y contenido {#separation-of-config-and-content}

Aunque el [administrador y los usuarios pueden considerar las configuraciones como lugares de trabajo](#configurations-administrator) para administrar diferentes configuraciones y contenido, es importante comprender que las configuraciones y el contenido se almacenan y administran por separado por AEM en el repositorio.

* `/content` es el hogar de todo el contenido.
* `/conf` es el hogar de toda la configuración.

El contenido hace referencia a su configuración asociada mediante una `cq:conf` propiedad. AEM realiza una búsqueda basada en el contenido y es `cq:conf` propiedad contextual encontrar la configuración adecuada.

### Ejemplo {#developer-example}

Para este ejemplo, supongamos que tiene algún código de aplicación que esté interesado en la configuración de DAM.

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

El punto de partida de todas las búsquedas de configuración es un recurso de contenido, generalmente en algún lugar debajo de `/content`. Podría ser una página, un componente dentro de una página, un recurso o una carpeta DAM. Este es el contenido real para el que buscamos la configuración correcta que se aplica en este contexto.

Ahora con el `Conf` objeto en cuestión, podemos recuperar el elemento de configuración específico que nos interesa. En este caso lo es `dam/imageserver`, que es una colección de configuraciones relacionadas con el `imageserver`. La `getItem` llamada devuelve un `ValueMap`. Luego leemos una propiedad de `bgkcolor` cadena y proporcionamos un valor predeterminado de &quot;FFFFFF&quot; en caso de que la propiedad (o todo el elemento de configuración) no esté presente.

Ahora veamos el contenido JCR correspondiente:

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wkns
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

En este ejemplo, asumimos una carpeta DAM específica de WKND aquí y una configuración correspondiente. A partir de esa carpeta `/content/dam/wknd`, veremos que hay una propiedad de cadena denominada `cq:conf` que hace referencia a la configuración que debe aplicarse al subárbol. La propiedad generalmente se establece en la parte `jcr:content` de una página o carpeta de recursos. Estos `conf` vínculos son explícitos, por lo que es fácil seguirlos con solo mirar el contenido de CRXDE.

Si saltamos dentro `/conf`, seguimos la referencia y vemos que hay un `/conf/wknd` nodo. Esta es una configuración. Tenga en cuenta que su búsqueda es completamente transparente para el código de la aplicación. El código de ejemplo nunca tiene una referencia dedicada a él, está oculto detrás del `Conf` objeto. La configuración que se aplica se controla completamente a través del contenido JCR.

Vemos que la configuración contiene un nodo con nombre fijo `settings` que contiene los elementos reales, incluyendo los `dam/imageserver` que necesitamos en nuestro caso. Este elemento puede considerarse como un &quot;documento de configuración&quot; y normalmente está representado por un elemento `cq:Page` que incluye un contenido `jcr:content` real.

Finalmente, vemos la propiedad `bgkcolor` que necesita nuestro código de muestra. El `ValueMap` resultado `getItem` se basa en el `jcr:content` nodo de la página.

### Resolución de configuración {#configuration-resolution}

El ejemplo básico anterior mostraba una configuración única. Sin embargo, hay muchos casos en los que desea tener configuraciones diferentes, como una configuración global predeterminada, una diferente para cada marca y tal vez una específica para sus subproyectos.

Para admitir esto, la búsqueda de configuración en AEM tiene herencia y mecanismo de reserva en el siguiente orden de preferencia:

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * Configuración específica a la que se hace referencia desde `cq:conf` algún punto `/content`
   * La jerarquía es arbitraria y se puede diseñar de la misma manera que la estructura del sitio, no es asunto del código de la aplicación saber esto
   * Modificable en tiempo de ejecución por usuarios con privilegios de configuración
1. `/conf/<siteconfig>/<parentconfig>`
   * Padres de recorrido para configuraciones de reserva
   * Modificable en tiempo de ejecución por usuarios con privilegios de configuración
1. `/conf/<siteconfig>`
   * Padres de recorrido para configuraciones de reserva
   * Modificable en tiempo de ejecución por usuarios con privilegios de configuración
1. `/conf/global`
   * Configuración global del sistema
   * Generalmente valores predeterminados globales para la instalación
   * Definido por una `admin` función
   * Modificable en tiempo de ejecución por usuarios con privilegios de configuración
1. `/apps`
   * Valores predeterminados de la aplicación
   * Se ha corregido la implementación de la aplicación
   * Sólo lectura en tiempo de ejecución
1. `/libs`
   * Valores predeterminados del producto AEM
   * Solo se puede cambiar por Adobe, no se permite el acceso al proyecto
   * Se ha corregido la implementación de la aplicación
   * Sólo lectura en tiempo de ejecución

### Uso de configuraciones {#using-configurations}

Las configuraciones de AEM se basan en configuraciones según el contexto de Sling. Los paquetes de Sling proporcionan una API de servicio que puede utilizarse para obtener configuraciones según el contexto. Las configuraciones según el contexto son configuraciones relacionadas con un recurso de contenido o un árbol de recursos, como se [describió en el ejemplo anterior.](#developer-example)

Para obtener más información sobre las configuraciones según el contexto, ejemplos y cómo utilizarlos, [consulte la documentación de Sling.](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr Web Console {#confmgr-web-console}

Para depurar y probar, hay una consola web **ConfMgr** en `https://<host>:<port>/system/console/conf`, que puede mostrar configuraciones para una ruta/elemento determinado.

![ConfMgr](assets/configuration-confmgr.png)

Simplemente proporcione:

* **Ruta de contenido**
* **Elemento**
* **Usuario**

Haga clic en **Resolver** para ver qué configuraciones se resuelven y recibir código de muestra que resuelva dichas configuraciones.

### Consola Web de configuración según el contexto {#context-aware-web-console}

Para depurar y probar, existe una consola web de configuración **según el** contexto en `https://<host>:<port>/system/console/slingcaconfig`, que permite consultar configuraciones según el contexto en el repositorio y ver sus propiedades.

![Consola web de configuración según el contexto](assets/configuration-context-aware-console.png)

Simplemente proporcione:

* **Ruta de contenido**
* **Nombre de configuración**

Haga clic en **Resolver** para recuperar las rutas de contexto y propiedades asociadas para la configuración seleccionada.
