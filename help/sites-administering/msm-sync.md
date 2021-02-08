---
title: Configuración de la sincronización de Live Copy
seo-title: Configuración de la sincronización de Live Copy
description: Obtenga más información sobre la configuración de la sincronización de Live Copy.
seo-description: Obtenga más información sobre la configuración de la sincronización de Live Copy.
uuid: a5db0bee-a761-4cff-81dc-31b374525f47
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 6bcf0fcc-481a-4283-b30d-80b517701280
docset: aem65
translation-type: tm+mt
source-git-commit: 31f546400f4c3335953d05b1df9394445b5feb56
workflow-type: tm+mt
source-wordcount: '2707'
ht-degree: 76%

---


# Configuración de la sincronización de Live Copy{#configuring-live-copy-synchronization}

Realice las siguientes tareas para controlar cómo y cuándo se sincronizan los elementos de Live Copy con su contenido de origen.

* Decida si las opciones de configuración de lanzamiento existentes cumplen los requisitos o si necesita crear una o más.
* Especifique las opciones de configuración de lanzamiento que se utilizarán en los elementos de Live Copy.

## Opciones de configuración de lanzamiento personalizadas e instaladas {#installed-and-custom-rollout-configurations}

Esta sección proporciona información sobre las opciones de configuración de lanzamiento instaladas y las acciones de sincronización que utilizan, así como información para crear opciones de configuración personalizadas si es necesario.

>[!CAUTION]
>
>Se recomienda actualizar o cambiar una configuración de implementación predeterminada (instalada) **no**. Si hay un requisito para una acción en directo personalizada, debe agregarse en una configuración de implementación personalizada.

### Activadores de lanzamiento {#rollout-triggers}

Cada configuración de lanzamiento utiliza un activador de lanzamiento que hace que se produzca el lanzamiento. En las opciones de configuración de lanzamiento se puede utilizar uno de los siguientes activadores:

* **En el lanzamiento**: el comando **Lanzar** se utiliza en la página del modelo, o el comando **Sincronizar** se utiliza en la página de Live Copy.

* **En la modificación**: la página de origen se modifica.

* **En la activación**: la página de origen se activa.

* **En la desactivación**: la página de origen se desactiva.

