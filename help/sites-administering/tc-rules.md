---
title: Identificación del contenido para traducir
seo-title: Identificación del contenido para traducir
description: Aprenda a identificar el contenido que necesita traducción.
seo-description: Aprenda a identificar el contenido que necesita traducción.
uuid: 81b9575c-1c7a-4955-b03f-3f26cbd4f956
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: eedff940-4a46-4c24-894e-a5aa1080d23d
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Identificación del contenido para traducir{#identifying-content-to-translate}

Las reglas de traducción identifican el contenido que se va a traducir para las páginas, los componentes y los recursos que se incluyen o excluyen de los proyectos de traducción. Cuando se traduce una página o un recurso, AEM extrae este contenido para que se pueda enviar al servicio de traducción.

Las páginas y los recursos se representan como nodos en el repositorio JCR. El contenido extraído es uno o varios valores de propiedad de los nodos. Las reglas de traducción identifican las propiedades que contienen el contenido que se va a extraer.

Las reglas de traducción se expresan en formato XML y se almacenan en estas ubicaciones posibles:

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

El archivo se aplica a todos los proyectos de traducción.

>[!NOTE]
>
>Después de una actualización a 6.4, se recomienda mover el archivo de /etc. Consulte Reestructuración [común de repositorios en AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules) para obtener más información.

Las reglas incluyen la siguiente información:

* Ruta del nodo al que se aplica la regla. La regla también se aplica a los descendientes del nodo.
* Nombres de las propiedades de nodo que contienen el contenido que se va a traducir. La propiedad puede ser específica de un tipo de recurso específico o de todos los tipos de recurso.

Por ejemplo, puede crear una regla que traduzca el contenido que los autores añaden a todos los componentes de texto de base de AEM de sus páginas. La regla puede identificar el `/content` nodo y la `text` propiedad del `foundation/components/text` componente.

Se ha agregado una [consola](#translation-rules-ui) para configurar las reglas de traducción. Las definiciones de la interfaz de usuario le rellenarán el archivo.

Para obtener una descripción general de las funciones de traducción de contenido en AEM, consulte [Traducción de contenido para sitios](/help/sites-administering/translation.md)multilingües.

>[!NOTE]
>
>AEM admite la asignación uno a uno entre los tipos de recursos y los atributos de referencia para la traducción del contenido al que se hace referencia en una página.

## Sintaxis de regla para páginas, componentes y recursos {#rule-syntax-for-pages-components-and-assets}

Una regla es un `node` elemento con uno o más elementos secundarios `property` y cero o más elementos secundarios `node` :

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

Cada uno de estos `node` elementos tiene las características siguientes:

* El `path` atributo contiene la ruta al nodo raíz de la rama a la que se aplican las reglas.
* Los elementos secundarios `property` identifican las propiedades del nodo que se van a traducir para todos los tipos de recursos:

   * El `name` atributo contiene el nombre de la propiedad.
   * El `translate` atributo opcional es igual `false` si la propiedad no está traducida. By default the value is `true`. Este atributo resulta útil al anular reglas anteriores.

* Los elementos secundarios `node` identifican las propiedades de nodo que se van a traducir para tipos de recursos específicos:

   * El `resourceType` atributo contiene la ruta que responde al componente que implementa el tipo de recurso.
   * Los `property` elementos secundarios identifican la propiedad node que se va a traducir. Utilice este nodo del mismo modo que los elementos secundarios `property` para las reglas de nodo.

La regla de ejemplo siguiente hace que el contenido de todas `text` las propiedades se traduzca para todas las páginas debajo del `/content` nodo. La regla es eficaz para cualquier componente que almacene contenido en una `text` propiedad, como el componente de base Texto y el componente de base Imagen.

```xml
<node path="/content">
          <property name="text"/>
</node>
```

En el siguiente ejemplo se traduce el contenido de todas `text` las propiedades y también otras propiedades del componente de base Imagen. Si otros componentes tienen propiedades con el mismo nombre, la regla no se les aplica.

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

Utilice la siguiente sintaxis de regla para incluir recursos incrustados o a los que se hace referencia desde componentes:

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

Cada `assetNode` elemento tiene las características siguientes:

* Un `resourceType` atributo que es igual a la ruta que se resuelve en el componente.
* Un `assetReferenceAttribute` atributo igual al nombre de la propiedad que almacena el binario de recursos (para recursos incrustados) o la ruta al recurso al que se hace referencia.

El siguiente ejemplo extrae imágenes del componente de base Imagen:

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## Anulación de reglas {#overriding-rules}

El archivo Translation_rules.xml consta de un `nodelist` elemento con varios `node` elementos secundarios. AEM lee la lista de nodos de arriba a abajo. Cuando varias reglas segmentan el mismo nodo, se utiliza la regla inferior del archivo. Por ejemplo, las siguientes reglas hacen que se traduzca todo el contenido de `text` las propiedades, excepto la rama de las `/content/mysite/en` páginas:

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

Puede filtrar nodos que tengan una propiedad específica mediante un `filter` elemento.

Por ejemplo, las siguientes reglas hacen que se traduzca todo el contenido de `text` las propiedades, excepto los nodos que tienen la propiedad `draft` establecida en `true`.

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

1. Vaya a **Herramientas** y, a continuación, a **General**.

   ![chlimage_1-55](assets/chlimage_1-55.jpeg)

1. Seleccione Configuración **de traducción**.

   ![chlimage_1-56](assets/chlimage_1-56.jpeg)

Desde aquí puede **añadir contexto**. Esto le permite agregar una ruta.

![chlimage_1-57](assets/chlimage_1-57.jpeg)

A continuación, debe seleccionar el contexto y, a continuación, hacer clic en **Editar**. Se abrirá el Editor de reglas de traducción.

![chlimage_1-58](assets/chlimage_1-58.jpeg)

Hay 4 atributos que puede cambiar mediante la interfaz de usuario: `isDeep`, `inherit`, `translate` y `updateDestinationLanguage`.

**isDeep** Este atributo se aplica a los filtros de nodo y es true de forma predeterminada. Comprueba si el nodo (o sus antecesores) contiene esa propiedad con el valor de propiedad especificado en el filtro. Si es false, solo comprueba en el nodo actual.

Por ejemplo, los nodos secundarios se agregan a un trabajo de traducción incluso cuando el nodo principal tiene la propiedad `draftOnly` establecida en true para marcar el contenido de borrador. Aquí `isDeep` entra en juego y comprueba si los nodos principales tienen una propiedad `draftOnly` como true y excluye esos nodos secundarios.

En el Editor, puede marcar o desmarcar **Es profundo** en la ficha **Filtros** .

![chlimage_1-59](assets/chlimage_1-59.jpeg)

A continuación se muestra un ejemplo del XML resultante cuando **Is Deep** no está marcado en la interfaz de usuario:

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**inherit** Esto se aplica a las propiedades. De forma predeterminada, todas las propiedades se heredan, pero si desea que una propiedad no se herede en el elemento secundario, puede marcar esa propiedad como falsa para que se aplique solamente en ese nodo específico.

En la interfaz de usuario, puede marcar o desmarcar **Heredar** en la ficha **Propiedades** .

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**translate** El atributo translate se utiliza simplemente para especificar si se traduce o no una propiedad.

En la interfaz de usuario, puede marcar o desmarcar **Traducir** en la ficha **Propiedades** .

**updateDestinationLanguage** Este atributo se utiliza para propiedades que no tienen texto sino códigos de idioma, por ejemplo jcr:language. El usuario no está traduciendo texto, sino la configuración regional del idioma de origen a destino. Estas propiedades no se envían para su traducción.

En la interfaz de usuario, puede marcar o desmarcar **Traducir** en la ficha **Propiedades** , pero para las propiedades específicas que tienen códigos de idioma como valor.

Para ayudar a aclarar la diferencia entre `updateDestinationLanguage` y `translate`, aquí hay un ejemplo sencillo de un contexto con solo dos reglas:

![chlimage_1-61](assets/chlimage_1-61.jpeg)

El resultado en el xml será el siguiente:

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## Edición manual del archivo de reglas {#editing-the-rules-file-manually}

El archivo Translation_rules.xml que se instala con AEM contiene un conjunto predeterminado de reglas de traducción. Puede editar el archivo para satisfacer los requisitos de sus proyectos de traducción. Por ejemplo, puede agregar reglas para que se traduzca el contenido de los componentes personalizados.

Si edita el archivo Translation_rules.xml, mantenga una copia de seguridad en un paquete de contenido. La instalación de los Service Packs de AEM o la reinstalación de determinados paquetes de AEM pueden reemplazar el archivo actual Translation_rules.xml por el original. Para restaurar las reglas en esta situación, puede instalar el paquete que contiene la copia de seguridad.

>[!NOTE]
>
>Después de crear el paquete de contenido, vuelva a compilarlo cada vez que edite el archivo.

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

