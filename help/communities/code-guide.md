---
title: Directrices de codificación
description: Directrices, sugerencias y trucos para desarrolladores de Communities
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# Directrices de codificación {#coding-guidelines}

## Directrices, consejos y trucos {#guidelines-tips-and-tricks}

El trabajo con AEM Communities ha evolucionado desde depender en gran medida de las páginas de servidor Java hasta ser flexible en la elección de lenguajes de secuencias de comandos de plantilla en los que la lógica empresarial, el estilo y el contenido de la página son distintos entre sí.

Una mayor flexibilidad para trabajar con contenido generado por el usuario (UGC) es a través de la API de SocialResourceProvider, que elimina la necesidad de saber qué opción de [SRP](srp.md) se eligió para la implementación.

A continuación se indican varias directrices de codificación y prácticas recomendadas para los desarrolladores de AEM Communities:

### Código {#code}

* [Acceder a UGC con SRP](accessing-ugc-with-srp.md) - cómo evitar escribir una aplicación que solo funciona cuando UGC está almacenada en JCR (JSRP).
* [Refactorización de SocialUtils](socialutils.md): métodos de utilidad para SRP que reemplazan SocialUtils.
* [Convenciones de nomenclatura](naming-conventions.md): convenciones de nomenclatura para clases de Java personalizadas.

### Scripts {#scripts}

* [Descarga de componentes de comunidades](sideloading.md): cómo agregar dinámicamente un componente después de que se cargue la página.
* [Elementos esenciales del editor de texto enriquecido](rte.md): cómo personalizar la interfaz de usuario de texto enriquecido proporcionada a los miembros para publicar contenido.

### IDE {#ide}

* [Usar Maven para comunidades](maven.md) - cómo incluir el JAR de la API de comunidades.
* [Refactorización de SocialUtils](socialutils.md): métodos de utilidad para SRP que reemplazan SocialUtils.
