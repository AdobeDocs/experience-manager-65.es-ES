---
title: Vista previa de recursos
description: Obtenga información sobre cómo previsualizar recursos en Dynamic Media.
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
feature: Administración de activos
role: User, Admin
exl-id: 84f0c406-4ab6-48c7-8223-61a8c3ade363
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 1%

---

# Vista previa de recursos mediante la interfaz de software {#previewing-assets}

Puede utilizar Vista previa para ver el aspecto que tiene un recurso digital que ha cargado cuando lo ve un cliente en su propio navegador web. El visor predeterminado integrado entre dispositivos asignado al recurso se utiliza para la vista previa.

Un visor es una colección de varias configuraciones o *ajustes preestablecidos*, como el tamaño de visualización, el comportamiento del zoom, los esquemas de colores, los bordes y las fuentes. Estos ajustes preestablecidos determinan la forma en que los usuarios ven los recursos de medios enriquecidos en sus pantallas de equipo y dispositivos móviles.

Además de utilizar la función de vista previa dedicada para vídeo, conjuntos de giros y conjuntos de imágenes, también puede obtener una vista previa de un recurso mediante los ajustes preestablecidos de visor que ha creado. O bien, utilice ajustes preestablecidos de imagen para previsualizar las representaciones de imágenes.

* [Aplicar ajustes preestablecidos de imagen](/help/assets/image-presets.md)
* [Aplicar ajustes preestablecidos de visor](/help/assets/viewer-presets.md)

>[!NOTE]
>
>Cuando se encuentra en una página web (Sitios) en Adobe Experience Manager, no puede obtener una vista previa de los recursos en modo **Editar**. Vaya al modo Vista previa haciendo clic en **[!UICONTROL Preview]** en la esquina superior derecha de la página.

Para habilitar o deshabilitar los ajustes preestablecidos de visualizador en la interfaz de usuario, consulte [Administrar ajustes preestablecidos de visualizador](/help/assets/managing-viewer-presets.md).

**Para previsualizar recursos mediante la interfaz de software:**

