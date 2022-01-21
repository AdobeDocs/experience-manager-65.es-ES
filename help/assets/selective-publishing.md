---
title: Trabajar con publicación selectiva en Dynamic Media
description: Puede elegir entre publicar o cancelar la publicación de recursos en Adobe Experience Manager o Dynamic Media en el nivel de carpeta, o desde ellos. Puede utilizar Administrar publicación o Publicación rápida en lugar de depender únicamente de la configuración de Dynamic Media cuya configuración sea global para todas las carpetas de la instancia de Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
source-git-commit: 664e22cc4c6acd74f285a4ec1a0dbd7d301240b7
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 4%

---

# Configurar la publicación selectiva en el nivel de carpeta en Dynamic Media {#selective-publish-configure-folder}

Puede elegir entre publicar o cancelar la publicación de recursos en Adobe Experience Manager o Dynamic Media en el nivel de carpeta, o desde ellos. Puede usar cualquiera de las opciones siguientes: **[!UICONTROL Administrar publicación]** o **[!UICONTROL Publicación rápida]** en lugar de depender únicamente de la variable **[!UICONTROL Configuración de Dynamic Media]** cuya configuración es global para todas las carpetas de la instancia de Dynamic Media.

Por ejemplo, con la publicación selectiva puede trabajar en recursos para productos que aún no están activos. En tal caso, un equipo de marketing puede acceder a las imágenes de recorte inteligente y a las representaciones dinámicas sincronizadas con Dynamic Media. Pueden crear materiales promocionales, sin necesidad de publicar esos recursos en Dynamic Media para su envío global.

>[!IMPORTANT]
>
>La publicación selectiva solo está disponible en el modo Dynamic Media - Scene7 .

>[!NOTE]
>
>*Copia* los recursos que se dirigen a las carpetas y que se extraen de ellas borran el estado de publicación de dichos recursos. Sin embargo, cuando *move* recursos a y desde carpetas cuya propiedad de carpeta está definida en **[!UICONTROL Publicación selectiva]**, se mantiene el estado de publicación de esos recursos.

Si más adelante decide cambiar la variable **[!UICONTROL Publicación selectiva]** en una carpeta, estos cambios solo afectan a los nuevos recursos que cargue en esa carpeta a partir de ese momento. El estado de publicación de los recursos existentes en la carpeta permanece tal cual hasta que los cambie manualmente de **[!UICONTROL Publicación rápida]** o **[!UICONTROL Administrar publicación]** para abrir el Navegador.

El nivel de carpeta **[!UICONTROL Modo de publicación de Dynamic Media]** siempre establece de forma predeterminada el valor que se encuentra en la variable **[!UICONTROL Publicar recursos]** en **[!UICONTROL Configuración de Dynamic Media]**. Sin embargo, los siguientes pasos en este tema muestran cómo cambiar manualmente este valor predeterminado en el nivel de carpeta (como se describe en los pasos siguientes) para anular la variable **[!UICONTROL Configuración de Dynamic Media]** valor.

Independientemente de si se basa en alguna de las siguientes opciones:

* **[!UICONTROL Publicar recursos]** valor establecido en **[!UICONTROL Configuración de Dynamic Media]**.
* **[!UICONTROL Modo de publicación de Dynamic Media]** definido en propiedades de nivel de carpeta.

Puede elegir **[!UICONTROL Inmediatamente]**, **[!UICONTROL Al activar]** o **[!UICONTROL Publicación selectiva]**. Por ejemplo, puede configurar la variable **[!UICONTROL Publicar recursos]** en su **[!UICONTROL Configuración de Dynamic Media]** a **[!UICONTROL Al activar]**, pero configure la variable **[!UICONTROL Publicación en Dynamic Media]** valor de modo en el nivel de carpeta a **[!UICONTROL Publicación selectiva]** y, a la inversa.

Después de configurar la publicación selectiva en una carpeta, puede realizar cualquiera de las siguientes acciones:

