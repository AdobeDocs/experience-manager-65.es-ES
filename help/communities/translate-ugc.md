---
title: Traducción del contenido generado por el usuario
seo-title: Traducción del contenido generado por el usuario
description: Funcionamiento de la función de traducción
seo-description: Funcionamiento de la función de traducción
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 1%

---


# Traducción del contenido generado por el usuario {#translating-user-generated-content}

La función de traducción para AEM Communities amplía el concepto de [traducción del contenido de la página](../../help/sites-administering/translation.md) al contenido generado por el usuario (UGC) publicado en sitios de la comunidad mediante los componentes [del marco de componentes sociales (SCF)](scf.md).

La traducción de UGC permite a los visitantes del sitio y a los miembros experimentar una comunidad global eliminando barreras lingüísticas.

Por ejemplo, suponga:

* Un miembro de Francia postea una receta en francés al foro comunitario de un sitio web de cocina multinacional.
* Otro miembro de Japón usa la característica de traducción para déclencheur de la traducción del francés al japonés.
* Luego de leer la receta en japonés, el miembro de Japón luego publica un comentario en japonés.
* El miembro de Francia usa la característica de traducción para traducir el comentario japonés al francés.
* Comunicación global.

## Información general {#overview}

En esta sección de la documentación se explica específicamente cómo funciona el servicio de traducción con UGC, asumiendo al mismo tiempo la comprensión de cómo conectar AEM a un [proveedor de servicios de traducción](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) e integrar ese servicio en un sitio web configurando un [marco de integración de traducción](../../help/sites-administering/tc-tic.md).

Cuando un proveedor de servicios de traducción está asociado con el sitio, cada copia de idioma del sitio mantiene sus propios subprocesos de UGC anunciados a través de componentes de SCF, como comentarios.

