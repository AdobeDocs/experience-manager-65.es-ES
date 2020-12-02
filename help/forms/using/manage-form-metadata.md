---
title: Administrar metadatos de formulario
seo-title: Administrar metadatos de formulario
description: Los metadatos facilitan la categorización y organización de los recursos y ayudan a los usuarios que buscan un recurso específico.
seo-description: Los metadatos facilitan la categorización y organización de los recursos y ayudan a los usuarios que buscan un recurso específico.
uuid: d982df6f-a256-4bad-868f-74fcd08350f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: ba571f8e-8bd3-48eb-82e1-c93b14ffe44a
docset: aem65
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503
workflow-type: tm+mt
source-wordcount: '1994'
ht-degree: 1%

---


# Administrar metadatos de formulario{#manage-form-metadata}

## Información general  {#overview-nbsp}

Los metadatos facilitan la categorización y organización de los recursos y ayudan a los usuarios que buscan un recurso específico.

De forma predeterminada, AEM Forms proporciona un conjunto definido de metadatos para cada tipo de recurso. Más allá de los metadatos predeterminados, puede agregar metadatos personalizados a cada uno de los tipos de recursos. AEM Forms también le proporciona los medios adecuados para crear, administrar e intercambiar todos estos metadatos de forma eficaz en los formularios.

Si es desarrollador o propietario de un sitio, puede personalizar Forms Portal, la interfaz de usuario final de AEM Forms para que refleje los metadatos que utiliza en su organización. Para obtener más información sobre Forms Portal, consulte [Introducción a la publicación de formularios en un portal](../../forms/using/introduction-publishing-forms.md).

## Metadatos en AEM Forms {#metadata-in-aem-forms}

En AEM Forms, la lista de las propiedades de metadatos asociadas a un recurso depende de su tipo. Además, si agrega una propiedad de metadatos personalizada, se agrega a todos los recursos del tipo en el que se agregaron los metadatos personalizados.

### Tipos de recursos {#asset-types}

AEM Forms admite los siguientes tipos de recursos:

* Plantillas de formulario (formularios XFA)
* PDF forms
* Documento (archivos PDF planos)
* Formularios adaptables
* Medios
* XFS

#### Gran lista de metadatos {#extensive-list-of-metadata}

A continuación se muestra una extensa lista de propiedades de metadatos admitidas en AEM Forms:

