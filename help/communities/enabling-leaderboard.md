---
title: Función de clasificación
seo-title: Leaderboard Feature
description: Adición de un componente Tabla de posiciones a una página
seo-description: Adding a Leaderboard component to a page
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 10%

---

# Función de clasificación {#leaderboard-feature}

## Introducción {#introduction}

El `Leaderboard` Este componente proporciona la capacidad de obtener una idea de cómo interactúan los miembros dentro de la comunidad mediante la clasificación de los miembros según los puntos obtenidos (puntuación básica) o su experiencia (puntuación avanzada).

Antes de incluir el componente de tabla de posiciones en una página, es necesario configurar [Puntuación y distintivos de comunidades](/help/communities/implementing-scoring.md).

Esta sección de la documentación describe lo siguiente:

* Añadir el `Leaderboard` componente a [sitio comunitario](/help/communities/overview.md#community-sites).
* Ajustes de configuración para `Leaderboard` componente.

### Agregar una tabla de posiciones a una página {#adding-a-leaderboard-to-a-page}

Para agregar un `Leaderboard` a una página en modo de autor, busque el componente

* `Communities / Leaderboard`

y arrástrela a su lugar en una página.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](/help/communities/basics.md).

Cuando se coloca por primera vez en una página de un sitio de la comunidad, así es como aparece el componente:

![tabla de clasificación](assets/leaderboard.png)

### Configurar tabla de posiciones {#configuring-leaderboard}

Seleccione el colocado `Leaderboard` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

![configure-leader-board](assets/configure-leaderboard.png)

#### Pestaña Configuración {#settings-tab}

En el **[!UICONTROL Configuración]** , especifique qué información relacionada con el miembro se muestra :

* **Nombre para mostrar**

   Un nombre descriptivo para mostrar para el tablero, que refleje las reglas seleccionadas para mostrar insignias y puntuaciones.
El valor predeterminado es `Leaderboard`, si no se ha introducido nada.

* **Distintivo**

   Si se selecciona, se incluye una columna para los iconos de distintivo en la tabla de clasificación.
El valor predeterminado está desmarcado.

* **Nombre de distintivo**

   Si se selecciona, se incluye una columna para el nombre del distintivo en la tabla de clasificación.
El valor predeterminado está desmarcado.

* **Usar avatar**

   Si se selecciona, la imagen de avatar del miembro se incluirá en la tabla de clasificación, junto al vínculo de su nombre a su perfil de miembro.
El valor predeterminado está desmarcado.

#### Pestaña Reglas {#rules-tab}

En el **Reglas** , el sitio de la comunidad y sus reglas de puntuación y distintivos

* **Ubicación de la regla**

   (Obligatorio) Ubicación donde se configura la regla de puntuación/distintivos.

* **Regla de puntuación**

   (Obligatorio) Regla específica que genera las puntuaciones que se van a mostrar.

* **Regla de creación de distintivos**

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
   * Regla de creación de distintivos = `/libs/settings/community/badging/rules//reference-badging`
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
   * Regla de creación de distintivos = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Límite de visualización = `10`

![tabla de clasificación de expertos](assets/experts-leaderboard.png)

### Información adicional {#additional-information}

Puede encontrar más información en la [Leaderboard Essentials](/help/communities/leaderboard.md) para desarrolladores.

Las instrucciones para la creación de reglas se proporcionan en [Puntuación y distintivos de comunidades](/help/communities/implementing-scoring.md) para administradores.
