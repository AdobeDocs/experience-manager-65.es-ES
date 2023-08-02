---
title: Acceder y cumplimentar formularios publicados
description: El portal de formularios proporciona a los desarrolladores web componentes para crear y personalizar un portal de formularios en sitios web creados con Adobe Experience Manager (AEM).
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: aedf890c-a2f1-412f-8897-2492ffab335a
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 90%

---

# Acceder y cumplimentar formularios publicados{#accessing-and-filling-published-forms}

En una configuración de implementación del portal centrado en formularios, el desarrollo de los formularios y del portal son dos actividades distintas. Mientras los diseñadores de formularios diseñan y almacenan formularios en un repositorio, los desarrolladores web crean una aplicación web para enumerar formularios y controlar los envíos. Los formularios se copian en el nivel web, ya que no hay ninguna comunicación entre el repositorio de formularios y la aplicación web.

Esto suele provocar problemas con la administración de los retrasos de configuración y producción. Por ejemplo, si hay una versión más reciente de un formulario en el repositorio, el diseñador reemplazará el formulario en el nivel web, modificará la aplicación web y volverá a implementar el formulario en el sitio público. Volver a implementar la aplicación web puede causar cierto tiempo de inactividad en el servidor. Dado que el tiempo de inactividad del servidor es una actividad planificada, los cambios no pueden ser enviados al sitio público inmediatamente.

El portal de formularios reduce los gastos generales de administración y los retrasos en la producción. Proporciona a los desarrolladores web componentes para crear y personalizar el portal de formularios en sitios web creados con Adobe Experience Manager (AEM).

Para obtener más información sobre el portal de formularios y sus características, consulte [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md).

## Introducción al portal de formularios {#getting-started-with-forms-portal}

Navegue hasta la página publicada del portal de formularios. Para obtener más información sobre cómo crear una página de portal de formularios, consulte [Crear una página de portal de formularios](../../forms/using/creating-form-portal-page.md).

El componente Buscar y listar del portal de formularios muestra los formularios disponibles en la instancia de publicación del servidor de AEM. Esta lista incluye todos los formularios o los formularios definidos en el filtro en el momento de crear la página del portal de formularios. Una página del portal de formularios tiene un aspecto similar al que se muestra en la siguiente imagen:

![Página de ejemplo del portal de formularios ](assets/forms-portal-page.png)

Página de ejemplo del portal de formularios 

### Buscar y listar {#search-and-lister}

El componente Buscar y listar permite agregar la siguiente funcionalidad al portal de formularios:

* Enumerar formularios en el panel, la tarjeta o la vista de cuadrícula que estén disponibles de forma predeterminada. También admite formularios personalizados templatesList de carpetas específicas en Forms Manager.
* Especificar cómo se procesan los formularios: HTML5, PDF o ambos.
* Especificar cómo se procesan los formularios PDF y XFA: HTML5, PDF o ambos. Formularios que no son XFA como HTML5.
* Permite buscar formularios basados en criterios, como propiedades, metadatos y etiquetas de formularios.
* Enviar datos de formulario a un servlet.
* Utilizar hojas de estilo personalizadas (CSS) para personalizar la apariencia del portal.
* Crea vínculos a formularios.

Puede buscar formularios en la página del portal de formularios mediante las siguientes opciones:

* Búsqueda de texto completo
* Búsqueda avanzada

La búsqueda de texto completo permite encontrar y enumerar formularios en función de las palabras clave especificadas.

![Cuadro de diálogo de búsqueda avanzada](assets/search-panel.png)

Cuadro de diálogo de búsqueda avanzada

La búsqueda avanzada permite buscar formularios en función de las propiedades especificadas del formulario. Esto proporciona un resultado más específico que la búsqueda de texto completo. La búsqueda avanzada incluye la búsqueda basada en etiquetas, propiedades (como autor, descripción y título), fecha de modificación y texto completo.

La lista muestra los formularios en función de los parámetros de búsqueda. Cada formulario del resultado de la búsqueda se muestra con un icono que es un hipervínculo al formulario asociado. Puede hacer clic en el icono para abrir y trabajar con el formulario asociado.

### Rellenar un formulario {#filling-a-form}

![Formulario adaptable de ejemplo](assets/filling_a_form.png)

Formulario adaptable de ejemplo

Se puede acceder a los formularios desde el vínculo proporcionado junto con el formulario en el componente Buscar y listar de la página.

Cada formulario contiene información de ayuda que permite al usuario rellenarlo.

#### Borradores y envíos {#drafts-and-submission}

Si lo desea, el usuario puede guardar el borrador de un formulario haciendo clic en **Guardar**. Esto permite al usuario trabajar en un formulario durante un periodo de tiempo antes de enviarlo.

Los datos rellenados en el formulario (incluidos los archivos adjuntos) se guardarán como borrador en el servidor. El borrador de un formulario se puede guardar cualquier número de veces. El formulario guardado aparecerá en la pestaña Borradores del componente Borradores y envíos de la página.

Al cumplimentar el formulario, el usuario envía los formularios al hacer clic en el botón Enviar en el formulario. Los formularios enviados aparecerán en la pestaña Envíos del componente Borradores y envíos de la página.

>[!NOTE]
>
>Los formularios enviados aparecerán en la pestaña Formularios enviados solo si la acción de envío del formulario adaptable está configurada como Acción de envío del portal de formularios. Para obtener información detallada sobre las acciones de envío, consulte [Configurar la acción de envío](../../forms/using/configuring-submit-actions.md).

![Componente Borradores y envíos](assets/draft-submission.png)

Componente Borradores y envíos

## Inicie un formulario nuevo con los datos de un formulario enviado {#start-a-new-form-using-submitted-form-data}

Algunos formularios que debe rellenarlos y enviarlos con frecuencia. Por ejemplo, el formulario para presentar la declaración de impuestos individual se envía cada año. En estos casos, mientras que parte de la información cambia cada vez que se rellena el formulario, la mayoría de ella, como los detalles personales y familiares, no cambia. Sin embargo, debe rellenar todo el formulario de nuevo, desde cero.

AEM Forms puede ayudar a optimizar la experiencia de cumplimentación de formularios y reducir significativamente el tiempo para rellenar y enviar un formulario de nuevo. Los usuarios finales pueden iniciar un nuevo formulario con los datos de un formulario enviado. Esta funcionalidad está integrada en el [Componente Borradores y envíos](../../forms/using/draft-submission-component.md). Cuando se agrega el componente Borradores y envíos a la página del portal de formularios y se publica, los usuarios finales ven una opción en las pestañas Enviado Forms y Borrador Forms para iniciar un nuevo formulario con los datos de un formulario enviado. La siguiente imagen resalta esa opción.

![start-a-new-form](assets/start-a-new-form.png)

Al hacer clic en el botón para iniciar un nuevo formulario, se abrirá un formulario nuevo con datos del formulario enviado correspondiente. Ahora puede revisar y actualizar la información, según sea necesario y enviar el formulario.
