---
title: Uso de cURL con AEM
seo-title: Uso de cURL con AEM
description: Aprenda a utilizar cURL con AEM.
seo-description: Aprenda a utilizar cURL con AEM.
uuid: 771b9acc-ff3a-41c9-9fee-7e5d2183f311
contentOwner: Silviu Raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d4ceb82e-2889-4507-af22-b051af83be38
translation-type: tm+mt
source-git-commit: 7ee76afa11384aedc79b17e823c8dc9594662388

---


# Uso de cURL con AEM{#using-curl-with-aem}

Los administradores generalmente necesitan automatizar o simplificar tareas comunes dentro de cualquier sistema. En AEM, por ejemplo, la administración de usuarios, la instalación de paquetes y la administración de paquetes OSGi son tareas que se deben realizar con frecuencia.

Debido a la naturaleza RESTful del marco de trabajo de Sling en el que se crea AEM, la mayoría de las tareas se pueden reducir a una llamada mediante URL. cURL puede utilizarse para ejecutar estas llamadas mediante URL y puede ser una herramienta útil para los administradores de AEM.

## Qué es cURL {#what-is-curl}

cURL es una herramienta de línea de comandos de código abierto que se utiliza para realizar manipulaciones de URL. Admite una amplia gama de protocolos de Internet, incluidos HTTP, HTTPS, FTP, FTPS, SCP, SFTP, TFTP, LDAP, DAP, DICT, TELNET, FILE, IMAP, POP3, SMTP y RTSP.

cURL es una herramienta bien establecida y ampliamente utilizada para obtener o enviar datos usando la sintaxis de la dirección URL y fue lanzada originalmente en 1997. El nombre cURL originalmente significaba &quot;ver URL&quot;.

