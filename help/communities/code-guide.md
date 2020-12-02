---
title: Directrices de codificación
seo-title: Directrices de codificación
description: Directrices, consejos y trucos para desarrolladores de comunidades
seo-description: Directrices, consejos y trucos para desarrolladores de comunidades
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# Directrices de codificación {#coding-guidelines}

## Pautas, consejos y trucos {#guidelines-tips-and-tricks}

El trabajo con AEM Communities ha pasado de depender en gran medida de las páginas de servidor Java a la flexibilidad en la elección de los lenguajes de secuencias de comandos de plantilla en los que la lógica empresarial, el estilo y el contenido de la página son distintos entre sí.

La mayor flexibilidad en el trabajo con contenido generado por el usuario (UGC, por sus siglas en inglés) se obtiene a través de la API de SocialResourceProvider, que elimina la necesidad de saber qué opción [SRP](srp.md) se eligió para la implementación.

A continuación se indican varias directrices de codificación y prácticas recomendadas para desarrolladores de AEM Communities:

### Código {#code}

* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) : cómo evitar la escritura de una aplicación que solo funciona cuando UGC se almacena en JCR (JSRP).
* [SocialUtils Refactoring](socialutils.md) : métodos de utilidad para SRP que reemplazan a SocialUtils.
* [Convenciones](naming-conventions.md)  de nomenclatura: convenciones de nomenclatura para clases de Java personalizadas.

### Secuencias de comandos {#scripts}

* [Cargar componentes](sideloading.md)  de comunidades: cómo agregar un componente de forma dinámica después de que se cargue la página.
* [Elementos esenciales](rte.md)  del editor de texto enriquecido: cómo personalizar la interfaz de usuario de texto enriquecido proporcionada a los miembros para publicar contenido.

### IDE {#ide}

* [Uso de Maven para Comunidades](maven.md) : cómo incluir el jar de API de Comunidades.
* [SocialUtils Refactoring](socialutils.md) : métodos de utilidad para SRP que reemplazan a SocialUtils.

