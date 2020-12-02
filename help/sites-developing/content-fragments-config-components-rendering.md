---
title: Fragmentos de contenido Configurar componentes para procesamiento
seo-title: Fragmentos de contenido Configurar componentes para procesamiento
description: Fragmentos de contenido Configurar componentes para procesamiento
seo-description: Fragmentos de contenido Configurar componentes para procesamiento
uuid: 3f5aaf36-e6a7-4a3c-b305-e35ebcc98d0d
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2aef9048-9d6e-4f5d-b443-5e73f8066d76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 9%

---


# Fragmentos de contenido Configurar componentes para procesamiento{#content-fragments-configuring-components-for-rendering}

Existen varios [servicios avanzados](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) relacionados con la representación de fragmentos de contenido. Para utilizar estos servicios, los tipos de recursos de dichos componentes deben darse a conocer al marco de fragmentos de contenido.

Esto se lleva a cabo configurando la [Configuración del componente de fragmento de contenido del servicio OSGi](#osgi-service-content-fragment-component-configuration).

>[!CAUTION]
>
>Si no necesita los [servicios avanzados](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) que se describen a continuación, puede ignorar esta configuración.

>[!CAUTION]
>
>Al ampliar o utilizar los componentes integrados, no se recomienda cambiar la configuración.

>[!CAUTION]
>
>Puede escribir un componente desde cero que utilice únicamente la API de fragmentos de contenido, sin servicios avanzados. Sin embargo, en este caso, tendrá que desarrollar el componente para que gestione el procesamiento adecuado.
>
>Por lo tanto, se recomienda utilizar los componentes principales.

## Definición de los servicios avanzados que necesitan configuración {#definition-of-advanced-services-that-need-configuration}

Los servicios que requieren el registro de un componente son:

* Determinar las dependencias correctamente durante la publicación (es decir, asegurarse de que los fragmentos y modelos se pueden publicar automáticamente con una página si han cambiado desde la última publicación).
* Compatibilidad con fragmentos de contenido en la búsqueda de texto completo.
* Administración/administración de *contenido intermedio.*
* Administración/administración de *recursos de medios mixtos.*
* Despegue del despachante para fragmentos a los que se hace referencia (si se vuelve a publicar una página que contiene un fragmento).
* Mediante el procesamiento basado en párrafos.

Si necesita una o más de estas funciones, entonces (normalmente) es más fácil utilizar la funcionalidad lista para usar, en lugar de desarrollarla desde cero.

## Servicio OSGi - Configuración del componente de fragmento de contenido {#osgi-service-content-fragment-component-configuration}

La configuración debe enlazarse al servicio OSGi **Configuración del componente de fragmento de contenido**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más detalles.

Por ejemplo:

![cfm-01](assets/cfm-01.png)

La configuración OSGi es:

<table>
 <tbody>
  <tr>
   <td>Etiqueta</td>
   <td>Configuración de OSGi<br /> </td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td><strong>Tipo de medio</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>El tipo de recurso que se va a registrar; p. ej. <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>Propiedad Reference</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>El nombre de la propiedad que contiene la referencia al fragmento; p. ej. <code>fragmentPath</code> o <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Propiedad Element(s)</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>El nombre de la propiedad que contiene los nombres de los elementos que se van a procesar; p. ej.<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Propiedad de variación</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>El nombre de la propiedad que contiene el nombre de la variación que se va a procesar; p. ej.<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Para algunas funciones (por ejemplo, para representar solo un rango de párrafos), deberá cumplir algunas convenciones:

<table>
 <tbody>
  <tr>
   <td>Nombre de propiedad</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Una propiedad de cadena que define el rango de párrafos que se van a generar si se encuentra en <em>modo de procesamiento de un solo elemento</em>.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> o <code>1-3</code> o <code>1-3;6;7-8</code> o <code>*-3;5-*</code></li>
     <li>solo se evalúa si <code>paragraphScope</code> está establecido en <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>Una propiedad de cadena que define cómo se van a generar los párrafos si se encuentra en <em>modo de procesamiento de un solo elemento</em>.</p> <p>Valores:</p>
    <ul>
     <li><code>all</code> :: para procesar todos los párrafos</li>
     <li><code>range</code> :: para representar el rango de párrafos proporcionado por <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>Una propiedad booleana que define si los encabezados (por ejemplo, <code>h1</code>, <code>h2</code>, <code>h3</code>) se cuentan como párrafos (<code>true</code>) o no (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Esto puede cambiar en 6,5 hitos posteriores.

## Ejemplo {#example}

Como ejemplo, consulte lo siguiente (en una instancia de AEM lista para usar):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

Contiene:

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```

