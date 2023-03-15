---
title: AEM Usuarios de servicio en
seo-title: Service Users in AEM
description: AEM Obtenga información acerca de los usuarios de servicio en.
seo-description: Learn about Service Users in AEM.
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Security
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 0%

---

# AEM Usuarios de servicio en{#service-users-in-aem}

## Información general {#overview}

AEM La forma principal de obtener un solucionador de sesión administrativa o de recursos en la aplicación de era usando el método de resolución de recursos de la aplicación de la aplicación de la. `SlingRepository.loginAdministrative()` y `ResourceResolverFactory.getAdministrativeResourceResolver()` métodos proporcionados por Sling.

Sin embargo, ninguno de estos métodos se diseñó en torno a la [principio de menor privilegio](https://en.wikipedia.org/wiki/Principle_of_least_privilege) y facilitar al desarrollador la tarea de no planificar una estructura adecuada y los niveles de control de acceso (ACL) correspondientes para su contenido desde el principio. Si una vulnerabilidad está presente en un servicio de este tipo, a menudo conduce a escalaciones de privilegios a `admin` usuario, incluso si el código en sí no necesita privilegios administrativos para funcionar.

## Cómo eliminar gradualmente las sesiones de administración {#how-to-phase-out-admin-sessions}

### Prioridad 0: ¿La función está activa/necesaria/abandonada? {#priority-is-the-feature-active-needed-derelict}

Puede haber casos en los que no se utilice la sesión de administración o en los que la función esté completamente deshabilitada. Si este es el caso de la implementación, asegúrese de eliminar por completo la función o de ajustarla con [código NOP](https://en.wikipedia.org/wiki/NOP).

### Prioridad 1: Utilizar La Sesión De Solicitud {#priority-use-the-request-session}

Siempre que sea posible, refactorice la función para que la sesión de solicitud autenticada dada se pueda utilizar para leer o escribir contenido. Si esto no es factible, a menudo se puede lograr aplicando las prioridades siguientes a las siguientes.

### Prioridad 2: Reestructurar contenido {#priority-restructure-content}

Muchos problemas se pueden resolver reestructurando el contenido. Tenga en cuenta estas reglas sencillas al realizar la reestructuración:

* **Cambiar control de acceso**

   * Asegúrese de que los usuarios o grupos que realmente necesitan acceso tengan acceso;

* **Refinamiento de la estructura de contenido**

   * Muévalo a otras ubicaciones, por ejemplo, donde el control de acceso coincida con las sesiones de solicitud disponibles;
   * Cambiar la granularidad del contenido;

* **Refactorice su código para que sea un servicio adecuado**

   * Cambie la lógica empresarial del código JSP al servicio. Esto permite modelar contenido de forma diferente.

Además, asegúrese de que todas las nuevas funciones que desarrolle se ajusten a estos principios:

* **Los requisitos de seguridad deben orientar la estructura de contenido**

   * La gestión del control de acceso debería ser natural
   * El control de acceso lo debe aplicar el repositorio, no la aplicación

* **Utilizar tipos de nodos**

   * Restringir el conjunto de propiedades que se pueden establecer

* **Respetar la configuración de privacidad**

   * En el caso de los perfiles privados, un ejemplo sería no exponer la imagen del perfil, el correo electrónico o el nombre completo que se encuentra en el perfil privado `/profile` nodo.

## Estricto control de acceso {#strict-access-control}

Tanto si aplica el control de acceso al reestructurar el contenido como si lo hace para un nuevo usuario de servicio, debe aplicar las ACL más estrictas posibles. Utilice todas las posibilidades de control de acceso:

* Por ejemplo, en lugar de aplicar `jcr:read` el `/apps`, solo aplíquelo a `/apps/*/components/*/analytics`

* Uso [restricciones](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* Aplicar ACL para los tipos de nodo
* Limitar permisos

   * por ejemplo, cuando solo necesite escribir propiedades, no asigne el valor `jcr:write` permiso; uso `jcr:modifyProperties` en su lugar

## Usuarios de servicio y asignaciones {#service-users-and-mappings}

Si lo anterior falla, Sling 7 ofrece un servicio de asignación de usuarios de servicio, que permite configurar una asignación de paquete a usuario y dos métodos de API correspondientes: ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` y ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` que devuelven un solucionador de sesión/recurso con los privilegios de un usuario configurado solamente. Estos métodos tienen las siguientes características:

* Permiten asignar servicios a los usuarios
* Permiten definir a los usuarios de subservicios
* El punto de configuración central es: `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [ &quot;:&quot; nombre-subservicio ] 

* `service-id` está asignado a un solucionador de recursos o a un ID de usuario del repositorio JCR para la autenticación
* `service-name` es el nombre simbólico del paquete que proporciona el servicio

## Otros Recommendations {#other-recommendations}

### Reemplazar la sesión de administración por un usuario de servicio {#replacing-the-admin-session-with-a-service-user}

Un usuario de servicio es un usuario de JCR sin contraseña establecida y con un conjunto mínimo de privilegios necesarios para realizar una tarea específica. Si no se ha establecido ninguna contraseña, no será posible iniciar sesión con un usuario del servicio.

Una forma de dejar de utilizar una sesión administrativa es reemplazarla por sesiones de usuarios de servicio. También podría reemplazarse con varios usuarios de subservicios si es necesario.

Para reemplazar la sesión de administración por un usuario de servicio, debe realizar los siguientes pasos:

1. Identifique los permisos necesarios para su servicio, teniendo en cuenta el principio de permisos mínimos.
1. Compruebe si ya hay un usuario disponible con exactamente la configuración de permisos que necesita. Cree un nuevo usuario de servicio del sistema si ningún usuario existente coincide con sus necesidades. RTC es necesario para crear un nuevo usuario de servicio. A veces, tiene sentido crear varios usuarios de subservicios (por ejemplo, uno para escribir y otro para leer) para compartimentar el acceso aún más.
1. Configure y pruebe los ACE para el usuario.
1. Añadir un `service-user` asignación para el servicio y para `user/sub-users`

1. Ponga a disposición del paquete la función de usuario de servicio sling: actualice a la versión más reciente de. `org.apache.sling.api`.

1. Reemplace el `admin-session` en el código con la variable `loginService` o `getServiceResourceResolver` API.

## Creación de un nuevo usuario de servicio {#creating-a-new-service-user}

AEM Después de comprobar que no hay ningún usuario en la lista de usuarios del servicio de aplicable a su caso de uso y de aprobar los problemas de RTC correspondientes, puede continuar y agregar el nuevo usuario al contenido predeterminado.

El método recomendado es crear un usuario de servicio para utilizar el explorador de repositorios en *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*

El objetivo es obtener un válido `jcr:uuid` propiedad que es obligatoria para crear el usuario a través de la instalación de un paquete de contenido.

Puede crear usuarios de servicios de:

1. Ir al explorador de repositorios en *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. Iniciar sesión como administrador presionando la tecla **Iniciar sesión** en la esquina superior izquierda de la pantalla.
1. A continuación, cree y asigne un nombre al usuario del sistema. Para crear el usuario como uno del sistema, establezca la ruta intermedia como `system` y agregue subcarpetas opcionales según sus necesidades:

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Compruebe que el nodo de usuario del sistema tenga el siguiente aspecto:

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >Tenga en cuenta que no hay tipos de mezcla asociados a usuarios de servicios. Esto significa que no habrá políticas de control de acceso para los usuarios del sistema.

Al agregar el archivo .content.xml correspondiente al contenido del paquete, asegúrese de haber establecido el `rep:authorizableId` y que el tipo principal es `rep:SystemUser`. Debería tener un aspecto similar al siguiente:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Agregar una modificación de configuración a la configuración de ServiceUserMapper {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Para añadir una asignación desde el servicio a los usuarios del sistema correspondientes, debe crear una configuración de fábrica para ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)` servicio. Para mantener esta configuración modular, se pueden proporcionar estas configuraciones utilizando el [Mecanismo de modificación de Sling](https://issues.apache.org/jira/browse/SLING-3578). La forma recomendada de instalar estas configuraciones con el paquete es mediante [Cargando contenido inicial de Sling](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. Cree una subcarpeta SLING-INF/content debajo de la carpeta src/main/resources del paquete
1. En esta carpeta, cree un archivo llamado org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.modified-&lt;some unique=&quot;&quot; name=&quot;&quot; for=&quot;&quot; your=&quot;&quot; factory=&quot;&quot; configuration=&quot;&quot;>.xml con el contenido de la configuración de fábrica (incluidas todas las asignaciones de usuario de subservicio). Ejemplo:

1. Crear un `SLING-INF/content` carpeta debajo de `src/main/resources` carpeta de su paquete;
1. En esta carpeta, cree un archivo `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` con el contenido de la configuración de fábrica, incluidas todas las asignaciones de usuario de subservicio.

   Para ilustrar, tome un archivo llamado `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. Hacer referencia al contenido inicial de Sling en la configuración del `maven-bundle-plugin` en el `pom.xml` de su paquete. Ejemplo:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Instale el paquete y asegúrese de que se ha instalado la configuración de fábrica. Para ello:

   * Vaya a la consola web en *https://serverhost:serveraddress/system/console/configMgr*
   * Buscar por **Modificación del servicio del asignador de usuarios del servicio Apache Sling**
   * Haga clic en el vínculo para ver si se ha implementado la configuración adecuada.

## Tratar sesiones compartidas en servicios {#dealing-with-shared-sessions-in-services}

Llamadas a `loginAdministrative()` a menudo aparecen junto con sesiones compartidas. Estas sesiones se adquieren al activarse el servicio y solo se cierran después de que este se detiene. Aunque esta es una práctica común, conduce a dos problemas:

* **Seguridad:** Estas sesiones de administración se utilizan para almacenar en caché y devolver recursos u otros objetos enlazados a la sesión compartida. Más adelante en la pila de llamadas, estos objetos podrían adaptarse a sesiones o solucionadores de recursos con privilegios elevados y, a menudo, el llamador no tiene claro que esté operando en una sesión de administrador.
* **Rendimiento:** En Oak, las sesiones compartidas pueden causar problemas de rendimiento y, actualmente, no se recomienda utilizarlas.

La solución más obvia para el riesgo de seguridad es simplemente reemplazar el `loginAdministrative()` llamada con a `loginService()` una a un usuario con privilegios restringidos. Sin embargo, esto no tendrá ningún impacto en ninguna degradación potencial del rendimiento. Una posibilidad de mitigar que es envolver toda la información solicitada en un objeto que no tiene asociación con la sesión. A continuación, cree (o destruya) la sesión bajo demanda.

El método recomendado es refactorizar la API del servicio para dar al que llama control sobre la creación o destrucción de la sesión.

## Sesiones administrativas en JSP {#administrative-sessions-in-jsps}

Los JSP no pueden usar `loginService()`, porque no hay ningún servicio asociado. Sin embargo, las sesiones administrativas en los JSP suelen ser un signo de una violación del paradigma de MVC.

Esto se puede solucionar de dos maneras:

1. Reestructurar el contenido de manera que permita manipularlo con la sesión del usuario;
1. Extraer la lógica a un servicio que proporciona una API que luego JSP puede utilizar.

El primer método es el preferido.

## Procesamiento de eventos, preprocesadores de replicación y trabajos {#processing-events-replication-preprocessors-and-jobs}

Al procesar eventos o trabajos, y en algunos casos flujos de trabajo, la sesión correspondiente que activó el evento generalmente se pierde. Esto lleva a que los controladores de eventos y los procesadores de trabajos a menudo utilicen sesiones administrativas para realizar su trabajo. Existen diferentes enfoques concebibles para resolver este problema, cada uno con sus ventajas y desventajas:

1. Pase el `user-id` en la carga útil de evento y utilice la suplantación.

   **Ventajas:** Fácil de usar.

   **Desventajas:** Sigue usando `loginAdministrative()`. Vuelve a autenticar una solicitud que ya se ha autenticado.

1. Crear o reutilizar un usuario de servicio que tenga acceso a los datos.

   **Ventajas:** Compatible con el diseño actual. Necesita un cambio mínimo.

   **Desventajas:** Necesita usuarios de servicios muy poderosos para ser flexible, lo que puede llevar fácilmente a escalados de privilegios. Elude el modelo de seguridad.

1. Pasar una serialización de `Subject` en la carga útil de evento y cree un `ResourceResolver` basado en ese tema. Un ejemplo sería el uso del JAAS `doAsPrivileged` en el `ResourceResolverFactory`.

   **Ventajas:** Una implementación limpia desde el punto de vista de la seguridad. Evita la reautenticación y funciona con los privilegios originales. El código relevante para la seguridad es transparente para el consumidor del evento.

   **Desventajas:** Necesita refactorización. El hecho de que el código relevante para la seguridad sea transparente para el consumidor del evento también puede provocar problemas.

El tercer enfoque es actualmente la técnica de procesamiento preferida.

## Procesos de flujo de trabajo {#workflow-processes}

Dentro de las implementaciones de procesos de flujo de trabajo, la sesión de usuario correspondiente que activó el flujo de trabajo generalmente se pierde. Esto lleva a procesos de flujo de trabajo que a menudo utilizan sesiones administrativas para realizar su trabajo.

Para solucionar estos problemas, se recomienda que los mismos enfoques mencionados en [Procesamiento de eventos, preprocesadores de replicación y trabajos](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) se utilizará.

## Procesadores de POST Sling y páginas eliminadas {#sling-post-processors-and-deleted-pages}

Hay un par de sesiones administrativas que se utilizan en las implementaciones de POST de Sling. Normalmente, las sesiones administrativas se utilizan para acceder a nodos cuya eliminación está pendiente dentro del POST que se está procesando. En consecuencia, ya no están disponibles a través de la sesión de solicitud. Se puede acceder a un nodo pendiente de eliminación para revelar la metáfora que, de lo contrario, no debería ser accesible.
