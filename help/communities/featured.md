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
* Ajustes de configuración para el componente `Featured Content`.

## Adición de contenido destacado a una página {#adding-featured-content-to-a-page}

Para agregar un componente `Featured Content` a una página en modo de autor, use el explorador de componentes para localizar

* `Communities / Featured Content`

Y arrástrelo a su lugar en una página donde debería aparecer el contenido destacado.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Cuando se incluyen las [bibliotecas requeridas del lado del cliente](essentials-featured.md#essentials-for-client-side), así es como aparece el componente `Featured Content`:

![contenido destacado](assets/featuredcontent.png)

## Configuración del contenido destacado {#configuring-featured-content}

Seleccione el componente `Featured Content` colocado para que pueda acceder y seleccionar el icono `Configure` que abre el cuadro de diálogo de edición.

![configurar-nuevo](assets/configure-new.png)

![contenido destacado1](assets/featuredcontent1.png)

### Pestaña Configuración {#settings-tab}

En la ficha **[!UICONTROL Configuración]**, identifique el contenido que se va a incluir:

* **[!UICONTROL Nombre para mostrar]**

  Título de la lista de contenido destacado. Por ejemplo, `Featured Questions` o `Featured Ideas`. El valor predeterminado es `Featured Content` si se deja vacío.

* **[!UICONTROL Ubicación del contenido destacado]**

  *(obligatorio)* Vaya a la página que contiene el contenido que puede aparecer en pantalla (los componentes de esa página deben configurarse para permitir contenido destacado). Por ejemplo, `/content/sites/engage/en/forum`.

* **[!UICONTROL Límite de visualización]**

  Número máximo de contenido destacado que se va a mostrar. El valor predeterminado es 5.

## Experiencia del visitante del sitio {#site-visitor-experience}

La capacidad de marcar contenido como contenido destacado requiere privilegios de moderador.

Cuando un moderador ve el contenido publicado, tiene acceso a las marcas de moderación en contexto, que incluyen la nueva marca `Feature`.

![experiencia-visitante-del-sitio](assets/site-visitor-experience.png)

Una vez que se haya marcado como característica, la marca de moderación se convierte en `Unfeature`.

La página que contiene el componente `Featured Content`, ahora incluye esta publicación.

![experiencia-visitante-del-sitio1](assets/site-visitor-experience1.png)

El `Read More` vincula a la publicación real.

## Información adicional {#additional-information}

Encontrará más información en la página [Contenido destacado](essentials-featured.md) para desarrolladores.

Para marcar contenido como destacado, consulte [Moderar contenido generado por el usuario](moderate-ugc.md).