Debido a la naturaleza RESTful del marco de trabajo de Sling en el que se crea AEM, la mayoría de las tareas se pueden reducir a una llamada de URL, que se puede ejecutar con cURL. [Las tareas](/help/sites-administering/curl.md#common-content-manipulation-aem-curl-commands) de manipulación de contenido, como activar páginas y comenzar flujos de trabajo, así como las tareas [](/help/sites-administering/curl.md#common-operational-aem-curl-commands) operativas como la administración de paquetes y la administración de usuarios, se pueden automatizar mediante cURL. Además, puede [crear sus propios comandos cURL](/help/sites-administering/curl.md#building-a-curl-ready-aem-command) para la mayoría de las tareas en AEM.

>[!NOTE]
>
>Cualquier comando de AEM ejecutado mediante cURL debe autorizarse como cualquier usuario a AEM. Se respetan todas las ACL y los derechos de acceso al utilizar cURL para ejecutar un comando de AEM.

## Descarga de cURL {#downloading-curl}

cURL es una parte estándar de macOS y algunas distribuciones Linux. Sin embargo, está disponible para la mayoría de los sistemas operativos. Las últimas descargas se encuentran en [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html).

El repositorio de origen de cURL también se encuentra en GitHub.

## Creación de un comando AEM listo para cURL {#building-a-curl-ready-aem-command}

Los comandos cURL se pueden crear para la mayoría de las operaciones en AEM, como activar flujos de trabajo, comprobar configuraciones OSGi, activar comandos JMX, crear agentes de replicación y mucho más.

Para encontrar el comando exacto que necesita para una operación concreta, debe utilizar las herramientas de desarrollador del navegador para capturar la llamada POST al servidor cuando ejecute el comando AEM.

Los pasos siguientes describen cómo hacerlo mediante la creación de una nueva página en el navegador Chrome como ejemplo.

1. Prepare la acción que desee invocar en AEM. En este caso, hemos llegado al final del asistente **Crear página** , pero aún no hemos hecho clic en **Crear**.

   ![chlimage_1-66](assets/chlimage_1-66a.png)

1. Inicie las herramientas del desarrollador y seleccione la ficha **Red** . Haga clic en la opción **Mantener registro** antes de borrar la consola.

   ![chlimage_1-67](assets/chlimage_1-67a.png)

1. Haga clic en **Crear** en el asistente **Crear página** para crear el flujo de trabajo.
1. Haga clic con el botón derecho en la acción POST resultante y seleccione **Copiar** -> **Copiar como cURL**.

   ![chlimage_1-68](assets/chlimage_1-68a.png)

1. Copie el comando cURL en un editor de texto y elimine todos los encabezados del comando, que comienzan por `-H` (resaltados en azul en la imagen siguiente) y agregan el parámetro de autenticación adecuado como, por ejemplo, `-u admin:admin`.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Ejecute el comando cURL a través de la línea de comandos y vea la respuesta.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

## Comandos de AEM cURL operativos comunes {#common-operational-aem-curl-commands}

Esta es una lista de comandos cURL de AEM para tareas administrativas y operativas comunes.

>[!NOTE]
>
>En los siguientes ejemplos se da por supuesto que AEM se está ejecutando `localhost` en el puerto `4502` y utiliza al usuario `admin` con contraseña `admin`. Los marcadores de posición de comandos adicionales se definen entre paréntesis angulares.

### Administración de paquetes {#package-management}

#### Create a Package {#create-a-package}

```shell
curl -u admin:admin -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=create -d packageName=<name> -d groupName=<name>
```

#### Vista previa de un paquete {#preview-a-package}

```shell
curl -u admin:admin -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=preview
```

#### Mostrar contenido del paquete {#list-package-content}

```shell
curl -u admin:admin -X POST http://localhost:4502/crx/packmgr/service/console.html/etc/packages/mycontent.zip?cmd=contents
```

#### Generar un paquete {#build-a-package}

```shell
curl -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=build
```

#### Volver a ajustar un paquete {#rewrap-a-package}

```shell
curl -u admin:admin -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=rewrap
```

#### Cambiar el nombre de un paquete {#rename-a-package}

```shell
curl -u admin:admin -X POST -Fname=<New Name> http://localhost:4502/etc/packages/<Group Name>/<Package Name>.zip/jcr:content/vlt:definition
```

#### Cargar un paquete {#upload-a-package}

```shell
curl -u admin:admin -F cmd=upload -F force=true -F package=@test.zip http://localhost:4502/crx/packmgr/service/.json
```

#### Instalar un paquete {#install-a-package}

```shell
curl -u admin:admin -F cmd=install http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Desinstalar un paquete {#uninstall-a-package}

```shell
curl -u admin:admin -F cmd=uninstall http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Eliminar un paquete {#delete-a-package}

```shell
curl -u admin:admin -F cmd=delete http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Descargar un paquete {#download-a-package}

```shell
curl -u admin:admin http://localhost:4502/etc/packages/my_packages/test.zip
```

### Administración de usuarios {#user-management}

#### Create a New User {#create-a-new-user}

```shell
curl -u admin:admin -FcreateUser= -FauthorizableId=hashim -Frep:password=hashim http://localhost:4502/libs/granite/security/post/authorizables
```

#### Create a New Group {#create-a-new-group}

```shell
curl -u admin:admin -FcreateGroup=group1 -FauthorizableId=testGroup1 http://localhost:4502/libs/granite/security/post/authorizables
```

#### Agregar una propiedad a un usuario existente {#add-a-property-to-an-existing-user}

```shell
curl -u admin:admin -Fprofile/age=25 http://localhost:4502/home/users/h/hashim.rw.html
```

#### Crear un usuario con un perfil {#create-a-user-with-a-profile}

```shell
curl -u admin:admin -FcreateUser=testuser -FauthorizableId=hashimkhan -Frep:password=hashimkhan -Fprofile/gender=male http://localhost:4502/libs/granite/security/post/authorizables
```

#### Crear un nuevo usuario como miembro de un grupo {#create-a-new-user-as-a-member-of-a-group}

```shell
curl -u admin:admin -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fmembership=contributor http://localhost:4502/libs/granite/security/post/authorizables
```

#### Agregar un usuario a un grupo {#add-a-user-to-a-group}

```shell
curl -u admin:admin -FaddMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### Eliminar un usuario de un grupo {#remove-a-user-from-a-group}

```shell
curl -u admin:admin -FremoveMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### Configurar la pertenencia a un grupo de usuarios {#set-a-user-s-group-membership}

```shell
curl -u admin:admin -Fmembership=contributor -Fmembership=testgroup http://localhost:4502/home/users/t/testuser.rw.html
```

#### Eliminar un usuario {#delete-a-user}

```shell
curl -u admin:admin -FdeleteAuthorizable= http://localhost:4502/home/users/t/testuser 
```

#### Eliminar un grupo {#delete-a-group}

```shell
curl -u admin:admin -FdeleteAuthorizable= http://localhost:4502/home/groups/t/testGroup
```

### Copia de seguridad {#backup}

Consulte [Copia de seguridad y restauración](/help/sites-administering/backup-and-restore.md#automating-aem-online-backup) para obtener más información.

### los paquetes {#osgi}

#### Inicio de un paquete {#starting-a-bundle}

```shell
curl -u admin:admin -Faction=start http://localhost:4502/system/console/bundles/<bundle-name>
```

#### Detención de un paquete {#stopping-a-bundle}

```shell
curl -u admin:admin -Faction=stop http://localhost:4502/system/console/bundles/<bundle-name>
```

### Dispatcher {#dispatcher}

#### Invalidar la caché {#invalidate-the-cache}

```shell
curl -H "CQ-Action: Activate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

#### Desalojo de la caché {#evict-the-cache}

```shell
curl -H "CQ-Action: Deactivate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

### Agente de replicación {#replication-agent}

#### Comprobar el estado de un agente {#check-the-status-of-an-agent}

```shell
curl -u admin:admin "http://localhost:4502/etc/replication/agents.author/publish/jcr:conten t.queue.json?agent=publish"
http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.js on?agent=publish
```

#### Eliminar un agente {#delete-an-agent}

```shell
curl -X DELETE http://localhost:4502/etc/replication/agents.author/replication99 -u admin:admin
```

#### Crear un agente {#create-an-agent}

```shell
curl -u admin:admin -F "jcr:primaryType=cq:Page" -F "jcr:content/jcr:title=new-replication" -F "jcr:content/sling:resourceType=/libs/cq/replication/components/agent" -F "jcr:content/template=/libs/cq/replication/templates/agent" -F "jcr:content/transportUri=http://localhost:4503/bin/receive?sling:authRequestLogin=1" -F "jcr:content/transportUser=admin" -F "jcr:content/transportPassword={DES}8aadb625ced91ac483390ebc10640cdf"http://localhost:4502/etc/replication/agents.author/replication99
```

#### Pausar un agente {#pause-an-agent}

```shell
curl -u admin:admin -F "cmd=pause" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.js on
```

#### Borrar una cola de agente {#clear-an-agent-queue}

```shell
curl -u admin:admin -F "cmd=clear" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.js on
```

### Communities {#communities}

#### Asignar y revocar distintivos {#assign-and-revoke-badges}

Consulte Puntuación y distintivos de [comunidades](/help/communities/implementing-scoring.md#assign-and-revoke-badges) para obtener más información.

Consulte [Puntuación y distintivos esenciales](/help/communities/configure-scoring.md#example-setup) para obtener más información.

#### Reindexación del MSRP {#msrp-reindexing}

Consulte [MSRP - Proveedor](/help/communities/msrp.md#running-msrp-reindex-tool-using-curl-command) de recursos de almacenamiento MongoDB para obtener más información.

### Seguridad {#security}

#### Activación y desactivación de CRX DE Lite {#enabling-and-disabling-crx-de-lite}

Consulte [Activación de CRXDE Lite en AEM](/help/sites-administering/enabling-crxde-lite.md) para obtener más información.

### Recolección de papelera del almacén de datos {#data-store-garbage-collection}

Consulte Recopilación [de elementos no utilizados del almacén](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) de datos para obtener más información.

### Integración de Analytics y Target {#analytics-and-target-integration}

Consulte [Opción en Adobe Analytics y Adobe Target](/help/sites-administering/opt-in.md#configuring-the-setup-and-provisioning-via-script) para obtener más información.

### Inicio de sesión único {#single-sign-on}

#### Enviar encabezado de prueba {#send-test-header}

Consulte Inicio de sesión [único](/help/sites-deploying/single-sign-on.md) para obtener más información.

## Comandos cURL de AEM de Manipulación de contenido común {#common-content-manipulation-aem-curl-commands}

Esta es una lista de comandos cURL de AEM para la manipulación de contenido.

>[!NOTE]
>
>En los siguientes ejemplos se da por supuesto que AEM se está ejecutando `localhost` en el puerto `4502` y utiliza al usuario `admin` con contraseña `admin`. Los marcadores de posición de comandos adicionales se definen entre paréntesis angulares.

### Administración de páginas {#page-management}

#### Activación de página {#page-activation}

```shell
curl -u admin:admin -X POST -F path="/content/path/to/page" -F cmd="activate" http://localhost:4502/bin/replicate.json
```

#### Desactivación de página {#page-deactivation}

```shell
curl -u admin:admin -X POST -F path="/content/path/to/page" -F cmd="deactivate" http://localhost:4502/bin/replicate.json
```

#### Activación de árbol {#tree-activation}

```shell
curl -u admin:admin -F cmd=activate -F ignoredeactivated=true -F onlymodified=true -F path=/content/geometrixx http://localhost:4502/etc/replication/treeactivation.html
```

#### Bloquear página {#lock-page}

```shell
curl -u admin:admin -X POST -F cmd="lockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### Desbloquear página {#unlock-page}

```shell
curl -u admin:admin -X POST -F cmd="unlockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### Copiar página {#copy-page}

```shell
curl -u admin:admin -F cmd=copyPage -F destParentPath=/path/to/destination/parent -F srcPath=/path/to/source/location http://localhost:4502/bin/wcmcommand
```

### Flujos de trabajo {#workflows}

Consulte [Interacción con flujos de trabajo mediante programación](/help/sites-developing/workflows-program-interaction.md) para obtener más información.

### Contenido de Sling {#sling-content}

#### Create a Folder {#create-a-folder}

```shell
curl -u admin:admin -F jcr:primaryType=sling:Folder http://localhost:4502/etc/test
```

#### Eliminar un nodo {#delete-a-node}

```shell
curl -u admin:admin -F :operation=delete http://localhost:4502/etc/test/test.properties
```

#### Mover un nodo {#move-a-node}

```shell
curl -u admin:admin -F":operation=move" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### Copiar un nodo {#copy-a-node}

```shell
curl -u admin:admin -F":operation=copy" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### Carga de archivos con Sling PostServlet {#upload-files-using-sling-postservlet}

```shell
curl -u admin:admin -F"*=@test.properties"  http://localhost:4502/etc/test
```

#### Carga de archivos con Sling PostServlet y especificación del nombre del nodo {#upload-files-using-sling-postservlet-and-specifying-node-name}

```shell
curl -u admin:admin -F"test2.properties=@test.properties"  http://localhost:4502/etc/test
```

#### Cargar archivos que especifican un tipo de contenido {#upload-files-specifying-a-content-type}

```shell
curl -u admin:admin -F "*=@test.properties;type=text/plain" http://localhost:4502/etc/test
```

### Manipulación de recursos {#asset-manipulation}

Consulte API [HTTP de](/help/assets/mac-api-assets.md) Assets para obtener más información.
