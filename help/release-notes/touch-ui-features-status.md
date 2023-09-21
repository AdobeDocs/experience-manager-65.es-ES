---
title: Estado de la función de IU táctil
description: Notas de versión específicas de [!DNL Adobe Experience Manager] IU táctil.
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 15%

---

# Estado de la función de IU táctil {#touch-ui-feature-status}

Adobe Experience Manager AEM () 6.4 en adelante [La IU clásica está obsoleta](../release-notes/deprecated-removed-features.md). El Adobe de no está realizando más mejoras en la IU clásica y se recomienda a los usuarios utilizar las potentes nuevas funciones disponibles en la IU táctil.

AEM A partir de la versión 6.0 de, introdujo una nueva interfaz de usuario denominada &quot;IU táctil&quot; (denominada &quot;IU táctil&quot;) que se alinea con la [!DNL Adobe Experience Cloud] y a las directrices generales de la interfaz de usuario de Adobe. AEM Una vez alcanzada la paridad casi total de las características, esta se ha convertido en la interfaz de usuario estándar en comparación con la interfaz heredada y orientada al escritorio, denominada &quot;IU clásica&quot;.

Aunque la mayoría de las funciones están presentes en la interfaz de usuario táctil, hay funciones que aún no se han completado y que se añadirán en versiones futuras.

AEM La siguiente lista muestra el estado de las funciones tal como se implementaron en la versión 6.5 de la.

