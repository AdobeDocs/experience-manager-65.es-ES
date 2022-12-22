---
title: Requisitos técnicos
seo-title: Technical Requirements
description: Una lista de las plataformas de cliente y servidor compatibles para AEM.
seo-description: A list of the supported client and server platforms for AEM.
content-type: reference
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: e8026cb0c7de3b1c903bf95dc31e567076e837eb
workflow-type: tm+mt
source-wordcount: '3488'
ht-degree: 3%

---

# Requisitos técnicos{#technical-requirements}

Adobe es compatible con Adobe Experience Manager (AEM) en las plataformas tal como se detalla en la siguiente información de este documento.

Para cualquier problema relacionado específicamente con la plataforma, póngase en contacto con el proveedor de la plataforma.

>[!NOTE]
>
>Según la plataforma en la que instale AEM, podría haber diferentes conjuntos de requisitos para la administración de usuarios.

## Requisitos previos {#prerequisites}

Requisitos mínimos para instalar Adobe Experience Manager:

* Java Platform instalado, Standard Edition JDK u otro soporte [Máquinas virtuales Java](#java-virtual-machines)
* Archivo de inicio rápido del Experience Manager (JAR independiente o WAR de implementación de aplicaciones web)

### Requisitos mínimos de tamaño {#minimum-sizing-requirements}

Requisitos mínimos para ejecutar Adobe Experience Manager:

* 5 GB de espacio libre en disco en el directorio de instalación
* 2 GB de memoria

>[!NOTE]
>
>* Los casos de uso de recursos digitales necesitan más memoria base. Consulte [Implementación y mantenimiento](/help/sites-deploying/deploy.md#default-local-install) para obtener más información.
>* [Paquete de complementos de AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) requiere 15 GB de espacio temporal.
>


Para obtener más información, consulte la [Pautas para el tamaño del hardware](/help/managing/hardware-sizing-guidelines.md).

### Niveles de compatibilidad {#support-levels}

Este documento enumera las plataformas de cliente y servidor compatibles con Adobe Experience Manager. Adobe proporciona varios niveles de soporte, tanto para configuraciones recomendadas como para otras configuraciones.

### Configuraciones admitidas {#supported-configurations}

Adobe recomienda estas configuraciones y proporciona soporte completo como parte del acuerdo de mantenimiento de software estándar.

<table>
 <tbody>
  <tr>
   <td>Nivel de soporte</td>
   <td>Descripción<br /> </td>
  </tr>
  <tr>
   <td><strong>A: Admitido</strong></td>
   <td>Adobe proporciona soporte y mantenimiento completos para esta configuración. Esta configuración está cubierta por el proceso de garantía de calidad del Adobe.</td>
  </tr>
  <tr>
   <td><strong>R: Compatibilidad restringida</strong></td>
   <td>Para garantizar el éxito del proyecto de nuestros clientes, Adobe proporciona soporte completo dentro de un programa de soporte restringido, que requiere que se cumplan condiciones específicas. El soporte de nivel R requiere una solicitud formal del cliente y confirmación por parte del Adobe. Para obtener más información, póngase en contacto con el servicio de atención al cliente de Adobe.</td>
  </tr>
 </tbody>
</table>

### Configuraciones no admitidas {#unsupported-configurations}

| Nivel de soporte | Descripción |
|---|---|
| **Z: No admitido** | La configuración no es compatible. Adobe no realiza ninguna declaración sobre si la configuración funciona o no y no la admite. |

## Plataformas compatibles {#supported-platforms}

### Máquinas virtuales Java {#java-virtual-machines}

La aplicación requiere una máquina virtual Java para ejecutarse, que proporciona la distribución Java Development Kit (JDK) .

Adobe Experience Manager funciona con las siguientes versiones de las máquinas virtuales Java:

>[!CAUTION]
>
>Se recomienda realizar un seguimiento de los boletines de seguridad del proveedor de Java para garantizar la seguridad de los entornos de producción e instalar las últimas actualizaciones de Java.

| **Plataforma** | **Nivel de soporte** | **Vincular** |
|---|---|---|
| Oracle Java SE 11 JDK - 64 bits | A: Admitido `[1]` | [Descargar](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| Oracle Java SE 10 JDK | Z: No admitido `[1]` |
| Oracle Java SE 9 JDK | Z: No admitido `[1]` |
| Oracle Java SE 8 JDK - 64 bits | A: Admitido `[1]` | [Descargar](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM J9 VM: versión 2.9, JRE 1.8.0 | A: Admitido `[2]` |
| IBM J9 VM: versión 2.8, JRE 1.8.0 | A: Admitido `[2]` |
| Azul Zulu OpenJDK 11 - 64 bits | A: Admitido `[3]` |  |
| Azul Zulu OpenJDK 8 - 64 bits | A: Admitido `[3]` |  |

1. Oracle ha adoptado un modelo de soporte a largo plazo (LTS) para los productos Oracle Java SE. Java 9, Java 10 y Java 12 son versiones no LTS por Oracle (consulte [Plan de soporte de Oracle Java SE](https://www.oracle.com/technetwork/java/eol-135779.html)). Para implementar AEM en el entorno de producción, Adobe solo ofrece soporte para las versiones LTS de Java. El soporte técnico y la distribución del Oracle Java SE JDK, incluidas todas las actualizaciones de mantenimiento de las versiones LTS más allá del final de las actualizaciones públicas, serán compatibles directamente con el Adobe para todos los clientes AEM que utilicen la tecnología Oracle Java SE. Consulte la [Política de soporte de Java para Adobe Experience Manager](assets/Java_Policy_for_Adobe_Experience_Manager.pdf) para obtener más información.


1. IBM JRE solo es compatible con el servidor de aplicaciones WebSphere.

1. Las versiones LTS de Azul Zulu OpenJDK son compatibles con implementaciones de AEM locales a partir de la versión 6.5 SP9. El soporte y la distribución de las versiones de Azul Zulu JDK LTS deben ser licenciadas directamente desde Azul por nuestros clientes.


### Almacenamiento y persistencia {#storage-persistence}

Existen varias opciones para implementar el repositorio de Adobe Experience Manager. Consulte la siguiente lista para ver las tecnologías compatibles y las opciones de almacenamiento.

| **Plataforma** | **Descripción** | **Nivel de soporte** |
|---|---|---|
| **Sistema de archivos con archivos TAR** `[1]` | Repositorio | A: Admitido |
| **Sistema de archivos con almacén de datos** `[1]` | Binarios | A: Admitido |
| Almacenar binarios en archivos TAR en el sistema de archivos `[1]` | Binarios | Z: No compatible con la producción |
| Amazon S3 | Binarios | A: Admitido |
| Almacenamiento del Blob de Microsoft Azure | Binarios | A: Admitido |
| MongoDB Enterprise 4.2 | Repositorio | A: Admitido `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | Repositorio | Z: No admitido |
| MongoDB Enterprise 3.6 | Repositorio | Z: No admitido |
| MongoDB Enterprise 3.4 | Repositorio | Z: No admitido |
| IBM DB2 10.5 | Base de datos de repositorio y Forms | R: Compatibilidad restringida `[5]` |
| Base de datos de oracle 12c (12.1.x) | Base de datos de repositorio y Forms | R: Compatibilidad restringida |
| Microsoft SQL Server 2016 | Base de datos de Forms | A: Admitido |
| **Apache Lucene (integrado de Quickstart)** | Servicio de búsqueda | A: Admitido |
| Apache Solr | Servicio de búsqueda | A: Admitido |

1. &#39;File System&#39; incluye almacenamiento en bloque compatible con POSIX. Esto incluye la tecnología de almacenamiento en red. Tenga en cuenta que el rendimiento del sistema de archivos puede variar e influir en el rendimiento general. Se recomienda cargar AEM de prueba en combinación con el sistema de archivos de red/remoto.
1. MongoDB Enterprise 4.2 requiere AEM 6.5 SP9 como mínimo.
1. El uso compartido MongoDB no es compatible con AEM.
1. Sólo se admite el motor de almacenamiento MongoDB WiredTiger.
1. Compatible con los clientes de actualización de AEM Forms. No es compatible con las nuevas instalaciones.

>[!NOTE]
>
>Consulte [Implementación de comunidades](/help/communities/deploy-communities.md) para obtener información adicional sobre la capacidad de AEM Communities.

>[!NOTE]
>
>MongoDB es software de terceros y no está incluido en el paquete de licencias de AEM. Para obtener más información, consulte [Política de licencias de MongoDB](https://www.mongodb.org/about/licensing/) página.
>
>Para aprovechar al máximo su implementación de AEM con MongoDB, Adobe recomienda licenciar la versión de MongoDB Enterprise para beneficiarse del soporte profesional. Consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) para obtener más información.
>
>La licencia incluye un conjunto de réplicas estándar, que consta de una instancia principal y dos instancias secundarias que pueden utilizarse para el autor o para las implementaciones de publicación.
>
>En caso de que desee ejecutar la creación y la publicación en MongoDB, se deben adquirir dos licencias independientes.
>
>El Servicio de atención al cliente de Adobe ayudará a calificar los problemas relacionados con el uso de MongoDB con AEM.
>
>Para obtener más información, consulte la [Página MongoDB para Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
>
>Las bases de datos relacionales compatibles que se enumeran anteriormente son software de terceros y no se incluyen en el paquete de licencias de AEM.
>
>Para ejecutar AEM 6.5 con una base de datos relacional admitida, se requiere un contrato de soporte independiente con un proveedor de base de datos. El Servicio de atención al cliente de Adobe ayudará a calificar los problemas relacionados con el uso de bases de datos relacionales con AEM 6.5.
>
>**Actualmente, la mayoría de las bases de datos relacionales son compatibles con Level-R en la AEM 6.5, que incluye criterios de soporte y un programa de soporte, como se indica en la descripción de Level-R anterior.**

### Motores Servlet / Servidores de aplicaciones {#servlet-engines-application-servers}

Adobe Experience Manager puede ejecutarse como servidor independiente (el archivo JAR de inicio rápido) o como aplicación web dentro de un servidor de aplicaciones de terceros (el archivo WAR).

La versión mínima de la API de servlet necesaria es Servlet 3.1

| Plataforma | Nivel de soporte |
|---|---|
| **Motor Servlet integrado de inicio rápido (Jetty 9.4)** | A: Admitido |
| Oracle WebLogic Server 12.2 (12cR2) | Z: No admitido |
| Entrega continua del servidor de aplicaciones IBM WebSphere (LibertyProfile) con perfil web 7.0 y IBM JRE 1.8 | R: Compatibilidad restringida para nuevos contratos `[2]` |
| IBM WebSphere Application Server 9.0 y IBM JRE 1.8 | R: Compatibilidad restringida para nuevos contratos `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: Compatibilidad restringida para nuevos contratos `[2]` |
| JBoss EAP 7.2.x con el servidor de aplicaciones JBoss | Z: No admitido |
| JBoss EAP 7.1.4 con servidor de aplicaciones JBoss | R: Compatibilidad restringida para nuevos contratos `[1]` `[2]` |
| JBoss EAP 7.0.x con el servidor de aplicaciones JBoss | Z: No admitido |

1. Recomendado para implementaciones con AEM Forms.
1. A partir de las implementaciones de AEM 6.5 en los servidores de aplicaciones, se cambia a Compatibilidad restringida. Los clientes existentes pueden actualizar a AEM 6.5 y seguir utilizando servidores de aplicaciones. Para los nuevos clientes, viene con criterios de asistencia y un programa de asistencia, como se indica en la descripción de nivel R anterior.

### Sistemas operativos del servidor {#server-operating-systems}

Adobe Experience Manager funciona con las siguientes plataformas de servidor para entornos de producción:

| **Plataforma** | **Nivel de soporte** |
|---|---|
| **Linux, basado en la distribución de Red Hat** | A: Admitido `[1]` `[3]` |
| Linux, basado en la distribución de Debian incl. Ubuntu | A: Admitido `[1]` `[2]` |
| Linux, basado en la distribución SUSE | A: Admitido `[1]` |
| Microsoft Windows Server 2019 `[4]` | R: Compatibilidad restringida para nuevos contratos `[5]` |
| Microsoft Windows Server 2016 `[4]` | R: Compatibilidad restringida para nuevos contratos `[5]` |
| Microsoft Windows Server 2012 R2 | Z: No admitido |
| Oracle Solaris 11 | Z: No admitido |
| IBM AIX 7.2 | Z: No admitido |

1. Linux Kernel 2.6, 3.x, 4.x y 5.x incluye derivados de la distribución de Red Hat, incluyendo Red Hat Enterprise Linux, CentOS, Oracle Linux y Amazon Linux. Las funciones de complementos de AEM Forms solo son compatibles con CentOS 7, Red Hat Enterprise Linux 7 y Red Hat Enterprise Linux 8.
1. AEM Forms es compatible con Ubuntu 20.04 LTS.
1. Distribución de Linux compatible con Adobe Managed Services.
1. Las implementaciones de producción de Microsoft Windows son compatibles con los clientes que actualizan a la versión 6.5 y con el uso que no es de producción. Las nuevas implementaciones se encuentran bajo solicitud para AEM Sites y Assets.
1. AEM Forms es compatible con Microsoft Window Server sin las restricciones de nivel de soporte R.


### Entornos de computación virtual y en la nube {#virtual-cloud-computing-environments}

Adobe Experience Manager es compatible con la ejecución en una máquina virtual en entornos de computación en la nube, como Microsoft Azure y Amazon Web Service (AWS), de acuerdo con los requisitos técnicos enumerados en esta página y según los términos de asistencia estándar de Adobe.

Para un entorno nativo de la nube, revise la última oferta de la línea de productos AEM: Adobe Experience Manager as a Cloud Service. Consulte [Documentación de Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=en) para obtener más información.

Adobe también ofrece Adobe Managed Services para implementar AEM en Azure o AWS. Adobe Managed Services proporciona a los expertos experiencia y habilidades para implementar y operar AEM en estos entornos de computación en la nube. Consulte [documentación adicional sobre Adobe Managed Services](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).

En todos los demás casos de implementación de AEM en Azure o AWS, o en cualquier otro entorno de computación en nube, la compatibilidad con Adobe se contendrá en el entorno de computación virtual de acuerdo con las especificaciones técnicas enumeradas en esta página. Cualquier problema informado relativo a AEM que se ejecute en cualquiera de estos entornos de nube tendrá que ser reproducible de forma independiente de cualquier servicio de nube específico para el entorno de computación en nube, a menos que el servicio de nube sea compatible específicamente como parte de los requisitos técnicos enumerados en esta página, por ejemplo, almacenamiento Azure Blob o AWS S3.

Para obtener recomendaciones sobre cómo implementar AEM en Azure o AWS, fuera de Adobe Managed Services, Adobe recomienda trabajar directamente con el proveedor de nube o los socios de Adobe que admitan la implementación de AEM en el entorno de nube que elija. El proveedor o socio de nube seleccionado será responsable de las especificaciones de tamaño, el diseño y la implementación de la arquitectura, para satisfacer sus requisitos específicos de rendimiento, carga, escalabilidad y seguridad.

### Plataformas de Dispatcher (servidores web) {#dispatcher-platforms-web-servers}

Dispatcher es el componente de almacenamiento en caché y equilibrio de carga. [Descargar la última versión de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html). Experience Manager 6.5 requiere la versión 4.3.2 o superior de Dispatcher.

Los siguientes servidores web son compatibles para su uso con Dispatcher versión 4.3.2:

| Plataforma | Nivel de soporte |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: Admitido |
| Microsoft IIS 10 (Servidor de información de Internet) | A: Admitido |
| Microsoft IIS 8.5 (Servidor de información de Internet) | Z: No admitido |

1. Los servidores web creados sobre la base del código fuente httpd de Apache tendrán el mismo nivel de compatibilidad que la versión de httpd en la que se basa. En caso de duda, pida al Adobe que confirme el nivel de asistencia relacionado con el producto del servidor correspondiente. Los siguientes casos:

   1. El servidor HTTP se creó utilizando solamente las distribuciones de fuentes oficiales de Apache, o
   1. El servidor HTTP se entregó como parte del sistema operativo en el que se está ejecutando. Ejemplos: Servidor HTTP de IBM, servidor HTTP de Oracle

1. Dispatcher no está disponible para Apache 2.4.x para sistemas operativos Windows.

## Plataformas de cliente compatibles {#supported-client-platforms}

### Exploradores admitidos para la creación de la interfaz de usuario {#supported-browsers-for-authoring-user-interface}

La interfaz de usuario de Adobe Experience Manager funciona con las siguientes plataformas de cliente. Todos los exploradores se prueban con el conjunto predeterminado de complementos.

La interfaz de usuario de AEM está optimizada para pantallas más grandes (normalmente portátiles y equipos de escritorio) y factor de forma de tableta (como Apple iPad o Microsoft Surface). No se admite el factor de formulario telefónico.

>[!NOTE]
>
>**Compatibilidad con exploradores con ciclos de versiones rápidos:**
>
>Mozilla Firefox, Google Chrome y Microsoft Edge se actualizan cada pocos meses. Adobe se compromete a proporcionar actualizaciones para Adobe Experience Manager para mantener el nivel de asistencia que se indica a continuación con las próximas versiones de estos navegadores.

<table>
 <tbody>
  <tr>
   <td><strong>Explorador</strong></td>
   <td><strong>Compatibilidad con la interfaz de usuario<br /> </strong></td>
   <td><strong>Compatibilidad con la IU clásica</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (Evergreen)</strong></td>
   <td>A: Admitido</td>
   <td>A: Admitido</td>
  </tr>
  <tr>
   <td>Microsoft Edge (Evergreen)</td>
   <td>A: Admitido</td>
   <td>A: Admitido</td>
  </tr>
  <tr>
   <td>Microsoft Internet Explorer 11</td>
   <td>Z: No admitido</td>
   <td>Z: No admitido</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A: Admitido</td>
   <td>A: Admitido</td>
  </tr>
  <tr>
   <td>Mozilla Firefox último ESR [1]</td>
   <td>A: Admitido</td>
   <td>A: Admitido</td>
  </tr>
  <tr>
   <td>Apple Safari en macOS (Evergreen)</td>
   <td>A: Admitido</td>
   <td>A: Admitido</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x en macOS</td>
   <td>Z: No admitido</td>
   <td>Z: No admitido</td>
  </tr>
  <tr>
   <td>Apple Safari en iOS 12.x</td>
   <td>A: Admitido [2]</td>
   <td>Z: No admitido</td>
  </tr>
  <tr>
   <td>Apple Safari en iOS 11.x</td>
   <td>Z: No admitido</td>
   <td>Z: No admitido</td>
  </tr>
 </tbody>
</table>

1. Versión ampliada de soporte de Firefox [Más información sobre esto en mozilla.org](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. compatibilidad con Apple iPad

### Exploradores admitidos para sitios web {#supported-browsers-for-websites}

Por lo general, la compatibilidad del explorador con los sitios web procesados por AEM Sites depende de la implementación de AEM plantillas de página, el diseño y la salida de componentes, y por lo tanto controla a la parte que implementa estas partes.

### Clientes de WebDAV {#webdav-clients}

**Microsoft Windows 7+**

Para conectarse correctamente con Microsoft Windows 7+ a una instancia de AEM que no esté segura con SSL, la autenticación básica sobre una red no segura debe estar habilitada en Windows. Esto requiere un cambio en el Registro de Windows de WebClient:

1. Busque la subclave del Registro:

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Agregue la entrada de registro BasicAuthLevel a esta subclave con un valor de 2 o más.

Para mejorar la capacidad de respuesta del cliente WebDav en Windows, consulte [Compatibilidad con Microsoft KB 2445570](https://support.microsoft.com/kb/2445570)

## Notas adicionales de la plataforma {#additional-platform-notes}

Esta sección proporciona notas especiales e información más detallada sobre la ejecución de Adobe Experience Manager y sus complementos.

### IPv4 e IPv6 {#ipv-and-ipv}

Todos los elementos de Adobe Experience Manager (instancia, Dispatcher) se pueden instalar en redes IPv4 e IPv6.

La operación es perfecta, ya que no se requiere ninguna configuración especial. Puede simplemente especificar una dirección IP utilizando el formato apropiado para su tipo de red, si es necesario.

Esto significa que, cuando se debe especificar una dirección IP, se puede seleccionar (según sea necesario) de:

* una dirección IPv6, por ejemplo `https://[ab12::34c5:6d7:8e90:1234]:4502`

* una dirección IPv4, por ejemplo `https://123.1.1.4:4502`

* un nombre de servidor, por ejemplo, `https://www.yourserver.com:4502`

* el caso predeterminado de `localhost` por ejemplo, se interpretará para las instalaciones de red IPv4 e IPv6, `https://localhost:4502`

### Requisitos para AEM complemento de Dynamic Media {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media está desactivado de forma predeterminada. Consulte aquí para [habilitar Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

Con Dynamic Media habilitado, se aplican los siguientes requisitos técnicos adicionales.

>[!NOTE]
>
>Estos requisitos del sistema **only** se aplica si utiliza Dynamic Media en modo híbrido; Dynamic Media - El modo híbrido tiene un servidor de imágenes integrado, que solo está certificado en determinados sistemas operativos.
>
>Para los clientes de Dynamic Media que ejecutan Dynamic Media: modo Scene7 (es decir, **dynamic_media_scene7** runmode), no hay requisitos adicionales del sistema; solo los mismos requisitos del sistema que AEM. Dynamic Media: la arquitectura del modo Scene7 utiliza el servicio de imagen basado en la nube y no el servicio incrustado en AEM.

#### Hardware {#hardware}

Los siguientes requisitos de hardware son aplicables tanto para Linux como para Windows:

* CPU Intel Xeon o AMD Opteron con al menos 4 núcleos
* Al menos, 16 GB de RAM

#### Linux {#linux}

Si utiliza Dynamic Media en Linux, deben cumplirse los siguientes requisitos previos:

* RedHat Enterprise 7 o CentOS 7 y posteriores con los parches de correcciones más recientes
* Sistema operativo de 64 bits
* Intercambio desactivado (recomendado)
* SELinux deshabilitado (ver nota a continuación)

>[!NOTE]
>
>Si la configuración regional está definida de tal modo que LC_CTYPE no sea igual a `en_US.UTF-8`, impide que Dynamic Media funcione. Para ver cuál es su valor, escriba &quot;locale&quot; en el símbolo del sistema. Si no se establece en eso, entonces establezca la variable de entorno LC_CTYPE en la cadena vacía escribiendo &quot;export LC_CTYPE=&quot; antes de ejecutar AEM.

>[!NOTE]
>
>**Desactivación de SELinux:** Image Serving no funciona con SELinux activado. Esta opción está activada de forma predeterminada. Para solucionar este problema, edite la **/etc/selinux/config** y cambie el valor SELinux de:
>
>`SELINUX=enforcing` **hasta** `SELINUX=disabled`

>[!NOTE]
>
>**Arquitectura NUMA:** Los sistemas con procesadores AMD64 e Intel EM64T suelen configurarse como plataformas de arquitectura de memoria no uniforme (NUMA), lo que significa que el núcleo construye varios nodos de memoria en el momento del inicio en lugar de construir un solo nodo de memoria.
>
>La construcción de varios nodos puede provocar el agotamiento de la memoria en uno o varios nodos antes de que otros se agoten. Cuando ocurre el agotamiento de la memoria, el núcleo puede decidir matar procesos (por ejemplo, Image Server o Platform Server) aunque haya memoria disponible.
>
>Por lo tanto, Adobe recomienda que, si está ejecutando un sistema de este tipo, desactive NUMA mediante el **numa=off** para evitar que el núcleo mate estos procesos.

>[!NOTE]
>
>**El nombre de host del servidor debe resolver:** Asegúrese de que el nombre de host del servidor se puede resolver en una dirección IP. Si no es posible, añada el nombre de host completo y la dirección IP a **/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* Intercambiar espacio igual a al menos el doble de la memoria física (RAM)

Para usar Dynamic Media en Windows, instale Microsoft Visual Studio 2010, 2013 y 2015 redistribuibles para x64 y x86.

Para Windows x64:

* Obtenga Microsoft Visual Studio 2010 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/en-us/download/details.aspx?id=13523)
* Obtenga Microsoft Visual Studio 2013 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Obtenga Microsoft Visual Studio 2015 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Para Windows x86:

* Obtenga Microsoft Visual Studio 2010 redistribuible en [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)
* Obtenga Microsoft Visual Studio 2013 redistribuible en [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Obtenga Microsoft Visual Studio 2015 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x y posteriores
* Solo se admite con fines de prueba y demostración

### Requisitos del Generador de PDF de AEM Forms {#requirements-for-aem-forms-pdf-generator}

### Soporte de software para Generador de PDF {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Producto</strong></p> </th>
   <th><p><strong>Formatos compatibles para la conversión a PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Seguimiento clásico de Acrobat 2020</a> última versión</td>
   <td>XPS, formatos de imagen (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF y DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Seguimiento clásico de Acrobat 2017</a> versión más reciente (obsoleta)</td>
   <td>XPS, formatos de imagen (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF y DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF y TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016 (obsoleto)</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF y TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016 (obsoleto)<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016 (obsoleto)<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Proyecto Microsoft® 2016 (obsoleto)<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX,formatos de imagen (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM RTF, y TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2 (obsoleto)</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX,formatos de imagen (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM RTF, y TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator solo admite versiones en alemán, francés, inglés y japonés de los sistemas operativos y aplicaciones compatibles.
>
>Además:
>
>* El generador de PDF requiere una versión de 32 bits de [Acrobat 2020 Classic track versión 20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) o Acrobat 2017 versión 17.011.30078 para realizar la conversión.
>* Las conversiones de PDF Generator para OpenOffice solo son compatibles con Windows y Linux.
>* PDF Generator solo admite la versión comercial de 32 bits de Microsoft Office Professional Plus y otro software necesario para la conversión en el sistema operativo Windows.
>* PDF Generator es compatible con las versiones de 32 y 64 bits de OpenOffice en el sistema operativo Linux.
>* El Generador de PDF no es compatible con Microsoft Office 365.
>* Las características de PDF, Optimize PDF y Export PDF de OCR solo son compatibles con Windows.
>* Una versión de Acrobat se incluye con AEM Forms para habilitar la funcionalidad de Generador de PDF. Solo se debe acceder a la versión agrupada mediante programación con AEM Forms, durante el período de licencia de AEM Forms, para su uso con el Generador de PDF de AEM Forms. Para obtener más información, consulte la descripción del producto de AEM Forms según la implementación ([On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) o [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))
>* El servicio Generador de PDF no es compatible con Microsoft Windows 10.
>* El Generador de PDF no puede convertir archivos con Microsoft Visio 2019. Puede seguir utilizando Microsoft Visio 2016 para convertir archivos .VSD y .VSDX.
>* El Generador de PDF no puede convertir archivos mediante Microsoft Project 2019. Puede seguir utilizando Microsoft Project 2016 para convertir archivos .VSD y .VSDX.
>


### Requisitos de AEM Forms Designer {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server o Microsoft® Windows® 10
* Procesador de 1 GHz o más rápido con soporte para PAE, NX y SSE2.
* 1 GB de RAM para 32 bits o 2 GB de RAM para SO de 64 bits;
* 16 GB de espacio en disco para 32 o 20 GB de espacio en disco para SO de 64 bits
* Memoria gráfica: 128 MB de GPU (se recomiendan 256 MB);
* 2,35 GB de espacio disponible en disco duro;
* 1024 X 768 píxeles de resolución de monitor o superior;
* Aceleración de hardware de vídeo (opcional);
* Acrobat Pro DC, Acrobat Standard DC o Adobe Acrobat Reader DC;
* Privilegios administrativos para instalar Designer.

### Requisitos para la reescritura de metadatos de AEM Assets XMP {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP reescritura es compatible y está habilitada para las siguientes plataformas y formatos de archivo:

* **Sistemas operativos:**

   * Linux (compatibilidad con aplicaciones de 32 y 32 bits en sistemas de 64 bits). Para ver los pasos para instalar bibliotecas de cliente de 32 bits, consulte [Cómo habilitar la extracción y escritura de XMP en RedHat Linux de 64 bits](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * Mac OS X (64 bits)

* **Formatos de archivo**: JPEG, PNG, TIFF, PDF, INDD, AI y EPS.

### Requisitos para que AEM Assets procese recursos con gran cantidad de metadatos en Linux {#assetsonlinux}

El proceso XMPFilesProcessor requiere que funcione la biblioteca GLIBC_2.14. Utilice un núcleo Linux que contenga GLIBC_2.14, por ejemplo Linux kernel versión 3.1.x. Mejora el rendimiento para el procesamiento de recursos que contienen una gran cantidad de metadatos, como archivos de PSD. El uso de una versión anterior de GLIBC da lugar a errores en los registros que comienzan por `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
