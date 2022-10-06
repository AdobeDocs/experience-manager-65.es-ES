---
title: Información acerca de la segmentación
seo-title: Understanding Segmentation
description: La segmentación es una consideración clave al crear una campaña
seo-description: Segmentation is a key consideration when creating a campaign
uuid: 900da068-5dda-4b6b-8be3-4b7ad614126d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 36c87684-e62a-4983-b123-87f56dbf7bc5
exl-id: 61a5875f-ad09-4971-a886-b0d88e0c9967
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 67%

---

# Información acerca de la segmentación{#understanding-segmentation}

La segmentación es una consideración clave al crear una campaña. En la mayoría de los casos, será necesario tener segmentos ya definidos antes de comenzar una campaña.

Los visitantes del sitio tienen diferentes intereses y objetivos cuando acceden al sitio. Comprender estos objetivos y cumplir las expectativas son importantes factores de éxito para el marketing en línea.

La segmentación ayuda a lograr esto, analizando y caracterizando los siguientes aspectos de un visitante:

* La actividad en el sitio web.
* El perfil.
* La actividad en otros sitios web.

El contenido puede personalizarse específicamente para satisfacer las necesidades y los intereses del visitante, según los segmentos con los que coincidan.

## Uso de la segmentación {#using-segmentation}

Los segmentos se definen en [Configurar segmentación](/help/sites-administering/campaign-segmentation.md). Se utilizan para dirigir el contenido real que visualiza un público objetivo concreto.

## Terminología de segmentación {#segmentation-terminology}

Al analizar la segmentación, se emplea la siguiente terminología:

**Visitante** Un visitante es una persona que visita un sitio web. La visita de esa persona se suele iniciar desde una página de referencia y después se mueve a una o varias vistas de página en su propio sitio web. Se puede crear un perfil de comportamiento a partir de la información de la visita de esa persona.

**Usuario** Un usuario es un visitante que se registra con el sitio web para recibir un perfil de cuenta. Para generar su perfil, proporcionan identificación adicional como, por ejemplo, una dirección de correo electrónico y el género, entre otros datos. La información adicional también se puede recopilar, incluyendo la actividad de la comunidad y los modelos de compra, entre otros datos. En función de la información proporcionada en el perfil, se puede crear un perfil demográfico.

**Característica** Un rasgo es una característica o propiedad de un visitante que se puede usar para determinar la pertenencia a un segmento específico.

**Segmento** Un segmento es una colección de visitantes que comparten ciertas características. Los segmentos deben ser distintivos, con un mínimo de superposición con otros segmentos.

**Características de comportamiento** Las características de comportamiento son aquellas que se relacionan con el comportamiento de un visitante en el sitio web. Entre estas características se incluyen:

* Interés en el sitio web, incluyendo las páginas y los productos comprados.
* Interés en el sitio web de referencia, incluyendo los términos de búsqueda utilizados o los anuncios en los que se ha hecho clic.
* Interés en otros sitios; se determina con herramientas como Spyjax.
* Fidelidad del visitante; duración de la visita, frecuencia de las visitas.

**Características demográficas** Estas son características de población seleccionadas, entre las que se incluyen:

* Edad
* Ingresos
* Tamaño familiar
* Estado civil
* Sexo
* Lugar de residencia

**Características derivadas** Algunas características demográficas son difíciles de determinar sin registro, pero se pueden derivar combinando características demográficas y de comportamiento.

Por ejemplo, la combinación de la dirección URL de referencia (como característica de comportamiento) con datos demográficos (adquiridos con herramientas como [Google Ad Planner](https://www.google.com/adplanner/)) permite que los propietarios del sitio obtengan características demográficas de los visitantes.

**Subsegmento** Un segmento se puede subdividir en varios subsegmentos. Esto se lleva a cabo definiendo características adicionales.

**Página Teaser** Una página de teaser está dirigida a una audiencia específica. Incluye contenido reutilizable que se puede emplear en el párrafo de teaser.

**Campaign** Una campaña es una colección de páginas de teaser y páginas de marketing por correo electrónico, como newsletters o invitaciones. Una campaña se suele llevar a cabo durante un período limitado y está precedida de otra campaña.

**Párrafo de teaser** Se trata de un párrafo que extrae contenido de otra página en función de una estrategia de selección. Esta estrategia de selección puede tener en cuenta segmentos y campañas.

**Lista** Una lista se extrae de un segmento de usuarios registrados. Por ejemplo, la ubicación se utiliza para dirigir los contenidos del párrafo de teaser.

>[!NOTE]
>
>Consulte [Segmentación](/help/sites-administering/campaign-segmentation.md) para obtener más información sobre los segmentos de AEM.
