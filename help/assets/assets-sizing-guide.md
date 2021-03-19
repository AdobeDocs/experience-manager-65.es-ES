---
title: '[!DNL Assets] guía de tamaño'
description: Prácticas recomendadas para determinar métricas eficientes para estimar la infraestructura y los recursos necesarios para implementar [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Arquitecto, Administrador
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 0%

---


# [!DNL Assets] guía de tamaño  {#assets-sizing-guide}

Al cambiar el tamaño del entorno para una implementación [!DNL Adobe Experience Manager Assets], es importante asegurarse de que haya suficientes recursos disponibles en términos de disco, CPU, memoria, E/S y rendimiento de red. Para cambiar el tamaño de muchos de estos recursos es necesario conocer la cantidad de recursos que se están cargando en el sistema. Si no hay una métrica mejor disponible, puede dividir el tamaño de la biblioteca existente por la edad de la biblioteca para encontrar la tasa a la que se crean los recursos.

## Disco {#disk}

### Almacén de datos {#datastore}

Un error común que se produce al cambiar el tamaño del espacio en disco necesario para una implementación [!DNL Assets] es basar los cálculos en el tamaño de las imágenes sin procesar que se van a introducir en el sistema. De forma predeterminada, [!DNL Experience Manager] crea tres representaciones además de la imagen original para usarlas en la renderización de los elementos de la interfaz de usuario [!DNL Experience Manager]. En implementaciones anteriores, se ha observado que estas representaciones suponen el doble del tamaño de los recursos ingeridos.

La mayoría de los usuarios definen representaciones personalizadas, además de las representaciones predeterminadas. Además de las representaciones, [!DNL Assets] permite extraer subrecursos de tipos de archivo comunes, como [!DNL Adobe InDesign] y [!DNL Adobe Illustrator].

Por último, las funciones de versiones de [!DNL Experience Manager] almacenan duplicados de los recursos en el historial de versiones. Puede configurar las versiones que desea depurar con frecuencia. Sin embargo, muchos usuarios eligen conservar versiones en el sistema durante mucho tiempo, lo que consume espacio de almacenamiento adicional.

Teniendo en cuenta estos factores, necesita una metodología para calcular un espacio de almacenamiento aceptablemente preciso para almacenar los activos de los usuarios.

1. Determine el tamaño y la cantidad de recursos que se cargarán en el sistema.
1. Obtenga una muestra representativa de los recursos que se van a cargar en [!DNL Experience Manager]. Por ejemplo, si planea cargar archivos PSD, JPG, AI y PDF en el sistema, necesitará varias imágenes de muestra de cada formato de archivo. Además, estas muestras deben ser representativas de los diferentes tamaños de archivo y complejidades de las imágenes.
1. Defina las representaciones que desea utilizar.
1. Cree las variantes de representación en [!DNL Experience Manager] utilizando las aplicaciones [!DNL ImageMagick] o [!DNL Adobe Creative Cloud]. Además de las representaciones que especifican los usuarios, cree representaciones listas para usar. Para los usuarios que implementan Dynamic Media, puede utilizar el binario IC para generar las representaciones PTIFF que se almacenarán en el Experience Manager.
1. Si planea utilizar subrecursos, genéelos para los tipos de archivo correspondientes.
1. Compare el tamaño de las imágenes de salida, las representaciones y los subrecursos con las imágenes originales. Permite generar un factor de crecimiento esperado cuando se carga el sistema. Por ejemplo, si genera representaciones y subrecursos con un tamaño combinado de 3 GB después de procesar 1 GB de activos, el factor de crecimiento de la representación es 3.
1. Determine el tiempo máximo durante el cual se deben mantener las versiones de los recursos en el sistema.
1. Determine con qué frecuencia se modifican los recursos existentes en el sistema. Si [!DNL Experience Manager] se utiliza como centro de colaboración en flujos de trabajo creativos, la cantidad de cambios es alta. Si solo se cargan en el sistema los recursos finalizados, este número es mucho menor.
1. Determine cuántos recursos se cargan en el sistema cada mes. Si no está seguro, compruebe el número de recursos que están disponibles actualmente y divida el número por la edad del recurso más antiguo para calcular un número aproximado.

Al realizar los pasos anteriores, puede determinar lo siguiente:

* Tamaño sin procesar de los recursos que se van a cargar.
* Número de recursos que se van a cargar.
* Factor de crecimiento de la representación.
* Número de modificaciones de recursos realizadas por mes.
* Número de meses para mantener las versiones de los recursos.
* Número de nuevos activos cargados cada mes.
* Años de crecimiento para la asignación del espacio de almacenamiento.

Puede especificar estos números en la hoja de cálculo Tamaño de red para determinar el espacio total necesario para el almacén de datos. También es una herramienta útil para determinar el impacto de mantener versiones de recursos o modificar recursos en [!DNL Experience Manager] en el crecimiento del disco.

Los datos de ejemplo rellenados en la herramienta muestran la importancia de realizar los pasos mencionados. Si cambia el tamaño del almacén de datos basándose únicamente en las imágenes sin procesar que se están cargando (1 TB), es posible que haya subestimado el tamaño del repositorio en un factor de 15.

[Obtener archivo](assets/disk_sizing_tool.xlsx)

### Almacenes de datos compartidos {#shared-datastores}

Para grandes almacenes de datos, puede implementar un almacén de datos compartido a través de un almacén de datos de archivos compartidos en una unidad conectada a la red o a través de un almacén de datos Amazon S3. En este caso, las instancias individuales no necesitan mantener una copia de los binarios. Además, un almacén de datos compartido facilita la replicación sin binarios y ayuda a reducir el ancho de banda utilizado para replicar recursos en entornos de publicación.

#### Casos de uso {#use-cases}

El almacén de datos se puede compartir entre una instancia de autor principal y en espera para minimizar el tiempo que se tarda en actualizar la instancia en espera con los cambios realizados en la instancia principal. También puede compartir el almacén de datos entre el autor y las instancias de publicación para minimizar el tráfico durante la replicación.

#### Inconvenientes {#drawbacks}

Debido a algunos inconvenientes, no se recomienda compartir un almacén de datos en todos los casos.

#### Un solo punto de error {#single-point-of-failure}

Al tener un almacén de datos compartido, introduce un solo punto de fallo en una infraestructura. Considere un escenario en el que su sistema tiene un autor y dos instancias de publicación, cada una con su propio almacén de datos. Si alguno de ellos se bloquea, los otros dos pueden seguir ejecutándose. Sin embargo, si se comparte el almacén de datos, una única falla de disco puede eliminar toda la infraestructura. Por lo tanto, asegúrese de mantener una copia de seguridad del almacén de datos compartido desde el que pueda restaurar el almacén de datos rápidamente.

Se prefiere implementar el servicio AWS S3 para los almacenes de datos compartidos porque reduce significativamente la probabilidad de fallo en comparación con las arquitecturas de disco normales.

#### Mayor complejidad {#increased-complexity}

Los almacenes de datos compartidos también aumentan la complejidad de las operaciones, como la colección de residuos. Normalmente, la recolección de basura para un almacén de datos independiente se puede iniciar con un solo clic. Sin embargo, los almacenes de datos compartidos requieren operaciones de barrido de marca en cada miembro que utiliza el almacén de datos, además de ejecutar la colección real en un solo nodo.

Para las operaciones de AWS, la implementación de una única ubicación central (a través de Amazon S3), en lugar de crear una matriz RAID de volúmenes EBS, puede compensar de manera significativa la complejidad y los riesgos operativos del sistema.

#### Problemas de rendimiento {#performance-concerns}

Un almacén de datos compartido requiere que los binarios se almacenen en una unidad montada en red que se comparte entre todas las instancias. Dado que se accede a estos binarios a través de una red, el rendimiento del sistema se ve afectado negativamente. Puede mitigar parcialmente el impacto mediante el uso de una conexión de red rápida a una matriz rápida de discos. Sin embargo, esta es una propuesta cara. En el caso de las operaciones de AWS, todos los discos son remotos y requieren conectividad de red. Los volúmenes efímeros pierden datos cuando la instancia se inicia o se detiene.

#### Latencia {#latency}

La latencia en implementaciones S3 se introduce mediante los subprocesos de escritura en segundo plano. Los procedimientos de copia de seguridad deben tener en cuenta esta latencia. Además, los índices de Lucene pueden seguir incompletos al realizar una copia de seguridad. Se aplica a cualquier archivo con distinción de tiempo escrito en el almacén de datos S3 y al que se accede desde otra instancia.

### Almacén de nodos o almacén de documentos {#node-store-document-store}

Es difícil obtener cifras precisas de tamaño para un almacén de nodos o almacén de documentos debido a los recursos que consumen los siguientes:

* Metadatos de recursos
* Versiones de recursos
* Registros de auditoría
* Flujos de trabajo archivados y activos

Dado que los binarios se almacenan en el almacén de datos, cada binario ocupa algún espacio. La mayoría de los repositorios tienen un tamaño inferior a 100 GB. Sin embargo, puede haber repositorios más grandes de hasta 1 TB de tamaño. Además, para realizar la compactación sin conexión, se necesita suficiente espacio libre en el volumen para reescribir el repositorio compactado junto con la versión compactada previamente. Una buena regla general es cambiar el tamaño del disco a 1,5 veces el tamaño esperado para el repositorio.

Para el repositorio, utilice SSD o discos con un nivel IOPS bueno a 3000. Para eliminar las posibilidades de que IOPS introduzca cuellos de botella en el rendimiento, supervise los niveles de espera de E/S de CPU para detectar signos tempranos de problemas.

[Obtener archivo](assets/aem_environment_sizingtool.xlsx)

## Red {#network}

[!DNL Assets] tiene una serie de casos de uso que hacen que el rendimiento de la red sea más importante que en muchos de nuestros  [!DNL Experience Manager] proyectos. Un cliente puede tener un servidor rápido, pero si la conexión de red no es lo suficientemente grande como para soportar la carga de los usuarios que cargan y descargan recursos del sistema, entonces seguirá pareciendo lenta. Existe una buena metodología para determinar el punto de interrupción en la conexión de red de un usuario a [!DNL Experience Manager] en [Consideraciones sobre los recursos para la experiencia del usuario, el tamaño de las instancias, la evaluación del flujo de trabajo y la topología de red](/help/assets/assets-network-considerations.md).

## Restricciones     {#limitations}

Al dimensionar una implementación, es importante tener en cuenta las limitaciones del sistema. Si la implementación propuesta supera estas limitaciones, utilice estrategias creativas, como la partición de los recursos en varias [!DNL Assets] implementaciones.

El tamaño del archivo no es el único factor que contribuye a los problemas de falta de memoria (OOM). También depende de las dimensiones de la imagen. Puede evitar problemas con OOM proporcionando un tamaño de pila más alto al iniciar [!DNL Experience Manager].

Además, puede editar la propiedad de tamaño de umbral del componente `com.day.cq.dam.commons.handler.StandardImageHandler` en Configuration Manager para utilizar un archivo temporal intermedio bueno a cero.

## Número máximo de activos {#maximum-number-of-assets}

El límite en el número de archivos que pueden existir en un almacén de datos puede ser de 2.1 billones debido a las limitaciones del sistema de archivos. Es probable que el repositorio encuentre problemas debido a un gran número de nodos mucho antes de alcanzar el límite del almacén de datos.

Si las representaciones se generan incorrectamente, utilice la biblioteca Camera Raw. Sin embargo, en este caso, el lado más largo de la imagen no debe ser bueno de 65000 píxeles. Además, la imagen no debe contener más de 512 MP (512 x 1024 x 1024 píxeles). El tamaño del recurso no importa.

Es difícil estimar con precisión el tamaño del archivo TIFF compatible de serie con una pila específica para [!DNL Experience Manager] porque factores adicionales, como el procesamiento de la influencia del tamaño de los píxeles. Es posible que [!DNL Experience Manager] pueda procesar un archivo de tamaño predeterminado de 255 MB, pero no puede procesar un tamaño de archivo de 18 MB porque este último consta de un número inusualmente mayor de píxeles en comparación con el primero.

## Tamaño de los recursos {#size-of-assets}

De forma predeterminada, [!DNL Experience Manager] permite cargar recursos de tamaño de archivo de hasta 2 GB. Para cargar recursos muy grandes en [!DNL Experience Manager], consulte [Configuración para cargar recursos muy grandes](managing-video-assets.md#configuration-to-upload-assets-that-are-larger-than-gb).
