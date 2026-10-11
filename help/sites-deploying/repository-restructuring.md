---
title: Reestructuración de repositorios en AEM 6.5
description: Conozca los conceptos básicos y el razonamiento detrás de la reestructuración de repositorios en AEM 6.5
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 835ee49e-9248-5578-a60a-15c097807178
    internal-label: Upgrading
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%
---
# Reestructuración de repositorios en AEM 6.5{#repository-restructuring-in-aem}

## Introducción {#introduction}

Antes de AEM 6.4, el código de cliente se implementaba en áreas impredecibles del JCR que estaban sujetas a cambios en las actualizaciones. Debido a esto, era común que las versiones formales de AEM sobrescribieran código, configuración o contenido personalizados. Además, los cambios del cliente a veces sobrescribían el código o el contenido del producto de AEM, lo que rompía la funcionalidad del producto.

Al delinear claramente las jerarquías para el código de producto AEM y el código de cliente, se pueden evitar estos conflictos.

Con este fin, a partir de AEM 6.4 y para que continúe en futuras versiones, el contenido se está reestructurando fuera de /etc a otras carpetas del repositorio, junto con directrices sobre qué contenido va a dónde, siguiendo las siguientes reglas de alto nivel:

* El código de producto de AEM siempre se colocará en /libs, que no se debe sobrescribir con el código personalizado
* El código personalizado debe colocarse en /apps, /content y /conf

## Impacto en las actualizaciones de 6.5 {#impact-on-upgrades}

Al actualizar a AEM 6.5, un gran subconjunto del contenido en /etc se duplicará en otras carpetas del repositorio. Estas nuevas ubicaciones son las ubicaciones preferidas en las que se hace referencia al contenido. Sin embargo, se ha hecho todo lo posible para que la actualización de AEM 6.5 sea compatible con las ubicaciones anteriores en la carpeta /etc y, por lo tanto, en la mayoría de los casos el código de AEM seguirá haciendo referencia a las ubicaciones antiguas hasta que se realicen cambios activos, y en muchos casos manuales, en la aplicación de un cliente. Desde una perspectiva de cronología, hay dos categorías de cambios:

* Con la actualización a 6.5: algunos de los cambios de reestructuración /etc no son compatibles con versiones anteriores y, por lo tanto, las modificaciones deben planificarse e implementarse como parte de la actualización a AEM 6.5.
* Antes de una actualización futura: la gran mayoría de los cambios de reestructuración /etc se pueden aplazar hasta algún momento posterior a la actualización. Como se ha mencionado anteriormente, el código de AEM 6.5 seguirá haciendo referencia a las ubicaciones antiguas hasta que las modificaciones se implementen como parte de una versión del cliente. Aunque no hay una cronología forzada para la cual se deban realizar los cambios, se recomienda que se realicen antes de la actualización futura, ya que las funciones futuras pueden depender de las nuevas ubicaciones a las que se hace referencia. Además, la documentación de una función determinada hará referencia por convención a las nuevas ubicaciones y, por lo tanto, podría resultar confuso si se siguen utilizando las ubicaciones antiguas.

### Directrices de reestructuración {#restructuring-guidance}

Al planificar la actualización a AEM 6.5, se debe hacer referencia a las siguientes páginas por solución para evaluar el esfuerzo de trabajo:

* [Reestructuración de repositorios común a todas las soluciones de AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [Reestructuración del repositorio de AEM Sites](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [Reestructuración del repositorio de AEM Assets](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [Reestructuración del repositorio de Dynamic Media para AEM Assets](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [Reestructuración del repositorio de AEM Forms](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [Reestructuración del repositorio de AEM Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [Reestructuración del repositorio de AEM Commerce](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

Cada página contiene dos secciones que corresponden a la urgencia de los cambios necesarios. Cualquier elemento de la sección &quot;Con actualización de 6.5&quot; debe tratarse como parte del proyecto de actualización de AEM 6.5. Todo lo que se encuentre bajo la sección &quot;Antes de una actualización futura&quot; se puede diferir opcionalmente hasta después de la actualización.

Cada entrada en la página incluye un campo &quot;Directrices de reestructuración&quot;, que detalla la estrategia técnica recomendada para alinearse con el nuevo modelo de repositorio de 6.5, de modo que se haga referencia a las nuevas ubicaciones para el contenido que anteriormente se encontraba en la carpeta /etc. Un campo adicional &quot;Notas&quot; proporciona cualquier contexto útil adicional.
