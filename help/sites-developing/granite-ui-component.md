---
title: Creación de un nuevo componente de campo de IU de Granite
seo-title: Creating a New Granite UI Field Component
description: La interfaz de usuario de Granite proporciona una serie de componentes diseñados para utilizarse en formularios, denominados campos
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

# Creación de un nuevo componente de campo de IU de Granite{#creating-a-new-granite-ui-field-component}

La interfaz de usuario de Granite proporciona una serie de componentes diseñados para utilizarse en formularios; estos se denominan *campos* en el vocabulario de la IU de Granite. Los componentes de formulario estándar de Granite están disponibles en:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Estos campos de formulario de la interfaz de usuario de Granite son de especial interés para [cuadros de diálogo de componentes](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Para obtener más información sobre los campos, consulte la [Documentación de Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Utilice el marco de trabajo Granite UI Foundation para desarrollar o ampliar componentes de Granite. Tiene dos elementos:

* del lado del servidor:

   * una colección de componentes de base

      * base: modular, componible, capas, reutilizable
      * componentes: componentes de Sling
   * ayudantes para el desarrollo de aplicaciones


* lado del cliente:

   * una colección de clientlibs que proporciona cierto vocabulario (es decir, extensión del lenguaje HTML) para lograr patrones de interacción genéricos a través de una interfaz de usuario impulsada por hipermedia

El componente de interfaz de usuario de Granite genérico `field` se compone de dos archivos de interés:

* `init.jsp`: administra el procesamiento genérico; el etiquetado, la descripción y proporciona el valor de formulario que necesitará al procesar el campo.
* `render.jsp`: aquí es donde se realiza la representación real del campo, que debe anularse para el campo personalizado. se incluye mediante `init.jsp`.

Consulte la [Documentación de la IU de Granite: campo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) si desea obtener más detalles.

Para ver ejemplos, consulte:

* `cqgems/customizingfield/components/colorpicker`

   * proporcionadas por el [Ejemplo de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Como este mecanismo utiliza JSP, i18n y XSS no se proporcionan listas para usar. Esto significa que tendrá que internacionalizarse y escapar de sus cadenas. El siguiente directorio contiene los campos genéricos de una instancia estándar, que puede utilizar como referencia:
>
>`/libs/granite/ui/components/foundation/form` directorio

## Creación del script del lado del servidor para el componente {#creating-the-server-side-script-for-the-component}

El campo personalizado solo debe anular la variable `render.jsp` , donde se proporciona el marcado para el componente. Puede considerar JSP (es decir, el script de procesamiento) como un envoltorio para el marcado.

1. Cree un nuevo componente que utilice la variable `sling:resourceSuperType` propiedad de la que heredar:

   `/libs/granite/ui/components/foundation/form/field`

1. Anule la secuencia de comandos:

   `render.jsp`

   En este script, debe generar el marcado hipermedia (es decir, el marcado enriquecido, que contiene la asequibilidad de hipermedia) para que el cliente sepa cómo interactuar con el elemento generado. Esto debe seguir el estilo de codificación del lado del servidor de Granite UI.

   Al personalizar, el único contrato que *debe* fulfill es para leer el valor del formulario (inicializado en `init.jsp`) de la solicitud utilizando:

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Para obtener más información, consulte la implementación de los campos de interfaz de usuario de Granite predeterminados; por ejemplo, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >Por el momento, JSP es el método de script preferido, ya que pasar información de un componente a otro (que es bastante frecuente en el contexto de formularios/campos) no se logra fácilmente en HTL.

## Creación de la biblioteca de cliente para el componente {#creating-the-client-library-for-the-component}

Para agregar un comportamiento específico del lado del cliente al componente:

1. Crear una clientlib de categoría `cq.authoring.dialog`.
1. Crear una clientlib de categoría `cq.authoring.dialog` y defina su `JS`/ `CSS` dentro de él.

   Defina su `JS`/ `CSS` dentro de clientlib.

   >[!NOTE]
   >
   >Por el momento, la interfaz de usuario de Granite no proporciona escuchas o enlaces predeterminados que pueda utilizar directamente para agregar el comportamiento de JS. Por lo tanto, para agregar un comportamiento JS adicional al componente, debe implementar un vínculo JS a una clase personalizada que luego asigne al componente durante la generación de marcado.
