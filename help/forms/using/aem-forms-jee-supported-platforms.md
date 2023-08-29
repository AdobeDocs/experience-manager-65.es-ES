---
title: Plataformas compatibles con AEM Forms en JEE
seo-title: Supported Platforms for AEM Forms on JEE
description: Lista de componentes de infraestructura requeridos y admitidos para instalar AEM Forms en JEE
seo-description: List of infrastructure components required and supported for installing AEM Forms on JEE
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
source-git-commit: 34be3b4695679a9b5e8001d28f05ed804f929e61
workflow-type: tm+mt
source-wordcount: '3699'
ht-degree: 95%

---


# Plataformas compatibles con AEM Forms en JEE {#supported-platforms-for-aem-forms-on-jee}

## Plataformas compatibles {#supported-platforms}

<div class="preview">

Adobe ha lanzado un [instalador completo](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) con AEM 6.5 Forms Service Pack 12 (6.5.12.0) en JEE junto con los instaladores de parches. El instalador completo proporciona soporte para plataformas nuevas, mientras que el instalador de parches solo incluye correcciones de errores.

Si realiza una instalación nueva o planea utilizar el software más reciente para su AEM Forms 6.5 en el entorno JEE, Adobe recomienda utilizar [AEM 6.5.12.0 Forms en el instalador completo de JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) lanzado el 3 de marzo de 2022, en lugar del instalador de AEM Forms 6.5 lanzado el 8 de abril de 2019.

</div>

### Niveles de soporte {#support-levels}

AEM Forms en el servidor JEE se puede configurar mediante cualquier combinación de sistemas operativos compatibles, servidores de aplicaciones, bases de datos, controladores de base de datos, JDK, servidores LDAP y servidores de correo electrónico.

Este documento enumera las plataformas de cliente y servidor compatibles con AEM Forms en JEE. Adobe proporciona varios niveles de soporte, tanto para nuestras configuraciones recomendadas como para otras configuraciones. El documento también enumera otro software compatible y su versión, excepciones, definiciones de parches y la directiva de soporte de parches para software de terceros.

