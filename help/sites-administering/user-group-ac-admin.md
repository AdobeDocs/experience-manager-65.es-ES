---
title: Administración de derechos de usuario, grupo y acceso
seo-title: User, Group and Access Rights Administration
description: AEM Obtenga información acerca de la administración de derechos de usuario, grupo y acceso en la.
seo-description: Learn about user, group and access rights administration in AEM.
uuid: 26d7bb25-5a38-43c6-bd6a-9ddba582c60f
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 66674e47-d19f-418f-857f-d91cf8660b6d
docset: aem65
exl-id: 5808b8f9-9b37-4970-b5c1-4d33404d3a8b
feature: Security
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '3120'
ht-degree: 1%

---

# Administración de derechos de usuario, grupo y acceso{#user-group-and-access-rights-administration}

Habilitar el acceso a un repositorio CRX implica varios temas:

* [Derechos de acceso](#how-access-rights-are-evaluated) - los conceptos de cómo se definen y evalúan
* [Administración de usuarios](#user-administration) - administrar las cuentas individuales utilizadas para el acceso
* [Administración de grupos](#group-administration) - simplificar la administración de usuarios formando grupos
* [Administración de derechos de acceso](#access-right-management) - definir políticas que controlen cómo estos usuarios y grupos pueden acceder a los recursos

Los elementos básicos son:

**Cuentas de usuario** CRX autentica el acceso identificando y verificando a un usuario (por esa persona, u otra aplicación) según los detalles que contenga la cuenta de usuario.

En CRX, cada cuenta de usuario es un nodo en el espacio de trabajo. Una cuenta de usuario CRX tiene las siguientes propiedades:

* Representa a un usuario de CRX.
* Contiene un nombre de usuario y una contraseña.
* Es aplicable a ese espacio de trabajo.
* No puede tener subusuarios. Para los derechos de acceso jerárquicos, debe utilizar grupos.

* Puede especificar derechos de acceso para la cuenta de usuario.

   Sin embargo, para simplificar la administración, le recomendamos que (en la mayoría de los casos) asigne derechos de acceso a las cuentas de grupo. La asignación de derechos de acceso a cada usuario individual se vuelve rápidamente muy difícil de administrar (las excepciones son determinados usuarios del sistema cuando solo existen una o dos instancias).

**Cuentas de grupo** Las cuentas de grupo son colecciones de usuarios u otros grupos. Se utilizan para simplificar la administración, ya que un cambio en los derechos de acceso asignados a un grupo se aplica automáticamente a todos los usuarios de ese grupo. Un usuario no tiene que pertenecer a ningún grupo, pero a menudo pertenece a varios.

En CRX, un grupo tiene las siguientes propiedades:

* Representa un grupo de usuarios con derechos de acceso comunes. Por ejemplo, autores o desarrolladores.
* Es aplicable a ese espacio de trabajo.
* Puede tener miembros; pueden ser usuarios individuales u otros grupos.
* La agrupación jerárquica se puede lograr con relaciones de miembros. No puede colocar un grupo directamente debajo de otro grupo en el repositorio.
* Puede definir los derechos de acceso para todos los miembros del grupo.

**Derechos de acceso** CRX utiliza derechos de acceso para controlar el acceso a áreas específicas del repositorio.

Esto se realiza asignando privilegios para permitir o denegar el acceso a un recurso (nodo o ruta) en el repositorio. Dado que se pueden asignar varios privilegios, estos deben evaluarse para determinar qué combinación es aplicable a la solicitud actual.

CRX le permite configurar los derechos de acceso para las cuentas de usuario y de grupo. Los mismos principios básicos de evaluación se aplican a ambos.

## Cómo se evalúan los derechos de acceso {#how-access-rights-are-evaluated}

>[!NOTE]
>
>Implementaciones CRX [control de acceso definido por JSR-283](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).
>
>Se configura una instalación estándar de un repositorio CRX para utilizar listas de control de acceso basadas en recursos. Esta es una posible implementación del control de acceso JSR-283 y una de las implementaciones presentes con Jackrabbit.

### Sujetos y principales {#subjects-and-principals}

CRX utiliza dos conceptos clave al evaluar los derechos de acceso:

* A **principal** es una entidad que cuenta con derechos de acceso. Las entidades principales incluyen:

   * Una cuenta de usuario
   * Una cuenta de grupo

      Si una cuenta de usuario pertenece a uno o más grupos, también se asocia a cada una de esas entidades de seguridad de grupo.

* A **sujeto** se utiliza para representar el origen de una solicitud.

   Se utiliza para consolidar los derechos de acceso aplicables a esa solicitud. Estas se toman de:

   * Principal de usuario

      Los derechos que asigna directamente a la cuenta de usuario.

   * Todas las entidades de seguridad de grupo asociadas a ese usuario

      Todos los derechos asignados a cualquiera de los grupos a los que pertenece el usuario.
   A continuación, el resultado se utiliza para permitir o denegar el acceso al recurso solicitado.

#### Compilación de la lista de derechos de acceso para un asunto {#compiling-the-list-of-access-rights-for-a-subject}

En CRX, el asunto depende de lo siguiente:

* principal de usuario
* todas las entidades de seguridad de grupo asociadas a ese usuario

La lista de derechos de acceso aplicables al sujeto de ensayo se elabora a partir de:

* los derechos que asigna directamente a la cuenta de usuario
* además de todos los derechos asignados a cualquiera de los grupos a los que pertenece el usuario

![chlimage_1-56](assets/chlimage_1-56.png)

>[!NOTE]
>
>* CRX no tiene en cuenta ninguna jerarquía de usuarios cuando compila la lista.
>* CRX utiliza una jerarquía de grupo solo cuando se incluye un grupo como miembro de otro grupo. No hay herencia automática de permisos de grupo.
>* El orden en que se especifican los grupos no afecta a los derechos de acceso.
>


### Resolver solicitudes y derechos de acceso {#resolving-request-and-access-rights}

Cuando CRX administra la solicitud, compara la solicitud de acceso del asunto con la lista de control de acceso del nodo del repositorio:

Así que si Linda solicita actualizar el `/features` en la siguiente estructura de repositorio:

![chlimage_1-57](assets/chlimage_1-57.png)

### Orden de prioridad {#order-of-precedence}

Los derechos de acceso en CRX se evalúan de la siguiente manera:

* Las entidades de seguridad de usuario siempre tienen prioridad sobre las de grupo, independientemente de:

   * su orden en la lista de control de acceso
   * su posición en la jerarquía del nodo

* Para un principal determinado existe (como máximo) 1 entrada denegada y 1 entrada permitida en un nodo determinado. La implementación siempre borra las entradas redundantes y se asegura de que el mismo privilegio no aparezca en las entradas de permiso y de denegación.

>[!NOTE]
>
>Este proceso de evaluación es adecuado para el control de acceso basado en recursos de una instalación CRX estándar.

Tomando dos ejemplos donde el usuario `aUser` es miembro del grupo `aGroup`:

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
       + grandChildNode
```

En el caso anterior:

* `aUser` no tiene permiso de escritura en `grandChildNode`.

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
         + ace: aUser - deny - write
       + grandChildNode
```

En este caso:

* `aUser` no tiene permiso de escritura en `grandChildNode`.
* El segundo ACE para `aUser` es redundante.

Los derechos de acceso de varios principales de grupo se evalúan en función de su orden, tanto dentro de la jerarquía como dentro de una sola lista de control de acceso.

### Prácticas recomendadas {#best-practices}

En la tabla siguiente se enumeran algunas recomendaciones y prácticas recomendadas:

<table>
 <tbody>
  <tr>
   <td>Recomendación...</td>
   <td>Motivo...</td>
  </tr>
  <tr>
   <td><i>Usar grupos</i></td>
   <td><p>Evite asignar derechos de acceso usuario por usuario. Esto se debe a varios motivos:</p>
    <ul>
     <li>Hay muchos más usuarios que grupos, por lo que los grupos simplifican la estructura.</li>
     <li>Los grupos ayudan a proporcionar una visión general de todas las cuentas.</li>
     <li>La herencia es más sencilla con los grupos.</li>
     <li>Los usuarios van y vienen. Los grupos son a largo plazo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><i>Sea positivo</i></td>
   <td><p>Utilice siempre las instrucciones Allow para especificar los derechos de acceso del principal del grupo (siempre que sea posible). Evite utilizar una instrucción Deny.</p> <p>Las entidades de seguridad de grupo se evalúan en orden, tanto dentro de la jerarquía como en orden dentro de una sola lista de control de acceso.</p> </td>
  </tr>
  <tr>
   <td><i>Manténgalo simple</i></td>
   <td><p>Invertir algo de tiempo y reflexión en la configuración de una nueva instalación será una buena recompensa.</p> <p>La aplicación de una estructura clara simplificará el mantenimiento y la administración continuos, lo que garantiza que tanto sus compañeros actuales como los sucesores futuros puedan comprender fácilmente qué se está implementando.</p> </td>
  </tr>
  <tr>
   <td><i>Probar</i></td>
   <td>Utilice una instalación de prueba para practicar y asegurarse de que comprende las relaciones entre los distintos usuarios y grupos.</td>
  </tr>
  <tr>
   <td><i>Usuarios/grupos predeterminados</i></td>
   <td>Actualice siempre Usuarios y grupos predeterminados inmediatamente después de la instalación para evitar problemas de seguridad.</td>
  </tr>
 </tbody>
</table>

## Administración de usuarios {#user-administration}

Se utiliza un cuadro de diálogo estándar para **Administración de usuarios**.

Debe haber iniciado sesión en el espacio de trabajo adecuado. A continuación, puede acceder al cuadro de diálogo desde los dos:

* el **Administración de usuarios** en la consola principal de CRX
* el **Seguridad** del Explorador de CRX

![chlimage_1-58](assets/chlimage_1-58.png)

**Propiedades**

* **UserID**

   Nombre corto de la cuenta, que se utiliza al acceder a CRX.

* **Nombre principal**

   Un nombre de texto completo para la cuenta.

* **Contraseña**

   Necesario al acceder a CRX con esta cuenta.

* **ntlmhash**

   Se asigna automáticamente a cada cuenta nueva y se actualiza cuando se cambia la contraseña.

* Puede agregar nuevas propiedades definiendo un nombre, tipo y valor. Haga clic en Guardar (símbolo de verificación verde) para cada nueva propiedad.

**Miembros del grupo**

Muestra todos los grupos a los que pertenece la cuenta. La columna Heredado indica la pertenencia que se ha heredado como resultado de la pertenencia a otro grupo.

Al hacer clic en un ID de grupo (cuando esté disponible) se abrirá el [Administración de grupos](#group-administration) para ese grupo.

**Suplantadores**

Con la funcionalidad Suplantar, un usuario puede trabajar en nombre de otro usuario.

Esto significa que una cuenta de usuario puede especificar otras cuentas (usuario o grupo) que pueden funcionar con su cuenta. En otras palabras, si el usuario B puede suplantar al usuario A, el usuario B puede realizar acciones utilizando los detalles completos de la cuenta del usuario A (incluidos el ID, el nombre y los derechos de acceso).

Esto permite a las cuentas de suplantación completar tareas como si estuvieran utilizando la cuenta que están suplantando; por ejemplo, durante una ausencia o para compartir una carga excesiva a corto plazo.

Si una cuenta suplanta a otra es muy difícil de ver. Los archivos de registro no contienen información sobre el hecho de que se haya producido una suplantación en los eventos. Por lo tanto, si el usuario B se hace pasar por el usuario A, todos los eventos parecerán realizados por el usuario A personalmente.

### Creación de una cuenta de usuario {#creating-a-user-account}

1. Abra el **Administración de usuarios** diálogo.
1. Clic **Crear usuario**.
1. A continuación, puede introducir las propiedades:

   * **UserID** se utiliza como nombre de cuenta.
   * **Contraseña** necesario al iniciar sesión.
   * **Nombre principal** para proporcionar un nombre textual completo.
   * **Ruta intermedia** que se puede utilizar para formar una estructura de árbol.

1. Haga clic en Guardar (símbolo de marca de verificación verde).
1. El cuadro de diálogo se expandirá para que pueda:

   1. Configurar **Propiedades**.
   1. Consulte **Pertenencia a grupo**.
   1. Definir **Suplantadores**.

>[!NOTE]
>
>A veces, se puede observar una pérdida de rendimiento al registrar nuevos usuarios en instalaciones que tienen un número elevado de ambos:
>
>* usuarios
>* grupos con muchos miembros
>


### Actualización de una cuenta de usuario {#updating-a-user-account}

1. Con el **Administración de usuarios** diálogo abra la vista de lista de todas las cuentas.
1. Desplácese por la estructura de árbol.
1. Haga clic en la cuenta requerida para abrirla y editarla.
1. Realice un cambio y haga clic en Guardar (símbolo de verificación verde) para esa entrada.
1. Clic **Cerrar** para finalizar, o **Lista...** para volver a la lista de todas las cuentas de usuario.

### Eliminación de una cuenta de usuario {#removing-a-user-account}

1. Con el **Administración de usuarios** diálogo abra la vista de lista de todas las cuentas.
1. Desplácese por la estructura de árbol.
1. Seleccione la cuenta requerida y haga clic en **Quitar usuario**; la cuenta se eliminará inmediatamente.

>[!NOTE]
>
>Esto elimina el nodo de esta entidad de seguridad del repositorio.
>
>Las entradas de derechos de acceso no se eliminan. Esto garantiza la integridad histórica.

### Definición de propiedades {#defining-properties}

Puede definir **Propiedades** para cuentas nuevas o existentes:

1. Abra el **Administración de usuarios** para la cuenta adecuada.
1. Defina un **Propiedad** nombre.
1. Seleccione el **Tipo** en la lista desplegable.
1. Defina el **Valor**.
1. Haga clic en Guardar (símbolo de clic verde) para la nueva propiedad.

Las propiedades existentes se pueden eliminar con el símbolo de papelera.

A excepción de la contraseña, las propiedades no se pueden editar, se deben eliminar y volver a crear.

#### Cambio de la contraseña {#changing-the-password}

El **Contraseña** es una propiedad especial que se puede cambiar haciendo clic en el icono **Cambiar contraseña** vínculo.

También puede cambiar la contraseña a su propia cuenta de usuario desde el **Seguridad** en el Explorador de CRX.

### Definición de un suplantador {#defining-an-impersonator}

Puede definir suplantadores para cuentas nuevas o existentes:

1. Abra el **Administración de usuarios** para la cuenta adecuada.
1. Especifique la cuenta que puede suplantar a esa cuenta.

   Puede usar Examinar... para seleccionar una cuenta existente.

1. Haga clic en Guardar (símbolo de verificación verde) para la nueva propiedad.

## Administración de grupos {#group-administration}

Se utiliza un cuadro de diálogo estándar para **Administración de grupos**.

Debe haber iniciado sesión en el espacio de trabajo adecuado. A continuación, puede acceder al cuadro de diálogo desde los dos:

* el **Administración de grupos** en la consola principal de CRX
* el **Seguridad** del Explorador de CRX

![chlimage_1-8](assets/chlimage_1-8.jpeg)

**Propiedades**

* **GroupID**

   Nombre abreviado de la cuenta de grupo.

* **Nombre principal**

   Un nombre de texto completo para la cuenta de grupo.

* Puede agregar nuevas propiedades definiendo un nombre, tipo y valor. Haga clic en Guardar (símbolo de verificación verde) para cada nueva propiedad.

* **Miembros**

   Puede agregar usuarios u otros grupos como miembros de este grupo.

**Miembros del grupo**

Muestra todos los grupos a los que pertenece la cuenta de grupo actual. La columna Heredado indica la pertenencia que se ha heredado como resultado de la pertenencia a otro grupo.

Al hacer clic en un GroupID, se abrirá el cuadro de diálogo de ese grupo.

**Miembros**

Enumera todas las cuentas (usuarios o grupos) que son miembros del grupo actual.

El **Heredado** indica la pertenencia que se ha heredado como resultado de la pertenencia a otro grupo.

>[!NOTE]
>
>Cuando se asigna la función Propietario, Editor o Visualizador a un usuario de cualquier carpeta de recursos, se crea un nuevo grupo. El nombre del grupo tiene el formato `mac-default-<foldername>` para cada carpeta en la que se definen las funciones.

### Crear una cuenta de grupo {#creating-a-group-account}

1. Abra el **Administración de grupos** diálogo.
1. Clic **Crear grupo**.
1. A continuación, puede introducir las propiedades:

   * **Nombre principal** para proporcionar un nombre textual completo.
   * **Ruta intermedia** que se puede utilizar para formar una estructura de árbol.

1. Haga clic en Guardar (símbolo de marca de verificación verde).
1. El cuadro de diálogo se expandirá para que pueda:

   1. Configurar **Propiedades**.
   1. Consulte **Pertenencia a grupo**.
   1. Administrar **Miembros**.

### Actualización de una Cuenta de Grupo {#updating-a-group-account}

1. Con el **Administración de grupos** diálogo abra la vista de lista de todas las cuentas.
1. Desplácese por la estructura de árbol.
1. Haga clic en la cuenta requerida para abrirla y editarla.
1. Realice un cambio y haga clic en Guardar (símbolo de verificación verde) para esa entrada.
1. Clic **Cerrar** para finalizar, o **Lista...** para volver a la lista de todas las cuentas de grupo.

### Eliminación de una cuenta de grupo {#removing-a-group-account}

1. Con el **Administración de grupos** diálogo abra la vista de lista de todas las cuentas.
1. Desplácese por la estructura de árbol.
1. Seleccione la cuenta requerida y haga clic en **Quitar grupo**; la cuenta se eliminará inmediatamente.

>[!NOTE]
>
>Esto elimina el nodo de esta entidad de seguridad del repositorio.
>
>Las entradas de derechos de acceso no se eliminan. Esto garantiza la integridad histórica.

### Definición de propiedades {#defining-properties-1}

Puede definir Propiedades para cuentas nuevas o existentes:

1. Abra el **Administración de grupos** para la cuenta adecuada.
1. Defina un **Propiedad** nombre.
1. Seleccione el **Tipo** en la lista desplegable.
1. Defina el **Valor**.
1. Haga clic en Guardar (símbolo de verificación verde) para la nueva propiedad.

Las propiedades existentes se pueden eliminar con el símbolo de papelera.

### Miembros {#members}

Puede agregar miembros al grupo actual:

1. Abra el **Administración de grupos** para la cuenta adecuada.
1. O bien, haga lo siguiente:

   * Introduzca el nombre del miembro requerido (cuenta de usuario o de grupo).
   * O use **Examinar...** para buscar y seleccionar el principal (cuenta de usuario o de grupo) que desea agregar.

1. Haga clic en Guardar (símbolo de verificación verde) para la nueva propiedad.

O elimine un miembro existente con el símbolo de papelera.

## Administración de derechos de acceso {#access-right-management}

Con el **Control de acceso** pestaña del CRXDE Lite puede definir las políticas de control de acceso y asignar los privilegios relacionados.

Por ejemplo, para **Ruta actual** seleccione el recurso necesario en el panel izquierdo, la pestaña Control de acceso en el panel inferior derecho:

![crx_accesscontrol_tab](assets/crx_accesscontrol_tab.png)

Las directivas se clasifican de acuerdo con:

* **Políticas de control de acceso aplicables**

   Estas políticas se pueden aplicar.

   Son directivas que están disponibles para crear una directiva local. Una vez seleccionada y agregada una directiva aplicable, se convierte en una directiva local.

* **Políticas de control de acceso local**

   Son directivas de control de acceso que ha aplicado. A continuación, puede actualizarlas, pedirlas o eliminarlas.

   Una directiva local anulará cualquier directiva heredada del elemento principal.

* **Políticas de control de acceso efectivas**

   Estas son las políticas de control de acceso que ahora están en vigor para cualquier solicitud de acceso. Muestran las directivas agregadas derivadas tanto de las directivas locales como de las heredadas del elemento principal.

### Selección de directiva {#policy-selection}

Se pueden seleccionar las políticas para:

* **Ruta actual**

   Como en el ejemplo anterior, seleccione un recurso dentro del repositorio. Se mostrarán las políticas para esta &quot;ruta actual&quot;.

* **Repositorio**

   Selecciona el control de acceso de nivel de repositorio. Por ejemplo, al configurar la variable `jcr:namespaceManagement` , que solo es relevante para el repositorio, no para un nodo.

* **Principal**

   Un principal registrado en el repositorio.

   Puede escribir en el campo **Principal** nombre o haga clic en el icono a la derecha del campo para abrir **Seleccionar principal** diálogo.

   Esto le permite **Buscar** para un **Usuario** o **Grupo**. Seleccione el principal requerido de la lista resultante y haga clic en **OK** para volver a llevar el valor al cuadro de diálogo anterior.

![crx_accesscontrol_selectprincipal](assets/crx_accesscontrol_selectprincipal.png)

>[!NOTE]
>
>Para simplificar la administración, le recomendamos que asigne derechos de acceso a las cuentas de grupo, no a las cuentas de usuario individuales.
>
>Es más fácil administrar algunos grupos que varias cuentas de usuario.

### Privilegios {#privileges}

Los siguientes privilegios están disponibles para seleccionarlos al agregar una entrada de control de acceso (consulte la [API de seguridad](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/security/Privilege.html) para obtener información detallada):

<table>
 <tbody>
  <tr>
   <th><strong>Nombre de privilegio</strong></th>
   <th><strong>Lo que controla el privilegio de...</strong></th>
  </tr>
  <tr>
   <td><code>jcr:read</code></td>
   <td>Recupere un nodo y lea sus propiedades y sus valores.</td>
  </tr>
  <tr>
   <td><code>rep:write</code></td>
   <td>Se trata de un privilegio agregado específico de jackrabbit de jcr:write y jcr:nodeTypeManagement.<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:all</code></td>
   <td>Es un privilegio agregado que contiene todos los demás privilegios predefinidos.</td>
  </tr>
  <tr>
   <td><strong>Avanzado </strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>crx:replicate</code></td>
   <td>Realice la replicación de un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:addChildNodes</code></td>
   <td>Crear nodos secundarios de un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:lifecycleManagement</code></td>
   <td>Realizar operaciones del ciclo vital en un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:lockManagement</code></td>
   <td>Bloquear y desbloquear un nodo; actualizar un bloqueo.</td>
  </tr>
  <tr>
   <td><code>jcr:modifyAccessControl</code></td>
   <td>Modificar las directivas de control de acceso de un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:modifyProperties</code></td>
   <td>Cree, modifique y elimine las propiedades de un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:namespaceManagement</code></td>
   <td>Registrar, anular el registro y modificar definiciones de área de nombres.</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeDefinitionManagement</code></td>
   <td>Importe definiciones de tipo de nodo al repositorio.</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeManagement</code></td>
   <td>Añada y elimine tipos de nodos de mezcla y cambie el tipo de nodo principal de un nodo. Esto también incluye cualquier llamada a los métodos de importación Node.addNode y XML donde el tipo mixin o principal del nuevo nodo se especifica explícitamente.</td>
  </tr>
  <tr>
   <td><code>jcr:readAccessControl</code></td>
   <td>Leer la directiva de control de acceso de un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:removeChildNodes</code></td>
   <td>Quitar nodos secundarios de un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:removeNode</code></td>
   <td>Elimine un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:retentionManagement</code></td>
   <td>Realizar operaciones de administración de retención en un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:versionManagement</code></td>
   <td>Realizar operaciones de versiones en un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:workspaceManagement</code></td>
   <td>Creación y eliminación de espacios de trabajo mediante la API JCR.</td>
  </tr>
  <tr>
   <td><code>jcr:write</code></td>
   <td>Se trata de un privilegio agregado que contiene:<br /> - jcr:modifyProperties<br /> - jcr:addChildNodes<br /> - jcr:removeNode<br /> - jcr:removeChildNodes</td>
  </tr>
  <tr>
   <td><code>rep:privilegeManagement</code></td>
   <td>Registrar nuevo privilegio.</td>
  </tr>
 </tbody>
</table>

### Registro de nuevos privilegios {#registering-new-privileges}

También puede registrar nuevos privilegios:

1. En la barra de herramientas, seleccione **Herramientas**, entonces **Privilegios** para mostrar los privilegios registrados actualmente.

   ![ac_privilegios](assets/ac_privileges.png)

1. Utilice el **Registrar privilegio** icono (**+**) para abrir el cuadro de diálogo y definir un nuevo privilegio:

   ![ac_privilegieregister](assets/ac_privilegeregister.png)

1. Haga clic en **Aceptar** para guardar. El privilegio ahora estará disponible para su selección.

### Agregar una entrada de control de acceso {#adding-an-access-control-entry}

1. Seleccione el recurso y abra **Control de acceso** pestaña.

1. Para añadir una nueva **Políticas de control de acceso local**, haga clic en **+** en la parte derecha del icono **Política de control de acceso aplicable** lista:

   ![crx_accesscontrol_apply](assets/crx_accesscontrol_applicable.png)

1. Aparece una nueva entrada debajo de **Políticas de control de acceso local:**

   ![crx_accesscontrol_newlocal](assets/crx_accesscontrol_newlocal.png)

1. Haga clic en **+** icono para añadir una nueva entrada:

   ![crx_accesscontrol_addentry](assets/crx_accesscontrol_addentry.png)

   >[!NOTE]
   >
   >Actualmente, se necesita una solución para especificar una cadena vacía.
   >
   >Para ello, debe utilizar &quot;&quot;.

1. Defina la política de control de acceso y haga clic en **OK** para guardar. La nueva directiva:

   * se enumerarán en **Directiva de control de acceso local**
   * los cambios se reflejarán en la **Políticas de control de acceso efectivas**.

CRX validará su selección; para un principal determinado existe (como máximo) 1 entrada denegada y 1 entrada permitida en un nodo determinado. La implementación siempre borra las entradas redundantes y se asegura de que el mismo privilegio no aparezca en las entradas de permiso y de denegación.

### Ordenación de directivas de control de acceso local {#ordering-local-access-control-policies}

El orden en la lista indica el orden en que se aplican las directivas.

1. En la tabla de **Políticas de control de acceso local** seleccione la entrada requerida y arrástrela a la nueva posición de la tabla.

   ![crx_accesscontrol_reorder](assets/crx_accesscontrol_reorder.png)

1. Los cambios se mostrarán en ambas tablas de **Local** y el **Políticas de control de acceso efectivas**.

### Eliminación de una directiva de control de acceso {#removing-an-access-control-policy}

1. En la tabla de **Políticas de control de acceso local** haga clic en el icono rojo (-) a la derecha de la entrada.
1. La entrada se eliminará de ambas tablas para el **Local** y el **Políticas de control de acceso efectivas**.

### Probar una directiva de control de acceso {#testing-an-access-control-policy}

1. En la barra de herramientas del CRXDE Lite, seleccione **Herramientas**, entonces **Probar control de acceso...**.
1. Se abrirá un nuevo cuadro de diálogo en el panel superior derecho. Seleccione el **Ruta** y/o **Principal** que desee probar.
1. Clic **Prueba** para ver los resultados de su selección:

   ![crx_accesscontrol_test](assets/crx_accesscontrol_test.png)
