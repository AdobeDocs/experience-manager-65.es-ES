---
title: Medir y mejorar la eficacia y conversión de los formularios
seo-title: Medir y mejorar la eficacia y conversión de los formularios
description: AEM Forms se integra con las soluciones Adobe Target y Adobe Analytics que le permiten medir y mejorar el rendimiento y la tasa de conversión de los formularios.
seo-description: AEM Forms se integra con las soluciones Adobe Target y Adobe Analytics que le permiten medir y mejorar el rendimiento y la tasa de conversión de los formularios.
uuid: fd2f087c-39f5-457d-8b44-c3ec4400b3fc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: a128877d-239c-4272-99c2-72d6486d5703
docset: aem65
translation-type: tm+mt
source-git-commit: befbdfd574949a7f7449b70a15480e7c105418fe
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 0%

---


# Mida y mejore la eficacia y conversión de los formularios{#measure-and-improve-effectiveness-and-conversion-of-forms}

## El desafío {#the-challenge-br}

Las organizaciones están potenciando y alentando cada vez más a sus clientes a realizar transacciones mediante autoservicios digitales a través de múltiples canales. Sin embargo, a falta de un mecanismo de comentarios uno a uno, resulta difícil medir el éxito y experimentar con formularios digitales para mejorar la experiencia del cliente y aumentar las conversiones.

Para maximizar el ROI, las organizaciones deben monitorear la forma en que sus clientes interactúan con los servicios y experimentar con sus artefactos digitales (formularios) para mejorar las experiencias de los clientes. Para medir el éxito y definir una estrategia de mejora, las organizaciones necesitan respuestas a preguntas como:

* ¿Cuántos clientes intentaron acceder a mis formularios o realizar transacciones con ellos?
* ¿Cuántos de ellos completaron correctamente la transacción?
* ¿Cuántos de ellos abandonaron el formulario?
* ¿Cuáles son las áreas problemáticas en las que los clientes enfrentan problemas?
* ¿Qué cambios se producen y cómo se comprueba qué causa una mejor conversión?

## La solución {#the-solution}

AEM Forms se integra con [soluciones de Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) - [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) y [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html) - que pueden ayudarle a monitorear y analizar el rendimiento de los formularios y permitirle experimentar e identificar la experiencia que conduce a una mejor tasa de conversión.

## El flujo de trabajo {#the-workflow}

Veamos los detalles de cómo medir el rendimiento y mejorar las tasas de conversión de los formularios.

### Audiencia de destinatario {#target-audience}

* Usuarios y analistas empresariales responsables de las estrategias de mercadotecnia y del éxito
* Personal de TI que se ocupa de la configuración y el mantenimiento de la infraestructura y las soluciones

### Componentes y características de AEM Forms implicados {#aem-forms-components-and-features-involved}

* Formularios adaptables
* Integración con Adobe Analytics para recopilar, organizar e informar sobre las interacciones de los clientes con sus formularios adaptables
* Integración con Adobe Target para ejecutar pruebas A/B en formularios adaptables

### Suposiciones {#assumptions}

* Ya tiene una cuenta de Adobe Marketing Cloud y se ha registrado para las soluciones de Analytics y Destinatario.
* Tiene un formulario adaptable publicado al que los clientes pueden acceder.

### Pasos del flujo de trabajo {#workflow-steps}

#### Paso 1: Configurar Analytics y Destinatario en AEM Forms {#step-configure-analytics-and-target-in-aem-forms-br}

**Configurar Analytics**

Para obtener información detallada sobre las interacciones del cliente con los formularios, primero debe configurar Analytics en AEM Forms. Siga estos pasos:

1. Crear un grupo de informes en Adobe Analytics
1. Crear configuración de servicio de nube en AEM
1. Crear un marco de servicios en la nube en AEM
1. Configurar el servicio de configuración de AEM Forms Analytics en AEM
1. Habilitar análisis en el formulario en AEM

Para ver los pasos detallados, consulte [Configuración de análisis e informes para formularios adaptables](../../forms/using/configure-analytics-forms-documents.md).

**Configurar Destinatario**

