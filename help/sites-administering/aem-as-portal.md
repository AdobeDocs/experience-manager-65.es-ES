---
title: Portales AEM y portlets
seo-title: AEM Portals and Portlets
description: Obtenga información sobre Portals y Portles en AEM.
seo-description: Learn about Portals and Portles in AEM.
uuid: 7f9e316d-277e-4a1e-b6f3-cd89addc897b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 99528fda-5c8c-4034-bcbe-a4cea42f694b
docset: aem65
exl-id: b5f3d3a6-39c0-4aa5-8562-3cc6fa2b9e46
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6086'
ht-degree: 0%

---

# Portales AEM y portlets{#aem-portals-and-portlets}

En este documento se describe lo siguiente:

* Arquitectura AEM Portal
* Administración y configuración de AEM como portal
* Uso de AEM como portal
* Instalación, configuración y visualización AEM contenido en un portlet (por ejemplo, un servidor web)

## Arquitectura AEM Portal {#aem-portal-architecture}

AEM arquitectura del portal incluye definiciones de portales y portlets.

### ¿Qué es un portal? {#what-is-a-portal}

Un portal es una aplicación web que proporciona personalización, inicio de sesión único, integración de contenido de diferentes fuentes y aloja la capa de presentación de los sistemas de información.

Puede ejecutar portlets compatibles con JSR 286 en AEM. El componente portlet permite incrustar un portlet en la página. Consulte [Administración del Portlet de Contenido AEM](#administeringthecqcontentportlet).

### ¿Qué es un portlet? {#what-is-a-portlet}

Los portlets son componentes web implementados dentro de un contenedor que genera contenido dinámico. La interfaz de portlet se empaqueta y se implementa como un archivo .war dentro de un contenedor de portlet. Si está ejecutando AEM como portal, necesita el archivo .war del portlet para ejecutar el portlet.

Para configurar AEM contenido para que aparezca en un portal, consulte [Instalación, configuración y uso de AEM en un portlet](#installingconfiguringandusingcqinaportlet).

### AEM Portal Director {#aem-portal-director}

>[!CAUTION]
>
>El AEM Portal Director está en desuso a partir de AEM 6.4. Consulte [Funciones obsoletas y eliminadas](https://helpx.adobe.com/experience-manager/6-4/release-notes/deprecated-removed-features.html).

## Administración del Portlet de Contenido AEM {#administering-the-aem-content-portlet}

El portlet de contenido AEM permite mostrar contenido AEM en un portal. El portlet está disponible en `/crx-quickstart/opt/portal`, y se pueden personalizar de varias formas. Por ejemplo, puede personalizar la administración de SSO/Autenticación implementando su propio servicio de autenticación generando la información de autenticación necesaria para AEM sobrescribir el comportamiento predeterminado. Los complementos utilizan una API definida que le permite añadir su propia funcionalidad creando el complemento con la API. El complemento se puede implementar en el portlet en ejecución. Para funcionar correctamente, necesita una configuración de la instancia de creación y publicación de AEM junto con la ruta de contenido para mostrar al inicio.

Algunas de las configuraciones se pueden cambiar a través de las preferencias de portlet y otras a través de las configuraciones de servicio OSGi. Puede cambiar estas configuraciones utilizando **config** o la consola web OSGi.

### Preferencias de Portlet {#portlet-preferences}

Las preferencias de portlet se pueden configurar en el momento de la implementación en el servidor de portal o editando el **WEB-INF/portlet.xml** antes de implementar la aplicación web portlet. El archivo portlet.xml aparece de la siguiente manera de forma predeterminada:

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
   <td><p>Esta es la ruta de inicio del portlet: define el contenido que se muestra inicialmente.</p> <p><strong>Importante</strong>: Si el portlet está configurado para conectarse a AEM instancias de autor y publicación que se ejecutan en una ruta de contexto diferente a<strong> /</strong>, debe activar la fuerza <strong>CQUrlInfo</strong> en la configuración de Html Library Manager de estas instancias de AEM (por ejemplo, a través de Felix Webconsole) o la edición no funcionará y el cuadro de diálogo de preferencias no aparecerá.</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>Selector que se anexa a cada URL. De forma predeterminada, es <strong>portlet</strong>, de modo que todas las solicitudes para páginas html utilizan direcciones url que terminan en <strong>.portlet.html.</strong> Esto permite el uso de scripts personalizados en AEM para la renderización de portlets.</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>De forma predeterminada, los archivos css incluidos en la página HTML de AEM se incluyen en el portlet. Al desactivar esta opción, se excluyen los archivos css predeterminados.</p> <p>Si esta opción está habilitada, los archivos CSS se añaden al encabezado de la página html o se incrustan en la página html en función del comportamiento del portal.</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>De forma predeterminada, se representa una barra de herramientas dentro del portlet de contenido para la funcionalidad de administración. Al desactivar esta opción, no se procesa ninguna barra de herramientas.</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>Lista de nombres de parámetros de URL alternativos que pueden contener la nueva dirección URL de contenido para mostrar en el portlet. La lista se procesa de arriba a abajo, se utiliza el primer parámetro que contiene un valor. Si no se encuentra ninguna URL, se utiliza el parámetro de URL predeterminado. La dirección URL proporcionada se utiliza, tal como está, sin más modificaciones.</p> <p>Esta configuración es por portlet implementado - también es para configurar globalmente algunos parámetros de url en la configuración OSGi para el "Puente de Portlet Day Portal Director".</p> </td>
  </tr>
  <tr>
   <td>priorityDialog</td>
   <td>Ruta al cuadro de diálogo de preferencias en AEM : si se deja vacío, se utilizará el cuadro de diálogo de preferencias integrado. El valor predeterminado es /libs/portal/content/prefs.html.</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>De forma predeterminada, el portlet realiza un redireccionamiento de javascript de toda la página del portal en la primera invocación. Esto es compatible con el escenario de arrastrar y soltar de los servidores de portal modernos. En producción, esta redirección raramente es necesaria y, por lo tanto, se puede desactivar si se establece esta preferencia en <em>false</em>.</td>
  </tr>
 </tbody>
</table>

#### Consola web OSGi {#osgi-web-console}

Suponiendo que el servidor de portal se ejecute en host localhost, puerto 8080 y que la aplicación web AEM portlet esté montada en el contexto de la aplicación web *cqportlet*, la dirección url a para la consola web es `https://localhost:8080/cqportlet/cqbridge/system/console`. El usuario y la contraseña predeterminados son **admin**.

Abra el **Configuraciones** y seleccione **Configuración del servidor CQ de directorio de portal**. Aquí puede especificar la URL base para el autor y la instancia de publicación. Este procedimiento se describe en [Configuración del Portlet](#configuring-the-portlet).

>[!NOTE]
>
>La consola web OSGi solo está pensada para cambiar configuraciones durante el desarrollo (o las pruebas). Asegúrese de bloquear las solicitudes a la consola para los sistemas de producción.

### Proporcionar configuraciones {#providing-configurations}

Para admitir implementaciones automatizadas y aprovisionamiento de configuración, el portlet de contenido AEM tiene compatibilidad de configuración integrada que intenta leer configuraciones de la ruta de clase proporcionada a la aplicación portlet.

Al inicio, la propiedad del sistema **com.day.cq.portet.config** se lee para detectar el entorno actual. Normalmente, el valor de esta propiedad es algo así como **dev**, **prod**, **prueba** y así sucesivamente. Si no se establece ningún entorno, no se lee ninguna configuración.

Si se configura un entorno, se busca un archivo de configuración en la ruta de clases en* ***com/day/cq/portlet/{env}.config** donde **env** se sustituye por el valor real del entorno. Este archivo debe listar todos los archivos de configuración para este entorno. Estos archivos se buscan en función de la ubicación del archivo de configuración. Por ejemplo, si el archivo contiene una línea `my.service.xml,` este archivo se lee desde la ruta de clases en `com/day/cq/portlet/my.service.config.` El nombre del archivo consta del ID de persistencia del servicio, seguido de **.config**. En el ejemplo anterior, el ID de persistencia es **my.service**. El formato del archivo de configuración es el formato utilizado por el instalador Apache Sling OSGi.

Esto significa que, para cada entorno, es necesario agregar un archivo de configuración correspondiente. Se debe introducir una configuración que se aplique a todos los entornos en todos estos archivos. Si es solo para un entorno único, simplemente se introduce en ese archivo. Este mecanismo garantiza el control total sobre qué configuración se lee en cada entorno.

Es posible utilizar una propiedad de sistema diferente para detectar el entorno. Especificar la propiedad del sistema **com.day.cq.portet.configproperty** que contiene el nombre de la propiedad del sistema que se va a usar en lugar de **com.day.cq.portet.config**.

#### Invalidación de almacenamiento en caché {#caching-and-caching-invalidation}

El portlet, en su configuración predeterminada, almacena en caché las respuestas que recibe de AEM WCM en una caché específica del usuario. Las cachés deben invalidarse cuando se producen cambios en el contenido de la instancia de publicación. Para este fin, en AEM WCM debe configurarse un agente de replicación en la instancia de autor. La caché también se puede vaciar manualmente. En esta sección se describen ambos procedimientos.

El portlet puede configurarse con su propia caché, de modo que el contenido del portlet se muestre sin necesidad de acceso a AEM. El portal está disponible como contenido en /libs/portal/director. Para acceder al contenido, inicie una instancia de AEM y descargue, mediante el CRXDE Lite o Webdav, el archivo desde esa ubicación.

Puede implementar este paquete durante la ejecución o agregarlo a la aplicación web del portlet en `WEB-INF/lib/resources/bundles` antes de la implementación.

Una vez implementada la caché, el portlet almacena en caché el contenido de la instancia de publicación. La caché del portlet se puede invalidar con un vaciado de Dispatcher de AEM. Para configurar el portlet para que utilice su propia caché:

1. Configure un agente de replicación en author que se dirija al servidor de portal.
1. Suponiendo que el servidor de portal se ejecute en el host **localhost**, **puerto 8080 **y la aplicación web AEM portlet se monta en el contexto **cqportlet**, la dirección url para vaciar la caché es `https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)`. Utilice GET como método.
   **Nota:** En lugar de utilizar un parámetro de solicitud, puede enviar un encabezado http denominado **Ruta**.

#### Vaciado de la caché mediante el agente de replicación {#flushing-the-cache-via-replication-agent}

Al igual que la invalidación normal de Dispatcher, se puede configurar un agente de replicación para que se dirija a la caché AEM portlet del portal. Después de configurar el agente de replicación, cada activación de página normal descarga la caché del portal.

Si opera varios nodos de portal que ejecutan el AEM portlet, debe crear un agente para cada nodo como se describe en este procedimiento.

Para configurar un agente de replicación para el portal:

1. Inicie sesión en la instancia de autor.
1. En la ficha Sitios web , haga clic en la *Herramientas* pestaña .
1. Haga clic en **Nueva página...** en los agentes de replicación **Nuevo...** para abrir el Navegador.

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. En *Plantilla*, seleccione *Agente de replicación* e introduzca un nombre para el agente. Haga clic en *Crear*.

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. Haga doble clic en el agente de replicación que acaba de crear. Se muestra como no válido, ya que aún no se ha configurado.

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. Haga clic en **Editar.**
1. En el **Configuración** , seleccione **Habilitado** casilla de verificación, seleccione **Vaciado de Dispatcher** como tipo de serialización e introduzca un tiempo de espera de reintento (por ejemplo, 60000).

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. Haga clic en el **Transporte** pestaña .
1. En el **URI** , introduzca el URI de vaciado (URL) del portlet. El URI tiene el siguiente formato:

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322pm](assets/screen_shot_2012-02-15at42322pm.png)

1. Haga clic en el **Extendido** pestaña .

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. En el **Método HTTP** campo, tipo **GET**.
1. En el **Encabezados HTTP** , haga clic en **+** para agregar una nueva entrada y escribir **Ruta: {ruta}**.
1. Si es necesario, haga clic en el botón **Proxy** e introduzca información de proxy al agente.
1. Haga clic en **OK** para guardar los cambios.
1. Para probar la conexión, haga clic en el botón **Probar conexión** vínculo. Aparece un mensaje de registro que indica si la prueba de replicación se realizó correctamente. Por ejemplo:

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### Vaciar manualmente la caché de Portlet {#manually-flushing-the-portlet-cache}

Puede vaciar manualmente la caché del portlet accediendo a la misma URL configurada para el agente de replicación. Consulte [Vaciando la caché](#flushing-the-cache-via-replication-agent) para el formulario de la URL. Además, la dirección URL debe ampliarse con un parámetro de URL Path=&lt;path> para indicar qué vaciar.

Por ejemplo:

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` descarga la caché completa. `https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz` flushes `/content/mypage/xyz` de la caché.

### Seguridad del portal {#portal-security}

El portal es el mecanismo de autenticación de la conducción. Puede iniciar sesión en AEM con un usuario técnico, el usuario del portal, un grupo, etc. El portlet no tiene acceso a la contraseña del usuario en el portal, por lo que si el portlet no conoce todas las credenciales para iniciar sesión correctamente en un usuario, se debe utilizar una solución SSO. En este caso, el AEM portlet reenvía toda la información necesaria a AEM, lo que a su vez reenvía esta información al repositorio AEM subyacente. Este comportamiento es conectable y se puede personalizar.

### Autenticación en publicación {#authentication-on-publish}

En esta sección se describen los modos de autenticación disponibles que el portlet puede utilizar para comunicarse con las instancias de WCM de AEM subyacentes.

De forma predeterminada, no se envía ninguna información de usuario a la instancia de publicación de AEM; el contenido siempre se muestra como usuario anónimo. Si la información específica del usuario debe entregarse desde AEM o si se requiere autenticación de usuario para la publicación, esto debe activarse.

#### Acceso a la configuración de autenticación del Portlet {#accessing-the-portlet-s-authentication-configuration}

Las opciones de configuración de autenticación que utiliza el portlet en AEM instancias WCM están disponibles en la consola web (configuración OSGi).

>[!NOTE]
>
>Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de los servicios OSGi (nodos de consola o repositorio).
>
>Consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información.

Para acceder a la configuración de autenticación del portlet:

1. Acceda a la consola web en la siguiente URL:

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   Por ejemplo, en su configuración predeterminada:

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. Inicie sesión en la consola web. Las credenciales predeterminadas son `admin/admin`.
1. En la consola, seleccione **Configuración**.
1. En el **Configuración** , seleccione un servicio concreto que desea configurar. Los servicios son proporcionados por el portlet en el marco de OSGi.

   | Nombre del servicio | Descripción |
   |---|---|
   | Autenticador de Day Portal Director | Configure qué modo de autenticación se utiliza para AEM instancias WCM. Según el modo seleccionado, se puede especificar un usuario técnico o el nombre de la cookie SSO. Además, se puede habilitar la autenticación para AEM instancias de publicación de WCM. |
   | Caché de archivos Director del portal del día | Configure los parámetros de cómo el portlet almacena en caché las respuestas que recibe de AEM instancias de WCM. |
   | Servicio de cliente HTTP Day Portal Director | Configure cómo se conecta el portlet a través de HTTP con las instancias AEM WCM subyacentes. Por ejemplo, puede especificar un servidor proxy. |
   | Controlador de configuración regional de Director del portal de días | Configure qué configuraciones regionales admite el portlet. Las solicitudes para AEM instancias de WCM se basan en la configuración regional del usuario; por ejemplo, idioma del usuario *alemán *solicitaría `/content/geometrixx/de/`.... |
   | Administrador de privilegios de Day Portal Director | Configure si el portlet debe probar la ficha Sitios web en función del usuario que ha iniciado sesión. |
   | Procesador de la barra de herramientas de Day Portal Director | Personalice la renderización de la barra de herramientas del portlet. |

1. Además, puede configurar la consola web y el servicio de registro. Por ejemplo, puede cambiar las credenciales de administrador para la consola web haciendo clic en el vínculo de la Consola de administración Apache Felix OSGi.

#### Modo de usuario técnico {#technical-user-mode}

En el modo predeterminado, todas las solicitudes emitidas por el portlet para la instancia de autor de WCM de AEM se autentican con el mismo usuario técnico, independientemente del usuario del portal actual. El modo Usuario técnico está habilitado de forma predeterminada. Puede habilitar/deshabilitar este modo en la pantalla de configuración correspondiente en la consola de administración de OSGi:

El usuario técnico especificado debe existir en la instancia de autor de WCM AEM y en la instancia de publicación si **Autenticar al publicar** está activada. Asegúrese de otorgar al usuario privilegios de acceso suficientes para el trabajo de creación.

#### SSO {#sso}

El portlet admite SSO con AEM fuera de la caja. El servicio de autenticación puede configurarse para utilizar SSO y transmitir el usuario del portal actual con formato **Básico** como una cookie denominada `cqpsso` a AEM. AEM debe configurarse para utilizar el controlador de autenticación SSO para la ruta /. El nombre de la cookie también debe configurarse aquí.

La variable `crx-quickstart/repository/repository.xml` para AEM repositorio debe configurarse en consecuencia:

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### Modo de autenticación SSO {#sso-authentication-mode}

El portlet puede autenticarse para AEM WCM mediante el esquema de inicio de sesión único (SSO). En este modo, el usuario que ha iniciado sesión en el portal se reenvía a AEM WCM en forma de cookie SSO. Si se utiliza el modo SSO, todos los usuarios del portal con acceso al portlet AEM deben ser conocidos por las instancias de WCM AEM subyacentes, normalmente en forma de AEM WCM conectado a LDAP, o por haber creado manualmente los usuarios de antemano. Además, antes de habilitar SSO en el portlet, la instancia de autor AEM WCM subyacente (y la instancia de publicación, si **Autenticar al publicar** está habilitado) debe configurarse para aceptar solicitudes basadas en SSO.

Para configurar el portlet para que utilice el modo de autenticación SSO, complete los siguientes pasos (descritos detalladamente en las secciones siguientes):

* Habilite AEM repositorio de WCM para aceptar credenciales de confianza.
* Habilite la autenticación SSO en el WCM AEM.
* Habilite la autenticación SSO en el portlet AEM.

#### Habilitación AEM repositorio de WCM para aceptar credenciales de confianza {#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

Antes de que SSO se pueda habilitar para AEM WCM, el repositorio subyacente debe configurarse para aceptar las credenciales de confianza proporcionadas por AEM WCM. Para ello, configure AEM repository.xml.

1. En el sistema de archivos donde está instalado AEM WCM, abra el siguiente archivo:

   `//crx-quickstart/repository/repository.xml`

1. En el archivo XML, busque la entrada para la variable **LoginModule** y agregue el atributo trust_credentials_attribute a su configuración:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
     <param name="anonymous_principal" value="anonymous"/>
   </LoginModule>
   ```

1. Reinicie AEM WCM para que los cambios surtan efecto.

#### Habilitar la autenticación SSO en el WCM AEM {#enabling-sso-authentication-in-the-aem-wcm}

Para habilitar SSO en AEM WCM, acceda a la entrada de configuración correspondiente en la consola de gestión web Apache Felix (OSGi) de AEM WCM:

1. Acceda a la consola a través de su URI en https://&lt;aem-host>:&lt;port>/system/console.
1. En el menú Configuración, seleccione Gestor de autenticación SSO. En este ejemplo, el controlador SSO acepta solicitudes SSO para todas las rutas de acceso en función de la cookie proporcionada por el AEM portlet. La configuración puede variar.

   | Ruta  | / | Habilita el controlador SSO para todas las solicitudes |
   |---|---|---|
   | Nombres de cookies | cqpsso | Nombre de la cookie proporcionada por el portlet tal como está configurada en la consola OSGi del portlet. |

1. Haga clic en **Guardar** para habilitar SSO. SSO es ahora el esquema de autenticación principal.

Por cada solicitud que AEM WCM recibe, primero se intenta la autenticación basada en SSO. En caso de error, se realiza una alternativa al esquema de autenticación básico habitual. Como tal, las conexiones normales a AEM WCM sin SSO siguen siendo posibles.

#### Habilitar la autenticación SSO en un Portlet AEM {#enabling-sso-authentication-in-a-aem-portlet}

Para que la instancia WCM de AEM subyacente acepte solicitudes SSO, el modo de autenticación del portlet debe conmutarse de **Técnico** a **SSO**.

Para habilitar la autenticación SSO en un portlet AEM:

1. Acceda a la consola a través de su URI en https://&lt;aem-host>:&lt;port>/system/console.
1. En el menú Configuración, seleccione Autenticador de Day Portal Director de la lista de configuraciones disponibles.
1. En Modo, seleccione SSO. Deje los demás parámetros con sus valores predeterminados.

   ![chlimage_1-135](assets/chlimage_1-135.png)

1. Haga clic en Guardar para habilitar SSO para el portlet.

   Para fines de prueba, acceda al portlet con el usuario administrativo del portal, después de crear el mismo usuario en AEM WCM con privilegios de administrador.

Después de realizar este procedimiento, las solicitudes se autentican mediante SSO. Un fragmento típico de la comunicación HTTP revela la presencia de los siguientes encabezados específicos de SSO y Portlet:

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

Si no utiliza las funciones de edición en línea predeterminadas del portlet de contenido AEM, pero desea que la parte de creación y administración del portlet fuera del portal directamente en la instancia de autor de AEM, debe habilitar la autenticación PIN. También debe cambiar la configuración de los botones de administración.

Para abrir la página de administración del sitio web o editar una página desde el portlet, el portlet de contenido AEM utiliza la nueva autenticación de pines. De forma predeterminada, la autenticación del pin está deshabilitada, por lo tanto, los siguientes cambios de configuración deben realizarse en AEM:

1. Habilite la autenticación de confianza en AEM agregando la información de confianza en el archivo repository.xml:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. En la consola de configuración OSGi, de forma predeterminada ubicada en https://localhost:4502/system/console/configMgr, seleccione **Gestor de autenticación CQ PIN** en el menú desplegable.
1. Edite el **Ruta raíz de URL** para contener solo el valor único **/**.

### Privilegios {#privileges}

Algunas funciones del portlet están protegidas por privilegios. El usuario actual necesita tener este privilegio para poder acceder a esta función. Hay los siguientes privilegios predefinidos:

* &quot;barra de herramientas&quot; : Este es el privilegio general de ver/usar la barra de herramientas en el portlet.
* &quot;prefs&quot; : Si el usuario tiene este privilegio, se le permite ver o cambiar las preferencias del portlet.
* &quot;cq-author:edit&quot; : Con este privilegio, el usuario puede invocar la vista de edición del contenido.
* &quot;cq-author:preview&quot; : Con este privilegio, el usuario puede ver la vista previa.
* &quot;cq-author:siteadmin&quot; : Con esta privacidad, el usuario puede abrir el siteadmin dentro de AEM.

El mejor enfoque para administrar los privilegios es utilizar las funciones de portal y asignar funciones a estos privilegios. Esto se puede hacer mediante una configuración OSGi. El &quot;Day Portal Director Privilege Manager&quot; se puede configurar con un conjunto de funciones para cada privilegio. Si el usuario tiene una de las funciones, tiene el privilegio correspondiente.

Además, es posible definir este acceso basado en el acceso a cada instancia de portlet. El cuadro de diálogo de preferencias del portlet contiene un campo de entrada para cada uno de los privilegios anteriores. Para cada privilegio se puede configurar una lista de funciones de portlet separadas por coma. Si se configura un valor, esto anula la configuración global del servicio &quot;Day Portal Director Privilege Manager&quot; y puede ser necesario agregar las mismas funciones de esta configuración global, ya que las funciones no se combinan. Si no se especifica ningún valor, se utiliza la configuración global.

### Personalización de la aplicación AEM portlet {#customizing-the-aem-portlet-application}

La aplicación AEM portlet proporcionada inicia un contenedor OSGi dentro de la aplicación web tal como AEM. Esta arquitectura le permite aprovechar todas las ventajas de OSGi:

* Fácil de actualizar y ampliar
* Proporciona actualizaciones rápidas del portlet sin ninguna interacción del servidor de portal
* Fácil de personalizar el portlet

### Botones de la barra de herramientas {#toolbar-buttons}

La barra de herramientas y sus botones se pueden configurar y personalizar. Puede añadir sus propios botones a la barra de herramientas o definir qué botones se muestran en cada modo. Cada botón es un servicio OSGi configurable a través de una configuración OSGi.

La consola web OSGi enumera todas las configuraciones de botones en la **Configuración** pestaña . Para cada botón, puede definir en qué modo se muestra este botón. Esto permite desactivar un botón eliminando todos los modos, por ejemplo.

De forma predeterminada, el AEM portlet de contenido utiliza la funcionalidad de edición en línea. Sin embargo, si prefiere cambiar a la instancia de autor de AEM para editarla, habilite la variable **Botón SiteAdmin** y **Botón ContentFinder**, pero deshabilite **Botón Editar**. En este caso, asegúrese de configurar correctamente la autenticación PIN en AEM.

El diseño de la barra de herramientas del portlet se puede personalizar instalando un paquete a través de la Consola Web Felix del portlet, que contiene CSS/HTML personalizado en una ubicación predefinida.

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

La carpeta META-INF contiene el archivo MANIFEST.MF requerido por OSGi para identificarlo como un paquete. Aparece de la siguiente manera:

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

El portlet exige que el HTML/CSS/images esté dentro de la carpeta /com/day/cq/portlet/toolbar/layout y no se puede cambiar. En las mismas líneas, los encabezados Import-Package y Export-Package de MANIFEST.MF también deben llamarse /com/day/cq/portlet/toolbar/layout. Bundle-SymbolicName debe ser un nombre de paquete único y completo.

Puede crearlo con una herramienta como maven o crear manualmente un archivo jar de este tipo con el encabezado correspondiente establecido como se muestra en esta sección.

#### Vistas de la barra de herramientas del portlet {#portlet-toolbar-views}

La barra de herramientas del portlet básicamente tiene dos estados de vista. Cada vista y los botones asociados se pueden personalizar con un archivo de HTML correspondiente.

#### Vista de publicación {#publish-view}

La vista de publicación solo tiene un botón que cambia la barra de herramientas a la vista Administrar. La vista de publicación se representa mediante el archivo publish.html en [paquete anterior](/help/sites-deploying/configuring-osgi.md#bundles). En el HTML, puede utilizar los siguientes marcadores de posición, que se sustituyen por el portlet con el contenido respectivo cuando se procesan:

#### Publicar marcadores de posición de vista {#publish-view-placeholders}

| Cadena del marcador de posición | Descripción |
|---|---|
| {buttonManage} | El marcador de posición se sustituye por **Administrar** , que cambia el estado del portlet al estado de administración. |

#### Administrar vista {#manage-view}

La vista Administrar tiene cuatro botones: Editar, ficha Sitios web, Actualizar y Atrás. La vista de administración se representa mediante el archivo manage.html en el [paquete anterior](/help/sites-deploying/configuring-osgi.md#bundles). En el HTML, puede utilizar los siguientes marcadores de posición, que se sustituyen por el portlet con el contenido respectivo cuando se procesan:

#### Administrar marcadores de posición de vista {#manage-view-placeholders}

| Cadena del marcador de posición | Descripción |
|---|---|
| {buttonEdit} | El marcador de posición se sustituye por **Editar** , que abre una nueva ventana con la página actual en AEM modo de edición. |
| {ficha buttonWebsites} | Marcador de posición, reemplazado por un botón que abre la pestaña Sitios web de AEM WCM. |
| {buttonRefresh} | Actualiza la vista actual. |
| {buttonBack} | Vuelve a colocar el portlet en la vista de publicación. |

#### Botones {#buttons}

Los botones, cualquiera que sea la vista que aparezcan, utilizan el mismo HTML común, definido en button.html.

En el HTML, puede utilizar los siguientes marcadores de posición, que se sustituyen por el portlet con el contenido respectivo cuando se procesan:

#### Botones Administrar y Publicar vista {#manage-and-publish-view-buttons}

| Cadena del marcador de posición | Descripción |
|---|---|
| {name} | Nombre del botón, por ejemplo, autor**, atrás, actualizar**, etc. |
| {id} | ID de CSS del botón. |
| {url} | URL del destino del botón. |
| {text} | Etiqueta del botón . |
| {onclick} | Javascript **onclick** (contiene {url}). |

Ejemplo de archivo button.html:

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### Instalación de un diseño personalizado {#installing-a-custom-layout}

Para instalar un diseño personalizado, acceda a la sección de la consola web OSGI del portlet **Paquetes **y cargue el paquete.

#### Paquetes {#packages}

Si necesita cargar o crear paquetes para su instalación, consulte el Administrador de paquetes en la documentación de AEM para obtener instrucciones detalladas.

### Administración de vínculos {#link-handling}

Todos los vínculos se reescriben para que funcionen en el contexto del portal. De forma predeterminada, se utilizan vínculos con parámetros de renderización. El reescritura de HTML de Portal Director se puede configurar para que utilice vínculos de acción en su lugar.

También puede definir parámetros de solicitud adicionales que desea consultar para que se muestre la ruta de contenido. Esto resulta útil, por ejemplo, si hay un vínculo desde el exterior a contenido específico.

Además, el reescritura de HTML de Portal Director se puede configurar con una lista de expresiones regulares definidas exclusiones para la reescritura de vínculos. Por ejemplo, si tiene vínculos relativos a sistemas externos, debe agregarlos a esta lista de exclusión.

### Localización {#localization}

El AEM portlet de contenido tiene una función de localización integrada, que garantiza que el contenido de AEM esté en el idioma correcto.

Esto se realiza en dos pasos:

1. El detector de configuración regional de Portal Directory detecta la configuración regional del usuario del portal obteniendo la configuración regional del portal. Este servicio debe configurarse con la lista de idiomas disponibles en AEM.
1. El controlador de configuración regional de Portal Director gestiona la localización de la solicitud actual. Toma la ruta del contenido solicitado, por ejemplo `/content/geometrixx/en/company.html`y según la configuración, reescribe el **en** con la configuración regional real del usuario.

El controlador de configuración regional de Portal Director se puede configurar con las rutas para comprobar la información de la configuración regional; normalmente esto incluye todo lo que se encuentra debajo `/content` y con la posición de la información de configuración regional en la ruta. De forma predeterminada, el controlador de configuración regional sigue la recomendación de estructurar sitios en varios idiomas dentro de AEM.

Si el sitio no tiene una regla estricta para administrar la información de configuración regional dentro de la ruta, es posible reemplazar el controlador de configuración regional con su propia implementación.

### Servicios opcionales de OSGi {#optional-osgi-services}

Se pueden implementar servicios OSGi opcionales para personalizar varias partes del portlet. Cada servicio corresponde a una interfaz de Java. Esta interfaz se puede implementar e implementar mediante un paquete en el portlet.

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>El rastreador de solicitudes recibe una notificación cada vez que el portlet muestra contenido. Esto le permite realizar un seguimiento de las invocaciones del portlet.</td>
  </tr>
  <tr>
   <td>InvocationContextListener</td>
   <td>Receptor que se invoca al principio y al final de cada solicitud al portlet. El oyente puede utilizarse para cambiar o añadir información para la solicitud actual.<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>Controlador de errores personalizado para detectar errores durante la fase de procesamiento.</td>
  </tr>
  <tr>
   <td>HttpProcessor</td>
   <td>Este servicio se puede utilizar para agregar información a cada invocación http a AEM.</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>Agregue una acción propia al portlet : esta acción se puede invocar a través de un vínculo de acción del portlet.</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>Este servicio se puede utilizar para decorar el contenido del portlet.</td>
  </tr>
  <tr>
   <td>ResourceProvider</td>
   <td>Añada su propio proveedor de recursos para entregar algún recurso a través de un vínculo de recurso de portlet al cliente.</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>Permite anunciar archivos de HTML de proceso, CSS y Javascript.</td>
  </tr>
  <tr>
   <td>ToolbarButton</td>
   <td>Agregue su propio botón a la barra de herramientas.</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>Añada un servicio para aplicar una asignación o reescritura de url personalizada.</td>
  </tr>
  <tr>
   <td>UserInfoProvider</td>
   <td>Añada su propia información sobre el usuario. Este servicio se puede utilizar para obtener información del portal al portlet.</td>
  </tr>
 </tbody>
</table>

#### Reemplazar servicios predeterminados {#replacing-default-services}

Los siguientes servicios tienen una implementación predeterminada en el portlet de contenido (con una interfaz Java correspondiente). Para personalizar, un paquete que contenga la nueva implementación de servicio debe implementarse en la aplicación portlet.

Al implementar un servicio de este tipo, asegúrese de establecer la variable **service.ranking** propiedad del servicio a un valor positivo. La implementación predeterminada utiliza la clasificación** 0** y el portlet utiliza el servicio con la clasificación más alta.

| **Nombre** | **Descripción** | **Comportamiento predeterminado** |
|---|---|---|
| Autenticador | Proporciona la información de autenticación a AEM | Utiliza un usuario técnico configurable tanto para el autor como para la publicación. O SSO. |
| HTMLRewriter | Reescribe vínculos, imágenes, etc. | Reescribe AEM vínculos a vínculos de portal, se pueden ampliar con un UrlMapper y un TextMapper |
| HttpClientService | Gestiona todas las conexiones http | Implementación estándar |
| LocaleHandler | Gestiona la información de configuración regional | Reescribe un vínculo al contenido con respecto a la configuración regional. |
| LocaleDetector | Detecta la configuración regional del usuario. | Utiliza la configuración regional proporcionada por el portal. |
| PrivilegeManager | Comprueba los derechos de usuario | Comprueba el acceso a la instancia de autor si el usuario puede editar el contenido |
| ToolbarRenderer | Procesa la barra de herramientas | Añade una funcionalidad de barra de herramientas |

### Eventos de portlet {#portlet-events}

La API de portlet (JSR-286) especifica eventos de portlet. El portlet de contenido AEM tiene un puente integrado, distribuyendo eventos portlet para el portlet AEM como eventos OSGi - esto hace que el manejo de eventos portlet sea conectable.

Si desea gestionar eventos específicos, declare que reciben eventos en el descriptor de implementación (o configúrelos a través del servidor de portal) e implemente un servicio OSGi declarando la interfaz EventHandler (consulte la especificación OSGi EventAdmin ).

Siempre que se produce un evento de portlet, se envía un evento de OSGi específico invocando al controlador. El controlador obtiene toda la información de contexto y puede actualizar el estado del portlet en consecuencia o enviar nuevos eventos. Básicamente, dentro del método de manejo se puede usar toda la funcionalidad de la fase del evento portlet.

## Uso de AEM como portal {#using-aem-as-a-portal}

Utilice el componente Portlet para agregar ventanas de portlet a páginas AEM. Las bibliotecas compartidas que instale en el servidor de aplicaciones permiten que el componente Portlet detecte las aplicaciones portlet implementadas.

Para utilizar AEM como portal, realice las siguientes tareas:

1. Instale el componente Portlet y las bibliotecas compartidas.
1. Agregue el componente Portlet a la barra de tareas.
1. Configure e implemente la aplicación web que contiene los portlets que desea que aparezcan en el componente Portal.
1. Agregue el componente Portlet a una página y seleccione el portlet que desee mostrar.

>[!NOTE]
>
>Solo puede utilizar el componente portlet cuando AEM implemente como una aplicación web. ([Consulte Instalación de AEM con un servidor de aplicaciones](/help/sites-deploying/application-server-install.md).)

### Instalación del componente portlet {#installing-the-portlet-component}

El archivo JAR de inicio rápido AEM contiene los archivos de componentes portlet. Para obtener los archivos (cq-portlet-components.zip), puede ejecutar Quickstart o extraer el contenido.

1. Ejecute o extraiga el contenido del archivo JAR de inicio rápido y busque el archivo cq-portlet-components.zip correspondiente:

   * Ejecutar inicio rápido: crx-quickstart/opt/portal
   * Extraer contenido de inicio rápido: static/opt/portal

1. Abra el Administrador de paquetes de la instancia de autor de CQ5 que se implementa en el servidor de aplicaciones. (https://)*appserverhost*:*puerto*/cq5author/crx/packmgr)

1. Utilice el Administrador de paquetes para [Cargar e instalar](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) el paquete cq-portlets-components.zip.

   El paquete instala el cq-portlet-director-sharedlibs-x.x.x.jar en la carpeta /libs/portal/director del repositorio.

1. Copie cq-portlet-director-sharedlibs-x.x.x.jar en su disco duro. Utilice cualquier medio para obtener el archivo, por ejemplo, FileVault o un cliente WebDAV.
1. Mueva el archivo cq-portlet-director-sharedlibs.x.x.x.jar a la carpeta de biblioteca compartida de su servidor de aplicaciones para que las clases estén disponibles para las aplicaciones de portlet implementadas.

### Adición del componente Portlet a la barra de tareas {#adding-the-portlet-component-to-sidekick}

Agregue el componente portlet al sistema de párrafos para que esté disponible para los autores.

1. En la barra de tareas, haga clic en el icono de regla para entrar en el modo Diseño.
1. Junto a la `Design of par` Encima del primer párrafo, haga clic en **Editar**.

1. En el **General** categoría de componentes, active la casilla de verificación situada junto al componente Portlet y haga clic en Aceptar.

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### Configuración e implementación de las aplicaciones de portlet {#configuring-and-deploying-your-portlet-applications}

Implemente los portlets en el contenedor web del servidor de aplicaciones para que estén disponibles para el componente Portal. Antes de implementar la aplicación de portlet, debe configurar la aplicación para que cargue el servlet AEM contenedor de portal. Esta configuración permite que el componente Portlet acceda a los portlets.

1. Extraiga el contenido del archivo WAR de la aplicación portlet.

   **Sugerencia:** El jar xf *nameofapp*.war extrae los archivos.

1. Abra el archivo web.xml en un editor de texto.
1. Añada la siguiente configuración de servlet dentro del elemento web-app:

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

   **Sugerencia:** La variable `jar cvf nameofapp.war *` agrega contenido del directorio actual al archivo nameofapp.war.

1. Implemente la aplicación portlet en el servidor de aplicaciones. Para obtener más información, consulte la documentación del servidor de aplicaciones.

### Adición de portlets a la página AEM {#adding-portlets-to-your-aem-page}

Utilice el componente Portal para añadir una ventana de portlet a la página web. Utilice las propiedades del componente para especificar el portlet que se va a mostrar.

1. En la página web, arrastre el **Portlet** del grupo General en la barra de tareas a la página.

   >[!NOTE]
   >
   >Después de arrastrar el componente a la página, vuelva a cargar la página para asegurarse de que funciona correctamente.

1. Haga doble clic en el componente para abrir las propiedades de Portlet.
1. En el **Entidad Portlet** menú desplegable, seleccione el portlet en la lista.
1. Seleccione o desactive la casilla de verificación **Ocultar barra de título **en función de si desea ver la barra de título del portlet.
1. En el **Ventana Portlet** , introduzca un ID de ventana de Portlet único, si lo desea.

   >[!NOTE]
   >
   >Si planea usar el mismo portlet más de una vez en la misma página, asigne a cada portlet un ID de ventana diferente.

1. Haga clic en **Aceptar**. El portlet se muestra en la página AEM.

   ![chlimage_1-136](assets/chlimage_1-136.png)

## Instalación, configuración y uso de AEM en un Portlet {#installing-configuring-and-using-aem-in-a-portlet}

Para acceder al contenido proporcionado por AEM WCM, el servidor de portal debe estar equipado con el Portlet Director Portal de AEM. Para ello, instale, configure y agregue el portlet a la página del portal siguiendo los pasos que se proporcionan en esta sección.

De forma predeterminada, el portlet se conecta a la instancia de publicación en localhost:4503 y a la instancia de autor en localhost:4502. Estos valores se pueden cambiar durante la implementación del portlet. El director del portal está disponible como contenido en el repositorio en /libs/portal/directory. Deberá descargar el archivo de guerra de la aplicación antes de utilizarlo.

### Descarga del archivo war {#downloading-the-war-file}

1. Mediante Webdav o CRXDE Lite, vaya a /libs/portal/director.

1. Descargar *cq-portlet-webapp.war*.

>[!NOTE]
>
>Estos procedimientos utilizan el portal de Websphere como ejemplo, aunque son lo más genéricos posible; tenga en cuenta que los procedimientos varían para otros portales web. Aunque los pasos son esencialmente idénticos para todos los portales web, debe reutilizar los pasos para su portal web en particular.

#### Instalación del portlet {#installing-the-portlet}

Para instalar el portlet:

1. Inicie sesión en el portal con privilegios de administrador.
1. Vaya a la parte Administración de Portlets de su portal web.
1. Haga clic en Instalar y busque la aplicación AEM portlet (cq-portlet-webapp.war) que descargó e introduzca otra información importante sobre el portlet.

   Para otra información esencial del portlet, puede aceptar los valores predeterminados o cambiar los valores. Si acepta los valores predeterminados, el portlet está disponible en https://&lt;wps-host>:&lt;port>/wps/PA_CQ5_Portlet. La consola de administración OSGi proporcionada por el portlet está disponible en https://&lt;wps-host>:&lt;port>/wps/ PA_CQ5_Portlet/cqbridge/system/console (el nombre de usuario/contraseña predeterminado es admin/admin).

1. Asegúrese de que la aplicación de portlet se inicie automáticamente seleccionando esa opción o casilla de verificación y guardando los cambios. Verá un mensaje que indica que la instalación se realizó correctamente.

#### Configuración del Portlet {#configuring-the-portlet}

Después de instalar el portlet, debe configurarlo para que conozca las URL de las instancias de AEM subyacentes (autor y publicación). También puede configurar otras opciones.

Para configurar el portlet:

1. En la ventana Administración de portal del servidor de aplicaciones, vaya a administración de portlets, donde se muestran todos los portlets y seleccione el portlet AEM Portal Director.
1. Configure el portlet según sea necesario. Por ejemplo, es posible que tenga que cambiar la dirección URL de las instancias de autor y publicación y la dirección URL de la ruta de inicio. Las configuraciones predeterminadas se describen en [Preferencias de Portlet](/help/sites-administering/aem-as-portal.md#portlet-preferences).

   >[!NOTE]
   >
   >Si el portlet está configurado para conectarse a AEM instancias de autor y publicación que se ejecutan en una ruta de contexto diferente a** /**, debe habilitar la fuerza **CQUrlInfo** en la configuración de Html Library Manager de estas instancias de AEM (por ejemplo, a través de Felix Webconsole) o la edición no funcionará y el cuadro de diálogo de preferencias no aparecerá.

1. Guarde los cambios de configuración en el servidor de aplicaciones.

1. Vaya a la consola de administración OSGI para el portlet. La ubicación predeterminada es `https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr`. El nombre de usuario/contraseña predeterminado es **admin/admin**.

1. Seleccione el **Configuración del servidor Day Portal Director CQ Server** y edite los siguientes valores:

   * **URL de base del autor**: Dirección URL base de la instancia de autor de AEM.
   * **URL de base de publicación**: Dirección URL base de la instancia de publicación de AEM.
   * **El Autor Se Utiliza Como Publicación**: ¿Se utiliza la instancia de autor como instancia de publicación (para desarrollo)?

   ![chlimage_1-137](assets/chlimage_1-137.png)

1. Haga clic en **Guardar**. Ahora puede agregar el portlet a las páginas de portal y usar el portal.

### URL de contenido {#content-urls}

Cuando se solicita contenido a AEM, el portlet utiliza el modo de visualización actual (publicación o autor) y la ruta actual para ensamblar una dirección URL completa. Con los valores predeterminados, la primera url es `https://localhost:4503/content/geometrixx/en.portlet.html`. El valor de la variable `htmlSelector` se añade automáticamente a la dirección URL antes de la extensión.

Si el portlet cambia al modo de ayuda y a la función `appendHelpViewModeAsSelector` se selecciona y, a continuación, la variable `help` también se adjunta, por ejemplo, `https://localhost:4503/content/geometrixx/en.portlet.html.help`. Si la ventana del portlet está maximizada y la variable `appendMaxWindowStateAsSelector` está seleccionado, el selector también se anexa, por ejemplo, `https://localhost:4503/content/geometrixx/en.portlet.max.help`.

Los selectores se pueden evaluar en AEM y se puede utilizar una plantilla diferente para diferentes selectores.

### Uso de un mapa de URL de contenido en AEM {#using-a-content-url-map-in-aem}

Normalmente, la ruta de inicio apunta directamente al contenido de AEM. Sin embargo, si desea mantener las rutas de inicio en AEM en lugar de en las preferencias del portlet, puede señalar la ruta de inicio a un mapa de contenido en AEM, como `/var/portlets`. En este caso, una secuencia de comandos que se ejecute en AEM puede utilizar la información enviada desde el portlet para decidir qué dirección URL es la dirección URL de inicio. Debe emitir un redireccionamiento a la dirección URL correcta.

#### Adición del Portlet a la Página del Portal {#adding-the-portlet-to-the-portal-page}

Para agregar el portlet a la página del portal:

1. Asegúrese de que está en la ventana de administración del servidor de aplicaciones y vaya a la ubicación donde administra las páginas. (por ejemplo, en WebSphere 6.1, haga clic en **Administrar páginas**).
1. Seleccione el nombre del portlet y, a continuación, seleccione una página existente o cree una nueva página.
1. Edite el diseño de la página.
1. Seleccione el portlet y agréguelo a un contenedor.
1. Guarde los cambios.

#### Uso del Portlet {#using-the-portlet}

Para acceder a la página que agregó al portlet:

1. En el menú de personalización del portlet, configure el portlet tal como lo configuró en el portal.
1. Abra la configuración (el portlet muestra la URL de inicio de publicación configurada en la configuración del portlet), realice las modificaciones necesarias y, a continuación, guárdelas.
