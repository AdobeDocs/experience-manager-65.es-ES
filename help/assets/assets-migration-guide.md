---
title: Migración de recursos por lotes
description: Describe cómo incorporar recursos a [!DNL Adobe Experience Manager], aplique metadatos, genere representaciones y actívelos en instancias de publicación.
contentOwner: AG
role: Architect, Admin
feature: Migration,Renditions,Asset Management
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1791'
ht-degree: 8%

---

# Migración de recursos por lotes {#assets-migration-guide}

Al migrar recursos a [!DNL Adobe Experience Manager]Sin embargo, hay que tener en cuenta varios pasos. La extracción de recursos y metadatos de su directorio raíz actual está fuera del ámbito de este documento, ya que varía ampliamente entre implementaciones, pero este documento describe cómo incorporar estos recursos a [!DNL Experience Manager], aplique sus metadatos, genere representaciones y actívelos en instancias de publicación.

## Requisitos previos {#prerequisites}

Antes de llevar a cabo cualquiera de los pasos de esta metodología, revise e implemente las directrices de [Consejos de ajuste de rendimiento de Assets](performance-tuning-guidelines.md). Muchos de los pasos, como la configuración del máximo de trabajos simultáneos, mejoran en gran medida la estabilidad y el rendimiento del servidor bajo carga. Otros pasos, como configurar un almacén de datos de archivos, son mucho más difíciles de realizar después de cargar el sistema con recursos.

