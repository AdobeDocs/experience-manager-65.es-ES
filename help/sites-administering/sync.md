---
title: Sincronización de usuarios
seo-title: User Synchronization
description: AEM Obtenga información acerca de la sincronización de usuarios en.
seo-description: Learn about user synchronization in AEM.
uuid: 0a519daf-21b7-4adc-b419-eeb8c404c54f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: c061b358-8c0d-40d3-8090-dc9800309ab3
docset: aem65
exl-id: 89f55598-e749-42b8-8f2a-496f45face66
feature: Security
source-git-commit: f0acb130e1c68b927356c4e0ea625bbd88a6fc19
workflow-type: tm+mt
source-wordcount: '2527'
ht-degree: 5%

---


# Sincronización de usuarios{#user-synchronization}

## Introducción {#introduction}

Cuando la implementación es una [publicar conjunto de servidores](/help/sites-deploying/recommended-deploys.md#tarmk-farm), los miembros deben poder iniciar sesión y ver sus datos en cualquier nodo de publicación.

Los usuarios y grupos de usuarios (datos de usuario) creados en el entorno de publicación no son necesarios en el entorno de creación.

La mayoría de los datos de usuario creados en el entorno de autor están pensados para permanecer en el entorno de autor y no para copiarse en instancias de publicación.

El registro y las modificaciones realizadas en una instancia de publicación deben sincronizarse con otras instancias de publicación para que tengan acceso a los mismos datos de usuario.

AEM A partir de la versión 6.1, cuando la sincronización de usuarios está habilitada, los datos de usuario se sincronizan automáticamente en las instancias de publicación de la granja y no se crean en el autor.

## Distribución de Sling {#sling-distribution}

Los datos de usuario, junto con sus [ACL](/help/sites-administering/security.md), se almacenan en [Oak Core](/help/sites-deploying/platform.md), la capa debajo de Oak JCR y se accede a ellas mediante la variable [API de Oak](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html). Con actualizaciones poco frecuentes, es razonable sincronizar los datos de usuario con otras instancias de publicación mediante [Sling Content Distribution](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md) (Distribución de Sling).

Las ventajas de la sincronización de usuarios mediante la distribución Sling en comparación con la replicación tradicional son las siguientes:

* *usuarios*, *perfiles de usuario* y *grupos de usuarios* Las páginas creadas en la publicación no se crean en el autor

* La distribución de Sling establece propiedades en eventos jcr, lo que permite actuar dentro de detectores de eventos de publicación sin preocuparse por los bucles de replicación infinitos
* La distribución de Sling solo envía datos de usuario a instancias de publicación no originarias, lo que elimina el tráfico innecesario
* [ACL](/help/sites-administering/security.md) Los conjuntos de en el nodo de usuario se incluyen en la sincronización

>[!NOTE]
>
>Si son necesarias sesiones, se recomienda utilizar una solución SSO o una sesión fija y hacer que los clientes inicien sesión si se les cambia a otra instancia de publicación.

>[!CAUTION]
>
>Sincronización del **administradores** no se admite el grupo, incluso cuando la sincronización de usuarios está habilitada. En su lugar, se registrará un error al &quot;importar la comparación de diferencias&quot; en el registro de errores.
>
>Por lo tanto, cuando la implementación es un conjunto de servidores de publicación, si se agrega o se quita un usuario del **administradores** , la modificación debe realizarse manualmente en cada instancia de publicación.

## Activar sincronización de usuarios {#enable-user-sync}

>[!NOTE]
>
>De forma predeterminada, la sincronización de usuarios es `disabled`.
>
>Habilitar la sincronización de usuarios implica modificar *existente* Configuraciones de OSGi.
>
>No se deben agregar nuevas configuraciones como resultado de habilitar la sincronización del usuario.

La sincronización de usuarios se basa en el entorno de creación para administrar las distribuciones de datos de usuario, aunque los datos de usuario no se creen en el autor. Gran parte de la configuración, pero no toda, tiene lugar en el entorno de creación y cada paso identifica claramente si se va a realizar en el entorno de creación o publicación.

A continuación se indican los pasos necesarios para habilitar la sincronización de usuarios, seguidos de un [Solución de problemas](#troubleshooting) sección:

### Requisitos previos {#prerequisites}

1. Si ya se han creado usuarios y grupos de usuarios en una instancia de publicación, se recomienda [sincronización manual](#manually-syncing-users-and-user-groups) transfiera los datos de usuario a todas las instancias de publicación antes de configurar y habilitar la sincronización de usuarios.

Una vez habilitada la sincronización de usuarios, solo se sincronizan los usuarios y grupos recién creados.

1. Asegúrese de que se ha instalado el código más reciente:

* [AEM Actualizaciones de plataforma de](https://helpx.adobe.com/es/experience-manager/kb/aem62-available-hotfixes.html)
* [Actualizaciones de AEM Communities](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Agente de distribución de Apache Sling: fábrica de agentes de sincronización {#apache-sling-distribution-agent-sync-agents-factory}

**Habilitar sincronización de usuarios**

* **sobre el autor**

   * iniciar sesión con privilegios de administrador
   * acceda al [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * localizar `Apache Sling Distribution Agent - Sync Agents Factory`

      * seleccionar la configuración existente para abrirla y editarla (icono de lápiz) Verificar `name`: **`socialpubsync`**

      * seleccione el `Enabled` casilla de verificación
      * select `Save`

![Agente de distribución de Apache Sling](assets/chlimage_1-20.png)

### 2. Crear usuario autorizado {#createauthuser}

**Configuración de permisos**
Este usuario autorizado se utilizará en el paso 3 para configurar la distribución de Sling en el autor.

* **en cada instancia de publicación**

   * iniciar sesión con privilegios de administrador
   * acceda al [Consola de seguridad](/help/sites-administering/security.md)

      * por ejemplo, [https://localhost:4503/useradmin](https://localhost:4503/useradmin)

   * crear un nuevo usuario

      * por ejemplo, `usersync-admin`

   * agregar este usuario a **`administrators`** grupo de usuarios
   * [agregar ACL para este usuario a /home](#howtoaddacl)

      * `Allow jcr:all` con restricción `rep:glob=*/activities/*`

>[!CAUTION]
>
>Se debe crear un nuevo usuario.
>
>* El usuario predeterminado asignado es **`admin`**.
>* No use `communities-user-admin user.`
>

#### Cómo añadir ACL {#addacls}

* CRXDE Lite de acceso

   * por ejemplo, [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* select `/home` nodo
* en el panel derecho, seleccione `Access Control` pestaña
* seleccione el `+` para agregar una entrada ACL

   * **Principal**: *buscar usuario creado para sincronización de usuarios*
   * **Tipo**: `Allow`
   * **Privilegios**: `jcr:all`
   * **Restricciones** representante:glob: `*/activities/*`
   * select **OK**

* select **Guardar todo**

![Agregar ventana ACL](assets/chlimage_1-21.png)

Consulte también

* [Administración de derechos de acceso](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* Sección Resolución de problemas [Modificar Excepción De Operación Durante El Procesamiento De Respuesta](#modify-operation-exception-during-response-processing).

### 3. Adobe Granite Distribution - Proveedor secreto de transporte con contraseña cifrada {#adobegraniteencpasswrd}

**Configuración de permisos**

Una vez que es un usuario autorizado, es miembro de **`administrators`** El grupo de usuarios, que se ha creado en todas las instancias de publicación, debe identificarse en el autor como un usuario autorizado con permiso para sincronizar los datos de usuario del autor a la publicación.

* **sobre el autor**

   * iniciar sesión con privilegios de administrador
   * acceda al [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * localizar `com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name`
   * seleccionar la configuración existente para abrirla y editarla (icono de lápiz) Verificar `property name`: **`socialpubsync-publishUser`**

   * establezca el nombre de usuario y la contraseña en [usuario autorizado](#createauthuser) creado al publicar en el paso 2

      * por ejemplo, `usersync-admin`

![Proveedor secreto de transporte de contraseña cifrada](assets/chlimage_1-22.png)

### 4. Agente de distribución de Apache Sling: fábrica de agentes de cola {#apache-sling-distribution-agent-queue-agents-factory}

**Habilitar sincronización de usuarios**

* **en cada instancia de publicación**:

   * iniciar sesión con privilegios de administrador
   * acceda al [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * localizar `Apache Sling Distribution Agent - Queue Agents Factory`

      * seleccionar la configuración existente para abrirla y editarla (icono de lápiz) Verificar `Name`: `socialpubsync-reverse`

      * seleccione el `Enabled` casilla de verificación
      * select `Save`

   * **repetir** para cada instancia de publicación

![Fábrica de agentes de cola](assets/chlimage_1-23.png)

### 5. Adobe Social Sync - Diff Observer Factory {#diffobserver}

**Habilitar sincronización de grupos**

* **en cada instancia de publicación**:

   * iniciar sesión con privilegios de administrador
   * acceda al [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * localizar **`Adobe Social Sync - Diff Observer Factory`**

      * seleccionar la configuración existente para abrirla y editarla (icono de lápiz)

        Verificar `agent name`: `socialpubsync-reverse`

      * seleccione el `Enabled` casilla de verificación
      * select `Save`

![Diff Observer Factory](assets/screen-shot_2019-05-24at090809.png)

### 6. Déclencheur de distribución de Apache Sling: fábrica de Déclencheur programados {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**(Opcional) modificar intervalo de sondeo**

De forma predeterminada, el autor sondeará los cambios cada 30 segundos. Para modificar este intervalo:

* **sobre el autor**

   * iniciar sesión con privilegios de administrador
   * acceda al [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * localizar `Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * seleccionar la configuración existente para abrirla y editarla (icono de lápiz)

         * Verificar `Name`: `socialpubsync-scheduled-trigger`

      * configure el `Interval in Seconds` hasta el intervalo deseado
      * select `Save`

![Déclencheur programados de fábrica](assets/chlimage_1-24.png)

## Configurar para varias instancias de publicación {#configure-for-multiple-publish-instances}

La configuración predeterminada es para una sola instancia de publicación. Dado que el motivo para habilitar la sincronización de usuarios es sincronizar varias instancias de publicación, como para un conjunto de servidores de publicación, las instancias de publicación adicionales deberán agregarse a la fábrica de agentes de sincronización.

### 7. Agente de distribución de Apache Sling: fábrica de agentes de sincronización {#apache-sling-distribution-agent-sync-agents-factory-1}

**Añadir instancias de publicación:**

* **sobre el autor**

   * iniciar sesión con privilegios de administrador
   * acceda al [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * localizar `Apache Sling Distribution Agent - Sync Agents Factory`

      * seleccionar la configuración existente para abrirla y editarla (icono de lápiz) Verificar `Name`: `socialpubsync`

![Fábrica de agentes de sincronización](assets/chlimage_1-25.png)

* **Extremos del exportador**
Debe haber un extremo de exportador para cada instancia de publicación. Por ejemplo, si hay 2 instancias de publicación, localhost:4503 y 4504, debe haber 2 entradas:

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **Extremos del importador**
Debe haber un extremo de importador para cada instancia de publicación. Por ejemplo, si hay 2 instancias de publicación, localhost:4503 y 4504, debe haber 2 entradas:

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* select `Save`

### 8. Receptor de sincronización de usuarios de AEM Communities {#aem-communities-user-sync-listener}

**(Opcional) Sincronizar nodos JCR adicionales**

Si hay datos personalizados que desea sincronizar en varias instancias de publicación, haga lo siguiente:

* **en cada instancia de publicación**:

   * iniciar sesión con privilegios de administrador
   * acceda al [Consola web](/help/sites-deploying/configuring-osgi.md)

      * por ejemplo, `https://localhost:4503/system/console/configMgr`

   * localizar `AEM Communities User Sync Listener`
   * seleccionar la configuración existente para abrirla y editarla (icono de lápiz) Verificar `Name`: `socialpubsync-scheduled-trigger`

![Receptor de sincronización de usuarios de AEM Communities](assets/chlimage_1-26.png)

* **Tipos de nodo**
Esta es la lista de tipos de nodos que se sincronizarán. Cualquier tipo de nodo que no sea sling:Folder debe enumerarse aquí (sling:folder se administra por separado).
Lista predeterminada de tipos de nodos para sincronizar:

   * rep:Usuario
   * nt:unstructured
   * nt:resource

* **Propiedades ignorables**
Esta es la lista de propiedades que se ignorarán si se detecta algún cambio. Los cambios en estas propiedades pueden sincronizarse como efecto secundario de otros cambios (ya que la sincronización siempre se realiza en el nivel de nodo), pero los cambios en estas propiedades no almacenarán en déclencheur la sincronización por sí solos.
Propiedad predeterminada para omitir:

   * cq:lastModified

* **Nodos ignorables**
Subrutas que se ignorarán por completo durante la sincronización. No se sincronizará nada debajo de estas subrutas en ningún momento.
Nodos predeterminados para omitir:

   * .tokens
   * system

* **Carpetas distribuidas**
La mayoría de sling:Folders se omiten porque la sincronización no es necesaria. Las pocas excepciones se enumeran aquí.
Carpetas predeterminadas para sincronizar

   * segmentos/puntuación
   * social/relaciones
   * actividades

### 9. ID único de Sling {#unique-sling-id}

>[!CAUTION]
>
>Si el ID de Sling coincide entre dos o más instancias de publicación, la sincronización de grupos de usuarios fallará.

Si el ID de Sling es el mismo para varias instancias de publicación en un conjunto de servidores de publicación, los grupos de usuarios no se sincronizarán.

Para validar que todos los valores de ID de Sling son diferentes, en cada instancia de publicación:

1. examinar a `http://<host>:<port>/system/console/status-slingsettings`
1. compruebe el valor de **ID de Sling**

![Comprobación del valor del ID de Sling](assets/chlimage_1-27.png)

Si el ID de Sling de una instancia de publicación coincide con el ID de Sling de cualquier otra instancia de publicación, haga lo siguiente:

1. detenga una de las instancias de publicación que tenga un ID de Sling coincidente
1. en el directorio crx-quickstart/launchpad/felix

   * busque y elimine el archivo llamado *sling.id.file*

      * por ejemplo, en un sistema Linux:
        `rm -i $(find . -type f -name sling.id.file)`

      * por ejemplo, en un sistema Windows:
        `use windows explorer and search for *sling.id.file*`

1. inicio de la instancia de publicación

   * al inicio se le asignará un nuevo ID de Sling

1. validar que la variable **ID de Sling** es ahora único

Repita estos pasos hasta que todas las instancias de publicación tengan un ID de Sling único.

## Generador de paquetes Vault Factory {#vault-package-builder-factory}

Para que las actualizaciones se sincronicen correctamente, es necesario modificar el generador de paquetes Vault para la sincronización de usuarios:

* AEM en cada instancia de publicación de la
* acceda al [Consola web](/help/sites-deploying/configuring-osgi.md)

   * por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* busque el `Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* seleccione el icono de edición
* añadir dos `Package Node Filters`:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* administración de directivas:

   * para sobrescribir los nodos rep:policy existentes con otros nuevos, agregue un tercer filtro de paquetes:

      * `/home/users|+.*/rep:policy`

   * para evitar que se distribuyan directivas, establezca

      * `Acl Handling:` `IGNORE`

![Generador de paquetes Vault Factory](assets/vault-package-builder-factory.png)

## ¿Qué sucede cuando...? {#what-happens-when}

### El usuario se registra automáticamente o edita el perfil al publicar {#user-self-registers-or-edits-profile-on-publish}

Por diseño, los usuarios y perfiles creados en el entorno de publicación (registro automático) no aparecen en el entorno de creación.

Cuando la topología es un [publicar conjunto de servidores](/help/sites-deploying/recommended-deploys.md#tarmk-farm) y la sincronización del usuario se ha configurado correctamente, el *usuario* y *perfil de usuario* se sincroniza en el conjunto de servidores de publicación mediante la distribución Sling.

### Los usuarios o grupos de usuarios se crean mediante la consola de seguridad {#users-or-user-groups-are-created-using-security-console}

Por diseño, los datos de usuario creados en el entorno de publicación no aparecen en el entorno de creación y viceversa.

Si la variable [Administración de usuarios y seguridad](/help/sites-administering/security.md) La consola de se utiliza para agregar nuevos usuarios en el entorno de publicación, la sincronización de usuarios sincronizará a los nuevos usuarios y su pertenencia a grupos con otras instancias de publicación, si es necesario. La sincronización de usuarios también sincronizará los grupos de usuarios creados mediante la consola de seguridad.

## Solución de problemas {#troubleshooting}

### Cómo quitar la sincronización de usuarios sin conexión {#how-to-take-user-sync-offline}

Para desconectar la sincronización de usuarios, haga lo siguiente [eliminación de una instancia de publicación](#how-to-remove-a-publish-instance) o [sincronización manual de datos](#manually-syncing-users-and-user-groups), la cola de distribución debe estar vacía y silenciosa.

Para comprobar el estado de la cola de distribución:

* sobre el autor:

   * usando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * buscar entradas en `/var/sling/distribution/packages`

         * nodos de carpeta llamados con el patrón `distrpackage_*`

   * usando [Administrador de paquetes](/help/sites-administering/package-manager.md)

      * buscar paquetes pendientes (aún no instalados)

         * con el nombre del patrón `socialpubsync-vlt*`
         * creado por `communities-user-admin`

Cuando la cola de distribución está vacía, deshabilitar la sincronización de usuarios:

* sobre el autor

   * *desmarque *el `Enabled` casilla para [Agente de distribución de Apache Sling: fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory)

Una vez completadas las tareas, para volver a habilitar la sincronización de usuarios:

* sobre el autor

   * consulte la `Enabled` casilla para [Agente de distribución de Apache Sling: fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory)

### Diagnóstico de sincronización de usuario {#user-sync-diagnostics}

Diagnóstico de sincronización de usuarios es una herramienta que comprueba la configuración e intenta identificar cualquier problema.

En autor, simplemente navegue desde la consola principal a través de **Herramientas, Operaciones, Diagnóstico, Diagnóstico de sincronización de usuarios.**

Al entrar en la consola de diagnóstico de sincronización de usuarios, se mostrarán los resultados.

Esto es lo que se muestra cuando la sincronización de usuarios no se ha habilitado:

![Advertencia de que Diagnóstico de sincronización de usuarios no está habilitado](assets/chlimage_1-28.png)

#### Cómo ejecutar diagnósticos para instancias de publicación {#how-to-run-diagnostics-for-publish-instances}

Cuando el diagnóstico se ejecuta desde el entorno de creación, los resultados de aprobado/suspenso incluirán un [INFORMACIÓN] que muestra la lista de instancias de publicación configuradas para su confirmación.

En la lista se incluye una dirección URL para cada instancia de publicación que ejecutará los diagnósticos para esa instancia. El parámetro de URL `syncUser` se anexa a la dirección URL de diagnóstico con su valor establecido en *usuario de sincronización autorizado* creado en [Paso 2](#createauthuser).

**Nota**: antes de iniciar la URL, el *usuario de sincronización autorizado* ya debe estar conectado a esa instancia de publicación.

![Diagnóstico para instancias de publicación](assets/chlimage_1-29.png)

### Configuración añadida incorrectamente {#configuration-improperly-added}

Cuando la sincronización del usuario no funciona, el problema más común es que se han realizado configuraciones adicionales *añadido*. En su lugar, la configuración predeterminada *existente debería haber sido *editado*.

A continuación, se muestran vistas de cómo deben aparecer las configuraciones predeterminadas editadas en la consola web. Si aparece más de una instancia, la configuración añadida debería eliminarse.

#### (autor) Un agente de distribución de Apache Sling: fábrica de agentes de sincronización {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![Vista de configuraciones predeterminadas editadas en la consola web](assets/chlimage_1-30.png)

#### (autor) Una credenciales de transporte de distribución de Apache Sling: credenciales de usuario basadas en DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![Vista de configuraciones predeterminadas editadas en la consola web](assets/chlimage_1-31.png)

#### (publicar) Un agente de distribución de Apache Sling: fábrica de agentes de cola {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![Vista de configuraciones predeterminadas editadas en la consola web](assets/chlimage_1-32.png)

#### (publicar) One Adobe Social Sync - Diff Observer Factory {#publish-one-adobe-social-sync-diff-observer-factory}

![Vista de configuraciones predeterminadas editadas en la consola web](assets/chlimage_1-33.png)

#### (autor) Un Déclencheur de distribución de Apache Sling: fábrica de Déclencheur programados {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![Vista de configuraciones predeterminadas editadas en la consola web](assets/chlimage_1-34.png)

### Modificar Excepción De Operación Durante El Procesamiento De Respuesta {#modify-operation-exception-during-response-processing}

Si lo siguiente es visible en el registro:

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

A continuación, compruebe que la sección [2. Crear usuario autorizado](#createauthuser) se ha seguido correctamente.

En esta sección se describe la creación de un usuario autorizado, que existe en todas las instancias de publicación, y su identificación en la configuración OSGi del &quot;Proveedor secreto&quot; en Autor. De forma predeterminada, el usuario es `admin`.

El usuario autorizado debe convertirse en miembro de **`administrators`** el grupo de usuarios y los permisos para ese grupo no deben modificarse.

El usuario autorizado debe tener explícitamente los siguientes privilegios y restricciones en todas las instancias de publicación:

| **ruta** | **jcr:todo** | **rep:glob** |
|---|---|---|
| /home | X | &#42;/actividades/&#42; |
| /home/users | X | &#42;/actividades/&#42; |
| /home/groups | X | &#42;/actividades/&#42; |

Como miembro de la `administrators` , el usuario autorizado debe tener los siguientes privilegios en todas las instancias de publicación:

| **ruta** | **jcr:todo** | **jcr:leer** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### Error de sincronización de grupo de usuarios {#user-group-sync-failed}

Si el ID de Sling coincide entre dos o más instancias de publicación, la sincronización de grupos de usuarios fallará.

Consulte la sección [9. ID único de Sling](#unique-sling-id)

### Sincronización manual de usuarios y grupos de usuarios {#manually-syncing-users-and-user-groups}

* en instancias de publicación en las que existen usuarios y grupos de usuarios:

   * [si está activada, deshabilitar la sincronización de usuarios](#how-to-take-user-sync-offline)
   * [creación de un paquete](/help/sites-administering/package-manager.md#creating-a-new-package) de `/home`

      * al editar el paquete

         * Pestaña Filtros: Añadir filtro: Ruta raíz: `/home`
         * Pestaña Avanzadas: Administración de CA: `Overwrite`

   * [exportación del paquete](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)

* en otras instancias de publicación:

   * [importación del paquete](/help/sites-administering/package-manager.md#installing-packages)

Para configurar o habilitar la sincronización de usuarios, vaya al paso 1: [Agente de distribución de Apache Sling: fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory)

### Cuando una instancia de publicación deja de estar disponible {#when-a-publish-instance-becomes-unavailable}

Cuando una instancia de publicación deja de estar disponible, no debe eliminarse si volverá a estar en línea en el futuro. Los cambios se pondrán en cola para la instancia de publicación y, una vez que vuelva a estar en línea, se procesarán los cambios.

Si la instancia de publicación nunca vuelve a estar en línea, si está sin conexión de forma permanente, debe eliminarse porque la acumulación de colas dará como resultado un uso notable del espacio en disco en el entorno de creación.

Cuando una instancia de publicación está desactivada, el registro de autor tendrá excepciones similares a las siguientes:

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### Eliminación de una instancia de publicación {#how-to-remove-a-publish-instance}

Para quitar una instancia de publicación de [Agente de distribución de Apache Sling: fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory), la cola de distribución debe estar vacía y silenciosa.

* sobre el autor:

   * [Desconectar la sincronización de usuarios](#how-to-take-user-sync-offline)
   * seguir [paso 7](#apache-sling-distribution-agent-sync-agents-factory) para eliminar la instancia de publicación de ambas listas de servidores:

      * `Exporter Endpoints`
      * `Importer Endpoints`

   * volver a habilitar la sincronización de usuarios

      * consulte la `Enabled` casilla para [Agente de distribución de Apache Sling: fábrica de agentes de sincronización](#apache-sling-distribution-agent-sync-agents-factory)
