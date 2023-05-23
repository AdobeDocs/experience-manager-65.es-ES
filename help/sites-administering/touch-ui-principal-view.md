---
title: Vista principal para la administración de permisos
seo-title: Principal View for Permissions Management
description: Obtenga información acerca de la nueva interfaz de usuario táctil que facilita la administración de permisos.
seo-description: Learn about the new Touch UI interface that facilitates permissions management.
uuid: 16c5889a-60dd-4b66-bbc4-74fbdb5fc32f
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: db8665fa-353f-45c2-8e37-169d5c1df873
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 1%

---

# Vista principal para la administración de permisos{#principal-view-for-permissions-management}

## Información general {#overview}

AEM.5 presenta la Administración de permisos para usuarios y grupos. La funcionalidad principal sigue siendo la misma que la IU clásica, pero es más fácil de usar y eficiente.

## Usos {#how-to-use}

### Acceso a la IU {#accessing-the-ui}

Se accede a la nueva administración de permisos basada en la interfaz de usuario a través de la tarjeta Permisos en Seguridad, como se muestra a continuación:

![](assets/screen_shot_2019-03-17at63333pm.png)

La nueva vista facilita la visualización de todo el conjunto de privilegios y restricciones para un principal determinado en todas las rutas en las que se han concedido permisos explícitamente. Esto elimina la necesidad de ir a

CRXDE para administrar privilegios y restricciones avanzados. Se ha consolidado en la misma vista. La vista predeterminada es Grupo &quot;todos&quot;.

![](assets/unu-1.png)

Hay un filtro que permite al usuario seleccionar el tipo de entidades de seguridad que desea ver **Usuarios**, **Grupos**, o **Todo** y buscar cualquier principal **.**

![](assets/image2019-3-20_23-52-51.png)

### Visualización de permisos para una entidad principal {#viewing-permissions-for-a-principal}

El marco de la izquierda permite a los usuarios desplazarse hacia abajo para encontrar cualquier principal o buscar un grupo o un usuario en función del filtro seleccionado, como se muestra a continuación:

![](assets/doi-1.png)

Al hacer clic en el nombre, se muestran los permisos asignados a la derecha. El panel de permisos muestra la lista de entradas de control de acceso en rutas específicas junto con las restricciones configuradas.

![](assets/trei-1.png)

### Agregar una nueva entrada de control de acceso para una entidad principal {#adding-new-access-control-entry-for-a-principal}

Para agregar nuevos permisos, agregue una nueva Entrada de control de acceso haciendo clic en el botón Agregar ACE.

![](assets/patru.png)

Esto abre la ventana que se muestra a continuación. El siguiente paso es elegir una ruta en la que se deba configurar el permiso.

![](assets/cinci-1.png)

Aquí seleccionamos una ruta en la que queremos configurar un permiso para **dam-users**:

![](assets/sase-1.png)

Una vez seleccionada la ruta, el flujo de trabajo vuelve a esta pantalla, donde el usuario puede seleccionar uno o varios privilegios de las áreas de nombres disponibles (como `jcr`, `rep` o `crx`) como se muestra a continuación.

Los privilegios se pueden añadir buscando en el campo de texto y seleccionando a continuación en la lista.

>[!NOTE]
>
>Para obtener una lista completa de privilegios y descripciones, consulte [esta página](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![](assets/image2019-3-21_0-5-47.png) ![](assets/image2019-3-21_0-6-53.png)

Una vez seleccionada la lista de privilegios, el usuario puede elegir el Tipo de permiso : Denegar o Permitir, como se muestra a continuación.

![](assets/screen_shot_2019-03-17at63938pm.png) ![](assets/screen_shot_2019-03-17at63947pm.png)

### Uso de restricciones {#using-restrictions}

Además de la lista de privilegios y el Tipo de permiso en una ruta determinada, esta pantalla también permite agregar restricciones para el control de acceso de grano fino como se muestra a continuación:

![](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>Para obtener más información sobre el significado de cada restricción, consulte [Documentación de Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html).

Las restricciones se pueden añadir como se muestra a continuación seleccionando el tipo de restricción, introduciendo el valor y pulsando el botón **+** icono.

![](assets/sapte-1.png) ![](assets/opt-1.png)

La nueva ACE se refleja en la Lista de control de acceso como se muestra a continuación. Tenga en cuenta que `jcr:write` es un privilegio agregado que incluye `jcr:removeNode` que se añadió anteriormente, pero no se muestra a continuación como cubierto en `jcr:write`.

### Edición de ACE {#editing-aces}

Las entradas de control de acceso se pueden editar seleccionando un principal y eligiendo el elemento ACE que desea editar.

Por ejemplo, aquí podemos editar la siguiente entrada para **dam-users** haciendo clic en el icono de lápiz a la derecha:

![Añadir restricción](assets/image2019-3-21_0-35-39.png)

La pantalla de edición se muestra con las entradas de control de acceso configuradas preseleccionadas, que se pueden eliminar haciendo clic en el icono en forma de cruz junto a ellas o se pueden añadir nuevos privilegios para la ruta dada, como se muestra a continuación.

![Editar entrada](assets/noua-1.png)

Aquí se agrega el `addChildNodes` privilegio para **dam-users** en la ruta dada.

![](assets/image2019-3-21_0-45-35.png)

Los cambios se pueden guardar haciendo clic en el **Guardar** en la parte superior derecha, y los cambios se reflejarán en los nuevos permisos para **dam-users **como se muestra a continuación:

![](assets/zece-1.png)

### Eliminación de ACE {#deleting-aces}

Las entradas de control de acceso se pueden eliminar para eliminar todos los permisos otorgados a una entidad de seguridad en una ruta específica. El icono X situado junto a ACE puede utilizarse para eliminarlo, como se muestra a continuación:

![](assets/image2019-3-21_0-53-19.png) ![](assets/unspe.png)

### Combinaciones de privilegios de IU clásica {#classic-ui-privilege-combinations}

Tenga en cuenta que la nueva interfaz de usuario de permisos utiliza explícitamente el conjunto básico de privilegios en lugar de combinaciones predefinidas que no reflejaban realmente los privilegios subyacentes exactos que se concedieron.

Causó confusión sobre qué se está configurando exactamente. En la tabla siguiente se muestra la asignación entre las combinaciones de privilegios de la IU clásica a los privilegios reales que las constituyen:

<table>
 <tbody>
  <tr>
   <th>Combinaciones de privilegios de IU clásica</th>
   <th>Privilegio de IU de permisos</th>
  </tr>
  <tr>
   <td>Leer</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>Modificar</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>Crear</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>Eliminar</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>Leer ACL</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>Editar ACL</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>Replicar</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
