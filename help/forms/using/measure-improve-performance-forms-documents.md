---
title: Medir y mejorar la eficacia y la conversión de formularios
seo-title: Measure and improve effectiveness and conversion of forms
description: AEM Forms se integra con las soluciones de Adobe Target y Adobe Analytics que le permiten medir y mejorar el rendimiento y la tasa de conversión de sus formularios.
seo-description: AEM Forms integrates with Adobe Target and Adobe Analytics solutions that allows you to measure and improve the performance and conversion rate of your forms.
uuid: fd2f087c-39f5-457d-8b44-c3ec4400b3fc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: a128877d-239c-4272-99c2-72d6486d5703
docset: aem65
exl-id: 4f45ad22-611b-4b4f-8e89-cb64a122b70a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 0%

---

# Medir y mejorar la eficacia y la conversión de formularios{#measure-and-improve-effectiveness-and-conversion-of-forms}

## El desafío {#the-challenge-br}

Las organizaciones están potenciando y alentando cada vez más a sus clientes a realizar transacciones mediante autoservicios digitales a través de múltiples canales. Sin embargo, en ausencia de un mecanismo de comentarios uno a uno, se torna difícil medir el éxito y experimentar con formularios digitales para mejorar la experiencia del cliente y aumentar las conversiones.

Para maximizar el ROI, las organizaciones deben monitorizar cómo sus clientes interactúan con los servicios y experimentar con sus artefactos digitales (formularios) para mejorar las experiencias de los clientes. Para medir el éxito y definir una estrategia de mejora, las organizaciones necesitan respuestas a preguntas como:

* ¿Cuántos clientes han intentado acceder o realizar transacciones con mis formularios?
* ¿Cuántos de ellos completaron correctamente la transacción?
* ¿Cuántos abandonaron el formulario?
* ¿Cuáles son las áreas problemáticas en las que los clientes se enfrentan a problemas?
* ¿Qué cambios traigo y cómo pruebo qué causa una mejor conversión?

## La solución {#the-solution}

AEM Forms se integra con [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) soluciones - [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) y [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html) : esto puede ayudarle a supervisar y analizar el rendimiento de los formularios, así como a experimentar e identificar la experiencia que conduce a una mejor tasa de conversión.

## El flujo de trabajo {#the-workflow}

Veamos los detalles de cómo medir el rendimiento y mejorar las tasas de conversión de los formularios.

### Audiencia objetivo {#target-audience}

* Usuarios y analistas empresariales responsables de estrategias de marketing y éxito
* Personal de TI que se ocupa de la configuración y mantenimiento de la infraestructura y las soluciones

### Componentes y funciones de AEM Forms implicados {#aem-forms-components-and-features-involved}

* Formularios adaptables
* Integración con Adobe Analytics para recopilar, organizar y crear informes de las interacciones de los clientes con los formularios adaptables
* Integración con Adobe Target para ejecutar pruebas A/B en formularios adaptables

### Suposiciones {#assumptions}

* Ya tiene una cuenta de Adobe Marketing Cloud y se ha registrado para las soluciones de Analytics y Target .
* Tiene un formulario adaptable publicado al que los clientes pueden acceder.

### Pasos del flujo de trabajo {#workflow-steps}

#### Paso 1: Configuración de Analytics y Target en AEM Forms  {#step-configure-analytics-and-target-in-aem-forms-br}

**Configurar Analytics**

Para obtener información detallada sobre las interacciones de los clientes con los formularios, primero debe configurar Analytics en AEM Forms. Siga estos pasos:

1. Crear un grupo de informes en Adobe Analytics
1. Crear la configuración del servicio en la nube en AEM
1. Crear marco de servicios en la nube en AEM
1. Configurar el servicio de configuración de AEM Forms Analytics en AEM
1. Habilitar analytics en el formulario en AEM

Para ver los pasos detallados, consulte [Configuración de análisis e informes para formularios adaptables](../../forms/using/configure-analytics-forms-documents.md).

**Configurar Target**

