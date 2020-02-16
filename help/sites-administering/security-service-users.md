---
title: Usuarios de servicio en AEM
seo-title: Usuarios de servicio en AEM
description: Obtenga información sobre los usuarios de servicios en AEM.
seo-description: Obtenga información sobre los usuarios de servicios en AEM.
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Usuarios de servicio en AEM{#service-users-in-aem}

## Información general {#overview}

La forma principal de obtener una sesión administrativa o resolución de recursos en AEM era utilizando los métodos `SlingRepository.loginAdministrative()` y `ResourceResolverFactory.getAdministrativeResourceResolver()` proporcionados por Sling.

Sin embargo, ninguno de estos métodos se diseñó en torno al [principio del menor privilegio](https://en.wikipedia.org/wiki/Principle_of_least_privilege) y hace que sea demasiado fácil para un desarrollador no planificar una estructura adecuada y los correspondientes Niveles de control de acceso (ACL) para su contenido desde el principio. Si una vulnerabilidad está presente en un servicio de este tipo, a menudo lleva a una escalación de privilegios para el usuario, incluso si el código mismo no necesita privilegios administrativos para funcionar. `admin`

## Cómo eliminar gradualmente las sesiones de administración {#how-to-phase-out-admin-sessions}

### Prioridad 0: ¿La función está activa/necesitada/es obsoleta? {#priority-is-the-feature-active-needed-derelict}

Puede haber casos en los que la sesión de administración no se utilice o la función esté totalmente deshabilitada. Si este es el caso con la implementación, asegúrese de eliminar la función por completo o de ajustarla al código [](https://en.wikipedia.org/wiki/NOP)NOP.

### Prioridad 1: Utilizar La Sesión De Solicitud {#priority-use-the-request-session}

Siempre que sea posible, redimensione la función para que la sesión de solicitud determinada y autenticada pueda utilizarse para leer o escribir contenido. Si esto no es factible, a menudo se puede lograr aplicando las prioridades que siguen a las que figuran a continuación.

### Prioridad 2: Reestructurar contenido {#priority-restructure-content}

Muchos problemas pueden resolverse reestructurando el contenido. Tenga en cuenta estas reglas sencillas al realizar la reestructuración:

* **Cambiar control de acceso**

   * Asegúrese de que los usuarios o grupos a los que realmente se necesita acceso tienen acceso;

* **Restringir la estructura de contenido**

   * Muévalo a otras ubicaciones, por ejemplo, donde el control de acceso coincida con las sesiones de solicitud disponibles;
   * Cambiar la granularidad del contenido;

* **Redimensionar el código para que sea un servicio adecuado**

   * Mueva la lógica empresarial del código JSP al servicio. Esto permite un modelo de contenido diferente.

Además, asegúrese de que todas las nuevas funciones que desarrolle se adhieran a estos principios:

* **Los requisitos de seguridad deben impulsar la estructura de contenido**

   * La administración del control de acceso debe sentirse natural
   * El repositorio debe aplicar el control de acceso, no la aplicación

* **Uso de tipos de nodos**

   * Restringir el conjunto de propiedades que se pueden definir

* **Respetar la configuración de privacidad**

   * En el caso de perfiles privados, un ejemplo sería no exponer la imagen de perfil, el correo electrónico o el nombre completo que se encuentra en el `/profile` nodo privado.

## Control de acceso estricto {#strict-access-control}

Tanto si aplica el control de acceso durante la reestructuración del contenido como si lo hace para un nuevo usuario de servicios, debe aplicar las ACL más estrictas posibles. Utilizar todas las instalaciones posibles para el control de acceso:

* Por ejemplo, en lugar de aplicar `jcr:read` en `/apps`, aplique solo a `/apps/*/components/*/analytics`

* Use [restrictions](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* Aplicar ACL para tipos de nodo
* Limitar permisos

   * por ejemplo, cuando solo necesite escribir propiedades, no conceda el `jcr:write` permiso; usar `jcr:modifyProperties`

## Usuarios y asignaciones de servicios {#service-users-and-mappings}

Si falla lo anterior, Sling 7 ofrece un servicio de Asignación de usuarios de servicios, que permite configurar una asignación de paquete a usuario y dos métodos de API correspondientes: ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` y ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` que devuelven una resolución de sesión/recurso con los privilegios de un usuario configurado solamente. Estos métodos tienen las características siguientes:

* Permiten los servicios de asignación a los usuarios
* Permiten definir usuarios de subservicios
* El punto de configuración central es: `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [ &quot;:&quot; subservice-name ] 

* `service-id` se asigna a un identificador de usuario de la autenticación de la resolución de recursos o del repositorio JCR
* `service-name` es el nombre simbólico del paquete que proporciona el servicio

## Otras recomendaciones {#other-recommendations}

### Sustitución de la sesión de administración por un usuario de servicio {#replacing-the-admin-session-with-a-service-user}

Un usuario de servicio es un usuario de JCR sin contraseña establecida y con un conjunto mínimo de privilegios necesarios para realizar una tarea específica. No tener una contraseña configurada significa que no será posible iniciar sesión con un usuario de servicio.

Una manera de desactivar una sesión administrativa es reemplazarla por sesiones de usuario de servicio. También podría ser reemplazado por varios usuarios de subservicios si fuera necesario.

Para reemplazar la sesión de administración por un usuario de servicio, debe realizar los siguientes pasos:

1. Identifique los permisos necesarios para su servicio, teniendo en cuenta el principio de mínimo permiso.
1. Compruebe si ya hay un usuario disponible con la configuración de permisos exacta que necesita. Cree un nuevo usuario del servicio del sistema si ningún usuario existente coincide con sus necesidades. RTC es necesario para crear un nuevo usuario de servicio. A veces, tiene sentido crear varios usuarios de subservicios (por ejemplo, uno para escritura y otro para lectura) para compartimentar el acceso aún más.
1. Configure y pruebe las ACE para su usuario.
1. Agregar una `service-user` asignación para el servicio y para `user/sub-users`

1. Ponga la función de sling del usuario del servicio a disposición del paquete: actualizar a la versión más reciente de `org.apache.sling.api`.

1. Reemplace el `admin-session` código con las `loginService` o `getServiceResourceResolver` API.

## Creación de un nuevo usuario de servicio {#creating-a-new-service-user}

Una vez verificado que ningún usuario de la lista de usuarios del servicio AEM es aplicable a su caso de uso y que se han aprobado los problemas de RTC correspondientes, puede continuar y agregar el nuevo usuario al contenido predeterminado.

El método recomendado es crear un usuario de servicio para utilizar el explorador del repositorio en *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*

El objetivo es obtener una `jcr:uuid` propiedad válida que sea obligatoria para crear al usuario a través de una instalación de paquete de contenido.

Puede crear usuarios de servicios mediante:

1. Ir al explorador del repositorio en *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. Para iniciar sesión como administrador, presione el vínculo **Iniciar sesión** en la esquina superior izquierda de la pantalla.
1. A continuación, cree y asigne un nombre al usuario del sistema. Para crear un usuario como sistema, defina la ruta intermedia como `system` y agregue subcarpetas opcionales según sus necesidades:

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Compruebe que el nodo de usuario del sistema tenga el siguiente aspecto:

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >Tenga en cuenta que no hay tipos de mezcla asociados con los usuarios de servicios. Esto significa que no habrá directivas de control de acceso para los usuarios del sistema.

Al agregar el archivo .content.xml correspondiente al contenido del paquete, asegúrese de haber establecido el `rep:authorizableId` y de que el tipo principal es `rep:SystemUser`. Debería tener este aspecto:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Adición de una modificación de configuración a la configuración de ServiceUserMapper {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Para agregar una asignación desde el servicio a los usuarios del sistema correspondientes, debe crear una configuración de fábrica para el ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)` servicio. Para mantener este módulo, estas configuraciones se pueden proporcionar usando el mecanismo [de modificación de](https://issues.apache.org/jira/browse/SLING-3578)Sling. La forma recomendada de instalar estas configuraciones con el paquete es mediante la carga [inicial de contenido de](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html)Sling:

1. Cree una subcarpeta SLING-INF/content debajo de la carpeta src/main/resources del paquete
1. En esta carpeta, cree un archivo llamado org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.modified-&lt;nombre exclusivo para la configuración de fábrica>.xml con el contenido de la configuración de fábrica (incluidas todas las asignaciones de usuarios de subservicios). Ejemplo:

1. Cree una `SLING-INF/content` carpeta debajo de la `src/main/resources` carpeta del paquete;
1. En esta carpeta, cree un archivo `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` con el contenido de la configuración de fábrica, incluidas todas las asignaciones de usuarios de subservicios.

   Para fines ilustrativos, utilice un archivo llamado `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

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

1. Haga referencia al contenido inicial de Sling en la configuración del `maven-bundle-plugin` en la `pom.xml` del paquete. Ejemplo:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Instale el paquete y asegúrese de que se ha instalado la configuración de fábrica. Puede hacerlo mediante:

   * Ir a la consola web en *https://serverhost:serveraddress/system/console/configMgr*
   * Búsqueda de la modificación del servicio de **asignación de usuarios del servicio Apache Sling**
   * Haga clic en el vínculo para ver si la configuración correcta está en su lugar.

## Tratamiento de sesiones compartidas en servicios {#dealing-with-shared-sessions-in-services}

Las llamadas a `loginAdministrative()` menudo aparecen junto con las sesiones compartidas. Estas sesiones se adquieren al activar el servicio y solo se cierran después de que se detenga el servicio. Aunque esta es una práctica común, lleva a dos problemas:

* **** Seguridad: Estas sesiones de administración se utilizan para almacenar en caché y devolver recursos u otros objetos enlazados a la sesión compartida. Más adelante, en la pila de llamadas, estos objetos se pueden adaptar a sesiones o a los solucionadores de recursos con privilegios elevados, y a menudo el llamador no tiene claro que se trata de una sesión de administración con la que están trabajando.
* **** Rendimiento: En Oak, las sesiones compartidas pueden causar problemas de rendimiento y actualmente no se recomienda usarlos.

La solución más obvia para el riesgo de seguridad es simplemente reemplazar la `loginAdministrative()` llamada con una `loginService()` a un usuario con privilegios restringidos. Sin embargo, esto no tendrá ningún efecto en ninguna posible degradación del rendimiento. Una posibilidad de mitigar esto es incluir toda la información solicitada en un objeto que no esté asociado a la sesión. A continuación, cree (o destruya) la sesión a petición.

El método recomendado es reconsiderar la API del servicio para otorgar al llamante control sobre la creación/destrucción de la sesión.

## Sesiones administrativas en JSP {#administrative-sessions-in-jsps}

Los JSP no pueden usar `loginService()`, ya que no hay ningún servicio asociado. Sin embargo, las sesiones administrativas en los JSP suelen ser un signo de violación del paradigma de MVC.

Esto se puede corregir de dos maneras:

1. Reestructurar el contenido de manera que permita manipularlo con la sesión del usuario;
1. Extracción de la lógica a un servicio que proporciona una API que luego puede utilizar el JSP.

El primer método es el preferido.

## Eventos de procesamiento, preprocesadores de replicación y trabajos {#processing-events-replication-preprocessors-and-jobs}

Cuando se procesan eventos o trabajos y, en algunos casos, flujos de trabajo, la sesión correspondiente que activó el evento generalmente se pierde. Esto lleva a que los administradores de eventos y los procesadores de trabajos a menudo utilicen sesiones administrativas para realizar su trabajo. Existen diferentes enfoques concebibles para resolver este problema, cada uno con sus ventajas y desventajas:

1. Pase la carga útil del `user-id` evento y utilice la suplantación.

   **** Ventajas: Fácil de usar.

   **** Desventajas: Todavía utiliza `loginAdministrative()`. Vuelve a autenticar una solicitud que ya se ha autenticado.

1. Cree o reutilice un usuario de servicios que tenga acceso a los datos.

   **** Ventajas: Coherente con el diseño actual. Necesita un cambio mínimo.

   **** Desventajas: Necesita usuarios de servicios muy poderosos para ser flexibles, lo que puede llevar fácilmente a escalaciones de privilegios. Elude el modelo de seguridad.

1. Pase una serialización de la `Subject` en la carga útil del evento y cree una `ResourceResolver` en función de ese asunto. Un ejemplo sería el uso del JAAS `doAsPrivileged` en el `ResourceResolverFactory`.

   **** Ventajas: Implementación limpia desde un punto de vista de seguridad. Evita la reautenticación y funciona con los privilegios originales. El código relevante para la seguridad es transparente para el consumidor del evento.

   **** Desventajas: Necesita refactorización. El hecho de que el código pertinente para la seguridad sea transparente para el consumidor del suceso también podría generar problemas.

El tercer método es actualmente la técnica de procesamiento preferida.

## Procesos de flujo de trabajo {#workflow-processes}

En implementaciones de procesos de flujo de trabajo, la sesión de usuario correspondiente que activó el flujo de trabajo se pierde normalmente. Esto conduce a procesos de flujo de trabajo que a menudo utilizan sesiones administrativas para realizar su trabajo.

Para solucionar estos problemas, se recomienda utilizar los mismos enfoques mencionados en los eventos de [procesamiento, los preprocesadores de replicación y los trabajos](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) .

## Procesadores POST de Sling y páginas eliminadas {#sling-post-processors-and-deleted-pages}

Hay un par de sesiones administrativas que se utilizan en las implementaciones del procesador Sling POST. Normalmente, las sesiones administrativas se utilizan para acceder a nodos que están pendientes de eliminación dentro del POST que se está procesando. En consecuencia, ya no están disponibles a través de la sesión de solicitud. Se puede acceder a un nodo pendiente de eliminación para revelar a metada que de otra manera no debería ser accesible.
