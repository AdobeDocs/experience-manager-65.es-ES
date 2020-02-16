---
title: Sincronización de formularios adaptables con plantillas de formulario XFA
seo-title: Sincronización de formularios adaptables con plantillas de formulario XFA
description: Sincronización de formularios adaptables con archivos XFA/XDP.
seo-description: Sincronización de formularios adaptables con archivos XFA/XDP.
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Sincronización de formularios adaptables con plantillas de formulario XFA{#synchronizing-adaptive-forms-with-xfa-form-templates}

## Introducción {#introduction}

Puede crear un formulario adaptable basado en una plantilla de formulario XFA ( `*.XDP` archivo). Esta reutilización le permite preservar su inversión en formularios XFA existentes. Para obtener información sobre cómo utilizar una plantilla de formulario XFA para crear un formulario adaptable, [cree un formulario adaptable basado en una plantilla](../../forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-an-xfa-form-template-p).

Puede reutilizar campos del archivo XDP en el formulario adaptable. Estos campos se denominan campos enlazados. Las propiedades de los campos enlazados (como secuencias de comandos, etiquetas y formato de visualización) se copian del archivo XDP. También puede optar por anular el valor de algunas de estas propiedades.

AEM Forms permite mantener los campos de los formularios adaptables sincronizados con los cambios que se realicen posteriormente en los campos correspondientes del archivo XDP. En este artículo se explica cómo activar esta sincronización.

![Puede arrastrar campos de un formulario XFA a un formulario adaptable](assets/drag-drop-xfa.gif.gif)

En el entorno de creación de AEM Forms, puede arrastrar campos de un formulario XFA (izquierda) a un formulario adaptable (derecha)

## Requisitos previos {#prerequisites}

Para utilizar la información de este artículo, se recomienda familiarizarse con las siguientes áreas:

* [Creación de un formulario adaptable](../../forms/using/creating-adaptive-form.md)

* XFA (XML Forms Architecture)

Para utilizar los recursos que se proporcionan para el ejemplo del artículo, descargue el paquete de muestra tal como se explica en la siguiente sección, [Paquete](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-sample-package-p)de muestra.

## Paquete de muestra {#sample-package}

El artículo utiliza un ejemplo para mostrar cómo sincronizar el formulario adaptable con una plantilla de formulario XFA actualizada. Los recursos utilizados en el ejemplo están disponibles en un paquete, que se puede descargar desde la sección [Descargas](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-downloads-p) de este artículo.

Después de cargar el paquete, puede ver estos recursos en la interfaz de usuario de AEM Forms.

Instale el paquete mediante el administrador de paquetes: `https://<server>:<port>/crx/packmgr/index.jsp`

El paquete contiene los siguientes recursos:

1. `sample-form.xdp`:: Plantilla de formulario XFA utilizada como ejemplo

1. `sample-xfa-af`:: Formulario adaptable basado en el archivo sample-form.xdp. Sin embargo, este formulario adaptable no incluye campos. En el siguiente paso, agregaremos contenido a este formulario adaptable.

### Agregar contenido a un formulario adaptable {#add-content-to-adaptive-form-br}

1. Vaya a https://&lt;server>:&lt;port>/aem/forms.html. Introduzca sus credenciales si se les solicita.
1. Abra el ejemplo-af-xfa para editarlo en modo de autor.
1. En el navegador de contenido de la barra lateral, elija la ficha Objetos del modelo de datos. Arrastre NumericField1 y TextField1 al formulario adaptable.
1. Cambie el Título del campo numérico1 de Campo **** numérico a Campo numérico **AF.**

>[!NOTE]
>
>En los pasos anteriores, se sobrescribió una propiedad de un campo en el archivo XDP. Por lo tanto, esta propiedad no se sincronizará si la propiedad correspondiente del archivo XDP se modifica más adelante.

## Detección de cambios en el archivo XDP {#detecting-changes-in-xdp-file}

Siempre que se produzca algún cambio en un archivo XDP o un fragmento, la interfaz de usuario de AEM Forms marca todos los formularios adaptables basados en el archivo XDP o el fragmento.

Después de actualizar un archivo XDP, debe cargarlo de nuevo en la interfaz de usuario de AEM Forms para marcar los cambios.

Por ejemplo, permítanos actualizar el `sample-form.xdp` archivo siguiendo los pasos siguientes:

1. Vaya a `https://<server>:<port>/projects.html.` Introduzca sus credenciales si se le solicita.
1. Haga clic en la ficha Formularios de la izquierda.
1. Descargue el `sample-form.xdp` archivo en su equipo local. El archivo XDP se descarga como un `.zip` archivo, que se puede extraer con cualquier utilidad de descompresión de archivos.

1. Abra el `sample-form.xdp` archivo y cambie el título del campo TextField1 de Campo **de** texto a **Mi campo** de texto.

1. Vuelva a cargar el `sample-form.xdp` archivo en la interfaz de usuario de AEM Forms.

Si se actualiza un archivo XDP, verá un icono en el editor al editar los formularios adaptables basados en el archivo XDP. Este icono indica que el formulario adaptable no está sincronizado con el archivo XDP. En la siguiente imagen, vea el icono situado junto a la barra lateral.

![Icono para mostrar que el formulario adaptable no está sincronizado con el archivo XDP](assets/sync-af-xfa.png)

## Sincronización de formularios adaptables con el archivo XDP más reciente {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

Cuando se abre un formulario adaptable que no está sincronizado con el archivo XDP para la creación la próxima vez, se muestra el siguiente mensaje: Se ha actualizado el **esquema/plantilla de formulario para el formulario adaptable.`Click Here`para volver a basarlo en la nueva versión.**

Al hacer clic en el mensaje, se sincronizan los campos del formulario adaptable con los campos correspondientes del archivo XDP.

Para ver el ejemplo utilizado en este artículo, abra `sample-xfa-af` en modo de creación. El mensaje se muestra hacia la parte inferior del formulario adaptable.

![Mensaje que solicita sincronizar el formulario adaptable con el archivo XDP](assets/sync-af-xfa-1.png)

### Actualización de las propiedades {#updating-the-properties}

Todas las propiedades que se copiaron del archivo XDP al formulario adaptable se actualizan, excepto las propiedades que el autor ha sobrescrito explícitamente en el formulario adaptable (del cuadro de diálogo Componente). La lista de propiedades que se han actualizado está disponible en los registros del servidor.

Para actualizar las propiedades en el formulario adaptable de ejemplo, haga clic en el vínculo (etiquetado `"Click Here"`) del mensaje. El título de TextField1 cambia de Campo **de** texto a **Mi campo** de texto.

![update-property](assets/update-property.png)

>[!NOTE]
>
>No se cambió la etiqueta Campo numérico AF porque se ha anulado esta propiedad del cuadro de diálogo de propiedades de componente, tal como se describe en [Agregar contenido a formularios](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p)adaptables.

### Adición de nuevos campos del archivo XDP a un formulario adaptable {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

Los campos que se agreguen más adelante al archivo XDP original aparecerán en la ficha Jerarquía de formulario y podrá arrastrar dichos campos nuevos al formulario adaptable.

No es necesario hacer clic en el vínculo del mensaje de error para actualizar los campos de la ficha Jerarquía de formularios.

### Campos eliminados en el archivo XDP {#deleted-fields-in-xdp-file}

Si un campo copiado anteriormente en un formulario adaptable se elimina de un archivo XDP, se muestra un mensaje de error en el modo de creación que indica que el campo no existe en el archivo XDP. En estos casos, elimine manualmente el campo del formulario adaptable o borre la `bindRef` propiedad en el cuadro de diálogo del componente.

Los siguientes pasos ilustran este flujo de uso para los recursos en el ejemplo utilizado en este artículo:

1. Actualice el `sample-form.xdp` archivo y elimine NumericField1.
1. Carga del `sample-form.xdp` archivo en la interfaz de usuario de AEM Forms
1. Abra el formulario `sample-xfa-af` adaptable para la creación. Se muestra el siguiente mensaje de error: Se ha actualizado la plantilla de esquema/formulario para el formulario adaptable. `Click Here` para volver a basarlo en la nueva versión.

1. Haga clic en el vínculo (con la etiqueta &quot; `Click Here`&quot;) del mensaje. Se muestra un mensaje de error que indica que el campo ya no existe en el archivo XDP.

![Error al eliminar un elemento en el archivo XDP](assets/no-element-xdp.png)

El campo que se ha eliminado también se marca con un icono para indicar un error en el campo.

![Icono de error en el campo](assets/error-field.png)

>[!NOTE]
>
>Los campos del formulario adaptable que tienen un enlace incorrecto (un valor no válido `bindRef` en el cuadro de diálogo de edición) también se consideran campos eliminados. Si el autor no corrige estos errores y publica el formulario adaptable, el campo se trata como un campo de formulario adaptable normal sin enlazar y se incluye en la sección sin enlazar del archivo XML de salida.

## Descargas {#downloads}

Content-package para el ejemplo de este artículo

[Obtener archivo](assets/sample-xfa-af-sync-1.0.zip)
