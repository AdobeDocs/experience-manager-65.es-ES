---
title: Organizar sus recursos digitales
description: Organice sus recursos digitales, imágenes, archivos, carpetas, etc. mediante Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 1%

---


# Organizar sus recursos digitales {#organize-digital-assets}

Todos los recursos digitales, los metadatos y el contenido de los documentos de Microsoft Office y PDF se extraen y permiten realizar búsquedas. La búsqueda permite un filtrado sofisticado de los recursos y respeta plenamente los permisos adecuados. Los metadatos se tratan en detalle en Administración de activos digitales.

[!DNL Experience Manager Assets] admite varias formas de organizar contenido. Puede organizarlas jerárquicamente mediante carpetas o bien puede organizarlas de forma no ordenada y ad-hoc, por ejemplo mediante etiquetas. Los usuarios pueden editar etiquetas en el Editor de recursos de DAM, donde se muestran subrecursos, representaciones y metadatos.

## Organizar recursos en carpetas {#organize-using-folders}

La forma más básica de organizar los recursos es guardarlos en carpetas. Es similar a organizar archivos en carpetas en nuestro sistema de archivos local. Para obtener más información sobre cómo crear y administrar carpetas, consulte [Administrar recursos](manage-assets.md). La forma en que se asignan nombres a los archivos y las carpetas, la forma en que se organizan las subcarpetas y la forma en que se gestionan los archivos dentro de estas carpetas puede tener un impacto significativo en la forma en que se procesan dichos recursos. Al utilizar estrategias de asignación de nombres de archivos y carpetas coherentes y adecuadas, junto con buenas prácticas de metadatos, puede aprovechar al máximo el repositorio de recursos digitales.

* En la mayoría de los casos, el repositorio de recursos digitales siempre está creciendo. Por lo tanto, es importante formalizar el uso de metadatos, la estructura de carpetas y la nominación de archivos al principio del ciclo de creación de contenido.
* Utilice las carpetas únicamente para imponer una estructura de almacenamiento uniforme a los recursos digitales. Esta coherencia ayuda a procesar y administrar mejor los recursos. Por ejemplo, los recursos colocados en los siguientes tipos de carpetas pueden ayudarle a utilizar los [perfiles adecuados para el procesamiento de recursos](processing-profiles.md):

   * **Carpetas** de desarrollo: contiene recursos digitales en los que está trabajando.
   * **Carpetas** de cliente: contiene recursos digitales basados en nombres de clientes o proyectos.
   * **Carpetas** principales: contiene recursos digitales originales.
   * **Carpetas** de representación: contiene representaciones y copias de los recursos digitales originales.
   * **Carpetas** de tamaño de archivo: contiene recursos digitales basados en tamaños de archivo pequeños, medianos o grandes.
   * **Carpetas** de ensayo: contiene recursos digitales que están listos para publicarse en directo en el sitio web.
   * **Carpetas** de tipo MIME: contiene recursos digitales específicos de tipos MIME como imágenes, documentos y multimedia.
   * **Archivar carpetas**: contiene activos digitales retirados.
   * **Carpetas** basadas en fecha: contiene recursos digitales basados en una fecha de creación o en una fecha de última modificación.

* Cree un directorio de carpetas que no es probable que cambien para que la personalización o la automatización sigan funcionando. Por ejemplo, los perfiles de procesamiento asignados siguen funcionando.
* Si ya se ha publicado un recurso, utilice [!DNL Experience Manager] para moverlo a otra carpeta y volver a publicarlo desde su nueva ubicación, la ubicación original del recurso publicado seguirá estando disponible, junto con el recurso recién republicado. Sin embargo, el recurso publicado original se *pierde* en [!DNL Experience Manager] y no se puede cancelar la publicación. Por lo tanto, como práctica recomendada, primero debe cancelar la publicación de un recurso y, a continuación, moverlo a otra carpeta.

## Organizar recursos con etiquetas {#use-tags-to-organize-assets}

Mediante el uso de etiquetas como metadatos, puede buscar fácilmente recursos, crear colecciones utilizando los resultados de búsqueda, mejorar la clasificación de la búsqueda de algunos recursos y aprovechar los algoritmos de IA de Adobe Sensei para la detección de recursos.

[!DNL Adobe Experience Manager Assets] utiliza un algoritmo de autoaprendizaje para crear etiquetas muy descriptivas que le permiten encontrar el recurso correcto en tan solo unos clics. El etiquetado inteligente utiliza Adobe Sensei, nuestra inteligencia artificial y nuestro sistema de aprendizaje automático, que se puede capacitar para reconocer y aplicar a las imágenes etiquetas estándar y específicas del negocio. Las etiquetas inteligentes también pueden identificar contenido, palabras individuales o frases y aplicar automáticamente etiquetas descriptivas a los recursos

Para obtener más información, consulte los siguientes artículos:

* [Acerca de las etiquetas en el Experience Manager](/help/sites-authoring/tags.md)
* [Editar metadatos de recursos](metadata.md)
* [Etiquetas inteligentes mejoradas en los recursos](enhanced-smart-tags.md)

## Organizar como colecciones {#organize-as-collections}

Con las colecciones de recursos en [!DNL Experience Manager Assets], puede optimizar la capacidad de crear, editar y compartir recursos entre usuarios. Cree varios tipos de colecciones en función de su uso, incluidas las colecciones que contienen una lista de referencia estática de recursos, carpetas y colecciones, así como las colecciones que extraen recursos en función de criterios de búsqueda.  También puede crear colecciones con recursos de distintas ubicaciones y compartirlas con varios usuarios con diferentes niveles de acceso, visualización y edición de privilegios.

Para obtener más información, consulte [administración de colecciones](manage-collections.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Organizar los recursos para utilizar perfiles {#organize-to-use-profiles}

Un perfil de procesamiento contiene [!DNL Assets] comandos de procesamiento que se aplican a los recursos que se cargan en carpetas predefinidas. Los perfiles se utilizan para automatizar el procesamiento del contenido de una carpeta o de los recursos que se han cargado recientemente. Puede aprovechar los perfiles para organizar mejor los recursos.

La estandarización del uso de metadatos, la nominación de archivos y la estructura de carpetas garantiza que, a medida que crezca el grupo de recursos digitales, podrá aplicar perfiles de procesamiento a las carpetas con buena precisión y coherencia.

>[!MORELIKETHIS]
>
>* [Perfiles para procesar metadatos, imágenes y vídeos](processing-profiles.md).
>* [Perfiles de metadatos](/help/assets/metadata-config.md#metadata-profiles).
>* [Perfiles](video-profiles.md) de vídeo.
>* [perfiles](image-profiles.md) de imagen de Dynamic Media.

