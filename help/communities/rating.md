---
title: Uso de clasificaciones
seo-title: Uso de clasificaciones
description: Añadir un componente Clasificación en una página
seo-description: Añadir un componente Clasificación en una página
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
translation-type: tm+mt
source-git-commit: 0051791da06d15a48b82cf93164a89b4ea42ce98
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 2%

---


# Uso de clasificaciones {#using-ratings}

El componente `Rating` se utiliza de forma independiente o junto con otras características de Communities. Este componente permite a los miembros de la comunidad con sesión iniciada expresar sus opiniones mediante la clasificación del contenido.

## Añadir una clasificación en una página {#adding-a-rating-to-a-page}

Para agregar un componente `Rating` a una página en modo de autor, localice el componente `Communities / Rating` y arrástrelo a su lugar en una página, como una posición relativa a la función que los miembros deben clasificar.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de comunidades](basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](rating-basics.md#essentials-for-client-side), así es como aparecerá el componente `Rating`.

![clasificación](assets/rating.png)

## Configuración de clasificación {#configuring-rating}

Seleccione el componente `Rating` colocado para acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

En la ficha **[!UICONTROL Textos y etiquetas]** debe especificar el identificador interno de la clasificación.

![nombre_de_talyname](assets/tallyname.png)

**[!UICONTROL Tally Name]**
(*Requerido*) Un nombre sencillo para la instancia  `Rating` que identifica exclusivamente a esta instancia. Debe ser un nombre de nodo válido para el repositorio.

## Experiencia de Visitante del sitio {#site-visitor-experience}

### Miembros {#members}

Solo se permite una clasificación por miembro. El miembro puede cambiar su calificación en cualquier momento.

### Anónimo {#anonymous}

No se admite la publicación anónima de una clasificación. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Rating Essentials](rating-basics.md) para desarrolladores.
