---
title: Grupos de usuarios cerrados en AEM
description: AEM Obtenga información acerca de los grupos de usuarios cerrados y las ventajas que aportan a la escalabilidad y la seguridad en los grupos de usuarios que tienen acceso a los servicios de.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '6816'
ht-degree: 0%

---

# Grupos de usuarios cerrados en AEM{#closed-user-groups-in-aem}

## Introducción {#introduction}

AEM Desde la versión 6.3, existe una nueva implementación de grupo cerrado de usuarios diseñada para abordar los problemas de rendimiento, escalabilidad y seguridad presentes en la implementación existente.

>[!NOTE]
>
>Para simplificar, en esta documentación se utiliza la abreviatura CUG.

El objetivo de la nueva implementación es cubrir la funcionalidad existente donde sea necesario y, al mismo tiempo, abordar los problemas y las limitaciones de diseño de versiones anteriores. El resultado es un nuevo diseño de CUG con las siguientes características:

* una clara separación de los elementos de autenticación y autorización, que pueden utilizarse de forma individual o combinada;
* Modelo de autorización dedicado para reflejar el acceso de lectura restringido en los árboles de CUG configurados sin interferir en otros requisitos de configuración y permiso de control de acceso;
* Separación entre la configuración de control de acceso del acceso de lectura restringido, que suele ser necesario en instancias de creación, y la evaluación de permisos, que normalmente solo se desea en la publicación;
* Edición de acceso de lectura restringido sin escalación de privilegios;
* Extensión de tipo de nodo dedicada para marcar el requisito de autenticación.
* Ruta de inicio de sesión opcional asociada al requisito de autenticación.

### La nueva implementación del grupo de usuarios personalizados {#the-new-custom-user-group-implementation}

AEM Un CUG, tal como se le conoce en el contexto de la creación de grupos de usuarios, consta de los siguientes pasos:

* Restrinja el acceso de lectura en el árbol que necesita protegerse y permita la lectura solo para las entidades principales que estén enumeradas con una instancia de CUG determinada o excluidas por completo de la evaluación de CUG. Esto se denomina **autorización** Elemento.
* Haga cumplir la autenticación en un árbol determinado y, opcionalmente, especifique una página de inicio de sesión dedicada para ese árbol que se excluya posteriormente. Esto se denomina **authentication** Elemento.

La nueva implementación se ha diseñado para trazar una línea entre los elementos de autenticación y autorización. AEM A partir de la versión 6.3, se puede restringir el acceso de lectura sin añadir explícitamente un requisito de autenticación. Por ejemplo, si una instancia determinada requiere autenticación por completo o un árbol determinado ya reside en un subárbol que requiere autenticación.

Del mismo modo, un árbol determinado se puede marcar con un requisito de autenticación sin cambiar la configuración de permisos efectiva. Las combinaciones y los resultados se enumeran en la [Combinación de políticas de CUG y el requisito de autenticación](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) sección.

## Información general {#overview}

### Autorización: Restricción del acceso de lectura {#authorization-restricting-read-access}

La función principal de un CUG es restringir el acceso de lectura a un árbol determinado del repositorio de contenido para todos excepto para las entidades de seguridad seleccionadas. En lugar de manipular el contenido de control de acceso predeterminado sobre la marcha, la nueva implementación adopta un enfoque diferente al definir un tipo dedicado de directiva de control de acceso que representa un CUG.

#### Política de control de acceso para CUG {#access-control-policy-for-cug}

Este nuevo tipo de directiva tiene las siguientes características:

* Política de control de acceso de tipo org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy (definida por la API de Apache Jackrabbit);
* PrincipalSetPolicy otorga privilegios a un conjunto modificable de principales;
* Los privilegios concedidos y el ámbito de la política son detalles de implementación.

La implementación de PrincipalSetPolicy utilizada para representar CUG además define lo siguiente:

* Las políticas de CUG solo conceden acceso de lectura a los elementos JCR normales (por ejemplo, se excluye el contenido de control de acceso).
* El ámbito se define mediante el nodo controlado por acceso que contiene la directiva CUG;
* Las políticas de CUG se pueden anidar, un CUG anidado inicia un nuevo CUG sin heredar el conjunto principal del CUG &quot;principal&quot;.
* El efecto de la directiva, si la evaluación está habilitada, se hereda a todo el subárbol hasta el siguiente CUG anidado.

