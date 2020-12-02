---
title: Estado de la función de IU táctil
description: Notas de la versión específicas de [!DNL Adobe Experience Manager] IU táctil.
translation-type: tm+mt
source-git-commit: d938f52766154b68df2f6db2c8c49a0ad97e7e6d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 14%

---


# Estado de la función de IU táctil {#touch-ui-feature-status}

A partir de AEM 6.4, la [IU clásica está en desuso](../release-notes/deprecated-removed-features.md). Adobe no realizará más mejoras en la IU clásica y se recomienda a los usuarios que aprovechen las nuevas y potentes funciones disponibles en la IU táctil.

A partir de la versión 6.0, AEM ha introducido una nueva interfaz de usuario denominada &quot;IU táctil&quot; (denominada simplemente &quot;IU táctil&quot;) que se alinea con [!DNL Adobe Experience Cloud] y con las directrices generales de la interfaz de usuario de Adobe. Al alcanzarse casi la paridad de funciones, esta se ha convertido en la IU estándar en AEM con la interfaz heredada orientada al escritorio denominada &quot;IU clásica&quot;.

Aunque la mayoría de las funciones están presentes en la IU táctil, hay funciones que aún no se han completado y que se añadirán en versiones futuras.

La siguiente lista muestra el estado actual de las capacidades tal como se implementaron en la AEM 6.5.