>[!NOTE]
>
>- Para obtener una lista completa de las excepciones a las plataformas de servidor compatibles, consulte [Excepciones a plataformas de servidor compatibles](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>- AEM Forms en JEE solo admite versiones en inglés, francés, alemán y japonés de los sistemas operativos y aplicaciones compatibles.

### Configuraciones recomendadas {#recommendedconfigurations}

Adobe recomienda estas configuraciones y proporciona soporte completo o restringido como parte del acuerdo de mantenimiento de software estándar:

<table>
 <tbody>
  <tr>
   <th>Nivel de soporte</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>A: Compatible<br /> </td>
   <td>Adobe proporciona soporte y mantenimiento completos para esta configuración. Esta configuración está cubierta por el proceso de garantía de calidad de Adobe.</td>
  </tr>
  <tr>
   <td>R: Compatibilidad restringida</td>
   <td>Adobe proporciona compatibilidad total con esta configuración si se cumplen ciertos requisitos previos. Póngase en contacto con el servicio de soporte técnico de la empresa de Adobe para obtener más información sobre los requisitos previos y presentar una solicitud de soporte.</td>
  </tr>
  <tr>
   <td>L: Compatibilidad limitada</td>
   <td>Adobe proporciona soporte y mantenimiento completos para estas configuraciones después de cumplir ciertos requisitos previos. No todas las funcionalidades están disponibles en la configuración. Póngase en contacto con el servicio de soporte técnico de la empresa de Adobe para obtener más información sobre los requisitos previos y presentar una solicitud de soporte.<br /> </td>
  </tr>
 </tbody>
</table>

### Configuraciones no compatibles {#unsupported-configurations}

| Nivel de soporte | Descripción |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E: Se espera que funcione | Se espera que la configuración funcione y no hay informes que indiquen lo contrario. |
| Z: No compatible | La configuración no es compatible. Adobe no realiza ninguna declaración sobre si la configuración funciona o no y no la admite. |

>[!NOTE]
>
>Para ayudar a los clientes de AEM Forms a reducir el coste de propiedad, simplificar la arquitectura de implementación y modernizar la pila de desarrollo, la plataforma empresarial de Adobe Experience Manager se aleja de las implementaciones basadas en servidores de aplicaciones en favor de implementaciones independientes basadas en OSGi. Adobe sigue siendo compatible con la pila JEE de AEM Forms con una matriz reducida de componentes de infraestructura.
>
>Con la versión 6.5, ya no se admiten los componentes de infraestructura que tengan el menor uso entre nuestros clientes, de la siguiente manera:
>
>- Base de datos IBM DB2
>- Sistemas operativos IBM AIX y Sun Solaris
>
>En el caso de nuevas instalaciones, siempre que sea factible, se recomienda implementar AEM Forms en la pila moderna de OSGi para aprovechar las últimas innovaciones en relación con los formularios adaptables para comunicaciones interactivas móviles multicanal e integraciones de datos back-end mediante el Modelo de datos de formulario.
>
>Reconocemos que los usuarios existentes deben seguir implementando AEM Forms en la pila JEE. En estos casos, Adobe requiere la implementación de AEM Forms JEE en la infraestructura admitida, tal como se describe en esta documentación. Si actualiza a Forms AEM 6.5 y utiliza una plataforma no compatible en la versión anterior de AEM Forms, puede ponerse en contacto con el servicio de soporte de Adobe para obtener ayuda sobre la actualización a una plataforma compatible.

### Máquinas virtuales Java (JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms requiere una máquina virtual Java para ejecutarse, que proporciona la distribución Java Development Kit (JDK). Adobe Experience Manager funciona con las siguientes versiones de las máquinas virtuales Java:

<table>
 <tbody>
  <tr>
   <th><p><strong>Plataforma</strong></p> </th>
   <th><p><strong>Nivel de soporte</strong></p> </th>
   <th><p><strong>Definiciones de parches compatibles</strong></p> </th>
  </tr>
  <tr> 
   <td><p>Oracle Java™ SE 11 (64 bits) <sup> [8] </sup> </p>  </td>
   <td><p>A: Compatible</p> </td>
   <td><p>Lanzamientos y actualizaciones menores </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 11 - 64 bits</td>
   <td>Z: No compatible</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 8 - 64bit</td>
   <td>Z: No compatible</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Oracle Java™ SE 8 (64 bits)</td>
   <td>A: Compatible</td>
   <td>Lanzamientos y actualizaciones menores</td>
  </tr>
  <tr>
   <td>Mñaquina virtual IBM® J9 (versión 2.9, JRE 1.8.0) IBM® JDK SR6-FP26<br /> </td>
   <td>A: Compatible</td>
   <td>Lanzamientos y actualizaciones menores</td>
  </tr>
  <tr>
   <td>IBM JAVA1.8.0_291 (versión 8.0.6.30)<br /> </td>
   <td>A: Compatible</td>
   <td>Lanzamientos y actualizaciones menores</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>- Se recomienda realizar un seguimiento de los boletines de seguridad del proveedor de Java para garantizar la seguridad de los entornos de producción e instalar las últimas actualizaciones de Java.
>- AEM Forms en JEE solo admite JVM de 64 bits en entornos de producción.

### Bases de datos y persistencia CRX {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Plataforma</strong></p> </td>
   <td><p><strong> Descripción</strong></p> </td>
   <td><p><strong>Nivel de soporte</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sistema de archivos</p> </td>
   <td><p>Microkernel del repositorio (archivos TAR MK)</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 4.0 (Obsoleto) </p> </td>
   <td><p>Repositorio Microkernel</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.2 </p> </td>
   <td><p>Repositorio Microkernel</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>Base de datos Oracle 12c Release 2 (12.2.0.1.0) (Obsoleto)</p> </td>
   <td><p>Repositorio Microkernel</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
   <tr>
   <td>Base de datos Oracle 19c (Ediciones Standard, Real Application Clusters (RAC) y Enterprise) </td>
   <td>Repositorio Microkernal </td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016 (Deprecated)</p> </td>
   <td><p>Repositorio Microkernel</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>Servidor Microsoft SQL 2019</p> </td>
   <td><p>Repositorio Microkernel</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1 (Obsoleto)</td>
   <td>Repositorio Microkernel</td>
   <td>R: Compatibilidad restringida</td>
  </tr>
  <tr>
   <td>MySQL 5.7.35 (Obsoleto) </td>
   <td>-</td>
   <td>R: Compatibilidad restringida</td>
  </tr>
  <tr>
   <td>MySQL 8.0.27</td>
   <td>-</td>
   <td>R: Compatibilidad restringida</td>
  </tr>
 </tbody>
</table>

- IBM DB2 no es compatible con instalaciones nuevas. Solo es compatible con los clientes existentes que actualizan a AEM Forms 6.5.
- MongoDB es software de terceros y no está incluido en el paquete de licencias de AEM. Para obtener más información, consulte la página [Directiva de licencias de MongoDB](https://www.mongodb.org/about/licensing/).
- Para aprovechar al máximo su implementación de AEM, Adobe recomienda licenciar la versión de MongoDB Enterprise para beneficiarse del soporte profesional.
- El Servicio de atención al cliente de Adobe ayudará a calificar los problemas relacionados con el uso de MongoDB con AEM. Para obtener más información, consulte la [Página MongoDB para Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
- “File System” incluye almacenamiento en bloque compatible con POSIX. Esto incluye la tecnología de almacenamiento en red. Tenga en cuenta que el rendimiento del sistema de archivos puede variar e influir en el rendimiento general. Se recomienda cargar AEM de prueba en combinación con el sistema de archivos de red/remoto.
- Solo soporta el motor de almacenamiento MongoDB WiredTiger.
- El uso compartido de MongoDB no es compatible con AEM.
- AEM Forms en JEE no admite MySQL para persistencia RDBMK.
- El módulo Seguridad de documentos no utiliza el Repositorio de contenido. Esto implica que, si solo utiliza la seguridad de los documentos y no planea utilizar el espacio de trabajo del HTML, los formularios del HTML5 o los formularios adaptables, no instale el repositorio de contenido.
- AEM Forms en JEE no admite el uso de MySQL para mantener el repositorio de AEM (CRX-Repository).

### Controladores de base de datos {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>Base de datos </th>
   <th><p><strong>Plataforma</strong></p> </th>
   <th><p><strong>Definiciones de parches compatibles</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>Conector MySQL/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar (versión 5.1.44)</p> </td>
   <td><p>Se suministra con AEM Forms en la instalación de JEE</p> </td>
  </tr>
  <tr>
   <td>Servidor Microsoft SQL <br /> </td>
   <td><p>Controlador JDBC del servidor Microsoft® SQL 6.2.1.0 (Obsoleto) <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>Se suministra con AEM Forms en la instalación de JEE.</p> </td>
  </tr>
    <tr>
   <td>Servidor Microsoft SQL <br /> </td>
   <td><p>Controlador JDBC del servidor Microsoft® SQL 6.2.2.0 <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>Se suministra con AEM Forms en la instalación de JEE.</p> </td>
  </tr>
  <tr>
   <td>Servidor Microsoft SQL <br /> </td>
   <td><p>Controlador JDBC del servidor Microsoft® SQL 8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>Descarga desde el sitio web de Microsoft.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Controlador JDBC de la base de datos de Oracle 19.3.0.0.0</p> <p>ojdbc8.jar (versión 19.3.0.0.0)<br /> </p> </td>
   <td><p>Descargar desde el <a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">Sitio web de Oracle</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Servidores de aplicaciones {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Plataforma</strong></p> </td>
   <td><p><strong>Nivel de soporte</strong></p> </td>
   <td><p><strong>Definiciones de parches compatibles</strong></p> </td>
  </tr>
  <tr>
   <td>Servidor Oracle WebLogic 12.2.1 (12c R2)</td>
   <td>A: Compatible</td>
   <td>Service Pack y actualizaciones críticas</td>
  </tr>
  <tr>
   <td>Servidor de aplicaciones IBM® WebSphere® 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
   <td>A: Compatible</td>
   <td>Service Pack y actualizaciones críticas</td>
  </tr>
  <tr>
   <td><p>Plataforma de aplicaciones empresariales (EAP) JBoss® 7.1.4 <sup>[2] [3] [7]</sup> (Obsoleto) </p> </td>
   <td><p>A: Compatible</p> </td>
   <td><p>Parches y parches acumulativos para la versión EAP compatible</p> </td>
  </tr>
  <tr>
   <td><p>Plataforma de aplicaciones empresariales (EAP) JBoss® 7.4 <sup>[2] [3] [7]</sup> </p> </td>
   <td><p>A: Compatible</p> </td>
   <td><p>Parches y parches acumulativos para la versión EAP compatible</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los clústeres IBM® WebSphere® solo son compatibles con las ediciones de implementación de red.

### Sistemas operativos del servidor {#server-operating-systems}

#### Entornos de producción {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Plataforma</strong></p> </th>
   <th><p><strong>Niveles de soporte</strong></p> </th>
   <th><p><strong>Definiciones de parches compatibles</strong></p> </th>
  </tr>
   <tr>
   <td>Servidor Microsoft Windows 2019 (64 bits)</td>
   <td>A: Compatible</td>
   <td>Service Packs y actualizaciones críticas</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>A: Compatible</td>
   <td>Service Packs y actualizaciones críticas</td>
  </tr>
  <tr>
   <td> Servidor Microsoft Windows 2016 (64 bits) (Obsoleto)</td>
   <td>A: Compatible</td>
   <td>Service Packs y actualizaciones críticas</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 8 (Kernel 4.x) (64 bits)</p> </td>
   <td><p>A: Compatible</p> </td>
   <td><p>Versiones menores, actualizaciones acumulativas y actualizaciones críticas</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7 (Kernel 3.x) (64 bits) (Obsoleto)</td>
   <td><p>A: Compatible</p> </td>
   <td><p>Versiones menores, actualizaciones acumulativas y actualizaciones críticas</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12 (64 bits)</p> </td>
   <td><p>A: Compatible</p> </td>
   <td><p>Service Packs, parches acumulativos y actualizaciones de seguridad críticas</p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Update 3 (64 bits)</td>
   <td>A: Compatible</td>
   <td>Service Packs, parches acumulativos y actualizaciones de seguridad críticas</td>
  </tr>
  <tr>
   <td>CentOS 7 (64 bits)<sup> [6]</sup></td>
   <td>A: Compatible</td>
   <td>Service Packs, parches acumulativos y actualizaciones de seguridad críticas</td>
  </tr>
 </tbody>
</table>

#### Entorno virtualizado {#virtualized-environment}

Puede ejecutar AEM Forms en JEE en una máquina física o un entorno virtual. Sin embargo, si tiene algún problema con AEM Forms en un entorno virtual, intente replicar el problema en una máquina física. Si el problema persiste en la máquina física, póngase en contacto con el servicio de asistencia de Adobe para obtener una solución. Para los problemas que no puede replicar en una máquina física, póngase en contacto con el proveedor del entorno virtual.

#### Entornos de desarrollo {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plataforma (versión base)</strong></p> </th>
   <th>Nivel de soporte</th>
   <th><p><strong>Definiciones de parches compatibles</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 de 64 bits</p> </td>
   <td>E: Se espera que funcione</td>
   <td><p>Service Pack y actualizaciones críticas</p> </td>
  </tr>
 </tbody>
</table>

### Excepciones a plataformas de servidor compatibles {#exceptions-to-supported-server-platforms}

Tenga en cuenta las siguientes excepciones al elegir una plataforma para configurar AEM Forms en el servidor JEE.

1. AEM Forms en JEE no es compatible con IBM® WebSphere® con MySQL.
1. AEM Forms en JEE no es compatible con JBoss en SUSE Linux Enterprise Server 12. Solo IBM WebSphere es compatible con SUSE Linux Enterprise Server 12.
1. AEM Forms en JEE no es compatible con ningún JDK con JBoss® excepto Oracle Java™ SE.
1. AEM Forms en JEE no es compatible con ningún JDK con IBM® WebSphere® que no sea IBM® JDK.
1. El repositorio CRX admite la persistencia de tipo TarMK, MongoDB y bases de datos relacionales (RDBMK). No puede tener dos sistemas de base de datos diferentes entre el servidor de aplicaciones y el repositorio CRX. Sin embargo, en AEM Forms en un entorno JEE, puede utilizar MongoMK con el repositorio CRX y una base de datos relacional compatible con el servidor de aplicaciones.
1. AEM Forms en JEE no es compatible con el servidor de aplicaciones WebSphere en CentOS.
1. AEM Forms en JEE no es compatible con el control de acceso basado en roles JBoss (RBAC).
1. AEM Forms en JEE es compatible con el SDK de Oracle Java™ SE 11 (64 bits) solo para el servidor de aplicaciones JBoss EAP 7.4.

Además, tenga en cuenta los siguientes puntos a la hora de elegir software para Adobe AEM Forms en implementaciones JEE:

- AEM Forms en JEE admite actualizaciones, parches y paquetes de correcciones además de la versión principal y secundaria especificada del software compatible. Sin embargo, la actualización a la siguiente versión principal o secundaria no es compatible a menos que se especifique lo contrario.
- Las instalaciones basadas en clústeres no admiten la persistencia de TarMK. Para obtener información sobre la persistencia admitida, consulte [Seleccionar un tipo de persistencia para una instalación de AEM Forms](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- AEM Forms en JEE soporta varios software de terceros según nuestra [Directiva de soporte de software de terceros](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
- AEM Forms en JEE admite plataformas según la compatibilidad proporcionada por proveedores externos. Es posible que algunos proveedores externos no permitan algunas combinaciones. Por ejemplo, muchos proveedores no han certificado sus servidores de aplicaciones con Oracle. Como resultado, AEM Forms en JEE tampoco es compatible con estas combinaciones. Para asegurarse de elegir las versiones de software compatibles, compruebe la matriz de asistencia para los proveedores de terceros.
- AEM Forms en JEE no es compatible con el modo de espera pasiva TarMK.
- AEM Forms en JEE no es compatible con la agrupación en clúster vertical.
- AEM Forms en JEE no es compatible con la base de datos MySQL en un entorno agrupado.
- Para obtener la lista de plataformas quitadas o actualizadas, consulte el documento [Resumen de las nuevas características de AEM Forms 6.5](../../forms/using/whats-new.md).

### Servidores LDAP (opcional) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>Producto (versión base)</strong></p> </th>
   <th><p><strong>Definiciones de parches compatibles</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft Active Directory 2016</td>
   <td>Versiones de mantenimiento y paquetes de correcciones</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>Paquetes de características y correcciones provisionales</p> </td>
  </tr>
 </tbody>
</table>

### Servidores de correo electrónico (opcional) {#email-servers-optional}

| Producto |
| ----------------------- |
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
   <td>EMC Documentum</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>Servidor IBM Content Manager (Obsoleto) </td>
   <td>8.5 Paquete de correcciones 2</td>
  </tr>
  <tr>
   <td> Cliente de IBM Content Manager (Obsoleto)</td>
   <td>8.5 </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint </td>
   <td>2016 (Obsoleto)<br /> </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint </td>
   <td>2019<br /> </td>
  </tr>
 </tbody>
</table>

### Compatibilidad con Cordova {#support-for-cordova}

La aplicación de AEM Forms ahora es compatible con Apache Cordova. A continuación se muestran las versiones específicas de Cordova que son compatibles para cada plataforma:

- Apache Cordova 6.4.0
- Cordova iOS 4.3.0
- Cordova Android 6.0.0
- Cordova Windows 4.4.3

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
Además:
>
- El generador de PDF requiere una versión de 32 bits de [Acrobat 2020 Classic track versión 20.004.30006](https://helpx.adobe.com/es/acrobat/release-note/release-notes-acrobat-reader.html) o Acrobat 2017 versión 17.011.30078 para realizar la conversión.
- El generador de PDF solo admite la versión comercial de 32 bits de Microsoft Office Professional Plus y otro software necesario para la conversión.
- El generador de PDF no es compatible con Microsoft Office 365.
- Las conversiones del generador de PDF para OpenOffice solo son compatibles con Windows y Linux.
- Las características de PDF, Optimizar PDF y Exportar PDF de OCR solo son compatibles con Windows.
- Una versión de Acrobat se incluye con AEM Forms para habilitar la funcionalidad Generador de PDF. Solo se debe acceder a la versión agrupada mediante programación con AEM Forms, durante el período de licencia de AEM Forms, para usarlo con el generador de PDF de AEM Forms. Para obtener más información, consulte la descripción del producto de AEM Forms según la implementación ([Local](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-manager-on-premise.html) o [Servicios administrados](https://helpx.adobe.com/es/legal/product-descriptions/adobe-experience-manager-managed-services.html))”
>
- El servicio Generador de PDF no es compatible con Microsoft Windows 10.
- El PDF Generator no puede convertir archivos mediante Microsoft Visio 2019. Puede seguir utilizando Microsoft Visio 2016 para convertir archivos .VSD y .VSDX.
- El PDF Generator no puede convertir archivos con Microsoft Project 2019. Puede seguir utilizando Microsoft Project 2016 para convertir archivos .MPP.
>

### Excepciones a la compatibilidad con la accesibilidad {#exceptions-to-accessibility-support}

Los siguientes subsistemas de AEM Forms no son compatibles con [508](https://www.section508.gov/):

- IU de creación de formularios adaptables
- IU de creación de Forms Manager
- IU de creación de Administración de correspondencia
- IU de administración (IU de la consola de administración)

## Requisitos del sistema para AEM Forms en JEE {#system-requirements-for-aem-forms-on-jee}

### Requisitos mínimos de hardware {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Plataforma</td>
   <td>Requisitos mínimos de hardware</td>
  </tr>
  <tr>
   <td>Servidor Microsoft Windows</td>
   <td>Procesador Intel® Xeon® E5-2680 de 2,4 GHz o equivalente<br /> VMWare ESX 5.1 o posterior<br /> RAM: 6 GB (sistema operativo de 64 bits con JVM de 64 bits)<br /> Espacio libre en disco: 15 GB de espacio temporal más 22 GB<br /> para AEM Forms en JEE</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>Procesador Intel Xeon E5-2670v2, 1 vCPU, procesador de 2,5 GHz<br /> AWS m3.medium (3 ECU)<br /> RAM: 6 GB (sistema operativo de 64 bits con JVM de 64 bits)<br /> Espacio libre en disco: 6 GB de espacio temporal más 22 GB<br /> para AEM Forms en JEE</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>Procesador Intel Xeon E5-2670v2, 1 vCPU, procesador de 2,5 GHz<br /> AWS m3.medium (3 ECU)<br /> RAM: 6 GB (sistema operativo de 64 bits con JVM de 64 bits)<br /> Espacio libre en disco: 6 GB de espacio temporal más 22 GB<br /> para AEM Forms en JEE<br /> </td>
  </tr>
  <tr>
   <td>Requisitos de hardware para un entorno de producción pequeño</td>
   <td>
    <ul>
     <li><strong>Entorno Intel®</strong>: Intel® Xeon® E5-2680, 2,4 GHz o mayor. El uso de un procesador de doble núcleo mejorará aún más el rendimiento</li>
     <li><strong>Memoria: </strong>4 GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Para conocer los requisitos adicionales, consulte:

- [Requisitos del sistema para AEM Forms de un solo servidor en una implementación JEE](https://www.adobe.com/go/learn_aemforms_sysreq_single_65_es)
- [Requisitos del sistema para una implementación de AEM Forms en clúster en JEE](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65_es)

## Clientes compaitbles para AEM Forms en JEE {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plataforma</strong></p> </th>
   <th><p><strong>Definiciones de parches compatibles</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 (Enterprise, Pro, Basic)</p> <p>Versión de 32 o 64 bits</p> <p> </p> </td>
   <td>Service Packs y actualizaciones críticas</td>
  </tr>
  <tr>
   <td>Servidor Microsoft® Windows® 2016</td>
   <td>Service Packs y actualizaciones críticas</td>
  </tr>
 </tbody>
</table>

- Espacio en disco para la instalación: 1,7 GB solo para Workbench, 2,7 GB en una sola unidad para una instalación completa de Workbench, Designer y el conjunto de muestras 400 MB para directorios de instalación temporales: 200 MB en el directorio temporal del usuario y 200 MB en el directorio temporal de Windows. Si todas estas ubicaciones residen en una sola unidad, deberá haber 1,5 GB de espacio disponible durante la instalación. Los archivos copiados en los directorios temporales se eliminan cuando finaliza la instalación.

- Memoria para ejecutar Workbench: 2 GB de RAM
- Requisitos de hardware: Procesador Intel® Pentium® 4 o AMD equivalente, 1 GHz
- Resolución mínima de pantalla de 1024 x 768 píxeles o buena resolución de pantalla de 16 bits a color o superior
- Conexión de red TCP/IPv4 o TCP/IPv6 a AEM Forms en el servidor JEE
- Debe tener privilegios de administrador para instalar Workbench en Windows. Si va a realizar la instalación con una cuenta que no sea de administrador, el instalador le pedirá las credenciales de una cuenta adecuada.

### Designer {#designer}

- Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server o Microsoft® Windows® 10
- Procesador de 1 GHz o más rápido con soporte para PAE, NX y SSE2.
- 1 GB de RAM para 32 bits o 2 GB de RAM para SO de 64 bits;
- 16 GB de espacio en disco para 32 bits o 20 GB de espacio en disco para el sistema operativo de 64 bits
- Memoria gráfica: 128 MB de GPU (se recomiendan 256 MB);
- 2,35 GB de espacio disponible en disco duro;
- 1024 X 768 píxeles de resolución de monitor o superior;
- Aceleración de hardware de vídeo (opcional);
- Acrobat Pro DC, Acrobat Standard DC o Adobe Acrobat Reader DC;
- Privilegios administrativos para instalar Designer.

### Adobe Acrobat y Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat y Adobe Reader (Base)</strong></p> </th>
   <th><p><strong>Definiciones de parches compatibles</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2020 (Classic track)</td>
   <td>Versión 20.004.30006 o posterior<br /> </td>
  </tr>
  <tr>
   <td>Acrobat 2017 (Classic track) (Obsoleto)</td>
   <td>Versión 17.011.30078 o posterior<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
>
La familia de productos de Acrobat DC presenta dos tracks tanto para Acrobat como para Reader, que son productos diferentes: “Classic” y “Continuous”. Para obtener detalles y una comparación de ambas, consulte [https://www.adobe.com/go/acrobatdctracks](https://www.adobe.com/go/acrobatdctracks).

### Exploradores {#browsers}

#### Equipos de escritorio {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>Explorador (base)</strong></p> </th>
   <th><p><strong>Niveles de soporte</strong></p> </th>
   <th><p><strong>Definiciones de parches compatibles</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft Edge (Evergreen)</p> </td>
   <td><p>A: Compatible</p> </td>
   <td><p>Service Packs y actualizaciones</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox (Evergreen)</p> </td>
   <td><p>A: Compatible</p> </td>
   <td>Todas las actualizaciones</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ESR</td>
   <td>E: Se espera que funcione</td>
   <td> Todas las actualizaciones</td>
  </tr>
  <tr>
   <td><p>Google Chrome (Evergreen)</p> </td>
   <td><p>A: Compatible</p> </td>
   <td>Todas las actualizaciones</td>
  </tr>
  <tr>
   <td>Apple Safari en macOS</td>
   <td>A: Compatible</td>
   <td>Todas las actualizaciones</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
Algunas excepciones relacionadas con el explorador para los escritorios son las siguientes:
>
- Safari solo es compatible con Macintosh OS X.
- Workspace es compatible con Safari 5.1 en Macintosh OS X 10.6 y 10.7 con Acrobat DC o versiones posteriores. Para obtener más información sobre la compatibilidad de Safari 5.1 con Adobe Reader, Acrobat, consulte [https://helpx.adobe.com/es/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/es/x-productkb/multi/safari-5-1-incompatible-reader.html).
- Safari no es compatible con la consola de administración.
- Administración de correspondencia no es compatible con Windows® Internet Explorer 9.0 para formularios AEM 6.1.
- El portal de formularios admite software de lector de pantalla JAWS 14.0 en Internet Explorer 11 para accesibilidad.

#### Clientes móviles {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>Explorador (base)</strong></p> </th>
   <th><p><strong>Definiciones de parches compatibles</strong></p> </th>
  </tr>
  <tr>
   <td><p>Chrome en Android™ 4.1.2 y superior</p> </td>
   <td><p>Todas las actualizaciones</p> </td>
  </tr>
  <tr>
   <td>Safari en iOS 15.1 y versiones posteriores</td>
   <td>Todas las actualizaciones</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>Todas las actualizaciones<br /> </td>
  </tr>
  <tr>
   <td>Explorador Android nativo en Android™ 4.4 y versiones posteriores</td>
   <td>Todas las actualizaciones</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
- El portal de formularios solo es compatible con Safari en iPad.

### Aplicación de AEM Forms {#aem-forms-workspace-app}

#### Compatibilidad con dispositivos móviles {#mobile-device-support}

La aplicación de AEM Forms está disponible en las siguientes plataformas:

| **Plataforma** | **Dispositivos compatibles** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS | Apple iPhone, iPad, iPad Air y iPad mini que ejecuten iOS 15.1 y versiones posteriores. |
| Google Android | Android 5.1 y versiones posteriores. La aplicación de AEM Forms está certificada para tabletas Samsung Galaxy de 7 y 10 pulgadas y en teléfonos inteligentes populares. |
| Microsoft Windows | Dispositivos Microsoft Surface, tabletas, portátiles y equipos de escritorio que ejecuten el sistema operativo Microsoft Windows 10. |

### Extensión de seguridad para documentos de Adobe para Microsoft Office {#adobe-rights-management-extension-for-microsoft-office}

Haga clic [aquí](https://www.adobe.com/es/products/livecycle/rightsmanagement/extension/downloads.html) para ver los requisitos del sistema para la extensión de seguridad para documentos de Adobe para Microsoft® Office.

### Excepciones al soporte de clientes {#exceptions-to-client-support}

AEM Forms en JEE admite actualizaciones, parches y paquetes de correcciones además de la versión principal y secundaria especificada del software compatible. Sin embargo, la actualización a la siguiente versión principal o secundaria no es compatible a menos que se especifique lo contrario.

## Directiva de compatibilidad de parches de terceros {#third-party-patch-support-policy}

Los requisitos de software de terceros para AEM Forms en JEE se documentan en la sección “Requisitos del sistema” de sus respectivos documentos de producto. Puede acceder a toda la documentación desde [https://adobe.com/go/learn_aemforms_documentation_65_es](https://adobe.com/go/learn_aemforms_documentation_65_es) .

AEM Forms en plataformas de referencia de terceros de JEE indica el nivel de parche específico de la infraestructura de terceros que se actualizó durante el desarrollo y lanzamiento de AEM Forms en JEE, y desde el nivel mínimo de parches/service pack de la infraestructura compatible con esa versión de AEM Forms en JEE.

Adobe es compatible con parches urgentes o recomendados que emitan proveedores de terceros en el momento de su lanzamiento, siempre que los proveedores de terceros garanticen la compatibilidad con versiones anteriores compatibles con AEM Forms en JEE. Adobe solo será compatible con parches publicados después del nivel mínimo de parches indicado en la documentación de AEM Forms en JEE.

En algunos casos, Adobe no será compatible con actualizaciones de terceros que cambien la funcionalidad principal y, por lo tanto, no admite la compatibilidad total con versiones anteriores. Para obtener más información sobre las actualizaciones compatibles, consulte [Definiciones de parches compatibles](https://helpx.adobe.com/es/aem-forms/aem-forms-third-party-software-patch.html) para productos de proveedores específicos y los tipos de parches compatibles con Adobe.

En circunstancias que escapan al control del Adobe, los parches de terceros que afirman ser compatibles con versiones anteriores pueden tener un impacto negativo en los productos de Adobe o en los entornos de los clientes. En estos casos, Adobe recomienda que los clientes evalúen el impacto de cualquier parche urgente de un tercero antes de aplicarlo a sistemas críticos. Adobe colaborará con terceros mediante esfuerzos comerciales razonables para resolver estos problemas, ya sea mediante programas normales de compatibilidad de Adobe o por terceros que corrijan el problema en su parche. Esto no garantiza que un parche de terceros recién lanzado que sea compatible con Adobe funcione según lo documentado por el proveedor o con AEM Forms en JEE.

Adobe se reserva el derecho de cambiar las plataformas de referencia de terceros compatibles con AEM Forms en la versión JEE y sus definiciones de parches compatibles en cualquier momento.

Para obtener información adicional sobre parches de terceros, consulte los artículos de la base de conocimientos relacionados con su producto en el sitio de soporte técnico de Adobe Enterprise.

## Actualizaciones de plataforma {#platform-updates}

Las siguientes plataformas están marcadas como obsoletas con la versión 6.5.13.0 de AEM Forms del 2 de junio de 2022:

- Microsoft SharePoint 2016

Las siguientes plataformas están marcadas como obsoletas con la versión 6.5.12.0 de AEM Forms del 3 de marzo de 2022:

- MongoDB Enterprise 4.0
- IBM DB2 11.1
- Base de datos de Oracle 12c Release 2
- MySQL 5.7.35
- Controlador JDBC del servidor Microsoft® SQL 6.2.1.0
- Plataforma de aplicaciones empresariales JBoss® (EAP) 7.1.4
- IBM Content Manager Server 8.5 Fix pack 2
- Cliente de IBM Content Manager 8.5
- Servidor Microsoft SQL 2016

Las siguientes plataformas están marcadas como obsoletas con la versión 6.5.10.0 de AEM Forms del 7 de septiembre de 2021:

- Adobe Acrobat 2017: [La compatibilidad principal con Adobe Acrobat 2017 finaliza el 6 de junio de 2022](https://helpx.adobe.com/es/support/programs/eol-matrix.html).
- Servidor Microsoft Windows 2016 (64 bits)
- Red Hat Enterprise Linux 7 (Kernel 3.x) (64 bits)
- Microsoft® Office 2016
- OpenOffice 4.1.2

>[!NOTE]
>
Las plataformas marcadas como [obsoletas con AEM Forms 6.5.12.0 y 6.5.10.0 seguirán siendo compatibles hasta la versión de AEM Forms 6.5 Service Pack 18 (6.5.18.0)](https://helpx.adobe.com/es/support/programs/eol-matrix.html).

## Historial de revisiones {#revision-history}

- 01 de septiembre de 2022

   - Se ha agregado compatibilidad con el SDK de Oracle Java™ SE 11 (64 bits) para el servidor de aplicaciones JBoss EAP 7.4.

- 03 de marzo de 2022

   - Se ha quitado la compatibilidad con lo siguiente:
      - Máquina virtual IBM® J9 (versión 2.8, JRE 1.8.0)
      - Base de datos de Oracle 12c Release 1
      - Base de datos de Oracle 18c
      - Oracle Unified Directory (OUD) 11g Release 2
      - IBM Lotus Domino 9.0
      - IBM Filenet 5.2
      - Adobe Flash Player

- 10 de octubre de 2021

   - Se ha cambiado la versión compatible de iOS para la aplicación de AEM Forms a iOS 15.1. La versión anterior era iOS 12.

- 07 de septiembre de 2021
   - **Actualizaciones de plataforma**: [!DNL Adobe Experience Manager Forms] en JEE se ha agregado compatibilidad con las siguientes plataformas:
      - [!DNL Adobe Acrobat 2020]
      - [!DNL Ubuntu 20.04]
      - [!DNL Open Office 4.1.10]
      - [!DNL Microsoft Office 2019]
      - [!DNL Microsoft Windows Server 2019]
      - [!DNL RHEL8]

- 3 de diciembre de 2020
   - Se agregó compatibilidad con AEM Forms 6.5.7.0 o posterior para la siguiente plataforma:
      - [!DNL Microsoft SQL Server 2019]

- 9 de septiembre de 2020

   - Se ha cambiado la versión compatible de iOS para la aplicación de AEM Forms a iOS 12. La versión anterior era iOS 11.