AEM Para ver las recomendaciones para los clientes que actualizan a la versión 6.5 de, consulte [Recomendaciones de interfaz de usuario para clientes de](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Esta página solo cubre la paridad de características con la IU clásica. No se enumeran las capacidades agregadas a la IU táctil y únicas a esta que no están presentes en la IU clásica.

>[!NOTE]
>
>Esta lista intenta ser completa, pero no es exhaustiva.

## Leyenda {#legend}

* **Completar**: la función está totalmente disponible en la IU táctil.
* **Principalmente**: la funcionalidad está disponible principalmente en la IU táctil.
* **Falta**: la función no está presente en la IU táctil, la IU clásica debe utilizarse para realizar esta acción.
* **Reemplazado**: la función se ha reemplazado con una nueva implementación que funciona de forma diferente.
* **Eliminado**: la función ya no existe en la IU táctil y no se reemplazará.

## Estado de la función: Administrador de sitios {#feature-status-sites-admin}

Esta es una lista de funcionalidades que ofrece el clásico Administrador del sitio de IU (`/siteadmin`) tiene y el estado en la IU táctil (`/sites.html`).

| Funcionalidad | Estado | Comentar |
|--- |--- |--- |
| Navegar por jerarquía del sitio | Completar | AEM.4 introdujo un [vista de árbol de contenido](/help/sites-authoring/basic-handling.md#content-tree). |
| Iniciar flujo de trabajo | Completar |  |
| Crear nueva página | Completar |  |
| Crear nuevo sitio | Completar |  |
| Crear nuevo lanzamiento | Completar |  |
| Crear nueva Live Copy | Completar |  |
| Crear carpeta | Completar |  |
| Mostrar estado de publicación | Completar | AEM A partir de la versión 6.5, el estado del flujo de trabajo se muestra en la vista de lista. |
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
| Ver/Editar propiedades | Completar |  |
| Definición de permisos en páginas | Completar |  |
| Historial de versiones | Completar |  |
| Restaurar versión | Completar |  |
| Restaurar árbol y restaurar páginas eliminadas | Falta | Utilice la IU clásica. |
| Mostrar diferencia entre la versión antigua y la actual | Completar |  |
| Acciones de Live Copy (Despliegue) | Completar |  |
| Consulte Copias de idioma | Completar |  |
| Buscar y reemplazar | Falta | Utilice la IU clásica. |
| Bandeja de entrada de notificaciones (eventos JCR) | Falta | Utilice la IU clásica. Se reemplazará con una implementación diferente en el futuro. |
| Referencias | Completar | AEM Visualización de los vínculos de página entrante añadidos a la versión 6.5 de la. |

## Estado de la función: Editor de páginas {#feature-status-page-editor}

Esta es una lista de funcionalidades del editor de páginas de IU clásico (`/cf#`) tiene y el estado en la opción táctil (`/editor.html`).

| Funcionalidad | Estado | Comentar |
|--- |--- |--- |
| Editar páginas web | Completar |  |
| Editar páginas web móviles | Completar |  |
| Editar contenido importado mediante el importador de diseños | Completar |  |
| Editar correos electrónicos | Completar |  |
| Editar aplicaciones móviles híbridas | Completar |  |
| Editar Forms | Completar |  |
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
| Administración de paquetes de flujo de trabajo | Principalmente | Accesible en la interfaz de usuario táctil. Varias cargas útiles de flujo de trabajo siguen presentándose en la IU clásica. |
| Bloquear/desbloquear página | Completar |  |
| Publicar página | Completar |  |
| Cancelar la publicación de la página | Completar |  |
| Copiar página | Eliminado | Use Administrador del sitio para [copiar páginas](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Mover página | Eliminado | Use Administrador del sitio para [mover páginas](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Eliminar página | Eliminado | Use Administrador del sitio para [eliminar páginas](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostrar referencias | Eliminado | Utilice el Administrador del sitio para ver las [lista de referencia detallada](/help/sites-authoring/author-environment-tools.md#references). |
| Registro de auditorías | Eliminado | Uso del administrador del sitio y [abrir carril de actividad](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Crear versión | Eliminado | Use Administrador del sitio para [crear nuevas versiones](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Restaurar versión | Eliminado | Use Administrador del sitio para [restaurar versiones](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Cambiar inicios | Eliminado | Use Administrador del sitio para [cambiar entre lanzamientos](/help/sites-authoring/launches-promoting.md). |
| Traducir página | Eliminado | Use Administrador del sitio para [añadir página a proyectos de traducción](/help/sites-administering/tc-manage.md). |
| Deformación de tiempo (elija la fecha y la hora y explore el sitio tal y como estaba) | Completar |  |
| Definir permisos | Completar |  |
| IU de Client Context | Reemplazado | Utilice el [ContextHub](/help/sites-authoring/ch-previewing.md) Interfaz de usuario en adelante. |
| Buscador de contenido para los distintos tipos de medios | Completar |  |
| Lista de componentes | Completar |  |
| Copiar y pegar componentes | Completar |  |
| Lista de componentes del portapapeles | Falta |  |
| Deshacer, Rehacer | Completar |  |
| Arrastre el contenido al marcador de posición de componente | Completar |  |
| Arrastre el contenido directamente al marcador de posición parsys con la creación automática de componentes | Completar |  |

## Estado de las funciones: editores de texto, tablas e imágenes {#feature-status-text-table-and-image-editors}

Esta es una lista de funcionalidades que tienen la IU clásica del Editor de texto, tablas e imágenes y el estado en la IU táctil.

| Funcionalidad | Estado | Comentar |
|--- |--- |--- |
| Editor de texto enriquecido | Completar | Se puede utilizar in situ, en cuadros de diálogo y en pantalla completa. |
| Habilitar/deshabilitar complementos RTE | Completar | Se puede realizar utilizando la variable [Editor de plantillas](/help/sites-authoring/templates.md). |
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
| Complemento RTE: Editor de origen (HTML de edición) | Completar | Solo disponible en diálogo y pantalla completa. |
| Complemento RTE: corrector ortográfico | Completar |  |
| Complemento RTE: Tabla (editor de tablas incrustado) | Completar |  |
| Complemento RTE: Deshacer/Rehacer | Completar |  |
| Complemento RTE: Permitir imágenes en línea | Completar |  |
| Editor de tabla | Completar | Se puede utilizar in situ, en cuadros de diálogo y en pantalla completa. |
| Arrastre la imagen a la celda de tabla | Completar | Utilizable en línea |
| Editor de imágenes | Completar | Se puede utilizar in situ, en cuadros de diálogo y en pantalla completa. |
| Habilitar/deshabilitar complementos IPE | Completar | AEM.3 ha introducido una interfaz de usuario de en [Editor de plantillas](/help/sites-authoring/templates.md). |
| Complemento IPE: Recortar | Completar |  |
| Complemento IPE: voltear | Completar |  |
| Complemento IPE: Deshacer/Rehacer | Completar |  |
| Complemento IPE: mapa de imagen | Completar |  |
| Complemento IPE: girar | Completar |  |
| Complemento IPE: zoom | Completar |  |

## Estado de la función: Herramientas {#feature-status-tools}

Esta es una lista de varias herramientas que tiene la IU clásica y el estado de la IU táctil.

| Funcionalidad | Estado | Comentar |
|--- |--- |--- |
| Administración de tareas | Reemplazado | 6.0 presentó Proyectos y tareas. |
| Bandeja de entrada de flujo | Completar |  |
| Configuración del flujo de trabajo a la plantilla de página (`/etc/workflow/wcm/templates.html`) | Falta | Utilice la IU clásica. |
| Etiquetado de IU de administración | Completar |  |
| Centro de control de MSM/modelo | Completar |  |
| IU del Administrador de modelos | Completar |  |
| Interfaz de usuario de configuración de despliegue | Falta | Utilice la IU clásica. |
| IU de usuario, grupos y permisos | Mayormente completo | Para la edición avanzada de permisos, utilice la IU clásica. |
| Purgar versiones (`/etc/versioning/purge.html`) | Falta | Utilice la IU clásica. |
| Comprobador de vínculos externos (`/etc/linkchecker.html`) | Falta | Utilice la IU clásica. |
| Editor por lotes (`/etc/importers/bulkeditor.html`) | Falta | Utilice la IU clásica. |
| Cargar miniaturas para añadirlas o sobrescribirlas | Falta | Utilice la IU clásica. |
