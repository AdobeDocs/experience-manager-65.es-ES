---
title: Prácticas de desarrollo
seo-title: Prácticas de desarrollo
description: Prácticas recomendadas para desarrollar la AEM
seo-description: Prácticas recomendadas para desarrollar la AEM
uuid: 27a75f7f-6e2c-4113-9e9f-c5013a4594c2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8b0297a1-d922-410f-9aaf-3a6b87e11dc0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# Prácticas de desarrollo{#development-practices}

## Trabajo según una definición de Listo {#work-according-to-a-definition-of-done}

Cada equipo tiene una definición diferente de lo que significa &quot;hecho&quot;, pero es importante tener una y asegurarse de que una historia cumpla los criterios definidos antes de ser aceptada.

Algunos de los criterios que suelen especificar los equipos son:

* Código revisado para dar formato
* Comentarios/Javadoc añadidos
* Cumple los niveles de cobertura de prueba requeridos
* Pasa las pruebas de unidad e integración
* Validado en el entorno de control de calidad
* Localización implementada

Sin un DoD bien definido, es fácil terminar en una situación en la que muchas cosas están a medio camino y nada está realmente completo.

### Defina y cumpla las convenciones de codificación y formato {#define-and-adhere-to-coding-and-formatting-conventions}

Cosas como los niveles de sangría y el espacio en blanco pueden no parecer importantes, pero tener un código formateado adecuadamente contribuye en gran medida a la legibilidad y mantenimiento. Las convenciones deben debatirse y acordarse como un equipo y seguirse en el código.

### Objetivo para una cobertura de prueba alta {#aim-for-high-test-coverage}

A medida que la implementación de un proyecto crece en tamaño, también lo hará la cantidad de tiempo necesaria para probarlo. Sin una buena cobertura de pruebas, el equipo de pruebas no podrá escalar y los desarrolladores terminarán enterrados en errores.

Los desarrolladores deben practicar TDD, escribiendo pruebas unitarias fallidas antes del código de producción que cumplirá con sus requisitos. El control de calidad debe crear un conjunto automatizado de pruebas de aceptación para garantizar que el sistema funcione según lo esperado desde un nivel elevado.

Existen marcos de trabajo personalizados disponibles, como Jackalope y Prosper, para simplificar la burla de las API de JCR a fin de garantizar la productividad de los desarrolladores mientras escriben pruebas unitarias.

### Esté listo para la demostración {#stay-demo-ready}

El sistema debe estar disponible para demostraciones al negocio al final de cada iteración. Al mantener el sistema en un estado listo para la demostración, el equipo siempre estará en una iteración de estar listo para la producción y la deuda técnica se puede mantener a un nivel sostenible.

### Implementar un entorno de integración continua y utilizarlo {#implement-a-continuous-integration-environment-and-use-it}

La implementación de un entorno de integración continua le permitirá ejecutar de forma fácil y repetida pruebas unitarias y pruebas de integración. También desacoplará los despliegues del equipo de desarrollo, lo que permitirá a las demás partes del equipo ser más eficientes y lograr despliegues más estables y predecibles.

### Mantenga el ciclo de desarrollo rápido manteniendo los tiempos de compilación bajos {#keep-the-development-cycle-fast-by-keeping-build-times-low}

Si las pruebas unitarias tardan mucho en ejecutarse, los desarrolladores evitarán ejecutarlas y perderán su valor. Si lleva mucho tiempo crear el código e implementarlo, las personas lo harán con menos frecuencia. Hacer de los tiempos de construcción cortos una prioridad garantiza que el tiempo que hemos invertido en nuestra cobertura de pruebas e infraestructura de CI seguirá haciendo que el equipo sea más productivo.

### Afinar Sonar y otras herramientas de análisis de código estático y actuar en sus informes {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

Las herramientas de análisis de código pueden ser valiosas, pero sólo si sus informes llevan a la acción por parte del equipo de desarrollo. Sin perfeccionar la análisis que estas herramientas proporcionan, las recomendaciones que generan no serán relevantes y perderán su valor.

### Siga la regla del Scout principal {#follow-the-boy-scout-rule}

Los Scout Boy tienen una regla: &quot;Déjalo mejor de lo que lo encontraste&quot;. Mientras todos los miembros del equipo de desarrollo se adhieran a esta regla y limpien algo cuando se encuentren con un desastre, el código mejorará constantemente.

### Evite implementar las características de YAGNI {#avoid-implementing-yagni-features}

Las características de YAGNI (o Usted no lo va a necesitar) son cosas que se implementan cuando esperamos que necesitaremos algo en el futuro, aunque no lo necesitamos ahora. Idealmente, deberíamos implementar lo más sencillo que funcione hoy en día y utilizar la refactorización continua para garantizar que la arquitectura del sistema evolucione con los requisitos a lo largo del tiempo. Esto nos permitirá centrarnos en lo que importa y evitar que el código se expanda y las funciones se propaguen.
