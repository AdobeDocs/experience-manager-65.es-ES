---
title: Uso de "Me gusta"
seo-title: Using Liking
description: Adición y configuración del componente "Me gusta"
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

# Uso de &quot;Me gusta&quot; {#using-liking}

La variable `Liking` es una herramienta útil que permite a los usuarios expresar una opinión sobre un contenido determinado, como un comentario dentro de un foro. Con la variable `Liking` , los miembros seleccionan el icono del corazón para indicar una opinión positiva.

## Adición de &quot;Me gusta&quot; a una página {#adding-liking-to-a-page}

Para agregar un `Liking` a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Liking`

y arrástrela a su lugar en una página, por ejemplo, una posición relativa a la función que desee para los usuarios.

Para obtener la información necesaria, visite [Conceptos básicos de los componentes de Communities](basics.md).

Cuando la variable [bibliotecas requeridas del lado del cliente](essentials-liking.md#essentials-for-client-side) se incluyen, así es como se muestra la variable `Liking` aparecerá el componente.

![componente de &quot;Me gusta&quot;](assets/liking-component.png)

## Configuración de &quot;Me gusta&quot; {#configuring-liking}

Seleccione la colocación `Liking` para acceder y seleccionar el componente `Configure` que abre el cuadro de diálogo de edición.

![configure-new](assets/configure-new.png)

En el **[!UICONTROL Textos y etiquetas]** especifique las propiedades utilizadas para registrar &quot;Me gusta&quot;.

![configure-link](assets/configure-liking.png)

* **[!UICONTROL Etiqueta de respuesta positiva]**

   (*Requerido*) El nombre de propiedad para una respuesta positiva.

* **[!UICONTROL Etiqueta de respuesta negativa]**

   (*Requerido*) El nombre de la propiedad para una respuesta negativa.

* **[!UICONTROL Nombre de recuento]**

   (*Requerido*) El nombre de propiedad interno identificable para esta instancia de un componente de votación.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Miembros {#members}

Los miembros podrán cambiar de forma similar en cualquier momento.

### Anónimo {#anonymous}

No se admite &quot;Me gusta&quot; anónimo. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar en el &quot;Me gusta&quot;.

## Información adicional {#additional-information}

Puede encontrar más información en la [&quot;Me gusta&quot; de Essentials](essentials-liking.md) para desarrolladores.
