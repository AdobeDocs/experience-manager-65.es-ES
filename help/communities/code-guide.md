---
title: Directrices de programación
description: Directrices, sugerencias y trucos para desarrolladores de Communities
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 3%
---
# Directrices de programación {#coding-guidelines}

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
