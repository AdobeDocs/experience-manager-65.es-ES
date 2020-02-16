---
title: Configuración de varios editores in situ
seo-title: Configuración de varios editores in situ
description: Es posible configurar el componente para que tenga varios editores in situ
seo-description: Es posible configurar el componente para que tenga varios editores in situ
uuid: 4abbfcd5-fe1b-4c02-b115-97db20e60e1e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 0fac1e4a-f08f-4c46-b070-cb1d5a05b6e0
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# Configuración de varios editores in situ{#configuring-multiple-in-place-editors}

Es posible configurar el componente para que tenga varios editores in-situ en la IU táctil.

Cuando esté configurado, puede seleccionar el contenido adecuado y abrir el editor correspondiente. Por ejemplo:

![chlimage_1-8](assets/chlimage_1-8a.png)

## Configuración de varios editores {#configuring-multiple-editors}

Para habilitar varios editores in-situ, la estructura de un tipo de `cq:InplaceEditingConfig` nodo se ha mejorado con la definición de tipo de `cq:ChildEditorConfig` nodo.

Por ejemplo:

```
   /**
       * Configures inplace editing of a component.
       *
       * @prop active true to activate inplace editing for the component
       * @prop editorType ID of inplace editor to use
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional)
       * @node config editor's config (used if no configPath is specified; optional)
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a subcomponent. The name of the this node will
      * be used as DD id.
      *
      * @prop type type of the inline editor. eg: ["image"]
      * @prop title totle od the inline editor
      * @prop icon icon to represent the inline editor
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

Para configurar varios editores:

1. En el nodo `cq:inplaceEditing` (de tipo `cq:InplaceEditingConfig`), defina la propiedad:

   * Nombre:`editorType`
   * Tipo: `String`
   * Value: `hybrid`

1. En este nodo, cree un nuevo nodo:

   * Nombre: `cq:ChildEditors`
   * Tipo: `nt:unstructured`

1. En el `cq:childEditors` nodo, cree un nuevo nodo para cada editor in-situ:

   * Nombre: el nombre de cada nodo debe ser el nombre de la propiedad que representa (como con los destinos de colocación). Por ejemplo, `image`, `text`.
   * Tipo: cq: `ChildEditorConfig`
   >[!NOTE]
   >
   >Existe una correlación entre los objetivos de colocación definidos y los editores secundarios. El nombre del `cq:ChildEditorConfig` nodo se considerará el ID de destino de colocación, para utilizarlo como parámetro del editor secundario seleccionado. Si el subárea editable no tiene un destino de colocación (por ejemplo, como con un componente de texto), el nombre del editor secundario se seguirá considerando como ID para identificar el área editable correspondiente.

1. En cada uno de estos nodos ( `cq:ChildEditorConfig`) defina las propiedades:

   * Nombre: `type`
   * Valor: nombre del editor in situ registrado; por ejemplo, `image`, `text`

   * Nombre: `title`
   * Valor: el título que desea mostrar en la lista de selección de componentes (de editores disponibles); por ejemplo, `Image`, `Text`

### Configuración adicional para editores de texto enriquecido {#additional-configuration-for-rich-text-editors}

La configuración de varios editores de texto enriquecido es ligeramente diferente, ya que puede configurar cada instancia de RTE por separado.

>[!NOTE]
>
>Para obtener más información, consulte [Configuración del editor](/help/sites-administering/rich-text-editor.md)de texto enriquecido.

Para tener varios RTEs necesita una configuración para cada RTE in-situ:

* En `cq:InplaceEditingConfig` definir un `config` nodo.

   * En el `config` nodo, defina cada configuración RTE individual.

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    config
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>Se recomienda definir el `config` nodo en `cq:InplaceEditingConfig` función de que cada RTE individual puede tener una configuración diferente.
>
>Sin embargo, para RTE, la `configPath` propiedad se admite cuando solo hay una instancia del editor de texto (subárea editable) en el componente. Este uso de `configPath` se proporciona para admitir la compatibilidad con versiones anteriores de los cuadros de diálogo más antiguos de la interfaz de usuario del componente.

## Ejemplos de código {#code-samples}

**CÓDIGO DE GITHUB**

Puede encontrar el código de esta página en GitHub

* [Open aem-authoring-hybrideditors project en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)

## Adición de un editor in-situ {#adding-an-in-place-editor}

Para obtener información general sobre cómo agregar un editor in-situ, consulte el documento [Personalización de la creación](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)de páginas.