* [Publicar recursos de forma selectiva en Dynamic Media o Experience Manager mediante Administrar publicación](#selective-publish-manage-publication).
* [Cancelar la publicación de forma selectiva desde Dynamic Media o Experience Manager mediante Administrar publicación](#selective-unpublish-manage-publication).
* [Publicación de recursos en Dynamic Media o Experience Manager mediante Publicación rápida](#quick-publish-aem-dm).
* [Publicar o cancelar la publicación de recursos de forma selectiva mediante los resultados de búsqueda](#selective-publish-unpublish-search-results).

**Para configurar la publicación selectiva en el nivel de carpeta en Dynamic Media:**

1. En el Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo, seleccione el icono Navegación (justo encima del icono Herramientas ) y, a continuación, seleccione **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]**.
1. Realice una de las acciones siguientes:
   * Editar las propiedades de una carpeta existente: En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, desplácese a la carpeta cuyas propiedades desee editar. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.
   * Editar las propiedades de una nueva carpeta: En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Crear]** > **[!UICONTROL Carpeta]**. En el **[!UICONTROL Crear carpeta]** , introduzca un título (obligatorio) para la carpeta y, a continuación, seleccione **[!UICONTROL Crear]**. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.

1. En el **[!UICONTROL Modo de sincronización]** en la lista desplegable, seleccione una de las siguientes opciones:

   | Modo de sincronización | Descripción |
   | --- | --- |
   | **[!UICONTROL Heredado]** | No hay ningún valor de sincronización explícito en la carpeta; en su lugar, la carpeta hereda el valor de sincronización de una de sus carpetas antecesoras o el modo predeterminado establecido en su **[!UICONTROL Configuración de Dynamic Media]**. El estado detallado de **[!UICONTROL Heredado]** se muestra mediante una información del objeto. |
   | **[!UICONTROL Sincronizar todo en este subárbol de carpetas con Dynamic Media]** | Para que la publicación en Dynamic Media se realice correctamente, los recursos deben sincronizarse con Dynamic Media. Al seleccionar esta opción, se incluyen todos los recursos de este subárbol para sincronizarlos con Dynamic Media. La configuración específica de la carpeta anula la configuración predeterminada de la variable **[!UICONTROL Configuración de Dynamic Media]**. |
   | **[!UICONTROL Excluir todo en este subárbol de carpetas de la sincronización de Dynamic Media]** | Excluya todos los recursos de este subárbol de la sincronización con Dynamic Media. |

   ![Publicación selectiva a nivel de carpeta](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. En el **[!UICONTROL Modo de publicación de Dynamic Media]** en la lista desplegable, seleccione una opción . La variable **[!UICONTROL Modo de publicación de Dynamic Media]** siempre establece de forma predeterminada el valor que se establece en la variable **[!UICONTROL Configuración de Dynamic Media]**. Sin embargo, puede anular manualmente este valor predeterminado **[!UICONTROL Configuración de Dynamic Media]** empleando una de las siguientes opciones.

   >[!IMPORTANT]
   >
   >Independientemente de la opción del modo de publicación de Dynamic Media que seleccione, cualquier actualización que realice posteriormente en un recurso que esté *already* publicadas, estas actualizaciones se publican inmediatamente sin que el usuario tome ninguna otra medida.
   >
   >Si se actualiza un vídeo publicado, debe volver a publicarse para reflejar los cambios en la entrega.

   | Opción de modo Publicación de Dynamic Media | Descripción |
   | --- | --- |
   | **[!UICONTROL Inmediatamente]** | Cuando los recursos se cargan en esta carpeta, el sistema los incorpora en el Experience Manager y proporciona la URL o la Incrustar al instante. Esta opción solo está vinculada a la publicación en Experience Manager y no es necesario que el usuario intervenga para publicar recursos.<br>Esta opción es *not* disponible si ha seleccionado **[!UICONTROL Excluir todo en este subárbol de carpetas de la sincronización de Dynamic Media]** en **[!UICONTROL Modo de sincronización]** en el paso anterior. |
   | **[!UICONTROL Tras la activación]** | Cuando los recursos se cargan en esta carpeta, primero debe publicar explícitamente el recurso antes de proporcionar un vínculo URL/incrustado. Esta opción solo está vinculada a la publicación en Experience Manager.<br>Esta opción es *not* disponible si ha seleccionado **[!UICONTROL Excluir todo en este subárbol de carpetas de la sincronización de Dynamic Media]** en **[!UICONTROL Modo de sincronización]** en el paso anterior. |
   | **[!UICONTROL Publicación selectiva]** | Los recursos se publican a su elección, ya sea en el Experience Manager o en Dynamic Media para su entrega en el dominio público. Ambos métodos de publicación se excluyen mutuamente. Es decir, puede publicar recursos en DMS7 para que pueda utilizar funciones como Recorte inteligente o representaciones dinámicas. O puede publicar recursos exclusivamente en Experience Manager para obtener una vista previa segura; esos mismos activos son *not* publicado en DMS7 para su entrega en el dominio público. Esta opción no está disponible si ha seleccionado **[!UICONTROL Excluir todo en este subárbol de carpetas de la sincronización de Dynamic Media]** en **[!UICONTROL Modo de sincronización]** en el paso anterior. |

1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar y cerrar]** y, a continuación, seleccione **[!UICONTROL OK]** para volver a Experience Manager Assets.

## Publicar recursos de forma selectiva en Dynamic Media o Experience Manager mediante Administrar publicación{#selective-publish-manage-publication}

Antes de poder usar **[!UICONTROL Administrar publicación]** para publicar recursos de forma selectiva en Dynamic Media o Experience Manager, asegúrese de haber establecido una de las siguientes opciones:

* La variable **[!UICONTROL Publicar recursos]** en **[!UICONTROL Configuración de Dynamic Media]** a **[!UICONTROL Publicación selectiva]**
* Se ha configurado la publicación selectiva en el nivel de carpeta.

Consulte [Crear una configuración de Dynamic Media](#configuring-dynamic-media-cloud-services) o [Configurar la publicación selectiva en el nivel de carpeta en Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>La publicación selectiva solo está disponible en el modo Dynamic Media - Scene7 .

>[!NOTE]
>
>*Copia* los recursos que se dirigen a las carpetas y que se extraen de ellas borran el estado de publicación de dichos recursos. Sin embargo, cuando *move* recursos a y desde carpetas cuya propiedad de carpeta está definida en **[!UICONTROL Publicación selectiva]**, se mantiene el estado de publicación de esos recursos.

**Para publicar selectivamente recursos en Dynamic Media o Experience Manager mediante Administrar publicación:**

1. En el Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo, seleccione el icono Navegación (justo encima del icono Herramientas ) y, a continuación, seleccione **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]**.
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Vaya a una carpeta cuyos recursos desee publicar. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Uso **[!UICONTROL Vista de lista]** de este modo, puede comprobar con mayor facilidad el estado de publicación de una carpeta concreta.
   * Vaya a una carpeta cuyos recursos desee publicar. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Uso **[!UICONTROL Vista de lista]** de este modo, puede comprobar con mayor facilidad el estado de publicación de un recurso en particular.

      >[!NOTE]
      >
      >If **[!UICONTROL Administrar publicación]** no aparece en la barra de herramientas, seleccione el botón de puntos suspensivos y, a continuación, seleccione **[!UICONTROL Administrar publicación]** en el menú de la lista.

1. En el **[!UICONTROL Administrar publicación: opciones]** página, en **[!UICONTROL Acción]**, seleccione el tipo de activación que desee.

   | Acción | Descripción |
   | --- | --- |
   | **[!UICONTROL Publicación]** (al Experience Manager) | Seleccione esta opción para publicar recursos en el Experience Manager y así obtener una vista previa segura. |
   | **[!UICONTROL Publicar en Dynamic Media]** | Seleccione esta opción para publicar recursos en Dynamic Media para su entrega en el dominio público o para que pueda utilizar funciones como Recorte inteligente o representaciones dinámicas.<br>Esta opción solo está disponible si **[!UICONTROL Modo de publicación de Dynamic Media]** está configurado como **[!UICONTROL Publicación selectiva]** en las propiedades de la carpeta. |

1. En **[!UICONTROL Programación]**, establezca el tiempo de publicación.

   | Programa | Descripción |
   | --- | --- |
   | **[!UICONTROL Ahora]** | Seleccione para publicar los recursos inmediatamente. |
   | **[!UICONTROL Más tarde]** | Seleccione para publicar los recursos en una fecha y hora concretas. |

1. En la esquina superior derecha de la variable **[!UICONTROL Administrar publicación]** página, seleccione **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Administrar publicación: ámbito]** , realice una de las siguientes acciones:

   * Si es necesario, seleccione uno o varios recursos que desee eliminar de la publicación.
   * En la esquina superior derecha de la variable **[!UICONTROL Administrar publicación: ámbito]** página, seleccione **[!UICONTROL Publicación]** o **[!UICONTROL Publicar en Dynamic Media]**.
1. Select **[!UICONTROL OK]**.

### Cancelar la publicación de forma selectiva desde Dynamic Media o Experience Manager mediante Administrar publicación {#selective-unpublish-manage-publication}

1. En el Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo, seleccione el icono Navegación (justo encima del icono Herramientas ) y, a continuación, seleccione **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]**.
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Desplácese a la carpeta cuyos recursos desee cancelar la publicación. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Uso **[!UICONTROL Vista de lista]** de este modo, puede comprobar con mayor facilidad el estado de publicación de una carpeta concreta.
   * Desplácese a la carpeta cuyos recursos desee cancelar la publicación. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Uso **[!UICONTROL Vista de lista]** de este modo, puede comprobar con mayor facilidad el estado de publicación de un recurso en particular.

      >[!NOTE]
      >
      >If **[!UICONTROL Administrar publicación]** no aparece en la barra de herramientas, seleccione el botón de puntos suspensivos y, a continuación, seleccione **[!UICONTROL Administrar publicación]** en el menú de la lista.

