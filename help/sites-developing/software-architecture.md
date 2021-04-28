---
title: Arquitectura de software
seo-title: Arquitectura de software
description: Prácticas recomendadas para diseñar el software
seo-description: Prácticas recomendadas para diseñar el software
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
translation-type: tm+mt
source-git-commit: 423e17dadf2e506eb68b37851dde5e68ed950866
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Arquitectura de software{#software-architecture}

## Diseño para actualizaciones {#design-for-upgrades}

Al ampliar los comportamientos de OOTB, es importante tener en cuenta las actualizaciones. Siempre aplique personalizaciones en el directorio /apps y superponga los nodos correspondientes en el directorio /libs o utilice sling:resourceSuperType para extender el comportamiento predeterminado. Aunque pueden ser necesarias algunas modificaciones para admitir una nueva versión de AEM, la nueva versión no debe sobrescribir las personalizaciones si se sigue esta práctica.

### Reutilizar plantillas y componentes cuando sea posible {#reuse-template-and-components-when-possible}

Esto permitirá que el sitio mantenga una apariencia más coherente y simplifique el mantenimiento del código. Cuando se necesite una nueva plantilla, asegúrese de extenderse desde una plantilla base compartida para que los requisitos globales, como la inclusión clientlib, se puedan codificar en un solo lugar. Cuando se necesita un componente nuevo, busque oportunidades para ampliar desde un componente existente.

### Diseño de diseños de plantilla {#design-template-designs}

Al definir qué componentes se pueden incluir en cada parsys de la página, se puede controlar la coherencia de la apariencia del sitio. Al restringir el acceso al diseño en las páginas, se puede permitir que los &quot;superautores&quot; modifiquen los componentes permitidos por página sin intervención del desarrollador, mientras que los demás autores se aseguran de que siguen los estándares corporativos.

### Desarrollar una arquitectura SOLID {#develop-a-solid-architecture}

SOLID es un acrónimo que describe cinco principios arquitectónicos que deben ser respetados:

* **** Principio de responsabilidad única: cada módulo, clase, método, etc. solo debe tener una responsabilidad.
* **** Principio abierto/cerrado: los módulos deben abrirse para su extensión y cerrarse para su modificación.
* **** Principio de sustitución de Liskov: los tipos deben reemplazarse por sus subtipos.
* **** Principio de segmentación de interfaz: ningún cliente debe estar obligado a depender de métodos que no utilice.
* **** Principio de inversión de dependencia: los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deberían depender de las abstracciones. Las abstracciones no deben depender de los detalles. Los detalles deben depender de las abstracciones.

La lucha por el cumplimiento de estos cinco principios debería dar lugar a un sistema que tenga una estricta separación de preocupaciones.

>[!TIP]
>
>SOLID es un concepto comúnmente utilizado en la programación orientada a objetos y cada elemento es ampliamente discutido en la bibliografía del sector.
>
>Este es solo un breve resumen presentado para la sensibilización y se le recomienda familiarizarse con estos conceptos en mayor profundidad.

### Siga el Principio de solidez {#follow-the-robustness-principle}

El principio de la solidez dice que deberíamos ser conservadores en lo que enviamos, pero liberales en lo que aceptamos. En otras palabras, al enviar mensajes a un tercero, debemos cumplir todas las especificaciones, pero al recibir mensajes de un tercero, debemos aceptar mensajes no conformes siempre y cuando el significado del mensaje sea claro.

### Implementar picos en sus propios módulos {#implement-spikes-in-their-own-modules}

Los picos y el código de prueba son una parte integral de cualquier implementación de software de Agile, pero queremos asegurarnos de que no entren en nuestra base de código de producción sin el nivel apropiado de supervisión. Como resultado, se recomienda crear picos en su propio módulo.

### Implementar scripts de migración de datos en su propio módulo {#implement-data-migration-scripts-in-their-own-module}

Los scripts de migración de datos, mientras que el código de producción, generalmente se ejecutan una sola vez al inicio inicial de un sitio. Por lo tanto, tan pronto como el sitio está activo, se convierte en código muerto. Para garantizar que no generemos código de implementación que dependa de los scripts de migración, estos deben implementarse en su propio módulo. Esto también nos permite eliminar y retirar este código inmediatamente después del lanzamiento, eliminando el código muerto del sistema.

### Siga las convenciones publicadas de Maven en los archivos POM {#follow-published-maven-conventions-in-pom-files}

Apache ha publicado convenciones de estilo en [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). Es mejor seguir estas convenciones, ya que facilitará que los nuevos recursos lleguen rápidamente.
