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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# Arquitectura de software{#software-architecture}

## Diseño para actualizaciones {#design-for-upgrades}

Al ampliar los comportamientos de la OOTB, es importante tener en cuenta las actualizaciones. Siempre aplique personalizaciones en el directorio /apps y superponga los nodos correspondientes en el directorio /libs o utilice sling:resourceSuperType para extender el comportamiento de fuera del cuadro. Aunque se necesitan algunas modificaciones para admitir una nueva versión de AEM, la nueva versión no debe sobrescribir las personalizaciones si se sigue esta práctica.

### Volver a utilizar plantillas y componentes cuando sea posible {#reuse-template-and-components-when-possible}

Esto permitirá que el sitio mantenga un aspecto y presentación más coherentes y simplifique el mantenimiento del código. Cuando se necesite una nueva plantilla, asegúrese de extenderse desde una plantilla base compartida para que los requisitos globales, como la inclusión de clientlib, se puedan codificar en un solo lugar. Cuando se necesita un nuevo componente, busque oportunidades para ampliar desde un componente existente.

### Diseñar diseños de plantilla {#design-template-designs}

Al definir qué componentes se pueden incluir en cada parsys de la página, se puede controlar la coherencia del aspecto del sitio. Al restringir el acceso al diseño en las páginas, se puede permitir que los &quot;superautores&quot; modifiquen los componentes permitidos por página sin la intervención del desarrollador, al mismo tiempo que se garantiza que los demás autores sigan los estándares corporativos.

### Desarrollar una arquitectura SOLID {#develop-a-solid-architecture}

SOLID es un acrónimo que describe cinco principios arquitectónicos que deben ser respetados:

* **Principio de responsabilidad**&#x200B;única: cada módulo, clase, método, etc. debe hacer una sola cosa.
* **Principio** abierto/cerrado: los módulos deben estar abiertos a la extensión y cerrados para su modificación.
* **Principio de sustitución de** Liskov: los tipos deberían reemplazarse por sus subtipos.
* **Principio** de segmentación de interfaz: ningún cliente debe verse obligado a depender de métodos que no utilice.
* **Principio de inversión en** dependencia: los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de las abstracciones. Las abstracciones no deben depender de los detalles. Los detalles deben depender de las abstracciones.

La lucha por el cumplimiento de estos cinco principios debería dar lugar a un sistema que tenga una estricta separación de preocupaciones.

### Siga el principio de solidez {#follow-the-robustness-principle}

El Principio de la Solidez establece que deberíamos ser conservadores en lo que enviamos, pero ser liberales en lo que aceptamos. En otras palabras, al enviar mensajes a un tercero, debemos cumplir completamente con las especificaciones, pero al recibir mensajes de un tercero, debemos aceptar mensajes no conformes siempre y cuando el significado del mensaje sea claro.

### Implementar picos en sus propios módulos {#implement-spikes-in-their-own-modules}

Los picos y el código de prueba son una parte integral de cualquier implementación de software ágil, pero queremos asegurarnos de que no entren en nuestra base de código de producción sin el nivel adecuado de supervisión. Como resultado, se recomienda crear picos en su propio módulo.

### Implementar secuencias de comandos de migración de datos en su propio módulo {#implement-data-migration-scripts-in-their-own-module}

Las secuencias de comandos de migración de datos, mientras que el código de producción, generalmente se ejecutan una sola vez en el inicio inicial de un sitio. Por lo tanto, tan pronto como el sitio está activo, esto se convierte en código muerto. Para garantizar que no generemos código de implementación que dependa de las secuencias de comandos de migración, deben implementarse en su propio módulo. Esto también nos permite eliminar y retirar este código inmediatamente después del lanzamiento, eliminando el código muerto del sistema.

### Siga las convenciones de Maven publicadas en los archivos POM {#follow-published-maven-conventions-in-pom-files}

Apache ha publicado convenciones de estilo en [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). Lo mejor es seguir estas convenciones, ya que será más fácil que los nuevos recursos lleguen rápidamente.
