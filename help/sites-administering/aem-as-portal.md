---
title: Portales y portlets de AEM
seo-title: Portales y portlets de AEM
description: Obtenga información sobre portales y portales en AEM.
seo-description: Obtenga información sobre portales y portales en AEM.
uuid: 7f9e316d-277e-4a1e-b6f3-cd89addc897b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 99528fda-5c8c-4034-bcbe-a4cea42f694b
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# Portales y portlets de AEM{#aem-portals-and-portlets}

En este documento se describe lo siguiente:

* Arquitectura de AEM Portal
* Administración y configuración de AEM como portal
* Uso de AEM como portal
* Instalación, configuración y visualización de contenido de AEM en un portlet (por ejemplo, un servidor web)

## Arquitectura de AEM Portal {#aem-portal-architecture}

La arquitectura del portal de AEM incluye definiciones de portales y portlets.

### ¿Qué es un portal? {#what-is-a-portal}

Un portal es una aplicación web que proporciona personalización, inicio de sesión único, integración de contenido de diferentes fuentes y aloja la capa de presentación de los sistemas de información.

Puede ejecutar portlets compatibles con JSR 286 en AEM. El componente portlet permite incrustar un portlet en la página. Consulte [Administración del portlet](#administeringthecqcontentportlet)de contenido de AEM.

### ¿Qué es un portlet? {#what-is-a-portlet}

Los portlets son componentes Web implementados dentro de un contenedor que genera contenido dinámico. La interfaz portlet se empaqueta e implementa como un archivo .war dentro de un contenedor portlet. Si está ejecutando AEM como portal, necesita el archivo .war del portlet para ejecutar el portlet.

Para configurar que el contenido de AEM aparezca en un portal, consulte [Instalación, configuración y uso de AEM en un portlet](#installingconfiguringandusingcqinaportlet).

### Director de AEM Portal {#aem-portal-director}

>[!CAUTION]
>
>AEM Portal Director ya no se utiliza en AEM 6.4.Consulte Funciones [obsoletas y eliminadas](https://helpx.adobe.com/experience-manager/6-4/release-notes/deprecated-removed-features.html).

## Administración del portlet de contenido de AEM {#administering-the-aem-content-portlet}

El portlet de contenido de AEM le permite mostrar contenido de AEM en un portal. El portlet está disponible en `/crx-quickstart/opt/portal`y se puede personalizar de diversas maneras. Por ejemplo, puede personalizar el control SSO/Authentication implementando su propio servicio de autenticación para generar la información de autenticación necesaria para que AEM sobrescriba el comportamiento predeterminado. Los complementos utilizan una API definida que le permite agregar su propia funcionalidad creando el complemento con la API. El complemento se puede implementar en el portlet en ejecución. Para funcionar correctamente, necesita una configuración de la instancia de publicación y creación de AEM junto con la ruta de contenido para mostrarla al iniciar.

Algunas de las configuraciones se pueden cambiar a través de las preferencias de portlet y otras a través de las configuraciones de servicio OSGi. Estas configuraciones se cambian mediante archivos de **configuración** o la consola web OSGi.

### Preferencias del portlet {#portlet-preferences}

Las preferencias del portlet se pueden configurar en el momento de la implementación en el servidor del portal o editando el archivo **WEB-INF/portlet.xml** antes de implementar la aplicación web del portlet. El archivo portlet.xml aparece de forma predeterminada de la siguiente manera:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<portlet-app xmlns="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd /opt/SUNWps/dtd/portlet.xsd"
             version="1.0">
   <portlet>
      <portlet-name>RSSWeatherPortlet</portlet-name>
      <portlet-class>org.jboss.portlet.weather.WeatherPortlet</portlet-class>
      <init-param>
         <name>default_zipcode</name>
         <value>05673</value>
      </init-param>
      <init-param>
         <name>RSS_XSL</name>
         <value>/WEB-INF/Rss.xsl</value>
      </init-param>
      <init-param>
         <name>base_url</name>
         <value>https://xml.weather.yahoo.com/forecastrss?p=</value>
      </init-param>
      <expiration-cache>180</expiration-cache>
      <supports>
         <mime-type>text/html</mime-type>
         <portlet-mode>VIEW</portlet-mode>
         <portlet-mode>EDIT</portlet-mode>
      </supports>
      <portlet-info>
         <title>Weather Portlet</title>
      </portlet-info>
      <portlet-preferences>
         <preference>
            <name>expires</name>
            <value>180</value>
         </preference>
         <preference>
            <name>RssXml</name>
            <value>https://xml.weather.yahoo.com/forecastrss?p=33145</value>
            <read-only>false</read-only>
         </preference>
      </portlet-preferences>
   </portlet>
</portlet-app>
```

El portlet se puede configurar con las siguientes preferencias:

<table>
 <tbody>
  <tr>
   <td>startPath</td>
   <td><p>Ésta es la ruta de inicio del portlet: define el contenido que se muestra inicialmente.</p> <p><strong>Importante</strong>: Si el portlet está configurado para conectarse al autor de AEM y publicar instancias que se ejecutan en una ruta de contexto distinta<strong> a /</strong>, debe activar la fuerza de <strong>CQUrlInfo</strong> en la configuración del Administrador de bibliotecas Html de estas instancias de AEM (por ejemplo, mediante Felix Webconsole) o la edición no funcionará y no aparecerá el cuadro de diálogo de preferencias.</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>Selector que se anexa a cada dirección URL. De forma predeterminada, se trata de un <strong>portlet</strong>, por lo que todas las solicitudes de páginas html utilizan direcciones URL que finalizan en <strong>.portlet.html.</strong> Esto permite el uso de scripts personalizados en AEM para el procesamiento de portlets.</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>De forma predeterminada, los archivos css incluidos en la página HTML de AEM se incluyen en el portlet. Al desactivar esta opción, se excluyen los archivos css predeterminados.</p> <p>Si esta opción está habilitada, los archivos CSS se agregan al encabezado de la página html o se incrustan en la página html, según el comportamiento del portal.</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>De forma predeterminada, se procesa una barra de herramientas dentro del portlet de contenido para la funcionalidad de administración. Al desactivar esta opción, no se procesa ninguna barra de herramientas.</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>Lista de nombres de parámetros de URL alternativos que pueden contener la nueva dirección URL de contenido para mostrar en el portlet. La lista se procesa de arriba abajo, se utiliza el primer parámetro que contiene un valor. Si no se encuentra ninguna URL, se utiliza el parámetro de URL predeterminado. La dirección URL proporcionada se utiliza, tal como está, sin ninguna modificación adicional.</p> <p>Esta configuración es por portlet implementado; también es para configurar globalmente algunos parámetros de URL en la configuración OSGi para el "Puente de portlet de Day Portal Director".</p> </td>
  </tr>
  <tr>
   <td>priorityDialog</td>
   <td>Ruta al cuadro de diálogo de preferencias en AEM: si se deja vacío, se utilizará el cuadro de diálogo de preferencias integrado. El valor predeterminado es /libs/portal/content/prefs.html.</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>De forma predeterminada, el portlet realiza una redirección de javascript de toda la página del portal en la primera invocación. Esto es para admitir el escenario de arrastrar y soltar de los servidores de portal modernos. En la producción, esta redirección raramente es necesaria y, por lo tanto, puede desactivarse si esta preferencia se establece en <em>false</em>.</td>
  </tr>
 </tbody>
</table>

#### OSGi Web Console {#osgi-web-console}

Si damos por supuesto que el servidor de portal se ejecuta en el host localhost, el puerto 8080 y la aplicación web del portlet AEM se monta en el *cqportlet* de contexto de la aplicación web, la dirección URL para la consola web es `https://localhost:8080/cqportlet/cqbridge/system/console`. El usuario y la contraseña predeterminados son **admin**.

Abra la ficha **Configuraciones** y seleccione Configuración **de CQ Server de** Portal Directory. Aquí puede especificar la URL base del autor y la instancia de publicación. Este procedimiento se describe en [Configuración del portlet](#configuring-the-portlet).

>[!NOTE]
>
>La consola web OSGi solo está pensada para cambiar las configuraciones durante el desarrollo (o la prueba). Asegúrese de bloquear las solicitudes a la consola para los sistemas de producción.

### Proporcionar configuraciones {#providing-configurations}

Para admitir las implementaciones automatizadas y el aprovisionamiento de configuración, el portlet de contenido de AEM cuenta con compatibilidad de configuración integrada que intenta leer las configuraciones de la ruta de clases proporcionada a la aplicación portlet.

Al iniciar, se lee la propiedad del sistema **com.day.cq.portet.config** para detectar el entorno actual. Normalmente, el valor de esta propiedad es algo como **dev**, **prod**, **test** , etc. Si no se establece ningún entorno, no se lee ninguna configuración.

Si se configura un entorno, se busca un archivo de configuración en la ruta de clases en* ***com/day/cq/portlet/{env}.config** , donde **env** se reemplaza por el valor real del entorno. Este archivo debe enumerar todos los archivos de configuración de este entorno. Estos archivos se buscan en relación con la ubicación del archivo de configuración. Por ejemplo, si el archivo contiene una línea, `my.service.xml,` este archivo se lee de la ruta de clases en `com/day/cq/portlet/my.service.config.` El nombre del archivo consiste en la ID de persistencia del servicio, seguida de **.config**. En el ejemplo anterior, el ID de persistencia es **my.service**. El formato del archivo de configuración es el formato utilizado por el instalador OSGi de Apache Sling.

Esto significa que, para cada entorno, se debe agregar un archivo de configuración correspondiente. Una configuración que debe aplicarse a todos los entornos debe introducirse en todos estos archivos; si es sólo para un entorno único, se introduce en ese archivo. Este mecanismo garantiza el control total sobre la configuración que se lee en cada entorno.

Es posible utilizar una propiedad de sistema diferente para detectar el entorno. Especifique la propiedad del sistema **com.day.cq.portet.configproperty** que contiene el nombre de la propiedad del sistema que se va a utilizar en lugar de **com.day.cq.portet.config**.

#### Almacenamiento en caché e invalidación del almacenamiento en caché {#caching-and-caching-invalidation}

El portlet, en su configuración predeterminada, almacena en caché las respuestas que recibe de AEM WCM en una caché específica del usuario. Las memorias caché deben invalidarse cuando se produzcan cambios en el contenido de la instancia de publicación. Con este fin, en AEM WCM debe configurarse un agente de replicación en la instancia de creación. La caché también se puede vaciar manualmente. En esta sección se describen ambos procedimientos.

El portlet se puede configurar con su propia caché, de modo que el contenido del portlet se muestre sin necesidad de acceder a AEM. El portal está disponible como contenido en /libs/portal/director. Para acceder al contenido, inicie una instancia de AEM y descargue el archivo desde esa ubicación mediante CRXDE Lite o Webdav.

Puede implementar este paquete en tiempo de ejecución o agregarlo a la aplicación web portlet antes `WEB-INF/lib/resources/bundles` de la implementación.

Una vez implementada la caché, el portlet almacena en caché el contenido de la instancia de publicación. La caché del portlet se puede invalidar con una descarga de despachante de AEM. Para configurar el portlet para que utilice su propia caché:

1. Configure un agente de replicación en el autor que se dirija al servidor de portal.
1. Si damos por supuesto que el servidor de portal se ejecuta en host **localhost**, **puerto 8080 **y la aplicación web de portlet AEM se monta en el **portlet** de contexto, la dirección URL para vaciar la caché es `https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)`. Utilice GET como método.
   **** Nota: En lugar de utilizar un parámetro de solicitud, puede enviar un encabezado http denominado **Ruta**.

#### Vaciar la memoria caché mediante el agente de replicación {#flushing-the-cache-via-replication-agent}

Al igual que la invalidación normal del despachante, se puede configurar un agente de replicación para que se dirija a la caché del portlet AEM del portal. Después de configurar el agente de replicación, cada activación de página normal descarga la caché del portal.

Si opera varios nodos de portal que ejecutan el portlet AEM, debe crear un agente para cada nodo como se describe en este procedimiento.

Para configurar un agente de replicación para el portal:

1. Inicie sesión en la instancia de creación.
1. En la ficha Sitios web, haga clic en la ficha *Herramientas* .
1. **** Haga clic en **Nueva página... en los agentes de replicación** Nuevo... del menú.

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. En *Plantilla*, seleccione Agente *de replicación* e introduzca un nombre para el agente. Haga clic en *Crear*.

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. Haga doble clic en el agente de replicación que acaba de crear. Se muestra como no válido porque aún no se ha configurado.

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. Haga clic en **Editar.**
1. En la ficha **Configuración** , active la casilla de verificación **Habilitado** , seleccione **Despacho** de despachante como tipo de serialización e introduzca un tiempo de espera de reintento (por ejemplo, 60000).

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. Click the **Transport** tab.
1. En el campo **URI** , introduzca el URI de vaciado (URL) del portlet. El URI tiene el siguiente formato:

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322pm](assets/screen_shot_2012-02-15at42322pm.png)

1. Click the **Extended** tab.

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. En el campo Método **** HTTP, escriba **GET**.
1. En el campo Encabezados **** HTTP, haga clic en **+** para agregar una nueva entrada y escriba **Ruta: {path}**.
1. Si es necesario, haga clic en la ficha **Proxy** e introduzca la información de proxy en el agente.
1. Click **OK** to save changes.
1. Para probar la conexión, haga clic en el vínculo **Probar conexión** . Aparece un mensaje de registro que indica si la prueba de replicación se realizó correctamente. Por ejemplo:

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### Descarga manual de la caché de portlet {#manually-flushing-the-portlet-cache}

Puede vaciar manualmente la caché del portlet accediendo a la misma dirección URL configurada para el agente de replicación. Consulte [Vacío de la caché](#flushing-the-cache-via-replication-agent) para ver la forma de la dirección URL. Además, la dirección URL debe ampliarse con un parámetro de URL Path=&lt;ruta> para indicar qué vaciar.

Por ejemplo:

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` borra la caché completa. `https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz` se borra `/content/mypage/xyz` de la caché.

### Seguridad del portal {#portal-security}

El portal es el mecanismo de autenticación que conduce. Puede iniciar sesión en AEM con un usuario técnico, un usuario del portal, un grupo, etc. El portlet no tiene acceso a la contraseña para el usuario en el portal, por lo que si el portlet no conoce todas las credenciales para iniciar sesión correctamente en un usuario, se debe utilizar una solución SSO. En este caso, el portlet de AEM reenvía toda la información necesaria a AEM, que a su vez reenvía esta información al repositorio de AEM subyacente. Este comportamiento es conectable y se puede personalizar.

### Autenticación al publicar {#authentication-on-publish}

En esta sección se describen los modos de autenticación disponibles que el portlet puede utilizar para comunicarse con las instancias WCM subyacentes de AEM.

De forma predeterminada, no se envía información de usuario a la instancia de publicación de AEM; el contenido siempre se muestra como usuario anónimo. Si la información específica del usuario se debe enviar desde AEM o si se requiere la autenticación del usuario para la publicación, esto debe activarse.

#### Acceso a la configuración de autenticación del portlet {#accessing-the-portlet-s-authentication-configuration}

Las opciones de configuración de autenticación que utiliza el portlet en las instancias de AEM WCM están disponibles en la consola web (configuración OSGi).

>[!NOTE]
>
>Al trabajar con AEM, existen varios métodos para administrar la configuración de los servicios OSGi (nodos de consola o repositorio).
>
>Consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información.

Para acceder a la configuración de autenticación del portlet:

1. Acceda a la consola web en la siguiente dirección URL:

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   Por ejemplo, en su configuración predeterminada:

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. Inicie sesión en la consola web. Las credenciales predeterminadas son `admin/admin`.
1. En la consola, seleccione **Configuración**.
1. En el menú **Configuración** , seleccione un servicio concreto para configurar. Los servicios son proporcionados por el portlet en el marco de OSGi.

   | Nombre de servicio | Descripción |
   |---|---|
   | Autenticador del director de Day Portal | Configure qué modo de autenticación se utiliza para las instancias de AEM WCM. Según el modo seleccionado, se puede especificar un usuario técnico o el nombre de la cookie SSO. Además, la autenticación para las instancias de publicación de AEM WCM puede habilitarse. |
   | Caché de archivos del director del portal de día | Configure los parámetros de cómo el portlet almacena en caché las respuestas que recibe de las instancias de AEM WCM. |
   | Servicio de cliente HTTP de Day Portal | Configure la forma en que el portlet se conecta mediante HTTP a las instancias de AEM WCM subyacentes. Por ejemplo, puede especificar un servidor proxy. |
   | Controlador de configuración regional de Day Portal | Configure qué configuraciones regionales admite el portlet. Las solicitudes a instancias de AEM WCM se basan en la configuración regional del usuario; por ejemplo, el idioma del usuario *alemán *solicitaría `/content/geometrixx/de/`... . |
   | Administrador de privilegios del director de Day Portal | Configure si el portlet debe probar la ficha Sitios web en función del usuario que ha iniciado sesión. |
   | Procesador de la barra de herramientas de Day Portal | Personalice la representación de la barra de herramientas del portlet. |

1. Además, puede configurar la consola web y el servicio de registro. Por ejemplo, puede cambiar las credenciales de administración de la consola Web haciendo clic en el vínculo de la Consola de administración Apache Felix OSGi.

#### Modo de usuario técnico {#technical-user-mode}

En el modo predeterminado, todas las solicitudes emitidas por el portlet para la instancia de creación de AEM WCM se autentican con el mismo usuario técnico, independientemente del usuario del portal actual. El modo de usuario técnico está activado de forma predeterminada. Active o desactive este modo en la pantalla de configuración correspondiente de la consola de administración OSGi:

El usuario técnico especificado debe existir en la instancia de creación de AEM WCM y en la instancia de publicación si **Autenticar en publicación **está activado. Asegúrese de otorgar al usuario privilegios de acceso suficientes para el trabajo de creación.

#### SSO {#sso}

El portlet admite SSO con AEM fuera de serie. El servicio de autentificador puede configurarse para utilizar SSO y transmitir el usuario del portal actual con el formato **Básico** como una cookie denominada `cqpsso` a AEM. AEM debe configurarse para utilizar el controlador de autenticación SSO para la ruta /. El nombre de la cookie también debe configurarse aquí.

El repositorio `crx-quickstart/repository/repository.xml` de AEM debe configurarse en consecuencia:

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### Modo de autenticación SSO {#sso-authentication-mode}

El portlet puede autenticarse para AEM WCM mediante el esquema de inicio de sesión único (SSO). En este modo, el usuario que ha iniciado sesión en el portal se reenvía a AEM WCM en forma de cookie SSO. Si se utiliza el modo SSO, todas las instancias de AEM WCM subyacentes deben conocer a todos los usuarios del portal con acceso al portlet AEM, principalmente en forma de que AEM WCM esté conectado a LDAP o de que los usuarios se hayan creado manualmente de antemano. Además, antes de activar SSO en el portlet, es necesario configurar la instancia de autor de AEM WCM subyacente (y la instancia de publicación, si la opción **Autenticar en la publicación** está activada) para aceptar solicitudes basadas en SSO.

Para configurar el portlet para que utilice el modo de autenticación SSO, complete los siguientes pasos (descritos en detalle en las siguientes secciones):

* Active el repositorio de AEM WCM para aceptar credenciales de confianza.
* Habilite la autenticación SSO en AEM WCM.
* Habilite la autenticación SSO en el portlet AEM.

#### Activación del repositorio de AEM WCM para aceptar credenciales de confianza {#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

Antes de habilitar SSO para AEM WCM, es necesario configurar el repositorio subyacente para que acepte las credenciales de confianza proporcionadas por AEM WCM. Para ello, configure el archivo repositorio.xml de AEM.

1. En el sistema de archivos en el que AEM WCM está instalado, abra el siguiente archivo:

   `//crx-quickstart/repository/repository.xml`

1. En el archivo XML, busque la entrada para **LoginModule** y agregue el atributo trust_dentials_attribute a su configuración:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
     <param name="anonymous_principal" value="anonymous"/>
   </LoginModule>
   ```

1. Reinicie AEM WCM para que los cambios surtan efecto.

#### Activación de la autenticación SSO en AEM WCM {#enabling-sso-authentication-in-the-aem-wcm}

Para activar SSO en AEM WCM, acceda a la entrada de configuración correspondiente en la consola de gestión web Apache Felix Web Management Console (OSGi) de AEM WCM:

1. Acceda a la consola a través de su URI en https://&lt;AEM-host>:&lt;puerto>/sistema/consola.
1. En el menú Configuración, seleccione Controlador de autenticación SSO. En este ejemplo, el controlador de SSO acepta solicitudes de SSO para todas las rutas basadas en la cookie proporcionada por el portlet de AEM. Su configuración puede variar.

   | Ruta | / | Habilita el controlador SSO para todas las solicitudes |
   |---|---|---|
   | Nombres de cookies | cqpsso | Nombre de la cookie proporcionada por el portlet según la configuración de la consola OSGi del portlet. |

1. Haga clic en **Guardar** para habilitar SSO. SSO es ahora el esquema de autenticación principal.

Para cada solicitud que recibe AEM WCM, primero se intenta la autenticación basada en SSO. Tras un error, se realiza una alternativa al esquema de autenticación básico habitual. Como tal, las conexiones normales a AEM WCM sin SSO siguen siendo posibles.

#### Activación de la autenticación SSO en un portlet AEM {#enabling-sso-authentication-in-a-aem-portlet}

Para que la instancia de AEM WCM subyacente acepte solicitudes de SSO, el modo de autenticación del portlet debe cambiarse de **técnico** a **SSO**.

Para habilitar la autenticación SSO en un portlet AEM:

1. Acceda a la consola a través de su URI en https://&lt;aem-host>:&lt;puerto>/system/console.
1. En el menú Configuración, seleccione Autenticador de Director de portal de día en la lista de configuraciones disponibles.
1. En Modo, seleccione SSO. Deje los demás parámetros con sus valores predeterminados.

   ![chlimage_1-135](assets/chlimage_1-135.png)

1. Haga clic en Guardar para habilitar SSO para el portlet.

   Para realizar pruebas, acceda al portlet con el usuario administrativo del portal, después de crear el mismo usuario en AEM WCM con privilegios de administrador.

Después de realizar este procedimiento, las solicitudes se autentican con SSO. Un fragmento típico de la comunicación HTTP revela la presencia de los siguientes encabezados específicos de SSO y Portlet:

```xml
C-12-#001898 -> [GET /mynet/en/_jcr_content/par/textimage/image.img.png HTTP/1.1 ]
C-12-#001963 -> [cq5:locale: en ]
C-12-#001979 -> [cq5:used-locale: en ]
C-12-#002000 -> [cq5:locales: en,en_US ]
C-12-#002023 -> [cqp:user: wpadmin ]
C-12-#002042 -> [cqp:portal: IBM WebSphere Portal/6.1 ]
C-12-#002080 -> [cqp:windowid: 7_CGAH47L000CE302V2KFNOG0084 ]
C-12-#002124 -> [cqp:windowstate: normal ]
C-12-#002149 -> [cqp:portletmode: view ]
C-12-#002172 -> [User-Agent: Jakarta Commons-HttpClient/3.1 ]
C-12-#002216 -> [Host: 10.0.0.68:4502 ]
C-12-#002238 -> [Cookie: $Version=0; cqpsso=Basic+d3BhZG1pbg%3D%3D ]
C-12-#002289 -> [ ]
```

### Habilitación de la autenticación PIN {#enabling-pin-authentication}

Si no utiliza las funciones de edición en línea predeterminadas del portlet de contenido AEM, pero desea que la creación y la administración formen parte del portlet fuera del portal directamente en la instancia de creación de AEM, debe activar la autenticación PIN. También debe cambiar la configuración de los botones de administración.

Para abrir la página de administración de sitios web o editar una página desde el portlet, el portlet de contenido de AEM utiliza la nueva autenticación de pines. De forma predeterminada, la autenticación de pin está deshabilitada, por lo que en AEM deben realizarse los siguientes cambios de configuración:

1. Habilite la autenticación de confianza en AEM agregando la información de confianza en el archivo repositorio.xml:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. En la consola de configuración OSGi, ubicada de forma predeterminada en https://localhost:4502/system/console/configMgr, seleccione Controlador **de autenticación de PIN de** CQ en el menú desplegable.
1. Edite el parámetro de ruta **raíz de** URL para que solo contenga el valor **o**&#x200B;único.

### Privilegios {#privileges}

Algunas funciones del portlet están protegidas por privilegios. El usuario actual necesita tener este privilegio para poder acceder a esta función. Hay los siguientes privilegios predefinidos:

* &quot;toolbar&quot; : Este es el privilegio general de ver/usar la barra de herramientas en el portlet.
* &quot;prefs&quot; : Si el usuario tiene este privilegio, puede ver o cambiar las preferencias del portlet.
* &quot;cq-author:edit&quot; : Con este privilegio, el usuario puede invocar la vista de edición del contenido.
* &quot;cq-author:preview&quot; : Con este privilegio, el usuario puede ver la vista previa.
* &quot;cq-author:siteadmin&quot; : Con esta privacidad, el usuario puede abrir el siteadmin en AEM.

El mejor método para administrar los privilegios es utilizar las funciones de portal y asignar funciones a estos privilegios. Esto se puede realizar mediante una configuración OSGi. El &quot;Administrador de privilegios del director de Day Portal&quot; se puede configurar con un conjunto de funciones para cada privilegio. Si el usuario tiene una de las funciones, tiene el privilegio correspondiente.

Además, es posible definir este rol en base al acceso en una base de instancias de portlet por portlet. El cuadro de diálogo de preferencias del portlet contiene un campo de entrada para cada uno de los privilegios anteriores. Para cada privilegio se puede configurar una lista separada por comas de las funciones de portlet. Si se configura un valor, se anula la configuración global del servicio &quot;Administrador de privilegios de director de Day Portal&quot; y es posible que sea necesario agregar las mismas funciones de esta configuración global, ya que las funciones no se combinan. Si no se especifica ningún valor, se utiliza la configuración global.

### Personalización de la aplicación de portlet AEM {#customizing-the-aem-portlet-application}

La aplicación portlet AEM proporcionada inicia un contenedor OSGi dentro de la aplicación web del mismo modo que AEM. Esta arquitectura le permite aprovechar todas las ventajas de OSGi:

* Fácil de actualizar y ampliar
* Proporciona actualizaciones urgentes del portlet sin ninguna interacción del servidor del portal
* Fácil de personalizar el portlet

### Botones de la barra de herramientas {#toolbar-buttons}

La barra de herramientas y sus botones se pueden configurar y personalizar. Puede agregar sus propios botones a la barra de herramientas o definir qué botones se muestran en cada modo. Cada botón es un servicio OSGi configurable mediante una configuración OSGi.

La consola web OSGi enumera todas las configuraciones de botones de la ficha **Configuración** . Para cada botón, puede definir en qué modo se muestra este botón. Esto le permite desactivar un botón eliminando todos los modos, por ejemplo.

De forma predeterminada, el portlet de contenido de AEM utiliza la funcionalidad de edición en línea. Sin embargo, si prefiere cambiar a la instancia de autor de AEM para editarla, habilite el botón **** SiteAdmin y el botón **** ContentFinder, pero desactive el botón **** Editar. En este caso, asegúrese de configurar correctamente la autenticación PIN en AEM.

El diseño de la barra de herramientas del portlet se puede personalizar instalando un paquete a través de la consola web Felix del portlet, que contiene CSS/HTML personalizado en una ubicación predefinida.

#### Estructura del paquete {#bundle-structure}

A continuación se muestra un ejemplo de estructura de paquetes:

```xml
$ jar tvf target/toolbarlayout-0.0.1-SNAPSHOT.jar | awk '{print $8}'
META-INF/
META-INF/MANIFEST.MF
/com/day/cq/portlet/toolbar/layout/
/com/day/cq/portlet/toolbar/layout/author.gif
/com/day/cq/portlet/toolbar/layout/back.gif
/com/day/cq/portlet/toolbar/layout/button.html
/com/day/cq/portlet/toolbar/layout/edit.gif
/com/day/cq/portlet/toolbar/layout/manage.html
/com/day/cq/portlet/toolbar/layout/publish.html
/com/day/cq/portlet/toolbar/layout/refresh.gif
/com/day/cq/portlet/toolbar/layout/siteadmin.gif
/com/day/cq/portlet/toolbar/layout/toolbar.css
```

La carpeta META-INF contiene el archivo MANIFEST.MF requerido por OSGi para identificarlo como un paquete. Aparece como sigue:

```xml
Manifest-Version: 1.0
Built-By: djaeggi
Created-By: Apache Maven Bundle Plugin
Import-Package: com.day.cq.portlet.toolbar.layout
Bnd-LastModified: 1234178347159
Export-Package: com.day.cq.portlet.toolbar.layout
Bundle-Version: 0.0.1.SNAPSHOT
Bundle-Name: Company CQ5 Portal Director Portlet Toolbar Layout
Bundle-Description: This bundle provides a custom layout for the CQ5 P
 ortal Director Portlet Toolbar.
Build-Jdk: 1.5.0_16
Bundle-ManifestVersion: 2
Bundle-SymbolicName: com.day.cq.portlet.company.toolbarlayout
Tool: Bnd-0.0.255
```

El portlet exige que las imágenes HTML/CSS se encuentren dentro de la carpeta /com/day/cq/portlet/toolbar/layout y no se pueden cambiar. En las mismas líneas, los encabezados Import-Package y Export-Package en MANIFEST.MF también deben llamarse /com/day/cq/portlet/toolbar/layout. Bundle-SymbolicName debe ser un nombre de paquete único y completo.

Puede crearlo con una herramienta como, por ejemplo, crear manualmente un archivo jar de este tipo con el encabezado correspondiente establecido como se muestra en esta sección.

#### Vistas de la barra de herramientas del portlet {#portlet-toolbar-views}

La barra de herramientas del portlet tiene básicamente dos estados de vista. Cada vista y los botones asociados se pueden personalizar con un archivo HTML respectivo.

#### Vista de publicación {#publish-view}

La vista de publicación solo tiene un botón que cambia la barra de herramientas a la vista Administrar. La vista de publicación está representada por el archivo publish.html en el paquete [](/help/sites-deploying/configuring-osgi.md#bundles)anterior. En el HTML, puede utilizar los siguientes marcadores de posición, que son reemplazados por el portlet con el contenido correspondiente cuando se procesan:

#### Marcadores de posición de vista de publicación {#publish-view-placeholders}

| Cadena de marcador de posición | Descripción |
|---|---|
| {buttonManage} | El marcador de posición se sustituye por el botón **Administrar **que cambia el estado del portlet al estado de administración. |

#### Administrar vista {#manage-view}

La vista de administración tiene cuatro botones: Editar, ficha Sitios web, Actualizar y Atrás. La vista de administración se representa mediante el archivo manage.html en el paquete [anterior](/help/sites-deploying/configuring-osgi.md#bundles). En el HTML, puede utilizar los siguientes marcadores de posición, que son reemplazados por el portlet con el contenido correspondiente cuando se procesan:

#### Administrar marcadores de posición de vista {#manage-view-placeholders}

| Cadena de marcador de posición | Descripción |
|---|---|
| {buttonEdit} | El marcador de posición se sustituye por el botón** Editar**, que abre una nueva ventana con la página actual en el modo de edición de AEM. |
| {ficha buttonWebsites} | Marcador de posición, sustituido por un botón que abre la ficha Sitios web de AEM WCM. |
| {buttonRefresh} | Actualiza la vista actual. |
| {buttonBack} | Cambia el portlet de nuevo a la vista de publicación. |

#### Botones {#buttons}

Los botones, en cualquier vista que aparezcan, utilizan el mismo código HTML común, definido en button.html.

En el HTML, puede utilizar los siguientes marcadores de posición, que son reemplazados por el portlet con el contenido correspondiente cuando se procesan:

#### Botones Administrar y Publicar vista {#manage-and-publish-view-buttons}

| Cadena de marcador de posición | Descripción |
|---|---|
| {name} | Nombre del botón, por ejemplo, autor**, reverso, actualizar**, etc. |
| {id} | ID de CSS del botón. |
| {url} | Dirección URL del destino del botón. |
| {text} | Etiqueta del botón. |
| {onclick} | Función **onclick** de JavaScript (contiene {url}). |

Ejemplo de un archivo button.html:

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### Instalación de un diseño personalizado {#installing-a-custom-layout}

Para instalar un diseño personalizado, acceda a la sección OSGI Web console del portlet **Bundles **y cargue el paquete.

#### Paquetes {#packages}

Si necesita cargar o crear paquetes para la instalación, consulte el Administrador de paquetes en la documentación de AEM para obtener instrucciones detalladas.

### Administración de vínculos {#link-handling}

Todos los vínculos se reescriben para que funcionen en el contexto del portal. De forma predeterminada, se utilizan vínculos con parámetros de procesamiento. El reescritor HTML del director del portal puede configurarse para utilizar vínculos de acción en su lugar.

También puede definir parámetros de solicitud adicionales que se consultarán para que se muestre la ruta de contenido. Esto resulta útil, por ejemplo, si hay un vínculo desde el exterior a contenido específico.

Además, el reescritor HTML del director del portal puede configurarse con una lista de expresiones regulares definidas excluidas para la reescritura de vínculos. Por ejemplo, si tiene vínculos relativos a sistemas externos, debe agregarlos a esta lista de exclusión.

### Localización {#localization}

El portlet de contenido de AEM tiene una función de localización integrada que garantiza que el contenido de AEM esté en el idioma correcto.

Esto se realiza en dos pasos:

1. El detector de configuración regional del directorio del portal detecta la configuración regional del usuario del portal obteniendo la configuración regional del portal. Este servicio debe configurarse con la lista de idiomas disponibles en AEM.
1. El controlador de configuración regional del director del portal gestiona la localización de la solicitud actual. Toma la ruta del contenido solicitado, por ejemplo `/content/geometrixx/en/company.html`y según la configuración, vuelve a escribir el **final** con la configuración regional real del usuario.

El controlador de configuración regional del director del portal se puede configurar con las rutas para comprobar la información de configuración regional; generalmente esto incluye todo lo que se encuentra debajo `/content` y con la posición de la información de configuración regional en la ruta. De forma predeterminada, el controlador de configuración regional sigue la recomendación de estructurar sitios en varios idiomas dentro de AEM.

Si su sitio no tiene una regla estricta para administrar la información de configuración regional dentro de la ruta, es posible reemplazar el controlador de configuración regional con su propia implementación.

### Servicios OSGi opcionales {#optional-osgi-services}

Los servicios OSGi opcionales se pueden implementar para personalizar varias partes del portlet. Cada servicio corresponde a una interfaz de Java. Esta interfaz se puede implementar e implementar mediante un paquete en el portlet.

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>El rastreador de solicitudes recibe notificaciones cada vez que el portlet muestra contenido. Esto le permite realizar un seguimiento de las invocaciones del portlet.</td>
  </tr>
  <tr>
   <td>InvocationContextListener</td>
   <td>Listener que se invoca al principio y al final de cada solicitud al portlet. El detector puede utilizarse para cambiar o agregar información para la solicitud actual.<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>Controlador de errores personalizado para los errores durante la fase de procesamiento.</td>
  </tr>
  <tr>
   <td>HttpProcessor</td>
   <td>Este servicio se puede utilizar para añadir información a cada invocación http en AEM.</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>Agregar una acción propia al portlet: esta acción se puede invocar a través de un vínculo de acción portlet.</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>Este servicio puede utilizarse para decorar el contenido del portlet.</td>
  </tr>
  <tr>
   <td>ResourceProvider</td>
   <td>Agregue su propio proveedor de recursos para entregar algún recurso a través de un vínculo de recurso de portlet al cliente.</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>Permite anunciar archivos HTML, CSS y Javascript de proceso.</td>
  </tr>
  <tr>
   <td>ToolbarButton</td>
   <td>Agregue su propio botón a la barra de herramientas.</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>Agregue un servicio para aplicar una asignación de URL personalizada o reescribir.</td>
  </tr>
  <tr>
   <td>UserInfoProvider</td>
   <td>Agregue su propia información sobre el usuario. Este servicio se puede utilizar para obtener información del portal al portlet.</td>
  </tr>
 </tbody>
</table>

#### Reemplazar servicios predeterminados {#replacing-default-services}

Los siguientes servicios tienen una implementación predeterminada en el portlet de contenido (con una interfaz Java correspondiente). Para personalizar, se debe implementar un paquete que contenga la nueva implementación de servicio en la aplicación portlet.

Al implementar un servicio de este tipo, asegúrese de establecer la propiedad **service.ranking** del servicio en un valor positivo. La implementación predeterminada utiliza la clasificación** 0** y el portlet utiliza el servicio con la clasificación más alta.

| **Nombre** | **Descripción** | **Comportamiento predeterminado** |
|---|---|---|
| Autenticador | Proporciona información de autenticación a AEM | Utiliza un usuario técnico configurable para crear y publicar. O SSO. |
| HTMLRewriter | Reescribe vínculos, imágenes, etc. | Reescribe los vínculos de AEM a los vínculos de portal, que se pueden ampliar con un objeto UrlMapper y un objeto TextMapper |
| HttpClientService | Gestiona todas las conexiones http | Implementación estándar |
| LocaleHandler | Gestiona la información de configuración regional | Reescribe un vínculo al contenido con respecto a la configuración regional. |
| LocaleDetector | Detecta la configuración regional del usuario. | Utiliza la configuración regional proporcionada por el portal. |
| PrivilegeManager | Comprueba los derechos de usuario | Comprueba el acceso a la instancia de autor si el usuario puede editar el contenido |
| ToolbarRenderer | Procesa la barra de herramientas | Agrega una funcionalidad de barra de herramientas |

### Eventos de portlet {#portlet-events}

La API de portlet (JSR-286) especifica eventos de portlet. El portlet de contenido de AEM tiene un puente integrado, que distribuye eventos de portlet para el portlet de AEM como eventos OSGi, lo que hace que el manejo de los eventos de portlet sea conectable.

Si desea gestionar eventos específicos, declare que reciben eventos en el descriptor de implementación (o configúrelos a través del servidor del portal) e implemente un servicio OSGi declarando la interfaz EventHandler (consulte la especificación OSGi EventAdmin).

Siempre que se produce un evento de portlet, se envía un evento de OSGi específico invocando al controlador. El controlador obtiene toda la información de contexto y puede actualizar el estado del portlet en consecuencia o enviar nuevos eventos. Básicamente, dentro del método de control se puede utilizar toda la funcionalidad de la fase del evento portlet.

## Uso de AEM como portal {#using-aem-as-a-portal}

Utilice el componente Portlet para agregar ventanas de portlet a las páginas de AEM. Las bibliotecas compartidas que instale en el servidor de aplicaciones permiten que el componente Portlet detecte las aplicaciones portlet implementadas.

Para utilizar AEM como portal, realice las siguientes tareas:

1. Instale el componente Portlet y las bibliotecas compartidas.
1. Agregue el componente Portlet a la barra de tareas.
1. Configure e implemente la aplicación web que contiene los portlets que desea que aparezcan en el componente Portal.
1. Agregue el componente Portlet a una página y seleccione el portlet que desea mostrar.

>[!NOTE]
>
>El componente portlet solo se puede usar cuando AEM se implementa como una aplicación web. ([Consulte Instalación de AEM con un servidor]de aplicaciones (/content/docs/en/aem/6-3/deploy/installing.md#installing adobe experience manager with an application server).)

### Instalación del componente portlet {#installing-the-portlet-component}

El archivo JAR de inicio rápido de AEM contiene los archivos de componentes del portlet. Para obtener los archivos (cq-portlet-components.zip), puede ejecutar Quickstart o extraer el contenido.

1. Ejecute o extraiga el contenido del archivo JAR de QuickStart y busque el archivo cq-portlet-components.zip según corresponda:

   * Ejecutar inicio rápido: crx-quickstart/opt/portal
   * Extraer contenido de inicio rápido: static/opt/portal

1. Abra el Administrador de paquetes de la instancia de creación de CQ5 implementada en el servidor de aplicaciones. (https://*appserverhost*:*port*/cq5author/crx/packmgr)

1. Utilice el Administrador de paquetes para [cargar e instalar](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) el paquete cq-portlets-components.zip.

   El paquete instala cq-portlet-director-sharedlibs-x.x.x.jar en la carpeta /libs/portal/director del repositorio.

1. Copie cq-portlet-director-sharedlibs-x.x.x.jar en el disco duro. Utilice cualquier medio para obtener el archivo, por ejemplo, FileVault o un cliente WebDAV.
1. Mueva el archivo cq-portlet-director-sharedlibs.x.x.x.jar a la carpeta de biblioteca compartida del servidor de aplicaciones para que las clases estén disponibles para las aplicaciones portlet implementadas.

### Adición del componente Portlet a la barra de tareas {#adding-the-portlet-component-to-sidekick}

Agregue el componente portlet al sistema de párrafos para que esté disponible para los autores.

1. En la barra de tareas, haga clic en el icono de regla para entrar en el modo Diseño.
1. Junto al `Design of par` encabezado sobre el primer párrafo, haga clic en **Editar**.

1. En la categoría de componentes **General** , active la casilla de verificación situada junto al componente Portlet y haga clic en Aceptar.

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### Configuración e implementación de las aplicaciones de portlet {#configuring-and-deploying-your-portlet-applications}

Implemente los portlets en el contenedor web del servidor de aplicaciones para que estén disponibles para el componente Portal. Antes de implementar la aplicación portlet, debe configurar la aplicación para que cargue el servlet de contenedor del portal de AEM. Esta configuración permite que el componente Portlet acceda a los portlets.

1. Extraiga el contenido del archivo WAR de la aplicación portlet.

   **** Sugerencia: El comando jar xf *name ofapp*.war extrae los archivos.

1. Abra el archivo web.xml en un editor de texto.
1. Agregue la siguiente configuración de servlet dentro del elemento web-app:

   ```xml
   <servlet>
           <servlet-name>slingportal</servlet-name>
           <servlet-class>org.apache.sling.portal.container.api.ContainerServlet</servlet-class>
           <load-on-startup>1</load-on-startup>
   </servlet>
   <servlet-mapping>
           <servlet-name>slingportal</servlet-name>
           <url-pattern>/SlingPortletInvoker</url-pattern>
   </servlet-mapping>
   ```

1. Guarde el archivo web.xml y vuelva a empaquetar el archivo WAR.

   **** Sugerencia: El `jar cvf nameofapp.war *` comando agrega contenido del directorio actual al archivo name.app.war.

1. Implemente la aplicación portlet en el servidor de aplicaciones. Para obtener más información, consulte la documentación del servidor de aplicaciones.

### Adición de portlets a la página de AEM {#adding-portlets-to-your-aem-page}

Utilice el componente Portal para añadir una ventana portlet a la página web. Utilice las propiedades del componente para especificar el portlet que se va a mostrar.

1. En la página web, arrastre el componente **Portlet** del grupo General en la barra de tareas a la página.

   >[!NOTE]
   >
   >Después de arrastrar el componente a la página, vuelva a cargar la página para asegurarse de que funciona correctamente.

1. Haga doble clic en el componente para abrir las propiedades de Portlet.
1. En el menú desplegable **Entidad** del portlet, seleccione el portlet en la lista.
1. Active o desactive la casilla de verificación **Ocultar barra de título **dependiendo de si desea ver la barra de título del portlet.
1. En el campo **Ventana** portlet, introduzca un ID de ventana de portlet único, si lo desea.

   >[!NOTE]
   >
   >Si planea utilizar el mismo portlet más de una vez en la misma página, proporcione a cada portlet un ID de ventana diferente.

1. Haga clic en **Aceptar**. El portlet se muestra en la página de AEM.

   ![chlimage_1-136](assets/chlimage_1-136.png)

## Instalación, configuración y uso de AEM en un portlet {#installing-configuring-and-using-aem-in-a-portlet}

Para acceder al contenido proporcionado por AEM WCM, el servidor del portal debe estar equipado con el portlet de AEM Portal Director. Para ello, instale, configure y agregue el portlet a la página del portal siguiendo los pasos que se indican en esta sección.

De forma predeterminada, el portlet se conecta a la instancia de publicación en localhost:4503 y a la instancia de autor en localhost:4502. Estos valores se pueden cambiar durante la implementación del portlet. El director del portal está disponible como contenido en el repositorio en /libs/portal/directory. Deberá descargar el archivo de guerra de la aplicación antes de utilizarlo.

### Descarga del archivo de guerra {#downloading-the-war-file}

1. Con Webdav o CRXDE Lite, navegue a /libs/portal/director.

1. Descargue *cq-portlet-webapp.war*.

>[!NOTE]
>
>Estos procedimientos utilizan como ejemplo el portal de la Web, aunque son lo más genéricos posible; tenga en cuenta que los procedimientos varían para otros portales web. Aunque los pasos son básicamente idénticos para todos los portales Web, debe reutilizar los pasos para el portal Web en particular.

#### Instalación del portlet {#installing-the-portlet}

Para instalar el portlet:

1. Inicie sesión en el portal con privilegios de administrador.
1. Vaya a la parte Administración de portlets del portal web.
1. Haga clic en Instalar y vaya a la aplicación portlet de AEM (cq-portlet-webapp.war) que ha descargado e introduzca otra información importante sobre el portlet.

   Para otra información esencial del portlet, puede aceptar los valores predeterminados o cambiar los valores. Si acepta los valores predeterminados, el portlet estará disponible en https://&lt;wps-host>:&lt;puerto>/wps/PA_CQ5_Portlet. La consola de administración OSGi proporcionada por el portlet está disponible en https://&lt;wps-host>:&lt;puerto>/wps/ PA_CQ5_Portlet/cqbridge/system/console (el nombre de usuario/contraseña predeterminado es admin/admin).

1. Asegúrese de que la aplicación portlet se inicia automáticamente seleccionando esa opción o casilla de verificación y guardando los cambios. Verá un mensaje que indica que la instalación se realizó correctamente.

#### Configuración del portlet {#configuring-the-portlet}

Después de instalar el portlet, debe configurarlo para que conozca las direcciones URL de las instancias de AEM subyacentes (autor y publicación). También puede configurar otras opciones.

Para configurar el portlet:

1. En la ventana de administración del portal del servidor de aplicaciones, navegue hasta la administración de portlets, donde se muestran todos los portlets, y seleccione el portlet de AEM Portal Director.
1. Configure el portlet según sea necesario. Por ejemplo, es posible que tenga que cambiar la dirección URL de las instancias de autor y publicación y la dirección URL de la ruta de inicio. Las configuraciones predeterminadas se describen en Preferencias [](/help/sites-administering/aem-as-portal.md#portlet-preferences)de portlet.

   >[!NOTE]
   >
   >Si el portlet está configurado para conectarse al autor de AEM y publicar instancias que se ejecutan en una ruta de contexto distinta a** /**, debe activar la fuerza **CQUrlInfo** en la configuración del Administrador de bibliotecas Html de estas instancias de AEM (por ejemplo, mediante Felix Webconsole) o la edición no funcionará y no aparecerá el cuadro de diálogo de preferencias.

1. Guarde los cambios de configuración en el servidor de aplicaciones.

1. Vaya a la consola de administración OSGI para el portlet. La ubicación predeterminada es `https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr`. El nombre de usuario/contraseña predeterminado es **admin/admin**.

1. Seleccione la configuración de configuración **de CQ Server de** Day Portal Director y edite los siguientes valores:

   * **Dirección URL** base del autor: Dirección URL base para la instancia de creación de AEM.
   * **Publicar URL** base: La URL base para la instancia de publicación de AEM.
   * **El Autor Se Utiliza Como Publicación**: ¿Se utiliza la instancia de autor como instancia de publicación (para desarrollo)?
   ![chlimage_1-137](assets/chlimage_1-137.png)

1. Haga clic en **Guardar.** Ahora puede agregar el portlet a las páginas de portal y usar el portal.

### Direcciones URL de contenido {#content-urls}

Cuando se solicita contenido desde AEM, el portlet utiliza el modo de visualización actual (publicación o autor) y la ruta actual para compilar una dirección URL completa. Con los valores predeterminados, la primera dirección URL es `https://localhost:4503/content/geometrixx/en.portlet.html`. El valor del `htmlSelector` se agrega automáticamente a la dirección URL antes de la extensión.

Si el portlet cambia al modo de ayuda y el `appendHelpViewModeAsSelector` está seleccionado, el `help` selector también se anexa, por ejemplo, `https://localhost:4503/content/geometrixx/en.portlet.html.help`. Si la ventana del portlet está maximizada y `appendMaxWindowStateAsSelector` está seleccionada, el selector también se anexa, por ejemplo, `https://localhost:4503/content/geometrixx/en.portlet.max.help`.

Los selectores se pueden evaluar en AEM y se puede utilizar una plantilla diferente para los distintos selectores.

### Uso de un mapa de URL de contenido en AEM {#using-a-content-url-map-in-aem}

Normalmente, la ruta de inicio apunta directamente al contenido de AEM. Sin embargo, si desea mantener las rutas de inicio en AEM en lugar de en las preferencias del portlet, puede señalar la ruta de inicio a un mapa de contenido en AEM, como `/var/portlets`. En este caso, una secuencia de comandos que se ejecute en AEM puede utilizar la información enviada desde el portlet para decidir qué dirección URL es la dirección URL de inicio. Debe enviar una redirección a la dirección URL correcta.

#### Adición del portlet a la página Portal {#adding-the-portlet-to-the-portal-page}

Para agregar el portlet a la página del portal:

1. Asegúrese de que se encuentra en la ventana de administración del servidor de aplicaciones y vaya a la ubicación donde administra las páginas. (por ejemplo, en WebSphere 6.1, haga clic en **Administrar páginas**).
1. Seleccione el nombre del portlet y, a continuación, seleccione una página existente o cree una nueva página.
1. Edite el diseño de la página.
1. Seleccione el portlet y agréguelo a un contenedor.
1.  Guarde los cambios.

#### Uso del portlet {#using-the-portlet}

Para acceder a la página agregada al portlet:

1. En el menú de personalización del portlet, configure el portlet tal como lo configuró en el portal.
1. Abra la configuración (el portlet muestra la URL de inicio de publicación configurada en la configuración del portlet), realice las modificaciones necesarias y guárdela.

