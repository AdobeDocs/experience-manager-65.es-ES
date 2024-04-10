---
title: Implementación y mantenimiento
description: AEM Obtenga información sobre cómo empezar con la instalación de la.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 5%

---

# Implementación y mantenimiento{#deploying-and-maintaining}

En esta página encontrará:

* [Conceptos básicos](#basic-concepts)

   * [AEM ¿Qué es la?](#what-is-aem)
   * [Implementaciones habituales](#typical-deployment-scenarios)

      * [On-Premise](#on-premise)
      * [Managed Services con Cloud Manager](#managed-services-using-cloud-manager)

* [Introducción](#getting-started)

   * [Requisitos previos](#prerequisites)
   * [Obtención del software](#getting-the-software)
   * [Instalación local predeterminada](#default-local-install)
   * [Instalaciones de creación y publicación](#author-and-publish-installs)
   * [Directorio de instalación desempaquetado](#unpacked-install-directory)
   * [Inicio y detención](#starting-and-stopping)

Una vez que se haya familiarizado con estos conceptos básicos, encontrará información más avanzada y detallada en las siguientes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalación independiente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Instalación del servidor de aplicaciones](/help/sites-deploying/application-server-install.md)
* [Solución de problemas](/help/sites-deploying/troubleshooting.md)
* [Inicio y parada de la línea de comandos](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuración](/help/sites-deploying/configuring.md)
* [AEM Actualización a 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Artículos sobre procedimientos de configuración](/help/sites-deploying/ht-deploy.md)
* [Consola web](/help/sites-deploying/web-console.md)
* [Solución de problemas de replicación](/help/sites-deploying/troubleshoot-rep.md)
* [Prácticas recomendadas](/help/sites-deploying/best-practices.md)
* [Implementación de comunidades](/help/communities/deploy-communities.md)
* [AEM Introducción a la plataforma de](/help/sites-deploying/platform.md)
* [Directrices de rendimiento](/help/sites-deploying/performance-guidelines.md)
* [Introducción a AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [¿Qué es AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=es)

## Conceptos básicos {#basic-concepts}

### AEM ¿Qué es la? {#what-is-aem}

Adobe Experience Manager es un sistema cliente-servidor basado en la web para crear, administrar e implementar sitios web comerciales y servicios relacionados. Combina varias funciones de nivel de infraestructura y de nivel de aplicación en un único paquete integrado.

AEM A nivel de infraestructura, proporciona lo siguiente:

* **Servidor de aplicaciones web** AEM : se puede implementar en modo independiente (incluye un servidor web Jetty integrado) o como aplicación web dentro de un servidor de aplicaciones de terceros.
* **Marco de aplicación web** AEM : incorpora el marco de trabajo de la aplicación web Sling, que simplifica la escritura de aplicaciones web RESTful orientadas a contenido.
* **Repositorio de contenido** AEM : incluye un repositorio de contenido Java™ (JCR), un tipo de base de datos jerárquica diseñada específicamente para datos no estructurados y semiestructurados. El repositorio almacena no solo el contenido orientado al usuario, sino también todo el código, las plantillas y los datos internos utilizados por la aplicación.

AEM Partiendo de esta base, también ofrece varias funciones de nivel de aplicación para la gestión de:

* **Sitios web**
* **Aplicaciones móviles**
* **Publicaciones digitales**
* **Forms y documentos**
* **Recursos digitales**
* **Communities**
* **Comercio en línea**

Por último, los clientes pueden utilizar estos componentes básicos de infraestructura y de nivel de aplicación para crear soluciones personalizadas mediante la creación de aplicaciones propias.

AEM El servidor de la es **Basado en Java** y se ejecuta en la mayoría de los sistemas operativos compatibles con esa plataforma. AEM Toda la interacción del cliente con el cliente se realiza a través de un **explorador web**.

>[!NOTE]
>
>La función Adaptive Forms AEM, disponible en QuickStart de la versión 6.5 de la versión, está diseñada únicamente para fines de exploración y evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms, ya que la funcionalidad Formularios adaptables requiere una licencia adecuada.

### Escenarios de implementación habituales {#typical-deployment-scenarios}

AEM AEM En la terminología de la, una &quot;instancia&quot; es una copia de la que se ejecuta en un servidor. AEM Las instalaciones suelen incluir al menos dos instancias, que suelen ejecutarse en equipos separados:

* **Autor**: la instancia de AEM utilizada para crear, cargar y editar contenido y administrar el sitio web. Una vez que el contenido está listo para su publicación, se replica en la instancia de publicación.
* **Publish** AEM : Instancia de que sirve el contenido publicado al público.

Estas instancias son idénticas en términos de software instalado. Solo se diferencian por la configuración. Además, la mayoría de las instalaciones utilizan un Dispatcher:

* **Dispatcher**: Un servidor web estático (Apache httpd, MicrosoftAEM ® IIS, etc.) ampliado con el módulo de Dispatcher de. Almacena en la caché las páginas web producidas por la instancia de publicación para mejorar el rendimiento.

Existen muchas opciones y elaboraciones avanzadas de esta configuración, pero el patrón básico de creación, publicación y Dispatcher es el núcleo de la mayoría de las implementaciones. Empecemos por centrarnos en una configuración simple. A continuación se describen las opciones de implementación avanzadas.

Las secciones siguientes describen ambos casos:

* **On-Premise** AEM : implementado y administrado en su entorno corporativo.

* **Managed Services: Cloud Manager para Adobe Experience Manager** AEM : implementado y administrado por Adobe Managed Services.

### On-Premise {#on-premise}

AEM Puede instalar los servidores de en su entorno corporativo de. Las instancias de instalación habituales incluyen: entornos de desarrollo, pruebas y publicación. Consulte [Primeros pasos](/help/sites-deploying/deploy.md#getting%20started) AEM para obtener detalles básicos sobre cómo obtener el software de la para instalarlo localmente.

Para obtener más información sobre las implementaciones locales típicas, consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md).

### Managed Services con Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services es una solución completa para la administración de experiencias digitales. Proporciona las ventajas de la solución de entrega de experiencias en la nube, al tiempo que conserva todas las ventajas de control, seguridad y personalización de una implementación On-Premise. AEM Managed Services permite a los clientes iniciar más rápido mediante la implementación en la nube y también basándose en las prácticas recomendadas y la asistencia desde el Adobe. Las organizaciones y los usuarios empresariales pueden atraer a los clientes en un tiempo mínimo, aumentar la cuota de mercado y centrarse en la creación de campañas de marketing innovadoras, al tiempo que reducen la carga para la TI.

AEM Con Managed Services, los clientes pueden obtener las siguientes ventajas:

**Tiempo de comercialización más rápido:** Con la infraestructura de nube flexible de Adobe Managed Services, las organizaciones pueden planificar, iniciar y optimizar rápidamente experiencias digitales exitosas. Adobe administra la arquitectura en la nube sin necesidad de capital, hardware ni software adicionales. Los ingenieros de soluciones para clientes de Adobe AEM le ayudarán con la arquitectura, el aprovisionamiento y la personalización de la conexión a las aplicaciones back-end, así como con las prácticas recomendadas de lanzamiento.

**Mayor rendimiento:** Proporciona experiencias digitales fiables para su empresa con cuatro opciones de disponibilidad de servicios: 99,5 %, 99,9 %, 99,95 % y 99,99 %. Además, permite realizar copias de seguridad automáticas y modelos de recuperación ante desastres multimodo para garantizar la fiabilidad y la gestión de contingencias.

**Costes de TI optimizados:** AEM La orientación proactiva y la experiencia ayudan a las organizaciones a mantenerse al día con la última versión de los programas de trabajo de la. Adobe El mantenimiento y la asistencia Platinum se incluyen automáticamente en las nuevas implementaciones de AMS Enterprise/Basic, ofreciendo experiencia técnica y operativa para ayudar a las organizaciones a mantener sus aplicaciones esenciales. Las funciones básicas gratuitas de Analytics o Target ofrecen un valor adicional, especialmente para organizaciones de mercado medio con necesidades limitadas de análisis y personalización.

**Máxima seguridad:** Garantiza la seguridad física, de red y de datos de nivel empresarial al alojar aplicaciones de clientes en una instalación de acceso restringido, detrás de sistemas de firewall o dentro de una nube privada virtual. Incluye máquinas virtuales de un solo inquilino con cifrado de almacenamiento de datos robusto, antivirales y aislamiento de datos.

**Cloud Manager**: Cloud Manager, parte de la oferta de Adobe Experience Manager Managed Services es un portal de autoservicio que permite a las organizaciones autoadministrar Adobe Experience Manager en la nube. Incluye una canalización de integración continua y entrega continua (CI/CD) de última generación que permite a los equipos de TI y a los asociados de la implementación acelerar la entrega de las personalizaciones o actualizaciones sin poner en riesgo el rendimiento o la seguridad. Cloud Manager solo está disponible para los clientes de Adobe Managed Service.

Para obtener más información sobre Cloud Manager y sus recursos, consulte [**Guía del usuario de Cloud Manager**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=es).

## Introducción {#getting-started}

### Requisitos previos {#prerequisites}

Mientras que las instancias de producción se ejecutan en equipos dedicados que ejecutan un sistema operativo oficialmente admitido (consulte [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)), el servidor de Experience Manager se ejecutará en cualquier sistema que admita [**Java™ Standard Edition 8**](https://www.oracle.com/java/technologies/downloads/#java8).

AEM Con fines de familiarización y para desarrollar en el tiempo de ejecución, es común utilizar una instancia instalada en su equipo local que ejecute Apple OS X o versiones de escritorio de Microsoft® Windows o Linux®.

AEM En el lado del cliente, funciona con todos los exploradores modernos (**Microsoft® Edge**, **Internet Explorer** 11, **Chrome **51+** **, **Firefox **47+, **Safari** 8+) en sistemas operativos de escritorio y tableta. Consulte [Plataformas de cliente compatibles](/help/sites-deploying/technical-requirements.md#supported-client-platforms) para obtener más información.

### Obtención del software {#getting-the-software}

AEM Los clientes con un contrato de mantenimiento y asistencia válido deberían haber recibido una notificación por correo electrónico con un código y poder descargar los datos de la aplicación de forma gratuita desde el sitio web de [**Sitio web de licencias de Adobe**](https://licensing.adobe.com/). Los socios comerciales pueden solicitar acceso de descarga desde [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

AEM El paquete de software de la está disponible de dos formas:

* **cq-quickstart-6.5.0.jar:** Un ejecutable independiente *jarra* que incluye todo lo que necesita para ponerse en marcha.

* **cq-quickstart-6.5.0.war:** A *guerra* para su implementación en un servidor de aplicaciones de terceros.

En la siguiente sección describimos el **instalación independiente**. AEM Para obtener más información sobre la instalación de la aplicación en un servidor de aplicaciones, consulte [Instalación del servidor de aplicaciones](/help/sites-deploying/application-server-install.md).

### Instalación local predeterminada {#default-local-install}

1. Cree un directorio de instalación en el equipo local. Por ejemplo:

   Ubicación de instalación de UNIX®: **/opt/aem**

   Ubicación de instalación de Windows: **`C:\Program Files\aem`**

   Del mismo modo, es común instalar instancias de ejemplo en una carpeta directamente en el escritorio. En cualquier caso, Adobe se refiere a esta ubicación genéricamente como:

   `<aem-install>`

   *La ruta del directorio de archivos sólo debe contener caracteres ASCII de EE.UU.*

1. Coloque el **jarra** y **licencia** archivos de este directorio:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Si no proporciona un `license.properties` AEM , redirecciona el explorador a un archivo de **Bienvenido** pantalla al inicio, donde puede introducir una clave de licencia. Debe solicitar una clave de licencia válida desde el Adobe si todavía no la tiene.

1. Para iniciar la instancia en un entorno GUI, haga doble clic en **`cq-quickstart-6.5.0.jar`** archivo.

   AEM Como alternativa, puede iniciar la ejecución de desde la línea de comandos de:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM El archivo jar tarda unos minutos en desempaquetarse, instalarse e iniciarse. El procedimiento anterior resulta en lo siguiente:

* un **AEM autor de la** instancia
* ejecución en **localhost**
* en el puerto **4502**

Para acceder a la instancia, dirija su explorador a:

**`https://localhost:4502`**

El resultado en la instancia de autor se configurará automáticamente para conectarse a una **instancia de publicación** el **`localhost:4503`**.

### Instalaciones de creación y publicación {#author-and-publish-installs}

La instalación predeterminada (un **autor** instancia en **`localhost:4502`**) se puede cambiar simplemente cambiando el nombre del `jar` antes de iniciarlo por primera vez. El patrón de nomenclatura es:

**`cq-<instance-type>-p<port-number>.jar`**

Por ejemplo, cambiar el nombre del archivo a

**`cq-author-p4502.jar`**

Al iniciarlo, se ejecuta una instancia de autor en **`localhost:4502`**.

Del mismo modo, cambiar el nombre del archivo e iniciarlo

**`cq-publish-p4503.jar`**

Se ejecuta una instancia de publicación en **`localhost:4503`**.

Instalaría estas dos instancias en, por ejemplo

`<aem-install>/author`y

**`<aem-install>/publish`**

Para obtener más información sobre cómo personalizar la instalación, consulte lo siguiente:

* [Instalación independiente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Ejecutar modos](/help/sites-deploying/configure-runmodes.md)

### Directorio de instalación desempaquetado {#unpacked-install-directory}

Cuando se inicia quickstart jar por primera vez, se desempaqueta en el mismo directorio bajo un nuevo subdirectorio llamado `crx-quickstart`. Debe tener lo siguiente:

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

Si la instancia se instaló desde la interfaz de usuario de, se abrirá automáticamente una ventana del explorador y una ventana de aplicación de escritorio que también mostrará el host y el puerto de la instancia y un conmutador de activación/desactivación:

![pantalla de inicio](assets/screen_shot_.png)

>[!NOTE]
>
>Si utiliza enlaces simbólicos, eche un vistazo a [problemas con symlink](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### Inicio y detención {#starting-and-stopping}

AEM Una vez que se ha desempaquetado a sí mismo y se ha iniciado por primera vez, al hacer doble clic en el archivo jar en el directorio de instalación simplemente se inicia la instancia, no se vuelve a instalar.

Para detener la instancia desde la GUI, haga clic en **activado/desactivado** encienda la ventana de la aplicación de escritorio.

AEM También puede detener e iniciar la ejecución de los comandos desde la línea de comandos de. Si ya ha instalado la instancia por primera vez, la variable **scripts de línea de comandos** están aquí:

**`<aem-install>/crx-quickstart/bin/`**

Esta carpeta contiene los siguientes scripts de shell bash de UNIX®:

* **`start`**: inicia la instancia
* `stop`: detiene la instancia
* **`status`**: informa del estado de la instancia
* **`quickstart`**: se utiliza para configurar la información de inicio, si es necesario.

También hay equivalentes **`bat`** archivos para Windows. Para obtener información más detallada, consulte:

* [Inicio y parada de la línea de comandos](/help/sites-deploying/command-line-start-and-stop.md)

AEM Se inicia la sesión y redirige automáticamente el explorador web a la página adecuada, normalmente la página de inicio de sesión; por ejemplo:

`https://localhost:4502/`

![pantalla de inicio de sesión](assets/screen_shot_2019-04-08at83533am.png)

AEM Una vez que haya iniciado sesión, tendrá acceso a la interfaz de usuario de. Para obtener más información, según su función, consulte lo siguiente:

* [Creación](/help/sites-authoring/first-steps.md)
* [Administración](/help/sites-administering/home.md)
* [El desarrollo de](/help/sites-developing/getting-started.md)
* [Administración](/help/managing/best-practices.md)

## Implementación avanzada {#advanced-deployment}

AEM La sección anterior le proporcionará una buena comprensión de los conceptos básicos de la instalación de la. AEM Sin embargo, la instalación de un sistema de producción completo de la puede implicar considerablemente más complejidad. Para obtener una cobertura completa de la instalación avanzada, consulte las siguientes subpáginas:

* [Requisitos técnicos](/help/sites-deploying/technical-requirements.md)
* [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md)
* [Instalación independiente personalizada](/help/sites-deploying/custom-standalone-install.md)
* [Instalación del servidor de aplicaciones](/help/sites-deploying/application-server-install.md)
* [Solución de problemas](/help/sites-deploying/troubleshooting.md)
* [Inicio y parada de la línea de comandos](/help/sites-deploying/command-line-start-and-stop.md)
* [Configuración](/help/sites-deploying/configuring.md)
* [AEM Actualización a 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Artículos sobre procedimientos de configuración](/help/sites-deploying/ht-deploy.md)
* [Consola web](/help/sites-deploying/web-console.md)
* [Solución de problemas de replicación](/help/sites-deploying/troubleshoot-rep.md)
* [Prácticas recomendadas](/help/sites-deploying/best-practices.md)
* [Implementación de comunidades](/help/communities/deploy-communities.md)
* [AEM Introducción a la plataforma de](/help/sites-deploying/platform.md)
* [Directrices de rendimiento](/help/sites-deploying/performance-guidelines.md)
* [Introducción a AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [¿Qué es AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=es)
