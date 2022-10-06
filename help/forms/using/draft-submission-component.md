---
title: Componente Borradores y presentaciones
seo-title: Drafts and submissions component
description: El componente Borradores y envíos enumera los formularios que están en estado borrador y que ya se han enviado. Puede personalizar el aspecto y el estilo del componente.
seo-description: Drafts and submissions component lists forms that are in the draft state and are already submitted. You can customize appearance and style of the component.
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
exl-id: f3f013a7-a399-4178-a901-d4a8c65ddbd3
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 4%

---

# Componente Borradores y presentaciones{#drafts-and-submissions-component}

El componente Borradores y envíos enumera todos los formularios que están en estado de borrador y los formularios que ya se han enviado. El componente tiene secciones independientes (pestañas) para borradores y formularios enviados. Los usuarios solo pueden ver los borradores y los formularios enviados.

## Configuración del componente {#configuring-the-component}

El componente Borradores y envíos tiene dos fichas: Borradores y presentaciones.

Para permitir que el envío de un formulario adaptable aparezca en la pestaña envíos , establezca la variable **Enviar acción** a **[Acción de envío del portal de Forms](../../forms/using/configuring-submit-actions.md). Alternativamente,** active la opción Envío del portal de Forms. Cada vez que un usuario envía el formulario, este se agrega a la ficha envíos.

La funcionalidad de borradores está habilitada de forma predeterminada. Cuando un usuario hace clic en **Guardar** en un formulario adaptable, el formulario se añade a la pestaña borradores .

Siga estos pasos para agregar y configurar un componente Borradores y envíos :

1. Arrastre y suelte la **Borradores y envíos** en la categoría Servicios de documentos del navegador de componentes de su página.
1. Pulse el componente y, a continuación, pulse ![settings_icon](assets/settings_icon.png) para abrir el cuadro de diálogo Editar del componente.

   ![Componente Borradores y envío](assets/drafts-submissions-edit.png)

1. En el cuadro de diálogo Editar, especifique los siguientes detalles y pulse **Listo** para guardar la configuración.

<table>
 <tbody>
  <tr>
   <th>Tab</th>
   <th>Configuración</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>General</td>
   <td>Resultado total</td>
   <td>Especifica el número máximo de resultados que se van a mostrar. Si el recuento de resultados aumenta el límite de resultados totales, una <strong>Más </strong>aparece en la parte inferior del componente. Hacer clic <strong>Más </strong>muestra todos los formularios. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Tipo de estilo</td>
   <td>Especifica el estilo del componente. Puede especificar <strong>Sin estilo</strong>, <strong>Estilo predeterminado</strong>o <strong>Estilo personalizado</strong> para listar los formularios. Para la opción Estilo personalizado, puede especificar la ruta del archivo CSS personalizado en la variable <strong>Ruta de estilo personalizada </strong>field<strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Ruta de estilo personalizada</td>
   <td>Si elige <strong>Estilo personalizado</strong> en la <strong>Tipo de estilo</strong> , utilice el <strong>Ruta de estilo personalizada</strong> para especificar la ruta del archivo CSS personalizado. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Opciones de visualización</td>
   <td><p>Especifica las fichas que se van a mostrar. Puede elegir mostrar formularios borrador, formularios enviados o ambos. </p> <p><strong>Nota</strong>:<em> Para <strong>Opciones de visualización</strong>, si selecciona una opción distinta de <strong>Ambas</strong>, el <strong>Ficha Predeterminada</strong> no se utiliza.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Pestaña predeterminada</td>
   <td>Especifica la ficha que se mostrará cuando se cargue la página del portal de formularios. Puede elegir entre <strong>Pestaña Borrador de Forms</strong> y <strong>Pestaña Forms enviada</strong>.</td>
  </tr>
  <tr>
   <td>Configuración de pestañas de borrador de formularios</td>
   <td>Título personalizado</td>
   <td>Especifica el título del <strong>Borrador de Forms</strong> pestaña . El valor predeterminado es <strong>Borrador de Forms.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Plantilla de diseño</td>
   <td>Especifica el diseño que se utiliza para la lista Borrador de Forms.</td>
  </tr>
  <tr>
   <td>Configuración de fichas de formularios enviados</td>
   <td>Título personalizado </td>
   <td>Especifica el título del <strong>Forms enviado </strong>pestaña . El valor predeterminado es <strong>Forms enviado.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Plantilla de diseño</td>
   <td>Especifica el diseño que se va a utilizar para el Forms enviado<strong> </strong>lista. </td>
  </tr>
 </tbody>
</table>

## Personalización del almacenamiento {#customizing-the-storage}

Cuando se utiliza la acción de envío de Forms Portal o se activa la opción Store data in forms portal en forma adaptativa, los datos del formulario se almacenan en AEM repositorio. En un entorno de producción, se recomienda no almacenar datos de formulario en borrador o enviados en AEM repositorio. En su lugar, debe integrar los borradores y el componente de envío con un almacenamiento seguro, como la base de datos empresarial, para almacenar borradores y enviar datos de formularios.

Portal de Forms le permite almacenar datos en el repositorio de AEM local, en el repositorio de AEM remoto o en una base de datos. AEM Forms le permite personalizar la implementación del almacenamiento de datos de usuario para borradores y envíos. Puede anular los métodos predeterminados para especificar cómo se almacenan los datos de borradores y envíos en el almacenamiento que elija. Por ejemplo, puede almacenar los datos en un almacén de datos implementado actualmente en su organización.

El portal de Forms proporciona servicios (API) listos para usar para almacenar datos en el repositorio crx de instancias de publicación locales y remotas de AEM Forms. Puede reemplazar las implementaciones predeterminadas que se describen en [Configuración de servicios de almacenamiento para borradores y envíos](/help/forms/using/configuring-draft-submission-storage.md) , con implementaciones personalizadas para reemplazar la funcionalidad predeterminada. Para obtener información detallada sobre los métodos necesarios en una implementación personalizada para almacenar contenido en una ubicación segura, consulte [Personalización de los servicios de datos Borrador y Envío](/help/forms/using/custom-draft-submission-data-services.md) y [Almacenamiento personalizado para borradores y componentes de envíos.](/help/forms/using/adding-custom-storage-provider-forms.md)

La documentación de AEM Forms proporciona un [Ejemplo para integrar el componente Borradores y envíos con la base de datos](integrate-draft-submission-database.md). Puede utilizar la implementación de muestra para desarrollar su propia implementación personalizada.

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Crear página de portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Enumerar formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalización del almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalización de plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)
