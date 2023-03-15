---
title: Uso de clasificaciones
seo-title: Using Ratings
description: Adición de un componente Clasificación a una página
seo-description: Adding a Rating component to a page
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# Uso de clasificaciones {#using-ratings}

El `Rating` El componente se utiliza de forma independiente o junto con otras funciones de Communities. Este componente permite a los miembros de la comunidad que iniciaron sesión expresar sus opiniones mediante la clasificación de contenido.

## Añadir una clasificación a una página {#adding-a-rating-to-a-page}

Para agregar un `Rating` a una página en modo de autor, busque el componente `Communities / Rating` y arrástrela a su lugar en una página, como una posición relativa a la función para que los miembros la clasifiquen.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](rating-basics.md#essentials-for-client-side) están incluidos, así es como se `Rating` El componente aparecerá.

![clasificación](assets/rating.png)

## Configuración de clasificación {#configuring-rating}

Seleccione el colocado `Rating` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

En el **[!UICONTROL Textos y etiquetas]** para especificar el identificador interno de la clasificación.

![tallyname](assets/tallyname.png)

**[!UICONTROL Nombre de recuento]**
(*Requerido*) Un nombre sencillo para `Rating` que identifica de forma exclusiva esta instancia. Debe ser un nombre de nodo válido para el repositorio.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Miembros {#members}

Solo se permite una clasificación por miembro. El socio puede cambiar su calificación en cualquier momento.

### Anónimo {#anonymous}

No se admite la publicación anónima de una clasificación. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar.

## Información adicional {#additional-information}

Puede encontrar más información en la [Rating Essentials](rating-basics.md) para desarrolladores.
