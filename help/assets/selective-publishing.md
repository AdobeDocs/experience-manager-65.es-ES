---
title: Uso de Publicación selectiva en Dynamic Media
description: Información sobre cómo trabajar con Publicación selectiva en Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 29f91713f5760ab0b5a557b5c811ef2efee1cc61
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 4%

---


# Configuración de la publicación selectiva a nivel de carpeta en Dynamic Media {#selective-publish-configure-folder}

Puede optar por publicar o cancelar la publicación de recursos en o desde AEM o Dynamic Media a nivel de carpeta, utilizando **[!UICONTROL Administrar publicación]** o **[!UICONTROL Publicación rápida]** en lugar de depender únicamente de la **[!UICONTROL Configuración de Dynamic Media]** cuya configuración sea global para todas las carpetas de la instancia de Dynamic Media.

Por ejemplo, con la publicación selectiva puede trabajar en recursos para productos que aún no están activos. En ese caso, un equipo de marketing puede acceder a imágenes de recorte inteligente y representaciones dinámicas sincronizadas con Dynamic Media para que puedan crear materiales promocionales, sin necesidad de publicar estos recursos en Dynamic Media para envío global.

>[!IMPORTANT]
>
>Publicación selectiva solo está disponible en el modo Dynamic Media - Scene7.

>[!NOTE]
>
>*Al* copiar recursos a y desde carpetas, se borra el estado de publicación de dichos recursos. Sin embargo, cuando *mueve* recursos a y desde carpetas cuya propiedad de carpeta está establecida en **[!UICONTROL Publicación selectiva]**, se mantiene el estado de publicación de esos recursos.

Si posteriormente decide cambiar la configuración de **[!UICONTROL Publicación selectiva]** en una carpeta, esos cambios solo afectarán a los recursos nuevos que cargue en esa carpeta a partir de ese momento. El estado de publicación de los recursos existentes en la carpeta permanece tal cual hasta que los cambie manualmente desde **[!UICONTROL Publicación rápida]** o el cuadro de diálogo **[!UICONTROL Administrar publicación]**.

La opción de nivel de carpeta **[!UICONTROL modo de publicación de Dynamic Media]** siempre establece de forma predeterminada el valor que se encuentra en la configuración **[!UICONTROL Publicar recursos]** de la configuración de **[!UICONTROL Dynamic Media.]** Sin embargo, los pasos siguientes en este tema muestran cómo cambiar manualmente este valor predeterminado en el nivel de carpeta (como se describe en los pasos siguientes) para anular el valor de  **[!UICONTROL Dynamic Media]** Configuration.

Independientemente de si confía en el valor **[!UICONTROL Publicar recursos]** establecido en **[!UICONTROL Configuración de Dynamic Media]** o en el valor **[!UICONTROL modo Publicar de Dynamic Media]** establecido en las propiedades de nivel de carpeta, aún puede elegir **[!UICONTROL Inmediatamente]**, **[!UICONTROL Tras la Activación]** o **[!UICONTROL Publicación selectiva.]** Por ejemplo, puede establecer el valor  **[!UICONTROL Publicar]** recursos en la configuración de  **[!UICONTROL Dynamic Media en]** Al realizar la Activación **[!UICONTROL , pero establecer el valor del modo]** Dynamic Media  **[!UICONTROL Publishmode en el nivel de carpeta en Publicación]**   **** selectiva, viceversa, etc.

Después de configurar la publicación selectiva en una carpeta, puede realizar cualquiera de las siguientes acciones:

