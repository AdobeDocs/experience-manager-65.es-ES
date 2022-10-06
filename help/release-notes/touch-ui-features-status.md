---
title: Estado de la función de IU táctil
description: Notas de la versión específicas de [!DNL Adobe Experience Manager] IU táctil.
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 15%

---

# Estado de la función de IU táctil {#touch-ui-feature-status}

AEM 6.4 en adelante [La IU clásica está en desuso](../release-notes/deprecated-removed-features.md). El Adobe no realizará más mejoras en la IU clásica y se anima a los usuarios a aprovechar las nuevas y potentes funciones disponibles en la IU táctil.

A partir de la versión 6.0, AEM introdujo una nueva interfaz de usuario denominada &quot;IU táctil&quot; (denominada simplemente &quot;IU táctil&quot;) que se alinea con el [!DNL Adobe Experience Cloud] y a las directrices generales de la interfaz de usuario de Adobe. Con casi la paridad de funciones alcanzada, esta se ha convertido en la interfaz de usuario estándar en AEM con la interfaz heredada orientada al escritorio denominada &quot;IU clásica&quot;.

Aunque la mayoría de las funciones están presentes en la IU táctil, hay funciones que aún no se han completado y que se añadirán en futuras versiones.

La siguiente lista muestra el estado actual de las capacidades tal como se implementan en la AEM 6.5.

