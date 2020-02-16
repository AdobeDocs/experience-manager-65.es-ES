---
title: Grupos de usuarios cerrados en AEM
seo-title: Grupos de usuarios cerrados en AEM
description: Obtenga información sobre los grupos de usuarios cerrados en AEM.
seo-description: Obtenga información sobre los grupos de usuarios cerrados en AEM.
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
translation-type: tm+mt
source-git-commit: 2142df4f7579e052e18879b437fc43911010b475

---


# Grupos de usuarios cerrados en AEM{#closed-user-groups-in-aem}

## Introducción {#introduction}

Desde AEM 6.3, existe una nueva implementación de Closed User Group destinada a resolver los problemas de rendimiento, escalabilidad y seguridad presentes en la implementación existente.

>[!NOTE]
>
>En aras de la simplicidad, la abreviatura de CUG se utilizará en toda esta documentación.

El objetivo de la nueva implementación es cubrir la funcionalidad existente cuando sea necesario, al mismo tiempo que se tratan los problemas y las limitaciones de diseño de versiones anteriores. El resultado es un nuevo diseño CUG con las siguientes características:

* Separación clara de los elementos de autenticación y autorización, que pueden utilizarse individualmente o en combinación;
* Modelo de autorización dedicado que refleje el acceso restringido de lectura en los árboles CUG configurados sin interferir con otros requisitos de configuración y permisos del control de acceso;
* Separación entre la configuración del control de acceso del acceso de lectura restringido, que suele ser necesaria en las instancias de creación, y la evaluación de permisos, que normalmente solo se desea en la publicación;
* Edición del acceso de lectura restringido sin escalación de privilegios;
* Extensión de tipo de nodo dedicada para marcar el requisito de autenticación;
* Ruta de inicio de sesión opcional asociada con el requisito de autenticación.

### La nueva implementación de grupos de usuarios personalizados {#the-new-custom-user-group-implementation}

Un CUG como se lo conoce en el contexto de AEM consta de los siguientes pasos:

* Restringir el acceso de lectura en el árbol que debe protegerse y permitir solo la lectura para entidades de seguridad que estén enumeradas con una instancia de CUG determinada o excluidas de la evaluación de CUG. Esto se denomina elemento de **autorización** .
* Aplique la autenticación en un árbol determinado y, opcionalmente, especifique una página de inicio de sesión dedicada para ese árbol que se excluya posteriormente. Esto se denomina elemento de **autenticación** .

La nueva implementación se ha diseñado para trazar una línea entre los elementos de autenticación y autorización. A partir de AEM 6.3, es posible restringir el acceso de lectura sin agregar explícitamente un requisito de autenticación. Por ejemplo, si una instancia determinada requiere autenticación por completo o un árbol dado ya reside en un subárbol que ya requiere autenticación.

Del mismo modo, un árbol determinado se puede marcar con un requisito de autenticación sin cambiar la configuración de permisos efectiva. Las combinaciones y los resultados se enumeran en la sección [Combinación de directivas de CUG y Requisito](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) de autenticación.

## Información general {#overview}

### Autorización: Restricción del acceso de lectura {#authorization-restricting-read-access}

La función clave de un CUG es restringir el acceso de lectura en un árbol determinado del repositorio de contenido para todos los usuarios excepto los principales seleccionados. En lugar de manipular el contenido predeterminado del control de acceso sobre la marcha, la nueva implementación adopta un enfoque diferente al definir un tipo dedicado de política de control de acceso que representa un CUG.

#### Directiva de control de acceso para CUG {#access-control-policy-for-cug}

Este nuevo tipo de política tiene las características siguientes:

* Directiva de control de acceso de tipo org.apache.jackrabbit.api.security.authorized.PrincipalSetPolicy (definida por la API de Apache Jackrabbit);
* PrincipalSetPolicy concede privilegios a un conjunto modificable de entidades principales;
* Los privilegios concedidos y el alcance de la política es un detalle de implementación.

La implementación de PrincipalSetPolicy utilizada para representar los CUG también define que:

* Las políticas de CUG solo otorgan acceso de lectura a elementos JCR normales (por ejemplo, se excluye el contenido de control de acceso);
* El ámbito está definido por el nodo controlado de acceso que contiene la directiva CUG;
* Las políticas de CUG se pueden anidar, un CUG anidado inicia un nuevo CUG sin heredar el conjunto principal del CUG &#39;principal&#39;;
* El efecto de la política, si se habilita la evaluación, se hereda a todo el subárbol hasta el siguiente CUG anidado.

Estas directivas de CUG se implementan en una instancia de AEM a través de un módulo de autorización independiente llamado oak-authorized-cug. Este módulo viene con su propia gestión de control de acceso y evaluación de permisos. En otras palabras, la configuración predeterminada de AEM incluye una configuración del repositorio de contenido Oak que combina varios mecanismos de autorización. Para obtener más información, consulte [esta página en la Documentación](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)de Apache Oak.

En esta configuración compuesta, un nuevo CUG no reemplaza el contenido de control de acceso existente adjunto al nodo de destino, sino que está diseñado para ser un suplemento que también se puede eliminar posteriormente sin afectar al control de acceso original, que de forma predeterminada en AEM sería una lista de control de acceso.