<table>
 <tbody> 
  <tr> 
   <td><strong>Nombre de la propiedad </strong></td> 
   <td><strong>Tipo de recurso</strong></td> 
   <td><strong>Descripción</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>Título</td> 
   <td>Todos excepto el recurso</td> 
   <td>Nombre para mostrar del formulario.<br /> </td> 
  </tr> 
  <tr> 
   <td>Descripción</td> 
   <td>Todos excepto el recurso</td> 
   <td>Descripción del formulario. El usuario puede especificar este valor.<br /> </td> 
  </tr> 
  <tr> 
   <td>Tipo</td> 
   <td>Todos</td> 
   <td><p>Un valor de sólo lectura que especifica el tipo de recurso. Puede tener uno de los siguientes valores:</p> 
    <ul> 
     <li>Plantilla de formulario</li> 
     <li>Formulario PDF, formulario PDF (Acrobat) o formulario PDF (Firmado)</li> 
     <li>Documento, Documento (Firmado)</li> 
     <li>Formulario adaptable</li> 
     <li>Medio</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Creado</td> 
   <td>Todos</td> 
   <td>Un valor de sólo lectura que especifica la hora de creación de recursos.</td> 
  </tr> 
  <tr> 
   <td>Fecha de la última modificación</td> 
   <td>Todos</td> 
   <td>Un valor de sólo lectura que especifica la hora en que se modificó el recurso por última vez.</td> 
  </tr> 
  <tr> 
   <td>Autor</td> 
   <td>Todos excepto el recurso</td> 
   <td><p>Valor de sólo lectura que se calcula automáticamente en función del tipo de formulario.</p> 
    <ul> 
     <li>DOCUMENTO/plantilla de PDF/formulario: recuperado del archivo binario cargado.</li> 
     <li>Formulario adaptable: se ha iniciado sesión de usuario en el momento de la creación del formulario.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Estado</td> 
   <td>Todos excepto el recurso</td> 
   <td><p> Un valor de sólo lectura que define uno de los siguientes estados de un formulario:</p> 
    <ul> 
     <li>Sin valor: Si un formulario nunca se ha publicado.</li> 
     <li>Publicado: Cuando se publica un formulario.</li> 
     <li>Modificado: Cuando se modifica un formulario después de publicarse una vez.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Fecha de la última publicación</td> 
   <td>Todos excepto el recurso</td> 
   <td>Un valor de sólo lectura que especifica la hora en la que se publicó por última vez el formulario.</td> 
  </tr> 
  <tr> 
   <td>Tiempo de activación/desactivación de la publicación</td> 
   <td>Todos excepto el recurso</td> 
   <td><p>Hora en la que se ha programado la publicación/cancelación automática del formulario. El usuario establece este valor en la edición de metadatos.</p> 
    <ul> 
     <li>Las horas de activación y desactivación de la publicación deben superar la fecha actual. </li> 
     <li>El tiempo de desactivación de la publicación debe superar el tiempo de activación de la publicación. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>Enviar URL</td> 
   <td><p>Plantilla de formulario</p> <p>formulario en PDF</p> </td> 
   <td><p>Para configurar una dirección URL especificada por el usuario para enviar datos de formulario a un servlet.</p> <p>La dirección URL de envío se puede configurar mediante cualquiera de los siguientes métodos, enumerados en orden de prioridad:</p> 
    <ul> 
     <li>Especifique una URL de envío directamente en una plantilla de formulario mediante el botón Enviar HTTP al crear un formulario XFA en AEM Forms Designer.</li> 
     <li>En la interfaz de usuario de AEM Forms, seleccione un formulario y especifique una URL de envío al editar las propiedades de metadatos.</li> 
     <li>En Forms Portal, edite el componente Buscar y listado y especifique una URL de envío en la ficha Vínculo de formulario.</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>PERFIL de procesamiento HTML</td> 
   <td>Plantilla de formulario</td> 
   <td>El perfil de procesamiento HTML utilizado al procesar una plantilla de formulario en formato HTML.</td> 
  </tr> 
  <tr> 
   <td>Formato de procesamiento</td> 
   <td><p>Plantilla de formulario</p> <p>Formulario adaptable</p> </td> 
   <td><p>Esta opción permite al usuario especificar el formato de procesamiento del formulario cuando se publican los formularios:</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>Ambas</li> 
    </ul> <p>Esta opción se utiliza para restringir el formato de procesamiento de los formularios únicamente en el portal de formularios, donde el usuario final los puede ver.</p> </td> 
  </tr> 
  <tr> 
   <td>Etiquetas</td> 
   <td>Todos excepto el recurso</td> 
   <td>Etiquetas asociadas al formulario para facilitar una búsqueda rápida y sencilla.</td> 
  </tr> 
  <tr> 
   <td>Referencias</td> 
   <td><p>Formulario adaptable</p> <p>Plantilla de formulario</p> <p>Medio</p> </td> 
   <td><p>Lista de recursos (otros formularios o recursos) a los que está relacionado este formulario. Estos recursos se pueden incluir en las dos categorías siguientes:</p> 
    <ul> 
     <li>Se refiere a: Recursos a los que se refiere el formulario actual.</li> 
     <li>Denominado por: Recursos que hacen referencia al activo actual.</li> 
    </ul> <p>Estos recursos se muestran como vínculos y se puede acceder a sus metadatos directamente haciendo clic en ellos.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Selección del modelo de formulario (XDP/XSD)</td> 
   <td>Formulario adaptable</td> 
   <td><p>Especifica qué modelo de formulario se utiliza durante la creación del formulario adaptable. Esta propiedad puede tener los siguientes valores:</p> 
    <ul> 
     <li>Plantilla de formulario: Se selecciona una plantilla de formulario entre las existentes en el repositorio. Este valor se puede actualizar.</li> 
     <li>ESQUEMA XML: Se carga un archivo XSD. Este valor se puede actualizar.</li> 
     <li>Ninguna</li> 
    </ul> 
    <div>
      Un modelo de formulario una vez seleccionado se puede actualizar pero no eliminar. 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## Metadatos del formulario de vista {#view-form-metadata}

Los recursos tienen valores de propiedad existentes, que se pueden ver en modo de solo lectura. Estos metadatos se originan en el momento de la carga o creación del formulario.

1. Navegue hasta la ubicación del recurso para el que desea realizar la vista de metadatos.

