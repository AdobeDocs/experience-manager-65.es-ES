---
title: Información acerca de la segmentación al crear una campaña
description: La segmentación es una consideración clave al crear una campaña.
uuid: 900da068-5dda-4b6b-8be3-4b7ad614126d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 36c87684-e62a-4983-b123-87f56dbf7bc5
exl-id: 61a5875f-ad09-4971-a886-b0d88e0c9967
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 31%

---

# Información acerca de la segmentación{#understanding-segmentation}

La segmentación es una consideración clave al crear una campaña. En la mayoría de los casos, deberá tener los segmentos ya definidos antes de iniciar la campaña.

Los visitantes del sitio tienen diferentes intereses y objetivos cuando llegan a un sitio. Comprender estos objetivos y cumplir las expectativas es un factor de éxito importante para el marketing en línea.

La segmentación ayuda a conseguirlo al analizar y caracterizar el comportamiento de un visitante:

* actividad en el sitio web
* perfil
* actividad en otros sitios web

El contenido puede personalizarse específicamente para satisfacer las necesidades y los intereses del visitante, según los segmentos con los que coincidan.

## Uso de la segmentación {#using-segmentation}

Los segmentos se definen en [Configuración de segmentación](/help/sites-administering/campaign-segmentation.md). Se utilizan para dirigir el contenido real que visualiza un público objetivo concreto.

## Terminología de segmentación {#segmentation-terminology}

Al analizar la segmentación, se emplea la siguiente terminología:

**Visitante** Un visitante es una persona que visita un sitio web. La visita de esa persona suele comenzar desde una página de referencia y luego pasa a una o más vistas de página del sitio web. Se puede crear un perfil de comportamiento a partir de los detalles de la visita de esa persona.

**Usuario** Un usuario es un visitante que se registra con el sitio web para recibir un perfil de cuenta. Para generar su perfil, proporcionan una identificación adicional, como una dirección de correo electrónico y el sexo, entre otros. También se puede recopilar información adicional, como actividad de la comunidad y patrones de compra, entre otros. A partir de la información proporcionada en el perfil, se puede crear un perfil demográfico.

**Rasgo** Un rasgo es una característica o propiedad de un visitante que se puede utilizar para determinar la pertenencia en un segmento específico.

**Segmento** Un segmento es un conjunto de visitantes que comparten determinadas características. Los segmentos deben ser distintivos, con un mínimo de superposición con otros segmentos.

**Características de comportamiento** Los rasgos de comportamiento son los que se relacionan con el comportamiento de un visitante en el sitio web. Entre estas características se incluyen:

* Interés en el sitio web, incluyendo las páginas y los productos comprados.
* Interés en el sitio web de referencia, incluyendo los términos de búsqueda utilizados o los anuncios en los que se ha hecho clic.
* Interés en otros sitios; se determina con herramientas como Spyjax.
* Lealtad del visitante; duración de la visita, frecuencia de las visitas.

**Características demográficas** Se trata de características de población seleccionadas, entre ellas:

* Edad
* Ingresos
* Tamaño de familia
* Estado civil
* Sexo
* Lugar de residencia

**Características derivadas** Algunos rasgos demográficos son difíciles de determinar sin registro, pero pueden obtenerse combinando rasgos demográficos y de comportamiento.

Por ejemplo, la combinación de la dirección URL de referencia (como característica de comportamiento) con datos demográficos (adquiridos con herramientas como [Google Ad Planner](https://www.google.com/adplanner/)) permite que los propietarios del sitio obtengan características demográficas de los visitantes.

**Subsegmento** Un segmento se puede subdividir en varios subsegmentos. Esto se lleva a cabo definiendo características adicionales.

**Página teaser** Una página de teaser se dirige a una audiencia específica. Incluye contenido reutilizable que se puede emplear en el párrafo de teaser.

**Campaign** Una campaña es una colección de páginas de teaser y páginas de marketing por correo electrónico, como boletines informativos o invitaciones. Normalmente una campaña se ejecuta durante un período limitado y está precedida por otra campaña.

**Párrafo de teaser** Se trata de un párrafo que extrae contenido de otra página que depende de una estrategia de selección. Esta estrategia de selección puede tener en cuenta segmentos y campañas.

**Lista** Se extrae una lista de un segmento de usuarios registrados. Por ejemplo, la ubicación se utiliza para dirigir los contenidos del párrafo de teaser.

>[!NOTE]
>
>Consulte lo siguiente [Segmentación](/help/sites-administering/campaign-segmentation.md) AEM para obtener más información sobre los segmentos de en la.
