---
title: Cómo endurecer el AEM Forms en el Entorno JEE
seo-title: Cómo endurecer el AEM Forms en el Entorno JEE
description: Obtenga información sobre una variedad de opciones de seguridad reforzada para mejorar la seguridad de AEM Forms en JEE que se ejecuta en una intranet corporativa.
seo-description: Obtenga información sobre una variedad de opciones de seguridad reforzada para mejorar la seguridad de AEM Forms en JEE que se ejecuta en una intranet corporativa.
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '7698'
ht-degree: 0%

---


# Cómo endurecer su AEM Forms en el Entorno JEE {#hardening-your-aem-forms-on-jee-environment}

Obtenga información sobre una variedad de opciones de seguridad reforzada para mejorar la seguridad de AEM Forms en JEE que se ejecuta en una intranet corporativa.

El artículo describe recomendaciones y prácticas recomendadas para proteger servidores que ejecutan AEM Forms en JEE. No se trata de un documento completo de refuerzo del host para el sistema operativo y los servidores de aplicaciones. En su lugar, este artículo describe una serie de opciones de seguridad que debe implementar para mejorar la seguridad de AEM Forms en JEE que se ejecuta en una intranet corporativa. Sin embargo, para garantizar que AEM Forms permanezca seguro en los servidores de aplicaciones JEE, también debe implementar procedimientos de supervisión, detección y respuesta de seguridad.

El artículo describe técnicas de endurecimiento que deben aplicarse durante las siguientes etapas durante el ciclo de vida de la instalación y configuración:

* **Preinstalación:** utilice estas técnicas antes de instalar AEM Forms en JEE.
* **Instalación:** utilice estas técnicas durante el proceso de instalación de AEM Forms en JEE.
* **Después de la instalación:** utilice estas técnicas después de la instalación y periódicamente a partir de entonces.

AEM Forms en JEE es altamente personalizable y puede funcionar en muchos entornos diferentes. Es posible que algunas de las recomendaciones no se ajusten a las necesidades de su organización.

## Preinstalación {#preinstallation}

Antes de instalar AEM Forms en JEE, puede aplicar soluciones de seguridad a la capa de red y al sistema operativo. Esta sección describe algunos problemas y hace recomendaciones para reducir las vulnerabilidades de seguridad en estas áreas.

**Instalación y configuración en UNIX y Linux**

No debe instalar ni configurar AEM Forms en JEE con un shell raíz. De forma predeterminada, los archivos se instalan en el directorio /opt y el usuario que realiza la instalación necesita todos los permisos de archivo en /opt. Como alternativa, se puede realizar una instalación en el directorio /user de un usuario individual, donde ya tienen todos los permisos de archivo.

**Instalación y configuración en Windows**

Debe realizar la instalación en Windows como administrador si va a instalar AEM Forms en JEE en JBoss mediante el método llave en mano o si va a instalar PDF Generator. Además, al instalar PDF Generator en Windows con compatibilidad con aplicaciones nativas, debe ejecutar la instalación como el mismo usuario de Windows que instaló Microsoft Office. Para obtener más información sobre los privilegios de instalación, consulte el documento* Instalación e implementación de AEM Forms en JEE* para su servidor de aplicaciones.

### Seguridad de capa de red {#network-layer-security}

Las vulnerabilidades de seguridad de red están entre las primeras amenazas para cualquier servidor de aplicaciones orientado a Internet o a intranet. Esta sección describe el proceso de endurecimiento de los hosts de la red contra estas vulnerabilidades. Se ocupa de la segmentación de red, el endurecimiento de la pila del Protocolo de control de transmisión/Protocolo de Internet (TCP/IP) y el uso de firewalls para la protección del host.

La siguiente tabla describe los procesos comunes que reducen las vulnerabilidades de seguridad de red.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descripción</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Zonas desmilitarizadas (DMZ)</p> </td> 
   <td><p>Implementar servidores de formularios dentro de una zona desmilitarizada (DMZ). La segmentación debe existir en al menos dos niveles con el servidor de aplicaciones utilizado para ejecutar AEM Forms en JEE ubicado detrás del servidor de seguridad interior. Separe la red externa de la DMZ que contiene los servidores Web, que a su vez deben separarse de la red interna. Utilice los cortafuegos para implementar las capas de separación. Clasifique y controle el tráfico que pasa por cada capa de red para asegurarse de que sólo se permite el mínimo absoluto de datos requeridos.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Direcciones IP privadas</p> </td> 
   <td><p>Utilice Traducción de direcciones de red (NAT) con direcciones IP privadas RFC 1918 en el servidor de aplicaciones de AEM Forms. Asigne direcciones IP privadas (10.0.0.0/8, 172.16.0.0/12 y 192.168.0.0/16) para que sea más difícil para un atacante enrutar el tráfico hacia y desde un host interno NAT a través de Internet.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Servidores de seguridad</p> </td> 
   <td><p>Utilice los siguientes criterios para seleccionar una solución de firewall:</p> 
    <ul> 
     <li><p>Implemente servidores de seguridad que admitan servidores proxy o <em>inspección con estado</em> en lugar de soluciones sencillas de filtrado de paquetes.</p> </li> 
     <li><p>Utilice un servidor de seguridad que admita un <em>denegar todos los servicios excepto aquellos paradigmas de seguridad permitidos de forma explícita</em>.</p> </li> 
     <li><p>Implemente una solución de cortafuegos que tenga dos o más hosts. Esta arquitectura proporciona el nivel bueno de seguridad y ayuda a evitar que usuarios no autorizados pasen por alto la seguridad del cortafuegos.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Puertos de base de datos</p> </td> 
   <td><p>No utilice puertos de escucha predeterminados para bases de datos (MySQL - 3306, Oracle - 1521, MS SQL - 1433). Para obtener información sobre cómo cambiar los puertos de base de datos, consulte la documentación de la base de datos.</p> <p>El uso de un puerto de base de datos diferente afecta a la configuración general de AEM Forms en JEE. Si cambia los puertos predeterminados, debe realizar las modificaciones correspondientes en otras áreas de configuración, como las fuentes de datos de AEM Forms en JEE.</p> <p>Para obtener información sobre la configuración de orígenes de datos en AEM Forms en JEE, consulte Instalar y actualizar AEM Forms en JEE o Actualizar a AEM Forms en JEE para su servidor de aplicaciones en <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">Guía del usuario de AEM Forms</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Seguridad del sistema operativo {#operating-system-security}

En la siguiente tabla se describen algunos enfoques posibles para minimizar las vulnerabilidades de seguridad que se encuentran en el sistema operativo.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p></th> 
   <th><p>Descripción</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Revisiones de seguridad</p></td> 
   <td><p>Existe un mayor riesgo de que un usuario no autorizado obtenga acceso al servidor de aplicaciones si no se aplican oportunamente los parches y las actualizaciones de seguridad del proveedor. Pruebe los parches de seguridad antes de aplicarlos a los servidores de producción.</p><p>Además, cree políticas y procedimientos para buscar e instalar parches de forma regular.</p></td> 
  </tr> 
  <tr> 
   <td><p>Software de protección antivirus</p></td> 
   <td><p>Los analizadores de virus pueden identificar los archivos infectados buscando una firma o buscando comportamientos inusuales. Los escáneres guardan sus firmas de virus en un archivo, que generalmente se almacena en el disco duro local. Debido a que con frecuencia se descubren nuevos virus, debe actualizar este archivo para que el analizador de virus identifique todos los virus actuales.</p></td> 
  </tr> 
  <tr> 
   <td><p>Protocolo de tiempo de red (NTP)</p></td> 
   <td><p>Para la análisis forense, mantenga un tiempo preciso en los servidores de formularios. Utilice NTP para sincronizar la hora en todos los sistemas conectados directamente a Internet.</p></td> 
  </tr> 
 </tbody> 
</table>

