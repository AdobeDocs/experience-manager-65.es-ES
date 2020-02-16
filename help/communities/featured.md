---
title: Función de contenido destacado
seo-title: Función de contenido destacado
description: La función Contenido destacado permite a los visitantes del sitio con sesión iniciada resaltar el contenido
seo-description: La función Contenido destacado permite a los visitantes del sitio con sesión iniciada resaltar el contenido
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Función de contenido destacado {#featured-content-feature}

## Introducción {#introduction}

La función de contenido destacado proporciona un área para que los visitantes del sitio que han iniciado sesión (miembros de la comunidad) en el entorno de publicación resalten el contenido para

* [Blogs](blog-feature.md)
* [Calendarios](calendar.md)
* [Foros](forum.md)
* [Ideas](ideation-feature.md)
* [P y R](working-with-qna.md)

Una vez que el contenido se marca como destacado, se enumerará dentro de este componente, que puede colocarse en páginas de aterrizaje específicas o en áreas que captan fácilmente la atención de los miembros de la comunidad.

La capacidad de presentar contenido puede estar permitida o no permitida por componente.

Esta sección de la documentación describe

* Adición de contenido destacado a un sitio de comunidad
* Configuración del `Featured Content`componente

## Adición de contenido destacado a una página {#adding-featured-content-to-a-page}

Para agregar un `Featured Content` componente a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Featured Content`

y arrástrelo a su lugar en una página donde debería aparecer el contenido destacado.

Para obtener la información necesaria, visite [Communities Components Basics](basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [del lado del cliente](essentials-featured.md#essentials-for-client-side) necesarias, así es como aparecerá el `Featured Content`componente:

![chlimage_1-13](assets/chlimage_1-13.png)

## Configuración del contenido destacado {#configuring-featured-content}

Seleccione el componente colocado al que desea acceder y seleccione el `Featured Content` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-14](assets/chlimage_1-14.png) ![chlimage_1-15](assets/chlimage_1-15.png)

### Ficha Configuración {#settings-tab}

En la ficha **[!UICONTROL Configuración]** , identifique el contenido para la función:

* **[!UICONTROL Nombre para mostrar]** El título de la lista de contenido destacado. Por ejemplo `Featured Questions` o `Featured Ideas`. El valor predeterminado es `Featured Content` si se deja vacío.

* **[!UICONTROL Ubicación del contenido destacado]**
   *(Requerido)* Vaya a la página que contenga el contenido que puede ser una característica (los componentes de esa página deben configurarse para permitir contenido destacado). Por ejemplo, `/content/sites/engage/en/forum`

* **[!UICONTROL Límite]** de visualización El número máximo de contenido destacado que se va a mostrar. El valor predeterminado es 5.

## Experiencia del visitante del sitio {#site-visitor-experience}

La capacidad de marcar el contenido como contenido destacado requiere privilegios de moderador.

Cuando un moderador visualiza contenido publicado, tiene acceso a los indicadores de moderación en contexto, que incluyen el nuevo `Feature` indicador.

![chlimage_1-16](assets/chlimage_1-16.png)

Una vez marcada como característica, el indicador de moderación se convierte en `Unfeature`.

La página que contiene el `Featured Content` componente incluirá ahora esta publicación.

![chlimage_1-17](assets/chlimage_1-17.png)

`Read More` es un vínculo al anuncio real.

## Información adicional {#additional-information}

Puede encontrar más información en la página [Contenido](essentials-featured.md) destacado para desarrolladores.

Para marcar el contenido como destacado, consulte [Moderación del contenido](moderate-ugc.md)generado por el usuario.
