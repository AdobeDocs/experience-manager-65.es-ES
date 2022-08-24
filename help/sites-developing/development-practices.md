---
title: Prácticas de desarrollo
seo-title: Development Practices
description: Prácticas recomendadas para el desarrollo en AEM
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

## Trabajo según una definición de finalizado {#work-according-to-a-definition-of-done}

Cada equipo tiene una definición diferente de lo que significa &quot;hecho&quot;, pero es importante tener una y asegurarse de que una historia cumpla los criterios definidos antes de ser aceptada.

Algunos criterios que suelen especificar los equipos son:

* Código revisado para formato
* Comentarios/Javadoc añadidos
* Cumple los niveles de cobertura de prueba necesarios
* Pasa las pruebas de unidad e integración
* Validado en el entorno de control de calidad
* Localización implementada

Sin un DoD bien definido, es fácil terminar en una situación donde muchas cosas se hacen a medio camino y nada es realmente completo.

### Definir y cumplir las convenciones de codificación y formato {#define-and-adhere-to-coding-and-formatting-conventions}

Cosas como los niveles de sangría y el espacio en blanco pueden no parecer importantes, pero tener un código formateado correctamente es un gran paso hacia la legibilidad y el mantenimiento. Las convenciones deben debatirse y acordarse como un equipo y luego seguirse en el código.

### Objetivo de una cobertura de pruebas elevada  {#aim-for-high-test-coverage}

A medida que la implementación de un proyecto crece en tamaño, también lo hará la cantidad de tiempo que sea necesario para probarlo. Sin una buena cobertura de pruebas, el equipo de pruebas no podrá escalar y los desarrolladores terminarán enterrados en errores.

Los desarrolladores deben practicar TDD, escribiendo pruebas unitarias fallidas antes del código de producción que cumpla con sus requisitos. El control de calidad debe crear un conjunto automatizado de pruebas de aceptación para garantizar que el sistema funciona como se espera desde un nivel elevado.

Hay marcos personalizados disponibles, como Jackalope y Prosper, para hacer que las burlas de las API de JCR sean más simples para garantizar la productividad de los desarrolladores mientras escriben pruebas unitarias.

### Esté listo para la demostración {#stay-demo-ready}

El sistema debe estar disponible para su demostración a la empresa al final de cada iteración. Al mantener el sistema en un estado listo para la demostración, el equipo siempre estará en una iteración de estar listo para la producción y la deuda técnica se puede mantener a un nivel sostenible.

### Implementar un entorno de integración continua y utilizarlo {#implement-a-continuous-integration-environment-and-use-it}

La implementación de un entorno de integración continua le permitirá ejecutar pruebas de unidades y pruebas de integración de forma fácil y repetible. También desacoplará las implementaciones del equipo de desarrollo, lo que permitirá que las demás partes del equipo sean más eficientes y permitan implementaciones más estables y predecibles.

### Mantenga el ciclo de desarrollo rápido manteniendo los tiempos de compilación bajos {#keep-the-development-cycle-fast-by-keeping-build-times-low}

Si las pruebas unitarias tardan mucho en ejecutarse, los desarrolladores evitarán ejecutarlas y perderán su valor. Si se tarda mucho tiempo en crear el código e implementarlo, las personas lo harán con menos frecuencia. Hacer de los tiempos de construcción cortos una prioridad garantiza que el tiempo que hemos invertido en nuestra cobertura de pruebas e infraestructura de CI seguirá haciendo que el equipo sea más productivo.

### Ajuste Sonar y otras herramientas de análisis de código estático y actúe en sus informes {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

Las herramientas de análisis de código pueden ser valiosas, pero solo si sus informes llevan a la acción por parte del equipo de desarrollo. Sin ajustar el análisis que proporcionan estas herramientas, las recomendaciones que generan no serán relevantes y perderán su valor.

### Siga la regla del Scout de niños {#follow-the-boy-scout-rule}

Los Scout Chico tienen una regla: &quot;Déjalo mejor de lo que lo encontraste&quot;. Mientras todos los miembros del equipo de desarrollo se adhieran a esta regla y limpien algo cuando se encuentren en un lío, el código mejorará constantemente.

### Evite implementar características de YAGNI {#avoid-implementing-yagni-features}

Las características de YAGNI (o no lo vas a necesitar) son cosas que se implementan cuando esperamos que necesitemos algo en el futuro, aunque no lo necesitamos ahora. Idealmente, deberíamos implementar lo más sencillo que funcione hoy en día y usar la refactorización continua para garantizar que la arquitectura del sistema evolucione con los requisitos a lo largo del tiempo. Esto nos permitirá centrarnos en lo que importa y evitar que el código se propague y las funciones se propaguen.
