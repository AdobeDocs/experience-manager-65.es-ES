---
title: Uso de Me gusta
description: Aprenda a añadir y configurar el componente "Me gusta" para que los usuarios puedan expresar su opinión sobre un contenido en particular, como un comentario.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Uso de Me gusta {#using-liking}

El componente `Liking` es una herramienta útil que permite a los usuarios expresar una opinión sobre un fragmento de contenido en particular, como un comentario dentro de un foro. Con el componente `Liking`, los miembros seleccionan el icono de corazón para indicar una opinión positiva.

## Agregar un me gusta a una página {#adding-liking-to-a-page}

Para agregar un componente `Liking` a una página en modo de autor, use el explorador de componentes para localizar

* `Communities / Liking`

Y arrástrela a su lugar en una página, como una posición relativa a la función que desee que tengan los usuarios.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Cuando se incluyen las [bibliotecas requeridas del cliente](essentials-liking.md#essentials-for-client-side), así es como aparece el componente `Liking`.

![componente de enlace](assets/liking-component.png)

## Configuración de vínculos {#configuring-liking}

Seleccione el componente `Liking` colocado para que pueda acceder y seleccionar el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar-nuevo](assets/configure-new.png)

En la ficha **[!UICONTROL Textos y etiquetas]**, especifique las propiedades utilizadas para registrar Me gusta.

![vínculo de configuración](assets/configure-liking.png)

* **[!UICONTROL Etiqueta de respuesta positiva]**

  (*Requerido*) El nombre de propiedad para una respuesta positiva.

* **[!UICONTROL Etiqueta de respuesta negativa]**

  (*Requerido*) El nombre de propiedad para una respuesta negativa.

* **[!UICONTROL Nombre de recuento]**

  (*Requerido*) El nombre de propiedad interno identificable para esta instancia de un componente de votación.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Miembros {#members}

Los miembros pueden cambiar de Me gusta en cualquier momento.

### Anónimo {#anonymous}

No se admite el vínculo anónimo. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar en el me gusta.

## Información adicional {#additional-information}

Encontrará más información en la página de [Like Essentials](essentials-liking.md) para desarrolladores.
