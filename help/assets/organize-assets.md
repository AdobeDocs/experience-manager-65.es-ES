---
title: Organizar sus recursos digitales
description: Organice sus recursos digitales, imágenes, archivos, carpetas, etc. mediante Experience Manager.
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

Todos los recursos digitales, metadatos y contenido de los documentos de Microsoft Office y PDF se extraen y se pueden buscar. La búsqueda permite un filtrado sofisticado de los recursos y respeta plenamente los permisos adecuados. Los metadatos se tratan en detalle en Metadatos en Digital Asset Management.

[!DNL Experience Manager Assets] admite varias formas de organizar el contenido. Puede organizarlas de forma jerárquica utilizando carpetas o puede organizarlas de forma desordenada y ad hoc, utilizando por ejemplo etiquetas. Los usuarios pueden editar etiquetas en el editor de recursos DAM, donde se muestran subrecursos, representaciones y metadatos.

## Organización de recursos en carpetas {#organize-using-folders}

La forma más básica de organizar los recursos es guardarlos en carpetas. Es análogo a organizar archivos en carpetas en nuestro sistema de archivos local. Para obtener más información sobre cómo crear y administrar carpetas, consulte [Administrar recursos](manage-assets.md). El modo de asignar nombres a los archivos y carpetas, organizar las subcarpetas y administrar los archivos de estas carpetas puede tener un impacto significativo en el modo en que se procesan esos recursos. Si utiliza estrategias de nomenclatura de archivos y carpetas coherentes y adecuadas, junto con una buena práctica de metadatos, puede sacar el máximo partido a su repositorio de recursos digitales.

* En la mayoría de los casos, el repositorio de recursos digitales siempre está creciendo. Por lo tanto, es importante formalizar el uso de metadatos, la estructura de carpetas y la nomenclatura de archivos al principio del ciclo de creación de contenido.
* Utilice carpetas únicamente para imponer una estructura de almacenamiento coherente para los recursos digitales. Esta coherencia le ayuda a procesar y administrar mejor sus recursos. Por ejemplo, los recursos colocados en los siguientes tipos de carpetas pueden ayudarle a utilizar los recursos adecuados [perfiles que se utilizarán para el procesamiento de recursos](processing-profiles.md):

   * **Carpetas de desarrollo**: contiene recursos digitales en los que está trabajando actualmente.
   * **Carpetas de cliente**: contiene recursos digitales basados en nombres de clientes o proyectos.
   * **Carpetas principales**: contiene recursos digitales originales.
   * **Representación de carpetas**: contiene representaciones y copias de los recursos digitales de origen originales.
   * **Carpetas de tamaño de archivo**: contiene recursos digitales basados en tamaños de archivo pequeños, medianos o grandes.
   * **Carpetas de ensayo**: contiene recursos digitales que están listos para publicarse en el sitio web.
   * **Carpetas de tipo MIME**: contiene recursos digitales específicos de tipos MIME, como imágenes, documentos y multimedia.
   * **Archivar carpetas**: contiene recursos digitales retirados.
   * **Carpetas basadas en fechas**: contiene recursos digitales basados en una fecha de creación o en una fecha de última modificación.

* Cree un directorio de carpetas que no tengan probabilidades de cambiar para que la personalización o automatización sigan funcionando. Por ejemplo, los perfiles de procesamiento asignados siguen funcionando.
* Si un recurso ya se ha publicado, utilice [!DNL Experience Manager] para mover el recurso a otra carpeta y volver a publicar desde su nueva ubicación, la ubicación del recurso publicado original aún está disponible junto con el recurso recién vuelto a publicar. Sin embargo, el recurso publicado original es *perdido* hasta [!DNL Experience Manager] y no se puede cancelar su publicación. Por lo tanto, como práctica recomendada, primero debe cancelar la publicación de un recurso y, a continuación, moverlo a una carpeta diferente.

## Organización de recursos mediante etiquetas {#use-tags-to-organize-assets}

Con las etiquetas, como metadatos, puede buscar recursos fácilmente, crear colecciones utilizando los resultados de búsqueda, aumentar la clasificación de búsqueda de algunos recursos y aprovechar los algoritmos de IA de Adobe Sensei para la detección de recursos.

[!DNL Adobe Experience Manager Assets] utiliza un algoritmo de autoaprendizaje para crear etiquetas altamente descriptivas que le permiten encontrar el recurso correcto en solo unos clics. El etiquetado inteligente utiliza Adobe Sensei, nuestro entorno de aprendizaje automático e inteligencia artificial, que puede formarse para reconocer y aplicar etiquetas estándar y específicas de la empresa a las imágenes. Las etiquetas inteligentes también pueden identificar contenido, palabras o frases individuales y aplicar automáticamente etiquetas descriptivas a los recursos

Para obtener más información, consulte los siguientes artículos:

* [Acerca de las etiquetas en Experience Manager](/help/sites-authoring/tags.md)
* [Editar metadatos de recursos](metadata.md)
* [Etiquetas inteligentes mejoradas en Assets](enhanced-smart-tags.md)

## Organizar como colecciones {#organize-as-collections}

Con colecciones de recursos en [!DNL Experience Manager Assets], puede optimizar la capacidad de crear, editar y compartir recursos entre usuarios. Cree varios tipos de colecciones en función de su uso, incluidas las que contienen una lista de referencia estática de recursos, carpetas y colecciones, así como las colecciones que extraen recursos según los criterios de búsqueda.  También puede crear colecciones con recursos de diferentes ubicaciones y compartirlas con varios usuarios con diferentes niveles de acceso, visualización y privilegios de edición.

Para obtener más información, consulte [administrar colecciones](manage-collections.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## Organizar los recursos para utilizar perfiles {#organize-to-use-profiles}

Un perfil de procesamiento contiene [!DNL Assets] comandos de procesamiento que se aplican a los recursos que se cargan en carpetas predefinidas. Los perfiles se utilizan para automatizar el procesamiento del contenido de una carpeta o de los recursos recién cargados. Puede aprovechar los perfiles para organizar mejor los recursos.

La estandarización del uso de metadatos, los nombres de archivo y la estructura de carpetas garantiza que, a medida que el grupo de recursos digitales crezca, pueda aplicar perfiles de procesamiento a las carpetas con la buena precisión y coherencia.

>[!MORELIKETHIS]
>
>* [Perfiles para procesar metadatos, imágenes y vídeos](processing-profiles.md).
>* [Perfiles de metadatos](/help/assets/metadata-config.md#metadata-profiles).
>* [Perfiles de vídeo](video-profiles.md).
>* [Perfiles de imagen de Dynamic Media](image-profiles.md).