>[!NOTE]
>
>Recuerde que el uso del activador &quot;En la modificación&quot; puede afectar al rendimiento. Consulte [las prácticas recomendadas de MSM](/help/sites-administering/msm-best-practices.md#onmodify) para obtener más información.

### Opciones de configuración de lanzamiento instaladas  {#installed-rollout-configurations}

En la siguiente tabla se enumeran las opciones de configuración de lanzamiento que se instalan con AEM. La tabla incluye las acciones de activación y sincronización de cada configuración de lanzamiento. Si las acciones de configuración de lanzamiento instaladas no cumplen los requisitos, puede [crear una nueva configuración de lanzamiento](#creating-a-rollout-configuration).

<table>
 <tbody>
  <tr>
   <th>Nombre</th>
   <th>Descripción</th>
   <th>Activador</th>
   <th>Acciones de sincronización<br /><br /> ; consulte también las <a href="#installed-synchronization-actions">acciones de sincronización instaladas</a></th>
  </tr>
  <tr>
   <td>Configuración de lanzamiento estándar</td>
   <td>La configuración de lanzamiento estándar permite iniciar procesos de lanzamiento con el activador de lanzamientos, y ejecuta acciones como crear, actualizar, eliminar contenido y ordenar nodos secundarios.</td>
   <td>En el lanzamiento</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Activar si se activa el modelo</td>
   <td>Publica la Live Copy cuando se publica el origen.</td>
   <td>En la activación</td>
   <td>targetActivate</td>
  </tr>
  <tr>
   <td>Desactivar si se desactiva el modelo</td>
   <td>Desactiva la Live Copy cuando se desactiva el origen.</td>
   <td>En la desactivación</td>
   <td>targetDeactivate<br /> </td>
  </tr>
  <tr>
   <td>Insertar al modificar</td>
   <td><p>Inserta el contenido la Live Copy cuando se modifica el origen.</p> <p>Utilice esta configuración de lanzamiento con moderación, ya que usa el activador "En la modificación".</p> </td>
   <td>En la modificación</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> </td>
  </tr>
  <tr>
   <td>Insertar al modificar (superficial)</td>
   <td><p>Inserta el contenido en la Live Copy cuando se modifica la página del modelo sin actualizar las referencias (por ejemplo, para copias superficiales).</p> <p>Utilice esta configuración de lanzamiento con moderación, ya que usa el activador "En la modificación".</p> </td>
   <td>En la modificación</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Lanzamiento de promoción</td>
   <td>Configuración del lanzamiento estándar para promocionar páginas de inicio con dicho fin.</td>
   <td>En el lanzamiento</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> markLiveRelationship</td>
  </tr>
  <tr>
   <td>Configuración del lanzamiento de contenido de la página del catálogo</td>
   <td>Aplica plantillas de página de un modelo de catálogo.</td>
   <td>En el lanzamiento</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productCreateUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Configuración del lanzamiento de actualización de la página del catálogo</td>
   <td>Aplica propiedades de destino de un modelo de catálogo. Debe ejecutarse después de la configuración de lanzamiento del contenido de la página del catálogo.</td>
   <td>En el lanzamiento</td>
   <td>catalogRolloutHooks</td>
  </tr>
  <tr>
   <td>Configuración del lanzamiento de publicaciones de DPS</td>
   <td>La configuración del lanzamiento de publicación de DPS permite iniciar el proceso del activador "En el lanzamiento" al mismo tiempo que se excluyen las propiedades de enlace de FolioProducer en el lanzamiento inicial.</td>
   <td>En el lanzamiento</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> dpsMetadataFilter</td>
  </tr>
  <tr>
   <td>Configuración del lanzamiento del catálogo heredado (5.6.0)</td>
   <td>En desuso. Use el generador de catálogos en lugar de MSM para los lanzamientos de catálogos.</td>
   <td>En el lanzamiento</td>
   <td>editProperties</td>
  </tr>
 </tbody>
</table>

### Acciones de sincronización instaladas  {#installed-synchronization-actions}

En la siguiente tabla se enumeran las acciones de sincronización que se instalan con AEM. Si las acciones instaladas no cumplen con sus requisitos, puede [Crear una nueva acción de sincronización](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).

<table>
 <tbody>
  <tr>
   <th>Nombre de la acción</th>
   <th>Descripción</th>
   <th>Propiedades<br /> </th>
  </tr>
  <tr>
   <td>contentCopy</td>
   <td>Cuando los nodos de origen no existen en la Live Copy, se copian en el mismo. <a href="#excluding-properties-and-node-types-from-synchronization">Configure el </a> servicio de acción Copiar contenido de CQ MSM para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que se van a excluir.  <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentDelete</td>
   <td><p>Elimina los nodos de la Live Copy que no existen en el origen. <a href="#excluding-properties-and-node-types-from-synchronization">Configure el </a> servicio de acción de eliminación de contenido MSM de CQ para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que desea excluir. </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentUpdate</td>
   <td>Actualiza el contenido de la Live Copy con los cambios del origen. <a href="#excluding-properties-and-node-types-from-synchronization">Configure el </a> servicio de acción de actualización de contenido MSM de CQ para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que desea excluir.  <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>editProperties</td>
   <td><p>Edita las propiedades de la Live Copy. La propiedad editMap determina qué propiedades se editan y su valor. El valor de la propiedad editMap debe utilizar el formato siguiente:</p> <p><code>[property_name_1]#[current_value]#</code>[new_value],<br /> <code>[property_name_2]#[current_value]#</code>[nuevo_valor],<br />... ,<br /> <code>[property_name_n]#[current_value]#</code>[nuevo_valor]</p> <p>Los elementos <code>current_value</code> y <code>new_value</code> son expresiones regulares. <br /> </p> <p>Por ejemplo, considere el valor siguiente para editMap:</p> <p><code>sling:resourceType#/</code>(contentpage|homepage)#/<br /> mobilecontentpage,<br /> cq:template#/contentpage#/mobilecontentpage</p> <p>Este valor edita las propiedades de los nodos de la Live Copy de la siguiente manera:</p>
    <ul>
     <li>Las propiedades <code>sling:resourceType</code> que se establecen en <code>contentpage</code> o en <code>homepage</code> se establecen en <code>mobilecontentpage.</code></li>
     <li>Las propiedades <code>cq:template</code> que están configuradas en <code>contentpage</code> se establecen en <code>mobilecontentpage.</code></li>
    </ul> </td>
   <td><p> </p> <p>editMap: (cadena) Identifica la propiedad, el valor actual y el nuevo valor. Consulte la descripción para obtener más información.<br /> </p> </td>
  </tr>
  <tr>
   <td>notify</td>
   <td>Envía un evento de página que indica que la página se ha lanzado. Para recibir notificaciones, primero debe suscribirse a eventos de lanzamiento.</td>
   <td> </td>
  </tr>
  <tr>
   <td>orderChildren</td>
   <td>En la Live Copy, ordena los elementos secundarios (nodos) según el orden del modelo<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>referencesUpdate</td>
   <td><p>En la Live Copy, esta acción de sincronización actualiza referencias como, por ejemplo, los vínculos.<br /> Busca rutas de acceso en las páginas de Live Copy que apuntan a un recurso dentro del modelo. Cuando se encuentran, se actualiza la ruta de acceso para que apunte al recurso relacionado dentro de la Live Copy (en lugar del modelo). Las referencias que tienen los destinos fuera del modelo no cambian.</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">Configure el </a> servicio de acción de actualización de referencias de MSM de CQ para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que desea excluir. </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetVersion</td>
   <td><p>Crea una versión de la Live Copy.</p> <p>Esta acción debe ser la única acción de sincronización incluida en una configuración de lanzamiento.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetActivate</td>
   <td><p>Activa la Live Copy.</p> <p>Esta acción debe ser la única acción de sincronización incluida en una configuración de lanzamiento.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetDeactivate</td>
   <td><p>Desactiva la Live Copy.</p> <p>Esta acción debe ser la única acción de sincronización incluida en una configuración de lanzamiento.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>flujo de trabajo</td>
   <td><p>Inicia el flujo de trabajo que define la propiedad de destino (solo para páginas) y toma la Live Copy como carga útil.</p> <p>La ruta de destinatario es la ruta del nodo del modelo.</p> </td>
   <td>destino: (cadena) La ruta de acceso del modelo de flujo de trabajo.<br /> </td>
  </tr>
  <tr>
   <td>obligatorio</td>
   <td><p>Establece el permiso de varias ACL en la página de la Live Copy como de solo lectura para un grupo de usuarios específico. Están configuradas las siguientes ACL:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_REMOVE</li>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>Utilice esta acción solo para páginas.</p> </td>
   <td>destino: (cadena) El ID del grupo para el que se define la configuración. <br /> </td>
  </tr>
  <tr>
   <td>mandatoryContent</td>
   <td><p>Establece el permiso de varias ACL en la página de la Live Copy como de solo lectura para un grupo de usuarios específico. Están configuradas las siguientes ACL:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>Utilice esta acción solo para páginas.</p> </td>
   <td>destino: (cadena) El ID del grupo para el que se define la configuración. </td>
  </tr>
  <tr>
   <td>mandatoryStructure</td>
   <td>Establece el permiso de la ACL ActionSet.ACTION_NAME_REMOVE en la página de la Live Copy como de solo lectura para un grupo de usuarios específico. Utilice esta acción solo para páginas.</td>
   <td>destino: (cadena) El ID del grupo para el que se define la configuración. </td>
  </tr>
  <tr>
   <td>VersionCopyAction</td>
   <td>Si la página de origen o el modelo se ha publicado al menos una vez, crea una página de Live Copy mediante la versión publicada. Nota: Esta acción solo está disponible para crear una página de Live Copy basada en una página de origen publicada, no para actualizar una página de Live Copy existente. </td>
   <td> </td>
  </tr>
  <tr>
   <td>PageMoveAction</td>
   <td><p>PageMoveAction se aplica cuando una página se ha movido en el modelo.</p> <p>La acción copia la página de Live Copy (relacionada) en lugar de moverla desde la ubicación, antes de realizar el traslado a la ubicación posterior.</p> <p>PageMoveAction no cambia la página de Live Copy a la ubicación antes del traslado. Por lo tanto, para configuraciones de RolloutConfigurations consecutivas, esta página tiene el estado de un elemento LiveRelationhip sin modelo.</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">Configure el </a> servicio de acción de movimiento de página CQ MSM para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que desea excluir. </p> <p>Esta acción debe ser la única acción de sincronización incluida en una configuración de lanzamiento.</p> </td>
   <td><p>prop_referenceUpdate: (booleano) establezca este valor en "verdadero" para actualizar las referencias. El valor predeterminado es "verdadero".</p> <p> </p> </td>
  </tr>
  <tr>
   <td>productCreateUpdate</td>
   <td>Crea o actualiza recursos del producto en un catálogo. Esta acción se debe utilizar en una de las siguientes situaciones:
    <ul>
     <li>Generación o lanzamiento de un catálogo (o sección de catálogos)</li>
     <li>Un usuario restaura la herencia de sincronización de un componente del producto.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>markLiveRelationship</td>
   <td>Indica una relación dinámica del contenido creado para el lanzamiento.</td>
   <td> </td>
  </tr>
  <tr>
   <td>catalogRolloutHooks</td>
   <td>Ejecuta enlaces de lanzamiento específicos de la generación del catálogo. Llama a los métodos executePageRolloutHooks y executeProductRolloutHooks del objeto CatalogGenerator.<br /> Consulte com.adobe.cq.commerce.pim.api.CatalogGenerator en los archivos JavaDoc de AEM.</td>
   <td> </td>
  </tr>
  <tr>
   <td>productUpdate</td>
   <td>Actualiza las páginas del producto en una Live Copy de un catálogo de productos</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Creación de una configuración de lanzamiento {#creating-a-rollout-configuration}

Puede [crear una configuración de lanzamiento](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) cuando las opciones de la misma que estén instaladas no cumplan los requisitos de la aplicación:

* [Cree la configuración de lanzamiento](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
* [Agregue acciones de sincronización a la configuración de lanzamiento](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

La nueva configuración de lanzamiento estará disponible al establecer las opciones de la misma en una página de Live Copy o modelo.

### Exclusión de propiedades y tipos de nodos de la sincronización  {#excluding-properties-and-node-types-from-synchronization}

Puede configurar varios servicios de OSGi que admitan las acciones de sincronización correspondientes para que no afecten a los tipos de nodos y propiedades específicos. Por ejemplo, muchas propiedades y subnodos relacionados con el funcionamiento interno de AEM no deben incluirse en una Live Copy. Solo se debe copiar el contenido relevante para el usuario de la página.

Al trabajar con AEM existen varios métodos para gestionar los parámetros de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más detalles y las prácticas recomendadas.

En la tabla siguiente se enumeran las acciones de sincronización para las que se pueden especificar los nodos que se excluirán. La tabla proporciona los nombres de los servicios que se configuran mediante la consola web y el PID para configurar el uso de un nodo del repositorio.

| Acción de sincronización | Nombre del servicio en la consola web | PID de servicio |
|---|---|---|
| contentCopy | Acción de copia de contenido de MSM de CQ | com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory |
| contentDelete | Acción de eliminación de contenido de MSM de CQ | com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory |
| contentUpdate | Acción de actualización de contenido de MSM de CQ | com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory |
| PageMoveAction | Acción de movimiento de página CQ MSM | com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory |
| ReferencesUpdate | Acción de actualización de referencias de MSM de CQ | com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory |

En la tabla siguiente se describen las propiedades que se pueden configurar:

<table>
 <tbody>
  <tr>
   <th>Propiedad de la consola web / propiedad OSGi</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><p>Tipos de nodos excluidos</p> <p>cq.wcm.msm.action.excludednodetypes</p> </td>
   <td>Una expresión regular que coincide con los tipos de nodo que se excluirán de la acción de sincronización.</td>
  </tr>
  <tr>
   <td><p>Elementos de párrafo excluidos</p> <p>cq.wcm.msm.action.excludedparagraphitems</p> </td>
   <td>Expresión regular que coincide con los elementos de párrafo que se excluirán de la acción de sincronización.</td>
  </tr>
  <tr>
   <td><p>Propiedades de página excluidas</p> <p>cq.wcm.msm.action.excludedprops</p> </td>
   <td>Expresión regular que coincide con las propiedades de página que se excluirán de la acción de sincronización.</td>
  </tr>
  <tr>
   <td><p>Tipos de nodos mixtos omitidos</p> <p>cq.wcm.msm.action.ignoredMixin</p> </td>
   <td>Solo está disponible para la acción de actualización de contenido de MSM de CQ. Expresión regular que coincide con los nombres de los tipos de nodos de Mixin que se van a excluir de la acción de sincronización.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>En la interfaz de usuario clásica, el icono de bloqueo que aparece en el cuadro de diálogo Propiedades de la página para las páginas de Live Copy no refleja la configuración de la propiedad &quot;Propiedades de la página excluidas&quot;. El icono de bloqueo aparece incluso para las propiedades que se excluyen de la acción de sincronización.

>[!NOTE]
>
>En la interfaz de usuario optimizada para pantallas táctiles, consulte también [Configuración de bloqueos MSM en Propiedades de la página (Interfaz de usuario optimizada para pantallas táctiles)](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-pagep-roperties-touch-optimized-ui).

#### Acción de actualización de contenido de CQ MSM: exclusiones {#cq-msm-content-update-action-exclusions}

Algunas propiedades y tipos de nodo se excluyen de forma predeterminada. Estos se definen en la configuración de OSGi de la **acción de actualización de contenido de CQ MSM**, en **Propiedades de página excluidas**.

De forma predeterminada, las propiedades que coinciden con las siguientes expresiones regulares se excluyen (es decir, no se actualizan) del lanzamiento:

![chlimage_1](assets/chlimage_1.png)

Puede cambiar las expresiones que definen la lista de exclusión según sea necesario.

Por ejemplo, si quiere que el **título** de la página se incluya en los cambios considerados para el lanzamiento, elimine `jcr:title` de las exclusiones. Por ejemplo, con la expresión regular:

`jcr:(?!(title)$).*`

### Configuración de la sincronización de actualización de referencias {#configuring-synchronization-for-updating-references}

Puede configurar varios servicios de OSGi que admitan las acciones de sincronización correspondientes relacionadas con la actualización de referencias.

Al trabajar con AEM existen varios métodos para gestionar los parámetros de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más detalles y las prácticas recomendadas.

En la siguiente tabla se enumeran las acciones de sincronización para las que se puede especificar la actualización de referencia. La tabla proporciona los nombres de los servicios que se configuran mediante la consola web y el PID para configurar el uso de un nodo del repositorio.

<table>
 <tbody>
  <tr>
   <th>Propiedad de la consola web / propiedad OSGi</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><p>Actualizar referencia en LiveCopies anidadas</p> <p>cq.wcm.msm.impl.action.referencesupdate.prop_updateNested</p> </td>
   <td>Solo disponible para la acción de actualización de referencias de MSM de CQ. Seleccione esta opción (consola web) o establezca esta propiedad booleana en true (configuración del repositorio) para reemplazar las referencias que destinatario cualquier recurso que se encuentre dentro de la rama de la parte superior de LiveCopy.</td>
  </tr>
  <tr>
   <td><p>Actualizar páginas de referencia</p> <p>cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate</p> </td>
   <td>Solo disponible para la acción de movimiento de página CQ MSM. Seleccione esta opción (consola web) o establezca esta propiedad booleana en <code>true</code> (configuración del repositorio) para actualizar cualquier referencia y utilizar la página original para hacer referencia a la página de LiveCopy.</td>
  </tr>
 </tbody>
</table>

## Especificación de las opciones de configuración de lanzamiento que se van a utilizar {#specifying-the-rollout-configurations-to-use}

MSM le permite especificar conjuntos de opciones de configuración de lanzamiento que se utilizan normalmente y, cuando sea necesario, puede invalidar determinadas Live Copy. MSM proporciona varias ubicaciones para especificar las opciones de configuración de lanzamiento que se deben utilizar. La ubicación determina si la configuración se aplica a una Live Copy específica.

En la siguiente lista de ubicaciones en la que se pueden especificar las opciones de configuración de lanzamiento que se deben utilizar, se describe cómo MSM determina qué opciones de configuración de lanzamiento se deben utilizar para una Live Copy:

* **[Propiedades de la página de Live Copy](/help/sites-administering/msm-sync.md#setting-the-rollout-configurations-for-a-live-copy-page):** cuando una página de Live Copy está configurada para utilizar una o varias opciones de configuración de lanzamiento, MSM utiliza dichas opciones de configuración.
* **[Propiedades de la página de modelo](/help/sites-administering/msm-sync.md#setting-the-rollout-configuration-for-a-blueprint-page):** cuando una página de Live Copy se basa en un modelo y la página de Live Copy no usa una configuración de lanzamiento, se utiliza la configuración de lanzamiento asociada a la página de origen del modelo.
* **Propiedades de la página principal de Live Copy:** cuando ni la página de Live Copy ni la página de origen de modelo están configuradas con una configuración de implementación, se utiliza la configuración de despliegue que se aplica a la página principal de la página de Live Copy.
* **[Valor predeterminado](/help/sites-administering/msm-sync.md#setting-the-system-default-rollout-configuration) del sistema:** cuando no se puede determinar la configuración de despliegue de la página principal de la Live Copy, se utiliza la configuración de despliegue predeterminada del sistema.

Por ejemplo, un modelo utiliza el sitio de referencia We.Retail como contenido de origen. Se crea un sitio a partir del modelo. Cada elemento de la lista siguiente describe un escenario diferente respecto al uso de las opciones de configuración de lanzamiento:

* Ninguna de las páginas del modelo ni las páginas de Live Copy están configuradas para utilizar una configuración de lanzamiento. MSM utiliza la configuración de lanzamiento predeterminada del sistema para todas las páginas de Live Copy.
* La página raíz del sitio de referencia We.Retail se configura con varias opciones de configuración de lanzamiento. MSM utiliza estas opciones de configuración de lanzamiento para todas las páginas de Live Copy.
* La página raíz del sitio de referencia de We.Retail está configurada con varias configuraciones de implementación y la página raíz del sitio de Live Copy está configurada con un conjunto diferente de configuraciones de implementación. MSM utiliza las opciones de configuración de lanzamiento que están en la página raíz del sitio de Live Copy.

### Configuración de las opciones de configuración de lanzamiento para una página de Live Copy  {#setting-the-rollout-configurations-for-a-live-copy-page}

Configure una página de Live Copy con las opciones de configuración de lanzamiento que se usarán cuando se lance la página de origen. Las páginas secundarias heredan la configuración de forma predeterminada. Al establecer la configuración de lanzamiento para su uso, se anula la configuración que la página de Live Copy hereda de su elemento principal.

También puede configurar las opciones de configuración de lanzamiento para una página de Live Copy al [crear la Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page).

1. Utilice la consola **Sitios** para seleccionar la página de Live Copy.
1. En la barra de herramientas, seleccione **Propiedades**.
1. Abra la ficha **Live Copy**.

   La sección **Configuración** muestra las opciones de configuración de lanzamiento que hereda la página.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Si es necesario, ajuste la marca de **Herencia de Live Copy**. Si se selecciona, la configuración de Live Copy es eficaz en todas las páginas secundarias.

1. Desactive la propiedad **Heredar configuración de lanzamiento del elemento principal** y, a continuación, seleccione una o varias opciones de configuración de lanzamiento de la lista.

   Las opciones de configuración de lanzamiento seleccionadas se muestran debajo de la lista desplegable.

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. Haga clic o pulse **Guardar**.

### Opciones de la configuración de lanzamiento para una página de modelo  {#setting-the-rollout-configuration-for-a-blueprint-page}

Configure una página de modelo con las opciones de configuración de lanzamiento que se usarán cuando se lance la página de modelo.

Tenga en cuenta que las páginas secundarias de la página de modelo heredan la configuración. Al establecer la configuración de lanzamiento para su uso, podría anular la configuración que la página hereda de su elemento principal.

1. Utilice la consola **Sites** para seleccionar la página raíz del modelo.
1. En la barra de herramientas, seleccione **Propiedades**.
1. Abra la ficha **Modelo**.
1. Seleccione una o más **opciones de configuración de lanzamiento** con el selector desplegable.
1. Para almacenar las actualizaciones, seleccione **Guardar**.

### Opciones de la configuración de lanzamiento predeterminada del sistema {#setting-the-system-default-rollout-configuration}

Especifique una configuración de lanzamiento para usar como valor predeterminado del sistema. Para especificar el valor predeterminado, configure el servicio de OSGi:

* **Administrador de relaciones dinámicas de CQ WCM por día**; el servicio PID es 
`com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

Configure el servicio mediante la [Consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o un [nodo de repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* En la consola web, el nombre de la propiedad que se va a configurar es la configuración de lanzamiento predeterminada.
* Mediante un nodo del repositorio, el nombre de la propiedad que se va a configurar es `liverelationshipmgr.relationsconfig.default`.

Establezca este valor de la propiedad en la ruta de la configuración de lanzamiento que se utilizará como valor predeterminado del sistema. El valor predeterminado es `/libs/msm/wcm/rolloutconfigs/default`, que es la **configuración de despliegue estándar**.