Para obtener recomendaciones para clientes que actualizan a AEM 6.5, consulte [Recomendaciones sobre la interfaz de usuario para los clientes](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Esta página solo cubre la paridad de características con la IU clásica. Las funciones añadidas a y exclusivas a la IU táctil que no están presentes en la IU clásica no aparecen en la lista.

>[!NOTE]
>
>Esta lista se esfuerza por ser completa, pero no exhaustiva.

## Leyenda {#legend}

* **Completar**: La función está totalmente disponible en la IU táctil.
* **Principalmente**: La función está disponible principalmente en la IU táctil.
* **Falta**: La función no está presente en la IU táctil; la IU clásica debe utilizarse para realizar esta acción.
* **Reemplazado**: La función se reemplazó con una nueva implementación que funciona de forma diferente.
* **Eliminado**: La función ya no existe en la IU táctil y no se reemplazará.

## Estado de la función: Administrador de sitios {#feature-status-sites-admin}

Esta es una lista de funcionalidades de la IU clásica Administrador del sitio (`/siteadmin`) tiene y el estado en la IU táctil (`/sites.html`).

| Función | Estado | Comentar |
|--- |--- |--- |
| Navegar por la jerarquía del sitio | Completar | AEM 6.4 introduce una [vista de árbol de contenido](/help/sites-authoring/basic-handling.md#content-tree). |
| Iniciar flujo de trabajo | Completar |  |
| Crear nueva página | Completar |  |
| Crear nuevo sitio | Completar |  |
| Crear nuevo lanzamiento | Completar |  |
| Crear nueva Live Copy | Completar |  |
| Crear carpeta | Completar |  |
| Mostrar estado de publicación | Completar | A partir de AEM 6.5, el estado del flujo de trabajo se muestra en la vista de lista. |
| Búsqueda | Completar |  |
| Copiar y pegar página (Duplicar) | Completar |  |
| Mover páginas | Completar |  |
| Publicar páginas | Completar |  |
| Publicar páginas sin derechos de replicación | Completar |  |
| Publicar posteriormente | Completar |  |
| Árbol de publicación | Completar |  |
| Cancelar la publicación de páginas | Completar |  |
| Cancelar la publicación de páginas sin derechos de replicación | Completar |  |
| Cancelar la publicación posteriormente | Completar |  |
| Eliminar | Completar |  |
| Bloquear/desbloquear | Completar |  |
| Ver/editar propiedades | Completar |  |
| Definir permisos en páginas | Completar |  |
| Historial de versiones | Completar |  |
| Restaurar versión | Completar |  |
| Restaurar árbol y restaurar páginas eliminadas | Falta | Utilice la IU clásica. |
| Mostrar diferencia entre la versión antigua y la actual | Completar |  |
| Acciones de Livecopy (lanzamiento) | Completar |  |
| Ver copias de idioma | Completar |  |
| Buscar y reemplazar | Falta | Utilice la IU clásica. |
| Bandeja de entrada de notificaciones (eventos JCR) | Falta | Utilice la IU clásica. Se reemplazará con una implementación diferente. |
| Referencias | Completar | Visualización de los vínculos de página entrantes agregados a AEM 6.5. |

## Estado de la función: Editor de página {#feature-status-page-editor}

Esta es una lista de funciones del editor de páginas de la IU clásica (`/cf#`) tiene y el estado en la opción táctil (`/editor.html`).

| Función | Estado | Comentar |
|--- |--- |--- |
| Editar páginas web | Completar |  |
| Editar páginas web móviles | Completar |  |
| Editar contenido importado mediante el importador de diseños | Completar |  |
| Editar correos electrónicos | Completar |  |
| Editar aplicaciones móviles híbridas | Completar |  |
| Editar Forms | Completar |  |
| Editar ofertas | Completar |  |
| Editar modelos de flujos de trabajo | Completar |  |
| Modo: Editar y previsualizar | Completar |  |
| Vista previa interactiva | Completar |  |
| Modo: Editar diseño | Completar |  |
| Modo: Andamiaje | Completar |  |
| Modo: Estado de Live Copy | Completar |  |
| Añadir anotaciones | Completar |  |
| Editar propiedades | Completar |  |
| Desplegar página | Completar |  |
| Iniciar y mostrar flujo de trabajo | Completar |  |
| Administración de paquetes de flujo de trabajo | Principalmente | Completamente accesible en la IU táctil. La carga útil de varios flujos de trabajo se sigue mostrando en la IU clásica. |
| Bloquear/desbloquear página | Completar |  |
| Publicar página | Completar |  |
| Cancelar la publicación de la página | Completar |  |
| Copiar página | Eliminado | Utilice el administrador del sitio para [copiar páginas](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Mover página | Eliminado | Utilice el administrador del sitio para [mover páginas](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Eliminar página | Eliminado | Utilice el administrador del sitio para [eliminar páginas](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostrar referencias | Eliminado | Utilice el administrador del sitio para ver la variable [lista de referencia detallada](/help/sites-authoring/author-environment-tools.md#references). |
| Registro de auditorías | Eliminado | Usar el administrador del sitio y [abrir carril de actividad](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Crear versión | Eliminado | Utilice el administrador del sitio para [crear nuevas versiones](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Restaurar versión | Eliminado | Utilice el administrador del sitio para [restaurar versiones](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Cambiar lanzamientos | Eliminado | Utilice el administrador del sitio para [cambiar entre lanzamientos](/help/sites-authoring/launches-promoting.md). |
| Traducir página | Eliminado | Utilice el administrador del sitio para [añadir página a proyectos de traducción](/help/sites-administering/tc-manage.md). |
| Deformación de tiempo (elija fecha/hora y busque el sitio tal y como se vio) | Completar |  |
| Definir permisos | Completar |  |
| Interfaz de usuario de Client Context | Reemplazado | Utilice la variable [ContextHub](/help/sites-authoring/ch-previewing.md) IU en adelante. |
| Buscador de contenido para los distintos tipos de medios | Completar |  |
| Lista de componentes | Completar |  |
| Copia y pegado de componentes | Completar |  |
| Lista de componentes del portapapeles | Falta |  |
| Deshacer/Rehacer | Completar |  |
| Arrastrar contenido al marcador de posición de componente | Completar |  |
| Arrastre el contenido directamente al marcador de posición parsys con la creación automática de componentes | Completar |  |

## Estado de la función: Editores de texto, tabla e imagen {#feature-status-text-table-and-image-editors}

Esta es una lista de las funciones que tienen la IU clásica Texto, Tabla y Editor de imágenes, así como el estado en la IU táctil.

| Función | Estado | Comentar |
|--- |--- |--- |
| Editor de texto enriquecido | Completar | Se puede utilizar in situ, en el cuadro de diálogo y en pantalla completa. |
| Habilitar/deshabilitar complementos RTE | Completar | Se puede realizar utilizando la variable [Editor de plantillas](/help/sites-authoring/templates.md). |
| Usar RTE para texto sin formato | Completar |  |
| Complemento RTE: Vínculos y anclaje | Completar |  |
| Complemento RTE: Mapa de caracteres | Completar |  |
| Complemento RTE: Copiar/pegar | Completar |  |
| Complemento RTE: Pegar desde Microsoft Word | Completar |  |
| Complemento RTE: Buscar y reemplazar | Completar |  |
| Complemento RTE: Formatos de texto (negrita, ...) | Completar |  |
| Complemento RTE: Subíndice y superíndice | Completar |  |
| Complemento RTE: Justificar | Completar |  |
| Complemento RTE: Listas (viñetas/números) | Completar |  |
| Complemento RTE: Formato de párrafo | Completar |  |
| Complemento RTE: Estilos de texto | Completar |  |
| Complemento RTE: Editor de origen (HTML de edición) | Completar | Solo disponible en el cuadro de diálogo y en la pantalla completa. |
| Complemento RTE: Corrector ortográfico | Completar |  |
| Complemento RTE: Tabla (Editor de tablas incrustado) | Completar |  |
| Complemento RTE: Deshacer/Rehacer | Completar |  |
| Complemento RTE: Permitir imágenes en línea | Completar |  |
| Editor de tabla | Completar | Se puede utilizar in situ, en el cuadro de diálogo y en pantalla completa. |
| Arrastrar imagen a celda de tabla | Completar | Utilizable en línea |
| Editor de imágenes | Completar | Se puede utilizar in situ, en el cuadro de diálogo y en pantalla completa. |
| Habilitar/deshabilitar complementos IPE | Completar | AEM 6.3 introdujo una interfaz de usuario en el [Editor de plantillas](/help/sites-authoring/templates.md). |
| Complemento IPE: Recortar | Completar |  |
| Complemento IPE: Girar | Completar |  |
| Complemento IPE: Deshacer/Rehacer | Completar |  |
| Complemento IPE: Mapa de imágenes | Completar |  |
| Complemento IPE: Rotar | Completar |  |
| Complemento IPE: Zoom | Completar |  |

## Estado de la función: Herramientas {#feature-status-tools}

Esta es una lista de las distintas herramientas que la IU clásica tiene y el estado en la IU táctil.

| Función | Estado | Comentar |
|--- |--- |--- |
| Administración de tareas | Reemplazado | 6.0 ha introducido Proyectos y tareas. |
| Bandeja de entrada del flujo de trabajo | Completar |  |
| Configuración de flujo de trabajo a plantilla de página (`/etc/workflow/wcm/templates.html`) | Falta | Utilice la IU clásica. |
| Etiquetado de la IU de administración | Completar |  |
| Centro de control de MSM/modelo | Completar |  |
| Interfaz de usuario del Administrador de modelos | Completar |  |
| Interfaz de usuario de configuración de lanzamiento | Falta | Utilice la IU clásica. |
| Interfaz de usuario, grupos y permisos | Finalizado principalmente | Para editar permisos avanzados, utilice la IU clásica. |
| Purgar versiones (`/etc/versioning/purge.html`) | Falta | Utilice la IU clásica. |
| Comprobador de vínculos externos (`/etc/linkchecker.html`) | Falta | Utilice la IU clásica. |
| Editor masivo (`/etc/importers/bulkeditor.html`) | Falta | Utilice la IU clásica. |
| Cargar miniaturas para agregarlas o sobrescribirlas | Falta | Utilice la IU clásica. |
