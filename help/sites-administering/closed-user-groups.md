---
title: Grupos de usuarios cerrados en AEM
seo-title: Closed User Groups in AEM
description: Obtenga información sobre los grupos de usuarios cerrados en AEM.
seo-description: Learn about Closed User Groups in AEM.
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '6872'
ht-degree: 0%

---

# Grupos de usuarios cerrados en AEM{#closed-user-groups-in-aem}

## Introducción {#introduction}

Desde AEM 6.3, existe una nueva implementación de grupo cerrado de usuarios que tiene como objetivo abordar los problemas de rendimiento, escalabilidad y seguridad presentes en la implementación existente.

>[!NOTE]
>
>Para simplificar, la abreviatura CUG se utilizará en toda esta documentación.

El objetivo de la nueva implementación es cubrir la funcionalidad existente cuando sea necesario, al mismo tiempo que se tratan los problemas y las limitaciones de diseño de versiones anteriores. El resultado es un nuevo diseño CUG con las siguientes características:

* Separación clara de los elementos de autenticación y autorización, que pueden utilizarse individualmente o en combinación;
* Modelo de autorización específico para reflejar el acceso restringido de lectura en los árboles CUG configurados sin interferir con otros requisitos de configuración y permisos de control de acceso;
* Separación entre la configuración del control de acceso del acceso de lectura restringido, que suele ser necesaria en instancias de creación, y la evaluación de permisos que normalmente solo se desea en la publicación;
* Edición del acceso de lectura restringido sin escalación de privilegios;
* Extensión de tipo de nodo dedicada para marcar el requisito de autenticación;
* Ruta de inicio de sesión opcional asociada con el requisito de autenticación.

### La nueva implementación de grupos de usuarios personalizados {#the-new-custom-user-group-implementation}

Un CUG como se conoce en el contexto de AEM consiste en los siguientes pasos:

* Restringir el acceso de lectura en el árbol que debe protegerse y permitir solo la lectura para entidades que estén incluidas en una instancia CUG determinada o que estén excluidas de la evaluación CUG. Esto se denomina **autorización** elemento.
* Aplique la autenticación en un árbol determinado y, opcionalmente, especifique una página de inicio de sesión dedicada para ese árbol que se excluya posteriormente. Esto se denomina **autenticación** elemento.

La nueva implementación se ha diseñado para trazar una línea entre los elementos de autenticación y autorización. A partir de AEM 6.3, es posible restringir el acceso de lectura sin añadir explícitamente un requisito de autenticación. Por ejemplo, si una instancia determinada requiere autenticación por completo o un árbol dado ya reside en un subárbol que ya requiere autenticación.

Del mismo modo, un árbol dado se puede marcar con un requisito de autenticación sin cambiar la configuración de permisos efectiva. Las combinaciones y los resultados se enumeran en la [Combinación de políticas CUG y el requisito de autenticación](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) para obtener más información.

## Información general {#overview}

### Autorización: Restricción del acceso de lectura {#authorization-restricting-read-access}

La función clave de un CUG es restringir el acceso de lectura en un árbol determinado en el repositorio de contenido para todos excepto para los principales seleccionados. En lugar de manipular el contenido de control de acceso predeterminado sobre la marcha, la nueva implementación adopta un enfoque diferente al definir un tipo dedicado de política de control de acceso que representa un CUG.

#### Política de control de acceso para CUG {#access-control-policy-for-cug}

Este nuevo tipo de política tiene las siguientes características:

* Política de control de acceso de tipo org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy (definida por la API de Apache Jackrabbit);
* PrincipalSetPolicy concede privilegios a un conjunto modificable de entidades principales;
* Los privilegios otorgados y el alcance de la política es un detalle de implementación.

La implementación de PrincipalSetPolicy utilizada para representar los CUGs también define que:

* Las directivas CUG solo conceden acceso de lectura a elementos JCR normales (por ejemplo, se excluye el contenido de control de acceso);
* El ámbito se define mediante el nodo controlado de acceso que contiene la política CUG;
* Las políticas de CUG se pueden anidar, un CUG anidado inicia un nuevo CUG sin heredar el conjunto principal del CUG &quot;principal&quot;;
* El efecto de la directiva, si la evaluación está habilitada, se hereda a todo el subárbol hasta el siguiente CUG anidado.

