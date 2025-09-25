---
title: Estado de la función de la IU táctil
description: Notas de la versión específicas de la  [!DNL Adobe Experience Manager] IU táctil.
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 25bf0d64b6839afec0112ea8c9fde0510e56ccf4
workflow-type: ht
source-wordcount: '1087'
ht-degree: 100%

---

# Estado de la función de la IU táctil {#touch-ui-feature-status}

La [IU clásica de Adobe Experience Manager (AEM) 6.4 y posteriores ha quedado obsoleta](../release-notes/deprecated-removed-features.md). Adobe no está realizando más mejoras en la IU clásica y se recomienda a los usuarios utilizar las potentes nuevas funciones disponibles en la IU táctil.

A partir de la versión 6.0, AEM introdujo una nueva interfaz de usuario denominada “IU táctil”, alineada con [!DNL Adobe Experience Cloud] y con las directrices generales de la interfaz de usuario de Adobe. Una vez alcanzada la paridad de características, se ha convertido en la interfaz de usuario estándar de AEM, con la interfaz heredada orientada al escritorio y denominada “IU clásica”.

Aunque la mayoría de las funciones están presentes en la interfaz de usuario táctil, hay funciones que aún no se han completado y que se añadirán en versiones futuras.

La siguiente lista muestra el estado de las funciones tal como se implementaron en AEM 6.5.

