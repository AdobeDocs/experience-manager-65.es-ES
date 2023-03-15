---
title: Configurar OSGi
seo-title: Configuring OSGi
description: OSGi es un elemento fundamental en la pila tecnológica de Adobe Experience Manager AEM (). AEM Se utiliza para controlar los paquetes compuestos de y su configuración de los paquetes de componentes de la interfaz de usuario de la interfaz de usuario de. Este artículo detalla cómo puede administrar los ajustes de configuración para estos paquetes.
seo-description: OSGi is a fundamental element in the technology stack of Adobe Experience Manager (AEM). It is used to control the composite bundles of AEM and their configuration. This article details how you can manage the configuration settings for such bundles.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 0%

---

# Configurar OSGi{#configuring-osgi}

[OSGi](https://www.osgi.org/) es un elemento fundamental de la pila tecnológica de Adobe Experience Manager AEM (). AEM Se utiliza para controlar los paquetes compuestos de y su configuración de los paquetes de componentes de la interfaz de usuario de la interfaz de usuario de.

OSGi &quot;*proporciona las primitivas estandarizadas que permiten crear aplicaciones a partir de componentes pequeños, reutilizables y de colaboración. Estos componentes se pueden componer en una aplicación e implementarse*&quot;.

Esto permite administrar fácilmente los paquetes, ya que se pueden detener, instalar e iniciar individualmente. Las interdependencias se gestionan automáticamente. Cada componente OSGi (consulte la [Especificación de OSGi](https://www.osgi.org/Specifications/HomePage)) está contenido en uno de los distintos paquetes.

Puede administrar los ajustes de configuración de estos paquetes mediante las siguientes opciones:

* uso del [Consola web de Adobe CQ](#osgi-configuration-with-the-web-console)
* usando [archivos de configuración](#osgi-configuration-with-configuration-files)
* configuración [content-nodes ( `sling:OsgiConfig`) en el repositorio](#osgi-configuration-in-the-repository)

Se puede utilizar cualquiera de los dos métodos aunque hay diferencias sutiles, principalmente en relación con [Modos de ejecución](/help/sites-deploying/configure-runmodes.md):

* [Consola web de Adobe CQ](#osgi-configuration-with-the-web-console)

   * La consola web es la interfaz estándar para la configuración de OSGi. Proporciona una interfaz de usuario para editar las distintas propiedades, donde es posible seleccionar valores de listas predefinidas.

      Como tal, es el método más fácil de usar.

   * Cualquier configuración realizada con la consola web se aplica inmediatamente y se aplica a la instancia actual, independientemente del modo de ejecución actual o de cualquier cambio posterior en el modo de ejecución.

* [archivos de configuración](#osgi-configuration-with-configuration-files)

   * Contiene la configuración definida en la consola web.
   * Se puede incluir en paquetes de contenido para usarlos en otras instancias.

* [content-nodes (sling:osgiConfig) en el repositorio](#osgi-configuration-in-the-repository)

   * Esto requiere una configuración manual con el CRXDE Lite.
   * Debido a las convenciones de nomenclatura de `sling:OsgiConfig` , puede enlazar la configuración a un nodo específico [modo de ejecución](/help/sites-deploying/configure-runmodes.md). Incluso puede guardar configuraciones para más de un modo de ejecución en el mismo repositorio.
   * Las configuraciones adecuadas se aplican inmediatamente (según el modo de ejecución).

Sea cual sea el método que utilice, todos estos métodos de configuración:

* Asegúrese de que al copiar o replicar el contenido del repositorio se vuelven a crear configuraciones idénticas.
* Le permite retirar configuraciones a FileVault o Subversion; ya sea por seguridad o por más actualizaciones.
* Se puede guardar en paquetes para utilizarlos al configurar otras instancias.
* Permite realizar despliegues de configuración utilizando secuencias de comandos para propagar los detalles de configuración.

>[!NOTE]
>
>Los detalles de ciertas configuraciones importantes se enumeran en [Ajustes de configuración de OSGi.](/help/sites-deploying/osgi-configuration-settings.md)

## Configuración de OSGi con la consola web {#osgi-configuration-with-the-web-console}

El [consola web](/help/sites-deploying/web-console.md) AEM en proporciona una interfaz estandarizada para configurar los paquetes. El **Configuración** AEM se utiliza para configurar los paquetes OSGi y, por lo tanto, es el mecanismo subyacente para configurar los parámetros del sistema de la.

Los cambios realizados se aplican inmediatamente a la configuración de OSGi correspondiente, no se requiere reiniciar.

>[!NOTE]
>
>Los cambios realizados en la consola web se guardan en el repositorio como [archivos de configuración](#osgi-configuration-with-configuration-files). Pueden incluirse en paquetes de contenido para su reutilización en instalaciones posteriores.

>[!NOTE]
>
>En la consola web, cualquier descripción que mencione la configuración predeterminada está relacionada con los valores predeterminados de Sling.
>
>Adobe Experience Manager tiene sus propios valores predeterminados y, por lo tanto, los valores predeterminados establecidos pueden diferir de los documentados en la consola.

Para actualizar una configuración con la consola web:

1. Acceda a la **Configuración** de la consola web mediante:

   * Al abrir la consola web desde el vínculo en la **Herramienta -> Operaciones** menú. Después de iniciar sesión en la consola, puede utilizar el menú desplegable de:

      **los paquetes >**

   * La dirección URL directa; por ejemplo:

      `http://localhost:4502/system/console/configMgr`
   Se mostrará una lista.

1. Seleccione el paquete que desea configurar mediante:

   * haciendo clic en **Editar** icono para ese paquete
   * haciendo clic en **Nombre** del paquete

1. Se abrirá un cuadro de diálogo: Aquí puede realizar las modificaciones necesarias; por ejemplo, defina las **Nivel de registro** hasta `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >Las actualizaciones se guardan en el repositorio como [archivos de configuración](#osgi-configuration-with-configuration-files). Para localizarlos posteriormente (por ejemplo, para incluirlos en un paquete de contenido para usarlos en otra instancia) debe tomar nota de la identidad persistente ( `PID`).

1. Haga clic en **Guardar**.

   Los cambios se aplican inmediatamente a la configuración OSGi relevante del sistema en ejecución; no se requiere reiniciar.

   >[!NOTE]
   >
   >Ahora puede localizar el [archivos de configuración](#osgi-configuration-with-configuration-files); por ejemplo, para incluir en un paquete de contenido para utilizarlo en otra instancia.

## Configuración de OSGi con archivos de configuración {#osgi-configuration-with-configuration-files}

Los cambios de configuración realizados mediante la consola web se mantienen en el repositorio como archivos de configuración ( `.config`) en:

`/apps`

Pueden incluirse en paquetes de contenido y reutilizarse en otras instancias.

>[!NOTE]
>
>El formato de los archivos de configuración es muy específico; consulte la [Documentación de Sling Apache](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format) para obtener información detallada.
>
>Por este motivo, se recomienda crear y mantener el archivo de configuración realizando cambios reales en la consola web.

La consola web no muestra ninguna indicación de dónde se han guardado los cambios en el repositorio, pero se pueden localizar fácilmente:

1. Cree el archivo de configuración mediante [realización de un cambio inicial en la consola web](#osgi-configuration-with-the-web-console).
1. Abra CRXDE Lite.
1. En el **Herramientas** selección de menú **Consulta...** .
1. Enviar una consulta de **Tipo** `SQL` para buscar el PID de la configuración que ha actualizado.

   Por ejemplo, **Consola de administración de Apache Felix OSGi** tiene la identidad persistente (PID) de:

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   Por lo tanto, la consulta SQL podría ser:

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. Se mostrará el nodo del archivo de configuración.

   Para el ejemplo anterior:

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >Puede abrir este archivo para ver los cambios, pero para evitar errores de escritura, se recomienda realizar cambios reales con la consola.

1. Ahora puede crear un paquete de contenido que contenga este nodo y utilizarlo según sea necesario en las demás instancias.

## Configuración de OSGi en el repositorio {#osgi-configuration-in-the-repository}

Además de utilizar la consola web, también puede definir los detalles de configuración en el repositorio. Esto le permite configurar fácilmente los diferentes modos de ejecución.

Estas configuraciones se realizan creando lo siguiente `sling:OsgiConfig` nodos en el repositorio a los que hace referencia el sistema. Estos nodos reflejan las configuraciones de OSGi y forman una interfaz de usuario para ellas. Para actualizar los datos de configuración, actualice las propiedades del nodo.

Si modifica los datos de configuración en el repositorio, los cambios se aplican inmediatamente a la configuración de OSGi correspondiente como si los cambios se hubieran realizado mediante la consola web, con las comprobaciones de validación y coherencia adecuadas. Esto también se aplica a la acción de copiar una configuración de `/libs/` hasta `/apps/`.

Como el mismo parámetro de configuración se puede encontrar en varios lugares, el sistema:

* busca todos los nodos del tipo `sling:OsgiConfig`
* filtros según el nombre del servicio
* filtros según el modo de ejecución

>[!NOTE]
>
>Lea también [cómo definir una restricción basada en el repositorio solo para una instancia específica](https://helpx.adobe.com/experience-manager/kb/RunModeDependentConfigAndInstall.html).

### Adición de una nueva configuración al repositorio {#adding-a-new-configuration-to-the-repository}

#### Lo que necesita saber {#what-you-need-to-know}

Para añadir una nueva configuración al repositorio, debe saber lo siguiente:

1. El **Identidad persistente** (PID) del servicio.

   Haga referencia a **Configuraciones** en la consola web. El nombre se muestra entre corchetes después del nombre del paquete (o en el **Información de configuración** hacia la parte inferior de la página).

   Por ejemplo, cree un nodo `com.day.cq.wcm.core.impl.VersionManagerImpl.` para configurar **AEM Administrador de versiones de WCM de**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Si una [modo de ejecución](/help/sites-deploying/configure-runmodes.md) es obligatorio. Cree la carpeta:

   * `config` - para todos los modos de ejecución
   * `config.author` - para el entorno de creación
   * `config.publish` - para el entorno de publicación
   * `config.<run-mode>` - según proceda

1. Si un **Configuración** o **Configuración de fábrica** es necesario.
1. Los parámetros individuales que se van a configurar, incluidas las definiciones de parámetros existentes que se tendrán que volver a crear.

   Haga referencia al campo de parámetro individual en la consola web. El nombre se muestra entre corchetes para cada parámetro.

   Por ejemplo, cree una propiedad
   `versionmanager.createVersionOnActivation` para configurar **Crear versión al activar**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. ¿Ya existe una configuración en? `/libs`? Para enumerar todas las configuraciones en la instancia, utilice el **Consulta** en CRXDE Lite para enviar la siguiente consulta SQL:

   `select * from sling:OsgiConfig`

   Si es así, esta configuración se puede copiar en ` /apps/<yourProject>/`, luego personalizado en la nueva ubicación.

#### Creación de la configuración en el repositorio {#creating-the-configuration-in-the-repository}

Para agregar realmente la nueva configuración al repositorio:

1. Utilice el CRXDE Lite para ir a:

   ` /apps/<yourProject>`

1. Si no existe todavía, cree el `config` carpeta ( `sling:Folder`):

   * `config` - aplicable a todos los modos de ejecución
   * `config.<run-mode>` - específico de un modo de ejecución concreto

1. En esta carpeta, cree un nodo:

   * Tipo: `sling:OsgiConfig`
   * Nombre: la identidad persistente (PID);

      AEM por ejemplo, para el uso de Administrador de versiones de WCM de `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >Al realizar un anexo de configuración de fábrica `-<identifier>` al nombre.
   >
   >Como en: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >Donde `<identifier>` se sustituye por texto libre que se debe introducir para identificar la instancia (no se puede omitir esta información); por ejemplo:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. Para cada parámetro que desee configurar, cree una propiedad en este nodo:

   * Nombre: el nombre del parámetro como se muestra en la consola web; el nombre se muestra entre corchetes al final de la descripción del campo. Por ejemplo, para `Create Version on Activation` use `versionmanager.createVersionOnActivation`
   * Tipo: según corresponda.
   * Valor: según sea necesario.

   AEM Solo debe crear propiedades para los parámetros que desea configurar; otros tomarán los valores predeterminados establecidos por el usuario, según lo establecido por el método de la configuración de la variable de parámetros de la lista de parámetros.

1. Guarde todos los cambios.

   Los cambios se aplican en cuanto se actualiza el nodo reiniciando el servicio (como con los cambios realizados en la consola web).

>[!CAUTION]
>
>No debe cambiar nada en el `/libs` ruta.

>[!CAUTION]
>
>La ruta completa de una configuración debe ser correcta para que se lea al inicio.

## Detalles de configuración {#configuration-details}

### Orden de resolución al inicio {#resolution-order-at-startup}

Se utiliza el siguiente orden de prioridad:

1. Nodos de repositorio en `/apps/*/config...`.ya sea con tipo `sling:OsgiConfig` o archivos de propiedad.

1. Nodos de repositorio con tipo `sling:OsgiConfig` bajo `/libs/*/config...`. (definiciones listas para usar).

1. Cualquiera `.config` archivos de `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. en el sistema de archivos local.

Esto significa que una configuración genérica en `/libs` se puede ocultar con una configuración específica del proyecto en `/apps`.

### Orden de resolución en tiempo de ejecución {#resolution-order-at-runtime}

Los cambios de configuración realizados mientras el sistema se ejecuta déclencheur una recarga con la configuración modificada.

A continuación, se aplica el siguiente orden de prioridad:

1. La modificación de una configuración en la consola web surtirá efecto inmediatamente, ya que tendrá prioridad durante la ejecución.
1. Modificación de una configuración en `/apps` tendrá efecto inmediato.
1. Modificación de una configuración en `/libs` tendrá efecto inmediato, a menos que esté enmascarado por una configuración en `/apps`.

### Resolución de varios modos de ejecución {#resolution-of-multiple-run-modes}

Para configuraciones específicas del modo de ejecución, se pueden combinar varios modos de ejecución. Por ejemplo, puede crear carpetas de configuración con el siguiente estilo:

`/apps/*/config.<runmode1>.<runmode2>/`

Las configuraciones en dichas carpetas se aplicarán si todos los modos de ejecución coinciden con un modo de ejecución definido al inicio.

Por ejemplo, si se inició una instancia con los modos de ejecución `author,dev,emea`, nodos de configuración en `/apps/*/config.emea`, `/apps/*/config.author.dev/` y `/apps/*/config.author.emea.dev/` se aplicarán mientras los nodos de configuración en `/apps/*/config.author.asean/` y `/config/author.dev.emea.noldap/` no se aplicará.

Si se aplican varias configuraciones para el mismo PID, se aplica la configuración con el número más alto de modos de ejecución coincidentes.

Por ejemplo, si se inició una instancia con los modos de ejecución `author,dev,emea`, y ambas `/apps/*/config.author/` y `/apps/*/config.emea.author/` defina una configuración para
`com.day.cq.wcm.core.impl.VersionManagerImpl`, la configuración en `/apps/*/config.emea.author/` se aplicarán.

La granularidad de esta regla es de nivel PID.
No se pueden definir algunas propiedades para el mismo PID en `/apps/*/config.author/` y más específicos en `/apps/*/config.emea.author/` para el mismo PID.
La configuración con el mayor número de modos de ejecución coincidentes será efectiva para todo el PID.

### Configuraciones estándar {#standard-configurations}

La siguiente lista muestra una pequeña selección de las configuraciones disponibles (en una instalación estándar) en el repositorio:

* AEM Autor - Filtro de WCM de:

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* AEM Publicar - Filtro de WCM de la:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* AEM Publicar - Estadísticas de página de WCM de la:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>Como estas configuraciones residen en `/libs` no deben editarse directamente, sino copiarse en el área de aplicación ( `/apps`) antes de la personalización.

Para enumerar todos los nodos de configuración de la instancia, utilice el **Consulta** funcionalidad en CRXDE Lite para enviar la siguiente consulta SQL:

`select * from sling:OsgiConfig`

### Persistencia de configuración {#configuration-persistence}

* Si cambia una configuración a través de la consola web, (normalmente) se escribe en el repositorio en:

   `/apps/{somewhere}`

   * De forma predeterminada `{somewhere}` es `system/config` por lo tanto, la configuración se escribe en

      `/apps/system/config`

   * Sin embargo, si está editando una configuración que inicialmente provino de otra parte del repositorio: por ejemplo:

      /libs/foo/config/someconfig

      A continuación, la configuración actualizada se escribe en la ubicación original; por ejemplo:

      `/apps/foo/config/someconfig`

* Configuración que ha cambiado `admin` se guardan en `*.config` archivos en:

   ```
      /crx-quickstart/launchpad/config
   ```

   * Es el área de datos privados del administrador de configuración de OSGi y contiene todos los detalles de configuración especificados por `admin`, independientemente de cómo hayan entrado en el sistema.
   * Este es un detalle de implementación y nunca debe editar este directorio directamente.
   * Sin embargo, es útil conocer la ubicación de estos archivos de configuración para que se puedan realizar copias de seguridad o instalaciones múltiples:

      * Consola de administración de Apache Felix OSGi

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * Repositorio de clientes de CRX Sling

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>Usted debe ***nunca*** edite las carpetas o archivos en:
>
>`/crx-quickstart/launchpad/config`
