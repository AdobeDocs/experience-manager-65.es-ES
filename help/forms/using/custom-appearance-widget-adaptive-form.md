---
title: Creación de apariencias personalizadas para campos de formulario adaptables
seo-title: Creación de apariencias personalizadas para campos de formulario adaptables
description: Personalice el aspecto de los componentes integrados en los formularios adaptables.
seo-description: Personalice el aspecto de los componentes integrados en los formularios adaptables.
uuid: 1aa36443-774a-49fb-b3d1-d5a2d5ff849a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: d388acef-7313-4e68-9395-270aef6ef2c6
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Creación de apariencias personalizadas para campos de formulario adaptables{#create-custom-appearances-for-adaptive-form-fields}

## Introducción {#introduction}

Los formularios adaptables aprovechan el marco [de](/help/forms/using/introduction-widgets.md) apariencia para ayudarle a crear apariencias personalizadas para los campos de formulario adaptables y ofrecer una experiencia de usuario diferente. Por ejemplo, reemplace los botones de radio y las casillas de verificación con botones de alternar o utilice complementos jQuery personalizados para restringir las entradas de los usuarios en campos como números de teléfono o ID de correo electrónico.

En este documento se explica cómo utilizar un complemento jQuery para crear estas experiencias alternativas para campos de formulario adaptables. Además, muestra un ejemplo para crear un aspecto personalizado para que el componente de campo numérico aparezca como un escalón numérico o un deslizador.

Analicemos primero los términos y conceptos clave utilizados en este artículo.

**Aspecto** Se refiere al estilo, el aspecto y la organización de varios elementos de un campo de formulario adaptable. Normalmente incluye una etiqueta, un área interactiva para proporcionar entradas, un icono de ayuda y descripciones cortas y largas del campo. La personalización del aspecto que se describe en este artículo es aplicable al aspecto del área de entrada del campo.

**Complemento** jQuery Proporciona un mecanismo estándar, basado en el marco de utilidades jQuery, para implementar un aspecto alternativo.

**ClientLib** Un sistema de bibliotecas del lado del cliente en el procesamiento del lado del cliente de AEM impulsado por código JavaScript y CSS complejo. Para obtener más información, consulte Uso de bibliotecas del lado del cliente.

**Archetype** Juego de herramientas de plantilla de proyecto Maven definido como un patrón o modelo original para proyectos Maven. Para obtener más información, consulte Introducción a los arquetipos.

**Control** de usuario Se refiere al elemento principal de una utilidad que contiene el valor del campo y se utiliza en la estructura de aspecto para enlazar la interfaz de usuario de la utilidad personalizada con el modelo de formulario adaptable.

## Pasos para crear un aspecto personalizado {#steps-to-create-a-custom-appearance}

Los pasos para crear un aspecto personalizado de alto nivel son los siguientes:

1. **Crear un proyecto**: Cree un proyecto de Maven que genere un paquete de contenido para implementarlo en AEM.
1. **Ampliar una clase** de utilidad existente: Amplíe una clase de widget existente y anule las clases requeridas.
1. **Crear una biblioteca** de cliente: Cree una `clientLib: af.customwidget` biblioteca y agregue los archivos JavaScript y CSS necesarios.

1. **Cree e instale el proyecto**: Cree el proyecto de Maven e instale el paquete de contenido generado en AEM.
1. **Actualizar el formulario** adaptable: Actualice las propiedades del campo de formulario adaptable para utilizar el aspecto personalizado.

### Creación de un proyecto {#create-a-project}

Un arquetipo determinado es un punto de partida para crear un aspecto personalizado. Los detalles del arquetipo a utilizar son los siguientes:

* **Repositorio**: https://repo.adobe.com/nexus/content/groups/public/
* **Id** de artefacto: custom-appearance-archetype
* **Id** de grupo: com.adobe.aemforms
* **Versión**: 1.0.4

Ejecute el siguiente comando para crear un proyecto local basado en el arquetipo:

`mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

El comando descarga los complementos de Maven y la información de arquetipo del repositorio, y genera un proyecto basado en la siguiente información:

* **groupId**: ID de grupo utilizado por el proyecto Maven generado
* **artiactId**: ID de artefacto utilizado por el proyecto Maven generado.
* **versión**: Versión del proyecto Maven generado.
* **paquete**: Paquete utilizado para la estructura de archivos.
* **artiactName**: Nombre de artefacto del paquete AEM generado.
* **packageGroup**: Grupo de paquetes del paquete AEM generado.
* **widgetName**: Nombre de aspecto utilizado como referencia.

El proyecto generado tiene la siguiente estructura:

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### Ampliación de una clase de utilidad existente {#extend-an-existing-widget-class}

Una vez creada la plantilla de proyecto, realice los siguientes cambios, según sea necesario:

1. Incluya la dependencia del complemento de terceros en el proyecto.

   1. Coloque los complementos de jQuery personalizados o de terceros en la `jqueryplugin/javascript` carpeta y los archivos CSS relacionados en la `jqueryplugin/css` carpeta. Para obtener más información, consulte los archivos JS y CSS de la `jqueryplugin/javascript and jqueryplugin/css` carpeta.

   1. Modifique los archivos `js.txt` y `css.txt` para incluir cualquier archivo JavaScript y CSS adicional del complemento jQuery.

1. Integre el complemento de terceros con la estructura para habilitar la interacción entre la estructura de aspecto personalizada y el complemento jQuery. La nueva utilidad solo funcionará después de ampliar o anular las siguientes funciones.

<table>
 <tbody>
  <tr>
   <td><strong>Función</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>La función de procesamiento devuelve el objeto jQuery para el elemento HTML predeterminado del widget. El elemento HTML predeterminado debe ser de tipo seleccionable. Por ejemplo, <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code>y <code>&lt;li&gt;</code>. El elemento devuelto se usa como <code>$userControl</code>. Si la restricción <code>$userControl</code> especifica la anterior, las funciones de la <code>AbstractWidget</code> clase funcionan según lo esperado, de lo contrario, algunas de las API comunes (enfoque, clic) requieren cambios. </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>Devuelve un mapa para convertir eventos HTML en eventos XFA. <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> Este ejemplo muestra que <code>blur</code> es un evento HTML y <code>XFA_EXIT_EVENT</code> es el evento XFA correspondiente. </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>Devuelve un mapa que proporciona detalles sobre la acción que se debe realizar al cambiar una opción. Las claves son las opciones que se proporcionan al widget y los valores son funciones a las que se llama cada vez que se detecta un cambio en la opción. La utilidad proporciona controladores para todas las opciones comunes (excepto <code>value</code> y <code>displayValue</code>).</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>La estructura de la utilidad jQuery carga la función cada vez que se guarda el valor de la utilidad jQuery en el modelo XFA (por ejemplo, en el suceso exit de un campo de texto). La implementación debe devolver el valor guardado en la utilidad. El controlador se proporciona con el nuevo valor para la opción.</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>De forma predeterminada, en XFA cuando se produce el suceso enter, se muestra el nombre <code>rawValue</code> del campo. Se llama a esta función para mostrar al usuario <code>rawValue</code> . </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>De forma predeterminada, en XFA cuando se produce un evento exit, se muestra el nombre <code>formattedValue</code> del campo. Se llama a esta función para mostrar al usuario <code>formattedValue</code> . </td>
  </tr>
 </tbody>
</table>

1. Actualice el archivo JavaScript de la `integration/javascript` carpeta según sea necesario.

   * Reemplace el texto `__widgetName__` con el nombre real del widget.
   * Extienda la utilidad desde una clase de utilidad lista para usar adecuada. En la mayoría de los casos, es la clase de widget que corresponde al widget existente que se está reemplazando. El nombre de clase principal se utiliza en varias ubicaciones, por lo que se recomienda buscar todas las instancias de la cadena `xfaWidget.textField` en el archivo y reemplazarlas por la clase principal real utilizada.
   * Amplíe el `render` método para proporcionar una IU alternativa. Es la ubicación desde la que se invocará el complemento jQuery para actualizar la interfaz de usuario o el comportamiento de la interacción. El `render` método debe devolver un elemento de control de usuario.

   * Amplíe el `getOptionsMap` método para anular cualquier opción que se vea afectada por un cambio en la utilidad. La función devuelve una asignación que proporciona detalles para la acción que se realizará al cambiar una opción. Las claves son las opciones proporcionadas al widget y los valores son las funciones a las que se llama cada vez que se detecta un cambio en la opción.
   * El `getEventMap` método asigna eventos activados por la utilidad, con los eventos requeridos por el modelo de formulario adaptable. El valor predeterminado asigna eventos HTML estándar para la utilidad predeterminada y debe actualizarse si se activa un evento alternativo.
   * La cláusula de visualización `showDisplayValue` `showValue` y aplicación de la cláusula de visualización y edición de imagen y se puede anular para tener un comportamiento alternativo.

   * El marco de formularios adaptables llama al `getCommitValue` método cuando se produce el `commit`suceso. Generalmente, es el evento exit, excepto para los elementos de lista desplegable, botón de radio y casilla de verificación donde se produce al cambiar. Para obtener más información, consulte Expresiones [de formularios](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p)adaptables.

   * El archivo de plantilla proporciona implementación de muestra para varios métodos. Elimine los métodos que no se van a ampliar.

### Creación de una biblioteca de cliente {#create-a-client-library}

El proyecto de muestra generado por el arquetipo Maven crea automáticamente las bibliotecas de cliente necesarias y las envuelve en una biblioteca de cliente con una categoría `af.customwidgets`. Los archivos JavaScript y CSS disponibles en el `af.customwidgets` se incluyen automáticamente durante la ejecución.

### Generar e instalar {#build-and-install}

Para crear el proyecto, ejecute el siguiente comando en el shell para generar un paquete CRX que debe instalarse en el servidor AEM.

`mvn clean install`

>[!NOTE]
>
>El proyecto principal hace referencia a un repositorio remoto dentro del archivo POM. Esto es sólo con fines de referencia y, según los estándares Maven, la información del repositorio se captura en el `settings.xml` archivo.

### Actualizar el formulario adaptable {#update-the-adaptive-form}

Para aplicar el aspecto personalizado a un campo de formulario adaptable:

1. Abra el formulario adaptable en modo de edición.
1. Abra el cuadro de diálogo **Propiedad** del campo en el que desea aplicar el aspecto personalizado.
1. En la ficha **Estilo** , actualice la propiedad `CSS class` para agregar el nombre de aspecto en el `widget_<widgetName>` formato. Por ejemplo: **widget_numericstep**

## Ejemplo: Crear un aspecto personalizado {#sample-create-a-custom-appearance-nbsp}

Veamos ahora un ejemplo para crear un aspecto personalizado para que un campo numérico aparezca como un paso numérico o un deslizador. Siga estos pasos:

1. Ejecute el siguiente comando para crear un proyecto local basado en el arquetipo Maven:

   `mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   Le solicita que especifique valores para los parámetros siguientes.
   *Los valores utilizados en esta muestra se resaltan en negrita*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. Vaya al directorio `customWidgets` (valor especificado para la `artifactID` propiedad) y ejecute el siguiente comando para generar un proyecto Eclipse:

   `mvn eclipse:eclipse`

1. Abra la herramienta Eclipse y haga lo siguiente para importar el proyecto Eclipse:

   1. Seleccione **[!UICONTROL Archivo > Importar > Proyectos existentes en Workspace]**.

   1. Busque y seleccione la carpeta en la que ejecutó el `archetype:generate` comando.

   1. Click **[!UICONTROL Finish]**.

      ![captura de pantalla de eclipse](assets/eclipse-screenshot.png)

1. Seleccione la utilidad que se utilizará para la apariencia personalizada. En este ejemplo se utiliza el siguiente widget numérico de pasos:

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   En el proyecto Eclipse, revise el código del complemento en el `plugin.js` archivo para asegurarse de que coincide con los requisitos del aspecto. En este ejemplo, la apariencia cumple los siguientes requisitos:

   * El paso numérico debería extenderse desde `- $.xfaWidget.numericInput`.
   * El `set value` método de la utilidad establece el valor después de que el enfoque esté en el campo. Es un requisito obligatorio para un widget de formulario adaptable.
   * El `render` método debe sobrescribirse para invocar el `bootstrapNumber` método.

   * No hay dependencia adicional para el complemento que no sea el código fuente principal del complemento.
   * El ejemplo no realiza ningún estilo en el componente, por lo que no se requiere CSS adicional.
   * El `$userControl` objeto debe estar disponible para el `render` método. Es un campo del `text` tipo que se clona con el código del complemento.

   * Los botones **+** y **-** deben desactivarse cuando el campo está desactivado.

1. Reemplace el contenido del `bootstrap-number-input.js` (complemento jQuery) con el contenido del `numericStepper-plugin.js` archivo.
1. En el `numericStepper-widget.js` archivo, agregue el siguiente código para anular el método de procesamiento para invocar el complemento y devolver el `$userControl` objeto:

   ```java
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. En el `numericStepper-widget.js` archivo, anule la `getOptionsMap` propiedad para anular la opción de acceso y oculte los botones + y - en modo desactivado.

   ```java
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. Guarde los cambios, vaya a la carpeta que contiene el `pom.xml` archivo y ejecute el siguiente comando Maven para crear el proyecto:

   `mvn clean install`

1. Instale el paquete mediante el Administrador de paquetes de AEM.

1. Abra el formulario adaptable en modo de edición en el que desea aplicar el aspecto personalizado y haga lo siguiente:

   1. Haga clic con el botón secundario en el campo en el que desea aplicar el aspecto y haga clic en **[!UICONTROL Editar]** para abrir el cuadro de diálogo Editar componente.

   1. En la ficha Estilo, actualice la propiedad de clase **** CSS para agregar `widget_numericStepper`.

La nueva apariencia que acaba de crear ahora está disponible para su uso.
