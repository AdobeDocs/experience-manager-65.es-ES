---
title: Comprobaciones posteriores a la actualización y resolución de problemas
seo-title: Comprobaciones posteriores a la actualización y resolución de problemas
description: Obtenga información sobre cómo solucionar problemas que puedan aparecer después de una actualización.
seo-description: Obtenga información sobre cómo solucionar problemas que puedan aparecer después de una actualización.
uuid: 3f525f2c-8d25-4bb8-a57e-3adf667edde8
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 5a67aa9f-e5eb-4d7e-89da-2ee1a45eb8ce
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 0%

---


# Comprobaciones posteriores a la actualización y resolución de problemas{#post-upgrade-checks-and-troubleshooting}

## Comprobaciones posteriores a la actualización {#post-upgrade-checks}

Después de la [Actualización in-situ](/help/sites-deploying/in-place-upgrade.md) se deben ejecutar las siguientes actividades para finalizar la actualización. Se da por supuesto AEM se ha iniciado con el tarro 6.5 y que se ha implementado la base de códigos actualizada.

* [Verificar registros para actualización correcta](#main-pars-header-290365562)

* [Verificar paquetes OSGi](#main-pars-header-1637350649)

* [Verificar versión Oak](#main-pars-header-1293049773)

* [Inspect la carpeta PreUpgradeBackup](#main-pars-header-988995987)

* [Validación inicial de páginas](#main-pars-header-20827371)
* [Aplicar Service Packs AEM](#main-pars-header-215142387)

* [Migrar funciones de AEM](#main-pars-header-1434457709)

* [Verificar las configuraciones de mantenimiento programadas](#main-pars-header-1552730183)

* [Habilitar agentes de replicación](#main-pars-header-823243751)

* [Habilitar trabajos programados personalizados](#main-pars-header-244535083)

* [Ejecutar plan de prueba](#main-pars-header-1167972233)

### Verificar registros para el éxito de la actualización {#verify-logs-for-upgrade-success}

**upgrade.log**

Anteriormente, la inspección del estado posterior a la actualización de su instancia requería una cuidadosa inspección de varios archivos de registro, partes del repositorio y el Launchpad. La generación de un informe posterior a la actualización puede ayudar a detectar actualizaciones defectuosas antes de activarlas.

El objetivo principal de esta función es reducir la necesidad de una interpretación manual o de una lógica de análisis compleja en varios extremos necesarios para calificar el éxito de una actualización. La solución tiene como objetivo proporcionar información inequívoca para que los sistemas de automatización externos reaccionen en cuanto al éxito o al error identificado de una actualización.

Más concretamente, garantiza que:

* Los errores de actualización detectados por el marco de actualización se pueden centralizar en un solo informe de actualización;
* El informe de actualización incluye indicadores sobre la intervención manual necesaria.

Para adaptarse a esto, se han realizado cambios en la forma en que se generan los registros en el archivo `upgrade.log`.

Este es un informe de muestra que no muestra errores durante la actualización:

![1487887443006](assets/1487887443006.png)

Este es un informe de muestra que muestra un paquete que no se instaló durante el proceso de actualización:

![1487887532730](assets/1487887532730.png)

**error.log**

El error.log debe revisarse cuidadosamente durante y después del inicio de AEM usando el tarro de la versión de destinatario. Cualquier advertencia o error debe revisarse. En general, es mejor buscar problemas al principio del registro. Los errores que se producen más adelante en el registro pueden ser en realidad efectos secundarios de una causa raíz que se invoca al principio del archivo. Si se producen errores y advertencias repetidos, consulte a continuación [Análisis de problemas con la actualización](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### Verificar paquetes OSGi {#verify-osgi-bundles}

Vaya a la consola OSGi `/system/console/bundles` y vea si no se ha iniciado ningún paquete. Si alguno de los paquetes está en estado de instalación, consulte `error.log` para determinar el problema raíz.

### Verificar la versión Oak {#verify-oak-version}

Después de la actualización, debería ver que la versión de Oak se ha actualizado a **1.10.2**. Para verificar la versión de Oak, vaya a la consola OSGi y mire la versión asociada a los paquetes de Oak: Oak Core, Oak Commons, Oak Segment Tar.

### Carpeta Inspect PreUpgradeBackup {#inspect-preupgradebackup-folder}

Durante la actualización, el AEM intentará hacer backup de las personalizaciones y almacenarlas debajo de `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`. Para poder vista esta carpeta en CRXDE Lite, es posible que deba [habilitar temporalmente CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

La carpeta con la marca de hora debe tener una propiedad denominada `mergeStatus` con un valor de `COMPLETED`. La carpeta **para procesar** debe estar vacía y el nodo **sobrescrito** indica qué nodos se sobrescribieron durante la actualización. El contenido debajo del nodo **izquierdas** indica el contenido que no se pudo combinar de forma segura durante la actualización. Si la implementación depende de cualquiera de los nodos secundarios (y no está instalada por el paquete de código actualizado), deberá combinarlos manualmente.

Desactive el CRXDE Lite que sigue este ejercicio si se encuentra en un escenario o entorno de producción.

### Validación inicial de páginas {#initial-validation-of-pages}

Realice una validación inicial con varias páginas de AEM. Si actualiza un entorno de creación, abra la página de Inicio y la página de bienvenida ( `/aem/start.html`, `/libs/cq/core/content/welcome.html`). Tanto en el entorno de creación como en el de publicación, se abren algunas páginas de aplicación y se realiza una prueba de humo que se procesan correctamente. Si se produce algún problema, consulte `error.log` para solucionarlo.

### Aplicar Service Packs de AEM {#apply-aem-service-packs}

Aplique los Service Packs relevantes de AEM 6.5 si se han lanzado.

### Migrar características de AEM {#migrate-aem-features}

Varias funciones de AEM requieren pasos adicionales después de la actualización. Puede encontrar una lista completa de estas características y pasos para migrarlas en AEM 6.5 en la página [Actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md).

### Verificar las configuraciones de mantenimiento programadas {#verify-scheduled-maintenance-configurations}

#### Habilitar recopilación de elementos no utilizados del almacén de datos {#enable-data-store-garbage-collection}

Si utiliza un almacén de datos de archivos, asegúrese de que la tarea Recopilación de elementos no utilizados del almacén de datos está activada y se agrega a la lista de mantenimiento semanal. Las instrucciones se describen [aquí](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>No se recomienda para instalaciones de almacén de datos personalizado S3 o cuando se utiliza un almacén de datos compartido.

#### Habilitar limpieza de revisión en línea {#enable-online-revision-cleanup}

Si utiliza MongoMK o el nuevo formato de segmento TarMK, asegúrese de que la tarea de limpieza de revisión esté activada y agregada a la lista de mantenimiento diario. Instrucciones descritas [aquí](/help/sites-deploying/revision-cleanup.md).

### Ejecutar plan de pruebas {#execute-test-plan}

Ejecute un plan de prueba detallado según se define en la sección [Actualización de código y personalizaciones](/help/sites-deploying/upgrading-code-and-customizations.md) de **Procedimiento de prueba**.

### Habilitar agentes de replicación {#enable-replication-agents}

Una vez que el entorno de publicación se haya actualizado y validado completamente, habilite los agentes de replicación en el Entorno de creación. Compruebe que los agentes pueden conectarse a las instancias de publicación correspondientes. Consulte U [Actualización del procedimiento](/help/sites-deploying/upgrade-procedure.md) para obtener más información sobre el orden de los eventos.

### Habilitar trabajos programados personalizados {#enable-custom-scheduled-jobs}

Cualquier trabajo programado como parte de la base de código puede habilitarse en este punto.

## Análisis De Problemas Con La Actualización {#analyzing-issues-with-upgrade}

Esta sección contiene algunos escenarios de problemas a los que podría enfrentarse durante el procedimiento de actualización a AEM 6.3.

Estos escenarios deberían ayudar a rastrear la causa raíz de los problemas relacionados con la actualización y deberían ayudar a identificar los problemas específicos del proyecto o producto.

### Error en la migración del repositorio {#repository-migration-failing-}

La migración de datos de CRX2 a Oak debería ser factible en cualquier escenario que comience con instancias de origen basadas en CQ 5.4. Asegúrese de seguir exactamente las instrucciones de actualización de este documento, que incluyen la preparación de `repository.xml`, asegurándose de que no se inicie ningún autenticador personalizado mediante JAAS y de que se hayan comprobado las incoherencias de la instancia antes de iniciar la migración.

Si la migración sigue fallando, puede averiguar cuál es la causa raíz inspeccionando el `upgrade.log`. Si el problema aún no se conoce, notifíquelo a la Asistencia al cliente.

### La Actualización No Se Ejecutó {#the-upgrade-did-not-run}

Antes de iniciar los pasos de preparación, asegúrese de ejecutar primero la instancia **source** ejecutándola con el comando java -jar aem-quickstart.jar. Esto es necesario para asegurarse de que el archivo quickstart.properties se genera correctamente. Si falta, la actualización no funcionará. También puede comprobar si el archivo está presente buscando `crx-quickstart/conf` en la carpeta de instalación de la instancia de origen. Además, al iniciar AEM para iniciar la actualización, debe ejecutarse con el comando java -jar aem-quickstart.jar. El inicio desde una secuencia de comandos de inicio no AEM en el modo de actualización.

### Los paquetes y los paquetes no se actualizan {#packages-and-bundles-fail-to-update-}

Si los paquetes no se instalan durante la actualización, tampoco se actualizarán los paquetes que contienen. Esta categoría de problemas suele deberse a una configuración incorrecta del almacén de datos. También aparecerán como mensajes **ERROR** y **WARN** en error.log. Dado que en la mayoría de estos casos el inicio de sesión predeterminado puede no funcionar, puede utilizar CRXDE directamente para inspeccionar y encontrar los problemas de configuración.

### Algunos paquetes AEM no cambian al estado activo {#some-aem-bundles-are-not-switching-to-the-active-state}

En caso de que los paquetes no se inicien, debe comprobar si hay dependencias insatisfechas.

En caso de que este problema esté presente pero se base en una instalación de paquete fallida que provocó que los paquetes no se actualizaran, se considerarán incompatibles con la nueva versión. Para obtener más información sobre cómo solucionar este problema, consulte **Paquetes y paquetes que no se actualizan** más arriba.

También se recomienda comparar la lista del paquete de una instancia de AEM 6.5 nueva con la actualización para detectar los paquetes que no se han actualizado. Esto proporcionará un alcance más cercano de lo que se debe buscar en `error.log`.

### Los paquetes personalizados no cambian al estado activo {#custom-bundles-not-switching-to-the-active-state}

En caso de que los paquetes personalizados no cambien al estado activo, lo más probable es que haya código que no importe la API de cambio. Esto generalmente lleva a dependencias insatisfechas.

La API que se eliminó debe marcarse como obsoleta en una de las versiones anteriores. Puede encontrar instrucciones sobre una migración directa del código en este aviso de desaprobación. Adobe tiene como objetivo el control semántico de versiones siempre que sea posible para que las versiones puedan indicar cambios de salto.

También es mejor comprobar si el cambio que ha causado el problema era absolutamente necesario y revertirlo si no lo es. Compruebe también si el aumento de la versión de la exportación de paquetes se ha incrementado más de lo necesario, tras una estricta versión semántica.

### Interfaz de usuario de plataforma con errores {#malfunctioning-platform-ui}

En el caso de que ciertas funciones de la interfaz de usuario no funcionen correctamente después de la actualización, primero debe buscar superposiciones personalizadas de la interfaz. Algunas estructuras podrían haber cambiado y la superposición podría necesitar una actualización o estar obsoleta.

A continuación, compruebe si hay errores de JavaScript que se puedan rastrear hasta las extensiones agregadas personalizadas que están vinculadas a bibliotecas de cliente. Lo mismo puede aplicarse a las CSS personalizadas que puedan estar causando problemas en el diseño de AEM.

Finalmente, compruebe si hay una configuración incorrecta con la que Javascript podría no poder lidiar. Este suele ser el caso de extensiones desactivadas incorrectamente.

### Componentes personalizados, plantillas o extensiones de interfaz de usuario que funcionan mal {#malfunctioning-custom-components-templates-or-ui-extensions}

En la mayoría de los casos, las causas de origen de estos problemas son las mismas que para los paquetes que no se inician o los paquetes que no se instalan con la única diferencia de que el inicio de problemas se produce al utilizar los componentes por primera vez.

La manera de lidiar con el código personalizado erróneo es realizar pruebas de humo para identificar la causa. Una vez que lo encuentre, consulte las recomendaciones de esta sección [link] del artículo para ver las formas de corregirlas.

### Personalizaciones que faltan en /etc {#missing-customizations-under-etc}

`/apps` y  `/libs` se gestionan bien con la actualización, pero es  `/etc` posible que sea necesario restaurar manualmente los cambios en  `/var/upgrade/PreUpgradeBackup` después de la actualización. Asegúrese de comprobar esta ubicación para cualquier contenido que deba combinarse manualmente.

### Analizando error.log y upgrade.log {#analyzing-the-error.log-and-upgrade.log}

En la mayoría de los casos, es necesario consultar los registros para buscar errores a fin de encontrar la causa de un problema. Sin embargo, en caso de actualizaciones, también es necesario supervisar los problemas de dependencia, ya que los paquetes antiguos podrían no actualizarse correctamente.

La mejor manera de hacerlo es eliminar el error.log eliminando todos los mensajes que se espera que no estén relacionados con el problema que se está enfrentando. Puede hacerlo mediante herramientas como grep, mediante:

```shell
grep -v UnrelatedErrorString
```

Es posible que algunos mensajes de error no sean explicativos inmediatamente. En este caso, mirar el contexto en el que se producen también puede ayudar a comprender dónde se creó el error. Puede separar el error mediante:

* `grep -B` para agregar líneas antes del error;

o

* `grep -A` para agregar líneas después de.

En algunos casos también se pueden encontrar errores en los mensajes WARN, ya que puede haber casos válidos que lleven a este estado y la aplicación no siempre puede decidir si se trata de un error real. Asegúrese de consultar estos mensajes también.

### Comuníquese con la asistencia de Adobe {#contacting-adobe-support}

Si ha seguido los consejos en esta página y sigue teniendo problemas, póngase en contacto con la asistencia de Adobe. Para proporcionar la mayor información posible al ingeniero de soporte técnico que trabaja en su caso, asegúrese de incluir el archivo upgrade.log de su actualización.
