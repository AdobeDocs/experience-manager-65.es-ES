---
title: Función de contenido destacado
seo-title: Función de contenido destacado
description: La función Contenido destacado permite que los visitantes del sitio con sesión resalten el contenido
seo-description: La función Contenido destacado permite que los visitantes del sitio con sesión resalten el contenido
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
translation-type: tm+mt
source-git-commit: a8b1ad0fcd2ca9c7fe3117dd8bd161da82d13e8a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 5%

---


# Función de contenido destacado {#featured-content-feature}

## Introducción {#introduction}

La función de contenido destacado proporciona un área para los visitantes del sitio con sesión iniciada (miembros de la comunidad) en el entorno de publicación para resaltar contenido para:

* [Blogs](blog-feature.md)
* [Calendarios](calendar.md)
* [Foros](forum.md)
* [Ideas](ideation-feature.md)
* [P y R](working-with-qna.md)

Una vez que el contenido se marque como destacado, se enumerará dentro de este componente, que puede colocarse en páginas de aterrizaje específicas o áreas que captan fácilmente la atención de los miembros de la comunidad.

La capacidad de presentar contenido puede estar permitida o no permitida por componente.

Esta sección de la documentación describe:

* Añadir contenido destacado en un sitio de comunidad.
* Configuración del componente `Featured Content`.

## Añadir contenido destacado en una página {#adding-featured-content-to-a-page}

Para agregar un componente `Featured Content` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Featured Content`

y arrástrelo a su lugar en una página donde debería aparecer el contenido destacado.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de comunidades](basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](essentials-featured.md#essentials-for-client-side), así es como aparecerá el componente `Featured Content`:

![contenido de funciones](assets/featuredcontent.png)

## Configuración del contenido destacado {#configuring-featured-content}

Seleccione el componente `Featured Content` colocado para acceder y seleccione el icono `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

![feature content1](assets/featuredcontent1.png)

### Ficha Configuración {#settings-tab}

En la ficha **[!UICONTROL Configuración]**, identifique el contenido para la función:

* **[!UICONTROL Nombre para mostrar]**

   Título para la lista del contenido destacado. Por ejemplo, `Featured Questions` o `Featured Ideas`. El valor predeterminado es `Featured Content` si se deja vacío.

* **[!UICONTROL Ubicación del contenido destacado]**

   *(Requerido)* Navegue hasta la página que contenga el contenido que puede ser una característica (los componentes de esa página deben configurarse para permitir contenido destacado). Por ejemplo, `/content/sites/engage/en/forum`.

* **[!UICONTROL Límite de visualización]**

   El número máximo de contenido destacado que se va a mostrar. El valor predeterminado es 5.

## Experiencia de Visitante del sitio {#site-visitor-experience}

La capacidad de marcar el contenido como contenido destacado requiere privilegios de moderador.

Cuando un moderador vista el contenido publicado, tiene acceso a los indicadores de moderación en contexto, que incluyen el nuevo indicador `Feature`.

![site-visitante-experience](assets/site-visitor-experience.png)

Una vez marcada como característica, el indicador de modelación se convierte en `Unfeature`.

La página que contiene el componente `Featured Content` incluirá ahora esta publicación.

![site-visitante-experience1](assets/site-visitor-experience1.png)

`Read More` es un vínculo al anuncio real.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Contenido destacado](essentials-featured.md) para desarrolladores.

Para marcar el contenido como destacado, consulte [Moderación del contenido generado por el usuario](moderate-ugc.md).
