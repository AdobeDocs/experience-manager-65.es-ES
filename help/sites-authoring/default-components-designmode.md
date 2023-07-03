---
title: Configuración de componentes predeterminados en el modo Diseño
description: Configuración de componentes en modo de diseño
uuid: b9c9792d-4398-446d-8767-44d4e7ce9a2e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8ae6817a-16d3-4740-b67a-498e75adf350
exl-id: 5e232886-75c1-4f0f-b359-4739ae035fd3
source-git-commit: cae9890cd61d6d894f34c7299e2e15ee70e14ac9
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 1%

---

# Configuración de componentes predeterminados en el modo Diseño{#configuring-components-in-design-mode}

AEM Cuando se instala la instancia de forma predeterminada, una selección de componentes está disponible inmediatamente en el explorador de componentes.

Además de estos, también hay otros componentes disponibles. Puede utilizar el modo Diseño para [habilitar/deshabilitar estos componentes](#enable-disable-components). Cuando esté activada y ubicada en la página, puede utilizar el modo Diseño para lo siguiente [configurar aspectos del diseño de componentes](#configuring-the-design-of-a-component) editando los parámetros de atributo.

>[!NOTE]
>
>Se debe tener cuidado al editar estos componentes. La configuración de diseño suele ser parte integral del diseño de todo el sitio web, por lo que solo debe cambiarla alguien con los privilegios y la experiencia adecuados, a menudo un administrador o un desarrollador. Consulte [Desarrollo de componentes](/help/sites-developing/components.md) para obtener más información.

>[!NOTE]
>
>El modo de diseño solo está disponible para plantillas estáticas. Las plantillas que se crean con plantillas editables deben editarse con la variable [editor de plantillas](/help/sites-authoring/templates.md).

>[!NOTE]
>
>El modo Diseño solo está disponible para configuraciones de diseño almacenadas como contenido en ( `/etc`).
>
>AEM A partir de la versión 6.4, se recomienda almacenar los diseños como datos de configuración en `/apps` para admitir escenarios de implementación continua. Diseños almacenados en `/apps` no se pueden editar durante la ejecución y el modo Diseño no estará disponible para los usuarios que no sean administradores de dichas plantillas.

Esto implica añadir o eliminar los componentes permitidos en el sistema de párrafos de la página. El sistema de párrafos ( `parsys`) es un componente compuesto que contiene todos los demás componentes de párrafo. El sistema de párrafos permite a los autores añadir componentes de diferentes tipos a una página, ya que contiene todos los demás componentes de párrafo. Cada tipo de párrafo se representa como un componente.

Por ejemplo, el contenido de una página de producto puede contener un sistema de párrafos que contenga lo siguiente:

* Una imagen del producto (en forma de imagen o de párrafo de imagen de texto)
* La descripción del producto (como párrafo de texto)
* Una tabla con datos técnicos (como un párrafo de tabla)
* Un formulario que los usuarios rellenan (al comenzar los formularios, el elemento y el párrafo final de los formularios)

>[!NOTE]
>
>Consulte [Desarrollo de componentes](/help/sites-developing/components.md) y [Directrices para el uso de plantillas y componentes](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) para obtener más información acerca de `parsys`.

>[!CAUTION]
>
>La edición del diseño mediante el modo de diseño, tal como se describe en este artículo, es la forma recomendada de definir diseños de plantillas estáticas
>
>Modificar diseños en CRX DE, por ejemplo, no es una práctica recomendada y la aplicación de dichos diseños puede variar del comportamiento esperado. Consulte el documento para desarrolladores [Plantillas de página: estáticas](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied) para obtener más información.

## Habilitar/deshabilitar componentes {#enable-disable-components}

Para habilitar o deshabilitar un componente:

1. Seleccione el **Diseño** modo.

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. Toque o haga clic en un componente. El componente tendrá un borde azul cuando se seleccione.

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. Toque o haga clic en **Principal** icono.

   ![Principal](do-not-localize/screen_shot_2018-03-22at103204.png)

   Se seleccionará el sistema de párrafos que contiene el componente actual.

1. El **Configurar** para el sistema de párrafos se mostrará en la barra de acciones del elemento principal.

   ![Configurar](do-not-localize/screen_shot_2018-03-22at103256.png)

   Seleccione esta opción para mostrar el cuadro de diálogo.

1. Utilice el cuadro de diálogo para definir los componentes disponibles en el explorador de componentes al editar la página actual.

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   El cuadro de diálogo tiene dos pestañas:

   * Componentes permitidos
   * Configuración

   **Componentes permitidos**

   En el **Componentes permitidos** , se definen qué componentes están disponibles para parsys.

   * Los componentes se agrupan por sus grupos de componentes, que se pueden expandir y contraer.
   * Se puede seleccionar un grupo completo marcando el nombre del grupo y se puede anular la selección de todos desmarcando.
   * Un signo menos representa al menos uno, pero no todos los elementos de un grupo están seleccionados.
   * Hay disponible una búsqueda para filtrar un componente por nombre.
   * Los recuentos enumerados a la derecha del nombre del grupo de componentes representan el número total de componentes seleccionados en esos grupos, independientemente del filtro.

   La configuración se define por componente de página. Si las páginas secundarias utilizan la misma plantilla o componente de página (normalmente alineado), se aplicará la misma configuración al sistema de párrafos correspondiente.

   >[!NOTE]
   >
   >Los componentes de formulario adaptable están diseñados para funcionar dentro del contenedor de formulario adaptable y aprovechar el ecosistema de Forms. Por lo tanto, estos componentes solo deben utilizarse en el editor de formularios adaptables y no funcionarán en el editor de páginas de Sites.

   **Configuración**

   En el **Configuración** pestaña puede definir opciones adicionales, como dibujar un anclaje para cada componente y definir el relleno de celda de cada contenedor.

1. Seleccionar **Listo** para guardar la configuración.

## Configuración del diseño de un componente {#configuring-the-design-of-a-component}

1. Seleccione el **Diseño** modo.

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. Toque o haga clic en un componente con un borde azul. En este ejemplo, se selecciona un componente de imagen a pantalla completa.

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. Utilice el **Configurar** para abrir el cuadro de diálogo.

   ![Icono Configurar](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   En el cuadro de diálogo de diseño, puede configurar el componente según los parámetros de diseño disponibles.

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   El cuadro de diálogo tiene tres pestañas:

   * Principal
   * Características
   * Estilos

   **Propiedades**

   El **Propiedades** permite configurar los parámetros de diseño importantes del componente. Por ejemplo, para un componente de imagen puede definir el tamaño máximo y mínimo de la imagen permitido.

   **Características**

   El **Funciones** permite activar o desactivar funciones adicionales del componente. Por ejemplo, para un componente de imagen puede definir la orientación de la imagen, las opciones de recorte disponibles y si se puede cargar una imagen.

   **Estilos**

   El **Estilos** permite definir las clases y los estilos CSS que se utilizarán con el componente.

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   Utilice el **Añadir** para agregar entradas adicionales a una lista de diálogo de varias entradas.

   ![chlimage_1-94](assets/chlimage_1-94.png)

   Utilice el **Eliminar** icono para quitar una entrada de una lista de cuadros de diálogo de varias entradas.

   ![Eliminar](do-not-localize/screen_shot_2018-03-22at103809.png)

   Utilice el **Mover** para reorganizar el orden de las entradas en una lista de diálogo de varias entradas.

   ![Mover](do-not-localize/screen_shot_2018-03-22at103816.png)

1. Toque o haga clic en **Listo** para guardar y cerrar el cuadro de diálogo.