A diferencia de la implementación anterior, las nuevas políticas de CUG siempre se reconocen y tratan como contenido de control de acceso. Esto implica que se crean y editan usando la API de administración de control de acceso JCR. Para obtener más información, consulte la sección [Administración de políticas](#managing-cug-policies) de CUG.

#### Evaluación de permisos de las políticas de CUG {#permission-evaluation-of-cug-policies}

Además de una gestión específica del control de acceso para los CUG, el nuevo modelo de autorización permite habilitar condicionalmente la evaluación de permisos para sus políticas. Esto permite configurar las políticas de CUG en un entorno de ensayo y solo permite la evaluación de los permisos efectivos una vez replicados en el entorno de producción.

La evaluación de permisos para las políticas de CUG y la interacción con el modelo predeterminado o con cualquier modelo de autorización adicional sigue el patrón diseñado para múltiples mecanismos de autorización en Apache Jackrabbit Oak: un conjunto determinado de permisos se concede si todos los modelos conceden acceso y sólo si lo hacen. Consulte [esta página](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) para obtener más detalles.

Las siguientes características se aplican a la evaluación de permisos asociada al modelo de autorización diseñado para gestionar y evaluar las políticas de CUG:

* Solo gestiona permisos de lectura para nodos y propiedades normales, pero no lee el contenido del control de acceso
* No gestiona permisos de escritura ni ningún tipo de permisos requeridos para la modificación del contenido de JCR protegido (control de acceso, información de tipo de nodo, control de versiones, bloqueo o administración de usuarios, entre otros); Estos permisos no se ven afectados por una directiva CUG y no serán evaluados por el modelo de autorización asociado. La concesión de estos permisos depende de los otros modelos configurados en la configuración de seguridad.

El efecto de una política de CUG única en la evaluación de los permisos puede resumirse de la siguiente manera:

* Se deniega el acceso de lectura a todos los usuarios, excepto a los sujetos que contengan principios o principios excluidos enumerados en la política;
* La política surte efecto en el nodo controlado de acceso que contiene la política y sus propiedades;
* El efecto se hereda adicionalmente en la jerarquía, es decir, el árbol de elementos definido por el nodo controlado de acceso;
* Sin embargo, no afecta a los hermanos ni a los ancestros del nodo controlado de acceso;
* La herencia de un CUG determinado se detiene en un CUG anidado.

#### Prácticas recomendadas {#best-practices}

Se deben tener en cuenta las siguientes prácticas recomendadas para definir el acceso restringido de lectura a través de los grupos de usuarios:

* Tome una decisión consciente sobre si su necesidad de un CUG es restringir el acceso de lectura o un requisito de autenticación. En el caso de estos últimos o si es necesario ambos, consulte la sección de optimizaciones para obtener detalles sobre el requisito de autenticación
* Cree un modelo de amenaza para los datos o el contenido que debe protegerse para identificar los límites de amenaza y obtener una imagen clara sobre la sensibilidad de los datos y las funciones asociadas con el acceso autorizado
* Modele el contenido del repositorio y los CUGs teniendo en cuenta los aspectos generales relacionados con la autorización y las prácticas recomendadas:

   * Recuerde que el permiso de lectura sólo se concederá si un CUG determinado y la evaluación de otros módulos implementados en la concesión de configuración permiten que un sujeto determinado lea un elemento de repositorio determinado
   * Evite crear CUG redundantes en los que el acceso de lectura ya esté restringido por otros módulos de autorización
   * Una necesidad excesiva de CUG anidados podría resaltar problemas en el diseño de contenido
   * Una necesidad muy excesiva de CUG (por ejemplo, en cada página) puede indicar la necesidad de un modelo de autorización personalizado que se adapte mejor a las necesidades de seguridad específicas de la aplicación y del contenido en cuestión.

* Limite las rutas admitidas para las directivas de CUG a algunos árboles del repositorio para permitir un rendimiento optimizado. Por ejemplo, permita únicamente CUG por debajo del nodo /content como se envía como valor predeterminado desde AEM 6.3.
* Las políticas de CUG están diseñadas para otorgar acceso de lectura a un pequeño conjunto de principios. La necesidad de contar con un gran número de directores puede poner de relieve cuestiones relacionadas con el contenido o el diseño de la aplicación y debe reconsiderarse.

### Autenticación: Definición del requisito de autenticación {#authentication-defining-the-auth-requirement}

Las partes relacionadas con la autenticación de la función CUG permiten marcar los árboles que requieren autenticación y, opcionalmente, especificar una página de inicio de sesión dedicada. De acuerdo con la versión anterior, la nueva implementación permite marcar los árboles que requieren autenticación en el repositorio de contenido y habilitar condicionalmente la sincronización con el `Sling org.apache.sling.api.auth.Authenticator`responsable de hacer cumplir finalmente el requisito y redirigir a un recurso de inicio de sesión.

Estos requisitos se registran en el autenticador mediante un servicio OSGi que proporciona la propiedad de `sling.auth.requirements` registro. Estas propiedades se utilizan para ampliar dinámicamente los requisitos de autenticación. Para obtener más información, consulte la documentación de [Sling](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### Definición del requisito de autenticación con un tipo de mezcla dedicado {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

Por razones de seguridad, la nueva implementación reemplaza el uso de una propiedad JCR residual por un tipo de mezcla dedicado llamado `granite:AuthenticationRequired`, que define una única propiedad opcional de tipo STRING para la ruta de inicio de sesión `granite:loginPath`. Solo los cambios de contenido relacionados con este tipo de mezcla llevarán a la actualización de los requisitos registrados con Apache Sling Authenticator. Las modificaciones se rastrean al persistir cualquier modificación transitoria y, por lo tanto, requieren una `javax.jcr.Session.save()` llamada para ser efectivas.

Lo mismo se aplica a la `granite:loginPath` propiedad. Sólo se respetará si está definida por el tipo de mezcla correspondiente al requisito de autenticación. Agregar una propiedad residual con este mismo nombre en un nodo JCR no estructurado no mostrará el efecto deseado y el controlador responsable de actualizar el registro OSGi ignorará la propiedad.

>[!NOTE]
>
>La configuración de la propiedad de ruta de inicio de sesión es opcional y solo es necesaria si el árbol que requiere autenticación no puede volver a la página de inicio de sesión predeterminada o heredada de otro modo. Consulte la [Evaluación de la ruta](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) de inicio de sesión a continuación.

#### Registro del requisito de autenticación y la ruta de inicio de sesión con el autenticador de Sling {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

Dado que se espera que este tipo de requisito de autenticación se limite a ciertos modos de ejecución y a un pequeño subconjunto de árboles dentro del repositorio de contenido, el seguimiento del tipo de combinación de requisitos y las propiedades de ruta de inicio de sesión es condicional y está enlazado a una configuración correspondiente que define las rutas admitidas (consulte Opciones de configuración más abajo). Por lo tanto, solo los cambios dentro del ámbito de estas rutas admitidas activarán una actualización del registro OSGi, ya que en otros lugares se omitirán tanto el tipo de mezcla como la propiedad.

La configuración predeterminada de AEM ahora utiliza esta configuración, ya que permite establecer la mezcla en el modo de ejecución del autor pero solo tiene efecto en la replicación a la instancia de publicación. Consulte [esta página](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) para obtener más información sobre cómo Sling aplica los requisitos de autenticación.

Al agregar el tipo de `granite:AuthenticationRequired` mezcla dentro de las rutas configuradas admitidas, el registro OSGi del controlador responsable se actualizará y contendrá una nueva entrada adicional con la `sling.auth.requirements` propiedad. Si un requisito de autenticación dado especifica la `granite:loginPath` propiedad opcional, el valor se registra además con el autenticador con un prefijo &#39;-&#39; para ser excluido del requisito de autenticación.

#### Evaluación y herencia del requisito de autenticación {#evaluation-and-inheritance-of-the-authentication-requirement}

Se espera que los requisitos de autenticación de Apache Sling se hereden a través de la jerarquía de páginas o nodos. Los detalles de la herencia y la evaluación de los requisitos de autenticación, como el orden y la precedencia, se consideran un detalle de implementación y no se documentarán en este artículo.

#### Evaluación de la ruta de inicio de sesión {#evaluation-of-login-path}

La evaluación de la ruta de inicio de sesión y la redirección al recurso correspondiente tras la autenticación es actualmente un detalle de implementación del controlador de autenticación del selector de inicio de sesión de Adobe Granite ( `com.day.cq.auth.impl.LoginSelectorHandler`), que es un controlador de autenticación de Apache Sling configurado con AEM de forma predeterminada.

Al llamar a `AuthenticationHandler.requestCredentials` este controlador se intenta determinar la página de inicio de sesión de asignación a la que se redirigirá al usuario. Esto incluye los siguientes pasos:

* Distinguir entre la contraseña caducada y la necesidad de iniciar sesión regularmente como motivo para la redirección;
* En el caso de un inicio de sesión normal, prueba si se puede obtener una ruta de inicio de sesión en el siguiente orden:

   * desde LoginPathProvider tal como lo implementa el nuevo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * desde la implementación anterior y obsoleta de CUG,
   * desde Asignaciones de página de inicio de sesión, tal como se define con el `LoginSelectorHandler`,
   * y, finalmente, devuelve a la página de inicio de sesión predeterminada, tal como se define en la `LoginSelectorHandler`.

* Tan pronto como se obtuvo una ruta de inicio de sesión válida a través de las llamadas enumeradas anteriormente, la solicitud del usuario se redirigirá a esa página.

El objetivo de esta documentación es la evaluación de la ruta de inicio de sesión tal como la expone la `LoginPathProvider` interfaz interna. La implementación enviada desde AEM 6.3 se comporta de la siguiente manera:

* El registro de las rutas de inicio de sesión depende de la distinción entre la contraseña caducada y la necesidad de un inicio de sesión regular como motivo para la redirección
* En caso de inicio de sesión normal, compruebe si se puede obtener una ruta de inicio de sesión en el siguiente orden:

   * a partir de la `LoginPathProvider` aplicación por el nuevo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * desde la implementación anterior y obsoleta de CUG,
   * desde las asignaciones de página de inicio de sesión definidas con la `LoginSelectorHandler`,
   * y finalmente se devuelve a la página de inicio de sesión predeterminada, tal como se define con el `LoginSelectorHandler`.

* Tan pronto como se obtuvo una ruta de inicio de sesión válida a través de las llamadas enumeradas anteriormente, la solicitud del usuario se redirigirá a esa página.

La `LoginPathProvider` implementación de la nueva compatibilidad con requisitos de autenticación en Granite expone las rutas de inicio de sesión definidas por las `granite:loginPath` propiedades, que a su vez se definen por el tipo de mezcla como se describe anteriormente. La asignación de la ruta del recurso que contiene la ruta de inicio de sesión y el valor de propiedad en sí se mantiene en la memoria y se evaluará para encontrar una ruta de inicio de sesión adecuada para otros nodos de la jerarquía.

>[!NOTE]
>
>La evaluación solo se realiza para solicitudes asociadas con recursos que se encuentran en las rutas configuradas admitidas. Para cualquier otra solicitud se evaluarán las formas alternativas de determinar la ruta de inicio de sesión.

#### Prácticas recomendadas {#best-practices-1}

Al definir los requisitos de autenticación, deben tenerse en cuenta las siguientes prácticas recomendadas:

* Evite anidar los requisitos de autenticación: la colocación de un marcador de requisito de autenticación único al principio de un árbol debe ser suficiente y se hereda a todo el subárbol definido por el nodo de destino. Los requisitos de autenticación adicionales dentro de ese árbol deben considerarse redundantes y pueden provocar problemas de rendimiento al evaluar el requisito de autenticación dentro de Apache Sling. Con la separación de las áreas de CUG relacionadas con la autorización y autenticación, es posible restringir el acceso de lectura mediante CUG u otro tipo de políticas, al mismo tiempo que se aplica la autenticación para todo el árbol.
* Cree modelos de contenido de repositorio de modo que los requisitos de autenticación se apliquen para todo el árbol sin necesidad de excluir de nuevo los subárboles anidados.
* Para evitar especificar y registrar posteriormente rutas de inicio de sesión redundantes:

   * depender de la herencia y evitar definir rutas de inicio de sesión anidadas,
   * no establezca la ruta de inicio de sesión opcional en un valor que corresponda al valor predeterminado o heredado,
   * los desarrolladores de aplicaciones deben identificar qué rutas de inicio de sesión deben configurarse en las configuraciones globales de ruta de inicio de sesión (tanto predeterminadas como asignaciones) asociadas con el `LoginSelectorHandler`.

## Representación en el repositorio {#representation-in-the-repository}

### Representación de directivas de CUG en el repositorio {#cug-policy-representation-in-the-repository}

La documentación de Oak cubre cómo se reflejan las nuevas políticas de CUG en el contenido del repositorio. Para obtener más información, consulte [esta página](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### Requisito de autenticación en el repositorio {#authentication-requirement-in-the-repository}

La necesidad de un requisito de autenticación independiente se refleja en el contenido del repositorio con un tipo de nodo mixin dedicado ubicado en el nodo de destino. El tipo de mezcla define una propiedad opcional para especificar una página de inicio de sesión dedicada para el árbol definido por el nodo de destino.

La página asociada con la ruta de inicio de sesión puede ubicarse dentro o fuera de ese árbol. Se excluirá del requisito de autenticación.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## Administración de directivas de CUG y requisitos de autenticación {#managing-cug-policies-and-authentication-requirement}

### Administración de directivas de CUG {#managing-cug-policies}

El nuevo tipo de políticas de control de acceso para restringir el acceso de lectura para un CUG se administra mediante la API de administración de control de acceso JCR y sigue los mecanismos descritos con la especificación [](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html)JCR 2.0.

#### Definir una nueva directiva de CUG {#set-a-new-cug-policy}

Código para aplicar una nueva directiva CUG en un nodo que no tenía un CUG establecido anteriormente. Tenga en cuenta que solo `getApplicablePolicies` devolverá nuevas directivas que no se hayan establecido anteriormente. Al final, la política debe ser reescrita y los cambios deben mantenerse.

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

#### Editar una directiva de CUG existente {#edit-an-existing-cug-policy}

Se necesitan los siguientes pasos para editar una directiva CUG existente. Tenga en cuenta que la política modificada debe escribirse de nuevo y que los cambios deben mantenerse usando `javax.jcr.Session.save()`.

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

La administración del control de acceso JCR define un método de mejor esfuerzo para recuperar las directivas que surten efecto en una ruta determinada. Debido al hecho de que la evaluación de las directivas de CUG es condicional y depende de la configuración correspondiente para habilitarse, la llamada `getEffectivePolicies` es una manera conveniente de verificar si una determinada directiva de CUG está surtiendo efecto en una instalación determinada.

>[!NOTE]
>
>Tenga en cuenta la diferencia entre `getEffectivePolicies` y el ejemplo de código subsiguiente que sube por la jerarquía para averiguar si una ruta determinada ya forma parte de un CUG existente.

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

Buscar todos los CUG anidados que se han definido en una ruta determinada, independientemente de si tienen o no efecto. Para obtener más información, consulte la sección Opciones [de configuración](/help/sites-administering/closed-user-groups.md#configuration-options) .

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

#### Administración de políticas de CUG por sector {#managing-cug-policies-by-pincipal}

Las extensiones definidas por `JackrabbitAccessControlManager` que permiten editar las directivas de control de acceso por principal no se implementan con la administración de control de acceso CUG, ya que por definición una política de CUG siempre afecta a todos los principios: a los enumerados con el `PrincipalSetPolicy` se les concede acceso de lectura, mientras que a todos los demás principios se les impedirá leer contenido en el árbol definido por el nodo de destino.

Los métodos correspondientes siempre devuelven una matriz de directivas vacía, pero no generan excepciones.

### Administración del requisito de autenticación {#managing-the-authentication-requirement}

La creación, modificación o eliminación de nuevos requisitos de autenticación se logra cambiando el tipo de nodo efectivo del nodo de destino. La propiedad opcional de ruta de inicio de sesión se puede escribir usando la API JCR normal.

>[!NOTE]
>
>Las modificaciones a un nodo de destino determinado mencionadas anteriormente solo se reflejarán en Apache Sling Authenticator si el `RequirementHandler` se ha configurado y el destino está contenido en los árboles definidos por las rutas admitidas (consulte la sección Opciones de configuración).
>
>Para obtener más información, consulte [Asignación de tipos]de nodos de mezcla (https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3ón de tipos de nodos de mezcla) y [Adición de nodos y definición de propiedades](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4ón de nodos y definición de propiedades)

#### Adición de un nuevo requisito de autenticación {#adding-a-new-auth-requirement}

A continuación se detallan los pasos para crear un nuevo requisito de autenticación. Tenga en cuenta que el requisito solo se registrará en Apache Sling Authenticator si `RequirementHandler` se ha configurado para el árbol que contiene el nodo de destino.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### Agregar un nuevo requisito de autenticación con la ruta de inicio de sesión {#add-a-new-auth-requirement-with-login-path}

Pasos para crear un nuevo requisito de autenticación, incluida una ruta de inicio de sesión. Tenga en cuenta que el requisito y la exclusión de la ruta de inicio de sesión solo se registrarán en el autenticador Apache Sling si el `RequirementHandler` árbol que contiene el nodo de destino ha sido configurado.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### Modificar una ruta de inicio de sesión existente {#modify-an-existing-login-path}

A continuación se detallan los pasos para cambiar una ruta de inicio de sesión existente. La modificación solo se registrará en el autenticador de Apache Sling si el `RequirementHandler` árbol que contiene el nodo de destino se ha configurado. El valor de ruta de inicio de sesión anterior se eliminará del registro. Esta modificación no afecta al requisito de autenticación asociado con el nodo de destino.

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

Pasos para eliminar una ruta de inicio de sesión existente. La entrada de ruta de inicio de sesión solo se cancelará del autenticador de Apache Sling si el `RequirementHandler` árbol que contiene el nodo de destino está configurado. El requisito de autenticación asociado con el nodo de destino no se ve afectado.

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

Pasos para eliminar un requisito de autenticación existente. El requisito solo se anulará del registro del autenticador de Apache Sling si el `RequirementHandler` ha sido configurado para el árbol que contiene el nodo de destino.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### Recuperar requisitos de autenticación efectivos {#retrieve-effective-auth-requirements}

No hay ninguna API pública dedicada a leer todos los requisitos de autenticación efectivos registrados en Apache Sling Authenticator. Sin embargo, la lista se muestra en la consola del sistema en `https://<serveraddress>:<serverport>/system/console/slingauth` la sección &quot;Configuración **de requisitos de** autenticación&quot;.

La siguiente imagen muestra los requisitos de autenticación de una instancia de publicación de AEM con contenido de demostración. La ruta resaltada de la página de comunidad ilustra cómo un requisito agregado por la implementación descrita en este documento se refleja en el autenticador Apache Sling.

>[!NOTE]
>
>En este ejemplo no se estableció la propiedad de ruta de inicio de sesión opcional. Por consiguiente, no se ha registrado ninguna segunda entrada en el autenticador.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### Recuperar la ruta de inicio de sesión efectiva {#retrieve-the-effective-login-path}

Actualmente no hay ninguna API pública para recuperar la ruta de inicio de sesión que surtirá efecto al acceder de forma anónima a un recurso que requiere autenticación. Consulte la sección Evaluación de la ruta de inicio de sesión para obtener detalles de implementación sobre cómo se recupera la ruta de inicio de sesión.

Sin embargo, tenga en cuenta que, aparte de las rutas de inicio de sesión definidas con esta función, existen otras formas de especificar la redirección al inicio de sesión, que deben tenerse en cuenta al diseñar el modelo de contenido y los requisitos de autenticación de una instalación de AEM determinada.

#### Recuperar el requisito de autenticación heredado {#retrieve-the-inherited-auth-requirement}

Al igual que con la ruta de inicio de sesión, no hay ninguna API pública para recuperar los requisitos de autenticación heredados definidos en el contenido. El siguiente ejemplo ilustra cómo enumerar todos los requisitos de autenticación que se han definido con una jerarquía determinada, independientemente de si tienen o no efecto. Para obtener más información, consulte Opciones [de configuración](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>Se recomienda depender del mecanismo de herencia tanto para los requisitos de autenticación como para la ruta de inicio de sesión, y evitar la creación de requisitos de autenticación anidados.
>
>Para obtener más información, consulte [Evaluación y herencia del requisito](#evaluation-and-inheritance-of-the-authentication-requirement)de autenticación, [Evaluación de la ruta](#evaluation-of-login-path) de inicio de sesión y [Optimizaciones](#best-practices).

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

### Combinación de directivas de CUG y el requisito de autenticación {#combining-cug-policies-and-the-authentication-requirement}

En la tabla siguiente se enumeran las combinaciones válidas de políticas CUG y el requisito de autenticación en una instancia de AEM que tiene ambos módulos habilitados mediante la configuración.

| **Autenticación obligatoria** | **Ruta de inicio de sesión** | **Acceso de lectura restringido** | **Efecto esperado** |
|---|---|---|---|
| Sí | Sí | Sí | Un usuario determinado solo podrá ver el subárbol marcado con la política CUG si la evaluación de permisos efectiva otorga acceso. Un usuario no autenticado será redirigido a la página de inicio de sesión especificada. |
| Sí | No | Sí | Un usuario determinado solo podrá ver el subárbol marcado con la política CUG si la evaluación de permisos efectiva otorga acceso. Un usuario no autenticado será redirigido a una página de inicio de sesión predeterminada heredada. |
| Sí | Sí | No | Un usuario no autenticado será redirigido a la página de inicio de sesión especificada. Si se permite o no ver el árbol marcado con el requisito de autenticación depende de los permisos efectivos de los elementos individuales contenidos en ese subárbol. No hay ningún CUG dedicado que restrinja el acceso de lectura. |
| Sí | No | No | Un usuario no autenticado será redirigido a una página de inicio de sesión predeterminada heredada. El permiso para ver o no el árbol marcado con el requisito de autenticación depende de los permisos efectivos de los elementos individuales contenidos en ese subárbol. No hay ningún CUG dedicado que restrinja el acceso de lectura. |
| No | No | Sí | Un usuario autenticado o no autenticado determinado solo podrá ver el subárbol marcado con la directiva CUG si la evaluación de permisos efectiva otorga acceso. Un usuario no autenticado será tratado de manera equitativa y no se le redirigirá al inicio de sesión. |

>[!NOTE]
>
>La combinación de &#39;Requisito de autenticación&#39; = No y &#39;Ruta de inicio de sesión&#39; = Sí no aparece en la lista anterior, ya que &#39;Ruta de inicio de sesión&#39; es un atributo opcional asociado a un requisito de autenticación. Especificar una propiedad JCR con ese nombre sin agregar el tipo de mezcla que define no tendrá ningún efecto y será ignorada por el controlador correspondiente.

## Componentes y configuración OSGi {#osgi-components-and-configuration}

En esta sección se proporciona una visión general de los componentes OSGi y las opciones de configuración individuales introducidas con la nueva implementación de CUG.

Consulte también la documentación de asignación de CUG para obtener una asignación completa de las opciones de configuración entre la implementación antigua y la nueva.

### Autorización: Configuración y configuración {#authorization-setup-and-configuration}

Las piezas nuevas relacionadas con la autorización se encuentran en el paquete de autorización **de** Oak CUG ( `org.apache.jackrabbit.oak-authorization-cug`), que forma parte de la instalación predeterminada de AEM. El paquete define un modelo de autorización separado que se va a implementar como una forma adicional de administrar el acceso de lectura.

#### Configuración de la autorización de CUG {#setting-up-cug-authorization}

La configuración de la autorización de CUG se describe en detalle en la Documentación [](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)pertinente de Apache. De forma predeterminada, AEM tiene la autorización de CUG implementada en todos los modos de ejecución. Las instrucciones paso a paso también pueden utilizarse para desactivar la autorización de CUG en aquellas instalaciones que requieran una configuración de autorización diferente.

#### Configuración del filtro de referente {#configuring-the-referrer-filter}

También debe configurar el filtro [de referente de](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) Sling con todos los nombres de host que se puedan utilizar para acceder a AEM; por ejemplo, a través de CDN, Equilibrador de carga y otros.

Si el filtro de referente no está configurado, se ven errores similares a los siguientes cuando un usuario intenta iniciar sesión en un sitio de CUG:

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### Características de los componentes de OSGi {#characteristics-of-osgi-components}

Se han introducido los dos componentes OSGi siguientes para definir los requisitos de autenticación y especificar las rutas de inicio de sesión dedicadas:

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorized.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>Etiqueta</td>
   <td> Configuración de Apache Jackrabbit Oak CUG</td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>Configuración de autorización dedicada a configurar y evaluar los permisos de CUG.</td>
  </tr>
  <tr>
   <td>Propiedades de configuración</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>Consulte también Opciones <a href="#configuration-options">de configuración</a> a continuación.</p> </td>
  </tr>
  <tr>
   <td>Directiva de configuración</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Referencias</td>
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td>
  </tr>
 </tbody>
</table>

**org.apache.jackrabbit.oak.spi.security.authorized.cug.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>Etiqueta</td>
   <td> Lista de exclusión de Apache Jackrabbit Oak CUG</td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>Permite excluir los principales con los nombres configurados de la evaluación CUG.</td>
  </tr>
  <tr>
   <td>Propiedades de configuración</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>Consulte también la sección Opciones de configuración a continuación.</p> </td>
  </tr>
  <tr>
   <td>Directiva de configuración</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Referencias</td>
   <td>ND</td>
  </tr>
 </tbody>
</table>

#### Configuration Options {#configuration-options}

Las opciones de configuración clave son:

* `cugSupportedPaths`:: especifique los subárboles que pueden contener CUG. No se ha establecido ningún valor predeterminado
* `cugEnabled`:: para habilitar la evaluación de permisos para las directivas de CUG actuales.

Las opciones de configuración disponibles asociadas con el módulo de autorización de CUG se enumeran y describen con más detalle en la Documentación [de](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration)Apache Oak.

#### Exclusión de los principales de la evaluación de CUG {#excluding-principals-from-cug-evaluation}

Se ha adoptado la exención de los principios individuales de la evaluación del CUG de la aplicación anterior. La nueva autorización de CUG cubre esto con una interfaz dedicada llamada CugExclude. Apache Jackrabbit Oak 1.4 se suministra con una implementación predeterminada que excluye un conjunto fijo de entidades principales, así como una implementación ampliada que permite configurar nombres principales individuales. Este último se configura en instancias de publicación de AEM.

El valor predeterminado desde AEM 6.3 impide que las directivas CUG afecten a las siguientes entidades principales:

* entidades de administración (usuario administrador, grupo de administradores)
* principales de usuarios de servicios
* principal del sistema interno del repositorio

Para obtener más información, consulte la tabla que aparece a continuación en la sección Configuración [predeterminada desde AEM 6.3](#default-configuration-since-aem) .

La exclusión del grupo &#39;administradores&#39; se puede modificar o expandir en la consola del sistema en la sección de configuración de la Lista **de exclusión de** Apache Jackrabbit Oak CUG.

Como alternativa, es posible proporcionar e implementar una implementación personalizada de la interfaz CugExclude para ajustar el conjunto de principios excluidos en caso de necesidades especiales. Consulte la documentación sobre la [capacidad de conexión](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) de CUG para obtener más detalles y una implementación de ejemplo.

### Autenticación: Configuración y configuración {#authentication-setup-and-configuration}

Las partes nuevas relacionadas con la autenticación se encuentran en el paquete **Adobe Granite Authentication Handler** (versión 5.6.48 `com.adobe.granite.auth.authhandler` ). Este paquete forma parte de la instalación predeterminada de AEM.

Para configurar la sustitución de requisitos de autenticación para la compatibilidad con CUG obsoleta, algunos componentes OSGi deben estar presentes y activos en una instalación de AEM determinada. Para obtener más información, consulte **Características de los componentes** OSGi más adelante.

>[!NOTE]
>
>Debido a la opción de configuración obligatoria con RequirementHandler, las partes relacionadas con la autenticación solo estarán activas si la función se ha habilitado especificando un conjunto de rutas admitidas. Con una instalación estándar de AEM, la función está deshabilitada en el modo de ejecución de autor y habilitada para /content en el modo de ejecución de publicación.

**Características de los componentes de OSGi**

Se han introducido los 2 componentes OSGi siguientes para definir los requisitos de autenticación y especificar las rutas de inicio de sesión dedicadas:

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
   <td>Servicio OSGi dedicado para los requisitos de autenticación que registra a un observador de los cambios de contenido que afectan a los requisitos de autenticación (a través del tipo de <code>granite:AuthenticationRequirement</code> mezcla) y las rutas de inicio de sesión con están expuestas al <code>LoginSelectorHandler</code>. </td>
  </tr>
  <tr>
   <td>Propiedades de configuración</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Directiva de configuración</td>
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

| Etiqueta |  Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión |
|---|---|
| Descripción | `RequirementHandler` que actualiza los requisitos de autenticación de Apache Sling y la exclusión correspondiente para las rutas de inicio de sesión asociadas. |
| Propiedades de configuración | `supportedPaths` |
| Directiva de configuración | `ConfigurationPolicy.REQUIRE` |
| Referencias | ND |

#### Configuration Options {#configuration-options-1}

Las partes relacionadas con la autenticación de la reescritura CUG solo incluyen una única opción de configuración asociada con el requisito de autenticación de Adobe Granite y el controlador de ruta de inicio de sesión:

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
   <td>Definir&lt;cadena&gt;</td>
   <td>-</td>
   <td>Rutas en las que este controlador respetará los requisitos de autenticación. Deje esta configuración sin definir si desea agregar el tipo de <code>granite:AuthenticationRequirement</code> mezcla a los nodos sin hacerlos obligatorios (por ejemplo, en instancias de autor). Si falta, la función se desactiva. </td>
  </tr>
 </tbody>
</table>

## Configuración predeterminada desde AEM 6.3 {#default-configuration-since-aem}

Las nuevas instalaciones de AEM utilizarán de forma predeterminada las nuevas implementaciones tanto para las partes relacionadas con la autorización como con la autenticación de la función CUG. La implementación antigua &quot;Compatibilidad con grupos cerrados de usuarios de Adobe Granite (CUG)&quot; se ha quedado obsoleta y se desactivará de forma predeterminada en todas las instalaciones de AEM. Las nuevas implementaciones se habilitarán de la siguiente manera:

### Instancias de autor {#author-instances}

| **&quot;Configuración de Apache Jackrabbit Oak CUG&quot;** | **Explicación** |
|---|---|
| Rutas admitidas `/content` | La administración del control de acceso para CUGpolicy está habilitada. |
| Evaluación de CUG habilitada FALSE | La evaluación de permisos está deshabilitada. Las políticas de CUG no surten efecto. |
| Clasificación | 200 | Consulte la documentación de Oak. |

>[!NOTE]
>
>No hay configuración para la lista **de exclusión de** Apache Jackrabbit Oak CUG, y el requisito de autenticación de **Adobe Granite y el controlador** de ruta de inicio de sesión están presentes en las instancias de creación predeterminadas.

### Instancias de publicación {#publish-instances}

| **&quot;Configuración de Apache Jackrabbit Oak CUG&quot;** | **Explicación** |
|---|---|
| Rutas admitidas `/content` | La administración del control de acceso para directivas CUG está habilitada debajo de las rutas configuradas. |
| Evaluación de CUG habilitada VERDADERA | La evaluación de permisos está habilitada debajo de las rutas configuradas. Las políticas de CUG surten efecto a partir de `Session.save()`. |
| Clasificación | 200 | Consulte la documentación de Oak. |

| **&quot;Lista de exclusión de Apache Jackrabbit Oak CUG&quot;** | **Explicación** |
|---|---|
| Administradores de nombres principales | Excluye a los administradores principales de la evaluación de CUG. |

| **&quot;Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión&quot;** | **Explicación** |
|---|---|
| Rutas admitidas `/content` | Los requisitos de autenticación definidos en el repositorio por medio del tipo de `granite:AuthenticationRequired` mezcla surtirán efecto a continuación `/content` sobre `Session.save()`. Se actualiza Sling Authenticator. Se ignora la adición del tipo de mezcla fuera de las rutas admitidas. |

## Desactivación del requisito de autenticación y autorización de CUG {#disabling-cug-authorization-and-authentication-requirement}

La nueva implementación puede deshabilitarse por completo en caso de que una instalación determinada no utilice CUG o utilice diferentes medios para la autenticación y autorización.

### Deshabilitar autorización de CUG {#disable-cug-authorization}

Consulte la documentación de [conectabilidad](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) de CUG para obtener detalles sobre cómo quitar el modelo de autorización de CUG de la configuración de autorización compuesta.

### Deshabilitar el requisito de autenticación {#disable-the-authentication-requirement}

Para desactivar la compatibilidad con el requisito de autenticación proporcionado por el `granite.auth.authhandler` módulo, basta con quitar la configuración asociada con el requisito de autenticación de **Adobe Granite y el controlador** de ruta de inicio de sesión.

>[!NOTE]
>
>Sin embargo, tenga en cuenta que la eliminación de la configuración no anulará el registro del tipo de mezcla, que aún era aplicable a los nodos sin tener efecto.

## Interacción con otros módulos {#interaction-with-other-modules}

### API de Apache Jackrabbit {#apache-jackrabbit-api}

Para reflejar el nuevo tipo de política de control de acceso utilizada por el modelo de autorización de CUG, se ha ampliado la API definida por Apache Jackrabbit. Desde la versión 2.11.0 del `jackrabbit-api` módulo define una nueva interfaz llamada `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`, que se extiende desde `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

El mecanismo de importación de Apache Jackrabbit FileVault se ha ajustado para lidiar con las políticas de control de acceso del tipo `PrincipalSetPolicy`.

### Distribución de contenido de Apache Sling {#apache-sling-content-distribution}

Consulte la sección anterior [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) .

### Replicación de Adobe Granite {#adobe-granite-replication}

El módulo de replicación se ha ajustado ligeramente para poder replicar las políticas de CUG entre diferentes instancias de AEM:

* `DurboImportConfiguration.isImportAcl()` se interpreta literalmente y sólo afectará a la implementación de las políticas de control de acceso `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` solo respetará esta configuración para ACL verdaderas
* Otras directivas como `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` instancias creadas por el modelo de autorización de CUG siempre se replicarán y se omitirá la opción de configuración `DurboImportConfiguration.isImportAcl`().

Existe una limitación en la replicación de políticas de CUG. Si se elimina una directiva de CUG determinada sin eliminar el tipo de nodo de mezcla correspondiente, la eliminación no se reflejará en la replicación. `rep:CugMixin,` Esto se ha abordado eliminando siempre la mezcla tras la eliminación de la política. No obstante, la limitación puede aparecer si se añade manualmente el tipo de mezcla.

### Adobe Granite Authentication Handler {#adobe-granite-authentication-handler}

El controlador de autenticación **Adobe Granite HTTP Header Authentication Handler** enviado con el `com.adobe.granite.auth.authhandler` paquete contiene una referencia a la `CugSupport` interfaz definida por el mismo módulo. Se utiliza para calcular el &#39;territorio&#39; en determinadas circunstancias, regresando al territorio configurado con el controlador.

Esto se ha ajustado para que la referencia a sea `CugSupport` opcional a fin de garantizar la máxima compatibilidad con versiones anteriores si una configuración determinada decide volver a habilitar la implementación obsoleta. Las instalaciones que utilicen la implementación ya no obtendrán el dominio extraído de la implementación de CUG, pero siempre mostrarán el territorio tal como se define con el controlador de autenticación de encabezado HTTP **Adobe Granite**.

>[!NOTE]
>
>De forma predeterminada, el controlador de autenticación de encabezado HTTP **Adobe Granite solo está configurado en modo de ejecución de publicación con la opción &quot;Deshabilitar página de inicio de sesión&quot; (** `auth.http.nologin`) activada.

### AEM LiveCopy {#aem-livecopy}

La configuración de CUGs junto con LiveCopy se representa en el repositorio mediante la adición de un nodo adicional y una propiedad adicional de la siguiente manera:

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Ambos elementos se crean en la sección `cq:Page`. Con el diseño actual, MSM solo gestiona nodos y propiedades que están debajo del nodo `cq:PageContent` (`jcr:content`).

Por lo tanto, los grupos de CUG no pueden revertirse de un modelo a una Live Copy. Planee esto según corresponda al configurar una Live Copy.

## Cambios en la implementación de nuevo CUG {#changes-with-the-new-cug-implementation}

El objetivo de esta sección es proporcionar una visión general de los cambios realizados en la función de CUG, así como una comparación entre la implementación antigua y la nueva. Enumera los cambios que afectan a la forma en que se configura la compatibilidad con CUG y describe cómo y quién administra los CUG en el contenido del repositorio.

### Diferencias en la configuración y configuración de CUG {#differences-in-cug-setup-and-configuration}

El componente OSGi **Adobe Granite Closed User Group (CUG) Support** ( `com.day.cq.auth.impl.cug.CugSupportImpl`) se ha sustituido por nuevos componentes para poder gestionar por separado las partes relacionadas con la autorización y la autenticación de la antigua funcionalidad CUG.

## Diferencias en la gestión de CUG en el contenido del repositorio {#differences-in-managing-cugs-in-the-repository-content}

Las siguientes secciones describen las diferencias entre las implementaciones antiguas y las nuevas desde las perspectivas de implementación y seguridad. Aunque la nueva implementación tiene como objetivo proporcionar la misma funcionalidad, hay cambios sutiles que es importante conocer al usar el nuevo CUG.

### Diferencias Con Respecto A La Autorización {#differences-with-regards-to-authorization}

Las principales diferencias desde el punto de vista de la autorización se resumen en la siguiente lista:

**Contenido de control de acceso dedicado para grupos de usuarios**

En la implementación anterior, el modelo de autorización predeterminado se utilizó para manipular las directivas de lista de control de acceso al publicar, reemplazando cualquier ACE existente por la configuración establecida por el CUG. Esto se activó al escribir propiedades JCR residuales y regulares que se interpretaron al publicar.

Con la nueva implementación, la configuración del control de acceso del modelo de autorización predeterminado no se ve afectada por ningún CUG que se esté creando, modificando o eliminando. En su lugar, se aplica un nuevo tipo de directiva denominado `PrincipalSetPolicy` como contenido de control de acceso adicional al nodo de destino. Esta directiva adicional se ubicará como un elemento secundario del nodo de destino y, si está presente, sería un elemento secundario del nodo de directiva predeterminado.

**Edición De Políticas De AcuG En La Administración Del Control De Acceso**

Este paso de las propiedades JCR residuales a una política de control de acceso dedicada afecta al permiso necesario para crear o modificar la parte de autorización de la función CUG. Dado que esto se considera una modificación para acceder al contenido de control, requiere `jcr:readAccessControl` y `jcr:modifyAccessControl` privilegios para ser escrito en el repositorio. Por lo tanto, solo los autores de contenido con derecho a modificar el contenido del control de acceso de una página pueden configurar o modificar este contenido. Esto contrasta con la implementación antigua, donde la capacidad de escribir propiedades JCR normales era suficiente, lo que resulta en una escalación de privilegios.

**Nodo de destino definido por la directiva**

Se espera que las políticas de CUG se creen en el nodo JCR que define el subárbol que estará sujeto a acceso de lectura restringido. Es probable que sea una página de AEM en caso de que el CUG afecte a todo el árbol.

Tenga en cuenta que la colocación de la directiva CUG solamente en el nodo jcr:content ubicado debajo de una página determinada restringirá el acceso al contenido s.str de una página determinada pero no tendrá efecto en ninguna página secundaria o página secundaria. Este puede ser un caso de uso válido y es posible conseguirlo con un editor de repositorio que permite aplicar contenido de acceso con precisión. Sin embargo, contrasta con la implementación anterior, donde la colocación de una propiedad cq:cugEnabled en el nodo jcr:content se reasignó internamente al nodo de página. Esta asignación ya no se realiza.

**Evaluación de permisos con políticas de CUG**

Al pasar de la compatibilidad anterior con CUG a un modelo de autorización adicional, se cambia la forma en que se evalúan los permisos de lectura efectivos. Tal como se describe en la documentación [de](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)Jackrabbit, a un determinado principal autorizado a ver el `CUGcontent` sólo se le concederá acceso de lectura si la evaluación de permisos de todos los modelos configurados en el repositorio Oak otorga acceso de lectura.

En otras palabras, para la evaluación de los permisos efectivos, se tendrán en cuenta tanto las entradas de control de acceso `CUGPolicy` como las predeterminadas, y el acceso de lectura en el contenido de CUG solo se concederá si lo conceden ambos tipos de políticas. En una instalación de publicación predeterminada de AEM en la que se concede acceso de lectura al `/content` árbol completo para todos, el efecto de las políticas de CUG será el mismo que con la implementación anterior.

**Evaluación a pedido**

El modelo de autorización de CUG permite activar individualmente la gestión del control de acceso y la evaluación de permisos:

* la administración del control de acceso está habilitada si el módulo tiene una o varias rutas admitidas en las que se pueden crear CUG
* la evaluación de permisos solo está habilitada si la opción Evaluación de **CUG habilitada** está marcada adicionalmente.

En la nueva evaluación de configuración predeterminada de AEM de las directivas de CUG, solo se habilita con el modo de ejecución &#39;publicar&#39;. Consulte los detalles sobre la configuración [predeterminada desde AEM 6.3](#default-configuration-since-aem) para obtener más información. Esto se puede verificar comparando las políticas efectivas de una ruta determinada con las políticas almacenadas en el contenido. Las políticas efectivas solo se mostrarán si la evaluación de permisos para CUG está habilitada.

Como se explicó anteriormente, las políticas de control de acceso de CUG ahora siempre se almacenan en el contenido, pero la evaluación de los permisos efectivos que resultan de esas políticas solo se aplicará si la evaluación de **CUG habilitada** está activada en la consola del sistema en la configuración de Apache Jackrabbit Oak **CUG.** De forma predeterminada, solo se habilita con el modo de ejecución &#39;publicar&#39;.

### Diferencias Con Respecto A La Autenticación {#differences-with-regards-to-authentication}

Las diferencias con respecto a la autenticación se describen a continuación.

#### Tipo De Mezcla Dedicada Para Requisito De Autenticación {#dedicated-mixin-type-for-authentication-requirement}

En la primera implementación, los aspectos de autorización y autenticación de un CUG se activaron con una sola propiedad JCR ( `cq:cugEnabled`). En lo que respecta a la autenticación, esto resultó en una lista actualizada de los requisitos de autenticación tal como se almacenan con la implementación de Apache Sling Authenticator. Con la nueva implementación, el mismo resultado se logra marcando el nodo de destino con un tipo de mezcla dedicado ( `granite:AuthenticationRequired`).

#### Propiedad Para Excluir Ruta De Inicio De Sesión {#property-for-excluding-login-path}

El tipo de mezcla define una única propiedad opcional denominada `granite:loginPath`, que básicamente corresponde a la `cq:cugLoginPage` propiedad. A diferencia de la implementación anterior, la propiedad de ruta de inicio de sesión solo se respetará si su tipo de nodo declarante es la mezcla mencionada. La adición de una propiedad con ese nombre sin configurar el tipo de mezcla no tendrá ningún efecto y ni un nuevo requisito ni una exclusión para la ruta de inicio de sesión se notificarán al autenticador.

#### Privilegio Para El Requisito De Autenticación {#privilege-for-authentication-requirement}

La adición o eliminación de un tipo de mezcla requiere que se conceda `jcr:nodeTypeManagement` privilegios. En la implementación anterior, el `jcr:modifyProperties` privilegio se utiliza para editar la propiedad residual.

En lo que respecta a la propiedad, `granite:loginPath` se requiere el mismo privilegio para añadir, modificar o eliminar la propiedad.

#### Nodo de destino definido por tipo de mezcla {#target-node-defined-by-mixin-type}

Se espera que los requisitos de autenticación se creen en el nodo JCR que define el subárbol para que esté sujeto a un inicio de sesión forzado. Es probable que sea una página de AEM en caso de que el CUG afecte a todo el árbol y la interfaz de usuario para la nueva implementación, en consecuencia, agregue el tipo de mezcla de requisito de autenticación en el nodo de página.

La colocación de la directiva CUG únicamente en el nodo jcr:content situado debajo de una página determinada restringirá el acceso al contenido, pero no afectará al nodo de la página ni a ninguna página secundaria.

Este escenario puede ser válido y es posible con un editor de repositorio que permite colocar la mezcla en cualquier nodo. Sin embargo, el comportamiento contrasta con la implementación anterior, donde la colocación de una propiedad cq:cugEnabled o cq:cugLoginPage en el nodo jcr:content se reasignó internamente al nodo de página. Esta asignación ya no se realiza.

#### Rutas configuradas admitidas {#configured-supported-paths}

Tanto el tipo de `granite:AuthenticationRequired` mezcla como la propiedad granite:loginPath solo se respetarán dentro del ámbito definido por el conjunto de opciones de configuración de rutas **** admitidas presentes con el Requisito de autenticación granite de **Adobe y el controlador de ruta** de inicio de sesión. Si no se especifica ninguna ruta, la función de requisito de autenticación se desactiva por completo. En este caso, el tipo de mezcla y la propiedad surten efecto al agregarse o establecerse en un nodo JCR determinado.

### Asignación del contenido de JCR, los servicios de OSGi y las configuraciones {#mapping-of-jcr-content-osgi-services-and-configurations}

El documento que se muestra a continuación proporciona una asignación completa de los servicios, las configuraciones y el contenido del repositorio OSGi entre la implementación antigua y la nueva.

Asignación de CUG desde AEM 6.3

[Obtener archivo](assets/cug-mapping.pdf)

## Actualizar CUG {#upgrade-cug}

### Instalaciones existentes con el CUG obsoleto {#existing-installations-using-the-deprecated-cug}

La implementación anterior de la compatibilidad con CUG se ha quedado obsoleta y se eliminará en versiones futuras. Se recomienda pasar a las nuevas implementaciones al actualizar desde versiones anteriores a AEM 6.3.

Para la instalación de AEM actualizada, es importante asegurarse de que solo está habilitada una implementación de CUG. La combinación de la compatibilidad con CUG nueva y antigua, obsoleta, no se prueba y es probable que cause un comportamiento no deseado:

* colisiones en el Sling Authenticator con respecto a los requisitos de autenticación
* se denegó el acceso de lectura cuando la configuración de ACL asociada con el CUG antiguo entra en conflicto con una nueva directiva de CUG.

### Migración de contenido existente de CUG {#migrating-existing-cug-content}

Adobe proporciona una herramienta para migrar a la nueva implementación de CUG. Para utilizarlo, realice los siguientes pasos:

1. Vaya a `https://<serveraddress>:<serverport>/system/console/cug-migration` para acceder a la herramienta.
1. Introduzca la ruta raíz para la que desea comprobar los CUG y pulse el botón **Realizar ejecución** en seco. Esto analizará los CUG que pueden convertirse en la ubicación seleccionada.
1. Después de revisar los resultados, presione el botón **Realizar migración** para migrar a la nueva implementación.

>[!NOTE]
>
>Si tiene problemas, es posible configurar un registrador específico a nivel **DEBUG** en `com.day.cq.auth.impl.cug` para obtener el resultado de la herramienta de migración. Consulte [Registro](/help/sites-deploying/configure-logging.md) para obtener más información sobre cómo hacerlo.

