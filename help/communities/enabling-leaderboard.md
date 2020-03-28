---
title: Función de tabla de clasificación
seo-title: Función de tabla de clasificación
description: Añadir un componente de tabla de clasificación en una página
seo-description: Añadir un componente de tabla de clasificación en una página
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Función de tabla de clasificación {#leaderboard-feature}

## Introducción {#introduction}

El `Leaderboard` componente proporciona la capacidad de obtener una idea de cómo interactúan los miembros dentro de la comunidad mediante la clasificación de los miembros según los puntos ganados (puntuación básica) o su experiencia (puntuación avanzada).

Antes de incluir el componente de la tabla de clasificación en una página, es necesario configurar la Puntuación de [comunidades y los distintivos](/help/communities/implementing-scoring.md).

Esta sección de la documentación describe

* Añadir el `Leaderboard` componente en un sitio [de comunidad](/help/communities/overview.md#community-sites)
* Configuración del `Leaderboard` componente

### Adding a Leaderboard to a Page {#adding-a-leaderboard-to-a-page}

Para agregar un `Leaderboard` componente a una página en modo de autor, ubique el componente

* `Communities / Leaderboard`

y arrástrelo a su lugar en una página.

Para obtener la información necesaria, visite [Communities Components Basics](/help/communities/basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se coloca por primera vez en una página de un sitio de comunidad, así es como aparece el componente:

![chlimage_1-19](assets/chlimage_1-19.png)

### Configuración de la tabla de clasificación {#configuring-leaderboard}

Seleccione el componente colocado al que desea acceder y seleccione el `Leaderboard` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-20](assets/chlimage_1-20.png) ![chlimage_1-21](assets/chlimage_1-21.png)

#### Ficha Configuración {#settings-tab}

En la ficha **Configuración** , especifique qué información relacionada con el miembro se muestra:

* **Nombre para mostrar**

   Nombre descriptivo que se mostrará en el tablero, que refleja las reglas seleccionadas para mostrar distintivos y puntuaciones.
El valor predeterminado es `Leaderboard`si no se ha introducido nada.

* **Distintivo**

   Si se selecciona, se incluye una columna para los iconos de distintivo en la tabla de clasificación.
El valor predeterminado no está marcado.

* **Nombre de distintivo**

   Si se selecciona, se incluye una columna para el nombre del distintivo en la tabla de clasificación.
El valor predeterminado no está marcado.

* **Usar avatar**

   Si se selecciona, la imagen de avatar del miembro se incluye en la tabla de clasificación, junto al vínculo de nombre del perfil del miembro.
El valor predeterminado no está marcado.

#### Ficha Reglas {#rules-tab}

Bajo la ficha **Reglas** , el sitio de la comunidad y sus reglas de puntuación y de distintivo

* **Ubicación de la regla**

   (Requerido) Ubicación en la que está configurada la regla de Puntuación/Insignia.

* **Regla de puntuación**

   (Requerido) Regla específica que genera las puntuaciones que se van a mostrar.

* **Regla de creación de distintivos**

   (Requerido) Regla específica que genera el distintivo para mostrar.

* **Límite de visualización**

   Número de miembros que mostrar por página.El valor predeterminado es 10.

### Ejemplo: Mesa de liderazgo de los participantes {#example-participants-leaderboard}

Este marcador de posición indica los resultados de la aplicación de reglas de puntuación básicas.

Configuración del componente de la tabla de clasificación:

* Ficha Configuración:

   * Nombre para mostrar = `Participation Board`
   * `checked`:

      * Distintivo
      * Nombre de distintivo
      * Usar avatar

* Ficha Reglas:

   * Ubicación de la regla = `/content/sites/communities/jcr:content`
   * Regla de puntuación = `/etc/community/scoring/rules/forums-scoring`
   * Regla de creación de distintivos = `/etc/community/badging/rules/reference-badging`
   * Límite de visualización = `10`

![chlimage_1-22](assets/chlimage_1-22.png)

### Ejemplo: Panel de liderazgo de expertos {#example-experts-leaderboard}

Este marcador de posición indica los resultados de la aplicación de reglas de puntuación avanzadas.

Configuración del componente de la tabla de clasificación:

* Ficha Configuración:

   * Nombre para mostrar = `Expertise Board`
   * `checked`:

      * Distintivo
      * Usar avatar

* Ficha Reglas:

   * Ubicación de la regla = `/content/sites/communities/jcr:content`
   * Regla de puntuación = `/etc/community/scoring/rules/adv-forums-scoring`
   * Regla de creación de distintivos = `/etc/community/badging/rules/adv-forums-badging`
   * Límite de visualización = `10`

![chlimage_1-23](assets/chlimage_1-23.png)

### Información adicional {#additional-information}

Puede encontrar más información en la página [Leaderboard Essentials](/help/communities/leaderboard.md) para desarrolladores.

Las instrucciones para crear reglas se proporcionan en la página Puntuación de [comunidades y distintivos](/help/communities/implementing-scoring.md) para administradores.
