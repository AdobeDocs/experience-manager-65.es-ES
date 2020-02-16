---
title: Tipos de nodos personalizados
seo-title: Tipos de nodos personalizados
description: AEM se basa en Sling y utiliza un repositorio JCR con tipos de nodos ofrecidos por ambos, pero AEM también proporciona una serie de tipos de nodos personalizados
seo-description: AEM se basa en Sling y utiliza un repositorio JCR con tipos de nodos ofrecidos por ambos, pero AEM también proporciona una serie de tipos de nodos personalizados
uuid: f2022504-e433-4b42-9cc1-eef41086483a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: aae186eb-e059-4a9d-b02d-86a86c86589d
translation-type: tm+mt
source-git-commit: d83cd0695f69d82e49b1761df2d8c64b0037e1f9

---


# Tipos de nodos personalizados{#custom-node-types}

Debido a que AEM se basa en Sling y utiliza un repositorio JCR, los tipos de nodos ofrecidos por ambos están disponibles para su uso:

* [Tipos de nodos JCR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Tipos de nodos Sling](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Además de esto. AEM proporciona una serie de tipos de nodos personalizados.

## Auditoría {#audit}

### cq:AuditEvent {#cq-auditevent}

**Descripción**

Define el tipo de nodo de un nodo de evento de auditoría.

* `@prop cq:time`
* `@prop cq:userid`
* `@prop cq:path`
* `@prop cq:type`
* `@prop cq:category`
* `@prop cq:properties`

**Definición**

* `[cq:AuditEvent]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
* `- cq:time (date)`
* `- cq:userid (string)`
* `- cq:path (string)`
* `- cq:type (string)`
* `- cq:category (string)`
* `- cq:properties (binary)`

## Comentario {#comment}

### cq:Comment {#cq-comment}

**Descripción**

Define el tipo de nodo de un nodo de comentario.

* `@prop userIdentifier`

**Definición**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq:CommentAttachment {#cq-commentattachment}

**Descripción**

Define el tipo de nodo de un `commentattachment` nodo

**Definición**

* `[cq:CommentAttachment] > nt:file`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:CommentContent {#cq-commentcontent}

**Descripción**

Define el tipo de nodo de un nodo de contenido de comentarios

**Definición**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq:GeoLocation {#cq-geolocation}

**Descripción**

Mezcla que define una ubicación geográfica en grados decimales (DD)

* `@prop latitude` - latitud codificada como doble utilizando grados decimales
* `@prop longitude` - longitud codificada como doble utilizando grados decimales

**Definición**

* `[cq:GeoLocation] mixin`
* `- latitude (double)`
* `- longitude (double)`

### cq:Trackback {#cq-trackback}

**Descripción**

Define el tipo de nodo de un nodo trackback.

**Definición**

* `[cq:Trackback] > mix:title, mix:created, mix:language, nt:unstructured`

## Núcleo {#core}

### cq:Page {#cq-page}

**Descripción**

Define la página de CQ predeterminada.

* `@node jcr:content` - Contenido principal de la página.

**Definición**

* `[cq:Page] > nt:hierarchyNode orderable`
   * `+ jcr:content (nt:base) = nt:unstructured copy primary`
   * `+ * (nt:base) = nt:base version`

### cq:PseudoPage {#cq-pseudopage}

**Descripción**

Define un tipo de mezcla que marca los nodos como pseudopáginas. Esto significa que pueden adaptarse para la compatibilidad con la edición de páginas y WCM.

**Definición**

* `[cq:PseudoPage] mixin`

### cq:PageContent {#cq-pagecontent}

**Descripción**

Define el nodo predeterminado para el contenido de la página, con las propiedades mínimas utilizadas por WCM.

* `@prop jcr:title` - Título de la página.
* `@prop jcr:description` - Descripción de esta página.
* `@prop cq:template` - Ruta a la plantilla utilizada para crear la página.
* `@prop cq:allowedTemplates` - Lista de expresiones regulares utilizadas para determinar las rutas a la plantilla permitida.
* `@prop pageTitle` - El título se muestra generalmente en la `<title>` etiqueta .
* `@prop navTitle` - Título que se utiliza normalmente en la navegación.
* `@prop hideInNav` - Especifica si la página debe estar oculta en la navegación.
* `@prop onTime` - Hora en la que esta página se convierte en válida.
* `@prop offTime` - Hora en la que esta página no es válida.
* `@prop cq:lastModified` - Fecha en la que se modificó la página (o sus párrafos) por última vez.
* `@prop cq:lastModifiedBy` - Último usuario en cambiar la página (o sus párrafos).
* `@prop jcr:language` - El idioma del contenido de la página.

>[!NOTE]
>
>No es obligatorio que el contenido de la página utilice este tipo.

**Definición**
* `[cq:PageContent] > nt:unstructured, mix:title, mix:created, cq:OwnerTaggable, sling:VanityPath, cq:ReplicationStatus, sling:Resource orderable`
   * `- cq:template (string)`
   * `- cq:allowedTemplates (string) multiple`
   * `- pageTitle (string)`
   * `- navTitle (string)`
   * `- hideInNav (boolean)`
   * `- onTime (date)`
   * `- offTime (date)`
   * `- cq:lastModified (date)`
   * `- cq:lastModifiedBy (string)`
   * `- cq:designPath (string)`
   * `- jcr:language (string)`

### cq:Template {#cq-template}

**Descripción**

Define una plantilla de CQ.

* `@node jcr:content` - Contenido predeterminado para páginas nuevas.
* `@node icon.png` - Archivo que contiene un icono característico.
* `@node thumbnail.png` - Archivo que contiene una imagen en miniatura característica.
* `@node workflows` - Asignación automática de configuración de flujo de trabajo. La configuración seguirá la siguiente estructura:
   * `+ workflows`
      * `+ name1`
         * `- cq:path`
            * `- cq:workflowName`
* `@prop allowedParents` - Patrones de expresión regulares para determinar las rutas a las plantillas permitidas como plantillas principales.
* `@prop allowedChildren` - Patrones de expresión regulares para determinar las rutas a las plantillas permitidas como plantillas secundarias.
* `@prop ranking` - Coloque dentro de la lista de plantillas en el cuadro de diálogo Crear página.

**Definición**

* `[cq:Template] > nt:hierarchyNode, mix:title`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ jcr:content (nt:base) copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `+ workflows (nt:base) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `- ranking (long)`

### cq:Component {#cq-component}

**Descripción**

Define un componente de CQ.

* `@prop jcr:title` - Título del componente.
* `@prop jcr:description` - Descripción del componente.
* `@node dialog` - Cuadro de diálogo principal.
* `@prop dialogPath` - Ruta del cuadro de diálogo principal (alternativa al cuadro de diálogo).
* `@node design_dialog` - Cuadro de diálogo Diseño.
* `@prop cq:cellName` - Nombre de la celda de diseño.
* `@prop cq:isContainer` - Indica si se trata de un componente contenedor. Esto fuerza el uso de los nombres de celda de los componentes secundarios en lugar de los nombres de ruta. Por ejemplo, `parsys` es un componente contenedor. Si no se define este valor, la comprobación se realiza en función de la existencia de un `cq:childEditConfig`.
* `@prop cq:noDecoration` - Si es true, no se dibujan `div` etiquetas decorativas al incluir este componente.
* `@node cq:editConfig` - La configuración que define los parámetros de la barra de edición.
* `@node cq:childEditConfig` - La configuración de edición heredada por los componentes secundarios.
* `@node cq:htmlTag` - Define atributos de etiqueta adicionales que se agregan a la etiqueta &quot;circundante&quot; `div` cuando se incluye el componente.
* `@node icon.png`- Archivo que contiene un icono característico.
* `@node thumbnail.png` - Archivo que contiene una imagen en miniatura característica.
* `@prop allowedParents` - Patrones de expresión regulares para determinar las rutas de los componentes permitidos como componentes principales.
* `@prop allowedChildren` - Patrones de expresión regulares para determinar las rutas de los componentes permitidos como componentes secundarios.
* `@node virtual` - Contiene subnodos que reflejan los componentes virtuales utilizados para arrastrar y soltar el componente.
* `@prop componentGroup` - Nombre del grupo de componentes, utilizado para arrastrar y soltar el componente.
* `@node cq:infoProviders` - Contiene subnodos, cada uno de los cuales tiene una propiedad `className` que hace referencia a un `PageInfoProvider`.

**Definición**

* `[cq:Component] > nt:folder, mix:title, sling:ResourceSuperType`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ dialog (nt:base) = nt:unstructured copy`
   * `- dialogPath (string)`
   * `+ design_dialog (nt:base) = nt:unstructured copy`
   * `- cq:cellName (string)`
   * `- cq:isContainer (boolean)`
   * `- cq:noDecoration (boolean)`
   * `+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:childEditConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:htmlTag (nt:base) = nt:unstructured copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `+ virtual (nt:base) = sling:Folder copy`
   * `- componentGroup (string)`
   * `+ cq:infoProviders (nt:base) = nt:unstructured copy`

### cq:ComponentMixin {#cq-componentmixin}

**Descripción**

Define un componente CQ como tipo de mezcla.

**Definición**

`[cq:ComponentMixin] > cq:Component mixin`

### cq:EditConfig {#cq-editconfig}

**Descripción**

Define la configuración de la &quot;barra de edición&quot;.

* `@prop cq:dialogMode` - Modo del cuadro de diálogo:
   * `floating` - para un diálogo normal y flotante
   * `inline` - edición en línea
   * `auto` - detección automática (según el espacio disponible)
* `@node cq:inplaceEditing` - Configuración de edición directa para este componente.
* `@prop cq:layout`- Diseño de la barra de edición:
   * `editbar` - editar barra
   * `rollover` - pasar el cursor sobre el marco
   * `auto` - detección automática
* `@node cq:formParameters`- Parámetros adicionales para agregar al formulario de diálogo.
* `@prop cq:actions`- Lista de acciones (editar botones de barra o elementos de menú).
* `@node cq:actionConfigs` - Configuraciones de utilidades para editar elementos de menú o de barra.
* `@prop cq:emptyText` - Texto que se mostrará si no hay contenido visual presente.
* `@node cq:dropTargets` - Colección de `{@link cq:DropTargetConfig}` nodos.

**Definición**

* `[cq:EditConfig] > nt:unstructured, nt:hierarchyNode orderable`
   * `- cq:dialogMode (string) < 'auto', 'floating', 'inline'`
   * `- cq:layout (string) < 'editbar', 'rollover', 'auto' + cq:formParameters (nt:base) = nt:unstructured`
   * `- cq:actions (string) multiple`
   * `+ cq:actionConfigs (nt:base) = nt:unstructured`
   * `- cq:emptyText (string)`
   * `+ cq:dropTargets (nt:base) = nt:unstructured`
   * `+ cq:listeners (nt:base) = cq:EditListenersConfig`

### cq:DropTargetConfig {#cq-droptargetconfig}

**Descripción**

Configura un destino de colocación de un componente. El nombre de este nodo se utilizará como ID para arrastrar y soltar.

* `@prop accept` - Lista de tipos de MIME aceptados por este objetivo de colocación;p. ej. `["image/*"]`
* `@prop groups` - Lista de grupos de arrastrar y soltar que aceptan un origen.
* `@prop propertyName` - Nombre de la propiedad utilizada para almacenar la referencia.

**Definición**

* `[cq:DropTargetConfig] > nt:unstructured orderable`
   * `- accept (string) multiple`
   * `- groups (string) multiple`
   * `- propertyName (string)`
   * `+ parameters (nt:base) = nt:unstructured`

### cq:VirtualComponent {#cq-virtualcomponent}

**Descripción**

Define un componente CQ virtual. Actualmente, solo se utilizan para el nuevo asistente de arrastrar y soltar componentes.

* `@prop jcr:title` - Título de este componente.
* `@prop jcr:description` - Descripción de este componente.
* `@node cq:editConfig` - Edite la configuración que define los parámetros de la barra de edición.
* `@node cq:childEditConfig`- Edite la configuración heredada por los componentes secundarios.
* `@node icon.png` - Archivo que contiene un icono característico.
* `@node thumbnail.png` - Archivo que contiene una imagen en miniatura característica.
* `@prop allowedParents` - Patrones de expresión regulares para determinar las rutas de los componentes permitidos como componentes principales.
* `@prop allowedChildren` - Patrones de expresión regulares para determinar las rutas de los componentes permitidos como componentes secundarios.
* `@prop componentGroup` - Nombre del grupo de componentes para arrastrar y soltar el componente.

**Definición**

`[cq:VirtualComponent] > nt:folder, mix:title`
`- * (undefined)`
`- * (undefined) multiple`
`+ * (nt:base) = nt:base multiple version`
`+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
`+ icon.png (nt:file) copy`
`+ thumbnail.png (nt:file) copy`
`- allowedParents (string) multiple`
`- allowedChildren (string) multiple`
`- componentGroup (string)`

### cq:EditListenersConfig {#cq-editlistenersconfig}

**Descripción**

Define los oyentes (del lado del cliente) que se ejecutarán en un evento de edición. Los valores deben hacer referencia a una función de detector del lado del cliente válida o contener un método abreviado predefinido:

* `REFRESH_PAGE`
* `REFRESH_SELF`
* `REFRESH_PARENT`

* `@prop aftercreate` - Se activa después de crear un componente.
* `@prop afteredit` - Se activa después de editar (modificar) un componente.
* `@prop afterdelete` - Se desencadena después de que se elimina un componente.
* `@prop afterinsert` - Se desencadena después de agregar un componente a este contenedor.
* `@prop afterremove` - Se desencadena después de que se haya eliminado un componente de este contenedor.
* `@prop aftermove` - Se desencadena después de que los componentes se hayan movido a este contenedor.

**Definición**

* `[cq:EditListenersConfig]`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `+ &ast; (nt:base) = nt:base multiple version`
   * `- aftercreate (string)`
   * `- afteredit (string)`
   * `- afterdelete (string)`
   * `- afterinsert (string)`
   * `- afterremove (string)`
   * `- aftermove (string)`

## DAM {#dam}

### dam:AssetContent {#dam-assetcontent}

**Descripción**

Contenido de un recurso DAM.

**Definición**

* `[dam:AssetContent] > nt:unstructured`
   * `+ metadata (nt:unstructured)`
   * `+ renditions (nt:folder)`

### dam:Asset {#dam-asset}

**Descripción**

Recurso DAM.

**Definición**

`[dam:Asset] > nt:hierarchyNode`
`+ jcr:content (dam:AssetContent) = dam:AssetContent copy primary`
`+ * (nt:base) = nt:base version`

### dam:Thumbnail {#dam-thumbnail}

**Descripción**

Miniatura para representar un recurso DAM.

**Definición**

* `[dam:Thumbnails]`
   * `mixin`
   * `+ dam:thumbnails (nt:folder)`

## Lista de contenedores de entrega {#delivery-container-list}

### cq:containerList {#cq-containerlist}

**Descripción**

Lista de contenedores.

**Definición**

* `[cq:containerList]`
   * `mixin`

## Página de envío {#delivery-page}

### cq:Cq4PageAttributes {#cq-cq-pageattributes}

**Descripción**

`cq:attributes` es el tipo de nodo para las etiquetas de versión de ContentBus. Este nodo solo tiene una serie de propiedades; de los cuales tres están predefinidos &quot;creado&quot;, &quot;csd&quot; y &quot;marca de tiempo&quot;.

* `@prop created (long) mandatory copy` - Marca de hora de la creación de la información de la versión, generalmente la hora de ingreso de la versión anterior o la hora de creación de la página.
* `@prop csd (string) mandatory copy` - atributo estándar csd, copia de la propiedad cq:csd del nodo de página
* `@prop timestamp (long) mandatory copy` - Marca de tiempo de la última modificación de la versión, generalmente tiempo de inicio de sesión.
* `@prop * (string) copy` - Atributos adicionales, con versiones del nodo principal.

**Definición**

* `[cq:Cq4PageAttributes] > nt:base`
   * `- created (long) mandatory copy`
   * `- csd (string) mandatory copy`
   * `- timestamp (long) mandatory copy`
   * `- &ast; (string) copy`

### cq:Cq4ContentPage {#cq-cq-contentpage}

**Descripción**

El tipo de nodo `cq:contentPage` contiene las definiciones de propiedad y nodo secundario para las páginas de contenido de ContentBus. Solo cuando se agrega este tipo de mezcla a un nodo de tipo `cq:page`, un nodo se convierte en una página de contenido de ContentBus.

Los elementos de una `cq:Cq4ContentPage` son:

* `@prop cq:csd` - El CSD de ContentBus de la página.
* `@node cq:content` - El contenido de la página. Este nodo secundario no existe si el nodo de página está en estado &quot;Existente sin contenido&quot; o &quot;Eliminado&quot;.
* `@node cq:attributes` - Lista de atributos de página, que anteriormente se conocían como etiquetas de versión. Este nodo es obligatorio para el tipo cq:contentPage. Se crea una versión del nodo de atributos cuando la página es un nodo con una versión.

**Definición**

* `[cq:Cq4ContentPage]`
   * `- cq:csd (string) mandatory copy`
   * `+ cq:attributes (cq:Cq4PageAttributes)`

## Importador {#importer}

### cq:PollConfig {#cq-pollconfig}

**Descripción**

Configuración de la encuesta.

* `@prop source (String) mandatory` - El URI de fuente de datos es obligatorio y no debe estar vacío
* `@prop target (String)` - Ubicación de destino en la que se almacenan los datos recuperados del origen de datos. Es opcional y se establece de forma predeterminada en el nodo cq:PollConfig.
* `@prop interval (Long)` - El intervalo en segundos en el que se sondearán los datos nuevos o actualizados del origen de datos. Es opcional y su valor predeterminado es de 30 minutos (1800 segundos).
* [Creación de servicios de importación de datos personalizados para Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/polling.html)

**Definición**

* `[cq:PollConfig]
   * `mixin`
   * `- source (String) mandatory`
   * `- target (String)`
   * `- interval (Long)`

### cq:PollConfigFolder {#cq-pollconfigfolder}

**Descripción**

Conveniencia de tipo de nodo principal para crear fácilmente nodos de configuración de encuesta.

**Definición**

`[cq:PollConfigFolder] > sling:Folder, cq:PollConfig`

## Ubicación {#location}

### cq:GeoLocation {#cq-geolocation-1}

**Descripción**

Mezcla que define una ubicación geográfica en grados decimales (DD).

* `@prop latitude` - Latitud codificada como doble utilizando grados decimales.
* `@prop longitude` - Longitud codificada como doble utilizando grados decimales.

**Definición**

* `[cq:GeoLocation]
   * `mixin`
   * `- latitude (double)`
   * `- longitude (double)`

## Mailer {#mailer}

### cq:mailerMessage {#cq-mailermessage}

**Descripción**

Tipos de nodos MailerService. El buzón utiliza nodos que tienen esta mezcla como nodos raíz de definiciones de mensajes.

**Definición**

* `[cq:mailerMessage]`
   * `mixin`
   * `- messageStatus (string)`
   * `= 'new'`
   * `mandatory autocreated`

## Medios convencionales {#msm}

### cq:LiveRelationship {#cq-liverelationship}

**Descripción**

Define una mezcla de LiveRelationship. Un nodo maestro y un nodo esclavo pueden vincularse virtualmente a través de LiveRelationship.

**Definición**

* `[cq:LiveRelationship] mixin`
   * `- cq:lastRolledout (date)`
   * `- cq:lastRolledoutBy (string)`
   * `- cq:sourceUUID (string)`

### cq:LiveSync {#cq-livesync}

**Descripción**

Define una mezcla de LiveSync. Si un nodo participa en una LiveRelationship con un nodo maestro como esclavo, se marca como LiveSync.

* `@prop cq:master` - Ruta del nodo maestro de LiveRelationship.
* `@prop cq:isDeep` - Define si la relación está disponible para niños.
* `@prop cq:syncTrigger` - Define cuándo se activa la sincronización.
* `@node * LiveSyncAction` - Acciones para realizar la sincronización

**Definición**

`[cq:LiveSync] > cq:LiveRelationship mixin orderable`
`+ * (cq:LiveSyncAction) = cq:LiveSyncAction`
`+ cq:LiveSyncConfig (nt:base) = cq:LiveSyncConfig`

### cq:LiveSyncCanceled {#cq-livesynccancelled}

**Descripción**

Define una mezcla de LiveSyncCanceled. Cancelar el comportamiento de LiveSync de un nodo esclavo que puede estar involucrado en una LiveRelationship debido a uno de sus padres.

* `@prop cq:isCancelledForChildren` - Define si se cancela LiveSync; también para niños.

**Definición**

* `[cq:LiveSyncCancelled] > cq:LiveRelationship mixin`
   * `- cq:isCancelledForChildren (boolean)`

### cq:LiveSyncAction {#cq-livesyncaction}

**Descripción**

Define un LiveSyncAction conectado a un LiveSync.

* `@prop name` - Nombre de la acción
* `@prop value` - Valor de la acción

**Definición**

* `[cq:LiveSyncAction] > nt:unstructured`

### cq:LiveSyncConfig {#cq-livesyncconfig}

**Descripción**

Configuración de Live Sync.

**Definición**

* `[cq:LiveSyncConfig]`
   * `- cq:master (string) mandatory`
   * `- cq:isDeep (boolean)`
   * `- cq:trigger (string) /** deprecated **/`

Para AEM 5.4, añada al final de la lista:

* `- cq:rolloutConfigs (string) multiple /** deprecated **/`

### cq:BlueprintAction {#cq-blueprintaction}

**Descripción**

Acción de modelo

**Definición**

* `[cq:BlueprintAction] > nt:unstructured`

## Plataforma {#platform}

### cq:Console {#cq-console}

**Descripción**

Define el tipo de nodo de una consola.

**Definición**

* `[cq:Console] > sling:VanityPath, mix:title`
   * `mixin`

## Replicación {#replication}

### cq:ReplicationStatus {#cq-replicationstatus}

**Descripción**

Define la combinación de información de estado de replicación.

* `@prop cq:lastPublished`- La fecha de la última publicación de la página (ya no se utiliza).
* `@prop cq:lastPublishedBy`- El usuario que publicó la página por última vez (ya no se usa).
* `@prop cq:lastReplicated` - La fecha en que se replicó la página por última vez.
* `@prop cq:lastReplicatedBy` - El usuario que replicó la última página.
* `@prop cq:lastReplicationAction` - La acción de replicación: activar o desactivar.
* `@prop cq:lastReplicationStatus` - El estado de la replicación (ya no se usa).

**Definición**

* `[cq:ReplicationStatus]
   * `mixin`
   * `- cq:lastPublished (date) ignore`
   * `- cq:lastPublishedBy (string) ignore`
   * `- cq:lastReplicated (date) ignore`
   * `- cq:lastReplicatedBy (string) ignore`
   * `- cq:lastReplicationAction (string) ignore`
   * `- cq:lastReplicationStatus (string) ignore`

## Seguridad {#security}

### cq:ApplicationPrivilege {#cq-applicationprivilege}

**Descripción**

Define un privilegio de aplicación.

**Definición**

* `[cq:ApplicationPrivilege] mixin`

### cq:PrivilegeAcl {#cq-privilegeacl}

**Descripción**

Define una ACL de privilegios de aplicación.

* `@prop cq:isPathDependent`
* `@node * ACEs`

**Definición**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace}

