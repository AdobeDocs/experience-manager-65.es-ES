---
title: Trabajo con Publicación selectiva en Dynamic Media
description: Puede optar por publicar recursos o cancelar la publicación de estos en Adobe Experience Manager o Dynamic Media en el nivel de carpeta. Puede utilizar Administrar publicación o Publicación rápida en lugar de depender únicamente de la Configuración de Dynamic Media cuya configuración sea global para todas las carpetas de la instancia de Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 3%

---

# Configuración de la publicación selectiva en el nivel de carpeta en Dynamic Media {#selective-publish-configure-folder}

Puede optar por publicar recursos o cancelar la publicación de estos en Adobe Experience Manager o Dynamic Media en el nivel de carpeta. Puede usar cualquiera de las siguientes opciones **[!UICONTROL Administrar publicación]** o **[!UICONTROL Publicación rápida]** en lugar de depender únicamente de **[!UICONTROL Configuración de Dynamic Media]** cuya configuración sea global para todas las carpetas de la instancia de Dynamic Media.

Por ejemplo, con la publicación selectiva puede trabajar en los recursos de los productos que aún no están activos. En tal caso, un equipo de marketing puede acceder a las imágenes de recorte inteligente y a las representaciones dinámicas sincronizadas con Dynamic Media. Pueden crear materiales promocionales, sin necesidad de publicar estos recursos en Dynamic Media para su distribución global.

>[!IMPORTANT]
>
>Publicación selectiva solo está disponible en el modo Dynamic Media - Scene7.

>[!NOTE]
>
>*Copiando* recursos hacia y desde carpetas borra el estado de publicación de esos recursos. Sin embargo, cuando *mover* recursos a y desde carpetas cuya propiedad folder está establecida en **[!UICONTROL Publicación selectiva]**, el estado de publicación de esos recursos se mantiene.

Si decide cambiar más adelante la **[!UICONTROL Publicación selectiva]** en una carpeta, esos cambios afectan únicamente a los nuevos recursos que cargue en esa carpeta a partir de ese momento. El estado de publicación de los recursos existentes en la carpeta permanece tal cual hasta que los cambie manualmente desde **[!UICONTROL Publicación rápida]** o el **[!UICONTROL Administrar publicación]** Cuadro de diálogo.

El nivel de carpeta **[!UICONTROL Modo de publicación de Dynamic Media]** La opción siempre toma el valor predeterminado que se encuentra en la variable **[!UICONTROL Publicar recursos]** configuración en su **[!UICONTROL Configuración de Dynamic Media]**. Sin embargo, los pasos siguientes de este tema le muestran cómo cambiar manualmente este valor predeterminado en el nivel de carpeta (como se describe en los pasos siguientes) para anular la variable **[!UICONTROL Configuración de Dynamic Media]** valor.

Independientemente de si confía en alguna de las siguientes opciones:

* **[!UICONTROL Publicar recursos]** valor establecido en **[!UICONTROL Configuración de Dynamic Media]**.
* **[!UICONTROL Modo de publicación de Dynamic Media]** valor establecido en propiedades de nivel de carpeta.

Puede elegir **[!UICONTROL Inmediata]**, **[!UICONTROL En la activación]**, o **[!UICONTROL Publicación selectiva]**. Por ejemplo, puede establecer la variable **[!UICONTROL Publicar recursos]** valor en su **[!UICONTROL Configuración de Dynamic Media]** hasta **[!UICONTROL En la activación]**, pero configure el **[!UICONTROL Publicación de Dynamic Media]** valor de modo en el nivel de carpeta a **[!UICONTROL Publicación selectiva]** y, a la inversa.

Después de configurar la publicación selectiva en una carpeta, puede realizar cualquiera de las siguientes acciones:

