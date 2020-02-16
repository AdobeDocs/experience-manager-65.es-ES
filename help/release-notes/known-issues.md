---
title: Problemas conocidos
description: Notas de versión específicas de problemas conocidos con Adobe Experience Manager 6.3
uuid: 8fbdb167-833a-4179-aad1-0a26a4e5b3a7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: d11fc727-f23a-4cde-9fa6-97e2c81b4ad0
docset: aem65
translation-type: tm+mt
source-git-commit: 57bad4e74b2dfd9e389643bfe58ef25564c5c545

---


# Problemas conocidos{#known-issues}

Esta página contiene una lista de problemas conocidos de Adobe Experience Manager 6.5 que se publicó en abril de 2019.

[Póngase en contacto con el servicio de soporte técnico](https://helpx.adobe.com/support/experience-manager.html) si necesita más información sobre los problemas conocidos.

## Plataforma {#platform}

Se informa de un problema en el que se eliminan CRX-Quickstart y su contenido.

En cada una de estas acciones, asegúrese de que la propiedad &quot;*htmllibmanager.fileSystemOutputCacheLocation*&quot; nunca sea una cadena vacía:

1. Llamando a &quot;*/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true*&quot;.
2. Actualización a AEM 6.5.
3. Ejecución de la &quot;migración de contenido flotante&quot; en AEM 6.5.

Hay disponible un artículo de la Base [de](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) conocimiento con más detalles y la solución alternativa para este problema.

## Recursos {#assets}

* **** Buscar: La búsqueda no devuelve ningún resultado si la cadena de búsqueda contiene espacios iniciales ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Esquema de metadatos de carpeta**: después de añadir un botón de opciones, los campos Id. y Valor no se procesan como se esperaba y la funcionalidad de eliminación no funciona. (CQ-4261144)
* Al cambiar el nombre de un recurso, no se puede utilizar un espacio en blanco en el nombre del recurso. (CQ-4266403)

## Formularios {#forms}

* Cuando se instala AEM Forms en el sistema operativo de Linux, la firma digital con el módulo de seguridad de hardware no funciona. (CQ-4266721)
* (AEM Forms on WebSphere only) The **Forms Workflow **> **Task Search** option does not return any result if you search for an **Administrator** with **Username** as the search criteria. (CQ-4266457)

* AEM Forms no puede convertir archivos .tif ni .tiff con la opción de compresión JPEG en documentos PDF. (CQ-4265972)
* Las opciones **AEM Forms Assets Scanner** (Escáner de recursos de AEM Forms) y **Letter to Interactive Communication Migration** (Carta para la migración de comunicaciones interactiva) no funcionan en la página de **migración de AEM Forms**. (CQ-4266572)

* (Solo JBoss 7) Cuando se actualiza desde una versión anterior a AEM 6.5 Forms y la versión anterior tenía procesos (.lca) que creaban y utilizaban una copia del proceso de envío predeterminado o de procesamiento predeterminado, los formularios HTML5 que utilizaban estos procesos (.lca) no pueden realizar las acciones necesarias. (CQ-4243928)
* En un formulario adaptable, cuando se invoca un servicio de modelo de datos de formulario desde el editor de reglas para actualizar dinámicamente los valores del componente de elección de imágenes, los valores del componente de elección de imágenes no se actualizan. (CQ-4254754)
* AEM Forms Designer installer requires the 32-bit version of [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) and [Visual C++ redistributable runtime packages 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Asegúrese de que los paquetes de ejecución redistribuibles anteriores estén instalados antes de iniciar la instalación. (CQ-4265668)

* Cuando se configura un formulario adaptable para actualizar dinámicamente los valores de un componente y se accede a la instancia de publicación que aloja el formulario a través del controlador, la funcionalidad para actualizar dinámicamente los valores de un campo deja de funcionar. Para resolver el problema, en la instancia de publicación, abra CRXDE, desplácese hasta /libs/fd/af/runtime/clientlibs/guideChartReducer y cree la siguiente propiedad.

   * Nombre: allowProxy
   * Tipo: Boolean (booleano)
   * Valor: true (verdadero)
   * Protegido: false (falso)
   * Obligatorio: false (falso)
   * Varios: false (falso)
   * Creación automática: false (falso)

La propiedad permite que las bibliotecas de cliente en la carpeta de ejecución accedan a los proxy. (CQ-4268679)

