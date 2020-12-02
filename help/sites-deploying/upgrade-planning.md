---
title: Planificación de la actualización
seo-title: Planificación de la actualización
description: Este artículo ayuda a establecer objetivos, fases y resultados claros al planificar la actualización AEM.
seo-description: Este artículo ayuda a establecer objetivos, fases y resultados claros al planificar la actualización AEM.
uuid: 6128ac53-4115-4262-82d9-a0ad7d498ea6
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 49210824-ad87-4b6a-9ae8-77dcfe2b5c06
docset: aem65
translation-type: tm+mt
source-git-commit: 5035c9630b5e861f4386e1b5ab4f4ae7a8d26149
workflow-type: tm+mt
source-wordcount: '2447'
ht-degree: 0%

---


# Planificación de la actualización{#planning-your-upgrade}

## Información general del proyecto de AEM {#aem-project-overview}

AEM se utiliza a menudo en implementaciones de alto impacto que pueden servir a millones de usuarios. En la mayoría de los casos, hay aplicaciones personalizadas que se implementan en las instancias, lo que aumenta la complejidad. Cualquier esfuerzo por actualizar una implementación de este tipo debe ser manejado metódicamente.

Esta guía ayuda a establecer objetivos, fases y resultados claros al planificar la actualización. Se centra en la ejecución general del proyecto y en las directrices. Aunque ofrece una visión general de los pasos reales de la actualización, se refiere a los recursos técnicos disponibles cuando procede. Debe utilizarse junto con los recursos técnicos disponibles a que se refiere el documento.

El proceso de actualización de AEM necesita fases de planificación, análisis y ejecución cuidadosamente gestionadas, con los productos clave definidos para cada fase.

Tenga en cuenta que es posible actualizar directamente desde AEM versiones 6.0 y hasta 6.5. Los clientes que ejecutan 5.6.x y versiones posteriores deben actualizar primero a la versión 6.0 o superior, y se recomienda 6.0 (SP3). Además, el nuevo formato de la barra de segmentos OAK se utiliza ahora para el almacén de nodos del segmento desde la versión 6.3, y la migración del repositorio a este nuevo formato es obligatoria incluso para 6.0, 6.1 y 6.2.

>[!CAUTION]
>
>Si está actualizando de AEM 6.2 a 6.3, debe actualizar desde versiones (**6.2-SP1-CFP1 - -6.2SP1-CFP12.1**) o **6.2SP1-CFP15** posteriores. De lo contrario, si está actualizando de **6.2SP1-CFP13/6.2SP1CFP14** a AEM 6.3, también debe actualizar a al menos la versión **6.3.2.2**. De lo contrario, AEM Sites fallaría tras la actualización.

## Alcance y requisitos de actualización {#upgrade-scope-requirements}

