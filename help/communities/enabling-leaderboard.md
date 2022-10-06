---
title: Función de portapapeles
seo-title: Leaderboard Feature
description: Adición de un componente de panel de encabezado a una página
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

# Función de portapapeles {#leaderboard-feature}

## Introducción {#introduction}

La variable `Leaderboard` proporciona la capacidad de obtener una idea de cómo interactúan los miembros dentro de la comunidad mediante la clasificación de los miembros según los puntos ganados (puntuación básica) o su experiencia (puntuación avanzada).

Antes de incluir el componente de panel de encabezado en una página, es necesario configurar [Puntuación y distintivos de comunidades](/help/communities/implementing-scoring.md).

Esta sección de la documentación describe:

* Adición de la variable `Leaderboard` componente a un [sitio de la comunidad](/help/communities/overview.md#community-sites).
* Ajustes de configuración para `Leaderboard` componente.

### Adición de un tablero de vanguardia a una página {#adding-a-leaderboard-to-a-page}

Para agregar un `Leaderboard` a una página en modo de autor, busque el componente

* `Communities / Leaderboard`

y arrástrela a su lugar en una página.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de Communities](/help/communities/basics.md).

Cuando se coloca por primera vez en una página de un sitio de comunidad, así es como aparece el componente:

![panel](assets/leaderboard.png)

### Configuración del panel de clientes {#configuring-leaderboard}

Seleccione la colocación `Leaderboard` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

![configurar tablero de mandos](assets/configure-leaderboard.png)

#### Ficha Configuración {#settings-tab}

En el **[!UICONTROL Configuración]** especifique qué información relacionada con el miembro se muestra :

* **Nombre para mostrar**

   Un nombre descriptivo para mostrar para el tablero, que refleja las reglas seleccionadas para mostrar distintivos y puntuaciones.
El valor predeterminado es `Leaderboard`, si no se ha introducido nada.

* **Distintivo**

   Si se selecciona, se incluye una columna para los iconos de distintivo en el panel de mandos.
El valor predeterminado no está seleccionado.

* **Nombre de distintivo**

   Si se selecciona, se incluye una columna para el nombre del distintivo en el panel de control.
El valor predeterminado no está seleccionado.

* **Usar Avatar**

   Si se selecciona, la imagen de avatar del miembro se incluye en el panel de control, junto al vínculo de nombre a su perfil de miembro.
El valor predeterminado no está seleccionado.

#### Ficha Reglas {#rules-tab}

En el **Reglas** , el sitio de la comunidad y sus reglas de puntuación y de distintivo

* **Ubicación de la regla**

   (Obligatorio) Ubicación en la que está configurada la regla Puntuación / Distintivo.

* **Regla de puntuación**

   (Obligatorio) Regla específica que genera las puntuaciones que se van a mostrar.

* **Regla de creación de distintivos**

   (Obligatorio) Regla específica que genera el distintivo que se va a mostrar.

* **Límite de visualización**

   El número de miembros que se mostrarán por página.El valor predeterminado es 10.

### Ejemplo: Placa de encabezado de los participantes {#example-participants-leaderboard}

Este panel de liderazgo informa de los resultados de la aplicación de reglas de puntuación básicas.

Configuración de componentes del panel de vanguardia:

* Ficha Configuración :

   * Nombre para mostrar = `Participation Board`
   * `checked`:

      * Distintivo
      * Nombre de distintivo
      * Usar Avatar

* Ficha Reglas :

   * Ubicación de la regla = `/content/sites/<site name>/jcr:content`
   * Regla de puntuación = `/libs/settings/community/scoring/rules/forums-scoring`
   * Regla de creación de distintivos = `/libs/settings/community/badging/rules//reference-badging`
   * Límite de visualización = `10`

![participante-guía](assets/participants-leaderboard.png)

### Ejemplo: Panel de expertos {#example-experts-leaderboard}

Este panel de control resulta de la aplicación de reglas de puntuación avanzadas.

Configuración de componentes del panel de vanguardia:

* Ficha Configuración :

   * Nombre para mostrar = `Expertise Board`
   * `checked`:

      * Distintivo
      * Usar Avatar

* Ficha Reglas :

   * Ubicación de la regla = `/content/sites/<site name>/jcr:content`
   * Regla de puntuación = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * Regla de creación de distintivos = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Límite de visualización = `10`

![experto](assets/experts-leaderboard.png)

### Información adicional {#additional-information}

Puede encontrar más información en la [Elementos esenciales del panel de control](/help/communities/leaderboard.md) para desarrolladores.

Las instrucciones para crear reglas se proporcionan en la [Puntuación y distintivos de comunidades](/help/communities/implementing-scoring.md) para administradores.
