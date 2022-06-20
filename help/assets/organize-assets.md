---
title: Organizar sus recursos digitales
description: Organice los recursos digitales, las imágenes, los archivos, las carpetas, etc. mediante el Experience Manager.
contentOwner: AG
role: User
feature: Asset Management,Search
exl-id: d6f815b5-e4fc-4f8c-a6c1-9e50035ab9f2
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---

# Organizar sus recursos digitales {#organize-digital-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/organize-assets.html?lang=en) |
| AEM 6.5 | Este artículo |
| AEM 6.4 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/organize-assets.html?lang=en) |

Todos los recursos digitales, los metadatos y el contenido de los documentos de Microsoft Office y PDF se extraen y se pueden buscar. La búsqueda permite un filtrado sofisticado de los recursos y respeta plenamente los permisos adecuados. Los metadatos se tratan en detalle en los metadatos de Digital Asset Management.

[!DNL Experience Manager Assets] admite varias formas de organizar contenido. Puede organizarlas de forma jerárquica mediante carpetas o puede organizarlas de forma desordenada y según sea necesario, por ejemplo, mediante etiquetas. Los usuarios pueden editar etiquetas en el Editor de recursos DAM, donde se muestran subrecursos, representaciones y metadatos.

## Organizar recursos en carpetas {#organize-using-folders}

La forma más básica de organizar los recursos es guardarlos en carpetas. Es similar a organizar archivos en carpetas en nuestro sistema de archivos local. Para obtener más información sobre cómo crear y administrar carpetas, consulte [Administrar recursos](manage-assets.md). La forma en que se asignan nombres a archivos y carpetas, cómo se organizan las subcarpetas y cómo se gestionan los archivos dentro de estas carpetas puede tener un impacto significativo en la forma en que se procesan esos recursos. Al utilizar estrategias de asignación de nombres de archivos y carpetas coherentes y adecuadas, junto con prácticas recomendadas en materia de metadatos, puede aprovechar al máximo su repositorio de recursos digitales.

* En la mayoría de los casos, el repositorio de recursos digitales siempre está creciendo. Por lo tanto, es importante formalizar el uso de los metadatos, la estructura de carpetas y la nomenclatura de archivos al principio del ciclo de creación de contenido.
* Utilice carpetas solo para imponer una estructura de almacenamiento coherente para sus recursos digitales. Esta coherencia le ayuda a procesar y administrar mejor sus recursos. Por ejemplo, los recursos colocados en los siguientes tipos de carpetas pueden ayudarle a utilizar los recursos adecuados [perfiles que se utilizarán para el procesamiento de recursos](processing-profiles.md):

   * **Carpetas de desarrollo**: contiene recursos digitales en los que está trabajando.
   * **Carpetas de cliente**: contiene recursos digitales basados en clientes o nombres de proyectos.
   * **Carpetas principales**: contiene recursos digitales originales.
   * **Carpetas de representación**: contiene representaciones y copias de los recursos digitales de origen originales.
   * **Carpetas de tamaño de archivo**: contiene recursos digitales basados en tamaños de archivo pequeños, medianos o grandes.
   * **Carpetas de ensayo**: contiene recursos digitales listos para publicarse en el sitio web.
   * **Carpetas de tipo MIME**: contiene recursos digitales específicos de tipos MIME, como imágenes, documentos y multimedia.
   * **Archivar carpetas**: contiene activos digitales retirados.
   * **Carpetas basadas en fechas**: contiene recursos digitales basados en una fecha de creación o una fecha de última modificación.

* Cree un directorio de carpetas que no es probable que cambien para que cualquier personalización o automatización siga funcionando. Por ejemplo, los perfiles de procesamiento asignados siguen funcionando.
* Si un recurso ya está publicado, utilice [!DNL Experience Manager] para mover el recurso a otra carpeta y volver a publicar desde su nueva ubicación, la ubicación del recurso publicado originalmente sigue estando disponible, junto con el recurso recién republicado. Sin embargo, el recurso publicado originalmente es *perdido* a [!DNL Experience Manager] y no se pueden cancelar. Por lo tanto, se recomienda cancelar la publicación de un recurso y moverlo a una carpeta diferente.

## Organización de recursos mediante etiquetas {#use-tags-to-organize-assets}

Mediante etiquetas, como metadatos, puede buscar fácilmente recursos, crear colecciones utilizando los resultados de búsqueda, mejorar la clasificación de algunos recursos y aprovechar los algoritmos de IA de Adobe Sensei para la detección de recursos.

[!DNL Adobe Experience Manager Assets] utiliza un algoritmo de autoaprendizaje para crear etiquetas altamente descriptivas que le permitan encontrar el recurso adecuado en tan solo unos clics. El etiquetado inteligente utiliza Adobe Sensei, nuestra inteligencia artificial y nuestro marco de aprendizaje automático, que se puede entrenar para reconocer y aplicar etiquetas estándar y específicas del negocio a las imágenes. Las etiquetas inteligentes también pueden identificar contenido, palabras individuales o frases y aplicar automáticamente etiquetas descriptivas a los recursos

Para obtener más información, consulte los siguientes artículos:

* [Acerca de las etiquetas en el Experience Manager](/help/sites-authoring/tags.md)
* [Editar metadatos de recursos](metadata.md)
* [Etiquetas inteligentes mejoradas en recursos](enhanced-smart-tags.md)

## Organizar como colecciones {#organize-as-collections}

Con colecciones de recursos en [!DNL Experience Manager Assets], puede optimizar la capacidad de crear, editar y compartir recursos entre usuarios. Cree varios tipos de colecciones en función de la forma en que las utilice, incluidas las colecciones que contienen una lista de referencia estática de recursos, carpetas y colecciones, así como las colecciones que extraen recursos en función de criterios de búsqueda.  También puede crear colecciones con recursos de distintas ubicaciones y compartirlas con varios usuarios con distintos niveles de privilegios de acceso, visualización y edición.

Para obtener más información, consulte [administrar colecciones](manage-collections.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Organizar los recursos para utilizar perfiles {#organize-to-use-profiles}

Un perfil de procesamiento contiene [!DNL Assets] comandos de procesamiento que se aplican a los recursos que se cargan en carpetas predefinidas. Los perfiles se utilizan para automatizar el procesamiento de los contenidos de una carpeta o de los recursos cargados recientemente. Puede aprovechar los perfiles para organizar mejor los recursos.

La estandarización del uso de metadatos, la asignación de nombres a archivos y la estructura de carpetas garantiza que, a medida que crezca el grupo de recursos digitales, podrá aplicar perfiles de procesamiento a las carpetas con buena precisión y coherencia.

>[!MORELIKETHIS]
>
>* [Perfiles para procesar metadatos, imágenes y vídeos](processing-profiles.md).
>* [Perfiles de metadatos](/help/assets/metadata-config.md#metadata-profiles).
>* [Perfiles de vídeo](video-profiles.md).
>* [Perfiles de imagen de Dynamic Media](image-profiles.md).