A continuación encontrará una lista de las áreas que se ven afectadas en un proyecto típico de actualización de AEM:

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Impacto</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Sistema operativo</td>
   <td>Efectos inciertos pero sutiles</td>
   <td>En el momento de la actualización de la AEM, es posible que también sea el momento de actualizar el sistema operativo, lo que podría tener cierto impacto.</td>
  </tr>
  <tr>
   <td>Java Runtime</td>
   <td>Impacto moderado</td>
   <td>AEM 6.3 requiere JRE 1.7.x (64 bits) o posterior. JRE 1.8 es la única versión admitida actualmente por Oracle.</td>
  </tr>
  <tr>
   <td>Hardware</td>
   <td>Impacto moderado</td>
   <td>La limpieza de revisión en línea requiere espacio libre<br /> en disco igual al 25% del tamaño del repositorio y un 15% de espacio libre en el montón<br /> para completar correctamente. Es posible que deba actualizar el hardware para<br /> garantizar recursos suficientes para que la Limpieza de revisión en línea se ejecute completamente<br />. Además, si se actualiza desde una versión anterior a AEM 6, es posible que haya<br /> requisitos de almacenamiento adicionales.</td>
  </tr>
  <tr>
   <td>Repositorio de contenido (CRX u Oak)</td>
   <td>Impacto alto</td>
   <td>A partir de la versión 6.1, AEM no admite CRX2, por lo que se requiere una migración a<br /> Oak (CRX3) si se actualiza desde una versión anterior. AEM 6.3 ha<br /> implementado un nuevo almacén de nodos de segmento que también requiere una migración. La herramienta<br /> crx2oak se utiliza para este propósito.</td>
  </tr>
  <tr>
   <td>AEM componentes/contenido</td>
   <td>Impacto moderado</td>
   <td><code>/libs</code> y <code>/apps</code> se administran fácilmente a través de la actualización, pero <code>/etc</code> generalmente requiere una reaplicación manual de las personalizaciones.</td>
  </tr>
  <tr>
   <td>Servicios AEM</td>
   <td>Bajo impacto</td>
   <td>La mayoría de los servicios principales AEM se prueban para la actualización. Este es un área de bajo impacto.</td>
  </tr>
  <tr>
   <td>Servicios de aplicación personalizados</td>
   <td>Impacto bajo a alto</td>
   <td>Según la aplicación y la personalización, puede haber dependencias<br /> en JVM, versiones del sistema operativo y algunos cambios relacionados con la indexación<br />, ya que los índices no se generan automáticamente en Oak.</td>
  </tr>
  <tr>
   <td>Contenido de aplicación personalizado</td>
   <td>Impacto bajo a alto</td>
   <td>El contenido que no se gestionará mediante la actualización se puede hacer una copia de seguridad<br /> antes de que se realice la actualización y, a continuación, volver a colocarlo en el repositorio.<br /> La mayoría del contenido se puede gestionar mediante la herramienta de migración.</td>
  </tr>
 </tbody>
</table>

Es importante asegurarse de que está ejecutando un sistema operativo compatible, Java Runtime, httpd y Dispatcher. Para obtener más información, consulte la [AEM página Requisitos técnicos de 6.5](/help/sites-deploying/technical-requirements.md). La actualización de estos componentes deberá tenerse en cuenta en el plan del proyecto y se realizará antes de actualizar AEM.

## Fases del proyecto {#project-phases}

Se trabaja mucho en la planificación y ejecución de una actualización AEM. A fin de aclarar los diferentes esfuerzos que se realizan en este proceso, hemos desglosado los ejercicios de planificación y ejecución en fases separadas. En las secciones que figuran a continuación, cada fase da como resultado un resultado que a menudo se aprovecha en una fase futura del proyecto.

### Planificación de la capacitación de autores {#planning-for-author-training}

Con cualquier nueva versión, se pueden introducir cambios en la interfaz de usuario y en los flujos de trabajo de usuario. Además, las nuevas versiones introducen nuevas funciones que pueden resultar beneficiosas para el negocio. Recomendamos revisar los cambios funcionales que se han introducido y organizar un plan para capacitar a los usuarios en el aprovechamiento eficaz de los mismos.

![unu_cropped](assets/unu_cropped.png)

