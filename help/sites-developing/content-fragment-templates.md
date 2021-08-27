---
title: Plantillas de fragmento de contenido
seo-title: Content Fragment Templates
description: Las plantillas se seleccionan al crear un fragmento de contenido y proporcionan el nuevo fragmento con la estructura básica, el elemento y la variación
seo-description: Templates are selected when creating a content fragmen and provide the new fragment with the basic structure, element, and variation
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
source-git-commit: 2ec9625d480eb8cae23f44aa247fce2a519dec31
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 5%

---

# Plantillas de fragmento de contenido{#content-fragment-templates}

>[!CAUTION]
>
>[Ahora se recomiendan los ](/help/assets/content-fragments/content-fragments-models.md) modelos de fragmento de contenido para crear todos los fragmentos.
>
>Los modelos de fragmentos de contenido se utilizan en todos los ejemplos de We.Retail.

>[!NOTE]
>
>Antes de AEM 6.3, los fragmentos de contenido se creaban con el uso de plantillas en lugar de modelos. Las plantillas ya no están disponibles para crear nuevos fragmentos, pero los fragmentos creados con una plantilla de este tipo siguen siendo compatibles.

Las plantillas se seleccionan al crear un fragmento de contenido. Proporcionan al nuevo fragmento la estructura básica, los elementos y la variación. Las plantillas utilizadas para los fragmentos de contenido están sujetas al Administrador de configuración de Granite.

Las plantillas listas para usar se incluyen en:

* `/libs/settings/dam/cfm/templates`

Puede crear plantillas específicas del sitio para fragmentos de contenido en:

* `/apps/settings/dam/cfm/templates`
La ubicación para superponer plantillas integradas o proporcionar plantillas específicas del cliente y para toda la aplicación que no se pretendan ampliar o cambiar durante la ejecución.

* `/conf/global/settings/dam/cfm/templates`
La ubicación de las plantillas específicas del cliente para toda la instancia que deben cambiarse durante la ejecución.

El orden de prioridad es (en orden descendente) `/conf`, `/apps`, `/libs`.

>[!CAUTION]
>
>***no debe*** cambiar nada en la ruta `/libs`.
>
>Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y puede sobrescribirse al aplicar una corrección o un paquete de funciones).
>
>El método recomendado para la configuración y otros cambios es:
>
>1. Volver a crear el elemento requerido (es decir, tal como existe en `/libs`) en `/apps`
>
>1. Realizar cambios en `/apps`

>


La estructura básica de una plantilla se mantiene en:

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

Con una estructura específica:

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
     <th>Value</th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>Este nodo es la raíz de cada plantilla. Es obligatorio y debe tener un nombre único.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required<br /> </p> </td>
     <td>El título de la plantilla (se muestra en el asistente <strong>Crear fragmento</strong>).</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>opcional</p> </td>
     <td>Texto que describe el propósito de la plantilla (mostrado en el asistente <strong>Crear fragmento</strong>).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>opcional</p> </td>
     <td>Matriz con rutas a colecciones que deben asociarse a un fragmento de contenido recién creado de forma predeterminada.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>required</p> </td>
     <td><p><code>true</code>, si los subrecursos que representan los elementos (excepto el elemento maestro) del fragmento de contenido se deben crear al crear el fragmento de contenido; <em>false</em> si se deben crear "sobre la marcha".</p> <p><strong>Nota</strong>: actualmente, este parámetro debe establecerse en  <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>obligatorio</p> </td>
     <td><p>Versión de la estructura de contenido; compatible actualmente:</p> <p><strong>Nota</strong>: actualmente, este parámetro debe establecerse en  <code>2</code>.<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **Elementos**

   <table>
   <tbody>
    <tr>
     <th>Nombre</th>
     <th>Tipo</th>
     <th>Valor</th>
    </tr>
    <tr>
     <td><code>elements</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>obligatorio</p> </td>
     <td><p>Nodo que contiene la definición de los elementos del fragmento de contenido. Es obligatorio y debe contener al menos un nodo secundario para el elemento <strong>Principal</strong>, pero puede contener [1..n] nodos secundarios.</p> <p>Cuando se utiliza la plantilla, la subrama de elementos se copia en la subrama de modelo del fragmento.</p> <p>El primer elemento (como se ve en el CRXDE Lite) se considera automáticamente como el elemento <i>main</i>; el nombre del nodo es irrelevante y el nodo en sí no tiene una relevancia especial, aparte del hecho de que está representado por el recurso principal; los demás elementos se gestionan como subrecursos.</p> </td>
    </tr>
   </tbody>
  </table>

* **Nombre de elemento**

   <table>
   <tbody>
    <tr>
     <th>Nombre</th>
     <th>Tipo</th>
     <th>Valor</th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>Este nodo define un elemento. Es obligatorio y debe tener un nombre único.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obligatorio</p> </td>
     <td>Título del elemento (mostrado en el selector de elementos del editor de fragmentos).</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>predeterminada: ""</p> </td>
     <td>Contenido inicial del elemento; solo se usa si <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>predeterminada: <code>text/html</code></p> </td>
     <td><p>Tipo de contenido inicial del elemento; solo se usa si <code>precreateElements</code><i> = </i><code>true</code>; compatible actualmente:</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>obligatorio</p> </td>
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
     <th>Valor</th>
    </tr>
    <tr>
     <td><code>variations</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>opcional</p> </td>
     <td>Este nodo opcional contiene la definición de las variaciones iniciales del fragmento de contenido.</td>
    </tr>
   </tbody>
  </table>

* **Nombre de la variación**

   <table>
   <tbody>
    <tr>
     <th>Nombre</th>
     <th>Tipo</th>
     <th>Valor</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>obligatorio si hay un nodo de variación</p> </td>
     <td><p>Define una variación inicial.<br /> La variación se agrega a todos los elementos del fragmento de contenido de forma predeterminada.</p> <p>La variación tendrá el mismo contenido inicial que el elemento respectivo (consulte <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obligatorio</p> </td>
     <td>El título de la variación (se muestra en la pestaña <strong>Variation</strong> del editor de fragmentos (carril izquierdo)).</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>opcional</p> <p>predeterminada: ""</p> </td>
     <td>Texto que proporciona una descripción de la variación <span> (se muestra en la pestaña <strong>Variation</strong> del editor de fragmentos (carril izquierdo)).</code></td>
    </tr>
   </tbody>
  </table>
