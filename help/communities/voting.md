---
title: Uso de la votación
seo-title: Uso de la votación
description: Añadir el componente Votación en una página
seo-description: Añadir el componente Votación en una página
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---


# Uso de Votación {#using-voting}

El componente `Voting` es una herramienta útil que permite a los miembros de la comunidad clasificar un contenido determinado, como una respuesta dentro de un componente QnA. Con el componente `Voting`, los miembros seleccionan flechas arriba o abajo para indicar su opinión.

## Añadir la votación en una página {#adding-voting-to-a-page}

Para agregar un componente `Voting` a una página en modo de autor, utilice el navegador de componentes para ubicar `Communities / Voting` y arrástrelo a su lugar en una página, como una posición relativa a la función en la que los usuarios deben votar.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de comunidades](basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](essentials-voting.md#essentials-for-client-side), así es como aparecerá el componente `Voting`.

![componente de votación](assets/voting-component.png)

## Configuración de la votación {#configuring-voting}

Seleccione el componente `Voting` colocado para acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar](assets/configure-new.png)

En la ficha **[!UICONTROL Textos y etiquetas]**, especifique las propiedades utilizadas para registrar votos.

![rótulo de voto](assets/voting-label.png)

* **[!UICONTROL Etiqueta de respuesta positiva]**

   (*Requerido*) El nombre de la propiedad interna para una respuesta positiva.

* **[!UICONTROL Etiqueta de respuesta negativa]**

   (*Requerido*) El nombre de la propiedad interna para una respuesta negativa.

* **[!UICONTROL Nombre de recuento]**

   (*Requerido*) El nombre de propiedad interno identificable para esta instancia de un componente de votación.

## Experiencia de Visitante del sitio {#site-visitor-experience}

### Miembros {#members}

Los Miembros sólo podrán votar una vez, pero podrán modificarlo en cualquier momento.

### Anónimo {#anonymous}

No se admite la votación anónima. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar en la votación una vez.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Voting Essentials](essentials-voting.md) para desarrolladores.