**Descripción**

Define una ACE de privilegios de aplicación.

* `@prop path`
* `@prop deny`

**Definición**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

### cq:ApplicationPrivilege {#cq-applicationprivilege-1}

**Descripción**

Define un privilegio de aplicación.

**Definición**

* `[cq:ApplicationPrivilege] mixin`

### cq:PrivilegeAcl {#cq-privilegeacl-1}

**Descripción**

Define una ACL de privilegios de aplicación.

* `@prop cq:isPathDependent`
* `@node * ACEs`

**Definición**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace-1}

**Descripción**

Define una ACE de privilegios de aplicación.

* `@prop path`
* `@prop deny`

**Definición**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

## Importador de sitios {#site-importer}

### cq:ComponentExtractorSource {#cq-componentextractorsource}

**Descripción**

Define un tipo de mezcla que marca los archivos que se pueden abrir con el extractor de componentes.

**Definición**

`[cq:ComponentExtractorSource] mixin`

## Etiquetado {#tagging}

### cq:Tag {#cq-tag}

**Descripción**

Define una sola etiqueta, pero también puede contener etiquetas, creando así una taxonomía

**Definición**

* `[cq:Tag] > nt:base, mix:title`
   * `- sling:resourceType (String)`
   * `- * (undefined) multiple`
   * `- * (undefined)`
   * `+ * (nt:base) = cq:Tag version`

