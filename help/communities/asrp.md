---
title: ASRP - Proveedor de recursos de Almacenamiento de Adobe
seo-title: ASRP - Proveedor de recursos de Almacenamiento de Adobe
description: Configure AEM Communities para utilizar una base de datos relacional como su almacén común
seo-description: Configure AEM Communities para utilizar una base de datos relacional como su almacén común
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
translation-type: tm+mt
source-git-commit: 3202866bd38779a9784e44ab470152df61c585f5
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---


# ASRP - Proveedor de recursos de Almacenamiento de Adobe {#asrp-adobe-storage-resource-provider}

## Acerca de ASRP {#about-asrp}

Cuando AEM Communities está configurado para utilizar ASRP como su almacén común, el contenido generado por el usuario (UGC) es accesible desde todas las instancias de creación y publicación sin necesidad de sincronización ni replicación.

Consulte también [Características de las opciones de SRP](/help/communities/working-with-srp.md#characteristics-of-srp-options) y [Topologías recomendadas](/help/communities/topologies.md).

## Requisitos {#requirements}

Se requiere una licencia adicional para el uso de ASRP.

Para configurar el sitio de AEM Communities para que utilice ASRP para UGC, póngase en contacto con su representante de cuentas para:

* Dirección URL del centro de datos (dirección del extremo ASRP)
* Clave de consumidor
* Clave secreta
* ID del grupo de informes

Las claves de consumidor y clave secreta se comparten en todos los grupos de informes de una compañía. Hay un grupo de informes por inquilino.

## Configuración {#configuration}

### Seleccione ASRP {#select-asrp}

La [consola de configuración de Almacenamiento](/help/communities/srp-config.md) permite seleccionar la configuración de almacenamiento predeterminada, que identifica la implementación de SRP que se va a utilizar.

**En la instancia de AEM Author:**

* Desde la navegación global, vaya a **[!UICONTROL Herramientas > Comunidades > Configuración de Almacenamiento]** y seleccione **[!UICONTROL Proveedor de recursos de Almacenamiento de Adobe (ASRP)]**.

![asrp-default](assets/asrp-default.png)

La siguiente información proviene del proceso de aprovisionamiento:

* **Dirección URL** del centro de datos: Despliegue para seleccionar el centro de datos de producción identificado por el representante de cuentas.
* **Grupo** de informes predeterminado: Escriba el nombre del grupo de informes predeterminado.
* **clave del cliente**: Introduzca la clave del cliente.
* **Secreto**: Escribe el secreto.
* Seleccione **Enviar**.

Prepare las instancias de publicación:

* [Replicar la clave criptográfica](#replicate-the-crypto-key)
* [Replicar la configuración](#publishing-the-configuration)

Después de enviar la configuración, pruebe la conexión:

* Seleccione **Probar configuración**.

   Para cada instancia de creación y publicación, pruebe la conexión al centro de datos desde la consola de configuración de Almacenamiento.

* Asegúrese de que las direcciones URL del sitio para los datos de perfil sean enrutables desde el Centro de datos [externalizando vínculos](#externalize-links).

### Replicar la clave de cifrado {#replicate-the-crypto-key}

La Clave del cliente y la clave secreta están cifradas. Para que las claves se cifren o descifren correctamente, la clave de cifrado de granito principal debe ser la misma en todas las instancias AEM.

Siga las instrucciones en [Replicar la clave de cifrado](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Externalizar vínculos {#externalize-links}

Para los vínculos de imagen de perfil y perfil correctos, asegúrese de [Configurar correctamente el Externalizador de vínculos](/help/sites-developing/externalizer.md).

Asegúrese de establecer los dominios como direcciones URL que se pueden enrutar desde la dirección URL del centro de datos (extremo ASRP).

### Sincronización de tiempo {#time-synchronization}

Para que la autenticación con el extremo ASRP tenga éxito, los equipos que ejecutan el AEM Communities alojado deben sincronizarse a la hora, como con el [Protocolo de tiempo de red (NTP)](https://www.ntp.org/).

### Publicación de la configuración {#publishing-the-configuration}

ASRP debe identificarse como el almacén común en todas las instancias de creación y publicación.

Para que la configuración idéntica esté disponible en el entorno de publicación:

En la instancia de AEM Author:

* Vaya del menú principal a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Replicación]**
* Seleccione **Activar árbol**
* **Ruta** de inicio: buscar  `/conf/global/settings/communities/srpc/`
* Anule la selección de **Solo modificado**
* Seleccione **Activar**

## Actualización desde AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Si habilita ASRP en un sitio de comunidad publicado, cualquier UGC ya almacenado en [JCR](/help/communities/jsrp.md) ya no estará visible, ya que no hay sincronización de datos entre el almacenamiento local y el almacenamiento en la nube.

**`AEM Communities Extension`** previamente se introdujo en AEM comunidades sociales 6.0 como servicio de nube. A partir de AEM comunidades 6.1, no es necesaria ninguna configuración de nube, simplemente seleccione ASRP en la [consola de configuración de almacenamiento](/help/communities/srp-config.md).

Debido a la nueva estructura de almacenamientos, es necesario seguir las [instrucciones de actualización](/help/communities/upgrade.md#adobe-cloud-storage) al actualizar de comunidades sociales a comunidades.

## Administración de datos de usuario {#managing-user-data}

Para obtener información acerca de *usuarios*, *perfiles de usuario* y *grupos de usuarios*, que a menudo se introducen en el entorno de publicación, visite

* [Sincronización de usuarios](/help/communities/sync.md)
* [Administración de usuarios y grupos de usuarios](/help/communities/users.md)

## Solución de problemas {#troubleshooting}

### UGC desaparece tras la actualización {#ugc-disappears-after-upgrade}

Si realiza la actualización desde un sitio de comunidad social AEM 6.0 existente, asegúrese de seguir las [instrucciones de actualización](/help/communities/upgrade.md#adobe-cloud-storage), de lo contrario, parece que UGC se pierde.

### Errores de autenticación {#authentication-errors}

Si recibe errores de autenticación con la dirección URL del centro de datos y el AEM error.log contiene mensajes sobre marcas de hora antiguas, compruebe que se está realizando la sincronización de hora.

Utilice una herramienta como [Network Time Protocol (NTP)](https://www.ntp.org/) para sincronizar con el tiempo todos los servidores de publicación y creación de AEM.

### El nuevo contenido no aparece en las búsquedas {#new-content-does-not-appear-in-searches}

La infraestructura de almacenamiento de nube de Adobe utiliza *consistencia eventual* para lograr sus objetivos de escalamiento y performance. Por este motivo, el nuevo contenido no está disponible al instante y tarda varios segundos en aparecer en los resultados de búsqueda.

Mientras se supervisa el intervalo que afecta a la coherencia final, póngase en contacto con el representante de la cuenta si el contenido nuevo tarda más de unos segundos en aparecer en las búsquedas.

### UGC no visible en ASRP {#ugc-not-visible-in-asrp}

Asegúrese de que el ASRP se haya configurado para que sea el proveedor predeterminado mediante la comprobación de la configuración de la opción de almacenamiento. De forma predeterminada, el proveedor de recursos de almacenamiento es JSRP, no ASRP.

En todas las instancias de creación y publicación de AEM, vuelva a la consola de Configuración de Almacenamiento o compruebe el repositorio de AEM.

En JCR, si [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* No contiene un nodo [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp), significa que el proveedor de almacenamiento es JSRP.
* Si el nodo srpc existe y contiene el nodo [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration), las propiedades de configuración predeterminada definen ASRP como el proveedor predeterminado.

