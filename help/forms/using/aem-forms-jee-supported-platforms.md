---
title: Plataformas admitidas para AEM Forms en JEE
seo-title: Plataformas admitidas para AEM Forms en JEE
description: Lista de los componentes de infraestructura necesarios y admitidos para instalar AEM Forms en JEE
seo-description: Lista de los componentes de infraestructura necesarios y admitidos para instalar AEM Forms en JEE
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
translation-type: tm+mt
source-git-commit: 4e1f5d549df1db28a8679296afb4b758051d8f6c
workflow-type: tm+mt
source-wordcount: '3298'
ht-degree: 0%

---


# Plataformas admitidas para AEM Forms en JEE{#supported-platforms-for-aem-forms-on-jee}

## Plataformas compatibles {#supported-platforms}

### Niveles de soporte {#support-levels}

AEM Forms en el servidor JEE se puede configurar mediante cualquier combinación de sistemas operativos admitidos, servidores de aplicaciones, bases de datos, controladores de bases de datos, JDK, servidores LDAP y servidores de correo electrónico.

Este documento lista las plataformas de cliente y servidor admitidas para AEM Forms en JEE. Adobe proporciona varios niveles de soporte, tanto para nuestras configuraciones recomendadas como para otras configuraciones. El documento también lista otro software compatible y su versión, excepciones, definiciones de parches y política de soporte de parches de software de terceros.

