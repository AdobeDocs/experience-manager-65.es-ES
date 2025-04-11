---
title: Uso de cURL con AEM
description: Aprenda a usar cURL para tareas Adobe Experience Manager comunes.
contentOwner: Silviu Raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: e3f018e6-563e-456f-99d5-d232f1a4aa55
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 12b370e3041ff179cd249f3d4e6ef584c4339909
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 1%

---

# Uso de cURL con AEM{#using-curl-with-aem}

Los administradores a menudo necesitan automatizar o simplificar tareas comunes dentro de cualquier sistema. En AEM, por ejemplo, la administración de usuarios, la instalación de paquetes y la administración de paquetes OSGi son tareas que se deben realizar con frecuencia.

Debido a la naturaleza RESTful del marco de trabajo de Sling en el que se crea AEM, la mayoría de las tareas se pueden realizar con una llamada de URL. cURL puede utilizarse para ejecutar dichas llamadas de URL y puede ser una herramienta útil para los administradores de AEM.

## Qué es cURL {#what-is-curl}

cURL es un herramienta de línea de comandos de código abierto que se utiliza para realizar manipulaciones URL. Es compatible con una amplia gama de protocolos de Internet, incluidos HTTP, HTTPS, FTP, FTPS, SCP, SFTP, TFTP, LDAP, DAP, DICT, TELNET, FILE, IMAP, POP3, SMTP y RTSP.

cURL es una herramienta bien establecida y ampliamente utilizada para obtener o enviar datos utilizando la sintaxis URL y se lanzó originalmente en 1997. El nombre cURL originalmente significaba &quot;ver URL&quot;.