1. Abra la página de propiedades de una de las siguientes maneras:

   1. Haga clic en el icono Propiedades de la Vista ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) en Acciones rápidas.

      >[!NOTE]
      >
      >Acciones rápidas son los elementos de acción que se muestran sobre una miniatura al pasar el ratón por encima.

   1. Seleccione el formulario y haga clic en el icono Propiedades de la Vista ![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png) que aparece en la barra de herramientas.
   1. Vaya a la página de detalles del formulario haciendo clic en la miniatura del formulario cuando no se encuentra en el modo de selección. A continuación, haga clic en el icono del ojo ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) situado en la parte superior derecha y, a continuación, haga clic en Propiedades en la lista situada debajo.

1. La página de propiedades que se abre muestra un esquema que contiene solo las propiedades de metadatos que contienen algún valor.

   La página de propiedades tiene una barra de herramientas que contiene dos iconos de acción:

   * Editar: ![aem6forms_edit](assets/aem6forms_edit.png) Editar los valores de las propiedades de metadatos
   * Vista: ![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png) Navegue hasta la página de detalles del formulario, que abre el formulario en modo de previsualización.

   La parte de contenido se divide en dos partes:

   * El panel izquierdo contiene una miniatura del formulario
   * El panel derecho contiene propiedades de metadatos en el modo de solo lectura, distribuidas en varias fichas.


## Añadir/actualizar valores de metadatos de formulario {#add-update-form-metadata-values}

Puede editar el valor de las propiedades de metadatos existentes o agregar nuevos valores a un campo de propiedad de metadatos existente (por ejemplo, cuando un campo de metadatos está en blanco).

### Actualizar valores de propiedades de metadatos {#update-metadata-property-values}

1. Siga los pasos mencionados en la sección anterior para abrir la página de propiedades donde se pueden ver los metadatos existentes del formulario seleccionado.

1. En la barra de herramientas, haga clic en el icono de edición ![aem6forms_edit](assets/aem6forms_edit.png) para cambiar el modo de la página de sólo lectura a lectura y escritura.

1. La página de propiedades que se abre contiene un esquema que contiene una combinación de campos de entrada editables y texto estático.

1. Las propiedades que se muestran en el texto estático son las que no se pueden editar.

1. Puede desplazarse a otras fichas para buscar campos de entrada para propiedades de metadatos situadas debajo de ellas.

   Esta página tiene una barra de herramientas que contiene dos iconos de acción diferentes de los del modo de vista:

   * Cancelar: ![aem6forms_close](assets/aem6forms_close.svg_w24.png) Cancelar los cambios realizados hasta ahora en los valores de las propiedades de metadatos
   * Listo: ![aem6forms_check](assets/aem6forms_check.png) Guarde todos los cambios realizados hasta ahora en los valores de propiedad de metadatos

   Ambas acciones dirigen al usuario de nuevo al modo de solo lectura de la página de propiedades que contiene los valores actualizados.

### Actualizar la miniatura del formulario {#update-the-form-thumbnail}

El panel izquierdo de la página de propiedades muestra la miniatura del formulario. De forma predeterminada, la miniatura que se muestra es la generada en el momento de la creación del formulario (formulario adaptable) o en el momento de la carga del formulario.

Para todos los tipos de formulario, puede cargar una imagen haciendo clic en **[!UICONTROL Cargar imagen]** y buscando un archivo de imagen desde el directorio local. La imagen seleccionada se utiliza como miniatura en lugar de como predeterminada.

Para los formularios adaptables, se proporciona una funcionalidad adicional que permite al usuario generar una miniatura como instantánea de la previsualización de formulario adaptable actual. Como AEM Forms también admite la creación de formularios adaptables, la previsualización del formulario adaptable puede cambiar cada vez que se cambia el formulario adaptable. Esta funcionalidad para generar una miniatura le ayuda a obtener una miniatura nueva para el formulario adaptable en función del estado de previsualización actual. Haga clic en **[!UICONTROL Generar Previsualización]** para llevar a cabo esta acción.

>[!NOTE]
>
>* Utilice una imagen cuadrada para la miniatura. Cuando se utiliza una imagen no cuadrada y se vista la miniatura en la vista de lista, la miniatura aparece recortada.
>* Una vez que se carga o genera una nueva imagen, la miniatura se reemplaza por esta imagen y no se puede restaurar a la imagen anterior.

>



## Añadir metadatos personalizados {#add-custom-metadata}

Además de los metadatos proporcionados de forma predeterminada, AEM Forms admite nuevos metadatos personalizados.

Se proporciona una herramienta (Editor de Esquemas de metadatos) para definir el esquema de la presentación de metadatos; es decir, la presentación de lo que aparece en la página **[!UICONTROL Propiedades]** de un formulario. El Editor de Esquemas de metadatos permite agregar o modificar un esquema personalizado para los recursos.

