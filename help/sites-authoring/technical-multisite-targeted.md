---
title: Cómo se estructura la administración de diversos sitios para el contenido objetivo
seo-title: Cómo se estructura la administración de diversos sitios para el contenido objetivo
description: En un diagrama se muestra la estructuración de la compatibilidad con el uso de varios sitios para contenido de destino
seo-description: En un diagrama se muestra la estructuración de la compatibilidad con el uso de varios sitios para contenido de destino
uuid: 2d30cdf0-ab77-490d-aac0-db3a0d417a58
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 7dd851ab-3fa7-426e-89cb-08b67e9b5999
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Cómo se estructura la administración de diversos sitios para el contenido objetivo{#how-multisite-management-for-targeted-content-is-structured}

En el siguiente diagrama se muestra la estructuración de la compatibilidad con el uso de varios sitios para contenido de destino

Areas appear underneath **/content/campaigns/&lt;brand>** and by default each brand has a master area, which is created automatically. Cada área tiene su propio conjunto de actividades, experiencias y ofertas.

![chlimage_1-268](assets/chlimage_1-268.png)

Para contenido de destino, las páginas o los sitios pueden asignarse a un área. Si no ninguna área configurada, AEM utiliza el área principal para esta marca específica.

En el diagrama siguiente se muestra un ejemplo de cómo funciona la lógica para tres sitios, llamados site1, site2 y site3.

![chlimage_1-269](assets/chlimage_1-269.png)

* El sitio site1 busca myarea1 para brand1 y otherarea2 para brand2 en función de la asignación de áreas.
* El sitio site2 busca myarea1 para brand1 y el área principal para brand2, dado que solo está definida la asignación de áreas para brand1.
* El sitio site3 busca el área principal para brand1 y brand2, ya que no se ha definido ninguna otra asignación de área para este sitio.