1. En **[!UICONTROL Adobe Experience Manager]**, en la página **[!UICONTROL Navegación]**, seleccione **[!UICONTROL Recursos]** y, a continuación, **[!UICONTROL Archivos]** para acceder a los recursos.
1. Cerca de la esquina superior derecha de la página, en la lista desplegable **[!UICONTROL View]**, seleccione **[!UICONTROL Vista de lista]**.
1. (Opcional) Utilice la columna **[!UICONTROL Type]** para ordenar los recursos por el tipo de vista previa.
1. En la columna **[!UICONTROL Title]** , haga clic en el nombre del título (no en la imagen en miniatura) del recurso cuya vista previa desea ver.
1. En función del tipo de recurso en el que haya hecho clic, realice una de las siguientes acciones:


   <table>
    <tbody>
      <tr>
      <td><strong>Tipo de recurso en el que ha hecho clic</strong><br /> </td>
      <td><strong>¿Es posible obtener una vista previa del recurso en una representación determinada?</strong></td>
      <td><strong>¿Se puede previsualizar el recurso en un visor?</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>Para previsualizar un recurso 3D en el visor Dimensional</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccione <strong>Visualizadores</strong> de la lista y, a continuación, seleccione el visualizador de dimensiones.</li>
      <li>Seleccione <strong>Reset</strong> si desea devolver la imagen al zoom original.</li>
      <li>Seleccione <strong>Pantalla completa</strong> para maximizar el visor en el dispositivo de visualización.</li>
      </ul>
      <p><strong>Navegación por la escena 3D</strong></p>
      <ul>
      <li><p><strong>Girar la cámara 3D</strong> : Girar la vista alrededor de la escena 3D y los objetos.</p> Mouse: Clic izquierdo + Arrastrar </p> Pantalla táctil: Pulse + Arrastrar</p></li>
      <li><p><strong>Panorre la cámara</strong> : desplace la vista hacia la izquierda, hacia la derecha, hacia arriba y hacia abajo.</p> Mouse: Haga clic con el botón derecho y arrastre </p> Pantalla táctil: Pulsar con dos dedos + Arrastrar</p></li>
      <li><p><strong>Zoom de la cámara</strong> : Aumente el zoom de la cámara para que pueda desplazarse dentro y fuera de las áreas de la escena 3D.</p> Mouse: Rueda de desplazamiento </p> Pantalla táctil: Pinza de dedo</p></li>
      <li><p><strong>Vuelva a introducir la cámara</strong> : ordene la vista alrededor de la escena 3D y los objetos.</p> Mouse: Hacer doble clic </p> Pantalla táctil: Pulsar dos veces</li></ul></td>
      </tr>
      <tr>
      <td><p>Imagen</p> </td>
      <td>Sí</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa del recurso en una representación concreta</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccione <strong>Representaciones </strong>de la lista y, a continuación, seleccione una representación concreta que desee previsualizar.</li>
      </ul> <p><strong>Para previsualizar recursos en un visor determinado</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccione <strong>Visualizadores</strong> de la lista y, a continuación, seleccione un visualizador que desee aplicar al recurso.</li>
      </ul> <p>Utilice los iconos <strong>+</strong> y <strong>-</strong> para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Seleccione <strong>Reset</strong> si desea devolver la imagen al zoom original.<br /> Si está en una pantalla táctil, toque dos veces la imagen para acercarla por pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado del zoom. Arrastre la imagen hasta la panorámica.</p> </td>
      </tr>
      <tr>
      <td>Multimedia</td>
      <td>Sí</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa del recurso en una representación concreta</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccione <strong>Representaciones </strong>de la lista y, a continuación, seleccione una representación concreta que desee previsualizar.</li>
      </ul> <p>Si se selecciona una representación de vídeo de mayor resolución para previsualizar, es posible que el vídeo aparezca truncado. Este problema se debe a que la vista previa de la representación muestra la resolución exacta que los clientes verán en el contexto del visor integrado que se utiliza para la vista previa.</p> <p>Al previsualizar un conjunto de vídeos adaptables en el nivel de recurso, las representaciones se agrupan en una experiencia de reproducción. Es decir, el vídeo adaptable tiene un tamaño adecuado para visualizarlo y reproducirlo con la mejor resolución en el contexto del dispositivo de visualización y la velocidad de conexión.<br /> </p> <p><strong>Para obtener una vista previa de un recurso en un visor concreto</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccione <strong>Visualizadores</strong> de la lista y, a continuación, seleccione un visualizador que desee aplicar al recurso.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Conjunto de imágenes</td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa de un recurso en un visor concreto</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccione <strong>Visualizadores</strong> de la lista y, a continuación, seleccione un visualizador que desee aplicar al recurso.</li>
      </ul> <p>Utilice los iconos <strong>+</strong> y <strong>-</strong> para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Seleccione <strong>Reset</strong> si desea devolver la imagen al zoom original.<br /> Si está en una pantalla táctil, toque dos veces la imagen para acercarla por pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado del zoom. Arrastre la imagen hasta la panorámica.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de giros</td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa de un recurso en un visor concreto</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccione <strong>Visualizadores</strong> de la lista y, a continuación, seleccione un visualizador que desee aplicar al recurso.</li>
      </ul> <p>Utilice los iconos <strong>+</strong> y <strong>-</strong> para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Seleccione <strong>Reset</strong> si desea devolver la imagen al zoom original.<br /> Si está en una pantalla táctil, toque dos veces la imagen para acercarla por pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado del zoom. Arrastre la imagen hasta la panorámica.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de medios mixtos</td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa de un recurso en un visor concreto</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccione <strong>Visualizadores</strong> de la lista y, a continuación, seleccione un visualizador que desee aplicar al recurso.</li>
      </ul> <p>Utilice los iconos <strong>+</strong> y <strong>-</strong> para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Seleccione <strong>Reset</strong> si desea devolver la imagen al zoom original.<br /> Si está en una pantalla táctil, toque dos veces la imagen para acercarla por pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado del zoom. Arrastre la imagen hasta la panorámica.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de carrusel</td>
      <td>No</td>
      <td>Sí</td>
      <td><strong>Para obtener una vista previa de un recurso en un visor concreto</strong>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccione un visor que desee aplicar al recurso.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>360 Video<br /> </td>
      <td>Sí</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa del recurso en una representación concreta</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, seleccione el icono para que aparezca la lista desplegable. Seleccione <strong>Representaciones</strong> y, a continuación, seleccione la representación que desee previsualizar.</li>
      </ul> <p><strong>Para previsualizar recursos en un visor determinado</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, seleccione el icono para que aparezca la lista desplegable. Seleccione <strong>Visualizadores</strong> y, a continuación, seleccione un visualizador que desee aplicar al recurso.</li>
      </ul> <p>Utilice los iconos <strong>+</strong> y <strong>-</strong> para aumentar o reducir el zoom de la imagen seleccionada, respectivamente. Seleccione <strong>Reset</strong> si desea devolver la imagen al zoom original.<br /> Si está en una pantalla táctil, toque dos veces la imagen para acercarla por pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado del zoom. Arrastre la imagen hasta la panorámica.</p> </td>
      </tr>
    </tbody>
    </table>

## Vista previa de recursos mediante un teclado {#keyboard-navigation-asset-preview}

1. En la interfaz de usuario de Assets, vaya a la carpeta que contenga el recurso cuya vista previa desee ver.

1. En la carpeta , pulse la tecla `<Tab>` o las teclas de flecha del teclado para seleccionar el recurso.

1. Pulse `<Enter>` para poder abrir el recurso seleccionado en el modo de vista previa.

1. Realice una de las acciones siguientes:

   * Para aumentar, presione `<Tab>` para mover el foco al icono de acercar (+) y, a continuación, presione `<Enter>` una o más veces para aumentar gradualmente.
   * Para alejar, presione `<Tab>` para mover el foco al icono de alejar (-) y, a continuación, presione `<Enter>` una o más veces para alejarlo gradualmente.
   * Para mover la vista de un recurso *ampliado* horizontal o verticalmente, presione las teclas de flecha correspondientes.
   * Pulse `<Shift>` + `<Tab>` para restablecer la vista y volver a centrar la atención en el recurso.
