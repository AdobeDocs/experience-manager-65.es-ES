---
title: Función Contenido destacado
description: La función Contenido destacado permite a los visitantes del sitio conectados resaltar contenido
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# Función Contenido destacado {#featured-content-feature}

## Introducción {#introduction}

La función de contenido destacado proporciona un área para que los visitantes del sitio (miembros de la comunidad) que han iniciado sesión en el entorno de publicación destaquen contenido para:

* [Blogs](blog-feature.md)
* [Calendarios](calendar.md)
* [Foros](forum.md)
* [Ideas](ideation-feature.md)
* [P y R](working-with-qna.md)

Una vez que el contenido se marca como destacado, se enumera dentro de este componente, que puede colocarse en páginas de aterrizaje específicas o áreas que capten fácilmente la atención de los miembros de la comunidad.

Se puede permitir o no la capacidad de incluir contenido por componente.

Esta sección de la documentación describe lo siguiente:

* Añadir contenido destacado a un sitio de la comunidad.
* Ajustes de configuración para `Featured Content` componente.

## Adición de contenido destacado a una página {#adding-featured-content-to-a-page}

Para agregar un `Featured Content` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Featured Content`

Y arrástrelo a su lugar en una página donde debería aparecer el contenido destacado.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](essentials-featured.md#essentials-for-client-side) están incluidos, así es como se `Featured Content` el componente aparece:

![contenido destacado](assets/featuredcontent.png)

## Configuración del contenido destacado {#configuring-featured-content}

Seleccione el colocado `Featured Content` para que pueda acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

![contenido destacado1](assets/featuredcontent1.png)

### Pestaña Configuración {#settings-tab}

En el **[!UICONTROL Configuración]** pestaña, identifique el contenido que se va a mostrar:

* **[!UICONTROL Nombre para mostrar]**

  Título de la lista de contenido destacado. Por ejemplo, `Featured Questions` o `Featured Ideas`. El valor predeterminado es `Featured Content` si se deja vacío.

* **[!UICONTROL Ubicación del contenido destacado]**

  *(Obligatorio)* Vaya a la página que contiene el contenido que se puede mostrar (los componentes de esa página deben configurarse para Permitir contenido destacado). Por ejemplo, `/content/sites/engage/en/forum`.

* **[!UICONTROL Límite de visualización]**

  Número máximo de contenido destacado que se va a mostrar. El valor predeterminado es 5.

## Experiencia del visitante del sitio {#site-visitor-experience}

La capacidad de marcar contenido como contenido destacado requiere privilegios de moderador.

Cuando un moderador ve el contenido publicado, tiene acceso a las marcas de moderación en contexto, que incluyen la nueva `Feature` Indicador.

![site-visitor-experience](assets/site-visitor-experience.png)

Una vez marcada como característica, la marca de moderación pasa a llamarse `Unfeature`.

La página que contiene el `Featured Content` componente, ahora incluye esta publicación.

![site-visitor-experience1](assets/site-visitor-experience1.png)

El `Read More` vínculos a la publicación real.

## Información adicional {#additional-information}

Puede encontrar más información en la [Contenido destacado](essentials-featured.md) para desarrolladores.

Para marcar el contenido como destacado, consulte [Moderación del contenido generado por el usuario](moderate-ugc.md).
