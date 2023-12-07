---
title: Búsqueda
description: El entorno de autor AEM ofrece varios mecanismos para buscar contenido, en función del tipo de recurso.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 1f46a57f-4966-4dd1-8c99-c0740718ae76
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 11%

---

# Búsqueda{#searching}

El entorno de autor AEM ofrece varios mecanismos para buscar contenido, en función del tipo de recurso.

>[!NOTE]
>
>Fuera del entorno de creación, también hay otros mecanismos disponibles para la búsqueda, como el [Generador de consultas](/help/sites-developing/querybuilder-api.md) y [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## Conceptos básicos de búsqueda {#search-basics}

Para acceder al panel de búsqueda, haga clic en **Buscar** en la parte superior del panel izquierdo de la consola correspondiente.

![chlimage_1-101](assets/chlimage_1-101.png)

El panel de búsqueda le permite buscar en todas las páginas del sitio web. Contiene campos y widgets para lo siguiente:

* **Texto completo**: buscar el texto especificado
* **Modificado después/antes de**: busque solo las páginas que se cambiaron entre las fechas específicas
* **Plantilla**: busque solo aquellas páginas en función de la plantilla especificada
* **Etiquetas**: busque solo las páginas con las etiquetas especificadas

>[!NOTE]
>
>Cuando la instancia esté configurada para [Búsqueda de Lucene](/help/sites-deploying/queries-and-indexing.md) puede utilizar lo siguiente en **Texto completo**:
>
>* [Comodines](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [Operadores booleanos](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)
>
>* [Expresiones regulares](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [Agrupación de campos](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [Aumento](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)
>

Ejecute la búsqueda haciendo clic en **Buscar** en la parte inferior del panel. Clic **Restablecer** para borrar los criterios de búsqueda.

## Filter {#filter}

En varias ubicaciones se puede definir (y borrar) un filtro para explorar en profundidad y acotar la vista:

![chlimage_1-102](assets/chlimage_1-102.png)

## Buscar y reemplazar {#find-and-replace}

En el **Sitios web** consola a **Buscar y reemplazar** La opción de menú permite buscar y reemplazar varias instancias de una cadena, dentro de una sección del sitio web.

1. Seleccione la página raíz, o carpeta, donde desea que tenga lugar la acción de buscar y reemplazar.
1. Seleccionar **Herramientas** entonces **Buscar y reemplazar**:

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. El **Buscar y reemplazar** El cuadro de diálogo hace lo siguiente:

   * confirma la ruta raíz en la que debe comenzar la acción de búsqueda
   * define el término que se busca
   * define el término que debe reemplazarlo
   * indica si la búsqueda debe distinguir entre mayúsculas y minúsculas
   * indica si solo se deben encontrar palabras completas (de lo contrario, también se encuentran subcadenas)

   Clic **Previsualizar** listas en las que se ha encontrado el término. Puede seleccionar o borrar instancias específicas para sustituirlas:

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. Clic **Reemplazar** para reemplazar realmente todas las instancias. Se le solicitará que confirme la acción.

El ámbito predeterminado del servlet de búsqueda y reemplazo cubre las siguientes propiedades:

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

El ámbito se puede cambiar mediante la consola de administración web de Apache Felix (por ejemplo, en `https://localhost:4502/system/console/configMgr`). Seleccionar `CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)` y configure el ámbito según sea necesario.

>[!NOTE]
>
>AEM En una instalación estándar, Buscar y reemplazar utiliza Lucene para la funcionalidad de búsqueda.
>
>Lucene indexa propiedades de cadena de hasta 16 K de longitud. No se buscarán las cadenas que superen este límite.
