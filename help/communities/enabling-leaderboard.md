---
title: Función de clasificación
description: Descubra cómo el componente Tabla de clasificación le permite ver cómo los miembros interactúan dentro de la comunidad clasificando a los miembros en función de los puntos obtenidos y la experiencia.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 2%

---

# Función de clasificación {#leaderboard-feature}

## Introducción {#introduction}

El componente `Leaderboard` le ayuda a tener una idea de cómo interactúan los miembros dentro de la comunidad mediante la clasificación de los miembros según los puntos obtenidos (puntuación básica) o su experiencia (puntuación avanzada).

Antes de incluir el componente de tabla de clasificación en una página, es necesario configurar [insignias y puntuación de comunidades](/help/communities/implementing-scoring.md).

Esta sección de la documentación describe lo siguiente:

* Agregando el componente `Leaderboard` a [sitio de la comunidad](/help/communities/overview.md#community-sites).
* Ajustes de configuración para el componente `Leaderboard`.

### Agregar una tabla de posiciones a una página {#adding-a-leaderboard-to-a-page}

Para agregar un componente `Leaderboard` a una página en modo de autor, busque el componente

* `Communities / Leaderboard`

Y arrástrela a su lugar en una página.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Cuando se coloca por primera vez en una página de un sitio de la comunidad, así es como aparece el componente:

![tabla de clasificación](assets/leaderboard.png)

### Configurar tabla de posiciones {#configuring-leaderboard}

Seleccione el componente `Leaderboard` colocado para que pueda acceder y seleccionar el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar-nuevo](assets/configure-new.png)

![configurar tabla de clasificación](assets/configure-leaderboard.png)

#### Pestaña Configuración {#settings-tab}

En la ficha **[!UICONTROL Configuración]**, especifique qué información relacionada con el miembro se muestra:

* **Nombre para mostrar**

  Un nombre descriptivo para mostrar para el tablero, que refleje las reglas seleccionadas para mostrar insignias y puntuaciones.
El valor predeterminado es `Leaderboard` si no se escribe nada.

* **Insignia**

  Si se selecciona, se incluye una columna para los iconos de distintivo en la tabla de clasificación.
El valor predeterminado está desmarcado.

* **Nombre de distintivo**

  Si se selecciona, se incluye una columna para el nombre del distintivo en la tabla de clasificación.
El valor predeterminado está desmarcado.

* **Usar avatar**

  Si se selecciona, la imagen de avatar del miembro se incluirá en la tabla de clasificación, junto al vínculo de su nombre a su perfil de miembro.
El valor predeterminado está desmarcado.

#### Pestaña Reglas {#rules-tab}

En la ficha **Reglas**, el sitio de la comunidad y sus reglas de puntuación y distintivos

* **Ubicación de la regla**

  (Obligatorio) Ubicación donde se configura la regla de puntuación/distintivos.

* **Regla de puntuación**

  (Obligatorio) Regla específica que genera las puntuaciones que se van a mostrar.

* **Regla de identificación**

  (Obligatorio) Regla específica que genera el distintivo que se va a mostrar.

* **Límite de visualización**

  Número de miembros que se mostrarán por página. El valor predeterminado es 10.

### Ejemplo: tabla de posiciones de participantes {#example-participants-leaderboard}

Estos informes de tabla de posiciones son el resultado de aplicar reglas de puntuación básicas.

Configuración de componentes de clasificación:

* Pestaña Configuración:

   * Nombre para mostrar = `Participation Board`
   * `checked`:

      * Distintivo
      * Nombre de distintivo
      * Usar avatar

* Pestaña Reglas:

   * Ubicación de la regla = `/content/sites/<site name>/jcr:content`
   * Regla de puntuación = `/libs/settings/community/scoring/rules/forums-scoring`
   * Regla de distintivos = `/libs/settings/community/badging/rules//reference-badging`
   * Límite de visualización = `10`

![participantes-tabla de clasificación](assets/participants-leaderboard.png)

### Ejemplo: tabla de clasificación de expertos {#example-experts-leaderboard}

Estos informes de tabla de clasificación son el resultado de aplicar reglas de puntuación avanzadas.

Configuración de componentes de clasificación:

* Pestaña Configuración:

   * Nombre para mostrar = `Expertise Board`
   * `checked`:

      * Distintivo
      * Usar avatar

* Pestaña Reglas:

   * Ubicación de la regla = `/content/sites/<site name>/jcr:content`
   * Regla de puntuación = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * Regla de distintivos = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Límite de visualización = `10`

![tabla de clasificación de expertos](assets/experts-leaderboard.png)

### Información adicional {#additional-information}

Encontrará más información en la página de [Elementos esenciales de la tabla de clasificación](/help/communities/leaderboard.md) para desarrolladores.

Encontrará instrucciones para crear reglas en la página [Insignias y puntuación de comunidades](/help/communities/implementing-scoring.md) para los administradores.
