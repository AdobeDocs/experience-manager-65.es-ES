---
title: Uso de bibliotecas del lado del cliente
seo-title: Using Client-Side Libraries
description: AEM proporciona carpetas de biblioteca del lado del cliente, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente
seo-description: AEM provides Client-side Library Folders, which allow you to store your client-side code in the repository, organize it into categories, and define when and how each category of code is to be served to the client
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
source-git-commit: 684474d764ac2a2c187827382e0180e6c0d5259b
workflow-type: tm+mt
source-wordcount: '2861'
ht-degree: 2%

---

# Uso de bibliotecas del lado del cliente{#using-client-side-libraries}

Los sitios web modernos dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. Organizar y optimizar el servicio de este código puede ser un problema complicado.

Para ayudar a resolver este problema, AEM proporciona **Carpetas de biblioteca del lado del cliente**, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente. A continuación, el sistema de biblioteca del lado del cliente se encarga de producir los vínculos correctos en la página web final para cargar el código correcto.

## Cómo funcionan las bibliotecas del lado del cliente en AEM {#how-client-side-libraries-work-in-aem}

La forma estándar de incluir una biblioteca del lado del cliente (es decir, un archivo JS o CSS) en el HTML de una página es simplemente incluir una `<script>` o `<link>` en el JSP de esa página, que contiene la ruta al archivo en cuestión. Por ejemplo,

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Aunque este enfoque funciona en AEM, puede causar problemas cuando las páginas y sus componentes se vuelven complejos. En estos casos existe el peligro de que se incluyan varias copias de la misma biblioteca JS en la salida final del HTML. Para evitarlo y permitir la organización lógica de las bibliotecas del lado del cliente AEM utiliza **carpetas de biblioteca del lado del cliente**.

