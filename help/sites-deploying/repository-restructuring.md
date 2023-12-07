---
title: AEM Reestructuración de repositorios en 6.5
description: AEM Obtenga información acerca de los conceptos básicos y el razonamiento detrás de la reestructuración de repositorios en.5
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# AEM Reestructuración de repositorios en 6.5{#repository-restructuring-in-aem}

## Introducción {#introduction}

AEM Antes de la versión 6.4 de, el código de cliente se implementaba en áreas impredecibles del JCR que estaban sujetas a cambios en las actualizaciones. AEM Debido a esto, era común que las versiones formales de la sobrescribieran código, configuración o contenido personalizados. AEM Además, los cambios del cliente a veces sobrescribían el código o el contenido del producto, lo que rompe la funcionalidad del producto.

AEM Al delinear claramente las jerarquías para el código de producto y el código de cliente, se pueden evitar estos conflictos.

AEM Con este fin, a partir de la versión 6.4 de la versión 6.4 y para continuar en futuras versiones, el contenido se está reestructurando fuera de /etc a otras carpetas del repositorio, junto con directrices sobre qué contenido va a dónde, siguiendo las siguientes reglas de alto nivel:

* AEM El código de producto siempre se colocará en /libs, que no se debe sobrescribir con el código personalizado
* El código personalizado debe colocarse en /apps, /content y /conf

## Impacto en las actualizaciones de 6.5 {#impact-on-upgrades}

AEM Al actualizar a la versión 6.5, un gran subconjunto del contenido en /etc se duplica en otras carpetas del repositorio. Estas nuevas ubicaciones son las ubicaciones preferidas en las que se hace referencia al contenido. AEM AEM Sin embargo, se ha hecho todo lo posible para que la actualización de la versión 6.5 de la aplicación sea compatible con las ubicaciones anteriores de la carpeta /etc y, por lo tanto, en la mayoría de los casos se seguirá haciendo referencia a las ubicaciones antiguas mediante código hasta que se realicen cambios activos, y en muchos casos manuales, en la aplicación de un cliente. Desde una perspectiva de cronología, hay dos categorías de cambios:

* AEM Con la actualización a 6.5: algunos de los cambios de reestructuración /etc no son compatibles con versiones anteriores y, por lo tanto, las modificaciones deben planificarse e implementarse como parte de la actualización a 6.5 de.
* Antes de una actualización futura: la gran mayoría de los cambios de reestructuración /etc se pueden aplazar hasta algún momento posterior a la actualización. AEM Como se ha mencionado anteriormente, el código de la versión 6.5 de seguirá haciendo referencia a las ubicaciones antiguas hasta que las modificaciones se implementen como parte de una versión del cliente. Aunque no hay una cronología forzada para la cual se deban realizar los cambios, se recomienda que se realicen antes de la actualización futura, ya que las funciones futuras pueden depender de las nuevas ubicaciones a las que se hace referencia. Además, la documentación de una función determinada hará referencia por convención a las nuevas ubicaciones y, por lo tanto, podría resultar confuso si se siguen utilizando las ubicaciones antiguas.

### Directrices de reestructuración {#restructuring-guidance}

AEM Al planificar la actualización a la versión 6.5 de la versión, se debe hacer referencia a las siguientes páginas por solución para evaluar el esfuerzo de trabajo:

* [AEM Reestructuración de repositorios común a todas las soluciones de la](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [Reestructuración del repositorio de AEM Sites](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [Reestructuración del repositorio de AEM Assets](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [Reestructuración del repositorio de AEM Assets Dynamic Media](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [Reestructuración del repositorio de AEM Forms](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [Reestructuración del repositorio de AEM Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM Reestructuración del repositorio de Commerce](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

Cada página contiene dos secciones que corresponden a la urgencia de los cambios necesarios. AEM Cualquier elemento de la sección &quot;Con actualización de 6.5&quot; debe abordarse como parte del proyecto de actualización de 6.5 de. Todo lo que se encuentre bajo la sección &quot;Antes de una actualización futura&quot; se puede diferir opcionalmente hasta después de la actualización.

Cada entrada en la página incluye un campo &quot;Directrices de reestructuración&quot;, que detalla la estrategia técnica recomendada para alinearse con el nuevo modelo de repositorio de 6.5, de modo que se haga referencia a las nuevas ubicaciones para el contenido que anteriormente se encontraba en la carpeta /etc. Un campo adicional &quot;Notas&quot; proporciona cualquier contexto útil adicional.
