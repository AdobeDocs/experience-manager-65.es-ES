---
title: Uso de Me gusta
seo-title: Using Liking
description: Adición y configuración del componente "me gusta"
seo-description: Adding and configuring the Liking component
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 5%

---

# Uso de Me gusta {#using-liking}

El `Liking` El componente es una herramienta útil que permite a los usuarios expresar una opinión sobre un fragmento de contenido en particular, como un comentario dentro de un foro. Con el `Liking` componente, los miembros seleccionan el icono del corazón para indicar una opinión positiva.

## Agregar un me gusta a una página {#adding-liking-to-a-page}

Para agregar un `Liking` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Liking`

y arrástrela a su lugar en una página, como una posición relativa a la función que desee que tengan los usuarios.

Para obtener la información necesaria, visite [Conceptos básicos de componentes de comunidades](basics.md).

Si la variable [bibliotecas requeridas del lado del cliente](essentials-liking.md#essentials-for-client-side) están incluidos, así es como se `Liking` El componente aparecerá.

![componente de simpatía](assets/liking-component.png)

## Configuración de vínculos {#configuring-liking}

Seleccione el colocado `Liking` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

En el **[!UICONTROL Textos y etiquetas]** , especifique las propiedades utilizadas para registrar me gusta.

![de enlace de configuración](assets/configure-liking.png)

* **[!UICONTROL Etiqueta de respuesta positiva]**

   (*Requerido*) El nombre de la propiedad para una respuesta positiva.

* **[!UICONTROL Etiqueta de respuesta negativa]**

   (*Requerido*) El nombre de propiedad de una respuesta negativa.

* **[!UICONTROL Nombre de recuento]**

   (*Requerido*) El nombre de propiedad interno e identificable para esta instancia de un componente de voto.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Miembros {#members}

Los miembros pueden cambiar su Me gusta en cualquier momento.

### Anónimo {#anonymous}

No se admite el vínculo anónimo. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar en el me gusta.

## Información adicional {#additional-information}

Puede encontrar más información en la [Aspectos básicos](essentials-liking.md) para desarrolladores.