Una carpeta de biblioteca del lado del cliente es un nodo de repositorio del tipo `cq:ClientLibraryFolder`. Está definido en [Anotación CND](https://jackrabbit.apache.org/node-type-notation.html) es

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

De forma predeterminada, `cq:ClientLibraryFolder` los nodos se pueden colocar en cualquier lugar dentro de `/apps`, `/libs` y `/etc` los subárboles del repositorio (estos valores predeterminados y otros ajustes se pueden controlar mediante la variable **Administrador de biblioteca de HTML de Adobe Granite** del panel [Consola del sistema](https://localhost:4502/system/console/configMgr)).

Cada `cq:ClientLibraryFolder` se rellena con un conjunto de archivos JS o CSS, junto con algunos archivos de apoyo (consulte a continuación). Las propiedades de la variable `cq:ClientLibraryFolder` se configuran de la siguiente manera:

* `categories`: Identifica las categorías en las que el conjunto de archivos JS o CSS dentro de esta `cq:ClientLibraryFolder` otoño. La variable `categories` , al tener varios valores, permite que una carpeta de biblioteca forme parte de más de una categoría (consulte a continuación para obtener información sobre su utilidad).

* `dependencies`: Esta es una lista de otras categorías de biblioteca de cliente de las que depende esta carpeta de biblioteca. Por ejemplo, dado dos `cq:ClientLibraryFolder` nodes `F` y `G`, si un archivo de `F` requiere otro archivo en `G` para funcionar correctamente, al menos una de las `categories` de `G` debe estar entre los `dependencies` de `F`.

* `embed`: Se utiliza para incrustar código de otras bibliotecas. Si el nodo F incrusta los nodos G y H, el HTML resultante será una restricción de contenido de los nodos G y H.
* `allowProxy`: Si una biblioteca de cliente se encuentra en `/apps`, esta propiedad permite acceder a ella a través del servlet proxy. Consulte [Localización de una carpeta de biblioteca de cliente y uso del servlet de bibliotecas de cliente proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) más abajo.

## Referencia a bibliotecas del lado del cliente {#referencing-client-side-libraries}

Como HTL es la tecnología preferida para desarrollar sitios AEM, HTL debe usarse para incluir bibliotecas del lado del cliente en AEM. Sin embargo, también es posible hacerlo usando JSP.

### Uso de HTL {#using-htl}

En HTL, las bibliotecas de cliente se cargan a través de una plantilla de ayuda proporcionada por AEM, a la que se puede acceder mediante [ `data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). Hay tres plantillas disponibles en este archivo a las que se puede llamar mediante [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** : carga solo los archivos CSS de las bibliotecas de cliente a las que se hace referencia.
* **js** : carga solo los archivos JavaScript de las bibliotecas de cliente a las que se hace referencia.
* **all** : carga todos los archivos de las bibliotecas de cliente a las que se hace referencia (tanto CSS como JavaScript).

Cada plantilla de ayuda espera una opción `categories` para hacer referencia a las bibliotecas de cliente deseadas. Esa opción puede ser una matriz de valores de cadena o una cadena que contenga una lista de valores separados por comas.

Para obtener más información y ejemplos de uso, consulte el documento [Introducción al lenguaje de plantilla de HTML](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### Uso de JSP {#using-jsp}

Agregue un `ui:includeClientLib` al código JSP para agregar un vínculo a las bibliotecas de cliente en la página HTML generada. Para hacer referencia a las bibliotecas, utilice el valor de la variable `categories` propiedad de la variable `ui:includeClientLib` nodo .

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Por ejemplo, la variable `/etc/clientlibs/foundation/jquery` el nodo es de tipo `cq:ClientLibraryFolder` con una propiedad de valor categories `cq.jquery`. El siguiente código de un archivo JSP hace referencia a las bibliotecas:

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

La página HTML generada contiene el siguiente código:

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

Para obtener información completa, incluidos los atributos para filtrar las bibliotecas de JS, CSS o temas, consulte [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`, que en el pasado se usaba comúnmente para incluir bibliotecas de cliente, ha quedado obsoleto desde AEM 5.6. [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) en su lugar debe usarse como se detalla más arriba.

## Creación de carpetas de la biblioteca del cliente {#creating-client-library-folders}

Cree un `cq:ClientLibraryFolder` para definir las bibliotecas de hojas de estilo en cascada y JavaScript y ponerlas a disposición de las páginas de HTML. Utilice la variable `categories` propiedad del nodo para identificar las categorías de biblioteca a las que pertenece.

El nodo contiene uno o varios archivos de origen que, durante la ejecución, se combinan en un solo archivo JS o CSS. El nombre del archivo generado es el nombre del nodo con la variable `.js` o `.css` extensión de nombre de archivo. Por ejemplo, el nodo de biblioteca denominado `cq.jquery` tiene como resultado el archivo generado llamado `cq.jquery.js` o `cq.jquery.css`.

Las carpetas de la biblioteca de cliente contienen los siguientes elementos:

* Los archivos de origen JS o CSS que se van a combinar.
* Recursos que admiten estilos CSS, como archivos de imagen.

   **Nota:** Puede utilizar subcarpetas para organizar los archivos de origen.
* One `js.txt` archivo o uno `css.txt` que identifica los archivos de origen que se van a combinar en los archivos JS o CSS generados.

![clientlibarch](assets/clientlibarch.png)

Para obtener información sobre los requisitos específicos de las bibliotecas de cliente para los widgets, consulte [Uso y ampliación de utilidades](/help/sites-developing/widgets.md).

El cliente web debe tener permisos para acceder al `cq:ClientLibraryFolder` nodo . También puede exponer bibliotecas de áreas seguras del repositorio (consulte Incrustación de código desde otras bibliotecas, más adelante).

### Anulación de bibliotecas en /lib {#overriding-libraries-in-lib}

Carpetas de biblioteca de cliente ubicadas más abajo `/apps` tienen prioridad sobre las carpetas con el mismo nombre que se encuentran de manera similar en `/libs`. Por ejemplo, `/apps/cq/ui/widgets` tiene prioridad sobre `/libs/cq/ui/widgets`. Cuando estas bibliotecas pertenecen a la misma categoría, la siguiente biblioteca `/apps` se utiliza.

### Localización de una carpeta de biblioteca de cliente y uso del servlet de bibliotecas de cliente proxy {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

En versiones anteriores, las carpetas de la biblioteca de cliente se ubicaban a continuación `/etc/clientlibs` en el repositorio. Esto sigue siendo compatible, pero se recomienda que las bibliotecas de cliente estén ahora ubicadas en `/apps`. Esto es para localizar las bibliotecas de cliente cerca de las otras secuencias de comandos, que generalmente se encuentran a continuación `/apps` y `/libs`.

>[!NOTE]
>
>Los recursos estáticos situados debajo de la carpeta de la biblioteca del cliente deben estar en una carpeta llamada *recursos*. Si no tiene los recursos estáticos, como imágenes, en la carpeta *recursos*, no se puede hacer referencia a él en una instancia de publicación. Este es un ejemplo: https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>Para aislar mejor el código del contenido y la configuración, se recomienda localizar las bibliotecas de cliente en `/apps` y exponerlos mediante `/etc.clientlibs` aprovechando el `allowProxy` propiedad.

Para las bibliotecas de cliente en `/apps` para que sea accesible, se utiliza un servidor proxy. Las ACL se siguen aplicando en la carpeta de la biblioteca del cliente, pero el servlet permite que el contenido se lea mediante `/etc.clientlibs/` si la variable `allowProxy` la propiedad se establece en `true`.

Solo se puede acceder a un recurso estático a través del proxy, si reside debajo de un recurso debajo de la carpeta de la biblioteca del cliente.

Por ejemplo:

* Tiene una clientlib en `/apps/myproject/clientlibs/foo`
* Tiene una imagen estática en `/apps/myprojects/clientlibs/foo/resources/icon.png`

A continuación, configure la variable `allowProxy` propiedad en `foo` a true.

* A continuación, puede solicitar `/etc.clientlibs/myprojects/clientlibs/foo.js`
* A continuación, puede hacer referencia a la imagen mediante `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>Cuando se utilizan bibliotecas de cliente proxy, la configuración AEM de Dispatcher puede requerir una actualización para garantizar que se permitan los URI con la extensión clientlibs.

>[!CAUTION]
>
>Adobe recomienda colocar bibliotecas de cliente en `/apps` y que estén disponibles mediante el servlet proxy. Sin embargo, tenga en cuenta que las prácticas recomendadas aún requieren que los sitios públicos nunca incluyan nada que se sirva directamente a través de un `/apps` o `/libs` ruta.

### Crear una carpeta de biblioteca de cliente {#create-a-client-library-folder}

1. Abra el CRXDE Lite en un explorador web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Seleccione la carpeta en la que desea localizar la carpeta de la biblioteca del cliente y haga clic en **Crear > Crear nodo**.
1. Escriba un nombre para el archivo de biblioteca y, en la lista Tipo, seleccione `cq:ClientLibraryFolder`. Haga clic en **OK** y haga clic en **Guardar todo**.
1. Para especificar la categoría o categorías a las que pertenece la biblioteca, seleccione la opción `cq:ClientLibraryFolder` , agregue la siguiente propiedad y, a continuación, haga clic en **Guardar todo**:

   * Nombre: categories
   * Tipo: Cadena
   * Valor: El nombre de la categoría
   * Varios: Select

1. Agregue archivos de origen a la carpeta de la biblioteca por cualquier medio. Por ejemplo, utilice un cliente WebDav para copiar archivos o cree un archivo y cree el contenido manualmente.

   **Nota:** Si lo desea, puede organizar los archivos de origen en subcarpetas.

1. Seleccione la carpeta de la biblioteca del cliente y haga clic en **Crear > Crear archivo**.
1. En el cuadro de nombre de archivo, escriba uno de los siguientes nombres de archivo y haga clic en Aceptar:

   * **`js.txt`:** Utilice este nombre de archivo para generar un archivo JavaScript.
   * **`css.txt`:** Utilice este nombre de archivo para generar una hoja de estilo en cascada.

1. Abra el archivo y escriba el siguiente texto para identificar la raíz de la ruta de los archivos de origen:

   `#base=*[root]*`

   Reemplazar * `[root]`* con la ruta a la carpeta que contiene los archivos de origen, en relación con el archivo TXT. Por ejemplo, use el siguiente texto cuando los archivos de origen estén en la misma carpeta que el archivo TXT:

   `#base=.`

   El siguiente código establece la raíz como la carpeta denominada mobile debajo de la variable `cq:ClientLibraryFolder` nodo:

   `#base=mobile`

1. En las líneas siguientes `#base=[root]`, escriba las rutas de los archivos de origen relativas a la raíz. Coloque cada nombre de archivo en una línea independiente.
1. Haga clic en **Guardar todo**.

### Vinculación a dependencias {#linking-to-dependencies}

Cuando el código de la carpeta de la biblioteca de cliente haga referencia a otras bibliotecas, identifique las demás bibliotecas como dependencias. En el JSP, la variable `ui:includeClientLib` que hace referencia a la carpeta de la biblioteca del cliente hace que el código del HTML incluya un vínculo al archivo de biblioteca generado, así como las dependencias.

Las dependencias deben ser otras `cq:ClientLibraryFolder`. Para identificar dependencias, agregue una propiedad a su `cq:ClientLibraryFolder` con los siguientes atributos:

* **Nombre:** dependencias
* **Tipo:** Cadena[]
* **Valores:** El valor de la propiedad categories del nodo cq:ClientLibraryFolder del que depende la carpeta de biblioteca actual.

Por ejemplo, / `etc/clientlibs/myclientlibs/publicmain` tiene una dependencia de `cq.jquery` biblioteca. El JSP que hace referencia a la biblioteca de cliente principal genera un HTML que incluye el siguiente código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incrustación De Código Desde Otras Bibliotecas {#embedding-code-from-other-libraries}

Puede incrustar código de una biblioteca de cliente en otra biblioteca de cliente. Durante el tiempo de ejecución, los archivos JS y CSS generados de la biblioteca de incrustación incluyen el código de la biblioteca incrustada.

La incrustación de código es útil para proporcionar acceso a las bibliotecas almacenadas en áreas seguras del repositorio.

#### Carpetas de biblioteca de cliente específicas de la aplicación {#app-specific-client-library-folders}

Se recomienda mantener todos los archivos relacionados con la aplicación en la carpeta de la aplicación siguiente `/apps`. También es una práctica recomendada denegar el acceso de los visitantes del sitio web al `/app` carpeta. Para satisfacer ambas prácticas recomendadas, cree una carpeta de biblioteca de cliente a continuación. `/apps`y haga que sea accesible a través del servlet proxy como se describe en [Localización de una carpeta de biblioteca de cliente y uso del servlet de bibliotecas de cliente proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

Utilice la propiedad categories para identificar la carpeta de biblioteca de cliente que desea incrustar. Para incrustar la biblioteca, agregue una propiedad a la incrustación `cq:ClientLibraryFolder` utilizando los siguientes atributos de propiedad:

* **Nombre:** embed
* **Tipo:** Cadena[]
* **Valor:** El valor de la propiedad categories de la `cq:ClientLibraryFolder` para incrustar.

#### Usar la incrustación para minimizar las solicitudes {#using-embedding-to-minimize-requests}

En algunos casos, es posible que descubra que el HTML final generado para la página típica por la instancia de publicación incluye un número relativamente grande de `<script>` , especialmente si el sitio utiliza información de ClientContext para análisis o segmentación. Por ejemplo, en un proyecto no optimizado puede encontrar la siguiente serie de `<script>` elementos en el HTML de una página:

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

En estos casos, puede resultar útil combinar todo el código de biblioteca de cliente necesario en un solo archivo para reducir el número de solicitudes de retorno y de adelante al cargar la página. Para ello, puede `embed` las bibliotecas necesarias en la biblioteca de cliente específica de la aplicación mediante la propiedad embed de la variable `cq:ClientLibraryFolder` nodo .

Las siguientes categorías de biblioteca de cliente se incluyen con AEM. Debe incrustar solo aquellos que sean necesarios para el funcionamiento de un sitio en particular. Sin embargo, **debe mantener el orden enumerado aquí**:

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

#### Rutas en archivos CSS {#paths-in-css-files}

Al incrustar archivos CSS, el código CSS generado utiliza rutas a los recursos que son relativas a la biblioteca de incrustación. Por ejemplo, la biblioteca accesible al público `/etc/client/libraries/myclientlibs/publicmain` incrusta el `/apps/myapp/clientlib` biblioteca de cliente:

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

La variable `main.css` contiene el siguiente estilo:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

El archivo CSS en el que `publicmain` genera contiene el siguiente estilo, utilizando la URL de la imagen original:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### Usar una biblioteca para grupos móviles específicos {#using-a-library-for-specific-mobile-groups}

Utilice la variable `channels` propiedad de una carpeta de biblioteca de cliente para identificar el grupo móvil que utiliza la biblioteca. La variable `channels` La propiedad de es útil cuando las bibliotecas de la misma categoría están diseñadas para diferentes funciones de dispositivo.

Para asociar una carpeta de biblioteca de cliente con un grupo de dispositivos, agregue una propiedad a su `cq:ClientLibraryFolder` con los siguientes atributos:

* **Nombre:** canales
* **Tipo:** Cadena[]
* **Valores:** Nombre del grupo móvil. Para excluir la carpeta de la biblioteca de un grupo, anteponga el nombre con un signo de exclamación (&quot;!&quot;).

Por ejemplo, la tabla siguiente enumera el valor de la variable `channels` propiedad para cada carpeta de biblioteca cliente de `cq.widgets` categoría:

| Carpeta de biblioteca de cliente | Valor de la propiedad channels |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## Uso de preprocesadores {#using-preprocessors}

AEM permite preprocesadores conectables y se envían con soporte para [Compresor YUI](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS y JavaScript y [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) para JavaScript con YUI establecido como preprocesador predeterminado AEM.

Los preprocesadores conectables permiten un uso flexible, que incluye:

* Definición de procesadores de secuencias de comandos que pueden procesar orígenes de secuencias de comandos
* Los procesadores son configurables con opciones
* Los procesadores pueden utilizarse para la minificación, pero también para casos no minificados
* La clientlib puede definir qué procesador utilizar

>[!NOTE]
>
>De forma predeterminada, AEM utiliza el compresor YUI. Consulte la [Documentación del compresor YUI GitHub](https://github.com/yui/yuicompressor/issues) para obtener una lista de los problemas conocidos. Cambiar al compresor GCC para clientlibs particulares puede resolver algunos problemas observados al usar YUI.

>[!CAUTION]
>
>No coloque una biblioteca minimizada en una biblioteca cliente. En su lugar, proporcione la biblioteca sin procesar y, si es necesario minificar, utilice las opciones de los preprocesadores.

### Uso {#usage}

Puede elegir configurar la configuración de los preprocesadores por clientlibrary o por todo el sistema.

* Adición de las propiedades multivalor `cssProcessor` y `jsProcessor` en el nodo clientlibrary

* O bien, defina la configuración predeterminada del sistema a través del **Administrador de bibliotecas de HTML** Configuración de OSGi

Una configuración de preprocesador en el nodo clientlib tiene prioridad sobre la configuración OSGI.

### Formato y ejemplos {#format-and-examples}

#### Formato {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### Compresor YUI para la minificación de CSS y GCC para JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Escrito previamente y, a continuación, GCC para minimizar y ofuscar {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### Opciones adicionales de GCC {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Para obtener más información sobre las opciones de GCC, consulte la [Documentación de GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

### Definir minificador predeterminado del sistema {#set-system-default-minifier}

YUI se establece como minificador predeterminado en AEM. Para cambiar esto a GCC, siga estos pasos.

1. Vaya al Administrador de configuración de Apache Felix en [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Busque y edite el **Administrador de biblioteca de HTML de Adobe Granite**.
1. Active la variable **Minificar** (si no está activada).
1. Establezca el valor **Configuraciones predeterminadas del procesador JS** a `min:gcc`.

   Las opciones se pueden pasar si se separan con un punto y coma, por ejemplo `min:gcc;obfuscate=true`.

1. Haga clic en **Guardar** para guardar los cambios.

## Herramientas de depuración {#debugging-tools}

AEM proporciona varias herramientas para depurar y probar carpetas de biblioteca de cliente.

### Consulte Archivos incrustados {#see-embedded-files}

Para rastrear el origen del código incrustado o para asegurarse de que las bibliotecas de cliente incrustadas producen los resultados esperados, puede ver los nombres de los archivos que se están incrustando durante la ejecución. Para ver los nombres de los archivos, añada la variable `debugClientLibs=true` a la dirección URL de la página web. La biblioteca que se genera contiene `@import` en lugar del código incrustado.

En el ejemplo de la [Incrustación De Código Desde Otras Bibliotecas](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) , la variable `/etc/client/libraries/myclientlibs/publicmain` la carpeta de la biblioteca de cliente incrusta la variable `/apps/myapp/clientlib` carpeta de biblioteca de cliente. Añadir el parámetro a la página web produce el siguiente vínculo en el código fuente de la página web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Apertura del `publicmain.css` muestra el siguiente código:

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. En el cuadro de dirección de su explorador web, añada el siguiente texto a la dirección URL de su HTML:

   `?debugClientLibs=true`
1. Cuando se carga la página, vea el origen de la página.
1. Haga clic en el vínculo que se proporciona como href para que el elemento del vínculo abra el archivo y vea el código fuente.

### Descubra las bibliotecas de clientes {#discover-client-libraries}

La variable `/libs/cq/granite/components/dumplibs/dumplibs` genera una página de información sobre todas las carpetas de la biblioteca cliente en el sistema. La variable `/libs/granite/ui/content/dumplibs` tiene el componente como tipo de recurso. Para abrir la página, use la siguiente dirección URL (cambie el host y el puerto según sea necesario):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

La información incluye la ruta y el tipo de biblioteca (CSS o JS), así como los valores de los atributos de biblioteca, como las categorías y dependencias. Las tablas posteriores de la página muestran las bibliotecas de cada categoría y canal.

### Consulte Salida generada {#see-generated-output}

La variable `dumplibs` incluye un selector de prueba que muestra el código fuente generado para `ui:includeClientLib` etiquetas. La página incluye código para diferentes combinaciones de js, css y atributos temáticos.

1. Utilice uno de los métodos siguientes para abrir la página Salida de prueba :

   * En el `dumplibs.html` , haga clic en el vínculo de la página **Haga clic aquí para probar los resultados** texto.

   * Abra la siguiente URL en su explorador web (use un host y puerto diferentes según sea necesario):

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   La página predeterminada muestra resultados para etiquetas sin valor para el atributo categories .

1. Para ver el resultado de una categoría, escriba el valor de la biblioteca de cliente `categories` propiedad y haga clic en **Enviar consulta**.

## Configuración de la administración de bibliotecas para desarrollo y producción {#configuring-library-handling-for-development-and-production}

Procesos del servicio Administrador de bibliotecas de HTML `cq:ClientLibraryFolder` etiqueta y genera las bibliotecas en tiempo de ejecución. El tipo de entorno, desarrollo o producción, determina cómo debe configurar el servicio:

* Mayor seguridad: Deshabilitar depuración
* Mejore el rendimiento: Elimine los espacios en blanco y comprima las bibliotecas.
* Mejore la legibilidad: Incluir espacios en blanco y no comprimir.

Para obtener información sobre la configuración del servicio, consulte [Administrador de biblioteca del HTML AEM](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
