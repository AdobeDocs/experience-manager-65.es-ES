---
title: 'Búsqueda  '
seo-title: 'Búsqueda  '
description: El entorno de autor AEM ofrece varios mecanismos para buscar contenido, en función del tipo de recurso.
seo-description: El entorno de autor AEM ofrece varios mecanismos para buscar contenido, en función del tipo de recurso.
uuid: 6dd3df4d-6040-4230-8373-fc028687b675
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8d32960c-47c3-4e92-b02e-ad4d8fea7b2d
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 85%

---


# Búsqueda{#searching}

El entorno de autor AEM ofrece varios mecanismos para buscar contenido, en función del tipo de recurso.

>[!NOTE]
>
>Fuera del entorno de creación también hay otros mecanismos disponibles para buscar, como [Query Builder](/help/sites-developing/querybuilder-api.md) y [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## Conceptos básicos de búsqueda {#search-basics}

Para acceder al panel de búsqueda, haga clic en la ficha **Buscar** situada en la parte superior del panel izquierdo en la consola apropiada.

![chlimage_1-101](assets/chlimage_1-101.png)

El panel de búsqueda permite realizar búsquedas en todas las páginas del sitio web. Contiene campos y utilidades para lo siguiente:

* **Texto completo**: buscar el texto especificado
* **Modificado después de/antes de**: buscar solo las páginas modificadas entre las fechas especificadas
* **Plantilla**: buscar solo las páginas basadas en una plantilla específica
* **Tags**: buscar solo las páginas con las tags especificadas

>[!NOTE]
>
>Si la instancia está configurada para la función de [búsqueda de Lucene](/help/sites-deploying/queries-and-indexing.md), puede utilizar el siguiente **texto completo**:
>
>* [Comodines](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches) 
>* [Operadores booleanos](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)

   >
   >
* [Expresiones regulares](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [Grupo de campos](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping) 
>* [Ampliación de búsqueda](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term) 

>



Para ejecutar la búsqueda, haga clic en **Buscar** en la parte inferior del panel. Haga clic en **Restablecer** para borrar los criterios de búsqueda.

## Filtro {#filter}

Un filtro se puede definir (y borrar) en varias ubicaciones para restringir y perfeccionar la vista:

![chlimage_1-102](assets/chlimage_1-102.png)

## Buscar y reemplazar {#find-and-replace}

En la consola **Sitios web** está la opción de menú **Buscar y reemplazar**, que le permite buscar y reemplazar varias instancias de una cadena en una sección del sitio web.

1. Seleccione la página, o carpeta, raíz donde desee realizar la acción de buscar y reemplazar.
1. Seleccione **Herramientas** y, a continuación, **Buscar y reemplazar**:

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. El cuadro de diálogo **Buscar y reemplazar** hace lo siguiente:

   * confirma la ruta de acceso raíz donde debería comenzar la acción de buscar
   * define el término que se desea encontrar
   * define el término con el que se debería reemplazar
   * indica si la búsqueda debería distinguir mayúsculas y minúsculas
   * indica si únicamente deberían buscarse palabras completas (de lo contrario, también se buscan subcadenas)

   Al hacer clic en **Previsualización** listas donde se encontró el término. Puede seleccionar o borrar instancias específicas para reemplazarlas:

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. Haga clic en **Reemplazar** para reemplazar efectivamente todas las instancias. Se le solicitará que confirme la acción.

El alcance predeterminado para el servlet de buscar y reemplazar cubre las siguientes propiedades:

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

El ámbito se puede cambiar con la consola de administración web Apache Felix (por ejemplo, en `https://localhost:4502/system/console/configMgr`). Seleccione `CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)` y configure el ámbito según sea necesario.

>[!NOTE]
>
>En una instalación de AEM estándar, Buscar y reemplazar usa Lucene para la funcionalidad de búsqueda.
>
>Lucene indexa propiedades de cadena de hasta 16 k de longitud. No se buscarán las cadenas que superen esto.
