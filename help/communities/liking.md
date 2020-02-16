---
title: Uso de "Me gusta"
seo-title: Uso de "Me gusta"
description: Adición y configuración del componente "Me gusta"
seo-description: Adición y configuración del componente "Me gusta"
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Uso de &quot;Me gusta&quot; {#using-liking}

El `Liking`componente es una herramienta útil que permite a los usuarios expresar una opinión sobre un contenido determinado, como un comentario dentro de un foro. Con el `Liking`componente, los miembros seleccionan el icono del corazón para indicar una opinión positiva.

## Adición de &quot;Me gusta&quot; a una página {#adding-liking-to-a-page}

Para agregar un `Liking` componente a una página en modo de autor, utilice el navegador de componentes para localizar

* `Communities / Liking`

y arrástrelo a su lugar en una página, como una posición relativa a la función que los usuarios deseen.

Para obtener la información necesaria, visite [Communities Components Basics](basics.md)(Conceptos básicos de componentes de comunidades).

Cuando se incluyen las bibliotecas [](essentials-liking.md#essentials-for-client-side) requeridas del lado del cliente, así es como aparecerá el `Liking` componente.

![chlimage_1-93](assets/chlimage_1-93.png)

## Configuración de &quot;Me gusta&quot; {#configuring-liking}

Seleccione el componente colocado al que desea acceder y seleccione el `Liking` `Configure` icono que abre el cuadro de diálogo de edición.

![chlimage_1-94](assets/chlimage_1-94.png)

En la ficha **[!UICONTROL Textos y etiquetas]** , especifique las propiedades utilizadas para registrar &quot;Me gusta&quot;.

![chlimage_1-95](assets/chlimage_1-95.png)

* **[!UICONTROL Etiqueta]** de respuesta positiva (*obligatoria*) El nombre de la propiedad para una respuesta positiva.

* **[!UICONTROL Etiqueta]** de respuesta negativa (*obligatoria*) El nombre de la propiedad para una respuesta negativa.

* **[!UICONTROL Tally Name]**(*Requerido*) El nombre de propiedad interno identificable para esta instancia de un componente de votación.

## Experiencia del visitante del sitio {#site-visitor-experience}

### Miembros {#members}

Los Miembros pueden cambiar su estilo en cualquier momento.

### Anónimo {#anonymous}

No se admite el &quot;Me gusta&quot; anónimo. Los visitantes del sitio deben registrarse (convertirse en miembros) e iniciar sesión para participar en el &quot;Me gusta&quot;.

## Información adicional {#additional-information}

Puede encontrar más información en la página [&quot;Me gusta&quot; de los desarrolladores](essentials-liking.md) .
