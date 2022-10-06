---
title: Búsqueda de instancias de proceso
seo-title: Searching for process instances
description: Utilice la página Buscar en proceso para introducir criterios de búsqueda para encontrar una instancia de proceso.
seo-description: Use the Process Search page to enter search criteria for finding a process instance.
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
exl-id: 35f9acbf-7a82-43b1-9e17-9be4de666212
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Búsqueda de instancias de proceso{#searching-for-process-instances}

Utilice la página Buscar en proceso para introducir criterios de búsqueda para encontrar una instancia de proceso. Puede acceder a la página Buscar en proceso desde la página de flujo de trabajo de formularios o haciendo clic en Buscar en la página Instancia de proceso .

Puede introducir criterios básicos para realizar una búsqueda general, atributos específicos para realizar una búsqueda detallada o una combinación de criterios básicos y atributos específicos para realizar una búsqueda combinada.

## Realizar una búsqueda general {#perform-a-general-search}

La búsqueda general de un proceso es más adecuada si conoce el ID de proceso de la instancia de proceso, si está buscando un grupo de instancias de proceso relacionadas o si solo se están ejecutando unas pocas instancias de proceso.

Introduzca criterios básicos para realizar una búsqueda general. Si introduce varios criterios, la búsqueda se realiza con una condición AND implícita.

1. En la consola de administración, haga clic en Services > Forms workflow > Process Search.
1. En la página Búsqueda de procesos , en Búsqueda general, proporcione los siguientes criterios:

   * **ID de proceso:** Número entero positivo que identifica cada instancia de proceso única.
   * **Estado del proceso:** Seleccione un estado de la lista.
   * **Aplicación:** Seleccione una aplicación de la lista. Solo se muestran las aplicaciones implementadas.
   * **Nombre del proceso - Versión:** Seleccione un nombre de proceso en el menú . Solo se muestran los procesos implementados.

1. Haga clic en Buscar. Aparece la página Instancia de proceso, que enumera las instancias encontradas.

## Realizar una búsqueda detallada de un proceso {#perform-a-detailed-search-for-a-process}

Puede introducir atributos específicos para realizar una búsqueda detallada. Una búsqueda detallada es la más apropiada si se tienen muchas instancias de proceso en ejecución y se necesita reducir los posibles hallazgos según ciertos criterios.

1. En la consola de administración, haga clic en Services > Forms workflow > Process Search.
1. En la página Búsqueda de procesos , en Búsqueda detallada, especifique su primer conjunto de criterios:

   * En la lista Atributo, seleccione un atributo.
   * En la lista Filtro, seleccione un operador.
   * En el cuadro Valor, escriba un valor apropiado para el atributo seleccionado.

1. Para añadir otra fila, seleccione Más filtros. Se muestra otro conjunto de listas Atributo, Filtro y Valor, así como una lista Condición.
1. En Condición, seleccione Y u O. Repita los pasos del 1 al 3 según sea necesario para restringir aún más la búsqueda.
1. Para agregar o quitar filas, haga clic en Más filtros o Menos filtros. Puede tener de una a cuatro filas.
1. Haga clic en Buscar. Aparece la página Instancia de proceso, que enumera las instancias encontradas.

[Acerca de los estados de instancias de proceso](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## Realizar una búsqueda combinada de un proceso {#perform-a-combined-search-for-a-process}

Para crear una búsqueda basada tanto en una búsqueda general como en una búsqueda detallada, con una Y implícita entre las áreas, introduzca los criterios de búsqueda en las áreas Búsqueda general y Búsqueda detallada de la página Buscar en proceso.

Si la búsqueda es demasiado estrecha, no se encontrarán instancias.