Para crear y ejecutar pruebas A/B para sus formularios adaptables, configure Destinatario en AEM Forms como se describe en [Configurar e integrar Destinatario en AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### Paso 2: Informe de análisis de vista {#step-view-analytics-report-br}

A medida que sus clientes acceden a los formularios en los que ha habilitado Analytics e interactúan con ellos, sus interacciones se capturan en bases de datos de Analytics con alta seguridad. Las bases de datos están segmentadas por clientes y son accesibles mediante conexiones seguras.

Puede vista de un informe desde dentro de AEM para los formularios habilitados para análisis y analizar los datos. Para vista del informe:

1. En AEM servidor, vaya a **Forms > Forms y Documentos**.
1. Seleccione el formulario para el que desea el informe de análisis.
1. Haga clic en el icono Informes de Analytics. Se muestra el informe.

Veamos los puntos de datos que Analytics recopila y genera informes para los formularios.

**Informe de análisis de Forms**

El informe de análisis para formularios adaptables captura los siguientes indicadores de rendimiento clave (KPI) en un nivel de formulario:

* **Tiempo** de relleno promedio: Tiempo promedio empleado en rellenar el formulario
* **Impresiones**: Número de veces que el formulario apareció en los resultados de la búsqueda

* **Representaciones**: Número de veces que se ha procesado o abierto el formulario
* **Borradores**: Número de veces que el formulario se ha guardado como borrador

* **Envíos**: Número de veces que se ha enviado el formulario
* **Anular**: Número de veces que los usuarios se han ido sin completar el formulario
* **Visitas/Envíos**: Tasa de visitas por envío

Además, se obtienen los siguientes detalles sobre cada panel del formulario:

* **Hora**: Tiempo promedio empleado (segundos) en el panel y sus campos

* **Error**: Número de errores encontrados en el panel y sus campos por cada 1000 representaciones de formularios

* **Ayuda**: Número de veces que los usuarios accedieron a la ayuda en contexto del panel y sus campos por cada 1000 representaciones de formularios

![Un informe de análisis de muestra para un formulario adaptable](assets/summary-report.png)

Para obtener más información sobre los informes de análisis de formularios, consulte [Visualización y comprensión de informes de análisis de AEM Forms](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>Puede vista de informes detallados y obtener una perspectiva más profunda sobre sus clientes y sus interacciones con los formularios desde su cuenta de Analytics en Adobe Marketing Cloud.

#### Paso 3: Analizar puntos de datos {#step-analyze-data-points}

En este paso, analizará los puntos de datos en el informe de análisis e informará sobre el rendimiento del formulario. Si no cumple los KPI de éxito, creará hipótesis basadas en datos y encontrará posibles soluciones para solucionar los problemas. Por ejemplo:

* Si el tiempo de relleno medio del formulario es superior al esperado, es posible que el formulario sea complejo para los clientes, que el formulario no utilice terminologías estándar, que el formulario sea demasiado largo, etc. En este caso, es posible que desee simplificar la estructura y los campos del formulario, volver a trabajar en el diseño de formulario, acortar la longitud del formulario o agregar descripciones y ejemplos de ayuda para campos de formulario no estándar.
* Si los datos indican que la mayoría de los clientes están accediendo a la ayuda de un panel de formularios, es evidente que los clientes están perplejos con la información que se va a rellenar. Es posible que desee utilizar una terminología alternativa o agregar algunas entradas de ejemplo y una descripción de ayuda para ese panel.
* Si la tasa de abandono o anulación de un formulario es superior a la esperada, puede deberse a que el formulario tarda mucho tiempo en procesarse, a que los clientes aterrizan inadvertidamente en el formulario o a que es demasiado complicado. En este caso, es posible que desee optimizar la descripción del formulario que aparece en los resultados de la búsqueda, simplificar el formulario, optimizar el formulario para una carga más rápida, etc.

Una vez que haya analizado estos puntos de datos y llegado a una hipótesis, realice los cambios necesarios en el formulario.

#### Paso 4: Valide la análisis y corrija {#step-validate-your-analysis-and-fixes}

En este paso, validará los cambios realizados en el formulario y comprobará si afectan a la tasa de conversión.

**Ejecutar una prueba A/B**

La integración de AEM Forms con Destinatario permite crear pruebas A/B para formularios adaptables. En las pruebas A/B, se presentan al azar diferentes experiencias de un formulario a los clientes en tiempo real para saber qué experiencia funciona mejor o genera más conversiones. Una vez que tenga datos significativos que indiquen que una experiencia ofrece una mejor conversión que la otra, puede declarar que las experiencias son las ganadoras y, a partir de ahora, se convierten en la experiencia predeterminada visible para todos los clientes.

Para obtener más información sobre la creación de una prueba A/B para un formulario adaptable, consulte [Prueba A/B de formularios adaptables](../../forms/using/ab-testing-adaptive-forms.md).

![Un informe de resumen de muestra de la prueba A/B para un formulario adaptable](assets/ab-test-report-4.png)

## Prácticas recomendadas {#best-practices}

Las prácticas recomendadas reales son las que usted mismo se identifica al realizar este flujo de trabajo. Son exclusivos de su entorno y de sus necesidades. Capture sus conocimientos a través del flujo de trabajo y documento los mismos como prácticas recomendadas.

Algunas recomendaciones sobre el diseño de formularios y la ejecución de pruebas A/B son las siguientes:

**Forms design**

* Mantenga el formulario sencillo, corto y fácil de navegar. Utilice indicaciones direccionales para la navegación.
* Utilice terminologías estándar o comunes para los campos de formulario.
* Explicar el campo y la entrada necesaria, con ejemplos o ayuda, donde los usuarios pueden confundirse.
* Valide las entradas del usuario a medida que las escriben, siempre que sea posible, para evitar errores en el envío del formulario.
* Optimice los diseños tanto para escritorio como para dispositivos móviles.
* Rellenar automáticamente información para usuarios conocidos.

**Pruebas A/B**

* Cree una hipótesis e identifique las métricas de éxito antes de ejecutar la prueba A/B.
* Realice variaciones mínimas (idealmente una a una) en la experiencia alternativa para saber qué impacto tuvo en la tasa de conversión.
* Realice pruebas con frecuencia para eliminar las ineficiencias.