Para obtener recomendaciones para clientes que actualizan a AEM 6.5, consulte [Recomendaciones de interfaz de usuario para clientes](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Esta página solo cubre la paridad de funciones con la IU clásica. Las funciones añadidas y exclusivas a la IU táctil que no están presentes en la IU clásica no aparecen en la lista.

>[!NOTE]
>
>Esta lista se esfuerza por ser completa, pero no es exhaustiva.

## Leyenda {#legend}

* **Completar**: La función está totalmente disponible en la IU táctil.
* **Principalmente**: La función está disponible principalmente en la IU táctil.
* **Falta**: La función no está presente en la IU táctil, la IU clásica debe utilizarse para realizar esta acción.
* **Reemplazado**: La función se reemplazó con una nueva implementación que funciona de manera diferente.
* **Eliminado**: La función ya no existe en la IU táctil y no se reemplazará.

## Estado de la función: Administración de sitios {#feature-status-sites-admin}

Es una lista de las funciones que tiene la IU clásica Administración de sitios (`/siteadmin`) y el estado en la IU táctil (`/sites.html`).

| Función | Estado | Comentario |
|--- |--- |--- |
| Navegar por la jerarquía del sitio | Completar | AEM 6.4 introdujo una [vista de árbol de contenido](/help/sites-authoring/basic-handling.md#content-tree). |
| Iniciar flujo de trabajo | Completar |  |
| Crear nueva página | Completar |  |
| Crear nuevo sitio | Completar |  |
| Crear nuevo lanzamiento | Completar |  |
| Crear nueva Live Copy | Completar |  |
| Crear carpeta | Completar |  |
| Mostrar estado de publicación | Completar | A partir de AEM 6.5, el estado del flujo de trabajo se muestra en la vista de lista. |
| Búsqueda   | Completar |  |
| Copiar y pegar página (Duplicado) | Completar |  |
| Mover páginas | Completar |  |
| Publicación de páginas | Completar |  |
| Publicación de páginas sin derechos de replicación | Completar |  |
| Publicar posteriormente | Completar |  |
| Árbol de publicaciones | Completar |  |
| Cancelar la publicación de páginas | Completar |  |
| Cancelar la publicación de páginas sin derechos de replicación | Completar |  |
| Cancelar la publicación posteriormente | Completar |  |
| Eliminar | Completar |  |
| Bloquear/Desbloquear | Completar |  |
| Vista/Editar propiedades | Completar |  |
| Definir permisos en páginas | Completar |  |
| Historial de versiones | Completar |  |
| Restaurar versión | Completar |  |
| Restaurar árbol y restaurar páginas eliminadas | Falta | Utilice la IU clásica. |
| Mostrar diferencia entre la versión antigua y la actual | Completar |  |
| Acciones de Live Copy (despliegue) | Completar |  |
| Ver copias de idioma | Completar |  |
| Buscar y reemplazar | Falta | Utilice la IU clásica. |
| Bandeja de entrada de notificaciones (eventos JCR) | Falta | Utilice la IU clásica. Se reemplazará con una implementación diferente. |
| Referencias | Completar | Visualización de los vínculos de página entrantes agregados a AEM 6.5. |

## Estado de la función: Editor de páginas {#feature-status-page-editor}

Esta es una lista de las funciones que tiene el Editor de páginas de la IU clásica (`/cf#`) y el estado en la IU táctil (`/editor.html`).

| Función | Estado | Comentario |
|--- |--- |--- |
| Editar páginas Web | Completar |  |
| Editar páginas web móviles | Completar |  |
| Editar contenido importado mediante el importador de diseños | Completar |  |
| Editar correos electrónicos | Completar |  |
| Editar aplicaciones móviles híbridas | Completar |  |
| Editar Forms | Completar |  |
| Editar Ofertas | Completar |  |
| Editar modelos de Flujos de trabajo | Completar |  |
| Modo: Editar y Previsualización | Completar |  |
| Previsualización adaptable | Completar |  |
| Modo: Editar diseño | Completar |  |
| Modo: Andamiaje | Completar |  |
| Modo: Estado de Live Copy | Completar |  |
| Añadir anotaciones | Completar |  |
| Editar propiedades | Completar |  |
| Página de despliegue | Completar |  |
| Inicio y mostrar flujo de trabajo | Completar |  |
| Entrega de paquetes de workflow | Principalmente | Totalmente accesible en la IU táctil. La carga útil de varios flujos de trabajo se sigue presentando en la IU clásica. |
| Bloquear/Desbloquear página | Completar |  |
| Publicar página | Completar |  |
| Cancelar la publicación de la página | Completar |  |
| Copiar página | Eliminado | Utilice Administración del sitio para [copiar páginas](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Mover página | Eliminado | Utilice Administración del sitio para [mover páginas](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Eliminar página | Eliminado | Utilice Administración del sitio para [eliminar páginas](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostrar referencias | Eliminado | Use Administración del sitio para ver la [lista de referencia detallada](/help/sites-authoring/author-environment-tools.md#references). |
| Registro de auditorías | Eliminado | Utilice Administración del sitio y [carril de actividad abierto](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Crear versión | Eliminado | Utilice Administración del sitio para [crear nuevas versiones](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Restaurar versión | Eliminado | Utilice Administración del sitio para [restaurar versiones](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Interruptores de inicio | Eliminado | Utilice Administración del sitio para [cambiar entre inicios](/help/sites-authoring/launches-promoting.md). |
| Traducir página | Eliminado | Utilice Administración del sitio para [agregar página a proyectos de traducción](/help/sites-administering/tc-manage.md). |
| Deformación de tiempo (elija la fecha y hora y el sitio de navegación tal y como se vio a continuación) | Completar |  |
| Definir permisos | Completar |  |
| Interfaz de usuario de ClientContext | Reemplazado | Utilice la interfaz de usuario [ContextHub](/help/sites-authoring/ch-previewing.md) a partir de ahora. |
| Buscador de contenido para los distintos tipos de medios | Completar |  |
| Lista de componentes | Completar |  |
| Copiar y pegar componentes | Completar |  |
| Lista de componentes en el portapapeles | Falta |  |
| Deshacer/Rehacer | Completar |  |
| Arrastrar contenido al marcador de posición de componente | Completar |  |
| Arrastre el contenido directamente al marcador de posición parsys con la creación automática de componentes | Completar |  |

## Estado de la función: Editores de texto, tabla e imagen {#feature-status-text-table-and-image-editors}

Es una lista de las funciones que tienen el texto, la tabla y el editor de imágenes de la IU clásica, así como el estado en la IU táctil.

| Función | Estado | Comentario |
|--- |--- |--- |
| Editor de texto enriquecido | Completar | Se puede utilizar in-situ, en cuadro de diálogo y en pantalla completa. |
| Habilitar/deshabilitar complementos RTE | Completar | Se puede hacer con el [Editor de plantillas](/help/sites-authoring/templates.md). |
| Usar RTE para texto sin formato | Completar |  |
| Complemento RTE: Vínculos y anclaje | Completar |  |
| Complemento RTE: Mapa de caracteres | Completar |  |
| Complemento RTE: Copiar/Pegar | Completar |  |
| Complemento RTE: Pegar desde Microsoft Word | Completar |  |
| Complemento RTE: Buscar y reemplazar | Completar |  |
| Complemento RTE: Formatos de texto (negrita, ...) | Completar |  |
| Complemento RTE: Subíndice y superíndice | Completar |  |
| Complemento RTE: Justificar | Completar |  |
| Complemento RTE: Listas (viñetas / números) | Completar |  |
| Complemento RTE: Formato de párrafo | Completar |  |
| Complemento RTE: Estilos de texto | Completar |  |
| Complemento RTE: Editor de origen (Editar HTML) | Completar | Solo disponible en cuadro de diálogo y pantalla completa. |
| Complemento RTE: Corrector ortográfico | Completar |  |
| Complemento RTE: Tabla (Editor de tablas incrustado) | Completar |  |
| Complemento RTE: Deshacer/Rehacer | Completar |  |
| Complemento RTE: Permitir imágenes en línea | Completar |  |
| Editor de tablas | Completar | Se puede utilizar in-situ, en cuadro de diálogo y en pantalla completa. |
| Arrastrar imagen a celda de tabla | Completar | Utilizable en línea |
| Editor de imágenes | Completar | Se puede utilizar in-situ, en cuadro de diálogo y en pantalla completa. |
| Habilitar/deshabilitar complementos IPE | Completar | AEM 6.3 introdujo una interfaz de usuario en el [Editor de plantillas](/help/sites-authoring/templates.md). |
| Complemento IPE: Recortar | Completar |  |
| Complemento IPE: Voltear | Completar |  |
| Complemento IPE: Deshacer/Rehacer | Completar |  |
| Complemento IPE: Mapa de imagen | Completar |  |
| Complemento IPE: Rotar | Completar |  |
| Complemento IPE: Zoom | Completar |  |

## Estado de la función: Herramientas {#feature-status-tools}

Esta es una lista de varias herramientas que tiene la IU clásica y del estado de la IU táctil.

| Función | Estado | Comentario |
|--- |--- |--- |
| Administración de tareas | Reemplazado | 6.0 presentó proyectos y tareas. |
| Bandeja de entrada de workflow | Completar |  |
| Configuración de plantilla de flujo de trabajo a página (`/etc/workflow/wcm/templates.html`) | Falta | Utilice la IU clásica. |
| Etiquetado de la IU de administración | Completar |  |
| Centro de control de MSM/modelo | Completar |  |
| IU del Administrador de modelos | Completar |  |
| Interfaz de usuario de configuración de despliegue | Falta | Utilice la IU clásica. |
| Interfaz de usuario, grupos y permisos | Finalizado principalmente | Para editar permisos avanzados, utilice la IU clásica. |
| Purgar versiones (`/etc/versioning/purge.html`) | Falta | Utilice la IU clásica. |
| Comprobador de vínculos externos (`/etc/linkchecker.html`) | Falta | Utilice la IU clásica. |
| Editor masivo (`/etc/importers/bulkeditor.html`) | Falta | Utilice la IU clásica. |
| Cargar miniaturas para agregarlas o sobrescribirlas | Falta | Utilice la IU clásica. |