* [Publicar recursos de forma selectiva en Dynamic Media o Experience Manager mediante Administrar publicación](#selective-publish-manage-publication).
* [Cancelar la publicación selectiva de recursos desde Dynamic Media o Experience Manager mediante Administrar publicación](#selective-unpublish-manage-publication).
* [Publicación de recursos en Dynamic Media o Experience Manager mediante Publicación rápida](#quick-publish-aem-dm).
* [Publicar o cancelar la publicación selectiva de recursos mediante resultados de búsqueda](#selective-publish-unpublish-search-results).

**Para configurar la publicación selectiva en el nivel de carpeta en Dynamic Media:**

1. En Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo, seleccione el icono Navegación (justo encima del icono Herramientas ) y, a continuación, seleccione **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Realice una de las siguientes acciones:
   * Editar las propiedades de una carpeta existente: en **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]**, o **[!UICONTROL Vista de lista]**, vaya a una carpeta cuyas propiedades desee editar. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.
   * Editar las propiedades de una nueva carpeta: en **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]**, o **[!UICONTROL Vista de lista]**, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Crear]** > **[!UICONTROL Carpeta]**. En el **[!UICONTROL Crear carpeta]** , introduzca un título (obligatorio) para la carpeta y, a continuación, seleccione **[!UICONTROL Crear]**. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.

1. En el **[!UICONTROL Modo de sincronización]** , seleccione una de las siguientes opciones:

   | Modo de sincronización | Descripción |
   | --- | --- |
   | **[!UICONTROL Heredado]** | No hay ningún valor de sincronización explícito en la carpeta; en su lugar, la carpeta hereda el valor de sincronización de una de sus carpetas antecesoras o del modo predeterminado establecido en su **[!UICONTROL Configuración de Dynamic Media]**. El estado detallado de **[!UICONTROL Heredado]** muestra mediante la información del objeto. |
   | **[!UICONTROL Sincronizar todo en este subárbol de carpetas con Dynamic Media]** | Para que la publicación en Dynamic Media se realice correctamente, los recursos deben sincronizarse con Dynamic Media. Al seleccionar esta opción, se incluyen todos los recursos de este subárbol para sincronizarlos con Dynamic Media. La configuración específica de la carpeta anula la configuración predeterminada de **[!UICONTROL Configuración de Dynamic Media]**. |
   | **[!UICONTROL Excluir todo el contenido del árbol secundario de carpetas de la sincronización de Dynamic Media]** | Excluya todos los recursos de este subárbol de la sincronización con Dynamic Media. |

   ![Publicación selectiva a nivel de carpeta](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. En el **[!UICONTROL Modo de publicación de Dynamic Media]** , seleccione una opción. El **[!UICONTROL Modo de publicación de Dynamic Media]** La opción siempre toma el valor predeterminado establecido en la variable **[!UICONTROL Configuración de Dynamic Media]**. Sin embargo, puede anular manualmente este valor predeterminado **[!UICONTROL Configuración de Dynamic Media]** mediante una de las siguientes opciones.

   >[!IMPORTANT]
   >
   >Independientemente de la opción del modo Publicación de Dynamic Media que seleccione, cualquier actualización que realice posteriormente en un recurso que esté *ya* Cuando se publican, esas actualizaciones se publican inmediatamente sin que el usuario tenga que hacer nada más.
   >
   >Si se actualiza un vídeo publicado, debe publicarse de nuevo para reflejar los cambios en la entrega.

   | Opción del modo Publicación de Dynamic Media | Descripción |
   | --- | --- |
   | **[!UICONTROL Inmediata]** | Cuando los recursos se cargan en esta carpeta, el sistema los incorpora en el Experience Manager y proporciona la URL o la incrustación de forma inmediata. Esta opción solo está vinculada a la publicación del Experience Manager y no es necesaria ninguna intervención del usuario para publicar los recursos.<br>Esta opción es *no* disponible si ha seleccionado **[!UICONTROL Excluir todo el contenido del árbol secundario de carpetas de la sincronización de Dynamic Media]** in **[!UICONTROL Modo de sincronización]** en el paso anterior. |
   | **[!UICONTROL Tras la activación]** | Cuando los recursos se cargan en esta carpeta, primero debe publicarlos explícitamente antes de proporcionar un vínculo URL/incrustado. Esta opción solo está vinculada a la publicación en Experience Manager.<br>Esta opción es *no* disponible si ha seleccionado **[!UICONTROL Excluir todo el contenido del árbol secundario de carpetas de la sincronización de Dynamic Media]** in **[!UICONTROL Modo de sincronización]** en el paso anterior. |
   | **[!UICONTROL Publicación selectiva]** | Los recursos se publican a su elección de Experience Manager o de Dynamic Media para su publicación en el dominio público. Ambos métodos de publicación son mutuamente excluyentes. Es decir, puede publicar recursos en DMS7 para poder utilizar funciones como Recorte inteligente o representaciones dinámicas. O bien, puede publicar recursos exclusivamente en Experience Manager para una previsualización segura; estos mismos recursos son *no* publicado en DMS7 para su envío de dominio público. Esta opción no está disponible si ha seleccionado **[!UICONTROL Excluir todo el contenido del árbol secundario de carpetas de la sincronización de Dynamic Media]** in **[!UICONTROL Modo de sincronización]** en el paso anterior. |

1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar y cerrar]**, luego seleccione **[!UICONTROL OK]** para volver a Experience Manager Assets.

## Publicar recursos de forma selectiva en Dynamic Media o Experience Manager mediante Administrar publicación{#selective-publish-manage-publication}

Antes de usar **[!UICONTROL Administrar publicación]** para publicar recursos de forma selectiva en Dynamic Media o Experience Manager, asegúrese de haber establecido una de las siguientes opciones:

* El **[!UICONTROL Publicar recursos]** opción en **[!UICONTROL Configuración de Dynamic Media]** hasta **[!UICONTROL Publicación selectiva]**
* Se ha configurado la publicación selectiva en el nivel de carpeta.

Consulte [Crear una configuración de Dynamic Media](#configuring-dynamic-media-cloud-services) o [Configuración de la publicación selectiva en el nivel de carpeta en Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>Publicación selectiva solo está disponible en el modo Dynamic Media - Scene7.

>[!NOTE]
>
>*Copiando* recursos hacia y desde carpetas borra el estado de publicación de esos recursos. Sin embargo, cuando *mover* recursos a y desde carpetas cuya propiedad folder está establecida en **[!UICONTROL Publicación selectiva]**, el estado de publicación de esos recursos se mantiene.

**Para publicar recursos de forma selectiva en Dynamic Media o Experience Manager mediante Administrar publicación:**

1. En Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo, seleccione el icono Navegación (justo encima del icono Herramientas ) y, a continuación, seleccione **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Entrada **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]**, o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Vaya a una carpeta cuyos recursos desee publicar. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Uso **[!UICONTROL Vista de lista]** para que pueda comprobar más fácilmente el estado de publicación de una carpeta en particular.
   * Vaya a una carpeta cuyos recursos desee publicar. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Uso **[!UICONTROL Vista de lista]** para que pueda comprobar más fácilmente el estado de publicación de un recurso en particular.

     >[!NOTE]
     >
     >If **[!UICONTROL Administrar publicación]** no aparece en la barra de herramientas, seleccione el botón de puntos suspensivos y, a continuación, seleccione **[!UICONTROL Administrar publicación]** en el menú de la lista.

1. En el **[!UICONTROL Administrar publicación: opciones]** página, debajo de **[!UICONTROL Acción]**, seleccione el tipo de activación que desee.

   | Acción | Descripción |
   | --- | --- |
   | **[!UICONTROL Publish]** (al Experience Manager) | Seleccione esta opción para poder publicar recursos en el Experience Manager para una previsualización segura. |
   | **[!UICONTROL Publicar en Dynamic Media]** | Seleccione esta opción para poder publicar recursos en Dynamic Media para su entrega en el dominio público o para poder utilizar funciones como Recorte inteligente o representaciones dinámicas.<br>Esta opción solo está disponible si **[!UICONTROL Modo de publicación de Dynamic Media]** se establece en **[!UICONTROL Publicación selectiva]** en las propiedades de la carpeta. |

1. En **[!UICONTROL Programación]**, establezca el tiempo de la publicación.

   | Programación | Descripción |
   | --- | --- |
   | **[!UICONTROL Ahora]** | Seleccione para publicar los recursos inmediatamente. |
   | **[!UICONTROL Más tarde]** | Seleccione para publicar los recursos en una fecha y hora determinadas. |

1. En la esquina superior derecha de la **[!UICONTROL Administrar publicación]** página, seleccione **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Administrar publicación - Ámbito]** , realice una de las siguientes acciones:

   * Si es necesario, seleccione uno o varios recursos que desee eliminar de la publicación.
   * En la esquina superior derecha de la **[!UICONTROL Administrar publicación - Ámbito]** página, seleccione **[!UICONTROL Publish]** o **[!UICONTROL Publicar en Dynamic Media]**.
