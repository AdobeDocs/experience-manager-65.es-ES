---
title: Uso de clasificaciones
description: Aprenda a añadir un componente Clasificación a una página que permita a los miembros de la comunidad que han iniciado sesión expresar sus opiniones clasificando el contenido.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 1%

---

# Uso de clasificaciones {#using-ratings}

El componente `Rating` se usa de forma independiente o con otras características de Communities. Este componente permite a los miembros de la comunidad que iniciaron sesión expresar sus opiniones mediante la clasificación de contenido.

## Añadir una clasificación a una página {#adding-a-rating-to-a-page}

Para agregar un componente `Rating` a una página en modo de autor, busque el componente `Communities / Rating` y arrástrelo a su lugar en una página, por ejemplo, una posición relativa a la característica para que los miembros la clasifiquen.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Cuando se incluyen las [bibliotecas requeridas del cliente](rating-basics.md#essentials-for-client-side), así es como aparece el componente `Rating`.

![clasificación](assets/rating.png)

## Configuración de clasificación {#configuring-rating}

Seleccione el componente `Rating` colocado para que pueda acceder y seleccionar el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar-nuevo](assets/configure-new.png)

En la ficha **[!UICONTROL Textos y etiquetas]**, especifique el identificador interno de la clasificación.

![nombreDeRegistro](assets/tallyname.png)

**[!UICONTROL Nombre de recuento]**
(*Obligatorio*) Un nombre simple para `Rating` que identifica de forma exclusiva esta instancia. Debe ser un nombre de nodo válido para el repositorio.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Miembros {#members}

Solo se permite una clasificación por miembro. El socio puede cambiar su calificación en cualquier momento.

### Anónimo {#anonymous}

No se admite la publicación anónima de una clasificación. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar.

## Información adicional {#additional-information}

Encontrará más información en la página [Elementos esenciales de clasificación](rating-basics.md) para desarrolladores.