>[!NOTE]
>
>Las siguientes herramientas de migración de recursos no forman parte de [!DNL Experience Manager] y no son compatibles con el Adobe:
>
>* AEM ACS Herramientas Creador de etiquetas
>* AEM Importador de recursos CSV de herramientas de ACS
>* Administrador de flujos de trabajo masivos ACS Commons
>* Administrador de acciones rápidas de ACS Commons
>* Flujo de trabajo sintético
>
>Este software es de código abierto y está cubierto por la [Licencia de ](https://adobe-consulting-services.github.io/pages/license.html)Apache v2. Para hacer una pregunta o informar de un problema, visite los respectivos [problemas de GitHub para ACS AEM Tools](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) y [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## Migrar a [!DNL Experience Manager] {#migrating-to-aem}

Migración de recursos a [!DNL Experience Manager] requiere varios pasos y debe considerarse como un proceso por fases. Las fases de la migración son las siguientes:

1. Desactivar flujos de trabajo.
1. Cargue las etiquetas.
1. Ingesta de recursos.
1. Procesar representaciones.
1. Activar recursos.
1. Habilitar flujos de trabajo.

![chlimage_1-223](assets/chlimage_1-223.png)

### Deshabilitar flujos de trabajo {#disabling-workflows}

Antes de iniciar la migración, deshabilite los iniciadores de [!UICONTROL Recurso de actualización DAM] flujo de trabajo. Es mejor ingerir todos los recursos en el sistema y luego ejecutar los flujos de trabajo por lotes. Si ya está activo mientras se produce la migración, puede programar estas actividades para que se ejecuten fuera de horas.

### Carga de etiquetas {#loading-tags}

Es posible que ya tenga una taxonomía de etiquetas configurada que esté aplicando a sus imágenes. Mientras que herramientas como el importador de recursos CSV y [!DNL Experience Manager] la compatibilidad con perfiles de metadatos puede automatizar el proceso de aplicación de etiquetas a los recursos, por lo que las etiquetas deben cargarse en el sistema. El [AEM ACS Herramientas Creador de etiquetas](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) Esta función permite rellenar etiquetas utilizando una hoja de cálculo de Microsoft Excel que se carga en el sistema.

### Ingesta de recursos {#ingesting-assets}

El rendimiento y la estabilidad son preocupaciones importantes al ingerir recursos en el sistema. Dado que está cargando una gran cantidad de datos en el sistema, debe asegurarse de que el sistema funciona correctamente para minimizar el tiempo necesario y evitar sobrecargar el sistema, lo que puede provocar un bloqueo del sistema, especialmente en sistemas que ya están en producción.

Existen dos métodos para cargar los recursos en el sistema: un método basado en push con HTTP o un método basado en pull con las API de JCR.

#### Enviar a través de HTTP {#pushing-through-http}

El equipo de Managed Services de Adobe utiliza una herramienta llamada Glutton para cargar datos en entornos de clientes. Glutton es una pequeña aplicación Java que carga todos los recursos de un directorio a otro en un [!DNL Experience Manager] implementación. En lugar de Glotón, también puede utilizar herramientas como Perl scripts para publicar los recursos en el repositorio.

Existen dos desventajas principales al utilizar el método de forzar https:

1. Los recursos deben transmitirse al servidor a través de HTTP. Esto requiere bastante carga y requiere mucho tiempo, lo que prolonga el tiempo necesario para realizar la migración.
1. Si tiene etiquetas y metadatos personalizados que deben aplicarse a los recursos, este método requiere un segundo proceso personalizado que debe ejecutar para aplicar estos metadatos a los recursos una vez importados.

El otro método para la ingesta de recursos es extraer recursos del sistema de archivos local. Sin embargo, si no puede montar una unidad externa o un recurso compartido de red en el servidor para realizar un enfoque basado en extracción, la mejor opción es publicar los recursos a través de HTTP.

#### Recuperación desde el sistema de archivos local {#pulling-from-the-local-filesystem}

El [AEM Importador de recursos CSV de herramientas de ACS](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) extrae recursos del sistema de archivos y metadatos de recursos de un archivo CSV para la importación de recursos. La API de Experience Manager Asset Manager se utiliza para importar los recursos al sistema y aplicar las propiedades de metadatos configuradas. Lo ideal es que los recursos se monten en el servidor mediante un montaje de archivo de red o a través de una unidad externa.

Dado que no es necesario transmitir los recursos a través de una red, el rendimiento general mejora considerablemente y este método se considera generalmente la forma más eficaz de cargar recursos en el repositorio. Además, como la herramienta admite la ingesta de metadatos, puede importar todos los recursos y metadatos en un solo paso en lugar de crear también un segundo paso para aplicar los metadatos a través de una herramienta independiente.

### Procesar representaciones {#processing-renditions}

Después de cargar los recursos en el sistema, debe procesarlos a través de la variable [!UICONTROL Recurso de actualización DAM] para extraer metadatos y generar representaciones. Antes de realizar este paso, debe duplicar y modificar la variable [!UICONTROL Recurso de actualización DAM] flujo de trabajo para satisfacer sus necesidades. El flujo de trabajo predeterminado contiene muchos pasos que pueden no ser necesarios para usted, como la generación de PTIFF de Dynamic Media o [!DNL InDesign Server] integración.

Después de configurar el flujo de trabajo según sus necesidades, tiene dos opciones para ejecutarlo:

1. El enfoque más sencillo es [Administrador de flujos de trabajo masivos de ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). Esta herramienta permite ejecutar una consulta y procesar sus resultados a través de un flujo de trabajo. También hay opciones para configurar los tamaños de lote.
1. Puede utilizar [ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) junto con [Synth Workflows](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html). Aunque este enfoque es mucho más complicado, le permite eliminar la sobrecarga del [!DNL Experience Manager] motor de flujo de trabajo optimizando el uso de los recursos del servidor. Además, Fast Action Manager aumenta todavía más el rendimiento mediante la supervisión dinámica de los recursos del servidor y la limitación de la carga localizada en el sistema. Se han proporcionado ejemplos de secuencias de comandos en la página de características de ACS Commons.

### Activar recursos {#activating-assets}

Para implementaciones que tienen un nivel de publicación, debe activar los recursos en el conjunto de servidores de publicación. Aunque Adobe recomienda ejecutar más de una instancia de publicación, lo más eficaz es replicar todos los recursos en una sola instancia de publicación y luego clonarla. Al activar grandes cantidades de recursos, después de activar una activación de árbol, es posible que tenga que intervenir. Esta es la razón: Al activar activaciones, los elementos se añaden a la cola de trabajos/eventos de Sling. Una vez que el tamaño de esta cola empieza a superar los 40 000 elementos, el procesamiento se ralentiza considerablemente. Una vez que el tamaño de esta cola supera los 100 000 elementos, la estabilidad del sistema empieza a verse afectada.

Para solucionar este problema, puede usar la variable [Administrador de acciones rápidas](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) para administrar la replicación de recursos. Esto funciona sin utilizar las colas de Sling, lo que reduce la sobrecarga, a la vez que limita la carga de trabajo para evitar que el servidor se sobrecargue. En la página de documentación de la función se muestra un ejemplo del uso de FAM para administrar la replicación.

Otras opciones para obtener recursos en el conjunto de servidores de publicación incluyen el uso de [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) o [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run), que se proporcionan como herramientas como parte de Jackrabbit. Otra opción es utilizar una herramienta de código abierto para sus [!DNL Experience Manager] infraestructura llamada [Grabbit](https://github.com/TWCable/grabbit), que afirma tener un rendimiento más rápido que el de vlt.

Para cualquiera de estos enfoques, la advertencia es que los recursos de la instancia de creación no se muestren como activados. Para gestionar la indicación de estos recursos con el estado de activación correcto, también debe ejecutar una secuencia de comandos para marcar los recursos como activados.

>[!NOTE]
>
>Adobe no mantiene ni admite Grabbit.

### Clonar publicación {#cloning-publish}

Una vez activados los recursos, puede clonar la instancia de publicación para crear tantas copias como sean necesarias para la implementación. La clonación de un servidor es bastante sencilla, pero hay que recordar algunos pasos importantes. Para clonar la publicación:

1. Haga una copia de seguridad de la instancia de origen y del almacén de datos.
1. Restaure la copia de seguridad de la instancia y el almacén de datos en la ubicación de destino. Todos los pasos siguientes hacen referencia a esta nueva instancia.
1. Realice una búsqueda del sistema de archivos en `crx-quickstart/launchpad/felix` para `sling.id`. Elimine este archivo.
1. En la ruta raíz del almacén de datos, busque y elimine cualquier `repository-XXX` archivos.
1. Editar `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` y `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` para señalar a la ubicación del almacén de datos en el nuevo entorno.
1. Inicie el entorno.
1. Actualice la configuración de cualquier agente de replicación en los autores para que apunte a las instancias de publicación o los agentes de vaciado de Dispatcher correctos en la nueva instancia y apunte a los distribuidores correctos para el nuevo entorno.

### Habilitar flujos de trabajo {#enabling-workflows}

Una vez completada la migración, los iniciadores de [!UICONTROL Recurso de actualización DAM] los flujos de trabajo deben volver a habilitarse para que admitan la generación de representaciones y la extracción de metadatos para el uso diario del sistema.

## Migrar entre [!DNL Experience Manager] implementaciones {#migrating-between-aem-instances}

Aunque no es tan común, a veces es necesario migrar grandes cantidades de datos de uno [!DNL Experience Manager] implementación en otro; por ejemplo, al realizar una [!DNL Experience Manager] actualizar, actualizar el hardware o migrar a un nuevo centro de datos, como con una migración de AMS.

En este caso, los recursos ya se han rellenado con metadatos y ya se han generado representaciones. Puede centrarse simplemente en mover recursos de una instancia a otra. Al migrar entre [!DNL Experience Manager] Para la implementación, debe realizar los siguientes pasos:

1. Deshabilitar flujos de trabajo: dado que está migrando representaciones junto con sus recursos, desea deshabilitar los iniciadores de flujos de trabajo para [!UICONTROL Recurso de actualización DAM] flujo de trabajo.

1. Migrar etiquetas: Debido a que ya tiene etiquetas cargadas en el origen [!DNL Experience Manager] , puede crearlos en un paquete de contenido e instalarlos en la instancia de target.

1. Migrar recursos: se recomiendan dos herramientas para mover recursos de una [!DNL Experience Manager] implementación en otro:

   * **Copia remota de Vault** o vlt rcp, permite utilizar vlt en una red. Puede especificar un directorio de origen y de destino, y vlt descargará todos los datos del repositorio de una instancia y los cargará en la otra. Rcp de Vault está documentado en [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit** es una herramienta de sincronización de contenido de código abierto desarrollada por Time Warner Cable para [!DNL Experience Manager] implementación. Debido a que utiliza flujos de datos continuos, en comparación con vlt rcp, tiene una latencia más baja y reclama una mejora de velocidad de dos a diez veces más rápida que vlt rcp. Grabbit también admite la sincronización de contenido delta solamente, lo que le permite sincronizar los cambios después de completar una fase de migración inicial.

1. Activar recursos: siga las instrucciones para [activar recursos](#activating-assets) documentado para la migración inicial a [!DNL Experience Manager].

1. Clonar publicación: al igual que con una nueva migración, cargar una sola instancia de publicación y clonarla es más eficaz que activar el contenido en ambos nodos. Consulte [Clonando publicación.](#cloning-publish)

1. Habilitar flujos de trabajo: una vez completada la migración, vuelva a habilitar los iniciadores para [!UICONTROL Recurso de actualización DAM] flujo de trabajo para admitir la generación de representaciones y la extracción de metadatos para el uso diario continuo del sistema.