1. En el **[!UICONTROL Administrar publicación: opciones]** página, en **[!UICONTROL Acción]**, seleccione el tipo de desactivación que desee.

   | Acción | Descripción |
   | --- | --- |
   | **[!UICONTROL Cancelar la publicación]** (del Experience Manager) | Seleccione esta opción si desea cancelar la publicación de los recursos del Experience Manager. |
   | **[!UICONTROL Cancelar la publicación de Dynamic Media]** | Seleccione esta opción si desea cancelar la publicación de recursos de Dynamic Media.<br>Esta opción solo está disponible si **[!UICONTROL Modo de publicación de Dynamic Media]** está configurado como **[!UICONTROL Publicación selectiva]** en las propiedades de la carpeta. |

1. En **[!UICONTROL Programación]**, establezca el tiempo de desactivación.

   | Programa | Descripción |
   | --- | --- |
   | **[!UICONTROL Ahora]** | Seleccione para cancelar la publicación de los recursos inmediatamente. |
   | **[!UICONTROL Más tarde]** | Seleccione para cancelar la publicación de los recursos en una fecha y hora concretas. |

1. En la esquina superior derecha de la variable **[!UICONTROL Administrar publicación]** página, seleccione **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Administrar publicación: ámbito]** , realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee eliminar de la cancelación de la publicación.
   * En la esquina superior derecha de la variable **[!UICONTROL Administrar publicación: ámbito]** página, seleccione **[!UICONTROL Cancelar la publicación]** o **[!UICONTROL Cancelar publicación desde Dynamic Media]**.
