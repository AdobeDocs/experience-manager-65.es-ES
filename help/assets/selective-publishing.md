---
title: Uso de Publicación selectiva en Dynamic Media
description: Información sobre cómo trabajar con Publicación selectiva en Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publicación
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '2944'
ht-degree: 4%

---

# Configuración de una publicación selectiva a nivel de carpeta en Dynamic Media {#selective-publish-configure-folder}

Puede elegir entre publicar o cancelar la publicación de recursos en Adobe Experience Manager o Dynamic Media en el nivel de carpeta, o desde ellos. Puede utilizar **[!UICONTROL Administrar publicación]** o **[!UICONTROL Publicación rápida]** en lugar de basarse únicamente en la **[!UICONTROL Configuración de Dynamic Media]** cuya configuración sea global para todas las carpetas de la instancia de Dynamic Media.

Por ejemplo, con la publicación selectiva puede trabajar en recursos para productos que aún no están activos. En tal caso, un equipo de marketing puede acceder a las imágenes de recorte inteligente y a las representaciones dinámicas sincronizadas con Dynamic Media. Pueden crear materiales promocionales, sin necesidad de publicar esos recursos en Dynamic Media para su envío global.

>[!IMPORTANT]
>
>La publicación selectiva solo está disponible en el modo Dynamic Media - Scene7 .

>[!NOTE]
>
>** Al copiar recursos a y desde carpetas, se borra el estado de publicación de esos recursos. Sin embargo, cuando *mueve* recursos a carpetas cuya propiedad de carpeta está establecida en **[!UICONTROL Publicación selectiva]**, se mantiene el estado de publicación de esos recursos.

Si más adelante decide cambiar la configuración de **[!UICONTROL Publicación selectiva]** en una carpeta, esos cambios solo afectarán a los nuevos recursos que cargue en esa carpeta a partir de ese momento. El estado de publicación de los recursos existentes en la carpeta permanece tal cual hasta que los cambie manualmente desde **[!UICONTROL Publicación rápida]** o el cuadro de diálogo **[!UICONTROL Administrar publicación]**.

La opción de nivel de carpeta **[!UICONTROL Dynamic Media Publish mode]** siempre establece de forma predeterminada el valor que se encuentra en la configuración **[!UICONTROL Publicar recursos]** de la **[!UICONTROL Configuración de Dynamic Media]**. Sin embargo, los siguientes pasos en este tema muestran cómo cambiar manualmente este valor predeterminado en el nivel de carpeta (como se describe en los pasos siguientes) para anular el valor **[!UICONTROL Dynamic Media Configuration]**.

