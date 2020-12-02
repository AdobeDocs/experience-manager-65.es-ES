---
title: Implementación y mantenimiento
seo-title: Implementación y mantenimiento
description: Obtenga información sobre cómo empezar con la instalación de AEM.
seo-description: Obtenga información sobre cómo empezar con la instalación de AEM.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
translation-type: tm+mt
source-git-commit: cb07e24b01084f57ad46615cb463ad5a0329c181
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 7%

---


# Implementación y mantenimiento{#deploying-and-maintaining}

En esta página encontrará:

* [Conceptos básicos](#basic-concepts)

   * [¿Qué es AEM?](#what-is-aem)
   * [Implementaciones habituales](#typical-deployment-scenarios) 

      * [In situ](#on-premise)
      * [Managed Services con Cloud Manager](#managed-services-using-cloud-manager)

* [Introducción](#getting-started)

   * [Requisitos previos](#prerequisites)
   * [Obtención del software](#getting-the-software)
   * [Instalación local predeterminada](#default-local-install)
   * [Creación y publicación de instalaciones](#author-and-publish-installs)
   * [Directorio de instalación sin empaquetar](#unpacked-install-directory)
   * [Inicio y parada](#starting-and-stopping)

Una vez familiarizado con estos conceptos básicos, encontrará información más avanzada y detallada en las siguientes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalación independiente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Instalación del servidor de aplicaciones](/help/sites-deploying/application-server-install.md)
* [Solución de problemas](/help/sites-deploying/troubleshooting.md)
* [Línea de comandos: start y stop](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuración](/help/sites-deploying/configuring.md)
* [Actualización a AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/sites-deploying/ecommerce.md)
* [Artículos de procedimientos de configuración](/help/sites-deploying/ht-deploy.md)
* [Consola web](/help/sites-deploying/web-console.md)
* [Resolución de problemas de replicación](/help/sites-deploying/troubleshoot-rep.md)
* [Prácticas recomendadas  ](/help/sites-deploying/best-practices.md)
* [Implementación de comunidades](/help/communities/deploy-communities.md)
* [Introducción a la Plataforma AEM](/help/sites-deploying/platform.md)
* [Directrices de rendimiento](/help/sites-deploying/performance-guidelines.md)
* [Introducción a AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [¿Qué es AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)

## Conceptos básicos {#basic-concepts}

### ¿Qué es AEM? {#what-is-aem}

Adobe Experience Manager es un sistema de cliente-servidor basado en web para crear, administrar e implementar sitios web comerciales y servicios relacionados. Combina varias funciones a nivel de infraestructura y aplicación en un único paquete integrado.

A nivel de infraestructura, AEM ofrece lo siguiente:

* **Servidor** de aplicación web: AEM puede implementarse en modo independiente (incluye un servidor web integrado de Jetty) o como una aplicación web dentro de un servidor de aplicaciones de terceros.
* **Marco** de aplicación web: AEM incorpora el Sling Aplicación web Framework que simplifica la escritura de aplicaciones web orientadas al contenido RESTful.
* **Repositorio** de contenido: AEM incluye un repositorio de contenido Java (JCR), un tipo de base de datos jerárquica diseñada específicamente para datos no estructurados y semiestructurados. El repositorio almacena no sólo el contenido orientado al usuario, sino también todo el código, las plantillas y los datos internos que utiliza la aplicación.

Sobre esta base, AEM también una serie de funciones a nivel de aplicación para la administración de:

* **Sitios web**
* **Aplicaciones móviles**
* **Publicaciones digitales**
* **Forms**
* **Recursos digitales**
* **Comunidades**
* **Comercio en línea**

Por último, los clientes pueden utilizar estos componentes de infraestructura y de nivel de aplicación para crear soluciones personalizadas mediante la creación de aplicaciones propias.

El servidor de AEM está **basado en Java** y se ejecuta en la mayoría de los sistemas operativos que admiten esa plataforma. Toda la interacción del cliente con AEM se realiza a través de un **explorador Web**.

### Escenarios de implementación típicos {#typical-deployment-scenarios}

En AEM terminología, una &quot;instancia&quot; es una copia de AEM ejecutándose en un servidor. Las instalaciones de AEM suelen incluir al menos dos instancias, normalmente en equipos independientes:

* **Autor**: Instancia de AEM utilizada para crear, cargar y editar contenido y administrar el sitio web. Una vez que el contenido está listo para activarse, se replica en la instancia de publicación.
* **Publicar**: Una instancia de AEM que sirve el contenido publicado al público.

Estas instancias son idénticas en términos de software instalado. Solo se diferencian por configuración. Además, la mayoría de las instalaciones utilizan un distribuidor:

* **Dispatcher**: Un servidor web estático (Apache httpd, Microsoft IIS, etc.) se ha ampliado con el módulo de despachante de AEM. Almacena en caché las páginas web producidas por la instancia de publicación para mejorar el rendimiento.

Hay muchas opciones avanzadas y elaboraciones de esta configuración, pero el patrón básico de creación, publicación y despachante está en el centro de la mayoría de las implementaciones. Empezaremos por centrarnos en una configuración relativamente simple. A continuación se analizarán las opciones de implementación avanzada.

Las siguientes secciones describen ambos escenarios:

* **In situ**: AEM implementada y administrada en su entorno corporativo.

* **Managed Services - Cloud Manager para Adobe Experience Manager**: AEM implementada y administrada por Adobe Managed Services.

### In situ {#on-premise}

Puede instalar AEM en los servidores de su entorno corporativo. Las instancias de instalación habituales incluyen: Entornos de desarrollo, prueba y publicación. Consulte la sección [Introducción](/help/sites-deploying/deploy.md#getting%20started) para obtener detalles básicos sobre cómo obtener el software AEM para instalarlo localmente.

Para obtener más información sobre las implementaciones locales típicas, consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md).

### Managed Services con Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services es una solución completa para la administración de experiencias digitales. Ofrece beneficios de la solución de envío de experiencias en la nube, al tiempo que conserva todos los beneficios de control, seguridad y personalización de una implementación local. AEM Managed Services permite que los clientes se inicien más rápido mediante la implementación en la nube y también gracias a las optimizaciones y la asistencia técnica de Adobe. Las organizaciones y los usuarios empresariales pueden atraer a los clientes en un tiempo mínimo, impulsar la participación en el mercado y centrarse en crear campañas de mercadotecnia innovadoras, al tiempo que reducen la carga que supone para la TI.

Con AEM Managed Services, los clientes pueden obtener las siguientes ventajas:

**Tiempo de salida al mercado más rápido:** con una infraestructura flexible en la nube de los servicios gestionados de Adobe, las organizaciones pueden planificar, lanzar y optimizar experiencias digitales exitosas con rapidez. Adobe administra la arquitectura de la nube sin necesidad de capital adicional, hardware o software, y los ingenieros de éxito del cliente de Adobe le ayudan con la arquitectura, el aprovisionamiento y la personalización de AEM para conectarse a aplicaciones de back-end y las prácticas recomendadas de lanzamiento.

**Mayor rendimiento:** proporciona experiencias digitales fiables para su empresa con cuatro opciones de disponibilidad de servicios: 99,5%, 99,9%, 99,95% y 99,99%. Además, permite el backup automático y los modelos multimodo de recuperación ante desastres para garantizar la confiabilidad y la administración de contingencias.

**Costos de TI optimizados: la orientación** proactiva y la experiencia ayudan a las organizaciones a mantenerse al día en la versión más reciente de AEM. El mantenimiento y soporte de Adobe Platinum se incluye automáticamente en las nuevas implementaciones de AMS Enterprise/Basic, ofreciendo experiencia técnica y operacional para ayudar a las organizaciones a mantener sus aplicaciones de misión crítica. Las funciones básicas gratuitas de Analytics o Destinatario oferta un valor adicional, especialmente para organizaciones de mercado medio con necesidades limitadas de análisis y personalización.

**Mayor seguridad:** garantiza la seguridad física, de red y de datos de calidad empresarial alojando aplicaciones de cliente en una instalación de acceso restringido, detrás de sistemas de firewall o dentro de una nube privada virtual. Incluye máquinas virtuales de un solo inquilino con cifrado sólido de almacenamiento de datos, antivirales y aislamiento de datos.

**Administrador** de nube: Cloud Manager, que forma parte de la oferta de Adobe Experience Manager Managed Services, es un portal de autoservicio que permite a las organizaciones autoadministrar Adobe Experience Manager en la nube. Incluye una integración continua de última generación y una canalización de envío continuo (CI/CD) que permite a los equipos de TI y a los socios de implementación acelerar el envío de personalizaciones o actualizaciones sin comprometer el rendimiento ni la seguridad. Cloud Manager solo está disponible para los clientes de servicios gestionados de Adobe.

Para obtener más información sobre Cloud Manager y sus recursos, consulte la [**Guía del usuario del Administrador de nube**](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## Introducción {#getting-started}

### Requisitos previos {#prerequisites}

Aunque las instancias de producción se ejecutan generalmente en equipos dedicados que ejecutan un SO oficialmente admitido (consulte [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)), el servidor Experience Manager se ejecutará en cualquier sistema que admita [**Java Standard Edition 8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Para familiarizarse y desarrollar en AEM es bastante común utilizar una instancia instalada en el equipo local que ejecuta Apple OS X o versiones de escritorio de Microsoft Windows o Linux.

En el lado del cliente, AEM funciona con todos los exploradores modernos (**Microsoft Edge**, **Internet Explorer** 11, **Chrome **51+** **, **Firefox **47+, **Safari** 8+) en los sistemas operativos de escritorio y tablet. Consulte [Plataformas de cliente admitidas](/help/sites-deploying/technical-requirements.md#supported-client-platforms) para obtener más información.

### Obtención del software {#getting-the-software}

Los clientes con un contrato de mantenimiento y soporte válido deberían haber recibido una notificación por correo con un código y poder descargar AEM del [**sitio Web de licencias de Adobe**](https://licensing.adobe.com/). Los socios comerciales pueden solicitar acceso de descarga en [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

El paquete de software AEM está disponible en dos formatos:

* **cq-quickstart-6.5.0.jar:** archivo de  ** jerga ejecutable independiente que incluye todo lo necesario para ponerse en marcha.

* **cq-quickstart-6.5.0.war:** Un  ** archivo de almacenamiento para la implementación en un servidor de aplicaciones de terceros.

En la siguiente sección describimos la **instalación independiente**. Para obtener más información sobre la instalación de AEM en un servidor de aplicaciones, consulte [Instalación de Application Server](/help/sites-deploying/application-server-install.md).

### Instalación local predeterminada {#default-local-install}

1. Cree un directorio de instalación en el equipo local. Por ejemplo:

   Ubicación de instalación de UNIX: **/opt/aem**

   Ubicación de instalación de Windows: **`C:\Program Files\aem`**

   Del mismo modo, es común instalar instancias de ejemplo en una carpeta del escritorio. En cualquier caso, nos referiremos a esta ubicación de forma genérica como:

   `<aem-install>`

   *Tenga en cuenta que la ruta del directorio de archivos debe constar únicamente de caracteres ASCII de EE.UU.*

1. Coloque los archivos **jar** y **license **archivos en este directorio:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Si no proporciona un archivo `license.properties`, AEM redireccionará el explorador a una pantalla **Bienvenida** al inicio, donde puede introducir una clave de licencia. Deberá solicitar una clave de licencia válida a Adobe si todavía no la tiene.

1. Para inicio de la instancia en un entorno GUI, haga clic con el botón doble en el archivo **`cq-quickstart-6.5.0.jar`**.

   Como alternativa, puede iniciar AEM desde la línea de comandos. Para una VM Java de 32 bits, introduzca lo siguiente:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

   Para una VM de 64 bits, introduzca:

   ```shell
       java -XX:MaxPermSize=256m -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM tomarán unos minutos para desempaquetar el archivo jar, instalarse y inicio. El procedimiento anterior da lugar a:

* una instancia de **AEM autor**
* ejecutándose en **localhost**
* en el puerto **4502**

Para acceder a la instancia, dirija el explorador a:

**`https://localhost:4502`**

El resultado en la instancia de autor se configurará automáticamente para conectarse a una **instancia de publicación** en **`localhost:4503`**.

### Creación y publicación de instalaciones {#author-and-publish-installs}

La instalación predeterminada (una instancia **author** en **`localhost:4502`**) se puede cambiar simplemente cambiando el nombre del archivo `jar` antes de iniciarlo por primera vez. El patrón de nomenclatura es:

**`cq-<instance-type>-p<port-number>.jar`**

Por ejemplo, cambiar el nombre del archivo a

**`cq-author-p4502.jar`**

y al iniciarla, se ejecutará una instancia de autor en **`localhost:4502`**.

Del mismo modo, al cambiar el nombre del archivo y al iniciarlo

**`cq-publish-p4503.jar`**

resultará en una instancia de publicación que se ejecute el **`localhost:4503`**.

instalaría estas dos instancias en, por ejemplo

`<aem-install>/author`y

**`<aem-install>/publish`**

Para obtener más información sobre la personalización de la instalación, consulte:

* [Instalación independiente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Ejecutar modos](/help/sites-deploying/configure-runmodes.md)

### Directorio de instalación desempaquetado {#unpacked-install-directory}

Cuando el tarro de arranque rápido se inicia por primera vez, se descomprime en el mismo directorio bajo un nuevo subdirectorio llamado `crx-quickstart`. Debería terminar con lo siguiente:

```xml
<aem-install>/
    license.properties
    cq-quickstart-6.5.0.jar
    crx-quickstart/
        app/
        bin/
        conf/
        launchpad/
        logs/
        metrics/
        monitoring/
        opt/
        repository/
        threaddumps/
        eula-de_DE.html
        eula-en_US.html
        eula-fr_FR.html
        eula-ja_JP.html
        readme.txt
```

Si la instancia se instaló desde la interfaz de usuario, se abrirá automáticamente una ventana del explorador y también se abrirá una ventana de la aplicación de escritorio con el host y el puerto de la instancia y un conmutador de activación y desactivación:

![Pantalla de inicio hacia arriba](assets/screen_shot_.png)

>[!NOTE]
>
>Si está utilizando enlaces simbólicos, consulte [problemas con symlink](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### Inicio y parada {#starting-and-stopping}

Una vez que AEM se ha desempacado y se ha iniciado por primera vez, el doble de hacer clic en el archivo jar en el directorio de instalación simplemente inicio la instancia, no la vuelve a instalar.

Para detener la instancia desde la GUI, haga clic en el conmutador **on/off** en la ventana de la aplicación de escritorio.

También puede detener y inicio AEM desde la línea de comandos. Suponiendo que ya ha instalado la instancia por primera vez, los **scripts de línea de comandos** se encuentran aquí:

**`<aem-install>/crx-quickstart/bin/`**

Esta carpeta contiene los siguientes scripts de shell de bash de Unix:

* **`start`**:: Inicio la instancia
* `stop`:: Detiene la instancia
* **`status`**:: Informa del estado de la instancia
* **`quickstart`**:: Se utiliza para configurar la información de inicio, si es necesario.

También hay archivos equivalentes **`bat`** para Windows. Para obtener información más detallada, consulte:

* [Línea de comandos: start y stop](/help/sites-deploying/command-line-start-and-stop.md)

AEM inicios y redirige automáticamente el explorador Web a la página adecuada, generalmente la página de inicio de sesión; por ejemplo:

`https://localhost:4502/`

![pantalla de inicio de sesión](assets/screen_shot_2019-04-08at83533am.png)

Una vez que haya iniciado sesión, tendrá acceso a AEM. Para obtener más información, en función de su función, consulte:

* [Creación  ](/help/sites-authoring/home.md)
* [Administración](/help/sites-administering/home.md)
* [Desarrollo de](/help/sites-developing/home.md)
* [Administración](/help/managing/best-practices.md)

## Implementación avanzada {#advanced-deployment}

La sección anterior debería proporcionarle una buena comprensión de los conceptos básicos de AEM instalación. Sin embargo, la instalación de un sistema completo de producción de AEM puede implicar una complejidad considerablemente mayor. Para obtener una cobertura completa de la instalación avanzada, consulte las siguientes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalación independiente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Instalación del servidor de aplicaciones](/help/sites-deploying/application-server-install.md)
* [Solución de problemas](/help/sites-deploying/troubleshooting.md)
* [Línea de comandos: start y stop](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuración](/help/sites-deploying/configuring.md)
* [Actualización a AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/sites-deploying/ecommerce.md)
* [Artículos de procedimientos de configuración](/help/sites-deploying/ht-deploy.md)
* [Consola web](/help/sites-deploying/web-console.md)
* [Resolución de problemas de replicación](/help/sites-deploying/troubleshoot-rep.md)
* [Prácticas recomendadas  ](/help/sites-deploying/best-practices.md)
* [Implementación de comunidades](/help/communities/deploy-communities.md)
* [Introducción a la Plataforma AEM](/help/sites-deploying/platform.md)
* [Directrices de rendimiento](/help/sites-deploying/performance-guidelines.md)
* [Introducción a AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [¿Qué es AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