1. Select **[!UICONTROL OK]**.

## Publicación de recursos en Dynamic Media o Experience Manager mediante Publicación rápida {#quick-publish-aem-dm}

Puede usar **[!UICONTROL Publicación rápida]** para casos de activación de recursos simples. **[!UICONTROL Publicación rápida]** publica los recursos seleccionados inmediatamente sin más interacción del usuario. Debido a esta acción, cualquier referencia no publicada también se publica automáticamente.

>[!NOTE]
>
>Para usar **[!UICONTROL Publicación rápida]** para publicar recursos en Dynamic Media o Experience Manager, asegúrese de **[!UICONTROL Publicación selectiva]** está habilitado en su **[!UICONTROL Configuración de Dynamic Media]** o en las propiedades de la carpeta seleccionada.

**Para publicar recursos en Dynamic Media o Experience Manager mediante Publicación rápida:**

1. En el Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo de la página, seleccione el icono Navegación (justo encima del icono Herramientas ) y, a continuación, en el lado derecho de la página, seleccione **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]**.
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Vaya a una carpeta cuyos recursos desee publicar. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**. Uso **[!UICONTROL Vista de lista]** de este modo, puede comprobar con mayor facilidad el estado de publicación de una carpeta concreta.
   * Vaya a una carpeta cuyos recursos desee publicar. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**. Uso **[!UICONTROL Vista de lista]** de este modo, puede comprobar con mayor facilidad el estado de publicación de un recurso en particular.

      >[!NOTE]
      >
      >If **[!UICONTROL Publicación rápida]** no aparece en la barra de herramientas, seleccione el botón de puntos suspensivos y, a continuación, seleccione **[!UICONTROL Publicación rápida]** en el menú de la lista.

      ![Publicación rápida a nivel de carpeta en Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Seleccione una de las siguientes opciones en el **[!UICONTROL Publicación rápida]** lista de menús.

   | Opción Publicación rápida | Qué hace |
   | --- | --- | 
   | Publicar en el Experience Manager | Publica los recursos seleccionados inmediatamente en el Experience Manager. |
   | Publicar en Brand Portal | Publica los recursos seleccionados inmediatamente en **[!UICONTROL Brand Portal]**.<br>Esta opción solo está disponible si la instancia de Experience Manager Assets tiene **[!UICONTROL Brand Portal]** ya configurado. |
   | Publicar en Dynamic Media | Publica los recursos seleccionados inmediatamente en Dynamic Media.<br>Un recurso debe sincronizarse con Dynamic Media. Si es necesario, asegúrese de que **[!UICONTROL Modo de sincronización]** en las propiedades de una carpeta ya se ha definido como **[!UICONTROL Sincronizar todo en este subárbol de carpetas con Dynamic Media]**. |

1. Select **[!UICONTROL OK]** y, a continuación, seleccione **[!UICONTROL Cerrar]**.

## Publicar o cancelar la publicación de recursos de forma selectiva mediante los resultados de búsqueda {#selective-publish-unpublish-search-results}

Los resultados de búsqueda pueden mostrar recursos de todas las carpetas de recursos que tengan diferentes configuraciones de publicación de Dynamic Media. Si selecciona varios recursos de los resultados de búsqueda y cada recurso tiene diferentes configuraciones del modo de publicación de Dynamic Media, puede realizar la déclencheur **[!UICONTROL Administrar publicación]** en la barra de herramientas, para publicar o cancelar la publicación.

Consulte también [Buscar recursos en el Experience Manager](/help/assets/search-assets.md).

**Para publicar o cancelar la publicación de recursos de forma selectiva mediante los resultados de búsqueda:**

1. En el Experience Manager, en la esquina superior izquierda de la página, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo de la página, seleccione el icono Navegación (justo encima del icono Herramientas ) y, a continuación, seleccione **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]**.
1. En la barra de herramientas, cerca de la esquina superior derecha de la página, seleccione el icono de búsqueda (lupa).
1. En el **[!UICONTROL Tipo de búsqueda]** campo de texto, introduzca una palabra clave y, a continuación, pulse **[!UICONTROL Entrar]**.
1. Cerca de la esquina superior derecha de la página, seleccione la opción **[!UICONTROL Vista de lista]** icono.
1. Cerca de la esquina superior izquierda de la página, seleccione la opción **[!UICONTROL Filtros]** icono.

   ![Vista de lista y filtros en los resultados de búsqueda](/help/assets/assets-dm/select-publish-search-result.png)

