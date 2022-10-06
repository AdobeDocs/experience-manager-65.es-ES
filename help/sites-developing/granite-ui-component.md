---
title: Creación de un nuevo componente de campo de interfaz de usuario de Granite
seo-title: Creating a New Granite UI Field Component
description: La interfaz de usuario de Granite proporciona una serie de componentes diseñados para utilizarse en formularios denominados campos
seo-description: Granite UI provides a range of components designed to be used in forms, called fields
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# Creación de un nuevo componente de campo de interfaz de usuario de Granite{#creating-a-new-granite-ui-field-component}

La interfaz de usuario de Granite proporciona una serie de componentes diseñados para utilizarse en formularios; se denominan *campos* en el vocabulario de la interfaz de usuario de Granite. Los componentes de formulario estándar de Granite están disponibles en:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Estos campos de formulario de la interfaz de usuario de Granite son de especial interés, ya que se utilizan para [cuadros de diálogo de componentes](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Para obtener más información sobre los campos, consulte la [Documentación de Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Utilice el marco de Granite UI Foundation para desarrollar o ampliar componentes de Granite. Tiene dos elementos:

* del lado del servidor:

   * una colección de componentes de base

      * base: modular, composable, legible, reutilizable
      * componentes: componentes de Sling
   * ayuda para el desarrollo de aplicaciones


* lado del cliente:

   * una colección de clientlibs que proporcionan un vocabulario (es decir, la extensión del idioma del HTML) para lograr patrones de interacción genéricos a través de una interfaz de usuario impulsada por Hypermedia

El componente genérico de la interfaz de usuario de Granite `field` consta de dos archivos de interés:

* `init.jsp`: gestiona el procesamiento genérico; etiquetado, descripción y proporciona el valor del formulario que necesitará al procesar el campo.
* `render.jsp`: aquí es donde se realiza la representación real del campo y debe anularse para el campo personalizado; está incluido por `init.jsp`.

Consulte la [Documentación de la interfaz de usuario de Granite: Campo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) si desea más detalles.

Para ver ejemplos, consulte:

* `cqgems/customizingfield/components/colorpicker`

   * proporcionado por el [Ejemplo de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Como este mecanismo utiliza JSP, i18n y XSS no se incluyen de serie. Esto significa que tendrá que internacionalizar y escapar de sus cadenas. El siguiente directorio contiene los campos genéricos de una instancia estándar, puede utilizarlos como referencia:
>
>`/libs/granite/ui/components/foundation/form` directory

## Creación de la secuencia de comandos del lado del servidor para el componente {#creating-the-server-side-script-for-the-component}

El campo personalizado solo debe anular la variable `render.jsp` , donde se proporciona el marcado para el componente. Puede considerar el JSP (es decir, el script de renderización) como un envoltorio para el marcado.

1. Cree un nuevo componente que use el `sling:resourceSuperType` propiedad de la que heredar:

   `/libs/granite/ui/components/foundation/form/field`

1. Anule la secuencia de comandos:

   `render.jsp`

   En esta secuencia de comandos, se debe generar el marcado de hipermedios (es decir, el marcado enriquecido, que contiene la asequibilidad de los hipermedios) para que el cliente sepa cómo interactuar con el elemento generado. Esto debe seguir el estilo de codificación de la interfaz de usuario de Granite del lado del servidor.

   Al personalizar, el único contrato que *must* el cumplimiento es leer el valor del formulario (inicializado en `init.jsp`) de la solicitud utilizando:

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Para obtener más información, consulte la implementación de los campos predeterminados de la interfaz de usuario de Granite; por ejemplo, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >En este momento, JSP es el método preferido para las secuencias de comandos, ya que el paso de información de un componente a otro (que es bastante frecuente en el contexto de los formularios o campos) no se consigue fácilmente en HTL.

## Creación de la biblioteca del cliente para el componente {#creating-the-client-library-for-the-component}

Para añadir un comportamiento específico del lado del cliente a su componente:

1. Crear una clientlib de categoría `cq.authoring.dialog`.
1. Crear una clientlib de categoría `cq.authoring.dialog` y defina su `JS`/ `CSS` dentro de él.

   Defina su `JS`/ `CSS` dentro de la clientlib.

   >[!NOTE]
   >
   >En este momento, la interfaz de usuario de Granite no proporciona ningún oyente ni gancho listos para usar que pueda utilizar directamente para agregar el comportamiento de JS. Por lo tanto, para añadir un comportamiento JS adicional al componente, debe implementar un vínculo JS a una clase personalizada que luego asigne al componente durante la generación del marcado.
