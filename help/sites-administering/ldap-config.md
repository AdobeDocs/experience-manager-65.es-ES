---
title: AEM Configuración de LDAP con 6
seo-title: Configuring LDAP with AEM 6
description: AEM Obtenga información sobre cómo configurar LDAP con el uso de la.
seo-description: Learn how to configure LDAP with AEM.
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 0%

---

# AEM Configuración de LDAP con 6 {#configuring-ldap-with-aem}

LDAP (el **L** peso ligero **D** directorio **A** Acceso **P** protocolo) se utiliza para acceder a los servicios de directorio centralizados. Esto ayuda a reducir el esfuerzo necesario para administrar las cuentas de usuario, ya que varias aplicaciones pueden acceder a ellas. Uno de estos servidores LDAP es Active Directory. LDAP se utiliza a menudo para lograr el inicio de sesión único, que permite al usuario acceder a varias aplicaciones después de iniciar sesión una vez.

Las cuentas de usuario se pueden sincronizar entre el servidor LDAP y el repositorio, y los detalles de la cuenta LDAP se guardan en el repositorio. Esto permite asignar las cuentas a grupos de repositorios para asignar los permisos y privilegios necesarios.

El repositorio utiliza la autenticación LDAP para autenticar a estos usuarios, con credenciales que se pasan al servidor LDAP para su validación, que es necesaria antes de permitir el acceso al repositorio. Para mejorar el rendimiento, el repositorio puede almacenar en caché las credenciales validadas correctamente, con un tiempo de espera de caducidad para garantizar que la revalidación se produzca después de un periodo adecuado.

Cuando se elimina una cuenta del servidor LDAP, ya no se concede la validación y, por lo tanto, se deniega el acceso al repositorio. Los detalles de las cuentas LDAP guardadas en el repositorio también se pueden purgar.

El uso de dichas cuentas es transparente para los usuarios, ya que no ven ninguna diferencia entre las cuentas de usuario y de grupo creadas a partir de LDAP y las creadas únicamente en el repositorio.

AEM En el 6 de marzo, la compatibilidad con LDAP viene con una nueva implementación que requiere un tipo de configuración diferente a la de las versiones anteriores.

Todas las configuraciones de LDAP están ahora disponibles como configuraciones de OSGi. Se pueden configurar mediante la consola de administración web en:
`https://serveraddress:4502/system/console/configMgr`

AEM Para que LDAP funcione con la, debe crear tres configuraciones OSGi:

1. Un proveedor de identidad LDAP (IDP).
1. Un controlador de sincronización.
1. Un módulo de inicio de sesión externo.

