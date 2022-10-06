---
title: Creación de una plantilla de formulario adaptable personalizada
seo-title: Creating a custom adaptive form template
description: Este artículo describe cómo crear plantillas de formulario adaptables personalizadas.
seo-description: This article describes how to create custom adaptive form templates.
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
exl-id: 35b50573-0be8-469d-a1ac-f51b9aaa5fef
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 2%

---

# Creación de una plantilla de formulario adaptable personalizada{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms ha introducido plantillas dinámicas. Puede utilizar el editor de plantillas de AEM Sites para [crear o editar plantillas dinámicas](../../forms/using/template-editor.md). Las plantillas mencionadas en el siguiente artículo son plantillas estáticas. No están disponibles en una instalación predeterminada. [Instalación del paquete de compatibilidad](../../forms/using/compatibility-package.md) para obtener estas plantillas en su entorno.

## Requisitos previos {#prerequisites}

* Comprensión de la AEM [Plantilla de página](/help/sites-authoring/templates.md) y [Creación de formularios adaptables](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* Comprensión de la AEM [Bibliotecas de cliente](/help/sites-developing/clientlibs.md)

## Plantilla de formulario adaptable {#adaptive-form-template}

Una plantilla de formulario adaptable es AEM plantilla de página especializada, con determinadas propiedades y estructura de contenido que se utiliza para crear el formulario adaptable. La plantilla tiene diseños, estilos y estructura de contenido inicial básica preconfigurados.

Una vez creado un formulario, los cambios realizados en la estructura de contenido de la plantilla original no se reflejan en el formulario.

## Plantillas de formulario adaptables predeterminadas {#default-adaptive-form-templates}

AEM QuickStart proporciona las siguientes plantillas de formulario adaptables:

* Plantilla de encuesta: Permite crear un formulario adaptable de una sola página con el diseño adaptable que tiene varias columnas configuradas. La presentación se ajusta automáticamente en función de las dimensiones de las distintas pantallas en las que desea mostrar el formulario.
* Plantilla de inscripción simple: Permite crear un formulario adaptable de varios pasos con una presentación de asistente. En este diseño, se puede especificar una expresión de finalización de paso para cada paso, que se valida antes de que el asistente continúe con el siguiente paso.
* Plantilla de inscripción tabulada: Permite crear un formulario adaptable multipestaña utilizando una presentación de pestañas a la izquierda, donde puede visitar las pestañas en cualquier orden aleatorio.
* Plantilla de inscripción avanzada: Permite crear un formulario con varias fichas y un asistente. Utiliza un diseño de pestañas en la izquierda que permite visitar las pestañas en cualquier orden. Utiliza los servicios de Adobe Document Cloud Design para la firma y verificación.
* Plantilla en blanco: Permite crear un formulario sin encabezado, pie de página ni contenido inicial. Puede añadir componentes, como cuadros de texto, botones e imágenes. La plantilla en blanco permite crear un formulario que puede [incrustar en páginas AEM sitio](/help/forms/using/embed-adaptive-form-aem-sites.md).

Estas plantillas tienen la variable `sling:resourceType` propiedad establecida en el componente de página correspondiente. El componente de página procesa la página de CQ, que contiene el contenedor de formulario adaptable, que a su vez procesa el formulario adaptable.

La siguiente tabla enumera la asociación entre las plantillas y el componente de página:

<table>
 <tbody>
  <tr>
   <td><p><strong>Plantilla</strong></p> </td>
   <td><p><strong>Componente Página </strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnscriptionsTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnscriptionsTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedensubscription</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnsubscriptionTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/Advancedensubscription</p> </td>
  </tr>
 </tbody>
</table>

## Creación de una plantilla de formulario adaptable mediante el editor de plantillas {#creating-an-adaptive-form-template-using-template-editor}

Puede especificar la estructura y el contenido inicial de un formulario adaptable mediante el Editor de plantillas. Por ejemplo, desea que todos los autores de formularios tengan pocos cuadros de texto, botones de navegación y un botón de envío en un formulario de inscripción. Puede crear una plantilla que los autores puedan utilizar para crear un formulario coherente con otros formularios de inscripción. AEM Editor de plantillas le permite:

* Agregar componentes de encabezado y pie de página de un formulario en la capa de estructura
* Proporcionar el contenido inicial para el formulario.
* Especifique un tema.
* Especifique acciones como enviar, restablecer y navegar.

Para obtener más información, consulte [Editor de plantillas](../../forms/using/template-editor.md).

## Creación de una plantilla de formulario adaptable a partir de CRXDE {#creating-an-adaptive-form-template-from-crxde}

En lugar de utilizar las plantillas disponibles, puede crear una plantilla y utilizarla para crear formularios adaptables. Las plantillas personalizadas se basan en varios componentes de página que hacen referencia a contenedores de formularios adaptables y elementos de página, como el encabezado y el pie de página.

Puede crear estos componentes utilizando el componente de página base para el sitio web. También puede ampliar el componente de página del formulario adaptable que utilizan las plantillas listas para usar.

Realice los siguientes pasos para crear una plantilla personalizada, como simpleEnSubscriptionTemplate.

1. Navegue hasta CRXDE Lite de la instancia de creación.

1. En el directorio /apps , cree la estructura de carpetas para la aplicación. Por ejemplo, si el nombre de la aplicación es mycompany, cree una carpeta con este nombre. Normalmente, la carpeta de la aplicación contiene componentes, configuración, plantillas, src y directorios de instalación. Para este ejemplo, cree las carpetas de componentes, configuración y plantillas.

1. Vaya a la carpeta /libs/fd/af/templates.
1. Copie el `simpleEnrollmentTemplate` nodo .
1. Vaya a la carpeta /apps/mycompany/templates. Haga clic con el botón derecho y seleccione **[!UICONTROL Pegar]**.
1. Si es necesario, cambie el nombre del nodo de plantilla que ha copiado. Por ejemplo, renómbralo como plantilla de inscripción.

1. Vaya a la ubicación /apps/mycompany/templates/enderechos-template.

1. Modifique el `jcr:title` y `jcr:description` propiedades de la variable `jcr:content` para distinguir la plantilla de la plantilla copiada.

1. La variable `jcr:content` El nodo de la plantilla modificada contiene la variable `guideContainer` y `guideformtitle` componentes. `guideContainer` es el contenedor que contiene el formulario adaptable. La variable `guideformtitle` muestra el nombre de la aplicación, la descripción, etc.

   En lugar de `guideformtitle`, puede incluir un componente personalizado o el `parsys` componente. Por ejemplo, remove `guideformtitle`y añada un componente personalizado o el `parsys` nodo de componente. Asegúrese de que la variable `sling:resourceType` la propiedad del componente hace referencia al componente y se define lo mismo en la página `component.jsp` archivo.

1. Vaya a la ubicación /apps/mycompany/templates/enderechos-template/jcr:content.

1. Abra el **[!UICONTROL Propiedades]** y cambie el valor de `cq:designPath` a /etc/designs/mycompany.

1. Ahora cree un nodo /etc/designs/mycompany para la variable `cq:Page` tipo .

## Creación de un componente de página de formulario adaptable {#create-an-adaptive-form-page-component}

La plantilla personalizada tiene el mismo estilo que la plantilla predeterminada porque hace referencia al componente de página /libs/fd/af/components/page/base. Puede encontrar la referencia del componente como propiedad `sling:resourceType` se define en el nodo /apps/mycompany/templates/ensubscription-template/jcr:content. Como base es un componente de producto principal, no modifique este componente.

1. Vaya al nodo /apps/mycompany/templates/enderechos-template/jcr:content y modifique el valor de la propiedad `sling:resourceType` a /apps/mycompany/components/page/enrollmentpage
1. Copie el nodo /libs/fd/af/components/page/base a la carpeta /apps/mycompany/components/page.

1. Cambiar el nombre del componente copiado a `enrollmentpage`.

1. **(Solo si ya tiene una página de contenido)** Realice los siguientes pasos (a-d), si ya tiene `contentpage`para su sitio web. Si no tiene un `contentpage`para su sitio web, puede dejar el `resourceSuperType`propiedad para señalar a la página base de OOTB.

   1. Para la variable `enrollmentpage` nodo, establecer valor de la propiedad `sling:resourceSuperType` a mycompany/components/page/contentpage. La variable `contentpage` es el componente de página base del sitio. Otros componentes de página pueden ampliarlo. Eliminar archivos de secuencias de comandos en `enrollmentpage`, excepto `head.jsp`, `content.jsp`y `library.jsp`. La variable `sling:resourceSuperType` componente, que es `contentpage` en este caso, incluye todas estas secuencias de comandos. Los encabezados, incluidas la barra de navegación y el pie de página, se heredan del `contentpage` componente.

   1. Abra el archivo `head.jsp`.

      El archivo JSP contiene la línea `<cq.include script="library.jsp"/>`.

      La variable `library.jsp` contiene el `guide.theme.simpleEnrollment` biblioteca de cliente, que contiene el estilo del formulario adaptable.

      El componente de página `enrollmentpage` tiene una `head.jsp` que anula la función `head.jsp` del `contentpage` componente.

   1. Incluya todas las secuencias de comandos en el `head.jsp` para `contentpage` al `head.jsp` para `enrollmentpage` componente.
   1. En el `content.jsp` , puede añadir contenido de página adicional o referencias a otros componentes que se incluyen cuando se procesa una página. Por ejemplo, si agrega el componente personalizado `applicationformheader`, asegúrese de añadir la siguiente referencia al componente en el archivo JSP:

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      Del mismo modo, si agrega un `parsys` en la estructura del nodo de plantilla, incluya también el componente personalizado.

## Creación de una biblioteca de cliente de formulario adaptable {#creating-an-adaptive-form-client-library}

La variable `head.jsp` del `enrollmentpage` componente para la nueva plantilla incluye una biblioteca de cliente `guide.theme.simpleEnrollment`. La plantilla predeterminada también utiliza esta biblioteca de cliente. Cambie el estilo en la nueva plantilla mediante uno de estos métodos:

* Definir un tema personalizado y reemplazar el tema predeterminado `guide.theme.simpleEnrollment` con el tema personalizado.
* Defina una nueva biblioteca de cliente en /etc/designs/mycompany. Incluya la biblioteca de cliente después de la entrada de tema predeterminada en la página jsp. Incluya todos los estilos anulados y archivos JavaScript adicionales en esta biblioteca de cliente.

>[!NOTE]
>
>El tema hace referencia a una biblioteca de cliente que se incluye en el componente de página que se utiliza para procesar un formulario adaptable. La biblioteca de cliente rige principalmente el aspecto de un formulario adaptable.
