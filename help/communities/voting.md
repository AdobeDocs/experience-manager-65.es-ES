---
title: Uso de la votación
description: Aprenda a añadir el componente Votación a una página que permita a los miembros de la comunidad conectados clasificar un contenido en particular, como una respuesta.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# Uso de la votación {#using-voting}

El `Voting` El componente es una herramienta útil que permite a los miembros de la comunidad clasificar un fragmento de contenido en particular, como una respuesta dentro de un componente de control de calidad. Con el `Voting` componente, los miembros seleccionan flechas arriba o abajo para indicar su opinión.

## Agregar la votación a una página {#adding-voting-to-a-page}

Para agregar un `Voting` para crear una página en el modo Autor, utilice el explorador de componentes. Localizar `Communities / Voting` y arrástrela a su lugar en una página, como una posición relativa a la función por la que los usuarios pueden votar.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](essentials-voting.md#essentials-for-client-side) están incluidos, así es como se `Voting` aparece el componente.

![componente de votación](assets/voting-component.png)

## Configuración de votación {#configuring-voting}

Seleccione el colocado `Voting` para que pueda acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

En el **[!UICONTROL Textos y etiquetas]** , especifique las propiedades utilizadas para registrar votos.

![etiqueta de votación](assets/voting-label.png)

* **[!UICONTROL Etiqueta de respuesta positiva]**

  (*Requerido*) El nombre de propiedad interno de una respuesta positiva.

* **[!UICONTROL Etiqueta de respuesta negativa]**

  (*Requerido*) El nombre de propiedad interno de una respuesta negativa.

* **[!UICONTROL Nombre de recuento]**

  (*Requerido*) El nombre de propiedad interno e identificable para esta instancia de un componente de voto.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Miembros {#members}

Los diputados sólo podrán votar una vez, pero podrán cambiar su voto en cualquier momento.

### Anónimo {#anonymous}

No se admite el voto anónimo. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar en la votación una vez.

## Información adicional {#additional-information}

Puede encontrar más información en la [Voting Essentials](essentials-voting.md) para desarrolladores.