1. Seleccionar **[!UICONTROL OK]**.

### Cancelar la publicación selectiva de recursos desde Dynamic Media o Experience Manager mediante Administrar publicación {#selective-unpublish-manage-publication}

1. En Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo, seleccione el icono Navegación (justo encima del icono Herramientas ) y, a continuación, seleccione **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Entrada **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]**, o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Vaya a una carpeta cuyos recursos desee cancelar la publicación. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Uso **[!UICONTROL Vista de lista]** para que pueda comprobar más fácilmente el estado de publicación de una carpeta en particular.
   * Vaya a una carpeta cuyos recursos desee cancelar la publicación. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Uso **[!UICONTROL Vista de lista]** para que pueda comprobar más fácilmente el estado de publicación de un recurso en particular.

     >[!NOTE]
     >
     >If **[!UICONTROL Administrar publicación]** no aparece en la barra de herramientas, seleccione el botón de puntos suspensivos y, a continuación, seleccione **[!UICONTROL Administrar publicación]** en el menú de la lista.

1. En el **[!UICONTROL Administrar publicación: opciones]** página, debajo de **[!UICONTROL Acción]**, seleccione el tipo de desactivación que desee.

   | Acción | Descripción |
   | --- | --- |
   | **[!UICONTROL Cancelar publicación]** (del Experience Manager) | Seleccione esta opción si desea cancelar la publicación de recursos del Experience Manager. |
   | **[!UICONTROL Cancelar publicación de Dynamic Media]** | Seleccione esta opción si desea cancelar la publicación de recursos desde Dynamic Media.<br>Esta opción solo está disponible si **[!UICONTROL Modo de publicación de Dynamic Media]** se establece en **[!UICONTROL Publicación selectiva]** en las propiedades de la carpeta. |

