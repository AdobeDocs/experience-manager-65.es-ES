---
title: Estado de la función de IU táctil
description: Notas de la versión específicas de  [!DNL Adobe Experience Manager] IU táctil.
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 25bf0d64b6839afec0112ea8c9fde0510e56ccf4
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 15%

---

# Estado de la función de IU táctil {#touch-ui-feature-status}

La [IU clásica de Adobe Experience Manager (AEM) 6.4 y posteriores está obsoleta](../release-notes/deprecated-removed-features.md). Adobe no está realizando más mejoras en la IU clásica y se recomienda a los usuarios utilizar las potentes nuevas funciones disponibles en la IU táctil.

A partir de la versión 6.0, AEM introdujo una nueva interfaz de usuario denominada &quot;IU táctil&quot; (denominada &quot;IU táctil&quot;) que está alineada con [!DNL Adobe Experience Cloud] y con las directrices generales de la interfaz de usuario de Adobe. Una vez alcanzada la paridad de características, se ha convertido en la interfaz de usuario estándar de AEM, con la interfaz heredada orientada al escritorio y denominada &quot;IU clásica&quot;.

Aunque la mayoría de las funciones están presentes en la interfaz de usuario táctil, hay funciones que aún no se han completado y que se añadirán en versiones futuras.

La siguiente lista muestra el estado de las funciones tal como se implementaron en AEM 6.5.

