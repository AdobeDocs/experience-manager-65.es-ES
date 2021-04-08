---
title: Administración de usuarios y seguridad
seo-title: Administración de usuarios y seguridad
description: Obtenga información sobre la Administración de usuarios y la seguridad en AEM.
seo-description: Obtenga información sobre la Administración de usuarios y la seguridad en AEM.
uuid: 4512c0bf-71bf-4f64-99f6-f4fa5a61d572
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e72da81b-4085-49b0-86c3-11ad48978a8a
docset: aem65
exl-id: 53d8c654-8017-4528-a44e-e362d8b59f82
feature: Seguridad
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '5488'
ht-degree: 2%

---

# Administración de usuarios y seguridad{#user-administration-and-security}

En este capítulo se describe cómo configurar y mantener la autorización de usuario y también se describe la teoría detrás de cómo funcionan la autenticación y la autorización en AEM.

## Usuarios y grupos en AEM {#users-and-groups-in-aem}

Esta sección trata las distintas entidades y los conceptos relacionados de forma más detallada para ayudarle a configurar un concepto de administración de usuarios fácil de mantener.

### Usuarios {#users}

Los usuarios iniciarán sesión en AEM con su cuenta. Cada cuenta de usuario es única y contiene los detalles básicos de la cuenta, junto con los privilegios asignados.

Los usuarios suelen ser miembros de Grupos, lo que simplifica la asignación de estos permisos y/o privilegios.

### Grupos {#groups}

Los grupos son colecciones de usuarios u otros grupos; todos ellos se denominan miembros de un grupo.

Su principal propósito es simplificar el proceso de mantenimiento reduciendo el número de entidades que se van a actualizar, ya que el cambio realizado en un grupo se aplica a todos los miembros del grupo. Los grupos a menudo reflejan:

* una función en la solicitud; como alguien con permiso para navegar por el contenido o alguien con permiso para contribuir.
* su propia organización; es posible que desee ampliar las funciones para diferenciar entre colaboradores de diferentes departamentos cuando están restringidos a distintas ramas del árbol de contenido.

Por lo tanto, los grupos tienden a permanecer estables, mientras que los usuarios van y vienen con mayor frecuencia.

Con la planificación y una estructura limpia, el uso de grupos puede reflejar su estructura, lo que le ofrece una visión general clara y un mecanismo eficaz para las actualizaciones.

### Usuarios y grupos integrados {#built-in-users-and-groups}

AEM WCM instala varios usuarios y grupos. Esto se puede ver cuando accede por primera vez a la Consola de seguridad después de la instalación.

Las tablas siguientes enumeran cada elemento junto con:

* una breve descripción
* cualquier recomendación sobre los cambios necesarios

*Cambie todas las contraseñas predeterminadas*  (si no elimina la cuenta en sí en determinadas circunstancias).

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
   <td><p>Cuenta de administración del sistema con derechos de acceso completos.</p> <p>Esta cuenta se utiliza para la conexión entre AEM WCM y CRX.</p> <p>Si elimina accidentalmente esta cuenta, se volverá a crear al reiniciar el repositorio (en la configuración predeterminada).</p> <p>La cuenta de administrador es un requisito de la plataforma AEM. Como consecuencia, esta cuenta no se puede eliminar.</p> </td>
   <td><p>Adobe recomienda encarecidamente que la contraseña de esta cuenta de usuario se cambie de la predeterminada.</p> <p>Preferiblemente tras la instalación, aunque se puede hacer después.</p> <p>Nota: Esta cuenta no debe confundirse con la cuenta de administrador del motor Servlet de CQ.</p> </td>
  </tr>
  <tr>
   <td><p>anónimo</p> <p> </p> </td>
   <td>Usuario</td>
   <td><p>Contiene los derechos predeterminados para el acceso no autenticado a una instancia. De forma predeterminada, contiene los derechos de acceso mínimos.</p> <p>Si elimina accidentalmente esta cuenta, se vuelve a crear al inicio. No se puede eliminar permanentemente, pero se puede deshabilitar.</p> </td>
   <td>Evite eliminar o deshabilitar esta cuenta, ya que afectará negativamente el funcionamiento de las instancias de autor. Si hay requisitos de seguridad que le obliguen a eliminarlo, asegúrese de probar correctamente primero los efectos que tiene en sus sistemas.</td>
  </tr>
  <tr>
   <td><p>author</p> <p>Contraseña predeterminada: author</p> </td>
   <td>Usuario</td>
   <td><p>Una cuenta de autor autorizada para escribir en /content. Incluye privilegios de colaborador y de internauta.</p> <p>Se puede utilizar como administrador web, ya que tiene acceso a todo el directorio /content.</p> <p>No es un usuario integrado, sino otro usuario de demostración de geometrixx</p> </td>
   <td><p>Adobe recomienda que la cuenta se elimine por completo o que la contraseña cambie de la predeterminada.</p> <p>Preferiblemente tras la instalación, aunque se puede hacer después.</p> </td>
  </tr>
  <tr>
   <td>administradores</td>
   <td>Agrupar</td>
   <td><p>Grupo que otorga derechos de administrador a todos sus miembros. Solo el administrador puede editar este grupo.</p> <p>Tiene derechos de acceso completos.</p> </td>
   <td>Si establece un nodo 'deny-all' en un nodo, los administradores solo tendrán acceso si está habilitado de nuevo para ese grupo.</td>
  </tr>
  <tr>
   <td>content-authors</td>
   <td>Agrupar</td>
   <td><p>Grupo responsable de la edición de contenido. Requiere permisos de lectura, modificación, creación y eliminación.</p> </td>
   <td>Puede crear sus propios grupos de creación de contenido con derechos de acceso específicos del proyecto, siempre que agregue permisos de lectura, modificación, creación y eliminación.</td>
  </tr>
  <tr>
   <td>colaborador</td>
   <td>Agrupar</td>
   <td><p>Privilegios básicos que permiten al usuario escribir contenido (solo en funcionalidad).</p> <p>No asigna ningún privilegio al directorio /content: estos deben asignarse específicamente a grupos o usuarios individuales.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>dam-users</td>
   <td>Agrupar</td>
   <td>Grupo de referencia predeterminado para un usuario típico de AEM Assets. Los miembros de este grupo tienen los privilegios adecuados para permitir la carga y el uso compartido de recursos y colecciones.</td>
   <td> </td>
  </tr>
  <tr>
   <td>every</td>
   <td>Agrupar</td>
   <td><p>Todos los usuarios de AEM son miembros del grupo todos, aunque es posible que no vea el grupo o la relación de pertenencia en todas las herramientas.</p> <p>Este grupo puede considerarse como los derechos predeterminados, ya que se puede utilizar para aplicar permisos para todos, incluso para los usuarios que se crearán en el futuro.</p> </td>
   <td><p>No modifique ni elimine este grupo.</p> <p>Modificar esta cuenta tiene implicaciones de seguridad adicionales.</p> </td>
  </tr>
  <tr>
   <td>administradores de etiquetas</td>
   <td>Agrupar</td>
   <td>Grupo al que se permite editar etiquetas.</td>
   <td> </td>
  </tr>
  <tr>
   <td>usuarios administradores</td>
   <td>Agrupar</td>
   <td>Autoriza la administración de usuarios, es decir, el derecho a crear usuarios y grupos.</td>
   <td> </td>
  </tr>
  <tr>
   <td>workflow-editors</td>
   <td>Agrupar</td>
   <td>Grupo que puede crear y modificar modelos de flujo de trabajo.</td>
   <td> </td>
  </tr>
  <tr>
   <td>flujo de trabajo-usuarios</td>
   <td>Agrupar</td>
   <td><p>Un usuario que participa en un flujo de trabajo debe ser miembro del grupo de usuarios del flujo de trabajo. Esto le da pleno acceso a: /etc/workflow/instances para que pueda actualizar la instancia del flujo de trabajo.</p> <p>El grupo se incluye en la instalación estándar, pero debe agregar manualmente los usuarios al grupo.</p> </td>
  </tr>
 </tbody>
