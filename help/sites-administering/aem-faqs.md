---
title: AEM Preguntas más frecuentess
description: AEM Utilice estas preguntas frecuentes para comprender, configurar y solucionar problemas o flujos de trabajo comunes en los flujos de trabajo de.
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: 0aa929021aa724e4ec18d49fea26f8c0b0538bdc
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---

# AEM Preguntas más frecuentess {#aem-faqs}

AEM Conozca las respuestas a algunos problemas de solución de problemas y configuración de la.

## Sites {#sites}

### ¿Cómo configuro la distribución sin binarios? {#how-do-i-configure-binary-less-distribution}

La distribución sin binarios es compatible con implementaciones en un almacén de datos compartido e implica a agentes que utilizan el exportador de paquetes de distribución basado en Vault (PID de fábrica: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`) generador de paquetes.

Con el modo sin binarios habilitado, los paquetes de contenido distribuidos contienen referencias a binarios en lugar de a los binarios reales.

#### ¿Cómo habilito la distribución sin binarios? {#how-do-i-enable-binary-less-distribution}

Para habilitar la distribución sin binarios, implemente con un almacén de blobs compartido.
Compruebe la `useBinaryReferences` en la configuración de OSGI con el PID de fábrica ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* que está utilizando su agente.

#### AEM ¿Cómo se habilitan los permisos al crear una copia de idioma para autores de contenido en la creación de? {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

Para crear la función de copia de idioma, los autores de contenido necesitan permisos en `/content/projects` ubicación.

Si uno requiere que los autores administren también proyectos, la solución es agregar al autor a `projects-administrators` grupo.

#### ¿Cómo cambiar el formato al crear una copia de idioma para un proyecto? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

Cree una raíz de idioma y una copia de idioma dentro de la raíz antes de crear un proyecto de traducción.

Por ejemplo, cree una raíz de idioma en `/content/geometrixx` con nombre como `fr_LU` (y título en francés (Luxemburgo)). A continuación, cree una copia de idioma de la página desde el panel Referencias y navegue hasta `Create structure only` opción en `Create & Translate`. Finalmente, cree un proyecto de traducción y luego añada la copia de idioma al trabajo de traducción.

Para obtener más información, consulte los recursos adicionales a continuación:

* [Preparación de contenido para su traducción](/help/sites-administering/tc-prep.md)
* [Administración de proyectos de traducción](/help/sites-administering/tc-manage.md)

#### AEM ¿Cómo se auditan las capacidades de la, como los intentos de inicio de sesión y los cambios de ACL o de permisos? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM ha introducido la capacidad de registrar cambios administrativos para mejorar la resolución de problemas y la auditoría. De forma predeterminada, la información se registra en `error.log` archivo. Para facilitar la monitorización, se recomienda redirigirlos a un archivo de registro independiente.
Para redirigir el resultado a un archivo de registro independiente, consulte [AEM Cómo auditar las operaciones de administración de usuarios en el](/help/sites-administering/audit-user-management-operations.md).

#### ¿Cómo se habilita SSL de forma predeterminada? {#how-to-enable-ssl-by-default}

Adobe Experience Manager AEM () 6.4 se envía con el asistente SSL y ofrece una interfaz de usuario para configurar el soporte SSL de Jetty y Granite Jetty.

Para habilitar SSL de forma predeterminada, consulte [SSL de forma predeterminada](/help/sites-administering/ssl-by-default.md).

#### AEM ¿Cuál es la arquitectura recomendada al utilizar los servicios de contenido de la aplicación móvil, idealmente React Native? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

AEM Los servicios de contenido se basan en los modelos Sling, y los desarrolladores de deben proporcionar un pojo de modelo Sling para cada componente exportado.

AEM Para obtener información sobre cómo consumir servicios de contenido desde una aplicación de React, consulte [AEM Introducción a los servicios de contenido de](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) tutorial.

Además, si los desarrolladores desean exportar un árbol de componentes, también pueden implementar el `ComponentExporter` y `ContainerExporter` y utilice la variable `ModelFactory` para iterar en los componentes secundarios y devolver la representación del modelo. Consulte los siguientes recursos:

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :: Modelos Sling](https://sling.apache.org/documentation/bundles/models.html)

#### AEM ¿Cómo deshabilitar la ventana emergente de la encuesta de 6.4? {#how-to-disable-aem-survey-pop-up}

Puede optar por recopilar estadísticas de uso mediante la interfaz de usuario táctil o la consola web. Para obtener instrucciones detalladas, consulte [Inclusión en la recopilación de estadísticas de uso agregadas](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### AEM ¿Existe un buen recurso que destaque las características clave para actualizar a la versión 6.4 de la versión de la aplicación de la versión de? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Consulte [AEM Explicación de los motivos para actualizar el](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) en se describe un desglose de alto nivel de las funciones clave para los clientes que se plantean actualizar a la versión más reciente de Adobe Experience Manager.

## Assets {#assets}

### ¿Por qué el flujo de trabajo de Assets se repite al cargar archivos MP4 (por ejemplo, mediante el método de arrastrar y soltar)? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

Si el usuario que carga los archivos de película no tiene permisos de eliminación en el nodo de recursos, se produce un error en la eliminación de nodos de fragmentos y se reinicia la carga.

#### ¿Cuáles son los ajustes predeterminados para las configuraciones predeterminadas al crear la copia de idioma? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

Cuando crea una copia de idioma mediante la IU táctil (**Referencias** > **Actualizar copia de idioma**), se crea una nueva carpeta DAM en el nuevo idioma y se hace referencia a los recursos desde allí.

Esta es la configuración predeterminada para las configuraciones listas para usarse. Puede establecer **Traducir recursos de la página** = **No traducir** en Configuraciones de traducción.
AEM Para la versión 6.4, **Herramientas** > **Cloud Service** > **Servicios de nube de traducción**.

#### AEM AEM AEM ¿Cómo desactivar un componente de la que causa un crecimiento exponencial para la tienda de segmentos de la (6.3.1.1)? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

Puede deshabilitar el desactivador de componentes OSGi. Para utilizar este servicio, consulte [Desactivador del componente OSGi](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

Como solución alternativa, también puede deshabilitar manualmente el componente a través de la interfaz de usuario o a través de un `curl` AEM (ejemplo abajo), después de cada reinicio de la sesión de la sesión de la.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### ¿Cómo personalizar Admin Consoles? {#how-to-customize-admin-consoles}

AEM proporciona varios mecanismos para permitirle personalizar las consolas y la funcionalidad de creación de páginas de la instancia de creación. Para obtener información sobre cómo crear una consola personalizada y personalizar una vista predeterminada para una consola, consulte [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md).

#### ¿Cuál es la diferencia entre los componentes basados en CoralUI 2 y CoralUI 3? {#what-is-the-difference-between-coralui-and-coralui-based-components}

Se crea un nuevo conjunto de componentes Sling de Granite UI Foundation para Coral3 y se encuentra en [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) Hay un conjunto para los componentes basados en CoralUI 2 y un conjunto para los basados en CoralUI 3. El nuevo conjunto no será solo una copia y pegado del conjunto antiguo, sino que se limpiará (por ejemplo, optimizando, eliminando la función obsoleta). Por lo tanto, se recomienda que una página solo utilice un conjunto basado en CoralUI 3 o en CoralUI 2.

Para obtener más información, consulte [Guía de migración para CoralUI basado en 3](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### ¿Cómo se personaliza el componente de búsqueda en AEM Assets? {#how-to-customize-the-search-component-in-aem-assets}

Para obtener más información sobre el aumento/clasificación de la búsqueda y la implementación, consulte [Guía de implementación de búsqueda simple](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

AEM La implementación de búsqueda simple es el material del laboratorio de Summit 2017 Búsqueda Desmitificada.

#### ¿Es posible crear un plugin para WordPress que permita a un cliente acceder al Selector de recursos de Adobe para seleccionar imágenes? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

Sí, un cliente que utiliza WordPress puede utilizar el Selector de recursos de Adobe para seleccionar imágenes de su servidor de AEM Assets para añadirlas a las publicaciones en su sitio de WordPress.

Consulte [Selector de recursos](../assets/search-assets.md#assetpicker) para obtener más información.
