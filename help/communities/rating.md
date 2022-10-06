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

La variable `Rating` se utiliza de forma independiente o junto con otras funciones de Communities. Este componente permite a los miembros de la comunidad que han iniciado sesión expresar sus opiniones clasificando el contenido.

## Adición de una clasificación a una página {#adding-a-rating-to-a-page}

Para agregar un `Rating` a una página en modo de autor, busque el componente `Communities / Rating` y arrástrela a su lugar en una página, como una posición relativa a la función que deben clasificar los miembros.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de Communities](basics.md).

Cuando la variable [bibliotecas requeridas del lado del cliente](rating-basics.md#essentials-for-client-side) se incluyen, así es como se muestra la variable `Rating` aparecerá el componente.

![clasificación](assets/rating.png)

## Configuración de la clasificación {#configuring-rating}

Seleccione la colocación `Rating` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

En el **[!UICONTROL Textos y etiquetas]** especifique el identificador interno de la clasificación.

![nombre_talyname](assets/tallyname.png)

**[!UICONTROL Nombre Tally]**
(*Requerido*) Un nombre sencillo para el `Rating` que identifica de forma exclusiva esta instancia. Debe ser un nombre de nodo válido para el repositorio.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Miembros {#members}

Solo se permite una clasificación por miembro. El miembro podrá cambiar su calificación en cualquier momento.

### Anónimo {#anonymous}

No se admite la publicación anónima de una clasificación. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar.

## Información adicional {#additional-information}

Puede encontrar más información en la [Aspectos básicos de la clasificación](rating-basics.md) para desarrolladores.