* [Publique recursos en Dynamic Media o AEM de forma selectiva mediante Administrar publicación.](#selective-publish-manage-publication)
* [Cancele selectivamente la publicación de recursos de Dynamic Media o AEM mediante Administrar publicación.](#selective-unpublish-manage-publication)
* [Publicación de recursos en Dynamic Media o AEM mediante Publicación rápida.](#quick-publish-aem-dm)
* [Publique o cancele la publicación de recursos de forma selectiva mediante los resultados de la búsqueda.](#selective-publish-unpublish-search-results)

**Para configurar la publicación selectiva en el nivel de carpeta en Dynamic Media**

1. En AEM, toque el logotipo AEM para acceder a la consola de navegación global. En el lado izquierdo, toque el icono de navegación (justo encima del icono Herramientas) y luego toque **[!UICONTROL Recursos > Archivos.]**
1. Realice una de las acciones siguientes:
   * Edite las propiedades de una carpeta existente: en **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de Lista]**, navegue a la carpeta cuyas propiedades desee editar. Seleccione la carpeta y, en la barra de herramientas, toque **[!UICONTROL Propiedades.]**
   * Edite las propiedades de una nueva carpeta: en **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de Lista]**, cerca de la esquina superior derecha de la página, toque **[!UICONTROL Crear > Carpeta.]** En el cuadro de diálogo  **[!UICONTROL Crear]** carpeta, escriba un título (obligatorio) para la carpeta y, a continuación, toque  **[!UICONTROL Crear.]** Seleccione la carpeta y, en la barra de herramientas, toque  **[!UICONTROL Propiedades.]**

1. En la lista desplegable **[!UICONTROL Modo de sincronización]**, seleccione una de las siguientes opciones:

   | Modo de sincronización | Descripción |
   | --- | --- |
   | **[!UICONTROL Heredado]** | No hay ningún valor de sincronización explícita en la carpeta; en su lugar, la carpeta hereda el valor de sincronización de una de sus carpetas antecesoras o del modo predeterminado establecido en la configuración de **[!UICONTROL Dynamic Media.]** El estado detallado de  **** Heredado se muestra mediante una información del objeto. |
   | **[!UICONTROL Sincronizar todo en este diagrama secundario de carpetas con dynamicmedia]** | Para que la publicación en Dynamic Media se realice correctamente, los recursos deben sincronizarse con Dynamic Media. Si selecciona esta opción, se incluirán todos los recursos de este subárbol para sincronizarlos con Dynamic Media. La configuración específica de la carpeta anula la configuración predeterminada en la **[!UICONTROL Configuración de Dynamic Media.]** |
   | **[!UICONTROL Excluir todo el subárbol de carpetas de la sincronización DynamicMedia]** | Excluya todos los recursos de este subárbol de la sincronización con Dynamic Media. |

   ![Publicación selectiva a nivel de carpeta](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. En la lista desplegable **[!UICONTROL Modo de publicación de Dynamic Media]**, seleccione una opción. Tenga en cuenta que la opción **[!UICONTROL Modo de publicación de Dynamic Media]** siempre establece de forma predeterminada el valor que se establece en la configuración de **[!UICONTROL Dynamic Media.]** Sin embargo, puede anular manualmente este valor predeterminado de  **[!UICONTROL Dynamic Media]** Configurationmediante una de las siguientes opciones.

   >[!IMPORTANT]
   >
   >Tenga en cuenta que, independientemente de la opción de modo de publicación de Dynamic Media que seleccione, cualquier actualización que realice posteriormente en un recurso que *ya esté* publicado, dichas actualizaciones se publicarán inmediatamente sin ninguna otra acción por parte del usuario.

   | Opción de modo Dynamic Media Publish | Descripción |
   | --- | --- |
   | **[!UICONTROL Inmediatamente]** | Cuando se cargan recursos en esta carpeta, el sistema los transfiere a AEM y proporciona la URL o incrustación de forma instantánea. Esta opción solo está vinculada a la publicación AEM y no es necesaria la intervención del usuario para publicar recursos.<br>Esta opción  ** no está disponible si seleccionó  **[!UICONTROL Excluir todo en este subárbol de carpetas del]** modelo de sincronización  **** de Dynamic Media en el paso anterior. |
   | **[!UICONTROL Tras la activación]** | Cuando los recursos se cargan en esta carpeta, primero debe publicar explícitamente el recurso antes de proporcionar un vínculo URL/Incrustar. Esta opción solo está vinculada a AEM publicación.<br>Esta opción  ** no está disponible si seleccionó  **[!UICONTROL Excluir todo en este subárbol de carpetas del]** modelo de sincronización  **** de Dynamic Media en el paso anterior. |
   | **[!UICONTROL Publicación selectiva]** | Los recursos se publican a su elección, ya sea en AEM o en Dynamic Media, para su envío en el dominio público. Ambos métodos de publicación se excluyen mutuamente.  Es decir, puede publicar recursos en DMS7 para que pueda utilizar funciones como Recorte inteligente o representaciones dinámicas. O bien, puede publicar recursos exclusivamente en AEM para obtener una vista previa segura; los mismos recursos se *no* publican en DMS7 para envío en el dominio público. Esta opción no está disponible si seleccionó **[!UICONTROL Excluir todo en este subárbol de carpetas de la sincronización Dynamic Media]** en **[!UICONTROL modo de sincronización]** en el paso anterior. |

1. En la esquina superior derecha de la página, toque **[!UICONTROL Guardar y cerrar]** y luego toque **[!UICONTROL Aceptar]** para volver a AEM Assets.

## Publicación selectiva de recursos en Dynamic Media o AEM mediante Administrar publicación{#selective-publish-manage-publication}

Antes de utilizar **[!UICONTROL Administrar publicación]** para publicar recursos en Dynamic Media o para AEM de forma selectiva, asegúrese de establecer la opción **[!UICONTROL Publicar recursos]** en **[!UICONTROL Configuración de Dynamic Media]** en **[!UICONTROL Publicación selectiva]** o publicación selectiva configurada en el nivel de carpeta.

Consulte [Creación de una configuración de Dynamic Media](#configuring-dynamic-media-cloud-services) o [Configuración de la publicación selectiva a nivel de carpeta en Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>Publicación selectiva solo está disponible en el modo Dynamic Media - Scene7.

>[!NOTE]
>
>*Al* copiar recursos a y desde carpetas, se borra el estado de publicación de dichos recursos. Sin embargo, cuando *mueve* recursos a y desde carpetas cuya propiedad de carpeta está establecida en **[!UICONTROL Publicación selectiva]**, se mantiene el estado de publicación de esos recursos.

**Para publicar recursos en Dynamic Media de forma selectiva o AEM mediante Administrar publicación**

1. En AEM, toque el logotipo AEM para acceder a la consola de navegación global. En el lado izquierdo, toque el icono de navegación (justo encima del icono Herramientas) y luego toque **[!UICONTROL Recursos > Archivos.]**
1. En **[!UICONTROL Vista de tarjetas]**, **[!UICONTROL Vista de columnas]** o **[!UICONTROL Vista de Listas]**, realice una de las siguientes acciones:
   * Desplácese a una carpeta cuyos recursos desee publicar. Seleccione la carpeta y, en la barra de herramientas, toque **[!UICONTROL Administrar publicación.]**  Puede que le resulte útil utilizar  **[!UICONTROL Lista]** Viewer para poder comprobar con más facilidad el estado de publicación de una carpeta en particular.
   * Desplácese a una carpeta cuyos recursos desee publicar. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, toque **[!UICONTROL Administrar publicación.]** Puede que le resulte útil utilizar la  **[!UICONTROL vista de]** Lista para poder comprobar más fácilmente el estado de publicación de un recurso en particular.

      >[!NOTE]
      >
      >Si **[!UICONTROL Administrar publicación]** no se ve en la barra de herramientas, toque el botón de puntos suspensivos en su lugar y, a continuación, seleccione **[!UICONTROL Administrar publicación]** en el menú lista.

1. En la página **[!UICONTROL Administrar publicación - Opciones]**, en **[!UICONTROL Acción]**, seleccione el tipo de activación que desee.

   | Acción | Descripción |
   | --- | --- |
   | **[!UICONTROL Publicar]** (en AEM) | Seleccione esta opción para publicar recursos en AEM para una previsualización segura. |
   | **[!UICONTROL Publicar en Dynamic Media]** | Seleccione esta opción para publicar recursos en Dynamic Media para su envío en el dominio público o para que pueda utilizar funciones como Recorte inteligente o representaciones dinámicas.<br>Esta opción solo está disponible si  **[!UICONTROL Dynamic Media Publish]** modele está configurado como Publicación  **[!UICONTROL selectiva en las propiedades de la]** carpeta. |

1. En **[!UICONTROL Programar]**, establezca la temporización de la publicación.

   | Programa | Descripción |
   | --- | --- |
   | **[!UICONTROL Ahora]** | Seleccione esta opción para publicar los recursos inmediatamente. |
   | **[!UICONTROL Más tarde]** | Seleccione esta opción para publicar los recursos en una fecha y hora concretas. |

1. En la esquina superior derecha de la página **[!UICONTROL Administrar publicación]**, toque **[!UICONTROL Siguiente.]**
1. En la página **[!UICONTROL Administrar publicación - Ámbito]**, realice una de las siguientes acciones:

   * Si es necesario, seleccione uno o varios recursos que desee eliminar de la publicación.
   * En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Ámbito]**, toque **[!UICONTROL Publicar]** o **[!UICONTROL Publicar en Dynamic Media.]**
1. Toque **[!UICONTROL Aceptar.]**

### Cancelación selectiva de la publicación de recursos de Dynamic Media o AEM mediante Administrar publicación {#selective-unpublish-manage-publication}

1. En AEM, toque el logotipo AEM para acceder a la consola de navegación global. En el lado izquierdo, toque el icono de navegación (justo encima del icono Herramientas) y luego toque **[!UICONTROL Recursos > Archivos.]**
1. En **[!UICONTROL Vista de tarjetas]**, **[!UICONTROL Vista de columnas]** o **[!UICONTROL Vista de Listas]**, realice una de las siguientes acciones:
   * Desplácese a una carpeta cuyos recursos desee cancelar la publicación. Seleccione la carpeta y, en la barra de herramientas, toque **[!UICONTROL Administrar publicación.]**  Puede que le resulte útil utilizar  **[!UICONTROL Lista]** Viewer para poder comprobar con más facilidad el estado de publicación de una carpeta en particular.
   * Desplácese a una carpeta cuyos recursos desee cancelar la publicación. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, toque **[!UICONTROL Administrar publicación.]** Puede que le resulte útil utilizar la  **[!UICONTROL vista de]** Lista para poder comprobar más fácilmente el estado de publicación de un recurso en particular.

      >[!NOTE]
      >
      >Si **[!UICONTROL Administrar publicación]** no se ve en la barra de herramientas, toque el botón de puntos suspensivos en su lugar y, a continuación, seleccione **[!UICONTROL Administrar publicación]** en el menú lista.

1. En la página **[!UICONTROL Administrar publicación - Opciones]**, en **[!UICONTROL Acción]**, seleccione el tipo de activación que desee.

   | Acción | Descripción |
   | --- | --- |
   | **[!UICONTROL Cancelar la publicación]**  (desde AEM) | Seleccione esta opción para cancelar la publicación de recursos de AEM. |
   | **[!UICONTROL Cancelar la publicación de Dynamic Media]** | Seleccione esta opción para cancelar la publicación de recursos de Dynamic Media.<br>Esta opción solo está disponible si  **[!UICONTROL Dynamic Media Publish]** modele está configurado como Publicación  **[!UICONTROL selectiva en las propiedades de la]** carpeta. |

1. En **[!UICONTROL Programar]**, establezca la temporización de la desactivación.

   | Programa | Descripción |
   | --- | --- |
   | **[!UICONTROL Ahora]** | Seleccione esta opción para cancelar la publicación de los recursos inmediatamente. |
   | **[!UICONTROL Más tarde]** | Seleccione esta opción para cancelar la publicación de los recursos en una fecha y hora concretas. |

1. En la esquina superior derecha de la página **[!UICONTROL Administrar publicación]**, toque **[!UICONTROL Siguiente.]**
1. En la página **[!UICONTROL Administrar publicación - Ámbito]**, realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee eliminar de la cancelación de la publicación.
   * En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Ámbito]**, toque **[!UICONTROL Cancelar publicación]** o **[!UICONTROL Cancelar publicación de Dynamic Media.]**
1. Toque **[!UICONTROL Aceptar.]**

## Publicación de recursos en Dynamic Media o AEM mediante Publicación rápida {#quick-publish-aem-dm}

Puede utilizar **[!UICONTROL Publicación rápida]** para casos de activación de recursos sencillos. **[!UICONTROL Publicación rápida]** publica los recursos seleccionados inmediatamente sin ninguna interacción del usuario. Debido a esto, las referencias no publicadas también se publican automáticamente.

>[!NOTE]
>
>Para utilizar **[!UICONTROL Publicación rápida]** para publicar recursos en Dynamic Media o AEM, asegúrese de que **[!UICONTROL Publicación selectiva]** esté activada en la **[!UICONTROL Configuración de Dynamic Media]** o en las propiedades de carpeta de la carpeta seleccionada.

**Para publicar recursos en Dynamic Media o AEM mediante Publicación rápida**

1. En AEM, toque el logotipo AEM para acceder a la consola de navegación global. En la parte izquierda de la página, toque el icono de navegación (justo encima del icono Herramientas) y, a continuación, en la parte derecha de la página, toque **[!UICONTROL Recursos > Archivos.]**
1. En **[!UICONTROL Vista de tarjetas]**, **[!UICONTROL Vista de columnas]** o **[!UICONTROL Vista de Listas]**, realice una de las siguientes acciones:
   * Desplácese a una carpeta cuyos recursos desee publicar. Seleccione la carpeta y, en la barra de herramientas, toque **[!UICONTROL Publicación rápida.]**  Puede que le resulte útil utilizar  **[!UICONTROL Lista]** Viewer para poder comprobar con más facilidad el estado de publicación de una carpeta en particular.
   * Desplácese a una carpeta cuyos recursos desee publicar. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, toque **[!UICONTROL Publicación rápida.]** Puede que le resulte útil utilizar la  **[!UICONTROL vista de]** Lista para poder comprobar más fácilmente el estado de publicación de un recurso en particular.

      >[!NOTE]
      >
      >Si **[!UICONTROL Publicación rápida]** no se ve en la barra de herramientas, toque el botón de puntos suspensivos en su lugar y, a continuación, seleccione **[!UICONTROL Publicación rápida]** en el menú lista.

      ![Publicación rápida a nivel de carpeta en Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Seleccione una de las siguientes opciones en la lista de menú **[!UICONTROL Publicación rápida]**.

   | Opción Publicación rápida | Qué hace |
   | --- | --- | 
   | Publicar en AEM | Publica los recursos seleccionados inmediatamente para AEM. |
   | Publicar en Brand Portal | Publica los recursos seleccionados inmediatamente en **[!UICONTROL Brand Portal.]**<br>Esta opción solo está disponible si la instancia de AEM Assets ya tiene**[!UICONTROL  Brand ]**Portal configurado. |
   | Publicar en Dynamic Media | Publica los recursos seleccionados inmediatamente en Dynamic Media.<br>Un recurso ya debe sincronizarse con Dynamic Media. Si es necesario, asegúrese de que **[!UICONTROL el modo de sincronización]** en las propiedades de una carpeta ya está establecido en **[!UICONTROL Sincronice todo en este subárbol de carpetas con dynamicmedia.]** |

1. Toque **[!UICONTROL Aceptar]** y luego toque **[!UICONTROL Cerrar.]**

## Publicar o cancelar selectivamente la publicación de recursos mediante los resultados de búsqueda {#selective-publish-unpublish-search-results}

Los resultados de la búsqueda pueden mostrar recursos de distintas carpetas de recursos con diferentes configuraciones de publicación de Dynamic Media. Si ha seleccionado uno o varios recursos de los resultados de búsqueda y los recursos tienen diferentes ajustes del modo de publicación de Dynamic Media, puede déclencheur **[!UICONTROL Administrar publicación]** desde la barra de herramientas para publicar o cancelar la publicación.

Consulte también [Buscar recursos en AEM.](/help/assets/search-assets.md)

**Para publicar o cancelar la publicación de recursos de forma selectiva mediante los resultados de búsqueda**

1. En AEM, en la esquina superior izquierda de la página, toque el logotipo AEM para acceder a la consola de navegación global. En el lado izquierdo de la página, toque el icono de navegación (justo encima del icono Herramientas) y luego toque **[!UICONTROL Recursos > Archivos.]**
1. En la barra de herramientas, cerca de la esquina superior derecha de la página, toque el icono de búsqueda (lupa).
1. En el campo de texto **[!UICONTROL Escriba para buscar]**, escriba una palabra clave y luego presione **[!UICONTROL Intro.]**
1. Cerca de la esquina superior derecha de la página, toque el icono **[!UICONTROL Vista de Lista]**.
1. Cerca de la esquina superior izquierda de la página, toque el icono **[!UICONTROL Filtros]**.

   ![Vista de lista y Filtros en los resultados de búsqueda](/help/assets/assets-dm/select-publish-search-result.png)

1. En el panel izquierdo, expanda **[!UICONTROL Estado]** y luego expanda el predicado de búsqueda **[!UICONTROL Dynamic Media]**.
1. Utilice las casillas de verificación **[!UICONTROL Publicado]** y **[!UICONTROL No publicado]** para restringir aún más los resultados de búsqueda según el estado publicado de los recursos de Dynamic Media.
Opcionalmente, puede utilizar estas casillas de verificación junto con el predicado de búsqueda **[!UICONTROL Publicar]** para refinar los resultados de búsqueda de **[!UICONTROL Recursos de AEM publicados]** y **[!UICONTROL No publicados]**.
1. Realice una de las acciones siguientes:
   * Seleccione uno o varios recursos que desee publicar o cancelar la publicación.
   * Cerca de la esquina superior derecha de la página **[!UICONTROL Resultados de búsqueda]**, toque **[!UICONTROL Seleccionar todo.]**
1. En la barra de herramientas, toque **[!UICONTROL Administrar publicación.]** Es posible que deba tocar el icono de puntos suspensivos de la barra de herramientas para ver  **[!UICONTROL Administrar publicación.]**
1. En la página **[!UICONTROL Administrar publicación - Opciones]**, seleccione la acción que desee.

   | Acción seleccionada | Configuración de Publicar recursos en Configuración de Dynamic Media | Los recursos son |
   | --- | --- | --- |
   | Publicación | Inmediatamente o tras la Activación | Publicado en AEM y Dynamic Media. |
   | Publicación | Publicación selectiva | Solo se publica en AEM. |
   | Cancelar publicación | Inmediatamente o tras la Activación | No publicado desde AEM y Dynamic Media. |
   | Cancelar publicación | Publicación selectiva | No publicado solo desde AEM. |
   | Publicar en Dynamic Media | Inmediatamente o tras la Activación | No publicado en AEM, Dynamic Media o ambos. |
   | Publicar en Dynamic Media | Publicación selectiva | Solo se publica en Dynamic Media. |
   | Cancelar la publicación de Dynamic Media | Inmediatamente o tras la Activación | Sin cancelar la publicación desde AEM, Dynamic Media o ambos. |
   | Cancelar la publicación de Dynamic Media | Publicación selectiva | Solo se deja de publicar en Dynamic Media. |

1. En **[!UICONTROL Programar]**, establezca la temporización de la desactivación.

   | Programación seleccionada | Qué sucede |
   | --- | --- |
   | Ahora | La acción seleccionada se realiza inmediatamente. |
   | Más tarde | La acción seleccionada se ejecuta en la fecha y hora específicas seleccionadas. |

1. En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Opciones]**, toque **[!UICONTROL Siguiente.]**
1. (Opcional) En la página **[!UICONTROL Administrar publicación - Ámbito]**, revise la columna **[!UICONTROL Publicar Destinatario]** de la tabla de los recursos seleccionados.

   | Configuración de Publicar recursos en Configuración de Dynamic Media | Acción seleccionada | Destino de publicación |
   | --- | --- | --- |
   | Inmediatamente o <br>Tras la Activación | Publicación | AEM y Dynamic Media |
   | Inmediatamente o <br>Tras la Activación | Publicar en Dynamic Media | Ninguna |
   | Publicación selectiva | Publicación | AEM |
   | Publicación selectiva | Publicar en Dynamic Media | Dynamic Media |
   | Inmediatamente o <br>Tras la Activación | Cancelar publicación | AEM y Dynamic Media |
   | Inmediatamente o <br>Tras la Activación | Cancelar la publicación de Dynamic Media | Ninguna |
   | Publicación selectiva | Cancelar publicación | AEM |
   | Publicación selectiva | Cancelar la publicación de Dynamic Media | Dynamic Media |

1. En la página **[!UICONTROL Administrar publicación - Ámbito]**, realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee eliminar de la publicación o cancelación de publicación.
   * En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Ámbito]**, toque **[!UICONTROL Publicar]** o **[!UICONTROL Cancelar publicación]** para iniciar la acción.
1. Toque **[!UICONTROL Aceptar.]**

## Comprobación del estado de publicación de un recurso {#check-publish-status-of-asset}

Puede utilizar **[!UICONTROL Línea de tiempo]** con **[!UICONTROL vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de Lista]** en AEM para comprobar rápidamente el estado de publicación de un recurso.

**Para comprobar el estado de publicación de un recurso**

1. En AEM, en la esquina superior izquierda de la página, toque el logotipo AEM para acceder a la consola de navegación global. En el lado izquierdo de la página, toque el icono de navegación (justo encima del icono Herramientas) y luego toque **[!UICONTROL Recursos > Archivos.]**
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de Lista]** (la captura de pantalla siguiente muestra la **[!UICONTROL Vista de Lista]**), abra una carpeta que contenga los recursos que haya publicado o no.
1. Seleccione un recurso para que aparezca con una marca de verificación. Consulte la captura de pantalla siguiente, por ejemplo.
1. Cerca de la esquina superior izquierda de la página, en el menú desplegable, seleccione **[!UICONTROL Línea de tiempo.]** La  **** región Estado del panel izquierdo muestra el estado de publicación del recurso seleccionado.
Cuando se utiliza **[!UICONTROL Vista de Lista]**, aparece una columna adicional para **[!UICONTROL estado de publicación de Dynamic Media]**.
   * Una carpeta configurada para sincronizar con Dynamic Media mostrará la columna **[!UICONTROL Dynamic Media]** de manera predeterminada.
   * Una carpeta *no* configurada para sincronizar con Dynamic Media no mostrará la columna Dynamic Media.
      ![Vista de lista y cronología](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Solución de problemas de publicación selectiva {#selective-publish-troubleshoot}

Un recurso que no se sincroniza con Dynamic Media pero que tiene una acción de publicación de Dynamic Media activada en él genera el siguiente mensaje de error y solución:

![Error de publicación selectiva](/help/assets/assets-dm/selective-publish-error.png)

