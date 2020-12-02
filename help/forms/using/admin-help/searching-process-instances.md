---
title: Búsqueda de instancias de proceso
seo-title: Búsqueda de instancias de proceso
description: Utilice la página Buscar proceso para introducir los criterios de búsqueda para encontrar una instancia de proceso.
seo-description: Utilice la página Buscar proceso para introducir los criterios de búsqueda para encontrar una instancia de proceso.
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Buscando instancias de proceso{#searching-for-process-instances}

Utilice la página Buscar proceso para introducir los criterios de búsqueda para encontrar una instancia de proceso. Puede acceder a la página Buscar proceso desde la página de flujo de trabajo de formularios o haciendo clic en Buscar en la página Instancia de proceso.

Puede introducir criterios básicos para realizar una búsqueda general, atributos específicos para realizar una búsqueda detallada o una combinación de criterios básicos y atributos específicos para realizar una búsqueda combinada.

## Realizar una búsqueda general {#perform-a-general-search}

La búsqueda general de un proceso es más adecuada si conoce la ID del proceso de la instancia de proceso, si busca un grupo de instancias de proceso relacionadas o si sólo se están ejecutando unas pocas instancias de proceso.

Introduzca criterios básicos para realizar una búsqueda general. Si introduce varios criterios, la búsqueda se realiza con una condición Y implícita.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Buscar en procesos.
1. En la página Buscar proceso, en Búsqueda general, proporcione los siguientes criterios:

   * **ID de proceso:** el entero positivo que identifica cada instancia de proceso única.
   * **Estado del proceso:** seleccione un estado en la lista.
   * **Aplicación:** seleccione una aplicación de la lista. Solo se muestran las aplicaciones implementadas.
   * **Nombre del proceso: Versión:** seleccione un nombre de proceso en el menú. Solo se muestran los procesos implementados.

1. Haga clic en Buscar. Aparece la página Instancia de proceso, que enumera las instancias encontradas.

## Realice una búsqueda detallada de un proceso {#perform-a-detailed-search-for-a-process}

Puede introducir atributos específicos para realizar una búsqueda detallada. Una búsqueda detallada es más apropiada si se tienen muchas instancias de proceso en ejecución y se necesita reducir las posibles hallazgos según ciertos criterios.

1. En la consola de administración, haga clic en Servicios > Flujo de trabajo de Forms > Buscar en procesos.
1. En la página Buscar en proceso, en Búsqueda detallada, especifique el primer conjunto de criterios:

   * En la lista Atributo, seleccione un atributo.
   * En la lista Filtro, seleccione un operador.
   * En el cuadro Valor, escriba un valor apropiado para el atributo seleccionado.

1. Para agregar otra fila, seleccione Más Filtros. Se muestra otro conjunto de listas Atributo, Filtro y Valor, así como una lista Condición.
1. En Condición, seleccione Y u O. Repita los pasos 1 a 3 según sea necesario para reducir la búsqueda.
1. Para agregar o quitar filas, haga clic en Más Filtros o Menos Filtros. Puede tener de una a cuatro filas.
1. Haga clic en Buscar. Aparece la página Instancia de proceso, que enumera las instancias encontradas.

[Acerca de los estados de instancias de proceso](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## Realizar una búsqueda combinada de un proceso {#perform-a-combined-search-for-a-process}

Para crear una búsqueda basada tanto en una búsqueda general como en una búsqueda detallada, con una Y implícita entre las áreas, introduzca los criterios de búsqueda en las áreas Búsqueda general y Búsqueda detallada de la página Buscar en proceso.

Si la búsqueda es demasiado estrecha, no se encontrarán instancias.
