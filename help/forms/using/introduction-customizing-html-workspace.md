---
title: Introducción a la personalización del espacio de trabajo de formularios de AEM
seo-title: Introducción a la personalización del espacio de trabajo de formularios de AEM
description: Introducción rápida, con información conceptual y técnica, para personalizar el espacio de trabajo de LiveCycle AEM Forms para la gestión de procesos.
seo-description: Introducción rápida, con información conceptual y técnica, para personalizar el espacio de trabajo de LiveCycle AEM Forms para la gestión de procesos.
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4

---


# Introducción a la personalización del espacio de trabajo de formularios de AEM{#introduction-to-customizing-aem-form-workspace}

El espacio de trabajo de formularios de AEM ofrece funciones para modificar la semántica de presentación y la funcionalidad de su interfaz. A continuación se describen los tipos de personalizaciones para cambiar el estilo, el diseño, el formato, la marca y la funcionalidad básica.

![cu_custom_Workspace_example](assets/cu_customized_workspace_example.png)

Ejemplo de un espacio de trabajo personalizado

## Tipos de personalizaciones {#types-of-customizations}

El espacio de trabajo de AEM Forms admite una amplia variedad de personalizaciones para actualizar el diseño de la interfaz de usuario, su apariencia, funcionalidad y mucho más. Las personalizaciones implican actualizar una o varias de las siguientes opciones:

* Aspectos visuales de la interfaz de usuario
* Funcionalidad mediante personalizaciones semánticas
* Reutilización de componentes HTML en otras aplicaciones

### Cambios en la interfaz de usuario {#user-interface-changes}

Puede cambiar la apariencia, el diseño y otras formas semánticas de presentación del espacio de trabajo de AEM Forms. Cambie el espacio de trabajo personalizando los archivos CSS, HTML y JavaScript™. Todos los archivos predeterminados se proporcionan en la instalación predeterminada.

Los pasos más habituales se tratan en Pasos [genéricos para la personalización](../../forms/using/generic-steps-html-workspace-customization.md)del espacio de trabajo de AEM Forms. Para obtener ejemplos específicos de dichas personalizaciones, incluidos los pasos detallados, consulte los artículos relacionados al final de este artículo.

#### Explicación de la hoja de estilo {#understanding-the-style-sheet}

Antes de personalizar el espacio de trabajo, familiarícese con la hoja de estilo predeterminada suministrada con AEM Forms en /libs/ws/css/style.css.

Para personalizar el espacio de trabajo, se recomienda familiarizarse con la hoja de estilo existente, style.css, ubicada en la carpeta /libs/ws/css. A continuación se describen algunos componentes destacados.

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
   <td><p>.categoryList.header</p> </td>
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
   <td><p>.category:hover, .category.selected, .filter:hover, .filter.selected</p> </td>
   <td><p>Categoría seleccionada y pasar el ratón sobre el estilo de la categoría</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar.tool, categoryListBar.content</p> </td>
   <td><p>Página de inicio del proceso (lista de categorías cerradas)</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar.tool, filterListBar.content</p> </td>
   <td><p>Página Tareas pendientes (lista de filtros cerrados)</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar.tool, processNameListBar.content</p> </td>
   <td><p>Página de seguimiento (lista de nombres de proceso cerrada)</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>La lista de puntos de partida o la lista de tareas</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList.header, .tasklist.header</p> </td>
   <td><p>El encabezado de una lista de puntos de inicio o una lista de tareas</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected, .task.selected</p> </td>
   <td><p>El punto de inicio o la tarea seleccionados</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected.description, .task.selected.description</p> </td>
   <td><p>Descripción del punto de inicio o la tarea seleccionados</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>El área Tarea</p> </td>
  </tr>
  <tr>
   <td><p>#header.dropdown</p> </td>
   <td><p>Lista desplegable de usuarios en el encabezado</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>Lista desplegable de tareas de ordenación</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

El aspecto del espacio de trabajo de AEM Forms se obtiene a partir de una CSS. Al personalizar la CSS, puede cambiar la semántica de presentación del espacio de trabajo, como las fuentes, los colores, la marca y el diseño.

Los pasos de nivel superior para la personalización de CSS son:

* Cree un archivo CSS.
* Agregue elementos de estilo a esta CSS. Consulte Explicación de los estilos CSS para obtener más información.
* Actualice sus referencias en `html.jsp`.

