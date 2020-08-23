---
title: Creación de apariencias personalizadas en formularios HTML5
seo-title: Creación de apariencias personalizadas en formularios HTML5
description: Puede conectar utilidades personalizadas a un Forms móvil. Puede ampliar los widgets de jQuery existentes o desarrollar sus propios widgets personalizados.
seo-description: Puede conectar utilidades personalizadas a un Forms móvil. Puede ampliar los widgets de jQuery existentes o desarrollar sus propios widgets personalizados.
uuid: a9013c3d-20c7-45c9-be24-8e9d4525eff8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 17a86543-30d3-4e16-a373-67b46d551da9
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---


# Creación de apariencias personalizadas en formularios HTML5{#create-custom-appearances-in-html-forms}

Puede conectar utilidades personalizadas a un Forms móvil. Puede ampliar las utilidades de jQuery existentes o desarrollar sus propias utilidades personalizadas mediante el marco de apariencias. El motor XFA utiliza varios widgets; consulte Marco de [apariencia para formularios](/help/forms/using/introduction-widgets.md) adaptables y HTML5 para obtener información detallada.

![Ejemplo de utilidad predeterminada y personalizada](assets/custom-widgets.jpg)

Ejemplo de utilidad predeterminada y personalizada

## Integración de widgets personalizados con formularios HTML5 {#integrating-custom-widgets-with-html-forms}

### Crear un perfil  {#create-a-profile-nbsp}

Puede crear un perfil o elegir un perfil existente para agregar un widget personalizado. Para obtener más información sobre la creación de perfiles, consulte [Creación de Perfiles](/help/forms/using/custom-profile.md)personalizados.

### Creación de una utilidad {#create-a-widget}

Los formularios HTML5 proporcionan una implementación de la estructura de utilidades que se puede ampliar para crear nuevas utilidades. La implementación es una utilidad jQuery *abstractWidget* que se puede ampliar para escribir una nueva utilidad. La nueva utilidad solo puede funcionar si amplía o anula las funciones mencionadas a continuación.

<table>
 <tbody>
  <tr>
   <td>Función/Clase</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td>procesar</td>
   <td>La función de procesamiento devuelve el objeto jQuery para el elemento HTML predeterminado del widget. El elemento HTML predeterminado debe ser de tipo seleccionable. Por ejemplo, &lt;a&gt;, &lt;input&gt; y &lt;li&gt;. El elemento devuelto se usa como $userControl. Si $userControl especifica la restricción anterior, las funciones de la clase AbstractWidget funcionan según lo esperado; de lo contrario, algunas de las API comunes (focus, click) requieren cambios. </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>Devuelve un mapa para convertir eventos HTML en eventos XFA. <br /> {<br /> desenfocar: XFA_EXIT_EVENTO,<br /> }<br /> Este ejemplo muestra que el desenfoque es un evento HTML y XFA_EXIT_EVENTO es el evento XFA correspondiente. </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>Devuelve un mapa que proporciona detalles sobre qué acción realizar al cambiar una opción. Las claves son las opciones que se proporcionan al widget y los valores son las funciones a las que se llama cada vez que se detecta un cambio en esa opción. La utilidad proporciona controladores para todas las opciones comunes (excepto value y displayValue)</td>
  </tr>
  <tr>
   <td>getCommitValue</td>
   <td>La estructura Widget carga la función cada vez que se guarda el valor de la utilidad en el modelo XFAM (por ejemplo, en el evento de salida de un objeto textField). La implementación debe devolver el valor guardado en la utilidad. El controlador se proporciona con el nuevo valor para la opción.</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>De forma predeterminada, en XFA en el evento enter, se muestra el valor rawValue del campo. Se llama a esta función para mostrar el valor de rawValue al usuario. </td>
  </tr>
  <tr>
   <td>showDisplayValue</td>
   <td>De forma predeterminada, en XFA en el evento de salida, se muestra el valor formateado del campo. Se llama a esta función para mostrar el formattedValue al usuario. </td>
  </tr>
 </tbody>
</table>

Para crear su propia utilidad, en el perfil creado anteriormente, incluya referencias del archivo JavaScript que contiene funciones sustituidas y funciones recientemente agregadas. Por ejemplo, *sliderNumericFieldWidget* es una utilidad para campos numéricos. Para utilizar la utilidad en el perfil en la sección del encabezado, incluya la línea siguiente:

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### Registro de utilidades personalizadas con el motor de secuencias de comandos XFA  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

Cuando el código de la utilidad personalizada esté listo, registre la utilidad con el motor de secuencias de comandos mediante `registerConfig`API para [Form Bridge](/help/forms/using/form-bridge-apis.md). Toma widgetConfigObject como entrada.

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

La configuración de la utilidad se proporciona como un objeto JSON (una colección de pares de valor clave) donde la clave identifica los campos y el valor representa la utilidad que se utilizará con esos campos. Se muestra una configuración de ejemplo:

```
*{*

*“identifier1” : “customwidgetname”,
“identifier2” : “customwidgetname2”,
..
}*
```

donde &quot;identificador&quot; es un selector CSS de jQuery que representa un campo en particular, un conjunto de campos de un tipo en particular o todos los campos. La siguiente lista el valor del identificador en diferentes casos:

| Tipo de identificador | Identificador | Descripción |
|---|---|---|
| Campo particular con nombre de campo | Identificador:&quot;div.fieldname&quot; | Todos los campos con el nombre ‘nombre de campo’ se representan con la utilidad. |
| Todos los campos de tipo ‘type’(donde type es NumericField, DateField, etc.): | Identificador: &quot;div.type&quot; | Para Campo de tiempo y Campo de tiempo, el tipo es campo de texto, ya que estos campos no son compatibles. |
| Todos los campos | Identificador: &quot;div.field&quot; |  |