### cq:Taggable {#cq-taggable}

**Descripción**

Mezcla base abstracta para contenido etiquetable.

* `@node cq:tags`

**Definición**

* `[cq:Taggable]`
   * `- cq:tags (string) multiple`

### cq:OwnerTaggable {#cq-ownertaggable}

**Descripción**

Solo los autores y propietarios pueden etiquetar el contenido (etiquetado moderado/administrado).

**Definición**

* `[cq:OwnerTaggable] > cq:Taggable`

### cq:UserTaggable {#cq-usertaggable}

**Descripción**

Cualquier usuario o sitio web público puede etiquetar el contenido (estilo Web2.0), que se utiliza dentro de cq:userContent.

**Definición**

* `[cq:UserTaggable] > cq:Taggable`
   * `mixin`

### cq:AllowUserContent {#cq-allowsusercontent}

**Descripción**

Agrega un `cq:userContent` subnodo que los usuarios pueden modificar. Cada usuario tendrá su propio `cq:userContent/<userid>` subnodo, que generalmente tiene la mezcla `cq:UserTaggable`.

**Definición**

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (nt:unstructured)`

Variante extendida, que define más explícitamente el `cq:userContent` árbol

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (cq:UserContent)`

### cq:UserContent {#cq-usercontent}

**Descripción**