Independientemente de si confía en el valor **[!UICONTROL Publicar recursos]** establecido en **[!UICONTROL Configuración de Dynamic Media]** o en el valor **[!UICONTROL Modo de publicación de Dynamic Media]** establecido en las propiedades de nivel de carpeta, puede elegir **[!UICONTROL Inmediatamente]**, **[!UICONTROL Al activarse]** o &lt;a 10/>De forma inmediata. Active Publish ]**.**[!UICONTROL  Por ejemplo, puede establecer el valor **[!UICONTROL Publicar recursos]** en la **[!UICONTROL Configuración de Dynamic Media]** en **[!UICONTROL Al activarse]**, pero establecer el valor del modo **[!UICONTROL Publicación de Dynamic Media]** en el nivel de carpeta en **[!UICONTROL Publicación selectiva]** y, a la inversa.

Después de configurar la publicación selectiva en una carpeta, puede realizar cualquiera de las siguientes acciones:

* [Publicar recursos de forma selectiva en Dynamic Media o Experience Manager mediante Administrar publicación](#selective-publish-manage-publication).
* [Cancelar la publicación de forma selectiva desde Dynamic Media o Experience Manager mediante Administrar publicación](#selective-unpublish-manage-publication).
* [Publicación de recursos en Dynamic Media o Experience Manager mediante Publicación rápida](#quick-publish-aem-dm).
* [Publicar o cancelar la publicación de forma selectiva mediante los resultados](#selective-publish-unpublish-search-results) de búsqueda.

**Para configurar la publicación selectiva en el nivel de carpeta en Dynamic Media:**

1. En el Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo, pulse el icono Navegación (justo encima del icono Herramientas ) y, a continuación, pulse **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Realice una de las acciones siguientes:
   * Edite las propiedades de una carpeta existente: en **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, vaya a la carpeta cuyas propiedades desee editar. Seleccione la carpeta y, en la barra de herramientas, pulse **[!UICONTROL Propiedades]**.
   * Edite las propiedades de una nueva carpeta: en **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, cerca de la esquina superior derecha de la página, pulse **[!UICONTROL Crear]** > **[!UICONTROL Carpeta]**. En el cuadro de diálogo **[!UICONTROL Crear carpeta]**, introduzca un título (obligatorio) para la carpeta y, a continuación, pulse **[!UICONTROL Crear]**. Seleccione la carpeta y, en la barra de herramientas, pulse **[!UICONTROL Propiedades]**.

1. En la lista desplegable **[!UICONTROL Sync mode]**, seleccione una de las siguientes opciones:

   | Modo de sincronización | Descripción |
   | --- | --- |
   | **[!UICONTROL Heredado]** | No hay ningún valor de sincronización explícito en la carpeta; en su lugar, la carpeta hereda el valor de sincronización de una de sus carpetas antecesoras o el modo predeterminado establecido en su **[!UICONTROL Configuración de Dynamic Media]**. El estado detallado de **[!UICONTROL Heredado]** se muestra mediante una información del objeto. |
   | **[!UICONTROL Sincronizar todo en este subárbol de carpetas con Dynamic Media]** | Para que la publicación en Dynamic Media se realice correctamente, los recursos deben sincronizarse con Dynamic Media. Al seleccionar esta opción, se incluyen todos los recursos de este subárbol para sincronizarlos con Dynamic Media. La configuración específica de la carpeta anula la configuración predeterminada de la **[!UICONTROL Configuración de Dynamic Media]**. |
   | **[!UICONTROL Excluir todo en este subárbol de carpetas de la sincronización de Dynamic Media]** | Excluya todos los recursos de este subárbol de la sincronización con Dynamic Media. |

   ![Publicación selectiva a nivel de carpeta](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. En la lista desplegable **[!UICONTROL Dynamic Media Publish mode]**, seleccione una opción. La opción **[!UICONTROL Dynamic Media Publish mode]** siempre establece de forma predeterminada el valor establecido en **[!UICONTROL Dynamic Media Configuration]**. Sin embargo, puede anular manualmente este valor predeterminado **[!UICONTROL Dynamic Media Configuration]** mediante una de las siguientes opciones.

   >[!IMPORTANT]
   >
   >Independientemente de la opción del modo de publicación de Dynamic Media que seleccione, cualquier actualización que realice posteriormente en un recurso que ya esté *publicado*, esas actualizaciones se publican inmediatamente sin que el usuario tome ninguna otra medida.

   | Opción de modo Publicación de Dynamic Media | Descripción |
   | --- | --- |
   | **[!UICONTROL Inmediatamente]** | Cuando los recursos se cargan en esta carpeta, el sistema los incorpora en el Experience Manager y proporciona la URL o la Incrustar al instante. Esta opción solo está vinculada a la publicación en Experience Manager y no es necesario que el usuario intervenga para publicar recursos.<br>Esta opción  ** no está disponible si seleccionó  **[!UICONTROL Excluir todo en este subárbol de carpetas del modo de]** sincronización de Dynamic Media  **[!UICONTROL en el]** paso anterior. |
   | **[!UICONTROL Tras la activación]** | Cuando los recursos se cargan en esta carpeta, primero debe publicar explícitamente el recurso antes de proporcionar un vínculo URL/incrustado. Esta opción solo está vinculada a la publicación en Experience Manager.<br>Esta opción  ** no está disponible si seleccionó  **[!UICONTROL Excluir todo en este subárbol de carpetas del modo de]** sincronización de Dynamic Media  **[!UICONTROL en el]** paso anterior. |
   | **[!UICONTROL Publicación selectiva]** | Los recursos se publican a su elección, ya sea en el Experience Manager o en Dynamic Media para su entrega en el dominio público. Ambos métodos de publicación se excluyen mutuamente. Es decir, puede publicar recursos en DMS7 para que pueda utilizar funciones como Recorte inteligente o representaciones dinámicas. O puede publicar recursos exclusivamente en Experience Manager para obtener una vista previa segura; esos mismos activos son *no* publicados en DMS7 para su envío en el dominio público. Esta opción no está disponible si seleccionó **[!UICONTROL Excluir todo en este subárbol de carpetas de Dynamic Media sync]** en **[!UICONTROL Sync mode]** en el paso anterior. |

1. En la esquina superior derecha de la página, pulse **[!UICONTROL Guardar y cerrar]** y, a continuación, pulse **[!UICONTROL Aceptar]** para volver a Recursos Experience Manager.

## Publicar recursos de forma selectiva en Dynamic Media o Experience Manager mediante Administrar publicación{#selective-publish-manage-publication}

Antes de utilizar **[!UICONTROL Administrar publicación]** para publicar selectivamente recursos en Dynamic Media o Experience Manager, asegúrese de haber configurado una de las siguientes opciones:

* La opción **[!UICONTROL Publicar recursos]** en **[!UICONTROL Configuración de Dynamic Media]** para **[!UICONTROL Publicación selectiva]**
* Se ha configurado la publicación selectiva en el nivel de carpeta.

Consulte [Creación de una configuración de Dynamic Media](#configuring-dynamic-media-cloud-services) o [Configuración de la publicación selectiva a nivel de carpeta en Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>La publicación selectiva solo está disponible en el modo Dynamic Media - Scene7 .

>[!NOTE]
>
>** Al copiar recursos a y desde carpetas, se borra el estado de publicación de esos recursos. Sin embargo, cuando *mueve* recursos a carpetas cuya propiedad de carpeta está establecida en **[!UICONTROL Publicación selectiva]**, se mantiene el estado de publicación de esos recursos.

**Para publicar selectivamente recursos en Dynamic Media o Experience Manager mediante Administrar publicación:**

1. En el Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo, pulse el icono Navegación (justo encima del icono Herramientas ) y, a continuación, pulse **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Vaya a una carpeta cuyos recursos desee publicar. Seleccione la carpeta y, en la barra de herramientas, pulse **[!UICONTROL Administrar publicación]**. Utilice **[!UICONTROL Vista de lista]** para poder comprobar con mayor facilidad el estado de publicación de una carpeta en particular.
   * Vaya a una carpeta cuyos recursos desee publicar. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, pulse **[!UICONTROL Administrar publicación]**. Utilice la **[!UICONTROL Vista de lista]** para poder comprobar más fácilmente el estado de publicación de un recurso en particular.

      >[!NOTE]
      >
      >Si no se ve **[!UICONTROL Administrar publicación]** en la barra de herramientas, pulse el botón de puntos suspensivos y, a continuación, seleccione **[!UICONTROL Administrar publicación]** en el menú de la lista.

1. En la página **[!UICONTROL Administrar publicación: opciones]**, en **[!UICONTROL Acción]**, seleccione el tipo de activación que desee.

   | Acción | Descripción |
   | --- | --- |
   | **[!UICONTROL Publicar]**  (en Experience Manager) | Seleccione esta opción para publicar recursos en el Experience Manager y así obtener una vista previa segura. |
   | **[!UICONTROL Publicar en Dynamic Media]** | Seleccione esta opción para publicar recursos en Dynamic Media para su entrega en el dominio público o para que pueda utilizar funciones como Recorte inteligente o representaciones dinámicas.<br>Esta opción solo está disponible si el modo de publicación de  **[!UICONTROL Dynamic Media]** está establecido en Publicación  **[!UICONTROL selectiva]** en las propiedades de la carpeta. |

1. En **[!UICONTROL Programar]**, establezca la temporización de la publicación.

   | Programa | Descripción |
   | --- | --- |
   | **[!UICONTROL Ahora]** | Seleccione para publicar los recursos inmediatamente. |
   | **[!UICONTROL Más tarde]** | Seleccione para publicar los recursos en una fecha y hora concretas. |

1. En la esquina superior derecha de la página **[!UICONTROL Administrar publicación]**, pulse **[!UICONTROL Siguiente]**.
1. En la página **[!UICONTROL Administrar publicación - Ámbito]**, realice una de las siguientes acciones:

   * Si es necesario, seleccione uno o varios recursos que desee eliminar de la publicación.
   * En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Ámbito]**, pulse **[!UICONTROL Publicar]** o **[!UICONTROL Publicar en Dynamic Media]**.
1. Pulse **[!UICONTROL Aceptar]**.

### Cancelar la publicación de forma selectiva desde Dynamic Media o Experience Manager mediante Administrar publicación {#selective-unpublish-manage-publication}

1. En el Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo, pulse el icono Navegación (justo encima del icono Herramientas ) y, a continuación, pulse **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Desplácese a la carpeta cuyos recursos desee cancelar la publicación. Seleccione la carpeta y, en la barra de herramientas, pulse **[!UICONTROL Administrar publicación]**. Utilice **[!UICONTROL Vista de lista]** para poder comprobar con mayor facilidad el estado de publicación de una carpeta en particular.
   * Desplácese a la carpeta cuyos recursos desee cancelar la publicación. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, pulse **[!UICONTROL Administrar publicación]**. Utilice la **[!UICONTROL Vista de lista]** para poder comprobar más fácilmente el estado de publicación de un recurso en particular.

      >[!NOTE]
      >
      >Si no se ve **[!UICONTROL Administrar publicación]** en la barra de herramientas, pulse el botón de puntos suspensivos y, a continuación, seleccione **[!UICONTROL Administrar publicación]** en el menú de la lista.

1. En la página **[!UICONTROL Administrar publicación: opciones]**, en **[!UICONTROL Acción]**, seleccione el tipo de desactivación que desee.

   | Acción | Descripción |
   | --- | --- |
   | **[!UICONTROL Cancelar publicación]**  (del Experience Manager) | Seleccione esta opción si desea cancelar la publicación de los recursos del Experience Manager. |
   | **[!UICONTROL Cancelar la publicación de Dynamic Media]** | Seleccione esta opción si desea cancelar la publicación de recursos de Dynamic Media.<br>Esta opción solo está disponible si el modo de publicación de  **[!UICONTROL Dynamic Media]** está establecido en Publicación  **[!UICONTROL selectiva]** en las propiedades de la carpeta. |

1. En **[!UICONTROL Schedule]**, establezca el tiempo de desactivación.

   | Programa | Descripción |
   | --- | --- |
   | **[!UICONTROL Ahora]** | Seleccione para cancelar la publicación de los recursos inmediatamente. |
   | **[!UICONTROL Más tarde]** | Seleccione para cancelar la publicación de los recursos en una fecha y hora concretas. |

1. En la esquina superior derecha de la página **[!UICONTROL Administrar publicación]**, pulse **[!UICONTROL Siguiente]**.
1. En la página **[!UICONTROL Administrar publicación - Ámbito]**, realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee eliminar de la cancelación de la publicación.
   * En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Ámbito]**, pulse **[!UICONTROL Cancelar publicación]** o **[!UICONTROL Cancelar publicación desde Dynamic Media]**.
1. Pulse **[!UICONTROL Aceptar]**.

## Publicación de recursos en Dynamic Media o Experience Manager mediante Publicación rápida {#quick-publish-aem-dm}

Puede utilizar **[!UICONTROL Publicación rápida]** para casos sencillos de activación de recursos. **[!UICONTROL Publicación rápida]** publica los recursos seleccionados inmediatamente, sin más interacción del usuario. Debido a esta acción, cualquier referencia no publicada también se publica automáticamente.

>[!NOTE]
>
>Para utilizar **[!UICONTROL Publicación rápida]** para publicar recursos en Dynamic Media o Experience Manager, asegúrese de que **[!UICONTROL Publicación selectiva]** esté habilitada en su **[!UICONTROL Configuración de Dynamic Media]** o en las propiedades de carpeta de la carpeta seleccionada.

**Para publicar recursos en Dynamic Media o Experience Manager mediante Publicación rápida:**

1. En el Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo de la página, pulse el icono Navegación (justo encima del icono Herramientas ) y, a continuación, en el lado derecho de la página, pulse **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Vaya a una carpeta cuyos recursos desee publicar. Seleccione la carpeta y, a continuación, en la barra de herramientas, pulse **[!UICONTROL Publicación rápida]**. Utilice **[!UICONTROL Vista de lista]** para poder comprobar con mayor facilidad el estado de publicación de una carpeta en particular.
   * Vaya a una carpeta cuyos recursos desee publicar. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, pulse **[!UICONTROL Publicación rápida]**. Utilice la **[!UICONTROL Vista de lista]** para poder comprobar más fácilmente el estado de publicación de un recurso en particular.

      >[!NOTE]
      >
      >Si no se ve **[!UICONTROL Publicación rápida]** en la barra de herramientas, pulse el botón de puntos suspensivos en su lugar y, a continuación, seleccione **[!UICONTROL Publicación rápida]** en el menú de la lista.

      ![Publicación rápida a nivel de carpeta en Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Seleccione una de las siguientes opciones en la lista de menú **[!UICONTROL Publicación rápida]**.

   | Opción Publicación rápida | Qué hace |
   | --- | --- | 
   | Publicar en el Experience Manager | Publica los recursos seleccionados inmediatamente en el Experience Manager. |
   | Publicar en Brand Portal | Publica los recursos seleccionados inmediatamente en **[!UICONTROL Brand Portal]**.<br>Esta opción solo está disponible si la instancia de Recursos de Experience Manager tiene  **[!UICONTROL Brand]** Portal ya configurado. |
   | Publicar en Dynamic Media | Publica los recursos seleccionados inmediatamente en Dynamic Media.<br>Un recurso debe sincronizarse con Dynamic Media. Si es necesario, asegúrese de que **[!UICONTROL Sync mode]** en las propiedades de una carpeta ya esté configurado como **[!UICONTROL Sync all in this folder subtree to Dynamic Media]**. |

1. Pulse **[!UICONTROL Aceptar]** y, a continuación, pulse **[!UICONTROL Cerrar]**.

## Publicar o cancelar la publicación de recursos de forma selectiva mediante los resultados de búsqueda {#selective-publish-unpublish-search-results}

Los resultados de búsqueda pueden mostrar recursos de todas las carpetas de recursos que tengan diferentes configuraciones de publicación de Dynamic Media. Si selecciona varios recursos de los resultados de búsqueda y cada recurso tiene diferentes configuraciones del modo de publicación de Dynamic Media, puede almacenar en déclencheur **[!UICONTROL Administrar publicación]** desde la barra de herramientas para publicar o cancelar la publicación.

Consulte también [Buscar recursos en el Experience Manager](/help/assets/search-assets.md).

**Para publicar o cancelar la publicación de recursos de forma selectiva mediante los resultados de búsqueda:**

1. En el Experience Manager, en la esquina superior izquierda de la página, pulse el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo de la página, pulse el icono Navegación (justo encima del icono Herramientas) y, a continuación, pulse **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. En la barra de herramientas, cerca de la esquina superior derecha de la página, pulse el icono Buscar (lupa).
1. En el campo de texto **[!UICONTROL Type to search]**, introduzca una palabra clave y, a continuación, pulse **[!UICONTROL Enter]**.
1. Cerca de la esquina superior derecha de la página, pulse el icono **[!UICONTROL Vista de lista]**.
1. Cerca de la esquina superior izquierda de la página, pulse el icono **[!UICONTROL Filters]**.

   ![Vista de lista y filtros en los resultados de búsqueda](/help/assets/assets-dm/select-publish-search-result.png)

1. En el panel izquierdo, expanda **[!UICONTROL Status]** y luego expanda el predicado de búsqueda **[!UICONTROL Dynamic Media]**.
1. Utilice las casillas de verificación **[!UICONTROL Publicado]** y **[!UICONTROL No publicado]** para restringir aún más los resultados de búsqueda según el estado publicado de los recursos de Dynamic Media.
Opcionalmente, puede utilizar estas casillas de verificación con el predicado de búsqueda **[!UICONTROL Publicar]** para refinar los resultados de búsqueda de los recursos de Experience Manager **[!UICONTROL Publicados]** y **[!UICONTROL No publicados]**.
1. Realice una de las acciones siguientes:
   * Seleccione uno o varios recursos que desee publicar o cancelar la publicación.
   * Cerca de la esquina superior derecha de la página **[!UICONTROL Resultados de búsqueda]**, pulse **[!UICONTROL Seleccionar todo]**.
1. En la barra de herramientas, pulse **[!UICONTROL Administrar publicación]**. Pulse el icono de elipsis de la barra de herramientas para abrir **[!UICONTROL Administrar publicación]**.
1. En la página **[!UICONTROL Administrar publicación: opciones]**, seleccione la acción que desee.

   | Acción seleccionada | Publicar recursos en la configuración de Dynamic Media | Los recursos son |
   | --- | --- | --- |
   | Publicación | Inmediatamente o después de la activación | Publicado para Experience Manager y Dynamic Media. |
   | Publicación | Publicación selectiva | Se publica solo para el Experience Manager. |
   | Cancelar publicación | Inmediatamente o después de la activación | No publicado por Experience Manager y Dynamic Media. |
   | Cancelar publicación | Publicación selectiva | Cancelado la publicación solo del Experience Manager. |
   | Publicar en Dynamic Media | Inmediatamente o después de la activación | No se ha publicado para Experience Manager, Dynamic Media o ambos. |
   | Publicar en Dynamic Media | Publicación selectiva | Solo se publica en Dynamic Media. |
   | Cancelar la publicación de Dynamic Media | Inmediatamente o después de la activación | No se canceló la publicación de Experience Manager, Dynamic Media o ambos. |
   | Cancelar la publicación de Dynamic Media | Publicación selectiva | Cancelado la publicación solo desde Dynamic Media. |

1. En **[!UICONTROL Schedule]**, establezca el tiempo de desactivación.

   | Programación seleccionada | Qué sucede |
   | --- | --- |
   | Ahora | La acción seleccionada se realiza inmediatamente. |
   | Más tarde | La acción seleccionada se ejecuta en la fecha y hora concretas seleccionadas. |

1. En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Opciones]**, pulse **[!UICONTROL Siguiente]**.
1. (Opcional) En la página **[!UICONTROL Administrar publicación - Ámbito]**, revise la columna **[!UICONTROL Publicar destino]** de la tabla para los recursos seleccionados.

   | Publicar recursos en la configuración de Dynamic Media | Acción seleccionada | Destino de publicación |
   | --- | --- | --- |
   | Inmediatamente o <br>después de la activación | Publicación | Experience Manager y Dynamic Media |
   | Inmediatamente o <br>después de la activación | Publicar en Dynamic Media | Ninguna |
   | Publicación selectiva | Publicación | Experience Manager |
   | Publicación selectiva | Publicar en Dynamic Media | Dynamic Media |
   | Inmediatamente o <br>después de la activación | Cancelar publicación | Experience Manager y Dynamic Media |
   | Inmediatamente o <br>después de la activación | Cancelar la publicación de Dynamic Media | Ninguna |
   | Publicación selectiva | Cancelar publicación | Experience Manager |
   | Publicación selectiva | Cancelar la publicación de Dynamic Media | Dynamic Media |

1. En la página **[!UICONTROL Administrar publicación - Ámbito]**, realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee eliminar de la publicación o de la cancelación de la publicación.
   * En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Ámbito]**, pulse **[!UICONTROL Publicar]** o **[!UICONTROL Cancelar publicación]** para iniciar la acción.
1. Pulse **[!UICONTROL Aceptar]**.

## Comprobación del estado de publicación de un recurso {#check-publish-status-of-asset}

Puede utilizar **[!UICONTROL Línea de tiempo]** con **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]** en el Experience Manager para comprobar rápidamente el estado de publicación de un recurso.

**Para comprobar el estado de publicación de un recurso:**

1. En el Experience Manager, en la esquina superior izquierda de la página, pulse el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo de la página, pulse el icono Navegación (justo encima del icono Herramientas) y, a continuación, pulse **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]** (la captura de pantalla que aparece a continuación muestra la **[!UICONTROL Vista de lista]**), abra una carpeta que contenga los recursos que ha publicado o dejado de publicar.
1. Seleccione un recurso para que aparezca con una marca de verificación. Consulte la captura de pantalla siguiente, por ejemplo.
1. Cerca de la esquina superior izquierda de la página, en el menú desplegable, seleccione **[!UICONTROL Línea de tiempo]**. La región **[!UICONTROL Status]** del panel izquierdo muestra el estado de publicación del recurso seleccionado.
Cuando se utiliza **[!UICONTROL Vista de lista]**, aparece una columna adicional para el estado de publicación de **[!UICONTROL Dynamic Media]**.
   * Una carpeta configurada para sincronizar con Dynamic Media muestra la columna **[!UICONTROL Dynamic Media]** de forma predeterminada.
   * Una carpeta *not* configurada para sincronizar con Dynamic Media no muestra la columna Dynamic Media.
      ![Vista de lista y línea de tiempo](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Resolución de problemas de publicación selectiva {#selective-publish-troubleshoot}

Un recurso que no está sincronizado con Dynamic Media pero tiene una acción de publicación de Dynamic Media activada provoca el siguiente mensaje de error y solución:

![Error de publicación selectiva](/help/assets/assets-dm/selective-publish-error.png)