Para ver recomendaciones para clientes que actualizan a AEM 6.5, consulte [Recomendaciones de interfaz de usuario para clientes](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Esta página solo cubre la paridad de características con la IU clásica. No se incluyen las capacidades añadidas a la IU táctil y únicas a esta que no están presentes en la IU clásica.

>[!NOTE]
>
>Esta lista intenta ser completa, pero no es exhaustiva.

## Leyenda {#legend}

* **Completado**: la característica está totalmente disponible en la interfaz de usuario táctil.
* **Principalmente**: la característica está disponible principalmente en la interfaz de usuario táctil.
* **Ausente**: la característica no está presente en la IU táctil, la IU clásica debe usarse para realizar esta acción.
* **Reemplazada**: la característica se reemplazó con una nueva implementación que funciona de manera diferente.
* **Eliminada**: la característica ya no existe en la interfaz de usuario táctil y no se reemplazará.

## Estado de la característica: Administrador de sitios {#feature-status-sites-admin}

Esta es una lista de funcionalidades que tiene el administrador del sitio de la interfaz de usuario clásica (`/siteadmin`) y el estado de la interfaz de usuario táctil (`/sites.html`).

| Característica | Estado | Comentario |
|--- |--- |--- |
| Navegar por jerarquía del sitio | Completar | AEM 6.4 ha introducido una [vista de árbol de contenido](/help/sites-authoring/basic-handling.md#content-tree). |
| Iniciar flujo de trabajo | Completar |  |
| Creación de una página nueva | Completar |  |
| Creación de un nuevo sitio | Completar |  |
| Creación de un nuevo lanzamiento | Completar |  |
| Creación de una nueva live copy | Completar |  |
| Crear carpeta | Completar |  |
| Mostrar estado de publicación | Completar | A partir de AEM 6.5, el estado del flujo de trabajo se muestra en la vista de lista. |
| Búsqueda | Completar |  |
| Copiar y pegar página (duplicado) | Completar |  |
| Mover páginas | Completar |  |
| Publicar páginas | Completar |  |
| Publicar páginas sin derechos de replicación | Completar |  |
| Publicar posteriormente | Completar |  |
| Publicar árbol | Completar |  |
| Cancelar publicación de páginas | Completar |  |
| Cancelar la publicación de páginas sin derechos de replicación | Completar |  |
| Cancelar la publicación posteriormente | Completar |  |
| Eliminar | Completar |  |
| Bloquear/Desbloquear | Completar |  |
| Ver/editar propiedades | Completar |  |
| Definición de permisos en páginas | Completar |  |
| Historial de versiones | Completar |  |
| Restaurar versión | Completar |  |
| Restaurar árbol y restaurar páginas eliminadas | Ausente | Utilice la IU clásica. |
| Mostrar diferencia entre la versión antigua y la actual | Completar |  |
| Acciones de Live Copy (Despliegue) | Completar |  |
| Ver copias de idioma | Completar |  |
| Buscar y reemplazar | Ausente | Utilice la IU clásica. |
| Bandeja de entrada de notificaciones (eventos JCR) | Ausente | Utilice la IU clásica. Se reemplazará con una implementación diferente en el futuro. |
| Referencias | Completar | Visualización de los vínculos de página entrante añadidos a AEM 6.5. Solo se muestran los vínculos directos a la página por motivos de rendimiento. |

## Estado de la característica: Editor de páginas {#feature-status-page-editor}

Esta es una lista de las capacidades que tiene el editor de páginas de IU clásica (`/cf#`) y el estado en la IU táctil (`/editor.html`).

| Característica | Estado | Comentario |
|--- |--- |--- |
| Editar páginas web | Completar |  |
| Editar páginas web móviles | Completar |  |
| Editar contenido importado mediante el importador de diseños | Completar |  |
| Editar correos electrónicos | Completar |  |
| Editar aplicaciones móviles híbridas | Completar |  |
| Editar formularios | Completar |  |
| Editar ofertas | Completar |  |
| Editar modelos de flujos de trabajo | Completar |  |
| Modo: editar y previsualizar | Completar |  |
| Previsualización interactiva | Completar |  |
| Modo: Editar diseño | Completar |  |
| Modo: Andamiaje | Completar |  |
| Modo: Estado de Live Copy | Completar |  |
| Añadir anotaciones | Completar |  |
| Editar propiedades | Completar |  |
| Desplegar página | Completar |  |
| Iniciar y mostrar flujo de trabajo | Completar |  |
| Entrega de paquete de flujo de trabajo | Principalmente | Accesible en la IU táctil. Varias cargas útiles de flujo de trabajo siguen presentándose en la IU clásica. |
| Bloquear/desbloquear página | Completar |  |
| Publicar página | Completar |  |
| Cancelar la publicación de la página | Completar |  |
| Copiar página | Eliminado | Use el administrador del sitio para [copiar páginas](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Mover página | Eliminado | Use el administrador del sitio para [mover páginas](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Eliminar página | Eliminado | Use el administrador del sitio para [eliminar páginas](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostrar referencias | Eliminado | Use el administrador del sitio para ver la [lista de referencias detalladas](/help/sites-authoring/author-environment-tools.md#references). |
| Registro de auditoría | Eliminado | Use Administrador del sitio y [abrir carril de actividades](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Crear versión | Eliminado | Use el administrador del sitio para [crear nuevas versiones](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Restaurar versión | Eliminado | Use el administrador del sitio para [restaurar versiones](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Cambiar lanzamientos | Eliminado | Use el administrador del sitio para [cambiar entre lanzamientos](/help/sites-authoring/launches-promoting.md). |
| Traducir la página | Eliminado | Use el administrador del sitio para [añadir página a los proyectos de traducción](/help/sites-administering/tc-manage.md). |
| Deformación de tiempo (elija la fecha y la hora y explore el sitio tal y como estaba) | Completar |  |
| Establecer permisos | Completar |  |
| IU de contexto de cliente | Reemplazado | Utilice la IU de [ContextHub](/help/sites-authoring/ch-previewing.md) a partir de ahora. |
| Buscador de contenido para los distintos tipos de medios | Completar |  |
| Lista de componentes | Completar |  |
| Copiar y pegar componentes | Completar |  |
| Lista de componentes del portapapeles | Ausente |  |
| Deshacer, Rehacer | Completar |  |
| Arrastre el contenido al marcador de posición de componente | Completar |  |
| Arrastre el contenido directamente al marcador de posición parsys con la creación automática de componentes | Completar |  |

## Estado de las funciones: editores de texto, tablas e imágenes {#feature-status-text-table-and-image-editors}

Esta es una lista de funcionalidades que tienen la IU clásica del Editor de texto, tablas e imágenes y el estado en la IU táctil.

| Característica | Estado | Comentario |
|--- |--- |--- |
| Editor de texto enriquecido | Completar | Se puede utilizar in situ, en cuadros de diálogo y en pantalla completa. |
| Habilitar/deshabilitar complementos RTE | Completar | Se puede hacer con el [Editor de plantillas](/help/sites-authoring/templates.md). |
| Utilizar RTE para texto sin formato | Completar |  |
| Complemento RTE: Vínculos y anclajes | Completar |  |
| Complemento RTE: mapa de caracteres | Completar |  |
| Complemento RTE: copiar/pegar | Completar |  |
| Complemento RTE: pegar desde Microsoft® Word | Completar |  |
| Complemento RTE: buscar y reemplazar | Completar |  |
| Complemento RTE: Formatos de texto (negrita, ...) | Completar |  |
| Complemento RTE: subíndice y superíndice | Completar |  |
| Complemento RTE: Justificar | Completar |  |
| Complemento RTE: Listas (viñetas/números) | Completar |  |
| Complemento RTE: Formato de párrafo | Completar |  |
| Complemento RTE: estilos de texto | Completar |  |
| Complemento RTE: Editor de fuente (Editar HTML) | Completar | Solo disponible en cuadro de diálogo y pantalla completa. |
| Complemento RTE: corrector ortográfico | Completar |  |
| Complemento RTE: Tabla (editor de tablas incrustadas) | Completar |  |
| Complemento RTE: Deshacer/Rehacer | Completar |  |
| Complemento RTE: Permitir imágenes en línea | Completar |  |
| Editor de tablas | Completar | Se puede utilizar in situ, en cuadros de diálogo y en pantalla completa. |
| Arrastre la imagen a la celda de la tabla | Completar | Utilizable en línea |
| Editor de imágenes | Completar | Se puede utilizar in situ, en cuadros de diálogo y en pantalla completa. |
| Habilitar/deshabilitar complementos IPE | Completar | AEM 6.3 ha introducido una IU en [Editor de plantillas](/help/sites-authoring/templates.md). |
| Complemento IPE: Recortar | Completar |  |
| Complemento IPE: voltear | Completar |  |
| Complemento IPE: deshacer/rehacer | Completar |  |
| Complemento IPE: mapa de imagen | Completar |  |
| Complemento IPE: girar | Completar |  |
| Complemento IPE: zoom | Completar |  |

## Estado de la característica: Herramientas {#feature-status-tools}

Esta es una lista de varias herramientas que tiene la IU clásica y el estado de la IU táctil.

| Característica | Estado | Comentario |
|--- |--- |--- |
| Administración de tareas | Reemplazado | 6.0 presentó Proyectos y tareas. |
| Bandeja de entrada de flujo de trabajo | Completar |  |
| Configuración de flujo de trabajo a plantilla de página (`/etc/workflow/wcm/templates.html`) | Ausente | Utilice la IU clásica. |
| Etiquetado de IU de administración | Completar |  |
| Centro de control de MSM/Blueprint | Completar |  |
| IU de Blueprint Manager | Completar |  |
| IU de configuración de despliegue | Ausente | Utilice la IU clásica. |
| IU de usuario, grupos y permisos | Mayormente completo | Para la edición avanzada de permisos, utilice la IU clásica. |
| Purgar versiones (`/etc/versioning/purge.html`) | Ausente | Utilice la IU clásica. |
| Comprobador de vínculos externos (`/etc/linkchecker.html`) | Ausente | Utilice la IU clásica. |
| Editor por lotes (`/etc/importers/bulkeditor.html`) | Ausente | Utilice la IU clásica. |
| Cargar miniaturas para añadirlas o sobrescribirlas | Ausente | Utilice la IU clásica. |
