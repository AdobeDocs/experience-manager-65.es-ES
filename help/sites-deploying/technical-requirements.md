---
title: Requisitos técnicos
description: Una lista de las plataformas de cliente y servidor compatibles con Adobe Experience Manager.
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 0dd6e3fc2fa9539e5c3ce4e99ab367752dfeaad6
workflow-type: tm+mt
source-wordcount: '3597'
ht-degree: 17%

---

# Requisitos técnicos{#technical-requirements}

Adobe Systems admite (AEM) Adobe Experience Manager en las plataformas, tal y como se detalla en la siguiente información de este documento.

Para cualquier problema relacionado con la plataforma, póngase en contacto con el proveedor de la plataforma.

>[!NOTE]
>
>AEM Dependiendo de la plataforma en la que instale la aplicación, puede haber diferentes conjuntos de requisitos para la administración de usuarios.

## Requisitos previos {#prerequisites}

Requisitos mínimos para instalar Adobe Experience Manager:

* Instalación de Platform Java, JDK Standard Edition u otras máquinas virtuales Java™™ compatibles [](#java-virtual-machines)
* Experience Manager Archivo de inicio rápido (JAR independiente o WAR de aplicación implementación web)

### Requisitos mínimos de tamaño {#minimum-sizing-requirements}

Requisitos mínimos para ejecutar Adobe Experience Manager:

* 5 GB gratuito espacio en disco en el directorio de instalación
* 2 GB de memoria

>[!NOTE]
>
>* Los casos de uso de recursos digitales necesitan más memoria base. Consulte [Implementación y mantenimiento](/help/sites-deploying/deploy.md#default-local-install) para obtener más información.
>* [Paquete de complemento de AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) requiere 15 GB de espacio temporal.
>

Para obtener más información, consulte la [Directrices de tamaño de hardware](/help/managing/hardware-sizing-guidelines.md).

### Niveles de soporte {#support-levels}

Este documento enumera las plataformas de cliente y servidor compatibles con Adobe Experience Manager. El Adobe de proporciona varios niveles de compatibilidad, tanto para las configuraciones recomendadas como para otras configuraciones.

### Configuraciones compatibles {#supported-configurations}

El Adobe recomienda estas configuraciones y proporciona soporte completo como parte del acuerdo de mantenimiento de software estándar.

<table>
 <tbody>
  <tr>
   <td>Nivel de soporte</td>
   <td>Descripción<br /> </td>
  </tr>
  <tr>
   <td><strong>A: Compatible</strong></td>
   <td>Adobe proporciona soporte y mantenimiento completos para esta configuración. Esta configuración está cubierta por el proceso de garantía de calidad de Adobe.</td>
  </tr>
  <tr>
   <td><strong>R: Compatibilidad restringida</strong></td>
   <td>Para garantizar el éxito del proyecto de los clientes, Adobe proporciona soporte completo dentro de un programa de soporte restringido, que requiere que se cumplan condiciones específicas. El soporte de nivel R requiere una solicitud formal del cliente y una confirmación por Adobe. Para obtener más información, póngase en contacto con el Servicio de atención al cliente de Adobe.</td>
  </tr>
 </tbody>
</table>

### Configuraciones no admitidas {#unsupported-configurations}

| Nivel de soporte | Descripción |
|---|---|
| **Z: No compatible** | La configuración no es compatible. El Adobe no hace declaraciones sobre si la configuración funciona o no y no la admite. |

## Plataformas compatibles {#supported-platforms}

### Java™ máquinas virtuales {#java-virtual-machines}

La aplicación requiere una máquina virtual Java™ para ejecutarse, que proporciona la distribución Java™ Development Kit (JDK).

Adobe Experience Manager funciona con las siguientes versiones de las máquinas virtuales Java™:

>[!CAUTION]
>
>Realice un seguimiento de los boletines de seguridad del proveedor de Java™. Al hacerlo, se garantiza la seguridad de los entornos de producción. Además, instale siempre las últimas actualizaciones de Java™.

| **Plataforma** | **Nivel de soporte** | **Vincular** |
|---|---|---|
| Oracle Java™ SE 17 JDK | Z: No compatible `[1]` |
| Oracle Java™ SE 11 JDK de 64 bits | A: Compatible `[1]` | [Descargar](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| Oracle Java™ SE 10 JDK | Z: No compatible `[1]` |
| Oracle Java™ SE 9 JDK | Z: No compatible `[1]` |
| Oracle Java™ SE 8 JDK de 64 bits | A: Compatible `[1]` | [Descargar](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| VM IBM® J9: versión 2.9, JRE 1.8.0 | A: Compatible `[2]` |
| VM IBM® J9: versión 2.8, JRE 1.8.0 | A: Compatible `[2]` |
| Azul Zulu OpenJDK 11 de 64 bits | A: Compatible `[3]` | |
| Azul Zulu OpenJDK 8 - 64 bits | A: Compatible `[3]` | |

1. Oracle ha adoptado un modelo de soporte a largo plazo (LTS) para los productos Oracle Java™ SE. Java 9, Java 10 y Java 12 son versiones no LTS de Oracle (consulte la hoja de ruta de soporte de Oracle Java™™™™ SE).](https://www.oracle.com/technetwork/java/eol-135779.html)[ AEM Para implementar en un entorno de producción, Adobe solo es compatible con las versiones LTS de Java™. El soporte y la distribución del Oracle Java™ SE JDK, incluidas todas las actualizaciones de mantenimiento de las versiones de LTS más allá del final de las actualizaciones públicas, es compatible con el Adobe AEM directamente para todos los clientes de que utilizan la tecnología de Oracle Java™ SE. Consulte la [Directiva de soporte de Java™ para Adobe Experience Manager](assets/Java_Policy_for_Adobe_Experience_Manager.pdf).
   **Importante: Oracle Java™ 11 es compatible hasta septiembre de 2026 como mínimo. Se está preparando la compatibilidad con Oracle Java™ 17.**

1. IBM® JRE sólo se da soporte junto con WebSphere® Application Server.

1. Las versiones Azul Zulu OpenJDK LTS son compatibles con implementaciones locales AEM a partir de la versión 6.5 SP9. El soporte y la distribución de las versiones de Azul Zulu JDK LTS deben ser licenciados directamente de Azul por Adobe Systems clientes.


### Almacenamiento y persistencia {#storage-persistence}

Existen varias opciones para implementar el repositorio de Adobe Experience Manager. Consulte los siguientes lista para conocer las tecnologías compatibles y las opciones de almacenamiento.

| **Plataforma** | **Descripción** | **Nivel de soporte** |
|---|---|---|
| **Sistema de archivos con archivos TAR** `[1]` | Repositorio | A: Compatible |
| **Sistema de archivos con almacén de datos** `[1]` | Binarios | A: Compatible |
| Almacenar binarios en archivos TAR en el sistema de archivos `[1]` | Binarios | Z: No compatible con la producción |
| Amazon S3 | Binarios | A: Compatible |
| Microsoft® Azure Blob Storage | Binarios | A: Compatible |
| MongoDB Enterprise 4.4 | Repositorio | A: Compatible `[2, 3, 4]` |
| MongoDB Enterprise 4.2 | Repositorio | A: Compatible `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | Repositorio | Z: No compatible |
| MongoDB Enterprise 3.6 | Repositorio | Z: No compatible |
| MongoDB Enterprise 3.4 | Repositorio | Z: No compatible |
| IBM® DB2® 10.5 | Repositorio y base de datos de Forms | R: Compatibilidad restringida `[5]` |
| Base de datos de oracle 12c (12.1.x) | Repositorio y base de datos de Forms | R: Compatibilidad restringida |
| Microsoft® SQL Server 2016 | Base de datos Forms | A: Compatible |
| **Apache Lucene (integrado en Quickstart)** | Servicio de búsqueda | A: Compatible |
| Apache Solr | Servicio de búsqueda | A: Compatible |

1. &quot;File System&quot; incluye almacenamiento en bloque compatible con POSIX. Incluye tecnología de almacenamiento en red. Tenga en cuenta que el rendimiento del sistema de archivos puede variar e influir en el rendimiento general. Cargue prueba AEM con el sistema de archivos de red o remoto.
1. Las versiones 4.2 y 4.4 de MongoDB Enterprise requieren AEM 6.5 SP9 como mínimo.
1. El uso compartido de MongoDB no es compatible con AEM.
1. El motor de almacenamiento MongoDB WiredTiger solo es compatible.
1. Compatible con los clientes de actualización de AEM Forms. No compatible con nuevas instalaciones.
1. Solo AEM Forms aplicable:
   * Se ha eliminado la compatibilidad con Oracle Database 12c y se ha añadido compatibilidad con Oracle Database 19c.
   * Se ha eliminado la compatibilidad con Microsoft SQL Server 2016 y se ha agregado compatibilidad con Microsoft®® SQL Server 2019.

>[!NOTE]
>
Consulte [Implementación de Communities](/help/communities/deploy-communities.md) para obtener información adicional sobre la capacidad AEM Communities.

>[!NOTE]
>
AEM MongoDB es un programa de software de terceros y no está incluido en el paquete de licencias de la. Para obtener más información, consulte la [Directiva de licencias de MongoDB](https://www.mongodb.com/licensing/server-side-public-license/faq) página.
>
AEM Para sacar el máximo partido a su implementación con MongoDB, Adobe recomienda licenciar la versión de MongoDB Enterprise para beneficiarse del soporte profesional. Consulte [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) para obtener más información.
>
La licencia incluye un conjunto de réplicas estándar, que está compuesto por una instancia principal y dos secundarias que se pueden utilizar para las implementaciones de autor o publicación.
>
Si desea ejecutar tanto la creación como la publicación en MongoDB, se deben adquirir dos licencias independientes.
>
Adobe Systems Servicio de atención al cliente asiste a los problemas de calificación relacionados con el uso de MongoDB con AEM.
>
Para obtener más información, consulte la [Página MongoDB para Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
>
Las bases de datos relacionales compatibles enumeradas anteriormente son terceros software y no se incluyen en el paquete de licencias AEM.
>
AEM Para ejecutar la versión 6.5 con una base de datos relacional compatible, se requiere un contrato de soporte independiente con un proveedor de la base de datos. El Servicio de atención al cliente de Adobe AEM ayuda a calificar los problemas relacionados con el uso de bases de datos relacionales con 6.5.
>
**AEM Actualmente, la mayoría de las bases de datos relacionales son compatibles con el nivel R de la versión 6.5, que viene con criterios de compatibilidad y un programa de asistencia, tal como se indica en la descripción del nivel R anterior.**

### Motores servlet/servidores de aplicaciones {#servlet-engines-application-servers}

Adobe Experience Manager se puede ejecutar como servidor independiente (el archivo JAR de inicio rápido) o como aplicación web dentro de un servidor de aplicaciones de terceros (el archivo WAR).

La versión mínima de la API de servlet requerida es Servlet 3.1

| Plataforma | Nivel de soporte |
|---|---|
| **Motor de servlet integrado de Quickstart (Jetty 9.4)** | A: Compatible |
| Oracle WebLogic Server 12.2 (12cR2) | Z: No compatible |
| IBM® WebSphere® Application Server Continuous Delivery (LibertyProfile) con Web Profile 7.0 y IBM® JRE 1.8 | R: Compatibilidad restringida con nuevos contratos `[2]` |
| IBM® WebSphere® Application Server 9.0 y IBM® JRE 1.8 | R: Compatibilidad restringida con nuevos contratos `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: Compatibilidad restringida con nuevos contratos `[2]` |
| JBoss® EAP 7.2.x con el servidor de aplicaciones JBoss® | Z: No compatible |
| JBoss® EAP 7.1.4 con el servidor de aplicaciones JBoss® | R: Compatibilidad restringida con nuevos contratos `[1]` `[2]` |
| JBoss® EAP 7.0.x con el servidor de aplicaciones JBoss® | Z: No compatible |

1. Recomendado para implementaciones con AEM Forms.
1. AEM Al iniciar implementaciones de 6.5 en servidores de aplicaciones, se pasa a Compatibilidad restringida. AEM Los clientes existentes pueden actualizar a la versión 6.5 de y seguir utilizando servidores de aplicaciones. Para nuevos clientes, incluye criterios de asistencia y un programa de asistencia, tal como se indica en la descripción del nivel R anterior.
1. Solo AEM Forms aplicable:
   * Se ha eliminado la compatibilidad con JBoss® EAP 7.1.4 y se ha agregado compatibilidad con JBoss® EAP 7.4.10.

### Sistemas operativos del servidor {#server-operating-systems}

Adobe Experience Manager funciona con las siguientes plataformas de servidor para entornos de producción:

| **Plataforma** | **Nivel de soporte** |
|---|---|
| **Linux®, basado en la distribución Red Hat®** | A: Compatible `[1]` `[3]` |
| Linux®, basado en la distribución Debian incl. Ubuntu | A: Compatible `[1]` `[2]` |
| Linux®, basado en la distribución SUSE® | A: Compatible `[1]` |
| Microsoft® Windows Server 2019 `[4]` | R: Compatibilidad restringida con nuevos contratos `[5]` |
| Microsoft® Windows Server 2016 `[4]` | R: Compatibilidad restringida con nuevos contratos `[5]` |
| Microsoft® Windows Server 2012 R2 | Z: No compatible |
| Oracle Solaris™ 11 | Z: No compatible |
| IBM® AIX® 7.2 | Z: No compatible |

1. Linux® Kernel 2.6, 3. x, 4. x, y 5. x incluye derivados de la distribución de Red Hat®, incluidos Red Hat® Enterprise Linux, CentOS, Oracle Linux y Amazon Linux®®®. AEM Forms funciones complementarias solo son compatibles con CentOS 7, Red Hat Enterprise Linux 7, Red Hat Enterprise Linux 8 y Red Hat®®® Enterprise Linux®®® 9.
1. AEM Forms es compatible con Ubuntu 20.04 LTS.
1. Distribución Linux® compatible con Adobe Managed Services.
1. Las implementaciones de producción de Microsoft® Windows son compatibles con los clientes que actualizan a la versión 6.5 y con el uso que no sea de producción. Las nuevas implementaciones se realizan bajo petición para AEM Sites y Assets.
1. AEM Forms es compatible con Microsoft® Window Server sin las restricciones R de nivel de soporte.
1. AEM Forms eliminó la compatibilidad con Microsoft® Windows Server 2016.

>[!NOTE]
>
Si va a instalar AEM Forms 6.5, asegúrese de que ha instalado el siguiente redistribuible de Microsoft® Visual C++ de 32 bits.
>
* Microsoft® Visual C++ 2008 redistribuible
* Microsoft® Visual C++ 2010 redistribuible
* Microsoft® Visual C++ 2012 redistribuible
* Microsoft® Visual C++ 2013 redistribuible
* Microsoft® Visual C++ 2019 (VC14.28 o superior) redistribuible



### Entornos de computación virtual y en la nube {#virtual-cloud-computing-environments}

Adobe Experience Manager es compatible con la ejecución en una máquina virtual en entornos de computación en la nube. Estos entornos incluyen, como Microsoft® Azure y Amazon Web Service (AWS), que se ejecutan de conformidad con los requisitos técnicos enumerados en esta página y según los términos de soporte estándar de Adobe.

AEM Para un entorno nativo de la nube, revise la oferta más reciente de la línea de productos de: Adobe Experience Manager as a Cloud Service. Consulte [Documentación de Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=en) para obtener más información.

Adobe también ofrece Managed Services AEM de Adobe para implementar en Azure o AWS la implementación de la implementación de la aplicación de forma. Adobe Managed Services AEM ofrece a los expertos la experiencia y los conocimientos necesarios para implementar y operar en estos entornos de computación en la nube (cloud computing) con el fin de realizar tareas de implementación y operación en estos entornos. Consulte [documentación adicional sobre Adobe Managed Services](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).

AEM En todos los demás casos de implementación de la aplicación en Azure o AWS, o en cualquier otro entorno de computación en la nube, la compatibilidad desde el Adobe se incluye en el entorno de computación virtual. Ese entorno virtual debe ejecutarse de acuerdo con las especificaciones técnicas enumeradas en esta página. AEM Cualquier problema informado relativo a la ejecución en cualquiera de estos entornos de nube debe ser reproducible independientemente de cualquier servicio de nube específico para el entorno de computación en nube. Es decir, a menos que el servicio en la nube sea compatible como parte de los requisitos técnicos enumerados en esta página, por ejemplo, almacenamiento del blob de Azure o AWS S3.

AEM Para obtener recomendaciones sobre cómo implementar en Azure o AWS, fuera de Adobe Managed Services, Adobe recomienda trabajar directamente con el proveedor de la nube. O bien, trabajar con socios de Adobe AEM que apoyen la implementación de la implementación de en el entorno de nube que elija. El proveedor o socio de nube seleccionado es responsable de las especificaciones de tamaño, el diseño y la implementación de la arquitectura, para satisfacer sus requisitos específicos de rendimiento, carga, escalabilidad y seguridad.

### Plataformas de Dispatcher (servidores web) {#dispatcher-platforms-web-servers}

Dispatcher es el componente de almacenamiento en caché y equilibrio de carga. [Descargue la última versión de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=en). Experience Manager 6.5 requiere la versión 4.3.2 o superior de Dispatcher.

Los siguientes servidores web son compatibles con la versión 4.3.2 de Dispatcher:

| Plataforma | Nivel de soporte |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: Compatible |
| Microsoft® IIS 10 (Internet Information Server) | A: Compatible |
| Microsoft® IIS 8.5 (Internet Information Server) | Z: No compatible |

1. Los servidores web creados en función del código fuente Apache httpd son tan compatibles como la versión de httpd en la que se basan. En caso de duda, pida al Adobe que confirme el nivel de asistencia relacionado con el producto del servidor correspondiente. Los casos siguientes:

   1. El servidor HTTP se creó utilizando solo distribuciones de origen oficiales de Apache, o
   1. El servidor HTTP se entregó como parte del sistema operativo en el que se está ejecutando. Ejemplos: IBM® HTTP Server, Servidor HTTP de Oracle

1. Dispatcher no está disponible para Apache 2.4.x para sistemas operativos Windows.

## Plataformas de cliente compatibles {#supported-client-platforms}

### Exploradores admitidos para la interfaz de usuario de creación {#supported-browsers-for-authoring-user-interface}

La interfaz de usuario de Adobe Experience Manager funciona con las siguientes plataformas de cliente. Todos los exploradores se prueban con el conjunto predeterminado de complementos y complementos.

AEM La interfaz de usuario de la aplicación está optimizada para pantallas más grandes (normalmente portátiles y equipos de escritorio) y para el formato de tableta (como Apple iPad o Microsoft® Surface). El factor de forma del teléfono no es compatible.

>[!NOTE]
>
**Compatibilidad con exploradores con ciclos de lanzamiento rápidos:**
>
Las versiones de Mozilla Firefox, Google Chrome y Microsoft® Edge se actualizan cada pocos meses. El Adobe de se compromete a proporcionar actualizaciones para Adobe Experience Manager a fin de mantener el nivel de compatibilidad que se indica a continuación con las próximas versiones de estos exploradores.

<table>
 <tbody>
  <tr>
   <td><strong>Explorador</strong></td>
   <td><strong>Compatibilidad con la IU de<br /> </strong></td>
   <td><strong>Compatibilidad con la IU clásica</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (Evergreen)</strong></td>
   <td>A: Compatible</td>
   <td>A: Compatible</td>
  </tr>
  <tr>
   <td>Microsoft® Edge (Evergreen)</td>
   <td>A: Compatible</td>
   <td>A: Compatible</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z: No compatible</td>
   <td>Z: No compatible</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A: Compatible</td>
   <td>A: Compatible</td>
  </tr>
  <tr>
   <td>Mozilla Firefox última ESR [1]</td>
   <td>A: Compatible</td>
   <td>A: Compatible</td>
  </tr>
  <tr>
   <td>Apple Safari en macOS (Evergreen)</td>
   <td>A: Compatible</td>
   <td>A: Compatible</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x en macOS</td>
   <td>Z: No compatible</td>
   <td>Z: No compatible</td>
  </tr>
  <tr>
   <td>Apple Safari en iOS 12.x</td>
   <td>A: Compatible [2]</td>
   <td>Z: No compatible</td>
  </tr>
  <tr>
   <td>Apple Safari en iOS 11.x</td>
   <td>Z: No compatible</td>
   <td>Z: No compatible</td>
  </tr>
 </tbody>
</table>

1. Lanzamiento de soporte ampliado de Firefox [Obtenga más información en mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/)
1. compatibilidad con Apple iPad

### Exploradores admitidos para sitios web {#supported-browsers-for-websites}

Por lo general, la compatibilidad del explorador con los sitios web procesados por AEM Sites AEM depende de la implementación de plantillas de página, diseño y salida de componente de la página de la aplicación, y, por lo tanto, está en el control de la parte que implementa estas partes.

### Clientes de WebDAV {#webdav-clients}

**Microsoft® Windows 7+**

Al conectarse con MicrosoftAEM ® Windows 7+ a una instancia de que no esté protegida con SSL, la autenticación básica a través de una red no segura debe habilitarse en Windows. Requiere un cambio en el Registro de Windows de WebClient:

1. Busque la subclave del Registro:

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Agregue la entrada de registro BasicAuthLevel a esta subclave con un valor de 2 o más.

## Notas Platform adicionales {#additional-platform-notes}

Esta sección proporciona notas especiales e información más detallada sobre la ejecución de Adobe Experience Manager y sus complementos.

### IPv4 e IPv6 {#ipv-and-ipv}

Todos los elementos de Adobe Experience Manager (Instance, Dispatcher) se pueden instalar en redes IPv4 e IPv6.

El funcionamiento es fluido, ya que no se requiere ninguna configuración especial. Si es necesario, especifique una dirección IP con el formato adecuado para el tipo de red.

Cuando se debe especificar una dirección IP, puede seleccionar (según sea necesario) entre las siguientes opciones:

* Una dirección IPv6. Por ejemplo, `https://[ab12::34c5:6d7:8e90:1234]:4502`

* Una dirección IPv4. Por ejemplo, `https://123.1.1.4:4502`

* Un nombre de servidor. Por ejemplo, `https://www.yourserver.com:4502`

* El caso predeterminado de `localhost` se interpreta para instalaciones de red IPv4 e IPv6. Por ejemplo, `https://localhost:4502`

### AEM Requisitos para el complemento de Dynamic Media de {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media está desactivado de forma predeterminada. Consulte aquí para [habilitar Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

Con Dynamic Media habilitado, se aplican los siguientes requisitos técnicos adicionales.

>[!NOTE]
>
Estos requisitos del sistema **solamente** se aplican si utiliza Dynamic Media (modo híbrido); Dynamic Media (modo híbrido) tiene un servidor de imágenes integrado que solo está certificado en determinados sistemas operativos.
>
Para los clientes de Dynamic Media que ejecutan el modo Dynamic Media - Scene7 (es decir, **dynamicmedia_scene7** AEM modo de ejecución), no hay requisitos de sistema adicionales; solo se aplican los mismos requisitos de sistema que los de los demás sistemas de los sistemas de la aplicación de los sistemas de los sistemas de la aplicación de los sistemas de los sistemas de la red. Dynamic Media: La arquitectura de modo Scene7 AEM utiliza el servicio de imágenes basado en la nube y no el servicio incrustado en la.

#### Hardware {#hardware}

Los siguientes requisitos de hardware son aplicables tanto para Linux® como para Windows:

* CPU Intel Xeon® o AMD® Opteron con al menos cuatro núcleos
* Al menos 16 GB de RAM

#### Linux® {#linux}

Si utiliza Dynamic Media en Linux®, se deben cumplir los siguientes requisitos previos:

* Red Hat® Enterprise 7 o CentOS 7 y versiones posteriores con los parches de correcciones más recientes
* Sistema operativo de 64 bits
* Intercambio desactivado (recomendado)
* SELinux desactivado (Consulte la nota que sigue)

>[!NOTE]
>
Si la configuración regional está establecida de tal manera que LC_CTYPE no es igual a `en_US.UTF-8`, evita que Dynamic Media funcione. Para ver su valor, escriba &quot;locale&quot; en el símbolo del sistema. AEM Si no se configura correctamente, establezca la variable de entorno LC_CTYPE en la cadena vacía escribiendo &quot;export LC_CTYPE=&quot; antes de ejecutar el proceso de ejecución de la.

>[!NOTE]
>
**Desactivación de SELinux:** Imagen servicio no funciona con SELinux activado. Esta opción está habilitada de forma predeterminada. Para remediar este problema, edite el archivo /etc/selinux/config **y cambie el** valor de SELinux de:
>
`SELINUX=enforcing`**Para** `SELINUX=disabled`

>[!NOTE]
>
**Arquitectura NUMA:** Los sistemas con procesadores con AMD64 e Intel® EM64T se configuran normalmente como plataformas de arquitectura de memoria no uniforme (NUMA). Es decir, el núcleo construye varios nodos de memoria durante el arranque en lugar de construir un solo nodo de memoria.
>
La construcción de varios nodos puede causar agotamiento de la memoria en uno o más de los nodos antes de que otros nodos se agoten. Cuando se agota la memoria, el núcleo puede decidir matar procesos (por ejemplo, el servidor de imágenes o el servidor de plataforma) aunque haya memoria disponible.
>
Por lo tanto, Adobe recomienda que, si está ejecutando un sistema de este tipo, desactive NUMA usando **numa=off** opción de arranque para evitar que el núcleo destruya estos procesos.

>[!NOTE]
>
**El nombre del host servidor debe resolverse:** Asegúrese de que el nombre host del servidor se pueda resolver en una dirección IP. Si eso no es posible, agregue el nombre de host completo y la dirección IP a **/etc/hosts**:
>
`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* Intercambiar el espacio al menos el doble de la cantidad de memoria física (RAM)

Para utilizar Dynamic Media en Windows, instale Microsoft® Visual Studio 2010, 2013 y 2015, que se puede redistribuir para x64 y x86.

Para Windows x64:

* Obtenga Microsoft® Visual Studio 2010 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Obtenga Microsoft® Visual Studio 2013 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Obtenga Microsoft® Visual Studio 2015 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Para Windows x86:

* Obtenga Microsoft® Visual Studio 2010 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Obtenga Microsoft® Visual Studio 2013 redistribuible en [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Obtenga Microsoft® Visual Studio 2015 redistribuible en [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x y posterior
* Solo se admite con fines de prueba y demostración

### Requisitos para el AEM Forms PDF Generator {#requirements-for-aem-forms-pdf-generator}

### Soporte de software para el generador de PDF {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Producto</strong></p> </th>
   <th><p><strong>Formatos compatibles para la conversión a PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 classic track</a> última versión</td>
   <td>XPS, formatos de imagen (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF y DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 classic track</a> versión más reciente (Obsoleto)</td>
   <td>XPS, formatos de imagen (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF, y DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF y TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016 (Obsoleto)</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF y TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016 (Obsoleto)<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016 (Obsoleto)<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016 (Obsoleto)<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formatos de imagen (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF y TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2 (Obsoleto)</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formatos de imagen (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF y TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
El generador de PDF solo admite versiones en alemán, francés, inglés y japonés de los sistemas operativos y aplicaciones compatibles.
>
Además,
>
* PDF Generator requiere una versión de 32 bits de [Acrobat 2020 classic track versión 20.004.30006](https://helpx.adobe.com/es/acrobat/release-note/release-notes-acrobat-reader.html) o Acrobat 2017 versión 17.011.30078 para realizar la conversión.
* Las conversiones del generador de PDF para OpenOffice solo son compatibles con Windows y Linux®.
* PDF Generator sólo admite la versión comercial de 32 bits de Microsoft® Office Professional Plus y otro software necesario para la conversión en el sistema operativo Windows.
* PDF Generator admite las versiones de 32 y 64 bits de OpenOffice en el sistema operativo Linux®.
* PDF Generator no admite Microsoft® Office 365.
* Las características de PDF, Optimizar PDF y Exportar PDF de OCR solo son compatibles con Windows.
* Una versión de Acrobat se incluye con AEM Forms para habilitar la funcionalidad Generador de PDF. Acceda mediante programación a la versión empaquetada solo con AEM Forms, durante el período de vigencia de la licencia AEM Forms, para su uso con AEM Forms generador de PDF. Para obtener más información, consulte AEM Forms descripción del producto según su implementación ([On-Premise](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-manager-on-premise.html) o [Managed Services](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-manager-managed-services.html))
* El servicio PDF Generator no es compatible con Microsoft® Windows 10.
* El generador de PDF no puede convertir archivos con Microsoft® Visio 2019. Puede seguir utilizando Microsoft® Visio 2016 para convertir `.VSD` y `.VSDX` archivos.
* El PDF Generator no puede convertir archivos mediante Microsoft® Project 2019. Puede seguir utilizando Microsoft® Project 2016 para convertir `.VSD` y `.VSDX` archivos.
>

### Requisitos de AEM Forms Designer {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server o Microsoft® Windows® 10
* Procesador de 1 GHz o más rápido con soporte para PAE, NX y SSE2.
* 1 GB de RAM para 32 bits o 2 GB de RAM para SO de 64 bits;
* 16 GB de espacio en disco para 32 bits o 20 GB de espacio en disco para SO de 64 bits;
* Memoria gráfica: 128 MB de GPU (se recomiendan 256 MB);
* 2,35 GB de espacio disponible en disco duro;
* 1024 X 768 píxeles de resolución de monitor o superior;
* Aceleración de hardware de vídeo (opcional);
* Acrobat Pro DC, Acrobat Standard DC o Adobe Acrobat Reader DC
* Privilegios administrativos para instalar Designer
* Microsoft Visual C++ 2019 (VC 14.28 o superior) con tiempo de ejecución de 32 bits

### Requisitos para la reescritura de metadatos de AEM Assets XMP {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP La reescritura de datos es compatible y está habilitada para las siguientes plataformas y formatos de archivo:

* **Sistemas operativos:**

   * Linux® (compatibilidad con aplicaciones de 32 y 32 bits en sistemas de 64 bits). Para ver los pasos para instalar bibliotecas de cliente de 32 bits, consulte [XMP Cómo habilitar la extracción y reescritura de datos en Red Hat® Linux de 64 bits®](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * macOS X (64 bits)

* **Formatos de archivo**: JPEG, PNG, TIFF, PDF, INDD, AI y EPS.

### Requisitos para que AEM Assets procese recursos con muchos metadatos en Linux® {#assetsonlinux}

El proceso XMPFilesProcessor requiere la biblioteca GLIBC_2.14 para funcionar. Utilice un núcleo Linux® que contenga GLIBC_2.14, por ejemplo la versión 3.1.x del núcleo Linux®. Mejora el rendimiento para procesar recursos que contienen una gran cantidad de metadatos, como archivos de PSD. El uso de una versión anterior de GLIBC provoca un error en los registros que comienzan por `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
