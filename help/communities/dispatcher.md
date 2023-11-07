---
title: Configurar Dispatcher para comunidades
description: Aprenda a configurar Dispatcher para AEM Communities a fin de garantizar el funcionamiento adecuado de los sitios de la comunidad.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
exl-id: fb4e3973-2193-4bb5-8120-bf2f3ec80112
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 12%

---

# Configurar Dispatcher para comunidades {#configuring-dispatcher-for-communities}

## Comunidades AEM {#aem-communities}

Para AEM Communities, es necesario configurar Dispatcher para garantizar el funcionamiento adecuado de [sitios de la comunidad](overview.md#community-sites). Es necesario realizar configuraciones adicionales al incluir funciones como el inicio de sesión social.

Para saber qué es necesario para la implementación y el diseño de sitios específicos

* Contacto con el [Servicio de atención al cliente](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home&amp;lang=es#support)

Consulte también la sección principal [Documentación de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es).

## Almacenamiento en caché de Dispatcher {#dispatcher-caching}

### Información general {#overview}

El almacenamiento en caché de Dispatcher para AEM Communities es la capacidad de Dispatcher para ofrecer versiones en caché completas de las páginas de un sitio de la comunidad.

Actualmente, solo es compatible con visitantes anónimos del sitio, como los usuarios que navegan por el sitio de la comunidad o aterrizan en una página de la comunidad como resultado de una búsqueda, y con los motores de búsqueda que indexan las páginas. La ventaja es que los usuarios anónimos y los motores de búsqueda experimentan un rendimiento mejorado.

En el caso de los miembros conectados, Dispatcher omite la caché y retransmite las solicitudes directamente al editor, de modo que todas las páginas se generan y entregan de forma dinámica.

Cuando se configura para admitir el almacenamiento en caché de Dispatcher, se agrega una caducidad máxima basada en TTL al encabezado para garantizar que las páginas en caché de Dispatcher estén actualizadas.

### Requisitos  {#requirements}

* Versión 4.1.2 o posterior de Dispatcher (consulte [Instalación de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html?lang=en) para la última versión)
* [AEM Paquete de ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)

   * Versión 3.3.2 o posterior
   * `ACS AEM Commons - Dispatcher Cache Control Header - Max Age` Configuración de OSGi

### Configuración {#configuration}

La configuración de OSGi **AEM ACS Commons - Encabezado de control de caché de Dispatcher - Edad máxima** establece la caducidad de las páginas en caché que aparecen en una ruta de acceso especificada.

* Desde el [Consola web](../../help/sites-deploying/configuring-osgi.md).

   * Por ejemplo, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Localizar `ACS AEM Commons - Dispatcher Cache Control Header - Max Age`
* Seleccione el icono &quot;+&quot; para poder crear una configuración de conexión.

  ![dispatcher](assets/dispatcher.png)

* **Patrones de filtro**
  *(obligatorio)* Una o más rutas a páginas de la comunidad. Por ejemplo, `/content/sites/engage/(.*)`.

* **Edad máxima de control de caché**
  *(obligatorio)* Edad máxima (en segundos) que se agregará al encabezado Control de caché. El valor debe ser mayor que cero (0).

## Filtros de Dispatcher {#dispatcher-filters}

La sección /filter del `dispatcher.any` el archivo está documentado en [Configuración del acceso al contenido: /filter](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es).

En esta sección se describen las entradas que probablemente sean necesarias para el correcto funcionamiento de las funciones de Communities.

Los nombres de las propiedades de filtro siguen la convención de utilizar un número de cuatro dígitos para indicar el orden en que se aplican los patrones de filtro. Cuando se aplican varios patrones de filtro a una solicitud, el último que se aplica es efectivo. Por lo tanto, el primer patrón de filtro se utiliza a menudo para denegar todo, de modo que los siguientes patrones sirven para restaurar el acceso de forma controlada.

Los siguientes ejemplos utilizan nombres de propiedad que es probable que deban modificarse para adaptarse a cualquier `dispatcher.any` archivo.

Consulte también lo siguiente:

* [Lista de comprobación de seguridad de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=en)

>[!NOTE]
>
>**Ejemplos de nombres de propiedades**
>Se muestran todos los nombres de propiedades, como **/0050** y **/0170**, debe ajustarse para que se ajuste a un `dispatcher.any` archivo de configuración.
>

>[!CAUTION]
>
>Consulte la [Lista de comprobación de seguridad de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html) para obtener más información al restringir el acceso con Dispatcher. Además, lea la [Lista de comprobación de seguridad de AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es) para obtener más información sobre la seguridad relacionada con su instalación de AEM.
>

Las siguientes entradas deben agregarse al final de la sección /filter, especialmente después de todas las entradas denegadas.

<!-- New code wrt CQDOC-16081, changed by Vishabh on 10 Dec 2020.
-->

```shell
# design and template assets
/0050 { /type "allow" /url "/etc/designs/*" }

# collected JS/CSS from the components and design
/0051 { /type "allow" /url "/etc/clientlibs/*" }

# foundation search component - write stats
/0052 { /type "allow" /url "/bin/statistics/tracker/*" }

# allow users to edit profile page
/0054 { /type "allow" /url "* /home/users/*/*/profile.form.html*" }

# all profile data
/0057 { /type "allow" /url "/home/users/*/profile/*" }

# required for social "Sign In" link.
/0059 { /type "allow" /url "/etc/clientcontext/*" }

# required for "Sign Out" operation
/0063 { /type "allow" /url "* /system/sling/logout*" }

# enable Facebook and Twitter signin
/0064 { /type "allow" /url "/etc/cloudservices/*" }

# enable personalization
/0062 { /type "allow" /url "/libs/cq/personalization/*" }

# Enable CSRF token otherwise nothings works.
/5001 { /type "allow" /url "/libs/granite/csrf/token.json *"}
# Allow SCF User Model to bootstrap as it depends on the granite user
/5002 { /type "allow" /url "/libs/granite/security/currentuser.json*" }

# Allow Communities Site Logout button work
/5003 { /type "allow" /url "/system/sling/logout.html*" }

# Allow i18n to load correctly
/5004 { /type "allow" /url "/libs/cq/i18n/dict.en.json *" }

# Allow social json get pattern.
/6002 { /type "allow" /url "*.social.*.json*" }

# Allow loading of templates
/6003 { /type "allow" /url "/services/social/templates*" }

# Allow SCF User model to check moderator rules
/6005 { /type "allow" /url "/services/social/getLoggedInUser?moderatorCheck=*" }

# Allow CKEditor to load which uses a query pattern.
/6006 { /type "allow" /url "/etc/clientlibs/social/thirdparty/ckeditor/*.js?t=*" }
/6007 { /type "allow" /url "/etc/clientlibs/social/thirdparty/ckeditor/*.css?t=*" }

# Allow Fonts from Communities to load
/6050 { /type "allow" /url "*.woff" }
/6051 { /type "allow" /url "*.ttf" }

# Enable CQ Security checkpoint for component guide.
/7001 { /type "allow" /url "/libs/cq/security/userinfo.json?cq_ck=*"
```


<!-- existing content as of Dec 10, wrt CQDOC-16081

```shell
# design and template assets
/0050 { /type "allow" /glob "GET /etc/designs/*" }

# collected JS/CSS from the components and design
/0051 { /type "allow" /glob "GET /etc/clientlibs/*" }

# foundation search component - write stats
/0052 { /type "allow" /glob "GET /bin/statistics/tracker/*" }

# allow users to edit profile page
/0054 { /type "allow" /glob "* /home/users/*/*/profile.form.html*" }

# all profile data
/0057 { /type "allow" /glob "GET /home/users/*/profile/*" }

# required for social "Sign In" link.
/0059 { /type "allow" /glob "GET /etc/clientcontext/*" }

# required for "Sign Out" operation
/0063 { /type "allow" /glob "* /system/sling/logout*" }

# enable Facebook and Twitter signin
/0064 { /type "allow" /glob "GET /etc/cloudservices/*" }

# enable personalization
/0062 { /type "allow" /url "/libs/cq/personalization/*" }

# Enable CSRF token otherwise nothings works.
/5001 { /type "allow" /glob "GET /libs/granite/csrf/token.json *"}
# Allow SCF User Model to bootstrap as it depends on the granite user
/5002 { /type "allow" /glob "GET /libs/granite/security/currentuser.json*" }

# Allow Communities Site Logout button work
/5003 { /type "allow" /glob "GET /system/sling/logout.html*" }

# Allow i18n to load correctly
/5004 { /type "allow" /glob "GET /libs/cq/i18n/dict.en.json *" }

# Allow social json get pattern.
/6002 { /type "allow" /glob "GET *.social.*.json*" }

# Allow loading of templates
/6003 { /type "allow" /glob "GET /services/social/templates*" }

# Allow SCF User model to check moderator rules
/6005 { /type "allow" /glob "GET /services/social/getLoggedInUser?moderatorCheck=*" }

# Allow CKEditor to load which uses a query pattern not sufficed by regular glob above.
/6006 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.js?t=*" }
/6007 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.css?t=*" }

# Allow Fonts from Communities to load
/6050 { /type "allow" /glob "GET *.woff *" }
/6051 { /type "allow" /glob "GET *.ttf *" }

# Enable CQ Security checkpoint for component guide.
/7001 { /type "allow" /glob "GET /libs/cq/security/userinfo.json?cq_ck=*"

```
-->

## Reglas de Dispatcher {#dispatcher-rules}

La sección de reglas de `dispatcher.any` define qué respuestas deben almacenarse en caché en función de la dirección URL solicitada. Para las comunidades, se utiliza la sección de reglas para definir lo que no se debe almacenar nunca en caché.

<!-- New code wrt CQDOC-16081, changed by Vishabh on 10 Dec 2020.
-->

```shell
# Never cache the client-side .social.json calls
/0001 { /type "deny" /url "*.social.json*" }

# Never cache the user-specific .json requests
/0002 { /type "deny" /url "/libs/granite/csrf/token.json*" }
/0003 { /type "deny" /url "/libs/granite/security/currentuser.json*" }
/0004 { /type "deny" /url "/libs/granite/security/userinfo.json*" }

# Never cache the private community groups pages in case - add your own deny rules in there
/0005 { /type "deny" /url "/content/*/groups/*" }

# Never cache the assignments page in case the Enablement feature is in use - add your own deny rules in there
/0006 { /type "deny" /url "/content/*/assignments/*" }

# Never cache user generated content
/0208 { /type "deny" /url "/content/usergenerated/*" }
```

<!-- existing content as of Dec 10, wrt CQDOC-16081

```shell
# Never cache the client-side .social.json calls
/0001 { /type "deny" /glob "*.social.json*" }

# Never cache the user-specific .json requests
/0002 { /type "deny" /glob "/libs/granite/csrf/token.json*" }
/0003 { /type "deny" /glob "/libs/granite/security/currentuser.json*" }
/0004 { /type "deny" /glob "/libs/granite/security/userinfo.json*" }

# Never cache the private community groups pages in case - add your own deny rules in there
/0005 { /type "deny" /glob "/content/*/groups/*" }

# Never cache the assignments page in case the Enablement feature is in use - add your own deny rules in there
/0006 { /type "deny" /glob "/content/*/assignments/*" }

# Never cache user generated content
/0208 { /type "deny" /glob "/content/usergenerated/*" }
```
-->

## Solución de problemas {#troubleshooting}

Una causa importante de problemas es la inserción de reglas de filtro sin prestar atención al efecto en reglas anteriores, especialmente cuando se agrega una regla para denegar el acceso.

El primer patrón de filtro se utiliza a menudo para denegar todo, de modo que los siguientes filtros restauran el acceso de forma controlada. Cuando se aplican varios filtros a una solicitud, el último que se aplica es el que está en vigor.

## Dispatcher.any de muestra {#sample-dispatcher-any}

A continuación se muestra un ejemplo `dispatcher.any` que incluye los archivos Communities /filters y /rules.

<!-- New code wrt CQDOC-16081, changed by Vishabh on 10 Dec 2020.
-->

```shell
# Each farm configures a set of load balanced renders (i.e. remote servers)
/farms
  {
  # First farm entry
  /website
    {
    # Request headers that should be forwarded to the remote server.
    /clientheaders
      {
      # Forward all request headers that are end-to-end. If you want
      # to forward a specific set of headers, you'll have to list
      # them here.
      "*"
      }

    # Hostname matching for farm selection (virtual domain addressing)
    /virtualhosts
      {
      # Entries will be compared against the "Host" request header
      # and an optional request URL prefix.
      #
      # Examples:
      #
      #   www.company.com
      #   intranet.*
      #   myhost:8888/mysite
      "*"
      }

    # The load will be balanced among these render instances
    /renders
      {
      /rend01
        {
        # Hostname or IP of the render
        /hostname "127.0.0.1"
        # Port of the render
        /port "4503"
        # Connect timeout in milliseconds, 0 to wait indefinitely
        # /timeout "0"
        }
      }

    # The filter section defines the requests that should be handled by the dispatcher.
    #
    # Entries can be either specified using urls, or elements of the request line:
    #
    # (1) urls will be compared against the entire request line, for example,:
    #
    #     /0001 { /type "deny" /url "* /index.html *" }
    #
    #   matches request "GET /index.html HTTP/1.1" but not "GET /index.html?a=b HTTP/1.1".
    #
    # (2) method/url/query/protocol will be compared againts the respective elements of
    #   the request line, for example,:
    #
    #     /0001 { /type "deny" /method "GET" /url "/index.html" }
    #
    #   matches both "GET /index.html" and "GET /index.html?a=b HTTP/1.1".
    #
    # Note: specifying elements of the request line is the preferred method.
    /filter
      {
      # Deny everything first and then allow specific entries
      /0001 { /type "deny" /url "*" }

      # Open consoles
#     /0011 { /type "allow" /url "/admin/*"  }  # allow servlet engine admin
#     /0012 { /type "allow" /url "/crx/*"    }  # allow content repository
#     /0013 { /type "allow" /url "/system/*" }  # allow OSGi console

      # Allow non-public content directories
#     /0021 { /type "allow" /url "/apps/*"   }  # allow apps access
#     /0022 { /type "allow" /url "/bin/*"    }
      /0023 { /type "allow" /url "/content*" }  # disable this rule to allow mapped content only

#     /0024 { /type "allow" /url "/libs/*"   }
#     /0025 { /type "deny"  /url "/libs/shindig/proxy*" } # if you enable /libs close access to proxy

#     /0026 { /type "allow" /url "/home/*"   }
#     /0027 { /type "allow" /url "/tmp/*"    }
#     /0028 { /type "allow" /url "/var/*"    }

      # Enable specific mime types in non-public content directories
      /0041 { /type "allow" /url "*.css"   }  # enable css
      /0042 { /type "allow" /url "*.gif"   }  # enable gifs
      /0043 { /type "allow" /url "*.ico"   }  # enable icos
      /0044 { /type "allow" /url "*.js"    }  # enable javascript
      /0045 { /type "allow" /url "*.png"   }  # enable png
      /0046 { /type "allow" /url "*.swf"   }  # enable flash
      /0047 { /type "allow" /url "*.jpg"   }  # enable jpg
      /0048 { /type "allow" /url "*.jpeg"  }  # enable jpeg

      # Deny content grabbing
      /0081 { /type "deny"  /url "*.infinity.json" }
      /0082 { /type "deny"  /url "*.tidy.json"     }
      /0083 { /type "deny"  /url "*.sysview.xml"   }
      /0084 { /type "deny"  /url "*.docview.json"  }
      /0085 { /type "deny"  /url "*.docview.xml"  }

      /0086 { /type "deny"  /url "*.*[0-9].json" }
#     /0087 { /type "allow" /method "GET" /url "*.1.json" }  # allow one-level json requests

      # Deny query
   /0090 { /type "deny"  /url "*.query.json" }

      #######################################
      ## BEGIN: AEM COMMUNITITES ADDITIONS
   #######################################
   /0050 { /type "allow" /url "/etc/designs/*" }
   /0051 { /type "allow" /url "/etc/clientlibs/*" }
   /0052 { /type "allow" /url "/bin/statistics/tracker/*" }
   /0054 { /type "allow" /url "* /home/users/*/*/profile.form.html*" }
   /0057 { /type "allow" /url "/home/users/*/profile/*" }
   /0059 { /type "allow" /url "/etc/clientcontext/*" }
   /0063 { /type "allow" /url "* /system/sling/logout*" }
   /0064 { /type "allow" /url "/etc/cloudservices/*" }
   /0062 { /type "allow" /url "/libs/cq/personalization/*"  }  # enable personalization

         # Enable CSRF token otherwise nothings works.
   /5001 { /type "allow" /url "/libs/granite/csrf/token.json *"}

   # Allow SCF User Model to bootstrap as it depends on the granite user
   /5002 { /type "allow" /url "/libs/granite/security/currentuser.json*" }

      # Allow Communities Site Logout button work
      /5003 { /type "allow" /url "/system/sling/logout.html*" }

   # Allow i18n to load correctly
   /5004 { /type "allow" /url "/libs/cq/i18n/dict.en.json *" }

   # Allow social json get pattern.
   /6002 { /type "allow" /url "*.social.*.json*" }

   # Allow loading of templates
   /6003 { /type "allow" /url "/services/social/templates*" }

   # Allow SCF User model to check moderator rules
   /6005 { /type "allow" /url "/services/social/getLoggedInUser?moderatorCheck=*" }

   # Allow CKEditor to load which uses a query pattern.
   /6006 { /type "allow" /url "/etc/clientlibs/social/thirdparty/ckeditor/*.js?t=*" }
   /6007 { /type "allow" /url "/etc/clientlibs/social/thirdparty/ckeditor/*.css?t=*" }

   # Allow Fonts from Communities to load
   /6050 { /type "allow" /url "*.woff" }
   /6051 { /type "allow" /url "*.ttf" }

      # Enable CQ Security checkpoint for component guide.
   /7001 { /type "allow" /url "/libs/cq/security/userinfo.json?cq_ck=*"}

      #######################################
      ## END: AEM COMMUNITITES ADDITIONS
   #######################################

      }

    # The cache section regulates what responses will be cached and where.
    /cache
      {
      # The docroot must be equal to the document root of the webserver. The
      # dispatcher will store files relative to this directory and subsequent
      # requests may be "declined" by the dispatcher, allowing the webserver
      # to deliver them just like static files.
      /docroot "/opt/dispatcher"

      # Sets the level upto which files named ".stat" will be created in the
      # document root of the webserver. When an activation request for some
      # page is received, only files within the same subtree are affected
      # by the invalidation.
      #/statfileslevel "0"

      # Flag indicating whether to cache responses to requests that contain
      # authorization information.
      /allowAuthorized "1"

      # Flag indicating whether the dispatcher should serve stale content if
      # no remote server is available.
      #/serveStaleOnError "0"

      # The rules section defines what responses should be cached based on
      # the requested URL. Only the following requests can
      # lead to cacheable responses:
      #
      # - HTTP method is GET
      # - URL has an extension
      # - Request has no query string
      # - Request has no "Authorization" header (unless allowAuthorized is 1)
      /rules
        {
        /0000
          {
          # the matching pattern to be compared against the url
          # example: * -> everything
          #        : /foo/bar.* -> only the /foo/bar documents
          #        : /foo/bar/* -> all pages below /foo/bar
          #        : /foo/bar[./]* -> all pages below and /foo/bar itself
          #        : *.html        -> all .html files
          /url "*"
          /type "allow"
          }

      #######################################
      ## BEGIN: AEM COMMUNITITES ADDITIONS
     #######################################

   # Never cache the client-side .social.json calls
   /0001 { /type "deny" /url "*.social.json*" }

   # Never cache the user-specific .json requests
   /0002 { /type "deny" /url "/libs/granite/csrf/token.json*" }
   /0003 { /type "deny" /url "/libs/granite/security/currentuser.json*" }
   /0004 { /type "deny" /url "/libs/granite/security/userinfo.json*" }

   # Never cache the private community groups pages in case - add your own deny rules in there
   /0005 { /type "deny" /url "/content/*/groups/*" }

   # Never cache the assignments page in case the enablement feature is in use - add your own deny rules in there
   /0006 { /type "deny" /url "/content/*/assignments/*" }

      #######################################
      ## END: AEM COMMUNITITES ADDITIONS
      #######################################

        }

      # The invalidate section defines the pages that are "invalidated" after
      # any activation. The activated page itself and all
      # related documents are flushed on an modification. For example: if the
      # page /foo/bar is activated, all /foo/bar.* files are removed from the
      # cache.
      /invalidate
        {
        /0000
          {
          /url "*"
          /type "deny"
          }
        /0001
          {
          # Consider all HTML files stale after an activation.
          /url "*.html"
          /type "allow"
          }
        /0002
          {
          /url "/etc/segmentation.segment.js"
          /type "allow"
          }
        /0003
          {
          /url "*/analytics.sitecatalyst.js"
          /type "allow"
          }
        }

      # The allowedClients section restricts the client IP addresses that are
      # allowed to issue activation requests.
      /allowedClients
        {
        # Uncomment the following to restrict activation requests to originate
        # from "localhost" only.
        #
        #/0000
        #  {
        #  /url "*"
        #  /type "deny"
        #  }
        #/0001
        #  {
        #  /url "127.0.0.1"
        #  /type "allow"
        #  }
        }

      # The ignoreUrlParams section contains query string parameter names that
      # should be ignored when determining whether some request's output can be
      # cached or delivered from cache.
      #
      # In this example configuration, the "q" parameter will be ignored.
      #/ignoreUrlParams
      #  {
      #  /0001 { /url "*" /type "deny" }
      #  /0002 { /url "q" /type "allow" }
      #  }

    /enableTTL "1"

      }

    # The statistics sections dictates how the load should be balanced among the
    # renders according to the media-type.
    /statistics
      {
      /categories
        {
        /html
          {
          /url "*.html"
          }
        /others
          {
          /url "*"
          }
        }
      }
    }
  }
```

<!-- existing content as of Dec 10, wrt CQDOC-16081

```shell
# Each farm configures a set of load balanced renders (i.e. remote servers)
/farms
  {
  # First farm entry
  /website
    {
    # Request headers that should be forwarded to the remote server.
    /clientheaders
      {
      # Forward all request headers that are end-to-end. If you want
      # to forward a specific set of headers, you'll have to list
      # them here.
      "*"
      }

    # Hostname globbing for farm selection (virtual domain addressing)
    /virtualhosts
      {
      # Entries will be compared against the "Host" request header
      # and an optional request URL prefix.
      #
      # Examples:
      #
      #   www.company.com
      #   intranet.*
      #   myhost:8888/mysite
      "*"
      }

    # The load will be balanced among these render instances
    /renders
      {
      /rend01
        {
        # Hostname or IP of the render
        /hostname "127.0.0.1"
        # Port of the render
        /port "4503"
        # Connect timeout in milliseconds, 0 to wait indefinitely
        # /timeout "0"
        }
      }

    # The filter section defines the requests that should be handled by the dispatcher.
    #
    # Entries can be either specified using globs, or elements of the request line:
    #
    # (1) globs will be compared against the entire request line, for example,:
    #
    #     /0001 { /type "deny" /glob "* /index.html *" }
    #
    #   matches request "GET /index.html HTTP/1.1" but not "GET /index.html?a=b HTTP/1.1".
    #
    # (2) method/url/query/protocol will be compared againts the respective elements of
    #   the request line, for example,:
    #
    #     /0001 { /type "deny" /method "GET" /url "/index.html" }
    #
    #   matches both "GET /index.html" and "GET /index.html?a=b HTTP/1.1".
    #
    # Note: specifying elements of the request line is the preferred method.
    /filter
      {
      # Deny everything first and then allow specific entries
      /0001 { /type "deny" /glob "*" }

      # Open consoles
#     /0011 { /type "allow" /url "/admin/*"  }  # allow servlet engine admin
#     /0012 { /type "allow" /url "/crx/*"    }  # allow content repository
#     /0013 { /type "allow" /url "/system/*" }  # allow OSGi console

      # Allow non-public content directories
#     /0021 { /type "allow" /url "/apps/*"   }  # allow apps access
#     /0022 { /type "allow" /url "/bin/*"    }
      /0023 { /type "allow" /url "/content*" }  # disable this rule to allow mapped content only

#     /0024 { /type "allow" /url "/libs/*"   }
#     /0025 { /type "deny"  /url "/libs/shindig/proxy*" } # if you enable /libs close access to proxy

#     /0026 { /type "allow" /url "/home/*"   }
#     /0027 { /type "allow" /url "/tmp/*"    }
#     /0028 { /type "allow" /url "/var/*"    }

      # Enable specific mime types in non-public content directories
      /0041 { /type "allow" /url "*.css"   }  # enable css
      /0042 { /type "allow" /url "*.gif"   }  # enable gifs
      /0043 { /type "allow" /url "*.ico"   }  # enable icos
      /0044 { /type "allow" /url "*.js"    }  # enable javascript
      /0045 { /type "allow" /url "*.png"   }  # enable png
      /0046 { /type "allow" /url "*.swf"   }  # enable flash
      /0047 { /type "allow" /url "*.jpg"   }  # enable jpg
      /0048 { /type "allow" /url "*.jpeg"  }  # enable jpeg

      # Deny content grabbing
      /0081 { /type "deny"  /url "*.infinity.json" }
      /0082 { /type "deny"  /url "*.tidy.json"     }
      /0083 { /type "deny"  /url "*.sysview.xml"   }
      /0084 { /type "deny"  /url "*.docview.json"  }
      /0085 { /type "deny"  /url "*.docview.xml"  }

      /0086 { /type "deny"  /url "*.*[0-9].json" }
#     /0087 { /type "allow" /method "GET" /url "*.1.json" }  # allow one-level json requests

      # Deny query
   /0090 { /type "deny"  /url "*.query.json" }

      #######################################
      ## BEGIN: AEM COMMUNITITES ADDITIONS
   #######################################
   /0050 { /type "allow" /glob "GET /etc/designs/*" }
   /0051 { /type "allow" /glob "GET /etc/clientlibs/*" }
   /0052 { /type "allow" /glob "GET /bin/statistics/tracker/*" }
   /0054 { /type "allow" /glob "* /home/users/*/*/profile.form.html*" }
   /0057 { /type "allow" /glob "GET /home/users/*/profile/*" }
   /0059 { /type "allow" /glob "GET /etc/clientcontext/*" }
   /0063 { /type "allow" /glob "* /system/sling/logout*" }
   /0064 { /type "allow" /glob "GET /etc/cloudservices/*" }
   /0062 { /type "allow" /url "/libs/cq/personalization/*"  }  # enable personalization
   
      # Enable CSRF token otherwise nothings works.
   /5001 { /type "allow" /glob "GET /libs/granite/csrf/token.json *"}

   # Allow SCF User Model to bootstrap as it depends on the granite user
   /5002 { /type "allow" /glob "GET /libs/granite/security/currentuser.json*" }

      # Allow Communities Site Logout button work
      /5003 { /type "allow" /glob "GET /system/sling/logout.html*" }

   # Allow i18n to load correctly
   /5004 { /type "allow" /glob "GET /libs/cq/i18n/dict.en.json *" }

   # Allow social json get pattern.
   /6002 { /type "allow" /glob "GET *.social.*.json*" }

   # Allow loading of templates
   /6003 { /type "allow" /glob "GET /services/social/templates*" }

   # Allow SCF User model to check moderator rules
   /6005 { /type "allow" /glob "GET /services/social/getLoggedInUser?moderatorCheck=*" }

   # Allow CKEditor to load which uses a query pattern not sufficed by regular glob above.
   /6006 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.js?t=*" }
   /6007 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.css?t=*" }

   # Allow Fonts from Communities to load
   /6050 { /type "allow" /glob "GET *.woff *" }
   /6051 { /type "allow" /glob "GET *.ttf *" }

      # Enable CQ Security checkpoint for component guide.
   /7001 { /type "allow" /glob "GET /libs/cq/security/userinfo.json?cq_ck=*"}

      #######################################
      ## END: AEM COMMUNITITES ADDITIONS
   #######################################

      }

    # The cache section regulates what responses will be cached and where.
    /cache
      {
      # The docroot must be equal to the document root of the webserver. The
      # dispatcher will store files relative to this directory and subsequent
      # requests may be "declined" by the dispatcher, allowing the webserver
      # to deliver them just like static files.
      /docroot "/opt/dispatcher"

      # Sets the level upto which files named ".stat" will be created in the
      # document root of the webserver. When an activation request for some
      # page is received, only files within the same subtree are affected
      # by the invalidation.
      #/statfileslevel "0"

      # Flag indicating whether to cache responses to requests that contain
      # authorization information.
      /allowAuthorized "1"

      # Flag indicating whether the dispatcher should serve stale content if
      # no remote server is available.
      #/serveStaleOnError "0"

      # The rules section defines what responses should be cached based on
      # the requested URL. Only the following requests can
      # lead to cacheable responses:
      #
      # - HTTP method is GET
      # - URL has an extension
      # - Request has no query string
      # - Request has no "Authorization" header (unless allowAuthorized is 1)
      /rules
        {
        /0000
          {
          # the globbing pattern to be compared against the url
          # example: * -> everything
          #        : /foo/bar.* -> only the /foo/bar documents
          #        : /foo/bar/* -> all pages below /foo/bar
          #        : /foo/bar[./]* -> all pages below and /foo/bar itself
          #        : *.html        -> all .html files
          /glob "*"
          /type "allow"
          }

      #######################################
      ## BEGIN: AEM COMMUNITITES ADDITIONS
     #######################################

   # Never cache the client-side .social.json calls
   /0001 { /type "deny" /glob "*.social.json*" }

   # Never cache the user-specific .json requests
   /0002 { /type "deny" /glob "/libs/granite/csrf/token.json*" }
   /0003 { /type "deny" /glob "/libs/granite/security/currentuser.json*" }
   /0004 { /type "deny" /glob "/libs/granite/security/userinfo.json*" }

   # Never cache the private community groups pages in case - add your own deny rules in there
   /0005 { /type "deny" /glob "/content/*/groups/*" }

   # Never cache the assignments page in case the enablement feature is in use - add your own deny rules in there
   /0006 { /type "deny" /glob "/content/*/assignments/*" }

      #######################################
      ## END: AEM COMMUNITITES ADDITIONS
      #######################################

        }

      # The invalidate section defines the pages that are "invalidated" after
      # any activation. The activated page itself and all
      # related documents are flushed on an modification. For example: if the
      # page /foo/bar is activated, all /foo/bar.* files are removed from the
      # cache.
      /invalidate
        {
        /0000
          {
          /glob "*"
          /type "deny"
          }
        /0001
          {
          # Consider all HTML files stale after an activation.
          /glob "*.html"
          /type "allow"
          }
        /0002
          {
          /glob "/etc/segmentation.segment.js"
          /type "allow"
          }
        /0003
          {
          /glob "*/analytics.sitecatalyst.js"
          /type "allow"
          }
        }

      # The allowedClients section restricts the client IP addresses that are
      # allowed to issue activation requests.
      /allowedClients
        {
        # Uncomment the following to restrict activation requests to originate
        # from "localhost" only.
        #
        #/0000
        #  {
        #  /glob "*"
        #  /type "deny"
        #  }
        #/0001
        #  {
        #  /glob "127.0.0.1"
        #  /type "allow"
        #  }
        }

      # The ignoreUrlParams section contains query string parameter names that
      # should be ignored when determining whether some request's output can be
      # cached or delivered from cache.
      #
      # In this example configuration, the "q" parameter will be ignored.
      #/ignoreUrlParams
      #  {
      #  /0001 { /glob "*" /type "deny" }
      #  /0002 { /glob "q" /type "allow" }
      #  }

    /enableTTL "1"

      }

    # The statistics sections dictates how the load should be balanced among the
    # renders according to the media-type.
    /statistics
      {
      /categories
        {
        /html
          {
          /glob "*.html"
          }
        /others
          {
          /glob "*"
          }
        }
      }
    }
  }

```

-->
