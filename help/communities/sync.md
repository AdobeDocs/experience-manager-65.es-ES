---
title: Sincronización de usuarios de Communities
description: Descubra cómo funciona la sincronización de usuarios en Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2403'
ht-degree: 0%

---

# Sincronización de usuarios de Communities {#communities-user-synchronization}

## Introducción {#introduction}

En las comunidades de Adobe Experience Manager AEM (), desde el entorno de Publish (según los permisos que estén configurados), *los visitantes del sitio* pueden convertirse en *miembros*, crear *grupos de usuarios* y editar su *perfil de miembro*

*Los datos de usuario* hacen referencia a *usuarios*, *perfiles de usuario* y *grupos de usuarios*.

*Los miembros* se refieren a *usuarios* registrados en el entorno de Publish, a diferencia de los usuarios registrados en el entorno de autor.

Para obtener más información acerca de los datos de usuario, visite [Administrar usuarios y grupos de usuarios](/help/communities/users.md).

## Sincronizar usuarios en una granja de Publish {#synchronizing-users-across-a-publish-farm}

Por diseño, los datos de usuario creados en el entorno de Publish no aparecen en el entorno de creación.

La mayoría de los datos de usuario creados en el entorno de creación están pensados para permanecer en el entorno de creación y no se sincronizan ni replican en las instancias de Publish.

