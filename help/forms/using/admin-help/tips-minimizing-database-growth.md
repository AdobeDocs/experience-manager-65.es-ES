---
title: Sugerencias para minimizar el crecimiento de la base de datos
seo-title: Sugerencias para minimizar el crecimiento de la base de datos
description: Los procesos de larga duración almacenan datos de proceso en la base de datos de formularios de AEM. El crecimiento de la base de datos de formularios de AEM se puede minimizar con un sencillo diseño de procesos y estrategias de configuración de productos.
seo-description: Los procesos de larga duración almacenan datos de proceso en la base de datos de formularios de AEM. El crecimiento de la base de datos de formularios de AEM se puede minimizar con un sencillo diseño de procesos y estrategias de configuración de productos.
uuid: 13f99d4f-848e-451e-90d9-55e202dc0bdb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89441336-babc-4d1f-9053-d1566cd42d22
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Sugerencias para minimizar el crecimiento de la base de datos {#tips-for-minimizing-database-growth}

Los procesos de larga duración almacenan datos de proceso en la base de datos de formularios de AEM. El crecimiento de la base de datos de formularios de AEM se puede minimizar con un sencillo diseño de procesos y estrategias de configuración de productos.

## Sugerencias de diseño de procesos {#process-design-tips}

Utilice procesos de corta duración siempre que sea posible. Los procesos de corta duración no almacenan datos de proceso en la base de datos. La desventaja de utilizar procesos de corta duración es que su estado y estado no se rastrean en la consola de administración y no hay historial del proceso.

Algunas operaciones de servicio, como la operación Asignar tarea (servicio de usuario), requieren que se utilicen en procesos de larga duración. En este caso, puede segmentar el proceso en varios subprocesos y hacerlos de corta duración cuando sea posible. Si utiliza esta estrategia, los subprocesos de corta duración deben gestionar elementos de datos de gran tamaño, como valores de documento.

Utilice las variables con moderación. Cuando se utilizan procesos de larga duración, para cada instancia de proceso, se asigna espacio en la base de datos para cada variable del proceso. El uso estratégico de las variables puede ahorrar una cantidad considerable de espacio. Por ejemplo, puede sobrescribir valores de variables cuando ya no se necesiten valores antiguos en el proceso. Y elimine todas las variables que haya creado y que no esté utilizando. Puede validar el proceso para buscar variables no utilizadas.

Utilice tipos de variables simples (por ejemplo, string o int) y evite usar tipos de variables complejas cuando sea posible. El espacio de la base de datos se asigna a las variables aunque no contengan un valor. Las variables complejas generalmente requieren más espacio que las simples.

## Consejos de administración de productos {#product-administration-tips}

Utilice el almacenamiento global de documentos (GDS) de manera eficaz. El directorio GDS del servidor de formularios se utiliza para almacenar, entre otras cosas, archivos que se pasan a servicios que forman parte de formularios AEM en procesos. Para mejorar el rendimiento, los documentos más pequeños se almacenan en la memoria y se conservan en la base de datos.

la consola de administración expone la propiedad Tamaño en línea máximo del documento predeterminado para configurar el tamaño máximo de los documentos almacenados en la memoria y que se conservan en la base de datos. (Consulte [Configuración general de la configuración](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)de formularios AEM). Si establece esta propiedad en un valor bajo, la mayoría de los documentos se conservan en el directorio GDS en lugar de en la base de datos. La ventaja es que puede eliminar más fácilmente los archivos cuando ya no se necesitan cuando se almacenan en el directorio GDS.
