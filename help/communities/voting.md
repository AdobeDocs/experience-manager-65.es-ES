---
title: Uso de la votación
seo-title: Uso de la votación
description: Adición del componente Voto a una página
seo-description: Adición del componente Voto a una página
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Uso de la votación {#using-voting}

El `Voting` componente es una herramienta útil que permite a los miembros de la comunidad clasificar un contenido determinado, como una respuesta dentro de un componente QnA. Con el `Voting` componente, los miembros seleccionan flechas arriba o abajo para indicar su opinión.

## Adición de votos a una página {#adding-voting-to-a-page}

Para agregar un `Voting` componente a una página en modo de autor, utilice el navegador de componentes para ubicarlo `Communities / Voting` y arrastrarlo hasta su lugar en una página, como una posición relativa a la función por la que los usuarios deben votar.

Para obtener la información necesaria, visite [Communities Components Basics](basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [](essentials-voting.md#essentials-for-client-side) requeridas del lado del cliente, así es como aparecerá el `Voting` componente.

![chlimage_1-307](assets/chlimage_1-307.png)

## Configuración de la votación {#configuring-voting}

Seleccione el componente colocado al que desea acceder y seleccione el `Voting` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-308](assets/chlimage_1-308.png)

En la ficha **[!UICONTROL Textos y etiquetas]** , especifique las propiedades utilizadas para registrar votos.

![chlimage_1-309](assets/chlimage_1-309.png)

* **[!UICONTROL Etiqueta]** de respuesta positiva (*obligatoria*) El nombre de la propiedad interna para una respuesta positiva.

* **[!UICONTROL Etiqueta]** de respuesta negativa (*obligatoria*) El nombre de la propiedad interna para una respuesta negativa.

* **[!UICONTROL Tally Name]**(*Requerido*) El nombre de propiedad interno identificable para esta instancia de un componente de votación.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Miembros {#members}

Los Miembros sólo podrán votar una vez, pero podrán modificarlo en cualquier momento.

### Anónimo {#anonymous}

No se admite la votación anónima. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar en la votación una vez.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Voting Essentials](essentials-voting.md) para desarrolladores.
