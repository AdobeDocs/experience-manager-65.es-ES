---
title: Identificación del contenido para traducir
seo-title: Identificación del contenido para traducir
description: Aprenda a identificar el contenido que debe traducirse.
seo-description: Aprenda a identificar el contenido que debe traducirse.
uuid: 81b9575c-1c7a-4955-b03f-3f26cbd4f956
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: eedff940-4a46-4c24-894e-a5aa1080d23d
feature: Copiar idioma
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---


# Identificación del contenido para traducir{#identifying-content-to-translate}

Las reglas de traducción identifican el contenido que se debe traducir para páginas, componentes y recursos que se incluyen en proyectos de traducción o que se excluyen de ellos. Cuando se traduce una página o un recurso, AEM extrae este contenido para que se pueda enviar al servicio de traducción.

Las páginas y los recursos se representan como nodos en el repositorio JCR. El contenido extraído es uno o más valores de propiedad de los nodos. Las reglas de traducción identifican las propiedades que contienen el contenido que se va a extraer.

Las reglas de traducción se expresan en formato XML y se almacenan en estas posibles ubicaciones:

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

El archivo se aplica a todos los proyectos de traducción.

>[!NOTE]
>
>Después de una actualización a 6.4, se recomienda mover el archivo de /etc. Consulte [Reestructuración común de repositorios en AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules) para obtener más información.

Las reglas incluyen la siguiente información:

* Ruta del nodo al que se aplica la regla. La regla también se aplica a los descendientes del nodo.
* Nombres de las propiedades del nodo que contienen el contenido que se va a traducir. La propiedad puede ser específica para un tipo de recurso específico o para todos los tipos de recurso.

Por ejemplo, puede crear una regla que traduzca el contenido que los autores añaden a todos AEM componentes de base Texto en sus páginas. La regla puede identificar el nodo `/content` y la propiedad `text` para el componente `foundation/components/text`.

Hay una [consola](#translation-rules-ui) que se ha agregado para configurar las reglas de traducción. Las definiciones de la IU rellenarán el archivo por usted.

Para obtener una descripción general de las funciones de traducción de contenido de AEM, consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md).

>[!NOTE]
>
>AEM admite la asignación individual entre tipos de recursos y atributos de referencia para la traducción del contenido al que se hace referencia en una página.

## Sintaxis de reglas para páginas, componentes y recursos {#rule-syntax-for-pages-components-and-assets}

Una regla es un elemento `node` con uno o más elementos `property` secundarios y cero o más elementos `node` secundarios:

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

Cada uno de estos `node` elementos tiene las siguientes características:

* El atributo `path` contiene la ruta al nodo raíz de la rama a la que se aplican las reglas.
* Los elementos `property` secundarios identifican las propiedades de nodo que se deben traducir para todos los tipos de recursos:

   * El atributo `name` contiene el nombre de la propiedad.
   * El atributo opcional `translate` es igual a `false` si la propiedad no está traducida. De forma predeterminada, el valor es `true`. Este atributo es útil cuando se anulan reglas anteriores.

* Los elementos `node` secundarios identifican las propiedades de nodo que se deben traducir para tipos de recursos específicos:

   * El atributo `resourceType` contiene la ruta que se resuelve en el componente que implementa el tipo de recurso.
   * Los elementos `property` secundarios identifican la propiedad node que se va a traducir. Utilice este nodo del mismo modo que los elementos `property` secundarios para las reglas de nodo.

La siguiente regla de ejemplo hace que el contenido de todas las propiedades `text` se traduzca para todas las páginas debajo del nodo `/content`. La regla es efectiva para cualquier componente que almacena contenido en una propiedad `text`, como el componente Texto base y el componente Imagen base.

```xml
<node path="/content">
          <property name="text"/>
</node>
```

