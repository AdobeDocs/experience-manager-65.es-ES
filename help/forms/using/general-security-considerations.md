---
title: Consideraciones generales de seguridad para AEM Forms en JEE
seo-title: Consideraciones generales de seguridad para AEM Forms en JEE
description: Aprenda a prepararse para endurecer su AEM Forms en un entorno JEE.
seo-description: Aprenda a prepararse para endurecer su AEM Forms en un entorno JEE.
uuid: 4d098731-fc8f-41d7-98b5-5c2e31211614
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 64bc6018-2828-4634-9275-48f1d411452b
docset: aem65
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---


# Consideraciones generales de seguridad para AEM Forms en JEE{#general-security-considerations-for-aem-forms-on-jee}

Este artículo proporciona información introductoria que le ayuda a prepararse para endurecer su entorno de AEM Forms. Incluye información previa sobre AEM Forms en JEE, sistema operativo, servidor de aplicaciones y seguridad de bases de datos. Revise esta información antes de seguir bloqueando el entorno.

## Información de seguridad específica del proveedor {#vendor-specific-security-information}

Esta sección contiene información relacionada con la seguridad sobre sistemas operativos, servidores de aplicaciones y bases de datos que se incorporan a su solución AEM Forms en JEE.

Utilice los vínculos de esta sección para encontrar información de seguridad específica del proveedor para su sistema operativo, base de datos y servidor de aplicaciones.

### Información de seguridad del sistema operativo {#operating-system-security-information}

Al proteger el sistema operativo, considere detenidamente implementar las medidas descritas por el proveedor del sistema operativo, entre las que se incluyen las siguientes:

* Definición y control de usuarios, funciones y privilegios
* Monitorización de registros y pistas de auditoría
* Eliminación de servicios y aplicaciones innecesarios
* Copia de seguridad de archivos

Para obtener información de seguridad sobre los sistemas operativos compatibles con AEM Forms en JEE, consulte los recursos de la tabla:

<table>
 <thead>
  <tr>
   <th><p>Sistema operativo</p> </th>
   <th><p>Recurso de seguridad</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® AIX® 7.2</p> </td>
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">Beneficios de seguridad de IBM AIX</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Guía de seguridad de Windows Server 2016</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP o ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Guía de seguridad de Red Hat Enterprise Linux</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">Directrices de seguridad y endurecimiento</a></p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Update 3</td>
   <td><a href="https://docs.oracle.com/cd/E52668_01/E54670/E54670.pdf" target="_blank">Guía de seguridad de la versión 7</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">Documentación de protección</a></td>
  </tr>
 </tbody>
</table>

### Información de seguridad del servidor de aplicaciones {#application-server-security-information}

Al proteger el servidor de aplicaciones, considere detenidamente implementar las medidas descritas por el proveedor del servidor, entre las que se incluyen las siguientes:

* Uso de nombres de usuario de administrador no obvios
* Desactivación de servicios innecesarios
* Protección del administrador de la consola
* Habilitar cookies seguras
* Cierre de puertos innecesarios
* Limitación de clientes por direcciones IP o dominios
* Uso del Administrador de seguridad de Java™ para restringir privilegios mediante programación

Para obtener información de seguridad sobre los servidores de aplicaciones compatibles con AEM Forms en JEE, consulte los recursos de esta tabla.

<table>
 <thead>
  <tr>
   <th><p>Servidor de aplicaciones</p> </th>
   <th><p>Recurso de seguridad</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Oracle WebLogic®</p> </td>
   <td><p>Busque Información sobre la seguridad de WebLogic en <a href="https://download.oracle.com/docs/">https://download.oracle.com/docs/</a>.</p> </td>
  </tr>
  <tr>
   <td><p>IBM WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">Protección de las aplicaciones y su entorno</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security+subsystem+configuration">Configuración del subsistema de seguridad</a></p> </td>
  </tr>
 </tbody>
</table>

### Información de seguridad de la base de datos {#database-security-information}

Al proteger la base de datos, considere la posibilidad de implementar las medidas descritas por el proveedor de la base de datos, entre las que se incluyen las siguientes:

* Restricción de operaciones con listas de control de acceso (ACL)
* Uso de puertos no estándar
* Ocultar la base de datos detrás de un cortafuegos
* Codificación de datos confidenciales antes de escribirlos en la base de datos (consulte la documentación del fabricante de la base de datos)

Para obtener información de seguridad sobre las bases de datos compatibles con AEM Forms en JEE, consulte los recursos de esta tabla.

<table>
 <thead>
  <tr>
   <th><p>Base de datos</p> </th>
   <th><p>Recurso de seguridad</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">Biblioteca de la familia de productos DB2</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td>Buscar en la Web "SQL Server 2016: Seguridad"</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">Problemas generales de seguridad de MySQL 5.0</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">Problemas generales de seguridad de MySQL 5.1</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle® 12c</p> </td>
   <td><p>Consulte el capítulo Seguridad en la <a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">documentación de Oracle 12g</a></p> </td>
  </tr>
 </tbody>