AEM Estas políticas de CUG se implementan en una instancia de a través de un módulo de autorización independiente denominado oak-authorization-cug. Este módulo incluye su propia administración de control de acceso y evaluación de permisos. AEM En otras palabras, la configuración predeterminada del repositorio de contenido incluye una configuración de Oak que combina varios mecanismos de autorización. Para obtener más información, consulte [esta página contiene la documentación de Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

AEM En esta configuración compuesta, un nuevo CUG no reemplaza el contenido de control de acceso existente adjunto al nodo de destino, sino que está diseñado para ser un complemento que también se puede eliminar más adelante sin afectar al control de acceso original, que de forma predeterminada en la lista de control de acceso sería una lista de control de acceso.

A diferencia de la implementación anterior, las nuevas políticas de CUG siempre se reconocen y tratan como contenido de control de acceso. Esto implica que se crean y editan mediante la API de administración de control de acceso JCR. Para obtener más información, consulte la [Administración de políticas de CUG](#managing-cug-policies) sección.

#### Evaluación de permisos de políticas de CUG {#permission-evaluation-of-cug-policies}

Además de una administración de control de acceso dedicada para los CUG, el nuevo modelo de autorización permite habilitar de forma condicional la evaluación de permisos para sus directivas. Esto permite configurar las políticas de CUG en un entorno de ensayo y habilitar solo la evaluación de los permisos efectivos una vez duplicados en el entorno de producción.

La evaluación de permisos para políticas de CUG y la interacción con el modelo de autorización predeterminado o cualquier modelo de autorización adicional sigue el patrón diseñado para varios mecanismos de autorización en Apache Jackrabbit Oak: un conjunto determinado de permisos se concede si y solo si todos los modelos conceden acceso. Consulte [esta página](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) para obtener más información.

Las siguientes características se aplican a la evaluación de permisos asociada al modelo de autorización diseñado para gestionar y evaluar las políticas de CUG:

* Solo controla los permisos de lectura para nodos y propiedades normales, pero no lee el contenido de control de acceso
* No gestiona permisos de escritura ni ningún tipo de permisos necesarios para la modificación del contenido JCR protegido (control de acceso, información de tipo de nodo, versiones, bloqueo o administración de usuarios, entre otros); Estos permisos no se ven afectados por una directiva CUG y no serán evaluados por el modelo de autorización asociado. La concesión o no de estos permisos depende de los otros modelos configurados en la configuración de seguridad.

El efecto de una única política de CUG sobre la evaluación de permisos se puede resumir de la siguiente manera:

* Se deniega el acceso de lectura a todas las personas, excepto a los sujetos que contienen entidades principales excluidas o entidades principales enumeradas en la directiva.
* La directiva tiene efecto en el nodo controlado por acceso que contiene la directiva y sus propiedades;
* El efecto se hereda adicionalmente en la jerarquía, es decir, el árbol de elementos definido por el nodo controlado por acceso;
* Sin embargo, no afecta a los hermanos ni a los antecesores del nodo controlado por acceso;
* La herencia de un CUG determinado se detiene en un CUG anidado.

#### Prácticas recomendadas {#best-practices}

Se deben tener en cuenta las siguientes prácticas recomendadas para definir el acceso de lectura restringido a través de CUG:

* Tome una decisión consciente sobre si su necesidad de un CUG se trata de restringir el acceso de lectura o de un requisito de autenticación. Si esto último sucede, o si es necesario hacerlo, consulte la sección sobre Prácticas recomendadas para obtener más información sobre el requisito de autenticación
* Cree un modelo de amenazas para los datos o el contenido que debe protegerse para identificar los límites de las amenazas y tener una idea clara de la confidencialidad de los datos y las funciones asociadas con el acceso autorizado
* Modele el contenido del repositorio y los CUG teniendo en cuenta los aspectos generales relacionados con la autorización y las prácticas recomendadas:

   * Recuerde que el permiso de lectura solo se concederá si un CUG determinado y la evaluación de otros módulos implementados en la concesión de configuración permiten que un sujeto determinado lea un elemento de repositorio determinado
   * Evite crear CUG redundantes en los que el acceso de lectura ya está restringido por otros módulos de autorización
   * La necesidad excesiva de CUG anidados puede resaltar problemas en el diseño de contenido
   * Una necesidad muy excesiva de CUG (por ejemplo, en cada página) puede indicar la necesidad de un modelo de autorización personalizado potencialmente más adecuado para satisfacer las necesidades de seguridad específicas de la aplicación y el contenido en cuestión.

* Limite las rutas admitidas para las políticas de CUG a unos pocos árboles en el repositorio para permitir un rendimiento optimizado. AEM Por ejemplo, solo permite CUG debajo del nodo /content como enviado como valor predeterminado desde 6.3.
* Las políticas de CUG están diseñadas para conceder acceso de lectura a un pequeño conjunto de principales. La necesidad de un gran número de principios puede resaltar problemas en el diseño del contenido o la aplicación y debe reconsiderarse.

### Autenticación: Definición del requisito de autenticación {#authentication-defining-the-auth-requirement}

Las partes relacionadas con la autenticación de la función CUG permiten marcar árboles que requieren autenticación y, opcionalmente, especificar una página de inicio de sesión dedicada. De acuerdo con la versión anterior, la nueva implementación permite marcar los árboles que requieren autenticación en el repositorio de contenido y habilitar de forma condicional la sincronización con `Sling org.apache.sling.api.auth.Authenticator`responsable de aplicar finalmente el requisito y redirigir a un recurso de inicio de sesión.

Estos requisitos se registran con el autenticador mediante un servicio OSGi que proporciona el `sling.auth.requirements` propiedad de registro. A continuación, estas propiedades se utilizan para ampliar dinámicamente los requisitos de autenticación. Para obtener más información, consulte la [Documentación de Sling](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### Definición del requisito de autenticación con un tipo de mezcla dedicado {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

Por motivos de seguridad, la nueva implementación reemplaza el uso de una propiedad JCR residual por un tipo de mezcla dedicado denominado `granite:AuthenticationRequired`, que define una única propiedad opcional de tipo CADENA para la ruta de inicio de sesión `granite:loginPath`. Solo los cambios de contenido relacionados con este tipo de mezcla llevarán a una actualización de los requisitos registrados con Apache Sling Authenticator. Las modificaciones se rastrean al mantener cualquier modificación transitoria y, por lo tanto, requieren una `javax.jcr.Session.save()` llame a para que sea efectivo.

Lo mismo se aplica al `granite:loginPath` propiedad. Solo se respetará si está definido por el tipo de mezcla relacionado con el requisito de autenticación. Si se agrega una propiedad residual con este mismo nombre en un nodo JCR no estructurado, no se mostrará el efecto deseado y el controlador responsable de actualizar el registro OSGi ignorará la propiedad.

>[!NOTE]
>
>La configuración de la propiedad de ruta de acceso de inicio de sesión es opcional y solo es necesaria si el árbol que requiere autenticación no puede volver a la página de inicio de sesión predeterminada o heredada de otro modo. Consulte la [Evaluación de la ruta de inicio de sesión](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) más abajo.

#### Registro del requisito de autenticación y la ruta de inicio de sesión con el autenticador de Sling {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

Dado que se espera que este tipo de requisito de autenticación se limite a ciertos modos de ejecución y a un pequeño subconjunto de árboles dentro del repositorio de contenido, el seguimiento del tipo de mezcla de requisito y las propiedades de la ruta de inicio de sesión es condicional y está enlazado a una configuración correspondiente que define las rutas admitidas (consulte Opciones de configuración a continuación). Por consiguiente, solo los cambios dentro del ámbito de estas rutas admitidas almacenarán en déclencheur una actualización del registro OSGi, en cualquier otro lugar se omitirán tanto el tipo de mezcla como la propiedad.

AEM La configuración predeterminada de la ahora utiliza esta configuración para permitir establecer la mezcla en el modo de ejecución de autor, pero solo hacer que tenga efecto tras la replicación en la instancia de publicación. Consulte [esta página](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) para obtener más información sobre cómo Sling aplica el requisito de autenticación.

Añadir el `granite:AuthenticationRequired` El tipo de mezcla dentro de las rutas admitidas configuradas hará que el registro OSGi del controlador responsable se actualice y contenga una entrada nueva y adicional con el `sling.auth.requirements` propiedad. Si un requisito de autenticación determinado especifica lo opcional `granite:loginPath` , el valor se registra adicionalmente con el autenticador con un prefijo &quot;-&quot; que se excluirá del requisito de autenticación.

#### Evaluación y herencia del requisito de autenticación {#evaluation-and-inheritance-of-the-authentication-requirement}

Se espera que los requisitos de autenticación de Apache Sling se hereden a través de la jerarquía de páginas o nodos. Los detalles mismos de la herencia y la evaluación de los requisitos de autenticación, como el orden y la prioridad, se consideran un detalle de implementación y no se documentarán en este artículo.

#### Evaluación de la ruta de inicio de sesión {#evaluation-of-login-path}

La evaluación de la ruta de inicio de sesión y el redireccionamiento al recurso correspondiente tras la autenticación es actualmente un detalle de implementación del Controlador de autenticación del selector de inicio de sesión de Granite de Adobe ( `com.day.cq.auth.impl.LoginSelectorHandler`AEM ), que es un controlador de autenticación de Apache Sling configurado con la opción de autenticación de forma predeterminada.

Al llamar `AuthenticationHandler.requestCredentials` este controlador intenta determinar la página de inicio de sesión de asignación a la que se redirigirá al usuario. Esto incluye los siguientes pasos:

* Distinguir entre contraseña caducada y necesidad de inicio de sesión regular como motivo para la redirección;
* Si es un inicio de sesión normal, comprueba si se puede obtener una ruta de inicio de sesión en el siguiente orden:

   * desde LoginPathProvider tal como lo implementa el nuevo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * de la implementación antigua y obsoleta de CUG,
   * de las Asignaciones de páginas de inicio de sesión, tal como se definen con la variable `LoginSelectorHandler`,
   * y, por último, vuelva a la página de inicio de sesión predeterminada, tal como se define en la `LoginSelectorHandler`.

* Tan pronto como se obtenga una ruta de inicio de sesión válida a través de las llamadas enumeradas anteriormente, la solicitud del usuario se redirigirá a esa página.

El objetivo de esta documentación es la evaluación de la ruta de inicio de sesión expuesta por el `LoginPathProvider` interfaz. AEM La implementación enviada desde la versión 6.3 se comporta de la siguiente manera:

* El registro de las rutas de inicio de sesión depende de la distinción entre la contraseña caducada y la necesidad de iniciar sesión de forma regular como motivo para la redirección
* Si el inicio de sesión es regular, comprueba si la ruta de inicio de sesión se puede obtener en el siguiente orden:

   * desde el `LoginPathProvider` según lo implementado por el nuevo `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * de la implementación antigua y obsoleta de CUG,
   * de las Asignaciones de página de inicio de sesión tal como se definen con la variable `LoginSelectorHandler`,
   * y, finalmente, volver a la página de inicio de sesión predeterminada, tal como se define en la `LoginSelectorHandler`.

* Tan pronto como se obtenga una ruta de inicio de sesión válida a través de las llamadas enumeradas anteriormente, la solicitud del usuario se redirigirá a esa página.

El `LoginPathProvider` según se haya implementado mediante la nueva compatibilidad con requisitos de autenticación en Granite, expone las rutas de inicio de sesión tal como se definen en `granite:loginPath` propiedades, que a su vez se definen mediante el tipo de mezcla como se ha descrito anteriormente. La asignación de la ruta de recurso que contiene la ruta de inicio de sesión y el propio valor de propiedad se mantiene en memoria y se evalúa para encontrar una ruta de inicio de sesión adecuada para otros nodos de la jerarquía.

>[!NOTE]
>
>La evaluación solo se realiza para solicitudes asociadas con recursos que se encuentran en las rutas admitidas configuradas. Para cualquier otra solicitud, se evaluarán las formas alternativas de determinar la ruta de inicio de sesión.

#### Prácticas recomendadas {#best-practices-1}

Se deben tener en cuenta las siguientes prácticas recomendadas al definir los requisitos de autenticación:

* Evite anidar requisitos de autenticación: colocar un solo marcador de requisito de autenticación al principio de un árbol debe ser suficiente y se hereda a todo el subárbol definido por el nodo de destino. Los requisitos de autenticación adicionales dentro de ese árbol deben considerarse redundantes y pueden provocar problemas de rendimiento al evaluar el requisito de autenticación dentro de Apache Sling. Con la separación de las áreas de CUG relacionadas con la autorización y la autenticación, es posible restringir el acceso de lectura mediante CUG u otro tipo de políticas, al mismo tiempo que se aplica la autenticación para todo el árbol.
* Contenido del repositorio de modelo tal que los requisitos de autenticación se apliquen a todo el árbol sin necesidad de excluir de nuevo los subárboles anidados de los requisitos.
* Para evitar especificar y, posteriormente, registrar rutas de inicio de sesión redundantes:

   * basarse en la herencia y evitar definir rutas de inicio de sesión anidadas,
   * no establezca la ruta de inicio de sesión opcional en un valor que corresponda al valor predeterminado o heredado,
   * los desarrolladores de aplicaciones deben identificar qué rutas de inicio de sesión deben configurarse en las configuraciones globales de ruta de inicio de sesión (tanto predeterminadas como de asignaciones) asociadas con `LoginSelectorHandler`.

## Representación en el repositorio {#representation-in-the-repository}

### Representación de la directiva CUG en el repositorio {#cug-policy-representation-in-the-repository}

La documentación de Oak cubre cómo se reflejan las nuevas políticas de CUG en el contenido del repositorio. Para obtener más información, consulte [esta página](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### Requisito de autenticación en el repositorio {#authentication-requirement-in-the-repository}

La necesidad de un requisito de autenticación independiente se refleja en el contenido del repositorio con un tipo de nodo de mezcla dedicado ubicado en el nodo de destino. El tipo de mezcla define una propiedad opcional para especificar una página de inicio de sesión dedicada para el árbol definido por el nodo de destino.

La página asociada con la ruta de inicio de sesión puede encontrarse dentro o fuera de ese árbol. Se excluirá del requisito de autenticación.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## Administración de directivas de CUG y requisito de autenticación {#managing-cug-policies-and-authentication-requirement}

### Administración de políticas de CUG {#managing-cug-policies}

El nuevo tipo de políticas de control de acceso para restringir el acceso de lectura para un CUG se administra mediante la API de administración de control de acceso JCR y sigue los mecanismos descritos con la variable [Especificación JCR 2.0](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).

#### Establecer una nueva directiva CUG {#set-a-new-cug-policy}

Código para aplicar una nueva política de CUG en un nodo que no tenía un CUG establecido anteriormente. Tenga en cuenta que `getApplicablePolicies` solo devuelve las nuevas directivas que no se hayan establecido antes. Al final, la política debe volver a escribirse y los cambios deben persistir.

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
   log.debug("no applicable policy"); // path not supported or no applicable policy (for example,
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### Editar una política de CUG existente {#edit-an-existing-cug-policy}

Se necesitan los siguientes pasos para editar una política de CUG existente. La directiva modificada debe volver a escribirse y los cambios deben persistir usando `javax.jcr.Session.save()`.

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

### Recuperar políticas de CUG efectivas {#retrieve-effective-cug-policies}

La administración de control de acceso JCR define un método de mejor esfuerzo para recuperar las políticas que surten efecto en una ruta determinada. Dado que la evaluación de las políticas de CUG es condicional y depende de la configuración correspondiente para habilitarse, llame a `getEffectivePolicies` es una forma cómoda de comprobar si una directiva CUG determinada está surtiendo efecto en una instalación determinada.

>[!NOTE]
>
>La diferencia entre `getEffectivePolicies` y el ejemplo de código siguiente que sube por la jerarquía para buscar si una ruta determinada ya forma parte de un CUG existente.

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

#### Recuperar políticas de CUG heredadas {#retrieve-inherited-cug-policies}

Búsqueda de todos los CUG anidados que se han definido en una ruta determinada, independientemente de si tienen efecto o no. Para obtener más información, consulte la [Opciones de configuración](/help/sites-administering/closed-user-groups.md#configuration-options) sección.

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

#### Administración de directivas de CUG por principal {#managing-cug-policies-by-pincipal}

Las extensiones definidas por `JackrabbitAccessControlManager` que permiten editar directivas de control de acceso por principal no se implementan con la administración de control de acceso de CUG, ya que por definición una directiva de CUG siempre afecta a todas las principales: las enumeradas con la variable `PrincipalSetPolicy` se les concede acceso de lectura, mientras que a todos los demás principales se les impedirá leer el contenido en el árbol definido por el nodo de destino.

Los métodos correspondientes siempre devuelven una matriz de directivas vacía, pero no producen excepciones.

### Administración del requisito de autenticación {#managing-the-authentication-requirement}

La creación, modificación o eliminación de un nuevo requisito de autenticación se logra cambiando el tipo de nodo efectivo del nodo de destino. La propiedad de ruta de inicio de sesión opcional se puede escribir utilizando la API JCR normal.

>[!NOTE]
>
>Las modificaciones a un nodo de destino determinado mencionadas anteriormente solo se reflejarán en el autenticador de Apache Sling si el `RequirementHandler` se ha configurado y el objetivo está contenido en los árboles definidos por las rutas admitidas (consulte la sección Opciones de configuración).
>
>Para obtener más información, consulte [Asignar tipos de nodos mixin](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Asignar tipos de nodos mixin) y [Adición de nodos y configuración de propiedades](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 Agregar nodos y establecer propiedades)

#### Adición de un nuevo requisito de autenticación {#adding-a-new-auth-requirement}

A continuación se detallan los pasos para crear un requisito de autenticación. El requisito solo se registra con el autenticador de Apache Sling si el `RequirementHandler` se ha configurado para el árbol que contiene el nodo de destino.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### Agregar nuevo requisito de autenticación con ruta de inicio de sesión {#add-a-new-auth-requirement-with-login-path}

Pasos para crear un requisito de autenticación que incluya una ruta de inicio de sesión. Tenga en cuenta que el requisito y la exclusión de la ruta de inicio de sesión solo se registrarán con el autenticador de Apache Sling si la variable `RequirementHandler` se ha configurado para el árbol que contiene el nodo de destino.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### Modificar una ruta de inicio de sesión existente {#modify-an-existing-login-path}

A continuación se detallan los pasos para cambiar una ruta de inicio de sesión existente. La modificación solo se registrará con el autenticador de Apache Sling si `RequirementHandler` se ha configurado para el árbol que contiene el nodo de destino. El valor anterior de la ruta de inicio de sesión se eliminará del registro. El requisito de autenticación asociado al nodo de destino no se ve afectado por esta modificación.

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

Pasos para eliminar una ruta de inicio de sesión existente. La entrada de ruta de inicio de sesión solo se anulará del registro del autenticador de Apache Sling si `RequirementHandler` se ha configurado para el árbol que contiene el nodo de destino. El requisito de autenticación asociado con el nodo de destino no se ve afectado.

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

O bien, puede utilizar el siguiente método para lograr el mismo propósito:

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

Pasos para eliminar un requisito de autenticación existente. El requisito solo se anulará del registro del autenticador de Apache Sling si `RequirementHandler` se ha configurado para el árbol que contiene el nodo de destino.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### Recuperar requisitos de autenticación efectivos {#retrieve-effective-auth-requirements}

No hay ninguna API pública dedicada para leer todos los requisitos de autenticación efectivos registrados con el autenticador de Apache Sling. Sin embargo, la lista se expone en la consola del sistema en `https://<serveraddress>:<serverport>/system/console/slingauth` en la sección &quot;**Configuración del requisito de autenticación**&quot; sección.

AEM La siguiente imagen muestra los requisitos de autenticación de una instancia de publicación de la con contenido de demostración. La ruta resaltada de la página de la comunidad ilustra cómo se refleja un requisito agregado por la implementación descrita en este documento en el autenticador de Apache Sling.

>[!NOTE]
>
>En este ejemplo, no se estableció la propiedad de ruta de acceso de inicio de sesión opcional. Por consiguiente, no se ha registrado ninguna segunda entrada con el autenticador.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### Recuperación de la ruta de inicio de sesión efectiva {#retrieve-the-effective-login-path}

Actualmente no hay ninguna API pública para recuperar la ruta de inicio de sesión que surtirá efecto al acceder de forma anónima a un recurso que requiera autenticación. Consulte la sección Evaluación de la ruta de inicio de sesión para obtener detalles de implementación sobre cómo se recupera la ruta de inicio de sesión.

AEM Sin embargo, tenga en cuenta que, aparte de las rutas de inicio de sesión definidas con esta función, hay formas alternativas de especificar la redirección al inicio de sesión, que deben tenerse en cuenta al diseñar el modelo de contenido y los requisitos de autenticación de una instalación de determinada.

#### Recuperar el requisito de autenticación heredado {#retrieve-the-inherited-auth-requirement}

Al igual que con la ruta de inicio de sesión, no hay ninguna API pública para recuperar los requisitos de autenticación heredados definidos en el contenido. El siguiente ejemplo ilustra cómo enumerar todos los requisitos de autenticación que se han definido con una jerarquía determinada, independientemente de si surten efecto o no. Para obtener más información, consulte [Opciones de configuración](/help/sites-administering/closed-user-groups.md#configuration-options).

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

### Combinación de políticas de CUG y el requisito de autenticación {#combining-cug-policies-and-the-authentication-requirement}

AEM En la tabla siguiente se enumeran las combinaciones válidas de directivas CUG y el requisito de autenticación en una instancia de CUG que tiene ambos módulos habilitados mediante configuración.

| **Se requiere autenticación** | **Ruta de inicio de sesión** | **Acceso de lectura restringido** | **Efecto esperado** |
|---|---|---|---|
| Sí | Sí | Sí | Un usuario determinado solo podrá ver el subárbol marcado con la directiva CUG si la evaluación efectiva de permisos concede acceso. Se redirigirá a un usuario no autenticado a la página de inicio de sesión especificada. |
| Sí | No | Sí | Un usuario determinado solo podrá ver el subárbol marcado con la directiva CUG si la evaluación efectiva de permisos concede acceso. Se redirigirá a un usuario no autenticado a una página de inicio de sesión predeterminada heredada. |
| Sí | Sí | No | Se redirigirá a un usuario no autenticado a la página de inicio de sesión especificada. El hecho de que se permita o no ver el árbol marcado con el requisito de autenticación depende de los permisos efectivos de los elementos individuales contenidos en ese subárbol. No hay ningún CUG dedicado que restrinja el acceso de lectura. |
| Sí | No | No | Se redirigirá a un usuario no autenticado a una página de inicio de sesión predeterminada heredada. El hecho de que se permita o no ver el árbol marcado con el requisito de autenticación depende de los permisos efectivos de los elementos individuales contenidos en ese subárbol. No hay ningún CUG dedicado que restrinja el acceso de lectura. |
| No | No | Sí | Un usuario autenticado o no autenticado determinado solo podrá ver el subárbol marcado con la directiva CUG si la evaluación de permisos efectiva concede acceso. Un usuario no autenticado recibirá el mismo trato y no se le redirigirá para que inicie sesión. |

>[!NOTE]
>
>La combinación de &#39;Requisito de autenticación&#39; = No y &#39;Ruta de inicio de sesión&#39; = Sí no aparece en la lista anterior, ya que &#39;Ruta de inicio de sesión&#39; es un atributo opcional asociado con un requisito de autenticación. Especificar una propiedad JCR con ese nombre sin agregar el tipo de mezcla de definición no tendrá ningún efecto y el controlador correspondiente la ignorará.

## Componentes y configuración de OSGi {#osgi-components-and-configuration}

Esta sección proporciona información general sobre los componentes de OSGi y las opciones de configuración individuales introducidas con la nueva implementación de CUG.

Consulte también la documentación de asignación de CUG para una asignación completa de las opciones de configuración entre la implementación antigua y la nueva.

### Autorización: instalación y configuración {#authorization-setup-and-configuration}

Las partes nuevas relacionadas con la autorización se incluyen en el **Autorización de Oak CUG** paquete ( `org.apache.jackrabbit.oak-authorization-cug`AEM ), que forma parte de la instalación predeterminada de la. El paquete define un modelo de autorización separado que se va a implementar como una forma adicional de administrar el acceso de lectura.

#### Configuración de la autorización de CUG {#setting-up-cug-authorization}

La configuración de la autorización de CUG se describe en detalle en la [Documentación de Apache relevante](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). AEM De forma predeterminada, la autorización de CUG se ha implementado en todos los modos de ejecución de la. Las instrucciones paso a paso también pueden utilizarse para desactivar la autorización de CUG en aquellas instalaciones que requieran una configuración de autorización diferente.

#### Configuración del filtro de referente {#configuring-the-referrer-filter}

También debe configurar la variable [Filtro de referente de Sling](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) AEM con todos los nombres de host que se pueden utilizar para acceder a los datos; por ejemplo, a través de CDN, Equilibrador de carga y cualquier otro.

Si el filtro de referente no está configurado, se observan errores, similares a los siguientes, cuando un usuario intenta iniciar sesión en un sitio de CUG:

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### Características de los componentes OSGi {#characteristics-of-osgi-components}

Se han introducido los dos componentes OSGi siguientes para definir los requisitos de autenticación y especificar las rutas de inicio de sesión dedicadas:

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
   <td>Configuración de autorización específica para configurar y evaluar permisos de CUG.</td>
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
   <td>Directiva de configuración</td>
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
   <td>Permite excluir de la evaluación de CUG entidades de seguridad con los nombres configurados.</td>
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

#### Opciones de configuración {#configuration-options}

Las opciones de configuración clave son:

* `cugSupportedPaths`: especifique los subárboles que pueden contener CUG. No se ha establecido ningún valor predeterminado
* `cugEnabled`: opción de configuración para habilitar la evaluación de permisos para las políticas de CUG actuales.

Las opciones de configuración disponibles asociadas con el módulo de autorización de CUG se enumeran y describen de forma más detallada en la [Documentación de Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### Exclusión de identidades de la evaluación CUG {#excluding-principals-from-cug-evaluation}

Se ha excluido a los responsables individuales de la evaluación de los grupos de usuarios compartidos de la aplicación anterior. La nueva autorización de CUG cubre esto con una interfaz dedicada llamada CugExclude. Apache Jackrabbit Oak 1.4 se distribuye con una implementación predeterminada que excluye un conjunto fijo de principales y una implementación extendida que permite configurar nombres principales individuales. AEM Esto último se configura en instancias de publicación de la publicación de la.

AEM El valor predeterminado desde la versión 6.3 de evita que las siguientes entidades de seguridad se vean afectadas por las políticas de CUG:

* principales administrativos (usuario administrador, grupo de administradores)
* principales de usuario de servicio
* principal del sistema interno del repositorio

Para obtener más información, consulte la tabla de [AEM Configuración predeterminada desde la versión 6.3 de](#default-configuration-since-aem) más abajo.

La exclusión del grupo &quot;administradores&quot; se puede modificar o expandir en la consola del sistema en la sección de configuración de **Lista de exclusión de Apache Jackrabbit Oak CUG**.

Como alternativa, es posible proporcionar e implementar una implementación personalizada de la interfaz CugExclude para ajustar el conjunto de principales excluidos si hay necesidades especiales. Consulte la documentación sobre [Capacidad de conexión de CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) para obtener más información y un ejemplo de implementación.

### Autenticación: instalación y configuración {#authentication-setup-and-configuration}

Las partes nuevas relacionadas con la autenticación se encuentran en la variable **Controlador de autenticación de Adobe Granite** paquete ( `com.adobe.granite.auth.authhandler` versión 5.6.48). AEM Este paquete forma parte de la instalación predeterminada de la.

AEM Para configurar el reemplazo del requisito de autenticación para la compatibilidad con CUG obsoleta, algunos componentes OSGi deben estar presentes y activos en una instalación de determinada. Para obtener más información, consulte **Características de los componentes OSGi** más abajo.

>[!NOTE]
>
>Debido a la opción de configuración obligatoria con RequirementHandler, las partes relacionadas con la autenticación solo estarán activas si la función se ha habilitado al especificar un conjunto de rutas admitidas. AEM Con una instalación estándar, la característica se deshabilita en el modo de ejecución de autor y se habilita para /content en el modo de ejecución de publicación.

**Características de los componentes OSGi**

Se han introducido los dos componentes OSGi siguientes para definir los requisitos de autenticación y especificar las rutas de inicio de sesión dedicadas:

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
   <td>Servicio OSGi dedicado para los requisitos de autenticación que registra a un observador para los cambios de contenido que afectan al requisito de autenticación (a través del <code>granite:AuthenticationRequirement</code> tipo de mezcla) y las rutas de inicio de sesión con están expuestas al <code>LoginSelectorHandler</code>. </td>
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

**com.adobe.granite.auth.required.impl.DefaultRequirementHandler**

| Etiqueta | Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión |
|---|---|
| Descripción | `RequirementHandler` implementación que actualiza los requisitos de autenticación de Apache Sling y la exclusión correspondiente para las rutas de inicio de sesión asociadas. |
| Propiedades de configuración | `supportedPaths` |
| Directiva de configuración | `ConfigurationPolicy.REQUIRE` |
| Referencias | ND |

#### Opciones de configuración {#configuration-options-1}

Las partes relacionadas con la autenticación de la reescritura de CUG solo incluyen una única opción de configuración asociada al requisito de autenticación de Adobe Granite y al controlador de ruta de inicio de sesión:

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
   <td><p>Label = Rutas admitidas</p> <p>Nombre = 'supportedPaths'</p> </td>
   <td>Establecer&lt;string&gt;</td>
   <td>-</td>
   <td>Rutas en las que este controlador respetará los requisitos de autenticación. Deje esta configuración sin configurar si desea agregar el <code>granite:AuthenticationRequirement</code> tipo de mezcla en nodos sin que se apliquen (por ejemplo, en instancias de autor). Si falta, la función está desactivada. </td>
  </tr>
 </tbody>
</table>

## AEM Configuración predeterminada desde la versión 6.3 de {#default-configuration-since-aem}

AEM De forma predeterminada, las nuevas instalaciones de la función CUG utilizarán las nuevas implementaciones tanto para las partes relacionadas con la autorización como con la autenticación. La antigua implementación &quot;Compatibilidad con grupos cerrados de usuarios (CUG) de Adobe AEM Granite&quot; ha quedado obsoleta y, por defecto, se desactivará en todas las instalaciones de la. Las nuevas implementaciones se habilitarán de la siguiente manera:

### Instancias de autor {#author-instances}

| **&quot;Configuración de Apache Jackrabbit Oak CUG&quot;** | **Explicación** |
|---|---|
| Rutas admitidas `/content` | La administración del control de acceso para las directivas CUG está habilitada. |
| Evaluación de CUG habilitada FALSE | La evaluación de permisos está deshabilitada. Las políticas de CUG no surten efecto. |
| Clasificación | 200 | Consulte la documentación de Oak. |

>[!NOTE]
>
>No hay configuración para **Lista de exclusión de Apache Jackrabbit Oak CUG** y **Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión** está presente en las instancias de creación predeterminadas.

### Instancias de publicación {#publish-instances}

| **&quot;Configuración de Apache Jackrabbit Oak CUG&quot;** | **Explicación** |
|---|---|
| Rutas admitidas `/content` | La administración del control de acceso para las políticas de CUG está habilitada debajo de las rutas configuradas. |
| Evaluación de CUG habilitada VERDADERO | La evaluación de permisos está habilitada debajo de las rutas configuradas. Las políticas de CUG surten efecto en `Session.save()`. |
| Clasificación | 200 | Consulte la documentación de Oak. |

| **&quot;Lista de exclusión de Apache Jackrabbit Oak CUG&quot;** | **Explicación** |
|---|---|
| Administradores de nombres principales | Excluye al administrador principal de la evaluación de CUG. |

| **&quot;Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión&quot;** | **Explicación** |
|---|---|
| Rutas admitidas  `/content` | Requisitos de autenticación definidos en el repositorio mediante el `granite:AuthenticationRequired` el tipo de mezcla surte efecto a continuación `/content` tras `Session.save()`. Sling Authenticator se actualiza. Se omite la adición del tipo de mezcla fuera de las rutas admitidas. |

## Desactivación de la autorización de CUG y el requisito de autenticación {#disabling-cug-authorization-and-authentication-requirement}

La nueva implementación puede desactivarse por completo en caso de que una instalación determinada no utilice CUG o utilice medios diferentes para la autenticación y la autorización.

### Deshabilitar autorización de CUG {#disable-cug-authorization}

Consulte la [Capacidad de conexión de CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) documentación para obtener más información sobre cómo eliminar el modelo de autorización de CUG de la configuración de autorización compuesta.

### Desactivar el requisito de autenticación {#disable-the-authentication-requirement}

Para deshabilitar la compatibilidad con el requisito de autenticación proporcionado por el `granite.auth.authhandler` módulo, es suficiente con quitar la configuración asociada a **Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión**.

>[!NOTE]
>
>Sin embargo, tenga en cuenta que al eliminar la configuración no se anulará el registro del tipo de mezcla, que seguía siendo aplicable a los nodos sin tener efecto.

## Interacción con otros módulos {#interaction-with-other-modules}

### API de Apache Jackrabbit {#apache-jackrabbit-api}

Para reflejar el nuevo tipo de política de control de acceso utilizada por el modelo de autorización de CUG, se ha ampliado la API definida por Apache Jackrabbit. Desde la versión 2.11.0 de `jackrabbit-api` El módulo define una nueva interfaz llamada `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`, que se extiende desde `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

El mecanismo de importación de Apache Jackrabbit FileVault se ha ajustado para hacer frente a las políticas de control de acceso de tipo `PrincipalSetPolicy`.

### Distribución de contenido de Apache Sling {#apache-sling-content-distribution}

Consulte lo anterior [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) sección.

### Adobe de replicación de Granite {#adobe-granite-replication}

AEM El módulo de replicación se ha ajustado ligeramente para poder replicar las políticas de CUG entre diferentes instancias de:

* `DurboImportConfiguration.isImportAcl()` se interpreta literalmente y solo afectará a las políticas de control de acceso que implementen `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` solo respetará esta configuración para ACL verdaderas
* Otras políticas, como `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` las instancias creadas por el modelo de autorización de CUG siempre se replicarán y la opción de configuración `DurboImportConfiguration.isImportAcl`() se omitirá.

Hay una limitación en la replicación de políticas de CUG. Si se elimina una política de CUG determinada sin eliminar el tipo de nodo de mezcla correspondiente `rep:CugMixin,` la eliminación no se reflejará en la replicación. Esto se ha solucionado eliminando siempre el mixin tras la eliminación de la política. No obstante, la limitación puede aparecer si se añade manualmente el tipo de mezcla.

### Controlador de autenticación de Adobe Granite {#adobe-granite-authentication-handler}

El controlador de autenticación **Controlador de autenticación de encabezado HTTP de Adobe Granite** enviado con el `com.adobe.granite.auth.authhandler` el paquete contiene una referencia a `CugSupport` interfaz definida por el mismo módulo. Se utiliza para calcular el &quot;dominio kerberos&quot; en determinadas circunstancias, regresando al dominio configurado con el controlador.

Esto se ha ajustado para hacer referencia a `CugSupport` opcional para garantizar la máxima compatibilidad con versiones anteriores si una configuración determinada decide volver a habilitar la implementación obsoleta. Las instalaciones que utilicen la implementación ya no obtendrán el dominio extraído de la implementación de CUG, pero siempre mostrarán el dominio tal como se define con **Controlador de autenticación de encabezado HTTP de Adobe Granite**.

>[!NOTE]
>
>De forma predeterminada, la variable **Controlador de autenticación de encabezado HTTP de Adobe Granite** solo se configura en el modo de ejecución de publicación con &quot;Deshabilitar página de inicio de sesión&quot; ( `auth.http.nologin`) opción activada.

### AEM LiveCopy {#aem-livecopy}

La configuración de CUG junto con LiveCopy se representa en el repositorio mediante la adición de un nodo adicional y una propiedad adicional de la siguiente manera:

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Ambos elementos se crean en la variable `cq:Page`. Con el diseño actual, MSM solo gestiona los nodos y las propiedades que se encuentran en `cq:PageContent` (`jcr:content`) nodo.

Por lo tanto, los grupos de CUG no se pueden desplegar en Live Copies desde modelos. Tenga en cuenta esto al configurar Live Copy.

## Cambios con la nueva implementación de CUG {#changes-with-the-new-cug-implementation}

El objetivo de esta sección es proporcionar una visión general de los cambios realizados en la función CUG y una comparación entre la implementación antigua y la nueva. Enumera los cambios que afectan a la forma en que se configura la compatibilidad con CUG y describe cómo y por quién se administran los CUG en el contenido del repositorio.

### Diferencias en la configuración y configuración de CUG {#differences-in-cug-setup-and-configuration}

El componente OSGi obsoleto **Soporte de Adobe Granite Closed User Group (CUG)** ( `com.day.cq.auth.impl.cug.CugSupportImpl`) se ha sustituido por nuevos componentes para poder gestionar por separado las partes relacionadas con la autorización y la autenticación de la funcionalidad anterior de CUG.

## Diferencias en la gestión de CUG en el contenido del repositorio {#differences-in-managing-cugs-in-the-repository-content}

En las secciones siguientes se describen las diferencias entre las implementaciones antiguas y nuevas desde el punto de vista de la implementación y la seguridad. Aunque la nueva implementación pretende proporcionar la misma funcionalidad, hay cambios sutiles que son importantes conocer al utilizar el nuevo CUG.

### Diferencias Con Respecto A La Autorización {#differences-with-regards-to-authorization}

Las principales diferencias desde el punto de vista de la autorización se resumen en la lista siguiente:

**Contenido de control de acceso dedicado para CUG**

En la implementación antigua, el modelo de autorización predeterminado se utilizaba para manipular las políticas de lista de control de acceso en la publicación, sustituyendo cualquier ACE existente por la configuración establecida por el CUG. Esto se activó escribiendo propiedades JCR residuales normales que se interpretaron al publicar.

Con la nueva implementación, la configuración de control de acceso del modelo de autorización predeterminado no se ve afectada por la creación, modificación o eliminación de ningún CUG. En su lugar, se llama a un nuevo tipo de directiva `PrincipalSetPolicy` se aplica como contenido de control de acceso adicional al nodo de destino. Esta directiva adicional se ubicará como un elemento secundario del nodo de destino y sería secundario del nodo de directiva predeterminado si está presente.

**Edición de directivas de CUG en la administración de control de acceso**

Este cambio de las propiedades JCR residuales a una política de control de acceso dedicada afecta al permiso necesario para crear o modificar la parte de autorización de la función CUG. Dado que esto se considera una modificación del contenido de control de acceso, requiere lo siguiente `jcr:readAccessControl` y `jcr:modifyAccessControl` privilegios que se escribirán en el repositorio. Por lo tanto, solo los autores de contenido con derecho a modificar el contenido de control de acceso de una página pueden configurar o modificar este contenido. Esto contrasta con la implementación antigua, en la que la capacidad para escribir propiedades JCR normales era suficiente, lo que daba como resultado una escalación de privilegios.

**Nodo De Destino Definido Por La Directiva**

Se espera que las políticas de CUG se creen en el nodo JCR que define el subárbol que estará sujeto a acceso de lectura restringido. AEM Es probable que esta sea una página de en caso de que se espere que el CUG afecte a todo el árbol.

Tenga en cuenta que colocar la directiva CUG solo en el nodo jcr:content ubicado debajo de una página determinada solo restringirá el acceso al contenido s.str de una página determinada, pero no surtirá efecto en ninguna página del mismo nivel o secundaria. Este puede ser un caso de uso válido y se puede lograr con un editor de repositorios que permita aplicar contenido de acceso de grano fino. Sin embargo, contrasta con la implementación anterior, en la que al colocar una propiedad cq:cugEnabled en el nodo jcr:content se reasignaba internamente al nodo de la página. Esta asignación ya no se realiza.

**Evaluación de permisos con políticas de CUG**

Al pasar de la antigua compatibilidad con CUG a un modelo de autorización adicional, cambia la forma en que se evalúan los permisos de lectura efectivos. Como se describe en la [Documentación de Jackrabbit](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), una entidad de seguridad determinada que puede ver el `CUGcontent` solo se concederá acceso de lectura si la evaluación de permisos de todos los modelos configurados en el repositorio de Oak concede acceso de lectura.

En otras palabras, para la evaluación de los permisos efectivos, tanto la `CUGPolicy` y se tendrán en cuenta las entradas de control de acceso predeterminadas, y el acceso de lectura al contenido de CUG solo se concederá si lo conceden ambos tipos de directivas. AEM En una instalación predeterminada de publicación en la que el acceso de lectura a la `/content` El árbol se concede a todos, el efecto de las políticas de CUG será el mismo que con la implementación antigua.

**Evaluación bajo demanda**

El modelo de autorización de CUG permite activar individualmente la gestión del control de acceso y la evaluación de permisos:

* la administración del control de acceso está habilitada si el módulo tiene una o varias rutas admitidas en las que se pueden crear CUG
* la evaluación de permisos solo está habilitada si la opción **Evaluación de CUG habilitada** está marcado adicionalmente.

AEM En la nueva evaluación de configuración predeterminada de la configuración de la nueva configuración de la configuración de CUG, solo se activa con el modo de ejecución &quot;publicar&quot;. Consulte los detalles en la [AEM Configuración predeterminada desde la versión 6.3 de](#default-configuration-since-aem) para obtener más información. Esto se puede comprobar comparando las políticas efectivas para una ruta determinada con las políticas almacenadas en el contenido. Las políticas efectivas solo se mostrarán en caso de que la evaluación de permisos para CUG esté habilitada.

Como se ha explicado anteriormente, las políticas de control de acceso de CUG ahora siempre se almacenan en el contenido, pero la evaluación de los permisos efectivos que resultan de esas políticas solo se aplicará si **Evaluación de CUG habilitada** se activa en la consola del sistema en Apache Jackrabbit Oak **Configuración de CUG.** De forma predeterminada, solo está habilitado con el modo de ejecución &quot;publicar&quot;.

### Diferencias Con Respecto A La Autenticación {#differences-with-regards-to-authentication}

A continuación se describen las diferencias con respecto a la autenticación.

#### Tipo De Mixin Dedicado Para El Requisito De Autenticación {#dedicated-mixin-type-for-authentication-requirement}

En la implementación anterior, los aspectos de autorización y autenticación de un CUG se activaban mediante una sola propiedad JCR ( `cq:cugEnabled`). Por lo que respecta a la autenticación, esto dio como resultado una lista actualizada de los requisitos de autenticación almacenados con la implementación de Apache Sling Authenticator. Con la nueva implementación se logra el mismo resultado marcando el nodo de destino con un tipo de mezcla dedicado ( `granite:AuthenticationRequired`).

#### Propiedad Para Excluir Ruta De Acceso {#property-for-excluding-login-path}

El tipo de mezcla define una sola propiedad opcional llamada `granite:loginPath`, que básicamente corresponde a la `cq:cugLoginPage` propiedad. A diferencia de la implementación anterior, la propiedad de ruta de inicio de sesión solo se respetará si su tipo de nodo de declaración es el mixin mencionado. Añadir una propiedad con ese nombre sin establecer el tipo de mezcla no tendrá ningún efecto y no se informará al autenticador de ningún requisito nuevo ni de ninguna exclusión de la ruta de inicio de sesión.

#### Privilegio Para Requisito De Autenticación {#privilege-for-authentication-requirement}

Añadir o eliminar un tipo de mezcla requiere lo siguiente `jcr:nodeTypeManagement` privilegio que se concede. En la implementación anterior, la variable `jcr:modifyProperties` se utiliza para editar la propiedad residual.

En cuanto a la `granite:loginPath` En este caso, se requiere el mismo privilegio para añadir, modificar o eliminar la propiedad.

#### Nodo De Destino Definido Por Tipo De Mixin {#target-node-defined-by-mixin-type}

Se espera que los requisitos de autenticación se creen en el nodo JCR que define el subárbol que debe estar sujeto al inicio de sesión obligatorio. AEM Es probable que esta sea una página de en caso de que se espere que el CUG afecte a todo el árbol y, en consecuencia, la interfaz de usuario de la nueva implementación agregará el tipo de mezcla de requisito de autenticación en el nodo de página.

Colocar la directiva CUG solo en el nodo jcr:content ubicado debajo de una página determinada solo restringirá el acceso al contenido, pero no entrará en vigor en el propio nodo de la página ni en ninguna página secundaria.

Este puede ser un escenario válido y es posible con un editor de repositorios que permita colocar el mixin en cualquier nodo. Sin embargo, el comportamiento contrasta con la implementación anterior, en la que al colocar una propiedad cq:cugEnabled o cq:cugLoginPage en el nodo jcr:content se reasignaba internamente, en última instancia, al nodo de la página. Esta asignación ya no se realiza.

#### Rutas admitidas configuradas {#configured-supported-paths}

Tanto la `granite:AuthenticationRequired` El tipo de mezcla y la propiedad granite:loginPath solo se respetarán dentro del ámbito definido por el conjunto de **Rutas admitidas** opción de configuración presente con la variable **Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión**. Si no se especifica ninguna ruta, la función de requisito de autenticación se desactiva por completo. En este caso, el tipo de mezcla ni la propiedad tienen efecto cuando se agregan o establecen en un nodo JCR determinado.

### Asignación de contenido JCR, servicios OSGi y configuraciones {#mapping-of-jcr-content-osgi-services-and-configurations}

El documento siguiente proporciona una asignación completa de los servicios OSGi, las configuraciones y el contenido del repositorio entre la implementación antigua y la nueva.

AEM Asignación de CUG desde la versión 6.30000

[Obtener archivo](assets/cug-mapping.pdf)

## Actualizar CUG {#upgrade-cug}

### Instalaciones existentes que utilizan el CUG obsoleto {#existing-installations-using-the-deprecated-cug}

La antigua implementación de compatibilidad con CUG se ha desaprobado y se eliminará para en versiones futuras. AEM Se recomienda pasar a las nuevas implementaciones al actualizar desde versiones anteriores a la versión 6.3 de la aplicación de la versión de la versión de la versión de la versión de la versión de la versión 6.3.

AEM Para la instalación actualizada de la, es importante asegurarse de que solo se activa una implementación de CUG. La combinación de la nueva y la antigua compatibilidad con CUG obsoleta no se ha probado y es probable que cause un comportamiento no deseado:

* colisiones en Sling Authenticator con respecto a los requisitos de autenticación
* se ha denegado el acceso de lectura cuando la configuración de ACL asociada con el CUG antiguo entra en conflicto con una directiva de CUG nueva.

### Migración del contenido de CUG existente {#migrating-existing-cug-content}

El Adobe proporciona una herramienta para migrar a la nueva implementación de CUG. Para usarlo, realice los siguientes pasos:

1. Ir a `https://<serveraddress>:<serverport>/system/console/cug-migration` para acceder a la herramienta.
1. Introduzca la ruta raíz para la que desea comprobar los CUG y pulse el botón **Realizar simulacro** botón. Esto buscará los CUG aptos para la conversión en la ubicación seleccionada.
1. Después de revisar los resultados, presione la tecla **Realización de migración** para migrar a la nueva implementación.

>[!NOTE]
>
>Si tiene problemas, es posible configurar un registrador específico en **DEPURAR** nivel activado `com.day.cq.auth.impl.cug` para obtener el resultado de la herramienta de migración. Consulte [Registro](/help/sites-deploying/configure-logging.md) para obtener más información sobre cómo hacerlo.