Estas políticas de CUG se implementan en una instancia de AEM a través de un módulo de autorización separado llamado oak-authorization-cug. Este módulo viene con su propia administración de control de acceso y evaluación de permisos. En otras palabras, la configuración AEM predeterminada envía una configuración de repositorio de contenido Oak que combina varios mecanismos de autorización. Para obtener más información, consulte [esta página de la documentación de Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

En esta configuración compuesta, un nuevo CUG no reemplaza el contenido de control de acceso existente adjunto al nodo de destino, sino que está diseñado para ser un suplemento que también se puede eliminar más adelante sin afectar al control de acceso original, que de forma predeterminada en AEM sería una lista de control de acceso.

A diferencia de la implementación anterior, las nuevas políticas de CUG siempre se reconocen y tratan como contenido de control de acceso. Esto implica que se crean y editan usando la API de administración de control de acceso JCR. Para obtener más información, consulte la [Administración de directivas de CUG](#managing-cug-policies) para obtener más información.

#### Evaluación de permisos de las políticas del CUG {#permission-evaluation-of-cug-policies}

Además de una gestión específica del control de acceso para los CUG, el nuevo modelo de autorización permite habilitar condicionalmente la evaluación de permisos para sus políticas. Esto permite configurar las políticas de CUG en un entorno de ensayo y solo permite evaluar los permisos efectivos una vez replicados en el entorno de producción.

La evaluación de permisos para las políticas de CUG y la interacción con el modelo de autorización predeterminado o adicional sigue el patrón diseñado para múltiples mecanismos de autorización en Apache Jackrabbit Oak: se concede un conjunto determinado de permisos si y solo si todos los modelos conceden acceso. Consulte [esta página](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) para obtener más información.

Las siguientes características se aplican a la evaluación de permisos asociada al modelo de autorización diseñado para gestionar y evaluar las políticas CUG:

* Solo gestiona permisos de lectura para nodos y propiedades normales, pero no lee contenido de control de acceso
* No gestiona permisos de escritura ni ningún tipo de permisos requeridos para la modificación del contenido JCR protegido (control de acceso, información de tipo de nodo, control de versiones, bloqueo o administración de usuarios, entre otros); Estos permisos no se ven afectados por una directiva CUG y no serán evaluados por el modelo de autorización asociado. El otorgamiento o no de estos permisos depende de los otros modelos configurados en la configuración de seguridad.

El efecto de una política CUG única en la evaluación de los permisos puede resumirse de la siguiente manera:

* Se deniega el acceso de lectura a todas las personas, excepto a los sujetos que contengan entidades principales excluidas o entidades principales enumeradas en la política;
* La política surte efecto en el nodo controlado de acceso que contiene la política y sus propiedades;
* El efecto se hereda adicionalmente en la jerarquía, es decir, en el árbol de elementos definido por el nodo controlado de acceso;
* Sin embargo, no afecta a los hermanos ni a los antepasados del nodo controlado de acceso;
* La herencia de un CUG determinado se detiene en un CUG anidado.

#### Prácticas recomendadas {#best-practices}

Se deben tener en cuenta las siguientes prácticas recomendadas para definir el acceso restringido de lectura a través de CUG:

* Tome una decisión consciente sobre si su necesidad de un CUG es restringir el acceso de lectura o un requisito de autenticación. En el caso de estos últimos o si hay necesidad de ambos, consulte la sección Prácticas recomendadas para obtener más detalles sobre el requisito de autenticación
* Cree un modelo de amenaza para los datos o el contenido que debe protegerse para identificar los límites de amenaza y obtener una imagen clara sobre la sensibilidad de los datos y las funciones asociadas con el acceso autorizado
* Modele el contenido del repositorio y los CUG teniendo en cuenta aspectos generales relacionados con la autorización y prácticas recomendadas:

   * Recuerde que el permiso de lectura solo se concederá si un CUG determinado y la evaluación de otros módulos implementados en la subvención de configuración permiten que un sujeto dado lea un elemento determinado del repositorio
   * Evite crear CUG redundantes en los que el acceso de lectura ya esté restringido por otros módulos de autorización
   * La necesidad excesiva de CUG anidados puede destacar problemas en el diseño de contenido
   * Una necesidad excesiva de CUG (por ejemplo, en cada página) puede indicar la necesidad de un modelo de autorización personalizado que se adapte mejor a las necesidades de seguridad específicas de la aplicación y del contenido disponible.

* Limite las rutas admitidas para las políticas de CUG a unos cuantos árboles en el repositorio para permitir un rendimiento optimizado. Por ejemplo, permitir solo los CUGs por debajo del nodo /content tal como se envía como valor predeterminado desde AEM 6.3.
* Las políticas CUG están diseñadas para conceder acceso de lectura a un pequeño conjunto de entidades principales. La necesidad de un gran número de entidades principales puede poner de relieve cuestiones relacionadas con el contenido o el diseño de la aplicación y debe reconsiderarse.

### Autenticación: Definición del requisito de autenticación {#authentication-defining-the-auth-requirement}

Las partes relacionadas con la autenticación de la función CUG permiten marcar árboles que requieren autenticación y, opcionalmente, especificar una página de inicio de sesión dedicada. De acuerdo con la versión anterior, la nueva implementación permite marcar árboles que requieren autenticación en el repositorio de contenido y habilitar condicionalmente la sincronización con la variable `Sling org.apache.sling.api.auth.Authenticator`responsable de aplicar finalmente el requisito y redirigir a un recurso de inicio de sesión.

Estos requisitos se registran en el Authenticator mediante un servicio OSGi que proporciona la variable `sling.auth.requirements` propiedad de registro. Estas propiedades se utilizan para ampliar dinámicamente los requisitos de autenticación. Para obtener más información, consulte la [Documentación de Sling](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### Definición del requisito de autenticación con un tipo de mezcla dedicado {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

Por razones de seguridad, la nueva implementación reemplaza el uso de una propiedad JCR residual por un tipo de mezcla dedicada llamado `granite:AuthenticationRequired`, que define una sola propiedad opcional de tipo STRING para la ruta de inicio de sesión `granite:loginPath`. Solo los cambios de contenido relacionados con este tipo de mezcla llevarán a la actualización de los requisitos registrados con Apache Sling Authenticator. Las modificaciones se rastrean si se mantienen modificaciones transitorias y, por lo tanto, requieren una `javax.jcr.Session.save()` llamada a ser efectiva.

Lo mismo se aplica a la variable `granite:loginPath` propiedad. Sólo se respetará si está definido por el tipo de mezcla relacionado con el requisito de autenticación. Añadir una propiedad residual con este mismo nombre en un nodo JCR no estructurado no mostrará el efecto deseado y el controlador responsable de actualizar el registro OSGi ignorará la propiedad.

>[!NOTE]
>
>La configuración de la propiedad de ruta de inicio de sesión es opcional y solo es necesaria si el árbol que requiere autenticación no puede volver a la página de inicio de sesión predeterminada o heredada de otro modo. Consulte la [Evaluación de la ruta de inicio de sesión](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) más abajo.

#### Registro del requisito de autenticación y la ruta de inicio de sesión con el autenticador de Sling {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

Dado que se espera que este tipo de requisito de autenticación se limite a ciertos modos de ejecución y a un pequeño subconjunto de árboles dentro del repositorio de contenido, el seguimiento del tipo de mezcla de requisitos y las propiedades de la ruta de inicio de sesión es condicional y está enlazado a una configuración correspondiente que define las rutas admitidas (consulte Opciones de configuración a continuación). En consecuencia, sólo los cambios dentro del ámbito de estas rutas admitidas déclencheur una actualización del registro OSGi, en otras partes tanto el tipo de mezcla como la propiedad serán ignorados.

La configuración de AEM predeterminada ahora utiliza esta configuración permitiendo establecer la mezcla en el modo de ejecución del autor pero solo que tenga efecto en la replicación a la instancia de publicación. Consulte [esta página](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) para obtener más información sobre cómo Sling exige el requisito de autenticación.

Adición de la variable `granite:AuthenticationRequired` el tipo de mezcla dentro de las rutas soportadas configuradas hará que el registro OSGi del controlador responsable se actualice conteniendo una nueva entrada adicional con el `sling.auth.requirements` propiedad. Si un requisito de autenticación determinado especifica la opción `granite:loginPath` , el valor se registra adicionalmente en el Authenticator con un prefijo &quot;-&quot; para que se excluya de los requisitos de autenticación.

#### Evaluación y herencia del requisito de autenticación {#evaluation-and-inheritance-of-the-authentication-requirement}

Se espera que los requisitos de autenticación de Apache Sling se hereden a través de la jerarquía de páginas o nodos. Los detalles de la herencia y la evaluación de los requisitos de autenticación, como el orden y la precedencia, se consideran un detalle de implementación y no se documentarán en este artículo.

#### Evaluación de la ruta de inicio de sesión {#evaluation-of-login-path}

La evaluación de la ruta de inicio de sesión y el redireccionamiento al recurso correspondiente tras la autenticación es actualmente un detalle de implementación del Controlador de autenticación del selector de inicio de sesión de Adobe Granite ( `com.day.cq.auth.impl.LoginSelectorHandler`), que es un gestor de autenticación Apache Sling configurado con AEM de forma predeterminada.

Al llamar a `AuthenticationHandler.requestCredentials` este controlador intenta determinar la página de inicio de sesión de asignación a la que se redirigirá al usuario. Esto incluye los siguientes pasos:

* Distinguir entre la contraseña caducada y la necesidad de iniciar sesión regularmente como motivo del redireccionamiento;
* En caso de un inicio de sesión normal, comprueba si se puede obtener una ruta de inicio de sesión en el siguiente orden:

   * desde LoginPathProvider tal como lo implementa el nuevo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * desde la implementación anterior y obsoleta del CUG,
   * desde Asignaciones de páginas de inicio de sesión, tal como se define con la variable `LoginSelectorHandler`,
   * y finalmente, vuelva a la página de inicio de sesión predeterminada, tal como se define en la variable `LoginSelectorHandler`.

* Tan pronto como se haya obtenido una ruta de inicio de sesión válida mediante las llamadas enumeradas anteriormente, la solicitud del usuario se redirigirá a esa página.

El objetivo de esta documentación es la evaluación de la ruta de inicio de sesión tal como la expone el `LoginPathProvider` interfaz. La implementación enviada desde AEM 6.3 se comporta de la siguiente manera:

* El registro de las rutas de inicio de sesión depende de la distinción entre la contraseña caducada y la necesidad de iniciar sesión regularmente como motivo del redireccionamiento
* En caso de inicio de sesión normal, comprueba si se puede obtener una ruta de inicio de sesión en el siguiente orden:

   * de la variable `LoginPathProvider` tal como lo implementa el nuevo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * desde la implementación anterior y obsoleta del CUG,
   * desde Asignaciones de páginas de inicio de sesión, tal como se define con la variable `LoginSelectorHandler`,
   * y finalmente vuelven a la página de inicio de sesión predeterminada tal como se define con la variable `LoginSelectorHandler`.

* Tan pronto como se haya obtenido una ruta de inicio de sesión válida mediante las llamadas enumeradas anteriormente, la solicitud del usuario se redirigirá a esa página.

La variable `LoginPathProvider` tal como lo implementa el nuevo soporte de requisitos de autenticación en Granite expone las rutas de inicio de sesión tal como se define en la `granite:loginPath` propiedades, que a su vez se definen por el tipo de mezcla descrito anteriormente. La asignación de la ruta del recurso que contiene la ruta de inicio de sesión y el propio valor de la propiedad se conserva en la memoria y se evalúa para encontrar una ruta de inicio de sesión adecuada para otros nodos de la jerarquía.

>[!NOTE]
>
>La evaluación solo se realiza para solicitudes asociadas con recursos que se encuentran en las rutas configuradas admitidas. Para cualquier otra solicitud se evaluarán las formas alternativas de determinar la ruta de inicio de sesión.

#### Prácticas recomendadas {#best-practices-1}

Se deben tener en cuenta las siguientes prácticas recomendadas al definir los requisitos de autenticación:

* Evite anidar los requisitos de autenticación: colocar un marcador de requisito de autenticación único al principio de un árbol debe ser suficiente y se hereda a todo el subárbol definido por el nodo de destino. Los requisitos de autenticación adicionales dentro de ese árbol deben considerarse redundantes y pueden dar lugar a problemas de rendimiento al evaluar el requisito de autenticación dentro de Apache Sling. Con la separación de las áreas CUG relacionadas con la autorización y la autenticación, es posible restringir el acceso de lectura mediante CUG u otro tipo de políticas, al mismo tiempo que se aplica la autenticación para todo el árbol.
* Modele el contenido del repositorio de tal manera que los requisitos de autenticación se apliquen para todo el árbol sin la necesidad de excluir de nuevo los subárboles anidados.
* Para evitar la especificación y, posteriormente, registrar rutas de inicio de sesión redundantes:

   * depender de la herencia y evitar definir rutas de inicio de sesión anidadas,
   * no configure la ruta de inicio de sesión opcional en un valor que corresponda al valor predeterminado o heredado,
   * los desarrolladores de aplicaciones deben identificar qué rutas de inicio de sesión deben configurarse en las configuraciones globales de ruta de inicio de sesión (tanto predeterminadas como asignaciones) asociadas con la variable `LoginSelectorHandler`.

## Representación en el repositorio {#representation-in-the-repository}

### Representación de directivas de CUG en el repositorio {#cug-policy-representation-in-the-repository}

La documentación de Oak cubre cómo se reflejan las nuevas políticas de CUG en el contenido del repositorio. Para obtener más información, consulte [esta página](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### Requisito de autenticación en el repositorio {#authentication-requirement-in-the-repository}

La necesidad de un requisito de autenticación independiente se refleja en el contenido del repositorio con un tipo de nodo mixto dedicado colocado en el nodo de destino. El tipo de mezcla define una propiedad opcional para especificar una página de inicio de sesión dedicada para el árbol definido por el nodo de destino.

La página asociada con la ruta de inicio de sesión puede estar ubicada dentro o fuera de ese árbol. Se excluirá del requisito de autenticación.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## Administración de directivas CUG y requisitos de autenticación {#managing-cug-policies-and-authentication-requirement}

### Administración de directivas de CUG {#managing-cug-policies}

El nuevo tipo de políticas de control de acceso para restringir el acceso de lectura para un CUG se administra utilizando la API de administración de control de acceso JCR y sigue los mecanismos descritos con la variable [Especificación de JCR 2.0](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).

#### Establecer Una Nueva Política De CUG {#set-a-new-cug-policy}

Código para aplicar una nueva directiva CUG en un nodo que no tenía un CUG establecido anteriormente. Tenga en cuenta que `getApplicablePolicies` solo devuelve las nuevas directivas que no se hayan configurado anteriormente. Al final, la política necesita ser reescrita y los cambios deben mantenerse.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

AccessControlPolicyIterator it = acMgr.getApplicablePolicies(path);
while (it.hasNext()) {
        AccessControlPolicy policy = it.nextAccessControlPolicy();
        if (policy instanceof PrincipalSetPolicy) {
           cugPolicy = (PrincipalSetPolicy) policy;
           break;
        }
}

if (cugPolicy == null) {
   log.debug("no applicable policy"); // path not supported or no applicable policy (e.g.
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### Editar Una Política De CUG Existente {#edit-an-existing-cug-policy}

Se necesitan los siguientes pasos para editar una política CUG existente. Tenga en cuenta que la política modificada debe escribirse de nuevo y los cambios deben conservarse utilizando `javax.jcr.Session.save()`.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
     if (policy instanceof PrincipalSetPolicy) {
        cugPolicy = (PrincipalSetPolicy) policy;
        break;
     }
}

if (cugPolicy == null) {
   log.debug("no policy to edit"); // path not supported or policy not set before
   return;
}

if (cugPolicy.addPrincipals(toAdd1, toAdd2) || cugPolicy.removePrincipals(toRemove)) {
   acMgr.setPolicy(path, cugPolicy);
   session.save();
} else {
     log.debug("cug policy not modified");
}
```

### Recuperar directivas de CUG efectivas {#retrieve-effective-cug-policies}

La administración de control de acceso JCR define un método de mejor esfuerzo para recuperar las políticas que surten efecto en una ruta determinada. Debido al hecho de que la evaluación de las políticas de CUG es condicional y depende de la configuración correspondiente que se habilite, llamando a `getEffectivePolicies` es una forma conveniente de verificar si una directiva CUG determinada está surtiendo efecto en una instalación determinada.

>[!NOTE]
>
>Tenga en cuenta la diferencia entre `getEffectivePolicies` y el siguiente ejemplo de código que sube por la jerarquía para encontrar si una ruta dada ya es parte de un CUG existente.

```java
String path = [...] // needs to be a supported, absolute path

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

// log an debug message of all CUG policies that take effect at the given path
// there could be zero, one or many (creating nested CUGs is possible)
for (AccessControlPolicy policy : acMgr.getEffectivePolicies(path) {
     if (policy instanceof PrincipalSetPolicy) {
        String policyPath = "-";
        if (policy instanceof JackrabbitAccessControlPolicy) {
           policyPath = ((JackrabbitAccessControlPolicy) policy).getPath();
        }
        log.debug("Found effective CUG for path '{}' at '{}', path, policyPath);
     }
}
```

#### Recuperar directivas de CUG heredadas {#retrieve-inherited-cug-policies}

Encontrar todos los CUG anidados que se han definido en una ruta determinada independientemente de si tienen efecto o no. Para obtener más información, consulte la [Opciones de configuración](/help/sites-administering/closed-user-groups.md#configuration-options) para obtener más información.

```java
String path = [...]

List<AccessControlPolicy> cugPolicies = new ArrayList<AccessControlPolicy>();
while (isSupportedPath(path)) {
     for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
         if (policy instanceof PrincipalSetPolicy) {
            cugPolicies.add(policy);
         }
      }
      path = (PathUtils.denotesRoot(path)) ? null : PathUtils.getAncestorPath(path, 1);
}
```

#### Administración de políticas de CUG por ubicación {#managing-cug-policies-by-pincipal}

Las extensiones definidas por `JackrabbitAccessControlManager` que permiten editar las políticas de control de acceso por principal no se implementan con la administración de control de acceso CUG, ya que por definición una directiva CUG siempre afecta a todos los principales: aquellos enumerados con la variable `PrincipalSetPolicy` se les concede acceso de lectura, mientras que todas las demás entidades principales no podrán leer contenido en el árbol definido por el nodo de destino.

Los métodos correspondientes siempre devuelven una matriz de directiva vacía, pero no arrojarán excepciones.

### Administración del requisito de autenticación {#managing-the-authentication-requirement}

La creación, modificación o eliminación de nuevos requisitos de autenticación se logra cambiando el tipo de nodo efectivo del nodo de destino. La propiedad de ruta de inicio de sesión opcional se puede escribir usando la API JCR normal.

>[!NOTE]
>
>Las modificaciones realizadas en un nodo de destino determinado mencionadas anteriormente solo se reflejarán en el autenticador de Apache Sling si la variable `RequirementHandler` se ha configurado y el destino está contenido en los árboles definidos por las rutas admitidas (consulte la sección Opciones de configuración).
>
>Para obtener más información, consulte [Asignación de tipos de nodo de mezcla](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Asignación de tipos de nodo de mezcla) y [Adición de nodos y configuración de propiedades](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 Adición de nodos y configuración de propiedades)

#### Adición de un nuevo requisito de autenticación {#adding-a-new-auth-requirement}

A continuación se describen los pasos para crear un nuevo requisito de autenticación. Tenga en cuenta que el requisito solo se registrará con el Apache Sling Authenticator si la variable `RequirementHandler` se ha configurado para el árbol que contiene el nodo de destino.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### Añadir un nuevo requisito de autenticación con la ruta de inicio de sesión {#add-a-new-auth-requirement-with-login-path}

Pasos para crear un nuevo requisito de autenticación, incluida una ruta de inicio de sesión. Tenga en cuenta que el requisito y la exclusión de la ruta de inicio de sesión solo se registrarán con el Apache Sling Authenticator si la variable `RequirementHandler` se ha configurado para el árbol que contiene el nodo de destino.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### Modificar una ruta de inicio de sesión existente {#modify-an-existing-login-path}

A continuación se detallan los pasos para cambiar una ruta de inicio de sesión existente. La modificación solo se registrará con el Apache Sling Authenticator si la variable `RequirementHandler` se ha configurado para el árbol que contiene el nodo de destino. El valor de ruta de inicio de sesión anterior se eliminará del registro. La modificación no afecta al requisito de autenticación asociado al nodo de destino.

```java
Node targetNode = [...]
String newLoginPath = [...] // STRING property

if (targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", newLoginPath);
   session.save();
} else {
     log.debug("cannot modify login path property; mixin type missing");
}
```

#### Eliminar una ruta de inicio de sesión existente {#remove-an-existing-login-path}

Pasos para eliminar una ruta de inicio de sesión existente. La entrada de la ruta de inicio de sesión solo no se registrará desde Apache Sling Authenticator si la variable `RequirementHandler` se ha configurado para el árbol que contiene el nodo de destino. El requisito de autenticación asociado con el nodo de destino no se ve afectado.

```java
Node targetNode = [...]

if (targetNode.hasProperty("granite:loginPath") &&
   targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", null);
   session.save();
} else {
     log.debug("cannot remove login path property; mixin type missing");
}
```

O bien, puede utilizar el método siguiente para lograr el mismo propósito:

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### Eliminar un requisito de autenticación {#remove-an-auth-requirement}

Pasos para eliminar un requisito de autenticación existente. El requisito solo no se registrará en el Apache Sling Authenticator si la variable `RequirementHandler` se ha configurado para el árbol que contiene el nodo de destino.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### Recuperar requisitos de autenticación efectivos {#retrieve-effective-auth-requirements}

No hay una API pública dedicada para leer todos los requisitos de autenticación efectivos registrados en Apache Sling Authenticator. Sin embargo, la lista se expone en la consola del sistema en `https://<serveraddress>:<serverport>/system/console/slingauth` en el **Configuración de requisitos de autenticación**&quot;.

La siguiente imagen muestra los requisitos de autenticación de una instancia de publicación AEM con contenido de demostración. La ruta resaltada de la página de la comunidad ilustra cómo un requisito añadido por la implementación descrita en este documento se refleja en el Apache Sling Authenticator.

>[!NOTE]
>
>En este ejemplo no se estableció la propiedad de ruta de inicio de sesión opcional. Por lo tanto, no se ha registrado ninguna segunda entrada con el autenticador.

![imagen_1-24](assets/chlimage_1-24.jpeg)

#### Recuperar la ruta de inicio de sesión efectiva {#retrieve-the-effective-login-path}

Actualmente no hay ninguna API pública para recuperar la ruta de inicio de sesión que surtirá efecto al acceder de forma anónima a un recurso que requiere autenticación. Consulte la sección Evaluación de la ruta de inicio de sesión para obtener detalles de implementación sobre cómo se recupera la ruta de inicio de sesión.

No obstante, tenga en cuenta que, aparte de las rutas de inicio de sesión definidas con esta función, existen formas alternativas de especificar la redirección al inicio de sesión, que deben tenerse en cuenta al diseñar el modelo de contenido y los requisitos de autenticación de una instalación AEM determinada.

#### Recuperar el requisito de autenticación heredado {#retrieve-the-inherited-auth-requirement}

Al igual que con la ruta de inicio de sesión, no hay ninguna API pública para recuperar los requisitos de autenticación heredados definidos en el contenido. El siguiente ejemplo ilustra cómo enumerar todos los requisitos de autenticación que se han definido con una jerarquía determinada independientemente de si tienen efecto o no. Para obtener más información, consulte [Opciones de configuración](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>Se recomienda confiar en el mecanismo de herencia tanto para los requisitos de autenticación como para la ruta de inicio de sesión, y evitar la creación de requisitos de autenticación anidados.
>
>Para obtener más información, consulte [Evaluación y herencia del requisito de autenticación](#evaluation-and-inheritance-of-the-authentication-requirement), [Evaluación de la ruta de inicio de sesión](#evaluation-of-login-path) y [Prácticas recomendadas](#best-practices).

```java
String path = [...]
Node node = session.getNode(path);

Map<String, String> authRequirements = new ArrayList<String, String>();
while (isSupported(node)) {
     if (node.isNodeType("granite:AuthenticationRequired")) {
         String loginPath = (node.hasProperty("granite:loginPath") ?
                                     node.getProperty("granite:loginPath").getString() :
                                     "";
        authRequirements.put(node.getPath(), loginPath);
        node = node.getParent();
     }
}
```

### Combinación de políticas CUG y el requisito de autenticación {#combining-cug-policies-and-the-authentication-requirement}

En la tabla siguiente se enumeran las combinaciones válidas de las políticas CUG y el requisito de autenticación en una instancia AEM que tiene ambos módulos habilitados a través de la configuración.

| **Autenticación requerida** | **Ruta de inicio de sesión** | **Acceso de lectura restringido** | **Efecto esperado** |
|---|---|---|---|
| Sí | Sí | Sí | Un usuario determinado solo podrá ver el subárbol marcado con la política CUG si la evaluación efectiva de permisos concede acceso. Un usuario no autenticado se redirigirá a la página de inicio de sesión especificada. |
| Sí | No | Sí | Un usuario determinado solo podrá ver el subárbol marcado con la política CUG si la evaluación efectiva de permisos concede acceso. Un usuario no autenticado se redirigirá a una página de inicio de sesión heredada y predeterminada. |
| Sí | Sí | No | Un usuario no autenticado se redirigirá a la página de inicio de sesión especificada. Si se permite o no ver el árbol marcado con el requisito de autenticación depende de los permisos efectivos de los elementos individuales contenidos en ese subárbol. No hay CUG dedicado que restrinja el acceso de lectura en su lugar. |
| Sí | No | No | Un usuario no autenticado se redirigirá a una página de inicio de sesión heredada y predeterminada. Si se permite o no ver el árbol marcado con el requisito de autenticación depende de los permisos efectivos de los elementos individuales contenidos en ese subárbol. No hay CUG dedicado que restrinja el acceso de lectura en su lugar. |
| No | No | Sí | Un usuario autenticado o no autenticado determinado solo podrá ver el subárbol marcado con la política CUG si la evaluación efectiva de permisos concede acceso. Un usuario no autenticado será tratado de la misma manera y no se le redirigirá para que inicie sesión. |

>[!NOTE]
>
>La combinación de &#39;Requisito de autenticación&#39; = No y &#39;Ruta de inicio de sesión&#39; = Sí no aparece enumerada anteriormente, ya que &#39;Ruta de inicio de sesión&#39; es un atributo opcional asociado con un Requisito de autenticación. La especificación de una propiedad JCR con ese nombre sin añadir el tipo de mezcla de definición no tendrá ningún efecto y será ignorada por el controlador correspondiente.

## Componentes y configuración de OSGi {#osgi-components-and-configuration}

Esta sección proporciona información general sobre los componentes de OSGi y las opciones de configuración individuales introducidas con la nueva implementación de CUG.

Consulte también la documentación de asignación de CUG para obtener una asignación completa de las opciones de configuración entre la implementación antigua y la nueva.

### Autorización: Configuración y configuración {#authorization-setup-and-configuration}

Las nuevas partes relacionadas con la autorización se incluyen en el **Autorización de Oak CUG** paquete ( `org.apache.jackrabbit.oak-authorization-cug`), que forma parte de la instalación predeterminada de AEM. El paquete define un modelo de autorización separado que se va a implementar como una manera adicional de administrar el acceso de lectura.

#### Configuración de la autorización CUG {#setting-up-cug-authorization}

La configuración de la autorización de CUG se describe detalladamente en el [documentación relevante de Apache](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). De forma predeterminada, AEM ha implementado la autorización de CUG en todos los modos de ejecución. Las instrucciones paso a paso también pueden utilizarse para desactivar la autorización CUG en aquellas instalaciones que requieran una configuración de autorización diferente.

#### Configuración del filtro referente {#configuring-the-referrer-filter}

También debe configurar la variable [Filtro de referente de Sling](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) con todos los nombres de host que puedan utilizarse para acceder a AEM; por ejemplo, a través de CDN, Load Balancer y cualquier otro.

Si el filtro de referente no está configurado, se observan errores similares a los siguientes cuando un usuario intenta iniciar sesión en un sitio de CUG:

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### Características de los componentes de OSGi {#characteristics-of-osgi-components}

Se han introducido los dos componentes OSGi siguientes para definir los requisitos de autenticación y especificar rutas de inicio de sesión dedicadas:

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>Etiqueta</td>
   <td>Configuración de Apache Jackrabbit Oak CUG</td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>Configuración de autorización dedicada a la configuración y evaluación de permisos de CUG.</td>
  </tr>
  <tr>
   <td>Propiedades de configuración</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>Consulte también <a href="#configuration-options">Opciones de configuración</a> más abajo.</p> </td>
  </tr>
  <tr>
   <td>Política de configuración</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Referencias</td>
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td>
  </tr>
 </tbody>
</table>

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>Etiqueta</td>
   <td>Lista de exclusión de Apache Jackrabbit Oak CUG</td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>Permite excluir las principales con los nombres configurados de la evaluación CUG.</td>
  </tr>
  <tr>
   <td>Propiedades de configuración</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>Consulte también la sección Opciones de configuración que aparece a continuación.</p> </td>
  </tr>
  <tr>
   <td>Política de configuración</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Referencias</td>
   <td>ND</td>
  </tr>
 </tbody>
</table>

#### Opciones de configuración {#configuration-options}

Las opciones de configuración clave son:

* `cugSupportedPaths`: especifique los subárboles que pueden contener CUG. No hay ningún valor predeterminado establecido
* `cugEnabled`: opción de configuración para habilitar la evaluación de permisos para las políticas CUG actuales.

Las opciones de configuración disponibles asociadas con el módulo de autorización del CUG se enumeran y describen con más detalle en la sección [Documentación de Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### Exclusión de los principales de la evaluación de CUG {#excluding-principals-from-cug-evaluation}

Se ha adoptado una exención de la aplicación anterior de los principios individuales de la evaluación del CUG. La nueva autorización de CUG cubre esto con una interfaz dedicada llamada CugExclude. Apache Jackrabbit Oak 1.4 se entrega con una implementación predeterminada que excluye un conjunto fijo de entidades principales, así como una implementación ampliada que permite configurar nombres principales individuales. Este último se configura en AEM instancias de publicación.

El valor predeterminado desde AEM 6.3 evita que las directivas CUG afecten a los siguientes principios:

* entidades administrativas principales (usuario administrador, grupo de administradores)
* principales de usuario del servicio
* repositorio principal del sistema interno

Para obtener más información, consulte la tabla en la [Configuración predeterminada desde AEM 6.3](#default-configuration-since-aem) a continuación.

La exclusión del grupo &quot;administradores&quot; se puede modificar o expandir en la consola del sistema en la sección de configuración de **Lista de exclusión de Apache Jackrabbit Oak CUG**.

Alternativamente, es posible proporcionar e implementar una implementación personalizada de la interfaz CugExclude para ajustar el conjunto de entidades principales excluidas en caso de necesidades especiales. Consulte la documentación sobre [Posibilidad de conectar CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) para obtener más información y ver un ejemplo de implementación.

### Autenticación: Configuración y configuración {#authentication-setup-and-configuration}

Las nuevas partes relacionadas con la autenticación se incluyen en la **Controlador de autenticación de Adobe Granite** paquete ( `com.adobe.granite.auth.authhandler` versión 5.6.48). Este paquete forma parte de la instalación predeterminada AEM.

Para configurar el reemplazo del requisito de autenticación para el soporte de CUG obsoleto, algunos componentes de OSGi deben estar presentes y activos en una instalación de AEM determinada. Para obtener más información, consulte **Características de los componentes de OSGi** más abajo.

>[!NOTE]
>
>Debido a la opción de configuración obligatoria con RequirementHandler, las partes relacionadas con la autenticación solo estarán activas si la función se ha habilitado especificando un conjunto de rutas admitidas. Con una instalación de AEM estándar, la función está deshabilitada en el modo de ejecución de autor y habilitada para /content en el modo de ejecución de publicación.

**Características de los componentes de OSGi**

Se han introducido los dos componentes OSGi siguientes para definir los requisitos de autenticación y especificar rutas de inicio de sesión dedicadas:

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirements.impl.RequirementService**

<table>
 <tbody>
  <tr>
   <td>Etiqueta</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>Servicio dedicado de OSGi para requisitos de autenticación que registra a un observador de los cambios de contenido que afectan a los requisitos de autenticación (a través del <code>granite:AuthenticationRequirement</code> tipo de mezcla) y rutas de inicio de sesión con están expuestas al <code>LoginSelectorHandler</code>. </td>
  </tr>
  <tr>
   <td>Propiedades de configuración</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Política de configuración</td>
   <td><code>ConfigurationPolicy.OPTIONAL</code></td>
  </tr>
  <tr>
   <td>Referencias</td>
   <td>
    <ul>
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li>
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

**com.adobe.granite.auth.requirements.impl.DefaultRequirementHandler**

| Etiqueta | Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión |
|---|---|
| Descripción | `RequirementHandler` implementación que actualiza los requisitos de autenticación de Apache Sling y la exclusión correspondiente para las rutas de inicio de sesión asociadas. |
| Propiedades de configuración | `supportedPaths` |
| Política de configuración | `ConfigurationPolicy.REQUIRE` |
| Referencias | ND |

#### Opciones de configuración {#configuration-options-1}

Las partes relacionadas con la autenticación del CUG rewrite solo incluyen una opción de configuración única asociada con el Requisito de autenticación de Granite de Adobe y el Controlador de ruta de inicio de sesión:

**&quot;Requisito de autenticación y controlador de ruta de inicio de sesión&quot;**

<table>
 <tbody>
  <tr>
   <td>Propiedad</td>
   <td>Tipo</td>
   <td>Valor predeterminado</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td><p>Etiqueta = Rutas admitidas</p> <p>Nombre = 'supportedPaths'</p> </td>
   <td>Establezca&lt;string&gt;</td>
   <td>-</td>
   <td>Rutas en las que este controlador respetará los requisitos de autenticación. Deje esta configuración sin configurar si desea agregar la variable <code>granite:AuthenticationRequirement</code> tipo de mezcla a nodos sin que se apliquen (por ejemplo, en instancias de autor). Si falta, la función está deshabilitada. </td>
  </tr>
 </tbody>
</table>

## Configuración predeterminada desde AEM 6.3 {#default-configuration-since-aem}

De forma predeterminada, las nuevas instalaciones de AEM utilizarán las nuevas implementaciones tanto para las partes relacionadas con la autorización como para la autenticación de la función CUG. La implementación antigua &quot;Adobe Granite Closed User Group (CUG) Support&quot; (Compatibilidad con grupos cerrados de usuarios de Granite (CUG)) ha quedado obsoleta y se deshabilitará de forma predeterminada en todas las instalaciones AEM. Las nuevas implementaciones se habilitarán de la siguiente manera:

### Instancias de autor {#author-instances}

| **&quot;Configuración de Apache Jackrabbit Oak CUG&quot;** | **Explicación** |
|---|---|
| Rutas compatibles `/content` | La administración de control de acceso para las directivas CUG está habilitada. |
| Evaluación de CUG habilitada FALSE | La evaluación de permisos está deshabilitada. Las políticas de CUG no tienen efecto. |
| Clasificación | 200 | Consulte la documentación de Oak. |

>[!NOTE]
>
>No hay configuración para **Lista de exclusión de Apache Jackrabbit Oak CUG** y **Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión** está presente en las instancias de creación predeterminadas.

### Publicar instancias {#publish-instances}

| **&quot;Configuración de Apache Jackrabbit Oak CUG&quot;** | **Explicación** |
|---|---|
| Rutas compatibles `/content` | La administración de control de acceso para directivas CUG está habilitada debajo de las rutas configuradas. |
| Evaluación de CUG habilitada TRUE | La evaluación de permisos se habilita debajo de las rutas configuradas. Las políticas de CUG surten efecto `Session.save()`. |
| Clasificación | 200 | Consulte la documentación de Oak. |

| **&quot;Lista de exclusión de Apache Jackrabbit Oak CUG&quot;** | **Explicación** |
|---|---|
| Administradores de nombres principales | Excluye al administrador principal de la evaluación de CUG. |

| **&quot;Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión&quot;** | **Explicación** |
|---|---|
| Rutas compatibles  `/content` | Requisitos de autenticación definidos en el repositorio mediante la variable `granite:AuthenticationRequired` tipo de mezcla, efecto a continuación `/content` upon `Session.save()`. Sling Authenticator se actualiza. Se ignora la adición del tipo de mezcla fuera de las rutas admitidas. |

## Desactivación de los requisitos de autorización y autenticación de CUG {#disabling-cug-authorization-and-authentication-requirement}

La nueva implementación puede deshabilitarse por completo en caso de que una instalación determinada no utilice CUG o utilice medios diferentes para la autenticación y autorización.

### Deshabilitar autorización CUG {#disable-cug-authorization}

Consulte la [Posibilidad de conectar CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) documentación para obtener detalles sobre cómo quitar el modelo de autorización CUG de la configuración de autorización compuesta.

### Deshabilitar el requisito de autenticación {#disable-the-authentication-requirement}

Para deshabilitar la compatibilidad con los requisitos de autenticación proporcionados por la `granite.auth.authhandler` es suficiente para eliminar la configuración asociada a **Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión**.

>[!NOTE]
>
>Sin embargo, tenga en cuenta que si se elimina la configuración no se desregistrará el tipo de mezcla, que seguía siendo aplicable a los nodos sin tener efecto.

## Interacción con otros módulos {#interaction-with-other-modules}

### API de Apache Jackrabbit {#apache-jackrabbit-api}

Para reflejar el nuevo tipo de política de control de acceso utilizada por el modelo de autorización de CUG, se ha ampliado la API definida por Apache Jackrabbit. Desde la versión 2.11.0 del `jackrabbit-api` define una nueva interfaz denominada `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`, que se extiende desde `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

El mecanismo de importación de Apache Jackrabbit FileVault se ha ajustado para lidiar con las políticas de control de acceso del tipo `PrincipalSetPolicy`.

### Distribución de contenido de Apache Sling {#apache-sling-content-distribution}

Consulte lo anterior [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) para obtener más información.

### Replicación de Granite de Adobe {#adobe-granite-replication}

El módulo de replicación se ha ajustado ligeramente para poder replicar las políticas de CUG entre diferentes instancias de AEM:

* `DurboImportConfiguration.isImportAcl()` se interpreta literalmente y solo afecta a la implementación de las políticas de control de acceso `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` respetará esta configuración solo para ACL verdaderas
* Otras políticas como `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` las instancias creadas por el modelo de autorización de CUG siempre se replicarán y la opción de configuración `DurboImportConfiguration.isImportAcl`() se ignorará.

Existe una limitación en la replicación de las políticas CUG. Si se elimina una directiva CUG determinada sin eliminar el tipo de nodo mixto correspondiente `rep:CugMixin,` la eliminación no se reflejará en la replicación. Esto se ha abordado eliminando siempre la mezcla tras la eliminación de la política. No obstante, la limitación puede aparecer si se añade manualmente el tipo de mezcla.

### Controlador de autenticación de Adobe Granite {#adobe-granite-authentication-handler}

El controlador de autenticación **Controlador de autenticación de encabezado HTTP de Adobe Granite** enviado con la variable `com.adobe.granite.auth.authhandler` el paquete contiene una referencia a la variable `CugSupport` interfaz definida por el mismo módulo. Se utiliza para calcular el &quot;territorio&quot; en determinadas circunstancias, cayendo de nuevo en el territorio configurado con el controlador.

Esto se ha ajustado para hacer referencia a `CugSupport` opcional para garantizar la máxima compatibilidad con versiones anteriores si una configuración determinada decide volver a habilitar la implementación obsoleta. Las instalaciones que utilicen la implementación ya no obtendrán el dominio extraído de la implementación del CUG, pero siempre mostrarán el reino tal como se define en **Controlador de autenticación de encabezado HTTP de Adobe Granite**.

>[!NOTE]
>
>De forma predeterminada, la variable **Controlador de autenticación de encabezado HTTP de Adobe Granite** solo está configurado en el modo de ejecución de publicación con la opción &quot;Deshabilitar página de inicio de sesión&quot; ( `auth.http.nologin`) activada.

### AEM LiveCopy {#aem-livecopy}

La configuración de CUG junto con LiveCopy se representa en el repositorio mediante la adición de un nodo adicional y una propiedad adicional de la siguiente manera:

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Ambos elementos se crean en la sección `cq:Page`. Con el diseño actual, MSM solo gestiona los nodos y propiedades que se encuentran en la sección `cq:PageContent` (`jcr:content`).

Por lo tanto, los grupos CUG no se pueden desplegar en Live Copies desde modelos. Tenga en cuenta esto al configurar Live Copy.

## Cambios con la implementación del nuevo CUG {#changes-with-the-new-cug-implementation}

El objetivo de esta sección es proporcionar una visión general de los cambios realizados en la función CUG, así como una comparación entre la implementación antigua y la nueva. Enumera los cambios que afectan a la forma en que se configura la compatibilidad con CUG y describe cómo y por quién se administran los CUG en el contenido del repositorio.

### Diferencias en la configuración y configuración de CUG {#differences-in-cug-setup-and-configuration}

El componente OSGi obsoleto **Compatibilidad con el grupo cerrado de usuarios (CUG) de Adobe Granite** ( `com.day.cq.auth.impl.cug.CugSupportImpl`) se ha sustituido por nuevos componentes para poder gestionar por separado las partes relacionadas con la autorización y autenticación de la antigua funcionalidad CUG.

## Diferencias en la gestión de CUGs en el contenido del repositorio {#differences-in-managing-cugs-in-the-repository-content}

En las secciones siguientes se describen las diferencias entre las implementaciones antiguas y las nuevas desde las perspectivas de implementación y seguridad. Aunque la nueva implementación pretende proporcionar la misma funcionalidad, hay cambios sutiles que es importante conocer al utilizar el nuevo CUG.

### Diferencias Con Respecto A La Autorización {#differences-with-regards-to-authorization}

Las principales diferencias desde una perspectiva de autorización se resumen en la siguiente lista:

**Contenido de control de acceso dedicado para CUG**

En la implementación anterior, el modelo de autorización predeterminado se utilizó para manipular las directivas de lista de control de acceso al publicar, reemplazando cualquier ACE existente por la configuración establecida por el CUG. Esto se desencadenó al escribir propiedades JCR residuales regulares que se interpretaron al publicar.

Con la nueva implementación, la configuración del control de acceso del modelo de autorización predeterminado no se ve afectada por ningún CUG creado, modificado o eliminado. En su lugar, un nuevo tipo de política denominada `PrincipalSetPolicy` se aplica como contenido de control de acceso adicional al nodo de destino. Esta directiva adicional se ubicará como un elemento secundario del nodo de destino y sería un elemento secundario del nodo de directiva predeterminado si está presente.

**Edición De Políticas De CUG En Administración De Control De Acceso**

Este paso de las propiedades JCR residuales a una política de control de acceso dedicada afecta a los permisos necesarios para crear o modificar la parte de autorización de la función CUG. Dado que esto se considera una modificación para acceder al contenido de control, requiere `jcr:readAccessControl` y `jcr:modifyAccessControl` privilegios para que se escriban en el repositorio. Por lo tanto, solo los autores de contenido autorizados para modificar el contenido de control de acceso de una página pueden configurar o modificar este contenido. Esto contrasta con la antigua implementación donde la capacidad de escribir propiedades JCR normales era suficiente, lo que resultó en una escalación de privilegios.

**Nodo de destino definido por la directiva**

Se espera que las políticas de CUG se creen en el nodo JCR que define el subárbol a estar sujeto a acceso restringido de lectura. Es probable que sea una página AEM en caso de que el CUG afecte a todo el árbol.

Tenga en cuenta que colocar la directiva CUG solo en el nodo jcr:content ubicado debajo de una página determinada restringirá el acceso al contenido s.str de una página determinada, pero no tendrá efecto en ningún elemento del mismo nivel o página secundaria. Este puede ser un caso de uso válido y es posible conseguirlo con un editor de repositorios que permita aplicar contenido de acceso fino. Sin embargo, contrasta con la implementación anterior donde la colocación de una propiedad cq:cugEnabled en el nodo jcr:content se reasignó internamente al nodo de página. Esta asignación ya no se realiza.

**Evaluación de permisos con políticas de CUG**

Al pasar del antiguo soporte de CUG a un modelo de autorización adicional, se cambia la forma en que se evalúan los permisos de lectura efectivos. Como se describe en la sección [Documentación de Jackrabbit](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), una entidad de seguridad determinada a la que se permite ver el informe `CUGcontent` solo se concederá acceso de lectura si la evaluación de permisos de todos los modelos configurados en el repositorio Oak concede acceso de lectura.

En otras palabras, para evaluar los permisos efectivos, tanto la variable `CUGPolicy` y las entradas de control de acceso predeterminadas se tendrán en cuenta y el acceso de lectura en el contenido CUG solo se concederá si está concedido por ambos tipos de políticas. En una instalación de publicación AEM predeterminada, donde acceso de lectura al completo `/content` árbol se concede para todos, el efecto de las políticas de CUG será el mismo que con la implementación antigua.

**Evaluación bajo demanda**

El modelo de autorización CUG permite activar individualmente la gestión del control de acceso y la evaluación de permisos:

* la administración del control de acceso está habilitada si el módulo tiene una o varias rutas admitidas en las que se pueden crear CUG
* la evaluación de permisos solo está habilitada si la opción **Evaluación de CUG habilitada** está además activada.

En la nueva evaluación de configuración predeterminada de AEM de las directivas de CUG, solo se habilita con el modo de ejecución &quot;publicar&quot;. Consulte los detalles sobre la [configuración predeterminada desde AEM 6.3](#default-configuration-since-aem) para obtener más información. Esto se puede comprobar comparando las políticas efectivas para una ruta determinada con las políticas almacenadas en el contenido. Las políticas efectivas solo se mostrarán en caso de que se habilite la evaluación de permisos para CUG.

Como se explica más arriba, las políticas de control de acceso de CUG ahora siempre se almacenan en el contenido, pero la evaluación de los permisos efectivos que resultan de esas políticas solo se aplicará si **Evaluación de CUG habilitada** está activado en la consola del sistema en Apache Jackrabbit Oak **Configuración de CUG.** De forma predeterminada, solo está habilitado con el modo de ejecución &quot;publicar&quot;.

### Diferencias Con Respecto A La Autenticación {#differences-with-regards-to-authentication}

A continuación se describen las diferencias con respecto a la autenticación.

#### Tipo De Mixin Dedicado Al Requisito De Autenticación {#dedicated-mixin-type-for-authentication-requirement}

En la implementación anterior, los aspectos de autorización y autenticación de un CUG se activaron mediante una única propiedad JCR ( `cq:cugEnabled`). En cuanto a la autenticación, esto resultó en una lista actualizada de los requisitos de autenticación almacenados con la implementación de Apache Sling Authenticator. Con la nueva implementación se logra el mismo resultado marcando el nodo objetivo con un tipo de mezcla dedicado ( `granite:AuthenticationRequired`).

#### Propiedad Para Excluir La Ruta De Inicio De Sesión {#property-for-excluding-login-path}

El tipo de mezcla define una única propiedad opcional denominada `granite:loginPath`, que básicamente corresponde a la variable `cq:cugLoginPage` propiedad. A diferencia de la implementación anterior, la propiedad de ruta de inicio de sesión solo se respetará si su tipo de nodo declarante es la mezcla mencionada. Añadir una propiedad con ese nombre sin configurar el tipo de mezcla no tendrá ningún efecto y ni un nuevo requisito ni una exclusión para la ruta de inicio de sesión se notificará al autenticador.

#### Privilegio Para Requisito De Autenticación {#privilege-for-authentication-requirement}

La adición o eliminación de un tipo de mezcla requiere `jcr:nodeTypeManagement` privilegio concedido. En la implementación anterior, la variable `jcr:modifyProperties` se utiliza para editar la propiedad residual.

En la medida en que la variable `granite:loginPath` le interesa que se requiera el mismo privilegio para añadir, modificar o eliminar la propiedad.

#### Nodo de destino definido por tipo de mezcla {#target-node-defined-by-mixin-type}

Se espera que los requisitos de autenticación se creen en el nodo JCR que define el subárbol a ser sujeto de inicio de sesión forzado. Es probable que sea una página de AEM en caso de que se espere que el CUG afecte a todo el árbol y la interfaz de usuario para la nueva implementación, en consecuencia, agregue el tipo de mezcla de requisito de autenticación en el nodo de página.

Colocar la directiva CUG solo en el nodo jcr:content ubicado debajo de una página determinada restringirá el acceso al contenido, pero no afectará al nodo de la página en sí ni a ninguna página secundaria.

Este puede ser un escenario válido y es posible con un editor de repositorios que permite colocar la mezcla en cualquier nodo. Sin embargo, el comportamiento contrasta con la implementación anterior, donde la colocación de una propiedad cq:cugEnabled o cq:cugLoginPage en el nodo jcr:content se reasignó internamente en última instancia al nodo de página. Esta asignación ya no se realiza.

#### Rutas compatibles configuradas {#configured-supported-paths}

Ambas `granite:AuthenticationRequired` tipo mixin y la propiedad granite:loginPath solo se respetarán dentro del ámbito definido por el conjunto de **Rutas compatibles** opción de configuración presente con la variable **Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión**. Si no se especifica ninguna ruta, la función de requisito de autenticación se desactiva por completo. En este caso, el tipo de mezcla ni la propiedad tienen efecto cuando se agregan o se establecen en un nodo JCR determinado.

### Asignación del contenido de JCR, servicios de OSGi y configuraciones {#mapping-of-jcr-content-osgi-services-and-configurations}

El documento siguiente proporciona una asignación completa de servicios OSGi, configuraciones y contenido del repositorio entre la implementación antigua y la nueva.

Asignación de CUG desde AEM 6.3

[Obtener archivo](assets/cug-mapping.pdf)

## Actualizar CUG {#upgrade-cug}

### Instalaciones existentes utilizando el CUG obsoleto {#existing-installations-using-the-deprecated-cug}

La implementación de compatibilidad con CUG antigua ha quedado obsoleta y se eliminará para futuras versiones. Se recomienda pasar a las nuevas implementaciones al actualizar desde versiones anteriores a la AEM 6.3.

Para la instalación de AEM actualizada, es importante asegurarse de que solo se habilite una implementación de CUG. La combinación del nuevo y el antiguo soporte de CUG obsoleto no se ha probado y es probable que cause un comportamiento no deseado:

* conflictos en el autenticador de Sling con respecto a los requisitos de autenticación
* acceso de lectura denegado cuando la configuración de ACL asociada con el CUG antiguo entra en conflicto con una nueva directiva CUG.

### Migración de contenido existente de CUG {#migrating-existing-cug-content}

Adobe proporciona una herramienta para migrar a la nueva implementación de CUG. Para utilizarla, realice los pasos siguientes:

1. Vaya a `https://<serveraddress>:<serverport>/system/console/cug-migration` para acceder a la herramienta.
1. Introduzca la ruta raíz para la que desea comprobar los CUGs y presione la tecla **Realizar simulacro** botón. Esto analizará los CUG aptos para la conversión en la ubicación seleccionada.
1. Después de revisar los resultados, presione la tecla **Realizar migración** para migrar a la nueva implementación.

>[!NOTE]
>
>Si tiene problemas, es posible configurar un registrador específico en **DEBUG** nivel en `com.day.cq.auth.impl.cug` para obtener el resultado de la herramienta de migración. Consulte [Registro](/help/sites-deploying/configure-logging.md) para obtener más información sobre cómo hacerlo.
