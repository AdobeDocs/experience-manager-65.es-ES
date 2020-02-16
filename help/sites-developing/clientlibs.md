---
title: Uso de bibliotecas del lado del cliente
seo-title: Uso de bibliotecas del lado del cliente
description: AEM proporciona Carpetas de biblioteca del lado del cliente, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe proporcionar cada categoría de código al cliente
seo-description: AEM proporciona Carpetas de biblioteca del lado del cliente, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe proporcionar cada categoría de código al cliente
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Uso de bibliotecas del lado del cliente{#using-client-side-libraries}

Los sitios web modernos dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. Organizar y optimizar el servicio de este código puede ser un problema complicado.

Para ayudar a solucionar este problema, AEM proporciona carpetas **de biblioteca del lado del** cliente, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe proporcionar cada categoría de código al cliente. El sistema de biblioteca del cliente se encarga de producir los vínculos correctos en la página web final para cargar el código correcto.

## Cómo funcionan las bibliotecas del lado del cliente en AEM {#how-client-side-libraries-work-in-aem}

La forma estándar de incluir una biblioteca del lado del cliente (es decir, un archivo JS o CSS) en el HTML de una página es simplemente incluir una `<script>` o `<link>` etiqueta en el JSP de esa página, que contenga la ruta al archivo en cuestión. Por ejemplo,

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Aunque este enfoque funciona en AEM, puede generar problemas cuando las páginas y sus componentes se vuelven complejos. En esos casos, existe el peligro de que se incluyan varias copias de la misma biblioteca de JS en la salida HTML final. Para evitarlo y permitir la organización lógica de las bibliotecas del lado del cliente, AEM utiliza carpetas **de bibliotecas del lado del** cliente.

Una carpeta de biblioteca del lado del cliente es un nodo de repositorio de tipo `cq:ClientLibraryFolder`. Su definición en notación [](https://jackrabbit.apache.org/node-type-notation.html) CND es

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

De forma predeterminada, `cq:ClientLibraryFolder` los nodos se pueden colocar en cualquier lugar dentro del `/apps`repositorio `/libs` , así como en `/etc` los subárboles del repositorio (estos valores predeterminados y otros ajustes se pueden controlar mediante el panel Administrador **de biblioteca HTML de** Adobe Granite de la consola [del sistema](https://localhost:4502/system/console/configMgr)).

Cada una `cq:ClientLibraryFolder` de ellas se rellena con un conjunto de archivos JS y/o CSS, junto con algunos archivos de soporte (véase más adelante). Las propiedades del `cq:ClientLibraryFolder` se configuran de la siguiente manera:

* `categories`:: Identifica las categorías en las que se incluye el conjunto de archivos JS y/o CSS dentro de este `cq:ClientLibraryFolder` . La `categories` propiedad, que tiene varios valores, permite que una carpeta de biblioteca forme parte de más de una categoría (vea a continuación cómo puede resultar útil).

* `dependencies`:: Esta es una lista de otras categorías de biblioteca de cliente de las que depende esta carpeta de biblioteca. Por ejemplo, dados dos `cq:ClientLibraryFolder` nodos `F` y `G`, si un archivo de `F` requiere otro archivo `G` para funcionar correctamente, al menos uno de los `categories` de `G` debe estar entre los `dependencies` de `F`.

* `embed`:: Se utiliza para incrustar código de otras bibliotecas. Si el nodo F incrusta los nodos G y H, el HTML resultante será una concentración de contenido de los nodos G y H.
* `allowProxy`:: Si hay una biblioteca de cliente debajo de `/apps`, esta propiedad permite acceder a ella a través del servlet proxy. Consulte [Localización de una carpeta de biblioteca de cliente y Uso del servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) de bibliotecas de cliente proxy más abajo.

## Referencia a bibliotecas del lado del cliente {#referencing-client-side-libraries}

Dado que HTL es la tecnología preferida para desarrollar sitios AEM, HTL debe utilizarse para incluir bibliotecas de cliente en AEM. Sin embargo, también es posible hacerlo usando JSP.

### Uso de HTL {#using-htl}

En HTL, las bibliotecas de cliente se cargan mediante una plantilla de ayuda proporcionada por AEM, a la que se puede acceder a través de [`data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). Hay tres plantillas disponibles en este archivo, a las que se puede llamar a través de [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** : carga solo los archivos CSS de las bibliotecas de cliente a las que se hace referencia.
* **js** : carga solo los archivos JavaScript de las bibliotecas de cliente a las que se hace referencia.
* **all** : carga todos los archivos de las bibliotecas de cliente a las que se hace referencia (tanto CSS como JavaScript).

Cada plantilla de ayuda espera una `categories` opción para hacer referencia a las bibliotecas de cliente deseadas. Esa opción puede ser una matriz de valores de cadena o una cadena que contenga una lista de valores separados por comas.

Para obtener más información y ejemplos de uso, consulte el documento [Introducción al lenguaje](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries)de plantilla HTML.

### Uso de JSP {#using-jsp}

Agregue una `ui:includeClientLib` etiqueta al código JSP para agregar un vínculo a las bibliotecas de cliente en la página HTML generada. Para hacer referencia a las bibliotecas, se utiliza el valor de la `categories` propiedad del `ui:includeClientLib` nodo.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Por ejemplo, el `/etc/clientlibs/foundation/jquery` nodo es de tipo `cq:ClientLibraryFolder` con una propiedad category de valor `cq.jquery`. El siguiente código de un archivo JSP hace referencia a las bibliotecas:

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

La página HTML generada contiene el siguiente código:

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

Para obtener información completa, incluidos atributos para filtrar bibliotecas JS, CSS o de temas, consulte [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`, que en el pasado se usaba comúnmente para incluir bibliotecas de cliente, ha quedado obsoleto desde AEM 5.6. [ debe `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) utilizarse como se detalla anteriormente.

## Creación de carpetas de la biblioteca cliente {#creating-client-library-folders}

Cree un `cq:ClientLibraryFolder` nodo para definir las bibliotecas de hojas de estilo en cascada y JavaScript y ponerlas a disposición de las páginas HTML. Utilice la `categories` propiedad del nodo para identificar las categorías de biblioteca a las que pertenece.

El nodo contiene uno o varios archivos de origen que, en tiempo de ejecución, se combinan en un solo archivo JS y/o CSS. El nombre del archivo generado es el nombre del nodo con la extensión `.js` o el nombre del `.css` archivo. Por ejemplo, el nodo de biblioteca llamado `cq.jquery` resulta en el archivo generado llamado `cq.jquery.js` o `cq.jquery.css`.

Las carpetas de la biblioteca del cliente contienen los siguientes elementos:

* Los archivos de origen JS y/o CSS que se van a combinar.
* Recursos que admiten estilos CSS, como archivos de imagen.

   **** Nota: Puede utilizar subcarpetas para organizar los archivos de origen.
* Un `js.txt` archivo y/o un `css.txt` archivo que identifica los archivos de origen que se van a combinar en los archivos JS o CSS generados.

![clientlibarch](assets/clientlibarch.png)

Para obtener información sobre los requisitos específicos de las bibliotecas de cliente para widgets, consulte [Uso y ampliación de utilidades](/help/sites-developing/widgets.md).

El cliente web debe tener permisos para acceder al `cq:ClientLibraryFolder` nodo. También puede exponer bibliotecas de áreas seguras del repositorio (consulte Incrustación de código desde otras bibliotecas, más abajo).

### Anulación de bibliotecas en /lib {#overriding-libraries-in-lib}

Las carpetas de la biblioteca del cliente situadas debajo `/apps` tienen prioridad sobre las carpetas con el mismo nombre que se encuentran en `/libs`la misma ubicación. Por ejemplo, `/apps/cq/ui/widgets` tiene prioridad sobre `/libs/cq/ui/widgets`. Cuando estas bibliotecas pertenecen a la misma categoría, se utiliza la siguiente biblioteca `/apps` .

### Localización de una carpeta de biblioteca de cliente y uso del servlet de bibliotecas de cliente proxy {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

En versiones anteriores, las carpetas de la biblioteca de cliente se encontraban debajo `/etc/clientlibs` en el repositorio. Esto aún se admite, pero se recomienda que las bibliotecas de cliente se encuentren ahora en `/apps`. Esto es para localizar las bibliotecas de cliente cerca de las otras secuencias de comandos, que generalmente se encuentran a continuación `/apps` y `/libs`.

>[!NOTE]
>
>Los recursos estáticos situados debajo de la carpeta de la biblioteca del cliente deben estar en una carpeta denominada *resources*. Si no tiene los recursos estáticos, como imágenes, en los *recursos* de la carpeta, no se puede hacer referencia a ellos en una instancia de publicación. Este es un ejemplo: https://localhost:4503/etc.clientlibs/geometrixx/components/clinetlibs/resources/example.gif

>[!NOTE]
>
>Para aislar mejor el código del contenido y la configuración, se recomienda ubicar las bibliotecas cliente debajo `/apps` y exponerlas mediante `/etc.clientlibs` el uso de la `allowProxy` propiedad.

Para que las bibliotecas de cliente de debajo `/apps` sean accesibles, se utiliza un servidor proxy. Las ACL aún se aplican en la carpeta de la biblioteca del cliente, pero el servlet permite que el contenido se lea mediante `/etc.clientlibs/` si la `allowProxy` propiedad se establece en `true`.

Sólo se puede acceder a un recurso estático a través del proxy, si reside debajo de un recurso debajo de la carpeta de la biblioteca del cliente.

Como ejemplo:

* Tiene una clientlib en `/apps/myproject/clientlibs/foo`
* Tiene una imagen estática en `/apps/myprojects/clientlibs/foo/resources/icon.png`

A continuación, establezca la `allowProxy` propiedad en `foo` true.

* A continuación, puede solicitar `/etc.clientlibs/myprojects/clientlibs/foo.js`
* A continuación, puede hacer referencia a la imagen mediante `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>Al utilizar bibliotecas de cliente proxy, la configuración de AEM Dispatcher puede requerir una actualización para garantizar que se permiten los URI con los clientlibs de extensión.

>[!CAUTION]
>
>Adobe recomienda ubicar las bibliotecas de cliente en `/apps` y ponerlas a disposición mediante el servlet proxy. Sin embargo, tenga en cuenta que las mejores prácticas aún requieren que los sitios públicos nunca incluyan nada que se sirva directamente a través de una `/apps` o `/libs` ruta.

### Crear una carpeta de biblioteca de clientes {#create-a-client-library-folder}

1. Abra CRXDE Lite en un navegador web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Seleccione la carpeta en la que desea ubicar la carpeta de la biblioteca del cliente y haga clic en **Crear > Crear nodo**.
1. Escriba un nombre para el archivo de biblioteca y, en la lista Tipo, seleccione `cq:ClientLibraryFolder`. Haga clic en **Aceptar** y, a continuación, en **Guardar todo**.
1. Para especificar la categoría o categorías a las que pertenece la biblioteca, seleccione el `cq:ClientLibraryFolder` nodo, agregue la siguiente propiedad y, a continuación, haga clic en **Guardar todo**:

   * Nombre: categorías
   * Tipo: Cadena
   * Valor: El nombre de la categoría
   * Múltiple: Seleccionar

1. Agregue archivos de origen a la carpeta de la biblioteca por cualquier medio. Por ejemplo, utilice un cliente WebDav para copiar archivos o cree un archivo y cree el contenido manualmente.

   **** Nota: Si lo desea, puede organizar los archivos de origen en subcarpetas.

1. Seleccione la carpeta de la biblioteca del cliente y haga clic en **Crear > Crear archivo**.
1. En el cuadro Nombre de archivo, escriba uno de los siguientes nombres de archivo y haga clic en Aceptar:

   * **`js.txt`**:: Utilice este nombre de archivo para generar un archivo JavaScript.
   * **`css.txt`**:: Utilice este nombre de archivo para generar una hoja de estilo en cascada.

1. Abra el archivo y escriba el siguiente texto para identificar la raíz de la ruta de los archivos de origen:

   `#base=*[root]*`

   Reemplace * `[root]`* con la ruta de la carpeta que contiene los archivos de origen, en relación con el archivo TXT. Por ejemplo, utilice el siguiente texto cuando los archivos de origen estén en la misma carpeta que el archivo TXT:

   `#base=.`

   El siguiente código establece la raíz como la carpeta denominada mobile debajo del `cq:ClientLibraryFolder` nodo:

   `#base=mobile`

1. En las líneas siguientes `#base=[root]`, escriba las rutas de los archivos de origen relativas a la raíz. Coloque cada nombre de archivo en una línea independiente.
1. Haga clic en **Guardar todo**.

### Vinculación a dependencias {#linking-to-dependencies}

Cuando el código de la carpeta de la biblioteca del cliente haga referencia a otras bibliotecas, identifique las demás bibliotecas como dependencias. En JSP, la `ui:includeClientLib` etiqueta que hace referencia a la carpeta de la biblioteca de cliente hace que el código HTML incluya un vínculo al archivo de biblioteca generado, así como las dependencias.

Las dependencias deben ser otras `cq:ClientLibraryFolder`. Para identificar dependencias, agregue una propiedad al `cq:ClientLibraryFolder` nodo con los atributos siguientes:

* **** Nombre:dependencias
* **** Tipo: Cadena[]
* **** Valores: El valor de la propiedad categories del nodo cq:ClientLibraryFolder del que depende la carpeta de biblioteca actual.

Por ejemplo, / `etc/clientlibs/myclientlibs/publicmain` tiene una dependencia en la `cq.jquery` biblioteca. El JSP que hace referencia a la biblioteca de cliente principal genera HTML que incluye el siguiente código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incrustación De Código De Otras Bibliotecas {#embedding-code-from-other-libraries}

Puede incrustar código de una biblioteca de cliente en otra biblioteca de cliente. En tiempo de ejecución, los archivos JS y CSS generados de la biblioteca de incrustación incluyen el código de la biblioteca incrustada.

La incrustación de código es útil para proporcionar acceso a bibliotecas almacenadas en áreas seguras del repositorio.

#### Carpetas de biblioteca de cliente específicas de la aplicación {#app-specific-client-library-folders}

Se recomienda mantener todos los archivos relacionados con la aplicación en la carpeta de la aplicación que aparece a continuación `/app`. También se recomienda denegar el acceso a la `/app` carpeta a los visitantes del sitio Web. Para cumplir ambas prácticas recomendadas, cree una carpeta de biblioteca de cliente debajo de la `/etc` carpeta que incrusta la biblioteca de cliente que se encuentra debajo `/app`.

Utilice la propiedad categories para identificar la carpeta de la biblioteca del cliente que desea incrustar. Para incrustar la biblioteca, agregue una propiedad al `cq:ClientLibraryFolder` nodo de incrustación mediante los siguientes atributos de propiedad:

* **** Nombre: embed
* **** Tipo: Cadena[]
* **** Valor: El valor de la propiedad categories del `cq:ClientLibraryFolder` nodo que se va a incrustar.

#### Uso de la incrustación para minimizar solicitudes {#using-embedding-to-minimize-requests}

En algunos casos, es posible que el HTML final generado para una página típica por la instancia de publicación incluya un número relativamente grande de `<script>` elementos, especialmente si el sitio utiliza información de contexto de cliente para realizar análisis o segmentación. Por ejemplo, en un proyecto no optimizado puede encontrar la siguiente serie de `<script>` elementos en el HTML de una página:

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/underscore.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

En estos casos, puede resultar útil combinar todo el código de biblioteca de cliente necesario en un solo archivo para reducir el número de solicitudes de retorno y de avance al cargar la página. Para ello, puede introducir `embed` las bibliotecas necesarias en la biblioteca de cliente específica de la aplicación mediante la propiedad embed del `cq:ClientLibraryFolder` nodo.

Las siguientes categorías de biblioteca de cliente se incluyen con AEM. Debe incrustar solo aquellos que sean necesarios para el funcionamiento de un sitio en particular. Sin embargo, **debe mantener el orden indicado aquí**:

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

Al incrustar archivos CSS, el código CSS generado utiliza rutas a los recursos que son relativas a la biblioteca de incrustación. Por ejemplo, la biblioteca de acceso público `/etc/client/libraries/myclientlibs/publicmain` incrusta la biblioteca del `/apps/myapp/clientlib` cliente:

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

El `main.css` archivo contiene el siguiente estilo:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

El archivo CSS que genera el `publicmain` nodo contiene el siguiente estilo, utilizando la dirección URL de la imagen original:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### Uso de una biblioteca para grupos móviles específicos {#using-a-library-for-specific-mobile-groups}

Utilice la `channels` propiedad de una carpeta de biblioteca de cliente para identificar el grupo móvil que utiliza la biblioteca. La `channels` propiedad resulta útil cuando las bibliotecas de la misma categoría están diseñadas para diferentes funciones de dispositivo.

Para asociar una carpeta de biblioteca de cliente con un grupo de dispositivos, agregue una propiedad al `cq:ClientLibraryFolder` nodo con los atributos siguientes:

* **** Nombre: canales
* **** Tipo: Cadena[]
* **** Valores: Nombre del grupo móvil. Para excluir la carpeta de la biblioteca de un grupo, anteponga el nombre con un signo de exclamación (&quot;!&quot;).

Por ejemplo, en la tabla siguiente se muestra el valor de la `channels` propiedad para cada carpeta de biblioteca de cliente de la `cq.widgets` categoría:

| Carpeta de biblioteca de cliente | Valor de la propiedad channels |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets/themes/default` | *[ningún valor]* |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

## Uso de preprocesadores {#using-preprocessors}

AEM permite preprocesadores y envíos conectables con compatibilidad con [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS y JavaScript y [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) para JavaScript con YUI definido como preprocesador predeterminado de AEM.

Los preprocesadores conectables permiten un uso flexible que incluye:

* Definición de procesadores de secuencias de comandos que pueden procesar orígenes de secuencias de comandos
* Los procesadores son configurables con opciones
* Los procesadores se pueden utilizar para la minimización, pero también para casos no minimizados
* La clientlib puede definir qué procesador utilizar

>[!NOTE]
>
>De forma predeterminada, AEM utiliza el Compresor YUI. Consulte la documentación [de GitHub del Compresor](https://github.com/yui/yuicompressor/issues) YUI para obtener una lista de los problemas conocidos. Cambiar al compresor GCC para clientes particulares puede resolver algunos problemas observados al usar YUI.

>[!CAUTION]
>
>No coloque una biblioteca minimizada en una biblioteca de cliente. En su lugar, proporcione la biblioteca sin procesar y, si se requiere la minimización, utilice las opciones de los preprocesadores.

### Uso {#usage}

Puede configurar la configuración de preprocesadores por biblioteca de clientes o por todo el sistema.

* Agregue las propiedades de varios valores `cssProcessor` y `jsProcessor` en el nodo clientlibrary

* O defina la configuración predeterminada del sistema mediante la configuración OSGi del Administrador de bibliotecas **HTML**

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

#### Compresor YUI para la minimización de CSS y GCC para JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Escritura para preprocesar y luego GCC para minimizar y ocultar {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

Para obtener más información sobre las opciones del CCG, consulte la documentación [del](https://developers.google.com/closure/compiler/docs/compilation_levels)CCG.

### Definir minificador predeterminado del sistema {#set-system-default-minifier}

La IU se establece como minificador predeterminado en AEM. Para cambiar esto a GCC, siga estos pasos.

1. Vaya al Administrador de configuración Apache Felix en [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Busque y edite el Administrador **de bibliotecas HTML de** Adobe Granite.
1. Active la opción **Minificar** (si no está activada).
1. Establezca el valor Configuración **predeterminada del procesador** JS en `min:gcc`.

   Las opciones se pueden pasar si se separan con un punto y coma, por ejemplo `min:gcc;obfuscate=true`.

1. Click **Save** to save the changes.

## Herramientas de depuración {#debugging-tools}

AEM proporciona varias herramientas para depurar y probar carpetas de bibliotecas de cliente.

### Consulte Archivos incrustados {#see-embedded-files}

Para rastrear el origen del código incrustado o para asegurarse de que las bibliotecas de cliente incrustadas están produciendo los resultados esperados, puede ver los nombres de los archivos que se están incrustando en tiempo de ejecución. Para ver los nombres de archivo, anexe el `debugClientLibs=true` parámetro a la dirección URL de la página web. La biblioteca que se genera contiene `@import` instrucciones en lugar del código incrustado.

En el ejemplo de la sección anterior [Incrustar código de otras bibliotecas](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) , la carpeta de la biblioteca del `/etc/client/libraries/myclientlibs/publicmain` cliente incrusta la carpeta de la biblioteca del `/apps/myapp/clientlib` cliente. La adición del parámetro a la página web produce el siguiente vínculo en el código fuente de la página web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Al abrir el `publicmain.css` archivo se muestra el siguiente código:

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. En el cuadro de dirección del navegador web, anexe el siguiente texto a la dirección URL del HTML:

   `?debugClientLibs=true`
1. Cuando se cargue la página, vea el origen de la página.
1. Haga clic en el vínculo que se proporciona como href para que el elemento de vínculo abra el archivo y vea el código fuente.

### Bibliotecas de clientes de Discover {#discover-client-libraries}

El `/libs/cq/ui/components/dumplibs/dumplibs` componente genera una página de información sobre todas las carpetas de la biblioteca de cliente del sistema. El `/libs/cq/ui/content/dumplibs` nodo tiene el componente como un tipo de recurso. Para abrir la página, utilice la siguiente URL (utilice un host y puerto diferentes según sea necesario):

[https://localhost:4502/libs/cq/ui/content/dumplibs.test.html](https://localhost:4502/libs/cq/ui/content/dumplibs.test.html)

La información incluye la ruta y el tipo de biblioteca (CSS o JS), así como los valores de los atributos de biblioteca, como categorías y dependencias. Las tablas posteriores de la página muestran las bibliotecas de cada categoría y canal.

### Consulte Salida generada {#see-generated-output}

El `dumplibs` componente incluye un selector de prueba que muestra el código fuente que se genera para `ui:includeClientLib` las etiquetas. La página incluye código para diferentes combinaciones de js, css y atributos temáticos.

1. Utilice uno de los siguientes métodos para abrir la página Resultados de la prueba:

   * Desde la `dumplibs.html` página, haga clic en el vínculo del texto de prueba **de resultados de** Clic aquí.

   * Abra la siguiente URL en el explorador web (utilice un host y puerto diferentes según sea necesario):

      [https://localhost:4502/libs/cq/ui/content/dumplibs.html](https://localhost:4502/libs/cq/ui/content/dumplibs.html)
   La página predeterminada muestra el resultado de las etiquetas sin valor para el atributo de categorías.

1. Para ver el resultado de una categoría, escriba el valor de la propiedad de la biblioteca del cliente `categories` y haga clic en **Enviar consulta**.

## Configuración de la Administración de Biblioteca para Desarrollo y Producción {#configuring-library-handling-for-development-and-production}

El servicio Administrador de bibliotecas HTML procesa `cq:ClientLibraryFolder` etiquetas y genera las bibliotecas en tiempo de ejecución. El tipo de entorno, desarrollo o producción determina cómo debe configurar el servicio:

* Aumentar la seguridad: Deshabilitar depuración
* Mejorar el rendimiento: Elimine los espacios en blanco y comprima las bibliotecas.
* Mejorar la legibilidad: Incluya espacios en blanco y no comprima.

Para obtener más información sobre la configuración del servicio, consulte [AEM HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
