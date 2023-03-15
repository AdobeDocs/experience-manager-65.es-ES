---
title: Prácticas de desarrollo
seo-title: Development Practices
description: AEM Prácticas recomendadas para el desarrollo de en la
seo-description: Best practices for developing on AEM
uuid: 27a75f7f-6e2c-4113-9e9f-c5013a4594c2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8b0297a1-d922-410f-9aaf-3a6b87e11dc0
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 0%

---

# Prácticas de desarrollo{#development-practices}

## Trabajar según una definición de Listo {#work-according-to-a-definition-of-done}

Cada equipo tiene una definición diferente de lo que significa &quot;hecho&quot;, pero es importante tener una y asegurarse de que una historia cumpla con los criterios definidos antes de ser aceptada.

Algunos criterios que suelen especificar los equipos son:

* Código revisado para el formato
* Comentarios/Javadoc añadido
* Cumple los niveles de cobertura de prueba requeridos
* Supera las pruebas de unidad e integración
* Validado en el entorno de control de calidad
* Localización implementada

Sin un DoD bien definido, es fácil terminar en una situación donde muchas cosas están a medio camino y nada está verdaderamente completo.

### Definir y cumplir las convenciones de codificación y formato {#define-and-adhere-to-coding-and-formatting-conventions}

Las cosas como los niveles de sangría y el espacio en blanco pueden no parecer importantes, pero tener un código con el formato correcto contribuye en gran medida a la legibilidad y la capacidad de mantenimiento. Las convenciones deben debatirse y acordarse como un equipo y luego seguirse en el código.

### Objetivo para una alta cobertura de pruebas  {#aim-for-high-test-coverage}

A medida que la implementación de un proyecto aumenta de tamaño, también lo hará la cantidad de tiempo necesario para probarlo. Sin una buena cobertura de las pruebas, el equipo de pruebas no podrá escalar y los desarrolladores quedarán enterrados en errores.

Los desarrolladores deben practicar TDD y escribir pruebas unitarias fallidas antes del código de producción que cumplirá con sus requisitos. El control de calidad debe crear un conjunto automatizado de pruebas de aceptación para garantizar que el sistema funcione según lo esperado desde un alto nivel.

Hay marcos personalizados disponibles, como Jackalope y Prosper, para hacer que burlarse de las API de JCR sea más fácil para garantizar la productividad de los desarrolladores al escribir pruebas unitarias.

### Mantén la demostración lista {#stay-demo-ready}

El sistema debe estar disponible para la demostración a la empresa al final de cada iteración. Al mantener el sistema en un estado listo para la demostración, el equipo siempre estará dentro de una iteración de estar listo para la producción y la deuda técnica se puede mantener a un nivel mantenible.

### Implementar un entorno de integración continua y utilizarlo {#implement-a-continuous-integration-environment-and-use-it}

La implementación de un entorno de integración continua le permite ejecutar de forma fácil y repetida pruebas unitarias y de integración. También separará las implementaciones del equipo de desarrollo, lo que permitirá que las demás partes del equipo sean más eficientes y lograr implementaciones más estables y predecibles.

### Mantenga el ciclo de desarrollo rápido al mantener los tiempos de compilación bajos {#keep-the-development-cycle-fast-by-keeping-build-times-low}

Si las pruebas unitarias tardan mucho tiempo en ejecutarse, los desarrolladores evitarán ejecutarlas y perderán su valor. Si se tarda mucho tiempo en crear el código e implementarlo, las personas lo harán con menos frecuencia. Hacer que los tiempos de compilación cortos sean una prioridad garantiza que el tiempo que hemos invertido en nuestra cobertura de pruebas y en la infraestructura de CI siga haciendo que el equipo sea más productivo.

### Ajuste Sonar y otras herramientas de análisis de código estático y actúe en función de sus informes {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

Las herramientas de análisis de código pueden ser valiosas, pero solo si sus informes conducen a la acción por parte del equipo de desarrollo. Sin ajustar el análisis que proporcionan estas herramientas, las recomendaciones que generan no serán relevantes y perderán su valor.

### Sigue la regla del Scout {#follow-the-boy-scout-rule}

Los Boy Scout tienen una regla: &quot;Déjalo mejor de lo que lo encontraste&quot;. Mientras todos los miembros del equipo de desarrollo se adhieran a esta regla y limpien algo cuando se encuentren con un lío, el código mejorará constantemente.

### Evitar la implementación de funciones YAGNI {#avoid-implementing-yagni-features}

Las funciones de YAGNI (o no lo vas a necesitar) son cosas que se implementan cuando esperamos que necesitemos algo en el futuro, aunque no lo necesitemos ahora. Idealmente, deberíamos implementar lo más simple que funcione hoy en día y utilizar una refactorización continua para garantizar que la arquitectura del sistema evolucione con los requisitos a lo largo del tiempo. Esto nos permitirá centrarnos en lo que importa y evitar la hinchazón del código y la fluidez de las funciones.
