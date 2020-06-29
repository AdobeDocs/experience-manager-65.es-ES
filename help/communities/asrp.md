---
title: ASRP - Proveedor de recursos de Almacenamiento de Adobe
seo-title: ASRP - Proveedor de recursos de Almacenamiento de Adobe
description: Configurar AEM Communities para utilizar una base de datos relacional como su almacén común
seo-description: Configurar AEM Communities para utilizar una base de datos relacional como su almacén común
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
translation-type: tm+mt
source-git-commit: cf2733ecee5c74b79b85267191fbdf3cbce9c98b
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---


# ASRP - Proveedor de recursos de Almacenamiento de Adobe {#asrp-adobe-storage-resource-provider}

## Acerca de ASRP {#about-asrp}

Cuando los AEM Communities están configurados para utilizar ASRP como su almacén común, el contenido generado por el usuario (UGC) es accesible desde todas las instancias de creación y publicación sin necesidad de sincronización ni replicación.

Consulte también [Características de las Opciones](/help/communities/working-with-srp.md#characteristics-of-srp-options) de SRP y Topologías [](/help/communities/topologies.md)recomendadas.

## Requisitos {#requirements}

Se requiere una licencia adicional para el uso de ASRP.

Para configurar el sitio de AEM Communities para que utilice ASRP para UGC, póngase en contacto con el representante de cuentas para:

* Dirección URL del centro de datos (dirección del extremo ASRP)
* Clave de consumidor
* Clave secreta
* ID del grupo de informes

Las claves de consumidor y clave secreta se comparten en todos los grupos de informes de una compañía. Hay un grupo de informes por inquilino.

## Configuración {#configuration}

### Seleccionar ASRP {#select-asrp}

La consola [Configuración de](/help/communities/srp-config.md) Almacenamiento permite seleccionar la configuración de almacenamiento predeterminada, que identifica la implementación de SRP que se va a utilizar.

**En la instancia de AEM Author:**

* En la navegación global, vaya a **[!UICONTROL Herramientas > Comunidades > Configuración]** de Almacenamiento y seleccione Proveedor de recursos de Almacenamiento de **[!UICONTROL Adobe (ASRP)]**.

![asrp-default](assets/asrp-default.png)

La siguiente información proviene del proceso de aprovisionamiento:

* **Dirección URL** del centro de datos: Despliegue para seleccionar el centro de datos de producción identificado por el representante de cuentas.
* **Grupo** de informes predeterminado: Escriba el nombre del grupo de informes predeterminado.
* **Clave del cliente**: Introduzca la clave del cliente.
* **Secreto**: Escribe el secreto.
* Seleccione **Enviar**.

Prepare las instancias de publicación:

* [Replicar la clave criptográfica](#replicate-the-crypto-key)
* [Replicar la configuración](#publishing-the-configuration)

Después de enviar la configuración, pruebe la conexión:

* Seleccione **Probar configuración**.

   Para cada instancia de creación y publicación, pruebe la conexión al centro de datos desde la consola de configuración de Almacenamiento.

* Asegúrese de que las direcciones URL del sitio para los datos de perfil se pueden enrutar desde el centro de datos [externalizando los vínculos](#externalize-links).

### Replicar la clave de cifrado {#replicate-the-crypto-key}

La Clave del cliente y la clave secreta están cifradas. Para que las claves se cifren o descifren correctamente, la clave de cifrado de granito principal debe ser la misma en todas las instancias de AEM.

Siga las instrucciones de [Replicar la clave](/help/communities/deploy-communities.md#replicate-the-crypto-key)de cifrado.

### Externalizar vínculos {#externalize-links}

Para los vínculos de imagen de perfil y perfil correctos, asegúrese de [configurar correctamente el Externalizador](/help/sites-developing/externalizer.md)de vínculos.

Asegúrese de establecer los dominios como direcciones URL que se pueden enrutar desde la dirección URL del centro de datos (extremo ASRP).

### Sincronización de tiempo {#time-synchronization}

Para que la autenticación con el extremo ASRP tenga éxito, los equipos que ejecutan sus AEM Communities alojados deben sincronizarse a la hora, como con el protocolo de tiempo de [red (NTP)](https://www.ntp.org/).

### Publicación de la configuración {#publishing-the-configuration}

ASRP debe identificarse como el almacén común en todas las instancias de creación y publicación.

Para que la configuración idéntica esté disponible en el entorno de publicación:

En la instancia de AEM Author:

* Vaya del menú principal a **[!UICONTROL Herramientas > Operaciones > Replicación]**.
* Seleccione **Activar árbol**
* **Ruta** de Inicio: buscar `/etc/socialconfig/srpc/`
* Anular selección de **sólo modificado**
* Seleccionar **activar**

## Actualización desde AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Si habilita ASRP en un sitio de comunidad publicado, ya no se podrá ver ningún UGC almacenado en [JCR](/help/communities/jsrp.md) , ya que no hay sincronización de datos entre el almacenamiento local y el almacenamiento en la nube.

**`AEM Communities Extension`** anteriormente se introdujo en las comunidades sociales de AEM 6.0 como un servicio en la nube. A partir de AEM 6.1 Communities, no es necesaria ninguna configuración de nube, simplemente seleccione ASRP en la consola [de configuración de](/help/communities/srp-config.md)almacenamiento.

Debido a la nueva estructura de almacenamientos, es necesario seguir las instrucciones de [actualización](/help/communities/upgrade.md#adobe-cloud-storage) al pasar de las comunidades sociales a las comunidades.

## Administración de datos de usuario {#managing-user-data}

Para obtener información sobre *usuarios*, perfiles *de* usuarios y grupos *de* usuarios, que se especifican a menudo en el entorno de publicación, visite

* [Sincronización de usuarios](/help/communities/sync.md)
* [Administración de usuarios y grupos de usuarios](/help/communities/users.md)

## Solución de problemas {#troubleshooting}

### UGC desaparece tras la actualización {#ugc-disappears-after-upgrade}

Si realiza la actualización desde un sitio de comunidad social de AEM 6.0, asegúrese de seguir las instrucciones [de](/help/communities/upgrade.md#adobe-cloud-storage)actualización; de lo contrario, parece que se ha perdido UGC.

### Errores de autenticación {#authentication-errors}

Si recibe errores de autenticación con la dirección URL del centro de datos y el archivo error.log de AEM contiene mensajes sobre marcas de hora antiguas, compruebe que se esté realizando la sincronización de hora.

Utilice una herramienta como el Protocolo de tiempo de [red (NTP)](https://www.ntp.org/) para sincronizar con el tiempo todos los servidores de publicación y creación de AEM.

### El nuevo contenido no aparece en las búsquedas {#new-content-does-not-appear-in-searches}

La infraestructura de almacenamiento en la nube de Adobe utiliza *la coherencia* para lograr sus objetivos de rendimiento y escala. Por este motivo, el nuevo contenido no está disponible al instante y tarda varios segundos en aparecer en los resultados de búsqueda.

Mientras se supervisa el intervalo que afecta a la coherencia final, póngase en contacto con el representante de la cuenta si el contenido nuevo tarda más de unos segundos en aparecer en las búsquedas.

### UGC no visible en ASRP {#ugc-not-visible-in-asrp}

Asegúrese de que el ASRP se haya configurado para que sea el proveedor predeterminado mediante la comprobación de la configuración de la opción de almacenamiento. De forma predeterminada, el proveedor de recursos de almacenamiento es JSRP, no ASRP.

En todas las instancias de AEM de creación y publicación, vuelva a la consola de configuración de Almacenamiento o compruebe el repositorio de AEM.

En JCR, si [/etc/socialconfig](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* No contiene un nodo [srpc](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , significa que el proveedor de almacenamiento es JSRP.
* Si el nodo srpc existe y contiene la configuración [predeterminada](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)del nodo, las propiedades de configuración predeterminada definen ASRP como el proveedor predeterminado.