1. En el panel izquierdo, expanda **[!UICONTROL Estado]** y, a continuación, expanda el **[!UICONTROL Dynamic Media]** predicado de búsqueda.
1. Utilice la variable **[!UICONTROL Publicado]** y **[!UICONTROL Sin publicar]** para restringir aún más los resultados de búsqueda según el estado publicado de los recursos de Dynamic Media.
Opcionalmente, puede utilizar estas casillas de verificación con la variable **[!UICONTROL Publicación]** predicado de búsqueda para refinar los resultados de búsqueda de **[!UICONTROL Publicado]** y **[!UICONTROL Sin publicar]** Recursos del Experience Manager.
1. Realice una de las acciones siguientes:
   * Seleccione uno o varios recursos que desee publicar o cancelar la publicación.
   * Cerca de la esquina superior derecha de la **[!UICONTROL Resultados de la búsqueda]** página, seleccione **[!UICONTROL Seleccionar todo]**.
1. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Seleccione el icono de puntos suspensivos en la barra de herramientas para que pueda abrir **[!UICONTROL Administrar publicación]**.
1. En el **[!UICONTROL Administrar publicación: opciones]** seleccione la acción que desee.

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

1. En **[!UICONTROL Programación]**, establezca el tiempo de desactivación.

   | Programación seleccionada | Qué sucede |
   | --- | --- |
   | Ahora | La acción seleccionada se realiza inmediatamente. |
   | Más tarde | La acción seleccionada se ejecuta en la fecha y hora concretas seleccionadas. |

