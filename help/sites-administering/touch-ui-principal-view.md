---
title: Vista principal para la administración de permisos
seo-title: Vista principal para la administración de permisos
description: Obtenga información sobre la nueva interfaz de usuario táctil que facilita la administración de permisos.
seo-description: Obtenga información sobre la nueva interfaz de usuario táctil que facilita la administración de permisos.
uuid: 16c5889a-60dd-4b66-bbc4-74fbdb5fc32f
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: db8665fa-353f-45c2-8e37-169d5c1df873
docset: aem65
translation-type: tm+mt
source-git-commit: a156e09e77951041dce017f2f78069bc050b6bdb

---


# Vista principal para la administración de permisos{#principal-view-for-permissions-management}

## Información general {#overview}

AEM 6.5 presenta la administración de permisos para usuarios y grupos. La funcionalidad principal sigue siendo la misma que la IU clásica, pero es más fácil de usar y eficaz.

## Usos {#how-to-use}

### Acceso a la interfaz de usuario {#accessing-the-ui}

Se accede a la nueva administración de permisos basada en la interfaz de usuario a través de la tarjeta Permisos en Seguridad, como se muestra a continuación:

![](assets/screen_shot_2019-03-17at63333pm.png)

La nueva vista facilita la visualización de todo el conjunto de privilegios y restricciones para una entidad de seguridad determinada en todas las rutas en las que se han concedido permisos explícitamente. Esto elimina la necesidad de ir a

CRXDE para administrar privilegios y restricciones avanzados. Se ha consolidado en la misma opinión. El valor predeterminado de la vista es &quot;todos&quot; en el grupo.

![](assets/unu-1.png)

Existe un filtro que permite al usuario seleccionar el tipo de entidades principales para ver **Usuarios**, **Grupos** o **Todos** y buscar cualquier entidad de seguridad **.**

![](assets/image2019-3-20_23-52-51.png)

### Visualización de permisos para una entidad de seguridad {#viewing-permissions-for-a-principal}

El marco de la izquierda permite a los usuarios desplazarse hacia abajo para encontrar cualquier principal o buscar un grupo o un usuario según el filtro seleccionado, como se muestra a continuación:

![](assets/doi-1.png)

Al hacer clic en el nombre se muestran los permisos asignados a la derecha. El panel Permisos muestra la lista de Entradas de control de acceso en rutas específicas junto con las restricciones configuradas.

![](assets/trei-1.png)

### Adición de una nueva entrada de control de acceso para una entidad de seguridad {#adding-new-access-control-entry-for-a-principal}

Para agregar nuevos permisos, agregue una nueva entrada de control de acceso haciendo clic en el botón Agregar ACE.

![](assets/patru.png)

Esto abre la ventana que se muestra a continuación. El siguiente paso es elegir una ruta en la que se debe configurar el permiso.

![](assets/cinci-1.png)

Aquí seleccionamos una ruta en la que queremos configurar un permiso para **los usuarios** de presas:

![](assets/sase-1.png)

Una vez seleccionada la ruta, el flujo de trabajo regresa a esta pantalla, donde el usuario puede seleccionar uno o varios de los privilegios de los espacios de nombres disponibles (como `jcr`, `rep` o `crx`) como se muestra a continuación.

Los privilegios se pueden agregar buscando utilizando el campo de texto y seleccionando una opción de la lista.

>[!NOTE]
>
>Para obtener una lista completa de privilegios y descripciones, consulte [esta página](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![](assets/image2019-3-21_0-5-47.png) ![](assets/image2019-3-21_0-6-53.png)

Una vez seleccionada la lista de privilegios, el usuario puede elegir el tipo de permiso : Denegar o Permitir, como se muestra a continuación.

![](assets/screen_shot_2019-03-17at63938pm.png) ![](assets/screen_shot_2019-03-17at63947pm.png)

### Uso de restricciones {#using-restrictions}

Además de la lista de privilegios y el tipo de permiso en una ruta determinada, esta pantalla también permite agregar restricciones para un control de acceso preciso, como se muestra a continuación:

![](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>Para obtener más información sobre el significado de cada restricción, consulte [esta página](/help/sites-administering/user-group-ac-admin.md#restrictions).

Las restricciones se pueden agregar como se muestra a continuación seleccionando el tipo de restricción, introduciendo el valor y pulsando el icono **+** . ![](assets/sapte-1.png) ![](assets/opt-1.png)

El nuevo ACE se refleja en la lista de control de acceso, como se muestra a continuación. Tenga en cuenta que `jcr:write` es un privilegio agregado que incluye `jcr:removeNode` que se agregó arriba, pero que no se muestra debajo como cubierto en `jcr:write`.

### Edición de ACE {#editing-aces}

Las entradas de control de acceso se pueden editar seleccionando una entidad de seguridad y eligiendo la ACE que desee editar.

Por ejemplo, aquí podemos editar la entrada siguiente para usuarios **de** presas haciendo clic en el icono de lápiz de la derecha:

![](assets/image2019-3-21_0-35-39.png)

La pantalla de edición se muestra con las ACE configuradas preseleccionadas, se pueden eliminar haciendo clic en el icono de cruz que hay junto a ellas o se pueden agregar nuevos privilegios para la ruta dada, como se muestra a continuación.

![](assets/noua-1.png)

Aquí estamos agregando el `addChildNodes` privilegio para los usuarios **de** presas en el camino dado.

![](assets/image2019-3-21_0-45-35.png)

Los cambios se pueden guardar haciendo clic en el botón **Guardar** en la parte superior derecha, y los cambios se reflejarán en los nuevos permisos para **usuarios de represa **como se muestra a continuación:

![](assets/zece-1.png)

### Eliminación de ACE {#deleting-aces}

Las entradas de control de acceso se pueden eliminar para eliminar todos los permisos otorgados a una entidad de seguridad en una ruta específica. El icono X situado junto a ACE se puede utilizar para eliminarlo como se muestra a continuación:

![](assets/image2019-3-21_0-53-19.png) ![](assets/unspe.png)

### Combinaciones de privilegios de la IU clásica {#classic-ui-privilege-combinations}

Tenga en cuenta que la nueva interfaz de usuario de permisos utiliza explícitamente el conjunto básico de privilegios en lugar de combinaciones predefinidas que no reflejan realmente los privilegios subyacentes exactos que se concedieron.

Causó confusión sobre qué es exactamente lo que se está configurando. En la tabla siguiente se muestra la asignación entre las combinaciones de privilegios de la IU clásica y los privilegios reales que las constituyen:

<table>
 <tbody>
  <tr>
   <th>Combinaciones de privilegios de la IU clásica</th>
   <th>Privilegio de la interfaz de usuario de permisos</th>
  </tr>
  <tr>
   <td>Lectura</td>
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