Los usuarios pueden modificarlo.

**Definición**

* `[cq:UserContent] > nt:unstructured`
   * `// userids`
   * `+ * (cq:UserData)`
   * `// other content`
   * `+ * (nt:base)`

### cq:UserData {#cq-userdata}

**Descripción**

Datos del usuario

**Definición**

* `[cq:UserData] > nt:unstructured, cq:UserTaggable`

## Widgets {#widgets}

### cq:ClientLibraryFolder {#cq-clientlibraryfolder}

**Descripción**

Carpeta de biblioteca de cliente

**Definición**

* `[cq:ClientLibraryFolder] > sling:Folder`
   * `- categories (string) multiple`
   * `- dependencies (string) multiple`

### cq:Widget {#cq-widget}

**Descripción**

Widget

**Definición**

* `[cq:Widget] > nt:unstructured orderable`
   * `- xtype (string)`
   * `- name (string)`
   * `- title (string)`
   * `+ items (nt:base) = cq:WidgetCollection copy`

### cq:WidgetCollection {#cq-widgetcollection}

**Descripción**

Colección de utilidades

**Definición**

* `[cq:WidgetCollection] > nt:unstructured`
   * `orderable`
   * `+ * (cq:Widget) = cq:Widget copy`

### cq:Dialog {#cq-dialog}

