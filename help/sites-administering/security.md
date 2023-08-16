---
title: Administración de usuarios y seguridad
description: AEM Obtenga información sobre la administración de usuarios y la seguridad en la.
uuid: 4512c0bf-71bf-4f64-99f6-f4fa5a61d572
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e72da81b-4085-49b0-86c3-11ad48978a8a
docset: aem65
exl-id: 53d8c654-8017-4528-a44e-e362d8b59f82
feature: Security
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '5401'
ht-degree: 1%

---

# Administración de usuarios y seguridad{#user-administration-and-security}

AEM En este capítulo se describe cómo configurar y mantener la autorización de los usuarios, así como la teoría en la que se basa la autenticación y la autorización para trabajar en los entornos de trabajo de los usuarios de la red de área de trabajo de la.

## AEM Usuarios y grupos en la {#users-and-groups-in-aem}

Esta sección trata con más detalle las distintas entidades y conceptos relacionados para ayudarle a configurar un concepto de administración de usuarios fácil de mantener.

### Usuarios {#users}

AEM Los usuarios inician sesión en la cuenta de para acceder a la sesión de la cuenta de. Cada cuenta de usuario es única y contiene los detalles básicos de la cuenta, junto con los privilegios asignados.

Los usuarios suelen ser miembros de Grupos, lo que simplifica la asignación de estos permisos o privilegios.

### Grupos {#groups}

Los grupos son colecciones de usuarios, otros grupos o ambos. Todas estas colecciones se denominan Miembros de un grupo.

Su objetivo principal es simplificar el proceso de mantenimiento reduciendo el número de entidades que se van a actualizar, ya que los cambios realizados en un grupo se aplican a todos los miembros del grupo. Los grupos suelen reflejar:

* una función dentro de la aplicación; por ejemplo, alguien a quien se permite navegar por el contenido o alguien a quien se permite contribuir con contenido.
* su propia organización; puede que desee ampliar las funciones para diferenciar entre colaboradores de distintos departamentos cuando estén restringidos a distintas ramas del árbol de contenido.

Por lo tanto, los grupos tienden a permanecer estables, mientras que los usuarios van y vienen con más frecuencia.

Con una planificación y una estructura limpia, el uso de grupos puede reflejar su estructura, lo que le ofrece una visión general clara y un mecanismo eficaz para las actualizaciones.

### Usuarios y grupos integrados {#built-in-users-and-groups}

AEM WCM instala varios usuarios y grupos. Estas colecciones se ven al acceder por primera vez a la consola de seguridad después de la instalación.

Las siguientes tablas enumeran cada elemento junto con:

* una descripción breve
* cualquier recomendación sobre los cambios necesarios

*Cambiar todas las contraseñas predeterminadas* (si no elimina la cuenta en determinadas circunstancias).

<table>
 <tbody>
  <tr>
   <td>ID de usuario</td>
   <td>Tipo</td>
   <td>Descripción</td>
   <td>Recomendación</td>
  </tr>
  <tr>
   <td><p>administrador</p> <p>Contraseña predeterminada: admin</p> </td>
   <td>Usuario</td>
   <td><p>Cuenta de administración del sistema con derechos de acceso completos.</p> <p>AEM Esta cuenta se utiliza para la conexión entre WCM y CRX.</p> <p>Si elimina esta cuenta accidentalmente, se vuelve a crear al reiniciar el repositorio (en la configuración predeterminada).</p> <p>AEM La cuenta de administrador es un requisito de la plataforma de. Como consecuencia, esta cuenta no se puede eliminar.</p> </td>
   <td><p>El Adobe recomienda cambiar la contraseña predeterminada de esta cuenta de usuario.</p> <p>Preferiblemente en la instalación, aunque se puede realizar posteriormente.</p> <p>Nota: No confunda esta cuenta con la cuenta de administrador del motor de servlets CQ.</p> </td>
  </tr>
  <tr>
   <td><p>anónimo</p> <p> </p> </td>
   <td>Usuario</td>
   <td><p>Mantiene los derechos predeterminados para el acceso no autenticado a una instancia. De forma predeterminada, esta cuenta mantiene los derechos de acceso mínimos.</p> <p>Si elimina esta cuenta accidentalmente, se vuelve a crear al inicio. No se puede eliminar de forma permanente, pero se puede deshabilitar.</p> </td>
   <td>Evite eliminar o deshabilitar esta cuenta, ya que afecta negativamente al funcionamiento de las instancias de autor. Si existen requisitos de seguridad que obligan a eliminarla, asegúrese de probar correctamente los efectos que tiene en sus sistemas primero.</td>
  </tr>
  <tr>
   <td><p>autor</p> <p>Contraseña predeterminada: author</p> </td>
   <td>Usuario</td>
   <td><p>Una cuenta de autor con permiso para escribir en /content. Incluye privilegios de colaborador y internauta.</p> <p>Se puede utilizar como webmaster ya que tiene acceso a todo el árbol /content.</p> <p>Esta cuenta no es un usuario integrado, sino otro usuario de demostración de Geometrixx</p> </td>
   <td><p>El Adobe recomienda que la cuenta se elimine por completo o que se cambie la contraseña predeterminada.</p> <p>Preferiblemente en la instalación, aunque se puede realizar posteriormente.</p> </td>
  </tr>
  <tr>
   <td>administradores</td>
   <td>Grupo</td>
   <td><p>Grupo que otorga derechos de administrador a todos sus miembros. Solo el administrador puede editar este grupo.</p> <p>Tiene derechos de acceso completos.</p> </td>
   <td>Incluso si establece el valor "denegar a todos" en un nodo, los administradores podrán acceder a él</td>
  </tr>
  <tr>
   <td>content-authors</td>
   <td>Grupo</td>
   <td><p>Grupo responsable de la edición de contenido. Requiere permisos de lectura, modificación, creación y eliminación.</p> </td>
   <td>Puede crear sus propios grupos de autores de contenido con derechos de acceso específicos del proyecto, siempre que agregue permisos de lectura, modificación, creación y eliminación.</td>
  </tr>
  <tr>
   <td>colaborador</td>
   <td>Grupo</td>
   <td><p>Privilegios básicos que permiten al usuario escribir contenido (como en, solo funcionalidad).</p> <p>No asigna ningún privilegio al árbol /content. Se debe asignar a los grupos o usuarios individuales.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>dam-users</td>
   <td>Grupo</td>
   <td>Grupo de referencia predeterminado para un usuario típico de AEM Assets. Los miembros de este grupo tienen los privilegios adecuados para habilitar la carga o el uso compartido de recursos y colecciones.</td>
   <td> </td>
  </tr>
  <tr>
   <td>todos</td>
   <td>Grupo</td>
   <td><p>AEM Todos los usuarios de la lista de miembros son miembros del grupo y todos, aunque es posible que no vea el grupo o la relación de pertenencia en todas las herramientas.</p> <p>Este grupo puede considerarse como los derechos predeterminados, ya que puede utilizarse para aplicar permisos para todos, incluso para los usuarios que se creen en el futuro.</p> </td>
   <td><p>No modifique ni elimine este grupo.</p> <p>Modificar esta cuenta tiene implicaciones de seguridad adicionales.</p> </td>
  </tr>
  <tr>
   <td>administradores de etiquetas</td>
   <td>Grupo</td>
   <td>Grupo que puede editar etiquetas.</td>
   <td> </td>
  </tr>
  <tr>
   <td>user-administrators</td>
   <td>Grupo</td>
   <td>Autoriza la administración de usuarios, es decir, el derecho a crear usuarios y grupos.</td>
   <td> </td>
  </tr>
  <tr>
   <td>workflow-editors</td>
   <td>Grupo</td>
   <td>Grupo que puede crear y modificar modelos de flujo de trabajo.</td>
   <td> </td>
  </tr>
  <tr>
   <td>workflow-users</td>
   <td>Grupo</td>
   <td><p>Un usuario que participe en un flujo de trabajo debe ser miembro del grupo workflow-users. Otorga al usuario acceso completo a: /etc/workflow/instances para que puedan actualizar la instancia del flujo de trabajo.</p> <p>El grupo está incluido en la instalación estándar, pero debe agregar manualmente los usuarios al grupo.</p> </td>
  </tr>
 </tbody>
