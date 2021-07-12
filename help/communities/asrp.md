---
title: 'ASRP: proveedor de recursos de almacenamiento de Adobe'
seo-title: 'ASRP: proveedor de recursos de almacenamiento de Adobe'
description: Configuración de AEM Communities para utilizar una base de datos relacional como su tienda común
seo-description: Configuración de AEM Communities para utilizar una base de datos relacional como su tienda común
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
role: Admin
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# ASRP: proveedor de recursos de almacenamiento de Adobe {#asrp-adobe-storage-resource-provider}

## Acerca de ASRP {#about-asrp}

Cuando AEM Communities está configurado para utilizar ASRP como su almacén común, el contenido generado por el usuario (UGC) es accesible desde todas las instancias de autor y publicación sin necesidad de sincronización ni replicación.

Consulte también [Características de las opciones de SRP](/help/communities/working-with-srp.md#characteristics-of-srp-options) y [Topologías recomendadas](/help/communities/topologies.md).

## Requisitos {#requirements}

Se requiere una licencia adicional para el uso de ASRP.

Para configurar el sitio de AEM Communities para que use ASRP para UGC, póngase en contacto con el representante de cuentas para:

* URL del centro de datos (dirección del extremo ASRP)
* Clave de consumidor
* Clave secreta
* ID del grupo de informes

Las claves de consumidor y secreto se comparten entre todos los grupos de informes de una empresa. Hay un grupo de informes por inquilino.

## Configuración {#configuration}

### Seleccionar ASRP {#select-asrp}

La [consola de configuración de almacenamiento](/help/communities/srp-config.md) permite seleccionar la configuración de almacenamiento predeterminada, que identifica qué implementación de SRP utilizar.

**En la instancia de autor de AEM:**

* En la navegación global, vaya a **[!UICONTROL Tools > Communities > Storage Configuration]** y seleccione **[!UICONTROL Adobe Storage Resource Provider (ASRP)]**.

![asrp-default](assets/asrp-default.png)

La siguiente información proviene del proceso de aprovisionamiento:

* **Dirección URL** del centro de datos: Desplegable para seleccionar el centro de datos de producción identificado por el representante de cuentas.
* **Grupo de informes predeterminado**: Introduzca el nombre del grupo de informes predeterminado.
* **Clave de consumidor**: Introduzca la clave de consumidor.
* **Secreto**: Escriba el secreto.
* Seleccione **Enviar**.

Prepare las instancias de publicación:

* [Replicar la clave criptográfica](#replicate-the-crypto-key)
* [Replicar la configuración](#publishing-the-configuration)

Después de enviar la configuración, pruebe la conexión:

* Seleccione **Probar configuración**.

   Para cada instancia de autor y publicación, pruebe la conexión al centro de datos desde la consola de configuración de almacenamiento.

* Asegúrese de que las direcciones URL del sitio para los datos de perfil se pueden enrutar desde el centro de datos [externalizando vínculos](#externalize-links).

### Replicar la clave criptográfica {#replicate-the-crypto-key}

La clave de consumidor y la clave secreta están cifradas. Para que las claves se cifren o desencripten correctamente, la clave principal de Granite Crypto debe ser la misma en todas las instancias AEM.

Siga las instrucciones en [Replicar la clave criptográfica](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Externalizar vínculos {#externalize-links}

Para los vínculos de perfil e imagen de perfil correctos, asegúrese de [Configurar el externalizador de vínculos](/help/sites-developing/externalizer.md) correctamente.

Asegúrese de que los dominios sean direcciones URL que se puedan enrutar desde la URL del centro de datos (extremo ASRP).

### Sincronización de tiempo {#time-synchronization}

Para que la autenticación con el extremo ASRP se realice correctamente, los equipos que ejecuten su AEM Communities alojado deben sincronizarse a tiempo, como con el [Protocolo de tiempo de red (NTP)](https://www.ntp.org/).

### Publicación de la configuración {#publishing-the-configuration}

ASRP debe identificarse como el almacén común en todas las instancias de autor y publicación.

Para que la configuración idéntica esté disponible en el entorno de publicación:

En la instancia de autor de AEM:

* Vaya del menú principal a **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Replication]**
* Seleccione **Activar árbol**
* **Ruta de inicio**: buscar  `/conf/global/settings/communities/srpc/`
* Anule la selección de **Solo modificado**
* Seleccione **Activar**

## Actualización desde AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Si habilita ASRP en un sitio de comunidad publicado, cualquier UGC ya almacenado en [JCR](/help/communities/jsrp.md) ya no será visible, ya que no hay sincronización de datos entre el almacenamiento local y el almacenamiento en la nube.

**`AEM Communities Extension`** se ha introducido anteriormente en AEM 6.0 social communities as a cloud service. A partir de AEM 6.1 Communities, no es necesaria ninguna configuración de nube, simplemente seleccione ASRP en la [consola de configuración de almacenamiento](/help/communities/srp-config.md).

Debido a la nueva estructura de almacenamiento, es necesario seguir las instrucciones de [actualización](/help/communities/upgrade.md#adobe-cloud-storage) al actualizar de comunidades sociales a comunidades.

## Administración de datos de usuario {#managing-user-data}

Para obtener información sobre los *usuarios*, *perfiles de usuario* y *grupos de usuarios*, que a menudo se introducen en el entorno de publicación, visite

* [Sincronización de usuarios](/help/communities/sync.md)
* [Administración de usuarios y grupos de usuarios](/help/communities/users.md)

## Solución de problemas {#troubleshooting}

### UGC desaparece después de la actualización {#ugc-disappears-after-upgrade}

Si actualiza desde un sitio de comunidad social de AEM 6.0 existente, asegúrese de seguir las [instrucciones de actualización](/help/communities/upgrade.md#adobe-cloud-storage); de lo contrario, parece que se ha perdido el UGC.

### Errores de autenticación {#authentication-errors}

Si recibe errores de autenticación contra la dirección URL del centro de datos y el archivo error.log AEM contiene mensajes sobre marcas de hora antiguas, compruebe que se esté realizando la sincronización de hora.

Utilice una herramienta como [Network Time Protocol (NTP)](https://www.ntp.org/) para sincronizar con el tiempo todos los servidores AEM autor y publicación.

### El contenido nuevo no aparece en las búsquedas {#new-content-does-not-appear-in-searches}

La infraestructura de almacenamiento de información en la nube de Adobe utiliza *consistencia eventual* para lograr sus objetivos de performance y escala. Por este motivo, el nuevo contenido no está disponible al instante y tarda varios segundos en aparecer en los resultados de búsqueda.

Mientras se supervisa el intervalo que afecta a la coherencia final, póngase en contacto con el representante de la cuenta si el contenido nuevo tarda más de unos segundos en aparecer en las búsquedas.

### UGC no visible en ASRP {#ugc-not-visible-in-asrp}

Asegúrese de que ASRP se haya configurado para ser el proveedor predeterminado comprobando la configuración de la opción de almacenamiento. De forma predeterminada, el proveedor de recursos de almacenamiento es JSRP, no ASRP.

En todas las instancias de creación y publicación de AEM, vuelva a la consola Configuración de almacenamiento o compruebe el repositorio de AEM.

En JCR, si [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* No contiene un nodo [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp), significa que el proveedor de almacenamiento es JSRP.
* Si el nodo srpc existe y contiene el nodo [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration) , las propiedades de configuración predeterminada definen ASRP como el proveedor predeterminado.
