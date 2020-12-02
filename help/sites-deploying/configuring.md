---
title: Conceptos básicos de configuración
seo-title: Conceptos básicos de configuración
description: Obtenga información sobre cómo configurar AEM.
seo-description: Obtenga información sobre cómo configurar AEM.
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
translation-type: tm+mt
source-git-commit: 8f35717324cd2c1524fb2cf931b3ce21be05729a
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 1%

---


# Conceptos básicos de configuración{#basic-configuration-concepts}

Adobe Experience Manager (AEM) se instala con la configuración predeterminada de todos los parámetros, lo que le permite ejecutarse &quot;sin conexión&quot;. Sin embargo, puede configurar AEM para sus propios requisitos específicos.

Hay muchos aspectos de AEM que se pueden configurar:

* Algunos [se configuran comúnmente para cada instalación del proyecto](#primary-configuration-considerations) y deben revisarse para confirmar si son aplicables o no al proyecto.
* [Es posible que ](#further-configuration-considerations) las configuraciones adicionales sean comunes, aunque no imperativas; relacionadas con las funciones o el rendimiento y la estabilidad del sistema.
* Otras solo son necesarias para ciertas características opcionales de AEM (se documentan junto con la característica adecuada).

Según la configuración específica, estos cambios se pueden realizar mediante:

* **Adobe CQ Web Console**

   Es una ubicación estándar para configurar paquetes y servicios OSGi.

   Consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más detalles y prácticas recomendadas.

* **Repositorio**

   Hay un subconjunto de configuraciones de OSGi disponibles en el repositorio. Esto garantiza que al copiar o replicar el contenido del repositorio se vuelvan a crear configuraciones idénticas. También puede agregar sus propias configuraciones, según el modo de ejecución, al repositorio.

   Consulte [Configuración de OSGi en el Repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) y en particular [Añadir una nueva configuración al Repositorio](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) para obtener más detalles.

* **Sistema de archivos**

   Algunos archivos de configuración residen en el sistema de archivos.

* **WCM AEM**

   Se pueden configurar varios aspectos dentro AEM propio WCM, muchos de los cuales utilizan la consola [Tools](/help/sites-administering/tools-consoles.md); por ejemplo, agentes de replicación.

>[!NOTE]
>
>Al trabajar con Adobe Experience Manager, existen varios métodos para administrar la configuración de los servicios OSGi (nodos de consola o repositorio).
>
>Consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información.

>[!NOTE]
>
>La configuración de AEM es sencilla, pero debe tener en cuenta que:
>
>Algunos cambios pueden tener un impacto importante en las aplicaciones. Por este motivo, asegúrese de que tiene la experiencia y los conocimientos necesarios antes del inicio para configurar AEM y realizar únicamente los cambios que sabe que son necesarios. Cualquier cambio realizado a través de la consola OSGi se **inmediatamente** aplica al sistema en ejecución (no se requiere reinicio).

## Consideraciones de configuración principal {#primary-configuration-considerations}

Esta lista detalla las áreas principales que se configuran comúnmente para cada nuevo proyecto. No todos son necesarios, pero la lista debe leerse y revisarse para ver qué es lo que se aplica a su proyecto.

La lista ofrece una breve descripción general de cada aspecto de la configuración, junto con vínculos a las páginas que proporcionan detalles completos.

### Lista de comprobación de seguridad {#security-checklist}

En la [lista de comprobación de seguridad](/help/sites-administering/security-checklist.md) se enumeran varios problemas de configuración clave. Asegúrese de leer esto y de tomar las medidas necesarias para la instalación.

### Configuración de la IU predeterminada: táctil optimizada o clásica {#configuring-the-default-ui-touch-optimized-or-classic}

Hay dos IU disponibles para su uso en AEM:

* La IU táctil
* La IU clásica

Puede configurar la IU que necesita mediante [Asignación de raíz](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>Encontrará más información sobre la selección de la IU en [Selección de la IU](/help/sites-authoring/select-ui.md).

### IPv4 e IPv6 {#ipv-and-ipv}

Todos los elementos de AEM (por ejemplo, el repositorio, el despachante, etc.) se pueden instalar en redes IPv4 e IPv6.

La operación es fluida ya que no se requiere ninguna configuración especial, cuando sea necesario puede especificar una dirección IP con el formato adecuado para el tipo de red.

Esto significa que cuando se necesita especificar una dirección IP, puede seleccionar (según sea necesario) de:

* una dirección IPv6

   por ejemplo `https://[ab12::34c5:6d7:8e90:1234]:4502`

* una dirección IPv4

   por ejemplo `https://123.1.1.4:4502`

* un nombre de servidor

   por ejemplo, `https://www.yourserver.com:4502`

* el caso predeterminado de `localhost` se interpretará para las instalaciones de red IPv4 e IPv6

   por ejemplo, `http://localhost:4502`

### Depuración de versiones {#version-purging}

En una instalación estándar, AEM crea una nueva versión de una página o nodo cada vez que activa una página (después de actualizar el contenido).También puede crear versiones adicionales si así se solicita mediante la ficha **Versioning** de la barra de tareas. Todas estas versiones se almacenan en el repositorio y se pueden restaurar si es necesario.

Estas versiones nunca se depuran, por lo que el tamaño del repositorio crecerá con el tiempo y, por lo tanto, es necesario administrarlo.

Consulte [Depuración de versiones](/help/sites-deploying/version-purging.md) para obtener más información, en particular [Administrador de versiones](/help/sites-deploying/version-purging.md#version-manager), para obtener más información sobre cómo configurar AEM para depurar versiones anteriores cuando se crea una nueva versión.

### Registro {#logging}

AEM le ofrece la posibilidad de configurar:

* parámetros globales para el servicio de registro central
* registro de datos de solicitud; una configuración de registro especializada para información de solicitud
* ajustes específicos para los servicios individuales; por ejemplo, un archivo de registro y un formato individuales para los mensajes de registro

Consulte [Registro](/help/sites-deploying/configure-logging.md) para obtener más información.

### Ejecutar modos {#run-modes}

Los modos de ejecución le permiten ajustar la instancia de AEM para un fin específico; por ejemplo, creación o publicación, prueba, desarrollo o intranet, etc.

Esto se realiza definiendo colecciones de parámetros de configuración para cada modo de ejecución. Se aplica un conjunto básico de parámetros de configuración para todos los modos de ejecución, puede ajustar conjuntos adicionales según el propósito del entorno específico. A continuación, se aplican según sea necesario.

Todas las opciones de configuración se almacenan en el único repositorio y se activan configurando el **Modo de ejecución**.

Consulte [Run Modes](/help/sites-deploying/configure-runmodes.md) para obtener más información.

### Inicio de sesión único {#single-sign-on}

El inicio de sesión único (SSO) permite al usuario acceder a varios sistemas después de proporcionar credenciales de autenticación (como un nombre de usuario y una contraseña) una vez. Un sistema independiente (conocido como autenticador de confianza) realiza la autenticación y proporciona al Experience Manager las credenciales de usuario. El Experience Manager comprueba y aplica los permisos de acceso para el usuario (es decir, determina a qué recursos se le permite acceder).

Consulte [Inicio de sesión único](/help/sites-deploying/single-sign-on.md) para obtener más información.

### Asignación de recursos {#resource-mapping}

La asignación de recursos se utiliza para definir redirecciones, direcciones URL personales y hosts virtuales para AEM.

Por ejemplo, puede utilizar estas asignaciones para:

* Pruebe todas las solicitudes con `/content` para que la estructura interna se oculte de los visitantes del sitio web.
* Defina un redireccionamiento para que todas las solicitudes a la página `/content/en/gateway` del sitio Web se redirijan a `https://gbiv.com/`.

Consulte [Asignación de recursos](/help/sites-deploying/resource-mapping.md) para obtener más detalles.

### Agentes de replicación, replicación inversa y replicación {#replication-reverse-replication-and-replication-agents}

Los agentes de replicación son fundamentales para AEM como mecanismo utilizado para:

* [Publique (active)](/help/sites-authoring/publishing-pages.md) contenido de un autor en un entorno de publicación.
* Borre contenido explícitamente de la caché de Dispatcher.
* Devolver los datos introducidos por el usuario (por ejemplo, los datos introducidos en el formulario) desde el entorno de publicación al entorno de creación (bajo el control del entorno de creación).

Para obtener más información, consulte [Replicación](/help/sites-deploying/replication.md).

### Configuración de OSGi {#osgi-configuration-settings}

[](https://www.osgi.org/) OSGi es un elemento fundamental en la pila de AEM de tecnología. Se utiliza para controlar los paquetes compuestos de AEM y su configuración.

Consulte [Configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obtener una lista de los distintos paquetes que son relevantes para la implementación del proyecto (enumerados según el paquete). No es necesario realizar ajustes en todos los ajustes de la lista; algunos se mencionan para ayudarle a comprender el funcionamiento de AEM.

Al trabajar con AEM existen varios métodos para gestionar los parámetros de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más detalles y las prácticas recomendadas.

### Configuración de LDAP {#configuring-ldap}

La autenticación LDAP es necesaria para autenticar usuarios almacenados en un directorio LDAP (central) como Active Directory. Esto ayuda a reducir el esfuerzo necesario para administrar las cuentas de usuario.

La autenticación LDAP se produce en el nivel de repositorio, por lo que la gestiona directamente el repositorio. Para obtener más información, consulte [Configuración de LDAP con AEM](/help/sites-administering/ldap-config.md).

Para la administración de usuarios dentro de AEM (incluida la asignación de derechos de acceso), consulte [Administración de usuarios y seguridad](/help/sites-administering/security.md).

### Configuración del despachante {#configuring-the-dispatcher}

Dispatcher es una herramienta de almacenamiento en caché y/o equilibrio de carga de Adobe Experience Manager que se puede utilizar junto con un servidor web de clase empresarial.

Consulte [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) para obtener más detalles, en particular [Configuración del despachante](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) para obtener más detalles sobre la configuración.

### Configuración de AEM conector de LiveCycle {#configuring-aem-livecycle-connector}

Con el lanzamiento de AEM Doc Services y AEM Doc Security, ahora podemos invocar los servicios de documentación de LiveCycle para procesar un formulario XFA, convertir un documento a PDF y proteger un documento mediante políticas. Lea [Conector de LiveCycle de AEM](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) para obtener más detalles.

### Descarga de trabajo y administración de topología {#job-offloading-and-topology-administration}

[](/help/sites-deploying/offloading.md) Desfloadingdistribuye tareas de procesamiento entre instancias de Experience Manager en una topología. Con la descarga, puede utilizar instancias de Experience Manager específicas para realizar tipos de procesamiento específicos. El procesamiento especializado le permite maximizar el uso de los recursos de servidor disponibles.

Las topologías son clústeres de Experience Manager acoplados de forma laxa que participan en la descarga. Un clúster consta de una o varias instancias de servidor Experience Manager (una sola instancia se considera un clúster).

Para obtener más información sobre cómo vista o modificación de la pertenencia a la topología, consulte la sección [Administración de topologías](/help/sites-deploying/offloading.md#administering-topologies).

### Configuración de la consola de bienvenida {#configuring-the-welcome-console}

La consola de bienvenida de la IU clásica proporciona una lista de vínculos a las distintas consolas y funcionalidades de AEM.

Es posible configurar los vínculos visibles, consulte [Configuración de la consola de bienvenida](/help/sites-developing/customizing-the-welcome-console.md) para obtener más detalles.

### Configuración para el rendimiento {#configuring-for-performance}

[El ](/help/sites-deploying/configuring-performance.md) rendimiento es clave para el proyecto. Determinados aspectos de AEM (y/o del repositorio subyacente) se pueden configurar para optimizar el rendimiento.

Consulte [Configuración para el rendimiento](/help/sites-deploying/configuring-performance.md#configuring-for-performance) para obtener más detalles.

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Almacén de datos compartido {#shared-data-store}

El almacén de datos del repositorio se utiliza para descargar el almacenamiento de grandes binarios del repositorio en sí a un área separada, de modo que las instancias múltiples del mismo binario (por ejemplo, una imagen) dentro del árbol del repositorio se almacenen sólo una vez.

Esta función &quot;store-once, reference-many-times&quot; se puede ampliar para que sirva no sólo un único árbol de repositorio sino también repositorios completamente separados, configurando el almacén de datos de cada uno para que haga referencia a la misma ubicación del sistema de archivos compartido.

Este almacén de datos se puede compartir entre diferentes nodos del mismo clúster, distintas instancias de publicación o autor en la misma instalación, o incluso instancias totalmente independientes en diferentes instalaciones.

Para obtener más información, consulte [Configuración de almacenes de datos y almacenes de nodos](/help/sites-deploying/data-store-config.md).

## Más consideraciones sobre la configuración {#further-configuration-considerations}

### Habilitación de HTTP sobre SSL {#enabling-http-over-ssl}

Puede habilitar HTTP sobre SSL para utilizar conexiones más seguras con sus servidores.

Consulte [Habilitación de HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obtener más detalles.

### Portlets y portlets AEM {#aem-portals-and-portlets}

Un portal es una aplicación web que proporciona personalización, inicio de sesión único, integración de contenido de diferentes fuentes y aloja la capa de presentación de los sistemas de información. El componente portlet también permite incrustar un portlet en la página. Para acceder al contenido proporcionado por CQ5 WCM, el servidor de portal puede estar equipado con el portlet Director de CQ5 Portal. Para ello, instale, configure y agregue el portlet a la página del portal.

Consulte [Portal y portlets](/help/sites-administering/aem-as-portal.md) para obtener más detalles.

### Caducidad de objetos estáticos {#expiration-of-static-objects}

Los objetos estáticos (por ejemplo, iconos) no cambian. Por lo tanto, el sistema debe configurarse de modo que no caduque (durante un período de tiempo razonable) y se reduzca así el tráfico innecesario.

Consulte [Caducidad de objetos estáticos](/help/sites-deploying/expiration-static-objects.md) para obtener más detalles.

### Abrir archivos en el proceso Java {#open-files-in-the-java-process}

Cada proceso de Java puede acceder a los archivos, lo que requiere recursos del sistema. Por este motivo, se define un límite superior en cuanto a la cantidad de archivos a los que se permite el acceso simultáneo a cada proceso. Si se supera, puede producirse un error de excepción.

Si el proceso de AEM supera este máximo, el mensaje &quot; `too many open files`&quot; se verá en `error.log`.

Para evitar estas excepciones debe:

1. Compruebe cuántos archivos abiertos está utilizando el proceso de AEM.

   La forma en que realice esta comprobación dependerá de la plataforma en la que se ejecute la instancia. Se pueden utilizar utilidades como lsof (Unix) o Process Explorer (Windows).

   Este valor debe supervisarse durante el desarrollo y la realización de pruebas para:

   * confirmar que los archivos se están cerrando según sea necesario
   * para determinar el valor máximo necesario (en diversas circunstancias)

1. Establezca el máximo permitido.

   El nuevo valor debería atender tanto a las necesidades actuales como a los picos futuros, por lo que es aconsejable hacer un doble de las necesidades actuales.

   De forma predeterminada, `serverctl` configura `CQ_MAX_OPEN_FILES` en `8192`; esto debería ser suficiente para la mayoría de los escenarios.

### Configuración del editor de texto enriquecido {#configuring-the-rich-text-editor}

El **Editor de texto enriquecido** (**RTE**) proporciona a los autores una amplia gama de [funcionalidades](/help/sites-authoring/rich-text-editor.md) para editar su contenido textual; proporcionarles iconos, cuadros de selección y menús para una experiencia WYSIWYG.

Consulte [Configuración del editor de texto enriquecido](/help/sites-administering/rich-text-editor.md) para obtener más información.

### Configuración de Deshacer para la edición de páginas {#configuring-undo-for-page-editing}

Existen varias propiedades que controlan el comportamiento de los comandos deshacer y rehacer para editar páginas. Pueden configurarse en [Configuración de Deshacer para edición de página](/help/sites-administering/config-undo.md) para obtener más detalles.

### Configuración del componente de vídeo {#configuring-the-video-component}

El [componente de vídeo](/help/sites-authoring/default-components-foundation.md#video) permite colocar un elemento de vídeo predefinido y listo para usar en la página.

Para que se dé una transcodificación adecuada, su administrador debe [instalar FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) de manera separada. También pueden [configurar sus Perfiles de vídeo](/help/sites-administering/config-video.md#configure-video-profiles) para utilizarlos con elementos HTML5.

### Configuración y personalización de informes {#configuring-and-customizing-reports}

Para ayudarle a monitorear y analizar el estado de su instancia, CQ proporciona una selección de informes predeterminados, que se pueden configurar según sus necesidades individuales:

Consulte los [conceptos básicos de personalización de informes](/help/sites-administering/reporting.md#the-basics-of-report-customization) para obtener más detalles.

### Configuración de la notificación por correo electrónico {#configuring-email-notification}

CQ envía notificaciones por correo electrónico a los usuarios que:

* Se han suscrito a eventos de página, por ejemplo, modificación o replicación.
* Se han suscrito a los eventos del foro.
* Debe realizar un paso en un flujo de trabajo.

Consulte [Configuración de la notificación por correo electrónico](/help/sites-administering/notification.md) para obtener más detalles.

### Activación de impresiones de página {#enabling-page-impressions}

Las impresiones de página se muestran en la columna **Impresiones** de la consola clásica siteadmin de la IU. Para habilitar la captura de impresiones de página, debe configurar:

* En la instancia de publicación:

   * [Estadísticas de página de CQ WCM de día](/help/sites-deploying/osgi-configuration-settings.md)

* En la instancia de creación:

   * [Seguimiento de impresiones de página de Adobe](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>La configuración del Rastreador de impresiones de página de Adobe en el entorno de creación permitirá solicitudes anónimas al servicio de seguimiento.