Para ver recomendaciones para clientes que actualizan a AEM 6.5, consulte [Recomendaciones de interfaz de usuario para clientes](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Esta página solo cubre la paridad de características con la IU clásica. No se enumeran las capacidades agregadas a la IU táctil y únicas a esta que no están presentes en la IU clásica.

>[!NOTE]
>
>Esta lista intenta ser completa, pero no es exhaustiva.

## Leyenda {#legend}

* **Completado**: la característica está totalmente disponible en la interfaz de usuario táctil.
* **Principalmente**: La funcionalidad está disponible principalmente en la interfaz de usuario táctil.
* **Falta**: la característica no está presente en la IU táctil, la IU clásica debe usarse para realizar esta acción.
* **Reemplazada**: la característica se reemplazó con una nueva implementación que funciona de manera diferente.
* **Eliminada**: la característica ya no existe en la interfaz de usuario táctil y no se reemplazará.

## Estado de la función: Administrador de sitios {#feature-status-sites-admin}

Esta es una lista de funcionalidades que tiene el administrador del sitio de la interfaz de usuario clásica (`/siteadmin`) y el estado de la interfaz de usuario táctil (`/sites.html`).

| Función | Estado | Comentar |
|--- |--- |--- |
| Navegar por jerarquía del sitio | Completado | AEM 6.4 ha introducido una [vista de árbol de contenido](/help/sites-authoring/basic-handling.md#content-tree). |
| Iniciar flujo de trabajo | Completado |  |
| Crear nueva página | Completado |  |
| Crear nuevo sitio | Completado |  |
| Crear nuevo lanzamiento | Completado |  |
| Crear nueva Live Copy | Completado |  |
| Crear carpeta | Completado |  |
| Mostrar estado de publicación | Completado | A partir de AEM 6.5, el estado del flujo de trabajo se muestra en la vista de lista. |
| Búsqueda | Completado |  |
| Copiar y pegar página (duplicado) | Completado |  |
| Mover páginas | Completado |  |
| Publicar páginas | Completado |  |
| Publicar páginas sin derechos de replicación | Completado |  |
| Publicar posteriormente | Completado |  |
| Publicar árbol | Completado |  |
| Cancelar publicación de páginas | Completado |  |
| Cancelar la publicación de páginas sin derechos de replicación | Completado |  |
| Cancelar la publicación posteriormente | Completado |  |
| Eliminar | Completado |  |
| Bloquear/Desbloquear | Completado |  |
| Ver/Editar propiedades | Completado |  |
| Definición de permisos en páginas | Completado |  |
| Historial de versiones | Completado |  |
| Restaurar versión | Completado |  |
| Restaurar árbol y restaurar páginas eliminadas | Falta | Utilice la IU clásica. |
| Mostrar diferencia entre la versión antigua y la actual | Completado |  |
| Acciones de Live Copy (Despliegue) | Completado |  |
| Consulte Copias de idioma | Completado |  |
| Buscar y reemplazar | Falta | Utilice la IU clásica. |
| Bandeja de entrada de notificaciones (eventos JCR) | Falta | Utilice la IU clásica. Se reemplazará con una implementación diferente en el futuro. |
| Referencias | Completado | Visualización de los vínculos de página entrante añadidos a AEM 6.5. Solo se muestran los vínculos directos a la página por motivos de rendimiento. |

## Estado de la función: Editor de páginas {#feature-status-page-editor}

Esta es una lista de las capacidades que tiene el editor de páginas de IU clásica (`/cf#`) y el estado en el editor táctil (`/editor.html`).

| Función | Estado | Comentar |
|--- |--- |--- |
| Editar páginas web | Completado |  |
| Editar páginas web móviles | Completado |  |
| Editar contenido importado mediante el importador de diseños | Completado |  |
| Editar correos electrónicos | Completado |  |
| Editar aplicaciones móviles híbridas | Completado |  |
| Editar Forms | Completado |  |
| Editar ofertas | Completado |  |
| Editar modelos de flujos de trabajo | Completado |  |
| Modo: editar y previsualizar | Completado |  |
| Previsualización interactiva | Completado |  |
| Modo: Editar diseño | Completado |  |
| Modo: Andamiaje | Completado |  |
| Modo: Estado de Live Copy | Completado |  |
| Añadir anotaciones | Completado |  |
| Editar propiedades | Completado |  |
| Desplegar página | Completado |  |
| Iniciar y mostrar flujo de trabajo | Completado |  |
| Administración de paquetes de flujo de trabajo | Principalmente | Accesible en la interfaz de usuario táctil. Varias cargas útiles de flujo de trabajo siguen presentándose en la IU clásica. |
| Bloquear/desbloquear página | Completado |  |
| Publicar página | Completado |  |
| Cancelar la publicación de la página | Completado |  |
| Copiar página | Eliminado | Use el administrador del sitio para [copiar páginas](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Mover página | Eliminado | Use el administrador del sitio para [mover páginas](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Eliminar página | Eliminado | Use el administrador del sitio para [eliminar páginas](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostrar referencias | Eliminado | Use el administrador del sitio para ver la [lista de referencia detallada](/help/sites-authoring/author-environment-tools.md#references). |
| Registro de auditoría | Eliminado | Use Administrador del sitio y [abrir carril de actividades](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Crear versión | Eliminado | Use el administrador del sitio para [crear nuevas versiones](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Restaurar versión | Eliminado | Use el administrador del sitio para [restaurar versiones](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Cambiar inicios | Eliminado | Use el administrador del sitio para [cambiar entre inicios](/help/sites-authoring/launches-promoting.md). |
| Traducir página | Eliminado | Use el administrador del sitio para [agregar página a los proyectos de traducción](/help/sites-administering/tc-manage.md). |
| Deformación de tiempo (elija la fecha y la hora y explore el sitio tal y como estaba) | Completado |  |
| Definir permisos | Completado |  |
| IU de Client Context | Reemplazado | Utilice la interfaz de usuario de [ContextHub](/help/sites-authoring/ch-previewing.md) a partir de ahora. |
| Buscador de contenido para los distintos tipos de medios | Completado |  |
| Lista de componentes | Completado |  |
| Copiar y pegar componentes | Completado |  |
| Lista de componentes del portapapeles | Falta |  |
| Deshacer, Rehacer | Completado |  |
| Arrastre el contenido al marcador de posición de componente | Completado |  |
| Arrastre el contenido directamente al marcador de posición parsys con la creación automática de componentes | Completado |  |

## Estado de las funciones: editores de texto, tablas e imágenes {#feature-status-text-table-and-image-editors}

Esta es una lista de funcionalidades que tienen la IU clásica del Editor de texto, tablas e imágenes y el estado en la IU táctil.

| Función | Estado | Comentar |
|--- |--- |--- |
| Editor de texto enriquecido | Completado | Se puede utilizar in situ, en cuadros de diálogo y en pantalla completa. |
| Habilitar/deshabilitar complementos RTE | Completado | Se puede hacer con el [Editor de plantillas](/help/sites-authoring/templates.md). |
| Utilizar RTE para texto sin formato | Completado |  |
| Complemento RTE: Vínculos y anclajes | Completado |  |
| Complemento RTE: mapa de caracteres | Completado |  |
| Complemento RTE: copiar/pegar | Completado |  |
| Complemento RTE: pegar desde Microsoft® Word | Completado |  |
| Complemento RTE: buscar y reemplazar | Completado |  |
| Complemento RTE: Formatos de texto (negrita, ...) | Completado |  |
| Complemento RTE: subíndice y superíndice | Completado |  |
| Complemento RTE: Justificar | Completado |  |
| Complemento RTE: Listas (viñetas/números) | Completado |  |
| Complemento RTE: Formato de párrafo | Completado |  |
| Complemento RTE: estilos de texto | Completado |  |
| Complemento RTE: Editor de Source (Editar HTML) | Completado | Solo disponible en diálogo y pantalla completa. |
| Complemento RTE: corrector ortográfico | Completado |  |
| Complemento RTE: Tabla (editor de tablas incrustado) | Completado |  |
| Complemento RTE: Deshacer/Rehacer | Completado |  |
| Complemento RTE: Permitir imágenes en línea | Completado |  |
| Editor de tabla | Completado | Se puede utilizar in situ, en cuadros de diálogo y en pantalla completa. |
| Arrastre la imagen a la celda de tabla | Completado | Utilizable en línea |
| Editor de imágenes | Completado | Se puede utilizar in situ, en cuadros de diálogo y en pantalla completa. |
| Habilitar/deshabilitar complementos IPE | Completado | AEM 6.3 ha introducido una interfaz de usuario en [Editor de plantillas](/help/sites-authoring/templates.md). |
| Complemento IPE: Recortar | Completado |  |
| Complemento IPE: voltear | Completado |  |
| Complemento IPE: Deshacer/Rehacer | Completado |  |
| Complemento IPE: mapa de imagen | Completado |  |
| Complemento IPE: girar | Completado |  |
| Complemento IPE: zoom | Completado |  |

## Estado de la función: Herramientas {#feature-status-tools}

Esta es una lista de varias herramientas que tiene la IU clásica y el estado de la IU táctil.

| Función | Estado | Comentar |
|--- |--- |--- |
| Administración de tareas | Reemplazado | 6.0 presentó Proyectos y tareas. |
| Bandeja de entrada de flujo | Completado |  |
| Configuración de flujo de trabajo a plantilla de página (`/etc/workflow/wcm/templates.html`) | Falta | Utilice la IU clásica. |
| Etiquetado de IU de administración | Completado |  |
| Centro de control de MSM/modelo | Completado |  |
| IU del Administrador de modelos | Completado |  |
| Interfaz de usuario de configuración de despliegue | Falta | Utilice la IU clásica. |
| IU de usuario, grupos y permisos | Mayormente completo | Para la edición avanzada de permisos, utilice la IU clásica. |
| Purgar versiones (`/etc/versioning/purge.html`) | Falta | Utilice la IU clásica. |
| Verificador de vínculos externos (`/etc/linkchecker.html`) | Falta | Utilice la IU clásica. |
| Editor por lotes (`/etc/importers/bulkeditor.html`) | Falta | Utilice la IU clásica. |
| Cargar miniaturas para añadirlas o sobrescribirlas | Falta | Utilice la IU clásica. |