Para obtener más información sobre la seguridad de su sistema operativo, consulte [&quot;Información de seguridad del sistema operativo&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## Instalación {#installation}

En esta sección se describen las técnicas que puede utilizar durante el proceso de instalación de AEM Forms para reducir las vulnerabilidades de seguridad. En algunos casos, estas técnicas utilizan opciones que forman parte del proceso de instalación. En la tabla siguiente se describen estas técnicas.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descripción</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Privilegios</p> </td> 
   <td><p>Utilice el menor número de privilegios necesarios para instalar el software. Inicie sesión en el equipo con una cuenta que no esté en el grupo Administradores. En Windows, puede utilizar el comando Ejecutar como para ejecutar el programa de instalación de AEM Forms en JEE como usuario administrativo. En sistemas UNIX y Linux, utilice un comando como <code>sudo</code> para instalar el software.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Fuente de software</p> </td> 
   <td><p>No descargue ni ejecute AEM Forms en JEE desde fuentes no confiables.</p> <p>Los programas maliciosos pueden contener código que viola la seguridad de varias maneras, incluyendo robo, modificación y eliminación de datos, y denegación de servicio. Instale AEM Forms en JEE desde el DVD del Adobe o solo desde una fuente de confianza.</p> </td> 
  </tr> 
  <tr> 
   <td><p>particiones de disco</p> </td> 
   <td><p>Coloque AEM Forms en JEE en una partición de disco dedicada. La segmentación de discos es un proceso que mantiene datos específicos en el servidor en discos físicos separados para mayor seguridad. La organización de los datos de esta manera reduce el riesgo de ataques de inversión de directorios. Planee crear una partición separada de la partición del sistema en la que puede instalar el AEM Forms en el directorio de contenido JEE. (En Windows, la partición del sistema contiene el directorio system32 o la partición de inicio).</p> </td> 
  </tr> 
  <tr> 
   <td><p>Componentes</p> </td> 
   <td><p>Evalúe los servicios existentes y deshabilite o desinstale los que no sean necesarios. No instale componentes y servicios innecesarios.</p> <p>La instalación predeterminada de un servidor de aplicaciones puede incluir servicios que no son necesarios para su uso. Debe deshabilitar todos los servicios innecesarios antes de la implementación para minimizar los puntos de entrada para un ataque. Por ejemplo, en JBoss, puede comentar servicios innecesarios en el archivo descriptor META-INF/jboss-service.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Archivo de política entre dominios</p> </td> 
   <td><p>La presencia de un archivo <code>crossdomain.xml</code> en el servidor puede debilitar ese servidor inmediatamente. Se recomienda que la lista de dominios sea lo más restrictiva posible. No coloque el archivo <code>crossdomain.xml</code> que se utilizó durante el desarrollo en producción al utilizar Guías <em>(desaprobada)</em>. Para una guía que utiliza servicios Web, si el servicio está en el mismo servidor que proporcionó la guía, no se necesita un archivo <code>crossdomain.xml</code>. Pero si el servicio está en otro servidor, o si hay clústeres involucrados, se necesitaría la presencia de un archivo <code>crossdomain.xml</code>. Consulte <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a> para obtener más información sobre el archivo cross-domain.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Configuración de seguridad del sistema operativo</p> </td> 
   <td><p>Si necesita utilizar codificación XML de 192 o 256 bits en plataformas Solaris, asegúrese de instalar <code>pkcs11_softtoken_extra.so</code> en lugar de <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Pasos posteriores a la instalación {#post-installation-steps}

Después de instalar correctamente AEM Forms en JEE, es importante mantener periódicamente el entorno desde una perspectiva de seguridad.

En la siguiente sección se describen en detalle las diferentes tareas recomendadas para proteger el servidor de formularios implementado.

### Seguridad de AEM Forms {#aem-forms-security}

La siguiente configuración recomendada se aplica a AEM Forms en el servidor JEE fuera de la aplicación Web administrativa. Para reducir los riesgos de seguridad para el servidor, aplique esta configuración inmediatamente después de instalar AEM Forms en JEE.

**Revisiones de seguridad**

Existe un mayor riesgo de que un usuario no autorizado obtenga acceso al servidor de aplicaciones si no se aplican oportunamente los parches y las actualizaciones de seguridad del proveedor. Pruebe los parches de seguridad antes de aplicarlos a los servidores de producción para garantizar la compatibilidad y disponibilidad de las aplicaciones. Además, cree políticas y procedimientos para buscar e instalar parches de forma regular. Las actualizaciones de AEM Forms en JEE se encuentran en el sitio de descarga de productos de Enterprise.

**Cuentas de servicio (llave en mano de JBoss solo en Windows)**

AEM Forms en JEE instala un servicio de forma predeterminada mediante la cuenta LocalSystem. La cuenta de usuario integrada de LocalSystem tiene un alto nivel de accesibilidad; forma parte del grupo Administradores. Si una identidad de proceso de trabajo se ejecuta como la cuenta de usuario de LocalSystem, ese proceso de trabajo tiene acceso completo a todo el sistema.

Para ejecutar el servidor de aplicaciones en el que se implementa AEM Forms en JEE, mediante una cuenta específica no administrativa, siga estas instrucciones:

1. En Microsoft Management Console (MMC), cree un usuario local para que el servicio del servidor de formularios inicie sesión como:

   * Seleccione **El usuario no puede cambiar la contraseña**.
   * En la ficha **Miembro de**, asegúrese de que aparece el grupo **Usuarios**.

   >[!NOTE]
   >
   >No puede cambiar esta configuración para el generador de PDF.

1. Seleccione **Inicio** > **Configuración** > **Herramientas administrativas** > **Servicios**.
1. Haga clic con el doble en JBoss para AEM Forms en JEE y detenga el servicio.
1. En la ficha **Iniciar sesión**, seleccione **Esta cuenta**, busque la cuenta de usuario que ha creado e introduzca la contraseña para la cuenta.
1. En MMC, abra **Configuración de seguridad local** y seleccione **Directivas locales** > **Asignación de derechos de usuario**.
1. Asigne los siguientes derechos a la cuenta de usuario en la que se ejecuta el servidor de formularios:

   * Denegar el inicio de sesión a través de Servicios de Terminal Server
   * Denegar inicio de sesión localmente
   * Iniciar sesión como servicio (debe estar ya establecido)

1. Asigne a la nueva cuenta de usuario permisos de modificación en los directorios siguientes:
   * **Directorio** de Almacenamiento de Documento global (GDS): La ubicación del directorio GDS se configura manualmente durante el proceso de instalación de AEM Forms. Si la configuración de ubicación permanece vacía durante la instalación, la ubicación predeterminada es un directorio bajo la instalación del servidor de aplicaciones en `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Directorio** CRX-Repository: La ubicación predeterminada es  `[AEM-Forms-installation-location]\crx-repository`
   * **Directorios** temporales de AEM Forms:
      * (Windows) Ruta TMP o TEMP según se establece en las variables de entorno
      * (AIX, Linux o Solaris) Directorio de inicio del usuario con inicio de sesión
En sistemas basados en UNIX, un usuario no raíz puede utilizar el siguiente directorio como directorio temporal:
      * (Linux) /var/tmp o /usr/tmp
      * (AIX) /tmp o /usr/tmp
      * (Solaris) /var/tmp o /usr/tmp
1. Otorgue a la nueva cuenta de usuario permisos de escritura en los directorios siguientes:
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > Ubicación de instalación predeterminada del servidor de aplicaciones JBoss:
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jleader/

1. Inicio del servidor de aplicaciones.

**Desactivación del servlet de arranque de Configuration Manager**

Configuration Manager utilizó un servlet implementado en el servidor de aplicaciones para realizar el arranque de AEM Forms en la base de datos JEE. Dado que Configuration Manager accede a este servlet antes de que se complete la configuración, el acceso a él no se ha asegurado para los usuarios autorizados y debe deshabilitarse después de haber utilizado correctamente Configuration Manager para configurar AEM Forms en JEE.

1. Descomprima el archivo adobe-livecycle-[appserver].ear.
1. Abra el archivo META-INF/application.xml.
1. Busque la sección adobe-bootstrapper.war:

   ```java
   <!-- bootstrapper start --> 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   <!-- bootstrapper end-->
   ```

1. Detenga el servidor de AEM Forms.
1. Comente adobe-bootstrapper.war y adobe-lcm-bootstrapper-redirectory. módulos de guerra como se indica a continuación:

   ```java
   <!-- bootstrapper start --> 
   <!-- 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   --> 
   <!-- bootstrapper end-->
   ```

1. Guarde y cierre el archivo META-INF/application.xml.
1. Copie el archivo EAR y vuelva a implementarlo en el servidor de aplicaciones.
1. Inicio del servidor AEM Forms.
1. Escriba la dirección URL siguiente en un explorador para probar el cambio y asegurarse de que ya no funciona.

   https://&lt;localhost>:&lt;puerto>/adobe-bootstrapper/bootstrap

**Bloqueo del acceso remoto al almacén de confianza**

Configuration Manager permite cargar una credencial de extensiones de Acrobat Reader DC en el AEM Forms en el almacén de confianza JEE. Esto significa que el acceso al servicio de credenciales del almacén de confianza a través de protocolos remotos (SOAP y EJB) se ha habilitado de forma predeterminada. Este acceso ya no es necesario después de haber cargado las credenciales de derechos mediante Configuration Manager o si decide utilizar la Consola de administración más adelante para administrar las credenciales.

Puede deshabilitar el acceso remoto a todos los servicios del almacén de confianza siguiendo los pasos de la sección [Deshabilitar el acceso remoto no esencial a los servicios](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**Deshabilitar todos los accesos anónimos no esenciales**

Algunos servicios de servidor de formularios tienen operaciones que un llamador anónimo puede invocar. Si no se requiere acceso anónimo a estos servicios, desactívelo siguiendo los pasos de [Deshabilitación del acceso anónimo no esencial a los servicios](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### Cambiar la contraseña de administrador predeterminada {#change-the-default-administrator-password}

Cuando se instala AEM Forms en JEE, se configura una única cuenta de usuario predeterminada para el usuario Super Administrator/login-id Administrator con una contraseña predeterminada de *password*. Debe cambiar esta contraseña inmediatamente mediante Configuration Manager.

1. Escriba la siguiente dirección URL en un navegador web:

   ```java
   https://[host name]:[port]/adminui
   ```

   El número de puerto predeterminado es uno de estos:

   **JBoss:** 8080

   **WebLogic Server:** 7001

   **WebSphere:** 9080.

1. En el campo **Nombre de usuario**, escriba `administrator` y, en el campo **Contraseña**, escriba `password`.
1. Haga clic en **Configuración** > **Administración de usuarios** > **Usuarios y grupos**.
1. Escriba `administrator` en el campo **Buscar** y haga clic en **Buscar**.
1. Haga clic en **Superadministrador** desde la lista de usuarios.
1. Haga clic en **Cambiar contraseña** en la página Editar usuario.
1. Especifique la nueva contraseña y haga clic en **Guardar**.

Además, se recomienda cambiar la contraseña predeterminada del administrador de CRX siguiendo estos pasos:

1. Inicie sesión en `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` con el nombre de usuario/contraseña predeterminados.
1. Escriba Administrador en el campo de búsqueda y haga clic en **Ir**.
1. Seleccione **Administrador** en el resultado de la búsqueda y haga clic en el icono **Editar** en la parte inferior derecha de la interfaz de usuario.
1. Especifique la nueva contraseña en el campo **Nueva contraseña** y la contraseña antigua en el campo **Contraseña**.
1. Haga clic en el icono Guardar en la parte inferior derecha de la interfaz de usuario.

#### Deshabilitar generación WSDL {#disable-wsdl-generation}

La generación del lenguaje de definición de servicios Web (WSDL) solo debe habilitarse para entornos de desarrollo, donde los desarrolladores utilizan la generación WSDL para crear sus aplicaciones cliente. Puede desactivar la generación WSDL en un entorno de producción para evitar exponer los detalles internos de un servicio.

1. Escriba la siguiente dirección URL en un navegador web:

   ```java
   https://[host name]:[port]/adminui
   ```

1. Haga clic en **Configuración > Configuración del sistema principal > Configuraciones**.
1. Anule la selección de **Habilitar WSDL** y haga clic en **Aceptar**.

### Seguridad del servidor de aplicaciones {#application-server-security}

En la tabla siguiente se describen algunas técnicas para proteger el servidor de aplicaciones después de instalar AEM Forms en la aplicación JEE.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descripción</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Consola administrativa del servidor de aplicaciones</p> </td> 
   <td><p>Después de instalar, configurar e implementar AEM Forms en JEE en el servidor de aplicaciones, debe deshabilitar el acceso a las consolas administrativas del servidor de aplicaciones. Consulte la documentación del servidor de aplicaciones para obtener más información.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Configuración de cookies del servidor de aplicaciones</p> </td> 
   <td><p>El servidor de aplicaciones controla las cookies de la aplicación. Al implementar la aplicación, el administrador del servidor de aplicaciones puede especificar las preferencias de cookies en todo el servidor o en una aplicación específica. De forma predeterminada, la configuración del servidor tiene preferencia.</p> <p>Todas las cookies de sesión generadas por el servidor de aplicaciones deben incluir el atributo <code>HttpOnly</code>. Por ejemplo, al utilizar el servidor de aplicaciones JBoss, puede modificar el elemento SessionCookie a <code>httpOnly="true"</code> en el archivo <code>WEB-INF/web.xml</code>.</p> <p>Puede restringir el envío de cookies mediante HTTPS. Como resultado, no se envían sin cifrar a través de HTTP. Los administradores del servidor de aplicaciones deben habilitar las cookies seguras para el servidor de forma global. Por ejemplo, al utilizar el servidor de aplicaciones JBoss, puede modificar el elemento conector a <code>secure=true</code> en el archivo <code>server.xml</code>.</p> <p>Consulte la documentación del servidor de aplicaciones para obtener más detalles sobre la configuración de cookies.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Exploración de directorios</p> </td> 
   <td><p>Cuando alguien solicita una página que no existe o solicita el nombre de un director (la cadena de solicitud termina con una barra diagonal (/)), el servidor de aplicaciones no debe devolver el contenido de ese directorio. Para evitarlo, puede desactivar la exploración de directorios en el servidor de aplicaciones. Debe hacerlo para la aplicación de la consola de administración y para otras aplicaciones que se ejecuten en el servidor.</p> <p>Para JBoss, establezca el valor del parámetro de inicialización listings de la propiedad <code>DefaultServlet</code> en <code>false</code> en el archivo web.xml, como se muestra en este ejemplo:</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;predeterminado&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listas&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>Para WebSphere, establezca la propiedad <code>directoryBrowsingEnabled</code> en el archivo ibm-web-ext.xmi en <code>false</code>.</p> <p>Para WebLogic, establezca las propiedades de los directorios de índice del archivo weblogic.xml en <code>false</code>, como se muestra en este ejemplo:</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### Seguridad de la base de datos {#database-security}

Al proteger la base de datos, debe implementar las medidas descritas por el proveedor de la base de datos. Debe asignar un usuario de base de datos con los permisos mínimos requeridos de base de datos para su uso por AEM Forms en JEE. Por ejemplo, no utilice una cuenta con privilegios de administrador de base de datos.

En Oracle, la cuenta de la base de datos que utilice sólo necesita los privilegios de CONNECT, RECURSO y CREATE VISTA. Para conocer requisitos similares en otras bases de datos, consulte [Preparación de la instalación de AEM Forms en JEE (un solo servidor)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### Configuración de la seguridad integrada para SQL Server en Windows para JBoss {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. Modifique [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} para agregar `integratedSecurity=true` a la dirección URL de conexión, como se muestra en este ejemplo:

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. Añada el archivo sqljdbc_auth.dll a la ruta de acceso del sistema de Windows en el equipo que ejecuta el servidor de aplicaciones. El archivo sqljdbc_auth.dll se encuentra con la instalación del controlador JDBC 6.2.1.0 de Microsoft SQL.
1. Modifique la propiedad JBoss del servicio Windows (JBoss para AEM Forms en JEE) para Iniciar sesión desde el sistema local a una cuenta de inicio de sesión que tenga una base de datos AEM Forms y un conjunto mínimo de privilegios. Si ejecuta JBoss desde la línea de comandos en lugar de como un servicio de Windows, no es necesario que realice este paso.
1. Configure Seguridad para SQL Server del modo **Mixto** a **Autenticación de Windows solamente**.

#### Configuración de la seguridad integrada para SQL Server en Windows para WebLogic {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. Inicio de la Consola de administración de WebLogic Server escribiendo la siguiente URL en la línea URL de un explorador Web:

   ```java
   https://[host name]:7001/console
   ```

1. En Centro de cambios, haga clic en **Bloquear y editar**.
1. En Estructura de dominio, haga clic en *[dominio_base]* > **Servicios** > **JDBC** > **Fuentes de datos** y, en el panel derecho, haga clic en **IDP_DS**.
1. En la siguiente pantalla, en la ficha **Configuración**, haga clic en la ficha **Pool de conexiones** y, en el cuadro **Propiedades**, escriba `integratedSecurity=true`.
1. En Estructura de dominio, haga clic en **[dominio_base]** > **Servicios** > **JDBC** > **Fuentes de datos** y, en el panel derecho, haga clic en **RM_DS**.
1. En la siguiente pantalla, en la ficha **Configuración**, haga clic en la ficha **Pool de conexiones** y, en el cuadro **Propiedades**, escriba `integratedSecurity=true`.
1. Añada el archivo sqljdbc_auth.dll a la ruta de acceso del sistema de Windows en el equipo que ejecuta el servidor de aplicaciones. El archivo sqljdbc_auth.dll se encuentra con la instalación del controlador JDBC 6.2.1.0 de Microsoft SQL.
1. Configure Seguridad para SQL Server del modo **Mixto** a **Autenticación de Windows solamente**.

#### Configuración de la seguridad integrada para SQL Server en Windows para WebSphere {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

En WebSphere, puede configurar la seguridad integrada solo cuando utiliza un controlador JDBC de SQL Server externo, no el controlador JDBC de SQL Server incrustado en WebSphere.

1. Inicie sesión en la Consola administrativa de WebSphere.
1. En el árbol de navegación, haga clic en **Recursos** > **JDBC** > **Fuentes de datos** y, en el panel derecho, haga clic en **IDP_DS**.
1. En el panel derecho, en Propiedades adicionales, haga clic en **Propiedades personalizadas** y, a continuación, haga clic en **Nuevo**.
1. En el cuadro **Nombre**, escriba `integratedSecurity` y, en el cuadro **Valor**, escriba `true`.
1. En el árbol de navegación, haga clic en **Recursos** > **JDBC** > **Fuentes de datos** y, en el panel derecho, haga clic en **RM_DS**.
1. En el panel derecho, en Propiedades adicionales, haga clic en **Propiedades personalizadas** y, a continuación, haga clic en **Nuevo**.
1. En el cuadro **Nombre**, escriba `integratedSecurity` y, en el cuadro **Valor**, escriba `true`.
1. En el equipo en el que está instalado WebSphere, agregue el archivo sqljdbc_auth.dll a la ruta de acceso del sistema de Windows (C:\Windows). El archivo sqljdbc_auth.dll se encuentra en la misma ubicación que la instalación del controlador JDBC 1.2 de Microsoft SQL (el valor predeterminado es *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. Seleccione **Inicio** > **Panel de control de Campaign** > **Servicios**, haga clic con el botón derecho en el servicio de Windows para WebSphere (IBM WebSphere Application Server &lt;version> - &lt;node>) y seleccione **Propiedades**.
1. En el cuadro de diálogo Propiedades, haga clic en la ficha **Iniciar sesión**.
1. Seleccione **Esta cuenta** y proporcione la información necesaria para configurar la cuenta de inicio de sesión que desee utilizar.
1. Configure Seguridad en SQL Server del modo **Mixto** a **Autenticación de Windows solamente**.

### Protección del acceso al contenido confidencial en la base de datos {#protecting-access-to-sensitive-content-in-the-database}

El esquema de la base de datos de AEM Forms contiene información confidencial sobre la configuración del sistema y los procesos empresariales y debe ocultarse detrás del servidor de seguridad. La base de datos debe considerarse dentro del mismo límite de confianza que el servidor de formularios. Para evitar la divulgación de información y el robo de datos empresariales, el administrador de la base de datos (DBA) debe configurar la base de datos para permitir el acceso únicamente a los administradores autorizados.

Como precaución adicional, debe considerar el uso de herramientas específicas del proveedor de la base de datos para cifrar columnas en tablas que contengan los siguientes datos:

* Claves de Documento Rights Management
* Clave de cifrado del PIN de HSM de la tienda de confianza
* Hash de contraseña de usuario local

Para obtener información sobre las herramientas específicas del proveedor, consulte [&quot;Información de seguridad de la base de datos&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### Seguridad LDAP {#ldap-security}

Un directorio ligero de Protocolo de acceso a directorios (LDAP, Lightweight Directory Access Protocol ) es utilizado generalmente por AEM Forms en JEE como fuente de información de usuarios y grupos empresariales, y como medio para realizar la autenticación de contraseñas. Debe asegurarse de que el directorio LDAP está configurado para utilizar Secure Socket Layer (SSL) y de que AEM Forms en JEE está configurado para acceder al directorio LDAP mediante su puerto SSL.

#### Negación de servicio LDAP {#ldap-denial-of-service}

Un ataque común que utiliza LDAP implica que un atacante deliberadamente no puede autenticarse varias veces. Esto fuerza al servidor de directorio LDAP a bloquear a un usuario de todos los servicios dependientes de LDAP.

Puede establecer el número de intentos de error y el tiempo de bloqueo subsiguiente que AEM Forms implementa cuando un usuario falla repetidamente en autenticarse en AEM Forms. En la Consola de administración, elija valores bajos. Al seleccionar el número de intentos de error, es importante comprender que, una vez realizados todos los intentos, AEM Forms bloquea al usuario antes de que lo haga el servidor de directorio LDAP.

#### Establecer bloqueo automático de cuenta {#set-automatic-account-locking}

1. Inicie sesión en la Consola de administración.
1. Haga clic en **Configuración** > **Administración de usuarios** > **Administración de dominios**.
1. En Configuración automática de bloqueo de cuentas, establezca **Máximos errores de autenticación consecutiva** en un número bajo, como 3.
1. Haga clic en **Guardar**.

### Auditoría y registro {#auditing-and-logging}

El uso adecuado y seguro de la auditoría y el registro de aplicaciones puede ayudar a garantizar que la seguridad y otros eventos anómalos se rastreen y detecten lo antes posible. El uso efectivo de la auditoría y el registro dentro de una aplicación incluye elementos como el seguimiento de inicios de sesión exitosos y fallidos, así como eventos clave de la aplicación como la creación o eliminación de registros clave.

Puede utilizar la auditoría para detectar varios tipos de ataques, incluidos los siguientes:

* Ataques de contraseña de fuerza bruta
* Ataques de denegación de servicio
* Inyección de entradas hostiles y clases conexas de ataques de secuencias de comandos

En esta tabla se describen las técnicas de auditoría y registro que puede utilizar para reducir las vulnerabilidades del servidor.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descripción</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>ACL de archivos de registro</p> </td> 
   <td><p>Configure el AEM Forms adecuado en las listas de control de acceso de archivos de registro (ACL) de JEE.</p> <p>La configuración de las credenciales adecuadas ayuda a evitar que los atacantes eliminen los archivos.</p> <p>Los permisos de seguridad en el directorio de archivos de registro deben ser Control total para los grupos Administradores y SISTEMA. La cuenta de usuario de AEM Forms solo debe tener permisos de lectura y escritura.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Redundancia de archivos de registro</p> </td> 
   <td><p>Si los recursos lo permiten, envíe registros a otro servidor en tiempo real al que el atacante no pueda acceder (solo escritura) mediante Syslog, Tivoli, Microsoft Operations Manager (MOM) Server u otro mecanismo.</p> <p>Proteger los registros de esta manera ayuda a evitar alteraciones. Además, el almacenamiento de registros en un repositorio central ayuda en la correlación y supervisión (por ejemplo, si se utilizan varios servidores de formularios y se produce un ataque de adivinación de contraseña en varios equipos en los que se solicita una contraseña a cada equipo).</p> </td> 
  </tr> 
 </tbody> 
</table>

### Permitir que un usuario que no es administrador ejecute el generador de PDF

Puede habilitar a un usuario que no sea administrador para que utilice el generador de PDF. Normalmente, solo los usuarios con privilegios de administrador pueden utilizar el generador de PDF. Realice los siguientes pasos para permitir que un usuario que no es administrador ejecute el generador de PDF:

1. Cree un nombre de variable de entorno PDFG_NON_ADMIN_ENABLED.

1. Establezca el valor de la variable en VERDADERO.

1. Reinicie la instancia de AEM Forms.

## Configuración de AEM Forms en JEE para el acceso más allá de la empresa {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

Después de instalar correctamente AEM Forms en JEE, es importante mantener periódicamente la seguridad de su entorno. En esta sección se describen las tareas recomendadas para mantener la seguridad de su AEM Forms en el servidor de producción JEE.

### Configuración de un proxy inverso para acceso Web {#setting-up-a-reverse-proxy-for-web-access}

Se puede utilizar un *proxy inverso* para garantizar que un conjunto de direcciones URL para AEM Forms en aplicaciones web JEE esté disponible tanto para usuarios externos como internos. Esta configuración es más segura que permitir que los usuarios se conecten directamente al servidor de aplicaciones en el que se ejecuta AEM Forms en JEE. El proxy inverso realiza todas las solicitudes HTTP para el servidor de aplicaciones que ejecuta AEM Forms en JEE. Los usuarios solo tienen acceso de red al proxy inverso y solo pueden intentar conexiones URL admitidas por el proxy inverso.

**AEM Forms en direcciones URL raíz JEE para su uso con el servidor proxy inverso**

Las siguientes URL raíz de la aplicación para cada AEM Forms en la aplicación web JEE. Debe configurar el proxy inverso solo para exponer las direcciones URL a la funcionalidad de la aplicación web que desea proporcionar a los usuarios finales.

Determinadas direcciones URL se resaltan como aplicaciones web dirigidas al usuario final. Debe evitar la exposición de otras direcciones URL para Configuration Manager para el acceso a usuarios externos a través del proxy inverso.

<table> 
 <thead> 
  <tr> 
   <th><p>URL raíz</p> </th> 
   <th><p>Finalidad y/o aplicación web asociada</p> </th> 
   <th><p>Interfaz basada en la Web</p> </th> 
   <th><p>Acceso del usuario final</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Aplicación web de usuario final de extensiones de Acrobat Reader DC para aplicar derechos de uso a documentos PDF</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Aplicación web de usuario final Rights Management</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>URL de servicio Web para Rights Management</p> </td> 
   <td><p>No</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>Aplicación web de administración de PDF Generator</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/el espacio de trabajo/*</p> </td> 
   <td><p>Aplicación web de usuario final de Workspace</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/space-server/*</p> </td> 
   <td><p>Servlets y servicios de datos de Workspace que requiere la aplicación cliente de Workspace</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>Servlet para arrancar el repositorio de AEM Forms en JEE</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>Página de información para servicios Web del servidor de formularios</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>Dirección URL del servicio Web para todos los servicios del servidor de formularios</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Aplicación web de administración de Rights Management</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>Página de inicio de la Consola de administración</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>seguro/*</p> </td> 
   <td><p>Páginas de administración de Administración de almacén de confianza</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>Aplicación Forms IVS para probar y depurar la representación de formularios</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>Aplicación Output IVS para probar y depurar el servicio de salida</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>URL REST para Rights Management</p> </td> 
   <td><p>No</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>Páginas de administración de salida</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Archivos de aplicaciones web de Forms</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>Se utiliza para recuperar JavaScript durante la transformación HTML</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Páginas de administración de Forms</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repositorio/*</p> </td> 
   <td><p>URL para acceso WebDAV (depuración)</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>Interfaz de usuario de Aplicaciones y Servicios</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>Páginas de administración de Workspace</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>Páginas de asistencia restantes</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>Página de configuración de AEM Forms en JEE Core</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>Autenticación de administración de usuarios</p> </td> 
   <td><p>No</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>Interfaz de administración de administración de usuarios</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DoumentManager/*</p> </td> 
   <td><p>Carga y descarga de documentos que se van a procesar al acceder a puntos finales remotos, puntos finales WSDL SOAP y SDK de Java a través del transporte SOAP o de EJB con documentos HTTP activados.</p> </td> 
   <td><p>Sí</p> </td> 
   <td><p>Sí</p> </td> 
  </tr> 
 </tbody> 
</table>

## Protección contra ataques de falsificación de solicitudes entre sitios {#protecting-from-cross-site-request-forgery-attacks}

Un ataque de falsificación de solicitudes entre sitios (CSRF, por sus siglas en inglés) aprovecha la confianza que un sitio web tiene para el usuario, para transmitir comandos no autorizados y no deseados por el usuario. El ataque se configura incluyendo un vínculo o una secuencia de comandos en una página web, o una dirección URL en un mensaje de correo electrónico, para acceder a otro sitio en el que el usuario ya ha sido autenticado.

Por ejemplo, puede iniciar sesión en la Consola de administración mientras navega simultáneamente por otro sitio web. Una de las páginas web puede incluir una etiqueta de imagen HTML con un atributo `src` que destinatario una secuencia de comandos del lado del servidor en el sitio web de la víctima. Al aprovechar el mecanismo de autenticación de sesión basado en cookies proporcionado por los exploradores web, el sitio web atacante puede enviar solicitudes malintencionadas a este script de la víctima de servidor, que se muestra como el usuario legítimo. Para obtener más ejemplos, consulte [https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples).

Las siguientes características son comunes al RCSR:

* Involucrar sitios que dependen de la identidad del usuario.
* Explore la confianza del sitio en esa identidad.
* Haga clic en el explorador del usuario para enviar solicitudes HTTP a un sitio de destinatario.
* Involucrar solicitudes HTTP que tienen efectos secundarios.

AEM Forms en JEE utiliza la función Filtro de Remitente del reenvío para bloquear los ataques de CSRF. En esta sección se utilizan los términos siguientes para describir el mecanismo de filtrado de Remitentes del reenvío:

* **Remitente del reenvío permitido:** Un Remitente del reenvío es la dirección de la página de origen que envía una solicitud al servidor. Para páginas o formularios JSP, los Remitentes del reenvío son generalmente la página anterior en el historial de exploración. Los remitentes del reenvío de las imágenes son generalmente las páginas en las que se muestran las imágenes. Puede identificar el Remitente del reenvío al que se permite el acceso a los recursos del servidor agregándolos a la lista Remitente del reenvío permitido.
* **Excepciones de Remitente del reenvío permitidas:** es posible que desee restringir el ámbito de acceso de un Remitente del reenvío determinado en la lista de Remitente del reenvío permitido. Para aplicar esta restricción, puede agregar rutas individuales de ese Remitente del reenvío a la lista Excepciones de Remitente del reenvío permitidas. Las solicitudes procedentes de rutas de la lista Excepciones de Remitente del reenvío permitidas no pueden invocar ningún recurso en el servidor de formularios. Puede definir las excepciones de Remitente del reenvío permitidas para una aplicación específica y también utilizar una lista global de las excepciones que se aplican a todas las aplicaciones.
* **URI permitidos:** es una lista de recursos que se van a proporcionar sin comprobar el encabezado de Remitente del reenvío. Los recursos, por ejemplo, las páginas de ayuda, que no dan como resultado cambios de estado en el servidor, se pueden agregar a esta lista. Los recursos de la lista URI permitidos nunca son bloqueados por el filtro de Remitente del reenvío independientemente de quién sea el Remitente del reenvío.
* **Remitente del reenvío nulo:** una solicitud de servidor que no está asociada o no se origina desde una página web principal se considera una solicitud de un Remitente del reenvío nulo. Por ejemplo, cuando se abre una ventana nueva del explorador, se escribe una dirección y se pulsa Intro, el Remitente del reenvío enviado al servidor es nulo. Una aplicación de escritorio (.NET o SWING) que realiza una solicitud HTTP a un servidor web, también envía un Remitente del reenvío Null al servidor.

### Filtro de remitente del reenvío {#referer-filtering}

El proceso de filtrado de Remitentes del reenvío se puede describir de la siguiente manera:

1. El servidor de formularios comprueba el método HTTP utilizado para la invocación:

   1. Si es POST, el servidor de formularios realiza la comprobación de encabezado de Remitente del reenvío.
   1. Si es GET, el servidor de formularios omite la comprobación de Remitente del reenvío, a menos que *CSRF_CHECK_GETS* se establezca en true, en cuyo caso realiza la comprobación de encabezado de Remitente del reenvío. *CSRF_CHECK_* GETSse especifica en el archivo  *web.* xmlfile para la aplicación.

1. El servidor de formularios comprueba si el URI solicitado existe en la lista de permitidos:

   1. Si el URI está incluido en la lista de permitidos, el servidor acepta la solicitud.
   1. Si el URI solicitado no está incluido en la lista de permitidos, el servidor recupera el Remitente del reenvío de la solicitud.

1. Si hay un Remitente del reenvío en la solicitud, el servidor comprueba si es un Remitente del reenvío permitido. Si está permitido, el servidor comprueba si existe una excepción de Remitente del reenvío:

   1. Si se trata de una excepción, la solicitud se bloquea.
   1. Si no es una excepción, se pasa la solicitud.

1. Si no hay ningún Remitente del reenvío en la solicitud, el servidor comprueba si se permite un Remitente del reenvío nulo:

   1. Si se permite un Remitente del reenvío Null, se pasa la solicitud.
   1. Si no se permite un Remitente del reenvío Null, el servidor comprueba si el URI solicitado es una excepción para el Remitente del reenvío Null y gestiona la solicitud en consecuencia.

### Administración del filtro de Remitentes del reenvío {#managing-referer-filtering}

AEM Forms en JEE proporciona un filtro de Remitente del reenvío para especificar el Remitente del reenvío al que se permite el acceso a los recursos del servidor. De forma predeterminada, el filtro de Remitente del reenvío no filtra las solicitudes que utilizan un método HTTP seguro, por ejemplo, GET, a menos que *CSRF_CHECK_GETS* esté establecido en true. Si el número de puerto de una entrada de Remitente del reenvío permitida está establecido en 0, AEM Forms en JEE permitirá todas las solicitudes con Remitente del reenvío desde ese host, independientemente del número de puerto. Si no se especifica ningún número de puerto, solo se permiten las solicitudes del puerto predeterminado 80 (HTTP) o 443 (HTTPS). El filtrado de remitentes del reenvío se desactiva si se eliminan todas las entradas de la lista Remitente del reenvío permitido.

Al instalar por primera vez Documento Services, la lista Remitente del reenvío permitido se actualiza con la dirección del servidor en el que está instalado Documento Services. Las entradas para el servidor incluyen el nombre del servidor, la dirección IPv4, la dirección IPv6 si IPv6 está habilitada, la dirección loopback y una entrada localhost. El sistema operativo Host devuelve los nombres agregados a la lista Remitente del reenvío permitido. Por ejemplo, un servidor con una dirección IP de 10.40.54.187 incluirá las siguientes entradas: `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. Para cualquier nombre no apto devuelto por el sistema operativo del host (nombres que no tienen dirección IPv4, dirección IPv6 o nombre de dominio completo) no se actualiza la lista de permitidos. Modifique la lista Remitente del reenvío permitido para que se adapte a su entorno comercial. No implemente el servidor de formularios en el entorno de producción con la lista de Remitente del reenvío permitida predeterminada. Después de modificar cualquiera de los Remitentes del reenvío permitidos, las excepciones de Remitente del reenvío o los URI, asegúrese de reiniciar el servidor para que los cambios surtan efecto.

**Administración de la lista de Remitentes del reenvío permitidos**

Puede administrar la lista Remitente del reenvío permitido desde la interfaz de administración de usuarios de la Consola de administración. La interfaz de administración de usuarios le proporciona la funcionalidad de crear, editar o eliminar la lista. Consulte la sección * [Prevención de ataques CSRF](/help/forms/using/admin-help/preventing-csrf-attacks.md)* de la *ayuda de administración* para obtener más información sobre cómo trabajar con la lista de Remitente del reenvío permitido.

**Administración de excepciones de Remitente del reenvío permitidas y listas de URI permitidas**

AEM Forms en JEE proporciona API para administrar la lista de Excepción de Remitente del reenvío Permitida y la lista URI Permitida. Puede utilizar estas API para recuperar, crear, editar o eliminar la lista. A continuación se muestra una lista de las API disponibles:

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

Consulte la* Referencia de la API de AEM Forms en JEE* para obtener más información sobre las API.

Utilice la lista ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** para las excepciones de Remitente del reenvío permitidas a nivel global, es decir, para definir las excepciones aplicables a todas las aplicaciones. Esta lista solo contiene URI con una ruta absoluta (p. ej. `/index.html`) o una ruta relativa (p. ej. `/sample/`). También puede anexar una expresión regular al final de un URI relativo, por ejemplo: `/sample/(.)*`.

La ID de lista ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** se define como una constante en la clase `UMConstants` de la Área de nombres `com.adobe.idp.um.api`, que se encuentra en `adobe-usermanager-client.jar`. Puede utilizar las API de AEM Forms para crear, modificar o editar esta lista. Por ejemplo, para crear la lista Excepciones de Remitente del reenvío permitidos globales, utilice:

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

Utilice la lista ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** para las excepciones específicas de la aplicación.

**Desactivación del filtro Remitente del reenvío**

En el evento de que el Remitente del reenvío Filter bloquea completamente el acceso al servidor de formularios y no puede editar la lista Remitente del reenvío permitida, puede actualizar la secuencia de comandos de inicio del servidor y deshabilitar el filtrado de Remitentes del reenvío.

Incluya el argumento `-Dlc.um.csrffilter.disabled=true` JAVA en la secuencia de comandos de inicio y reinicie el servidor. Asegúrese de eliminar el argumento JAVA después de haber reconfigurado correctamente la lista Remitente del reenvío permitido.

**Filtrado de remitentes del reenvío para archivos WAR personalizados**

Es posible que haya creado archivos WAR personalizados para trabajar con AEM Forms en JEE con el fin de satisfacer los requisitos comerciales. Para habilitar el filtrado de Remitentes del reenvío para los archivos WAR personalizados, incluya ***adobe-usermanager-client.jar*** en la ruta de clases para la WAR e incluya una entrada de filtro en el archivo* web.xml* con los siguientes parámetros:

**CSRF_CHECK_** GETScontrola la comprobación de Remitentes del reenvío en las solicitudes de GET. Si no se define este parámetro, el valor predeterminado se establece en false. Incluya este parámetro solo si desea filtrar las solicitudes de GET.

**CSRF_ALLOWED_REFERER_** EXCEPTIONSes el ID de la lista de excepciones de Remitente del reenvío permitidas. El filtro de Remitente del reenvío impide que las solicitudes procedentes de Remitentes del reenvío de la lista identificada por el ID de lista invoquen cualquier recurso del servidor de formularios.

**CSRF_ALLOWED_URIS_LISTA_** NAMEes el ID de la lista URI permitidos. El filtro de Remitente del reenvío no bloquea las solicitudes de ninguno de los recursos de la lista identificada por el ID de lista, independientemente del valor del encabezado de Remitente del reenvío de la solicitud.

**CSRF_ALLOW_NULL_** REFERERcontrola el comportamiento del filtro de Remitente del reenvío cuando el Remitente del reenvío es nulo o no está presente. Si no se define este parámetro, el valor predeterminado se establece en false. Incluya este parámetro solo si desea permitir Remitentes del reenvío Null. Permitir remitentes del reenvío nulos puede permitir algunos tipos de ataques de falsificación de solicitudes entre sitios.

**CSRF_NULL_REFERER_** EXCEPTIONSes una lista de los URI para los que no se realiza una comprobación de Remitente del reenvío cuando el Remitente del reenvío es nulo. Este parámetro solo se habilita cuando *CSRF_ALLOW_NULL_REFERER* se establece en false. Separe varios URI de la lista con una coma.

A continuación se muestra un ejemplo de la entrada de filtro en el archivo *web.xml* para un archivo ***SAMPLE*** WAR:

```java
<filter> 
       <filter-name> filter-name </filter-name> 
       <filter-class> com.adobe.idp.um.auth.filter.RemoteCSRFFilter </filter-class> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_ALLOW_NULL_REFERER </param-name> 
      <param-value> false </param-value> 
     </init-param> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_CHECK_GETS </param-name> 
      <param-value> true </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
       <param-name> CSRF_NULL_REFERER_EXCEPTIONS </param-name> 
       <param-value> /SAMPLE/login, /SAMPLE/logout  </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_REFERER_EXCEPTIONS </param-name> 
      <param-value> SAMPLE_ALLOWED_REF_EXP_ID </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_URIS_LIST_NAME </param-name> 
      <param-value> SAMPLE_ALLOWED_URI_LIST_ID     </param-value> 
     </init-param> 
</filter> 
    ........ 
    <filter-mapping> 
      <filter-name> filter-name </filter-name> 
      <url-pattern>/*</url-pattern> 
    </filter-mapping>
```

**Solución de problemas**

Si el filtro CSRF bloquea las solicitudes legítimas del servidor, pruebe con uno de los siguientes métodos:

* Si la solicitud rechazada tiene un encabezado de Remitente del reenvío, considere detenidamente agregarla a la lista Remitente del reenvío permitido. Añada solo el Remitente del reenvío en el que confía.
* Si la solicitud rechazada no tiene un encabezado de Remitente del reenvío, modifique la aplicación cliente para incluir un encabezado de Remitente del reenvío.
* Si el cliente puede trabajar en un explorador, pruebe ese modelo de implementación.
* Como último recurso, puede agregar el recurso a la lista URI permitidos. No se trata de una configuración recomendada.

## Configuración de red segura {#secure-network-configuration}

En esta sección se describen los protocolos y puertos que AEM Forms necesita en JEE y se ofrecen recomendaciones para implementar AEM Forms en JEE en una configuración de red segura.

### Protocolos de red utilizados por AEM Forms en JEE {#network-protocols-used-by-aem-forms-on-jee}

Al configurar una arquitectura de red segura como se describe en la sección anterior, se requieren los siguientes protocolos de red para la interacción entre AEM Forms en JEE y otros sistemas de la red empresarial.

<table> 
 <thead> 
  <tr> 
   <th><p>Protocolo</p> </th> 
   <th><p>Uso</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>El explorador muestra Configuration Manager y aplicaciones Web de usuario final</p> </li> 
     <li><p>Todas las conexiones SOAP</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Aplicaciones cliente de servicios Web, como aplicaciones .NET</p> </li> 
     <li><p>Adobe Reader® utiliza SOAP para AEM Forms en los servicios web del servidor JEE</p> </li> 
     <li><p>Las aplicaciones Adobe Flash® utilizan SOAP para los servicios Web del servidor de formularios</p> </li> 
     <li><p>Llamadas al SDK de AEM Forms en JEE cuando se utilizan en modo SOAP</p> </li> 
     <li><p>Entorno de diseño de Workbench</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>Llamadas al SDK de AEM Forms en JEE cuando se utilizan en el modo de JavaBeans (EJB) de Enterprise</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP / POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>Entrada basada en correo electrónico a un servicio (extremo de correo electrónico)</p> </li> 
     <li><p>Notificaciones de tarea del usuario por correo electrónico</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>E/S de archivo UNC</p> </td> 
   <td><p>Control de AEM Forms en JEE de carpetas controladas para la entrada en un servicio (extremo de carpeta vigilada)</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Sincronizaciones de la información organizativa de usuarios y grupos en un directorio</p> </li> 
     <li><p>Autenticación LDAP para usuarios interactivos</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>Llamadas de consulta y procedimiento a una base de datos externa durante la ejecución de un proceso mediante el servicio JDBC</p> </li> 
     <li><p>Acceso interno a AEM Forms en el repositorio JEE</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>Permite la navegación remota del AEM Forms en el repositorio JEE en tiempo de diseño (formularios, fragmentos, etc.) por cualquier cliente WebDAV</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Aplicaciones de Flash de Adobe, donde AEM Forms en los servicios de servidor JEE está configurado con un extremo Remoting</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms en JEE expone MBeans para monitorear mediante JMX</p> </td> 
  </tr> 
 </tbody> 
</table>

### Puertos para servidores de aplicaciones {#ports-for-application-servers}

Esta sección describe los puertos predeterminados (e intervalos de configuración alternativos) para cada tipo de servidor de aplicaciones admitido. Estos puertos deben habilitarse o deshabilitarse en el servidor de seguridad interno, según la funcionalidad de red que desee permitir a los clientes que se conecten al servidor de aplicaciones que ejecutan AEM Forms en JEE.

>[!NOTE]
>
>De forma predeterminada, el servidor expone varios MBeans de JMX en la Área de nombres adobe.com. Solo se expone la información que resulta útil para la supervisión del estado del servidor. Sin embargo, para evitar la divulgación de información, debe evitar que los usuarios que llaman a una red de confianza busquen MBeans de JMX y accedan a métricas de estado.

**Puertos JBoss**

<table> 
 <thead> 
  <tr> 
   <th><p>Función</p> </th> 
   <th><p>Puerto</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Acceso a las aplicaciones Web</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[base de datos].xml</p> <p>Puerto del conector HTTP/1.1 8080</p> <p>Puerto 8009 del conector AJP 1.3</p> <p>Puerto del conector SSL/TLS 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>Compatibilidad con CORBA</p> </td> 
   <td><p>[JBoss root]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**Puertos WebLogic**

<table> 
 <thead> 
  <tr> 
   <th><p>Función</p> </th> 
   <th><p>Puerto</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Acceso a las aplicaciones Web</p> </td> 
   <td> 
    <ul> 
     <li><p>Puerto de escucha del servidor de administración: el valor predeterminado es 7001</p> </li> 
     <li><p>Puerto de escucha SSL del servidor de administración: el valor predeterminado es 7002</p> </li> 
     <li><p>Puerto configurado para servidor administrado, por ejemplo 8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>No se requieren puertos de administración WebLogic para acceder a AEM Forms en JEE</p> </td> 
   <td> 
    <ul> 
     <li><p>Puerto de escucha del servidor administrado: Configurable de 1 a 65534</p> </li> 
     <li><p>Puerto de escucha SSL del servidor administrado: Configurable de 1 a 65534</p> </li> 
     <li><p>Puerto de escucha del administrador de nodos: el valor predeterminado es 5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**Puertos WebSphere**

Para obtener información sobre los puertos WebSphere que requiere AEM Forms en JEE, vaya a Configuración del número de puerto en la interfaz de usuario del servidor de aplicaciones WebSphere.

### Configuración de SSL {#configuring-ssl}

En referencia a la arquitectura física que se describe en la sección [AEM Forms sobre la arquitectura física JEE](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture), debe configurar SSL para todas las conexiones que planea utilizar. Específicamente, todas las conexiones SOAP deben realizarse a través de SSL para evitar la exposición de las credenciales de usuario en una red.

Para obtener instrucciones sobre cómo configurar SSL en JBoss, WebLogic y WebSphere, consulte &quot;Configuración de SSL&quot; en la [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_64).

Para obtener instrucciones sobre cómo importar certificados a JVM (Máquina virtual Java) configurada para un servidor AEM Forms, consulte la sección Autenticación mutua en [Ayuda de AEM Forms Workbench](http://www.adobe.com/go/learn_aemforms_workbench_65).

### Configuración de la redirección SSL {#configuring-ssl-redirect}

Después de configurar el servidor de aplicaciones para que admita SSL, debe asegurarse de que todo el tráfico HTTP a aplicaciones y servicios se aplique para utilizar el puerto SSL.

Para configurar el redireccionamiento SSL para WebSphere o WebLogic, consulte la documentación del servidor de aplicaciones.

1. Abra el símbolo del sistema, vaya al directorio /JBOSS_HOME/standalone/configuration y ejecute el siguiente comando:

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. Abra el archivo JBOSS_HOME/standalone/configuration/standalone.xml para editarlo.

   Después del elemento &lt;subsistema xmlns=&quot;urn:jpatrón:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>, agregue los siguientes detalles:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot; />

1. Añada el siguiente código en el elemento de conector https:

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   Guarde y cierre el archivo standalone.xml.

## Recomendaciones de seguridad específicas de Windows {#windows-specific-security-recommendations}

Esta sección contiene recomendaciones de seguridad específicas de Windows cuando se utiliza para ejecutar AEM Forms en JEE.

### Cuentas de JBoss Service {#jboss-service-accounts}

La instalación llave en mano de AEM Forms en JEE configura una cuenta de servicio de forma predeterminada mediante la cuenta de sistema local. La cuenta de usuario integrada del sistema local tiene un alto nivel de accesibilidad; forma parte del grupo Administradores. Si la identidad de un proceso de trabajo se ejecuta como la cuenta de usuario del sistema local, ese proceso de trabajo tiene acceso completo a todo el sistema.

#### Ejecute el servidor de aplicaciones con una cuenta no administrativa {#run-the-application-server-using-a-non-administrative-account}

1. En Microsoft Management Console (MMC), cree un usuario local para que el servicio del servidor de formularios inicie sesión como:

   * Seleccione **El usuario no puede cambiar la contraseña**.
   * En la ficha **Miembro de**, asegúrese de que aparece el grupo Usuarios.

1. Seleccione **Configuración** > **Herramientas administrativas** > **Servicios**.
1. Haga clic con el botón doble en el servicio del servidor de aplicaciones y detenga el servicio.
1. En la ficha **Iniciar sesión**, seleccione **Esta cuenta**, busque la cuenta de usuario que ha creado e introduzca la contraseña para la cuenta.
1. En la ventana Configuración de seguridad local, en Asignación de derechos de usuario, otorgue los siguientes derechos a la cuenta de usuario en la que se ejecuta el servidor de formularios:

   * Denegar el inicio de sesión a través de Servicios de Terminal Server
   * Denegar el inicio de sesión localmente
   * Iniciar sesión como servicio (debe estar ya establecido)

1. Asigne a la nueva cuenta de usuario permisos de modificación en los directorios siguientes:
   * **Directorio** de Almacenamiento de Documento global (GDS): La ubicación del directorio GDS se configura manualmente durante el proceso de instalación de AEM Forms. Si la configuración de ubicación permanece vacía durante la instalación, la ubicación predeterminada es un directorio bajo la instalación del servidor de aplicaciones en `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Directorio** CRX-Repository: La ubicación predeterminada es  `[AEM-Forms-installation-location]\crx-repository`
   * **Directorios** temporales de AEM Forms:
      * (Windows) Ruta TMP o TEMP según se establece en las variables de entorno
      * (AIX, Linux o Solaris) Directorio de inicio del usuario con inicio de sesión
En sistemas basados en UNIX, un usuario no raíz puede utilizar el siguiente directorio como directorio temporal:
      * (Linux) /var/tmp o /usr/tmp
      * (AIX) /tmp o /usr/tmp
      * (Solaris) /var/tmp o /usr/tmp
1. Otorgue a la nueva cuenta de usuario permisos de escritura en los directorios siguientes:
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > Ubicación de instalación predeterminada del servidor de aplicaciones JBoss:
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jleader/.


1. Inicio del servicio del servidor de aplicaciones.

### Seguridad del sistema de archivos {#file-system-security}

AEM Forms en JEE utiliza el sistema de archivos de las siguientes maneras:

* Almacena los archivos temporales que se utilizan al procesar la entrada y salida de documento
* Almacena archivos en el almacén de archivos global que se utilizan para admitir los componentes de la solución instalados
* Las carpetas vigiladas almacenan los archivos perdidos que se utilizan como entrada a un servicio desde una ubicación de carpetas del sistema de archivos

Cuando utilice carpetas vigiladas como forma de enviar y recibir documentos con un servicio de servidor de formularios, tenga en cuenta las precauciones adicionales relacionadas con la seguridad del sistema de archivos. Cuando un usuario coloca contenido en la carpeta vigilada, este se expone a través de la carpeta vigilada. En este caso, el servicio no autentica al usuario final real. En su lugar, se basa en la seguridad de nivel ACL y Compartir para que se establezca en el nivel de carpeta a fin de determinar quién puede invocar el servicio de forma eficaz.

## Recomendaciones de seguridad específicas de JBoss {#jboss-specific-security-recommendations}

Esta sección contiene recomendaciones de configuración del servidor de aplicaciones específicas de JBoss 7.0.6 cuando se utiliza para ejecutar AEM Forms en JEE.

### Deshabilitar la Consola de administración JBoss y la Consola JMX {#disable-jboss-management-console-and-jmx-console}

El acceso a la consola de administración de JBoss y a la consola JMX ya está configurado (la supervisión de JMX está deshabilitada) al instalar AEM Forms en JEE en JBoss mediante el método de instalación llave en mano. Si utiliza su propio servidor de aplicaciones JBoss, asegúrese de que el acceso a la consola de administración JBoss y a la consola de supervisión JMX esté asegurado. El acceso a la consola de supervisión JMX se establece en el archivo de configuración JBoss llamado jmx-invoker-service.xml.

### Deshabilitar exploración de directorios {#disable-directory-browsing}

Después de iniciar sesión en la Consola de administración, es posible examinar la lista de directorios de la consola modificando la dirección URL. Por ejemplo, si cambia la dirección URL a una de las siguientes direcciones URL, puede aparecer un listado de directorio:

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## Recomendaciones de seguridad específicas de WebLogic {#weblogic-specific-security-recommendations}

Esta sección contiene recomendaciones de configuración del servidor de aplicaciones para proteger WebLogic 9.1 al ejecutar AEM Forms en JEE.

### Deshabilitar exploración de directorios {#disable_directory_browsing-1}

Configure las propiedades index-directory del archivo weblogic.xml en `false`, como se muestra en este ejemplo:

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### Habilitar el puerto SSL de WebLogic {#enable-weblogic-ssl-port}

De forma predeterminada, WebLogic no habilita el puerto de escucha SSL predeterminado, 7002. Habilite este puerto en la consola de administración de WebLogic Server antes de configurar SSL.

## Recomendaciones de seguridad específicas de WebSphere {#websphere-specific-security-recommendations}

Esta sección contiene recomendaciones de configuración del servidor de aplicaciones para proteger WebSphere que ejecuta AEM Forms en JEE.

### Deshabilitar exploración de directorios {#disable_directory_browsing-2}

Establezca la propiedad `directoryBrowsingEnabled` en el archivo ibm-web-ext.xml como `false`.

### Habilitar la seguridad administrativa de WebSphere {#enable-websphere-administrative-security}

1. Inicie sesión en la Consola administrativa de WebSphere.
1. En el árbol de navegación, vaya a **Seguridad** > **Seguridad global**
1. Seleccione **Habilitar seguridad administrativa**.
1. Anule la selección de **Activar seguridad de la aplicación** y **Usar seguridad de Java 2**.
1. Haga clic en **Aceptar** o **Aplicar**.
1. En el cuadro **Mensajes**, haga clic en **Guardar directamente en la configuración maestra**.