1. En la esquina superior derecha de la variable **[!UICONTROL Administrar publicación: opciones]** página, seleccione **[!UICONTROL Siguiente]**.
1. (Opcional) En la **[!UICONTROL Administrar publicación: ámbito]** página, revise la **[!UICONTROL Publicar Target]** en la tabla de los recursos seleccionados.

   | Publicar recursos en la configuración de Dynamic Media | Acción seleccionada | Destino de publicación |
   | --- | --- | --- |
   | Inmediatamente o <br>Tras la activación | Publicación | Experience Manager y Dynamic Media |
   | Inmediatamente o <br>Tras la activación | Publicar en Dynamic Media | Ninguna |
   | Publicación selectiva | Publicación | Experience Manager |
   | Publicación selectiva | Publicar en Dynamic Media | Dynamic Media |
   | Inmediatamente o <br>Tras la activación | Cancelar publicación | Experience Manager y Dynamic Media |
   | Inmediatamente o <br>Tras la activación | Cancelar la publicación de Dynamic Media | Ninguna |
   | Publicación selectiva | Cancelar publicación | Experience Manager |
   | Publicación selectiva | Cancelar la publicación de Dynamic Media | Dynamic Media |

1. En el **[!UICONTROL Administrar publicación: ámbito]** , realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee eliminar de la publicación o de la cancelación de la publicación.
   * En la esquina superior derecha de la variable **[!UICONTROL Administrar publicación: ámbito]** página, seleccione **[!UICONTROL Publicación]** o **[!UICONTROL Cancelar la publicación]** para iniciar la acción.
1. Select **[!UICONTROL OK]**.

## Comprobar el estado de publicación de un recurso {#check-publish-status-of-asset}

Puede usar **[!UICONTROL Cronología]** con **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]** en Experience Manager para comprobar rápidamente el estado de publicación de un recurso.

**Para comprobar el estado de publicación de un recurso:**

1. En el Experience Manager, en la esquina superior izquierda de la página, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global. En el lado izquierdo de la página, seleccione el icono Navegación (justo encima del icono Herramientas ) y, a continuación, seleccione **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]**.
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]** (la captura de pantalla a continuación muestra la **[!UICONTROL Vista de lista]**), abra una carpeta que contenga recursos que haya publicado o cancelado la publicación.
1. Seleccione un recurso para que aparezca con una marca de verificación. Consulte la captura de pantalla siguiente, por ejemplo.
1. Cerca de la esquina superior izquierda de la página, en el menú desplegable, seleccione **[!UICONTROL Cronología]**. La variable **[!UICONTROL Estado]** en el panel izquierdo se muestra el estado de publicación del recurso seleccionado.
Cuando utilice **[!UICONTROL Vista de lista]**, una columna adicional para **[!UICONTROL Dynamic Media]** aparece el estado de publicación.
   * Una carpeta configurada para sincronizar con Dynamic Media muestra la **[!UICONTROL Dynamic Media]** de forma predeterminada.
   * Una carpeta que *not* configurado para sincronizar con Dynamic Media no muestra la columna Dynamic Media .
      ![Vista de lista y línea de tiempo](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Resolución de problemas de publicación selectiva {#selective-publish-troubleshoot}

Un recurso que no está sincronizado con Dynamic Media pero tiene una acción de publicación de Dynamic Media activada provoca el siguiente mensaje de error y solución:

![Error de publicación selectiva](/help/assets/assets-dm/selective-publish-error.png)
