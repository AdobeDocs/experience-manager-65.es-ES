---
title: Prácticas recomendadas de traducción
seo-title: Prácticas recomendadas de traducción
description: Encuentre las prácticas recomendadas recopiladas por los equipos de consultoría e ingeniería de Adobe para ayudarle a poner en marcha proyectos de traducción.
seo-description: Encuentre las prácticas recomendadas recopiladas por los equipos de consultoría e ingeniería de Adobe para ayudarle a poner en marcha proyectos de traducción.
uuid: 3bac1d73-9696-4c9b-8bdd-6f00fac40cf7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 1554010e-a1d1-4edf-b28f-9eead8f83b4a
feature: Copiar idioma
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---


# Prácticas recomendadas de traducción{#translation-best-practices}

## General {#general}

La creación o ampliación de una presencia web global puede ser un proceso complejo, pero con una buena previsión y planificación AEM puede simplificar sus esfuerzos y apoyar sus objetivos comerciales globales.

* **Planifique la** expansión global antes de implementar el primer sitio. Adaptar un sitio existente para una cobertura global cuando el sitio se implementó con poco tiempo de antelación generalmente es más difícil que planificar la expansión global al principio:

   * Evalúe el estado actual de la madurez de localización de su organización. Determine si dispone de **herramientas**, **procesos** y **recursos** para admitir la expansión global.
   * Tenga en cuenta las **regulaciones globales** y **preferencias de idioma regional**. Diseñe estructuras y procesos de contenido flexibles que puedan adaptarse a un entorno comercial global cambiante.

* Determine un modelo de **gobernanza** que sea compatible con su negocio global y utilice mecanismos de AEM como MSM y permisos de usuario para aplicar el modelo elegido. Por ejemplo, determine si el contenido se creará de forma centralizada y si se &quot;insertará&quot; o &quot;extraerá&quot; a regiones o países. Determine qué contenido se puede desbloquear y modificar en las regiones geográficas. Determine quién es el responsable de iniciar y administrar las traducciones.
* Si los recursos lo permiten, es mejor administrar la actividad de traducción desde un equipo central que pueda desarrollar experiencia en las herramientas, los procesos y las relaciones con los proveedores necesarios.
* **Planifique**,  **** cree prototipos y  **** pruebe su estructura y procesos globales para asegurarse de que respalden el negocio y de que cuente con el apoyo necesario de las partes interesadas de la región.

## Estructura del sitio    {#site-structure}

* Al diseñar la estructura del sitio, comience por examinar el contenido y determinar dónde y en qué idioma se crea el contenido. Esta ubicación debe ser el nivel superior del sitio.
* La práctica recomendada es una **estructura basada en idiomas** con no más de 3 niveles entre los sitios de país y de creación de nivel superior.
* Utilice una convención de nomenclatura de sitios de idioma/país que siga los **estándares W3C**.
* Determine cómo se distribuye el contenido por regiones y países. Consideremos qué países comparten idiomas. Se recomienda crear maestros de idiomas, una capa de páginas no activadas, donde el contenido traducido puede revisarse y modificarse, luego ser transferido o llevado a un sitio de un país que comparte ese idioma.
* Existen dos métodos para crear maestros de idiomas: uso de copias de idioma y uso de MSM/Live Copies.

   * El enfoque de copia de idioma es el que utiliza AEM marco de integración de traducción predeterminado y, por lo tanto, es la forma más sencilla de empezar. El marco de trabajo proporciona una interfaz de usuario que facilita inicialmente la propagación y traducción de los cambios de contenido del maestro del idioma principal (p. ej. inglés) a los maestros del idioma. Sin embargo, a medida que el proyecto crece, la automatización del flujo de trabajo se hace cada vez más necesaria para administrar la traducción del mayor número de páginas o idiomas.
   * El método MSM/Live Copy puede ser una alternativa para casos de uso avanzados, donde los sitios son más grandes y complejos. Es necesario contar con un buen gobierno y una automatización del flujo de trabajo desde el principio para gestionar las complejas relaciones de herencia entre los maestros del inglés y del idioma, así como para reducir el riesgo de sobrescribir las traducciones existentes. Este manejo se puede realizar con la ayuda de algunos conectores de traducción. Consulte [MSM y sitios multilingües](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites) para obtener más información.

* Si el idioma principal tiene variaciones globales, una opción es usar MSM para crear una Live Copy del maestro global y utilizarla para la traducción. Por ejemplo, si la creación global se realiza en un maestro de inglés de EE. UU., cree un maestro de inglés internacional como Live Copy y base para la traducción a otros idiomas.
* Utilice MSM para crear sitios de país a partir de los maestros de idiomas traducidos y para desplegar contenido en sitios que compartan el mismo idioma. Por ejemplo, el maestro de francés se puede implantar en los sitios de Francia, Bélgica y Suiza.
* Planifique, cree prototipos y pruebe primero antes de iniciar la implementación.

## Procesos y métodos de traducción {#translation-processes-and-methods}

* Participe en un **proveedor de servicios de localización (LSP)** con experiencia en traducción y actividades de localización relacionadas. Los LSP pueden ayudar a escalar su negocio global al proporcionar una amplia gama de recursos y tecnologías para mejorar la eficiencia y ahorrar costos de traducción:

   * Algunos LSP son proveedores de servicios y tecnología. También hay proveedores independientes de tecnología que permiten a muchos LSP participar en sus plataformas de traducción.
   * El **AEM Translation Framework** admite la integración con una variedad de proveedores de tecnología de traducción tanto para la traducción automática como para la humana.
   * Aprenda a [integrar conectores LSP en su sistema AEM](/help/sites-administering/translation.md) para automatizar la traducción de contenido, o a crear, exportar e importar manualmente proyectos de traducción para probarlos y en casos en los que no haya ningún proveedor de tecnología de traducción o LSP.

* Elija un **método de traducción** que se adapte mejor al contenido.

   * **La** traducción humana es la más adecuada para el contenido en el que la mensajería y las expectativas de calidad son altas y el contenido estará activo durante algún tiempo en el sitio, como las páginas de marketing.
   * **La** traducción automática puede ser una buena elección para volúmenes masivos de traducción cuando el tiempo de publicación es crítico, las expectativas de calidad se relajan o los costos de traducción humana son prohibitivos. La base de conocimientos de soporte y el contenido generado por el usuario suelen traducirse automáticamente.

* Confíe en la experiencia de los proveedores de servicios de localización, los asesores de Adobe y los integradores de sistemas para planificar, crear prototipos y probar la estructura multilingüe de su sitio.

