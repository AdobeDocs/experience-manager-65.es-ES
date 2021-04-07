---
title: Sincronización de usuarios
seo-title: Sincronización de usuarios
description: Obtenga información sobre la sincronización de usuarios en AEM.
seo-description: Obtenga información sobre la sincronización de usuarios en AEM.
uuid: 0a519daf-21b7-4adc-b419-eeb8c404c54f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: c061b358-8c0d-40d3-8090-dc9800309ab3
docset: aem65
exl-id: 89f55598-e749-42b8-8f2a-496f45face66
feature: Seguridad
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '2437'
ht-degree: 3%

---

# Sincronización de usuarios{#user-synchronization}

## Introducción {#introduction}

Cuando la implementación es un [conjunto de servidores de publicación](/help/sites-deploying/recommended-deploys.md#tarmk-farm), los miembros deben poder iniciar sesión y ver sus datos en cualquier nodo de publicación.

Los usuarios y grupos de usuarios (datos de usuario) creados en el entorno de publicación no son necesarios en el entorno de creación.

La mayoría de los datos de usuario creados en el entorno de creación están pensados para permanecer en el entorno de creación y no se copian en las instancias de publicación.

El registro y las modificaciones realizadas en una instancia de publicación deben sincronizarse con otras instancias de publicación para que tengan acceso a los mismos datos de usuario.

A partir de AEM 6.1, cuando la sincronización de usuarios está habilitada, los datos de usuario se sincronizan automáticamente en las instancias de publicación de la granja y no se crean en el autor.

## Distribución de Sling {#sling-distribution}

Los datos del usuario, junto con sus [ACL](/help/sites-administering/security.md), se almacenan en el [Oak Core](/help/sites-deploying/platform.md), la capa debajo de Oak JCR, y se accede a ellos mediante la [API Oak](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html). Con actualizaciones poco frecuentes, es razonable que los datos de usuario se sincronicen con otras instancias de publicación que utilizan [Sling Content Distribution](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md) (distribución de Sling).

Los beneficios de la sincronización de usuarios mediante la distribución de Sling, en comparación con la replicación tradicional, son:

* *los usuarios*, los  *perfiles de* usuario y los grupos de  *usuarios* creados al publicar no se crean en el autor

* La distribución de Sling establece propiedades en eventos jcr, lo que permite actuar dentro de los oyentes de eventos del lado de publicación sin preocuparse por los bucles de replicación infinitos
* La distribución de Sling solo envía datos de usuario a instancias de publicación que no sean de origen, eliminando así el tráfico innecesario
* [](/help/sites-administering/security.md) Los ACLsset en el nodo de usuario se incluyen en la sincronización

>[!NOTE]
>
>Si se requieren sesiones, se recomienda utilizar una solución SSO o utilizar una sesión adhesiva y hacer que los clientes inicien sesión si se cambian a otro publicador.

>[!CAUTION]
>
>No se admite la sincronización del grupo ***administradores*** aunque la sincronización de usuarios esté habilitada. En su lugar, se registrará un error al &quot;importar la comparación de diferencias&quot; en el registro de errores.
>
>Por lo tanto, cuando la implementación es un conjunto de servidores de publicación, si se agrega o elimina un usuario del grupo ***administradores**, la modificación debe realizarse manualmente en cada instancia de publicación.

## Habilitar sincronización de usuarios {#enable-user-sync}

>[!NOTE]
>
>De forma predeterminada, la sincronización de usuarios es `disabled`.
>
>Habilitar la sincronización de usuarios implica modificar las configuraciones de OSGi *existentes*.
>
>No se deben agregar nuevas configuraciones como resultado de habilitar la sincronización de usuarios.

La sincronización de usuarios depende del entorno de creación para administrar las distribuciones de datos de usuario, aunque los datos de usuario no se creen en el autor. Gran parte de la configuración, pero no toda, se realiza en el entorno de creación y cada paso identifica claramente si se va a realizar en el autor o la publicación.

A continuación se indican los pasos necesarios para habilitar la sincronización de usuarios, seguidos de la sección [Resolución de problemas](#troubleshooting):

### Requisitos previos {#prerequisites}

1. Si ya se han creado usuarios y grupos de usuarios en un publicador, se recomienda [sincronizar manualmente](#manually-syncing-users-and-user-groups) los datos de usuario con todos los publicadores antes de configurar y habilitar la sincronización de usuarios.

Una vez habilitada la sincronización de usuarios, solo se sincronizan los usuarios y grupos recién creados.

1. Asegúrese de que se ha instalado el código más reciente:

* [AEM actualizaciones de la plataforma](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=es)
* [Actualizaciones de AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Agente de distribución Apache Sling: fábrica de agentes de sincronización {#apache-sling-distribution-agent-sync-agents-factory}

**Habilitar sincronización de usuarios**

* **en author**

   * iniciar sesión con privilegios de administrador
   * acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * localizar `Apache Sling Distribution Agent - Sync Agents Factory`

      * seleccione la configuración existente para abrirla y editarla (icono de lápiz)
Verificar `name`: **`socialpubsync`**

      * seleccione la casilla de verificación `Enabled`
      * select `Save`


![](assets/chlimage_1-20.png)

### 2. Crear usuario autorizado {#createauthuser}

**Configure**
permisosEste usuario autorizado se utilizará en el paso 3 para configurar la distribución de Sling en Author.

* **en cada instancia de publicación**

   * iniciar sesión con privilegios de administrador
   * acceda a la [Consola de seguridad](/help/sites-administering/security.md)

      * por ejemplo, [https://localhost:4503/useradmin](https://localhost:4503/useradmin)
   * crear un nuevo usuario

      * por ejemplo, `usersync-admin`
   * agregar este usuario al grupo de usuarios **`administrators`**
   * [agregar ACL para este usuario a /home](#howtoaddacl)

      * `Allow jcr:all` con restricción  `rep:glob=*/activities/*`



>[!CAUTION]
>
>Se debe crear un nuevo usuario.
>
>* El usuario predeterminado asignado es **`admin`**.
>* No use `communities-user-admin user.`

>



#### Cómo agregar ACL {#addacls}

* CRXDE Lite de acceso

   * por ejemplo, [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* seleccione el nodo `/home`
* en el panel derecho, seleccione la pestaña `Access Control`
* seleccione el botón `+` para añadir una entrada ACL

   * **Principal**:  *buscar usuarios creados para sincronización de usuarios*
   * **Tipo**: `Allow`
   * **Privilegios**:  `jcr:all`
   * **** Restricciones, rep:glob:  `*/activities/*`
   * seleccione **OK**

* seleccione **Guardar todo**

![](assets/chlimage_1-21.png)

Consulte también

* [Gestión de derechos de acceso](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* Sección Resolución de problemas [Modificación de la excepción de operación durante el procesamiento de respuestas](#modify-operation-exception-during-response-processing).

### 3. Distribución de Adobe Granite: proveedor secreto de transporte de contraseña cifrada {#adobegraniteencpasswrd}

**Configuración de permisos**

Una vez que se ha creado un usuario autorizado, un miembro del grupo de usuarios **`administrators`**, en todas las instancias de publicación, ese usuario autorizado debe ser identificado por el autor como con permiso para sincronizar los datos de usuario del autor a la publicación.

* **en author**

   * iniciar sesión con privilegios de administrador
   * acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * localizar `com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name`
   * seleccione la configuración existente para abrirla y editarla (icono de lápiz)
Verificar `property name`: **`socialpubsync-publishUser`**

   * establezca el nombre de usuario y la contraseña en el [usuario autorizado](#createauthuser) creado al publicar en el paso 2

      * por ejemplo, `usersync-admin`


![](assets/chlimage_1-22.png)

### 4. Agente de distribución Apache Sling: fábrica de agentes de cola {#apache-sling-distribution-agent-queue-agents-factory}

**Habilitar sincronización de usuarios**

* **al publicar**:

   * iniciar sesión con privilegios de administrador
   * acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * localizar `Apache Sling Distribution Agent - Queue Agents Factory`

      * seleccione la configuración existente para abrirla y editarla (icono de lápiz)
Verificar `Name`: `socialpubsync-reverse`

      * seleccione la casilla de verificación `Enabled`
      * seleccione `Save`
   * **repetir **para cada instancia de publicación



![](assets/chlimage_1-23.png)

### 5. Adobe Social Sync - Diff Observer Factory {#diffobserver}

**Habilitar la sincronización de grupos**

* **en cada instancia** de publicación:

   * iniciar sesión con privilegios de administrador
   * acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * localizar **`Adobe Social Sync - Diff Observer Factory`**

      * seleccione la configuración existente para abrirla y editarla (icono de lápiz)

         Verificar `agent name`: `socialpubsync-reverse`

      * seleccione la casilla de verificación `Enabled`
      * seleccione `Save`


![](assets/screen-shot_2019-05-24at090809.png)

### 6. Déclencheur de distribución de Apache Sling: fábrica de Déclencheur programados {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**(Opcional) modificar el intervalo de sondeo**

De forma predeterminada, el autor sondeará los cambios cada 30 segundos. Para modificar este intervalo:

* **en author**

   * iniciar sesión con privilegios de administrador
   * acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * localizar `Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * seleccione la configuración existente para abrirla y editarla (icono de lápiz)

         * Verificar `Name`: `socialpubsync-scheduled-trigger`
      * establezca el `Interval in Seconds` en el intervalo deseado
      * seleccione `Save`



![](assets/chlimage_1-24.png)

## Configurar para varias instancias de publicación {#configure-for-multiple-publish-instances}

La configuración predeterminada es para una única instancia de publicación. Como el motivo para habilitar la sincronización de usuarios es sincronizar varias instancias de publicación, como para un conjunto de servidores de publicación, las instancias de publicación adicionales deberán agregarse a la fábrica de agentes de sincronización.

### 7. Agente de distribución Apache Sling: fábrica de agentes de sincronización {#apache-sling-distribution-agent-sync-agents-factory-1}

**Agregar instancias de publicación:**

* **en author**

   * iniciar sesión con privilegios de administrador
   * acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * localizar `Apache Sling Distribution Agent - Sync Agents Factory`

      * seleccione la configuración existente para abrirla y editarla (icono de lápiz)
Verificar `Name`: `socialpubsync`


![](assets/chlimage_1-25.png)

* **Puntos**
finales del exportadorDebe haber un punto final del exportador para cada editor. Por ejemplo, si hay 2 editores, localhost:4503 y 4504, debe haber 2 entradas:

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **Puntos**
finales del importadorDebe haber un punto final del importador para cada publicador. Por ejemplo, si hay 2 editores, localhost:4503 y 4504, debe haber 2 entradas:

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* seleccione `Save`

### 8. Listener de sincronización de usuarios de AEM Communities {#aem-communities-user-sync-listener}

**(Opcional) Sincronizar nodos JCR adicionales**

Si hay datos personalizados que se desea sincronizar en varias instancias de publicación, entonces:

* **en cada instancia** de publicación:

   * iniciar sesión con privilegios de administrador
   * acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, `https://localhost:4503/system/console/configMgr`
   * localizar `AEM Communities User Sync Listener`
   * seleccione la configuración existente para abrirla y editarla (icono de lápiz)
Verificar `Name`: `socialpubsync-scheduled-trigger`


![](assets/chlimage_1-26.png)

* **Tipos de**
nodoEsta es la lista de tipos de nodos que se sincronizarán. Cualquier tipo de nodo que no sea sling:Folder debe aparecer aquí (sling:folder se gestiona de forma independiente).
Lista predeterminada de tipos de nodos para sincronizar:

   * rep:Usuario
   * nt:unstructured
   * nt:resource

* **Propiedades**
ignorablesEsta es la lista de propiedades que se ignorarán si se detecta algún cambio. Los cambios realizados en estas propiedades pueden sincronizarse como un efecto secundario de otros cambios (ya que la sincronización siempre se realiza en el nivel de nodo), pero los cambios realizados en estas propiedades no provocarán por sí mismos la sincronización de déclencheur.
Propiedad predeterminada para ignorar:

   * cq:lastModified

* **Subrutas de nodos**
ignorables que se ignorarán por completo durante la sincronización. Nada debajo de estas subrutas se sincronizará en cualquier momento.
Nodos predeterminados para ignorar:

   * .tokens
   * sistema

* **Distributed**
FoldersLa mayoría de las carpetas sling:Folders se ignoran porque la sincronización no es necesaria. Las pocas excepciones se enumeran aquí.
Carpetas predeterminadas para sincronizar

   * segmentos/puntuación
   * social/relaciones
   * actividades

### 9. ID de Sling único {#unique-sling-id}

>[!CAUTION]
>
>Si el ID de Sling coincide entre dos o más instancias de publicación, la sincronización de grupos de usuarios fallará.

Si el ID de Sling es el mismo para varias instancias de publicación en un conjunto de servidores de publicación, los grupos de usuarios no se sincronizarán.

Para validar que todos los valores de ID de Sling difieren, en cada instancia de publicación:

1. vaya a `http://<host>:<port>/system/console/status-slingsettings`
1. compruebe el valor de **Sling ID**

![](assets/chlimage_1-27.png)

Si el ID de Sling de una instancia de publicación coincide con el ID de Sling de cualquier otra instancia de publicación, entonces:

1. detener una de las instancias de publicación que tenga un ID de Sling coincidente
1. en el directorio crx-quickstart/launchpad/felix

   * busque y elimine el archivo denominado *sling.id.file*

      * por ejemplo, en un sistema Linux:
         `rm -i $(find . -type f -name sling.id.file)`

      * por ejemplo, en un sistema Windows:
         `use windows explorer and search for *sling.id.file*`

1. iniciar la instancia de publicación

   * al inicio, se le asignará un nuevo ID de Sling

1. valide que **Sling ID** ahora es único

Repita estos pasos hasta que todas las instancias de publicación tengan un ID de Sling único.

## Fábrica del Generador de paquetes Vault {#vault-package-builder-factory}

Para que las actualizaciones se sincronicen correctamente, es necesario modificar el creador de paquetes bóveda para la sincronización de usuarios:

* en cada instancia de publicación AEM
* acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md)

   * por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* localizar el `Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* seleccione el icono de edición
* añadir dos `Package Node Filters`:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* gestión de políticas:

   * para sobrescribir los nodos rep:policy existentes con otros nuevos, agregue un tercer filtro de paquetes:

      * `/home/users|+.*/rep:policy`
   * para evitar que las políticas se distribuyan, establezca

      * `Acl Handling:` `IGNORE`


![Fábrica de generador de paquetes de almacenamiento](assets/vault-package-builder-factory.png)

## Qué sucede cuando ... {#what-happens-when}

### El usuario se registra automáticamente o edita el perfil en la publicación {#user-self-registers-or-edits-profile-on-publish}

Por diseño, los usuarios y perfiles creados en el entorno de publicación (registro propio) no aparecen en el entorno de creación.

Cuando la topología es un [conjunto de servidores de publicación](/help/sites-deploying/recommended-deploys.md#tarmk-farm) y la sincronización de usuarios se ha configurado correctamente, el *usuario *y el *perfil de usuario* se sincronizan en el conjunto de servidores de publicación mediante la distribución Sling.

### Los usuarios o grupos de usuarios se crean mediante la Consola de seguridad {#users-or-user-groups-are-created-using-security-console}

Por diseño, los datos de usuario creados en el entorno de publicación no aparecen en el entorno de creación y viceversa.

Cuando se utiliza la consola [Administración de usuarios y seguridad](/help/sites-administering/security.md) para agregar nuevos usuarios en el entorno de publicación, la sincronización de usuarios sincroniza a los nuevos usuarios y su pertenencia a grupos con otras instancias de publicación, si es necesario. La sincronización de usuarios también sincronizará los grupos de usuarios creados mediante la consola de seguridad.

## Solución de problemas {#troubleshooting}

### Cómo desconectar la sincronización de usuarios {#how-to-take-user-sync-offline}

Para desactivar la sincronización de usuarios, para [eliminar un publicador](#how-to-remove-a-publisher) o [sincronizar manualmente los datos](#manually-syncing-users-and-user-groups), la cola de distribución debe estar vacía y en silencio.

Para comprobar el estado de la cola de distribución:

* sobre autor:

   * uso de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * buscar entradas en `/var/sling/distribution/packages`

         * nodos de carpeta con el patrón `distrpackage_*`
   * uso de [Administrador de paquetes](/help/sites-administering/package-manager.md)

      * buscar paquetes pendientes (aún no instalados)

         * con el patrón `socialpubsync-vlt*`
         * creado por `communities-user-admin`


Cuando la cola de distribución esté vacía, desactive la sincronización de usuarios:

* en author

   * *desmarque *la casilla de verificación `Enabled` para [Agente de distribución Apache Sling: fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory)

Una vez completadas las tareas, para volver a habilitar la sincronización de usuarios:

* en author

   * marque la casilla de verificación `Enabled` para [Agente de distribución Apache Sling: fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory)

### Diagnóstico de sincronización de usuario {#user-sync-diagnostics}

Diagnóstico de sincronización de usuarios es una herramienta que comprueba la configuración e intenta identificar cualquier problema.

En el autor, simplemente navegue desde la consola principal a través de **Herramientas, Operaciones, Diagnóstico, Diagnóstico de sincronización de usuarios.**

Al entrar simplemente en la consola Diagnóstico de sincronización de usuarios se mostrarán los resultados.

Esto es lo que se muestra cuando la sincronización de usuarios no está habilitada:

![](assets/chlimage_1-28.png)

#### Cómo ejecutar diagnósticos para editores {#how-to-run-diagnostics-for-publishers}

Cuando el diagnóstico se ejecuta desde el entorno de creación, los resultados de aprobación/error incluirán una sección [INFO] que muestra la lista de instancias de publicación configuradas para su confirmación.

En la lista se incluye una dirección URL para cada instancia de publicación que ejecutará los diagnósticos para esa instancia. El parámetro de URL `syncUser` se anexa a la URL de diagnóstico con su valor establecido en el *usuario de sincronización autorizado* creado en [Paso 2](#createauthuser).

**Nota**: antes de iniciar la URL, el usuario de sincronización  ** autorizado ya debe haber iniciado sesión en esa instancia de publicación.

![](assets/chlimage_1-29.png)

### Configuración añadida incorrectamente {#configuration-improperly-added}

Cuando la sincronización de usuarios no funciona, el problema más común es que se agregaron *configuraciones adicionales*. En su lugar, la *configuración predeterminada existente debería haber sido *editada*.

A continuación se muestran las vistas de cómo aparecen las configuraciones predeterminadas editadas en la consola web. Si aparece más de una instancia, se debe eliminar la configuración añadida.

#### (autor) Un agente de distribución Apache Sling: fábrica de agentes de sincronización {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![](assets/chlimage_1-30.png)

#### (autor) Un Apache Sling Distribution Transport Credentials - User Credentials based DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![](assets/chlimage_1-31.png)

#### (publicar) Un agente de distribución Apache Sling: fábrica de agentes de cola {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![](assets/chlimage_1-32.png)

#### (publicar) Una sincronización de Adobe Social: fábrica de observadores de diferencias {#publish-one-adobe-social-sync-diff-observer-factory}

![](assets/chlimage_1-33.png)

#### (autor) Un Déclencheur de distribución de Apache Sling: fábrica de Déclencheur programados {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![](assets/chlimage_1-34.png)

### Modificar excepción de operación durante el procesamiento de respuestas {#modify-operation-exception-during-response-processing}

Si lo siguiente está visible en el registro:

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

A continuación, compruebe que la sección [2. Se ha seguido correctamente la función Crear usuario autorizado](#createauthuser).

En esta sección se describe la creación de un usuario autorizado, que existe en todas las instancias de publicación, y la identificación de estos en la configuración OSGi de &quot;Proveedor secreto&quot; del autor. De forma predeterminada, el usuario es `admin`.

El usuario autorizado debe hacerse miembro del grupo de usuarios **`administrators`** y los permisos para ese grupo no deben modificarse.

El usuario autorizado debe tener explícitamente los siguientes privilegios y restricciones en todas las instancias de publicación:

| **path** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | */actividades/* |
| /home/users | X | */actividades/* |
| /home/groups | X | */actividades/* |

Como miembro del grupo `administrators`, el usuario autorizado debe tener los siguientes privilegios en todas las instancias de publicación:

| **ruta** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### Error en la sincronización del grupo de usuarios {#user-group-sync-failed}

Si el ID de Sling coincide entre dos o más instancias de publicación, la sincronización de grupos de usuarios fallará.

Consulte la sección [9. ID de Sling único](#unique-sling-id)

### Sincronización manual de usuarios y grupos de usuarios {#manually-syncing-users-and-user-groups}

* en el editor en el que existen usuarios y grupos de usuarios:

   * [si está activado, desactive la sincronización de usuarios](#how-to-take-user-sync-offline)
   * [crear un ](/help/sites-administering/package-manager.md#creating-a-new-package) paquete de  `/home`

      * al editar el paquete

         * Ficha Filtros : Agregar filtro: Ruta raíz: `/home`
         * Ficha Avanzado : Manejo de CA: `Overwrite`
   * [exportar el paquete](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)


* en otras instancias de publicación:

   * [importar el paquete](/help/sites-administering/package-manager.md#installing-packages)

Para configurar o habilitar la sincronización de usuarios, vaya al paso 1: [Agente de distribución Apache Sling: fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory)

### Cuando un publicador deja de estar disponible {#when-a-publisher-becomes-unavailable}

Cuando una instancia de publicación deja de estar disponible, no se debe eliminar si vuelve a estar en línea en el futuro. Los cambios se pondrán en cola para el editor y una vez que vuelva a estar en línea, se procesarán.

Si la instancia de publicación nunca volverá a estar en línea, si está sin conexión de forma permanente, debe eliminarse, ya que la acumulación de colas dará como resultado un uso notable del espacio en disco en el entorno de creación.

Cuando un editor está inactivo, el registro de autor tendrá excepciones similares a:

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### Cómo quitar un publicador {#how-to-remove-a-publisher}

Para eliminar un publicador de la [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory), la cola de distribución debe estar vacía y en silencio.

* sobre autor:

   * [Desconectar sincronización de usuarios](#how-to-take-user-sync-offline)
   * siga el [paso 7](#apache-sling-distribution-agent-sync-agents-factory) para eliminar el editor de ambas listas de servidores:

      * `Exporter Endpoints`
      * `Importer Endpoints`
   * volver a habilitar la sincronización de usuarios

      * marque la casilla de verificación `Enabled` para [Agente de distribución Apache Sling: fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory)
