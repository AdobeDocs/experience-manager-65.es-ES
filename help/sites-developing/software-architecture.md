---
title: Arquitectura de software
seo-title: Software Architecture
description: Prácticas recomendadas para crear el software
seo-description: Best practices for architecting your software
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Arquitectura de software{#software-architecture}

## Diseño para actualizaciones {#design-for-upgrades}

Al ampliar los comportamientos de OOTB, es importante tener en cuenta las actualizaciones. Aplique siempre las personalizaciones en el directorio /apps y superponga los nodos correspondientes en el directorio /libs o utilice sling:resourceSuperType para ampliar el comportamiento predeterminado. AEM Aunque es posible que se necesiten algunas modificaciones para admitir una nueva versión de, la nueva versión no debe sobrescribir las personalizaciones si se sigue esta práctica.

### Reutilizar plantillas y componentes siempre que sea posible {#reuse-template-and-components-when-possible}

Esto permitirá que el sitio mantenga una apariencia más coherente y simplifique el mantenimiento del código. Cuando se necesite una plantilla nueva, asegúrese de ampliarla desde una plantilla base compartida para que los requisitos globales, como la inclusión clientlib, se puedan codificar en un solo lugar. Cuando se necesite un nuevo componente, busque oportunidades para ampliarse desde un componente existente.

### Diseñar diseños de plantilla {#design-template-designs}

Al definir qué componentes se pueden incluir en cada parsys de la página, se puede controlar la coherencia de la apariencia del sitio. Al restringir el acceso al diseño en las páginas, se puede permitir a los &quot;superautores&quot; modificar los componentes permitidos por página sin la intervención del desarrollador, siempre que los demás autores sigan los estándares corporativos.

### Desarrollar una arquitectura sólida {#develop-a-solid-architecture}

SOLID es un acrónimo que describe cinco principios arquitectónicos a los que hay que adherirse:

* **S** Principio de responsabilidad único: cada módulo, clase, método, etc., solo debe tener una responsabilidad.
* **O** Principio abierto/Cerrado: los módulos deben estar abiertos para su extensión y cerrados para su modificación.
* **L** Principio de sustitución de iskov: los tipos deben ser reemplazables por sus subtipos.
* **I** Principio de segregación de interfaz: no se debe obligar a ningún cliente a depender de métodos que no utiliza.
* **D** Principio de inversión de dependencia: los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambas deberían depender de abstracciones. Las abstracciones no deben depender de los detalles. Los detalles deben depender de las abstracciones.

La lucha por el cumplimiento de estos cinco principios debería dar como resultado un sistema que tenga una estricta separación de intereses.

>[!TIP]
>
>SOLID es un concepto comúnmente utilizado en la programación orientada a objetos y cada elemento es ampliamente discutido en la literatura de la industria.
>
>Este es solo un breve resumen presentado para la concienciación y se le anima a que se familiarice con estos conceptos en más profundidad.

### Siga el principio de solidez {#follow-the-robustness-principle}

El Principio de Solidez afirma que debemos ser conservadores en lo que enviamos, pero ser liberales en lo que aceptamos. En otras palabras, cuando enviamos mensajes a un tercero, debemos cumplir completamente con las especificaciones, pero cuando recibimos mensajes de un tercero, debemos aceptar mensajes no conformes siempre y cuando el significado del mensaje sea claro.

### Implementar picos en sus propios módulos {#implement-spikes-in-their-own-modules}

Los picos y el código de prueba son parte integral de cualquier implementación de software de Agile, pero queremos asegurarnos de que no entren en nuestra base de código de producción sin el nivel adecuado de supervisión. Como resultado, se recomienda crear picos en su propio módulo.

### Implementar scripts de migración de datos en su propio módulo {#implement-data-migration-scripts-in-their-own-module}

Los scripts de migración de datos, mientras que el código de producción, suelen ejecutarse solo una vez al inicio del sitio. Por lo tanto, tan pronto como el sitio está activo, esto se convierte en código muerto. Para garantizar que no se genere código de implementación que dependa de los scripts de migración, deben implementarse en su propio módulo. Esto también nos permite eliminar y retirar este código inmediatamente después del lanzamiento, eliminando el código muerto del sistema.

### Seguir convenciones de Maven publicadas en archivos POM {#follow-published-maven-conventions-in-pom-files}

Apache ha publicado convenciones de estilo en [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). Es mejor seguir estas convenciones, ya que hará que sea más fácil que los nuevos recursos se pongan al día rápidamente.
