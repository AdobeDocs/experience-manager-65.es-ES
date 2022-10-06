---
title: Introducción a Personalización de AEM espacio de trabajo del formulario
seo-title: Introduction to Customizing AEM form workspace
description: Introducción rápida, con información conceptual y técnica, para personalizar el espacio de trabajo de AEM Forms de LiveCycle para la administración de procesos.
seo-description: A quick introduction, with conceptual and technical information, to customize LiveCycle AEM Forms workspace for process management.
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
exl-id: b183d42f-343c-4acb-bc73-f80ad72e54df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---

# Introducción a Personalización de AEM espacio de trabajo del formulario{#introduction-to-customizing-aem-form-workspace}

AEM espacio de trabajo del formulario proporciona funciones para modificar la semántica de presentación y la funcionalidad de su interfaz. A continuación se describen los tipos de personalizaciones para cambiar el estilo, el diseño, el formato, la marca y la funcionalidad principal.

![cu_custom_workspace_example](assets/cu_customized_workspace_example.png)

Ejemplo de un espacio de trabajo personalizado

## Tipos de personalizaciones {#types-of-customizations}

El espacio de trabajo de AEM Forms admite una amplia variedad de personalizaciones para actualizar el diseño de la interfaz de usuario, su apariencia, funcionalidad y mucho más. Las personalizaciones implican actualizar una o más de las siguientes opciones:

* Aspectos visuales de la interfaz de usuario
* Funcionalidad mediante personalizaciones semánticas
* Reutilización de componentes de HTML en otras aplicaciones

### Cambios en la interfaz de usuario {#user-interface-changes}

Puede cambiar el aspecto, el diseño y otra semántica de presentación del espacio de trabajo de AEM Forms. Cambie el espacio de trabajo personalizando los archivos CSS, HTML y JavaScript™. Todos los archivos predeterminados se proporcionan en la instalación predeterminada.

