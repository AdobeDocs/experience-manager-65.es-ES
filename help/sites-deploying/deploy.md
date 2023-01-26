---
title: Implementación y mantenimiento
seo-title: Deploying and Maintaining
description: Obtenga información sobre cómo empezar a utilizar la instalación de AEM.
seo-description: Learn how to get started with the AEM installation.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
source-git-commit: 2a350548674ff3f8dc49defa47ac2b028da76f4b
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 8%

---

# Implementación y mantenimiento{#deploying-and-maintaining}

En esta página encontrará:

* [Conceptos básicos](#basic-concepts)

   * [¿Qué es AEM?](#what-is-aem)
   * [Implementaciones habituales ](#typical-deployment-scenarios)

      * [On-Premise](#on-premise)
      * [Managed Services mediante Cloud Manager](#managed-services-using-cloud-manager)

* [Introducción](#getting-started)

   * [Requisitos previos](#prerequisites)
   * [Obtención del software](#getting-the-software)
   * [Instalación local predeterminada](#default-local-install)
   * [Creación y publicación de instalaciones](#author-and-publish-installs)
   * [Directorio de instalación desempaquetado](#unpacked-install-directory)
   * [Inicio y parada](#starting-and-stopping)

Una vez que se haya familiarizado con estos conceptos básicos, encontrará información más avanzada y detallada en las siguientes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalación independiente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Instalación del servidor de aplicaciones](/help/sites-deploying/application-server-install.md)
* [Solución de problemas](/help/sites-deploying/troubleshooting.md)
* [Línea de comandos: start y stop](/help/sites-deploying/command-line-start-and-stop.md)
* [Configurar](/help/sites-deploying/configuring.md)
* [Actualización a AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Artículos de procedimientos de configuración](/help/sites-deploying/ht-deploy.md)
* [Consola web](/help/sites-deploying/web-console.md)
* [Solución de problemas de replicación](/help/sites-deploying/troubleshoot-rep.md)
* [Prácticas recomendadas](/help/sites-deploying/best-practices.md)
* [Implementación de comunidades](/help/communities/deploy-communities.md)
* [Introducción a la plataforma AEM](/help/sites-deploying/platform.md)
* [Directrices de rendimiento](/help/sites-deploying/performance-guidelines.md)
* [Introducción a AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [¿Qué es AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=es)

## Conceptos básicos {#basic-concepts}

### ¿Qué es AEM? {#what-is-aem}

Adobe Experience Manager es un sistema de cliente-servidor basado en web para crear, administrar e implementar sitios web comerciales y servicios relacionados. Combina varias funciones a nivel de infraestructura y aplicación en un único paquete integrado.

A nivel de infraestructura AEM proporciona lo siguiente:

* **Servidor de aplicaciones web**: AEM puede implementarse en modo independiente (incluye un servidor web Jetty integrado) o como una aplicación web dentro de un servidor de aplicaciones de terceros.
* **Marco de aplicaciones web**: AEM incorpora el marco de aplicación web de Sling que simplifica la escritura de aplicaciones web orientadas al contenido y RESTful.
* **Repositorio de contenido**: AEM incluye un repositorio de contenido Java (JCR), un tipo de base de datos jerárquica diseñada específicamente para datos no estructurados y semiestructurados. El repositorio almacena no solo el contenido orientado al usuario, sino también todo el código, las plantillas y los datos internos utilizados por la aplicación.

Basándose en esta base, AEM también ofrece una serie de funciones a nivel de aplicación para la administración de:

* **Sitios web**
* **Aplicaciones móviles**
* **Publicaciones digitales**
* **Forms**
* **Recursos digitales**
* **Communities**
* **Comercio en línea**

Por último, los clientes pueden utilizar estos componentes básicos de infraestructura y de nivel de aplicación para crear soluciones personalizadas creando aplicaciones propias.

El servidor AEM es **Basado en Java** y se ejecuta en la mayoría de los sistemas operativos que admiten esa plataforma. Toda la interacción del cliente con AEM se realiza mediante un **explorador web**.

### Escenarios de implementación habituales {#typical-deployment-scenarios}

En AEM terminología, una &quot;instancia&quot; es una copia de AEM que se ejecuta en un servidor. AEM instalaciones suelen implicar al menos dos instancias, normalmente se ejecutan en equipos separados:

* **Autor**: Instancia de AEM utilizada para crear, cargar y editar contenido y para administrar el sitio web. Una vez que el contenido está listo para su publicación, se replica en la instancia de publicación.
* **Publicación**: Una instancia de AEM que sirve el contenido publicado al público.

Estas instancias son idénticas en términos de software instalado. Solo se diferencian por configuración. Además, la mayoría de las instalaciones utilizan un Dispatcher:

* **Dispatcher**: Un servidor web estático (Apache httpd, Microsoft IIS, etc.) se ha ampliado con el módulo AEM dispatcher. Almacena en caché las páginas web producidas por la instancia de publicación para mejorar el rendimiento.

Existen muchas opciones avanzadas y explicaciones sobre esta configuración, pero el patrón básico de autor, publicación y Dispatcher es el núcleo de la mayoría de las implementaciones. Empezaremos por centrarnos en una configuración relativamente sencilla. A continuación se analizan las opciones de implementación avanzadas.

Las secciones siguientes describen ambos escenarios:

* **On-Premise**: AEM implementado y administrado en su entorno corporativo.

* **Managed Services: Cloud Manager para Adobe Experience Manager**: AEM implementado y administrado por Adobe Managed Services.

### On-Premise {#on-premise}

Puede instalar AEM en los servidores de su entorno corporativo. Entre las instancias de instalación habituales se incluyen: Entornos de desarrollo, pruebas y publicación. Consulte la [Introducción](/help/sites-deploying/deploy.md#getting%20started) para obtener detalles básicos sobre cómo obtener el software AEM para instalarlo localmente.

Para obtener más información sobre las implementaciones locales típicas, consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md).

### Managed Services mediante Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services es una solución completa para la administración de experiencias digitales. Proporciona beneficios de la solución de entrega de experiencias en la nube, al tiempo que conserva todos los beneficios de control, seguridad y personalización de una implementación local. AEM Managed Services permite a los clientes iniciarse más rápido mediante la implementación en la nube y también gracias a las prácticas recomendadas y a la asistencia de Adobe. Las organizaciones y los usuarios empresariales pueden atraer a los clientes en un tiempo mínimo, impulsar la cuota de mercado y centrarse en la creación de campañas de marketing innovadoras, a la vez que reducen la carga para TI.

Con AEM Managed Services, los clientes pueden obtener las siguientes ventajas:

**Tiempo de comercialización más rápido:** Con la infraestructura flexible de nube de Adobe Managed Services, las organizaciones pueden planificar, iniciar y optimizar rápidamente experiencias digitales exitosas. Adobe administra la arquitectura de la nube sin necesidad de capital adicional, hardware ni software, y los ingenieros de éxito de los clientes de Adobe le ayudarán con la arquitectura de AEM, el aprovisionamiento y la personalización para conectarse a aplicaciones back-end y las prácticas recomendadas de lanzamiento.

**Mayor rendimiento:** Proporciona experiencias digitales fiables para su empresa con cuatro opciones de disponibilidad de servicios: 99,5%, 99,9%, 99,95% y 99,99%. Además, permite el backup automático y los modelos de recuperación ante desastres multimodo para ayudar a garantizar la confiabilidad y la administración de contingencias.

**Costes de TI optimizados:** La orientación proactiva y la experiencia ayudan a las organizaciones a mantenerse al día con la última versión de AEM. El mantenimiento y soporte de platino de Adobe se incluye automáticamente en las nuevas implementaciones de AMS Enterprise/Basic, ofreciendo experiencia técnica y operativa para ayudar a las organizaciones a mantener sus aplicaciones de misión crítica. Las funciones básicas gratuitas de Analytics o Target ofrecen un valor adicional, especialmente para organizaciones de mercado intermedio con necesidades limitadas de análisis y personalización.

**Mayor seguridad:** Garantiza la seguridad física, de red y de datos de nivel empresarial al alojar aplicaciones de clientes en una instalación de acceso restringido, detrás de sistemas de firewall o dentro de una nube privada virtual. Incluye máquinas virtuales de un solo inquilino con cifrado sólido de almacenamiento de datos, antivirales y aislamiento de datos.

**Cloud Manager**: Cloud Manager, parte de la oferta de Adobe Experience Manager Managed Services, es un portal de autoservicio que además permite a las organizaciones autoadministrar Adobe Experience Manager en la nube. Incluye una integración continua y una canalización de envío continuo (CI/CD) de última generación que permite a los equipos de TI y a los socios de implementación acelerar la entrega de personalizaciones o actualizaciones sin comprometer el rendimiento o la seguridad. Cloud Manager solo está disponible para los clientes de servicios administrados de Adobe.

Para obtener más información sobre Cloud Manager y sus recursos, consulte [**Guía del usuario de Cloud Manager**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html).

## Introducción {#getting-started}

### Requisitos previos {#prerequisites}

Mientras que las instancias de producción generalmente se ejecutan en máquinas dedicadas que ejecutan un sistema operativo oficialmente compatible (consulte [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)), el servidor Experience Manager se ejecutará en cualquier sistema que admita [**Java Standard Edition 8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Para familiarizarse y desarrollar en AEM es bastante común utilizar una instancia instalada en el equipo local que ejecuta Apple OS X o versiones de escritorio de Microsoft Windows o Linux.

En el lado del cliente, AEM funciona con todos los exploradores modernos (**Microsoft Edge**, **Internet Explorer** 11, **Chrome **51+** **, **Firefox **47+, **Safari** 8+) en los sistemas operativos de escritorio y tableta. Consulte [Plataformas de cliente compatibles](/help/sites-deploying/technical-requirements.md#supported-client-platforms) para obtener más información.

### Obtención del software {#getting-the-software}

Los clientes con un contrato de mantenimiento y asistencia válido deberían haber recibido una notificación por correo electrónico con un código y poder descargar AEM desde la [**Sitio web de licencias de Adobe**](https://licensing.adobe.com/). Los socios comerciales pueden solicitar acceso de descarga desde [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

El paquete de software AEM está disponible en dos formatos:

* **cq-quickstart-6.5.0.jar:** Un ejecutable independiente *jar* que incluye todo lo necesario para ponerse en marcha.

* **cq-quickstart-6.5.0.war:** A *war* para su implementación en un servidor de aplicaciones de terceros.

En la siguiente sección describimos el **instalación independiente**. Para obtener más información sobre la instalación de AEM en un servidor de aplicaciones, consulte [Instalación del servidor de aplicaciones](/help/sites-deploying/application-server-install.md).

### Instalación local predeterminada {#default-local-install}

1. Cree un directorio de instalación en el equipo local. Por ejemplo:

   Ubicación de instalación de UNIX: **/opt/aem**

   Ubicación de instalación de Windows: **`C:\Program Files\aem`**

   Del mismo modo, es común instalar instancias de ejemplo en una carpeta directamente en el escritorio. En cualquier caso, nos referiremos a esta ubicación de forma genérica como:

   `<aem-install>`

   *Tenga en cuenta que la ruta del directorio de archivos debe constar solamente de caracteres ASCII de EE. UU.*

1. Coloque el **jar** y **licencia** archivos en este directorio:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Si no proporciona un `license.properties` AEM redireccionará el explorador a un **Bienvenido** al inicio, donde puede introducir una clave de licencia. Deberá solicitar una clave de licencia válida al Adobe si todavía no la tiene.

1. Para iniciar la instancia en un entorno GUI, haga doble clic en el botón **`cq-quickstart-6.5.0.jar`** archivo.

   Como alternativa, puede iniciar AEM desde la línea de comandos:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM tardará unos minutos en desempaquetar el archivo jar, instalarse y comenzar. El procedimiento anterior da como resultado:

* an **AEM autor** instancia
* en ejecución **localhost**
* en puerto **4502**

Para acceder a la instancia, dirija el navegador a:

**`https://localhost:4502`**

El resultado en la instancia de autor se configurará automáticamente para conectarse a un **instancia de publicación** en **`localhost:4503`**.

### Creación y publicación de instalaciones {#author-and-publish-installs}

La instalación predeterminada (una **author** instancia en **`localhost:4502`**) se puede cambiar simplemente cambiando el nombre de la variable `jar` antes de iniciarlo por primera vez. El patrón de nomenclatura es:

**`cq-<instance-type>-p<port-number>.jar`**

Por ejemplo, cambiar el nombre del archivo a

**`cq-author-p4502.jar`**

y al iniciarlo, se ejecutará una instancia de autor en **`localhost:4502`**.

Del mismo modo, cambiar el nombre del archivo e iniciarlo

**`cq-publish-p4503.jar`**

resultará en una instancia de publicación en **`localhost:4503`**.

Puede instalar estas dos instancias en , por ejemplo

`<aem-install>/author`y

**`<aem-install>/publish`**

Para obtener más información sobre la personalización de la instalación, consulte lo siguiente:

* [Instalación independiente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Ejecutar modos](/help/sites-deploying/configure-runmodes.md)

### Directorio de instalación desempaquetado {#unpacked-install-directory}

Cuando se inicie el tarro de inicio rápido por primera vez, se descomprimirá en el mismo directorio bajo un nuevo subdirectorio llamado `crx-quickstart`. Debería terminar con lo siguiente:

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

Si la instancia se instaló desde la interfaz de usuario, se abrirá automáticamente una ventana del explorador y también se abrirá una ventana de la aplicación de escritorio que mostrará el host y el puerto de la instancia y un conmutador de encendido/apagado:

![pantalla de inicio](assets/screen_shot_.png)

>[!NOTE]
>
>Si está utilizando enlaces simbólicos, consulte [problemas con symlink](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### Inicio y parada {#starting-and-stopping}

Una vez AEM se ha desempaquetado y se ha iniciado por primera vez, haciendo doble clic en el archivo jar en el directorio de instalación simplemente inicia la instancia, no la reinstala.

Para detener la instancia desde la GUI, simplemente haga clic en el botón **encendido/apagado** en la ventana de la aplicación de escritorio.

También puede detener e iniciar AEM desde la línea de comandos. Suponiendo que ya haya instalado la instancia por primera vez, la variable **scripts de línea de comandos** se encuentran aquí:

**`<aem-install>/crx-quickstart/bin/`**

Esta carpeta contiene los siguientes scripts de shell de bash de Unix:

* **`start`**: Inicia la instancia
* `stop`: Detiene la instancia
* **`status`**: Informa del estado de la instancia
* **`quickstart`**: Se utiliza para configurar la información de inicio, si es necesario.

También hay equivalentes **`bat`** para Windows. Para obtener información más detallada, consulte:

* [Línea de comandos: start y stop](/help/sites-deploying/command-line-start-and-stop.md)

AEM inicia y redirige automáticamente el explorador web a la página adecuada, normalmente la página de inicio de sesión; por ejemplo:

`https://localhost:4502/`

![pantalla de inicio de sesión](assets/screen_shot_2019-04-08at83533am.png)

Una vez que haya iniciado sesión, tendrá acceso a AEM. Para obtener más información, según su función, consulte lo siguiente:

* [Creación](/help/sites-authoring/home.md)
* [Administración](/help/sites-administering/home.md)
* [Desarrollo de](/help/sites-developing/home.md)
* [Administración](/help/managing/best-practices.md)

## Implementación avanzada {#advanced-deployment}

La sección anterior debería proporcionarle una buena comprensión de los conceptos básicos de AEM instalación. Sin embargo, la instalación de un sistema completo de producción de AEM puede implicar una complejidad considerablemente mayor. Para obtener información completa sobre la instalación avanzada, consulte las siguientes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalación independiente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Instalación del servidor de aplicaciones](/help/sites-deploying/application-server-install.md)
* [Solución de problemas](/help/sites-deploying/troubleshooting.md)
* [Línea de comandos: start y stop](/help/sites-deploying/command-line-start-and-stop.md)
* [Configurar](/help/sites-deploying/configuring.md)
* [Actualización a AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Artículos de procedimientos de configuración](/help/sites-deploying/ht-deploy.md)
* [Consola web](/help/sites-deploying/web-console.md)
* [Solución de problemas de replicación](/help/sites-deploying/troubleshoot-rep.md)
* [Prácticas recomendadas](/help/sites-deploying/best-practices.md)
* [Implementación de comunidades](/help/communities/deploy-communities.md)
* [Introducción a la plataforma AEM](/help/sites-deploying/platform.md)
* [Directrices de rendimiento](/help/sites-deploying/performance-guidelines.md)
* [Introducción a AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [¿Qué es AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=es)
