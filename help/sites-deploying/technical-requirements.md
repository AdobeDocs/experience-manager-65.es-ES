---
title: Requisitos técnicos
seo-title: Requisitos técnicos
description: Una lista de las plataformas de cliente y servidor admitidas para AEM.
seo-description: Una lista de las plataformas de cliente y servidor admitidas para AEM.
uuid: 597f8fc1-9ac7-458d-a7c1-f576dd0f189b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 16c7a97d-884a-447e-9aad-18a2db1bda1d
docset: aem65
translation-type: tm+mt
source-git-commit: 7065a6b984afb18c188acd848b9b77da7da67749
workflow-type: tm+mt
source-wordcount: '3118'
ht-degree: 1%

---


# Requisitos técnicos{#technical-requirements}

Adobe admite Adobe Experience Manager (AEM) en las plataformas como se detalla en la siguiente información de este documento.

Para cualquier problema relacionado específicamente con la plataforma, póngase en contacto con el proveedor de la plataforma.

>[!NOTE]
>
>Según la plataforma en la que instale AEM, podría haber diferentes conjuntos de requisitos para la administración de usuarios.

## Requisitos previos {#prerequisites}

Requisitos mínimos para instalar Adobe Experience Manager:

* Java Platform instalado, Standard Edition JDK u otros [Máquinas virtuales Java](#java-virtual-machines) admitidos
* Archivo de inicio rápido Experience Manager (JAR independiente o WAR de implementación de aplicaciones web)

### Requisitos mínimos de tamaño {#minimum-sizing-requirements}

Requisitos mínimos para ejecutar Adobe Experience Manager:

* 5 GB de espacio libre en disco en el directorio de instalación
* 2 GB de memoria

>[!NOTE]
>
>* Los casos de uso de recursos digitales necesitan más memoria básica. Consulte [Implementación y mantenimiento](/help/sites-deploying/deploy.md#default-local-install) para obtener más información.
>* [AEM Forms Add-on ](/help/forms/using/installing-configuring-aem-forms-osgi.md) Packager requiere 15 GB de espacio temporal.

>



Para obtener más información, consulte las [Directrices de cambio de tamaño de hardware](/help/managing/hardware-sizing-guidelines.md).

### Niveles de soporte {#support-levels}

Este documento lista las plataformas de cliente y servidor admitidas para Adobe Experience Manager. Adobe proporciona varios niveles de soporte, tanto para configuraciones recomendadas como para otras configuraciones.

### Configuraciones admitidas {#supported-configurations}

Adobe recomienda estas configuraciones y proporciona soporte completo como parte del acuerdo de mantenimiento de software estándar.

<table>
 <tbody>
  <tr>
   <td>Nivel de asistencia</td>
   <td>Descripción<br /> </td>
  </tr>
  <tr>
   <td><strong>A: Admitido</strong></td>
   <td>Adobe proporciona soporte y mantenimiento completos para esta configuración. Esta configuración está cubierta por el proceso de garantía de calidad del Adobe.</td>
  </tr>
  <tr>
   <td><strong>R: Compatibilidad restringida</strong></td>
   <td>Para garantizar el éxito de los proyectos de nuestros clientes, Adobe proporciona soporte completo dentro de un programa de soporte restringido, que requiere que se cumplan condiciones específicas. El soporte de nivel R requiere una solicitud formal del cliente y confirmación por Adobe. Para obtener más información, póngase en contacto con el Servicio de atención al cliente de Adobe.</td>
  </tr>
 </tbody>
</table>

### Configuraciones no admitidas {#unsupported-configurations}

| Nivel de asistencia | Descripción |
|---|---|
| **Z: No admitido** | No se admite la configuración. Adobe no hace ninguna declaración sobre si la configuración funciona o no y no la admite. |

## Plataformas compatibles {#supported-platforms}

### Máquinas virtuales Java {#java-virtual-machines}

La aplicación requiere una máquina virtual Java para ejecutarse, que se proporciona mediante la distribución Java Development Kit (JDK).

Adobe Experience Manager funciona con las siguientes versiones de las máquinas virtuales Java:

>[!CAUTION]
>
>Se recomienda rastrear los boletines de seguridad del proveedor de Java para garantizar la seguridad de los entornos de producción e instalar las últimas actualizaciones de Java.

<table>
 <tbody>
  <tr>
   <td>Plataforma</td>
   <td>Nivel de asistencia</td>
  </tr>
  <tr>
   <td>Oracle Java SE 12 JDK [1]</td>
   <td>Z: No admitido </td>
  </tr>
  <tr>
   <td><strong>Oracle Java SE 11 JDK - 64 bits</strong></td>
   <td>A: Admitido</td>
  </tr>
  <tr>
   <td>Oracle Java SE 10 JDK [1]</td>
   <td>Z: No admitido </td>
  </tr>
  <tr>
   <td>Oracle Java SE 9 JDK [1]</td>
   <td>Z: No admitido</td>
  </tr>
  <tr>
   <td>Oracle Java SE 8 JDK - 64 bits</td>
   <td>A: Admitido [3]</td>
  </tr>
  <tr>
   <td>IBM J9 VM - compilación 2.9, JRE 1.8.0 [2]</td>
   <td>A: Admitido</td>
  </tr>
  <tr>
   <td>IBM J9 VM - compilación 2.8, JRE 1.8.0 [2]</td>
   <td>A: Admitido</td>
  </tr>
 </tbody>
</table>

1. Oracle ha adoptado un modelo de soporte a largo plazo (LTS) para los productos Oracle Java SE. Java 9, Java 10 y Java 12 son versiones no LTS de Oracle (consulte [Guía de soporte de Oracle Java SE](https://www.oracle.com/technetwork/java/eol-135779.html)). Para implementar AEM en el entorno de producción, Adobe solo ofrece soporte para las versiones LTS de Java.

1. IBM JRE sólo se admite junto con WebSphere Application Server.
1. El soporte y la distribución del JDK Java SE de Oracle, incluidas todas las actualizaciones de mantenimiento de las versiones LTS más allá del final de las actualizaciones públicas, serán soportados directamente por Adobe para todos los clientes AEM que utilicen la tecnología Oracle Java SE. Consulte la [compatibilidad con Java de Oracle para Adobe Experience Manager Q&amp;A](assets/adobe-oracle-java-license-agreement.pdf) para obtener más información.

### Almacenamiento y persistencia {#storage-persistence}

Existen varias opciones para implementar el repositorio de Adobe Experience Manager. Consulte la siguiente lista para ver las opciones de almacenamiento y las tecnologías admitidas.

| **Plataforma** | **Descripción** | **Nivel de asistencia** |
|---|---|---|
| **Sistema de archivos con archivos TAR** `[1]` | Repositorio | A: Admitido |
| **Sistema de archivos con Almacén de datos** `[1]` | Binarios | A: Admitido |
| Almacenar archivos binarios en archivos TAR en el sistema de archivos `[1]` | Binarios | Z: No compatible con la producción |
| Amazon S3 | Binarios | A: Admitido |
| Almacenamiento de blob de Microsoft Azure | Binarios | A: Admitido |
| MongoDB Enterprise 4.0 | Repositorio | A: Compatible con `[2, 3]` |
| MongoDB Enterprise 3.6 | Repositorio | Z: No admitido |
| MongoDB Enterprise 3.4 | Repositorio | Z: No admitido |
| IBM DB2 10.5 | Repositorio y base de datos de Forms | R: Soporte restringido `[4]` |
| Base de datos oracle 12c (12.1.x) | Repositorio y base de datos de Forms | R: Compatibilidad restringida |
| Microsoft SQL Server 2016 | Base de datos de Forms | A: Admitido |
| **Apache Lucene (integrado de Quickstart)** | Servicio de búsqueda | A: Admitido |
| Apache Solr | Servicio de búsqueda | A: Admitido |

1. &#39;File System&#39; incluye el almacenamiento de bloques que es compatible con POSIX. Esto incluye la tecnología de almacenamiento de red. Tenga en cuenta que el rendimiento del sistema de archivos puede variar e influir en el rendimiento general. Se recomienda cargar AEM de prueba en combinación con el sistema de archivos de red/remoto.
1. El uso compartido de MongoDB no se admite en AEM.
1. Solo se admite el motor de Almacenamiento MongoDB WiredTiger.
1. Compatible con clientes de actualización de AEM Forms. No compatible con las nuevas instalaciones.

>[!NOTE]
>
>Consulte [Implementación de comunidades](/help/communities/deploy-communities.md) para obtener información adicional acerca de la capacidad de AEM Communities.

>[!NOTE]
>
>MongoDB es un software de terceros y no está incluido en el paquete de licencias de AEM. Para obtener más información, consulte la página [Política de licencias de MongoDB](https://www.mongodb.org/about/licensing/).
>
>Para aprovechar al máximo su implementación AEM con MongoDB, Adobe recomienda que se le otorgue la licencia de la versión empresarial MongoDB para beneficiarse de la asistencia profesional. Consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) para obtener más información.
>
>La licencia incluye un conjunto de réplicas estándar, compuesto por una instancia primaria y dos instancias secundarias que se pueden usar para la implementación de publicación o del autor.
>
>Si desea ejecutar tanto la creación como la publicación en MongoDB, deberá adquirir dos licencias independientes.
>
>El Servicio de atención al cliente de Adobe asistirá en los problemas de calificación relacionados con el uso de MongoDB con AEM.
>
>Para obtener más información, consulte la página [MongoDB para Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
>
>Las bases de datos relacionales admitidas, como se indica anteriormente, son software de terceros y no se incluyen en el paquete de licencias de AEM.
>
>Para ejecutar AEM 6.5 con una base de datos relacional admitida, se requiere un contrato de soporte independiente con un proveedor de base de datos. El Servicio de atención al cliente de Adobe asistirá en los problemas de calificación relacionados con el uso de bases de datos relacionales con AEM 6.5.
>
>**La mayoría de las bases de datos relacionales se admiten actualmente en Level-R en AEM 6.5, que incluye criterios de soporte y un programa de soporte, como se indica en la descripción de Level-R anterior.**

### Motores de servlet / Servidores de aplicaciones {#servlet-engines-application-servers}

Adobe Experience Manager puede ejecutarse como servidor independiente (el archivo JAR de inicio rápido) o como aplicación web dentro de un servidor de aplicaciones de terceros (el archivo WAR).

Se requiere una versión mínima de la API de servlet para Servlet Servlet 3.1

| Plataforma | Nivel de asistencia |
|---|---|
| **Motor Servlet integrado de arranque rápido (Jetty 9.4)** | A: Admitido |
| Oracle WebLogic Server 12.2 (12cR2) | Z: No admitido |
| ENVÍO continuo (LibertyProfile) de Application Server para IBM WebSphere con Web Perfil 7.0 e IBM JRE 1.8 | R: Soporte restringido para nuevos contratos `[2]` |
| IBM WebSphere Application Server 9.0 e IBM JRE 1.8 | R: Soporte restringido para nuevos contratos `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: Soporte restringido para nuevos contratos `[2]` |
| JBoss EAP 7.2.x con el servidor de aplicaciones JBoss | Z: No admitido |
| JBoss EAP 7.1.4 con el servidor de aplicaciones JBoss | R: Soporte restringido para nuevos contratos `[1]` `[2]` |
| JBoss EAP 7.0.x con el servidor de aplicaciones JBoss | Z: No admitido |

1. Recomendado para implementaciones con AEM Forms.
1. A partir de las implementaciones de AEM 6.5 en los servidores de aplicaciones, se cambia a Soporte restringido. Los clientes existentes pueden actualizar a AEM 6.5 y seguir utilizando servidores de aplicaciones. Para los nuevos clientes viene con criterios de asistencia y un programa de asistencia, como se indica en la descripción de nivel R anterior.

### Sistemas operativos de servidor {#server-operating-systems}

Adobe Experience Manager funciona con las siguientes plataformas de servidor para entornos de producción:

| **Plataforma** | **Nivel de asistencia** |
|---|---|
| **Linux, basado en la distribución de Red Hat** | A: Compatible con `[1]` `[3]` |
| Linux, basado en la distribución Debian incl. Ubuntu | A: Compatible con `[2]` |
| Linux, basado en la distribución SUSE | A: Admitido |
| Microsoft Windows Server 2019 `[4]` | R: Compatibilidad restringida para nuevos contratos |
| Microsoft Windows Server 2016 `[4]` | R: Soporte restringido para nuevos contratos `[5]` |
| Microsoft Windows Server 2012 R2 | Z: No admitido |
| Oracle Solaris 11 | Z: No admitido |
| IBM AIX 7.2 | Z: No admitido |

1. Linux Kernel 2.6, 3.x y 4.x incluye derivados de la distribución de Red Hat, incluyendo Red Hat Enterprise Linux, CentOS, Oracle Linux y Amazon Linux. Las funciones adicionales de AEM Forms solo son compatibles con CentOS 7 y Red Hat Enterprise Linux 7.
1. AEM Forms solo es compatible con Ubuntu 16.04 LTS
1. Distribución de Linux admitida por Adobe Managed Services
1. Las implementaciones de producción de Microsoft Windows son compatibles con los clientes que actualizan a 6.5 y con el uso sin producción. Las nuevas implementaciones se realizan bajo petición para AEM Sites y Assets.
1. AEM Forms es compatible con Microsoft Windows Server sin las restricciones de Support-Level R

### Entornos de informática virtual y de nube {#virtual-cloud-computing-environments}

Adobe Experience Manager es compatible con la ejecución en una máquina virtual en entornos informáticos en la nube, como Microsoft Azure y Amazon Web Services (AWS), de acuerdo con los requisitos técnicos que se enumeran en esta página y según los términos de asistencia estándar de Adobe.

Adobe recomienda utilizar los servicios gestionados de Adobe para implementar AEM en Azure o AWS. Los servicios gestionados de Adobe proporcionan a los expertos experiencia y habilidades para implementar y operar AEM en estos entornos de cloud computing. Consulte [documentación adicional sobre los servicios administrados de Adobe](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).

En todos los demás casos de implementación de AEM en Azure o AWS, o en cualquier otro entorno de computación en nube, la compatibilidad con Adobe se contendrá en el entorno de cómputo virtual de conformidad con las especificaciones técnicas enumeradas en esta página. Cualquier problema informado relacionado con AEM que se ejecute en cualquiera de estos entornos de nube deberá ser reproducible independientemente de cualquier servicio de nube específico del entorno de cloud computing, a menos que el servicio de nube sea específicamente compatible como parte de los requisitos técnicos enumerados en esta página, por ejemplo, Azure Blob almacenamiento o AWS S3.

Para obtener recomendaciones sobre cómo implementar AEM en Azure o AWS, fuera de los servicios gestionados de Adobe, Adobe recomienda trabajar directamente con el proveedor de nube o los socios de Adobe que admiten la implementación de AEM en el entorno en la nube de su elección. El proveedor o socio de nube seleccionado se encargará de las especificaciones de tamaño, el diseño y la implementación de la arquitectura. Para satisfacer sus requisitos específicos de rendimiento, carga, escalabilidad y seguridad.

### Plataformas Dispatcher (Servidores Web) {#dispatcher-platforms-web-servers}

Dispatcher es el componente de almacenamiento en caché y equilibrio de carga. [Descargue la última versión](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html) de Dispatcher. Experience Manager 6.5 requiere Dispatcher versión 4.3.2 o superior.

Se admiten los siguientes servidores web para su uso con Dispatcher versión 4.3.2:

| Plataforma | Nivel de asistencia |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: Admitido |
| Microsoft IIS 10 (Servidor de información de Internet) | A: Admitido |
| Microsoft IIS 8.5 (Servidor de información de Internet) | Z: No admitido |

1. Los servidores Web creados sobre la base del código fuente httpd Apache tendrán el mismo nivel de soporte que la versión de httpd en la que se basa. En caso de duda, pida al Adobe que confirme el nivel de asistencia relacionado con el producto del servidor correspondiente. Casos siguientes:

   1. El servidor HTTP se creó utilizando únicamente las distribuciones oficiales de fuentes Apache, o
   1. El servidor HTTP se entregó como parte del sistema operativo en el que se ejecuta. Ejemplos: Servidor HTTP IBM, servidor HTTP Oracle

1. Dispatcher no está disponible para Apache 2.4.x en sistemas operativos Windows.

## Plataformas de cliente admitidas {#supported-client-platforms}

### Exploradores admitidos para la creación de la interfaz de usuario {#supported-browsers-for-authoring-user-interface}

La interfaz de usuario de Adobe Experience Manager funciona con las siguientes plataformas de cliente. Todos los exploradores se prueban con el conjunto predeterminado de complementos.

La interfaz de usuario de AEM está optimizada para pantallas más grandes (normalmente portátiles y equipos de escritorio) y factor de forma de tablet (como Apple iPad o Microsoft Surface). No se admite el factor de formulario de teléfono.

>[!NOTE]
>
>**Compatibilidad con exploradores con ciclos de versión rápidos:**
>
>Mozilla Firefox, Google Chrome y Microsoft Edge se actualizan cada pocos meses. Adobe se ha comprometido a proporcionar actualizaciones para Adobe Experience Manager a fin de mantener el nivel de asistencia que se indica a continuación con las próximas versiones de estos exploradores.

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
   <td>Mozilla Firefox última ESR [1]</td>
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

1. Versión de soporte ampliado de Firefox [Más información sobre esto en mozilla.org](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. compatibilidad con Apple iPad

### Exploradores admitidos para sitios web {#supported-browsers-for-websites}

Por lo general, la compatibilidad de los navegadores con los sitios web procesados por AEM Sites depende de la implementación de plantillas de página AEM, diseño y salida de componentes, y por lo tanto controla a la parte que los implementa.

### Clientes WebDAV {#webdav-clients}

**Microsoft Windows 7+**

Para conectarse correctamente con Microsoft Windows 7+ a una instancia de AEM que no está segura con SSL, la autenticación básica a través de una red no segura debe estar habilitada en Windows. Esto requiere un cambio en el Registro de Windows de WebClient:

1. Busque la subclave del Registro:

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Añada la entrada del Registro BasicAuthLevel a esta subclave con un valor de 2 o más.

Para mejorar la capacidad de respuesta del cliente WebDav en Windows, consulte [Soporte técnico de Microsoft KB 2445570](https://support.microsoft.com/kb/2445570)

## Notas de plataforma adicionales {#additional-platform-notes}

Esta sección proporciona notas especiales e información más detallada sobre la ejecución de Adobe Experience Manager y sus complementos.

### IPv4 e IPv6 {#ipv-and-ipv}

Todos los elementos de Adobe Experience Manager (Instance, Dispatcher) se pueden instalar en redes IPv4 e IPv6.

La operación es fluida, ya que no se requiere ninguna configuración especial. Puede simplemente especificar una dirección IP utilizando el formato adecuado para su tipo de red, si es necesario.

Esto significa que cuando se necesita especificar una dirección IP, puede seleccionar (según sea necesario) de:

* una dirección IPv6
por ejemplo `https://[ab12::34c5:6d7:8e90:1234]:4502`

* una dirección IPv4
por ejemplo `https://123.1.1.4:4502`

* un nombre de servidor
por ejemplo, `https://www.yourserver.com:4502`

* el caso predeterminado de `localhost` se interpretará para las instalaciones de red IPv4 e IPv6
por ejemplo, `https://localhost:4502`

### Requisitos para el Añado de Dynamic Media AEM {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media está deshabilitado de forma predeterminada. Consulte aquí para [habilitar Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

Con Dynamic Media activado, se aplican los siguientes requisitos técnicos adicionales.

>[!NOTE]
>
>Estos requisitos del sistema **sólo** se aplican si utiliza Dynamic Media - modo híbrido; Medios dinámicos: el modo híbrido tiene un servidor de imágenes incrustado, que solo está certificado en determinados sistemas operativos.
>
>Para los clientes de Dynamic Media que ejecutan Dynamic Media - modo Scene7 (es decir, modo de ejecución **dynamicmedia_scene7**), no hay requisitos adicionales del sistema; solo los mismos requisitos del sistema que AEM. Medios dinámicos: la arquitectura del modo Scene7 utiliza el servicio de imágenes basado en la nube y no el servicio incrustado en AEM.

#### Hardware {#hardware}

Los siguientes requisitos de hardware son aplicables tanto para Linux como para Windows:

* CPU Intel Xeon o AMD Opteron con al menos 4 núcleos
* Al menos, 16 GB de RAM

#### Linux {#linux}

Si utiliza Dynamic Media en Linux, deben cumplirse los siguientes requisitos previos:

* RedHat Enterprise 7 o CentOS 7 y posterior con los parches de corrección más recientes
* Sistema operativo de 64 bits
* Intercambio deshabilitado (recomendado)
* SELinux deshabilitado (ver nota a continuación)

>[!NOTE]
>
>Si la configuración regional está configurada de manera que LC_CTYPE no sea igual a `en_US.UTF-8`, evita que Dynamic Media funcione. Para ver cuál es su valor, escriba &quot;locale&quot; en el símbolo del sistema. Si no se establece en eso, establezca la variable de entorno LC_CTYPE en la cadena vacía escribiendo &quot;export LC_CTYPE=&quot; antes de ejecutar AEM.

>[!NOTE]
>
>**Deshabilitar SELinux:** El servicio de imágenes no funciona con SELinux activado. Esta opción está activada de forma predeterminada. Para solucionar este problema, edite el archivo **/etc/selinux/config** y cambie el valor de SELinux de:
>
>`SELINUX=enforcing` **hasta** `SELINUX=disabled`

>[!NOTE]
>
>**Arquitectura NUMA:** Los sistemas con procesadores con AMD64 e Intel EM64T suelen configurarse como plataformas de arquitectura de memoria no uniforme (NUMA), lo que significa que el núcleo construye varios nodos de memoria en el momento del inicio en lugar de construir un solo nodo de memoria.
>
>La construcción de varios nodos puede resultar en agotamiento de la memoria en uno o más nodos antes de agotarse otros nodos. Cuando ocurre el agotamiento de la memoria, el núcleo puede decidir eliminar procesos (por ejemplo, el Servidor de imágenes o el Servidor de plataformas) aunque haya memoria disponible.
>
>Por lo tanto, Adobe recomienda que si está ejecutando un sistema de este tipo, desactive NUMA usando la opción de inicio **numa=off** para evitar que el núcleo mate estos procesos.

>[!NOTE]
>
>**El nombre de host del servidor debe resolverse:** asegúrese de que el nombre de host del servidor se puede resolver en una dirección IP. Si no es posible, agregue el nombre de host completo y la dirección IP a **/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* Intercambiar espacio igual al menos al doble de la cantidad de memoria física (RAM)

Para usar Dynamic Media en Windows, instale Microsoft Visual Studio 2010, 2013 y 2015 redistribuibles para x64 y x86.

Para Windows x64:

* Obtenga Microsoft Visual Studio 2010 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/en-us/download/details.aspx?id=13523)
* Obtenga Microsoft Visual Studio 2013 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Obtenga Microsoft Visual Studio 2015 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Para Windows x86:

* Obtenga Microsoft Visual Studio 2010 redistribuible en [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)
* Obtenga Microsoft Visual Studio 2013 redistribuible en [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Obtenga Microsoft Visual Studio 2015 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### MacOS {#macos}

* 10.9.x y posterior
* Solo se admite con fines de prueba y demostración

### Requisitos de AEM Forms PDF Generator {#requirements-for-aem-forms-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Producto</strong></p> </th>
   <th><p><strong>Formatos admitidos para la conversión a PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 Classic </a> trackversión más reciente</td>
   <td>XPS, formatos de imagen (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF y DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF y TXT</td>
  </tr>
  <tr>
   <td>WordPerfect X7</td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX,formatos de imagen (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, TF y TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator solo admite versiones en inglés, francés, alemán y japonés de los sistemas operativos y las aplicaciones compatibles.
>
>Además:
>
>* PDF Generator requiere una versión de 32 bits de [Acrobat 2017 Classic track versión 17.011.30078 o posterior](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) para realizar la conversión.
>* PDF Generator solo es compatible con la versión comercial de 32 bits de Microsoft Office Professional Plus y con otro software necesario para la conversión.
>* PDF Generator no admite Microsoft Office 365.
>* Las conversiones de PDF Generator para OpenOffice solo son compatibles con Windows y Linux.
>* Las funciones de OCR PDF, Optimize PDF y Export PDF solo son compatibles con Windows.
>* Una versión de Acrobat se incluye con AEM Forms para habilitar la funcionalidad de PDF Generator. Sólo se debe acceder a la versión compilada mediante programación con AEM Forms, durante el período de vigencia de la licencia de AEM Forms, para su uso con AEM Forms PDF Generator. Para obtener más información, consulte la descripción del producto de AEM Forms según su implementación ([local](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) o [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;

   >
   >
* El servicio Generator de PDF no admite Microsoft Windows 10.

>



### Requisitos para la escritura de metadatos de AEM Assets XMP {#requirements-for-aem-assets-xmp-metadata-write-back}

Se admite y activa la XMP de escritura en retorno para las plataformas y formatos de archivo siguientes:

* **Sistemas operativos:**

   * Linux (compatibilidad con aplicaciones de 32 y 32 bits en sistemas de 64 bits). Para ver los pasos para instalar bibliotecas de cliente de 32 bits, consulte [Cómo habilitar XMP extracción y escritura en versiones anteriores en RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) de 64 bits.

   * Windows Server
   * Mac OS X (64 bits)

* **Formatos** de archivo: JPEG, PNG, TIFF, PDF, INDD, AI y EPS.

### Requisitos para que AEM Assets procese activos con gran cantidad de metadatos en Linux {#assetsonlinux}

El proceso XMPFilesProcessor requiere que funcione la biblioteca GLIBC_2.14. Utilice un núcleo Linux que contenga GLIBC_2.14, por ejemplo, Linux kernel versión 3.1.x. Mejora el rendimiento para procesar recursos que contienen una gran cantidad de metadatos, como archivos PSD. El uso de una versión anterior de GLIBC produce un error en los registros que comienzan con `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
