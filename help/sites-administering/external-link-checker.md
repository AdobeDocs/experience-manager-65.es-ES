---
title: Comprobador de vínculos externos
seo-title: Comprobador de vínculos externos
description: Obtenga información sobre el Comprobador de vínculos externos en AEM.
seo-description: Obtenga información sobre el Comprobador de vínculos externos en AEM.
uuid: 09160594-e45f-4604-8b36-f14b148b9f63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d1ccd194-8549-4188-8932-7136be1e88a2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---


# El Comprobador de vínculos externos{#the-external-link-checker}

En AEM se proporciona un comprobador de vínculos externo. Comprobador de vínculos:

* analiza todas las páginas de contenido
* genera una lista de todos los vínculos válidos y no válidos
* marca los vínculos no válidos como rotos in situ en las páginas de contenido individuales

## Cómo validar vínculos externos {#how-to-validate-external-links}

Para utilizar el comprobador de vínculos externo:

1. Mediante **Navegación**, seleccione **Herramientas** y luego **Sitios**.
1. Seleccione **Comprobador de vínculos externos**, se genera una lista de todos los vínculos externos.
1. Valide un vínculo específico seleccionándolo en la lista y luego haciendo clic en **Comprobar**:

   ![](assets/telc-01.png)

   Se muestra la información:

   * **Estado** del vínculo
   * **URL**
   * **Referencia**
   * tiempo desde que el vínculo fue **Última comprobación** (validado)
   * el **Último estado** devolvió

   * tiempo desde que el vínculo era **Última disponibilidad**
   * tiempo transcurrido desde que el vínculo era **Último acceso**

1. En las páginas de contenido individuales, los vínculos no válidos se mostrarán como rotos:

   ![](assets/chlimage_1-143.png)