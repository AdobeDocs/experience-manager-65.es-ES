---
title: Configuración de LDAP con AEM 6
seo-title: Configuring LDAP with AEM 6
description: Obtenga información sobre cómo configurar LDAP con AEM.
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

# Configuración de LDAP con AEM 6 {#configuring-ldap-with-aem}

LDAP (el **L** ponderación **D** directorio **A** acceso **P** protocolo) se utiliza para acceder a servicios de directorio centralizados. Esto ayuda a reducir el esfuerzo necesario para administrar las cuentas de usuario, ya que se puede acceder a ellas desde varias aplicaciones. Uno de estos servidores LDAP es Active Directory. LDAP se utiliza a menudo para lograr el inicio de sesión único, que permite al usuario acceder a varias aplicaciones después de iniciar sesión una vez.

Las cuentas de usuario se pueden sincronizar entre el servidor LDAP y el repositorio, y los detalles de las cuentas LDAP se guardan en el repositorio. Esto permite que las cuentas se asignen a grupos de repositorios para asignar los permisos y privilegios necesarios.

El repositorio utiliza la autenticación LDAP para autenticar a esos usuarios, con credenciales pasadas al servidor LDAP para su validación, que es necesario antes de permitir el acceso al repositorio. Para mejorar el rendimiento, el repositorio puede almacenar en caché las credenciales validadas correctamente, con un tiempo de espera de caducidad para garantizar que la revalidación se produzca después de un periodo adecuado.

Cuando se elimina una cuenta del servidor LDAP, ya no se concede la validación y, por lo tanto, se deniega el acceso al repositorio. Los detalles de las cuentas LDAP que se guardan en el repositorio también se pueden depurar.

El uso de estas cuentas es transparente para los usuarios, no ven ninguna diferencia entre las cuentas de usuario y grupo creadas a partir de LDAP y las creadas únicamente en el repositorio.

En AEM 6, la compatibilidad con LDAP viene con una nueva implementación que requiere un tipo de configuración diferente al de las versiones anteriores.

Todas las configuraciones LDAP ahora están disponibles como configuraciones de OSGi. Se pueden configurar a través de la consola de administración web en:
`https://serveraddress:4502/system/console/configMgr`

Para que LDAP funcione con AEM, debe crear tres configuraciones OSGi:

1. Un proveedor de identidad LDAP (IDP).
1. Controlador de sincronización.
1. Un módulo de inicio de sesión externo.