1. En **[!UICONTROL Programación]**, establezca el tiempo de desactivación.

   | Programación | Descripción |
   | --- | --- |
   | **[!UICONTROL Ahora]** | Seleccione para cancelar la publicación de los recursos inmediatamente. |
   | **[!UICONTROL Más tarde]** | Seleccione para cancelar la publicación de los recursos en una fecha y hora determinadas. |

1. En la esquina superior derecha de la **[!UICONTROL Administrar publicación]** página, seleccione **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Administrar publicación - Ámbito]** , realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee eliminar para cancelar la publicación.
   * En la esquina superior derecha de la **[!UICONTROL Administrar publicación - Ámbito]** página, seleccione **[!UICONTROL Cancelar publicación]** o **[!UICONTROL Cancelar publicación de Dynamic Media]**.
1. Seleccionar **[!UICONTROL OK]**.

## Publicación de recursos en Dynamic Media o Experience Manager mediante Publicación rápida {#quick-publish-aem-dm}

Puede utilizar **[!UICONTROL Publicación rápida]** para casos de activación de recursos simples. **[!UICONTROL Publicación rápida]** publica los recursos seleccionados inmediatamente sin ninguna otra interacción del usuario. Debido a esta acción, todas las referencias no publicadas también se publican automáticamente.

>[!NOTE]
>
>Para usar **[!UICONTROL Publicación rápida]** para publicar recursos en Dynamic Media o Experience Manager, asegúrese de lo siguiente **[!UICONTROL Publicación selectiva]** está habilitado en su **[!UICONTROL Configuración de Dynamic Media]** o en las propiedades de la carpeta de la carpeta seleccionada.

**Para publicar recursos en Dynamic Media o Experience Manager mediante Publicación rápida:**