AEM Forms expone los esquemas de metadatos de los tipos de formularios admitidos en esta herramienta. De este modo, puede acceder a estos esquemas y utilizar la funcionalidad proporcionada en el editor de esquemas de metadatos para agregar propiedades personalizadas.

### Navegue por el editor de esquemas de metadatos {#navigate-the-metadata-schema-editor}

1. Vaya a **[!UICONTROL Herramientas > Recursos > Esquemas de metadatos]**.

1. Haga clic en **[!UICONTROL formularios]** en los formularios de esquema enumerados.

1. En la lista que se abre, haga clic en el tipo de recurso para el que desee agregar metadatos personalizados.

   >[!NOTE]
   >
   >Estos esquemas contienen propiedades de metadatos que se proporcionan de forma predeterminada y no se deben modificar/editar (al seleccionar la casilla de verificación y hacer clic en Editar desde la barra de herramientas) para evitar problemas funcionales.

1. Cualquier tipo de recurso en el que se hace clic abre una lista que contiene la opción `extendedmetadata`. Edite este esquema.

1. Seleccione la casilla de verificación situada junto a `extendedmetadata` y, a continuación, haga clic en el icono Editar ![aem6formularios_edit](assets/aem6forms_edit.png) que aparece en la barra de herramientas.

1. AEM Forms abre el editor de esquemas de metadatos/creador de formularios del tipo de recurso seleccionado (en este caso, formulario adaptable).

   ![Editor de esquemas de metadatos para el tipo de formulario adaptable](assets/metadata-schema-editor-for-adaptive-form-type.png)

   Editor de metadatos

   1. El panel izquierdo contiene secciones con fichas donde se colocan los campos y el panel derecho muestra todos los componentes de interfaz de usuario disponibles y las propiedades del campo seleccionado en el panel izquierdo.

   1. La sección bloqueada no es editable y contiene campos para todas las propiedades de metadatos que se proporcionan de forma predeterminada.

   1. Puede agregar fichas adicionales haciendo clic en el símbolo +.

   1. Puede agregar un campo personalizado del tipo deseado arrastrando el componente de campo de la sección **[!UICONTROL Generar formulario]** a la página de esquema.
   1. Las especificaciones de este campo se pueden proporcionar en la sección **[!UICONTROL Configuración]** después de hacer clic en el campo.

### Añadir propiedad de metadatos personalizada en el editor de esquemas {#add-custom-metadata-property-in-schema-editor}

1. Vaya a la ficha (existente o nueva) donde desee agregar la propiedad personalizada.

1. Arrastre un componente del tipo deseado de la sección **[!UICONTROL Generar formulario]** al panel izquierdo y colóquelo en una ubicación conveniente.

   >[!NOTE]
   >
   >No puede mover las secciones bloqueadas, pero puede colocar el componente en cualquiera de los espacios vacíos.

1. Haga clic en un componente que acaba de arrastrar. En la ficha Configuración que se abre en el panel derecho, rellene la información de los siguientes campos:

   1. Especifique una etiqueta de campo que se utilizará como nombre para mostrar encima del campo colocado en el esquema (por ejemplo: Departamento)
   1. En Asignar a la propiedad, puede ver un valor prerelleno **&#39;./jcr:content/metadata/default&#39;**. Cambie el ‘**predeterminado**’ por un nombre de propiedad deseado, que se utiliza para almacenar la propiedad en el repositorio crx (por ejemplo: &#39;./jcr:content/metadata/Department&#39;)

      >[!NOTE]
      >
      >No cambie el prefijo ‘./jcr:content/metadata/’ tal como define la ruta en la que se almacena la propiedad.
      >
      >Además, el nombre de la propiedad debe ser único para evitar escribir valores para dos o más propiedades en la misma ubicación del repositorio. Por lo tanto, se recomienda cambiar el valor &#39;default&#39;.

   1. Rellene otros ajustes según los requisitos. Por ejemplo: seleccione la opción Obligatorio si desea hacer obligatorio el campo.
   1. Para eliminar un campo agregado, selecciónelo y haga clic en el icono Eliminar ![eliminar-1](assets/delete-1.png).

1. Si es necesario, siga los pasos del 1 al 3 para agregar otra propiedad.
1. Haga clic en **Listo** después de realizar todos los cambios.

   Ha agregado correctamente una propiedad de metadatos personalizada.

Todos los formularios adaptables de AEM Forms ahora contienen esta propiedad de metadatos adicional. Puede editarlo desde la página de propiedades.