>[!NOTE]
>
>* Para obtener una lista completa de las excepciones a las plataformas de servidor admitidas, consulte [Excepciones a las plataformas de servidor admitidas](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>* AEM Forms en JEE solo admite versiones en inglés, francés, alemán y japonés de los sistemas operativos y las aplicaciones compatibles.
>



### Configuraciones recomendadas {#recommendedconfigurations}

Adobe recomienda estas configuraciones y proporciona soporte completo o restringido como parte del acuerdo estándar de mantenimiento de software:

<table>
 <tbody>
  <tr>
   <th>Nivel de asistencia</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>A: Compatible<br /> </td>
   <td>Adobe proporciona soporte y mantenimiento completos para esta configuración. Esta configuración está cubierta por el proceso de garantía de calidad del Adobe.</td>
  </tr>
  <tr>
   <td>R: Compatibilidad restringida</td>
   <td>Adobe proporciona compatibilidad total con esta configuración después de cumplir ciertos requisitos previos. Póngase en contacto con el servicio de soporte técnico de la empresa de Adobe para conocer los requisitos previos y solicitar asistencia.</td>
  </tr>
  <tr>
   <td>L: Soporte limitado</td>
   <td>Adobe proporciona soporte y mantenimiento completos para estas configuraciones después de cumplir ciertos requisitos previos. No todas las capacidades están disponibles en la configuración. Póngase en contacto con el servicio de soporte técnico de la empresa de Adobe para obtener información sobre los requisitos previos y solicitar asistencia.<br /> </td>
  </tr>
 </tbody>
</table>

### Configuraciones no admitidas {#unsupported-configurations}

| Nivel de asistencia | Descripción |
|---|---|
| E: Se espera que funcione | Se espera que la configuración funcione, y no hay informes que indiquen lo contrario. |
| Z: No admitido | No se admite la configuración. Adobe no hace ninguna declaración sobre si la configuración funciona o no y no la admite. |

>[!NOTE]
>
>Para ayudar a los clientes de AEM Forms a reducir el costo de propiedad, simplificar la arquitectura de implementación y modernizar el stack de desarrollo, la plataforma empresarial de Adobe Experience Manager se está alejando de las implementaciones basadas en servidores de aplicaciones para favorecer implementaciones basadas en OSGi independientes. Adobe sigue admitiendo la pila de AEM Forms JEE con una matriz reducida de componentes de infraestructura.
>
>Con la versión 6.5, ya no se admiten los componentes de infraestructura que tienen el uso más bajo entre nuestros clientes, como se indica a continuación:
>Base de datos IBM DB2
>・ Sistemas operativos IBM AIX y Sun Solaris
>
>En el caso de nuevas instalaciones, siempre que sea posible, se recomienda implementar AEM Forms en la pila OSGi moderna para aprovechar las últimas innovaciones en cuanto a la capacidad de respuesta de Forms adaptable para comunicaciones interactivas móviles, de múltiples canales y integraciones de datos back-end mediante el modelo de datos de formulario.
>
>Reconocemos que los usuarios existentes deben seguir implementando AEM Forms en la pila JEE. En estos casos, el Adobe requiere la implementación de AEM Forms JEE en la infraestructura admitida como se describe en esta documentación. Si está actualizando a AEM 6.5 Forms y utiliza una plataforma no compatible en la versión anterior de AEM Forms, puede ponerse en contacto con la asistencia técnica de Adobe para obtener ayuda sobre la actualización a una plataforma admitida.

### Máquinas virtuales Java (JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms requiere una máquina virtual Java para ejecutarse, que se proporciona mediante la distribución Java Development Kit (JDK). Adobe Experience Manager funciona con las siguientes versiones de las máquinas virtuales Java:

<table>
 <tbody>
  <tr>
   <th><p><strong>Plataforma</strong></p> </th>
   <th><p><strong>Nivel de asistencia</strong></p> </th>
   <th><p><strong>Definiciones de parches admitidas</strong></p> </th>
  </tr>
  <tr>
   <td><p>Oracle Java™ SE 11 (64 bits)</p> </td>
   <td><p>Z: No admitido</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Oracle Java™ SE 8 (64 bits)</td>
   <td>A: Admitido</td>
   <td>Versiones y actualizaciones menores</td>
  </tr>
  <tr>
   <td>Máquina virtual IBM® J9 (compilación 2.8, JRE 1.8.0)</td>
   <td>A: Admitido</td>
   <td>Versiones y actualizaciones menores</td>
  </tr>
  <tr>
   <td>Máquina virtual IBM® J9 (compilación 2.9, JRE 1.8.0)<br /> </td>
   <td>A: Admitido</td>
   <td>Versiones y actualizaciones menores</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Se recomienda rastrear los boletines de seguridad del proveedor de Java para garantizar la seguridad de los entornos de producción e instalar las últimas actualizaciones de Java.
>* AEM Forms en JEE solo admite JVM de 64 bits en entornos de producción.


### Bases de datos y persistencia de CRX {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Plataforma</strong></p> </td>
   <td><p><strong> Descripción</strong></p> </td>
   <td><p><strong>Nivel de asistencia</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sistema de archivos</p> </td>
   <td><p>Microkernel de repositorio (archivos TAR MK)</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.0 </p> </td>
   <td><p>Microkernel de repositorio</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>Oracle Database 12c Versión 1</p> </td>
   <td><p>Microkernel de repositorio</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
   <tr>
   <td><p>Oracle Database 12c Versión 2 (12.2.0.1.0)</p> </td>
   <td><p>Microkernel de repositorio</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td>Base de datos oracle 18c </td>
   <td>Microkernel de repositorio</td>
   <td>Compatible</td>
  </tr> 
   <tr>
   <td>Base de datos de oracle 19c (Standard, Real Application Clusters (RAC) y ediciones Enterprise) </td>
   <td>Repositorio Microkernal </td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td><p>Microkernel de repositorio</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1</td>
   <td>Microkernel de repositorio</td>
   <td>R: Compatibilidad restringida</td>
  </tr>
    <tr>
   <td>MySQL 5.7.19 </td>
   <td>-</td>
   <td>R: Compatibilidad restringida</td>
  </tr>
 </tbody>
</table>

* IBM DB2 no es compatible con instalaciones nuevas. Solo se admite para clientes existentes que actualicen a AEM 6.5 Forms.
* MongoDB es un software de terceros y no está incluido en el paquete de licencias de AEM. Para obtener más información, consulte la página [Política de licencias de MongoDB](https://www.mongodb.org/about/licensing/).
* Para aprovechar al máximo su implementación de AEM, Adobe recomienda que se le otorgue la licencia de la versión MongoDB Enterprise para beneficiarse de la asistencia profesional.
* El Servicio de atención al cliente de Adobe asistirá en los problemas de calificación relacionados con el uso de MongoDB con AEM. Para obtener más información, consulte la página [MongoDB para Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
* &#39;File System&#39; incluye el almacenamiento de bloques que es compatible con POSIX. Esto incluye la tecnología de almacenamiento de red. Tenga en cuenta que el rendimiento del sistema de archivos puede variar e influir en el rendimiento general. Se recomienda cargar AEM de prueba en combinación con el sistema de archivos de red/remoto.
* Solo se admite el motor de Almacenamiento MongoDB WiredTiger.
* El uso compartido de MongoDB no se admite en AEM.
* AEM Forms en JEE no admite MySQL para persistencia RDBMK.
* El módulo Seguridad de Documento no utiliza el repositorio de contenido. Esto implica que, si solo utiliza Documento Security y no tiene pensado utilizar HTML Workspace, formularios HTML5 o formularios adaptables, no instale Content Repository.
* AEM Forms en JEE no admite el uso de MySQL para AEM Repositorio (CRX-Repository).


### Controladores de base de datos {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>Base de datos </th>
   <th><p><strong>Plataforma</strong></p> </th>
   <th><p><strong>Definiciones de parches admitidas</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>Conector MySQL/J 5.7</p> <p>mysql-Connector-java-5.1.44-bin.jar(versión 5.1.44)</p> </td>
   <td><p>Proporcionado con AEM Forms en la instalación de JEE</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Controlador JDBC de Microsoft® SQL Server 6.2.1.0<br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>Se suministra con AEM Forms en la instalación de JEE.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Controlador JDBC de oracle Database 19.3.0.0.0</p> <p>ojdbc8.jar (versión 19.3.0.0.0)<br /> </p> </td>
   <td><p>Descargue desde <a href="https://www.oracle.com/technetwork/database/features/jdbc/jdbc-ucp-122-3110062.html">sitio Web de Oracle</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Servidores de aplicaciones {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Plataforma</strong></p> </td>
   <td><p><strong>Nivel de asistencia</strong></p> </td>
   <td><p><strong>Definiciones de parches admitidas</strong></p> </td>
  </tr>
  <tr>
   <td>Oracle WebLogic Server 12.2.1 (12c R2)</td>
   <td>A: Admitido</td>
   <td>Service Pack y actualizaciones críticas</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0 <sup>[1] [4]</sup><br /> </td>
   <td>A: Admitido</td>
   <td>Service Pack y actualizaciones críticas</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.1.4 <sup>[2] [3] [7]</sup></p> </td>
   <td><p>A: Admitido</p> </td>
   <td><p>Parches y parches acumulativos para la versión EAP admitida</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los clústeres IBM® WebSphere® solo se admiten en las ediciones de Implementación de red.

### Sistemas operativos de servidor {#server-operating-systems}

#### Entornos de producción {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Plataforma</strong></p> </th>
   <th><p><strong>Nivel de asistencia</strong></p> </th>
   <th><p><strong>Definiciones de parches admitidas</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft Windows Server 2016 (64 bits)</td>
   <td>A: Admitido</td>
   <td>Service Packs y actualizaciones críticas</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7 (Kernel 3.x) (64 bits)</br><b>Nota:</b> <a href="https://access.redhat.com/articles/4665701">Red Hat Enterprise Linux 6</a> llega a la fase de Fin de Mantenimiento y transiciones a la fase de Soporte de Ciclo de Vida Extendido el 30 de noviembre de 2020. Adobe recomienda Red Hat Enterprise Linux 7 para actualizaciones e instalaciones nuevas. Las instalaciones existentes pueden utilizar Red Hat Enterprise Linux 6 durante la fase de soporte de ciclo de vida ampliado.</p> </td>
   <td><p>A: Admitido</p> </td>
   <td><p>Versiones menores, actualizaciones acumulativas y actualizaciones críticas</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12 (64 bits)</p> </td>
   <td><p>A: Admitido</p> </td>
   <td><p>Service Packs, parches acumulativos y actualizaciones de seguridad críticas</p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Actualización 3 (64 bits)</td>
   <td>A: Admitido</td>
   <td>Service Packs, parches acumulativos y actualizaciones de seguridad críticas</td>
  </tr>
  <tr>
   <td>CentOS 7 (64 bits)<sup> [6]</sup></td>
   <td>A: Admitido</td>
   <td>Service Packs, parches acumulativos y actualizaciones de seguridad críticas</td>
  </tr>
 </tbody>
</table>

#### Entorno virtualizado {#virtualized-environment}

Puede ejecutar AEM Forms en JEE en una máquina física o un entorno virtual. Sin embargo, si encuentra algún problema con AEM Forms en un entorno virtual, intente replicar el problema en una máquina física. Si el problema persiste en la máquina física, póngase en contacto con la asistencia de Adobe para obtener una resolución. Para los problemas que no puede replicar en una máquina física, póngase en contacto con el proveedor del entorno virtual.

#### Entornos de desarrollo {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plataforma (versión base)</strong></p> </th>
   <th>Nivel de asistencia</th>
   <th><p><strong>Definiciones de parches admitidas</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 de 64 bits</p> </td>
   <td>E: Se espera que funcione</td>
   <td><p>Service Pack y actualizaciones críticas</p> </td>
  </tr>
 </tbody>
</table>

### Excepciones a plataformas de servidor admitidas {#exceptions-to-supported-server-platforms}

Tenga en cuenta las siguientes excepciones al elegir una plataforma para configurar su AEM Forms en el servidor JEE.

1. AEM Forms on JEE no soporta IBM® WebSphere® con MySQL.
1. AEM Forms en JEE no admite ni JBoss en SUSE Linux Enterprise Server 12. Solo se admite IBM WebSphere en SUSE Linux Enterprise Server 12.
1. AEM Forms en JEE no admite ningún JDK con JBoss® excepto Oracle Java™ SE.
1. AEM Forms on JEE no admite ningún JDK con IBM® WebSphere®, excepto IBM® JDK.
1. El repositorio de CRX admite la persistencia de tipo TarMK, MongoDB y bases de datos relacionales (RDBMK). No puede tener dos sistemas de base de datos diferentes entre el servidor de aplicaciones y el repositorio de CRX. Sin embargo, en un AEM Forms en entorno JEE, puede utilizar MongoMK con el repositorio CRX y una base de datos relacional admitida con el servidor de aplicaciones.
1. AEM Forms en JEE no admite el servidor de aplicaciones WebSphere en CentOS.
1. AEM Forms en JEE no admite el control de acceso basado en roles JBoss (RBAC).

Además, tenga en cuenta los siguientes puntos a la hora de elegir software para Adobe AEM Forms en implementaciones JEE:

* AEM Forms en JEE admite actualizaciones, parches y paquetes de correcciones además de la versión principal y secundaria especificada del software admitido. Sin embargo, la actualización a la siguiente versión principal o secundaria no se admite a menos que se especifique lo contrario.
* Las instalaciones basadas en clústeres no admiten la persistencia TarMK. Para obtener información sobre la persistencia admitida, consulte [Elección de un tipo de persistencia para una instalación de AEM Forms](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
* AEM Forms en JEE soporta diversos software de terceros según nuestra [Política de soporte de software de terceros](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
* AEM Forms en JEE admite plataformas según la compatibilidad proporcionada por proveedores de terceros. Es posible que proveedores externos no permitan algunas combinaciones. Por ejemplo, muchos proveedores no han certificado sus servidores de aplicaciones con Oracle. Como resultado, AEM Forms en JEE tampoco admite estas combinaciones. Para asegurarse de elegir las versiones de software admitidas, compruebe también la matriz de soporte de los proveedores de terceros.
* AEM Forms en JEE no admite TarMK Cold Standby.
* AEM Forms en JEE no admite clústeres verticales.
* AEM Forms en JEE no admite la base de datos MySQL en un entorno agrupado.
* Para ver la lista de las plataformas eliminadas o actualizadas, consulte el documento [AEM 6.5 Forms New Feature Summary](../../forms/using/whats-new.md).

### Servidores LDAP (opcional) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>Producto (versión base)</strong></p> </th>
   <th><p><strong>Definiciones de parches admitidas</strong></p> </th>
  </tr>
  <tr>
   <td>Oracle Unified Directory (OUD) 11g versión 2</td>
   <td>Service Packs</td>
  </tr>
  <tr>
   <td>Microsoft Active Directory 2016</td>
   <td>Revisión de mantenimiento y paquetes de correcciones</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>Paquetes de funciones y correcciones provisionales</p> </td>
  </tr>
 </tbody>
</table>

### Servidores de correo electrónico (opcional) {#email-servers-optional}

| Producto |
|---|
| IBM Lotus Domino 9.0 |
| Microsoft Exchange 2013 |
| Microsoft Office 365 |

### Administradores de contenido y conectores correspondientes {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>Producto<br /> </strong></td>
   <td><strong>Versión</strong></td>
  </tr>
  <tr>
   <td>Documentum de EMC</td>
   <td>7,3</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.2</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM Content Manager Server</td>
   <td>8.5 Envase para correcciones 2</td>
  </tr>
  <tr>
   <td>Cliente de IBM Content Manager</td>
   <td>8,5 </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint</td>
   <td>2016<br /> </td>
  </tr>
 </tbody>
</table>

### Compatibilidad con Cordova {#support-for-cordova}

AEM Forms App ahora admite Apache Cordova. A continuación se indican las versiones específicas de la plataforma de Cordova que se admiten:

* Apache Cordova 6.4.0
* Cordova iOS 4.3.0
* Cordova Android 6.0.0
* Cordova Windows 4.4.3

### Compatibilidad con software para PDF Generator {#software-support-for-pdf-generator}

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



### Excepciones a la compatibilidad con accesibilidad {#exceptions-to-accessibility-support}

Los siguientes subsistemas de AEM Forms no son [508](https://www.section508.gov/) compatibles:

* IU adaptable de creación de Forms
* IU de creación de Forms Manager
* Interfaz de usuario de creación de Correspondencia Management
* IU de administración (IU de la Consola de administración)

## Requisitos del sistema para AEM Forms en JEE {#system-requirements-for-aem-forms-on-jee}

### Requisitos mínimos de hardware {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Plataforma</td>
   <td>Requisito de hardware mínimo</td>
  </tr>
  <tr>
   <td>Microsoft Windows Server</td>
   <td>Procesador Intel® Xeon® E5-2680, 2,4 GHz o equivalente<br /> VMWare ESX 5.1 o posterior<br /> RAM: 6 GB (SO de 64 bits con JVM de 64 bits)<br /> Espacio libre en disco: 15 GB de espacio temporal más 22 GB<br /> para AEM Forms en JEE</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>Procesador Intel Xeon E5-2670v2, 1 vCPU, 2,5 GHz<br /> AWS m3.medium (3 ECUs)<br /> RAM: 6 GB (SO de 64 bits con JVM de 64 bits)<br /> Espacio libre en disco: 6 GB de espacio temporal más 22 GB<br /> para AEM Forms en JEE</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>Procesador Intel Xeon E5-2670v2, 1 vCPU, 2,5 GHz<br /> AWS m3.medium (3 ECUs)<br /> RAM: 6 GB (SO de 64 bits con JVM de 64 bits)<br /> Espacio libre en disco: 6 GB de espacio temporal más 22 GB<br /> para AEM Forms en JEE<br /> </td>
  </tr>
  <tr>
   <td>Requisitos de hardware para un pequeño entorno de producción</td>
   <td>
    <ul>
     <li><strong>Entorno</strong> con tecnología Intel: Intel® Xeon® E5-2680, 2,4 GHz o bueno. El uso de un procesador de doble núcleo mejorará aún más el rendimiento</li>
     <li><strong>Memoria:  </strong>4 GB  <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Para obtener información adicional, consulte:

* [Requisitos del sistema para un AEM Forms de un solo servidor en implementación JEE](https://www.adobe.com/go/learn_aemforms_sysreq_single_63)
* [Requisitos del sistema para un AEM Forms agrupado en la implementación JEE](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_63)

## Clientes admitidos para AEM Forms en JEE {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plataforma</strong></p> </th>
   <th><p><strong>Definiciones de parches admitidas</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 (Enterprise, Pro, Basic)</p> <p>Versión de 32 o 64 bits</p> <p> </p> </td>
   <td>Service Packs y actualizaciones críticas</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2016 Server</td>
   <td>Service Packs y actualizaciones críticas</td>
  </tr>
 </tbody>
</table>

* Espacio en disco para la instalación: 1,7 GB sólo para Workbench, 2,7 GB en una sola unidad para una instalación completa de Workbench, Designer y el conjunto de muestras 400 MB para directorios de instalación temporales: 200 MB en el directorio temporal del usuario y 200 MB en el directorio temporal de Windows. Si todas estas ubicaciones residen en una sola unidad, debe haber 1,5 GB de espacio disponible durante la instalación. Los archivos copiados en los directorios temporales se eliminan al finalizar la instalación.

* Memoria para ejecutar Workbench: 2 GB de RAM
* Requisitos de hardware: Procesador Intel® Pentium® 4 o AMD equivalente, 1 GHz
* Resolución mínima de pantalla de 1024 X 768 píxeles o buena con color de 16 bits o superior
* Conexión de red TCP/IPv4 o TCP/IPv6 a AEM Forms en el servidor JEE
* Debe tener privilegios de administrador para instalar Workbench en Windows. Si va a realizar la instalación con una cuenta que no sea de administrador, el programa de instalación le pedirá las credenciales de una cuenta adecuada.

### Diseñador {#designer}

>[!NOTE]
>
>Para instalar Designer en Windows, ejecute el programa de instalación con privilegios administrativos.

* Microsoft® Windows® 2016 Server, Microsoft Windows 10

   * Procesador de 1 GHz o más rápido compatible con PAE, NX y SSE2.
   * 1 GB de RAM para 32 bits o 2 GB de RAM para SO de 64 bits
   * 16 GB de espacio en disco para 32 bits o 20 GB de espacio en disco para SO de 64 bits

* Memoria gráfica: 128 MB de GPU (se recomiendan 256 MB)
* 2,35 GB de espacio disponible en el disco duro
* Unidad de DVD-ROM
* Internet Explorer 10 o 11; Firefox 45.x
* Resolución de pantalla de 1024 X 768 píxeles o buena
* Aceleración de hardware de vídeo (opcional)
* Acrobat Pro DC, Acrobat Standard DC o Adobe Acrobat Reader DC.

### Adobe Acrobat y Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat y Adobe Reader (Base)</strong></p> </th>
   <th><p><strong>Definiciones de parches admitidas</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2017 (Classic track)</td>
   <td>Versión 17.011.30078 o posterior<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>La familia de productos Acrobat DC presenta dos pistas tanto para Acrobat como para Reader, que son esencialmente diferentes: &quot;Classic&quot; y &quot;Continuous&quot;. Para obtener más información y una comparación de las dos pistas, consulte [https://www.adobe.com/go/acrobatdctracks.](https://www.adobe.com/go/acrobatdctracks)

### Exploradores {#browsers}

#### Equipos de sobremesa {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>Explorador (base)</strong></p> </th>
   <th><p><strong>Nivel de asistencia</strong></p> </th>
   <th><p><strong>Definiciones de parches admitidas</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft Edge (Evergreen)</p> </td>
   <td><p>A: Admitido</p> </td>
   <td><p>Service Packs y actualizaciones</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox (Evergreen)</p> </td>
   <td><p>A: Admitido</p> </td>
   <td>Todas las actualizaciones</td>
  </tr>
  <tr>
   <td>Microsoft Firefox ESR</td>
   <td>E: Se espera que funcione</td>
   <td> Todas las actualizaciones</td>
  </tr>
  <tr>
   <td><p>Google Chrome (Evergreen)</p> </td>
   <td><p>A: Admitido</p> </td>
   <td>Todas las actualizaciones</td>
  </tr>
  <tr>
   <td>Google Chrome y Firefox en MAC OS X</td>
   <td>A: Compatible<br /> <br /> </td>
   <td>Todas las actualizaciones</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x</td>
   <td>A: Admitido</td>
   <td>Todas las actualizaciones</td>
  </tr>
  <tr>
   <td>Apple Safari 12.x<br /> <br /> </td>
   <td>A: Admitido</td>
   <td>Todas las actualizaciones</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Algunas excepciones relacionadas con el navegador para equipos de escritorio son las siguientes:
>
>* La mayoría de los exploradores modernos ya no admiten complementos basados en NPAPI. Para obtener información sobre cómo afecta a las aplicaciones y flujos de trabajo de AEM Forms, consulte [Interrupción de los complementos del explorador NPAPI y su impacto](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html).
>* Safari solo se admite en Macintosh OS X.
>* Workspace admite Safari 5.1 en Macintosh OS X 10.6 y 10.7 con Acrobat DC o versiones posteriores. Para obtener más información sobre la compatibilidad de Safari 5.1 con Adobe Reader, Acrobat, consulte [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
>* Safari no admite la Consola de administración.
>* La administración de correspondencia no admite Windows® Internet Explorer 9.0 para formularios AEM 6.1.
>* El portal de Forms admite el software de lector de pantalla JAWS 14.0 en Internet Explorer 11 para accesibilidad.
>



#### Clientes móviles {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>Explorador (base)</strong></p> </th>
   <th><p><strong>Definiciones de parches admitidas</strong></p> </th>
  </tr>
  <tr>
   <td><p>Chrome en Android™ 4.1.2 y posterior</p> </td>
   <td><p>Todas las actualizaciones</p> </td>
  </tr>
  <tr>
   <td>Safari en iOS 11.0 y posterior</td>
   <td>Todas las actualizaciones</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>Todas las actualizaciones<br /> </td>
  </tr>
  <tr>
   <td>Navegador nativo de Android™ 4.4 y posterior</td>
   <td>Todas las actualizaciones</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Forms Portal solo es compatible con Safari en iPad.
>



### Aplicación de AEM Forms {#aem-forms-workspace-app}

#### Compatibilidad con dispositivos móviles {#mobile-device-support}

La aplicación de AEM Forms está disponible en las siguientes plataformas:

| **Plataforma** | **Dispositivos admitidos** |
|---|---|
| Apple iOS | Apple iPhone, iPad, iPad Air y iPad mini con iOS 12 o posterior. |
| Google Android | Android 5.1 y posterior. La aplicación de AEM Forms está certificada en tabletas Samsung Galaxy de 7 y 10 pulgadas y en teléfonos inteligentes populares. |
| Microsoft Windows | Dispositivos Microsoft Surface, tabletas, portátiles y equipos de escritorio que ejecutan el sistema operativo Microsoft Windows 10. |

### Flash Player de Adobe {#adobe-flash-player}

<table>
 <tbody>
  <tr>
   <th><p><strong>Flash Player (base)</strong></p> </th>
   <th><p><strong>Definiciones de parches admitidas</strong></p> </th>
  </tr>
  <tr>
   <td><p>Última versión de Flash Player</p> </td>
   <td><p>Versiones y actualizaciones menores</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Adobe [dejará de actualizar y distribuir el Flash Player a finales de 2020](https://theblog.adobe.com/adobe-flash-update/).

### Adobe Documento Security Extension for Microsoft Office {#adobe-rights-management-extension-for-microsoft-office}

Haga clic [aquí](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html) para ver los requisitos del sistema para Adobe Documento Security Extension for Microsoft® Office.

### Excepciones al soporte al cliente {#exceptions-to-client-support}

AEM Forms en JEE admite actualizaciones, parches y paquetes de correcciones además de la versión principal y secundaria especificada del software admitido. Sin embargo, la actualización a la siguiente versión principal o secundaria no se admite a menos que se especifique lo contrario.

## Directiva de soporte de parches de terceros {#third-party-patch-support-policy}

Los requisitos de software de terceros para AEM Forms en JEE están documentados en la sección &quot;Requisitos del sistema&quot; de sus respectivos documentos de productos. Puede acceder a toda la documentación en [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65).

AEM Forms en las plataformas de referencia de terceros de JEE indica el nivel de parche específico de la infraestructura de terceros que se encontraba vigente durante el desarrollo y la publicación de AEM Forms en JEE, y desde el nivel mínimo de parche/Service Pack de la infraestructura soportada por esa versión de AEM Forms en JEE.

Adobe admite revisiones urgentes o recomendadas emitidas por proveedores externos en el momento de su lanzamiento, suponiendo que los proveedores de terceros garantizan la compatibilidad con versiones anteriores compatibles con las versiones compatibles con AEM Forms en JEE. Adobe sólo admitirá parches lanzados después del nivel mínimo de parche indicado en la documentación de AEM Forms en JEE.

En algunos casos, Adobe no admite actualizaciones de terceros que cambien la funcionalidad principal y, por lo tanto, no admite compatibilidad total con versiones anteriores. Para obtener más información sobre las actualizaciones admitidas, consulte [Definiciones de parches admitidas](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) para productos de proveedores específicos y los tipos de parches compatibles con Adobe.

En circunstancias que escapan al control del Adobe, los parches de terceros que reclaman compatibilidad con versiones anteriores pueden tener un impacto negativo en los productos de Adobe o en los entornos del cliente. En estos casos, Adobe recomienda que los clientes evalúen el impacto de cualquier parche urgente de un tercero antes de aplicarlo a sistemas críticos. El Adobe trabajará con terceros mediante esfuerzos comerciales razonables para resolver estos problemas, ya sea a través de programas normales de apoyo al Adobe o de terceros que rectifican la cuestión en su parche. Esto no garantiza que un parche de terceros recién lanzado que será compatible con Adobe funcione según lo documentado por el proveedor o con AEM Forms en JEE.

Adobe se reserva el derecho de cambiar las plataformas de referencia de terceros admitidas por un AEM Forms en la versión JEE y sus definiciones de parches admitidas en cualquier momento.

También puede encontrar información adicional sobre parches de terceros buscando en el sitio de soporte empresarial de Adobe artículos de la base de conocimiento relacionados con su producto.

## Historial de revisión {#revision-history}

* 9 de septiembre de 2020
   * Se ha cambiado la versión compatible de iOS para la aplicación de AEM Forms a iOS 12. La versión anterior era iOS 11.
