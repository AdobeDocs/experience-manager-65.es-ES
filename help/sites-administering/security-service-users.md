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
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Seguridad
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '1789'
ht-degree: 0%

---

# Usuarios de servicio en AEM{#service-users-in-aem}

## Información general {#overview}

La forma principal de obtener una sesión administrativa o resolución de recursos en AEM era mediante los métodos `SlingRepository.loginAdministrative()` y `ResourceResolverFactory.getAdministrativeResourceResolver()` proporcionados por Sling.

Sin embargo, ninguno de estos métodos se diseñó en torno al [principio de menor privilegio](https://en.wikipedia.org/wiki/Principle_of_least_privilege) y facilita a los desarrolladores no planificar una estructura adecuada y los niveles de control de acceso (ACL) correspondientes para su contenido de forma temprana. Si existe una vulnerabilidad en un servicio de este tipo, a menudo conduce a escalaciones de privilegios al usuario `admin`, incluso si el código en sí no necesita privilegios administrativos para funcionar.

## Cómo eliminar gradualmente las sesiones de administración {#how-to-phase-out-admin-sessions}

### Prioridad 0: ¿La función está activa/es necesaria/no se selecciona? {#priority-is-the-feature-active-needed-derelict}

Puede haber casos en los que la sesión de administración no se utilice o la función esté deshabilitada por completo. Si este es el caso de la implementación, asegúrese de eliminar la función por completo o de ajustarla al [código NOP](https://en.wikipedia.org/wiki/NOP).

### Prioridad 1: Usar la sesión de solicitud {#priority-use-the-request-session}

Siempre que sea posible, refactorice su función para que la sesión de solicitud determinada y autenticada se pueda utilizar para leer o escribir contenido. Si esto no es factible, a menudo se puede lograr aplicando las prioridades que se indican a continuación.

### Prioridad 2: Reestructurar contenido {#priority-restructure-content}

Se pueden resolver muchos problemas reestructurando el contenido. Tenga en cuenta estas reglas sencillas al realizar la reestructuración:

* **Cambiar control de acceso**

   * Asegúrese de que los usuarios o grupos a los que realmente se necesita acceder tengan acceso;

* **Ajustar la estructura de contenido**

   * Moverla a otras ubicaciones, por ejemplo, donde el control de acceso coincida con las sesiones de solicitud disponibles;
   * Cambiar la granularidad del contenido;

* **Refactorizar el código para que sea un servicio adecuado**

   * Mueva la lógica empresarial del código JSP al servicio. Esto permite realizar modelos de contenido diferentes.

Además, asegúrese de que cualquier función nueva que desarrolle cumpla estos principios:

* **Los requisitos de seguridad deben dirigir la estructura de contenido**

   * La gestión del control de acceso debería ser natural
   * El control de acceso debe ser reforzado por el repositorio, no por la aplicación

* **Usar nodos**

   * Restringir el conjunto de propiedades que se pueden establecer

* **Respetar la configuración de privacidad**

   * En el caso de los perfiles privados, un ejemplo sería no exponer la imagen de perfil, el correo electrónico o el nombre completo que se encuentra en el nodo privado `/profile`.

## Control de acceso estricto {#strict-access-control}

Tanto si aplica el control de acceso durante la reestructuración de contenido como cuando lo hace para un nuevo usuario de servicio, debe aplicar las ACL más estrictas posibles. Utilice todas las instalaciones posibles de control de acceso:

* Por ejemplo, en lugar de aplicar `jcr:read` en `/apps`, aplique solo a `/apps/*/components/*/analytics`

* Usar [restricciones](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* Aplicar ACL para tipos de nodos
* Límite de permisos

   * por ejemplo, cuando solo necesite escribir propiedades, no conceda el permiso `jcr:write`; utilice `jcr:modifyProperties` en su lugar

## Usuarios y asignaciones de servicio {#service-users-and-mappings}

Si lo anterior falla, Sling 7 ofrece un servicio de Asignación de usuarios de servicio, que permite configurar una asignación entre paquetes y usuarios y dos métodos de API correspondientes: ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` y ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` que devuelven una resolución de sesión/recurso con los privilegios de un usuario configurado únicamente. Estos métodos tienen las siguientes características:

* Permiten asignar servicios a los usuarios
* Permiten definir usuarios de subservicios
* El punto de configuración central es: `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` =  `service-name` [ &quot;:&quot; subservice-name  ] 

* `service-id` está asignado a un solucionador de recursos o a un ID de usuario del repositorio JCR para la autenticación
* `service-name` es el nombre simbólico del paquete que proporciona el servicio

## Otro Recommendations {#other-recommendations}

### Reemplazar la sesión de administración por un usuario de servicio {#replacing-the-admin-session-with-a-service-user}

Un usuario de servicio es un usuario JCR sin contraseña establecida y con un conjunto mínimo de privilegios necesarios para realizar una tarea específica. Si no se ha establecido ninguna contraseña, no será posible iniciar sesión con un usuario de servicio.

Una forma de eliminar una sesión administrativa es reemplazarla por sesiones de usuario de servicio. También se puede sustituir por varios usuarios de subservicio si es necesario.

Para reemplazar la sesión de administrador por un usuario de servicio, debe realizar los siguientes pasos:

1. Identifique los permisos necesarios para su servicio, teniendo en cuenta el principio de mínimo permiso.
1. Compruebe si ya hay un usuario disponible con exactamente la configuración de permisos que necesita. Cree un nuevo usuario de servicio del sistema si ningún usuario existente coincide con sus necesidades. RTC es necesario para crear un nuevo usuario de servicio. A veces, tiene sentido crear varios usuarios de subservicios (por ejemplo, uno para escribir y otro para leer) para compartimentar el acceso aún más.
1. Configure y pruebe los ACE para su usuario.
1. Agregue una asignación `service-user` para su servicio y para `user/sub-users`

1. Haga que la función sling del usuario del servicio esté disponible para su paquete: actualice a la versión más reciente de `org.apache.sling.api`.

1. Reemplace el `admin-session` en su código por las API `loginService` o `getServiceResourceResolver` .

## Creación de un nuevo usuario de servicio {#creating-a-new-service-user}

Después de comprobar que ningún usuario de la lista de usuarios de AEM servicio es aplicable para su caso de uso y de aprobar los problemas correspondientes de RTC, puede continuar y agregar el nuevo usuario al contenido predeterminado.

El método recomendado es crear un usuario de servicio para utilizar el explorador de repositorios en *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*

El objetivo es obtener una propiedad `jcr:uuid` válida que sea obligatoria para crear el usuario a través de una instalación de paquete de contenido.

Puede crear usuarios de servicios mediante:

1. Ir al explorador del repositorio en *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. Para iniciar sesión como administrador, pulse el enlace **Iniciar sesión** en la esquina superior izquierda de la pantalla.
1. A continuación, cree y asigne un nombre al usuario del sistema. Para crear el usuario como un sistema, establezca la ruta intermedia como `system` y añada subcarpetas opcionales según sus necesidades:

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Compruebe que el nodo de usuario del sistema tenga el siguiente aspecto:

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >Tenga en cuenta que no hay tipos de mezcla asociados con los usuarios de servicios. Esto significa que no habrá políticas de control de acceso para los usuarios del sistema.

Al añadir el .content.xml correspondiente al contenido del paquete, asegúrese de haber configurado el `rep:authorizableId` y de que el tipo principal sea `rep:SystemUser`. Debería tener este aspecto:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Agregar una modificación de configuración a la configuración de ServiceUserMapper {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Para agregar una asignación desde el servicio a los usuarios del sistema correspondientes, debe crear una configuración de fábrica para el servicio ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)`. Para mantener este modular, estas configuraciones se pueden proporcionar utilizando el [mecanismo de modificación de Sling](https://issues.apache.org/jira/browse/SLING-3578). La forma recomendada de instalar estas configuraciones con su paquete es mediante [Sling Initial Content Loading](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. Cree una subcarpeta SLING-INF/content debajo de la carpeta src/main/resources del paquete
1. En esta carpeta, cree un archivo llamado org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.modified-&lt;some unique name for your factory configuration>.xml con el contenido de su configuración de fábrica (incluidas todas las asignaciones de usuarios de subservicio). Ejemplo:

1. Cree una carpeta `SLING-INF/content` debajo de la carpeta `src/main/resources` del paquete;
1. En esta carpeta, cree un archivo `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` con el contenido de la configuración de fábrica, incluidas todas las asignaciones de usuario de subservicio.

   Para fines ilustrativos, tome un archivo llamado `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

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

1. Haga referencia al contenido inicial de Sling en la configuración del `maven-bundle-plugin` en el `pom.xml` del paquete. Ejemplo:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Instale el paquete y asegúrese de que la configuración de fábrica se ha instalado. Para ello:

   * Accediendo a la consola web en *https://serverhost:serveraddress/system/console/configMgr*
   * Busque **Apache Sling Service User Mapper Service Modif**
   * Haga clic en el vínculo para ver si se ha configurado correctamente.

## Cómo tratar las sesiones compartidas en los servicios {#dealing-with-shared-sessions-in-services}

Las llamadas a `loginAdministrative()` suelen aparecer junto con las sesiones compartidas. Estas sesiones se adquieren al activar el servicio y solo se cerran tras detener el servicio. Aunque esta es una práctica común, conduce a dos problemas:

* **Seguridad:** Estas sesiones de administración se utilizan para almacenar en caché y devolver recursos u otros objetos enlazados a la sesión compartida. Más adelante en la pila de llamadas, estos objetos podrían adaptarse a las sesiones o a los solucionadores de recursos con privilegios elevados y, a menudo, el llamador no tiene claro que sea una sesión de administrador con la que esté operando.
* **Rendimiento:** En las sesiones compartidas de Oak pueden causar problemas de rendimiento y actualmente no se recomienda usarlos.

La solución más obvia para el riesgo de seguridad es simplemente reemplazar la llamada `loginAdministrative()` por una `loginService()` a un usuario con privilegios restringidos. Sin embargo, esto no tendrá ningún impacto en ninguna posible degradación del rendimiento. Una posibilidad de mitigar esto es envolver toda la información solicitada en un objeto que no esté asociado con la sesión. A continuación, cree (o destruya) la sesión bajo demanda.

El método recomendado es refactorizar la API del servicio para proporcionar al llamador control sobre la creación/destrucción de la sesión.

## Sesiones administrativas en JSP {#administrative-sessions-in-jsps}

Los JSP no pueden utilizar `loginService()` porque no hay ningún servicio asociado. Sin embargo, las sesiones administrativas en los JSP suelen ser una señal de violación del paradigma de MVC.

Esto se puede corregir de dos maneras:

1. Reestructurar el contenido de manera que permita manipularlo con la sesión del usuario;
1. Extracción de la lógica a un servicio que proporcione una API que luego JSP pueda usar.

El primer método es el preferido.

## Eventos de procesamiento, preprocesadores de replicación y trabajos {#processing-events-replication-preprocessors-and-jobs}

Al procesar eventos o trabajos, y en algunos casos flujos de trabajo, la sesión correspondiente que activó el evento generalmente se pierde. Esto lleva a que los administradores de eventos y los procesadores de trabajos a menudo utilicen sesiones administrativas para realizar su trabajo. Hay diferentes enfoques concebibles para resolver este problema, cada uno con sus ventajas y desventajas:

1. Pase el `user-id` en la carga útil del evento y utilice la suplantación.

   **Ventajas:** Fácil de usar.

   **Desventajas:** sigue usando  `loginAdministrative()`. Vuelve a autenticar una solicitud que ya se ha autenticado.

1. Cree o reutilice un usuario de servicio que tenga acceso a los datos.

   **Ventajas:** coherente con el diseño actual. Necesita un cambio mínimo.

   **Desventajas:** necesita usuarios de servicios muy poderosos para ser flexibles, lo que puede conducir fácilmente a escalaciones de privilegios. Elude el modelo de seguridad.

1. Pase una serialización del `Subject` en la carga útil de evento y cree un `ResourceResolver` basado en ese asunto. Un ejemplo sería el uso de JAAS `doAsPrivileged` en `ResourceResolverFactory`.

   **Ventajas:**  Limpie la implementación desde un punto de vista de seguridad. Evita la reautenticación y funciona con los privilegios originales. El código relevante para la seguridad es transparente para el consumidor del evento.

   **Desventajas:** necesita refactorización. El hecho de que el código relevante para la seguridad sea transparente para el consumidor del evento también podría causar problemas.

El tercer método es actualmente la técnica de procesamiento preferida.

## Procesos de flujo de trabajo {#workflow-processes}

En implementaciones de procesos de flujo de trabajo, la sesión de usuario correspondiente que activó el flujo de trabajo generalmente se pierde. Esto lleva a que los procesos de flujo de trabajo a menudo utilicen sesiones administrativas para realizar su trabajo.

Para solucionar estos problemas, se recomienda utilizar los mismos enfoques mencionados en [Eventos de procesamiento, preprocesadores de replicación y trabajos](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs).

## Procesadores de POST Sling y páginas eliminadas {#sling-post-processors-and-deleted-pages}

Hay un par de sesiones administrativas que se utilizan en las implementaciones de procesador de sling POST. Normalmente, las sesiones administrativas se utilizan para acceder a los nodos que están pendientes de eliminación dentro del POST que se está procesando. Por lo tanto, ya no están disponibles a través de la sesión de solicitud. Se puede acceder a un nodo pendiente de eliminación para revelar a metada que de otra manera no debería ser accesible.