Cuando se configura un marco de integración de traducción además del proveedor de servicios de traducción, es posible que cada copia de idioma del sitio comparta un solo subproceso de UGC, proporcionando así comunicación global entre copias de idioma. En lugar de un subproceso de discusión segregado por idioma, la [tienda compartida global](#global-translation-of-ugc) configurada permite que todo el subproceso sea visible independientemente del idioma en que se esté viendo. Además, se pueden configurar varias configuraciones de integración de traducción que especifiquen diferentes tiendas compartidas globales para una agrupación lógica de participantes globales, como por regiones.

## El servicio de traducción predeterminado {#the-default-translation-service}

AEM Communities incluye una [licencia de prueba](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) para un [servicio de traducción predeterminado](../../help/sites-administering/tc-msconf.md) habilitado para varios idiomas.

Al [crear un sitio de la comunidad](sites-console.md), el servicio de traducción predeterminado se activa cuando `Allow Machine Translation` se comprueba desde el subpanel [TRANSLATION](sites-console.md#translation).

>[!CAUTION]
>
>El servicio de traducción predeterminado es solo para demostración.
>
>Para un sistema de producción, se requiere un servicio de traducción con licencia. Si no tiene licencia, el servicio de traducción predeterminado debe estar [desactivado](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## Traducción global de UGC {#global-translation-of-ugc}

Cuando un sitio web tiene varias [copias de idioma](../../help/sites-administering/tc-prep.md), el servicio de traducción predeterminado no reconoce que el UGC introducido en un sitio puede estar relacionado con el UGC introducido en otro, como cuando el UGC se genera esencialmente por el mismo componente (la copia de idioma de la página que contiene el componente).

Es similar a los grupos de personas que discuten un tema sin tener en cuenta los comentarios hechos en grupos distintos a los suyos, en comparación con todos en un grupo grande que participa en una conversación.

Si se desea una &quot;conversación de grupo único&quot;, es posible habilitar la traducción global a través de un sitio web con varias copias de idioma, de modo que todo el subproceso sea visible independientemente de qué copia de idioma se esté viendo.

Por ejemplo, si se estableció un foro en el sitio de base, se crearon copias de idiomas y se habilitó la traducción global, entonces un tema publicado en el foro en un solo idioma aparecería en todos los ejemplares de idiomas. Lo mismo ocurriría con las respuestas, independientemente del idioma del que se haya escrito la respuesta. El resultado sería que el tema y todo su subproceso de respuestas serían visibles independientemente del idioma desde el que se vea el tema.

>[!CAUTION]
>
>Ya no es visible ningún UGC que existiera antes de la traducción global.
>
>Aunque el UGC sigue en el [almacén común](working-with-srp.md), se encuentra en la ubicación UGC específica del idioma, mientras que el nuevo contenido, agregado después de configurar la traducción global, se recupera de la ubicación de tienda compartida global.
>
>No hay ninguna herramienta de migración para mover o combinar contenido específico de un idioma en la tienda compartida global.

### Configuración de integración de traducción {#translation-integration-configuration}

Para crear una nueva integración de traducción, que integra un conector del servicio de traducción con el sitio web de la instancia de autor:

* Iniciar sesión como administrador
* Desde el [menú principal](http://localhost:4502/)
* Seleccionar **[!UICONTROL Herramientas]**
* Seleccione **[!UICONTROL Operaciones]**
* Seleccione **[!UICONTROL Cloud]**
* Seleccione **[!UICONTROL Cloud Services]**
* Desplácese hacia abajo hasta **[!UICONTROL Translation Integration]**

   ![traducción-integración](assets/translation-integration.png)

* Seleccione **[!UICONTROL Mostrar configuraciones]**

   ![show-configuration](assets/translation-integration1.png)

* Seleccione el icono `[+]` junto a **[!UICONTROL Configuraciones disponibles]** para crear una nueva configuración

#### Crear cuadro de diálogo de configuración {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL Configuración principal]**

   (Obligatorio) Normalmente se deja como predeterminado. El valor predeterminado es `/etc/cloudservices/translation`.

* **[!UICONTROL Título]**

   (Obligatorio) Introduzca un título de visualización de su elección. No hay ningún valor predeterminado.

* **[!UICONTROL Nombre]**

   (Opcional) Introduzca un nombre para la configuración. El valor predeterminado es un nombre de nodo basado en el título.

* Seleccione **[!UICONTROL Crear]**

#### Cuadro de diálogo Configuración de traducción {#translation-config-dialog}

![configuration-dialog](assets/translation-integration3.png)

Para obtener instrucciones detalladas, visite [Creación de una configuración de integración de traducción](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **** Actividad del sitio: puede dejarse como predeterminado.

* **** Cláusula comunitaria:
   * **[!UICONTROL Proveedor de]**
traducciónSeleccione el proveedor de traducción en la lista desplegable. El valor predeterminado es 
`microsoft`, el servicio de prueba.

   * ****
Categoría de contenidoSeleccione una categoría que describa el contenido que se está traduciendo. El valor predeterminado es 
`General.`

   * **[!UICONTROL Elegir una configuración regional...]**
(Opcional) Al seleccionar una configuración regional para almacenar UGC, las publicaciones de todas las copias de idiomas aparecerán en una conversación global. Por convención, elija la configuración regional para el [idioma base](sites-console.md#translation) del sitio web. Al seleccionar `No Common Store` se deshabilitará la traducción global. De forma predeterminada, la traducción global está desactivada.

* **** Ficha Recursos: puede dejarse como predeterminado.
* Seleccione **[!UICONTROL OK]**

#### Activación {#activation}

El nuevo servicio de nube de integración de traducción deberá activarse en el entorno de publicación. Cuando esté asociado con un sitio web, si aún no está activado, el flujo de trabajo de activación solicitará la publicación de esta configuración del servicio de nube cuando se publique la página con la que está asociado.

## Administración de la configuración de traducción {#managing-translation-settings}

>[!NOTE]
>
>**Idioma preferido**
>
>Con el fin de detectar si el anuncio está en un idioma distinto al idioma preferido, se debe establecer el idioma preferido del visitante del sitio.
>
>El idioma preferido es la preferencia de idioma establecida en el perfil de un usuario, cuando el visitante del sitio ha iniciado sesión y ha especificado una preferencia de idioma.
>
>Cuando el visitante del sitio es anónimo o no ha especificado ninguna preferencia de idioma en su perfil, el idioma preferido es el idioma base de la plantilla de página.

### Preferencia de usuario {#user-preference}

#### Perfil de usuario {#user-profile}

Todos los sitios de comunidades proporcionan un perfil de usuario que los miembros que han iniciado sesión pueden editar para identificarse con la comunidad y establecer sus preferencias.

Una de estas opciones es si se debe mostrar o no siempre el contenido de la comunidad en su idioma preferido. De forma predeterminada, la configuración no está definida y se establecerá de forma predeterminada en la configuración del sistema. El usuario puede cambiar la configuración a Activado o Desactivado, anulando así la configuración del sistema.

Cuando las páginas se traducen automáticamente al idioma preferido del usuario, la interfaz de usuario para mostrar el texto original y mejorar la traducción sigue estando disponible.

![user-profile](assets/translation-integration4.png)

### Configuración del sitio de la comunidad {#community-site-setting}

Cuando se crea un sitio de comunidad, la opción de traducción se puede activar y configurar. La configuración de traducción está en vigor para el contenido que los visitantes anónimos del sitio pueden ver, pero la configuración de perfil del usuario anula.
