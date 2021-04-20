---
title: Modelos de fragmento de contenido
seo-title: Modelos de fragmento de contenido
description: Los modelos de fragmento de contenido se utilizan para crear fragmentos de contenido con contenido estructurado.
seo-description: Los modelos de fragmento de contenido se utilizan para crear fragmentos de contenido con contenido estructurado.
uuid: 73e38629-37c6-4f68-97a9-62f9783cc3d4
content-type: reference
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 9da10294-2dc8-4e82-8d32-f034e6a5aeeb
docset: aem65
feature: Content Fragments
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 21%

---


# Modelos de fragmento de contenido{#content-fragment-models}

Los modelos de fragmento de contenido definen la estructura de contenido para los [fragmentos de contenido](/help/assets/content-fragments/content-fragments.md).

## Habilitar modelos de fragmento de contenido {#enable-content-fragment-models}

>[!CAUTION]
>
>Si no habilita **Modelos de fragmento de contenido**, la opción **Crear** no estará disponible para crear nuevos modelos.

Para habilitar los modelos de fragmento de contenido, debe:

* Habilitar el uso de modelos de fragmento de contenido en el [Navegador de configuración](/help/sites-administering/configurations.md)
* Aplique la configuración a la carpeta Assets

### Habilitar los modelos de fragmento de contenido en el Administrador de configuración {#enable-content-fragment-models-in-configuration-manager}

Para [crear un nuevo modelo de fragmento de contenido](#creating-a-content-fragment-model) primero debe **habilitarlos** mediante el Administrador de configuración:

>[!CAUTION]
>
>Las subconfiguraciones (una configuración anidada en una configuración) no se admiten para su uso con fragmentos de contenido.

1. Vaya a **Herramientas**, **General**, luego abra el **Explorador de configuración**.

1. Utilice **Crear** para abrir el cuadro de diálogo, donde:

   1. Especifique un **Título**.
   1. Seleccione **Modelos de fragmento de contenido** para habilitar su uso.

   ![cfm-6420-09](assets/cfm-6420-09.png)

1. Seleccione **Create** para guardar la definición.

<!-- 1. Select the location appropriate to your website. -->

### Aplicar la configuración a la carpeta de recursos {#apply-the-configuration-to-your-assets-folder}

Cuando la configuración **global** está habilitada para los modelos de fragmento de contenido, cualquier modelo que creen los usuarios se puede usar en cualquier carpeta de Assets.

Para utilizar otras configuraciones (es decir, excluyendo global) con una carpeta de Assets comparable, debe definir la conexión. Esto se realiza mediante **Configuración** en la pestaña **Cloud Services** de las **Propiedades de la carpeta** correspondiente.

## Creación de un modelo de fragmento de contenido {#creating-a-content-fragment-model}

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra **Modelos de fragmento de contenido**.
1. Vaya a la carpeta correspondiente a su [configuración](#enable-content-fragment-models).
1. Utilice **Crear** para abrir el asistente.

   >[!CAUTION]
   >
   >Si el [uso de modelos de fragmento de contenido no se ha habilitado](#enable-content-fragment-models), la opción **Crear** no estará disponible.

1. Especifique el **Título del modelo**. También puede agregar una **descripción** si fuera necesario.

   ![cfm-6420-10](assets/cfm-6420-10.png)

1. Utilice **Crear** para guardar el modelo vacío. Un mensaje indicará el éxito de la acción, puede seleccionar **Abrir** para editar inmediatamente el modelo o **Listo** para volver a la consola.

## Definición del modelo de fragmento de contenido {#defining-your-content-fragment-model}

El modelo de fragmento de contenido define de forma eficaz la estructura de los fragmentos de contenido resultantes. Con el editor de modelos puede añadir y configurar los campos obligatorios:

>[!CAUTION]
>
>Editar un modelo de fragmento de contenido existente puede afectar a los fragmentos dependientes.

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra **Modelos de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmento de contenido.
1. Abra el modelo necesario para **Edit**; utilice la acción rápida o seleccione el modelo y, a continuación, la acción en la barra de herramientas.

   Una vez abierto, el editor de modelos muestra:

   * a la izquierda: campos ya definidos
   * right: **Tipos de datos** disponibles para crear campos (y **Propiedades** para su uso una vez creados los campos)

   >[!NOTE]
   >
   >Cuando un campo es **obligatorio**, la **etiqueta** indicada en el panel izquierdo se marca con un asterisco (*****).

   ![cfm-6420-12](assets/cfm-6420-12.png)

1. **Adición de un campo**

   * Arrastre un tipo de datos requerido a la ubicación requerida para un campo:

   ![cfm-6420-11](assets/cfm-6420-11.png)

   * Una vez agregado un campo al modelo, el panel derecho mostrará las **Propiedades** que se pueden definir para ese tipo de datos en particular. Aquí puede definir lo que se requiere para ese campo. Por ejemplo:

   ![cfm-6420-13](assets/cfm-6420-13.png)

   >[!NOTE]
   Para el tipo de datos **Texto multilínea** es posible definir el **tipo predeterminado** como:
   * **Texto enriquecido**

   * **Markdown**

   * **Texto sin formato**

   Si no se especifica, el valor predeterminado **Texto enriquecido** se utiliza para este campo.
   Cambiar el **tipo predeterminado** en un modelo de fragmento de contenido solo surtirá efecto en un fragmento de contenido existente relacionado después de que dicho fragmento se abra en el editor y se guarde.

1. **Eliminación de un campo**

   Seleccione el campo requerido y, a continuación, toque o haga clic en el icono de la papelera. Se le solicitará que confirme la acción.

   ![cf-32](assets/cf-32.png)

1. Después de agregar todos los campos obligatorios y definir las propiedades, utilice **Guardar** para mantener la definición. Por ejemplo:

   ![cfm-6420-14](assets/cfm-6420-14.png)

## Eliminación de un modelo de fragmento de contenido {#deleting-a-content-fragment-model}

>[!CAUTION]
La eliminación de un modelo de fragmento de contenido puede afectar a los fragmentos dependientes.

Para eliminar un modelo de fragmento de contenido:

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra **Modelos de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmento de contenido.
1. Seleccione el modelo, seguido de **Delete** en la barra de herramientas.

   >[!NOTE]
   Si se hace referencia al modelo, se envía una advertencia. Tome las medidas adecuadas.

## Publicación de un modelo de fragmento de contenido {#publishing-a-content-fragment-model}

Los modelos de fragmento de contenido deben publicarse cuando se publican fragmentos de contenido dependientes, o antes de hacerlo.

Para publicar un modelo de fragmento de contenido:

1. Vaya a **Herramientas**, **Recursos** y, a continuación, abra **Modelos de fragmento de contenido**.

1. Vaya a la carpeta que contiene el modelo de fragmento de contenido.
1. Seleccione el modelo, seguido de **Publish** en la barra de herramientas.

   >[!NOTE]
   Si publica un fragmento de contenido para el que el modelo aún no se ha publicado, una lista de selección lo indicará y el modelo se publicará con el fragmento.

