---
title: Uso de Publicación selectiva en Dynamic Media
description: Información sobre cómo trabajar con Publicación selectiva en Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner, Administrator
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publicación
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '2935'
ht-degree: 4%

---

# Configuración de la publicación selectiva a nivel de carpeta en Dynamic Media {#selective-publish-configure-folder}

Puede elegir publicar o cancelar la publicación de recursos en o desde AEM o Dynamic Media a nivel de carpeta, utilizando **[!UICONTROL Administrar publicación]** o **[!UICONTROL Publicación rápida]** en lugar de confiar únicamente en la **[!UICONTROL Configuración de Dynamic Media]** cuya configuración sea global para todas las carpetas de la instancia de Dynamic Media.

Por ejemplo, con la publicación selectiva puede trabajar en recursos para productos que aún no están activos. En tal caso, un equipo de marketing puede acceder a las imágenes de recorte inteligente y a las representaciones dinámicas sincronizadas con Dynamic Media para que puedan crear materiales promocionales, sin necesidad de publicar estos recursos en Dynamic Media para su envío global.

>[!IMPORTANT]
>
>La publicación selectiva solo está disponible en el modo Dynamic Media - Scene7 .

>[!NOTE]
>
>** Al copiar recursos a y desde carpetas, se borra el estado de publicación de esos recursos. Sin embargo, cuando *mueve* recursos a carpetas cuya propiedad de carpeta está establecida en **[!UICONTROL Publicación selectiva]**, se mantiene el estado de publicación de esos recursos.

Si más adelante decide cambiar la configuración de **[!UICONTROL Publicación selectiva]** en una carpeta, esos cambios solo afectarán a los nuevos recursos que cargue en esa carpeta a partir de ese momento. El estado de publicación de los recursos existentes en la carpeta permanece tal cual hasta que los cambie manualmente desde **[!UICONTROL Publicación rápida]** o el cuadro de diálogo **[!UICONTROL Administrar publicación]**.

La opción de nivel de carpeta **[!UICONTROL Dynamic Media Publish mode]** siempre establece de forma predeterminada el valor que se encuentra en la configuración **[!UICONTROL Publicar recursos]** en la configuración de **[!UICONTROL Dynamic Media.]** Sin embargo, los siguientes pasos en este tema muestran cómo cambiar manualmente este valor predeterminado en el nivel de carpeta (como se describe en los pasos siguientes) para anular el valor de  **[!UICONTROL Configuración de]** Dynamic Media.

Independientemente de si confía en el valor **[!UICONTROL Publicar recursos]** establecido en **[!UICONTROL Configuración de Dynamic Media]** o en el valor **[!UICONTROL Modo de publicación de Dynamic Media]** establecido en las propiedades de nivel de carpeta, aún puede elegir **[!UICONTROL Inmediatamente]**, **[!UICONTROL Tras la activación]** o **[!UICONTROL Publicación selectiva.]** Por ejemplo, puede establecer el valor  **[!UICONTROL Publicar]** recursos en la configuración de  **[!UICONTROL Dynamic Media]** en  **[!UICONTROL Al activarse]**, pero el valor  **[!UICONTROL Dynamic Media]** Publishmode en el nivel de carpeta en Publicación  **[!UICONTROL selectiva]**, viceversa, etc.

Después de configurar la publicación selectiva en una carpeta, puede realizar cualquiera de las siguientes acciones:

* [Publicar recursos de forma selectiva en Dynamic Media o AEM mediante Administrar publicación.](#selective-publish-manage-publication)
* [Cancelar la publicación de forma selectiva desde Dynamic Media o AEM mediante Administrar publicación.](#selective-unpublish-manage-publication)
* [Publicación de recursos en Dynamic Media o AEM mediante Publicación rápida.](#quick-publish-aem-dm)
* [Publicar o cancelar la publicación de forma selectiva mediante resultados de búsqueda.](#selective-publish-unpublish-search-results)

**Para configurar la publicación selectiva en el nivel de carpeta en Dynamic Media**

1. En AEM, pulse el logotipo de AEM para acceder a la consola de navegación global. En el lado izquierdo, pulse el icono Navegación (justo encima del icono Herramientas ) y, a continuación, pulse **[!UICONTROL Assets > Archivos.]**
1. Realice una de las acciones siguientes:
   * Edite las propiedades de una carpeta existente: en **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, vaya a la carpeta cuyas propiedades desee editar. Seleccione la carpeta y, a continuación, en la barra de herramientas, pulse **[!UICONTROL Propiedades.]**
   * Edite las propiedades de una nueva carpeta: en **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, cerca de la esquina superior derecha de la página, pulse **[!UICONTROL Crear > Carpeta.]** En el cuadro de diálogo  **[!UICONTROL Crear]** carpeta , introduzca un título (obligatorio) para la carpeta y, a continuación, pulse  **[!UICONTROL Crear.]** Seleccione la carpeta y, a continuación, en la barra de herramientas, pulse  **[!UICONTROL Propiedades.]**

1. En la lista desplegable **[!UICONTROL Sync mode]**, seleccione una de las siguientes opciones:

   | Modo de sincronización | Descripción |
   | --- | --- |
   | **[!UICONTROL Heredado]** | No hay ningún valor de sincronización explícito en la carpeta; en su lugar, la carpeta hereda el valor de sincronización de una de sus carpetas antecesoras o el modo predeterminado establecido en la configuración **[!UICONTROL Dynamic Media.]** El estado detallado de  **** Heredado se muestra mediante una información del objeto. |
   | **[!UICONTROL Sincronizar todo en este diagrama secundario de carpetas con dynamicmedia]** | Para que la publicación en Dynamic Media se realice correctamente, los recursos deben sincronizarse con Dynamic Media. Al seleccionar esta opción, se incluirán todos los recursos de este subárbol para sincronizarlos con Dynamic Media. La configuración específica de la carpeta anula la configuración predeterminada de la **[!UICONTROL Configuración de Dynamic Media.]** |
   | **[!UICONTROL Excluir todo lo que hay en este subárbol de carpetas de la sincronización con medios dinámicos]** | Excluya todos los recursos de este subárbol de la sincronización con Dynamic Media. |

   ![Publicación selectiva a nivel de carpeta](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. En la lista desplegable **[!UICONTROL Dynamic Media Publish mode]**, seleccione una opción. Tenga en cuenta que la opción **[!UICONTROL Dynamic Media Publish mode]** siempre establece de forma predeterminada el valor establecido en la **[!UICONTROL Configuración de Dynamic Media.]** Sin embargo, puede anular manualmente este valor predeterminado de configuración de  **[!UICONTROL Dynamic Media]** utilizando una de las siguientes opciones.

   >[!IMPORTANT]
   >
   >Tenga en cuenta que, independientemente de la opción de modo Publicación de Dynamic Media que seleccione, cualquier actualización que realice posteriormente en un recurso que ya esté *publicado*, esas actualizaciones se publican inmediatamente sin que el usuario tome ninguna otra medida.

   | Opción de modo Publicación de Dynamic Media | Descripción |
   | --- | --- |
   | **[!UICONTROL Inmediatamente]** | Cuando los recursos se cargan en esta carpeta, el sistema los incorpora en AEM y proporciona la URL/Incrustar al instante. Esta opción está vinculada únicamente a AEM publicación y no es necesario que el usuario intervenga para publicar recursos.<br>Esta opción  ** no está disponible si ha seleccionado  **[!UICONTROL Excluir todo en este subárbol de carpetas del modelo de]** sincronización con dynamic media  **[!UICONTROL Sync]** en el paso anterior. |
   | **[!UICONTROL Tras la activación]** | Cuando los recursos se cargan en esta carpeta, primero debe publicar explícitamente el recurso antes de proporcionar un vínculo de URL/incrustación. Esta opción está vinculada únicamente a AEM publicación.<br>Esta opción  ** no está disponible si ha seleccionado  **[!UICONTROL Excluir todo en este subárbol de carpetas del modelo de]** sincronización con dynamic media  **[!UICONTROL Sync]** en el paso anterior. |
   | **[!UICONTROL Publicación selectiva]** | Los recursos se publican a su elección, ya sea en AEM o en Dynamic Media para su entrega en el dominio público. Ambos métodos de publicación se excluyen mutuamente.  Es decir, puede publicar recursos en DMS7 para que pueda utilizar funciones como Recorte inteligente o representaciones dinámicas. O bien, puede publicar recursos exclusivamente en AEM para obtener una vista previa segura; esos mismos activos son *no* publicados en DMS7 para su envío en el dominio público. Esta opción no está disponible si ha seleccionado **[!UICONTROL Excluir todo en este subárbol de carpetas de la sincronización de medios dinámicos]** en **[!UICONTROL Modo de sincronización]** en el paso anterior. |

1. En la esquina superior derecha de la página, pulse **[!UICONTROL Guardar y cerrar]** y, a continuación, pulse **[!UICONTROL Aceptar]** para volver a AEM Assets.

## Publicar recursos de forma selectiva en Dynamic Media o AEM mediante Administrar publicación{#selective-publish-manage-publication}

Antes de utilizar **[!UICONTROL Administrar publicación]** para publicar selectivamente recursos en Dynamic Media o AEM, asegúrese de que ha establecido la opción **[!UICONTROL Publicar recursos]** en **[!UICONTROL Configuración de Dynamic Media]** en **[!UICONTROL Publicación selectiva]** o la publicación selectiva configurada a nivel de carpeta.

Consulte [Creación de una configuración de Dynamic Media](#configuring-dynamic-media-cloud-services) o [Configuración de la publicación selectiva a nivel de carpeta en Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>La publicación selectiva solo está disponible en el modo Dynamic Media - Scene7 .

>[!NOTE]
>
>** Al copiar recursos a y desde carpetas, se borra el estado de publicación de esos recursos. Sin embargo, cuando *mueve* recursos a carpetas cuya propiedad de carpeta está establecida en **[!UICONTROL Publicación selectiva]**, se mantiene el estado de publicación de esos recursos.

**Para publicar selectivamente recursos en Dynamic Media o AEM mediante Administrar publicación**

1. En AEM, pulse el logotipo de AEM para acceder a la consola de navegación global. En el lado izquierdo, pulse el icono Navegación (justo encima del icono Herramientas ) y, a continuación, pulse **[!UICONTROL Assets > Archivos.]**
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Vaya a una carpeta cuyos recursos desee publicar. Seleccione la carpeta y, a continuación, en la barra de herramientas, pulse **[!UICONTROL Administrar publicación.]**  Puede que le resulte útil utilizar la  **[!UICONTROL Vista de]** lista para poder comprobar con mayor facilidad el estado de publicación de una carpeta en particular.
   * Vaya a una carpeta cuyos recursos desee publicar. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, pulse **[!UICONTROL Administrar publicación.]** Puede que le resulte útil utilizar la  **[!UICONTROL Vista de]** lista para poder comprobar con mayor facilidad el estado de publicación de un recurso en particular.

      >[!NOTE]
      >
      >Si no se ve **[!UICONTROL Administrar publicación]** en la barra de herramientas, pulse el botón de puntos suspensivos y, a continuación, seleccione **[!UICONTROL Administrar publicación]** en el menú de la lista.

1. En la página **[!UICONTROL Administrar publicación: opciones]**, en **[!UICONTROL Acción]**, seleccione el tipo de activación que desee.

   | Acción | Descripción |
   | --- | --- |
   | **[!UICONTROL Publicar]**  (en AEM) | Seleccione esta opción para publicar recursos en AEM para una vista previa segura. |
   | **[!UICONTROL Publicar en Dynamic Media]** | Seleccione esta opción para publicar recursos en Dynamic Media para su entrega en el dominio público o para que pueda utilizar funciones como Recorte inteligente o representaciones dinámicas.<br>Esta opción solo está disponible si el modo de publicación de  **[!UICONTROL Dynamic Media]** está establecido en Publicación  **[!UICONTROL selectiva]** en las propiedades de la carpeta. |

1. En **[!UICONTROL Programar]**, establezca la temporización de la publicación.

   | Programa | Descripción |
   | --- | --- |
   | **[!UICONTROL Ahora]** | Seleccione para publicar los recursos inmediatamente. |
   | **[!UICONTROL Más tarde]** | Seleccione para publicar los recursos en una fecha y hora concretas. |

1. En la esquina superior derecha de la página **[!UICONTROL Administrar publicación]**, pulse **[!UICONTROL Siguiente.]**
1. En la página **[!UICONTROL Administrar publicación - Ámbito]**, realice una de las siguientes acciones:

   * Si es necesario, seleccione uno o varios recursos que desee eliminar de la publicación.
   * En la esquina superior derecha de la página **[!UICONTROL Administrar publicación: ámbito]**, pulse **[!UICONTROL Publicar]** o **[!UICONTROL Publicar en Dynamic Media.]**
1. Toque **[!UICONTROL Aceptar.]**

### Cancelar la publicación selectivamente de Dynamic Media o AEM usando Administrar publicación {#selective-unpublish-manage-publication}

1. En AEM, pulse el logotipo de AEM para acceder a la consola de navegación global. En el lado izquierdo, pulse el icono Navegación (justo encima del icono Herramientas ) y, a continuación, pulse **[!UICONTROL Assets > Archivos.]**
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Desplácese a la carpeta cuyos recursos desee cancelar la publicación. Seleccione la carpeta y, a continuación, en la barra de herramientas, pulse **[!UICONTROL Administrar publicación.]**  Puede que le resulte útil utilizar la  **[!UICONTROL Vista de]** lista para poder comprobar con mayor facilidad el estado de publicación de una carpeta en particular.
   * Desplácese a la carpeta cuyos recursos desee cancelar la publicación. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, pulse **[!UICONTROL Administrar publicación.]** Puede que le resulte útil utilizar la  **[!UICONTROL Vista de]** lista para poder comprobar con mayor facilidad el estado de publicación de un recurso en particular.

      >[!NOTE]
      >
      >Si no se ve **[!UICONTROL Administrar publicación]** en la barra de herramientas, pulse el botón de puntos suspensivos y, a continuación, seleccione **[!UICONTROL Administrar publicación]** en el menú de la lista.

1. En la página **[!UICONTROL Administrar publicación: opciones]**, en **[!UICONTROL Acción]**, seleccione el tipo de desactivación que desee.

   | Acción | Descripción |
   | --- | --- |
   | **[!UICONTROL Cancelar publicación]**  (desde AEM) | Seleccione esta opción para cancelar la publicación de recursos de AEM. |
   | **[!UICONTROL Cancelar la publicación de Dynamic Media]** | Seleccione esta opción para cancelar la publicación de recursos desde Dynamic Media.<br>Esta opción solo está disponible si el modo de publicación de  **[!UICONTROL Dynamic Media]** está establecido en Publicación  **[!UICONTROL selectiva]** en las propiedades de la carpeta. |

1. En **[!UICONTROL Schedule]**, establezca el tiempo de desactivación.

   | Programa | Descripción |
   | --- | --- |
   | **[!UICONTROL Ahora]** | Seleccione para cancelar la publicación de los recursos inmediatamente. |
   | **[!UICONTROL Más tarde]** | Seleccione para cancelar la publicación de los recursos en una fecha y hora concretas. |

1. En la esquina superior derecha de la página **[!UICONTROL Administrar publicación]**, pulse **[!UICONTROL Siguiente.]**
1. En la página **[!UICONTROL Administrar publicación - Ámbito]**, realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee eliminar de la cancelación de la publicación.
   * En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Ámbito]**, pulse **[!UICONTROL Cancelar publicación]** o **[!UICONTROL Cancelar publicación desde Dynamic Media.]**
1. Toque **[!UICONTROL Aceptar.]**

## Publicación de recursos en Dynamic Media o AEM mediante Publicación rápida {#quick-publish-aem-dm}

Puede utilizar **[!UICONTROL Publicación rápida]** para casos sencillos de activación de recursos. **[!UICONTROL Publicación rápida]** publica los recursos seleccionados inmediatamente, sin más interacción del usuario. Debido a esto, cualquier referencia no publicada también se publica automáticamente.

>[!NOTE]
>
>Para utilizar **[!UICONTROL Publicación rápida]** para publicar recursos en Dynamic Media o AEM, asegúrese de que **[!UICONTROL Publicación selectiva]** esté habilitada en su **[!UICONTROL Configuración de Dynamic Media]** o en las propiedades de carpeta de la carpeta seleccionada.

**Para publicar recursos en Dynamic Media o AEM con Publicación rápida**

1. En AEM, pulse el logotipo de AEM para acceder a la consola de navegación global. En el lado izquierdo de la página, pulse el icono Navegación (justo encima del icono Herramientas ) y, a continuación, en el lado derecho de la página, pulse **[!UICONTROL Assets > Archivos.]**
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Vaya a una carpeta cuyos recursos desee publicar. Seleccione la carpeta y, a continuación, en la barra de herramientas, pulse **[!UICONTROL Publicación rápida.]**  Puede que le resulte útil utilizar la  **[!UICONTROL Vista de]** lista para poder comprobar con mayor facilidad el estado de publicación de una carpeta en particular.
   * Vaya a una carpeta cuyos recursos desee publicar. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, pulse **[!UICONTROL Publicación rápida.]** Puede que le resulte útil utilizar la  **[!UICONTROL Vista de]** lista para poder comprobar con mayor facilidad el estado de publicación de un recurso en particular.

      >[!NOTE]
      >
      >Si no se ve **[!UICONTROL Publicación rápida]** en la barra de herramientas, pulse el botón de puntos suspensivos en su lugar y, a continuación, seleccione **[!UICONTROL Publicación rápida]** en el menú de la lista.

      ![Publicación rápida a nivel de carpeta en Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Seleccione una de las siguientes opciones en la lista de menú **[!UICONTROL Publicación rápida]**.

   | Opción Publicación rápida | Qué hace |
   | --- | --- | 
   | Publicar en AEM | Publica los recursos seleccionados inmediatamente para AEM. |
   | Publicar en Brand Portal | Publica los recursos seleccionados inmediatamente en **[!UICONTROL Brand Portal.]**<br>Esta opción solo está disponible si la instancia de AEM Assets tiene**[!UICONTROL  Brand ]**Portal ya configurado. |
   | Publicar en Dynamic Media | Publica los recursos seleccionados inmediatamente en Dynamic Media.<br>Un recurso ya debe sincronizarse con Dynamic Media. Si es necesario, asegúrese de que **[!UICONTROL Sync mode]** en las propiedades de una carpeta ya esté configurado como **[!UICONTROL Sincronice todo en este subárbol de carpetas con dynamicMedia.]** |

1. Pulse **[!UICONTROL Aceptar]** y, a continuación, pulse **[!UICONTROL Cerrar.]**

## Publicar o cancelar la publicación de recursos de forma selectiva mediante los resultados de búsqueda {#selective-publish-unpublish-search-results}

Los resultados de búsqueda pueden mostrar recursos de todas las carpetas de recursos que tengan diferentes configuraciones de publicación de Dynamic Media. Si ha seleccionado uno o varios recursos de los resultados de búsqueda y los recursos tienen diferentes configuraciones del modo de publicación de Dynamic Media, puede almacenar en déclencheur **[!UICONTROL Administrar publicación]** desde la barra de herramientas para publicar o cancelar la publicación.

Consulte también [Buscar recursos en AEM.](/help/assets/search-assets.md)

**Para publicar o cancelar la publicación de recursos de forma selectiva mediante los resultados de búsqueda**

1. En AEM, en la esquina superior izquierda de la página, pulse el logotipo de AEM para acceder a la consola de navegación global. En el lado izquierdo de la página, pulse el icono Navegación (justo encima del icono Herramientas) y, a continuación, pulse **[!UICONTROL Assets > Archivos.]**
1. En la barra de herramientas, cerca de la esquina superior derecha de la página, pulse el icono Buscar (lupa).
1. En el campo de texto **[!UICONTROL Type to search]**, introduzca una palabra clave y, a continuación, pulse **[!UICONTROL Enter.]**
1. Cerca de la esquina superior derecha de la página, pulse el icono **[!UICONTROL Vista de lista]**.
1. Cerca de la esquina superior izquierda de la página, pulse el icono **[!UICONTROL Filters]**.

   ![Vista de lista y filtros en los resultados de búsqueda](/help/assets/assets-dm/select-publish-search-result.png)

1. En el panel izquierdo, expanda **[!UICONTROL Status]** y luego expanda el predicado de búsqueda **[!UICONTROL Dynamic Media]**.
1. Utilice las casillas de verificación **[!UICONTROL Publicado]** y **[!UICONTROL No publicado]** para restringir aún más los resultados de búsqueda según el estado publicado de los recursos de Dynamic Media.
Opcionalmente, puede utilizar estas casillas de verificación junto con el predicado de búsqueda **[!UICONTROL Publicar]** para refinar los resultados de búsqueda de los recursos de AEM **[!UICONTROL Publicados]** y **[!UICONTROL No publicados]**.
1. Realice una de las acciones siguientes:
   * Seleccione uno o varios recursos que desee publicar o cancelar la publicación.
   * Cerca de la esquina superior derecha de la página **[!UICONTROL Resultados de búsqueda]**, pulse **[!UICONTROL Seleccionar todo.]**
1. En la barra de herramientas, pulse **[!UICONTROL Administrar publicación.]** Es posible que deba pulsar el icono de puntos suspensivos en la barra de herramientas para ver  **[!UICONTROL Administrar publicación.]**
1. En la página **[!UICONTROL Administrar publicación: opciones]**, seleccione la acción que desee.

   | Acción seleccionada | Publicar recursos en la configuración de Dynamic Media | Los recursos son |
   | --- | --- | --- |
   | Publicación | Inmediatamente o después de la activación | Publicado en AEM y Dynamic Media. |
   | Publicación | Publicación selectiva | Publicado solo para AEM. |
   | Cancelar publicación | Inmediatamente o después de la activación | No publicado desde AEM y Dynamic Media. |
   | Cancelar publicación | Publicación selectiva | No publicado solo desde AEM. |
   | Publicar en Dynamic Media | Inmediatamente o después de la activación | No publicado en AEM, Dynamic Media o ambos. |
   | Publicar en Dynamic Media | Publicación selectiva | Solo se publica en Dynamic Media. |
   | Cancelar la publicación de Dynamic Media | Inmediatamente o después de la activación | No se canceló la publicación de AEM, Dynamic Media o ambos. |
   | Cancelar la publicación de Dynamic Media | Publicación selectiva | Cancelado la publicación solo desde Dynamic Media. |

1. En **[!UICONTROL Schedule]**, establezca el tiempo de desactivación.

   | Programación seleccionada | Qué sucede |
   | --- | --- |
   | Ahora | La acción seleccionada se realiza inmediatamente. |
   | Más tarde | La acción seleccionada se ejecuta en la fecha y hora concretas seleccionadas. |

1. En la esquina superior derecha de la página **[!UICONTROL Administrar publicación: opciones]**, pulse **[!UICONTROL Siguiente.]**
1. (Opcional) En la página **[!UICONTROL Administrar publicación - Ámbito]**, revise la columna **[!UICONTROL Publicar destino]** de la tabla para los recursos seleccionados.

   | Publicar recursos en la configuración de Dynamic Media | Acción seleccionada | Destino de publicación |
   | --- | --- | --- |
   | Inmediatamente o <br>después de la activación | Publicación | AEM y Dynamic Media |
   | Inmediatamente o <br>después de la activación | Publicar en Dynamic Media | Ninguna |
   | Publicación selectiva | Publicación | AEM |
   | Publicación selectiva | Publicar en Dynamic Media | Dynamic Media |
   | Inmediatamente o <br>después de la activación | Cancelar publicación | AEM y Dynamic Media |
   | Inmediatamente o <br>después de la activación | Cancelar la publicación de Dynamic Media | Ninguna |
   | Publicación selectiva | Cancelar publicación | AEM |
   | Publicación selectiva | Cancelar la publicación de Dynamic Media | Dynamic Media |

1. En la página **[!UICONTROL Administrar publicación - Ámbito]**, realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee eliminar de la publicación o de la cancelación de la publicación.
   * En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Ámbito]**, pulse **[!UICONTROL Publicar]** o **[!UICONTROL Cancelar publicación]** para iniciar la acción.
1. Toque **[!UICONTROL Aceptar.]**

## Comprobación del estado de publicación de un recurso {#check-publish-status-of-asset}

Puede utilizar **[!UICONTROL Línea de tiempo]** con **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]** en AEM para comprobar rápidamente el estado de publicación de un recurso.

**Para comprobar el estado de publicación de un recurso**

1. En AEM, en la esquina superior izquierda de la página, pulse el logotipo de AEM para acceder a la consola de navegación global. En el lado izquierdo de la página, pulse el icono Navegación (justo encima del icono Herramientas) y, a continuación, pulse **[!UICONTROL Assets > Archivos.]**
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]** (la captura de pantalla que aparece a continuación muestra la **[!UICONTROL Vista de lista]**), abra una carpeta que contenga los recursos que ha publicado o dejado de publicar.
1. Seleccione un recurso para que aparezca con una marca de verificación. Consulte la captura de pantalla siguiente, por ejemplo.
1. Cerca de la esquina superior izquierda de la página, en el menú desplegable, seleccione **[!UICONTROL Línea de tiempo.]** La  **** región Estado del panel izquierdo muestra el estado de publicación del recurso seleccionado.
Cuando se utiliza **[!UICONTROL Vista de lista]**, aparece una columna adicional para el estado de publicación de **[!UICONTROL Dynamic Media]**.
   * Una carpeta configurada para sincronizar con Dynamic Media mostrará la columna **[!UICONTROL Dynamic Media]** de forma predeterminada.
   * Una carpeta *not* configurada para sincronizar con Dynamic Media no mostrará la columna de Dynamic Media.
      ![Vista de lista y línea de tiempo](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Solución de problemas de publicación selectiva {#selective-publish-troubleshoot}

Un recurso que no está sincronizado con Dynamic Media pero tiene una acción de publicación de Dynamic Media activada provoca el siguiente mensaje de error y solución:

![Error de publicación selectiva](/help/assets/assets-dm/selective-publish-error.png)