Debido a la naturaleza RESTful del marco de trabajo Sling sobre el que se construye AEM, la mayoría de las tareas se pueden reducir a una llamada URL, que se puede ejecutar con cURL. [Las tareas](/help/sites-administering/curl.md#common-content-manipulation-aem-curl-commands) de manipulación de contenido, como la activación de páginas y el inicio de tareas](/help/sites-administering/curl.md#common-operational-aem-curl-commands) flujos de trabajo y [operativas, como la administración de paquetes y la administración de usuarios, se pueden automatizar mediante cURL. Además, puede [crear sus propios comandos cURL](/help/sites-administering/curl.md#building-a-curl-ready-aem-command) para la mayoría de las tareas de AEM.

>[!NOTE]
>
>Cualquier comando AEM ejecutado a través de cURL tiene que ser autorizado al igual que cualquier usuario a AEM. Se respetan todas las ACL y los derechos de acceso cuando se utiliza cURL para ejecutar un comando AEM.

## Descargando cURL {#downloading-curl}

cURL es una parte estándar de macOS y algunas distribuciones de Linux. Sin embargo, está disponible para la mayoría de los sistemas operativos. Las últimas descargas se pueden encontrar en [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html).

La repositorio de origen de cURL también se puede encontrar en GitHub.

## Creación de una AEM lista para cURL Comando {#building-a-curl-ready-aem-command}

Los comandos cURL se pueden crear para la mayoría de las operaciones en AEM como desencadenar flujos de trabajo, verificar configuraciones OSGi, desencadenar comandos JMX, crear agentes de replicación y mucho más.

Para encontrar el comando exacto que necesita para su operación particular, debe usar las herramientas de desarrollo de su explorador para capturar la llamada de POST al servidor cuando ejecuta el comando AEM.

En los pasos siguientes se describe cómo hacerlo utilizando la creación de una nueva página en el explorador Chrome como ejemplo.

1. Prepare la acción que desee invocar en AEM. En este caso, hemos seguido hasta el final del asistente para **Crear página**, pero aún no hemos hecho clic en **Crear**.

   ![chlimage_1-66](assets/chlimage_1-66a.png)

1. Inicie las herramientas para desarrolladores y seleccione la ficha **Red**. Haga clic en la opción **Conservar registro** antes de borrar la consola.

   ![chlimage_1-67](assets/chlimage_1-67a.png)

1. Haga clic en **Crear** en el asistente para **Crear página** para crear el flujo de trabajo.
1. Haga clic con el botón derecho en la acción POST resultante y seleccione **Copiar** > **Copiar como cURL**.

   ![chlimage_1-68](assets/chlimage_1-68a.png)

1. Copie el comando cURL en un editor de texto y quite todos los encabezados del comando, que comienzan por `-H` (resaltado en azul en la imagen siguiente) y agregue el parámetro de autenticación adecuado como `-u <user>:<password>`.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Ejecute el comando cURL a través de la línea de comandos y vea la respuesta.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

## Comandos cURL operativos comunes de AEM {#common-operational-aem-curl-commands}

Esta es una lista de comandos cURL de AEM para tareas administrativas y operativas comunes.

>[!NOTE]
>
>Los siguientes ejemplos suponen que AEM se está ejecutando en `localhost` en el puerto `4502` y utiliza el usuario `admin` con la contraseña `admin`. Los marcadores de posición de comandos adicionales se establecen entre corchetes angulares.

### Administración de paquetes {#package-management}

#### Mostrar todos los paquetes instalados

```shell
curl -u <user>:<password> http://<host>:<port>/crx/packmgr/service.jsp?cmd=ls
```

#### Crear un paquete {#create-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=create -d packageName=<name> -d groupName=<name>
```

#### Previsualización de un paquete {#preview-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=preview
```

#### Contenido del paquete de lista {#list-package-content}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/console.html/etc/packages/mycontent.zip?cmd=contents
```

#### Creación de un paquete {#build-a-package}

```shell
curl -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=build
```

#### Volver a empaquetar un paquete {#rewrap-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=rewrap
```

#### Cambiar nombre un paquete {#rename-a-package}

```shell
curl -u <user>:<password> -X POST -Fname=<New Name> http://localhost:4502/etc/packages/<Group Name>/<Package Name>.zip/jcr:content/vlt:definition
```

#### Cargar un paquete {#upload-a-package}

```shell
curl -u <user>:<password> -F cmd=upload -F force=true -F package=@test.zip http://localhost:4502/crx/packmgr/service/.json
```

#### Instalación de un paquete {#install-a-package}

```shell
curl -u <user>:<password> -F cmd=install http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Desinstalar un paquete {#uninstall-a-package}

```shell
curl -u <user>:<password> -F cmd=uninstall http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Eliminar un paquete {#delete-a-package}

```shell
curl -u <user>:<password> -F cmd=delete http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Descargar un paquete {#download-a-package}

```shell
curl -u <user>:<password> http://localhost:4502/etc/packages/my_packages/test.zip
```

#### Replicar un paquete {#replicate-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip?cmd=replicate
```

### Administración de usuarios {#user-management}

#### Crear un nuevo usuario {#create-a-new-user}

```shell
curl -u <user>:<password> -FcreateUser= -FauthorizableId=hashim -Frep:password=hashim http://localhost:4502/libs/granite/security/post/authorizables
```

#### Crear un grupo nuevo {#create-a-new-group}

```shell
curl -u <user>:<password> -FcreateGroup=group1 -FauthorizableId=testGroup1 http://localhost:4502/libs/granite/security/post/authorizables
```

#### Añadir una propiedad a un usuario existente {#add-a-property-to-an-existing-user}

```shell
curl -u <user>:<password> -Fprofile/age=25 http://localhost:4502/home/users/h/hashim.rw.html
```

#### Crear un usuario con un perfil {#create-a-user-with-a-profile}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=hashimkhan -Frep:password=hashimkhan -Fprofile/gender=male http://localhost:4502/libs/granite/security/post/authorizables
```

#### Crear un nuevo usuario como miembro de un grupo {#create-a-new-user-as-a-member-of-a-group}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fmembership=contributor http://localhost:4502/libs/granite/security/post/authorizables
```

#### Añadir un usuario a un grupo {#add-a-user-to-a-group}

```shell
curl -u <user>:<password> -FaddMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### Eliminar un usuario de un grupo {#remove-a-user-from-a-group}

```shell
curl -u <user>:<password> -FremoveMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### Establecer la pertenencia a grupo de un usuario {#set-a-user-s-group-membership}

```shell
curl -u <user>:<password> -Fmembership=contributor -Fmembership=testgroup http://localhost:4502/home/users/t/testuser.rw.html
```

#### Eliminar usuario {#delete-a-user}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/users/t/testuser
```

#### Eliminar un grupo {#delete-a-group}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/groups/t/testGroup
```

### Copia de seguridad {#backup}

Consulte [Copia de seguridad y restauración](/help/sites-administering/backup-and-restore.md#automating-aem-online-backup) para obtener más información.

### OSGi {#osgi}

#### Inicio de un paquete {#starting-a-bundle}

```shell
curl -u <user>:<password> -Faction=start http://localhost:4502/system/console/bundles/<bundle-name>
```

#### Detener un paquete {#stopping-a-bundle}

```shell
curl -u <user>:<password> -Faction=stop http://localhost:4502/system/console/bundles/<bundle-name>
```

### Dispatcher {#dispatcher}

#### Invalidar la caché {#invalidate-the-cache}

```shell
curl -H "CQ-Action: Activate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

#### Desalojar la caché {#evict-the-cache}

```shell
curl -H "CQ-Action: Deactivate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

### Agente de replicación {#replication-agent}

#### Comprobar la Estado de un agente {#check-the-status-of-an-agent}

```shell
curl -u <user>:<password> "http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish"
http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish
```

#### Eliminar un agente {#delete-an-agent}

```shell
curl -X DELETE http://localhost:4502/etc/replication/agents.author/replication99 -u <user>:<password>
```

#### Crear un agente {#create-an-agent}

```shell
curl -u <user>:<password> -F "jcr:primaryType=cq:Page" -F "jcr:content/jcr:title=new-replication" -F "jcr:content/sling:resourceType=/libs/cq/replication/components/agent" -F "jcr:content/template=/libs/cq/replication/templates/agent" -F "jcr:content/transportUri=http://localhost:4503/bin/receive?sling:authRequestLogin=1" -F "jcr:content/transportUser=admin" -F "jcr:content/transportPassword={DES}8aadb625ced91ac483390ebc10640cdf"http://localhost:4502/etc/replication/agents.author/replication99
```

#### Poner en pausa a un agente {#pause-an-agent}

```shell
curl -u <user>:<password> -F "cmd=pause" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

#### Borrar una cola de agentes {#clear-an-agent-queue}

```shell
curl -u <user>:<password> -F "cmd=clear" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

### Comunidades {#communities}

#### Asignar y revocar distintivos {#assign-and-revoke-badges}

Consulte [Communities Puntuación e insignias](/help/communities/implementing-scoring.md#assign-and-revoke-badges) para obtener más información.

Consulte [Conceptos básicos de puntuación e insignias](/help/communities/configure-scoring.md#example-setup) para obtener más información.

#### Reindexación del MSRP {#msrp-reindexing}

Consulte [MSRP - Proveedor de recursos de almacenamiento de MongoDB](/help/communities/msrp.md#running-msrp-reindex-tool-using-curl-command) para obtener detalles.

### Seguridad {#security}

#### Activación y desactivación de CRX DE Lite {#enabling-and-disabling-crx-de-lite}

Consulte [Habilitar CRXDE Lite en AEM](/help/sites-administering/enabling-crxde-lite.md) para obtener más información.

### Recopilación de datos almacenados desechables {#data-store-garbage-collection}

Consulte [Recopilación de residuos del almacén de datos](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) para obtener más información.

### Integración de Analytics y Target {#analytics-and-target-integration}

Consulte [Inclusión en Adobe Analytics y Adobe Target](/help/sites-administering/opt-in.md#configuring-the-setup-and-provisioning-via-script) para obtener más información.

### Inicio de sesión único {#single-sign-on}

#### Enviar encabezado de prueba {#send-test-header}

Consulte [Inicio de sesión único](/help/sites-deploying/single-sign-on.md) para obtener más información.

## Comandos cURL comunes de AEM para la manipulación de contenido {#common-content-manipulation-aem-curl-commands}

Esta es una lista de comandos cURL de AEM para la manipulación de contenido.

>[!NOTE]
>
>Los siguientes ejemplos suponen que AEM se está ejecutando en `localhost` en el puerto `4502` y utiliza el usuario `admin` con la contraseña `admin`. Los marcadores de posición de comandos adicionales se establecen entre corchetes angulares.

### Administración de páginas {#page-management}

#### Activación de página {#page-activation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="activate" http://localhost:4502/bin/replicate.json
```

#### Desactivación de página {#page-deactivation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="deactivate" http://localhost:4502/bin/replicate.json
```

#### Activación de árbol {#tree-activation}

```shell
curl -u <user>:<password> -F cmd=activate -F ignoredeactivated=true -F onlymodified=true -F path=/content/geometrixx http://localhost:4502/etc/replication/treeactivation.html
```

#### Bloquear página {#lock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="lockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### Desbloquear página {#unlock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="unlockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### Copiar página {#copy-page}

```shell
curl -u <user>:<password> -F cmd=copyPage -F destParentPath=/path/to/destination/parent -F srcPath=/path/to/source/location http://localhost:4502/bin/wcmcommand
```

### Cómo realizar un despliegue superficial {#shallow-rollout}

Al utilizar AEM as a Cloud Service, puede haber casos en los que necesite desplegar una sola página específica sin propagar sus subpáginas. Si no se configura correctamente, el comando curl típico para desplegar páginas podría incluir inadvertidamente subpáginas. En esta sección se describe cómo ajustar el comando curl para lograr un despliegue superficial de una página especificada y excluir cualquier subpágina adicional.

Para realizar un despliegue superficial, siga estos pasos:

1. Modifique el comando curl existente cambiando el parámetro de `type=deep` a `type=page`.
1. Utilice la siguiente sintaxis para el comando curl:

```shell
curl -H "Authorization: Bearer <token>" "https://<instance-url>/bin/asynccommand" \
   -d type=page \
   -d operation=asyncRollout \
   -d cmd=rollout \
   -d path="/content/<your-path>"
```

Compruebe también lo siguiente:

1. Asegúrese de reemplazar `<token>` con su token de autorización real y `<instance-url>` con su URL de instancia específica.
1. Reemplace `/content/<your-path>` por la ruta de acceso de la página específica que desea desplegar.

Al establecer `type=page`, el comando identifica solamente la página especificada y excluye las subpáginas. Como tal, esta configuración permite un control preciso sobre la implementación de contenido, lo que garantiza que solo los cambios deseados se propaguen entre entornos. Además, este ajuste también se ajusta a cómo se administran los despliegues mediante la interfaz gráfica de usuario de AEM al seleccionar páginas individuales.

### Flujos de trabajo {#workflows}

Consulte [Interactuar con flujos de trabajo mediante programación](/help/sites-developing/workflows-program-interaction.md) para obtener más información.

### Contenido de Sling {#sling-content}

#### Crear una carpeta {#create-a-folder}

```shell
curl -u <user>:<password> -F jcr:primaryType=sling:Folder http://localhost:4502/etc/test
```

#### Eliminar un nodo {#delete-a-node}

```shell
curl -u <user>:<password> -F :operation=delete http://localhost:4502/etc/test/test.properties
```

#### Mover un nodo {#move-a-node}

```shell
curl -u <user>:<password> -F":operation=move" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### Copiar un nodo {#copy-a-node}

```shell
curl -u <user>:<password> -F":operation=copy" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### Cargar Archivos con Sling PostServlet {#upload-files-using-sling-postservlet}

```shell
curl -u <user>:<password> -F"*=@test.properties"  http://localhost:4502/etc/test
```

#### Cargar Archivos usando Sling PostServlet y especificando el nombre del nodo {#upload-files-using-sling-postservlet-and-specifying-node-name}

```shell
curl -u <user>:<password> -F"test2.properties=@test.properties"  http://localhost:4502/etc/test
```

#### Cargar Archivos especificar un tipo de contenido {#upload-files-specifying-a-content-type}

```shell
curl -u <user>:<password> -F "*=@test.properties;type=text/plain" http://localhost:4502/etc/test
```

### Manipulación de recursos {#asset-manipulation}

Consulte [API HTTP de Assets](/help/assets/mac-api-assets.md) para obtener más información.
