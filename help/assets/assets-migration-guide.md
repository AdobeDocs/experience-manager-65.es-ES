---
title: Migración masiva de recursos a Recursos Adobe Experience Manager
description: Describe cómo incorporar recursos a AEM, aplicar metadatos, generar representaciones y activarlos para publicar instancias.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Cómo migrar recursos de forma masiva {#assets-migration-guide}

Al migrar recursos a AEM, hay que tener en cuenta varios pasos. La extracción de recursos y metadatos de su página principal actual está fuera del ámbito de este documento, ya que varía considerablemente entre implementaciones, pero este documento describe cómo incorporar estos recursos a AEM, aplicar sus metadatos, generar representaciones y activarlos para publicar instancias.

## Requisitos previos {#prerequisites}

Antes de realizar realmente cualquiera de los pasos de esta metodología, revise e implemente las directrices en consejos [de ajuste del rendimiento de](performance-tuning-guidelines.md)los activos. Muchos de los pasos, como la configuración de los trabajos simultáneos máximos, mejoran considerablemente la estabilidad del servidor y el rendimiento bajo carga. Otros pasos, como la configuración de un almacén de datos de archivos, son mucho más difíciles de realizar después de cargar el sistema con los recursos.

>[!NOTE]
>
>Las siguientes herramientas de migración de recursos no forman parte de AEM y no son compatibles con Adobe:
>
>* ACS AEM Tools Tag Maker
>* Importador de recursos CSV de herramientas AEM de ACS
>* ACS Commons Bulk Workflow Manager
>* ACS Commons Fast Action Manager
>* Flujo de trabajo sintético
>
>
Este software es de código abierto y está cubierto por la Licencia [de](https://adobe-consulting-services.github.io/pages/license.html)Apache v2. Para hacer una pregunta o informar de un problema, visite los respectivos [problemas de GitHub para ACS AEM Tools](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) y [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## Migrar a AEM {#migrating-to-aem}

La migración de recursos a AEM requiere varios pasos y debe verse como un proceso por fases. Las fases de la migración son las siguientes:

1. Desactive los flujos de trabajo.
1. Cargar etiquetas.
1. Ingesta de recursos.
1. Procesar representaciones.
1. Activar recursos.
1. Habilitar flujos de trabajo.

![chlimage_1-223](assets/chlimage_1-223.png)

### Deshabilitar flujos de trabajo {#disabling-workflows}

Antes de iniciar la migración, deshabilite los lanzadores para el flujo de trabajo de recursos de actualización de DAM. Es mejor ingerir todos los recursos en el sistema y, a continuación, ejecutar los flujos de trabajo por lotes. Si ya está activo durante la migración, puede programar estas actividades para que se ejecuten en horas de inactividad.

### Cargar etiquetas {#loading-tags}

Es posible que ya tenga una taxonomía de etiquetas en su lugar de aplicación a las imágenes. Aunque las herramientas como el importador de recursos CSV y la compatibilidad de AEM con los perfiles de metadatos pueden automatizar el proceso de aplicación de etiquetas a los recursos, las etiquetas deben cargarse en el sistema. La función [ACS Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) permite rellenar etiquetas mediante una hoja de cálculo de Microsoft Excel que se carga en el sistema.

### Recursos de entrada {#ingesting-assets}

El rendimiento y la estabilidad son cuestiones importantes que se deben tener en cuenta a la hora de transferir recursos al sistema. Dado que está cargando una gran cantidad de datos en el sistema, debe asegurarse de que el sistema funciona lo mejor posible para minimizar la cantidad de tiempo necesaria y evitar sobrecargar el sistema, lo que puede provocar un bloqueo del sistema, especialmente en sistemas que ya están en producción.

Existen dos métodos para cargar los recursos en el sistema: un enfoque basado en push que utiliza HTTP o un método basado en extracción que utiliza las API de JCR.

#### Enviar a través de HTTP {#pushing-through-http}

El equipo de servicios gestionados de Adobe utiliza una herramienta llamada Glutton para cargar datos en entornos de clientes. Glutton es una pequeña aplicación Java que carga todos los recursos de un directorio en otro directorio en una instancia de AEM. En lugar de utilizar Glutton, también puede utilizar herramientas como scripts Perl para publicar los recursos en el repositorio.

Existen dos aspectos negativos principales a la hora de utilizar el método de pasar por https:

1. Los recursos deben transmitirse a través de HTTP al servidor. Esto requiere un poco de sobrecarga y requiere mucho tiempo, lo que prolonga el tiempo necesario para realizar la migración.
1. Si tiene etiquetas y metadatos personalizados que deben aplicarse a los recursos, este método requiere un segundo proceso personalizado que debe ejecutarse para aplicar estos metadatos a los recursos una vez importados.

El otro método para la ingesta de recursos es extraer recursos del sistema de archivos local. Sin embargo, si no puede obtener una unidad externa o un recurso compartido de red montados en el servidor para realizar un método basado en extracción, la mejor opción es publicar los recursos a través de HTTP.

#### Buscar desde el sistema de archivos local {#pulling-from-the-local-filesystem}

El importador [de recursos CSV de las herramientas de AEM de](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) ACS extrae recursos del sistema de archivos y los metadatos de los recursos de un archivo CSV para la importación de recursos. La API de AEM Asset Manager se utiliza para importar los recursos al sistema y aplicar las propiedades de metadatos configuradas. Idealmente, los recursos se montan en el servidor mediante un montaje de archivo de red o a través de una unidad externa.

Dado que no es necesario transmitir los recursos a través de una red, el rendimiento general mejora considerablemente y este método se considera generalmente la forma más eficaz de cargar los recursos en el repositorio. Además, como la herramienta admite la ingestión de metadatos, puede importar todos los recursos y metadatos en un solo paso en lugar de crear un segundo paso para aplicar los metadatos mediante una herramienta independiente.

### Procesar representaciones {#processing-renditions}

Después de cargar los recursos en el sistema, debe procesarlos mediante el flujo de trabajo de recursos de actualización de DAM para extraer metadatos y generar representaciones. Antes de realizar este paso, debe duplicar y modificar el flujo de trabajo de recursos de actualización de DAM para adaptarlo a sus necesidades. El flujo de trabajo integrado contiene muchos pasos que puede no necesitar, como la generación de PTIFF de Scene7 o la integración del servidor de InDesign.

Después de configurar el flujo de trabajo según sus necesidades, tiene dos opciones para ejecutarlo:

1. El enfoque más sencillo es [ACS Commons&#39;Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). Esta herramienta le permite ejecutar una consulta y procesar los resultados de la misma a través de un flujo de trabajo. También hay opciones para configurar los tamaños de lote.
1. Puede utilizar el [ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) en conjunto con [Synth Workflows](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html). Aunque este enfoque está mucho más involucrado, le permite eliminar la sobrecarga del motor de flujo de trabajo de AEM y optimizar el uso de los recursos del servidor. Además, Fast Action Manager aumenta aún más el rendimiento mediante la supervisión dinámica de los recursos del servidor y la limitación de la carga colocada en el sistema. Se han proporcionado ejemplos de secuencias de comandos en la página de características de ACS Commons.

### Activar recursos {#activating-assets}

Para implementaciones que tienen un nivel de publicación, debe activar los recursos en el conjunto de publicaciones. Aunque Adobe recomienda ejecutar más de una única instancia de publicación, es más eficaz replicar todos los recursos en una única instancia de publicación y clonar dicha instancia. Al activar un gran número de recursos, después de activar un árbol, es posible que tenga que intervenir. He aquí por qué: Al desactivar las activaciones, los elementos se agregan a la cola de trabajos/eventos de Sling. Después de que el tamaño de esta cola comience a superar los 40.000 elementos aproximadamente, el procesamiento se ralentiza considerablemente. Después de que el tamaño de esta cola supere los 100.000 elementos, la estabilidad del sistema empezará a verse afectada.

Para solucionar este problema, puede utilizar el Administrador de acciones [rápidas](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) para administrar la replicación de recursos. Esto funciona sin utilizar las colas de Sling, lo que reduce la sobrecarga y reduce la carga de trabajo para evitar que el servidor se sobrecargue. En la página de documentación de la función se muestra un ejemplo de uso de FAM para administrar la replicación.

Otras opciones para obtener recursos en el conjunto de servidores de publicación incluyen el uso de [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) o [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run), que se proporcionan como herramientas como parte de Jackrabbit. Otra opción es utilizar una herramienta de código abierto para su infraestructura de AEM llamada [Grabbit](https://github.com/TWCable/grabbit), que afirma tener un rendimiento más rápido que el de vlt.

Para cualquiera de estos enfoques, la advertencia es que los recursos de la instancia de autor no se muestran como activados. Para controlar el marcado de estos recursos con el estado de activación correcto, también debe ejecutar una secuencia de comandos para marcar los recursos como activados.

>[!NOTE]
>
>Adobe no mantiene ni admite Grabbit.

### Clonar publicación {#cloning-publish}

Una vez activados los recursos, puede clonar la instancia de publicación para crear tantas copias como sea necesario para la implementación. Clonar un servidor es bastante sencillo, pero hay que recordar algunos pasos importantes. Para clonar la publicación:

1. Realice una copia de seguridad de la instancia de origen y del almacén de datos.
1. Restaure la copia de seguridad de la instancia y del almacén de datos en la ubicación de destino. Los siguientes pasos hacen referencia a esta nueva instancia.
1. Realice una búsqueda del sistema de archivos en `crx-quickstart/launchpad/felix` busca de `sling.id`. Elimine este archivo.
1. En la ruta raíz del almacén de datos, busque y elimine `repository-XXX` los archivos.
1. Edite `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` y `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` señale la ubicación del almacén de datos en el nuevo entorno.
1. Inicie el entorno.
1. Actualice la configuración de cualquier agente de replicación en los autores para que señale a las instancias de publicación correctas o a los agentes de vaciado del despachante en la nueva instancia para que señalen a los despachantes correctos para el nuevo entorno.

### Habilitar flujos de trabajo {#enabling-workflows}

Una vez completada la migración, los lanzadores de los flujos de trabajo de recursos de actualización de DAM deben volver a habilitarse para admitir la generación de representaciones y la extracción de metadatos para el uso diario del sistema.

## Migrar entre implementaciones de AEM {#migrating-between-aem-instances}

Aunque no es tan común, a veces es necesario migrar grandes cantidades de datos de una instancia de AEM a otra; por ejemplo, al realizar una actualización de AEM, actualizar el hardware o migrar a un nuevo centro de datos, como con una migración de AMS.

En este caso, los recursos ya están rellenados con metadatos y las representaciones ya se han generado. Puede centrarse simplemente en mover recursos de una instancia a otra. Al migrar entre instancias de AEM, se realizan los siguientes pasos:

1. Deshabilitar flujos de trabajo:Como está migrando representaciones junto con nuestros recursos, desea deshabilitar los iniciadores de flujo de trabajo para DAM Update Asset.

1. Migrar etiquetas:Como ya tiene etiquetas cargadas en la instancia de AEM de origen, puede crearlas en un paquete de contenido e instalarlas en la instancia de destino.

1. Migrar recursos:Existen dos herramientas recomendadas para mover recursos de una instancia de AEM a otra:

   * **Vault Remote Copy** o vlt rcp, le permite usar vlt en una red. Puede especificar un directorio de origen y destino y vlt descarga todos los datos del repositorio de una instancia y los carga en la otra. Vlt rcp está documentado en [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit** es una herramienta de sincronización de contenido de código abierto desarrollada por Time Warner Cable para su implementación de AEM. Debido a que utiliza flujos de datos continuos, en comparación con vlt rcp, tiene una latencia menor y reclama una mejora de velocidad de dos a diez veces más rápida que vlt rcp. Grabbit también admite la sincronización de contenido delta solamente, lo que le permite sincronizar los cambios una vez que se ha completado una fase de migración inicial.

1. Activar recursos:Siga las instrucciones para [activar los recursos](#activating-assets) documentados para la migración inicial a AEM.

1. Clonar publicación:Al igual que con una nueva migración, cargar una única instancia de publicación y clonarla es más eficaz que activar el contenido en ambos nodos. Consulte Publicación [de clonación.](#cloning-publish)

1. Habilitar flujos de trabajo:Una vez completada la migración, vuelva a habilitar los lanzadores para los flujos de trabajo de recursos de actualización de DAM para admitir la generación de representaciones y la extracción de metadatos para el uso diario del sistema.