Los pasos más aplicables se tratan en [Pasos genéricos para la personalización del espacio de trabajo de AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Para ver ejemplos específicos de dichas personalizaciones, incluidos los pasos detallados, consulte los artículos relacionados al final de este artículo.

#### Explicación de la hoja de estilo {#understanding-the-style-sheet}

Antes de personalizar el espacio de trabajo, familiarícese con la hoja de estilos predeterminada que se proporciona con AEM Forms en /libs/ws/css/style.css.

Para personalizar el espacio de trabajo, se recomienda que se familiarice con la hoja de estilo existente, style.css, ubicada en la carpeta /libs/ws/css. A continuación se describen algunos componentes destacados.

<table>
 <tbody>
  <tr>
   <th><p>Elemento CSS</p> </th>
   <th><p>Componente de interfaz de usuario modificado</p> </th>
  </tr>
  <tr>
   <td><p>#encabezado</p> </td>
   <td><p>Encabezado del espacio de trabajo de AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>Lista de categorías</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList .header</p> </td>
   <td><p>Encabezado de la lista de categorías</p> </td>
  </tr>
  <tr>
   <td><p>.categories, .filters</p> </td>
   <td><p>Espacio debajo de la lista de categorías</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>Categoría</p> </td>
  </tr>
  <tr>
   <td><p>.category:pasar el cursor, .category.selected, .filter:pasar el cursor, .filter.selected</p> </td>
   <td><p>Categoría seleccionada y pase el ratón sobre el estilo de la categoría</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool, categoryListBar .content</p> </td>
   <td><p>Página de inicio del proceso (lista de categorías cerradas)</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool, filterListBar .content</p> </td>
   <td><p>Página Para hacer (lista de filtros cerrada)</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool, processNameListBar .content</p> </td>
   <td><p>Página de seguimiento (lista de nombres de proceso cerrada)</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>La lista de puntos de inicio o la lista de tareas</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header, .tasklist .header</p> </td>
   <td><p>El encabezado de una lista de puntos de inicio o una lista de tareas</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected, .task.selected</p> </td>
   <td><p>El punto de inicio o la tarea seleccionados</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected .description, .task.selected .description</p> </td>
   <td><p>Descripción del punto de inicio o la tarea seleccionados</p> </td>
  </tr>
  <tr>
   <td><p>#área de tareas</p> </td>
   <td><p>El área Tarea</p> </td>
  </tr>
  <tr>
   <td><p>#header.dropdown</p> </td>
   <td><p>Menú desplegable de usuario en el encabezado</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>Lista desplegable Ordenar tarea</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

El aspecto del espacio de trabajo de AEM Forms toma su aspecto de una CSS. Al personalizar el CSS, puede cambiar la semántica de presentación del espacio de trabajo, como fuentes, colores, marca y diseño.

Los pasos de nivel superior para la personalización de CSS son:

* Cree un archivo CSS.
* Agregue elementos de estilo a esta CSS. Consulte Explicación de los estilos CSS para obtener más información.
* Actualizar sus referencias en `html.jsp`.

Para ver los pasos exactos para realizar estas personalizaciones, consulte [Pasos genéricos para la personalización del espacio de trabajo de AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). El archivo CSS enviado con el espacio de trabajo de AEM Forms se encuentra en /libs/ws/css/. Para las personalizaciones relacionadas con CSS, utilice la variable [Paquete de envío](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). Para ver ejemplos específicos de personalizaciones relacionadas con CSS, consulte los temas de ayuda relacionados al final de este artículo.

#### Imagen {#image}

Puede personalizar el espacio de trabajo de AEM Forms para agregar avatares de usuarios o para agregar el logotipo de su organización. Para estas personalizaciones, utilice [Paquete de envío](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

Los pasos de nivel superior para la personalización de las imágenes son:

* Instale y configure WebDAV.
* Añada nuevas imágenes.
* Añada nuevos estilos correspondientes a las imágenes añadidas.
* Vínculo al nuevo archivo CSS en `html.jsp` archivo.

Para empezar a personalizar las imágenes en el espacio de trabajo de AEM Forms, siga las instrucciones de [Pasos genéricos para la personalización del espacio de trabajo de AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Para ver ejemplos específicos de personalizaciones relacionadas con imágenes, consulte los temas de ayuda relacionados al final de este artículo.

#### plantilla de HTML {#html-template}

Las plantillas de HTML ayudan a definir el aspecto y el diseño de la interfaz de usuario del espacio de trabajo. Al actualizar las plantillas de HTML predeterminadas, puede personalizar el diseño de la interfaz de usuario predeterminada.

Los pasos de nivel superior para las personalizaciones de la plantilla de HTML son:

* En una carpeta creada por el usuario, realice copias de los archivos predeterminados necesarios.
* Añada nuevas plantillas en la carpeta definida por el usuario.
* Realice actualizaciones relevantes de los archivos copiados como, la ruta de la nueva plantilla.

Para ver ejemplos específicos de estas personalizaciones, consulte los temas de Ayuda que se proporcionan al final de este artículo. Elija entre las [Paquete de envío](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) o [Paquete de desarrollo](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), según la plantilla que se personalice.

### Cambios semánticos {#semantic-changes}

Para modificar la funcionalidad del espacio de trabajo de AEM Forms, cambie el código fuente JavaScript. Las modificaciones en la funcionalidad principal se etiquetan como cambios semánticos. Los modelos, las vistas y las plantillas se modifican como parte del código fuente del espacio de trabajo de AEM Forms.

Los pasos de nivel superior para realizar cambios semánticos con el fin de modificar la funcionalidad del espacio de trabajo de AEM Forms son:

* En una carpeta creada por el usuario, realice copias de los archivos predeterminados correspondientes.
* Añada nuevos modelos y vistas en la carpeta definida por el usuario.
* Realice actualizaciones relevantes, como la actualización de rutas de modelos y vistas recién añadidos en los archivos JavaScript predeterminados.
* Minimice el paquete para optimizar el rendimiento.

Para obtener más información conceptual sobre los componentes que forman parte del código fuente, consulte la [Descripción de los componentes reutilizables](/help/forms/using/description-reusable-components.md). Para estas personalizaciones, utilice el paquete de desarrollo.

### Componentes reutilizables {#reusable-components}

Como el espacio de trabajo de AEM Forms es un software basado en componentes, se puede personalizar y reutilizar fácilmente. Puede integrar fácilmente los componentes del espacio de trabajo con las aplicaciones web.

Para obtener más información conceptual, consulte la [Descripción de los componentes reutilizables](/help/forms/using/description-reusable-components.md) y para obtener instrucciones sobre el uso de los componentes, consulte [Integración de componentes de espacio de trabajo de AEM Forms en aplicaciones web](/help/forms/using/description-reusable-components.md).

## Creación del código de espacio de trabajo de AEM Forms {#building-html-workspace-code}

### Paquete de SDK {#sdk-package}

El paquete contiene el código fuente del espacio de trabajo de AEM Forms. El paquete está disponible en `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

Está pensado principalmente para las personalizaciones, ya que proporciona la capacidad de generar:

* Paquetes CRX para perfiles de envío, depuración y desarrollo (mencionados a continuación en [Paquetes CRX](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)).
* Versión minimizada de código personalizado (para cambios semánticos).

#### Contenido WS {#ws-content}

* client-pkg:

   * src : contiene artefactos necesarios para crear nodos CRX.
   * pom.xml: secuencia de comandos para crear paquetes de implementación para varios perfiles Paquete WS-Deploy

* client-html:

   * assembly : contiene zip.xml utilizado por el script para crear el SDK de espacio de trabajo de AEM Forms.
   * src/main/webapp -

      * css : contiene hojas de estilo para el espacio de trabajo de AEM Forms.
      * imágenes : contiene imágenes utilizadas en el espacio de trabajo de AEM Forms.
      * js:

         * libs : contiene todas las bibliotecas de terceros utilizadas en el espacio de trabajo de AEM Forms.
         * licencias : contiene licencias para archivos HTML y JS, así como código para prefijar estas licencias en los respectivos archivos de origen.
         * minificador : se utiliza para la combinación, minificación y simplificación del código personalizado de JavaScript.
         * resourcejs_optimizer : se utiliza para la combinación, minimización y simplificación del origen JavaScript.
         * resource_generator : se utiliza para generar register.js y modelcontrollerpath.js.
         * tiempo de ejecución:

            * inicializer : contiene initializer.js utilizado para inicializar las vistas de la red troncal y los modelos utilizados en el espacio de trabajo de AEM Forms.
            * modelos : contiene modelos de estructura básica de todos los componentes presentes en el espacio de trabajo de AEM Forms.
            * Rutas : contiene archivos JavaScript y archivos HTML que cargan el proceso de inicio, las tareas de finalización, el seguimiento y las preferencias en el espacio de trabajo de AEM Forms.
            * servicios : contiene service.js utilizado en el espacio de trabajo de AEM Forms. Todas las llamadas al servidor se realizan mediante service.js.
            * plantillas : contiene todas las plantillas, es decir, archivos HTML de todas las vistas del espacio de trabajo de AEM Forms.
            * util : contiene todos los archivos de utilidad (javascript) que se utilizan en el espacio de trabajo de AEM Forms.
            * vistas : contiene vistas de la estructura básica de todos los componentes del espacio de trabajo de AEM Forms.
         * main.js
         * router.js
      * libs/ws: pdf.html y pluginPing.pdf se utilizan para cargar PDF forms en el espacio de trabajo de AEM Forms y WSNextAdapter.swf se utiliza para cargar formularios y guías SWF en el espacio de trabajo de AEM Forms.
      * configuraciones regionales:

         * de-DE : contiene translation.json para alemán.
         * en-US : contiene translation.json para inglés.
         * fr-FR : contiene translation.json para francés.
         * ja-JP : contiene translation.json para japonés.
         * html.jsp : contiene código para averiguar la configuración regional actual del explorador.
      * html.jsp
      * GET.jsp




### Paquete CRX {#crx-package}

El paquete CRX se puede implementar en el repositorio CRX™. Está disponible en `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

Este paquete se puede crear utilizando los tres perfiles que se describen a continuación.

| **Perfil** | **Descripción** | **Uso** |
|---|---|---|
| Perfil de envío | Este perfil crea un paquete CRX del tamaño más pequeño posible mediante la minificación. Este paquete es el más eficiente. Todos los archivos JavaScript™ se combinan y minimizan en un solo archivo JS. | Utilice este perfil cuando no se requieran más cambios semánticos en los archivos JS. |
| Perfil de depuración | Este perfil crea un paquete CRX moderadamente eficiente. El tamaño del paquete es ligeramente superior al del paquete creado mediante el perfil de envío. Este paquete tiene la mayoría de los archivos JavaScript combinados en un solo archivo JS. | Utilice este perfil para la depuración. |
| Perfil de desarrollo | Este perfil crea un paquete CRX del mayor tamaño posible. Todos los archivos JavaScript están disponibles por separado, ya que están en el paquete SDK. | Utilice este perfil al incorporar cambios semánticos. |

#### Perfil de envío {#ship-profile}

#### Comando {#command}

* mvn clean -P Send install en la carpeta client-pkg del paquete de origen enviado al cliente.
* La ejecución del comando de perfil de envío solo funciona en una JVM de 64 bits.

#### Contenido WS {#ws-content-1}

* css: contiene style.css, ie.css y jquery-ui.css.
* imágenes : contiene todas las imágenes.
* js:

   * libs:

      * need - Contiene required.js.
      * jqueryui - Contiene jquery.ui.datepicker.ja.js.
   * tiempo de ejecución:

      * plantillas : contiene todas las plantillas, es decir, archivos HTML de todos los componentes del espacio de trabajo de AEM Forms.
   * main.js (combinado, minificado y desconfigurado).
   * registry.js



* libs:

   * ws: Contiene pluginPing.pdf, pdf.html y WSNextAdapter.swf.

* Configuración regional: contiene .content.xml.
* configuraciones regionales:

   * de-DE : contiene translation.json para alemán.
   * en-US : contiene translation.json para inglés.
   * fr-FR : contiene translation.json para francés.
   * ja-JP : contiene translation.json para japonés.
   * html.jsp : contiene código para averiguar la configuración regional actual del explorador.

* Índice: contiene .content.xml
* profile : contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Perfil de depuración {#debug-profile}

#### Comando {#command-1}

* mvn clean -P Debug install on client-pkg
* La ejecución del comando de perfil de depuración solo funciona en JVM de 64 bits.

#### Contenido WS {#ws-content-2}

* css: contiene style.css, ie.css y jqueri-ui.css.
* imágenes : contiene todas las imágenes.
* js:

   * libs:

      * need - Contiene required.js.
      * jqueryui - Contiene jquery.ui.datepicker.ja.js.
   * tiempo de ejecución:

      * plantillas : contiene todas las plantillas, es decir, archivos HTML de todos los componentes del espacio de trabajo de AEM Forms.
   * main.js (combinado).
   * registry.js



* libs:

   * ws: Contiene pluginPing.pdf, pdf.html y WSNextAdapter.swf.

* Configuración regional: contiene .content.xml.
* configuraciones regionales:

   * de-DE : contiene translation.json para alemán.
   * en-US : contiene translation.json para inglés.
   * fr-FR : contiene translation.json para francés.
   * ja-JP : contiene translation.json para japonés.
   * html.jsp : contiene código para averiguar la configuración regional actual del explorador.

* Índice: contiene .content.xml
* profile : contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Perfil de desarrollo {#dev-profile}

#### Comando {#command-2}

mvn clean -P Dev install en client-pkg

#### Contenido WS {#ws-content-3}

* css: contiene style.css, ie.css y jqueri-ui.css.
* imágenes : contiene todas las imágenes.
* js:

   * libs : contiene todas las bibliotecas utilizadas en el espacio de trabajo de AEM Forms.
   * Requisito : contiene required.js
   * jqueryui: contiene jquery.ui.datepicker.ja.js
   * tiempo de ejecución:

      * inicializer : contiene initializer.js y modelcontrollerpath.js.
      * modelos : contiene modelos de todos los componentes del espacio de trabajo de AEM Forms.
      * Rutas : contiene archivos JavaScript y archivos HTML que cargan el proceso de inicio, las tareas de finalización, el seguimiento y las preferencias en el espacio de trabajo de AEM Forms.
      * servicios : contiene service.js utilizado en el espacio de trabajo de AEM Forms.
      * plantillas : contiene todas las plantillas, es decir, archivos HTML de todos los componentes del espacio de trabajo de AEM Forms.
      * util : contiene todos los archivos de utilidad (JavaScript) que se utilizan en el espacio de trabajo de AEM Forms.
      * vistas : contiene vistas de todos los componentes del espacio de trabajo de AEM Forms.
   * main.js
   * registry.js
   * router.js


* libs:

   * ws: Contiene pluginPing.pdf, pdf.html y WSNextAdapter.swf.

* Configuración regional: contiene .content.xml.
* configuraciones regionales:

   * de-DE : contiene translation.json para alemán.
   * en-US : contiene translation.json para inglés.
   * fr-FR : contiene translation.json para francés.
   * ja-JP : contiene translation.json para japonés.
   * html.jsp : contiene código para averiguar la configuración regional actual del explorador.

* Índice: contiene .content.xml
* profile : contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