1. En Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global. En la parte izquierda de la página, seleccione el icono Navegación (justo encima del icono Herramientas ) y, a continuación, en la parte derecha de la página, seleccione **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Entrada **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]**, o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Vaya a una carpeta cuyos recursos desee publicar. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**. Uso **[!UICONTROL Vista de lista]** para que pueda comprobar más fácilmente el estado de publicación de una carpeta en particular.
   * Vaya a una carpeta cuyos recursos desee publicar. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**. Uso **[!UICONTROL Vista de lista]** para que pueda comprobar más fácilmente el estado de publicación de un recurso en particular.

     >[!NOTE]
     >
     >If **[!UICONTROL Publicación rápida]** no aparece en la barra de herramientas, seleccione el botón de puntos suspensivos y, a continuación, seleccione **[!UICONTROL Publicación rápida]** en el menú de la lista.

     ![Publicación rápida en Dynamic Media a nivel de carpeta](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Seleccione una de las siguientes opciones de la **[!UICONTROL Publicación rápida]** lista de menús.

   | Opción Publicación rápida | Qué hace |
   | --- | --- | 
   | Publicar en Experience Manager | Publica los recursos seleccionados inmediatamente en el Experience Manager. |
   | Publicar en Brand Portal | Publica los recursos seleccionados inmediatamente en **[!UICONTROL Brand Portal]**.<br>Esta opción solo está disponible si la instancia de Experience Manager Assets tiene **[!UICONTROL Brand Portal]** ya está configurado. |
   | Publicar en Dynamic Media | Publica los recursos seleccionados inmediatamente en Dynamic Media.<br>Se debe sincronizar un recurso con Dynamic Media. Si es necesario, asegúrese de que **[!UICONTROL Modo de sincronización]** en las propiedades de una carpeta ya está establecido en **[!UICONTROL Sincronizar todo en este subárbol de carpetas con Dynamic Media]**. |

1. Seleccionar **[!UICONTROL OK]**, luego seleccione **[!UICONTROL Cerrar]**.

## Publicar o cancelar la publicación selectiva de recursos mediante resultados de búsqueda {#selective-publish-unpublish-search-results}

Los resultados de la búsqueda pueden mostrar recursos de carpetas de recursos que tienen diferentes configuraciones de publicación de Dynamic Media. Si selecciona varios recursos en los resultados de búsqueda y cada recurso tiene diferentes configuraciones del modo de publicación de Dynamic Media, puede almacenar en déclencheur **[!UICONTROL Administrar publicación]** en la barra de herramientas, seleccione publicar o cancelar la publicación.

Consulte también [Buscar recursos en Experience Manager](/help/assets/search-assets.md).

**Para publicar o cancelar la publicación de recursos de forma selectiva mediante los resultados de búsqueda:**

1. En Experience Manager, en la esquina superior izquierda de la página, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global. En la parte izquierda de la página, seleccione el icono Navegación (justo encima del icono Herramientas ) y, a continuación, seleccione **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. En la barra de herramientas, cerca de la esquina superior derecha de la página, seleccione el icono Buscar (lupa).
1. En el **[!UICONTROL Escriba para buscar]** campo de texto, introduzca una palabra clave y pulse **[!UICONTROL Entrar]**.
1. Cerca de la esquina superior derecha de la página, seleccione la opción **[!UICONTROL Vista de lista]** icono.
1. Cerca de la esquina superior izquierda de la página, seleccione la opción **[!UICONTROL Filtros]** icono.

   ![Vista de lista y filtros en los resultados de búsqueda](/help/assets/assets-dm/select-publish-search-result.png)

1. En el panel izquierdo, expanda **[!UICONTROL Estado]** y, a continuación, expanda **[!UICONTROL Dynamic Media]** predicado de búsqueda.
1. Utilice el **[!UICONTROL Publicado]** y **[!UICONTROL Sin publicar]** Marque las casillas para restringir aún más los resultados de búsqueda en función del estado publicado de los recursos de Dynamic Media.
De forma opcional, puede utilizar estas casillas de verificación con **[!UICONTROL Publish]** predicado de búsqueda para restringir los resultados de búsqueda de **[!UICONTROL Publicado]** y **[!UICONTROL Sin publicar]** recursos del Experience Manager.
1. Realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee publicar o cancelar la publicación.
   * Cerca de la esquina superior derecha de la **[!UICONTROL Resultados de búsqueda]** página, seleccione **[!UICONTROL Seleccionar todo]**.
1. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Seleccione el icono de puntos suspensivos en la barra de herramientas para poder abrir **[!UICONTROL Administrar publicación]**.
1. En el **[!UICONTROL Administrar publicación: opciones]** , seleccione la acción que desee.

   | Acción seleccionada | Configuración de publicación de recursos en Dynamic Media | Los recursos son |
   | --- | --- | --- |
   | Publicación | Inmediatamente o tras la activación | Publicado en Experience Manager y Dynamic Media. |
   | Publicación | Publicación selectiva | Publicado solo en el Experience Manager. |
   | Cancelar publicación | Inmediatamente o tras la activación | Publicación cancelada de Experience Manager y Dynamic Media. |
   | Cancelar publicación | Publicación selectiva | Solo se ha cancelado la publicación del Experience Manager. |
   | Publicar en Dynamic Media | Inmediatamente o tras la activación | No se ha publicado en el Experience Manager, en Dynamic Media o en ambos. |
   | Publicar en Dynamic Media | Publicación selectiva | Publicado solo en Dynamic Media. |
   | Cancelar la publicación de Dynamic Media | Inmediatamente o tras la activación | No se ha cancelado la publicación del Experience Manager, de Dynamic Media o de ambos. |
   | Cancelar la publicación de Dynamic Media | Publicación selectiva | Solo se ha cancelado la publicación de Dynamic Media. |

1. En **[!UICONTROL Programación]**, establezca el tiempo de desactivación.

   | Programación seleccionada | ¿Qué sucede? |
   | --- | --- |
   | Ahora | La acción seleccionada se realiza inmediatamente. |
   | Más tarde | La acción seleccionada se ejecuta en la fecha y la hora seleccionadas. |

1. En la esquina superior derecha de la **[!UICONTROL Administrar publicación: opciones]** página, seleccione **[!UICONTROL Siguiente]**.
1. (Opcional) En el **[!UICONTROL Administrar publicación - Ámbito]** , revise la **[!UICONTROL Destino de publicación]** en la tabla para los recursos seleccionados.

   | Configuración de publicación de recursos en Dynamic Media | Acción seleccionada | Destino de publicación |
   | --- | --- | --- |
   | Inmediata o <br>Tras la activación | Publicación | EXPERIENCE MANAGER y DYNAMIC MEDIA |
   | Inmediata o <br>Tras la activación | Publicar en Dynamic Media | Ninguno |
   | Publicación selectiva | Publicación | Experience Manager |
   | Publicación selectiva | Publicar en Dynamic Media | Dynamic Media |
   | Inmediata o <br>Tras la activación | Cancelar publicación | EXPERIENCE MANAGER y DYNAMIC MEDIA |
   | Inmediata o <br>Tras la activación | Cancelar la publicación de Dynamic Media | Ninguno |
   | Publicación selectiva | Cancelar publicación | Experience Manager |
   | Publicación selectiva | Cancelar la publicación de Dynamic Media | Dynamic Media |

1. En el **[!UICONTROL Administrar publicación - Ámbito]** , realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee eliminar de la publicación o cancelación de la publicación.
   * En la esquina superior derecha de la **[!UICONTROL Administrar publicación - Ámbito]** página, seleccione **[!UICONTROL Publish]** o **[!UICONTROL Cancelar publicación]** para comenzar la acción.
1. Seleccionar **[!UICONTROL OK]**.

## Comprobar el estado de publicación de un recurso {#check-publish-status-of-asset}

Puede utilizar **[!UICONTROL Cronología]** con **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]**, o **[!UICONTROL Vista de lista]** en Experience Manager para comprobar rápidamente el estado de publicación de un recurso.

