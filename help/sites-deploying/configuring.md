---
title: Conceptos básicos de configuración
seo-title: Basic Configuration Concepts
description: AEM Obtenga información sobre cómo configurar los.
seo-description: Learn how to configure AEM.
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 2%

---

# Conceptos básicos de configuración{#basic-configuration-concepts}

Adobe Experience Manager AEM () se instala con la configuración predeterminada para todos los parámetros, lo que le permite ejecutarse de forma predeterminada. AEM Sin embargo, puede configurar los parámetros para sus propios requisitos específicos.

AEM Se pueden configurar muchos aspectos de la:

* Algunos son [se configura normalmente para cada instalación de proyecto](#primary-configuration-considerations) y deben revisarse para confirmar si son aplicables o no a su proyecto.
* [Configuraciones adicionales](#further-configuration-considerations) puede ser común aunque no imperativo; relacionado con las características o el rendimiento y la estabilidad del sistema.
* AEM Otras solo son necesarias para determinadas funciones opcionales de la (estas se documentan junto con la función adecuada).

Según la configuración específica, estos cambios se pueden realizar mediante las siguientes opciones:

* **Consola web de Adobe CQ**

   Esta es una ubicación estándar para configurar paquetes y servicios de OSGi.

   Consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y prácticas recomendadas.

* **Repositorio**

   Hay un subconjunto de configuraciones de OSGi disponibles en el repositorio. Esto garantiza que al copiar o replicar el contenido del repositorio se vuelvan a crear configuraciones idénticas. También puede agregar sus propias configuraciones, según el modo de ejecución, al repositorio.

   Consulte [Configuración de OSGi en el repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) y, en particular [Adición de una nueva configuración al repositorio](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) para obtener más información.

* **Sistema de archivos**

   Algunos archivos de configuración residen en el sistema de archivos.

* **WCM AEM**

   AEM Se pueden configurar varios aspectos dentro del propio WCM, muchos de los cuales utilizan el parámetro de configuración de la variable de configuración de la variable [Herramientas](/help/sites-administering/tools-consoles.md) consola; por ejemplo, agentes de replicación.

>[!NOTE]
>
>Al trabajar con Adobe Experience Manager, existen varios métodos para administrar los ajustes de configuración de los servicios OSGi (nodos de consola o de repositorio).
>
>Consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener información detallada.

>[!NOTE]
>
>AEM La configuración de la aplicación es sencilla, pero debe tener en cuenta lo siguiente:
>
>Ciertos cambios pueden tener un impacto importante en las aplicaciones. AEM Por este motivo, asegúrese de que tiene la experiencia y los conocimientos necesarios antes de empezar a configurar la configuración de la aplicación y realice solo los cambios que sepa que son necesarios. Cualquier cambio realizado a través de la consola OSGi es **inmediatamente** aplicado al sistema en ejecución (no es necesario reiniciar).

## Consideraciones de configuración principal {#primary-configuration-considerations}

Esta lista detalla las áreas principales que se configuran comúnmente para cada nuevo proyecto. No todos son necesarios, pero la lista debe leerse y revisarse para ver qué es aplicable a su proyecto.

La lista proporciona una breve descripción de cada aspecto de la configuración, junto con vínculos a las páginas que proporcionan detalles completos.

### Lista de comprobación de seguridad {#security-checklist}

En el archivo se enumeran varios problemas de configuración clave [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md). Asegúrese de leer esto y de realizar las acciones necesarias para la instalación.

### Configuración de la interfaz de usuario predeterminada: táctil o clásica {#configuring-the-default-ui-touch-optimized-or-classic}

AEM Hay dos interfaces de usuario disponibles para su uso en la:

* La IU táctil optimizada
* La IU clásica

Puede configurar la interfaz de usuario que necesite mediante [Asignación raíz](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>Encontrará más información sobre la selección de la interfaz de usuario en [Selección de la IU](/help/sites-authoring/select-ui.md).

### IPv4 e IPv6 {#ipv-and-ipv}

AEM Todos los elementos de la (por ejemplo, el repositorio, Dispatcher, etc.) se pueden instalar en redes IPv4 e IPv6.

El funcionamiento es fluido, ya que no se requiere ninguna configuración especial; cuando sea necesario, simplemente puede especificar una dirección IP utilizando el formato adecuado para su tipo de red.

Esto significa que cuando se necesita especificar una dirección IP, se puede seleccionar (según sea necesario) entre:

* una dirección IPv6

   por ejemplo `https://[ab12::34c5:6d7:8e90:1234]:4502`

* una dirección IPv4

   por ejemplo `https://123.1.1.4:4502`

* un nombre de servidor

   por ejemplo, `https://www.yourserver.com:4502`

* el caso predeterminado de `localhost` se interpretará para instalaciones de red IPv4 e IPv6

   por ejemplo, `http://localhost:4502`

### Depuración de versiones {#version-purging}

AEM En una instalación estándar, crea una nueva versión de una página o nodo cada vez que activa una página (después de actualizar el contenido). También puede crear versiones adicionales si lo solicita utilizando **Versiones** pestaña de la barra de tareas. Todas estas versiones se almacenan en el repositorio y se pueden restaurar si es necesario.

Estas versiones nunca se depuran, por lo que el tamaño del repositorio aumentará con el tiempo y, por lo tanto, debe administrarse.

Consulte [Depuración de versiones](/help/sites-deploying/version-purging.md) para obtener información detallada, en particular [Administrador de versiones](/help/sites-deploying/version-purging.md#version-manager) AEM para obtener más información sobre cómo configurar la depuración de versiones anteriores cuando se crea una versión nueva, haga lo siguiente:

### Registro {#logging}

AEM le ofrece la posibilidad de configurar lo siguiente:

* parámetros globales para el servicio de registro central
* registro de datos de solicitud; una configuración de registro especializada para solicitar información
* configuración específica para los servicios individuales; por ejemplo, un archivo de registro individual y formato para los mensajes de registro

Consulte [Registro](/help/sites-deploying/configure-logging.md) para obtener información detallada.

### Ejecutar modos {#run-modes}

AEM Los modos de ejecución permiten ajustar la instancia de la para un propósito específico; por ejemplo, crear o publicar, probar, desarrollar o intranet, etc.

Esto se realiza definiendo colecciones de parámetros de configuración para cada modo de ejecución. Se aplica un conjunto básico de parámetros de configuración para todos los modos de ejecución y, a continuación, puede ajustar conjuntos adicionales para el propósito de su entorno específico. A continuación, se aplican según sea necesario.

Todas las opciones de configuración se almacenan en el único repositorio y se activan estableciendo el **Modo de ejecución**.

Consulte [Modos de ejecución](/help/sites-deploying/configure-runmodes.md) para obtener información detallada.

### Inicio de sesión único {#single-sign-on}

Inicio de sesión único (SSO) permite a un usuario acceder a varios sistemas después de proporcionar credenciales de autenticación (como nombre de usuario y contraseña) una vez. Un sistema independiente (conocido como autenticador de confianza) realiza la autenticación y proporciona al Experience Manager las credenciales de usuario. El Experience Manager comprueba y aplica los permisos de acceso del usuario (es decir, determina a qué recursos puede acceder el usuario).

Consulte [Inicio de sesión único](/help/sites-deploying/single-sign-on.md) para obtener más información.

### Asignación de recursos {#resource-mapping}

AEM La asignación de recursos se utiliza para definir redirecciones, URL de vanidad y hosts virtuales para los usuarios de la red de distribución de recursos

Por ejemplo, puede utilizar estas asignaciones para lo siguiente:

* Agregue a todas las solicitudes el prefijo `/content` para que la estructura interna se oculte a los visitantes del sitio web.
* Defina una redirección para que todas las solicitudes a `/content/en/gateway` de su sitio web se redirigen a `https://gbiv.com/`.

Consulte [Asignación de recursos](/help/sites-deploying/resource-mapping.md) para obtener más información.

### Agentes de replicación, replicación inversa y replicación {#replication-reverse-replication-and-replication-agents}

AEM Los agentes de replicación son fundamentales para los, ya que el mecanismo utilizado para lo siguiente:

* [Publicar (activar)](/help/sites-authoring/publishing-pages.md) contenido de un autor a un entorno de publicación.
* Vaciar explícitamente contenido de la caché de Dispatcher.
* Devolver los datos introducidos por el usuario (por ejemplo, los datos de entrada de formulario) desde el entorno de publicación al entorno de creación (bajo el control del entorno de creación).

Para obtener más información, consulte [Replicación](/help/sites-deploying/replication.md).

### Ajustes de configuración de OSGi {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) AEM es un elemento fundamental en la pila tecnológica de los. AEM Se utiliza para controlar los paquetes compuestos de y su configuración de los paquetes de componentes de la interfaz de usuario de la interfaz de usuario de.

Consulte [Ajustes de configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obtener una lista de los distintos paquetes relevantes para la implementación del proyecto (enumerados según el paquete). AEM No es necesario ajustar todos los ajustes enumerados, algunos se mencionan para ayudarle a comprender cómo funciona la configuración de la lista de la manera en que funciona la.

AEM Al trabajar con los servicios de correo electrónico, existen varios métodos para administrar los parámetros de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

### Configuración de LDAP {#configuring-ldap}

Se requiere autenticación LDAP para autenticar a los usuarios almacenados en un directorio LDAP (central) como Active Directory. Esto ayuda a reducir el esfuerzo necesario para administrar las cuentas de usuario.

La autenticación LDAP se produce en el nivel del repositorio, por lo que el repositorio la gestiona directamente. Para obtener más información, consulte [AEM Configuración de LDAP con la](/help/sites-administering/ldap-config.md).

AEM Para obtener información sobre la administración de usuarios dentro de la administración de usuarios (incluida la asignación de derechos de acceso), consulte [Administración de usuarios y seguridad](/help/sites-administering/security.md).

### Configuración de Dispatcher {#configuring-the-dispatcher}

Dispatcher es una herramienta de equilibrio de carga o almacenamiento en caché de Adobe Experience Manager que se puede utilizar junto con un servidor web de clase empresarial.

Consulte [Dispatcher](https://helpx.adobe.com/es/experience-manager/dispatcher/using/dispatcher.html) para obtener información detallada, en particular [Configuración de Dispatcher](https://helpx.adobe.com/es/experience-manager/dispatcher/using/dispatcher-configuration.html) para obtener más información sobre la configuración.

### AEM Configuración del conector de LiveCycle {#configuring-aem-livecycle-connector}

AEM AEM Con el lanzamiento de los servicios de documentos de la y la seguridad de documentos de la, ahora tenemos la capacidad de invocar los servicios de documentos de la LiveCycle para procesar un formulario XFA, convertir un documento en PDF y proteger un documento mediante políticas. Por favor, lea [AEM Conector de LiveCycle de](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) para obtener más información.

### Administración de topologías y descarga de trabajos {#job-offloading-and-topology-administration}

[Descarga](/help/sites-deploying/offloading.md) distribuye las tareas de procesamiento entre las instancias de Experience Manager de una topología. Con la descarga, puede utilizar instancias de Experience Manager específicas para realizar tipos específicos de procesamiento. El procesamiento especializado le permite maximizar el uso de los recursos de servidor disponibles.

Las topologías son clústeres de Experience Manager de correspondencia imprecisa que participan en la descarga. Un clúster consta de una o más instancias de servidor de Experience Manager (una sola instancia se considera un clúster).

Para obtener más información sobre cómo ver o modificar la pertenencia a la topología, consulte la [Administración de topologías](/help/sites-deploying/offloading.md#administering-topologies) sección.

### Configuración de la consola de bienvenida {#configuring-the-welcome-console}

AEM La consola de Bienvenida de la IU clásica proporciona una lista de vínculos a las distintas consolas y funcionalidades de la interfaz de usuario de.

Es posible configurar los vínculos visibles; consulte [Configuración de la consola de bienvenida](/help/sites-developing/customizing-the-welcome-console.md) para obtener más información.

### Configurar para el rendimiento {#configuring-for-performance}

[Rendimiento](/help/sites-deploying/configuring-performance.md) es la clave de su proyecto. AEM Se pueden configurar ciertos aspectos de la (o del repositorio subyacente) para optimizar el rendimiento.

Consulte [Configurar para el rendimiento](/help/sites-deploying/configuring-performance.md#configuring-for-performance) para obtener más información.

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Almacén de datos compartidos {#shared-data-store}

El almacén de datos del repositorio se utiliza para descargar el almacenamiento de binarios grandes del repositorio en un área separada, de modo que varias instancias del mismo binario (una imagen, por ejemplo) dentro del árbol del repositorio se almacenen solo una vez.

Esta función &quot;almacenar una vez, hacer referencia varias veces&quot; se puede ampliar para que sirva no solo a un único árbol de repositorios, sino a repositorios completamente independientes, configurando el almacén de datos de cada uno para hacer referencia a la misma ubicación del sistema de archivos compartido.

Este almacén de datos se puede compartir entre diferentes nodos del mismo clúster, diferentes instancias de publicación o autor en la misma instalación o incluso instancias totalmente independientes en diferentes instalaciones.

Para obtener más información, consulte [Configuración de almacenes de datos y almacenes de nodos](/help/sites-deploying/data-store-config.md).

## Consideraciones de configuración adicionales {#further-configuration-considerations}

### Habilitar HTTP sobre SSL {#enabling-http-over-ssl}

Puede habilitar HTTP sobre SSL para utilizar conexiones más seguras con sus servidores.

Consulte [Habilitar HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obtener más información.

### AEM Portals y portlets de la red {#aem-portals-and-portlets}

Un portal es una aplicación web que proporciona personalización, inicio de sesión único, integración de contenido de diferentes fuentes y aloja la capa de presentación de los sistemas de información. El componente portlet también permite incrustar un portlet en la página. Para acceder al contenido proporcionado por el WCM CQ5, el servidor de portales puede equiparse con el portlet Director de portal CQ5. Para ello, instale, configure y agregue el portlet a la página del portal.

Consulte [Portal y portlets](/help/sites-administering/aem-as-portal.md) para obtener más información.

### Caducidad de objetos estáticos {#expiration-of-static-objects}

Los objetos estáticos (por ejemplo, los iconos) no cambian. Por lo tanto, el sistema debe configurarse para que no caduque (durante un periodo de tiempo razonable) y, por lo tanto, reducir el tráfico innecesario.

Consulte [Caducidad de objetos estáticos](/help/sites-deploying/expiration-static-objects.md) para obtener más información.

### Abrir archivos en el proceso de Java {#open-files-in-the-java-process}

Cada proceso java puede acceder a los archivos; esto requiere recursos del sistema. Por este motivo, se define un límite superior en cuanto a la cantidad de archivos a los que puede acceder cada proceso de forma simultánea. Si se supera este límite, puede producirse un error de excepción.

AEM Si el proceso de la supera este máximo, el mensaje &quot; `too many open files`&quot; se verá en `error.log`.

Para evitar estas excepciones, debe hacer lo siguiente:

1. AEM Compruebe cuántos archivos abiertos está usando su proceso de.

   La forma en que realice esta comprobación dependerá de la plataforma en la que se ejecute la instancia. Se pueden utilizar utilidades como lsof (Unix) o Process Explorer (Windows).

   Este valor debe controlarse durante el desarrollo y las pruebas para:

   * confirme que los archivos se cierran según sea necesario
   * para determinar el valor máximo necesario (en diversas circunstancias)

1. Defina el máximo permitido.

   El nuevo valor debe satisfacer tanto las necesidades actuales como los picos futuros, por lo que es aconsejable duplicar las necesidades actuales.

   De forma predeterminada, `serverctl` configura `CQ_MAX_OPEN_FILES` hasta `8192`; esto debería ser suficiente para la mayoría de los casos.

### Configuración del editor de texto enriquecido {#configuring-the-rich-text-editor}

El **Editor de texto enriquecido** (**RTE**) proporciona a los autores una amplia gama de [funcionalidad](/help/sites-authoring/rich-text-editor.md) para editar su contenido textual; proporcionándoles iconos, cuadros de selección y menús para una experiencia WYSIWYG.

Consulte [Configuración del editor de texto enriquecido](/help/sites-administering/rich-text-editor.md) para obtener más información.

### Configurar Deshacer para editar páginas {#configuring-undo-for-page-editing}

Existen varias propiedades que controlan el comportamiento de los comandos Deshacer y Rehacer para editar páginas. Se pueden configurar, consulte [Configurar Deshacer para editar páginas](/help/sites-administering/config-undo.md) para obtener más información.

### Configuración del componente de vídeo {#configuring-the-video-component}

El [Componente de vídeo](/help/sites-authoring/default-components-foundation.md#video) le permite colocar un elemento de vídeo predefinido y listo para usar en la página.

Para que se dé una transcodificación adecuada, su administrador debe [instalar FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) de manera separada. También pueden [Configurar los perfiles de vídeo](/help/sites-administering/config-video.md#configure-video-profiles) para su uso con elementos html5.

### Configuración y personalización de informes {#configuring-and-customizing-reports}

Para ayudarle a monitorizar y analizar el estado de su instancia, CQ proporciona una selección de informes predeterminados, que se pueden configurar para sus necesidades individuales:

Consulte la [Conceptos básicos de personalización de informes](/help/sites-administering/reporting.md#the-basics-of-report-customization) para obtener más información.

### Configuración de notificaciones por correo electrónico {#configuring-email-notification}

CQ envía notificaciones por correo electrónico a los usuarios que:

* Se han suscrito a eventos de página como, por ejemplo, una modificación o replicación.
* Se ha suscrito a eventos de foro.
* Deben realizar un paso en un flujo de trabajo.

Consulte [Configuración de notificaciones por correo electrónico](/help/sites-administering/notification.md) para obtener más información.

### Habilitando impresiones de página {#enabling-page-impressions}

Las impresiones de página se muestran en la **Impresiones** de la consola siteadmin de la IU clásica. Para habilitar la captura de impresiones de página, debe configurar lo siguiente:

* En la instancia de publicación:

   * [Estadísticas de página de CQ WCM de día](/help/sites-deploying/osgi-configuration-settings.md)

* En la instancia de autor:

   * [Seguimiento de impresiones de página Adobe](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>La configuración del Rastreador de impresiones de páginas de Adobe en el entorno de creación permitirá solicitudes anónimas al servicio de seguimiento.
