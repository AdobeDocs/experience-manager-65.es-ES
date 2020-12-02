---
title: Creación de un nuevo componente de campo de interfaz de usuario de Granite
seo-title: Creación de un nuevo componente de campo de interfaz de usuario de Granite
description: La interfaz de usuario de Granite proporciona una serie de componentes diseñados para utilizarse en formularios, denominados campos
seo-description: La interfaz de usuario de Granite proporciona una serie de componentes diseñados para utilizarse en formularios, denominados campos
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Creación de un nuevo componente de campo de interfaz de usuario de Granite{#creating-a-new-granite-ui-field-component}

La interfaz de usuario de Granite proporciona una serie de componentes diseñados para utilizarse en formularios; se denominan *campos* en el vocabulario de la interfaz de usuario de Granite. Los componentes de formulario Granite estándar están disponibles en:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Estos campos de formulario de la interfaz de usuario de Granite son de particular interés, ya que se utilizan para [cuadros de diálogo de componentes](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Para obtener más información sobre los campos, consulte la [documentación de la interfaz de usuario de Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Utilice la estructura Granite UI Foundation para desarrollar y/o ampliar componentes Granite. Tiene dos elementos:

* servidor:

   * una colección de componentes de base

      * base: modular, composable, legible, reutilizable
      * componentes: componentes Sling
   * ayuda para el desarrollo de aplicaciones


* cliente:

   * una colección de clientlibs que proporcionan algún vocabulario (es decir, la extensión del lenguaje HTML) para lograr patrones de interacción genéricos a través de una IU basada en Hypermedia

El componente genérico de la interfaz de usuario Granite `field` se compone de dos archivos de interés:

* `init.jsp`:: gestiona el procesamiento genérico; etiquetado, descripción y proporciona el valor del formulario que necesitará al procesar el campo.
* `render.jsp`:: aquí es donde se realiza la representación real del campo y debe anularse para el campo personalizado; está incluido por  `init.jsp`.

Consulte la [documentación de la interfaz de usuario de Granite: Campo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) si desea obtener más detalles.

Para ver ejemplos, consulte:

* `cqgems/customizingfield/components/colorpicker`

   * proporcionado por la [Muestra de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Dado que este mecanismo utiliza JSP, i18n y XSS no se incluyen de forma predeterminada. Esto significa que tendrá que internacionalizar y escapar de sus cadenas. El siguiente directorio contiene los campos genéricos de una instancia estándar, se pueden usar como referencia:
>
>`/libs/granite/ui/components/foundation/form` directory

## Creación de la secuencia de comandos del lado del servidor para el componente {#creating-the-server-side-script-for-the-component}

El campo personalizado solo debe anular la secuencia de comandos `render.jsp`, donde se proporciona la marca para el componente. Puede considerar el JSP (es decir, la secuencia de comandos de procesamiento) como un envoltorio para el marcado.

1. Cree un nuevo componente que utilice la propiedad `sling:resourceSuperType` para heredar de:

   `/libs/granite/ui/components/foundation/form/field`

1. Anular la secuencia de comandos:

   `render.jsp`

   En esta secuencia de comandos, debe generar el marcado de hipermedios (es decir, el marcado enriquecido, que contiene la asequibilidad de los hipermedios) para que el cliente sepa cómo interactuar con el elemento generado. Esto debe seguir el estilo de codificación de la interfaz de usuario Granite en el lado del servidor.

   Al personalizar, el único contrato que *debe* cumplir es leer el valor del formulario (inicializado en `init.jsp`) de la solicitud mediante:

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Para obtener más información, consulte la implementación de los campos predeterminados de la interfaz de usuario de Granite; por ejemplo, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >Por el momento, JSP es el método de secuencias de comandos preferido, ya que en HTL no es fácil pasar información de un componente a otro (algo bastante frecuente en el contexto de los campos o formularios).

## Creación de la biblioteca de cliente para el componente {#creating-the-client-library-for-the-component}

Para agregar un comportamiento específico del lado del cliente a su componente:

1. Cree una clientlib de categoría `cq.authoring.dialog`.
1. Cree una clientlib de categoría `cq.authoring.dialog` y defina su `JS`/ `CSS` interior.

   Defina su `JS`/ `CSS` dentro de la clientlib.

   >[!NOTE]
   >
   >En este momento, la interfaz de usuario de Granite no proporciona ningún detector o ganchos listos para usar que pueda utilizar directamente para añadir el comportamiento de JS. Por lo tanto, para agregar un comportamiento JS adicional a su componente, debe implementar un enlace JS en una clase personalizada que luego asigne a su componente durante la generación de marcado.