Las nuevas funciones de AEM 6.5 se encuentran en [la sección AEM de adobe.com](/help/release-notes/release-notes.md). Asegúrese de anotar los cambios en las IU o en las funciones del producto que se utilizan comúnmente en su organización. A medida que explora las nuevas funciones, también debe tener en cuenta cualquier elemento que pueda ser de utilidad para su organización. Después de analizar lo que ha cambiado en AEM 6.5, desarrolle un plan de formación para sus autores. Esto podría implicar aprovechar los recursos disponibles de forma gratuita, como los vídeos de la función de ayuda o la formación formal ofrecida a través de [Adobe Digital Learning Services](https://www.adobe.com/training.html).

### Creación de un plan de pruebas {#creating-a-test-plan}

La implementación de AEM por parte de cada cliente es única y se ha personalizado para satisfacer sus requerimientos comerciales. Como resultado, es importante determinar todas las personalizaciones realizadas en el sistema para que puedan incluirse en un plan de prueba. Este plan de prueba impulsará el proceso de control de calidad que realizamos en la instancia actualizada.

![test-plan](assets/test-plan.png)

Es necesario duplicar el entorno de producción exacto y realizar pruebas en él después de la actualización para asegurarse de que todas las aplicaciones y el código personalizado siguen ejecutándose según lo desee. Debe recuperar toda la personalización y ejecutar pruebas de rendimiento, carga y seguridad. Al organizar el plan de prueba, asegúrese de cubrir todas las personalizaciones realizadas en el sistema, además de las IU y flujos de trabajo predeterminados que se aprovechan en las operaciones diarias. Pueden incluir servicios y servlets OSGI personalizados, integraciones a Adobe Marketing Cloud, integraciones con terceros a través de conectores de AEM, integraciones de terceros personalizadas, componentes y plantillas personalizados, superposiciones de interfaz de usuario personalizadas en AEM y flujos de trabajo personalizados. Para los clientes que migran desde una versión anterior a la AEM 6, cualquier consulta personalizada debe analizarse, ya que es posible que deba indizarse. Para los clientes que ya están en una versión AEM 6.x, estas consultas deben probarse para garantizar que sus índices sigan funcionando de forma eficaz después de la actualización.

### Determinación de los cambios en la arquitectura y la infraestructura necesarios {#determining-architectural-and-infrastructure-changes-needed}

Al realizar la actualización, es posible que también necesite actualizar otros componentes de la pila técnica, como el sistema operativo o JVM. Además, es posible que debido a los cambios en la composición del repositorio se requiera hardware adicional. Normalmente, esto solo sucede con los clientes que migran desde instancias anteriores a 6.x, pero es importante tener en cuenta. Por último, es posible que se necesiten cambios en sus prácticas operacionales, incluidos procesos de monitoreo, mantenimiento y backup y recuperación ante desastres.

![doi_cropped](assets/doi_cropped.png)

Revise los requisitos técnicos de AEM 6.5 y asegúrese de que el hardware y el software actuales sean suficientes. Para ver los posibles cambios en los procesos operativos, consulte los siguientes documentos:

**Monitoreo y mantenimiento:**

[Tablero de operaciones](/help/sites-administering/operations-dashboard.md)

[Prácticas recomendadas de supervisión de recursos](/help/assets/assets-monitoring-best-practices.md)

[Monitoreo de los recursos del servidor mediante la consola JMX](/help/sites-administering/jmx-console.md)

[Limpieza de revisión](/help/sites-deploying/revision-cleanup.md)

**Backup/Restore y Recuperación ante Desastres:**

[Copia de seguridad y restauración](/help/sites-administering/backup-and-restore.md)

[Rendimiento y escalabilidad](/help/sites-deploying/performance.md)

[Cómo ejecutar AEM con TarMK Cold Standby](/help/sites-deploying/tarmk-cold-standby.md)

#### Consideraciones de reestructuración de contenido {#content-restructuring-considerations}

AEM ha introducido cambios en la estructura del repositorio que ayudarán a realizar las actualizaciones de manera más fluida. Los cambios implican mover el contenido de la carpeta /etc a carpetas, incluidas /libs, /apps y /content, en función de si Adobe o un cliente son propietarios del contenido, lo que limita las posibilidades de sobrescribir el contenido durante las versiones. La reestructuración del repositorio se ha realizado de tal manera que no debe requerir cambios en el código en el momento de la actualización a la versión 6.5, aunque se recomienda revisar los detalles en [Reestructuración del repositorio en AEM](/help/sites-deploying/repository-restructuring.md) mientras se planifica una actualización.

### Evaluación de la complejidad de la actualización {#assessing-upgrade-complexity}

Debido a la gran variedad en cuanto a la cantidad y naturaleza de las personalizaciones que nuestros clientes aplican a sus entornos de AEM, es importante pasar un tiempo por adelantado para determinar el nivel general de esfuerzo que debe esperarse en su actualización.

Existen dos métodos que puede seguir para evaluar la complejidad de la actualización: una fase preliminar puede utilizar el nuevo detector de patrones introducido, que está disponible para ejecutarse en las instancias de AEM 6.1, 6.2 y 6.3. El detector de patrones es la manera más fácil de evaluar la complejidad general de la actualización que se espera que se realice utilizando los patrones notificados. El informe del detector de patrones incluye patrones para identificar las API no disponibles que están siendo utilizadas por el código base personalizado (esto se hizo usando las comprobaciones de compatibilidad previas a la actualización en 6.3).

Después de la evaluación inicial, un paso más amplio podría ser realizar una actualización en una instancia de prueba y realizar algunas pruebas de humo básicas. Adobe también proporciona algunos . Además, la lista de [Funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md) debe revisarse no sólo para la versión a la que está actualizando, sino también para cualquier versión entre las versiones de origen y destinatario. Por ejemplo, si actualiza de AEM 6.2 a 6.5, es importante revisar las funciones AEM 6.3 obsoletas y eliminadas, además de las de AEM 6.5.

![trei_cropped](assets/trei_cropped.png)

El detector de patrones introducido recientemente debería proporcionarle una estimación bastante precisa de lo que se puede esperar durante una actualización en la mayoría de los casos. Sin embargo, para personalizaciones e implementaciones más complejas en las que tenga cambios incompatibles, puede actualizar una instancia de desarrollo a AEM 6.5 de acuerdo con las instrucciones de [Realización de una actualización in-situ](/help/sites-deploying/in-place-upgrade.md). Una vez finalizado, realice pruebas de humo de alto nivel en este entorno. El objetivo de este ejercicio no es completar exhaustivamente el inventario de casos de prueba y elaborar un inventario formal de defectos, sino darnos una estimación aproximada de la cantidad de trabajo que se requerirá para actualizar el código para la compatibilidad con 6.5. Cuando se combina con la [Detección de patrones](/help/sites-deploying/pattern-detector.md) y los cambios de arquitectura que se determinaron en la sección anterior, se puede proporcionar una estimación aproximada al equipo de administración del proyecto para planificar la actualización.

### Creación del Runbook de actualización y reversión {#building-the-upgrade-and-rollback-runbook}

Aunque Adobe ha documentado el proceso de actualización de una instancia de AEM, el diseño de la red, la arquitectura de implementación y las personalizaciones de cada cliente requerirán un ajuste y una adaptación de este enfoque. Por este motivo, le animamos a revisar toda la documentación que hemos proporcionado y a utilizarla para informar a un runbook específico del proyecto que describe los procedimientos específicos de actualización y reversión que seguirá en su entorno. Si realiza la actualización desde CRX2, asegúrese de evaluar cuánto tardará la migración de contenido en pasar de CRX2 a Oak. Para repositorios grandes, podría ser sustancial.

![runbook-chart](assets/runbook-diagram.png)

Hemos proporcionado procedimientos de actualización y reversión en [Procedimiento de actualización](/help/sites-deploying/upgrade-procedure.md), así como instrucciones paso a paso para aplicar la actualización en Realización de una [Actualización in-situ](/help/sites-deploying/in-place-upgrade.md). Estas instrucciones deben revisarse y tenerse en cuenta con la arquitectura del sistema, las personalizaciones y la tolerancia del tiempo de inactividad para determinar los procedimientos adecuados de cambio y reversión que se van a ejecutar durante la actualización. Cualquier cambio en la arquitectura o en el tamaño del servidor debe incluirse al redactar el runbook personalizado. Es importante señalar que esto debería tratarse como un primer proyecto. A medida que su equipo complete sus ciclos de control de calidad y desarrollo e implemente la actualización al entorno de ensayo, es probable que sea necesario realizar algunos pasos adicionales. Idealmente, este documento debería contener suficiente información para que, si se entregara a un miembro de su personal de operaciones, pudiera completar la actualización completamente a partir de la información contenida en él.

### Desarrollo de un plan de proyecto {#developing-a-project-plan}

Podemos utilizar los resultados de ejercicios anteriores para construir un plan de proyecto que abarque los plazos esperados para nuestros esfuerzos de prueba o desarrollo, capacitación y ejecución real de la actualización.

![plan de desarrollo-proyecto](assets/develop-project-plan.png)

Un plan general de proyecto debería incluir:

* Finalización de los planes de desarrollo y ensayo
* Actualización de los entornos de desarrollo y control de calidad
* Actualización de la base de código personalizado para AEM 6.5
* Prueba de control de calidad y ciclo de corrección
* Actualización del entorno de ensayo
* Integración, rendimiento y pruebas de carga
* Certificación de entorno
* Ir a vivir

### Realización de Desarrollo y Control de Calidad {#performing-development-and-qa}

Hemos proporcionado procedimientos para que [Actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md) sean compatibles con AEM 6.5. A medida que se ejecuta este proceso iterativo, se deben realizar los cambios necesarios en el runbook. Consulte también [Compatibilidad con versiones anteriores en AEM 6.5](/help/sites-deploying/backward-compatibility.md) para obtener información sobre cómo las personalizaciones pueden permanecer compatibles con versiones anteriores en la mayoría de los casos sin necesidad de desarrollo inmediatamente después de la actualización.

![patru_cropped](assets/patru_cropped.png)

El proceso de desarrollo y prueba suele ser iterativo. Debido a las personalizaciones, los cambios realizados durante la actualización podrían hacer que una sección completa del producto quede inutilizable. Una vez que los desarrolladores han abordado la causa raíz del problema y el equipo de prueba tiene acceso para probar estas funciones, existe la posibilidad de que descubra problemas adicionales. A medida que se descubran problemas que requieren ajustes en el proceso de actualización, asegúrese de agregarlos al runbook de actualización personalizada. Después de varias repeticiones de pruebas y correcciones, la base de código debe estar completamente validada y lista para su implementación en el entorno de ensayo.

### Prueba final {#final-testing}

Recomendamos una ronda final de pruebas después de que el equipo de control de calidad de su organización haya certificado el código base. Esta ronda de pruebas implicará validar el runbook en un entorno de ensayo seguido de rondas de aceptación del usuario, rendimiento y pruebas de seguridad.

![cinci_cropped](assets/cinci_cropped.png)

Este paso es vital, ya que es la única vez que puede validar los pasos del runbook con un entorno de producción. Una vez actualizado el entorno, es importante que los usuarios finales tengan tiempo de iniciar sesión y pasar por las actividades que realizan al utilizar el sistema en sus actividades diarias. No es raro que los usuarios aprovechen una parte del sistema que no se consideró anteriormente. Encontrar y corregir problemas en estas áreas antes de la puesta en marcha puede ayudar a evitar costosas interrupciones de la producción. Dado que una nueva versión de AEM contiene cambios significativos en la plataforma subyacente, también es importante realizar pruebas de rendimiento, carga y seguridad en el sistema como si lo estuviéramos iniciando por primera vez.

### Realización de la actualización {#performing-the-upgrade}

Una vez que todas las partes interesadas hayan recibido la aprobación final, es hora de ejecutar los procedimientos del runbook que se han definido. Hemos proporcionado los pasos para la actualización y la reversión en [Procedimiento de actualización](/help/sites-deploying/upgrade-procedure.md) y los pasos de instalación para realizar una [actualización in-situ](/help/sites-deploying/in-place-upgrade.md) como punto de referencia.

![ejecutar-actualizar](assets/perform-upgrade.png)

Hemos proporcionado algunos pasos en las instrucciones de actualización para la validación de entornos. Estas incluyen comprobaciones básicas como el análisis de los registros de actualización y la verificación de que todos los paquetes de OSGi se han iniciado correctamente, pero también recomendamos validar con sus propios casos de prueba en función de los procesos de su negocio. También le recomendamos que compruebe el programa de AEM limpieza de revisión en línea y las rutinas relacionadas para asegurarse de que se producirán en un momento tranquilo para su compañía. Estas rutinas son esenciales para el desempeño a largo plazo de AEM.
