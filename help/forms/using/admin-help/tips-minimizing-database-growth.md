---
title: Sugerencias para minimizar el crecimiento de las bases de datos
description: AEM Los procesos de larga duración almacenan datos de procesos en la base de datos de formularios de la. AEM El crecimiento de la base de datos de formularios de la se puede minimizar mediante unas sencillas estrategias de diseño de procesos y configuración de productos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f64efb06-815a-4608-ba1c-39e22f344ebb
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---

# Sugerencias para minimizar el crecimiento de las bases de datos {#tips-for-minimizing-database-growth}

AEM Los procesos de larga duración almacenan datos de procesos en la base de datos de formularios de la. AEM El crecimiento de la base de datos de formularios de la se puede minimizar mediante unas sencillas estrategias de diseño de procesos y configuración de productos.

## Sugerencias de diseño de procesos {#process-design-tips}

Utilice procesos de corta duración siempre que sea posible. Los procesos de corta duración no almacenan datos de proceso en la base de datos. La desventaja de utilizar procesos de corta duración es que su estado y estado no se rastrean en la consola de administración y no hay historial del proceso.

Algunas operaciones del servicio, como la operación Asignar tarea (servicio de usuario), requieren que se utilicen en procesos de larga duración. En este caso, puede segmentar el proceso en varios subprocesos y hacerlos de corta duración cuando sea posible. Si utiliza esta estrategia, los subprocesos de corta duración deben gestionar elementos de datos grandes, como valores de documento.

Utilice las variables con moderación. Al utilizar procesos de larga duración, para cada instancia de proceso, se asigna espacio en la base de datos para cada variable del proceso. El uso estratégico de variables puede ahorrar una cantidad considerable de espacio. Por ejemplo, puede sobrescribir valores de variables cuando ya no se necesiten valores antiguos en el proceso. Elimine todas las variables que haya creado y que no esté utilizando. Puede validar el proceso para buscar variables que no se utilicen.

Utilice tipos de variables simples (por ejemplo, string o int) y evite utilizar tipos de variables complejas cuando sea posible. El espacio de la base de datos se asigna para variables incluso cuando no contienen un valor. Las variables complejas suelen requerir más espacio que las simples.

## Sugerencias de administración de productos {#product-administration-tips}

Utilice el almacenamiento global de documentos (GDS) de forma eficaz. El directorio GDS del servidor de Forms AEM se utiliza para almacenar, entre otras cosas, los archivos que se pasan a servicios que forman parte de formularios en proceso de la. Para mejorar el rendimiento, los documentos más pequeños se almacenan en la memoria y se conservan en la base de datos.

La consola de administración expone la propiedad Tamaño máximo en línea del documento predeterminado para configurar el tamaño máximo de los documentos almacenados en memoria y conservados en la base de datos. (Consulte [AEM Configurar opciones generales de formularios](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).) Si establece esta propiedad en un valor bajo, la mayoría de los documentos se conservan en el directorio GDS en lugar de en la base de datos. La ventaja es que puede eliminar más fácilmente los archivos cuando ya no los necesita cuando están almacenados en el directorio GDS.