</table>

Esta tabla describe los puertos predeterminados que se deben abrir durante el proceso de configuración de AEM Forms en JEE. Si se conecta a través de https, ajuste la información del puerto y las direcciones IP en consecuencia. Para obtener más información sobre la configuración de puertos, consulte el documento *Instalación e implementación de AEM Forms en JEE* para su servidor de aplicaciones.

<table>
 <thead>
  <tr>
   <th><p>Producto o servicio</p> </th>
   <th><p>Número de puerto</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss</p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLogic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Servidor administrado por WebLogic</p> </td>
   <td><p>Definido por el administrador durante la configuración</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere</p> </td>
   <td><p>9060, si Seguridad global está habilitada, el valor predeterminado del puerto SSL es 9043.</p> <p>9080</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Servidor BAM</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SOAP</p> </td>
   <td><p>8880</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>MySQL</p> </td>
   <td><p>3306</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Oracle</p> </td>
   <td><p>1521</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>DB2</p> </td>
   <td><p>50000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>Puerto en el que se está ejecutando el servidor LDAP. El puerto predeterminado suele ser 389. Sin embargo, si selecciona la opción SSL, el puerto predeterminado suele ser 636. Confirme con su administrador LDAP qué puerto especificar.</p> </td>
  </tr>
 </tbody>
</table>

### Configuración de JBoss para utilizar un puerto HTTP no predeterminado {#configuring-jboss-to-use-a-non-default-http-port}

El servidor de aplicaciones JBoss utiliza 8080 como puerto HTTP predeterminado. JBoss también tiene puertos preconfigurados 8180, 8280 y 8380, que se comentan en el archivo jboss-service.xml. Si tiene una aplicación en el equipo que ya utiliza este puerto, cambie el puerto que utiliza AEM Forms en JEE siguiendo estos pasos:

1. Abra el siguiente archivo para editarlo:

   Instalación de un solo servidor: [Raíz de JBoss]/standalone/configuration/standalone.xml

   Instalaciones de clúster: [Raíz de JBoss]/domain/configuration/domain.xml

1. Cambie el valor del atributo **port** en la etiqueta **&lt;socket-binding>** por un número de puerto personalizado. Por ejemplo, los siguientes usan el puerto 8090:

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot; />

1. Guarde y cierre el archivo.
1. Reinicie el servidor de aplicaciones JBoss.

## AEM Forms en consideraciones de seguridad JEE {#aem-forms-on-jee-security-considerations}

En esta sección se describen algunos problemas de seguridad específicos de JEE de AEM Forms que debe conocer.

### Las credenciales de correo electrónico no están cifradas en la base de datos {#email-credentials-not-encrypted-in-database}

Las credenciales de correo electrónico almacenadas por las aplicaciones no se cifran antes de almacenarse en la base de datos de AEM Forms en JEE. Al configurar un extremo de servicio para que utilice el correo electrónico, la información de contraseña utilizada como parte de esa configuración de extremo no se cifra cuando se almacena en la base de datos.

### Contenido confidencial para el Rights Management en la base de datos {#sensitive-content-for-rights-management-in-the-database}

AEM Forms en JEE utiliza la base de datos AEM Forms en JEE para almacenar información confidencial de claves de documentos y otro material criptográfico que se utiliza para documentos de políticas. Proteger la base de datos contra intrusiones ayuda a proteger esta información confidencial.

### Contraseña en forma de texto claro {#password-in-clear-text-format-in-adobe-ds-xml}

El servidor de aplicaciones que se utiliza para ejecutar AEM Forms en JEE requiere su propia configuración para acceder a la base de datos a través de una fuente de datos configurada en el servidor de aplicaciones. Asegúrese de que el servidor de aplicaciones no exponga la contraseña de la base de datos en texto claro en su archivo de configuración de la fuente de datos.

El archivo lc_[database].xml no debe contener contraseña en formato de texto claro. Consulte con el proveedor del servidor de aplicaciones cómo cifrar estas contraseñas para su servidor de aplicaciones.

>[!NOTE]
>
>El instalador llave en mano de AEM Forms en JEE JBoss cifra la contraseña de la base de datos.

IBM WebSphere Application Server y Oracle WebLogic Server pueden cifrar contraseñas de fuentes de datos de forma predeterminada. Sin embargo, confirme con la documentación del servidor de aplicaciones para asegurarse de que esto sucede.

### Protección de la clave privada almacenada en el almacén de confianza {#protecting-the-private-key-stored-in-trust-store}

Las claves privadas o credenciales importadas en el almacén de confianza se almacenan en AEM Forms en la base de datos JEE. Tenga las precauciones adecuadas para proteger la base de datos y restringir el acceso solo a los administradores designados.
