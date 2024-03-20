---
title: Configure RTE para varios editores in situ.
description: Cree varios editores locales en Adobe Experience Manager configurando el Editor de texto enriquecido.
contentOwner: AG
exl-id: 03030317-8b7d-408a-bdfd-619824d7260c
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Configuración de varios editores in situ {#configure-multiple-in-place-editors}

Puede configurar el Editor de texto enriquecido en Adobe Experience Manager para que tenga varios editores locales. Cuando está configurado, puede seleccionar el contenido adecuado y abrir el editor correspondiente.

![Un editor in situ específico](assets/rte-inplace-editor.png)

## Configuración de varios editores {#configure-multiple-editors}

Para habilitar varios editores locales, utilice la estructura de un `cq:InplaceEditingConfig` el tipo de nodo se ha mejorado con la definición de `cq:ChildEditorConfig` tipo de nodo.

Por ejemplo:

```js
   /**
       * Configures in-place editing of a component.
       *
       * @prop active true to activate in-place editing for the component.
       * @prop editorType ID of in-place editor to use.
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional).
       * @node config editor's config (used if no configPath is specified; optional).
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a sub-component. The name of the this node is
      * used as DD ID.
      *
      * @prop type type of the inline editor. For example, ["image"].
      * @prop title Title of the inline editor.
      * @prop icon Icon to represent the inline editor.
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

Para configurar varios editores, siga estos pasos:

1. En el nodo `cq:inplaceEditing` (de tipo `cq:InplaceEditingConfig`) defina las siguientes propiedades:

   * Nombre:`editorType`
   * Tipo: `String`
   * Valor: `hybrid`

1. En este nodo, cree un nodo:

   * Nombre: `cq:ChildEditors`
   * Tipo: `nt:unstructured`

1. En `cq:childEditors` , cree un nodo para cada editor en contexto:

   * Nombre: el nombre de cada nodo es el nombre de la propiedad que representa, como en el caso de los destinos de colocación. Por ejemplo, `image` y `text`.
   * Tipo: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >Existe una correlación entre los destinos de colocación definidos y los editores secundarios. El nombre del `cq:ChildEditorConfig` El nodo se considera como el ID de destino de colocación, para utilizarlo como parámetro del editor secundario seleccionado. Si el subárea editable no tiene un destino de colocación, por ejemplo, en un componente de texto, el nombre del editor secundario se seguirá considerando como un ID para identificar el área editable correspondiente.

1. En cada uno de estos nodos (`cq:ChildEditorConfig`) defina las propiedades:

   * Nombre: `type`.
   * Valor: nombre del editor local registrado; por ejemplo, `image` y `text`.

   * Nombre: `title`.
   * Valor: título mostrado en la lista de selección de componentes de los editores disponibles. Por ejemplo, `Image` y `Text`.

### Configuración adicional para editores de texto enriquecido {#additional-configuration-for-rich-text-editors}

La configuración de varios editores de texto enriquecido es ligeramente diferente, ya que puede configurar cada instancia de RTE individual por separado. Para obtener más información, consulte [configuración del Editor de texto enriquecido](/help/sites-administering/rich-text-editor.md). Para que varios RTE creen una configuración para cada RTE local. El Adobe recomienda crear el nuevo nodo de configuración en `cq:InplaceEditingConfig` ya que cada RTE individual puede tener una configuración diferente. En el nuevo nodo, cree cada configuración de RTE individual.

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    someconfig
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>Sin embargo, para RTE, la variable `configPath` La propiedad se admite cuando solo hay una instancia del editor de texto (subárea editable) en el componente. Este uso de `configPath` se proporciona para admitir la compatibilidad con versiones anteriores de los cuadros de diálogo de interfaz de usuario del componente.

>[!CAUTION]
>
>No asigne un nombre al nodo de configuración RTE como `config`. De lo contrario, las configuraciones de RTE solo están disponibles para los administradores y no para los usuarios del grupo `content-author`.

## Muestras de código {#code-samples}

Puede encontrar el código de esta página en [proyecto aem-authoring-hybrideditors en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors). Puede descargar el proyecto completo como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip).

## Adición de un editor in situ {#add-an-in-place-editor}

Para obtener información general sobre cómo agregar un editor in situ, consulte el documento [personalizar la creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

>[!MORELIKETHIS]
>
>* [Configuración del editor de texto enriquecido en Experience Manager](/help/sites-administering/rich-text-editor.md).
