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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Traducción del contenido generado por el usuario {#translating-user-generated-content}

La función de traducción para comunidades AEM amplía el concepto de [traducir el contenido](../../help/sites-administering/translation.md) de la página al contenido generado por el usuario (UGC) publicado en sitios de la comunidad mediante componentes [de marco de componentes](scf.md)sociales (SCF).

La traducción de UGC permite a los visitantes y miembros del sitio experimentar una comunidad global eliminando barreras lingüísticas.

Como ejemplo, supongamos que

* Un miembro de Francia publica una receta en francés al foro comunitario de un sitio web multinacional de cocina
* Otro miembro de Japón usa la función de traducción para activar la traducción de la receta del francés al japonés
* Después de leer la receta en japonés, el miembro de Japón luego publica un comentario en japonés.
* El miembro de Francia usa la función de traducción para traducir el comentario japonés al francés
* ¡Comunicación global!

## Información general {#overview}

En esta sección de la documentación se explica específicamente cómo funciona el servicio de traducción con UGC, al tiempo que se asume la comprensión de cómo conectar AEM a un proveedor [de servicios de](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) traducción e integrar dicho servicio en un sitio web mediante la configuración de un marco [de integración de](../../help/sites-administering/tc-tic.md)traducción.

Cuando un proveedor de servicios de traducción está asociado con el sitio, cada copia de idioma del sitio mantiene sus propios subprocesos de UGC publicados a través de componentes de SCF, como comentarios.

Cuando se configura un marco de integración de traducción además del proveedor de servicios de traducción, es posible que cada copia de idioma del sitio comparta un solo subproceso de UGC, proporcionando así una comunicación global entre las copias de idiomas. En lugar de un subproceso de discusión segregado por idioma, la tienda [compartida](#global-translation-of-ugc) global configurada permite que todo el subproceso sea visible independientemente de qué copia de idioma se esté viendo. Además, se pueden configurar varias configuraciones de integración de traducción especificando diferentes almacenes globales compartidos para una agrupación lógica de participantes globales, como por regiones.

## El servicio de traducción predeterminado {#the-default-translation-service}

AEM Communities incluye una licencia [de](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) prueba para un servicio [de traducción](../../help/sites-administering/tc-msconf.md) predeterminado habilitado para varios idiomas.

Al [crear un sitio](sites-console.md)de comunidad, el servicio de traducción predeterminado se activa cuando `Allow Machine Translation` se comprueba desde el subpanel [TRANSLACIÓN](sites-console.md#translation) .

>[!CAUTION]
>
>El servicio de traducción predeterminado es solo para demostración.
>
>Para un sistema de producción, se requiere un servicio de traducción con licencia. Si no tiene licencia, el servicio de traducción predeterminado debe [desactivarse](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## Traducción global de UGC {#global-translation-of-ugc}

Cuando un sitio web tiene varias copias [de](../../help/sites-administering/tc-prep.md)idioma, el servicio de traducción predeterminado no reconoce que el UGC introducido en un sitio puede estar relacionado con el UGC introducido en otro, como cuando el UGC se genera esencialmente por el mismo componente (la copia de idioma de la página que contiene el componente).

Es similar a los grupos de personas que discuten un tema que no tiene conocimiento de los comentarios hechos en grupos distintos de los suyos, en comparación con todos los que participan en una conversación en un grupo grande.

Si se desea una &quot;conversación de un grupo&quot;, es posible habilitar la traducción global en un sitio web con varias copias de idioma, de modo que todo el subproceso sea visible independientemente de qué copia de idioma se esté viendo.

Por ejemplo, si se estableció un foro en el sitio de base, se crearon copias de idiomas y se habilitó la traducción global, entonces un tema publicado en el foro en una copia en un idioma aparecería en todos los ejemplares de idioma. Lo mismo puede decirse de todas las respuestas, independientemente del idioma en que se haya escrito la respuesta. El resultado sería que el tema y todo su hilo de respuestas serían visibles independientemente del idioma desde el que se vea la copia del tema.

>[!CAUTION]
>
>Ya no es visible ningún UGC que existiera antes de la traducción global.
>
>Aunque el UGC sigue en la tienda [](working-with-srp.md)común, se encuentra en la ubicación UGC específica del idioma, mientras que el nuevo contenido, agregado después de configurar la traducción global, se recupera desde la ubicación de la tienda compartida global.
>
>No hay ninguna herramienta de migración para mover o combinar contenido específico de idioma en la tienda compartida global.

### Configuración de integración de traducción {#translation-integration-configuration}

Para crear una nueva integración de traducción, que integra un conector de servicio de traducción con el sitio web en la instancia de creación:

* Iniciar sesión como administrador
* Desde el menú [principal](http://localhost:4502/)
* Seleccionar **[!UICONTROL herramientas]**
* Seleccionar **[!UICONTROL operaciones]**
* Seleccionar **[!UICONTROL nube]**
* Seleccionar servicios **[!UICONTROL de nube]**
* Desplácese hacia abajo hasta la integración **[!UICONTROL de traducción]**

![chlimage_1-65](assets/chlimage_1-65.png)

* Seleccione **[!UICONTROL Mostrar configuraciones]**

![chlimage_1-66](assets/chlimage_1-66.png)

* Seleccione `[+]` el icono junto a Configuraciones **** disponibles para crear una nueva configuración

#### Cuadro de diálogo Crear configuración {#create-configuration-dialog}

![chlimage_1-67](assets/chlimage_1-67.png)

* **[!UICONTROL Configuración]** principal (obligatoria) Normalmente se deja como predeterminado. El valor predeterminado es `/etc/cloudservices/translation`.

* **[!UICONTROL Título]**(obligatorio) Introduzca un título para mostrar de su elección. No hay ningún valor predeterminado.

* **[!UICONTROL Nombre]**(opcional) Introduzca un nombre para la configuración. El valor predeterminado es un nombre de nodo basado en el Título.

* Seleccione **[!UICONTROL Crear]**

#### Cuadro de diálogo Configuración de traducción {#translation-config-dialog}

![chlimage_1-68](assets/chlimage_1-68.png)

Para obtener instrucciones detalladas, visite [Creación de una configuración de integración de traducción](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **[!UICONTROL Ficha Sitios]** : puede salir como predeterminado
* **[!UICONTROL Ficha Comunidades]** :
   * **[!UICONTROL Proveedor]** de traducción Seleccione el proveedor de traducción en la lista desplegable. El valor predeterminado es `microsoft`, el servicio de prueba.

   * **[!UICONTROL Categoría]** de contenido Seleccione una categoría que describa el contenido que se va a traducir. El valor predeterminado es `General.`

   * **** Elegir una configuración regional...(Opcional) Al seleccionar una configuración regional para almacenar UGC, las publicaciones de todas las copias de idioma aparecerán en una conversación global. Por convención, elija la configuración regional para el idioma [](sites-console.md#translation) base del sitio web. Si elige `No Common Store` se deshabilitará la traducción global. De forma predeterminada, la traducción global está deshabilitada.

* **[!UICONTROL Ficha Recursos]** : puede salir como predeterminado
* Seleccione **[!UICONTROL Aceptar]**

#### Activación {#activation}

El nuevo servicio en la nube de integración de traducción deberá activarse en el entorno de publicación. Cuando se asocia a un sitio web, si aún no se ha activado, el flujo de trabajo de activación solicitará que se publique esta configuración del servicio en la nube cuando se publique la página con la que está asociado.

## Administración de la configuración de traducción {#managing-translation-settings}

>[!NOTE]
>
>**Idioma preferido**
>
>Para detectar si la publicación está en un idioma distinto al idioma preferido, se debe establecer el idioma preferido del visitante del sitio.
>
>El idioma preferido es la preferencia de idioma establecida en el perfil de un usuario, cuando el visitante del sitio ha iniciado sesión y ha especificado una preferencia de idioma.
>
>Cuando el visitante del sitio es anónimo o no ha especificado una preferencia de idioma en su perfil, el idioma preferido es el idioma base de la plantilla de página.

### Preferencia del usuario {#user-preference}

#### Perfil de usuario {#user-profile}

Todos los sitios de comunidades proporcionan un perfil de usuario que los miembros que iniciaron sesión pueden editar para identificarse con la comunidad y establecer sus preferencias.

Una de estas opciones es si se debe o no mostrar siempre el contenido de la comunidad en su idioma preferido. De forma predeterminada, la configuración no está establecida y se utilizará de forma predeterminada la configuración del sistema. El usuario puede cambiar la configuración a Activado o Desactivado, anulando así la configuración del sistema.

Cuando las páginas se traducen automáticamente al idioma preferido del usuario, la interfaz de usuario para mostrar el texto original y mejorar la traducción permanece disponible.

![chlimage_1-69](assets/chlimage_1-69.png)

### Configuración del sitio de la comunidad {#community-site-setting}

Cuando se crea un sitio de comunidad, la opción de traducción se puede habilitar y configurar. La configuración de traducción está en vigor para el contenido que pueden ver los visitantes anónimos del sitio, pero se anula por la configuración de perfil del usuario.