Si [topology](/help/communities/topologies.md) es una [granja de servidores de publicación](/help/sites-deploying/recommended-deploys.md#tarmk-farm), el registro y las modificaciones realizadas en una instancia de Publish deben sincronizarse con otras instancias de Publish. Los miembros deben poder iniciar sesión y ver sus datos en cualquier nodo de Publish.

Cuando la sincronización de usuarios está habilitada, los datos de usuario se sincronizan automáticamente en las instancias de Publish de la granja.

### Instrucciones de configuración de sincronización de usuarios {#user-sync-setup-instructions}

Para obtener instrucciones detalladas paso a paso sobre cómo habilitar la sincronización en un conjunto de servidores de publicación, consulte [Sincronización de usuarios](/help/sites-administering/sync.md).

## Sincronización de usuarios en segundo plano {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **paquete vlt**

  Es un archivo zip de todos los cambios realizados en un publicador, que deben distribuirse entre los publicadores. Los cambios en un editor generan eventos seleccionados por el oyente de eventos de cambio. Esto crea un paquete vlt que contiene todos los cambios.

* **paquete de distribución**

  Contiene información de distribución de Sling. Esta es información sobre dónde se debe distribuir el contenido y cuándo se distribuyó por última vez.

## ¿Qué sucede cuando...? {#what-happens-when}

### Sitio de Publish desde la consola Sitios de Communities {#publish-site-from-communities-sites-console}

En Autor, cuando se publica un sitio de la comunidad desde la consola [Sitios de comunidades](/help/communities/sites-console.md), el efecto es [replicar](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) las páginas asociadas y Sling distribuye los grupos de usuarios de la comunidad creados dinámicamente, incluida su pertenencia.

### Se crea el usuario o se edita el perfil en Publish {#user-is-created-or-edits-profile-on-publish}

Por diseño, los usuarios y perfiles creados en el entorno de Publish (como por ejemplo, por autorregistro, inicio de sesión social o autenticación LDAP) no aparecen en el entorno de creación.

Si la topología es una [granja de servidores de publicación](/help/communities/topologies.md) y la sincronización de usuarios se ha configurado correctamente, el *usuario* y el *perfil de usuario* se sincronizan en toda la granja de servidores de publicación mediante la distribución Sling.

### Se crea un nuevo grupo de comunidad en Publish {#new-community-group-is-created-on-publish}

Aunque se inicia desde una instancia de Publish, la creación de grupos de comunidad, que genera nuevas páginas de sitio y un nuevo grupo de usuarios, en realidad se produce en la instancia de autor.

Como parte del proceso, las nuevas páginas del sitio se replican en todas las instancias de Publish. El grupo de usuarios de la comunidad creado dinámicamente y sus miembros son Sling distribuido a todas las instancias de Publish.

### Los usuarios o grupos de usuarios se crean mediante la consola de seguridad {#users-or-user-groups-are-created-using-security-console}

Por diseño, los datos de usuario creados en el entorno de publicación no aparecen en el entorno de creación y a la inversa.

Cuando se usa la consola [Administración de usuarios y seguridad](/help/sites-administering/security.md) para agregar nuevos usuarios en el entorno de publicación, la sincronización de usuarios sincroniza los nuevos usuarios y su pertenencia a grupos con otras instancias de publicación, si es necesario. La sincronización de usuarios también sincroniza los grupos de usuarios creados mediante la consola de seguridad.

### El usuario publica contenido en Publish {#user-posts-content-on-publish}

Para el contenido generado por el usuario (UGC), se accede a los datos introducidos en una instancia de publicación a través del [SRP configurado](/help/communities/srp-config.md).

## Prácticas recomendadas {#bestpractices}

De manera predeterminada, la sincronización de usuarios está **deshabilitada**. Habilitar la sincronización de usuarios implica modificar *las configuraciones de OSGi existentes*. No se deben agregar nuevas configuraciones como resultado de habilitar la sincronización del usuario.

La sincronización de usuarios se basa en el entorno de creación para administrar las distribuciones de datos de usuario, aunque los datos de usuario no se creen en el autor.

**Requisitos previos**

1. Si ya se han creado usuarios y grupos de usuarios en un editor, se recomienda [sincronizar manualmente](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) los datos de usuarios con todos los editores antes de configurar y habilitar la sincronización de usuarios.

   Una vez habilitada la sincronización de usuarios, solo se sincronizan los usuarios y grupos recién creados

1. Asegúrese de que se ha instalado el código más reciente:

   * AEM [Actualizaciones de la plataforma de](https://helpx.adobe.com/es/experience-manager/kb/aem62-available-hotfixes.html)
   * [Actualizaciones de AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

Las siguientes configuraciones son necesarias para habilitar la sincronización de usuarios en AEM Communities. Asegúrese de que estas configuraciones sean correctas para evitar que la distribución de contenido de Sling falle.

### Agente de distribución de Apache Sling: fábrica de agentes de sincronización {#apache-sling-distribution-agent-sync-agents-factory}

Esta configuración recupera el contenido que se va a sincronizar entre los editores. La configuración se establece en una instancia de autor. El autor debe realizar un seguimiento de todos los editores que están allí y dónde sincronizar toda la información.

Los valores predeterminados de la configuración son para una sola instancia de publicación. Como la sincronización de usuarios es útil para sincronizar varias instancias de publicación, por ejemplo, para un conjunto de servidores de publicación, es necesario agregar instancias de publicación adicionales a la configuración.

**¿Cómo se sincroniza el contenido?**

La instancia de autor envía un ping al extremo de exportador de los editores. Cada vez que se crea o actualiza un usuario en editores específicos (n), el autor obtiene el contenido de sus extremos de exportador y [inserta el contenido](/help/communities/sync.md#main-pars-image-1413756164) en otros editores (n-1, que es aparte de los editores de los que se recupera el contenido).

Para configurar los agentes de sincronización de Apache Sling:

1. AEM Inicie sesión con privilegios de administrador en la instancia de autor de la.
1. Acceda a la [consola web](/help/sites-deploying/configuring-osgi.md). Por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Busque **Agente de distribución Apache Sling - Fábrica de agentes de sincronización**.

   * Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

     Comprobar nombre: **socialpubsync.**

   * Seleccione la casilla **Habilitado**.
   * Seleccionar **Usar varias colas.**
   * Especifique **extremos del exportador** y **extremos del importador** (puede agregar más extremos del exportador y del importador).

     Estos extremos definen desde dónde desea obtener el contenido y dónde desea insertarlo. El autor recupera el contenido del extremo del exportador especificado y lo envía a los editores (que no sean el editor desde el que obtuvo el contenido).

   ![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe Granite Distribution - Proveedor secreto de transporte con contraseña cifrada {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

Permite al autor identificar al usuario autorizado, como si tuviera permiso para sincronizar datos de usuario del autor a la publicación.

El [usuario autorizado creado](/help/sites-administering/sync.md#createauthuser) en todas las instancias de publicación ayuda a los editores a conectarse con el autor y a configurar la distribución de Sling en el autor. Este usuario autorizado tiene todas las [ACL](/help/sites-administering/sync.md#howtoaddacl) necesarias.

Siempre que se van a instalar datos en los editores o recuperarlos de ellos, el autor se conecta con los editores mediante las credenciales (nombre de usuario y contraseña) establecidas en esta configuración.

Para conectar el autor con los editores mediante un usuario autorizado:

1. AEM Inicie sesión con privilegios de administrador en la instancia de autor de la.
1. Acceda a la [consola web](/help/sites-deploying/configuring-osgi.md).

   Por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Localice **Adobe Granite Distribution - Proveedor de secreto de transporte con contraseña cifrada.**
1. Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

   Verificar propiedad **socialpubsync** - **publishUser.**

1. Establezca el nombre de usuario y la contraseña en [usuario autorizado](/help/sites-administering/sync.md#createauthorizeduser).

   Por ejemplo, **usersync - admin**

![granite-password-trans](assets/granite-paswrd-trans.png)

### Agente de distribución de Apache Sling: fábrica de agentes de cola {#apache-sling-distribution-agent-queue-agents-factory}

Esta configuración se utiliza para configurar los datos que desea sincronizar entre editores. Cuando los datos se crean o actualizan en las rutas especificadas en **Raíces permitidas**, &quot;var/community/distribution/diff&quot; se activa y el replicador creado recupera los datos de un publicador y los instala en otros publicadores.

Para configurar los datos (rutas de nodos) para sincronizar:

1. Inicie sesión con privilegios de administrador en la instancia de publicación.
1. Acceda a la [consola web](/help/sites-deploying/configuring-osgi.md).

   Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Busque **Agente de distribución Apache Sling - Fábrica de agentes de cola**.
1. Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

   Comprobar nombre: **socialpubsync -reverse**

1. Seleccione la casilla de verificación **Habilitado** y guarde los cambios.
1. Especifique las rutas de nodos que se replicarán en **Raíces permitidas**.
1. Repita el proceso para cada instancia de **publish**.

   ![queue-agents-fact](assets/queue-agents-fact.png)

### Adobe Granite Distribution - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

Esta configuración sincroniza la pertenencia a grupos entre editores.
Si al cambiar la pertenencia de un grupo en un editor no se actualiza la pertenencia a otros editores, asegúrese de que **ref :members** se agrega a **nombres de propiedades buscadas**.

Para garantizar la sincronización de miembros:

1. Inicie sesión con privilegios de administrador en la instancia de publicación.
1. Acceda a la [consola web](/help/sites-deploying/configuring-osgi.md).

   Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Localice **Adobe Granite Distribution - Diff Observer Factory**.
1. Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

   Comprobar **nombre de agente: socialpubsync -reverse**.

1. Seleccione la casilla **Habilitado**.
1. Especifique **rep:members** como descripción para propertyName en **nombres de propiedades buscadas** y haga clic en Guardar.

   ![diff-obs](assets/diff-obs.png)

### Déclencheur de distribución de Apache Sling: fábrica de Déclencheur programados {#apache-sling-distribution-trigger-scheduled-triggers-factory}

Esta configuración le permite configurar el intervalo de sondeo (después del cual el autor hace ping a los editores y extrae los cambios) para sincronizar los cambios entre los editores.

El autor sondea a los editores cada 30 segundos (valor predeterminado). Si hay algún paquete en la carpeta `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`, se recuperarán esos paquetes y se instalarán en otros editores.

Para modificar el intervalo de sondeo:

1. AEM Inicie sesión con privilegios de administrador en la instancia de autor de la.
1. Acceda a la [consola web](/help/sites-deploying/configuring-osgi.md), por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Busque el **Déclencheur de distribución de Apache Sling - Fábrica de Déclencheur programados**

   * Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

     Comprobar **socialpubsync -scheduled-déclencheur**

   * Establezca el intervalo en segundos con el intervalo deseado y guarde los cambios.

   ![déclencheur programado](assets/scheduled-trigger.png)

### Receptor de sincronización de usuarios de AEM Communities {#aem-communities-user-sync-listener}

Para los problemas de distribución de Sling en los que hay una discrepancia en las suscripciones y lo siguiente, compruebe si están establecidas las siguientes propiedades en **Receptor de sincronización de usuarios de AEM Communities** configuraciones:

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* DistributedFolders

Para sincronizar suscripciones, seguimientos y notificaciones

AEM En cada instancia de publicación de la:

1. Iniciar sesión con privilegios de administrador.
1. Acceda a la [consola web](/help/sites-deploying/configuring-osgi.md). Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Busque **Receptor de sincronización de usuarios de AEM Communities**.
1. Seleccione la configuración existente para abrirla y editarla (icono de lápiz)

   Comprobar nombre: **socialpubsync -scheduled-déclencheur**

1. Establezca los **tipos de nodo** siguientes:

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   Los tipos de nodo especificados en esta propiedad se sincronizan y la información de notificaciones (blogs y configuraciones seguidos) se sincroniza entre diferentes editores.

1. Agregue todas las carpetas para sincronizar en **DistributedFolders**. Por ejemplo,

   `segments/scoring`

   `social/relationships`

   `activities`

1. Establecer **ignorablenodes** en:

   `.tokens`

   `system`

   `rep:cache` (dado que se utilizan sesiones fijas, no es necesario sincronizar este nodo con distintos editores).

   ![user-sync-listner](assets/user-sync-listner.png)

### ID único de Sling {#unique-sling-id}

AEM La instancia de autor de utiliza el ID de Sling para identificar de dónde provienen los datos y a qué editores debe (o no debe) enviar el paquete de vuelta.

Asegúrese de que todos los editores de un conjunto de servidores de publicación tengan un ID de Sling único. Si el ID de Sling es el mismo para varias instancias de publicación en un conjunto de servidores de publicación, la sincronización de usuarios falla. Como el autor no sabe de dónde obtener el paquete ni dónde instalarlo.

Para garantizar un ID de Sling único de los editores del conjunto de servidores de publicación, en cada instancia de Publish:

1. Vaya a [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. Compruebe el valor de **Sling ID**.

   ![slingid](assets/slingid.png)

   Si el ID de Sling de una instancia de Publish coincide con el ID de Sling de cualquier otra instancia de Publish, haga lo siguiente:

1. Detenga una de las instancias de Publish que tenga un ID de Sling coincidente.
1. En el directorio `crx-quickstart/launchpad/felix`, busque y elimine el archivo de nombre *sling.id.file.*

   Por ejemplo, en un sistema Linux:

   `rm -i $(find . -type f -name sling.id.file)`

   Por ejemplo, en un sistema Windows:

   Usar el Explorador de Windows y buscar `sling.id.file`

1. Inicie la instancia de Publish. Al inicio se le asigna un nuevo ID de Sling.
1. Valide que **Sling ID** sea ahora único.

Repita estos pasos hasta que todas las instancias de Publish tengan un ID de Sling único.

### Generador de paquetes Vault Factory {#vault-package-builder-factory}

Para que las actualizaciones se sincronicen correctamente, es necesario modificar el generador de paquetes Vault para la sincronización de usuarios.
En `/home/users`, se crea un nodo `*/rep:cache`. Es una caché que se utiliza para encontrar que si consultamos el nombre principal de un nodo, entonces esta caché se puede utilizar directamente.

La sincronización de usuarios se puede detener si se sincronizan `rep :cache` nodos entre editores.

AEM Para asegurarse de que las actualizaciones se sincronizan correctamente entre los editores, en cada instancia de Publish de la:

1. Acceder a la [consola web](/help/sites-deploying/configuring-osgi.md)

   Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Busque el paquete de distribución **Apache Sling - Vault Package Builder Factory**

   Nombre del generador: socialpubsync-vlt.

1. Seleccione el icono de edición.
1. Añada dos filtros de nodo de paquete:
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. Gestión de políticas
   * Para sobrescribir los nodos de rep :policy existentes con los nuevos, agregue un tercer filtro de paquete: `/home/users|+.*/rep:policy`
   * Para evitar que se distribuyan directivas, establezca: `Acl Handling: IGNORE`

   ![Fábrica del generador de paquetes Vault](assets/vault-package-builder-factory.png)

## Solución de problemas de distribución de Sling en AEM Communities {#troubleshoot-sling-distribution-in-aem-communities}

Si la distribución de Sling falla, intente los siguientes pasos de depuración:

1. **Comprobar [configuraciones agregadas incorrectamente](/help/sites-administering/sync.md#improperconfig)**

   Asegúrese de que no se agregan ni editan varias configuraciones y, en su lugar, se deben editar las configuraciones predeterminadas existentes.
1. **Comprobar configuraciones**

   AEM Asegúrese de que todas las [configuraciones](/help/communities/sync.md#bestpractices) estén correctamente configuradas en su instancia de autor de la, tal como se menciona en las [prácticas recomendadas](/help/communities/sync.md#main-pars-header-863110628).

1. **Comprobar permisos de usuario autorizados**

   Si los paquetes no están instalados correctamente, compruebe que el [usuario autorizado](/help/sites-administering/sync.md#createauthuser) creado en la primera instancia de Publish tenga las ACL correctas.

   Para validar esto, en lugar de [crear usuario autorizado](/help/sites-administering/sync.md#createauthuser), cambie la configuración de [Adobe Granite Distribution - Encrypted Password Transport Secret Provider](/help/sites-administering/sync.md#adobegraniteencpasswrd) en la instancia de autor para usar las credenciales de usuario administrador. Ahora intente instalar los paquetes de nuevo. Si la sincronización de usuarios funciona correctamente con las credenciales del administrador, significa que el usuario de publicación creado no tenía las ACL adecuadas.

1. **Comprobar la configuración de fábrica de Diff Observer**

   Si solo los nodos específicos no se sincronizan en el conjunto de servidores de publicación (por ejemplo, los miembros del grupo no se sincronizan), asegúrese de que la configuración de [Adobe Granite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver) esté habilitada y de que **rep: members** se establezcan en **nombres de propiedades buscadas**.

1. **Compruebe la configuración del Receptor de sincronización de usuarios de AEM Communities.** Si los usuarios creados están sincronizados, pero las suscripciones y las siguientes no funcionan, asegúrese de que la configuración del Receptor de sincronización de usuarios de AEM Communities tenga:

   * Tipos de nodos- establecidos en **rep:User, nt:unstructured**, **nt:resource**, **rep:ACL**, **sling:Folder** y **sling:OrderedFolder**.
   * Nodos ignorables- establecidos en **.tokens**, **system** y **rep :cache**.
   * Carpetas distribuidas: establezca las carpetas que desea distribuir.

1. **Registros de comprobación generados al crear usuarios en la instancia de Publish**

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

   1. Acceda a la [consola web](/help/sites-deploying/configuring-osgi.md). Por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Busque la configuración **Agente de distribución Apache Sling: fábrica de agentes de sincronización**.
   1. Anule la selección de la casilla **Habilitado**.

      Al deshabilitar la sincronización de usuarios en los extremos de las instancias de autor (exportador e importador), se deshabilitan y la instancia de autor es estática. El autor no ha hecho ping a los paquetes **vlt** ni los ha recuperado.

      Ahora, si se crea un usuario en la instancia de publicación, el paquete **vlt** se crea en el nodo */var/sling/distribution/packages/ socialpubsync - vlt /data*. Y si el autor inserta estos paquetes en otro servicio. Puede descargar y extraer estos datos para comprobar qué propiedades se insertan en otros servicios.

1. Vaya a un editor y cree un usuario en él. Como resultado, se crean eventos.
1. Compruebe el [orden de los registros](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities) creados al crear el usuario.
1. Compruebe si se ha creado un paquete **vlt** en **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. AEM Ahora, habilite la sincronización de usuarios en la instancia de autor de la.
1. En el publicador, cambie los extremos del exportador o del importador en **Apache Sling Distribution Agent - Sync Agents Factory**.
Podemos descargar y extraer datos de paquetes para comprobar todas las propiedades que se insertan en otros editores y qué datos se pierden.
