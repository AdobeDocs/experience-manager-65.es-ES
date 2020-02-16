---
title: Sincronización de usuarios de comunidades
seo-title: Sincronización de usuarios de comunidades
description: Funcionamiento de la sincronización de usuarios
seo-description: Funcionamiento de la sincronización de usuarios
uuid: 772b82bd-a66c-4c1d-b80b-dcff77c873a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 97286c2c-f6e3-43ec-b1a9-2abb58616778
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Sincronización de usuarios de comunidades{#communities-user-synchronization}

## Introducción {#introduction}

En Comunidades AEM, desde el entorno de publicación (según los permisos configurados), los visitantes *del* sitio pueden convertirse en *miembros*, crear grupos *de* usuarios y editar su perfil *de* miembro.

*Datos* de usuario es un término utilizado para referirse a *usuarios*, perfiles *de* usuario y grupos *de* usuarios.

*Miembros* es un término que se utiliza para referirse a *los usuarios* registrados en el entorno de publicación, a diferencia de los usuarios registrados en el entorno de creación.

Para obtener más información sobre los datos de usuario, visite [Administración de usuarios y grupos](/help/communities/users.md)de usuarios.

## Sincronización de usuarios en un conjunto de servidores de publicación {#synchronizing-users-across-a-publish-farm}

Por diseño, los datos de usuario creados en el entorno de publicación no aparecen en el entorno de creación.

La mayoría de los datos de usuario creados en el entorno de creación están pensados para permanecer en el entorno de creación y no se sincronizan ni replican para publicar instancias.

Cuando la [topología](/help/communities/topologies.md) es un conjunto de servidores [de](/help/sites-deploying/recommended-deploys.md#tarmk-farm)publicación, el registro y las modificaciones realizadas en una instancia de publicación deben sincronizarse con otras instancias de publicación. Los miembros deben poder iniciar sesión y ver sus datos en cualquier nodo de publicación.

Cuando la sincronización de usuarios está habilitada, los datos de usuario se sincronizan automáticamente en todas las instancias de publicación del conjunto de servidores.

### Instrucciones de configuración de sincronización de usuarios {#user-sync-setup-instructions}

Para obtener instrucciones detalladas paso a paso sobre cómo habilitar la sincronización en un conjunto de servidores de publicación, consulte

* [Sincronización de usuarios](/help/sites-administering/sync.md)

## Sincronización del usuario en segundo plano {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **paquete** vlt: es un archivo zip de todos los cambios realizados en un editor, que deben distribuirse entre los editores. Los cambios realizados en un editor generan eventos que elige el detector de eventos change. Esto crea un paquete vlt que contiene todos los cambios.

* **paquete** de distribución: contiene información de distribución para Sling. Es información sobre dónde debe distribuirse el contenido y cuándo se distribuyó por última vez.

## Qué sucede cuando... {#what-happens-when}

### Publicar sitio desde la consola Sitios de comunidades {#publish-site-from-communities-sites-console}

En el autor, cuando se publica un sitio de comunidad desde la consola [Sitios de](/help/communities/sites-console.md)comunidades, el efecto es [replicar](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) las páginas asociadas y Sling distribuir los grupos de usuarios de la comunidad creados dinámicamente, incluida su pertenencia.

### El usuario se crea o edita el perfil al publicar {#user-is-created-or-edits-profile-on-publish}

Por diseño, los usuarios y perfiles creados en el entorno de publicación (por ejemplo, mediante registro propio, inicio de sesión social o autenticación LDAP) no aparecen en el entorno de creación.

Cuando la topología es un conjunto de servidores [de](/help/communities/topologies.md) publicación y la sincronización de usuarios se ha configurado correctamente, el perfil de *usuario* y ** usuario se sincroniza en el conjunto de servidores de publicación mediante la distribución Sling.

### Se crea un nuevo grupo de comunidad en la publicación {#new-community-group-is-created-on-publish}

Aunque se inicia desde una instancia de publicación, la creación de grupos de comunidad, que da como resultado nuevas páginas de sitio y un nuevo grupo de usuarios, se produce realmente en la instancia de autor.

Como parte del proceso, las nuevas páginas del sitio se replican en todas las instancias de publicación. El grupo de usuarios de la comunidad creado dinámicamente y su pertenencia son Sling distribuidos en todas las instancias de publicación.

### Los usuarios o grupos de usuarios se crean con la consola de seguridad {#users-or-user-groups-are-created-using-security-console}

Por diseño, los datos de usuario creados en el entorno de publicación no aparecen en el entorno de creación y viceversa.

Cuando se utiliza la consola Administración de [usuarios y seguridad](/help/sites-administering/security.md) para agregar usuarios nuevos en el entorno de publicación, la sincronización de usuarios sincronizará los usuarios nuevos y su pertenencia a grupos con otras instancias de publicación, si es necesario. La sincronización de usuarios también sincronizará los grupos de usuarios creados mediante la consola de seguridad.

### El usuario publica contenido al publicar {#user-posts-content-on-publish}

Para el contenido generado por el usuario (UGC), se accede a los datos introducidos en una instancia de publicación a través del SRP [](/help/communities/srp-config.md)configurado.

## Best practices {#bestpractices}

De forma predeterminada, la sincronización de usuarios está **deshabilitada**. Habilitar la sincronización de usuarios implica modificar las configuraciones de OSGi *existentes* . No se deben agregar nuevas configuraciones como resultado de habilitar la sincronización de usuarios.

La sincronización de usuarios depende del entorno de creación para administrar las distribuciones de datos de usuario, aunque los datos de usuario no se hayan creado en el autor.

**Requisitos previos**

1. Si ya se han creado usuarios y grupos de usuarios en un editor, se recomienda sincronizar [](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) manualmente los datos de usuario con todos los editores antes de configurar y habilitar la sincronización de usuarios.
Una vez habilitada la sincronización de usuarios, solo se sincronizan los usuarios y grupos recién creados.

1. Asegúrese de que se ha instalado el código más reciente:

   * [Actualizaciones de la plataforma AEM](https://helpx.adobe.com/experience-manager/kb/aem62-available-hotfixes.html)
   * [Actualizaciones de AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

Las siguientes configuraciones son necesarias para habilitar la sincronización de usuarios en comunidades AEM. Asegúrese de que estas configuraciones sean correctas para evitar que la distribución de contenido de sling falle.

### Agente de distribución Apache Sling: fábrica de agentes de sincronización {#apache-sling-distribution-agent-sync-agents-factory}

Esta configuración recoge el contenido que se va a sincronizar en los editores. La configuración está en la instancia de Autor. El autor debe realizar un seguimiento de todos los editores que están allí y dónde sincronizar toda la información.

Los valores predeterminados de la configuración son para una sola instancia de publicación. Dado que la sincronización de usuarios resulta útil para sincronizar varias instancias de publicación, como en un conjunto de publicaciones, es necesario agregar más instancias de publicación a la configuración.

**¿Cómo se sincroniza el contenido?**

La instancia de autor indica el punto final del exportador de los editores. Cada vez que se crea o actualiza un usuario en editores específicos (n), el autor obtiene el contenido de los extremos de sus exportadores y lo [](/help/communities/sync.md#main-pars-image-1413756164) envía a otros editores (n-1, que es distinto de los editores de los que se obtiene el contenido).

Para configurar los agentes de sincronización de Apache Sling

En la instancia de creación de AEM:

1. Inicie sesión con privilegios de administrador.
1. Acceda a la consola [web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html). Por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Localice **Apache Sling Distribution Agent - Sync Agent Factory.**

   * Seleccione la configuración existente para abrirla y editarla (icono de lápiz).
   Verificar nombre: **socialpubsync.**

   * Seleccione la casilla de verificación **Habilitado** .
   * Seleccione **Usar varias colas.**
   * Especifique los extremos **de** exportador y los extremos **de** importador (puede agregar más extremos de exportador e importador).

      Estos extremos definen de dónde desea obtener el contenido y desde dónde desea insertar el contenido. El autor obtiene el contenido del extremo del exportador especificado y lo envía a los editores (excepto al editor desde el que obtuvo el contenido).


![sync-agent-facto](assets/sync-agent-fact.png)

### Distribución de Adobe Granite: proveedor secreto de transporte de contraseña cifrada {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

Permite al autor identificar al usuario autorizado, ya que tiene permiso para sincronizar datos de usuario del autor para realizar la publicación.

El usuario [autorizado creado](/help/sites-administering/sync.md#createauthuser) en todas las instancias de publicación ayuda a los editores a conectarse con el autor y a configurar la distribución de Sling en el autor. Este usuario autorizado tiene todas las [ACL](/help/sites-administering/sync.md#howtoaddacl)necesarias.

Siempre que se vayan a instalar o recuperar datos de los editores, el autor se conecta con los editores mediante las credenciales (nombre de usuario y contraseña) establecidas en esta configuración.

Para conectar a un autor con editores mediante un usuario autorizado

En la instancia de creación de AEM:

1. Inicie sesión con privilegios de administrador.
1. Acceda a la consola [web](/help/sites-deploying/configuring-osgi.md).

   Por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Localice **Adobe Granite Distribution - Proveedor secreto de transporte de contraseña cifrada.**
1. Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

   Verificar propiedad **socialpubsync** - **publishUser.**

1. Establezca el nombre de usuario y la contraseña para el usuario [](/help/sites-administering/sync.md#createauthorizeduser)autorizado.

   Por ejemplo, **usersync - admin**

![granite-paswrd-trans](assets/granite-paswrd-trans.png)

### Agente de distribución Apache Sling: fábrica de agentes de cola {#apache-sling-distribution-agent-queue-agents-factory}

Esta configuración se utiliza para configurar los datos que desea sincronizar entre los editores. Cuando se crean o actualizan datos en rutas especificadas en **Allowed Roots**, se activa &quot;var/community/distribution/diff&quot; y el replicador creado obtiene los datos de un publicador y los instala en otros editores.

Para configurar los datos (rutas de nodos) para sincronizar

En la instancia de publicación de AEM:

1. Inicie sesión con privilegios de administrador.
1. Acceda a la consola [web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Localice **Apache Sling Distribution Agent - Queue Agent Factory.**
1. Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

   Verificar nombre: **socialpubsync -inverso.**

1. Seleccione la casilla de verificación **Habilitado** y guarde.
1. Especifique las rutas de nodo que se replicarán en las raíces **permitidas**.
1. Repita el procedimiento para cada instancia de **publicación** .

![queue-agent-facto](assets/queue-agents-fact.png)

### Distribución de Adobe Granite: Fábrica de observación de diferencias {#adobe-granite-distribution-diff-observer-factory}

Esta configuración sincroniza la pertenencia a grupos entre editores.
Si al cambiar la pertenencia a un grupo en un publicador no se actualiza su pertenencia a otros editores, asegúrese de que **ref:integrantes** se agrega a los nombres **de propiedades** vistos.

Para garantizar la sincronización de miembros

En cada instancia de publicación de AEM:

1. Inicie sesión con privilegios de administrador.
1. Acceda a la consola [web](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html).

   Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. Localice **Adobe Granite Distribution - Diff Observer Factory.**
1. Seleccione la configuración existente para abrirla y editarla (icono de lápiz).

   Verificar nombre **del agente: socialpubsync -inverso**.

1. Seleccione la casilla de verificación **Habilitado** .
1. Especifique **rep:miembros** como descripción para propertyName en nombres **de propiedades** vistos y Guardar.

![diff-obs](assets/diff-obs.png)

### Activador de distribución de Apache Sling: fábrica de activadores programados {#apache-sling-distribution-trigger-scheduled-triggers-factory}

Esta configuración le permite configurar el intervalo de sondeo (después de lo cual el autor hace ping a los editores y extrae los cambios) para sincronizar los cambios entre los editores.

El autor sondea a los editores cada 30 segundos (valor predeterminado). Si hay algún paquete presente en la carpeta */var/sling/distribution/packages/ socialpubsync - vlt /shared*, entonces recogerá esos paquetes y los instalará en otros editores.

Para modificar el intervalo de sondeo

En la instancia de creación de AEM:

1. Inicie sesión con privilegios de administrador.
1. Acceda a la consola [web](/help/sites-deploying/configuring-osgi.md), por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Localizar el activador de distribución Sling de **Apache - Fábrica de activadores programados**

   * Seleccione la configuración existente para abrirla y editarla (icono de lápiz)

      Verificar **socialpubsync -schedule-desencadenador**

   * Establezca el intervalo en segundos en el intervalo deseado y guárdelo.

![schedule-desencadenador](assets/scheduled-trigger.png)

### Escucha de sincronización de usuarios de AEM Communities {#aem-communities-user-sync-listener}

Para problemas en la distribución de Sling en los que hay discrepancia en las suscripciones y que se muestran a continuación, compruebe si se han establecido las siguientes propiedades en las configuraciones de escucha de sincronización de usuarios de Comunidades de **AEM** :

* NodeTypes
* IgnorableProperties
* Nodos ignorables
* DistributedFolders

Para sincronizar suscripciones, seguimientos y notificaciones

En cada instancia de publicación de AEM:

1. Inicie sesión con privilegios de administrador.
1. Acceda a la consola [web](/help/sites-deploying/configuring-osgi.md). Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Busque el oyente de sincronización de usuarios de comunidades **AEM.**
1. Seleccione la configuración existente para abrirla y editarla (icono de lápiz)

   Verificar nombre: **socialpubsync -schedule-desencadenador**

1. Establezca los siguientes **NodeTypes**:

   rep:Usuario

   nt:unstructured

   nt:resource

   rep:ACL

   sling:Folder

   sling:OrderedFolder

   Los tipos de nodo especificados en esta propiedad se sincronizarán y la información de notificaciones (blogs y configuraciones seguidos) se sincronizarán entre diferentes editores.

1. Agregue todas las carpetas para sincronizar en **DistributedFolders**. Por ejemplo,

   segmentos/puntuación

   social/relaciones

   actividades

1. Establecer los **ignorantes** como:

   .tokens

   sistema

   rep:cache (ya que usamos sesiones adhesivas, no necesitamos sincronizar este nodo con diferentes editores)

![user-sync-listner](assets/user-sync-listner.png)

### ID de Sling único {#unique-sling-id}

La instancia de creación de AEM utiliza el ID de Sling para identificar de dónde provienen los datos y a qué editores debe (o no necesita) devolver el paquete.

Asegúrese de que todos los editores de un conjunto de servidores de publicación tengan un ID de Sling único. Si el ID de Sling es el mismo para varias instancias de publicación en un conjunto de servidores de publicación, se producirá un error en la sincronización del usuario. Como el autor no sabrá de dónde recuperar el paquete y desde dónde instalarlo.

Para garantizar un ID de Sling único de los editores en el conjunto de servidores de publicación

En cada instancia de publicación:

1. Vaya a [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. Compruebe el valor del ID de **Sling.**

![slingid](assets/slingid.png)

Si el ID de Sling de una instancia de publicación coincide con el ID de Sling de cualquier otra instancia de publicación, entonces:

1. Detenga una de las instancias de publicación que tenga un ID de Sling coincidente.
1. En el `crx-quickstart/launchpad/felix` directorio, busque y elimine el archivo denominado *sling.id.file.*

   por ejemplo, en un sistema Linux:

   `rm -i $(find . -type f -name sling.id.file)`

   por ejemplo, en un sistema Windows:

   utilice el explorador de Windows y busque `sling.id.file`

1. Inicie la instancia de publicación. Al iniciar se le asignará un nuevo ID de Sling.
1. Valide que el ID **de** Sling sea ahora único.

Repita estos pasos hasta que todas las instancias de publicación tengan un ID de Sling único.

### Fábrica del generador de paquetes de almacén {#vault-package-builder-factory}

Para que las actualizaciones se sincronizen correctamente, es necesario modificar el creador de paquetes de bóveda para la sincronización del usuario.
En **/inicio/usuarios**, se crea un nodo ***/rep:cache **node. Es una caché que se utiliza para encontrar que si consultamos el nombre principal de un nodo, esta caché se puede utilizar directamente.

La sincronización de usuarios se puede detener si se sincronizan `rep :cache `nodos entre editores.

Para asegurarse de que las actualizaciones se sincronizan correctamente entre editores

En cada instancia de publicación de AEM:

1. Acceso a la consola [web](/help/sites-deploying/configuring-osgi.md)

   por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. Localice el paquete de distribución Sling de **Apache - Fábrica del generador de paquetes Vault**

   Nombre del generador: socialpubsync-vlt.

1. Seleccione el icono de edición.
1. Agregar dos filtros de nodo de paquete:
   * /home/users|-.*/.tokens
   * /home/users|**-**.*/rep:cache

1. Gestión de políticas

   * para sobrescribir los nodos rep:policy existentes con otros nuevos, agregue un tercer filtro de paquete:

      /home/users|**+**.*/rep:policy

   * para evitar que las políticas se distribuyan, establezca

      Administración de llamada: IGNORE

![Fábrica del generador de paquetes Vault](assets/vault-package-builder-factory.png)

## Solución de problemas de distribución de Sling en comunidades AEM {#troubleshoot-sling-distribution-in-aem-communities}

Si la distribución de Sling falla, pruebe los siguientes pasos de depuración:

1. **Compruebe si hay configuraciones[agregadas](/help/sites-administering/sync.md#improperconfig)incorrectamente.** Asegúrese de que no se agreguen ni editen varias configuraciones; en su lugar, se deben editar las configuraciones predeterminadas existentes.
1. **Compruebe las configuraciones**. Asegúrese de que todas las [](/help/communities/sync.md#bestpractices)configuraciones estén correctamente configuradas en la instancia de AEM Author, como se indica en las [optimizaciones](/help/communities/sync.md#main-pars-header-863110628).
1. **Compruebe los permisos** de usuario autorizados. Si los paquetes no están instalados correctamente, compruebe que el usuario [](/help/sites-administering/sync.md#createauthuser) autorizado creado en la primera instancia de Publish tenga las ACL correctas.

   Para validar esto, en lugar de [crear un usuario](/help/sites-administering/sync.md#createauthuser) autorizado, cambie la configuración del proveedor [secreto de transporte de](/help/sites-administering/sync.md#adobegraniteencpasswrd) Adobe Granite Distribution - Encrypted Password Transport Secret en la instancia de autor para utilizar las credenciales de usuario administrador. Ahora intente instalar los paquetes de nuevo. Si la sincronización de usuario funciona correctamente con las credenciales de administrador, significa que el usuario de publicación creado no tenía las ACL adecuadas.

1. **Compruebe la configuración** de la fábrica de observación de Diff. Si solo los nodos específicos no se sincronizan en la granja de publicaciones (por ejemplo, los miembros del grupo no se sincronizan), asegúrese de que la configuración de [Adobe Granite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver) esté habilitada y **rep: los miembros** se configuran en nombres **de propiedades** miradas.
1. **Compruebe la configuración del escucha de sincronización de usuarios de AEM Communities.** Si los usuarios creados están sincronizados pero las suscripciones y los siguientes no están funcionando, asegúrese de que la configuración del agente de escucha de sincronización de usuarios de AEM Communities tenga:

   * Tipos de nodos: definidos en **rep:User, nt:unestructure**, **nt:resource**, **rep:ACL**, **sling:Folder** y **sling:OrderedFolder**
   * Nodos ignorables establecidos en **.tokens**, **sistema** y **rep:cache**
   * Carpetas distribuidas: configure las carpetas que desee distribuir

1. **Compruebe los registros generados al crear el usuario en la instancia** de publicación. Si las configuraciones anteriores están correctamente configuradas pero la sincronización de usuarios no funciona, compruebe los registros generados al crear el usuario.

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

   1. Deshabilitar la sincronización de usuarios:
   1. En la instancia de creación de AEM, inicie sesión con privilegios de administrador.

      1. Acceda a la consola [web](/help/sites-deploying/configuring-osgi.md). Por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
      1. Localice la configuración **Apache Sling Distribution Agent - Sync Agent Factory**.
      1. Anule la selección de la casilla de verificación **Habilitado** .
Al desactivar la sincronización de usuarios en la instancia de autor, los extremos (exportador e importador) se desactivan y la instancia de autor es estática. El **autor no pega ni captura los paquetes vlt** .
Ahora, si se crea un usuario en una instancia de publicación, el paquete **vlt** se crea en el nodo */var/sling/distribution/packages/ socialpubsync - vlt /data* . Y si el autor envía estos paquetes a otro servicio. Puede descargar y extraer estos datos para comprobar qué propiedades se insertan en otros servicios.
   1. Vaya a un editor y cree un usuario en el editor. Como resultado, se crean eventos.
   1. Compruebe el [orden de los registros](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities), creados al crearlos.
   1. Compruebe si se ha creado un **vlt **paquete en **/var/sling/distribution/packages/socialpubsync-vlt/data**.
   1. Ahora, habilite la sincronización de usuarios en la instancia de creación de AEM.
   1. En el editor, cambie los extremos del exportador o del importador en **Apache Sling Distribution Agent - Sync Agent Factory**.
Podemos descargar y extraer datos del paquete para comprobar qué propiedades se insertan en otros editores y qué datos se pierden.
