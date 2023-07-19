---
title: Sincronización de usuarios de Communities
seo-title: Communities User Synchronization
description: Funcionamiento de la sincronización de usuarios
seo-description: How user synchronization works
uuid: 772b82bd-a66c-4c1d-b80b-dcff77c873a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 97286c2c-f6e3-43ec-b1a9-2abb58616778
docset: aem65
role: Admin
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '2482'
ht-degree: 2%

---

# Sincronización de usuarios de Communities {#communities-user-synchronization}

## Introducción {#introduction}

En AEM Communities, desde el entorno de publicación (según los permisos configurados), *visitantes del sitio* puede convertirse en *miembros*, crear *grupos de usuarios* y editar su *perfil del miembro* .

*Datos de usuario* es un término utilizado para referirse a *usuarios*, *perfiles de usuario* y *grupos de usuarios*.

*Miembros* es un término utilizado para referirse a *usuarios* se ha registrado en el entorno de publicación, a diferencia de los usuarios registrados en el entorno de creación.

Para obtener más información sobre los datos de usuario, visite [Administración de usuarios y grupos de usuarios](/help/communities/users.md).

## Sincronizar usuarios en una granja de servidores de publicación {#synchronizing-users-across-a-publish-farm}

Por diseño, los datos de usuario creados en el entorno de publicación no aparecen en el entorno de creación.

La mayoría de los datos de usuario creados en el entorno de creación están pensados para permanecer en el entorno de creación y no se sincronizan ni replican en las instancias de publicación.

