---
title: Comparar [!DNL Assets] y ofertas de la biblioteca de medios
description: Compare [!DNL Experience Manager Assets] y las funciones de la biblioteca de medios y conozca las diferencias.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82c2df0e53e8ef595ad158ef46089d6e4964ca26
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 1%

---


# [!DNL Experience Manager Assets] frente a  [!DNL Experience Manager] Media Library  {#aem-assets-vs-aem-medialibrary}

[!DNL Adobe Experience Manager Assets] es una parte integral de la  [!DNL Experience Manager] plataforma. Esta integración suave se considera una ventaja importante de [!DNL Experience Manager] y asegura la consistencia en gestor de contenido y alta productividad para los creadores de contenido.

## ¿Qué es [!DNL Assets]? {#what-is-aem-assets}

[!DNL Assets] es una función de  [!DNL Experience Manager] que le permite administrar recursos digitales (imágenes, vídeos, documentos, clips de audio, etc.) en un repositorio basado en la Web. [!DNL Assets] incluye compatibilidad con metadatos, representaciones, buscador de recursos y la interfaz de administración.

## ¿Qué es la [!DNL Experience Manager] biblioteca de medios? {#what-is-the-aem-media-library}

La [!DNL Experience Manager] biblioteca de medios es una parte designada del repositorio de contenido [!DNL Experience Manager] WCM donde se almacenan las imágenes y otros recursos compartidos. La biblioteca de medios proporciona funciones básicas de administración de recursos digitales a WCM.

## ¿Qué puedo obtener de [!DNL Assets] que no forma parte de WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Las funciones únicas que solo están disponibles para los clientes de [!DNL Assets] son:

* La capacidad para extraer y editar metadatos que no sean título, etiquetas y descripción.
* El administrador [!DNL Assets], disponible en la pantalla de bienvenida.
* Todos los pasos del flujo de trabajo relacionados con la administración de recursos digitales, como la carga y la ingesta, la eliminación, la gestión de subrecursos, la gestión de metadatos y los perfiles de procesamiento.
* Bibliotecas que incluyen `dam` en el espacio del paquete.

El uso de estas características requiere una licencia válida de [!DNL Assets].

## ¿[!DNL Assets] está disponible como paquete separado? {#is-aem-assets-available-as-a-separate-package}

No. Para facilitar la instalación e implementación, todas las [!DNL Experience Manager] aplicaciones y complementos se entregan en un solo paquete con todas las funcionalidades incluidas. Esto no implica que tenga permiso para utilizar todas las funciones del paquete.

## Quiero editar metadatos de recursos digitales. ¿Necesito [!DNL Assets]? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Si planea editar metadatos que no sean el título, la descripción y las etiquetas, se requiere la licencia [!DNL Assets].

## Quiero usar el predicado de categoría en mi sitio web. ¿Necesito [!DNL Assets]? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Sí, el predicado de categoría forma parte de [!DNL Assets] y requiere una licencia [!DNL Assets].

## Deseo cambiar automáticamente el tamaño de las imágenes al importarlas. ¿Necesito [!DNL Assets]? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

No. El cambio de tamaño y la transformación automática de imágenes estáticas basada en el flujo de trabajo, así como la capacidad de administrar representaciones, forman parte de la biblioteca de medios [!DNL Experience Manager]. Estas funciones no requieren una licencia [!DNL Assets].

## Quiero cambiar el tamaño de las imágenes con un componente de imagen personalizado. ¿Necesito [!DNL Assets]? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

El componente de imagen forma parte de WCM. La biblioteca de gráficos que utiliza el componente de imagen (pero también [!DNL Assets]) forma parte de la plataforma [!DNL Experience Manager] y no requiere una licencia [!DNL Assets].

## ¿Cómo puedo evitar que mis usuarios utilicen [!DNL Assets] si no he obtenido la licencia [!DNL Assets]? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Puede eliminar todos los flujos de trabajo, componentes, taxonomías, opciones específicos de [!DNL Assets] y el [!DNL Assets] administrador de [!DNL Experience Manager]. Al hacerlo, evita que los usuarios utilicen accidentalmente las [!DNL Assets] funciones que no obtuvo la licencia.

## Quiero añadir imágenes a una página y recortar y cambiar el tamaño de estas imágenes. ¿Necesito [!DNL Assets]? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

En este caso de uso no es necesario comprar [!DNL Assets], ni siquiera es necesario utilizar la biblioteca de medios para usar imágenes en un sitio web, ya que el componente de imagen inteligente permite cargar imágenes directamente en la página.

## Una lista detallada de las funciones disponibles en [!DNL Assets] frente a la biblioteca de medios {#listoffeatures}

[!DNL Experience Manager Assets]

* Colecciones y caja de luz
* Administración y propiedades avanzadas de metadatos
* Vínculo de recurso de Adobe (conexión con Creative Cloud para empresas)
* [!DNL Experience Manager] aplicación de escritorio
* Perfiles de procesamiento
* [!DNL Adobe InDesign Server] integración
* Plantillas de activos y marco de productores de catálogos
* [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator]e  [!DNL Adobe InDesign] integración
* Administración de activos multilingües
* Integración de PIM
* Gestión de derechos
* Asistencia Camera Raw
* Administración y configuración de facetas de búsqueda
* Flujos de trabajo DAM previamente compilados (por ejemplo, sesión fotográfica)
* Sistema de informes y análisis de recursos llamados perspectivas
* Gestión de activos 3D
* Recursos conectados
* Brand Portal
* Acceso de autoservicio
* Explorar, buscar y descargar
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
* Flujo de actividad (escala de tiempo)
* Consulta Builder (API)
* Integración de Marketing Cloud
* Personalización y extensión de la interfaz de usuario
* Comentarios y anotaciones

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 Descripción del producto de Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 Descripción del producto in situ](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)

