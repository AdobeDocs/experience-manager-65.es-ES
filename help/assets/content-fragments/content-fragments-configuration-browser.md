---
title: 'Fragmentos de contenido: navegador de configuración'
description: Aprenda a habilitar ciertas funciones de fragmento de contenido en el navegador de configuración para aprovechar AEM potentes funciones de envío sin periféricos.
feature: Content Fragments
role: User
source-git-commit: 94145c6428f61e31f6784a3d6ea67aa8d81cedd6
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 18%

---

# Fragmentos de contenido: navegador de configuración{#content-fragments-configuration-browser}

Aprenda a habilitar ciertas funciones de fragmento de contenido en el navegador de configuración para aprovechar AEM potentes funciones de envío sin periféricos.

## Habilitar la funcionalidad de fragmento de contenido para la instancia {#enable-content-fragment-functionality-instance}

Antes de utilizar los fragmentos de contenido, debe utilizar el **Navegador de configuración** para habilitar:

* **Modelos de fragmento de contenido** : obligatorio
* **Consultas persistentes de GraphQL** : opcional

>[!CAUTION]
>
>Si no habilita **Modelos de fragmento de contenido**:
>
>* la opción **Crear** no estará disponible para crear nuevos modelos.
>* no podrá [seleccionar la configuración Sitios para crear el punto final relacionado](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint).


Para habilitar la funcionalidad de fragmento de contenido, debe:

* Habilitar el uso de la funcionalidad de fragmento de contenido mediante el navegador de configuración
* Aplique la configuración a la carpeta Assets

### Habilitar la funcionalidad de fragmento de contenido en el navegador de configuración {#enable-content-fragment-functionality-in-configuration-browser}

Para [utilizar cierta funcionalidad de fragmento de contenido](#creating-a-content-fragment-model) debe **habilitarlos primero** mediante el **Explorador de configuración**:

>[!NOTE]
>
>Para obtener más información, consulte también [Explorador de configuración:](/help/sites-administering/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>Las subconfiguraciones (una configuración anidada en una configuración) no se admiten para su uso con fragmentos de contenido.

1. Vaya a **Herramientas**, **General**, luego abra el **Explorador de configuración**.

1. Utilice **Crear** para abrir el cuadro de diálogo, donde:

   1. Especifique un **Título**.
   1. Para habilitar su uso, seleccione
      * **Modelos de fragmento de contenido**
      * **Consultas persistentes de GraphQL**

      ![Definir configuración](assets/cfm-conf-01.png)


1. Seleccione **Create** para guardar la definición.

<!-- 1. Select the location appropriate to your website. -->

### Aplicar la configuración a la carpeta de recursos {#apply-the-configuration-to-your-assets-folder}

Cuando la configuración **global** está habilitada para la funcionalidad de fragmentos de contenido, se aplica a cualquier carpeta de Assets.

Para utilizar otras configuraciones (es decir, excluyendo global) con una carpeta de Assets comparable, debe definir la conexión. Para ello, seleccione la **configuración** adecuada en la pestaña **Cloud Services** de las **Propiedades de carpeta** de la carpeta correspondiente.

![Aplicar configuración](assets/cfm-conf-02.png)
