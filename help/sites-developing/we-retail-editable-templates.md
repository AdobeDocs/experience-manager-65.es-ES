---
title: Probar plantillas editables en We.Retail
seo-title: Trying out Editable Templates in We.Retail
description: Probar plantillas editables en We.Retail
seo-description: null
uuid: 0d4b97cb-efcc-4312-a783-eae3ecd6f889
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3cc8ac23-98ff-449f-bd76-1203c7cbbed7
exl-id: efebe66d-3d30-4033-9c4c-ae347e134f2f
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 11%

---

# Probar plantillas editables en We.Retail{#trying-out-editable-templates-in-we-retail}

Con las plantillas editables, la creación y el mantenimiento de plantillas ya no es una tarea exclusiva para desarrolladores. Ahora, un tipo de usuario avanzado, que se denomina autor de plantillas, puede crear plantillas. Los desarrolladores siguen necesitando configurar el entorno, crear bibliotecas de clientes y crear los componentes que se van a utilizar, pero una vez que estos conceptos básicos están establecidos, el autor de la plantilla tiene la flexibilidad de crear y configurar plantillas sin un proyecto de desarrollo.

Todas las páginas de We.Retail se basan en plantillas editables, lo que permite a los no desarrolladores adaptar y personalizar las plantillas.

## Probándolo {#trying-it-out}

1. Edite la página Equipamiento de la rama maestra del idioma.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. Tenga en cuenta que el selector de modo ya no ofrece un modo de diseño. Todas las páginas de We.Retail se basan en plantillas editables y para modificar el diseño de plantillas editables, deben editarse en el editor de plantillas.
1. En el **Información de la página** menú seleccionar **Editar plantilla**.
1. Ahora está editando la plantilla Página principal .

   El modo de estructura de la página permite modificar la estructura de la plantilla. Esto incluye, por ejemplo, los componentes permitidos en el contenedor de diseño.

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. Configure las políticas del contenedor de diseño para definir qué componentes se permiten en el contenedor.

   Las políticas equivalen a las configuraciones de diseño.

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. En el cuadro de diálogo de diseño del contenedor de diseño, puede

   * Seleccione una directiva existente o cree una directiva nueva para el contenedor
   * Seleccionar qué componentes se permiten en el contenedor
   * Definir los componentes predeterminados que se deben colocar cuando un recurso se arrastre al contenedor

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. En el editor de plantillas, puede editar la política del componente de texto dentro del contenedor de diseño.

   Esto le permite:

   * Seleccione una directiva existente o cree una directiva nueva para el contenedor
   * Defina las funciones disponibles para el autor de la página al utilizar este componente, como

      * Fuentes de pegado permitidas
      * Opciones de formato
      * Estilos de párrafo permitidos
      * Caracteres especiales permitidos

   Muchos componentes basados en los componentes principales permiten la configuración de opciones a nivel de componente mediante las plantillas editables, lo que elimina la necesidad de que los desarrolladores las personalicen.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. De nuevo en el editor de plantillas, puede utilizar el selector de modo para cambiar a **Contenido inicial** para definir qué contenido se requiere en la página.

   **Diseño** se puede utilizar como en una página normal para definir el diseño de la plantilla.

## Más información {#more-information}

Para obtener más información, consulte el documento de creación [Creación de plantillas de página](/help/sites-authoring/templates.md) o la página del documento para desarrolladores [Plantillas: editables](/help/sites-developing/page-templates-editable.md) para obtener información técnica completa sobre plantillas editables.

También puede que desee investigar [componentes principales](/help/sites-developing/we-retail-core-components.md). Consulte el documento de creación [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) para obtener una descripción general de las capacidades de los componentes principales y del documento para desarrolladores [Desarrollo de componentes principales](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) para obtener una descripción general técnica.
