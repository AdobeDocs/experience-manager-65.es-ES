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

El `Rating` componente se utiliza de forma independiente o junto con otras funciones de Comunidades. Este componente permite a los miembros de la comunidad con sesión iniciada expresar sus opiniones mediante la clasificación del contenido.

## Adding a Rating to a Page {#adding-a-rating-to-a-page}

Para agregar un `Rating` componente a una página en modo de autor, ubique el componente `Communities / Rating` y arrástrelo a su lugar en una página, como una posición relativa a la función que deben clasificar los miembros.

Para obtener la información necesaria, visite [Communities Components Basics](basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [](rating-basics.md#essentials-for-client-side) requeridas del lado del cliente, así es como aparecerá el `Rating` componente.

![clasificación](assets/rating.png)

## Configuración de clasificación {#configuring-rating}

Seleccione el componente colocado al que desea acceder y seleccione el `Rating` `Configure` icono que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

En la ficha **[!UICONTROL Textos y etiquetas]** , especifique el identificador interno de la clasificación.

![nombre_de_talyname](assets/tallyname.png)

**[!UICONTROL Tally Name]**(*Requerido*) Un nombre sencillo para el `Rating` que identifica de forma exclusiva esta instancia. Debe ser un nombre de nodo válido para el repositorio.

## Experiencia de Visitante del sitio {#site-visitor-experience}

### Miembros {#members}

Solo se permite una clasificación por miembro. El miembro puede cambiar su calificación en cualquier momento.

### Anónimo {#anonymous}

No se admite la publicación anónima de una clasificación. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Rating Essentials](rating-basics.md) para desarrolladores.
