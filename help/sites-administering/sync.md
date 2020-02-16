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
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Sincronización de usuarios{#user-synchronization}

## Introducción {#introduction}

Cuando la implementación es un conjunto de servidores [de](/help/sites-deploying/recommended-deploys.md#tarmk-farm)publicación, los miembros deben poder iniciar sesión y ver sus datos en cualquier nodo de publicación.

Los usuarios y los grupos de usuarios (datos de usuario) creados en el entorno de publicación no son necesarios en el entorno de creación.

La mayoría de los datos de usuario creados en el entorno de creación están pensados para permanecer en el entorno de creación y no para copiarlos en instancias de publicación.

El registro y las modificaciones realizadas en una instancia de publicación deben sincronizarse con otras instancias de publicación para que tengan acceso a los mismos datos de usuario.

A partir de AEM 6.1, cuando la sincronización de usuarios está habilitada, los datos de usuario se sincronizan automáticamente en las instancias de publicación del conjunto de servidores y no se crean en el autor.

## Distribución de Sling {#sling-distribution}

Los datos del usuario, junto con sus [ACL](/help/sites-administering/security.md), se almacenan en el [Oak Core](/help/sites-deploying/platform.md), la capa debajo de Oak JCR, y se accede a ellos mediante la API [de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html)Oak. Con actualizaciones poco frecuentes, es razonable que los datos de usuario se sincronicen con otras instancias de publicación mediante [Sling Content Distribution](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md) (distribución de Sling).

Los beneficios de la sincronización de usuarios mediante la distribución Sling, en comparación con la replicación tradicional, son:

* *los usuarios*, perfiles *de* usuario y grupos *de* usuarios creados al publicar no se crean en el autor

* La distribución Sling establece propiedades en eventos jcr, lo que permite actuar dentro de los oyentes de eventos de publicación sin preocuparse por los bucles de replicación infinitos
* La distribución de Sling sólo envía datos de usuario a instancias de publicación no originales, eliminando así el tráfico innecesario
* [Las ACL](/help/sites-administering/security.md) establecidas en el nodo de usuario se incluyen en la sincronización

>[!NOTE]
>
>Si se requieren sesiones, se recomienda usar una solución SSO o una sesión adhesiva y hacer que los clientes inicien sesión si se cambian a otro editor.

>[!CAUTION]
>
>No se admite la sincronización del grupo de ***administradores*** , aunque la sincronización de usuarios esté activada. En su lugar, se registrará un error al &#39;importar la diferencia&#39; en el registro de errores.
>
>Por lo tanto, cuando la implementación es un conjunto de servidores de publicación, si se agrega o elimina un usuario del grupo ***administradores** , la modificación debe realizarse manualmente en cada instancia de publicación.

## Activar sincronización de usuario {#enable-user-sync}

>[!NOTE]
>
>De forma predeterminada, la sincronización de usuarios es `disabled`.
>
>Habilitar la sincronización de usuarios implica modificar las configuraciones de OSGi *existentes* .
>
>No se deben agregar nuevas configuraciones como resultado de habilitar la sincronización de usuarios.

La sincronización de usuarios depende del entorno de creación para administrar las distribuciones de datos de usuario, aunque los datos de usuario no se hayan creado en el autor. Gran parte de la configuración, pero no toda, se lleva a cabo en el entorno de creación y cada paso identifica claramente si se va a realizar durante la creación o publicación.

A continuación se indican los pasos necesarios para habilitar la sincronización de usuarios, seguidos de una sección de [resolución de problemas](#troubleshooting) :

### Requisitos previos {#prerequisites}

1. Si ya se han creado usuarios y grupos de usuarios en un editor, se recomienda sincronizar [](#manually-syncing-users-and-user-groups) manualmente los datos de usuario con todos los editores antes de configurar y habilitar la sincronización de usuarios.

Una vez habilitada la sincronización de usuarios, solo se sincronizan los usuarios y grupos recién creados.

1. Asegúrese de que se ha instalado el código más reciente:

* [Actualizaciones de la plataforma AEM](https://helpx.adobe.com/experience-manager/kb/aem62-available-hotfixes.html)
* [Actualizaciones de AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

### 1.Agente de distribución Apache Sling: fábrica de agentes de sincronización {#apache-sling-distribution-agent-sync-agents-factory}

**Habilitar sincronización de usuario**

* **en autor**

   * iniciar sesión con privilegios de administrador
   * acceder a la consola [web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * localizar `Apache Sling Distribution Agent - Sync Agents Factory`

      * seleccione la configuración existente para abrirla y editarla (icono de lápiz)Verificar `name`: **`socialpubsync`**

      * seleccione la `Enabled` casilla de verificación
      * select `Save`


![](assets/chlimage_1-20.png)

### 2. Crear usuario autorizado {#createauthuser}

**Configurar permisos** Este usuario autorizado se utilizará en el paso 3 para configurar la distribución de Sling en el autor.

* **en cada instancia de publicación**

   * iniciar sesión con privilegios de administrador
   * acceder a la consola [de seguridad](/help/sites-administering/security.md)

      * por ejemplo, [https://localhost:4503/useradmin](https://localhost:4503/useradmin)
   * crear un nuevo usuario

      * for example, `usersync-admin`
   * add this user to the **`administrators`** user group
   * [agregar ACL para este usuario a /home](#howtoaddacl)

      * `Allow jcr:all` con restricción `rep:glob=*/activities/*`



>[!CAUTION]
>
>Se debe crear un nuevo usuario.
>
>* El usuario predeterminado asignado es **`admin`**.
>* No use `communities-user-admin user.`
>



#### Cómo agregar ACL {#addacls}

* acceso a CRXDE Lite

   * por ejemplo, [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* seleccionar `/home` nodo
* en el panel derecho, seleccione la `Access Control` ficha
* seleccione el `+` botón para agregar una entrada ACL

   * **Principal**: *buscar usuarios creados para la sincronización de usuarios*
   * **Tipo**: `Allow`
   * **Privilegios**: `jcr:all`
   * **Restricciones** rep:glob: `*/activities/*`
   * seleccionar **Aceptar**

* seleccione **Guardar todo**

![](assets/chlimage_1-21.png)

Consulte también

* [Administración de derechos de acceso](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* Sección Resolución de problemas [Modificar excepción de operación durante el procesamiento](#modify-operation-exception-during-response-processing)de la respuesta.

### 3. Credenciales de transporte de distribución de Apache Sling - Credenciales de usuario basadas en DistributionTransportSecretProvider {#adobegraniteencpasswrd}

**Configurar permisos**

Una vez que se ha creado un usuario autorizado, un miembro del grupo de usuarios **`administrators`***, en todas las instancias de publicación, ese usuario autorizado debe ser identificado por el autor como que tiene permiso para sincronizar datos de usuario del autor para publicar.

* **en autor**

   * iniciar sesión con privilegios de administrador
   * acceder a la consola [web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * localizar `Apache Sling Distribution Transport Credentials - User Credentials based DistributionTransportSecretProvider`
   * seleccione la configuración existente para abrirla y editarla (icono de lápiz)Verificar `property name`: **`socialpubsync-publishUser`**

   * establezca el nombre de usuario y la contraseña para el usuario [](#createauthorizeduser) autorizado creado al publicar en el paso 2

      * for example, `usersync-admin`


![](assets/chlimage_1-22.png)

### 4.Agente de distribución Apache Sling: fábrica de agentes de cola {#apache-sling-distribution-agent-queue-agents-factory}

**Habilitar sincronización de usuario**

* **al publicar**:

   * iniciar sesión con privilegios de administrador
   * acceder a la consola [web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * localizar `Apache Sling Distribution Agent - Queue Agents Factory`

      * seleccione la configuración existente para abrirla y editarla (icono de lápiz)Verificar `Name`: `socialpubsync-reverse`

      * seleccione la `Enabled` casilla de verificación
      * select `Save`
   * **repetir **para cada instancia de publicación



![](assets/chlimage_1-23.png)

### 5. Adobe Social Sync - Fábrica de observación de diferencias {#diffobserver}

**Habilitar sincronización de grupos**

* **en cada instancia** de publicación:

   * iniciar sesión con privilegios de administrador
   * acceder a la consola [web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * localizar **`Adobe Social Sync - Diff Observer Factory`**

      * seleccione la configuración existente para abrirla y editarla (icono de lápiz)

         Verificar `agent name`: `socialpubsync-reverse`

      * seleccione la `Enabled` casilla de verificación
      * select `Save`


![](assets/screen-shot_2019-05-24at090809.png)

### 6.Activador de distribución de Apache Sling: fábrica de activadores programados {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**(Opcional) modificar el intervalo de sondeo**

De forma predeterminada, el autor sondeará los cambios cada 30 segundos. Para modificar este intervalo:

* **en autor**

   * iniciar sesión con privilegios de administrador
   * acceder a la consola [web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * localizar `Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * seleccione la configuración existente para abrirla y editarla (icono de lápiz)

         * Verificar `Name`: `socialpubsync-scheduled-trigger`
      * establezca el intervalo `Interval in Seconds` en el intervalo deseado
      * select `Save`



![](assets/chlimage_1-24.png)

## Configurar para varias instancias de publicación {#configure-for-multiple-publish-instances}

La configuración predeterminada es para una sola instancia de publicación. Dado que el motivo para habilitar la sincronización de usuarios es sincronizar varias instancias de publicación, como en un conjunto de publicaciones, las instancias de publicación adicionales deberán agregarse a la fábrica de agentes de sincronización.

### 7.Agente de distribución Apache Sling: fábrica de agentes de sincronización {#apache-sling-distribution-agent-sync-agents-factory-1}

**Agregar instancias de publicación:**

* **en autor**

   * iniciar sesión con privilegios de administrador
   * acceder a la consola [web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * localizar `Apache Sling Distribution Agent - Sync Agents Factory`

      * seleccione la configuración existente para abrirla y editarla (icono de lápiz)Verificar `Name`: `socialpubsync`


![](assets/chlimage_1-25.png)

* **Extremos** del exportador Debe haber un extremo del exportador para cada publicador. Por ejemplo, si hay dos editores, localhost:4503 y 4504, debe haber dos entradas:

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **Extremos** del importador Debe haber un extremo del importador para cada publicador. Por ejemplo, si hay dos editores, localhost:4503 y 4504, debe haber dos entradas:

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* select `Save`

### 8.Escucha de sincronización de usuarios de AEM Communities {#aem-communities-user-sync-listener}

**(Opcional) Sincronizar nodos JCR adicionales**

Si hay datos personalizados que desea sincronizar en varias instancias de publicación, entonces:

* **en cada instancia** de publicación:

   * iniciar sesión con privilegios de administrador
   * acceder a la consola [web](/help/sites-deploying/configuring-osgi.md)

      * for example, `https://localhost:4503/system/console/configMgr`
   * localizar `AEM Communities User Sync Listener`
   * seleccione la configuración existente para abrirla y editarla (icono de lápiz)Verificar `Name`: `socialpubsync-scheduled-trigger`


![](assets/chlimage_1-26.png)

* **Tipos**de nodosEsta es la lista de tipos de nodos que se sincronizarán. Cualquier tipo de nodo que no sea sling:Folder debe aparecer aquí (sling:folder se gestiona por separado).
Lista predeterminada de tipos de nodo que sincronizar:

   * rep:Usuario
   * nt:unstructured
   * nt:resource

* **Propiedades**ignorables Es la lista de propiedades que se omitirán si se detecta algún cambio. Los cambios realizados en estas propiedades pueden sincronizarse como un efecto secundario de otros cambios (ya que la sincronización siempre se encuentra en el nivel de nodo), pero los cambios realizados en estas propiedades no activarán la sincronización por sí mismos.
Propiedad predeterminada que se debe ignorar:

   * cq:lastModified

* **Subrutas de nodos**ignorables que se omitirán por completo durante la sincronización. No se sincronizará nada debajo de estas subrutas en cualquier momento.
Nodos predeterminados que se deben ignorar:

   * .tokens
   * sistema

* **Carpetas**distribuidas La mayoría de sling:Folders se ignoran porque no es necesaria la sincronización. Las pocas excepciones se enumeran aquí.
Carpetas predeterminadas para sincronizar

   * segmentos/puntuación
   * social/relaciones
   * actividades

### 9.ID de Sling único {#unique-sling-id}

>[!CAUTION]
>
>Si el ID de Sling coincide entre dos o más instancias de publicación, la sincronización de grupos de usuarios fallará.

Si el ID de Sling es el mismo para varias instancias de publicación en un conjunto de servidores de publicación, los grupos de usuarios no se sincronizarán.

Para validar que todos los valores de ID de Sling difieran, en cada instancia de publicación:

1. vaya a [https://*host:port*/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings)
1. comprobar el valor de **Sling ID**

![](assets/chlimage_1-27.png)

Si el ID de Sling de una instancia de publicación coincide con el ID de Sling de cualquier otra instancia de publicación, entonces:

1. detenga una de las instancias de publicación que tenga un ID de Sling coincidente
1. en el directorio crx-quickstart/launchpad/felix

   * buscar y eliminar el archivo denominado *sling.id.file*

      * por ejemplo, en un sistema Linux:
         `rm -i $(find . -type f -name sling.id.file)`

      * por ejemplo, en un sistema Windows:
         `use windows explorer and search for *sling.id.file*`

1. iniciar la instancia de publicación

   * al iniciar, se le asignará un nuevo ID de Sling

1. validar que el ID **de** Sling ahora sea único

Repita estos pasos hasta que todas las instancias de publicación tengan un ID de Sling único.

## Fábrica del generador de paquetes de almacén {#vault-package-builder-factory}

Para que las actualizaciones se sincronizen correctamente, es necesario modificar el creador de paquetes vault para la sincronización del usuario:

* en cada instancia de publicación de AEM
* acceder a la consola [web](/help/sites-deploying/configuring-osgi.md)

   * por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* ubique la variable `Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* seleccione el icono de edición
* agregar dos `Package Node Filters`:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* administración de políticas:

   * para sobrescribir nodos rep:policy existentes con otros nuevos, agregue un tercer filtro de paquete:

      * `/home/users|+.*/rep:policy`
   * para evitar que las políticas se distribuyan, establezca

      * `Acl Handling:` `IGNORE`


![Fábrica del generador de paquetes de almacén](assets/vault-package-builder-factory.png)

## Qué sucede cuando... {#what-happens-when}

### El usuario se registra automáticamente o edita el perfil al publicar {#user-self-registers-or-edits-profile-on-publish}

Por diseño, los usuarios y perfiles creados en el entorno de publicación (autorregistro) no aparecen en el entorno de creación.

Cuando la topología es un conjunto de servidores [de](/help/sites-deploying/recommended-deploys.md#tarmk-farm) publicación y la sincronización de usuarios se ha configurado correctamente, el *usuario *y el perfil *de* usuario se sincronizan en el conjunto de servidores de publicación mediante la distribución Sling.

### Los usuarios o grupos de usuarios se crean con la consola de seguridad {#users-or-user-groups-are-created-using-security-console}

Por diseño, los datos de usuario creados en el entorno de publicación no aparecen en el entorno de creación y viceversa.

Cuando se utiliza la consola Administración de [usuarios y seguridad](/help/sites-administering/security.md) para agregar usuarios nuevos en el entorno de publicación, la sincronización de usuarios sincronizará los usuarios nuevos y su pertenencia a grupos con otras instancias de publicación, si es necesario. La sincronización de usuarios también sincronizará los grupos de usuarios creados mediante la consola de seguridad.

## Solución de problemas {#troubleshooting}

### Cómo desconectar la sincronización de usuarios {#how-to-take-user-sync-offline}

Para desactivar la sincronización de usuarios, para [eliminar un publicador](#how-to-remove-a-publisher) o sincronizar datos [](#manually-syncing-users-and-user-groups)manualmente, la cola de distribución debe estar vacía y silenciosa.

Para comprobar el estado de la cola de distribución:

* sobre el autor:

   * uso de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * buscar entradas en `/var/sling/distribution/packages`

         * nodos de carpeta con el patrón `distrpackage_*`
   * uso del Administrador [de paquetes](/help/sites-administering/package-manager.md)

      * buscar paquetes pendientes (aún no instalados)

         * con el nombre del patrón `socialpubsync-vlt*`
         * created by `communities-user-admin`


Cuando la cola de distribución esté vacía, deshabilite la sincronización de usuarios:

* en autor

   * *desmarcar *la `Enabled` casilla de verificación para Agente de distribución Sling de [Apache - Fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory)

Una vez completadas las tareas, para volver a habilitar la sincronización de usuarios:

* en autor

   * marque la `Enabled` casilla de verificación de Agente de distribución Sling de [Apache - Fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory)

### Diagnóstico de sincronización de usuario {#user-sync-diagnostics}

Diagnósticos de sincronización de usuarios es una herramienta que comprueba la configuración e intenta identificar cualquier problema.

En el autor, simplemente desplácese desde la consola principal a través de **Herramientas, Operaciones, Diagnóstico de sincronización de usuarios.**

Al entrar en la consola Diagnósticos de sincronización de usuarios se mostrarán los resultados.

Esto es lo que se muestra cuando la sincronización de usuarios no se ha activado:

![](assets/chlimage_1-28.png)

#### Cómo ejecutar diagnósticos para editores {#how-to-run-diagnostics-for-publishers}

Cuando el diagnóstico se ejecuta desde el entorno de creación, los resultados de aprobado/suspenso incluirán una sección [INFO] con la lista de instancias de publicación configuradas para su confirmación.

En la lista se incluye una URL para cada instancia de publicación que ejecutará los diagnósticos para esa instancia. El parámetro url `syncUser` se anexa a la dirección URL de diagnóstico con su valor establecido en el usuario *de sincronización* autorizado creado en el [paso 2](/help/sites-administering/sync.md#2createauthorizeduser).

**Nota**: antes de iniciar la URL, el usuario *de sincronización* autorizado ya debe haber iniciado sesión en esa instancia de publicación.

![](assets/chlimage_1-29.png)

### Configuración agregada incorrectamente {#configuration-improperly-added}

Cuando la sincronización de usuarios no funciona, el problema más común es que se *agregaron* configuraciones adicionales. En su lugar, la *configuración predeterminada existente debería haberse *editado*.

A continuación se muestran las vistas de cómo deben aparecer las configuraciones predeterminadas editadas en la consola web. Si aparece más de una instancia, se debe eliminar la configuración agregada.

#### (autor) Un agente de distribución Apache Sling: fábrica de agentes de sincronización {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![](assets/chlimage_1-30.png)

#### (autor) Un Apache Sling Distribution Transport Credentials - User Credentials based DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![](assets/chlimage_1-31.png)

#### (publicar) Un agente de distribución Apache Sling: fábrica de agentes de cola {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![](assets/chlimage_1-32.png)

#### (publicar) Una sincronización de Adobe Social: Fábrica de observadores de diferencias {#publish-one-adobe-social-sync-diff-observer-factory}

![](assets/chlimage_1-33.png)

#### (autor) Un activador de distribución Apache Sling: fábrica de activadores programados {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![](assets/chlimage_1-34.png)

### Modificar excepción de operación durante el procesamiento de respuesta {#modify-operation-exception-during-response-processing}

Si en el registro está visible lo siguiente:

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

A continuación, compruebe que la sección [2. Crear usuario]autorizado(/content/docs/en/aem/6-1/administer/security/security/sync.md#2. crear usuario autorizado) se siguió correctamente.

En esta sección se describe la creación de un usuario autorizado, que existe en todas las instancias de publicación, y su identificación en la configuración OSGi de &#39;Proveedor secreto&#39; del autor. By default, the user is `admin`.

El usuario autorizado debe ser miembro del grupo de usuarios y no se deben modificar los permisos para ese grupo **`administrators`** .

El usuario autorizado debe tener explícitamente los siguientes privilegios y restricciones en todas las instancias de publicación:

| **path** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | */actividades/* |
| /home/users | X | */actividades/* |
| /home/groups | X | */actividades/* |

Como miembro del `administrators` grupo, el usuario autorizado debe tener los siguientes privilegios en todas las instancias de publicación:

| **path** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### Error al sincronizar el grupo de usuarios {#user-group-sync-failed}

Si el ID de Sling coincide entre dos o más instancias de publicación, la sincronización de grupos de usuarios fallará.

Véase la sección [9. ID de Sling único](#unique-sling-id)

### Sincronización manual de usuarios y grupos de usuarios {#manually-syncing-users-and-user-groups}

* en el editor en el que existen usuarios y grupos de usuarios:

   * [si está habilitado, deshabilitar la sincronización de usuarios](#how-to-take-user-sync-offline)
   * [crear un paquete](/help/sites-administering/package-manager.md#creating-a-new-package) de `/home`

      * al editar el paquete

         * Ficha Filtros: Agregar filtro: Ruta raíz: `/home`
         * Ficha Avanzado: Administración de CA: `Overwrite`
   * [exportar el paquete](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)


* en otras instancias de publicación:

   * [importar el paquete](/help/sites-administering/package-manager.md#installing-packages)

Para configurar o habilitar la sincronización de usuarios, vaya al paso 1: Agente de distribución [Apache Sling: fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory)

### Cuando un publicador deja de estar disponible {#when-a-publisher-becomes-unavailable}

Cuando una instancia de publicación deja de estar disponible, no debe eliminarse si volverá a estar en línea en el futuro. Los cambios se pondrán en cola para el editor y, una vez que vuelvan a estar en línea, se procesarán.

Si la instancia de publicación nunca volverá a estar en línea, si está sin conexión de forma permanente, debe eliminarse porque la compilación de colas dará como resultado un uso notorio de espacio en disco en el entorno de creación.

Cuando un editor está inactivo, el registro de autor tendrá excepciones similares a:

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### Cómo eliminar un publicador {#how-to-remove-a-publisher}

Para eliminar un publicador de [Apache Sling Distribution Agent - Sync Agent Factory](#apache-sling-distribution-agent-sync-agents-factory), la cola de distribución debe estar vacía y en silencio.

* sobre el autor:

   * [Desconectar sincronización de usuarios](#how-to-take-user-sync-offline)
   * siga el [paso 7](#apache-sling-distribution-agent-sync-agents-factory) para eliminar el editor de ambas listas de servidores:

      * `Exporter Endpoints`
      * `Importer Endpoints`
   * volver a habilitar la sincronización de usuarios

      * marque la `Enabled` casilla de verificación de Agente de distribución Sling de [Apache - Fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory)
