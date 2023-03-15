---
title: Uso de la votación
seo-title: Using Voting
description: Adición del componente Votación a una página
seo-description: Adding the Voting component to a page
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 5%

---

# Uso de la votación {#using-voting}

El `Voting` El componente es una herramienta útil que permite a los miembros de la comunidad clasificar un fragmento de contenido en particular, como una respuesta dentro de un componente de control de calidad. Con el `Voting` componente, los miembros seleccionan flechas arriba o abajo para indicar su opinión.

## Agregar la votación a una página {#adding-voting-to-a-page}

Para agregar un `Voting` a una página en modo de autor, utilice el navegador de componentes para localizar `Communities / Voting` y arrástrela a su lugar en una página, como una posición relativa a la función por la que los usuarios pueden votar.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](essentials-voting.md#essentials-for-client-side) están incluidos, así es como se `Voting` El componente aparecerá.

![componente de votación](assets/voting-component.png)

## Configuración de votación {#configuring-voting}

Seleccione el colocado `Voting` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

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
