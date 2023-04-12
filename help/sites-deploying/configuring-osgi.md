---
title: Configuración de OSGi
seo-title: Configuring OSGi
description: OSGi es un elemento fundamental de la pila tecnológica de Adobe Experience Manager (AEM). Se utiliza para controlar los paquetes compuestos de AEM y su configuración. Este artículo detalla cómo puede administrar los ajustes de configuración de estos paquetes.
seo-description: OSGi is a fundamental element in the technology stack of Adobe Experience Manager (AEM). It is used to control the composite bundles of AEM and their configuration. This article details how you can manage the configuration settings for such bundles.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 0%

---

# Configuración de OSGi{#configuring-osgi}

[OSGi](https://www.osgi.org/) es un elemento fundamental de la pila tecnológica de Adobe Experience Manager (AEM). Se utiliza para controlar los paquetes compuestos de AEM y su configuración.

OSGi &quot;*proporciona los primitivos estandarizados que permiten construir aplicaciones a partir de componentes pequeños, reutilizables y colaborativos. Estos componentes se pueden componer en una aplicación e implementar*&quot;.

De este modo, es fácil gestionar los paquetes a medida que se pueden detener, instalar e iniciar individualmente. Las interdependencias se gestionan automáticamente. Cada componente OSGi (consulte la [Especificación de OSGi](https://docs.osgi.org/specification/)) está contenido en uno de los distintos paquetes.

Puede administrar los ajustes de configuración de estos paquetes mediante:

* usando la variable [Consola web de Adobe CQ](#osgi-configuration-with-the-web-console)
* using [archivos de configuración](#osgi-configuration-with-configuration-files)
* configurar [nodos de contenido ( `sling:OsgiConfig`) en el repositorio](#osgi-configuration-in-the-repository)

Cualquiera de los métodos puede utilizarse aunque haya diferencias sutiles, principalmente en relación con [Modos de ejecución](/help/sites-deploying/configure-runmodes.md):

* [Consola web de Adobe CQ](#osgi-configuration-with-the-web-console)

   * La Consola Web es la interfaz estándar para la configuración OSGi. Proporciona una interfaz de usuario para editar las distintas propiedades, donde se pueden seleccionar valores posibles de listas predefinidas.

      Como tal, es el método más fácil de usar.

   * Las configuraciones realizadas con la consola web se aplican inmediatamente y son aplicables a la instancia actual, independientemente del modo de ejecución actual o de los cambios posteriores en el modo de ejecución.

* [archivos de configuración](#osgi-configuration-with-configuration-files)

   * Contiene la configuración definida en la consola web.
   * Se puede incluir en paquetes de contenido para su uso en otras instancias.

* [content-nodes (sling:osgiConfig) en el repositorio](#osgi-configuration-in-the-repository)

   * Requiere una configuración manual mediante el CRXDE Lite.
   * Debido a las convenciones de nomenclatura de la variable `sling:OsgiConfig` , puede enlazar la configuración a un [modo de ejecución](/help/sites-deploying/configure-runmodes.md). Incluso puede guardar configuraciones para más de un modo de ejecución en el mismo repositorio.
   * Las configuraciones adecuadas se aplican inmediatamente (depende del modo de ejecución).

Cualquiera que sea el método que utilice, todos estos métodos de configuración:

* Asegúrese de que al copiar o replicar el contenido del repositorio se recrean configuraciones idénticas.
* Permiten comprobar las configuraciones en FileVault o Subversion; para seguridad o para actualizaciones adicionales.
* Se puede guardar en paquetes para utilizarlos al configurar otras instancias.
* Permite realizar implementaciones de configuración mediante secuencias de comandos para propagar los detalles de configuración.

>[!NOTE]
>
>Los detalles de ciertas configuraciones importantes se enumeran en [Ajustes de configuración de OSGi.](/help/sites-deploying/osgi-configuration-settings.md)

## Configuración de OSGi con la consola web {#osgi-configuration-with-the-web-console}

La variable [Consola web](/help/sites-deploying/web-console.md) en AEM proporciona una interfaz estandarizada para configurar los paquetes. La variable **Configuración** se utiliza para configurar los paquetes OSGi y, por lo tanto, es el mecanismo subyacente para configurar AEM parámetros del sistema.

Los cambios realizados se aplican inmediatamente a la configuración OSGi relevante, no es necesario reiniciar.

>[!NOTE]
>
>Los cambios realizados en la consola web se guardan en el repositorio como [archivos de configuración](#osgi-configuration-with-configuration-files). Estos archivos se pueden incluir en paquetes de contenido para su reutilización en instalaciones posteriores.

>[!NOTE]
>
>En la consola web, cualquier descripción que mencione la configuración predeterminada está relacionada con los valores predeterminados de Sling.
>
>Adobe Experience Manager tiene sus propios valores predeterminados, por lo que los valores predeterminados que se establecen pueden diferir de los valores predeterminados documentados en la consola.

Para actualizar una configuración con la consola web:

1. Acceda a la **Configuración** de la Consola Web mediante:

   * Apertura de la consola web desde el vínculo en el **Herramienta -> Operaciones** para abrir el Navegador. Después de iniciar sesión en la consola, puede utilizar el menú desplegable de:

      **OSGi >**

   * La dirección URL directa; por ejemplo:

      `http://localhost:4502/system/console/configMgr`
   Se muestra una lista.

1. Seleccione el paquete que desea configurar mediante:

   * haga clic en **Editar** icono para ese paquete
   * haga clic en **Nombre** del paquete

1. Se abre un cuadro de diálogo. Aquí puede editar según sea necesario. Por ejemplo, establezca la variable **Nivel de registro** a `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >Las actualizaciones se guardan en el repositorio como [archivos de configuración](#osgi-configuration-with-configuration-files). Para localizar estos archivos posteriormente para incluirlos en un paquete de contenido para usarlos en otra instancia, por ejemplo, tome nota de la identidad persistente ( `PID`).

1. Haga clic en **Guardar**.

   Los cambios se aplican inmediatamente a la configuración OSGi relevante del sistema en ejecución, no es necesario reiniciar.

   >[!NOTE]
   >
   >Ahora puede localizar el [archivos de configuración](#osgi-configuration-with-configuration-files). Por ejemplo, para incluir en un paquete de contenido para utilizarlo en otra instancia.

## Configuración de OSGi con archivos de configuración {#osgi-configuration-with-configuration-files}

Los cambios de configuración realizados con la consola web se mantienen en el repositorio como archivos de configuración ( `.config`) en:

`/apps`

Estos archivos se pueden incluir en paquetes de contenido y reutilizar en otras instancias.

>[!NOTE]
>
>El formato de los archivos de configuración es específico; consulte la [Documentación de Sling Apache](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format) para obtener más información.
>
>Por este motivo, se recomienda crear y mantener el archivo de configuración realizando cambios reales en la consola web.

La consola web no muestra en qué parte del repositorio se han guardado los cambios, pero se pueden localizar fácilmente:

1. Cree el archivo de configuración de [realización de un cambio inicial en la consola web](#osgi-configuration-with-the-web-console).
1. Abra CRXDE Lite.
1. En el **Herramientas** seleccione **Consulta ...** .
1. Para buscar el PID de la configuración que ha actualizado, envíe una consulta de **Tipo** `SQL`.

   Por ejemplo, **Consola de administración Apache Felix OSGi** tiene la identidad persistente (PID) de:

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   Por lo tanto, la consulta SQL podría ser:

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. Se muestra el nodo del archivo de configuración.

   Para el ejemplo anterior:

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >Puede abrir este archivo para ver los cambios, pero para evitar errores de escritura, se recomienda realizar cambios reales con la consola.

1. Ahora puede crear un paquete de contenido que contenga este nodo y utilizarlo como sea necesario en las demás instancias.

## Configuración de OSGi en el repositorio {#osgi-configuration-in-the-repository}

Además de utilizar la consola web, también puede definir los detalles de configuración en el repositorio. Al hacerlo, puede configurar fácilmente los distintos modos de ejecución.

Estas configuraciones se realizan creando `sling:OsgiConfig` nodos en el repositorio al que hace referencia el sistema. Estos nodos reflejan las configuraciones de OSGi y se les forma una interfaz de usuario. Para actualizar los datos de configuración, actualice las propiedades del nodo.

Si modifica los datos de configuración en el repositorio, los cambios se aplican inmediatamente a la configuración OSGi relevante. Es como si los cambios se hubieran realizado utilizando la consola web, con las correspondientes comprobaciones de validación y coherencia. Este flujo de trabajo también se aplica a la acción de copiar una configuración de `/libs/` a `/apps/`.

Como el mismo parámetro de configuración se encuentra en varios lugares, el sistema:

* busca todos los nodos del tipo `sling:OsgiConfig`
* filtros según el nombre del servicio
* filtros según el modo de ejecución

>[!NOTE]
>
>Lea también [cómo definir una configuración basada en repositorios solo para una instancia específica](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17500.html?lang=en).

### Adición de una nueva configuración al repositorio {#adding-a-new-configuration-to-the-repository}

#### Qué debe saber {#what-you-need-to-know}

Para agregar una configuración al repositorio, debe saber lo siguiente:

1. La variable **Identidad persistente** (PID) del servicio.

   Consulte la **Configuraciones** en la consola web. El nombre se muestra entre corchetes después del nombre del paquete (o en el **Información de configuración** hacia la parte inferior de la página).

   Por ejemplo, crear un nodo `com.day.cq.wcm.core.impl.VersionManagerImpl.` para configurar **Administrador de versiones de WCM AEM**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Es un [modo de ejecución](/help/sites-deploying/configure-runmodes.md) obligatorio? Cree la carpeta:

   * `config` - para todos los modos de ejecución
   * `config.author` - para el entorno de creación
   * `config.publish` - para el entorno de publicación
   * `config.<run-mode>` - según proceda

1. Es un **Configuración** o **Configuración de fábrica** ¿es necesario?
1. Los parámetros individuales que se van a configurar, incluidas las definiciones de parámetros existentes que se deben volver a crear.

   Haga referencia al campo de parámetro individual en la consola web. El nombre se muestra entre corchetes para cada parámetro.

   Por ejemplo, crear una propiedad
   `versionmanager.createVersionOnActivation` para configurar **Crear versión al activar**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. ¿Existe una configuración en `/libs`? Para enumerar todas las configuraciones en la instancia, utilice el **Consulta** herramienta en CRXDE Lite para enviar la siguiente consulta SQL:

   `select * from sling:OsgiConfig`

   Si es así, esta configuración se puede copiar en ` /apps/<yourProject>/`, luego se personaliza en la nueva ubicación.

#### Creación de la configuración en el repositorio {#creating-the-configuration-in-the-repository}

Para añadir la nueva configuración al repositorio:

1. Utilice el CRXDE Lite para desplazarse a:

   ` /apps/<yourProject>`

1. Si no existe, cree la variable `config` carpeta ( `sling:Folder`):

   * `config` - aplicable a todos los modos de ejecución
   * `config.<run-mode>` : específico para un modo de ejecución determinado

1. En esta carpeta, cree un nodo:

   * Tipo: `sling:OsgiConfig`
   * Nombre: la identidad persistente (PID);

      por ejemplo, para AEM uso del administrador de versiones de WCM `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >Al realizar un anexado de configuración de fábrica `-<identifier>` al nombre.
   >
   >Como en: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >Donde `<identifier>` se reemplaza por texto libre que debe introducir para identificar la instancia (no puede omitir esta información); por ejemplo:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. Para cada parámetro que desee configurar, cree una propiedad en este nodo:

   * Nombre: el nombre del parámetro como se muestra en la consola web; el nombre se muestra entre corchetes al final de la descripción del campo. Por ejemplo, para `Create Version on Activation` use `versionmanager.createVersionOnActivation`
   * Tipo: según proceda.
   * Valor: según sea necesario.

   Solo debe crear propiedades para los parámetros que desea configurar, mientras que otros siguen tomando los valores predeterminados establecidos por AEM.

1. Guarde todos los cambios.

   Los cambios se aplican cuando se actualiza el nodo reiniciando el servicio (como sucede con los cambios realizados en la consola web).

>[!CAUTION]
>
>No cambie nada en la variable `/libs` ruta.

>[!CAUTION]
>
>La ruta completa de una configuración debe ser correcta para que se lea al inicio.

## Detalles de configuración {#configuration-details}

### Orden de resolución al inicio {#resolution-order-at-startup}

Se utiliza el siguiente orden de prioridad:

1. Nodos del repositorio bajo `/apps/*/config...`.o con tipo `sling:OsgiConfig` o archivos de propiedad.

1. Nodos de repositorio con tipo `sling:OsgiConfig` under `/libs/*/config...`. (definiciones predeterminadas).

1. Cualquiera `.config` archivos de `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. en el sistema de archivos local.

Una configuración genérica de `/libs` se puede ocultar mediante una configuración específica del proyecto en `/apps`.

### Orden de resolución en tiempo de ejecución {#resolution-order-at-runtime}

Los cambios de configuración realizados mientras el sistema ejecuta déclencheur de recarga con la configuración modificada.

A continuación, se aplica el siguiente orden de prioridad:

1. La modificación de una configuración en la consola web tiene efecto inmediato, ya que tiene prioridad durante la ejecución.
1. Modificación de una configuración en `/apps` tiene efecto inmediato.
1. Modificación de una configuración en `/libs` tiene efecto inmediato, a menos que esté enmascarado por una configuración de `/apps`.

### Resolución de varios modos de ejecución {#resolution-of-multiple-run-modes}

Para configuraciones específicas del modo de ejecución, se pueden combinar varios modos de ejecución. Por ejemplo, puede crear carpetas de configuración en el siguiente estilo:

`/apps/*/config.<runmode1>.<runmode2>/`

Las configuraciones en dichas carpetas se aplican si todos los modos de ejecución coinciden con un modo de ejecución definido al inicio.

Por ejemplo, si se inició una instancia con los modos de ejecución `author,dev,emea`, nodos de configuración en `/apps/*/config.emea`, `/apps/*/config.author.dev/`y `/apps/*/config.author.emea.dev/` mientras se aplican los nodos de configuración en `/apps/*/config.author.asean/` y `/config/author.dev.emea.noldap/` no se aplican.

Si se aplican varias configuraciones para el mismo PID, se aplica la configuración con el mayor número de modos de ejecución coincidentes.

Por ejemplo, si se inició una instancia con los modos de ejecución `author,dev,emea`y ambos `/apps/*/config.author/` y `/apps/*/config.emea.author/` definir una configuración para
`com.day.cq.wcm.core.impl.VersionManagerImpl`, la configuración de `/apps/*/config.emea.author/` se aplica.

La granularidad de esta regla se encuentra en el nivel de PID.
No se pueden definir algunas propiedades para el mismo PID en `/apps/*/config.author/` y más específicos en `/apps/*/config.emea.author/` para el mismo PID.
La configuración con el mayor número de modos de ejecución coincidentes es efectiva para todo el PID.

### Configuraciones estándar {#standard-configurations}

La siguiente lista muestra una pequeña selección de las configuraciones disponibles (en una instalación estándar) en el repositorio:

* Autor: AEM filtro WCM:

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* Publicar: AEM filtro WCM:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* Publicar: AEM Estadísticas de página de WCM:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>Como estas configuraciones residen en `/libs` no deben editarse directamente, sino copiarse en el área de la aplicación ( `/apps`) antes de la personalización.

Para enumerar todos los nodos de configuración en la instancia, utilice el **Consulta** en CRXDE Lite para enviar la siguiente consulta SQL:

`select * from sling:OsgiConfig`

### Persistencia de configuración {#configuration-persistence}

* Si cambia una configuración a través de la consola web, (normalmente) se escribe en el repositorio en:

   `/apps/{somewhere}`

   * De forma predeterminada `{somewhere}` es `system/config` por lo tanto, la configuración se escribe en

      `/apps/system/config`

   * Sin embargo, si está editando una configuración que inicialmente proviene de otras partes del repositorio: por ejemplo:

      /libs/foo/config/someconfig

      A continuación, la configuración actualizada se escribe en la ubicación original; por ejemplo:

      `/apps/foo/config/someconfig`

* Configuración que cambia `admin` se guardan en `*.config` archivos en:

   ```
      /crx-quickstart/launchpad/config
   ```

   * Esta área es los datos privados del administrador de configuración de OSGi y contiene todos los detalles de configuración especificados por `admin`, independientemente de cómo hayan entrado en el sistema.
   * Esta área es un detalle de implementación y nunca debe editar este directorio directamente.
   * Sin embargo, es útil conocer la ubicación de estos archivos de configuración para que se puedan realizar copias de seguridad, o varias instalaciones, o ambas:

      * Consola de administración Apache Felix OSGi

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * Repositorio de cliente CRX Sling

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>Nunca edite las carpetas o archivos en:
>
>`/crx-quickstart/launchpad/config`