Si la variable [topología](/help/communities/topologies.md) es un [publicar conjunto de servidores](/help/sites-deploying/recommended-deploys.md#tarmk-farm), el registro y las modificaciones realizadas en una instancia de publicación deben sincronizarse con otras instancias de publicación. Los miembros deben poder iniciar sesión y ver sus datos en cualquier nodo de publicación.

Cuando la sincronización de usuarios está habilitada, los datos de usuario se sincronizan automáticamente en las instancias de publicación de la granja.

### Instrucciones de configuración de sincronización de usuarios {#user-sync-setup-instructions}

Para obtener instrucciones detalladas paso a paso sobre cómo habilitar la sincronización en un conjunto de servidores de publicación, consulte:

* [Sincronización de usuarios](/help/sites-administering/sync.md)

## Sincronización de usuarios en segundo plano  {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **paquete vlt**

  Es un archivo zip de todos los cambios realizados en un editor que deben distribuirse entre los editores. Los cambios en un editor generan eventos seleccionados por el oyente de eventos de cambio. Esto crea un paquete vlt que contiene todos los cambios.

* **paquete de distribución**

  Contiene información de distribución de Sling. Esta es información sobre dónde debe distribuirse el contenido y cuándo se distribuyó por última vez.

## ¿Qué sucede cuando...? {#what-happens-when}

### Publicar sitio desde la consola Sitios de Communities {#publish-site-from-communities-sites-console}

En autor, cuando se publica un sitio de la comunidad desde el [Consola Sitios de Communities](/help/communities/sites-console.md), el efecto es [replicar](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) las páginas asociadas y Sling distribuyen los grupos de usuarios de la comunidad creados dinámicamente, incluida su pertenencia.

### El usuario se ha creado o edita el perfil en la publicación {#user-is-created-or-edits-profile-on-publish}

Por diseño, los usuarios y perfiles creados en el entorno de publicación (como por ejemplo, por autorregistro, inicio de sesión en redes sociales o autenticación LDAP) no aparecen en el entorno de creación.

Cuando la topología es un [publicar conjunto de servidores](/help/communities/topologies.md) y la sincronización del usuario se ha configurado correctamente, el *usuario* y *perfil de usuario* se sincroniza en el conjunto de servidores de publicación mediante la distribución Sling.

### Se crea un nuevo grupo de comunidad en Publicar {#new-community-group-is-created-on-publish}

Aunque se inicia desde una instancia de publicación, la creación del grupo de comunidad, que genera nuevas páginas de sitio y un nuevo grupo de usuarios, en realidad se produce en la instancia de autor.

Como parte del proceso, las nuevas páginas del sitio se replican en todas las instancias de publicación. El grupo de usuarios de la comunidad creado dinámicamente y sus miembros son Sling distribuido a todas las instancias de publicación.

### Los usuarios o grupos de usuarios se crean mediante la consola de seguridad {#users-or-user-groups-are-created-using-security-console}

Por diseño, los datos de usuario creados en el entorno de publicación no aparecen en el entorno de creación y a la inversa.

Si la variable [Administración de usuarios y seguridad](/help/sites-administering/security.md) La consola de se utiliza para agregar nuevos usuarios en el entorno de publicación, la sincronización de usuarios sincronizará a los nuevos usuarios y su pertenencia a grupos con otras instancias de publicación, si es necesario. La sincronización de usuarios también sincronizará los grupos de usuarios creados mediante la consola de seguridad.

### El usuario publica contenido en Publish {#user-posts-content-on-publish}

Para el contenido generado por el usuario (UGC), se accede a los datos introducidos en una instancia de publicación a través de [SRP configurado](/help/communities/srp-config.md).

## Prácticas recomendadas {#bestpractices}

De forma predeterminada, la sincronización de usuarios es **inhabilitado**. Habilitar la sincronización de usuarios implica modificar *existente* Configuraciones de OSGi. No se deben agregar nuevas configuraciones como resultado de habilitar la sincronización del usuario.

La sincronización de usuarios se basa en el entorno de creación para administrar las distribuciones de datos de usuario, aunque los datos de usuario no se creen en el autor

**Requisitos previos**

1. Si ya se han creado usuarios y grupos de usuarios en un editor, se recomienda [sincronización manual](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) los datos de usuario a todos los editores antes de configurar y habilitar la sincronización de usuarios.

   Una vez habilitada la sincronización de usuarios, solo se sincronizan los usuarios y grupos recién creados

1. Asegúrese de que se ha instalado el código más reciente:

   * [AEM Actualizaciones de plataforma de](https://helpx.adobe.com/es/experience-manager/kb/aem62-available-hotfixes.html)
   * [Actualizaciones de AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

Las siguientes configuraciones son necesarias para habilitar la sincronización de usuarios en AEM Communities. Asegúrese de que estas configuraciones sean correctas para evitar que la distribución de contenido de Sling falle.

### Agente de distribución de Apache Sling: fábrica de agentes de sincronización {#apache-sling-distribution-agent-sync-agents-factory}

Esta configuración recupera el contenido que se va a sincronizar entre los editores. La configuración se establece en una instancia de autor. El autor debe realizar un seguimiento de todos los editores que están allí y dónde sincronizar toda la información.

Los valores predeterminados de la configuración son para una sola instancia de publicación. Como la sincronización de usuarios es útil para sincronizar varias instancias de publicación, por ejemplo, para un conjunto de servidores de publicación, es necesario agregar instancias de publicación adicionales a la configuración.

**¿Cómo se sincroniza el contenido?**

La instancia de autor envía un ping al extremo de exportador de los editores. Cada vez que se crea o actualiza un usuario en editores específicos (n), el autor obtiene el contenido de sus extremos de exportador y [inserta el contenido](/help/communities/sync.md#main-pars-image-1413756164) a otros editores (n-1, que es aparte de los editores de los que se recupera el contenido).

Para configurar los agentes de sincronización de Apache Sling:

1. AEM Inicie sesión con privilegios de administrador en la instancia de autor de la.
1. Acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md). Por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Localizar **Agente de distribución de Apache Sling: fábrica de agentes de sincronización**.

   * Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

     Comprobar nombre: **socialpubsync.**

   * Seleccione el **Habilitado** casilla de verificación
   * Seleccionar **Utilice Varias colas.**
   * Especificar **Extremos del exportador** y **Extremos del importador** (puede agregar más extremos de exportador e importador).

     Estos extremos definen desde dónde desea obtener el contenido y dónde desea insertarlo. El autor recupera el contenido del extremo del exportador especificado y lo envía a los editores (que no sean el editor desde el que obtuvo el contenido).

   ![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe Granite Distribution - Proveedor secreto de transporte con contraseña cifrada {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

Permite al autor identificar al usuario autorizado, como si tuviera permiso para sincronizar datos de usuario del autor a la publicación.

El [usuario autorizado creado](/help/sites-administering/sync.md#createauthuser) en todas las instancias de publicación ayuda a los editores a conectarse con el autor y a configurar la distribución de Sling en el autor. Este usuario autorizado tiene todos los requisitos [ACL](/help/sites-administering/sync.md#howtoaddacl).

Siempre que se van a instalar datos en los editores o recuperarlos de ellos, el autor se conecta con los editores mediante las credenciales (nombre de usuario y contraseña) establecidas en esta configuración.

Para conectar el autor con los editores mediante un usuario autorizado:

1. AEM Inicie sesión con privilegios de administrador en la instancia de autor de la.
1. Acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md).

   Por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Localizar **Adobe Granite Distribution - Proveedor secreto de transporte con contraseña cifrada.**
1. Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

   Verificar propiedad **socialpubsync** - **publishUser.**

1. Establezca el nombre de usuario y la contraseña en [usuario autorizado](/help/sites-administering/sync.md#createauthorizeduser).

   Por ejemplo, **usersync - admin**

![granite-password-trans](assets/granite-paswrd-trans.png)

### Agente de distribución de Apache Sling: fábrica de agentes de cola {#apache-sling-distribution-agent-queue-agents-factory}

Esta configuración se utiliza para configurar los datos que desea sincronizar entre editores. Cuando los datos se crean o actualizan en las rutas especificadas en **Raíces permitidas**, &quot;var/community/distribution/diff&quot; se activa y el replicador creado recupera los datos de un editor y los instala en otros editores.

Para configurar los datos (rutas de nodos) para sincronizar:

1. Inicie sesión con privilegios de administrador en la instancia de publicación.
1. Acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md).

   Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Localizar **Agente de distribución de Apache Sling: fábrica de agentes de cola**.
1. Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

   Comprobar nombre: **socialpubsync -reverse**

1. Seleccione el **Habilitado** marque la casilla y guarde.
1. Especifique las rutas de nodos que se van a replicar en **Raíces permitidas**.
1. Repetir para cada **publicar** ejemplo.

   ![queue-agents-fact](assets/queue-agents-fact.png)

### Adobe Granite Distribution - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

Esta configuración sincroniza la pertenencia a grupos entre editores.
Si al cambiar la pertenencia de un grupo a un editor no se actualiza la pertenencia a otros editores, asegúrese de que **ref :members** se añade a **nombres de propiedades buscados**.

Para garantizar la sincronización de miembros:

1. Inicie sesión con privilegios de administrador en la instancia de publicación.
1. Acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md).

   Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Localizar **Adobe Granite Distribution - Diff Observer Factory**.
1. Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

   Verificar **nombre del agente: socialpubsync -reverse**.

1. Seleccione el **Habilitado** casilla de verificación
1. Especificar **rep:miembros** como descripción para propertyName en **nombres de propiedades buscados** y Guardar.

   ![diff-obs](assets/diff-obs.png)

### Déclencheur de distribución de Apache Sling: fábrica de Déclencheur programados {#apache-sling-distribution-trigger-scheduled-triggers-factory}

Esta configuración le permite configurar el intervalo de sondeo (después del cual el autor realiza un ping a los editores y extrae los cambios) para sincronizar los cambios entre los editores.

El autor sondea a los editores cada 30 segundos (valor predeterminado). Si hay algún paquete en la carpeta `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`, entonces recuperará esos paquetes e los instalará en otros editores.

Para modificar el intervalo de sondeo:

1. AEM Inicie sesión con privilegios de administrador en la instancia de autor de la.
1. Acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md), por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Localizar **Déclencheur de distribución de Apache Sling: fábrica de Déclencheur programados**

   * Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

     Verificar **socialpubsync -scheduled-déclencheur**

   * Establezca el intervalo en segundos con el intervalo deseado y guarde los cambios.

   ![déclencheur programado](assets/scheduled-trigger.png)

### Receptor de sincronización de usuarios de AEM Communities {#aem-communities-user-sync-listener}

Para los problemas de distribución de Sling en los que hay una discrepancia en las suscripciones y lo siguiente, compruebe si las siguientes propiedades en **Receptor de sincronización de usuarios de AEM Communities** se establecen las siguientes configuraciones:

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* DistributedFolders

Para sincronizar suscripciones, seguimientos y notificaciones

AEM En cada instancia de publicación de la:

1. Iniciar sesión con privilegios de administrador.
1. Acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md). Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Localizar **Receptor de sincronización de usuarios de AEM Communities**.
1. Seleccione la configuración existente para abrirla y editarla (icono de lápiz)

   Comprobar nombre: **socialpubsync -scheduled-déclencheur**

1. Configure lo siguiente **NodeTypes**:

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   Los tipos de nodo especificados en esta propiedad se sincronizarán y la información de notificaciones (blogs y configuraciones seguidos) se sincronizará entre diferentes editores.

1. Agregar todas las carpetas para sincronizar en **DistributedFolders**. Por ejemplo,

   `segments/scoring`

   `social/relationships`

   `activities`

1. Configure las variables **ignorablenodes** hasta:

   `.tokens`

   `system`

   `rep:cache` (dado que utilizamos sesiones fijas, no es necesario sincronizar este nodo con diferentes editores).

   ![user-sync-listner](assets/user-sync-listner.png)

### ID único de Sling {#unique-sling-id}

AEM La instancia de autor de utiliza el ID de Sling para identificar de dónde provienen los datos y a qué editores debe (o no debe) enviar el paquete de vuelta.

Asegúrese de que todos los editores de un conjunto de servidores de publicación tengan un ID de Sling único. Si el ID de Sling es el mismo para varias instancias de publicación en un conjunto de servidores de publicación, la sincronización de usuarios fallará. Como el autor no sabrá de dónde obtener el paquete ni dónde instalarlo.

Para garantizar un ID de Sling único de los editores del conjunto de servidores de publicación, en cada instancia de publicación:

1. Navegar a [https://_host:puerto_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. Compruebe el valor de **ID de Sling**.

   ![slíngido](assets/slingid.png)

   Si el ID de Sling de una instancia de publicación coincide con el ID de Sling de cualquier otra instancia de publicación, haga lo siguiente:

1. Detenga una de las instancias de publicación que tenga un ID de Sling coincidente.
1. En el `crx-quickstart/launchpad/felix` , busque y elimine el archivo llamado *sling.id.file.*

   Por ejemplo, en un sistema Linux:

   `rm -i $(find . -type f -name sling.id.file)`

   Por ejemplo, en un sistema Windows:

   Utilizar el Explorador de Windows y buscar `sling.id.file`

1. Inicie la instancia de publicación. Al inicio se le asignará un nuevo ID de Sling.
1. Validar que la variable **ID de Sling** es ahora único.

Repita estos pasos hasta que todas las instancias de publicación tengan un ID de Sling único.

### Generador de paquetes Vault Factory {#vault-package-builder-factory}

Para que las actualizaciones se sincronicen correctamente, es necesario modificar el generador de paquetes Vault para la sincronización de usuarios.
Entrada `/home/users`, a `*/rep:cache` se ha creado el nodo. Es una caché que se utiliza para encontrar que si consultamos el nombre principal de un nodo, entonces esta caché se puede utilizar directamente.

La sincronización de usuarios se puede detener si `rep :cache` Los nodos de se sincronizan entre editores.

AEM Para asegurarse de que las actualizaciones se sincronizan correctamente entre los editores, en cada instancia de publicación de la:

1. Acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md)

   Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Busque el **Empaquetado de distribución de Apache Sling: generador de paquetes Vault de fábrica**

   Nombre del generador: socialpubsync-vlt.

1. Seleccione el icono de edición.
1. Añada dos filtros de nodo de paquete:
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. Gestión de políticas
   * Para sobrescribir los nodos de rep :policy existentes por otros nuevos, añada un tercer filtro de paquetes: `/home/users|+.*/rep:policy`
   * Para evitar que se distribuyan directivas, establezca: `Acl Handling: IGNORE`

   ![Fábrica del generador de paquetes Vault](assets/vault-package-builder-factory.png)

## Solución de problemas de distribución de Sling en AEM Communities {#troubleshoot-sling-distribution-in-aem-communities}

Si la distribución de Sling falla, intente los siguientes pasos de depuración:

1. **Marcar para [configuraciones añadidas incorrectamente](/help/sites-administering/sync.md#improperconfig)**

   Asegúrese de que no se agregan ni editan varias configuraciones y, en su lugar, se deben editar las configuraciones predeterminadas existentes.
1. **Comprobar configuraciones**

   Asegúrese de que todas las [configuraciones](/help/communities/sync.md#bestpractices) están correctamente configuradas en la instancia de autor de AEM, como se menciona en la [Prácticas recomendadas](/help/communities/sync.md#main-pars-header-863110628).

1. **Comprobar permisos de usuario autorizados**

   Si los paquetes no están instalados correctamente, compruebe que la [usuario autorizado](/help/sites-administering/sync.md#createauthuser) creado en la primera instancia de Publish tiene las ACL correctas.

   Para validar esto, en lugar de [creó usuario autorizado](/help/sites-administering/sync.md#createauthuser) cambie la [Adobe Granite Distribution - Proveedor secreto de transporte con contraseña cifrada](/help/sites-administering/sync.md#adobegraniteencpasswrd) Configuración de en la instancia de autor para utilizar las credenciales de usuario de administrador. Ahora intente instalar los paquetes de nuevo. Si la sincronización de usuarios funciona correctamente con las credenciales del administrador, significa que el usuario de publicación creado no tenía las ACL adecuadas.

1. **Compruebe la configuración de fábrica de Diff Observer**

   Si solo no se sincronizan nodos específicos en el conjunto de servidores de publicación (por ejemplo, los miembros del grupo no están sincronizados), asegúrese de que la variable [Adobe Granite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver) La configuración de está activada y **rep: members** se establecen en **nombres de propiedades buscados**.

1. **Compruebe la configuración del Receptor de sincronización de usuarios de AEM Communities.** Si los usuarios creados están sincronizados, pero las suscripciones y las siguientes no funcionan, asegúrese de que la configuración del Receptor de sincronización de usuarios de AEM Communities tenga:

   * Tipos de nodo: establecer en **rep:User, nt :unstructured**, **nt :resource**, **rep:ACL**, **sling:Carpeta**, y **sling:CarpetaOrdenada**.
   * Nodos ignorables: se establece en **.tokens**, **sistema**, y **rep :cache**.
   * Carpetas distribuidas: establezca las carpetas que desea distribuir.

1. **Comprobar los registros generados al crear el usuario en la instancia de publicación**

   Si las configuraciones anteriores están correctamente configuradas pero la sincronización de usuarios no funciona, compruebe los registros generados al crear el usuario.

   Compruebe si el orden de los registros es el mismo, como se indica a continuación:

   ```shell
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ2: ADD paths=[/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK], user=communities-user-admin
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ3: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy], user=communities-user-admin
   15.05.2016 18:33:01.757 *INFO* [sling-oak-observation-7431] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_ebb27ad9-a861-4405-9342-d64c916654e2:0.0.1
   15.05.2016 18:33:01.820 *INFO* [sling-oak-observation-7422] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_58811273-5861-48fe-95d2-4aff367b99c3:0.0.1
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK/profile]
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ4: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK/profile], user=communities-user-admin
   15.05.2016 18:33:02.273 *INFO* [sling-oak-observation-7430] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337182039_f34f4fa6-10b9-42eb-8740-4da9d4d38f99:0.0.1
   ```

Para depurar:

1. Deshabilite la sincronización de usuarios:
1. AEM En la instancia de autor de, inicie sesión con privilegios de administrador.

   1. Acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md). Por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Busque la configuración **Agente de distribución de Apache Sling: fábrica de agentes de sincronización**.
   1. Anule la selección de **Habilitado** casilla de verificación.

      Al deshabilitar la sincronización de usuarios en la instancia de autor, los extremos (exportador e importador) se deshabilitan y la instancia de autor es estática. El **vlt** el autor no realiza un ping de los paquetes ni los recupera.

      Ahora, si se crea un usuario en la instancia de publicación, la variable **vlt** el paquete se crea en */var/sling/distribution/packages/ socialpubsync - vlt /data* nodo. Y si el autor inserta estos paquetes en otro servicio. Puede descargar y extraer estos datos para comprobar qué propiedades se insertan en otros servicios.

1. Vaya a un editor y cree un usuario en él. Como resultado, se crean eventos.
1. Compruebe la [orden de los registros](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities), creado al crear el usuario.
1. Compruebe si una **vlt** el paquete se ha creado el **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. AEM Ahora, habilite la sincronización de usuarios en la instancia de autor de la.
1. En el publicador, cambie los extremos del exportador o importador en **Agente de distribución de Apache Sling: fábrica de agentes de sincronización**.
Podemos descargar y extraer datos de paquetes para comprobar qué propiedades se insertan en otros editores y qué datos se pierden.