Para crear y ejecutar pruebas A/B en los formularios adaptables, configure Target en AEM Forms como se describe en [Configuración e integración de Target en AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### Paso 2: Ver informe de análisis {#step-view-analytics-report-br}

A medida que sus clientes acceden a los formularios en los que ha habilitado Analytics e interactúan con ellos, sus interacciones se capturan en bases de datos de Analytics altamente seguras. Los clientes segmentan las bases de datos y se puede acceder a ellas a través de conexiones seguras.

Puede ver un informe desde AEM para ver los formularios habilitados para análisis y analizar los datos. Para ver el informe:

1. En AEM servidor, vaya a **Forms > Forms y documentos**.
1. Seleccione el formulario para el que desea el informe de análisis.
1. Haga clic en el icono Informes de Analytics . Se muestra el informe.

Echemos un vistazo a los puntos de datos que Analytics recopila y genera informes para los formularios.

**Informe de análisis de Forms**

El informe de análisis para formularios adaptables captura los siguientes indicadores clave de rendimiento (KPI) a nivel de formulario:

* **Promedio de tiempo de llenado**: Tiempo promedio empleado en rellenar el formulario
* **Impresiones**: Número de veces que el formulario apareció en los resultados de la búsqueda

* **Representaciones**: Número de veces que se ha procesado o abierto el formulario
* **Borradores**: Número de veces que el formulario se ha guardado como borrador

* **Envíos**: Número de veces que se ha enviado el formulario
* **Anular**: Número de veces que los usuarios se han quedado sin completar el formulario
* **Visitas/envíos**: Proporción de visitas por envío

Además, obtiene los siguientes detalles sobre cada panel en el formulario:

* **Tiempo**: Tiempo promedio empleado (segundos) en el panel y sus campos

* **Error**: Número de errores encontrados en el panel y sus campos por 1000 representaciones de formulario

* **Ayuda**: Número de veces que los usuarios accedieron a la ayuda en contexto del panel y sus campos por cada 1000 representaciones de formulario

![Informe de análisis de ejemplo para un formulario adaptable](assets/summary-report.png)

Para obtener más información sobre los informes de análisis de formularios, consulte [Visualización y comprensión de los informes de análisis de AEM Forms](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>Puede ver informes detallados y comprender mejor los clientes y sus interacciones con los formularios desde la cuenta de Analytics en Adobe Marketing Cloud.

#### Paso 3: Analizar puntos de datos {#step-analyze-data-points}

En este paso, se analizarán los puntos de datos en el informe de análisis y se deducirá el rendimiento del formulario. Si no cumple con los KPI de éxito, construirá hipótesis basadas en datos y encontrará soluciones posibles para solucionar los problemas. Por ejemplo:

* Si el tiempo de rellenado promedio del formulario es mayor de lo esperado, es posible que el formulario sea complejo para los clientes, que el formulario no utilice terminologías estándar, que el formulario sea demasiado largo, etc. En este caso, es posible que desee simplificar la estructura y los campos del formulario, volver a trabajar en el diseño del formulario, acortar la longitud del formulario o agregar descripciones de ayuda y ejemplos para campos de formulario no estándar.
* Si los datos indican que la mayoría de los clientes acceden a la ayuda de un panel de formulario, es evidente que los clientes están confundidos con la información que se va a rellenar. Es posible que desee utilizar una terminología alternativa o agregar algunas entradas de ejemplo y una descripción de ayuda para ese panel.
* Si la tasa de anulación o abandono de un formulario es mayor de lo esperado, puede deberse a que el formulario tarda mucho tiempo en procesarse, los clientes aterrizan involuntariamente en el formulario o es demasiado complicado. En este caso, puede que desee optimizar la descripción del formulario que aparece en los resultados de la búsqueda, simplificar el formulario, optimizar el formulario para una carga más rápida, etc.

Una vez analizado estos puntos de datos y llegue a una hipótesis, realice los cambios necesarios en el formulario.

#### Paso 4: Validación del análisis y las correcciones {#step-validate-your-analysis-and-fixes}

En este paso, validará los cambios realizados en el formulario y comprobará si afectan a la tasa de conversión.

**Ejecutar una prueba A/B**

La integración de AEM Forms con Target permite crear pruebas A/B para formularios adaptables. En las pruebas A/B, se presentan aleatoriamente a los clientes diferentes experiencias de un formulario en tiempo real para saber qué experiencia funciona mejor o causa más conversiones. Una vez que tenga datos significativos que indiquen que una experiencia ofrece una mejor conversión que la otra, puede declarar que las experiencias son ganadoras y, a partir de ahora, se convertirá en la experiencia predeterminada visible para todos los clientes.

Para obtener más información sobre la creación de una prueba A/B para un formulario adaptable, consulte [Prueba A/B de formularios adaptables](../../forms/using/ab-testing-adaptive-forms.md).

![Informe de resumen de ejemplo de la prueba A/B para un formulario adaptable](assets/ab-test-report-4.png)

## Prácticas recomendadas {#best-practices}

Las prácticas recomendadas reales son las que se identifica a sí mismo al realizar este flujo de trabajo. Son exclusivos de su entorno y de sus requisitos. Descubra sus conocimientos a través del flujo de trabajo y fíltrelos como prácticas recomendadas.

Algunas recomendaciones sobre el diseño de formularios y la ejecución de pruebas A/B son las siguientes:

**Diseño de Forms**

* Mantenga el formulario sencillo, corto y fácil de navegar. Utilice indicaciones direccionales para la navegación.
* Utilice terminologías estándar o comunes para los campos de formulario.
* Explique el campo y la entrada necesaria, con ejemplos o ayuda, donde los usuarios pueden confundirse.
* Valide las entradas del usuario a medida que las escriban, siempre que sea posible, para evitar errores en el envío del formulario.
* Optimice los diseños tanto para escritorio como para dispositivos móviles.
* Rellenar automáticamente información para usuarios conocidos.

**Pruebas A/B**

* Construya una hipótesis e identifique las métricas de éxito antes de ejecutar la prueba A/B.
* Realice variaciones mínimas (idealmente, de una en una) en la experiencia alternativa para saber qué ha afectado a la tasa de conversión.
* Pruebe con frecuencia para eliminar las ineficiencias.
