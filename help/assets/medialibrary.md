---
title: Comparar [!DNL Assets] y las ofertas de la biblioteca multimedia
description: Compare [!DNL Experience Manager Assets] y las funciones de la biblioteca multimedia y conozca las diferencias.
contentOwner: AG
role: Arquitecto, Encabezado
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 1%

---


# [!DNL Experience Manager Assets] frente a  [!DNL Experience Manager] Media Library  {#aem-assets-vs-aem-medialibrary}

[!DNL Adobe Experience Manager Assets] forma parte integral de la  [!DNL Experience Manager] plataforma. Esta integración sin problemas se considera una ventaja importante de [!DNL Experience Manager] y garantiza la coherencia en la administración de contenido y una alta productividad para los autores de contenido.

## ¿Qué es [!DNL Assets]? {#what-is-aem-assets}

[!DNL Assets] es una capacidad de  [!DNL Experience Manager] que le permite administrar recursos digitales (imágenes, vídeos, documentos, clips de audio y más) en un repositorio basado en web. [!DNL Assets] incluye compatibilidad con metadatos, representaciones, buscador de recursos y la interfaz de administración.

## ¿Qué es la [!DNL Experience Manager] Biblioteca de medios? {#what-is-the-aem-media-library}

La [!DNL Experience Manager] Biblioteca de medios es una parte designada del repositorio de contenido [!DNL Experience Manager] WCM donde se almacenan las imágenes y otros recursos compartidos. La biblioteca de medios proporciona funciones básicas de administración de recursos digitales a WCM.

## ¿Qué obtengo de [!DNL Assets] que no forma parte de WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Las funciones únicas que solo están disponibles para los clientes de [!DNL Assets] son:

* La capacidad de extraer y editar metadatos que no sean título, etiquetas y descripción.
* El [!DNL Assets] administrador, disponible en la pantalla de bienvenida.
* Todos los pasos del flujo de trabajo relacionados con la administración de recursos digitales, como la carga y la ingesta, la eliminación, la gestión de subrecursos, la administración de metadatos y los perfiles de procesamiento.
* Bibliotecas que incluyen `dam` en el espacio del paquete.

El uso de estas funciones requiere una licencia válida de [!DNL Assets].

## ¿Está [!DNL Assets] disponible como paquete independiente? {#is-aem-assets-available-as-a-separate-package}

No. Para facilitar la instalación y la implementación, todas las [!DNL Experience Manager] aplicaciones y complementos se entregan en un solo paquete con todas las funcionalidades incluidas. Esto no implica que tenga permiso para utilizar todas las funciones del paquete.

## Quiero editar metadatos de recursos digitales. ¿Necesito [!DNL Assets]? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Si planea editar metadatos que no sean título, descripción y etiquetas, debe obtener la licencia [!DNL Assets].

## Quiero usar el predicado de categoría en mi sitio web. ¿Necesito [!DNL Assets]? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Sí, el predicado de categoría forma parte de [!DNL Assets] y requiere una licencia [!DNL Assets].

## Quiero cambiar automáticamente el tamaño de las imágenes al importarlas. ¿Necesito [!DNL Assets]? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

No. El cambio de tamaño y la transformación automática, impulsada por el flujo de trabajo, de las imágenes estáticas, así como la capacidad de administrar representaciones, forman parte de la [!DNL Experience Manager] Biblioteca de medios. Estas funciones no requieren una licencia [!DNL Assets].

## Quiero cambiar el tamaño de las imágenes mediante un componente de imagen personalizado. ¿Necesito [!DNL Assets]? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

El componente de imagen forma parte de WCM. La biblioteca de gráficos que utiliza el componente de imagen (pero también [!DNL Assets]) forma parte de la plataforma [!DNL Experience Manager] y no requiere una licencia [!DNL Assets].

## ¿Cómo puedo evitar que mis usuarios utilicen [!DNL Assets] si no he obtenido la licencia [!DNL Assets]? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Puede eliminar todos los flujos de trabajo, componentes, taxonomías, opciones y el administrador [!DNL Assets] específicos de [!DNL Assets] de [!DNL Experience Manager]. De hacerlo, evitará que los usuarios utilicen accidentalmente las características [!DNL Assets] que no obtuvo licencia.

## Quiero añadir imágenes a una página y recortar y cambiar el tamaño de estas imágenes. ¿Necesito [!DNL Assets]? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

Para este caso de uso no es necesario comprar [!DNL Assets], ni siquiera es necesario el uso de la biblioteca multimedia para utilizar imágenes en un sitio web, ya que el componente de imagen inteligente permite cargar imágenes directamente en la página.

## Una lista detallada de las funciones disponibles en [!DNL Assets] frente a la biblioteca multimedia {#listoffeatures}

[!DNL Experience Manager Assets]

* Colecciones y lightbox
* Administración y propiedades de metadatos avanzadas
* Adobe Asset Link (conectar con el Creative Cloud de Enterprise)
* Aplicación de escritorio de [!DNL Experience Manager] 
* Perfiles de procesamiento
* [!DNL Adobe InDesign Server] integración
* Plantillas de recursos y marco de producción de catálogos
* [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator]e  [!DNL Adobe InDesign] integración
* Gestión de recursos multilingües
* Integración de PIM
* Gestión de derechos
* compatibilidad Camera Raw
* Administración y configuración de facetas de búsqueda
* Flujos de trabajo DAM creados previamente (por ejemplo, sesión fotográfica)
* Informes y análisis de recursos llamados Insights
* Administración de recursos 3D
* Recursos conectados
* Brand Portal
* Acceso a autoservicio
* Examinar, buscar y descargar
* Colecciones y uso compartido de carpetas
* Herramientas de administración e interfaz
* Etiquetado inteligente
* Búsqueda visual

**Biblioteca de medios**

* Propiedades de metadatos básicas
* Administración de etiquetas
* Control de versiones
* Representaciones estáticas
* Proyectos, tareas, creación de flujos de trabajo
* Flujo de actividad (línea de tiempo)
* Generador de consultas (API)
* Integración de Marketing Cloud
* Personalización y extensión de la interfaz de usuario
* Comentarios y anotaciones

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 Descripción del producto de Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 Descripción del producto local](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

