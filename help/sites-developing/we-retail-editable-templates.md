---
title: Prueba de plantillas editables en We.Retail
seo-title: Prueba de plantillas editables en We.Retail
description: nulo
seo-description: nulo
uuid: 0d4b97cb-efcc-4312-a783-eae3ecd6f889
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3cc8ac23-98ff-449f-bd76-1203c7cbbed7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Prueba de plantillas editables en We.Retail{#trying-out-editable-templates-in-we-retail}

Con las plantillas editables, la creación y el mantenimiento de plantillas ya no es una tarea exclusiva para el desarrollador. Ahora, un tipo de usuario avanzado, que se denomina autor de plantilla, puede crear plantillas. Los desarrolladores aún tienen que encargarse de configurar el entorno y crear bibliotecas del cliente y los componentes que se vayan a utilizar, pero una vez efectuados estos pasos básicos, el autor de plantillas disfruta de la flexibilidad para crear y configurar plantillas sin un proyecto de desarrollo.

Todas las páginas de We.Retail se basan en plantillas editables, lo que permite a los no desarrolladores adaptar y personalizar las plantillas.

## Intentándolo {#trying-it-out}

1. Edite la página Equipo de la ramificación maestra de idioma.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. Tenga en cuenta que el selector de modo ya no ofrece un modo de diseño. Todas las páginas de We.Retail se basan en plantillas editables y para alterar el diseño de plantillas editables deben editarse en el editor de plantillas.
1. En el menú Información **de** página, seleccione **Editar plantilla**.
1. Ahora está editando la plantilla Página principal.

   El modo de estructura de la página permite modificar la estructura de la plantilla. Esto incluye, por ejemplo, los componentes permitidos en el contenedor de diseño.

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. Configure las directivas para el contenedor de diseño para definir qué componentes se permiten en el contenedor.

   Las políticas equivalen a las configuraciones de diseño.

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. En el cuadro de diálogo de diseño del contenedor de diseño, puede

   * Seleccione una directiva existente o cree una nueva directiva para el contenedor
   * Seleccione los componentes permitidos en el contenedor
   * Definir los componentes predeterminados que se colocarán cuando se arrastre un recurso al contenedor
   ![chlimage_1-140](assets/chlimage_1-140.png)

1. De nuevo en el editor de plantillas, puede editar la política del componente de texto dentro del contenedor de diseño.

   Esto le permite:

   * Seleccione una directiva existente o cree una nueva directiva para el contenedor
   * Defina las funciones disponibles para el autor de la página al utilizar este componente, como

      * Fuentes de pegado permitidas
      * Opciones de formato
      * Estilos de párrafo permitidos
      * Caracteres especiales permitidos
   Muchos componentes basados en los componentes principales permiten la configuración de opciones a nivel de componente mediante plantillas editables, lo que elimina la necesidad de personalización por parte de los desarrolladores.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. De nuevo en el editor de plantillas, puede utilizar el selector de modo para cambiar al modo Contenido **** inicial para definir qué contenido se necesita en la página.

   **El modo Diseño** se puede utilizar como en una página normal para definir el diseño de la plantilla.

## Más información {#more-information}

Para obtener más información, consulte el documento de creación [Creación de plantillas](/help/sites-authoring/templates.md) de página o el documento de desarrollo [Plantillas de página - Editables](/help/sites-developing/page-templates-editable.md) para obtener detalles técnicos completos sobre plantillas editables.

También es posible que desee investigar los componentes [principales](/help/sites-developing/we-retail-core-components.md). Consulte el documento de creación [Componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) principales para obtener una descripción general de las capacidades de los componentes principales y el documento para desarrolladores [Desarrollar componentes](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) principales para obtener una descripción general técnica.