>[!NOTE]
>
>Ver [Módulo de inicio de sesión externo de Oak: autenticación con LDAP y versiones posteriores](https://docs.adobe.com/content/ddc/en/gems/oak-s-external-login-module---authenticating-with-ldap-and-beyon.html#) para profundizar en los módulos de inicio de sesión externo.
>
>Para leer un ejemplo de configuración de Experience Manager con Apache DS, consulte [Configuración de Adobe Experience Manager 6.5 para utilizar el servicio de directorio de Apache.](https://helpx.adobe.com/experience-manager/using/configuring-aem64-apache-directory-service.html)

## Configuración del proveedor de identidad LDAP {#configuring-the-ldap-identity-provider}

El proveedor de identidad LDAP se utiliza para definir cómo se recuperan los usuarios del servidor LDAP.

Se encuentra en la consola de administración, en **Proveedor de identidad LDAP Apache Jackrabbit Oak** nombre.

Las siguientes opciones de configuración están disponibles para el proveedor de identidad LDAP:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre de proveedor LDAP</strong></td>
   <td>Nombre de esta configuración de proveedor LDAP.</td>
  </tr>
  <tr>
   <td><strong>Nombre de host del servidor LDAP</strong><br /> </td>
   <td>Nombre de host del servidor LDAP</td>
  </tr>
  <tr>
   <td><strong>Puerto del servidor LDAP</strong></td>
   <td>Puerto del servidor LDAP</td>
  </tr>
  <tr>
   <td><strong>Usar SSL</strong></td>
   <td>Indica si se debe utilizar una conexión SSL (LDAP).</td>
  </tr>
  <tr>
   <td><strong>Usar TLS</strong></td>
   <td>Indica si TLS debe iniciarse en las conexiones.</td>
  </tr>
  <tr>
   <td><strong>Deshabilitar comprobación de certificados</strong></td>
   <td>Indica si la validación de certificados de servidor debe deshabilitarse.</td>
  </tr>
  <tr>
   <td><strong>Enlazar DN</strong></td>
   <td>DN del usuario para la autenticación. Si se deja vacío, se realizará un enlace anónimo.</td>
  </tr>
  <tr>
   <td><strong>Contraseña de enlace</strong></td>
   <td>Contraseña del usuario para la autenticación</td>
  </tr>
  <tr>
   <td><strong>Tiempo de espera de búsqueda</strong></td>
   <td>Tiempo hasta que finaliza la búsqueda</td>
  </tr>
  <tr>
   <td><strong>Grupo de administradores máximo activo</strong></td>
   <td>Tamaño máximo activo del grupo de conexión de administrador.</td>
  </tr>
  <tr>
   <td><strong>Grupo de usuarios máximo activo</strong></td>
   <td>Tamaño máximo activo del grupo de conexión de usuario.</td>
  </tr>
  <tr>
   <td><strong>DN base de usuario</strong></td>
   <td>DN para búsquedas de usuarios</td>
  </tr>
  <tr>
   <td><strong>Clases de objeto de usuario</strong></td>
   <td>La lista de clases de objeto que debe contener una entrada de usuario.</td>
  </tr>
  <tr>
   <td><strong>Atributo de ID de usuario</strong></td>
   <td>Nombre del atributo que contiene el ID de usuario.</td>
  </tr>
  <tr>
   <td><strong>Filtro adicional de usuario</strong></td>
   <td>Filtro LDAP adicional que se utiliza al buscar usuarios. El filtro final tiene el siguiente formato: '(&amp;(&lt;idattr&gt;=&lt;userid&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>Rutas DN de usuario</strong></td>
   <td>Controla si el DN debe utilizarse para calcular una parte de la ruta intermedia.</td>
  </tr>
  <tr>
   <td><strong>DN base de grupo</strong></td>
   <td>DN base para búsquedas de grupo.</td>
  </tr>
  <tr>
   <td><strong>Agrupar clases de objeto</strong></td>
   <td>La lista de clases de objeto que debe contener una entrada de grupo.</td>
  </tr>
  <tr>
   <td><strong>Atributo de nombre de grupo</strong></td>
   <td>Nombre del atributo que contiene el nombre del grupo.</td>
  </tr>
  <tr>
   <td><strong>Filtro adicional de grupo</strong></td>
   <td>Filtro LDAP adicional que se utilizará al buscar grupos. El filtro final tiene el siguiente formato: '(&amp;(&lt;nameattr&gt;=&lt;groupname&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Agrupar rutas DN</strong></td>
   <td>Controla si el DN debe utilizarse para calcular una parte de la ruta intermedia.</td>
  </tr>
  <tr>
   <td><strong>Atributo de miembro de grupo</strong></td>
   <td>Atributo de grupo que contiene los miembros de un grupo.</td>
  </tr>
 </tbody>
</table>

## Configuración Del Controlador De Sincronización {#configuring-the-synchronization-handler}

El controlador de sincronización definirá cómo se sincronizarán los usuarios y grupos del proveedor de identidad con el repositorio.

Se encuentra bajo la **Controlador de sincronización predeterminado Apache Jackrabbit Oak** nombre en la consola de administración.

Las siguientes opciones de configuración están disponibles para el Controlador de sincronización:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre del controlador de sincronización</strong></td>
   <td>Nombre de la configuración de sincronización.</td>
  </tr>
  <tr>
   <td><strong>Hora de caducidad del usuario</strong></td>
   <td>Duración hasta que caduque un usuario sincronizado.</td>
  </tr>
  <tr>
   <td><strong>Abono automático de usuario</strong></td>
   <td>Lista de grupos a los que se agrega automáticamente un usuario sincronizado.</td>
  </tr>
  <tr>
   <td><strong>Asignación de propiedades de usuario</strong></td>
   <td>Definición de asignación de lista de propiedades locales de propiedades externas.</td>
  </tr>
  <tr>
   <td><strong>Prefijo de ruta de usuario</strong></td>
   <td>Prefijo de ruta utilizado al crear nuevos usuarios.</td>
  </tr>
  <tr>
   <td><strong>Caducidad de abono de usuario</strong></td>
   <td>Tiempo tras el cual caduca la pertenencia.<br /> </td>
  </tr>
  <tr>
   <td><strong>Profundidad de anidación de pertenencia a usuario</strong></td>
   <td>Devuelve la profundidad máxima de anidamiento de grupos cuando se sincronizan las relaciones de pertenencia. Un valor de 0 deshabilita de forma efectiva la búsqueda de miembros del grupo. El valor 1 solo agrega los grupos directos de un usuario. Este valor no tiene ningún efecto cuando se sincronizan grupos individuales únicamente cuando se sincroniza una ascendencia de pertenencia de usuarios.</td>
  </tr>
  <tr>
   <td><strong>Tiempo de vencimiento del grupo</strong></td>
   <td>Duración hasta que caduque un grupo sincronizado.</td>
  </tr>
  <tr>
   <td><strong>Pertenencia automática al grupo</strong></td>
   <td>Lista de grupos a los que se agrega automáticamente un grupo sincronizado.</td>
  </tr>
  <tr>
   <td><strong>Asignación de propiedades de grupo</strong></td>
   <td>Definición de asignación de lista de propiedades locales de propiedades externas.</td>
  </tr>
  <tr>
   <td><strong>Prefijo de ruta de grupo</strong></td>
   <td>Prefijo de ruta utilizado al crear nuevos grupos.</td>
  </tr>
 </tbody>
</table>

## El módulo de inicio de sesión externo {#the-external-login-module}

El módulo de inicio de sesión externo se encuentra en **Módulo de inicio de sesión externo de Apache Jackrabbit Oak** en la consola de administración.

>[!NOTE]
>
>El módulo de inicio de sesión externo Apache Jackrabbit Oak implementa las especificaciones del Servicio de autenticación y autorización de Java (JAAS). Consulte la [oracle oficial Guía de referencia de seguridad de Java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) para obtener más información.

Su trabajo es definir qué proveedor de identidad y controlador de sincronización utilizar, enlazando de forma eficaz los dos módulos.

Estas son las opciones de configuración disponibles:

| **Clasificación JAAS** | Especificar la clasificación (es decir, el criterio de ordenación) de esta entrada del módulo de inicio de sesión. Las entradas se ordenan en orden descendente (es decir, las configuraciones con mayor valor clasificado son las primeras). |
|---|---|
| **Indicador de control de JAAS** | Propiedad que especifica si un LoginModule es OBLIGATORIO, REQUERIDO, SUFICIENTE u OPCIONAL. Consulte la documentación de configuración de JAAS para obtener más información sobre el significado de estos indicadores. |
| **Dominio JAAS** | El nombre de territorio (o nombre de aplicación) con el que se va a registrar LoginModule. Si no se proporciona ningún nombre de dominio kerberos, LoginModule se registra con un dominio kerberos predeterminado, tal como se ha configurado en la configuración de Felix JAAS. |
| **Nombre del proveedor de identidad** | Nombre del proveedor de identidad. |
| **Nombre del controlador de sincronización** | Nombre del controlador de sincronización. |

>[!NOTE]
>
>AEM Si planea tener más de una configuración LDAP con la instancia de la instancia de, es necesario crear proveedores de identidad y controladores de sincronización independientes para cada configuración.

## Configuración de LDAP sobre SSL {#configure-ldap-over-ssl}

AEM Se puede configurar 6 para que se autentique con LDAP a través de SSL siguiendo el siguiente procedimiento:

1. Compruebe la **Usar SSL** o **Usar TLS** casillas de verificación al configurar [Proveedor de identidad LDAP](#configuring-the-ldap-identity-provider).
1. Configure el controlador de sincronización y el módulo de inicio de sesión externo según la configuración.
1. Instale los certificados SSL en su VM de Java si es necesario. Esto se puede hacer con keytool:

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Pruebe la conexión con el servidor LDAP.

### Creación de certificados SSL {#creating-ssl-certificates}

AEM Los certificados autofirmados se pueden utilizar al configurar la autenticación con LDAP a través de SSL. AEM A continuación se muestra un ejemplo de un procedimiento de trabajo para generar certificados para su uso con la.

1. Asegúrese de tener una biblioteca SSL instalada y en funcionamiento. Este procedimiento utilizará OpenSSL como ejemplo.

1. Cree un archivo de configuración OpenSSL (cnf) personalizado. Esto se puede hacer copiando el archivo de configuración **openssl.cnf ** predeterminado y personalizándolo. En sistemas UNIX, normalmente se encuentra en `/usr/lib/ssl/openssl.cnf`

1. Continúe creando la clave raíz de la CA ejecutando el siguiente comando en un terminal:

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. A continuación, cree un nuevo certificado autofirmado:

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Inspect utiliza el certificado recién generado para asegurarse de que todo está en orden:

   `openssl x509 -noout -text -in root-ca.crt`

1. Asegúrese de que existen todas las carpetas especificadas en el archivo de configuración de certificado (.cnf). Si no es así, créelos.
1. Cree una semilla aleatoria ejecutando, por ejemplo:

   `openssl rand -out private/.rand 8192`

1. Mueva los archivos .pem creados a las ubicaciones configuradas en el archivo .cnf.

1. Finalmente, agregue el certificado al repositorio de claves Java.

## Habilitar el registro de depuración {#enabling-debug-logging}

El registro de depuración se puede habilitar tanto para el proveedor de identidad LDAP como para el módulo de inicio de sesión externo para solucionar los problemas de conexión.

Para habilitar el registro de depuración, debe:

1. Vaya a la consola de administración web.
1. Busque &quot;Configuración del registrador de Apache Sling&quot; y cree dos registradores con las siguientes opciones:

* Nivel de registro: depuración
* Archivo de registro logs/ldap.log
* Patrón de mensajes: {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Registrador: org.apache.jackrabbit.oak.security.authentication.ldap

* Nivel de registro: depuración
* Archivo de registro: logs/external.log
* Patrón de mensajes: {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Registrador: org.apache.jackrabbit.oak.spi.security.authentication.external

## Una palabra sobre afiliación grupal {#a-word-on-group-affiliation}

AEM Los usuarios sincronizados a través de LDAP pueden formar parte de diferentes grupos en el espacio de trabajo de. AEM Estos grupos pueden ser grupos LDAP externos que se agregarán a los grupos como parte del proceso de sincronización, pero también pueden ser grupos que se agregan por separado y que no forman parte del esquema de afiliación original del grupo LDAP.

AEM En la mayoría de los casos, estos pueden ser grupos agregados por un administrador de la red local de identidad o por cualquier otro proveedor de identidad.

AEM Si se elimina un usuario de un grupo en el servidor LDAP, el cambio también se reflejará en el lado del usuario tras la sincronización. El cambio también se reflejará en el lado del usuario en el que se haya realizado la sincronización. Sin embargo, todas las demás afiliaciones de grupo del usuario que no fueron agregadas por LDAP permanecerán en su lugar.

AEM y gestiona la depuración de usuarios de grupos externos utilizando `rep:externalId` propiedad. Esta propiedad se agrega automáticamente a cualquier usuario o grupo sincronizado por el controlador de sincronización y contiene información sobre el proveedor de identidad de origen.

Para obtener más información, consulte Documentación de Apache Oak sobre [Sincronización de usuarios y grupos](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## Problemas conocidos {#known-issues}

Si planea utilizar LDAP sobre SSL, asegúrese de que los certificados que está utilizando se crean sin la opción de comentario Netscape. Si esta opción está habilitada, la autenticación fallará con un error de protocolo de enlace SSL.
