---
title: Previsualización de recursos
description: Obtenga información sobre cómo previsualizar recursos en Dynamic Media.
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 84f0c406-4ab6-48c7-8223-61a8c3ade363
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 1%

---

# Vista previa de recursos mediante la interfaz de software {#previewing-assets}

Puede usar Vista previa para ver el aspecto de un recurso digital que ha cargado cuando un cliente lo ve en su propio explorador web. El visor incrustado y entre dispositivos predeterminado asignado al recurso se utiliza para la vista previa.

Un visor es una colección de varias configuraciones o *ajustes preestablecidos*, como el tamaño de visualización del visor, el comportamiento del zoom, las combinaciones de colores, los bordes y las fuentes. Estos ajustes preestablecidos determinan cómo ven los usuarios los recursos de medios enriquecidos en las pantallas de sus equipos y dispositivos móviles.

Además de utilizar la función de previsualización dedicada para vídeos, conjuntos de giros y conjuntos de imágenes, también puede obtener una vista previa de un recurso mediante los ajustes preestablecidos de visualizador que ha creado. O bien, utilice ajustes preestablecidos de imagen para previsualizar representaciones de imágenes.

* [Aplicar ajustes preestablecidos de imagen](/help/assets/image-presets.md)
* [Aplicar ajustes preestablecidos de visor](/help/assets/viewer-presets.md)

>[!NOTE]
>
>Cuando se encuentra en una página web (Sites) en Adobe Experience Manager, no puede obtener una vista previa de los recursos en **Editar** modo. Vaya al modo de vista previa haciendo clic en **[!UICONTROL Previsualizar]** en la esquina superior derecha de la página.

Para habilitar o deshabilitar los ajustes preestablecidos de visualizador en la interfaz de usuario, consulte [Administrar ajustes preestablecidos de visor](/help/assets/managing-viewer-presets.md).

**Para obtener una vista previa de los recursos mediante la interfaz de software:**