>[!NOTE]
>
>Watch [Módulo de inicio de sesión externo de Oak: autenticación con LDAP y más allá](https://docs.adobe.com/content/ddc/en/gems/oak-s-external-login-module---authenticating-with-ldap-and-beyon.html#) para profundizar en los módulos de inicio de sesión externos.
>
>Para leer un ejemplo de configuración de Experience Manager con Apache DS, consulte [Configuración de Adobe Experience Manager 6.5 para utilizar el servicio de directorio Apache.](https://helpx.adobe.com/experience-manager/using/configuring-aem64-apache-directory-service.html)

## Configuración Del Proveedor De Identidad LDAP {#configuring-the-ldap-identity-provider}

El proveedor de identidad LDAP se utiliza para definir cómo se recuperan los usuarios del servidor LDAP.

Se encuentra en la consola de administración, en la sección **Proveedor de identidad de Apache Jackrabbit Oak LDAP** nombre.

Las siguientes opciones de configuración están disponibles para el proveedor de identidad LDAP:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre del proveedor LDAP</strong></td>
   <td>Nombre de esta configuración del proveedor LDAP.</td>
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
   <td>Indica si TLS debe iniciarse en conexiones.</td>
  </tr>
  <tr>
   <td><strong>Deshabilitar la comprobación de certificados</strong></td>
   <td>Indica si se debe deshabilitar la validación de certificados de servidor.</td>
  </tr>
  <tr>
   <td><strong>Enlace DN</strong></td>
   <td>DN del usuario para la autenticación. Si se deja vacío, se realiza un enlace anónimo.</td>
  </tr>
  <tr>
   <td><strong>Vincular contraseña</strong></td>
   <td>Contraseña del usuario para la autenticación</td>
  </tr>
  <tr>
   <td><strong>Tiempo de espera de la búsqueda</strong></td>
   <td>Tiempo hasta que se agota el tiempo de espera de una búsqueda</td>
  </tr>
  <tr>
   <td><strong>Máximo del grupo de administración activo</strong></td>
   <td>El tamaño máximo activo del grupo de conexiones de administración.</td>
  </tr>
  <tr>
   <td><strong>Acumulación máxima de usuarios activa</strong></td>
   <td>Tamaño máximo activo del grupo de conexiones de usuario.</td>
  </tr>
  <tr>
   <td><strong>DN de base de usuario</strong></td>
   <td>DN para búsquedas de usuarios</td>
  </tr>
  <tr>
   <td><strong>Clases de objetos de usuario</strong></td>
   <td>La lista de clases de objeto que debe contener una entrada de usuario.</td>
  </tr>
  <tr>
   <td><strong>Atributo de ID de usuario</strong></td>
   <td>Nombre del atributo que contiene el identificador de usuario.</td>
  </tr>
  <tr>
   <td><strong>Filtro extra del usuario</strong></td>
   <td>Filtro LDAP adicional que se utilizará al buscar usuarios. El filtro final tiene el siguiente formato: '(&amp;(&lt;idattr&gt;=&lt;userid&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>Rutas de DN de usuario</strong></td>
   <td>Controla si el DN debe utilizarse para calcular una parte de la ruta intermedia.</td>
  </tr>
  <tr>
   <td><strong>DN de base de grupo</strong></td>
   <td>DN base para búsquedas de grupo.</td>
  </tr>
  <tr>
   <td><strong>Agrupar clases de objetos</strong></td>
   <td>La lista de clases de objetos que debe contener una entrada de grupo.</td>
  </tr>
  <tr>
   <td><strong>Atributo de nombre de grupo</strong></td>
   <td>Nombre del atributo que contiene el nombre del grupo.</td>
  </tr>
  <tr>
   <td><strong>Filtro extra de grupo</strong></td>
   <td>Filtro LDAP adicional que se utilizará al buscar grupos. El filtro final tiene el siguiente formato: '(&amp;(&lt;nameattr&gt;=&lt;groupname&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Rutas de DN de grupo</strong></td>
   <td>Controla si el DN debe utilizarse para calcular una parte de la ruta intermedia.</td>
  </tr>
  <tr>
   <td><strong>Atributo de miembro del grupo</strong></td>
   <td>Atributo de grupo que contiene los miembros de un grupo.</td>
  </tr>
 </tbody>
</table>

## Configuración Del Controlador De Sincronización {#configuring-the-synchronization-handler}

El controlador de sincronización definirá cómo se sincronizarán los usuarios y grupos del proveedor de identidad con el repositorio.

Se encuentra debajo de la **Controlador de sincronización predeterminado Apache Jackrabbit Oak** nombre en la consola de administración.

Las siguientes opciones de configuración están disponibles para el controlador de sincronización:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre del controlador de sincronización</strong></td>
   <td>Nombre de la configuración de sincronización.</td>
  </tr>
  <tr>
   <td><strong>Hora de caducidad del usuario</strong></td>
   <td>Duración hasta que un usuario sincronizado caduque.</td>
  </tr>
  <tr>
   <td><strong>Pertenencia automática del usuario</strong></td>
   <td>Lista de grupos a los que se agrega automáticamente un usuario sincronizado.</td>
  </tr>
  <tr>
   <td><strong>Asignación de propiedades de usuario</strong></td>
   <td>Enumerar la definición de asignación de propiedades locales de las externas.</td>
  </tr>
  <tr>
   <td><strong>Prefijo de ruta de usuario</strong></td>
   <td>El prefijo de ruta que se utiliza al crear nuevos usuarios.</td>
  </tr>
  <tr>
   <td><strong>Caducidad de pertenencia del usuario</strong></td>
   <td>Tiempo después del cual caduca la pertenencia.<br /> </td>
  </tr>
  <tr>
   <td><strong>Profundidad de anidación de la pertenencia del usuario</strong></td>
   <td>Devuelve la profundidad máxima del anidado de grupos cuando se sincronizan las relaciones de pertenencia. Un valor de 0 deshabilita de forma efectiva la búsqueda de miembros del grupo. Un valor de 1 solo agrega los grupos directos de un usuario. Este valor no tiene ningún efecto cuando se sincronizan grupos individuales solo al sincronizar un antecedente de pertenencia de usuarios.</td>
  </tr>
  <tr>
   <td><strong>Hora de caducidad del grupo</strong></td>
   <td>Duración hasta que caduque un grupo sincronizado.</td>
  </tr>
  <tr>
   <td><strong>Pertenencia automática de grupo</strong></td>
   <td>Lista de grupos a los que se agrega automáticamente un grupo sincronizado.</td>
  </tr>
  <tr>
   <td><strong>Asignación de propiedades de grupo</strong></td>
   <td>Enumerar la definición de asignación de propiedades locales de las externas.</td>
  </tr>
  <tr>
   <td><strong>Prefijo de ruta de grupo</strong></td>
   <td>Prefijo de ruta que se utiliza al crear nuevos grupos.</td>
  </tr>
 </tbody>
</table>

## El módulo de inicio de sesión externo {#the-external-login-module}

El módulo de inicio de sesión externo se encuentra en la sección **Módulo de inicio de sesión externo Apache Jackrabbit Oak** en la consola de administración.

>[!NOTE]
>
>El Módulo de inicio de sesión externo Apache Jackrabbit Oak implementa las especificaciones de JAAS (Autenticación y autorización de Java). Consulte la [guía de referencia de seguridad de Oracle oficial de Java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) para obtener más información.

Su trabajo es definir qué proveedor de identidad y controlador de sincronización utilizar, enlazando efectivamente los dos módulos.

Estas son las opciones de configuración disponibles:

| **Clasificación de JAAS** | Especificar la clasificación (es decir, el orden de clasificación) de esta entrada del módulo de inicio de sesión. Las entradas se ordenan en orden descendente (es decir, las configuraciones de clasificación de valores más altos son las primeras). |
|---|---|
| **Indicador de control JAAS** | Propiedad que especifica si se REQUIERE o no un LoginModule, REQUISITO, SUFICIENTE u OPCIONAL. Consulte la documentación de configuración de JAAS para obtener más información sobre el significado de estos indicadores. |
| **Dominio de JAAS** | Nombre de territorio (o nombre de aplicación) con el que se registra LoginModule. Si no se proporciona ningún nombre de dominio, LoginModule se registra con un dominio predeterminado tal como se configura en la configuración Felix JAAS. |
| **Nombre del proveedor de identidad** | Nombre del proveedor de identidad. |
| **Nombre del controlador de sincronización** | Nombre del controlador de sincronización. |

>[!NOTE]
>
>Si planea tener más de una configuración LDAP con su instancia de AEM, es necesario crear proveedores de identidad y controladores de sincronización independientes para cada configuración.

## Configuración de LDAP sobre SSL {#configure-ldap-over-ssl}

AEM 6 se puede configurar para autenticarse con LDAP sobre SSL siguiendo el siguiente procedimiento:

1. Marque la **Usar SSL** o **Usar TLS** casillas de verificación al configurar la variable [Proveedor de identidad LDAP](#configuring-the-ldap-identity-provider).
1. Configure el controlador de sincronización y el módulo de inicio de sesión externo según su configuración.
1. Instale los certificados SSL en la VM de Java si es necesario. Esto se puede hacer con keytool:

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Pruebe la conexión con el servidor LDAP.

### Creación de certificados SSL {#creating-ssl-certificates}

Los certificados con firma automática se pueden utilizar al configurar AEM para autenticarse con LDAP mediante SSL. A continuación se muestra un ejemplo de un procedimiento de trabajo para generar certificados para su uso con AEM.

1. Asegúrese de tener una biblioteca SSL instalada y funcionando. Este procedimiento utilizará OpenSSL como ejemplo.

1. Cree un archivo de configuración OpenSSL personalizado (cnf). Esto se puede hacer copiando el archivo de configuración predeterminado **openssl.cnf **y personalizándolo. En sistemas UNIX, normalmente se ubica en `/usr/lib/ssl/openssl.cnf`

1. Continúe creando la clave raíz de CA ejecutando el siguiente comando en un terminal:

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. A continuación, cree un nuevo certificado autofirmado:

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Inspect el certificado recién generado para asegurarse de que todo está en orden:

   `openssl x509 -noout -text -in root-ca.crt`

1. Asegúrese de que todas las carpetas especificadas en el archivo de configuración de certificado (.cnf) existan. Si no es así, créelos.
1. Cree una semilla aleatoria, ejecutando, por ejemplo:

   `openssl rand -out private/.rand 8192`

1. Mueva los archivos .pem creados a las ubicaciones configuradas en el archivo .cnf.

1. Finalmente, agregue el certificado al almacén de claves de Java.

## Habilitación del registro de depuración {#enabling-debug-logging}

El registro de depuración se puede habilitar tanto para el proveedor de identidad LDAP como para el módulo de inicio de sesión externo para solucionar problemas de conexión.

Para habilitar el registro de depuración, debe:

1. Vaya a la Consola de administración web.
1. Busque &quot;Configuración del registrador de Sling de Apache&quot; y cree dos registradores con las siguientes opciones:

* Nivel de registro: Depuración
* Archivo de registro logs/ldap.log
* Patrón de mensaje: {0,date,dd.MM.yyyy HH:mm:s.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Registrador: org.apache.jackrabbit.oak.security.authentication.ldap

* Nivel de registro: Depuración
* Archivo de registro: logs/external.log
* Patrón de mensaje: {0,date,dd.MM.yyyy HH:mm:s.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Registrador: org.apache.jackrabbit.oak.spi.security.authentication.external

## Una palabra sobre afiliación de grupo {#a-word-on-group-affiliation}

Los usuarios sincronizados a través de LDAP pueden formar parte de diferentes grupos en AEM. Estos grupos pueden ser grupos LDAP externos que se agregarán a AEM como parte del proceso de sincronización, pero también pueden ser grupos que se agregan por separado y que no forman parte del esquema de afiliación del grupo LDAP original.

En la mayoría de los casos, pueden ser grupos agregados por un administrador de AEM local o por cualquier otro proveedor de identidad.

Si se elimina a un usuario de un grupo en el servidor LDAP, el cambio también se reflejará en el lado AEM tras la sincronización. Sin embargo, todas las demás afiliaciones de grupo del usuario que no fueron agregadas por LDAP permanecerán en su lugar.

AEM detecta y gestiona la depuración de usuarios de grupos externos mediante el uso de la variable `rep:externalId` propiedad. Esta propiedad se agrega automáticamente a cualquier usuario o grupo que sincronice el controlador de sincronización y contiene información sobre el proveedor de identidad de origen.

Para obtener más información, consulte la documentación de Apache Oak en [Sincronización de usuarios y grupos](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## Problemas conocidos {#known-issues}

Si planea utilizar LDAP sobre SSL, asegúrese de que los certificados que está utilizando se crean sin la opción de comentario de Netscape. Si esta opción está habilitada, la autenticación fallará con un error de protocolo de enlace SSL.
