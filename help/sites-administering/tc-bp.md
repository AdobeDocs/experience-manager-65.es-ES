---
title: Prácticas recomendadas de traducción
seo-title: Prácticas recomendadas de traducción
description: Encuentre las mejores prácticas recopiladas por los equipos de ingeniería y consultoría de Adobe para ayudarle a ponerse en marcha con los proyectos de traducción.
seo-description: Encuentre las mejores prácticas recopiladas por los equipos de ingeniería y consultoría de Adobe para ayudarle a ponerse en marcha con los proyectos de traducción.
uuid: 3bac1d73-9696-4c9b-8bdd-6f00fac40cf7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 1554010e-a1d1-4edf-b28f-9eead8f83b4a
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# Translation Best Practices{#translation-best-practices}

## General {#general}

Crear o expandir una presencia Web global puede ser un proceso complejo, pero con una buena previsión y planificación AEM puede simplificar sus esfuerzos y apoyar sus objetivos comerciales globales.

* **Planee la expansión** global antes de implementar el primer sitio. Adaptar un sitio existente para la cobertura global cuando se implementó el sitio con poco tiempo de preaviso generalmente es más difícil que planificar la expansión global al principio:

   * Evalúe el estado actual de la madurez de localización de su organización. Determine si dispone de **herramientas**, **procesos** y **recursos** para admitir la expansión global.
   * Tenga en cuenta las regulaciones **** globales y las preferencias **lingüísticas** regionales. Diseñe estructuras y procesos de contenido flexibles que puedan adaptarse a un entorno empresarial global cambiante.

* Determine un modelo de **gobernanza** que admita su negocio global y utilice mecanismos de AEM como MSM y permisos de usuario para aplicar el modelo que ha elegido. Por ejemplo, determine si el contenido se creará de forma centralizada y se &quot;insertará&quot; o &quot;extraerá&quot; a regiones o países. Determine qué contenido se puede desbloquear y modificar en las zonas geográficas. Determine quién es el responsable de iniciar y administrar las traducciones.
* Si los recursos lo permiten, lo mejor es administrar la actividad de traducción desde un equipo central que pueda desarrollar conocimientos en las herramientas, los procesos y las relaciones con los proveedores necesarios.
* **Planifique**, **cree prototipos** y **pruebe** su estructura y procesos globales para asegurarse de que admiten el negocio y de que cuenta con el apoyo necesario de los interesados en las áreas geográficas.

## Estructura del sitio    {#site-structure}

* Al diseñar la estructura del sitio, realice inicios examinando el contenido y determinando dónde y en qué idioma se crea el contenido. Esta ubicación debe ser el nivel superior del sitio.
* La práctica recomendada es una estructura **basada en** idiomas con no más de tres niveles entre los sitios de país y de creación de nivel superior.
* Utilice una convención de nombres de sitios de idioma o país que siga los estándares **** W3C.
* Determine cómo se distribuye el contenido por regiones y países. Considere qué países comparten idiomas. Se recomienda crear maestros de idiomas, una capa de páginas no activadas, donde el contenido traducido se puede revisar y modificar y luego enviar o llevar a un sitio de país que comparte ese idioma.
* Existen dos métodos para crear maestros de idiomas: uso de copias de idioma y uso de copias en vivo/MSM.

   * El método de copia de idioma es el que utiliza AEM marco de integración de traducción lista para usar, y por lo tanto es la manera más fácil de empezar. El marco proporciona una interfaz de usuario que facilita inicialmente la propagación y traducción de los cambios de contenido desde el maestro del idioma principal (por ejemplo, inglés) a los maestros del idioma. Sin embargo, a medida que el proyecto crece, la automatización del flujo de trabajo se hace cada vez más necesaria para administrar la traducción del mayor número de páginas o idiomas.
   * El enfoque de MSM/Live Copy puede ser una alternativa para casos de uso avanzados, donde los sitios son más grandes y complejos. El inicio necesita una buena gobernanza y automatización del flujo de trabajo para gestionar las complejas relaciones de herencia entre el inglés y los maestros del idioma, y reducir el riesgo de sobrescribir las traducciones existentes. Este manejo se puede realizar con la ayuda de algunos conectores de traducción. Consulte [MSM y sitios](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites) multilingües para obtener más información.

* Si el idioma principal tiene variaciones globales, una opción es utilizar MSM para crear una Live Copy desde el maestro global y utilizarla para la traducción. Por ejemplo, si la creación global se realiza en un maestro de inglés de EE.UU., cree un maestro de inglés internacional como una Live Copy y base para la traducción a otros idiomas.
* Utilice MSM para crear sitios de países a partir de los maestros de idiomas traducidos y para desplegar contenido en sitios que compartan el mismo idioma. Por ejemplo, el maestro de francés se puede distribuir a los sitios de Francia, Bélgica y Suiza.
* Planee, prototype y pruebe primero, antes de iniciar la implementación.

## Métodos y procesos de traducción {#translation-processes-and-methods}

* Participación de un proveedor de servicio de **localización (LSP)** con experiencia en traducción y actividades de localización relacionadas. Los LSP pueden ayudar a ampliar su negocio global proporcionando una amplia gama de recursos y tecnologías para mejorar la eficiencia y ahorrar costos de traducción:

   * Algunos proveedores de servicios locales son proveedores de servicios y tecnología. También hay proveedores de tecnología independientes que permiten que muchos proveedores de servicios locales participen en sus plataformas de traducción.
   * El **AEM Marco** de Traducción admite la integración con una variedad de proveedores de tecnología de traducción tanto para la traducción automática como para la humana.
   * Aprenda a [integrar los conectores LSP en su sistema](/help/sites-administering/translation.md) de AEM para automatizar la traducción de contenido, o a crear, exportar e importar manualmente proyectos de traducción para realizar pruebas y en los casos en que no haya ningún proveedor de tecnología LSP o de traducción.

* Elija un método **de** traducción que se adapte mejor al contenido.

   * **La traducción** humana es la mejor opción para el contenido en el que los mensajes y las expectativas de calidad son elevadas y el contenido se mantendrá durante algún tiempo en el sitio, como las páginas de marketing.
   * **La traducción** automática puede ser una buena opción para volúmenes masivos de traducción cuando el tiempo de publicación es crítico, las expectativas de calidad se relajan o los costos de traducción humana son prohibitivos. La base de conocimientos de soporte y el contenido generado por el usuario generalmente se traducen automáticamente.

* Confíe en la experiencia de los proveedores de servicio de localización, los asesores de Adobe y los integradores de sistemas para planificar, crear prototipos y probar la estructura multilingüe del sitio.