**Para comprobar el estado de publicación de un recurso:**

1. En Experience Manager, en la esquina superior izquierda de la página, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global. En la parte izquierda de la página, seleccione el icono Navegación (justo encima del icono Herramientas ) y, a continuación, seleccione **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Entrada **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]**, o **[!UICONTROL Vista de lista]** (la captura de pantalla siguiente muestra el **[!UICONTROL Vista de lista]**), abra una carpeta que contenga recursos que haya publicado o que haya cancelado la publicación.
1. Seleccione un recurso para que aparezca con una marca de verificación. Vea la captura de pantalla siguiente para ver un ejemplo.
1. Cerca de la esquina superior izquierda de la página, en el menú desplegable, seleccione **[!UICONTROL Cronología]**. El **[!UICONTROL Estado]** La región en el panel izquierdo muestra el estado de publicación del recurso seleccionado.
Cuando se usa **[!UICONTROL Vista de lista]**, una columna adicional para **[!UICONTROL Dynamic Media]** aparece el estado de publicación.
   * Una carpeta configurada para sincronizarse con Dynamic Media muestra el **[!UICONTROL Dynamic Media]** de forma predeterminada.
   * Una carpeta que es *no* configurado para sincronizarse con Dynamic Media no muestra la columna Dynamic Media.
     ![Vista de lista y cronología](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Solucionar problemas de publicación selectiva {#selective-publish-troubleshoot}

Un recurso que no está sincronizado con Dynamic Media pero que tiene una acción de publicación de Dynamic Media activada da como resultado el siguiente mensaje de error y solución:

![Error de publicación selectiva](/help/assets/assets-dm/selective-publish-error.png)