1. Desde **[!UICONTROL Adobe Experience Manager]**, en el **[!UICONTROL Navegación]** página, seleccione **[!UICONTROL Assets]**, entonces **[!UICONTROL Archivos]** para acceder a los recursos.
1. Cerca de la esquina superior derecha de la página, desde el **[!UICONTROL Ver]** , seleccione la opción **[!UICONTROL Vista de lista]**.
1. (Opcional) Utilice la variable **[!UICONTROL Tipo]** para ordenar los recursos por el tipo que desee previsualizar.
1. En el **[!UICONTROL Título]** , haga clic en el nombre del título (no en la imagen en miniatura) del recurso que desea previsualizar.
1. Según el tipo de recurso en el que hizo clic, realice una de las siguientes acciones:


   <table>
    <tbody>
      <tr>
      <td><strong>Tipo de recurso en el que ha hecho clic</strong><br /> </td>
      <td><strong>¿Es posible previsualizar el recurso en una representación concreta?</strong></td>
      <td><strong>¿Es posible previsualizar el recurso en un visor?</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa de un recurso 3D en el visor dimensional</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccionar <strong>Espectadores</strong> en la lista, seleccione el visualizador dimensional.</li>
      <li>Seleccionar <strong>Restablecer</strong> si desea que la imagen vuelva al zoom original.</li>
      <li>Seleccionar <strong>Pantalla completa</strong> para maximizar el visor en el dispositivo de visualización.</li>
      </ul>
      <p><strong>Navegación por la escena 3D</strong></p>
      <ul>
      <li><p><strong>Convierta su cámara 3D</strong> - Orbita tu vista alrededor de la escena 3D y los objetos.</p> Mouse: clic izquierdo + arrastrar </p> Pantalla táctil: presionar + arrastrar</p></li>
      <li><p><strong>Panorámica de la cámara</strong> - Mueva la vista a la izquierda, a la derecha, arriba o abajo.</p> Ratón: clic con el botón derecho + arrastrar </p> Pantalla táctil: pulsar dos dedos + arrastrar</p></li>
      <li><p><strong>Zoom de la cámara</strong> - Aplique el zoom de la cámara para poder moverse dentro y fuera de las áreas de la escena 3D.</p> Ratón: rueda de desplazamiento </p> Pantalla táctil: Pellizco de dedo</p></li>
      <li><p><strong>Vuelva a centrar su cámara</strong> - Orbita tu vista alrededor de la escena 3D y los objetos.</p> Ratón: doble clic </p> Pantalla táctil: pulsar dos veces</li></ul></td>
      </tr>
      <tr>
      <td><p>Imagen</p> </td>
      <td>Sí</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa del recurso en una representación concreta</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccionar <strong>Representaciones </strong>en la lista, seleccione una representación concreta que desee previsualizar.</li>
      </ul> <p><strong>Para obtener una vista previa del recurso en un visor concreto</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccionar <strong>Espectadores</strong> en la lista, seleccione el visor que desee aplicar al recurso.</li>
      </ul> <p>Utilice el <strong>+</strong> y <strong>-</strong> para aumentar o disminuir el zoom de la imagen seleccionada, respectivamente. Seleccionar <strong>Restablecer</strong> si desea que la imagen vuelva al zoom original.<br /> Si está en una pantalla táctil, toque dos veces la imagen para acercarla por pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado de zoom. Arrastre por la imagen para desplazarse.</p> </td>
      </tr>
      <tr>
      <td>Multimedia</td>
      <td>Sí</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa del recurso en una representación concreta</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccionar <strong>Representaciones </strong>en la lista, seleccione una representación concreta que desee previsualizar.</li>
      </ul> <p>Si selecciona una representación de vídeo de mayor resolución para previsualizarla, es posible que el vídeo aparezca truncado. Este problema se debe a que la vista previa de la representación muestra la resolución exacta que los clientes van a ver todos los en el contexto del visor incrustado que se utiliza para la vista previa.</p> <p>Cuando previsualiza un conjunto de vídeos adaptables en el nivel de recurso, las representaciones se agrupan en una experiencia de reproducción. Es decir, el vídeo adaptable tiene el tamaño adecuado para su visualización y reproducción con la mejor resolución en el contexto del dispositivo de visualización y la velocidad de conexión.<br /> </p> <p><strong>Para obtener una vista previa de un recurso en un visor concreto</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccionar <strong>Espectadores</strong> en la lista, seleccione el visor que desee aplicar al recurso.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Conjunto de imágenes</td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa de un recurso en un visor concreto</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccionar <strong>Espectadores</strong> en la lista, seleccione el visor que desee aplicar al recurso.</li>
      </ul> <p>Utilice el <strong>+</strong> y <strong>-</strong> iconos para aumentar o disminuir el zoom de la imagen seleccionada, respectivamente. Seleccionar <strong>Restablecer</strong> si desea que la imagen vuelva al zoom original.<br /> Si está en una pantalla táctil, toque dos veces la imagen para acercarla por pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado de zoom. Arrastre por la imagen para desplazarse.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de giros</td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa de un recurso en un visor concreto</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccionar <strong>Espectadores</strong> en la lista, seleccione el visor que desee aplicar al recurso.</li>
      </ul> <p>Utilice el <strong>+</strong> y <strong>-</strong> para aumentar o disminuir el zoom de la imagen seleccionada, respectivamente. Seleccionar <strong>Restablecer</strong> si desea que la imagen vuelva al zoom original.<br /> Si está en una pantalla táctil, toque dos veces la imagen para acercarla por pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado de zoom. Arrastre por la imagen para desplazarse.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de medios mixtos</td>
      <td>No</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa de un recurso en un visor concreto</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccionar <strong>Espectadores</strong> en la lista, seleccione el visor que desee aplicar al recurso.</li>
      </ul> <p>Utilice el <strong>+</strong> y <strong>-</strong> para aumentar o disminuir el zoom de la imagen seleccionada, respectivamente. Seleccionar <strong>Restablecer</strong> si desea que la imagen vuelva al zoom original.<br /> Si está en una pantalla táctil, toque dos veces la imagen para acercarla por pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado de zoom. Arrastre por la imagen para desplazarse.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de carrusel</td>
      <td>No</td>
      <td>Sí</td>
      <td><strong>Para obtener una vista previa de un recurso en un visor concreto</strong>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, haga clic en el icono para que aparezca la lista desplegable. Seleccione el visor que desee aplicar al recurso.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Vídeo 360<br /> </td>
      <td>Sí</td>
      <td>Sí</td>
      <td><p><strong>Para obtener una vista previa del recurso en una representación concreta</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, seleccione el icono para que aparezca la lista desplegable. Seleccionar <strong>Representaciones</strong>, luego seleccione la representación que desee previsualizar.</li>
      </ul> <p><strong>Para obtener una vista previa del recurso en un visor concreto</strong></p>
      <ul>
      <li>Cerca de la esquina superior izquierda de la página, seleccione el icono para que aparezca la lista desplegable. Seleccionar <strong>Espectadores</strong>, a continuación, seleccione un visor que desee aplicar al recurso.</li>
      </ul> <p>Utilice el <strong>+</strong> y <strong>-</strong> para aumentar o disminuir el zoom de la imagen seleccionada, respectivamente. Seleccionar <strong>Restablecer</strong> si desea que la imagen vuelva al zoom original.<br /> Si está en una pantalla táctil, toque dos veces la imagen para acercarla por pasos. Cuando alcance el zoom máximo, vuelva a tocar dos veces la imagen para restablecer el estado de zoom. Arrastre por la imagen para desplazarse.</p> </td>
      </tr>
    </tbody>
    </table>

## Vista previa de recursos con un teclado {#keyboard-navigation-asset-preview}

1. En la interfaz de usuario de Assets, vaya a una carpeta que contenga un recurso que desee previsualizar.

1. En la carpeta, pulse el botón `<Tab>` teclas de dirección o de flecha del teclado para seleccionar el recurso.

1. Prensa `<Enter>` para poder abrir el recurso seleccionado en el modo de vista previa.

1. Realice una de las siguientes acciones:

   * Para acercar, pulse `<Tab>` para desplazar el foco al icono de ampliar (+), pulse `<Enter>` una o más veces para aumentar gradualmente.
   * Para alejar, pulse `<Tab>` para desplazar el enfoque al icono de alejar (-), pulse `<Enter>` una o más veces para alejar gradualmente.
   * Para mover la vista de un *ampliado* recurso horizontal o verticalmente, presione las teclas de flecha correspondientes.
   * Prensa `<Shift>` + `<Tab>` para poder restablecer la vista y volver a colocar el enfoque en el recurso.
