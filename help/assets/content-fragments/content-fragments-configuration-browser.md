---
title: 'Fragmentos de contenido: explorador de configuración'
description: Aprenda a habilitar ciertas funciones de fragmento de contenido en el navegador de configuración para aprovechar AEM potentes funciones de envío sin periféricos.
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
source-git-commit: 8dc8eff86ff25534a578dd227033aa185853d930
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 70%

---

# Fragmentos de contenido: explorador de configuración{#content-fragments-configuration-browser}

Aprenda a habilitar ciertas funciones de fragmento de contenido en el navegador de configuración para aprovechar AEM potentes funciones de envío sin periféricos.

## Habilitación de la funcionalidad de fragmento de contenido para la instancia {#enable-content-fragment-functionality-instance}

Antes de usar fragmentos de contenido, debe usar el **Explorador de configuración** para habilitar lo siguiente:

* **Modelos de fragmentos de contenido**: obligatorio
* **Consultas persistentes de GraphQL**: opcional

>[!CAUTION]
>
>Si no habilita **Modelos de fragmentos de contenido**:
>
>* la opción **Crear** no estará disponible para crear nuevos modelos.
>* no podrá [seleccionar la configuración de Sites para crear el punto de conexión relacionado](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint).


Para habilitar la funcionalidad de fragmento de contenido, debe hacer lo siguiente:

* Habilitar el uso de la funcionalidad de fragmento de contenido mediante el Explorador de configuración
* Aplicar la configuración a la carpeta de Assets

### Habilitación de la funcionalidad de fragmento de contenido en el Explorador de configuración {#enable-content-fragment-functionality-in-configuration-browser}

Para [usar ciertas funcionalidades de fragmentos de contenido](#creating-a-content-fragment-model), primero **debe** activarlas a través del **Explorador de configuración**:

>[!NOTE]
>
>Para obtener más información, consulte también [Explorador de configuración:](/help/sites-administering/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>Las subconfiguraciones (una configuración anidada dentro de una configuración) se admiten para su uso con fragmentos de contenido, pero no se pueden usar en consultas de GraphQL.

1. Vaya a **Herramientas**, **General**, luego abra el **Explorador de configuración**.

1. Use **Crear** para abrir el cuadro de diálogo, donde:

   1. Especifique un **Título**.
   1. Para habilitar su uso, seleccione
      * **Modelos de fragmentos de contenido**
      * **Consultas persistentes de GraphQL**

      ![Definir configuración](assets/cfm-conf-01.png)


1. Seleccione **Crear** para guardar la definición.

<!-- 1. Select the location appropriate to your website. -->

### Aplicar la configuración a la carpeta de recursos {#apply-the-configuration-to-your-assets-folder}

Cuando la configuración **global** está habilitado para la funcionalidad de fragmentos de contenido y se aplica a cualquier carpeta de recursos.

Para utilizar otras configuraciones (es decir, excluyendo global) con una carpeta de Assets comparable, debe definir la conexión. Para ello, seleccione la **configuración** adecuada en la pestaña **Cloud Services** de las **Propiedades de carpeta** de la carpeta correspondiente.

![Aplicar configuración](assets/cfm-conf-02.png)
