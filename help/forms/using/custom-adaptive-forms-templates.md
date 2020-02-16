---
title: Creación de una plantilla de formulario adaptable personalizada
seo-title: Creación de una plantilla de formulario adaptable personalizada
description: En este artículo se describe cómo crear plantillas de formulario adaptables personalizadas.
seo-description: En este artículo se describe cómo crear plantillas de formulario adaptables personalizadas.
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe

---


# Creación de una plantilla de formulario adaptable personalizada{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms ha introducido plantillas dinámicas. Puede utilizar el editor de plantillas de AEM Sites para [crear o editar plantillas](../../forms/using/template-editor.md)dinámicas. Las plantillas mencionadas en el artículo siguiente son plantillas estáticas. No están disponibles en una instalación predeterminada. [Instale el paquete](../../forms/using/compatibility-package.md) Compatibilidad para obtener estas plantillas en su entorno.

## Requisitos previos {#prerequisites}

* Explicación de la creación de plantillas [de](/help/sites-authoring/templates.md) página y formularios [adaptables de AEM](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* Información sobre las bibliotecas del [cliente de AEM](/help/sites-developing/clientlibs.md)

## Adaptive form template {#adaptive-form-template}

Una plantilla de formulario adaptable es una plantilla de página de AEM especializada, con determinadas propiedades y estructura de contenido que se utiliza para crear un formulario adaptable. La plantilla tiene diseños, estilos y estructura de contenido inicial básica preconfigurados.

Una vez creado un formulario, los cambios realizados en la estructura de contenido de la plantilla original no se reflejan en el formulario.

## Plantillas de formulario adaptables predeterminadas {#default-adaptive-form-templates}

AEM QuickStart proporciona las siguientes plantillas de formulario adaptables:

* Plantilla de estudio: Permite crear un formulario adaptable de una sola página con el diseño adaptable con varias columnas configuradas. La presentación se ajusta automáticamente en función de las dimensiones de las distintas pantallas en las que desea mostrar el formulario.
* Plantilla de inscripción simple: Permite crear un formulario adaptable de varios pasos con una presentación de asistente. En este diseño, puede especificar una expresión de finalización de pasos para cada paso, que se valida antes de que el asistente continúe con el paso siguiente.
* Plantilla de inscripción en fichas: Permite crear un formulario adaptable con varias fichas con una presentación de fichas a la izquierda, donde puede visitar las fichas en cualquier orden aleatorio.
* Plantilla de inscripción avanzada: Permite crear un formulario con varias fichas y un asistente. Utiliza un diseño de fichas a la izquierda que permite visitar las fichas en cualquier orden. Utiliza los servicios de firma y verificación de Adobe Document Cloud.
* Plantilla en blanco: Permite crear un formulario sin encabezado, pie de página ni contenido inicial. Puede agregar componentes como cuadros de texto, botones e imágenes. La plantilla en blanco le permite crear un formulario que puede [incrustar en las páginas](/help/forms/using/embed-adaptive-form-aem-sites.md)del sitio de AEM.

Estas plantillas tienen la `sling:resourceType` propiedad establecida en el componente de página correspondiente. El componente de página procesa la página de CQ, que contiene el contenedor de formularios adaptables, que a su vez procesa el formulario adaptable.

La siguiente tabla enumera la asociación entre plantillas y componentes de página:

<table>
 <tbody>
  <tr>
   <td><p><strong>Plantilla</strong></p> </td>
   <td><p><strong>Componente de página</strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnregistrationTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnregistrationTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenregistration</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnregistrationTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/Advancedenregistration</p> </td>
  </tr>
 </tbody>
</table>

## Creación de una plantilla de formulario adaptable mediante el editor de plantillas {#creating-an-adaptive-form-template-using-template-editor}

Puede especificar la estructura y el contenido inicial de un formulario adaptable mediante el Editor de plantillas. Por ejemplo, desea que todos los autores de formularios tengan pocos cuadros de texto, botones de navegación y un botón de envío en un formulario de inscripción. Puede crear una plantilla que los autores puedan utilizar para crear un formulario coherente con otros formularios de inscripción. El Editor de plantillas de AEM le permite:

* Adición de componentes de encabezado y pie de página de un formulario en la capa de estructura
* Proporcione el contenido inicial del formulario.
* Especifique un tema.
* Especifique acciones como enviar, restablecer y desplazarse.

Para obtener más información, consulte Editor [de plantillas](../../forms/using/template-editor.md).

## Creación de una plantilla de formulario adaptable a partir de CRXDE {#creating-an-adaptive-form-template-from-crxde}

En lugar de utilizar las plantillas disponibles, puede crear una plantilla y utilizarla para crear formularios adaptables. Las plantillas personalizadas se basan en varios componentes de página que hacen referencia a contenedores de formularios adaptables y elementos de página, como el encabezado y el pie de página.

Puede crear estos componentes con el componente de página base del sitio Web. También puede ampliar el componente de página del formulario adaptable que utilizan las plantillas integradas.

Realice los siguientes pasos para crear una plantilla personalizada, como simpleEnregistrationTemplate.

1. Vaya a CRXDE Lite en la instancia de creación.

1. En el directorio /apps, cree la estructura de carpetas para la aplicación. Por ejemplo, si el nombre de la aplicación es miempresa, cree una carpeta con este nombre. Normalmente, la carpeta de la aplicación contiene componentes, configuración, plantillas, src y directorios de instalación. Para este ejemplo, cree las carpetas de componentes, configuración y plantillas.

1. Vaya a la carpeta /libs/fd/af/templates.
1. Copie el `simpleEnrollmentTemplate` nodo.
1. Vaya a la carpeta /apps/miempresa/templates. Haga clic con el botón derecho y seleccione **[!UICONTROL Pegar]**.
1. Si es necesario, cambie el nombre del nodo de plantilla que ha copiado. Por ejemplo, cambie su nombre como plantilla de inscripción.

1. Vaya a la ubicación /apps/miempresa/templates/enregistration-template.

1. Modifique las propiedades `jcr:title` y `jcr:description` del `jcr:content` nodo para distinguir la plantilla de la plantilla copiada.

1. El `jcr:content` nodo de la plantilla modificada contiene los `guideContainer` componentes y `guideformtitle` . `guideContainer` es el contenedor que contiene el formulario adaptable. El `guideformtitle` componente muestra el nombre de la aplicación, la descripción, etc.

   En lugar de `guideformtitle`, puede incluir un componente personalizado o el `parsys` componente. Por ejemplo, elimine `guideformtitle`y agregue un componente personalizado o el nodo del `parsys` componente. Asegúrese de que la `sling:resourceType` propiedad del componente hace referencia al componente y que lo mismo se define en el archivo de página `component.jsp` .

1. Vaya a la ubicación /apps/miempresa/templates/enregistration-template/jcr:content.

1. Abra la ficha **[!UICONTROL Propiedades]** y cambie el valor de la `cq:designPath` propiedad a /etc/designs/miempresa.

1. Ahora cree un nodo /etc/designs/miempresa para el `cq:Page` tipo.

## Creación de un componente de página de formulario adaptable {#create-an-adaptive-form-page-component}

La plantilla personalizada tiene el mismo estilo que la plantilla predeterminada porque hace referencia al componente de página /libs/fd/af/components/page/base. Puede encontrar la referencia del componente como la propiedad `sling:resourceType` definida en el nodo /apps/miempresa/templates/enregistration-template/jcr:content. Dado que base es un componente de producto principal, no modifique este componente.

1. Vaya al nodo /apps/miempresa/templates/enplication-template/jcr:content y modifique el valor de la propiedad `sling:resourceType` en /apps/miempresa/components/page/enrollmentpage
1. Copie el nodo /libs/fd/af/components/page/base en la carpeta /apps/miempresa/components/page.

1. Cambie el nombre del componente copiado a `enrollmentpage`.

1. **(Solo si ya tiene una página de contenido)** Realice los siguientes pasos (a-d), si ya tiene un `contentpage`componente existente para el sitio Web. Si no tiene un `contentpage`componente existente para el sitio web, puede dejar la `resourceSuperType`propiedad para que apunte a la página base de OOTB.

   1. Para el `enrollmentpage` nodo, establezca el valor de la propiedad `sling:resourceSuperType` en mycompany/components/page/contentpage. El `contentpage` componente es el componente de página base del sitio. Otros componentes de página pueden ampliarla. Elimine los archivos de secuencias de comandos debajo `enrollmentpage`, excepto `head.jsp`, `content.jsp`y `library.jsp`. El `sling:resourceSuperType` componente, que es `contentpage` en este caso, incluye todas estas secuencias de comandos. Los encabezados, incluidas la barra de navegación y el pie de página, se heredan del `contentpage` componente.

   1. Abra el archivo `head.jsp`.

      El archivo JSP contiene la línea `<cq.include script="library.jsp"/>`.

      El `library.jsp` archivo contiene la biblioteca del `guide.theme.simpleEnrollment` cliente, que contiene el estilo del formulario adaptable.

      El componente de página `enrollmentpage` tiene un `head.jsp` archivo exclusivo que anula el `head.jsp` archivo del `contentpage` componente.

   1. Incluya todas las secuencias de comandos del `head.jsp` archivo del `contentpage` componente en el `head.jsp` archivo del `enrollmentpage` componente.
   1. En la secuencia de comandos, puede agregar contenido de página adicional o referencias a otros componentes que se incluyen cuando se procesa una página. `content.jsp` Por ejemplo, si agrega el componente personalizado `applicationformheader`, asegúrese de agregar la siguiente referencia al componente en el archivo JSP:

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      Del mismo modo, si agrega un `parsys` componente en la estructura del nodo de plantilla, incluya también el componente personalizado.

## Creación de una biblioteca de cliente de formulario adaptable {#creating-an-adaptive-form-client-library}

El `head.jsp` archivo del `enrollmentpage` componente para la nueva plantilla incluye una biblioteca de cliente `guide.theme.simpleEnrollment`. La plantilla predeterminada también utiliza esta biblioteca de cliente. Cambie el estilo en la nueva plantilla mediante uno de estos métodos:

* Defina un tema personalizado y reemplace el tema predeterminado `guide.theme.simpleEnrollment` por el tema personalizado.
* Defina una nueva biblioteca de cliente en /etc/designs/miempresa. Incluya la biblioteca de cliente después de la entrada de tema predeterminada en la página jsp. Incluya todos los estilos anulados y los archivos de Java Script adicionales en esta biblioteca de cliente.

>[!NOTE]
>
>El tema hace referencia a una biblioteca de cliente que se incluye en el componente de página utilizado para procesar un formulario adaptable. La biblioteca de cliente rige principalmente el aspecto de un formulario adaptable.