El siguiente ejemplo traduce el contenido de todas las propiedades `text` y también traduce otras propiedades del componente de imagen base. Si otros componentes tienen propiedades con el mismo nombre, la regla no se les aplica.

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="foundation/components/textimage">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## Sintaxis de regla para extraer recursos de páginas {#rule-syntax-for-extracting-assets-from-pages}

Utilice la siguiente sintaxis de regla para incluir recursos incrustados en componentes o a los que se hace referencia desde ellos:

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

Cada elemento `assetNode` tiene las siguientes características:

* Un atributo `resourceType` que es igual a la ruta que se resuelve en el componente.
* Un atributo `assetReferenceAttribute` igual al nombre de la propiedad que almacena el binario del recurso (para los recursos incrustados) o la ruta al recurso al que se hace referencia.

El siguiente ejemplo extrae imágenes del componente de imagen base:

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## Reglas de anulación {#overriding-rules}

El archivo translation_rules.xml consta de un elemento `nodelist` con varios elementos `node` secundarios. AEM lee la lista de nodos de arriba a abajo. Cuando varias reglas se dirigen al mismo nodo, se utiliza la regla que se encuentra más abajo en el archivo. Por ejemplo, las siguientes reglas hacen que todo el contenido de las propiedades `text` se traduzca excepto para la rama `/content/mysite/en` de las páginas:

```xml
<nodelist>
     <node path="/content”>
           <property name="text" />
     </node>
     <node path=“/content/mysite/en”>
          <property name=“text” translate=“false" />
     </node>
<nodelist>
```

## Filtrado de propiedades {#filtering-properties}

Puede filtrar nodos que tengan una propiedad específica utilizando un elemento `filter`.

Por ejemplo, las siguientes reglas hacen que todo el contenido de las propiedades `text` se traduzca excepto para los nodos que tienen la propiedad `draft` establecida en `true`.

