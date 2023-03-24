---
title: Ampliación del administrador de varios sitios
seo-title: Extending the Multi Site Manager
description: Esta página le ayuda a ampliar las funcionalidades del administrador de varios sitios
seo-description: This page helps you extend the functionalities of the Multi Site Manager
uuid: dfa7d050-29fc-4401-8d4d-d6ace6b49bea
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6128c91a-4173-42b4-926f-bbbb2b54ba5b
docset: aem65
exl-id: bba64ce6-8b74-4be1-bf14-cfdf3b9b60e1
source-git-commit: 0caaa4b5de519567df4a527f62a2583abd7ed937
workflow-type: tm+mt
source-wordcount: '2593'
ht-degree: 2%

---

# Ampliación del administrador de varios sitios{#extending-the-multi-site-manager}

Esta página le ayuda a ampliar las funcionalidades del administrador de varios sitios:

* Obtenga información sobre los miembros principales de la API Java de MSM.
* Cree una nueva acción de sincronización que se pueda utilizar en una configuración de lanzamiento.
* Modifique el idioma predeterminado y los códigos de país.

<!-- * Remove the "Chapters" step in the Create Site wizard. -->

>[!NOTE]
>
>Esta página debe leerse junto con [Reutilización del contenido: Administrador de varios sitios](/help/sites-administering/msm.md).
>
>Las siguientes secciones de la reestructuración del repositorio de Sites de la AEM 6.4 también pueden ser de interés:
>* [Configuraciones del modelo del administrador de varios sitios](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html?lang=en#multi-site-manager-blueprint-configurations)
>* [Configuraciones de lanzamiento del administrador de varios sitios](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-rollout-configurations)


>[!CAUTION]
>
>El administrador de varios sitios y su API se utilizan durante la creación de un sitio web, por lo que solo están pensados para utilizarse en un entorno de creación.

## Información general sobre la API de Java {#overview-of-the-java-api}

La administración de varios sitios consta de los siguientes paquetes:

* [com.day.cq.wcm.msm.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

Los principales objetos de la API de MSM interactúan de la siguiente manera (consulte también [Términos utilizados](/help/sites-administering/msm.md#terms-used)):

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   A `Blueprint` (como en [configuración de modelo](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)) especifica las páginas desde las que una Live Copy puede heredar contenido.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * El uso de una configuración de modelo ( `Blueprint`) es opcional, pero:

      * Permite que el autor use el **Despliegue** en el origen (para insertar (explícitamente) modificaciones en Live Copies que heredan de este origen).
      * Permite al autor utilizar **Crear sitio**; esto permite al usuario seleccionar fácilmente idiomas y configurar la estructura de la Live Copy.
      * Define la configuración de lanzamiento predeterminada para cualquier Live Copies resultante.

* **`LiveRelationship`**

   La variable `LiveRelationship` especifica la conexión (relación) entre un recurso de la rama de Live Copy y su recurso de origen/modelo equivalente.

   * Las relaciones se utilizan al realizar la herencia y el despliegue.
   * `LiveRelationship` los objetos proporcionan acceso (referencias) a las configuraciones de despliegue ( `RolloutConfig`), `LiveCopy`y `LiveStatus` objetos relacionados con la relación.

   * Por ejemplo, se crea una Live Copy en `/content/copy/us` del origen/modelo en `/content/we-retail/language-masters`. Los recursos `/content/we.retail/language-masters/en/jcr:content` y `/content/copy/us/en/jcr:content` formar una relación.

* **`LiveCopy`**

   `LiveCopy` contiene los detalles de configuración de las relaciones ( `LiveRelationship`) entre los recursos de Live Copy y sus recursos de origen/modelo.

   * Utilice la variable `LiveCopy` para acceder a la ruta de la página, a la ruta de la página de origen/modelo, a las configuraciones de lanzamiento y si las páginas secundarias también se incluyen en la `LiveCopy`.

   * A `LiveCopy` nodo se crea cada vez **Crear sitio** o **Crear Live Copy** se utiliza.

* **`LiveStatus`**

   `LiveStatus` los objetos proporcionan acceso al estado de ejecución de un `LiveRelationship`. Se utiliza para consultar el estado de sincronización de una Live Copy.

* **`LiveAction`**

   A `LiveAction` es una acción que se ejecuta en cada recurso que participa en la implementación.

   * LiveActions solo las genera RolloutConfigs.

* **`LiveActionFactory`**

   Crea `LiveAction` objetos dados un `LiveAction` configuración. Las configuraciones se almacenan como recursos en el repositorio.

* **`RolloutConfig`**

   La variable `RolloutConfig` contiene una lista de `LiveActions`, que se utilizará cuando se active. La variable `LiveCopy` hereda la variable `RolloutConfig` y el resultado está presente en la variable `LiveRelationship`.

   * La configuración de una Live Copy por primera vez también utiliza un RolloutConfig (que déclencheur LiveActions).

## Creación de una nueva acción de sincronización {#creating-a-new-synchronization-action}

Cree acciones de sincronización personalizadas para utilizarlas con las configuraciones de lanzamiento. Cree una acción de sincronización al [acciones instaladas](/help/sites-administering/msm-sync.md#installed-synchronization-actions) no cumpla los requisitos específicos de la aplicación. Para ello, cree dos clases:

* Una implementación de [ `com.day.cq.wcm.msm.api.LiveAction`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) que realiza la acción.
* Un componente OSGI que implementa el [ `com.day.cq.wcm.msm.api.LiveActionFactory`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) y crea instancias de su `LiveAction` Clase .

La variable `LiveActionFactory` crea instancias del `LiveAction` para una configuración determinada:

* `LiveAction` las clases incluyen los siguientes métodos:

   * `getName`: Devuelve el nombre de la acción El nombre se utiliza para hacer referencia a la acción, por ejemplo en las configuraciones de lanzamiento.
   * `execute`: Realiza las tareas de la acción.

* `LiveActionFactory` las clases incluyen los siguientes miembros:

   * `LIVE_ACTION_NAME`: Campo que contiene el nombre del `LiveAction`. Este nombre debe coincidir con el valor devuelto por la variable `getName` método de la variable `LiveAction` Clase .

   * `createAction`: Crea una instancia de la variable `LiveAction`. La opción `Resource` para proporcionar información de configuración.

   * `createsAction`: Devuelve el nombre del `LiveAction`.

### Acceso al nodo de configuración de LiveAction {#accessing-the-liveaction-configuration-node}

Utilice la variable `LiveAction` nodo de configuración en el repositorio para almacenar información que afecte al comportamiento de tiempo de ejecución del `LiveAction` instancia. El nodo del repositorio que almacena el `LiveAction` la configuración de `LiveActionFactory` en tiempo de ejecución. Por lo tanto, puede agregar propiedades al nodo de configuración a y utilizarlas en su `LiveActionFactory` implementación según sea necesario.

Por ejemplo, una `LiveAction` debe almacenar el nombre del autor del modelo. Una propiedad del nodo de configuración incluye el nombre de propiedad de la página de modelo que almacena la información. Durante el tiempo de ejecución, la variable `LiveAction` recupera el nombre de propiedad de la configuración y, a continuación, obtiene el valor de propiedad.

El parámetro de la variable ` [LiveActionFactory](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html).createAction` es un método `Resource` objeto. Esta `Resource` representa la variable `cq:LiveSyncAction` para esta acción activa en la configuración de lanzamiento; see [Creación de una configuración de lanzamiento](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration). Como de costumbre, al utilizar un nodo de configuración, debe adaptarlo a un `ValueMap` objeto:

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### Acceso a Nodos de Target, Nodos de origen y LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

Los siguientes objetos se proporcionan como parámetros de la variable `execute` método de la variable `LiveAction` objeto:

* A [ `Resource`](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) que representa el origen de Live Copy.
* A `Resource` que representa el destino de Live Copy.
* La variable [ `LiveRelationship`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) para la Live Copy.
* La variable `autoSave` indica si `LiveAction` debe guardar los cambios realizados en el repositorio.

* El valor de restablecimiento indica el modo de restablecimiento de lanzamiento.

Desde estos objetos puede obtener toda la información sobre la variable `LiveCopy`. También puede usar la variable `Resource` objetos que desea obtener `ResourceResolver`, `Session`y `Node` objetos. Estos objetos son útiles para manipular el contenido del repositorio:

En la primera línea del siguiente código, la fuente es el `Resource` objeto de la página de origen:

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>La variable `Resource` los argumentos pueden `null` o `Resources` objetos que no se adaptan a `Node` objetos, como [ `NonExistingResource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/NonExistingResource.html) objetos.

## Creación de una nueva configuración de lanzamiento {#creating-a-new-rollout-configuration}

Cree una configuración de lanzamiento cuando las configuraciones de lanzamiento instaladas no cumplan los requisitos de la aplicación:

* [Crear la configuración de lanzamiento](#create-the-rollout-configuration).
* [Agregar acciones de sincronización a la configuración de lanzamiento](#add-synchronization-actions-to-the-rollout-configuration).

A continuación, la nueva configuración de lanzamiento estará disponible cuando configure las opciones de configuración de lanzamiento en un modelo o una página de Live Copy.

>[!NOTE]
>
>Consulte también la [prácticas recomendadas para personalizar lanzamientos](/help/sites-administering/msm-best-practices.md#customizing-rollouts).

### Crear la configuración de lanzamiento {#create-the-rollout-configuration}

Para crear una nueva configuración de lanzamiento:

1. CRXDE Lite abierto; por ejemplo:
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Vaya a :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >Esta es la versión personalizada de su proyecto de:
   >`/libs/msm/wcm/rolloutconfigs`
   >Si esta es su primera configuración, `/libs` la rama debe utilizarse como plantilla para crear la nueva rama en `/apps`.

   >[!NOTE]
   >
   >No debe cambiar nada en la ruta /libs.
   >Esto se debe a que el contenido de /libs se sobrescribe la próxima vez que actualice la instancia (y puede sobrescribirse al aplicar una corrección o un paquete de funciones).
   >El método recomendado para la configuración y otros cambios es:
   >
   >* Vuelva a crear el elemento requerido (es decir, tal como existe en /libs) en /apps
   >* Realice cambios en /apps


1. En **Crear** un nodo con las siguientes propiedades:

   * **Nombre**: El nombre del nodo de la configuración de lanzamiento. md#installation-synchronization-actions), por ejemplo `contentCopy` o `workflow`.
   * **Tipo**: `cq:RolloutConfig`

1. Agregue las siguientes propiedades a este nodo:
   * **Nombre**: `jcr:title`

      **Tipo**: `String`
      **Valor**: Un título identificativo que aparecerá en la interfaz de usuario.
   * **Nombre**: `jcr:description`

      **Tipo**: `String`
      **Valor**: Una descripción opcional.
   * **Nombre**: `cq:trigger`

      **Tipo**: `String`
      **Valor**: La variable [Desplegar Déclencheur](/help/sites-administering/msm-sync.md#rollout-triggers) para usar. Seleccione entre:
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. Haga clic en **Guardar todo**.

### Agregar acciones de sincronización a la configuración de lanzamiento {#add-synchronization-actions-to-the-rollout-configuration}

Las configuraciones de lanzamiento se almacenan debajo del [nodo de configuración de lanzamiento](#create-the-rollout-configuration) que ha creado en `/apps/msm/<your-project>/rolloutconfigs` nodo .

Agregar nodos secundarios de tipo `cq:LiveSyncAction` para agregar acciones de sincronización a la configuración de lanzamiento. El orden de los nodos de acción de sincronización determina el orden en que se producen las acciones.

1. Todavía en el CRXDE Lite, seleccione su [Configuración de lanzamiento](#create-the-rollout-configuration) nodo .

   Por ejemplo:
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **Crear** un nodo con las siguientes propiedades de nodo:

   * **Nombre**: El nombre del nodo de la acción de sincronización.
El nombre debe ser el mismo que el **Nombre de la acción** en la tabla de [Acciones de sincronización](/help/sites-administering/msm-sync.md#installed-synchronization-actions), por ejemplo `contentCopy` o `workflow`.
   * **Tipo**: `cq:LiveSyncAction`

1. Añada y configure todos los nodos de acción de sincronización que necesite. Reorganice los nodos de acción para que su orden coincida con el orden en que desea que se produzcan. El nodo de acción superior se produce primero.

## Creación y uso de una clase simple LiveActionFactory {#creating-and-using-a-simple-liveactionfactory-class}

Siga los procedimientos de esta sección para desarrollar un `LiveActionFactory` y utilícelo en una configuración de lanzamiento. Los procedimientos utilizan Maven y Eclipse para desarrollar e implementar el `LiveActionFactory`:

1. [Creación del proyecto maven](#create-the-maven-project) e impórtelos en Eclipse.
1. [Añadir dependencias](#add-dependencies-to-the-pom-file) al archivo POM.
1. [Implementación de `LiveActionFactory` interfaz](#implement-liveactionfactory) e implemente el paquete OSGi.
1. [Crear la configuración de lanzamiento](#create-the-example-rollout-configuration).
1. [Crear la Live Copy](#create-the-live-copy).

El proyecto Maven y el código fuente de la clase Java están disponibles en el repositorio Git público.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto experience emanager-java-msmrollout en GitHub](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### Creación del proyecto Maven {#create-the-maven-project}

El siguiente procedimiento requiere que haya agregado el perfil adobe-public al archivo de configuración de Maven.

* Para obtener información sobre el perfil adobe-public, consulte [Obtención del complemento Maven del paquete de contenido](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* Para obtener información sobre el archivo de configuración de Maven, consulte Maven [Referencia de ajustes](https://maven.apache.org/settings.html).

1. Abra un terminal o una sesión de línea de comandos y cambie el directorio para que apunte a la ubicación donde crear el proyecto.
1. Introduzca el siguiente comando:

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. Especifique los siguientes valores en el mensaje interactivo:

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`: `MyLiveActionFactory`
   * `version`: `1.0-SNAPSHOT`
   * `package`: `MyPackage`
   * `appsFolderName`: `myapp`
   * `artifactName`: `MyLiveActionFactory package`
   * `packageGroup`: `myPackages`

1. Inicie Eclipse y [importación del proyecto Maven](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse).

### Añadir dependencias al archivo POM {#add-dependencies-to-the-pom-file}

Agregue dependencias para que el compilador de Eclipse pueda hacer referencia a las clases que se utilizan en la variable `LiveActionFactory` código.

1. En el Explorador de proyectos de Eclipse, abra el archivo :

   `MyLiveActionFactory/pom.xml`

1. En el editor, haga clic en la `pom.xml` y busque `project/dependencyManagement/dependencies` para obtener más información.
1. Añada el siguiente XML dentro del `dependencyManagement` y, a continuación, guarde el archivo.

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. Abra el archivo POM para el paquete desde **Explorador de proyectos** at `MyLiveActionFactory-bundle/pom.xml`.
1. En el editor, haga clic en la `pom.xml` y busque la sección proyecto/dependencias . Añada el siguiente XML dentro del elemento dependencias y, a continuación, guarde el archivo:

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### Implementación de LiveActionFactory {#implement-liveactionfactory}

Lo siguiente `LiveActionFactory` la clase implementa un `LiveAction` que registra mensajes sobre las páginas de origen y de destino, y copia la variable `cq:lastModifiedBy` propiedad del nodo de origen al nodo de destino. El nombre de la acción activa es `exampleLiveAction`.

1. En el Explorador de proyectos de Eclipse, haga clic con el botón derecho en el `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` paquete y haga clic en **Nuevo** > **Clase**. Para la variable **Nombre**, introduzca `ExampleLiveActionFactory` y haga clic en **Finalizar**.
1. Abra el `ExampleLiveActionFactory.java` reemplace el contenido por el siguiente código y guarde el archivo.

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. Utilizando el terminal o la sesión de comandos, cambie el directorio a la `MyLiveActionFactory` (el directorio del proyecto Maven). A continuación, introduzca el siguiente comando:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   El AEM `error.log` debe indicar que el paquete se ha iniciado.

   Por ejemplo, [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs).

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### Creación de la configuración de lanzamiento de ejemplo {#create-the-example-rollout-configuration}

Cree la configuración de lanzamiento de MSM que use el `LiveActionFactory` que ha creado:

1. Cree y configure un [Configuración de lanzamiento con el procedimiento estándar](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) - y utilizando las propiedades:

   * **Título**: Ejemplo de configuración de lanzamiento
   * **Nombre**: examplerolloutconfig
   * **cq:déclencheur**: `publish`

### Añadir la acción activa a la configuración de lanzamiento de ejemplo {#add-the-live-action-to-the-example-rollout-configuration}

Configure la configuración de lanzamiento que creó en el procedimiento anterior para que utilice el `ExampleLiveActionFactory` Clase .

1. CRXDE Lite abierto; por ejemplo, [https://localhost:4502/crx/de](https://localhost:4502/crx/de).
1. Cree el siguiente nodo en `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **Nombre**: `exampleLiveAction`
   * **Tipo**: `cq:LiveSyncAction`

1. Haga clic en **Guardar todo**.
1. Seleccione el `exampleLiveAction` y agregue la siguiente propiedad:

   * **Nombre**: `repLastModBy`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

   Esta propiedad indica que `ExampleLiveAction` que el `cq:LastModifiedBy` La propiedad de debe replicarse desde el origen al nodo de destino.

1. Haga clic en **Guardar todo**.

### Creación de Live Copy {#create-the-live-copy}

[Crear una Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) de la rama Inglés/Productos del sitio de referencia We.Retail utilizando la configuración de lanzamiento:

* **Origen**: `/content/we-retail/language-masters/en/products`

* **Configuración de lanzamiento**: Ejemplo de configuración de lanzamiento

Active la variable **Productos** (en inglés) de la rama de origen y observe los mensajes de registro que la variable `LiveAction` genera la clase:

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

<!--
## Removing the Chapters Step in the Create Site Wizard {#removing-the-chapters-step-in-the-create-site-wizard}

In some cases, the **Chapters** selection is not required in the create site wizard (only the **Languages** selection is required). To remove this step in the default We.Retail English blueprint:

1. In CRX Explorer, remove the node:
   `/etc/blueprints/weretail-english/jcr:content/dialog/items/tabs/items/tab_chap`.

1. Navigate to `/libs/wcm/msm/templates/blueprint/defaults/livecopy_tab/items` and create a new node:

    1. **Name** = `chapters`; **Type** = `cq:Widget`.

1. Add following properties to the new node:

    1. **Name** = `name`; **Type** = `String`; **Value** = `msm:chapterPages`

    1. **Name** = `value`; **Type** = `String`; **Value** = `all`

    1. **Name** = `xtype`; **Type** = `String`; **Value** = `hidden`
-->

## Cambio de los nombres de idioma y los países predeterminados {#changing-language-names-and-default-countries}

AEM utiliza un conjunto predeterminado de códigos de idioma y de país.

* El código de idioma predeterminado es el código de dos letras en minúscula definido por ISO-639-1.
* El código de país predeterminado es el código de dos letras en minúsculas o mayúsculas, tal como se define en la norma ISO 3166.

MSM utiliza una lista almacenada de códigos de idioma y de país para determinar el nombre del país asociado con el nombre de la versión de idioma de la página. Si es necesario, puede cambiar los siguientes aspectos de la lista:

* Títulos de idioma
* Nombres de países
* Países predeterminados para idiomas (para códigos como `en`, `de`, entre otros)

La lista de idiomas se almacena debajo de la variable `/libs/wcm/core/resources/languages` nodo . Cada nodo secundario representa un idioma o un país de idioma:

* El nombre del nodo es el código de idioma (por ejemplo, `en` o `de`) o el código language_country (como `en_us` o `de_ch`).

* La variable `language` la propiedad del nodo almacena el nombre completo del idioma para el código.
* La variable `country` la propiedad del nodo almacena el nombre completo del país para el código.
* Cuando el nombre del nodo solo consta de un código de idioma (como `en`), la propiedad country es `*`y un `defaultCountry` almacena el código del país-idioma para indicar el país que se va a usar.

![chlimage_1-76](assets/chlimage_1-76.png)

Para modificar los idiomas:

1. Abra el CRXDE Lite en el explorador web; por ejemplo, [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. Seleccione el `/apps` carpeta y haga clic en **Crear**, luego **Crear carpeta.**

   Asigne un nombre a la nueva carpeta `wcm`.

1. Repita el paso anterior para crear la variable `/apps/wcm/core` árbol de carpetas. Crear un nodo de tipo `sling:Folder` en `core` llamado `resources`. <!-- ![chlimage_1-77](assets/chlimage_1-77.png) -->

1. Haga clic con el botón derecho en el `/libs/wcm/core/resources/languages` nodo y haga clic en **Copiar**.
1. Haga clic con el botón derecho en el `/apps/wcm/core/resources` carpeta y haga clic en **Pegar**. Modifique los nodos secundarios según sea necesario.
1. Haga clic en **Guardar todo**.
1. Haga clic en **Herramientas**, **Operaciones** then **Consola web**. Desde esta consola, haga clic en **OSGi**, luego **Configuración**.
1. Busque y haga clic en **Day CQ WCM Language Manager** y cambie el valor de **Lista de idiomas** a `/apps/wcm/core/resources/languages`y haga clic en **Guardar**.

   ![chlimage_1-78](assets/chlimage_1-78.png)

## Configuración de bloqueos MSM en propiedades de página (IU táctil) {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

Al crear una propiedad de página personalizada, es posible que tenga que considerar si la nueva propiedad puede implementarse en cualquier Live Copy.

Por ejemplo, si se agregan dos propiedades de página nuevas:

* Correo electrónico de contacto:

   * No es necesario desplegar esta propiedad, ya que será diferente en cada país (o marca, etc.).

* Estilo visual clave:

   * El requisito del proyecto es que esta propiedad se implemente ya que es (normalmente) común a todos los países (o marcas, etc.).

A continuación, debe asegurarse de que:

* Correo electrónico de contacto:

* Se excluye de las propiedades desplegadas; see [Exclusión de propiedades y tipos de nodo de la sincronización](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization).

* Estilo visual clave:

* Asegúrese de que no puede editar esta propiedad en la interfaz de usuario táctil a menos que se cancele la herencia y de que, a continuación, pueda restablecer la herencia; esto se controla haciendo clic en los vínculos de cadena/cadena rota que alternan para indicar el estado de la conexión.

Si una propiedad de página está sujeta a implementación y, por lo tanto, sujeta a cancelación o restablecimiento de la herencia al editar, está controlada por la propiedad dialog :

* `cq-msm-lockable`

   * es aplicable a los elementos del cuadro de diálogo IU táctil
   * creará el símbolo de vínculo de cadena en el cuadro de diálogo
   * solo permite la edición si se cancela la herencia (el vínculo de cadena está roto)
   * solo se aplica al primer nivel secundario del recurso
      * **Tipo**: `String`

      * **Valor**: contiene el nombre de la propiedad en cuestión (y es comparable al valor de la propiedad) `name`; por ejemplo, consulte
         `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

When `cq-msm-lockable` se ha definido, romper/cerrar la cadena interactuará con MSM de la siguiente manera:

* si el valor de `cq-msm-lockable` es:

   * **Relativo** (p. ej. `myProperty` o `./myProperty`)

      * agregará y quitará la propiedad de `cq:propertyInheritanceCancelled`.
   * **Absoluto** (p. ej. `/image`)

      * al romper la cadena, se cancelará la herencia añadiendo la variable `cq:LiveSyncCancelled` mezcla a `./image` y configuración `cq:isCancelledForChildren` a `true`.

      * cerrar la cadena revertirá la herencia.


>[!NOTE]
>
>`cq-msm-lockable` se aplica al primer nivel secundario del recurso que se va a editar y no funciona en ningún antecesor de nivel más profundo independientemente de si el valor se define como absoluto o relativo.

>[!NOTE]
>
>Al volver a habilitar la herencia, la propiedad de la página de Live Copy no se sincroniza automáticamente con la propiedad de origen. Puede solicitar manualmente una sincronización si es necesario.
