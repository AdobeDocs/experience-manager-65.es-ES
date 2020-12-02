---
title: Componente de proyectos y presentaciones
seo-title: Componente de proyectos y presentaciones
description: Borradores y envíos listas componentes formularios que se encuentran en estado borrador y que ya se han enviado. Puede personalizar el aspecto y el estilo del componente.
seo-description: Borradores y envíos listas componentes formularios que se encuentran en estado borrador y que ya se han enviado. Puede personalizar el aspecto y el estilo del componente.
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
translation-type: tm+mt
source-git-commit: 23252989bb8649b2f0b96a58972c831257e0c5dc
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# Componente Borradores y envíos{#drafts-and-submissions-component}

El componente Borradores y envíos lista todos los formularios que están en el estado borrador y los formularios que ya se han enviado. El componente tiene secciones independientes (fichas) para borradores y formularios enviados. Los usuarios solo pueden realizar vistas de los borradores y los formularios enviados.

## Configuración del componente {#configuring-the-component}

El componente Borradores y envíos tiene dos fichas: Borradores y presentaciones.

Para permitir que el envío de un formulario adaptable aparezca en la ficha Envíos, establezca la **acción de envío** en **[Acción de envío de Forms Portal](../../forms/using/configuring-submit-actions.md). Como alternativa,** habilite la opción Enviar de Forms Portal. Cada vez que un usuario envía el formulario, éste se agrega a la ficha envíos.

La funcionalidad de borradores está activada de forma predeterminada. Cuando un usuario hace clic **Guardar** en un formulario adaptable, el formulario se agrega a la ficha Borradores.

Realice los siguientes pasos para agregar y configurar un componente Borradores y envíos:

1. Arrastre y suelte el componente **Borradores y envíos** en la categoría de Documento Services en el navegador de componentes de la página.
1. Toque el componente y, a continuación, toque ![settings_icon](assets/settings_icon.png) para abrir el cuadro de diálogo Editar del componente.

   ![Componente Borradores y envío](assets/drafts-submissions-edit.png)

1. En el cuadro de diálogo Editar, especifique los siguientes detalles y toque **Listo** para guardar la configuración.

<table>
 <tbody>
  <tr>
   <th>Ficha</th>
   <th>Configuración</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>General</td>
   <td>Resultado total</td>
   <td>Especifica el número máximo de resultados que se van a mostrar. Si el recuento de resultados aumenta el límite de resultados totales, aparece un vínculo <strong>Más </strong>en la parte inferior del componente. Al hacer clic en <strong>Más </strong>se muestran todos los formularios. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Tipo de estilo</td>
   <td>Especifica el estilo del componente. Puede especificar <strong>Sin estilo</strong>, <strong>Estilo predeterminado</strong> o <strong>Estilo personalizado</strong> para enumerar los formularios. Para la opción Estilo personalizado, puede especificar la ruta del archivo CSS personalizado en el campo <strong>Ruta de estilo personalizada </strong>a2/&gt;.</strong><strong></strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Ruta de estilo personalizada</td>
   <td>Si elige la opción <strong>Estilo personalizado</strong> en el campo <strong>Tipo de estilo</strong>, utilice el campo <strong>Ruta de estilo personalizada</strong> para especificar la ruta del archivo CSS personalizado. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Opciones de visualización</td>
   <td><p>Especifica las fichas que se van a mostrar. Puede elegir mostrar formularios de borrador, formularios enviados o ambos. </p> <p><strong>Nota</strong>:<em> Para las opciones <strong> de </strong>visualización, si selecciona una opción distinta a  <strong>ambas</strong>, no se utiliza la opción  <strong>Predeterminado </strong> Tabfield.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Ficha predeterminada</td>
   <td>Especifica la ficha que se mostrará cuando se cargue la página del portal de formularios. Puede elegir entre <strong>Ficha Forms de borrador</strong> y <strong>Ficha Forms de envío</strong>.</td>
  </tr>
  <tr>
   <td>Configuración de la ficha Borrador de Forms</td>
   <td>Título personalizado</td>
   <td>Especifica el título de la ficha <strong>Borrador de Forms</strong>. El valor predeterminado es <strong>Borrador de Forms.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Plantilla de diseño</td>
   <td>Especifica el diseño que se va a utilizar para la lista de Borrador de Forms.</td>
  </tr>
  <tr>
   <td>Configuración de la ficha de Forms enviada</td>
   <td>Título personalizado </td>
   <td>Especifica el título de la ficha <strong>Envío de Forms </strong>. El valor predeterminado es <strong>Forms enviado.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Plantilla de diseño</td>
   <td>Especifica el diseño que se usará para la lista de Forms<strong> </strong>enviado. </td>
  </tr>
 </tbody>
</table>

## Personalización del almacenamiento {#customizing-the-storage}

Cuando se utiliza la acción de envío de Forms Portal o se activa la opción Almacenar datos en el portal de formularios en un formulario adaptable, los datos del formulario se almacenan en AEM repositorio. En un entorno de producción, se recomienda no almacenar datos de formulario borrador o enviados en AEM repositorio. En su lugar, debe integrar los borradores y el componente de envío con un almacenamiento seguro como la base de datos de empresa para almacenar borradores y datos de formularios enviados.

El portal de Forms le permite almacenar datos en un repositorio de AEM local, en un repositorio AEM remoto o en una base de datos. AEM Forms le permite personalizar la implementación del almacenamiento de datos de usuario para borradores y envíos. Puede anular los métodos predeterminados para especificar cómo se almacenan los datos de borrador y envío en un almacenamiento de su elección. Por ejemplo, puede almacenar los datos en un almacén de datos implementado actualmente en su organización.

El portal de Forms proporciona servicios (API) listos para usar para almacenar datos en el repositorio crx de instancias de publicación local y remota de AEM Forms. Puede reemplazar las implementaciones predeterminadas que se describen en el artículo [Configuración de los servicios de almacenamiento para borradores y envíos](/help/forms/using/configuring-draft-submission-storage.md) por implementaciones personalizadas para reemplazar la funcionalidad predeterminada. Para obtener información detallada sobre los métodos requeridos en una implementación personalizada para almacenar contenido en una ubicación segura, consulte [Personalización de los servicios de datos de borradores y envíos](/help/forms/using/custom-draft-submission-data-services.md) y [almacenamiento personalizado para borradores y componentes de envíos.](/help/forms/using/adding-custom-storage-provider-forms.md)

La documentación de AEM Forms proporciona una [muestra para integrar los borradores y el componente de envíos con la base de datos](integrate-draft-submission-database.md). Puede utilizar la implementación de muestra para desarrollar su propia implementación personalizada.

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Crear página del portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Lista de formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalización del almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente de borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalización de plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)