</table>

## AEM Permisos en la {#permissions-in-aem}

AEM Utiliza ACL de para determinar qué acciones puede realizar un usuario o grupo y dónde puede realizar esas acciones.

### Permisos y ACL {#permissions-and-acls}

Los permisos definen quién puede realizar qué acciones en un recurso. Los permisos son el resultado de [control de acceso](#access-control-lists-and-how-they-are-evaluated) evaluaciones.

AEM Puede cambiar los permisos concedidos o denegados a un usuario determinado activando o desactivando las casillas de verificación de cada uno de los usuarios en cuestión [acciones](security.md#actions). Una marca de verificación indica que se permite una acción. Ninguna marca de verificación indica que se haya denegado una acción.

AEM La posición de la marca de verificación en la cuadrícula también indica qué permisos tienen los usuarios en qué ubicaciones dentro de la cuadrícula (es decir, en qué rutas de acceso).

### Acciones {#actions}

Las acciones se pueden realizar en una página (recurso). Para cada página de la jerarquía, puede especificar qué acción puede realizar el usuario en esa página. [Permisos](#permissions-and-acls) permite o deniega una acción.

<table>
 <tbody>
  <tr>
   <td><strong>Acción </strong></td>
   <td><strong>Descripción </strong></td>
  </tr>
  <tr>
   <td>Leer</td>
   <td>El usuario tiene permiso para leer la página y las páginas secundarias.</td>
  </tr>
  <tr>
   <td>Modificar</td>
   <td><p>El usuario puede:</p>
    <ul>
     <li>modifique el contenido existente en la página y en cualquier página secundaria.</li>
     <li>cree párrafos en la página o en cualquier página secundaria.</li>
    </ul> <p>En el nivel JCR, los usuarios pueden editar un recurso editando sus propiedades, bloqueando, creando versiones, no modificando y tienen permiso de escritura completo en los nodos que definen un nodo secundario jcr:content. Por ejemplo: cq:Page, nt:file, cq:Asset.</p> </td>
  </tr>
  <tr>
   <td>Crear</td>
   <td><p>El usuario puede:</p>
    <ul>
     <li>cree una página o una página secundaria.</li>
    </ul> <p>If <strong>modificar</strong> se ha denegado, los subárboles debajo de jcr:content se excluyen porque la creación de jcr:content y sus nodos secundarios se consideran una modificación de la página. Esta regla solo se aplica a los nodos que definen un nodo secundario jcr:content.</p> </td>
  </tr>
  <tr>
   <td>Eliminar</td>
   <td><p>El usuario puede:</p>
    <ul>
     <li>elimine los párrafos existentes de la página o de cualquier página secundaria.</li>
     <li>elimine una página o página secundaria.</li>
    </ul> <p>If <strong>modificar</strong> se deniega a cualquier subárbol debajo de jcr:content porque la eliminación de jcr:content y sus nodos secundarios se considera una modificación de la página. Esta regla solo se aplica a los nodos que definen un nodo secundario jcr:content.</p> </td>
  </tr>
  <tr>
   <td>Leer ACL</td>
   <td>El usuario puede leer la lista de control de acceso de la página o de las páginas secundarias.</td>
  </tr>
  <tr>
   <td>Editar ACL</td>
   <td>El usuario puede modificar la lista de control de acceso de la página o de cualquier página secundaria.</td>
  </tr>
  <tr>
   <td>Replicar</td>
   <td>El usuario puede replicar contenido en otro entorno (por ejemplo, el entorno de publicación). El privilegio también se aplica a cualquier página secundaria.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM El usuario genera automáticamente grupos de usuarios para la asignación de funciones (propietario, editor, visor) en [Colecciones](/help/assets/manage-collections.md). AEM Sin embargo, añadir manualmente ACL para estos grupos puede introducir vulnerabilidades de seguridad dentro de los grupos de trabajo de. Adobe recomienda evitar agregar ACL manualmente.

### Listas de control de acceso y cómo se evalúan {#access-control-lists-and-how-they-are-evaluated}

AEM WCM utiliza Listas de control de acceso (ACL) para organizar los permisos que se aplican a las distintas páginas.

Las listas de control de acceso están formadas por los permisos individuales y se utilizan para determinar el orden en que se aplican estos permisos. La lista se forma según la jerarquía de las páginas que se consideren. A continuación, esta lista se analiza de abajo hacia arriba hasta que se encuentre el primer permiso apropiado para aplicar a una página.

>[!NOTE]
>
>Hay ACL que se incluyen con los ejemplos. Se recomienda revisar y determinar qué es lo más apropiado para sus aplicaciones. Para revisar las ACL que se incluyen, vaya a **CRXDE** y seleccione la **Control de acceso** para los siguientes nodos:
>
>* `/etc/cloudservices`
>* `/home/users/we-retail`
>
>La aplicación personalizada puede establecer el acceso para otras relaciones, como:
>
>* `*/social/relationships/friend/*`
>* o `*/social/relationships/pending-following/*`.
>
>Al crear ACL específicos de las comunidades, se pueden otorgar permisos adicionales a los miembros que se unen a esas comunidades. Por ejemplo, cuando los usuarios se unen a las comunidades en: `/content/we-retail/us/en/community`

### Estados de permisos {#permission-states}

>[!NOTE]
>
>Para usuarios de CQ 5.3:
>
>A diferencia de las versiones anteriores de CQ, **crear** y **eliminar** ya no debería concederse si un usuario solo debe modificar páginas. En su lugar, conceda la **modificar** solo si desea que los usuarios puedan crear, modificar o eliminar componentes en páginas existentes.
>
>Por motivos de compatibilidad con versiones anteriores, las pruebas para acciones no toman el tratamiento especial de nodos que definen **jcr:contenido** en cuenta.

| **Acción** | **Descripción** |
|---|---|
| Permitir (marca de verificación) | AEM WCM permite que el usuario realice la acción en esta página o en cualquier página secundaria. |
| Denegar (sin marca de verificación) | AEM WCM no permite que el usuario realice la acción en esta página ni en ninguna página secundaria. |

Los permisos también se aplican a cualquier página secundaria.

Si un permiso no se hereda del nodo principal pero tiene al menos una entrada local para él, los siguientes símbolos se anexan a la casilla de verificación. Una entrada local es la que se crea en la interfaz CRX 2.2 (actualmente, solo se pueden crear ACL comodín en CRX).

Para una acción en una ruta determinada:

<table>
 <tbody>
  <tr>
   <td>* (asterisco)</td>
   <td>Hay al menos una entrada local (efectiva o ineficaz). Estas ACL comodín se definen en CRX.</td>
  </tr>
  <tr>
   <td>! (signo de exclamación)</td>
   <td>Hay al menos una entrada que actualmente no tiene ningún efecto.</td>
  </tr>
 </tbody>
</table>

Cuando pasa el ratón sobre el asterisco o el signo de exclamación, la información sobre herramientas proporciona más detalles sobre las entradas declaradas. La información del objeto se divide en dos partes:

<table>
 <tbody>
  <tr>
   <td>Parte superior</td>
   <td><p>Muestra las entradas efectivas.</p> </td>
  </tr>
  <tr>
   <td>Parte inferior</td>
   <td>Enumera las entradas no efectivas que pueden tener efecto en algún otro lugar del árbol (tal como indica un atributo especial presente con la ACE correspondiente que limita el ámbito de la entrada). Alternativamente, es una entrada cuyo efecto se revoca con otra entrada definida en la ruta dada o en un nodo antecesor.</td>
  </tr>
 </tbody>
</table>

![chlimage_1-112](assets/chlimage_1-112.png)

>[!NOTE]
>
>Si no se definen permisos para una página, se deniegan todas las acciones.

A continuación se ofrecen recomendaciones acerca de la administración de listas de control de acceso:

* No asigne permisos directamente a los usuarios. Asígnelos únicamente a grupos.

  Esto simplifica el mantenimiento, ya que el número de grupos es mucho menor que el número de usuarios y también menos volátil.

* Si desea que un grupo o usuario solo pueda modificar páginas, no le conceda derechos de creación ni de denegación. Conceda solo derechos de modificación y lectura.
* Utilice Denegar con moderación. En la medida de lo posible, utilice Permitir solamente.

  El uso de denegar puede producir efectos inesperados si los permisos se aplican en un orden diferente al esperado. Si un usuario es miembro de más de un grupo, las instrucciones Denegar de un grupo pueden cancelar la instrucción Permitir de otro grupo o viceversa. Es difícil mantener una visión general cuando sucede algo así y puede llevar fácilmente a resultados imprevistos, mientras que Permitir asignaciones no causa tales conflictos.

  El Adobe recomienda trabajar con Permitir en lugar de Denegar para ver [Prácticas recomendadas](#best-practices).

Antes de modificar cualquiera de los permisos, asegúrese de comprender cómo funcionan y cómo se relacionan entre sí. AEM Consulte la documentación de CRX que ilustra cómo se usa WCM para la administración de la [evalúa los derechos de acceso](/help/sites-administering/user-group-ac-admin.md#how-access-rights-are-evaluated)y ejemplos sobre la configuración de listas de control de acceso.

### Permisos {#permissions}

AEM AEM Los permisos otorgan a los usuarios y grupos acceso a la funcionalidad de la en páginas de informes.

Para examinar los permisos por ruta, expanda o contraiga los nodos y puede realizar un seguimiento de la herencia de permisos hasta el nodo raíz.

Para permitir o denegar permisos, active o desactive las casillas de verificación correspondientes.

![cqsecuritypermimissionstab](assets/cqsecuritypermissionstab.png)

### Visualización de información detallada de permisos {#viewing-detailed-permission-information}

AEM Junto con la vista de cuadrícula, proporciona una vista detallada de los permisos para un usuario/grupo seleccionado en una ruta determinada. La vista de detalles proporciona información adicional.

Además de ver la información, también puede incluir o excluir al usuario o grupo actual de un grupo. Consulte [Agregar usuarios o grupos al agregar permisos](#adding-users-or-groups-while-adding-permissions). Los cambios realizados aquí se reflejan inmediatamente en la parte superior de la vista detallada.

Para acceder a la vista de detalles, en **Permisos** pestaña, haga clic en **Detalles** para cualquier grupo/usuario y ruta seleccionados.

![detalles del permiso](assets/permissiondetails.png)

Los detalles se dividen en dos partes:

<table>
 <tbody>
  <tr>
   <td>Parte superior</td>
   <td><p>Repite la información que se ve en la cuadrícula del árbol. Para cada acción, un icono muestra si la acción está permitida o denegada:</p>
    <ul>
     <li>sin icono = sin entrada declarada</li>
     <li>(marca) = acción declarada (permitir)</li>
     <li>(-) = acción declarada (denegar)</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Parte inferior</td>
   <td><p>Muestra la cuadrícula de usuarios y grupos que hace lo siguiente:</p>
    <ul>
     <li>Declara una entrada para la ruta dada AND</li>
     <li>¿El OR autorizado dado es un grupo?</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Suplantar a otro usuario {#impersonating-another-user}

Con el [Suplantar funcionalidad](/help/sites-authoring/user-properties.md#user-settings), un usuario puede trabajar en nombre de otro usuario.

Es decir, una cuenta de usuario puede especificar otras cuentas que pueden funcionar con su cuenta. Por ejemplo, si el usuario B puede suplantar al usuario A, el usuario B puede actuar utilizando los detalles completos de la cuenta del usuario A.

Esta funcionalidad permite que las cuentas de suplantación completen tareas como si estuvieran utilizando la cuenta que están suplantando. Por ejemplo, durante una ausencia o para compartir una carga excesiva a corto plazo.

>[!NOTE]
>
>Para que la suplantación funcione para usuarios no administradores, el suplantador (en el caso anterior, el usuario B) debe tener permisos de LECTURA en `/home/users` ruta.
>
>Consulte [AEM Permisos en la](/help/sites-administering/security.md#permissions-in-aem).

>[!CAUTION]
>
>Si una cuenta suplanta a otra, es difícil verla. Se realiza una entrada en el registro de auditoría cuando comienza y finaliza la suplantación, pero los demás archivos de registro (como el registro de acceso) no contienen información de que se haya producido una suplantación en los eventos. Por lo tanto, si el usuario B está suplantando al usuario A, todos los eventos tienen el aspecto de que el usuario A los realizó.

>[!CAUTION]
>
>El bloqueo de páginas se puede realizar al suplantar a un usuario. Sin embargo, una página bloqueada de este modo solo se puede desbloquear como el usuario que se ha suplantado o como un usuario con privilegios de administrador.
>
>Las páginas no se pueden desbloquear al suplantar al usuario que ha bloqueado la página.

### Prácticas recomendadas {#best-practices}

A continuación se describen las prácticas recomendadas al trabajar con permisos y privilegios:

| Regla | Motivo |
|--- |--- |
| *Usar grupos* | Evite asignar derechos de acceso usuario por usuario. Existen varias razones para este consejo:<ul><li>Hay muchos más usuarios que grupos, por lo que los grupos simplifican la estructura.</li><li>Los grupos ayudan a proporcionar una visión general de todas las cuentas.</li> <li>La herencia es más sencilla con los grupos.</li><li>Los usuarios van y vienen. Los grupos son a largo plazo.</li></ul> |
| *Sea positivo* | Utilice siempre las instrucciones Allow para especificar los derechos del grupo (siempre que sea posible). Evite utilizar una instrucción Deny. Los grupos se evalúan en orden y el orden puede definirse de forma diferente por usuario. En otras palabras: es posible que tenga poco control sobre el orden en que se implementan y evalúan las instrucciones. Si solo utiliza instrucciones Allow, el orden no importa. |
| *Manténgalo Simple* | Invertir algo de tiempo y reflexión a la hora de configurar una nueva instalación merece la pena. La aplicación de una estructura clara simplifica el mantenimiento y la administración continuos, lo que garantiza que tanto sus compañeros actuales como sus futuros sucesores puedan comprender fácilmente qué se implementa. |
| *Probar* | Utilice una instalación de prueba para practicar y asegurarse de que comprende las relaciones entre los distintos usuarios y grupos. |
| *Usuarios/grupos predeterminados* | Actualice siempre Usuarios y grupos predeterminados inmediatamente después de la instalación para evitar problemas de seguridad. |

## Administración de usuarios y grupos {#managing-users-and-groups}

Los usuarios incluyen a las personas que utilizan el sistema y a los sistemas extranjeros que realizan solicitudes al sistema.

Un grupo es un conjunto de usuarios.

Ambos se pueden configurar mediante la funcionalidad Administración de usuarios de la consola de seguridad.

### Acceso a la administración de usuarios con la consola de seguridad {#accessing-user-administration-with-the-security-console}

Puede acceder a todos los usuarios, grupos y permisos asociados mediante la consola de seguridad. Todos los procedimientos descritos en esta sección se realizan en esta ventana.

AEM Para tener acceso a la seguridad de WCM de la, siga uno de estos procedimientos:

* AEM En la pantalla de bienvenida de o en varias ubicaciones de, haga clic en el icono de seguridad:

![AEM Pestaña Seguridad de WCM de](do-not-localize/wcmtoolbar.png)

* Vaya directamente a `https://<server>:<port>/useradmin`. AEM Asegúrese de iniciar sesión en el servicio de administración de.

Se muestra la siguiente ventana:

![cqsecuritypage](assets/cqsecuritypage.png)

El árbol izquierdo enumera todos los usuarios y grupos que hay actualmente en el sistema. Puede seleccionar las columnas que desea mostrar, ordenar su contenido e incluso cambiar el orden en que se muestran arrastrando el encabezado de columna a una nueva posición.

![cqsecuritycolumncontext](assets/cqsecuritycolumncontext.png)

Las pestañas proporcionan acceso a varias configuraciones:

<!-- ??? in table below. -->

| Pestaña | Descripción |
|--- |--- |
| Cuadro de filtro | Mecanismo para filtrar los usuarios, grupos o ambos enumerados. Consulte [Filtrado de usuarios y grupos](#filtering-users-and-groups). |
| Ocultar usuarios | Conmutador que oculta todos los usuarios de la lista y deja sólo grupos. Consulte [Ocultar usuarios y grupos](#hiding-users-and-groups). |
| Ocultar grupos | Conmutador que oculta todos los grupos enumerados y deja solamente usuarios. Consulte [Ocultar usuarios y grupos](#hiding-users-and-groups). |
| Editar | Un menú que le permite crear y eliminar, así como activar y desactivar usuarios o grupos. Consulte [Creación de usuarios y grupos](#creating-users-and-groups) y [Eliminación de usuarios y grupos](#deleting-users-and-groups). |
| Propiedades | Enumera información sobre el usuario o grupo que puede incluir información de correo electrónico, una descripción e información de nombres. También permite cambiar la contraseña de un usuario. Consulte [Creación de usuarios y grupos](#creating-users-and-groups), [Modificación de las propiedades de usuario y grupo](#modifying-user-and-group-properties) y [Cambiar una contraseña de usuario](#changing-a-user-password). |
| Grupos | Enumera todos los grupos a los que pertenece el usuario o grupo seleccionado. Puede asignar el usuario o grupos seleccionados a grupos adicionales o eliminarlos de grupos. Consulte [Grupos](#adding-users-or-groups-to-a-group). |
| Miembros | Disponible solo para grupos. Enumera los miembros de un grupo determinado. Consulte [Miembros](#members-adding-users-or-groups-to-a-group). |
| Permisos | Puede asignar permisos a un usuario o grupo. Permite controlar lo siguiente:<ul><li>Permisos relacionados con páginas o nodos concretos. Consulte [Configuración de permisos](#setting-permissions). </li><li>Permisos relacionados con la creación y eliminación de páginas y la modificación de la jerarquía. ??? le permite [asignación de privilegios](#settingprivileges), como la modificación de jerarquías, que permite crear y eliminar páginas,</li><li>Permisos relacionados con [privilegios de replicación](#setting-replication-privileges) (normalmente de autor a publicación) según una ruta.</li></ul> |
| Suplantadores | Permite que otro usuario suplante la cuenta. Resulta útil cuando necesita que un usuario actúe en nombre de otro usuario. Consulte [Suplantación de usuarios](#impersonating-another-user). |
| Preferencias | Conjuntos [preferencias para el grupo o usuario](#setting-user-and-group-preferences). Por ejemplo, las preferencias de idioma. |

### Filtrado de usuarios y grupos {#filtering-users-and-groups}

Puede filtrar la lista introduciendo una expresión de filtro, que oculta todos los usuarios y grupos que no coinciden con la expresión. También puede ocultar usuarios y grupos mediante el [Ocultar usuario y ocultar grupo](#hiding-users-and-groups) botones.

Para filtrar usuarios o grupos:

1. En la lista del árbol izquierdo, escriba la expresión de filtro en el espacio proporcionado. Por ejemplo, introducir **administrador** muestra todos los usuarios y grupos que contienen esta cadena.
1. Haga clic en la lupa para filtrar la lista.

   ![cqsecurityfilter](assets/cqsecurityfilter.png)

1. Haga clic en **x** cuando desee eliminar todos los filtros.

### Ocultar usuarios y grupos {#hiding-users-and-groups}

Ocultar usuarios o grupos es otra forma de filtrar la lista de todos los usuarios y grupos de un sistema. Existen dos mecanismos de alternancia. Al hacer clic en Ocultar usuario, se ocultan todos los usuarios de la vista y al hacer clic en Ocultar grupos, se ocultan todos los grupos de la vista (no se pueden ocultar tanto los usuarios como los grupos al mismo tiempo). Para filtrar la lista utilizando una expresión de filtro, consulte [Filtrado de usuarios y grupos](#filtering-users-and-groups).

Para ocultar usuarios y grupos:

1. En el **Seguridad** consola, haga clic en **Ocultar usuarios** o **Ocultar grupos**. El botón seleccionado aparece resaltado.

   ![cqsecurityhideusers](assets/cqsecurityhideusers.png)

1. Para que vuelvan a aparecer usuarios o grupos, haga clic de nuevo en el botón correspondiente.

### Creación de usuarios y grupos {#creating-users-and-groups}

Para crear un usuario o un grupo:

1. En el **Seguridad** lista del árbol de la consola, haga clic en **Editar** y, a continuación, **Crear usuario** o **Crear grupo**.

   ![cqseruityeditcontextmenu](assets/cqseruityeditcontextmenu.png)

1. Introduzca los detalles necesarios, en función de si está creando un usuario o un grupo.

   * Si selecciona **Crear usuario,** Introduzca el ID de inicio de sesión, el nombre y los apellidos, la dirección de correo electrónico y una contraseña. AEM De forma predeterminada, crea una ruta basada en la primera letra del apellido, pero puede seleccionar otra ruta.

   ![createuserdialog](assets/createuserdialog.png)

   * Si selecciona **Crear grupo**, introduzca un ID de grupo y una descripción opcional.

   ![creategroupdialog](assets/creategroupdialog.png)

1. Haga clic en **Crear**. El usuario o grupo que ha creado aparece en la lista de árbol.

### Eliminación de usuarios y grupos {#deleting-users-and-groups}

Para eliminar un usuario o un grupo:

1. En el **Seguridad** , seleccione el usuario o grupo que desee eliminar. Si desea eliminar varios elementos, pulse Mayús + clic o Control + clic para seleccionarlos.
1. Clic **Editar,** a continuación, seleccione Eliminar. AEM WCM pregunta si desea eliminar el usuario o el grupo.
1. Clic **OK** para confirmar o cancelar.

### Modificación de las propiedades de usuario y grupo {#modifying-user-and-group-properties}

Para modificar las propiedades de usuario y grupo:

1. En el **Seguridad** , haga doble clic en el nombre de usuario o de grupo que desee modificar.

1. Haga clic en **Propiedades** , realice los cambios necesarios y haga clic en **Guardar**.

   ![cqsecurityuserprops](assets/cqsecurityuserprops.png)

>[!NOTE]
>
>La ruta del usuario se muestra en la parte inferior de las propiedades del usuario. No se puede modificar.

### Cambiar una contraseña de usuario {#changing-a-user-password}

Utilice el siguiente procedimiento para modificar la contraseña de un usuario.

>[!NOTE]
>
>No puede usar la consola de seguridad para cambiar la contraseña de administrador. Para cambiar la contraseña de la cuenta de administrador, utilice la variable [Consola de usuarios](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user) que proporciona Granite Operations.
>
>Si utiliza AEM Forms en JEE, no utilice las instrucciones siguientes para cambiar la contraseña, sino que utilice AEM Forms en el Admin Console JEE (/adminui) para cambiar la contraseña.

1. En el **Seguridad** , haga doble clic en el nombre de usuario cuya contraseña desea cambiar.
1. Haga clic en **Propiedades** pestaña (si no está activa).
1. Clic **Establecer contraseña**. Se abrirá la ventana Establecer contraseña, donde podrá cambiarla.

   ![cqsecurityuserpassword](assets/cqsecurityuserpassword.png)

1. Introduzca la nueva contraseña dos veces; ya que no se muestran en texto no cifrado, esta acción es para confirmación: si no coinciden, el sistema muestra un error.
1. Clic **Establecer** para activar la nueva contraseña de la cuenta.

### Adición de usuarios o grupos a un grupo {#adding-users-or-groups-to-a-group}

AEM Ofrece tres formas diferentes de agregar usuarios o grupos a un grupo existente:

* Cuando esté en el grupo, puede agregar miembros (usuarios o grupos).
* Cuando esté en el miembro, puede agregar miembros a grupos.
* Cuando esté trabajando en Permisos, puede agregar miembros a grupos.

### Grupos: agregar usuarios o grupos a un grupo {#groups-adding-users-or-groups-to-a-group}

El **Grupos** La pestaña muestra a qué grupos pertenece la cuenta actual. Puede utilizarlo para agregar la cuenta seleccionada a un grupo:

1. Haga doble clic en el nombre de la cuenta (usuario o grupo) que desee asignar a un grupo.
1. Haga clic en **Grupos** pestaña. Verá una lista de grupos a los que ya pertenece la cuenta.
1. En la lista de árbol, haga clic en el nombre del grupo al que desee agregar la cuenta y arrástrelo al **Grupos** panel. (Si desea agregar varios usuarios, pulse Mayús + clic o Control + clic en esos nombres y arrástrelos).

   ![cqsecurityaddusertogroup](assets/cqsecurityaddusertogroup.png)

1. Clic **Guardar** para guardar los cambios.

### Miembros: agregar usuarios o grupos a un grupo {#members-adding-users-or-groups-to-a-group}

El **Miembros** La pestaña solo funciona para grupos y muestra los usuarios y grupos que pertenecen al grupo actual. Puede utilizarlo para agregar cuentas a un grupo:

1. Haga doble clic en el nombre del grupo al que desea agregar miembros.
1. Haga clic en **Miembros** pestaña. Verá una lista de miembros que ya pertenecen a este grupo.
1. En la lista de árbol, haga clic en el nombre del miembro que desee agregar al grupo y arrástrelo al **Miembros** panel. (Si desea agregar varios usuarios, pulse Mayús + clic o Control + clic en esos nombres y arrástrelos).

   ![cqsecurityadduserasmember](assets/cqsecurityadduserasmember.png)

1. Clic **Guardar** para guardar los cambios.

### Agregar usuarios o grupos al agregar permisos {#adding-users-or-groups-while-adding-permissions}

Para agregar miembros a un grupo en en una ruta determinada:

1. Haga doble clic en el nombre del grupo o usuario al que desee agregar usuarios.

1. Haga clic en **Permisos** pestaña.

1. Vaya a la ruta a la que desee agregar permisos y haga clic en **Detalles**. La parte inferior de la ventana de detalles proporciona información sobre quién tiene permisos para esa página.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. Seleccione la casilla de verificación en la **Miembro** para los miembros que desea que tengan permisos para esa ruta. Desactive la casilla de verificación del miembro para el que desea quitar permisos. Aparece un triángulo rojo en la celda que ha cambiado.
1. Clic **OK** para guardar los cambios.

### Quitar usuarios o grupos de grupos {#removing-users-or-groups-from-groups}

AEM Ofrece tres formas diferentes de eliminar usuarios o grupos de un grupo:

* Cuando se encuentra en el perfil de grupo, puede quitar miembros (usuarios o grupos).
* Cuando se encuentra en el perfil de miembro, puede quitar miembros de los grupos.
* Cuando esté trabajando en Permisos, puede quitar miembros de los grupos.

### Grupos: quitar usuarios o grupos de grupos {#groups-removing-users-or-groups-from-groups}

Para quitar una cuenta de usuario o de grupo de un grupo:

1. Haga doble clic en el nombre del grupo o cuenta de usuario que desea quitar de un grupo.
1. Haga clic en **Grupos** pestaña. Verá a qué grupos pertenece la cuenta seleccionada.
1. En el **Grupos** , haga clic en el nombre del usuario o grupo que desea quitar del grupo y haga clic en **Eliminar**. (Si desea quitar varias cuentas, pulse Mayús + clic o Control + clic en esos nombres y haga clic en **Eliminar**.)

   ![cqsecurityremoveuserfromgrp](assets/cqsecurityremoveuserfromgrp.png)

1. Clic **Guardar** para guardar los cambios.

### Miembros - Quitar usuarios o grupos de grupos {#members-removing-users-or-groups-from-groups}

Para quitar cuentas de un grupo:

1. Haga doble clic en el nombre del grupo del que desea quitar miembros.
1. Haga clic en **Miembros** pestaña. Verá una lista de miembros que ya pertenecen a este grupo.
1. En el **Miembros** , haga clic en el nombre del miembro que desea quitar del grupo y haga clic en **Eliminar**. (Si desea eliminar varios usuarios, pulse Mayús + clic o Control + clic en esos nombres y haga clic en **Eliminar**.)

   ![cqsecurityremovemember](assets/cqsecurityremovemember.png)

1. Clic **Guardar** para guardar los cambios.

### Quitar usuarios o grupos al agregar permisos {#removing-users-or-groups-while-adding-permissions}

Para eliminar miembros de un grupo en una ruta determinada:

1. Haga doble clic en el nombre del grupo o usuario del que desee quitar usuarios.

1. Haga clic en **Permisos** pestaña.

1. Vaya a la ruta en la que desee quitar permisos y haga clic en **Detalles**. La parte inferior de la ventana de detalles proporciona información sobre quién tiene permisos para esa página.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. Seleccione la casilla de verificación en la **Miembro** para los miembros que desea que tengan permisos para esa ruta. Desactive la casilla de verificación del miembro para el que desea quitar permisos. Aparece un triángulo rojo en la celda que ha cambiado.
1. Clic **OK** para guardar los cambios.

### Sincronización de usuarios {#user-synchronization}

Cuando la implementación es una [publicar conjunto de servidores](/help/sites-deploying/recommended-deploys.md#tarmk-farm), los usuarios y grupos deben sincronizarse entre todos los nodos de publicación.

Para obtener más información sobre la sincronización de usuarios y cómo habilitarla, consulte [Sincronización de usuarios](/help/sites-administering/sync.md).

## Administración de permisos {#managing-permissions}

>[!NOTE]
>
>El Adobe ha introducido una nueva vista principal basada en la IU táctil para la administración de permisos. Para obtener más información sobre cómo utilizarla, consulte [esta página](/help/sites-administering/touch-ui-principal-view.md).

En esta sección se describe cómo definir permisos, incluidos los privilegios de replicación.

### Configuración de permisos {#setting-permissions}

Los permisos permiten a los usuarios realizar determinadas acciones en los recursos en determinadas rutas. También incluye la capacidad de crear o eliminar páginas.

Para agregar, modificar o eliminar permisos:

1. En el **Seguridad** , haga doble clic en el nombre del usuario o grupo para el que desee establecer permisos o [buscar nodos](#searching-for-nodes).

1. Haga clic en **Permisos** pestaña.

   ![cquserpermissions](assets/cquserpermissions.png)

1. En la cuadrícula del árbol, active una casilla de verificación para permitir que el usuario o grupo seleccionado realice una acción o desactive una casilla de verificación para denegar al usuario o grupo seleccionado la realización de una acción. Para obtener más información, haga clic en **Detalles**.

1. Cuando termine, haga clic en **Guardar**.

### Configuración de Privilegios de Replicación {#setting-replication-privileges}

El privilegio de replicación es el derecho para publicar contenido y se puede establecer para grupos y usuarios.

>[!NOTE]
>
>* Cualquier derecho de replicación aplicado a un grupo se aplica a todos los usuarios de ese grupo.
>* Los privilegios de replicación de un usuario reemplazan a los de un grupo.
>* Los derechos Permitir replicación tienen una prioridad mayor que Denegar derechos de replicación. Consulte [AEM Permisos en la](#permissions-in-aem) para obtener más información.
>

Para establecer privilegios de replicación:

1. Seleccione el usuario o grupo en la lista, haga doble clic para abrir y haga clic en **Permisos**.
1. En la cuadrícula, vaya a la ruta en la que desea que el usuario tenga privilegios de replicación o [busque nodos.](#searching-for-nodes)

1. En el **Replicar** columna en la ruta seleccionada, active una casilla de verificación para agregar el privilegio de replicación para ese usuario o grupo, o desactive la casilla de verificación para quitar el privilegio de replicación. AEM muestra un triángulo rojo en cualquier lugar donde haya realizado cambios que aún no se hayan guardado.

   ![cquserreplicatepermissions](assets/cquserreplicatepermissions.png)

1. Clic **Guardar** para guardar los cambios.

### Búsqueda de nodos {#searching-for-nodes}

Al agregar o quitar permisos, puede examinar o buscar el nodo.

Existen dos tipos diferentes de búsqueda de ruta:

* Búsqueda de ruta: si la cadena de búsqueda comienza con &quot;/&quot;, busca los subnodos directos de la ruta dada:

![cqsecuritypathsearch](assets/cqsecuritypathsearch.png)

En el cuadro de búsqueda, puede hacer lo siguiente:

| Acción | Qué hace |
|--- |--- |
| Tecla de flecha derecha | Selecciona un subnodo en el resultado de la búsqueda |
| Tecla de flecha abajo | Inicia la búsqueda de nuevo. |
| Tecla Intro (Retorno) | Selecciona un subnodo y lo carga en la cuadrícula del árbol |

* Búsqueda de texto completo: si la cadena de búsqueda no comienza con &quot;/&quot;, se ejecuta una búsqueda de texto completo en todos los nodos de la ruta &quot;/content&quot;.

![cqsecurityfulltextsearch](assets/cqsecurityfulltextsearch.png)

Para realizar una búsqueda de rutas o texto completo:

1. En la consola de seguridad, seleccione un usuario o grupo y, a continuación, haga clic en **Permisos** pestaña.

1. En el cuadro Buscar, escriba el término que desea buscar.

### Suplantación de usuarios {#impersonating-users}

Puede especificar uno o varios usuarios que pueden suplantar al usuario actual. Esta capacidad significa que pueden cambiar la configuración de su cuenta a la del usuario actual y actuar en nombre de este usuario.

Utilice esta función con precaución, ya que puede permitir a los usuarios realizar acciones que su propio usuario no puede. Al suplantar a un usuario, se notifica a los usuarios que no han iniciado sesión como ellos mismos.

Hay varios escenarios en los que puede que desee utilizar esta funcionalidad, incluidos los siguientes:

* Si está fuera de la oficina, puede dejar que otra persona le suplante mientras está fuera. Al utilizar esta función, puede asegurarse de que alguien tenga sus derechos de acceso y de que no necesite modificar un perfil de usuario ni proporcionar su contraseña.
* Puede utilizarlo con fines de depuración. Por ejemplo, para ver cómo el sitio Web busca un usuario con derechos de acceso restringidos. Además, si un usuario se queja de problemas técnicos, puede suplantar a ese usuario para diagnosticar y solucionar el problema.

Para suplantar a un usuario existente:

1. En la lista de árbol, seleccione el nombre de la persona a la que desea asignar otros usuarios para que suplanten. Haga doble clic para abrir.
1. Haga clic en **Suplantadores** pestaña.
1. Haga clic en el usuario que desea que pueda suplantar al usuario seleccionado. Arrastre el usuario (el suplantador) de la lista al panel Suplantar. El nombre aparece en la lista.

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. Haga clic en **Guardar**.

### Estableciendo preferencias de usuario y grupo {#setting-user-and-group-preferences}

Para establecer las preferencias de usuario y grupo, incluidos el idioma, la administración de ventanas y las preferencias de la barra de herramientas:

1. Seleccione el usuario o grupo cuyas preferencias desee cambiar en el árbol de la izquierda. Para seleccionar varios usuarios o grupos, pulse Ctrl+clic o Mayús+clic en sus selecciones.
1. Haga clic en **Preferencias** pestaña.

   ![cqsecuritypreferences](assets/cqsecuritypreferences.png)

1. Realice los cambios necesarios en las preferencias del grupo o usuario y haga clic en **Guardar** cuando termine.

### Configuración de usuarios o administradores para que tengan el privilegio de administrar otros usuarios {#setting-users-or-administrators-to-have-the-privilege-to-manage-other-users}

Para configurar usuarios o administradores para que tengan privilegios de eliminación, activación o desactivación de otros usuarios:

1. Agregue el usuario al que desea otorgar privilegios para administrar otros usuarios al grupo de administradores y guarde los cambios.

   ![cqsecurityaddmembertoadmin](assets/cqsecurityaddmembertoadmin.png)

1. En el de **Permisos** , vaya a &quot;/&quot; y en la columna Replicar, active la casilla de verificación para permitir la replicación en &quot;/&quot; y haga clic en **Guardar**.

   ![cqsecurityreplicatepermissions](assets/cqsecurityreplicatepermissions.png)

   El usuario seleccionado ahora puede desactivar, activar, eliminar y crear usuarios.

### Ampliación de Privilegios en un Nivel de Proyecto {#extending-privileges-on-a-project-level}

Si planea implementar privilegios específicos de la aplicación, la siguiente información describe lo que debe saber para implementar un privilegio personalizado y cómo aplicarlo a través de CQ:

El privilegio de modificación de jerarquía está cubierto por una combinación de privilegios jcr. El privilegio de replicación se denomina **crx:replicar** que se almacena/evalúa junto con otros privilegios en el repositorio jcr. Sin embargo, no se aplica en el nivel jcr.

La definición y el registro de privilegios personalizados forman parte oficialmente del [API de Jackrabbit](https://jackrabbit.apache.org/oak/docs/security/privilege.html) a partir de la versión 2.4 (consulte también [JCR-2887](https://issues.apache.org/jira/browse/JCR-2887)). La administración de control de acceso JCR, tal como se define en, cubre un uso adicional [JSR 283](https://jcp.org/en/jsr/detail?id=283) (sección 16). Además, la API de Jackrabbit define un par de extensiones.

El mecanismo de registro de privilegios se refleja en la interfaz de usuario en **Configuración del repositorio**.

El registro de nuevos privilegios (personalizados) está protegido por un privilegio integrado que debe otorgarse en el nivel de repositorio. En JCR: pasar &quot;null&quot; como parámetro &quot;absPath&quot; en la API de ac mgt, consulte jsr 333 para obtener más información. De forma predeterminada, **administrador** y todos los miembros de administradores tienen ese privilegio concedido.

>[!NOTE]
>
>Aunque la implementación se encarga de validar y evaluar los privilegios personalizados, no puede aplicarlos a menos que sean agregados de privilegios integrados.
