---
title: Componente de proyectos y presentaciones
seo-title: Componente de proyectos y presentaciones
description: El componente Borradores y envíos enumera los formularios que están en estado borrador y que ya se han enviado. Puede personalizar el aspecto y el estilo del componente.
seo-description: El componente Borradores y envíos enumera los formularios que están en estado borrador y que ya se han enviado. Puede personalizar el aspecto y el estilo del componente.
uuid: 42c205b5-3141-4b80-85d9-dad921e223a2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: ad71b423-02e1-4476-9c7c-f832cea6b0a6
docset: aem65
translation-type: tm+mt
source-git-commit: 23252989bb8649b2f0b96a58972c831257e0c5dc

---


# Componente de proyectos y presentaciones{#drafts-and-submissions-component}

El componente Borradores y envíos enumera todos los formularios que están en estado de borrador y los formularios que ya se han enviado. El componente tiene secciones independientes (fichas) para borradores y formularios enviados. Los usuarios solo pueden ver los borradores y los formularios enviados.

## Configuración del componente {#configuring-the-component}

El componente Borradores y envíos tiene dos fichas: Borradores y presentaciones.

Para permitir que el envío de un formulario adaptable aparezca en la ficha Envíos, establezca la acción **** Enviar en Acción **[de envío de](../../forms/using/configuring-submit-actions.md)Forms Portal. De forma alternativa,**active la opción Envío de Forms Portal. Cada vez que un usuario envía el formulario, éste se agrega a la ficha envíos.

La funcionalidad de borradores está activada de forma predeterminada. Cuando un usuario hace clic en **Guardar** en un formulario adaptable, el formulario se agrega a la ficha Borradores.

Realice los siguientes pasos para agregar y configurar un componente Borradores y envíos:

1. Arrastre y suelte el componente **Borradores y envíos** en la categoría Document Services del navegador de componentes en la página.
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
   <td>Especifica el número máximo de resultados que se van a mostrar. Si el recuento de resultados aumenta el límite de resultados totales, aparecerá un <strong>vínculo Más </strong>en la parte inferior del componente. Al hacer clic en <strong>Más </strong>se muestran todos los formularios. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Tipo de estilo</td>
   <td>Especifica el estilo del componente. Puede especificar <strong>Sin estilo</strong>, Estilo <strong></strong>predeterminado o Estilo <strong></strong> personalizado para enumerar los formularios. En la opción Estilo personalizado, puede especificar la ruta del archivo CSS personalizado en el <strong>campo </strong>Ruta de estilo<strong>personalizada.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Ruta de estilo personalizada</td>
   <td>Si selecciona la opción Estilo <strong></strong> personalizado en el campo Tipo <strong>de</strong> estilo, utilice el campo Ruta <strong>de estilo</strong> personalizada para especificar la ruta del archivo CSS personalizado. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Opciones de visualización</td>
   <td><p>Especifica las fichas que se van a mostrar. Puede elegir mostrar formularios de borrador, formularios enviados o ambos. </p> <p><strong></strong> Nota<em>: En el caso de las opciones <strong>de</strong>visualización, si selecciona una opción distinta a <strong>ambas</strong>, no se utiliza la opción de campo de ficha <strong></strong> predeterminada.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Ficha predeterminada</td>
   <td>Especifica la ficha que se mostrará cuando se cargue la página del portal de formularios. Puede elegir entre la ficha <strong>Formularios</strong> de dibujo y la ficha <strong>Formularios</strong>enviados.</td>
  </tr>
  <tr>
   <td>Configuración de la ficha Formularios de borrador</td>
   <td>Título personalizado</td>
   <td>Especifica el título de la ficha <strong>Borradores de formularios</strong> . El valor predeterminado es <strong>Borrador de formularios.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Plantilla de diseño</td>
   <td>Especifica la presentación que se va a utilizar para la lista de formularios de borrador.</td>
  </tr>
  <tr>
   <td>Configuración de la ficha Formularios enviados</td>
   <td>Título personalizado </td>
   <td>Especifica el título de la <strong>ficha Formularios </strong>enviados. El valor predeterminado es Formularios <strong>enviados.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Plantilla de diseño</td>
   <td>Especifica la presentación que se va a utilizar en la<strong> lista Formularios </strong>enviados. </td>
  </tr>
 </tbody>
</table>

## Personalización del almacenamiento {#customizing-the-storage}

Cuando se utiliza la acción de envío de Forms Portal o se activa la opción Almacenar datos en el portal de formularios en un formulario adaptable, los datos del formulario se almacenan en el repositorio de AEM. En un entorno de producción, se recomienda no almacenar datos de formulario enviados o borrador en el repositorio de AEM. En su lugar, debe integrar los borradores y el componente de envío con un almacenamiento seguro como la base de datos empresarial para almacenar borradores y datos de formularios enviados.

Forms Portal le permite almacenar datos en el repositorio local de AEM, en el repositorio remoto de AEM o en una base de datos. AEM Forms permite personalizar la implementación del almacenamiento de datos de usuario para borradores y envíos. Puede anular los métodos predeterminados para especificar cómo se almacenan los datos de borradores y envíos en un almacenamiento de su elección. Por ejemplo, puede almacenar los datos en un almacén de datos implementado actualmente en su organización.

Forms Portal proporciona servicios predeterminados (API) para almacenar datos en el repositorio crx de instancias de publicación de AEM Forms locales y remotas. Puede reemplazar las implementaciones predeterminadas, descritas en [Configuración de servicios de almacenamiento para borradores y artículos de envío](/help/forms/using/configuring-draft-submission-storage.md) , por implementaciones personalizadas para reemplazar la funcionalidad predeterminada. Para obtener información detallada sobre los métodos requeridos en una implementación personalizada para almacenar contenido en una ubicación segura, consulte [Personalización de los servicios](/help/forms/using/custom-draft-submission-data-services.md) de datos de borradores y envíos y Almacenamiento [personalizado para borradores y componentes de envíos.](/help/forms/using/adding-custom-storage-provider-forms.md)

La documentación de AEM Forms proporciona un [Ejemplo para integrar los borradores y el componente de envíos con la base de datos](integrate-draft-submission-database.md). Puede utilizar la implementación de muestra para desarrollar su propia implementación personalizada.

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Crear página del portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Lista de formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalización del almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente de borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalización de plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)
