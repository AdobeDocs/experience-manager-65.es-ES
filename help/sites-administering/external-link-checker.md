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

---


# Comprobador de vínculos externos{#the-external-link-checker}

AEM proporciona un comprobador de vínculos externo. Comprobador de vínculos:

* analiza todas las páginas de contenido
* genera una lista de todos los vínculos válidos y no válidos
* marca los vínculos no válidos como rotos in situ en las páginas de contenido individuales

## Cómo validar vínculos externos {#how-to-validate-external-links}

Para utilizar el comprobador de vínculos externo:

1. Con **Navegación**, seleccione **Herramientas** y luego **Sitios**.
1. Seleccione Comprobador de vínculos **externos** y se generará una lista de todos los vínculos externos.
1. Valide un vínculo específico seleccionándolo en la lista y luego haciendo clic en **Comprobar**:

   ![](assets/telc-01.png)

   Se muestra la información:

   * **Estado** del vínculo
   * **URL**
   * **Referencia**
   * tiempo transcurrido desde la **última comprobación** del vínculo (validado)
   * el **último estado** devuelto

   * tiempo transcurrido desde la **última disponibilidad del vínculo**
   * tiempo transcurrido desde el **último acceso al vínculo**

1. En las páginas de contenido individuales, los vínculos no válidos se mostrarán como rotos:

   ![](assets/chlimage_1-143.png)