Para ver los pasos exactos para realizar estas personalizaciones, consulte Pasos [genéricos para la personalización](../../forms/using/generic-steps-html-workspace-customization.md)del espacio de trabajo de AEM Forms. El archivo CSS enviado con el espacio de trabajo de AEM Forms se encuentra en /libs/ws/css/. Para las personalizaciones relacionadas con CSS, utilice el [paquete](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)de envío. Para ver ejemplos específicos de personalizaciones relacionadas con CSS, consulte los temas de ayuda relacionados al final de este artículo.

#### Imagen {#image}

Puede personalizar el espacio de trabajo de AEM Forms para agregar avatares de usuarios o para agregar el logotipo de su organización. Para estas personalizaciones, utilice [Enviar paquete](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

Los pasos de nivel superior para personalizar las imágenes son:

* Instale y configure WebDAV.
* Agregue nuevas imágenes.
* Agregue nuevos estilos correspondientes a las imágenes agregadas.
* Vínculo al nuevo archivo CSS del `html.jsp` archivo.

Para empezar a personalizar las imágenes en el espacio de trabajo de AEM Forms, siga los pasos [genéricos para la personalización](../../forms/using/generic-steps-html-workspace-customization.md)del espacio de trabajo de AEM Forms. Para ver ejemplos específicos de personalizaciones relacionadas con imágenes, consulte los temas de ayuda relacionados al final de este artículo.

#### Plantilla HTML {#html-template}

Las plantillas HTML ayudan a definir el aspecto y el diseño de la interfaz de usuario del espacio de trabajo. Al actualizar las plantillas HTML predeterminadas, puede personalizar la interfaz de usuario predeterminada del diseño.

Los pasos de nivel superior para las personalizaciones de la plantilla HTML son:

* En una carpeta creada por el usuario, realice copias de los archivos predeterminados necesarios.
* Agregue nuevas plantillas en la carpeta definida por el usuario.
* Realice las actualizaciones pertinentes a los archivos copiados como, por ejemplo, la ruta de la nueva plantilla.

Para ver ejemplos específicos de dichas personalizaciones, consulte los temas de ayuda que se proporcionan al final de este artículo. Elija entre el paquete [de](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) envío o el paquete [de](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)desarrolladores, según la plantilla que desee personalizar.

### Cambios semánticos {#semantic-changes}

Para modificar la funcionalidad del espacio de trabajo de AEM Forms, cambie el código fuente JavaScript. Las modificaciones en la funcionalidad principal se etiquetan como cambios semánticos. Los modelos, las vistas y las plantillas se modifican como parte del código fuente del espacio de trabajo de AEM Forms.

Los pasos de nivel superior para realizar cambios semánticos con el fin de modificar la funcionalidad del espacio de trabajo de AEM Forms son:

* En una carpeta creada por el usuario, realice copias de los archivos predeterminados correspondientes.
* Agregue nuevos modelos y vistas en la carpeta definida por el usuario.
* Realice actualizaciones relevantes como la actualización de rutas de modelos y vistas recientemente agregados en los archivos JavaScript predeterminados.
* Minimice el paquete para optimizar el rendimiento.

Para obtener más información conceptual sobre los componentes que forman parte del código fuente, consulte la [Descripción de los componentes](/help/forms/using/description-reusable-components.md)reutilizables. Para estas personalizaciones, utilice el paquete Dev.

### Componentes reutilizables {#reusable-components}

Dado que el espacio de trabajo de AEM Forms es un software basado en componentes, se puede personalizar y reutilizar fácilmente. Puede integrar fácilmente los componentes del espacio de trabajo con sus aplicaciones Web.

Para obtener más información conceptual, consulte la [Descripción de los componentes](/help/forms/using/description-reusable-components.md) reutilizables y para obtener instrucciones sobre cómo utilizar los componentes, consulte [Integración de los componentes del espacio de trabajo de AEM Forms en aplicaciones](/help/forms/using/description-reusable-components.md)web.

## Creación del código de espacio de trabajo de AEM Forms {#building-html-workspace-code}

### Paquete SDK {#sdk-package}

El paquete contiene el código fuente del espacio de trabajo de AEM Forms. El paquete está disponible en `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

Está pensado principalmente para personalizaciones, ya que proporciona la capacidad de generar:

* Paquetes CRX para perfiles de Envío, Depuración y Dev (mencionados a continuación en los paquetes [](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)CRX).
* Versión minimizada de código personalizado (para cambios semánticos).

#### Contenido de WS {#ws-content}

* client-pkg:

   * src: contiene artefactos necesarios para crear nodos CRX.
   * pom.xml: secuencia de comandos para crear paquetes de implementación para varios perfiles Paquete WS-Deploy

* client-html:

   * ensamblado: contiene zip.xml utilizado por la secuencia de comandos para crear el SDK de espacio de trabajo de AEM Forms.
   * src/main/webapp -

      * css: contiene hojas de estilo para el espacio de trabajo de AEM Forms.
      * imágenes: contiene imágenes utilizadas en el espacio de trabajo de AEM Forms.
      * js:

         * libs: contiene todas las bibliotecas de terceros utilizadas en el espacio de trabajo de AEM Forms.
         * licencias: contiene licencias para archivos HTML y JS, así como código para anteponer estas licencias a los respectivos archivos de origen.
         * minificador: se utiliza para la combinación, minimización y simplificación del código personalizado de javascript.
         * resourceJs_optimizer: se utiliza para la combinación, minimización y simplificación del código fuente de javascript.
         * resource_generator: se utiliza para generar register.js y modelcontrollerpath.js.
         * tiempo de ejecución:

            * inicializer: contiene inicializer.js utilizado para inicializar vistas de red troncal y modelos utilizados en el espacio de trabajo de AEM Forms.
            * modelos: contiene modelos de red troncal de todos los componentes presentes en el espacio de trabajo de AEM Forms.
            * rutas: contiene archivos JavaScript y archivos HTML que cargan el proceso de inicio, la realización de tareas, el seguimiento y las preferencias en el espacio de trabajo de AEM Forms.
            * services: contiene service.js utilizados en el espacio de trabajo de AEM Forms. Todas las llamadas al servidor se realizan a través de service.js.
            * plantillas: contiene todas las plantillas, es decir, archivos HTML de todas las vistas del espacio de trabajo de AEM Forms.
            * util: contiene todos los archivos de utilidad (javascript) que se utilizan en el espacio de trabajo de AEM Forms.
            * vistas: contiene vistas de red troncal de todos los componentes del espacio de trabajo de AEM Forms.
         * main.js
         * router.js
      * libs/ws: pdf.html y pluginPing.pdf se utilizan para cargar formularios PDF en el espacio de trabajo de AEM Forms y WSNextAdapter.swf se utiliza para cargar formularios SWF y guías en el espacio de trabajo de AEM Forms.
      * configuraciones regionales:

         * de-DE - Contiene translate.json para alemán.
         * en-US - Contiene translate.json para inglés.
         * fr-FR: contiene Translation.json para francés.
         * ja-JP - Contiene translate.json para japonés.
         * html.jsp: contiene código para averiguar la configuración regional actual del explorador.
      * html.jsp
      * GET.jsp




### Paquete CRX {#crx-package}

El paquete CRX se puede implementar en el repositorio de CRX™. Está disponible en `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

Este paquete se puede crear utilizando los tres perfiles que se describen a continuación.

| **Perfil** | **Descripción** | **Uso** |
|---|---|---|
| Perfil de envío | Este perfil crea un paquete CRX del menor tamaño posible mediante la minimización. Este paquete es el más eficiente. Todos los archivos JavaScript™ se combinan y minimizan en un solo archivo JS. | Utilice este perfil cuando no se requieran más cambios semánticos en los archivos JS. |
| Perfil de depuración | Este perfil crea un paquete CRX moderadamente eficiente. El tamaño del paquete es ligeramente superior al del paquete creado con el perfil de envío. Este paquete tiene la mayoría de los archivos JavaScript combinados en un solo archivo JS. | Utilice este perfil para la depuración. |
| Perfil de desarrollador | Este perfil crea un paquete CRX del mayor tamaño posible. Todos los archivos JavaScript están disponibles por separado, como en el paquete SDK. | Utilice este perfil al incorporar cambios semánticos. |

#### Perfil de envío {#ship-profile}

#### Comando {#command}

* mvn clean -P Se envía la instalación en la carpeta client-pkg del paquete de origen enviado al cliente.
* La ejecución del comando de perfil de envío solo funciona en un JVM de 64 bits.

#### Contenido de WS {#ws-content-1}

* css: contiene style.css, ie.css y jquery-ui.css.
* imágenes: contiene todas las imágenes.
* js:

   * libs:

      * requerir - Contiene required.js.
      * jqueryui: contiene jquery.ui.datepicker.ja.js.
   * tiempo de ejecución:

      * plantillas: contiene todas las plantillas, es decir, archivos HTML de todos los componentes del espacio de trabajo de AEM Forms.
   * main.js (combinado, minimizado y desacreditado).
   * Registry.js



* libs:

   * ws - Contiene pluginPing.pdf, pdf.html y WSNextAdapter.swf.

* Configuración regional: contiene .content.xml.
* configuraciones regionales:

   * de-DE - Contiene translate.json para alemán.
   * en-US - Contiene translate.json para inglés.
   * fr-FR: contiene Translation.json para francés.
   * ja-JP - Contiene translate.json para japonés.
   * html.jsp: contiene código para averiguar la configuración regional actual del explorador.

* Índice: contiene .content.xml
* profile - Contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Depurar perfil {#debug-profile}

#### Comando {#command-1}

* mvn clean -P Instalación de depuración en client-pkg
* La ejecución del comando de perfil de depuración solo funciona en JVM de 64 bits.

#### Contenido de WS {#ws-content-2}

* css: contiene style.css, ie.css y jqueri-ui.css.
* imágenes: contiene todas las imágenes.
* js:

   * libs:

      * requerir - Contiene required.js.
      * jqueryui: contiene jquery.ui.datepicker.ja.js.
   * tiempo de ejecución:

      * plantillas: contiene todas las plantillas, es decir, archivos HTML de todos los componentes del espacio de trabajo de AEM Forms.
   * main.js (combinado).
   * Registry.js



* libs:

   * ws - Contiene pluginPing.pdf, pdf.html y WSNextAdapter.swf.

* Configuración regional: contiene .content.xml.
* configuraciones regionales:

   * de-DE - Contiene translate.json para alemán.
   * en-US - Contiene translate.json para inglés.
   * fr-FR: contiene Translation.json para francés.
   * ja-JP - Contiene translate.json para japonés.
   * html.jsp: contiene código para averiguar la configuración regional actual del explorador.

* Índice: contiene .content.xml
* profile - Contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Perfil de desarrollador {#dev-profile}

#### Comando {#command-2}

mvn clean -P Instalación de Dev en client-pkg

#### Contenido de WS {#ws-content-3}

* css: contiene style.css, ie.css y jqueri-ui.css.
* imágenes: contiene todas las imágenes.
* js:

   * libs: contiene todas las bibliotecas utilizadas en el espacio de trabajo de AEM Forms.
   * requerir - Contiene required.js
   * jqueryui: contiene jquery.ui.datepicker.ja.js
   * tiempo de ejecución:

      * inicializer: contiene inicializer.js y modelcontrollerpath.js.
      * modelos: contiene modelos de todos los componentes del espacio de trabajo de AEM Forms.
      * rutas: contiene archivos JavaScript y archivos HTML que cargan el proceso de inicio, la realización de tareas, el seguimiento y las preferencias en el espacio de trabajo de AEM Forms.
      * services: contiene service.js utilizados en el espacio de trabajo de AEM Forms.
      * plantillas: contiene todas las plantillas, es decir, archivos HTML de todos los componentes del espacio de trabajo de AEM Forms.
      * util: contiene todos los archivos de utilidad (JavaScript) que se utilizan en el espacio de trabajo de AEM Forms.
      * vistas: contiene vistas de todos los componentes del espacio de trabajo de AEM Forms.
   * main.js
   * Registry.js
   * router.js


* libs:

   * ws - Contiene pluginPing.pdf, pdf.html y WSNextAdapter.swf.

* Configuración regional: contiene .content.xml.
* configuraciones regionales:

   * de-DE - Contiene translate.json para alemán.
   * en-US - Contiene translate.json para inglés.
   * fr-FR: contiene Translation.json para francés.
   * ja-JP - Contiene translate.json para japonés.
   * html.jsp: contiene código para averiguar la configuración regional actual del explorador.

* Índice: contiene .content.xml
* profile - Contiene offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