```xml
<nodelist>
    <node path="/content”>
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## Interfaz de usuario de reglas de traducción {#translation-rules-ui}

También hay una consola disponible para configurar las reglas de traducción.

Para acceder a él:

1. Vaya a **Tools** y, a continuación, a **General**.

   ![imagen_1-55](assets/chlimage_1-55.jpeg)

1. Seleccione **Configuración de traducción**.

   ![imagen_1-56](assets/chlimage_1-56.jpeg)

Desde aquí puede **Agregar contexto**. Esto le permite agregar una ruta.

![chlimage_1-57](assets/chlimage_1-57.jpeg)

A continuación, debe seleccionar el contexto y hacer clic en **Editar**. Se abrirá el Editor de reglas de traducción.

![chlimage_1-58](assets/chlimage_1-58.jpeg)

Hay 4 atributos que puede cambiar mediante la interfaz de usuario: `isDeep`, `inherit`, `translate` y `updateDestinationLanguage`.

**** isDeepEste atributo se aplica a los filtros de nodo y es true de forma predeterminada. Comprueba si el nodo (o sus antecesores) contiene esa propiedad con el valor de propiedad especificado en el filtro. Si es false, solo comprueba en el nodo actual.

Por ejemplo, los nodos secundarios se agregan a un trabajo de traducción incluso cuando el nodo principal tiene la propiedad `draftOnly` establecida en true para marcar el contenido de borrador. Aquí `isDeep` entra en juego y comprueba si los nodos principales tienen la propiedad `draftOnly` como true y excluye esos nodos secundarios.

En el Editor, puede comprobar/desmarcar **Is Deep** en la pestaña **Filters**.

![chlimage_1-59](assets/chlimage_1-59.jpeg)

Este es un ejemplo del xml resultante cuando **Is Deep** no está marcado en la interfaz de usuario:

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**** inheritEsto es aplicable a las propiedades. De forma predeterminada, todas las propiedades se heredan, pero si desea que alguna propiedad no se herede en el elemento secundario, puede marcar esa propiedad como falsa para que se aplique únicamente en ese nodo específico.

En la interfaz de usuario, puede marcar o desmarcar **Heredar** en la pestaña **Properties**.

![imagen_1-60](assets/chlimage_1-60.jpeg)

**** translateEl atributo translate se utiliza simplemente para especificar si se debe traducir o no una propiedad.

En la interfaz de usuario, puede marcar o desmarcar **Translate** en la pestaña **Properties**.

**** updateDestinationLanguageEste atributo se utiliza para propiedades que no tienen texto sino códigos de idioma, por ejemplo jcr:language. El usuario no traduce texto sino la configuración regional del idioma de origen a destino. Estas propiedades no se envían para su traducción.

En la interfaz de usuario, puede marcar o desmarcar **Translate** en la pestaña **Properties**, pero para las propiedades específicas que tienen códigos de idioma como valor.

Para ayudar a aclarar la diferencia entre `updateDestinationLanguage` y `translate`, a continuación se muestra un ejemplo sencillo de contexto con solo dos reglas:

![climage_1-61](assets/chlimage_1-61.jpeg)

El resultado en el xml tendrá este aspecto:

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## Edición manual del archivo de reglas {#editing-the-rules-file-manually}

El archivo translation_rules.xml que se instala con AEM contiene un conjunto predeterminado de reglas de traducción. Puede editar el archivo para satisfacer los requisitos de sus proyectos de traducción. Por ejemplo, puede agregar reglas para que se traduzca el contenido de los componentes personalizados.

Si edita el archivo translation_rules.xml, mantenga una copia de seguridad en un paquete de contenido. La instalación AEM service packs o la reinstalación de ciertos paquetes de AEM puede reemplazar el archivo translation_rules.xml actual por el original. Para restaurar las reglas en esta situación, puede instalar el paquete que contiene la copia de seguridad.

>[!NOTE]
>
>Después de crear el paquete de contenido, reconstruya el paquete cada vez que edite el archivo.

## Ejemplo de archivo de reglas de traducción {#example-translation-rules-file}

```xml
<nodelist>
    <!-- translation rules for Geometrixx Demo site (example) -->
    <node path="/content/geometrixx">
        <!-- list all node properties that should be translated -->
        <property name="jcr:title" /> <!-- translation workflows running on content saved in /content/geometrixx, will extract jcr:title values independent of the component. -->
        <property name="jcr:description" />
        <node resourceType ="foundation/components/image"> <!-- translation workflows running on content saved in /content/geometrixx, will extract alternateText values only for Image component. -->
            <property name="alternateText"/>
        </node>
        <node resourceType ="geometrixx/components/title">
            <property name="richText"/>
            <property name="jcr:title" translate="false"/> <!-- translation workflows running on content saved in /content/geometrixx, will not extract jcr:title for Title component, but instead use richText. -->
        </node>
        <node pathContains="/cq:annotations">
            <property name="text" translate="false"/> <!-- translation workflows running on content saved in /content/geometrixx, will not extract text if part of cq:annotations node. -->
        </node>
    </node>
    <!-- translation rules for Geometrixx Outdoors site (example) -->
    <node path="/content/geometrixx-outdoors">
        <node resourceType ="foundation/components/image">
            <property name="alternateText"/>
            <property name="jcr:title" />
        </node>
        <node resourceType ="geometrixx-outdoors/components/title">
            <property name="richText"/>
        </node>
    </node>
    <!-- translation rules for ASSETS (example) -->
    <node path="/content/dam">
        <!-- configure list of metadata properties here -->
        <property name="dc:title" />
        <property name="dc:description" />
    </node>
    <!-- translation rules for extracting ASSETS from SITES content, configure all components that embed or reference assets -->
    <assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="foundation/components/video" assetReferenceAttribute="asset"/>
    <assetNode resourceType="foundation/components/download" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="foundation/components/mobileimage" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="wcm/foundation/components/image" assetReferenceAttribute="fileReference"/>
</nodelist>
```

