---
title: Configuración de componentes en el modo Diseño
description: AEM Cuando se instala la instancia de forma predeterminada, una selección de componentes está disponible inmediatamente en la barra de tareas. Además de estos, también hay otros componentes disponibles. Puede utilizar el modo Diseño para habilitar o deshabilitar estos componentes.
uuid: 2cd5dad0-2f9c-4f34-aae8-1638d1445eb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 10466b49-f8bd-4c2c-8106-b0c7ba054989
docset: aem65
exl-id: cb2d2d0d-feb4-4b89-8325-80f735816904
source-git-commit: 75c6bb87bb06c5ac9378ccebf193b5416c080bb1
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# Configuración de componentes en el modo Diseño{#configuring-components-in-design-mode}

AEM Cuando se instala la instancia de forma predeterminada, una selección de componentes está disponible inmediatamente en la barra de tareas.

Además de estos, también hay otros componentes disponibles. Puede utilizar el modo Diseño para [Habilitar/deshabilitar estos componentes](#enabledisablecomponentsusingdesignmode). Cuando esté activada y ubicada en la página, puede utilizar el modo Diseño para lo siguiente [configurar aspectos del diseño de componentes](#configuringcomponentsusingdesignmode) editando los parámetros de atributo.

>[!NOTE]
>
>Se debe tener cuidado al editar estos componentes. La configuración de diseño suele ser parte integral del diseño de todo el sitio web, por lo que solo debe cambiarla alguien con los privilegios (y experiencia) adecuados, a menudo un administrador o desarrollador. Consulte [Desarrollo de componentes](/help/sites-developing/components.md) para obtener más información.

En realidad, esto implica agregar o quitar los componentes permitidos en el sistema de párrafos de la página. El sistema de párrafos ( `parsys`) es un componente compuesto que contiene todos los demás componentes de párrafo. El sistema de párrafos permite a los autores añadir componentes de diferentes tipos a una página, ya que contiene todos los demás componentes de párrafo. Cada tipo de párrafo se representa como un componente.

Por ejemplo, el contenido de una página de producto puede contener un sistema de párrafos que contenga lo siguiente:

* Una imagen del producto (en forma de imagen o de párrafo de imagen de texto)
* La descripción del producto (como párrafo de texto)
* Una tabla con datos técnicos (como un párrafo de tabla)
* Un formulario que los usuarios rellenan (al comenzar los formularios, el elemento y el párrafo final de los formularios)

>[!NOTE]
>
>Consulte [Desarrollo de componentes](/help/sites-developing/components.md#paragraphsystem) y [Directrices para el uso de plantillas y componentes](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) para obtener más información acerca de `parsys`.

## Habilitar/deshabilitar componentes {#enable-disable-components}

En el modo Diseño, la barra de tareas se minimiza y tiene la posibilidad de configurar los componentes accesibles para la creación:

1. Para entrar en el modo Diseño, abra una página para editarla y utilice el icono del Sidekick:

   ![Modo de diseño](do-not-localize/chlimage_1.png)

1. Clic **Editar** en el sistema de párrafos (**Diseño del par**).

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. Se abrirá un cuadro de diálogo que enumera los grupos de componentes que se muestran en la barra de tareas junto con los componentes individuales que contienen.

   Seleccione según sea necesario para agregar o quitar los componentes que deben estar disponibles en la barra de tareas.

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. El Sidekick minimiza en modo de diseño. Al hacer clic en la flecha, puede maximizar el Sidekick y volver al modo de edición:

   ![Sidekick minimizado](do-not-localize/sidekick-collapsed.png)

## Configuración del diseño de un componente {#configuring-the-design-of-a-component}

En el modo Diseño, también puede configurar atributos para los componentes individuales. Cada componente tiene sus propios parámetros. En el siguiente ejemplo se muestra el **Imagen** componente:

1. Para entrar en el modo Diseño, abra una página para editarla y utilice el icono del Sidekick:

   ![Modo de diseño: Sidekick](do-not-localize/chlimage_1-1.png)

1. Puede configurar el diseño de los componentes.

   Por ejemplo, si hace clic en **Editar** en el componente Imagen (**Diseño de la imagen**) puede configurar los parámetros específicos del componente:

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. Clic **OK** para guardar los cambios.

1. El Sidekick minimiza en modo de diseño. Al hacer clic en la flecha, puede maximizar el Sidekick y volver al modo de edición:

   ![Sidekick minimizado](do-not-localize/sidekick-collapsed-1.png)