**Descripción**

Cuadro de diálogo

**Definición**

* `[cq:Dialog] > cq:Widget orderable`

### cq:Panel {#cq-panel}

**Descripción**

Panel

**Definición**

`[cq:Panel] > cq:Widget orderable`

### cq:TabPanel {#cq-tabpanel}

**Descripción**

Panel de fichas

**Definición**

* `[cq:TabPanel] > cq:Panel ordenable&quot;
   * `- activeTab (long)`

### cq:Field {#cq-field}

**Descripción**

Campo

**Definición**

* `[cq:Field] > cq:Widget orderable`
   * `- fieldLabel (string)`
   * `- value (string)`
   * `- ignoreData (boolean)`

## Wiki {#wiki}

### wiki:Tema {#wiki-topic}

**Descripción**

Tema Wiki

**Definición**

* `[wiki:Topic] > nt:unstructured, nt:hierarchyNode, mix:versionable, mix:lockable`
   * `+ * (wiki:Topic) version`
   * `+ wiki:attachments (nt:folder) = nt:folder version`
   * `+ wiki:properties (wiki:Properties) = wiki:Properties copy`
   * `- wiki:text (string) mandatory primary`
   * `- wiki:lastModified (date) mandatory`
   * `- wiki:lastModifiedBy (string) mandatory`
   * `- wiki:topicName`
   * `- wiki:topicTitle`
   * `- wiki:lockedBy`
   * `- wiki:logMessage (string)`
   * `- wiki:quietSave (boolean)`

### wiki:Usuario {#wiki-user}

**Descripción**

Usuario Wiki

**Definición**

* `[wiki:User] mixin`
   * `- wiki:subscriptions (string) multiple`

### wiki:Propiedades {#wiki-properties}

**Descripción**

Propiedades de Wiki

**Definición**

* `[wiki:Properties]`
   * `- wiki:isGlobal (boolean)`
   * `- * (undefined)`

## Flujo de trabajo {#workflow}

### cq:Workflow {#cq-workflow}

**Descripción**

Representa una instancia de flujo de trabajo.

**Definición**

* `[cq:Workflow] > nt:base, mix:referenceable`
   * `- modelId (String)`
   * `- modelVersion (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- initiator (String)`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `- sling:resourceType (String) = "cq/workflow/components/instance" mandatory autocreated`
   * `+ workflowStack (nt:unstructured)`
   * `+ wait (nt:unstructured)`
   * `+ orTab (nt:unstructured)`
   * `+ data (cq:WorkflowData)`
   * `+ history (nt:unstructured)`
   * `+ metaData (nt:unstructured)`
   * `+ workItems (nt:unstructured)`

### cq:WorkItem {#cq-workitem}

**Descripción**

Elemento de trabajo.

**Definición**

* `[cq:WorkItem]`
   * `- assignee (String)`
   * `- workflowId (String)`
   * `- nodeId (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- dueTime (Date)`
   * `- sling:resourceType (String) = "cq/workflow/components/workitem" mandatory autocreated`
   * `+ metaData (nt:unstructured)`

### cq:Payload {#cq-payload}

**Descripción**

Carga útil

**Definición**

* `[cq:Payload]`
   * `- path (Path)`
   * `- uuid (String)`
   * `- jcr:url (String)`
   * `- binary (Binary)`
   * `- javaObject (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:WorkflowData {#cq-workflowdata}

**Descripción**

Datos de flujo de trabajo

**Definición**

* `[cq:WorkflowData]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ payload (cq:Payload)`
   * `+ metaData (nt:unstructured) copy`

### cq:WorkflowModel {#cq-workflowmodel}

**Descripción**

Configuración de flujo de trabajo de asignación automática. La configuración seguirá esta estructura a continuación:
* `workflows`
   * `+ name1`
      * `- cq:path`
      * `- cq:workflowName`
   * `+ workflows (nt:base)`

**Definición**

* `[cq:WorkflowModel] > nt:base, mix:versionable`
   * `orderable`
   * `- title (String)`
   * `- description (String)`
   * `- sling:resourceType (String) = "cq/workflow/components/model" mandatory autocreated`
   * `+ nodes (nt:unstructured)`
      * `copy`
   * `+ transitions (nt:unstructured)`
      * `copy`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:WorkflowNode {#cq-workflownode}

**Descripción**

Nodo de flujo de trabajo

**Definición**

* `[cq:WorkflowNode] orderable`
   * `- title (String)`
   * `- description (String)`
   * `- maxIdleTime (long)`
   * `- type (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ metaData (nt:unstructured)`
      * `copy`
   * `+ timeoutConfiguration (nt:unstructured)`
      * `copy`

### cq:WorkflowTransition {#cq-workflowtransition}

**Descripción**

Transición de flujo de trabajo

**Definición**

* `[cq:WorkflowTransition] orderable`
   * `- from (String)`
   * `- to (String)`
   * `- rule (String)`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:OrTab {#cq-ortab}

**Descripción**

Ficha O

**Definición**

* `[cq:OrTab]`
   * `- workflowId (String) // not compulsory as this node will already be attached to the workflow node`
   * `- nodeId (String)`

### cq:Wait {#cq-wait}

**Descripción**

Espera

**Definición**

* `[cq:Wait]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- destNodeId (String)`
   * `- fromNodeId (String)`

### cq:WorkflowStack {#cq-workflowstack}

**Descripción**

Pila de flujo de trabajo

**Definición**

* `[cq:WorkflowStack]`
   * `- containeeInstanceId (String)`
   * `- parentInstanceId (String)`
   * `- nodeId (String)`

### cq:ProcessStack {#cq-processstack}

**Descripción**

Pila de procesos

**Definición**

* `[cq:ProcessStack]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- containerWorkflowModelId (String)`
   * `- containerWorkflowNodeId`
   * `- containerWorkflowEndNodeId // still needed (if name already defines that id)`

### cq:WorkflowLauncher {#cq-workflowlauncher}

**Descripción**

Iniciador de flujo de trabajo

**Definición**

* `[cq:WorkflowLauncher]`
   * `- nodetype (String)`
   * `- glob (String)`
   * `- eventType (Long)`
   * `- description (String)`
   * `- condition (String)`
   * `- workflow (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
