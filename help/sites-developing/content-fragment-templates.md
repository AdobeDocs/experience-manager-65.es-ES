---
title: Plantillas de fragmentos de contenido
description: Las plantillas se seleccionan al crear un fragmento de contenido y proporcionan al nuevo fragmento la estructura básica, el elemento y la variación
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---

# Plantillas de fragmentos de contenido{#content-fragment-templates}

>[!CAUTION]
>
>Se recomiendan [modelos de fragmentos de contenido](/help/assets/content-fragments/content-fragments-models.md) para crear todos los fragmentos de contenido nuevos.
>
>Los modelos de fragmento de contenido se utilizan para todos los ejemplos en WKND.

>[!NOTE]
>
>AEM Antes de la versión 6.3, los fragmentos de contenido se creaban en función de plantillas en lugar de modelos.
>
>Las plantillas de fragmento de contenido ya no se utilizan. Todavía se pueden utilizar para crear fragmentos, pero se recomienda utilizar Modelos de fragmentos de contenido en su lugar. No se agregarán nuevas funciones a las plantillas de fragmento y se eliminarán en una versión futura.

Las plantillas se seleccionan al crear un fragmento de contenido. Proporcionan al nuevo fragmento la estructura básica, los elementos y la variación. Las plantillas utilizadas para los fragmentos de contenido están sujetas al Administrador de configuración de Granite.

Las plantillas listas para usar se encuentran en:

* `/libs/settings/dam/cfm/templates`

Puede crear plantillas específicas del sitio para fragmentos de contenido en:

* `/apps/settings/dam/cfm/templates`
La ubicación para superponer plantillas predeterminadas o proporcionar plantillas específicas del cliente para toda la aplicación que no se van a ampliar/cambiar durante la ejecución.

* `/conf/global/settings/dam/cfm/templates`
La ubicación de las plantillas específicas del cliente para toda la instancia que deben cambiarse durante la ejecución.

El orden de prioridad es (en orden descendente) `/conf`, `/apps`, `/libs`.

>[!CAUTION]
>
>Usted ***no debe*** cambiar nada en la ruta de acceso `/libs`.
>
>Esto se debe a que el contenido de `/libs` se sobrescribirá la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de características).
>
>El método recomendado para la configuración y otros cambios es:
>
>1. Vuelva a crear el elemento necesario (es decir, tal como existe en `/libs`) en `/apps`
>
>1. Realizar cambios en `/apps`
>

La estructura básica de una plantilla se encuentra debajo de:

```xml
conf
  global
    settings
      dam
        cfm
          templates
            <template-name>
              ...
```

Con la estructura específica:

```xml
+ <template-name>
    - jcr:primaryType
    - jcr:title
    - jcr:description
    - initialAssociatedContent
    - precreateElements
    - version
    + elements
        - jcr:primaryType
        + <element-name>
            - jcr:primaryType
            - jcr:title
            - defaultContent
            - initialContentType
            - name
        ... + other element definitions
    + variations
        - jcr:primaryType
        + <variation-name>
            - jcr:primaryType
            - jcr:title
            - jcr:description
            - name
        ... + other variation definitions
```

Más detalles sobre los nodos y sus propiedades son:

* **Plantilla**

  <table>
   <tbody>
    <tr>
     <th>Nombre</th>
     <th>Tipo</th>
     <th>Valor </th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>Este nodo es la raíz de cada plantilla. Es obligatorio y debe tener un nombre único.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obligatorio<br /> </p> </td>
     <td>El título de la plantilla (se muestra en el asistente <strong>Crear fragmento</strong>).</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>opcional</p> </td>
     <td>Un texto que describe el propósito de la plantilla (mostrado en el asistente <strong>Crear fragmento</strong>).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>opcional</p> </td>
     <td>Matriz con rutas a colecciones que deben asociarse a un fragmento de contenido recién creado de forma predeterminada.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>Requerido</p> </td>
     <td><p><code>true</code>, si los subrecursos que representan los elementos (excepto el elemento principal) del fragmento de contenido deben crearse cuando se cree el fragmento de contenido; <em>false</em> si deben crearse "sobre la marcha".</p> <p><strong>Nota</strong>: actualmente este parámetro debe establecerse en <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>Requerido</p> </td>
     <td><p>Versión de la estructura de contenido; compatible actualmente:</p> <p><strong>Nota</strong>: actualmente este parámetro debe establecerse en <code>2</code>.<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **Elementos**

  <table>
   <tbody>
    <tr>
     <th>Nombre</th>
     <th>Tipo</th>
     <th>Valor </th>
    </tr>
    <tr>
     <td><code>elements</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>Requerido</p> </td>
     <td><p>Nodo que contiene la definición de los elementos del fragmento de contenido. Es obligatorio y debe contener al menos un nodo secundario para el elemento <strong>Main</strong>, pero puede contener [1..n] nodos secundarios.</p> <p>Cuando se utiliza la plantilla, la subrama de elementos se copia en la subrama del modelo del fragmento.</p> <p>El primer elemento (tal como se ve en el CRXDE Lite) se considera automáticamente como el elemento <i>main</i>; el nombre del nodo es irrelevante y el nodo en sí no tiene una relevancia especial, aparte del hecho de que está representado por el recurso principal; los demás elementos se gestionan como subrecursos.</p> </td>
    </tr>
   </tbody>
  </table>

* **Nombre de elemento**

  <table>
   <tbody>
    <tr>
     <th>Nombre</th>
     <th>Tipo</th>
     <th>Valor </th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>Este nodo define un elemento. Es obligatorio y debe tener un nombre único.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>Requerido</p> </td>
     <td>El título del elemento (mostrado en el selector de elementos del editor de fragmentos).</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>predeterminado: ""</p> </td>
     <td>Contenido inicial del elemento; sólo se usa si <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>valor predeterminado: <code>text/html</code></p> </td>
     <td><p>Tipo de contenido inicial del elemento; sólo se usa si <code>precreateElements</code><i> = </i><code>true</code>; actualmente se admite:</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>Requerido</p> </td>
     <td>El nombre interno del elemento; debe ser único para el tipo de fragmento.</td>
    </tr>
   </tbody>
  </table>

* **Variaciones**

  <table>
   <tbody>
    <tr>
     <th>Nombre</th>
     <th>Tipo</th>
     <th>Valor </th>
    </tr>
    <tr>
     <td><code>variations</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>opcional</p> </td>
     <td>Este nodo opcional contiene la definición de las variaciones iniciales del fragmento de contenido.</td>
    </tr>
   </tbody>
  </table>

* **Nombre de variación**

  <table>
   <tbody>
    <tr>
     <th>Nombre</th>
     <th>Tipo</th>
     <th>Valor </th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>obligatorio si hay un nodo de variación</p> </td>
     <td><p>Define una variación inicial.<br /> La variación se agrega de manera predeterminada a todos los elementos del fragmento de contenido.</p> <p>La variación tendrá el mismo contenido inicial que el elemento respectivo (consulte <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>Requerido</p> </td>
     <td>El título de la variación (mostrado en la pestaña <strong>Variación</strong> del editor del fragmento (carril izquierdo)).</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>predeterminado: ""</p> </td>
     <td>Un texto que proporciona una descripción de la variación <span>(mostrada en la ficha <strong>Variación</strong> del editor del fragmento (carril izquierdo)).</code></td>
    </tr>
   </tbody>
  </table>
