---
title: Preguntas más frecuentes AEM
seo-title: AEM 6.4 preguntas más frecuentes
description: Utilice estas preguntas más frecuentes para comprender, configurar y solucionar problemas o flujos de trabajo comunes en AEM.
seo-description: Utilice estas preguntas más frecuentes para comprender, configurar y solucionar problemas o flujos de trabajo comunes en AEM.
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 0%

---


# Preguntas más frecuentes sobre AEM {#aem-faqs}

Conozca las respuestas a algunos problemas AEM de resolución de problemas y configuración.

## Sites {#sites}

### ¿Cómo configuro la distribución sin binarios? {#how-do-i-configure-binary-less-distribution}

La distribución sin binarios es compatible con implementaciones en un almacén de datos compartido e incluye agentes que aprovechan el exportador de paquetes de distribución basado en Vault (PID de fábrica: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`) generador de paquetes.

Con el modo sin binarios habilitado, los paquetes de contenido distribuidos contienen referencias a binarios en lugar de a los binarios reales.

#### ¿Cómo habilito la distribución sin binarios? {#how-do-i-enable-binary-less-distribution}

Para habilitar la distribución sin binarios, implemente con un almacén de blob compartido.
Compruebe la propiedad `useBinaryReferences` en la configuración OSGI con el PID de fábrica ( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* que utiliza su agente.

#### ¿Cómo puedo personalizar los mensajes de error al navegar por la jerarquía de páginas en AEM consola Sitios? {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

Compruebe el panel Red (del navegador Chrome) donde haya una configuración personal (JS no se ha minimizado).

Vista la columna `Initiator` para determinar el iniciador de una solicitud. Proporciona los archivos y los números de línea desde donde se realizan las llamadas de AJAX. Posteriormente, puede rastrear la función de gestión de errores y cambiar el mensaje de error según sus necesidades.

#### ¿Cómo habilitar permisos al crear una copia de idioma para autores de contenido en AEM? {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

Para crear la función de copia de idioma, los autores de contenido necesitan permisos en la ubicación `/content/projects`.

Si se requiere que los autores también administren proyectos, la solución consiste en agregar el autor al grupo `project-administrators`.

#### ¿Cómo cambiar el formato al crear una copia de idioma para un proyecto? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

Cree una raíz de idioma y una copia de idioma dentro de la raíz, antes de crear un proyecto de traducción.

Por ejemplo,
Cree una raíz de idioma en `/content/geometrixx` con el nombre `fr_LU` (y el título como francés (Luxemburgo)). Posteriormente, cree una copia de idioma de la página desde el panel de referencias y vaya a la opción `Create structure only` en `Create & Translate`. Finalmente, cree un proyecto de traducción y luego agregue la copia de idioma al trabajo de traducción.

Para obtener más información, consulte los recursos adicionales siguientes:

* [Preparación del contenido para la traducción](/help/sites-administering/tc-prep.md)
* [Administración de proyectos de traducción](/help/sites-administering/tc-manage.md)

#### ¿Cómo auditar las capacidades de AEM como, por ejemplo, los intentos de inicio de sesión y los cambios de ACL o permisos? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM ha introducido la capacidad de registrar cambios administrativos para mejorar la resolución de problemas y la auditoría. De forma predeterminada, la información se registra en el archivo `error.log`. Para facilitar la supervisión, se recomienda que se redirijan a un archivo de registro independiente.
Para redirigir el resultado a un archivo de registro independiente, consulte [Cómo auditar las operaciones de administración de usuarios en AEM](/help/sites-administering/audit-user-management-operations.md).

#### ¿Cómo habilitar SSL de forma predeterminada? {#how-to-enable-ssl-by-default}

Adobe Experience Manager (AEM) 6.4 se suministra con el asistente SSL y oferta una interfaz de usuario para configurar la compatibilidad con SSL de Jetty y Granite Jetty.

Para habilitar SSL de forma predeterminada, consulte [SSL de forma predeterminada](/help/sites-administering/ssl-by-default.md).

#### ¿Cuál es la arquitectura recomendada al utilizar los servicios de contenido de AEM desde una aplicación móvil, idealmente Reaccionar nativo? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

Los servicios de contenido se basan en los modelos de Sling y los desarrolladores de AEM deben proporcionar un pojo de modelo de Sling para cada componente exportado.

Para comprender cómo utilizar AEM servicios de contenido desde una aplicación React, consulte el tutorial [Introducción a AEM Content Services](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html).

Además, si los desarrolladores desean exportar un árbol de componentes, también pueden implementar las interfaces `ComponentExporter` y `ContainerExporter`, así como utilizar `ModelFactory` para iterar sobre los componentes secundarios y devolver su representación de modelo. Consulte los recursos siguientes:

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :: Modelos Sling](https://sling.apache.org/documentation/bundles/models.html)

#### ¿Cómo desactivar AEM ventana emergente de encuesta 6.4? {#how-to-disable-aem-survey-pop-up}

Puede optar por la recopilación de estadísticas de uso mediante la IU táctil o la consola web. Para obtener instrucciones detalladas, consulte [Opción de recopilación de estadísticas de uso agregadas](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### ¿Existe un buen recurso que destaca las características clave para la actualización a AEM 6.4? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

Consulte [Explicación de las razones para actualizar AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) que describe el desglose de alto nivel de las características clave para los clientes que están considerando actualizar a la versión más reciente de Adobe Experience Manager.

## Assets {#assets}

### ¿Por qué se repite el flujo de trabajo de Recursos al cargar archivos MP4 (por ejemplo, mediante el método de arrastrar y soltar)? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

Si el usuario no dispone de permisos de eliminación en el nodo de recursos para cargar los archivos de película, los nodos de fragmentos de eliminación fallan y se reinicia la carga.

#### ¿Cuál es el número máximo de recursos digitales que se pueden utilizar con AEM 6.4 a la vez? {#what-is-the-maximum-number-of-digital-assets-that-can-be-operated-with-aem-at-a-time}

Adobe Experience Manager (AEM) 6.5 permite cargar hasta 2 GB de recursos a la vez.

Para obtener información adicional sobre el número máximo de recursos que se pueden utilizar con AEM 6.5, consulte [Guía de tamaño de recursos](/help/assets/assets-sizing-guide.md).

#### ¿Cuál es la configuración predeterminada para las configuraciones de OOTB al crear una copia de idioma? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

Al crear copias de idioma mediante la IU clásica, los recursos no se mueven bajo la nueva jerarquía de idioma, sino que se utilizan desde el maestro de idioma.

Mientras que, al crear una copia de idioma mediante la IU táctil (**Referencias** -> **Actualizar copia de idioma**), se crea una nueva carpeta DAM en el nuevo idioma y se hace referencia a los recursos desde allí.

Esta es la configuración predeterminada para las configuraciones de OOTB. Puede establecer **Traducir recursos de página** = **No traducir** en configuraciones de traducción.
Para AEM 6.4, **Herramientas** > **Cloud Services** > **Servicios de nube de traducción**.

#### ¿Cómo deshabilitar un componente AEM que causa crecimiento exponencial para el AEM SegmentStore (AEM 6.3.1.1)? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

Puede desactivar el activador de componentes OSGi. Para utilizar este servicio, consulte [Activador de componentes OSGi](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

Como solución alternativa, también puede deshabilitar manualmente el componente mediante la interfaz de usuario o mediante un comando `curl` (ejemplo más abajo), después de cada reinicio AEM.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### ¿Cómo configurar las perspectivas de recursos con AEM instancia 6.5? {#how-to-configure-asset-insights-with-aem-instance}

Para configurar y configurar Asset Insights para Experience Manager implementado mediante Activación de Adobe (DTM), consulte cómo [Configurar Asset Insights con AEM Assets](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

#### ¿Cómo personalizar las consolas de administración? {#how-to-customize-admin-consoles}

AEM proporciona varios mecanismos que le permiten personalizar las consolas y la funcionalidad de creación de páginas de la instancia de creación. Para obtener información sobre cómo crear una consola personalizada y personalizar una vista predeterminada para una consola, consulte [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md).

#### ¿Cuál es la diferencia entre los componentes basados en CoralUI 2 y CoralUI 3? {#what-is-the-difference-between-coralui-and-coralui-based-components}

Se crea un nuevo conjunto de componentes Sling de Granite UI Foundation para Coral3 y se encuentra en [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) Hay un conjunto para los componentes basados en CoralUI 2 y otro para los componentes basados en CoralUI 3. El nuevo conjunto no será sólo una copia y pegado del conjunto anterior, sino que se limpiará (por ejemplo, racionalizando, eliminando funciones obsoletas). Por lo tanto, se recomienda que una página utilice únicamente conjuntos basados en CoralUI 3 o en CoralUI 2.

Para obtener más información detallada, consulte [Guía de migración a CoralUI 3-based](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### ¿Cómo personalizar el componente de búsqueda en AEM Assets? {#how-to-customize-the-search-component-in-aem-assets}

Para obtener más información sobre la ampliación/clasificación de la búsqueda y la implementación adicional, consulte [Guía de implementación de búsqueda simple](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

La implementación de la búsqueda simple son los materiales del laboratorio de la Cumbre 2017 AEM Search Demystified.

#### ¿Cuál es la diferencia entre AEM Assets y AEM MediaLibrary? {#what-is-the-difference-between-aem-assets-and-aem-medialibrary}

AEM Assets es una aplicación de la Plataforma de AEM que permite a nuestros clientes gestionar sus recursos digitales (imágenes, vídeos, documentos y clips de audio) en un repositorio basado en web, mientras que AEM Media Library es una parte designada del repositorio de contenido de WCM AEM donde se almacenan las imágenes y otros recursos compartidos.

Consulte [AEM Assets vs. AEM MediaLibrary](/help/assets/medialibrary.md) para obtener más información.

#### ¿Es posible crear un complemento para WordPress que permita a un cliente acceder al Selector de recursos de Adobe para seleccionar imágenes? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

Sí, un cliente que utilice WordPress puede utilizar el Selector de recursos de Adobe para seleccionar imágenes de su servidor AEM Assets y agregarlas a las publicaciones de su sitio de WordPress.

Consulte [Selector de recursos](../assets/search-assets.md#assetpicker) para obtener más información.

#### ¿Es posible ampliar las facetas de búsqueda en AEM Assets para agregar predicados adicionales? {#is-it-possible-to-extend-the-search-facets-in-aem-assets-to-add-additional-predicates}

Una implementación de Adobe Experience Manager (AEM) Assets en toda la empresa tiene la capacidad de almacenar muchos recursos. Puede agregar predicados al formulario predeterminado o utilizar un formulario personalizado que incluya facetas de su elección.

Consulte [Facetas de búsqueda](/help/assets/search-facets.md) para obtener más información.