</table>

## Permisos en AEM {#permissions-in-aem}

AEM utiliza ACL para determinar qué acciones puede realizar un usuario o grupo y dónde puede realizar esas acciones.

### Permisos y ACL {#permissions-and-acls}

Los permisos definen quién puede realizar qué acciones en un recurso. Los permisos son el resultado de evaluaciones de [control de acceso](#access-control-lists-and-how-they-are-evaluated).

Puede cambiar los permisos otorgados/denegados a un usuario determinado seleccionando o borrando las casillas de verificación de las acciones individuales de AEM [a1/>. ](security.md#actions) Una marca de verificación indica que se permite una acción. Ninguna marca de verificación indica que se ha denegado una acción.

El lugar donde se encuentra la marca de verificación en la cuadrícula también indica qué permisos tienen los usuarios en qué ubicaciones dentro de AEM (es decir, qué rutas).

### Acciones {#actions}

Las acciones se pueden realizar en una página (recurso). Para cada página de la jerarquía, puede especificar qué acción puede realizar el usuario en esa página. [](#permissions-and-acls) Permiso para permitir o denegar una acción.

<table>
 <tbody>
  <tr>
   <td><strong>Acción </strong></td>
   <td><strong>Descripción </strong></td>
  </tr>
  <tr>
   <td>Lectura</td>
   <td>El usuario puede leer la página y las páginas secundarias.</td>
  </tr>
  <tr>
   <td>Modificar</td>
   <td><p>El usuario puede:</p>
    <ul>
     <li>modifique el contenido existente en la página y en cualquier página secundaria.</li>
     <li>cree nuevos párrafos en la página o en cualquier página secundaria.</li>
    </ul> <p>En el nivel JCR, los usuarios pueden modificar un recurso modificando sus propiedades, bloqueando, versionando, sin modificaciones, y tienen permisos de escritura completos en los nodos que definen un nodo secundario jcr:content, por ejemplo cq:Page, nt:file, cq:Asset.</p> </td>
  </tr>
  <tr>
   <td>Crear</td>
   <td><p>El usuario puede:</p>
    <ul>
     <li>cree una nueva página o página secundaria.</li>
    </ul> <p>Si se deniega <strong>modify</strong> , los subárboles debajo de jcr:content se excluyen específicamente porque la creación de jcr:content y sus nodos secundarios se consideran una modificación de página. Esto solo se aplica a los nodos que definen un nodo hijo jcr:content.</p> </td>
  </tr>
  <tr>
   <td>Eliminar</td>
   <td><p>El usuario puede:</p>
    <ul>
     <li>elimine los párrafos existentes de la página o de cualquier página secundaria.</li>
     <li>elimine una página o página secundaria.</li>
    </ul> <p>Si a <strong>modify</strong> se niega, cualquier subárbol debajo de jcr:content se excluye específicamente al eliminar jcr:content y sus nodos secundarios se consideran una modificación de página. Esto solo se aplica a los nodos que definen un nodo hijo jcr:content.</p> </td>
  </tr>
  <tr>
   <td>Leer ACL</td>
   <td>El usuario puede leer la lista de control de acceso de la página o de las páginas secundarias.</td>
  </tr>
  <tr>
   <td>Editar ACL</td>
   <td>El usuario puede modificar la lista de control de acceso de la página o cualquier página secundaria.</td>
  </tr>
  <tr>
   <td>Replicar</td>
   <td>El usuario puede replicar contenido en otro entorno (por ejemplo, el entorno de publicación). El privilegio también se aplica a cualquier página secundaria.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM genera automáticamente grupos de usuarios para la asignación de funciones (Propietario, Editor, Visor) en [Colecciones](/help/assets/manage-collections.md). Sin embargo, la adición manual de ACL para estos grupos puede introducir vulnerabilidades de seguridad dentro de AEM. Adobe recomienda que evite añadir ACL manualmente.

### Listas de control de acceso y cómo se evalúan {#access-control-lists-and-how-they-are-evaluated}

AEM WCM utiliza Listas de control de acceso (ACL) para organizar los permisos que se aplican a las distintas páginas.

Las listas de control de acceso están formadas por permisos individuales y se utilizan para determinar el orden en que se aplican realmente estos permisos. La lista se forma según la jerarquía de las páginas consideradas. A continuación, esta lista se analiza de abajo hacia arriba hasta encontrar el primer permiso apropiado para aplicar a una página.

>[!NOTE]
>
>Hay ACL que se incluyen en los ejemplos. Se recomienda que revise y determine qué es lo apropiado para sus aplicaciones. Para revisar las ACL incluidas, vaya a **CRXDE **y seleccione la pestaña **Control de acceso** para los siguientes nodos:
>
>`/etc/cloudservices/facebookconnect/geometrixx-outdoorsfacebookapp`: Permite a todos leer el acceso.
>`/etc/cloudservices/twitterconnect/geometrixx-outdoors-twitter-app`: Permite a todos leer el acceso.
>`/home/users/geometrixx-outdoors`: Permite que todos lean acceso para `*/profile*` y
>`*/social/relationships/following/*`.
>
>La aplicación personalizada puede establecer el acceso para otras relaciones, como `*/social/relationships/friend/*` o `*/social/relationships/pending-following/*`.
>
>Al crear ACL específicas para comunidades, los miembros que se unan a esas comunidades pueden recibir permisos adicionales. Por ejemplo, este podría ser el caso cuando los usuarios se unen a las comunidades en `/content/geometrixx-outdoors/en/community/hiking` o `/content/geometrixx-outdoors/en/community/winter-sports`.

### Estados de permisos {#permission-states}

>[!NOTE]
>
>Para usuarios de CQ5.3:
>
>A diferencia de las versiones anteriores de CQ, **create** y **delete** ya no deben concederse si un usuario solo necesita modificar páginas. En su lugar, conceda la acción **modify** solo si desea que los usuarios puedan crear, modificar o eliminar componentes en páginas existentes.
>
>Por motivos de compatibilidad con versiones anteriores, las pruebas de acciones no tienen en cuenta el tratamiento especial de los nodos que definen **jcr:content**.

| **Acción** | **Descripción** |
|---|---|
| Permitir (marca de verificación) | AEM WCM permite al usuario realizar la acción en esta página o en cualquier página secundaria. |
| Denegar (sin marca de verificación) | AEM WCM no permite al usuario realizar la acción en esta página ni en ninguna página secundaria. |

Los permisos también se aplican a cualquier página secundaria.

Si un permiso no se hereda del nodo principal pero tiene al menos una entrada local para él, se añaden los siguientes símbolos a la casilla de verificación. Una entrada local es una que se crea en la interfaz CRX 2.2 (actualmente, las ACL comodín solo se pueden crear en CRX).

Para una acción en una ruta determinada:

<table>
 <tbody>
  <tr>
   <td>* (asterisco)</td>
   <td>Hay al menos una entrada local (efectiva o ineficaz). Estos ACL comodín se definen en CRX.</td>
  </tr>
  <tr>
   <td>! (signo de exclamación)</td>
   <td>Hay al menos una entrada que actualmente no tiene ningún efecto.</td>
  </tr>
 </tbody>
</table>

Cuando pasa el ratón por encima del asterisco o del signo de exclamación, la información sobre herramientas proporciona más detalles sobre las entradas declaradas. La información sobre herramientas se divide en dos partes:

<table>
 <tbody>
  <tr>
   <td>Parte superior</td>
   <td><p>Muestra las entradas efectivas.</p> </td>
  </tr>
  <tr>
   <td>Parte inferior</td>
   <td>Enumera las entradas no efectivas que pueden tener un efecto en otro lugar del árbol (tal como indica un atributo especial presente con el ACE correspondiente limitando el alcance de la entrada). Alternativamente, se trata de una entrada cuyo efecto se ha revocado por otra entrada definida en la ruta dada o en un nodo antecesor.</td>
  </tr>
 </tbody>
</table>

![chlimage_1-112](assets/chlimage_1-112.png)

>[!NOTE]
>
>Si no se definen permisos para una página, se deniegan todas las acciones.

Las siguientes son recomendaciones sobre la administración de listas de control de acceso:

* No asigne permisos directamente a los usuarios. Asignarlos solo a grupos.

   Esto simplificará el mantenimiento, ya que el número de grupos es mucho menor que el número de usuarios y también es menos volátil.

* Si desea que un grupo o usuario solo pueda modificar páginas, no les conceda derechos de creación o denegación. Conceda únicamente derechos de modificación y lectura.
* Utilice Denegar con moderación. En la medida de lo posible, utilice solamente Permitir.

   El uso de denegar puede producir efectos inesperados si los permisos se aplican en un orden diferente al esperado. Si un usuario es miembro de más de un grupo, las instrucciones Denegar de un grupo pueden cancelar la instrucción Permitir de otro grupo o viceversa. Es difícil mantener una visión general cuando esto sucede y puede conducir fácilmente a resultados imprevistos, mientras que permitir asignaciones no causa tales conflictos.

   Adobe recomienda trabajar con Permitir en lugar de Denegar para ver [Prácticas recomendadas](#best-practices).

Antes de modificar cualquiera de los permisos, asegúrese de comprender cómo funcionan y están interrelacionados. Consulte la documentación de CRX para ilustrar cómo AEM WCM [evalúa los derechos de acceso](/help/sites-administering/user-group-ac-admin.md#how-access-rights-are-evaluated) y ejemplos de configuración de listas de control de acceso.

### Permisos    {#permissions}

Los permisos otorgan a los usuarios y grupos acceso a AEM funcionalidad en AEM páginas.

Los permisos se exploran por ruta expandiendo o contrayendo los nodos y puede rastrear la herencia de permisos hasta el nodo raíz.

Para permitir o denegar permisos, seleccione o desactive las casillas de verificación correspondientes.

![cqsecuritypermission stab](assets/cqsecuritypermissionstab.png)

### Visualización de información detallada de permisos {#viewing-detailed-permission-information}

Junto con la vista de cuadrícula, AEM proporciona una vista detallada de los permisos para un usuario o grupo seleccionado en una ruta determinada. La vista de detalles proporciona información adicional.

Además de ver información, también puede incluir o excluir al usuario o grupo actual de un grupo. Consulte [Agregar usuarios o grupos al agregar permisos](#adding-users-or-groups-while-adding-permissions). Los cambios realizados aquí se reflejan inmediatamente en la parte superior de la vista detallada.

Para acceder a la vista de detalles, en la pestaña **Permisos**, haga clic en **Detalles** para cualquier grupo/usuario y ruta seleccionados.

![detalles del permiso](assets/permissiondetails.png)

Los detalles se dividen en dos partes:

<table>
 <tbody>
  <tr>
   <td>Parte superior</td>
   <td><p>Repite la información que se ve en la cuadrícula del árbol. Para cada acción, un icono muestra si la acción está permitida o denegada:</p>
    <ul>
     <li>ningún icono = ninguna entrada declarada</li>
     <li>(visto) = acción declarada (permitir)</li>
     <li>(-) = acción declarada (denegar)</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Parte inferior</td>
   <td><p>Muestra la cuadrícula de usuarios y grupos que hace lo siguiente:</p>
    <ul>
     <li>Declara una entrada para la ruta dada Y</li>
     <li>¿El OR autorizado dado es un grupo?</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Suplantar otro usuario {#impersonating-another-user}

Con la [Funcionalidad de suplantar](/help/sites-authoring/user-properties.md#user-settings) un usuario puede trabajar en nombre de otro usuario.

Esto significa que una cuenta de usuario puede especificar otras cuentas que pueden operar con su cuenta. En otras palabras, si el usuario B puede suplantar al usuario A, el usuario B puede realizar acciones utilizando los detalles completos de la cuenta del usuario A.

Esto permite que las cuentas del imitador completen tareas como si estuvieran utilizando la cuenta que están suplantando; por ejemplo, durante una ausencia o para compartir una carga excesiva a corto plazo.

>[!NOTE]
>
>Para que la suplantación funcione para usuarios no administradores, el suplantador (en el caso anterior, user-B) debe tener permisos READ en la ruta `/home/users`.
>
>Para obtener más información sobre cómo lograr esto, consulte [Permisos en AEM](/help/sites-administering/security.md#permissions-in-aem).

>[!CAUTION]
>
>Si una cuenta se hace pasar por otra es muy difícil de ver. Se realiza una entrada en el registro de auditoría cuando la suplantación comienza y finaliza, pero los demás archivos de registro (como el registro de acceso) no contienen información sobre el hecho de que se ha producido una suplantación en los eventos. Por lo tanto, si el usuario B está suplantando al usuario A, todos los eventos parecerán como si fueran realizados personalmente por el usuario A.

>[!CAUTION]
>
>El bloqueo de páginas se puede realizar al suplantar a un usuario. Sin embargo, una página bloqueada de este modo solo se puede desbloquear como el usuario que ha suplantado a otro usuario o un usuario con privilegios de administrador.
>
>Las páginas no se pueden bloquear al suplantar al usuario que ha bloqueado la página.

### Prácticas recomendadas    {#best-practices}

A continuación se describen las prácticas recomendadas al trabajar con permisos y privilegios:

| Regla | Motivo |
|--- |--- |
| *Usar grupos* | Evite asignar derechos de acceso usuario por usuario. Esto se debe a varios motivos:<ul><li>Tiene muchos más usuarios que grupos, por lo que los grupos simplifican la estructura.</li><li>Los grupos ayudan a proporcionar información general sobre todas las cuentas.</li> <li>La herencia es más sencilla con los grupos.</li><li>Los usuarios van y vienen. Los grupos son de largo plazo.</li></ul> |
| *Ser positivo* | Utilice siempre las instrucciones Allow para especificar los derechos del grupo (siempre que sea posible). Evite utilizar una instrucción Deny. Los grupos se evalúan en orden y el orden se puede definir de forma diferente por usuario. En otras palabras: Puede que tenga poco control sobre el orden en que se implementan y evalúan las instrucciones. Si solo utiliza instrucciones Allow, el orden no importa. |
| *Manténgalo simple* | Invertir un poco de tiempo y pensamiento al configurar una nueva instalación será bien pagado. La aplicación de una estructura clara simplificará el mantenimiento y la administración en curso, lo que garantiza que tanto sus colegas actuales como los futuros sucesores puedan comprender fácilmente qué se está implementando. |
| *Probar* | Utilice una instalación de prueba para practicar y asegurarse de que comprende las relaciones entre los distintos usuarios y grupos. |
| *Usuarios/grupos predeterminados* | Actualice siempre los usuarios y grupos predeterminados inmediatamente después de la instalación para ayudar a evitar problemas de seguridad. |

## Administración de usuarios y grupos {#managing-users-and-groups}

Los usuarios incluyen personas que utilizan el sistema y sistemas extranjeros que realizan solicitudes al sistema.

Un grupo es un conjunto de usuarios.

Ambas se pueden configurar utilizando la funcionalidad Administración de usuarios de la Consola de seguridad.

### Acceso a la administración de usuarios con la consola de seguridad {#accessing-user-administration-with-the-security-console}

Puede acceder a todos los usuarios, grupos y permisos asociados mediante la consola Seguridad. Todos los procedimientos descritos en esta sección se realizan en esta ventana.

Para acceder AEM seguridad de WCM, realice una de las siguientes acciones:

* En la pantalla de bienvenida o en varias ubicaciones de AEM, haga clic en el icono de seguridad:

![](do-not-localize/wcmtoolbar.png)

* Vaya directamente a `https://<server>:<port>/useradmin`. Asegúrese de iniciar sesión en AEM como administrador.

Se muestra la siguiente ventana:

![cqsecuritypage](assets/cqsecuritypage.png)

El árbol de la izquierda enumera todos los usuarios y grupos que hay actualmente en el sistema. Puede seleccionar las columnas que desea mostrar, ordenar el contenido de las columnas e incluso cambiar el orden en que se muestran arrastrando el encabezado de la columna a una nueva posición.

![cqsecuritycolumncontext](assets/cqsecuritycolumncontext.png)

Las pestañas proporcionan acceso a varias configuraciones:

<!-- ??? in table below. -->

| Ficha | Descripción |
|--- |--- |
| Cuadro de filtro | Mecanismo para filtrar los usuarios y/o grupos enumerados. Consulte [Filtrado de usuarios y grupos](#filtering-users-and-groups). |
| Ocultar usuarios | Un conmutador que ocultará a todos los usuarios de la lista, dejando solo grupos. Consulte [Ocultar usuarios y grupos](#hiding-users-and-groups). |
| Ocultar grupos | Un conmutador que ocultará todos los grupos enumerados, dejando solo usuarios. Consulte [Ocultar usuarios y grupos](#hiding-users-and-groups). |
| Editar | Un menú que le permite crear y eliminar, así como activar y desactivar usuarios o grupos. Consulte [Creación de usuarios y grupos](#creating-users-and-groups) y [Eliminación de usuarios y grupos](#deleting-users-and-groups). |
| Propiedades | Muestra información sobre el usuario o grupo que puede incluir información de correo electrónico, una descripción e información de nombre. También le permite cambiar la contraseña de un usuario. Consulte [Creación de usuarios y grupos](#creating-users-and-groups), [Modificación de las propiedades de usuario y grupo](#modifying-user-and-group-properties) y [Cambio de una contraseña de usuario](#changing-a-user-password). |
| Grupos | Enumera todos los grupos a los que pertenece el usuario o grupo seleccionado. Puede asignar el usuario o los grupos seleccionados a grupos adicionales o eliminarlos de los grupos. Consulte [Grupos](#adding-users-or-groups-to-a-group). |
| Miembros | Disponible solo para grupos. Enumera los miembros de un grupo en particular. Consulte [Miembros](#members-adding-users-or-groups-to-a-group). |
| Permisos | Puede asignar permisos a un usuario o grupo. Permite controlar lo siguiente:<ul><li>Permisos relacionados con páginas o nodos particulares. Consulte [Configuración de permisos](#setting-permissions). </li><li>Permisos relacionados con la creación y eliminación de páginas y modificación de la jerarquía. ?? permite [asignar privilegios](#settingprivileges), como la modificación de la jerarquía, que permite crear y eliminar páginas,</li><li>Permisos relacionados con [privilegios de replicación](#setting-replication-privileges) (normalmente de autor a publicación) según una ruta.</li></ul> |
| Suplantadores | Permite que otro usuario suplante la cuenta. Resulta útil cuando necesita que un usuario actúe en nombre de otro usuario. Consulte [Suplantar usuarios](#impersonating-another-user). |
| Preferencias | Establece [preferencias para el grupo o usuario](#setting-user-and-group-preferences). Por ejemplo, las preferencias de idioma. |

### Filtrado de usuarios y grupos {#filtering-users-and-groups}

Puede filtrar la lista introduciendo una expresión de filtro que oculte todos los usuarios y grupos que no coincidan con la expresión. También puede ocultar usuarios y grupos utilizando los botones [Ocultar usuario y Ocultar grupo](#hiding-users-and-groups).

Para filtrar usuarios o grupos:

1. En la lista del árbol de la izquierda, escriba la expresión del filtro en el espacio proporcionado. Por ejemplo, si se introduce **admin**, se muestran todos los usuarios y grupos que contienen esta cadena.
1. Haga clic en la lupa para filtrar la lista.

   ![cqsecurityfilter](assets/cqsecurityfilter.png)

1. Haga clic en **x** cuando desee eliminar todos los filtros.

### Ocultar usuarios y grupos {#hiding-users-and-groups}

Ocultar usuarios o grupos es otra manera de filtrar la lista de todos los usuarios y grupos de un sistema. Existen dos mecanismos de alternancia. Al hacer clic en Ocultar usuario se ocultan todos los usuarios de la vista y al hacer clic en Ocultar grupos se ocultan todos los grupos de la vista (no se pueden ocultar tanto a los usuarios como a los grupos al mismo tiempo). Para filtrar la lista utilizando una expresión de filtro, consulte [Filtrado de usuarios y grupos](#filtering-users-and-groups).

Para ocultar usuarios y grupos:

1. En la consola **Seguridad**, haga clic en **Ocultar usuarios** u **Ocultar grupos**. El botón seleccionado aparece resaltado.

   ![cqsecurityhideusers](assets/cqsecurityhideusers.png)

1. Para que vuelvan a aparecer usuarios o grupos, haga clic de nuevo en el botón correspondiente.

### Creación de usuarios y grupos {#creating-users-and-groups}

Para crear un nuevo usuario o grupo:

1. En la lista del árbol de la consola **Seguridad**, haga clic en **Editar** y, a continuación, en **Crear usuario** o en **Crear grupo**.

   ![cqseruityeditcontextmenu](assets/cqseruityeditcontextmenu.png)

1. Introduzca los detalles necesarios, en función de si está creando un usuario o un grupo.

   * Si selecciona **Crear usuario,** debe introducir el ID de inicio de sesión, el nombre y los apellidos, la dirección de correo electrónico y una contraseña. De forma predeterminada, AEM crea una ruta basada en la primera letra del apellido, pero puede seleccionar otra ruta.

   ![createuserdialog](assets/createuserdialog.png)

   * Si selecciona **Crear grupo**, debe introducir un ID de grupo y una descripción opcional.

   ![creategroupdialog](assets/creategroupdialog.png)

1. Haga clic en **Crear**. El usuario o grupo que ha creado aparece en la lista de árbol.

### Eliminación de usuarios y grupos {#deleting-users-and-groups}

Para eliminar un usuario o grupo:

1. En la consola **Security**, seleccione el usuario o grupo que desee eliminar. Si desea eliminar varios elementos, pulse Mayús+clic o Ctrl+clic para seleccionarlos.
1. Haga clic en **Editar,** y seleccione Eliminar. AEM WCM pregunta si desea eliminar el usuario o grupo.
1. Haga clic en **OK** para confirmar o en Cancelar para cancelar la acción.

### Modificación de las propiedades de usuario y grupo {#modifying-user-and-group-properties}

Para modificar las propiedades de usuario y grupo:

1. En la consola **Security**, haga doble clic en el nombre de usuario o grupo que desee modificar.

1. Haga clic en la pestaña **Properties**, realice los cambios necesarios y haga clic en **Save**.

   ![cqsecurityuserprops](assets/cqsecurityuserprops.png)

>[!NOTE]
>
>La ruta del usuario se muestra en la parte inferior de las propiedades del usuario. No se puede modificar.

### Cambio de una contraseña de usuario {#changing-a-user-password}

Utilice el siguiente procedimiento para modificar la contraseña de un usuario.

>[!NOTE]
>
>No puede usar la consola de seguridad para cambiar la contraseña de administrador. Para cambiar la contraseña de la cuenta de administrador, utilice la [Consola de usuarios](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user) que proporciona Granite Operations.
>
>Si utiliza AEM Forms en JEE, no utilice las instrucciones siguientes para cambiar la contraseña, sino AEM Forms en la consola de administración de JEE (/adminui) para cambiar la contraseña.

1. En la consola **Security**, haga doble clic en el nombre de usuario para el que desea cambiar la contraseña.
1. Haga clic en la pestaña **Properties** (si no está activa).
1. Haga clic en **Establecer contraseña**. Se abre la ventana Configurar contraseña, donde puede cambiar la contraseña.

   ![cqsecurityuserpassword](assets/cqsecurityuserpassword.png)

1. Escriba la nueva contraseña dos veces; ya que no se muestran en texto claro esto es para confirmación: si no coinciden, el sistema muestra un error.
1. Haga clic en **Set** para activar la nueva contraseña para la cuenta.

### Agregar usuarios o grupos a un grupo {#adding-users-or-groups-to-a-group}

AEM ofrece tres formas diferentes de agregar usuarios o grupos a un grupo existente:

* Cuando esté en el grupo, puede agregar miembros (usuarios o grupos).
* Cuando esté en el grupo, puede agregar miembros a los grupos.
* Cuando esté trabajando en Permisos, puede agregar miembros a grupos.

### Grupos: Agregar usuarios o grupos a un grupo {#groups-adding-users-or-groups-to-a-group}

La pestaña **Grupos** muestra a qué grupos pertenece la cuenta actual. Puede usarlo para agregar la cuenta seleccionada a un grupo:

1. Haga doble clic en el nombre de la cuenta (usuario o grupo) que desea asignar a un grupo.
1. Haga clic en la pestaña **Grupos**. Verá una lista de grupos a los que ya pertenece la cuenta.
1. En la lista de árbol, haga clic en el nombre del grupo al que desee agregar la cuenta y arrástrelo al panel **Grupos**. (Si desea agregar varios usuarios, pulse Mayús+clic o Ctrl+clic en esos nombres y arrástrelos).

   ![cqsecurityaddusertogroup](assets/cqsecurityaddusertogroup.png)

1. Haga clic en **Guardar** para guardar los cambios.

### Miembros: Agregar usuarios o grupos a un grupo {#members-adding-users-or-groups-to-a-group}

La ficha **Miembros** solo funciona para grupos y muestra los usuarios y grupos que pertenecen al grupo actual. Puede utilizarla para agregar cuentas a un grupo:

1. Haga doble clic en el nombre del grupo al que desee agregar miembros.
1. Haga clic en la pestaña **Members**. Verá una lista de miembros que ya pertenecen a este grupo.
1. En la lista de árbol, haga clic en el nombre del miembro que desea agregar al grupo y arrástrelo al panel **Miembros**. (Si desea agregar varios usuarios, pulse Mayús+clic o Ctrl+clic en esos nombres y arrástrelos).

   ![cqsecurityadduserasmember](assets/cqsecurityadduserasmember.png)

1. Haga clic en **Guardar** para guardar los cambios.

### Agregar usuarios o grupos al agregar permisos {#adding-users-or-groups-while-adding-permissions}

Para agregar miembros a un grupo en una ruta determinada:

1. Haga doble clic en el nombre del grupo o usuario al que desee agregar usuarios.

1. Haga clic en la pestaña **Permissions**.

1. Desplácese a la ruta a la que desee agregar permisos y haga clic en **Detalles**. La parte inferior de la ventana de detalles proporciona información sobre quién tiene permisos para esa página.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. Seleccione la casilla de verificación de la columna **Member** para los miembros que desea que tengan permisos para esa ruta. Desactive la casilla de verificación del miembro para el que desea eliminar los permisos. Aparece un triángulo rojo en la celda a la que ha realizado cambios.
1. Haga clic en **Aceptar** para guardar los cambios.

### Eliminación de usuarios o grupos de grupos {#removing-users-or-groups-from-groups}

AEM ofrece tres formas diferentes de eliminar usuarios o grupos de un grupo:

* Cuando se encuentra en el perfil de grupo, puede eliminar miembros (usuarios o grupos).
* Cuando esté en el perfil de miembro, puede quitar miembros de los grupos.
* Cuando esté trabajando en Permisos, puede quitar miembros de los grupos.

### Grupos - Eliminar usuarios o grupos de grupos {#groups-removing-users-or-groups-from-groups}

Para quitar una cuenta de usuario o grupo de un grupo:

1. Haga doble clic en el nombre del grupo o cuenta de usuario que desee eliminar de un grupo.
1. Haga clic en la pestaña **Grupos**. Verá a qué grupos pertenece la cuenta seleccionada.
1. En el panel **Grupos**, haga clic en el nombre del usuario o grupo que desee quitar del grupo y haga clic en **Quitar**. (Si desea eliminar varias cuentas, pulse Mayús+clic o Ctrl+clic en esos nombres y haga clic en **Quitar**).

   ![cqsecurityremoveuserfromgrp](assets/cqsecurityremoveuserfromgrp.png)

1. Haga clic en **Guardar** para guardar los cambios.

### Miembros: eliminación de usuarios o grupos de grupos {#members-removing-users-or-groups-from-groups}

Para quitar cuentas de un grupo:

1. Haga doble clic en el nombre del grupo del que desea quitar miembros.
1. Haga clic en la pestaña **Members**. Verá una lista de miembros que ya pertenecen a este grupo.
1. En el panel **Miembros**, haga clic en el nombre del miembro que desea quitar del grupo y haga clic en **Quitar**. (Si desea eliminar varios usuarios, pulse Mayús+clic o Ctrl+clic en esos nombres y haga clic en **Quitar**).

   ![cqsecurityremovemember](assets/cqsecurityremovemember.png)

1. Haga clic en **Guardar** para guardar los cambios.

### Eliminación de usuarios o grupos al agregar permisos {#removing-users-or-groups-while-adding-permissions}

Para eliminar miembros de un grupo en una ruta determinada:

1. Haga doble clic en el nombre del grupo o usuario del que desea eliminar a los usuarios.

1. Haga clic en la pestaña **Permissions**.

1. Desplácese a la ruta a la que desee eliminar los permisos y haga clic en **Detalles**. La parte inferior de la ventana de detalles proporciona información sobre quién tiene permisos para esa página.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. Seleccione la casilla de verificación de la columna **Member** para los miembros que desea que tengan permisos para esa ruta. Desactive la casilla de verificación del miembro para el que desea eliminar los permisos. Aparece un triángulo rojo en la celda a la que ha realizado cambios.
1. Haga clic en **Aceptar** para guardar los cambios.

### Sincronización de usuarios {#user-synchronization}

Cuando la implementación es un [conjunto de servidores de publicación](/help/sites-deploying/recommended-deploys.md#tarmk-farm), los usuarios y grupos deben sincronizarse entre todos los nodos de publicación.

Para obtener más información sobre la sincronización de usuarios y cómo habilitarla, consulte [Sincronización de usuarios](/help/sites-administering/sync.md).

## Administración de permisos {#managing-permissions}

>[!NOTE]
>
>Adobe ha introducido una nueva vista principal basada en la IU táctil para la administración de permisos. Para obtener más información sobre cómo utilizarla, consulte [esta página](/help/sites-administering/touch-ui-principal-view.md).

En esta sección se describe cómo establecer permisos, incluidos privilegios de replicación.

### Configuración de permisos {#setting-permissions}

Los permisos permiten a los usuarios realizar ciertas acciones en los recursos en determinadas rutas. También incluye la capacidad de crear o eliminar páginas.

Para agregar, modificar o eliminar permisos:

1. En la consola **Security**, haga doble clic en el nombre del usuario o grupo para el que desee establecer permisos o [busque nodos](#searching-for-nodes).

1. Haga clic en la pestaña **Permissions**.

   ![cquserpermissions](assets/cquserpermissions.png)

1. En la cuadrícula del árbol, active una casilla de verificación para permitir que el usuario o grupo seleccionado realice una acción o desactive una casilla de verificación para denegar al usuario o grupo seleccionado la realización de una acción. Para obtener más información, haga clic en **Detalles**.

1. Cuando termine, haga clic en **Guardar**.

### Configuración de Privilegios de Replicación {#setting-replication-privileges}

El privilegio de replicación es el derecho para publicar contenido y se puede establecer para grupos y usuarios.

>[!NOTE]
>
>* Los derechos de replicación aplicados a un grupo se aplican a todos los usuarios de dicho grupo.
>* Los privilegios de replicación de un usuario sustituyen a los privilegios de replicación de un grupo.
>* Los derechos Allow replication tienen una prioridad mayor que los derechos Deny replication . Consulte [Permisos en AEM](#permissions-in-aem) para obtener más información.

>



Para establecer privilegios de replicación:

1. Seleccione el usuario o grupo de la lista, haga doble clic para abrirlo y haga clic en **Permisos**.
1. En la cuadrícula, vaya a la ruta en la que desea que el usuario tenga privilegios de replicación o [busque nodos.](#searching-for-nodes)

1. En la columna **Replicate** en la ruta seleccionada, active una casilla de verificación para agregar el privilegio de replicación para ese usuario o grupo, o desactive la casilla de verificación para eliminar el privilegio de replicación. AEM muestra un triángulo rojo en cualquier parte donde haya realizado cambios que aún no se hayan guardado.

   ![cquserreplicatepermissions](assets/cquserreplicatepermissions.png)

1. Haga clic en **Guardar** para guardar los cambios.

### Buscando nodos {#searching-for-nodes}

Al añadir o eliminar permisos, puede examinar o buscar el nodo .

Existen dos tipos diferentes de búsqueda de rutas:

* Búsqueda de rutas : Si la cadena de búsqueda comienza con &quot;/&quot;, la búsqueda buscará los subnodos directos de la ruta dada:

![cqsecuritypathsearch](assets/cqsecuritypathsearch.png)

En el cuadro de búsqueda, puede hacer lo siguiente:

| Acción | Qué hace |
|--- |--- |
| Tecla de flecha derecha | Selecciona un subnodo en el resultado de la búsqueda |
| Tecla de flecha abajo | Inicia la búsqueda de nuevo. |
| Tecla Enter (Return) | Selecciona un subnodo y lo carga en la cuadrícula de árbol |

* Búsqueda de texto completo : si la cadena de búsqueda no comienza con &quot;/&quot;, se ejecuta una búsqueda de texto completo en todos los nodos de la ruta &quot;/content&quot;.

![cqsecurityfulltextsearch](assets/cqsecurityfulltextsearch.png)

Para realizar una búsqueda en rutas o texto completo:

1. En la consola de seguridad, seleccione un usuario o grupo y, a continuación, haga clic en la pestaña **Permisos**.

1. En el cuadro Buscar, escriba un término para buscar.

### Suplantar usuarios {#impersonating-users}

Puede especificar uno o más usuarios a los que se permite suplantar al usuario actual. Esto significa que pueden cambiar la configuración de su cuenta a la del usuario actual y actuar en nombre de este usuario.

Utilice esta función con precaución ya que puede permitir a los usuarios realizar acciones que su propio usuario no puede realizar. Al suplantar a un usuario, se notifica a los usuarios de que no han iniciado sesión por sí mismos.

Hay varios escenarios en los que puede querer utilizar esta funcionalidad, entre ellos:

* Si estás fuera de la oficina, puedes dejar que otra persona te imite mientras estás fuera. Al utilizar esta función, puede asegurarse de que alguien tenga sus derechos de acceso y no necesita modificar un perfil de usuario ni proporcionar su contraseña.
* Puede utilizarlo para la depuración. Por ejemplo, para ver cómo el sitio web busca un usuario con derechos de acceso restringidos. Además, si un usuario se queja de problemas técnicos, puede suplantar a ese usuario para diagnosticar y solucionar el problema.

Para suplantar un usuario existente:

1. En la lista de árbol, seleccione el nombre de la persona a la que desea asignar otros usuarios para que se suplanten. Haga doble clic para abrir.
1. Haga clic en la pestaña **Impersonators**.
1. Haga clic en el usuario que desea que pueda suplantar al usuario seleccionado. Arrastre el usuario (que suplantará) de la lista al panel Suplantar . El nombre aparece en la lista.

   ![chlimage_1-114](assets/chlimage_1-115.png)

1. Haga clic en **Guardar**.

### Configuración de las preferencias de usuario y grupo {#setting-user-and-group-preferences}

Para establecer las preferencias de usuario y grupo, incluidas las preferencias de idioma, administración de ventanas y barra de herramientas:

1. Seleccione el usuario o grupo cuyas preferencias desee cambiar en el árbol de la izquierda. Para seleccionar varios usuarios o grupos, pulse Ctrl+clic o Mayús+clic en las selecciones.
1. Haga clic en la pestaña **Preferences**.

   ![cqsecurityPreferences](assets/cqsecuritypreferences.png)

1. Realice los cambios necesarios en las preferencias del grupo o usuario y haga clic en **Guardar** cuando termine.

### Configurar usuarios o administradores para que tengan el privilegio de administrar otros usuarios {#setting-users-or-administrators-to-have-the-privilege-to-manage-other-users}

Para configurar a los usuarios o administradores para que tengan privilegios para eliminar, activar o desactivar otros usuarios:

1. Agregue al usuario al que desea otorgar privilegios para administrar otros usuarios al grupo de administradores y guarde los cambios.

   ![cqsecurityadmembertoadmin](assets/cqsecurityaddmembertoadmin.png)

1. En la pestaña **Permissions** del usuario, vaya a &quot;/&quot; y, en la columna Replicar, active la casilla de verificación para permitir la replicación en &quot;/&quot; y haga clic en **Guardar**.

   ![cqsecurityreplicatepermissions](assets/cqsecurityreplicatepermissions.png)

   El usuario seleccionado ahora tiene la capacidad de desactivar, activar, eliminar y crear usuarios.

### Ampliación de privilegios en un proyecto {#extending-privileges-on-a-project-level}

Si planea implementar privilegios específicos de la aplicación, la siguiente información describe lo que necesita saber para implementar un privilegio personalizado y cómo aplicarlo en todo CQ:

El privilegio de modificación de jerarquía está cubierto por una combinación de privilegios jcr. El privilegio de replicación se llama **crx:replicate** que se almacena/evalúa junto con otros privilegios en el repositorio jcr. Sin embargo, no se aplica a nivel jcr.

La definición y el registro de privilegios personalizados forman parte oficialmente de la [API de Jackrabbit](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/api/security/authorization/PrivilegeManager.html) a partir de la versión 2.4 (consulte también [JCR-2887](https://issues.apache.org/jira/browse/JCR-2887)). El uso adicional está cubierto por la Administración de control de acceso JCR, tal como se define en [JSR 283](https://jcp.org/en/jsr/detail?id=283) (sección 16). Además, la API de Jackrabbit define un par de extensiones.

El mecanismo de registro de privilegios se refleja en la interfaz de usuario en **Configuración del repositorio**.

El registro de nuevos privilegios (personalizados) está protegido por un privilegio integrado que debe otorgarse a nivel de repositorio (en JCR: pasando &#39;null&#39; como parámetro &#39;absPath&#39; en la api de ac mgt, consulte jsr 33 para obtener más información). De forma predeterminada, **admin** y todos los miembros de los administradores tienen ese privilegio concedido.

>[!NOTE]
>
>Aunque la implementación se encarga de validar y evaluar los privilegios personalizados, no puede aplicarlos a menos que se agreguen privilegios integrados.
