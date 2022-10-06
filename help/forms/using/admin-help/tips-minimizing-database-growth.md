---
title: Sugerencias para minimizar el crecimiento de las bases de datos
seo-title: Tips for minimizing database growth
description: Los procesos de larga duración almacenan datos de proceso en la base de datos de AEM forms. El crecimiento de la base de datos de formularios AEM se puede minimizar utilizando algunas estrategias sencillas de diseño de procesos y configuración de productos.
seo-description: Long-lived processes store process data in the AEM forms database. The growth of the AEM forms database can be minimized using a few easy process design and product configuration strategies.
uuid: 13f99d4f-848e-451e-90d9-55e202dc0bdb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89441336-babc-4d1f-9053-d1566cd42d22
exl-id: f64efb06-815a-4608-ba1c-39e22f344ebb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Sugerencias para minimizar el crecimiento de las bases de datos {#tips-for-minimizing-database-growth}

Los procesos de larga duración almacenan datos de proceso en la base de datos de AEM forms. El crecimiento de la base de datos de formularios AEM se puede minimizar utilizando algunas estrategias sencillas de diseño de procesos y configuración de productos.

## Sugerencias de diseño de procesos {#process-design-tips}

Utilice procesos de corta duración siempre que sea posible. Los procesos de corta duración no almacenan datos de proceso en la base de datos. La desventaja de utilizar procesos de corta duración es que su estado y estado no se rastrean en la consola de administración y no hay historial del proceso.

Algunas operaciones de servicio, como la operación Asignar tarea (servicio de usuario), requieren que se utilicen en procesos de larga duración. En este caso, puede segmentar el proceso en varios subprocesos y hacerlos de corta duración cuando sea posible. Si utiliza esta estrategia, los subprocesos de corta duración deben gestionar elementos de datos de gran tamaño, como valores de documento.

Utilice las variables con moderación. Cuando se utilizan procesos de larga duración, para cada instancia de proceso, el espacio se asigna en la base de datos para cada variable del proceso. El uso estratégico de variables puede ahorrar una cantidad considerable de espacio. Por ejemplo, puede sobrescribir los valores de las variables cuando ya no se necesiten valores antiguos en el proceso. Elimine las variables que haya creado y que no esté utilizando. Puede validar el proceso para buscar variables que no se utilicen.

Utilice tipos de variables simples (por ejemplo, cadena o int) y evite utilizar tipos de variables complejos cuando sea posible. El espacio de la base de datos se asigna para variables incluso cuando no contienen un valor. Las variables complejas suelen requerir más espacio que las simples.

## Sugerencias de administración de productos {#product-administration-tips}

Utilice el almacenamiento global de documentos (GDS) de forma eficaz. El directorio GDS del servidor de formularios se utiliza para almacenar, entre otras cosas, archivos que se pasan a servicios que forman parte de AEM formularios en procesos. Para mejorar el rendimiento, los documentos más pequeños se almacenan en la memoria y se conservan en la base de datos.

la consola de administración expone la propiedad Tamaño en línea máximo del documento predeterminado para configurar el tamaño máximo de los documentos almacenados en la memoria y que se mantienen en la base de datos. (Consulte [Configuración general de AEM formularios](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).) Si establece esta propiedad en un valor bajo, la mayoría de los documentos se mantienen en el directorio GDS en lugar de en la base de datos. La ventaja es que puede eliminar los archivos con mayor facilidad cuando ya no se necesitan cuando se almacenan en el directorio GDS.
