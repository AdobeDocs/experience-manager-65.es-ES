---
title: Migrar recursos y documentos de AEM Forms
seo-title: Migrate AEM Forms assets and documents
description: La utilidad Migración le permite migrar recursos y documentos de AEM Forms de AEM 6.3 Forms o versiones anteriores a AEM 6.4 Forms.
seo-description: The Migration utility allows you to Migrate AEM Forms assets and documents from AEM 6.3 Forms or prior versions to AEM 6.4 Forms.
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
role: Admin
exl-id: 0f9aab7d-8e41-449a-804b-7e1bfa90befd
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 2%

---

# Migrar recursos y documentos de AEM Forms{#migrate-aem-forms-assets-and-documents}

La utilidad de migración convierte la variable [Recursos adaptables de Forms](../../forms/using/introduction-forms-authoring.md), [configuraciones de nube](/help/sites-developing/extending-cloud-config.md)y [Activos de gestión de correspondencia](/help/forms/using/cm-overview.md) desde el formato utilizado en versiones anteriores hasta el formato utilizado en AEM 6.5 Forms. Al ejecutar la utilidad de migración, se migran los elementos siguientes:

* Componentes personalizados para formularios adaptables
* Plantillas de gestión de correspondencia y formularios adaptables
* Configuraciones de nube
* Gestión de correspondencia y recursos de formularios adaptables

>[!NOTE]
>
>En caso de una actualización fuera de lugar, en el caso de los recursos de Gestión de correspondencia, puede ejecutar la migración cada vez que importe los recursos. Para la migración de la gestión de correspondencia, debe tener instalado el paquete de compatibilidad de Forms.

## Enfoque de la migración {#approach-to-migration}

Puede [actualización](../../forms/using/upgrade.md) a la versión más reciente de AEM Forms 6.5 de AEM Forms 6.4, 6.3 o 6.2, o realice una instalación nueva. Dependiendo de si ha actualizado la instalación anterior o ha realizado una instalación nueva, debe realizar una de las siguientes acciones:

**En caso de una actualización in situ**

Si ha realizado una actualización in situ, la instancia actualizada ya tiene los recursos y documentos. Sin embargo, para poder utilizar los recursos y documentos, deberá instalar [Paquete de compatibilidad de AEMFD](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) (incluye el paquete de compatibilidad de gestión de correspondencia)

A continuación, debe actualizar los recursos y documentos mediante [ejecución de la utilidad Migración](#runningmigrationutility).

**En caso de instalación fuera de lugar**

Si se trata de una instalación fuera de lugar (nueva), antes de poder utilizar los recursos y documentos, deberá instalar [Paquete de compatibilidad de AEMFD](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) (incluye el paquete de compatibilidad de gestión de correspondencia).

A continuación, debe importar el paquete de recursos (zip o cmp) en la nueva configuración y, a continuación, actualizar los recursos y documentos en [ejecución de la utilidad Migración](#runningmigrationutility). Adobe recomienda crear nuevos recursos en la nueva configuración solo después de ejecutar la utilidad de migración.

Debido a [compatibilidad con versiones anteriores](/help/sites-deploying/backward-compatibility.md) cambios, se cambian las ubicaciones de algunas carpetas en el repositorio crx. Exportar e importar manualmente dependencias (bibliotecas y recursos personalizados) de la configuración anterior a un entorno nuevo.

## Lea esto antes de continuar con la migración {#prerequisites}

Para los activos de Gestión de Correspondencia:

* Para los recursos importados de la plataforma anterior, se agrega una propiedad: **fd:version=1.0**.
* Desde AEM 6.1 Forms, los comentarios no están disponibles de forma predeterminada. Los comentarios que se agregaron anteriormente están disponibles en los recursos, pero no son visibles en la interfaz automáticamente. Debe personalizar la propiedad extensionProperties en la interfaz de usuario de AEM Forms para que los comentarios estén visibles.
* En algunas versiones anteriores, como LiveCycle ES4, el texto se editaba con Flex RichTextEditor, pero desde AEM 6.1 Forms, se utiliza el editor HTML. Debido a esta renderización y al aspecto de las fuentes, los tamaños de fuente y los márgenes de fuente pueden ser diferentes de las versiones anteriores en la interfaz de usuario de Autor. Sin embargo, las letras tienen el mismo aspecto cuando se procesan.
* Las listas de los módulos de texto se mejoran y ahora se representan de forma diferente. Puede haber diferencias visuales. Le recomendamos que procese y vea las letras donde está utilizando listas en módulos de texto.
* Dado que los módulos de contenido de imagen se convierten en recursos DAM y que los diseños y fragmentos se añaden a los formularios durante la migración, la propiedad Updated By de estos módulos cambia a admin.
* El historial de versiones de los recursos no se migra y no está disponible después de la migración. Se mantiene el historial de versiones posterior a la migración.
* El estado Listo para publicar está en desuso desde AEM Forms 6.1, por lo que todos los recursos del estado Listo para publicar se cambian al estado Modificado.
* Dado que la interfaz de usuario se actualiza en AEM Forms 6.3, los pasos para realizar las personalizaciones también son diferentes. Debe rehacer la personalización si está migrando de una versión anterior a la 6.3.
* Los fragmentos de diseño pasan de /content/apps/cm/layouts/fragmentlayouts/1001 a /content/apps/cm/module/fragmentlayouts. La referencia del diccionario de datos en los recursos muestra la ruta del diccionario de datos en lugar de su nombre.
* Los espacios de tabulación que se utilicen para la alineación en módulos de texto deben reajustarse. Para obtener más información, consulte [Gestión de correspondencia - Uso del espaciado de tabulación para organizar el texto](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* Las configuraciones del Compositor de recursos cambian a las configuraciones de Gestión de correspondencia.
* Los recursos se mueven en carpetas con nombres como Texto existente y Lista existente.

## Uso de la utilidad Migración {#using-the-migration-utility}

### Ejecución de la utilidad Migración {#runningmigrationutility}

Ejecute la utilidad de migración antes de realizar cambios en los recursos o crear recursos. Se recomienda que no ejecute la utilidad después de realizar cambios o crear recursos. Asegúrese de que la interfaz de usuario de Gestión de correspondencia o Recursos Forms adaptables no esté abierta mientras se esté ejecutando el proceso de migración.

Cuando ejecuta la Utilidad de migración por primera vez, se crea un registro con la siguiente ruta y nombre: `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`. Este registro sigue actualizándose con la información de migración de la Gestión de Correspondencia y Forms adaptable, como la transferencia de recursos.

>[!NOTE]
>
>Antes de ejecutar la utilidad de migración, asegúrese de haber realizado una copia de seguridad de su repositorio crx.

1. En una sesión del explorador, inicie sesión en AEM instancia de autor como administrador.

1. Abra la siguiente URL en el explorador:

   https://[*hostname*]:[*puerto*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   El explorador muestra cuatro opciones:

   * Migración de recursos de AEM Forms
   * Migración de componentes personalizados de Forms adaptable
   * Migración de plantillas adaptables de Forms
   * Migración de configuraciones en la nube de AEM Forms

1. Para realizar la migración, haga lo siguiente:

   * Para migrar **activos**, pulse Migración de recursos de AEM Forms y, en la pantalla siguiente, pulse **Iniciar migración**. Se migra lo siguiente:

      * Formularios adaptables
      * Fragmentos de documento
      * Temas
      * Cartas
      * Diccionarios de datos

   >[!NOTE]
   >
   >Durante la migración de recursos, puede encontrar mensajes de advertencia como &quot;Conflicto encontrado para...&quot;. Estos mensajes indican que no se pudieron migrar las reglas de algunos de los componentes de los formularios adaptables. Por ejemplo, si el componente tenía un evento que tenía reglas y secuencias de comandos, si las reglas se producen después de cualquier secuencia de comandos, no se migra ninguna de las reglas del componente. Puede [migrar estas reglas abriendo el editor de reglas](#migrate-rules) en la creación de formularios adaptables.

   * Para migrar componentes personalizados de formulario adaptable, pulse **Migración de componentes personalizados de Forms adaptable** y en la página Migración de componentes personalizados , pulse **Iniciar migración**. Se migra lo siguiente:

      * Componentes personalizados escritos para Forms adaptable
      * Superposiciones de componentes, si las hay.
   * Para migrar plantillas de formulario adaptables, pulse **Migración de plantillas de Forms adaptable** y en la página Migración de componentes personalizados , pulse **Iniciar migración**. Se migra lo siguiente:

      * Plantillas de formulario adaptables creadas en `/apps` o `/conf` con AEM Editor de plantillas.
   * Migre los servicios de configuración de AEM Forms Cloud para aprovechar el nuevo paradigma de servicio en la nube según el contexto, que incluye la IU táctil (en `/conf`). Cuando migre los servicios de configuración de AEM Forms Cloud, los servicios de nube en `/etc` se mueven a `/conf`. Si no tiene personalizaciones de servicios de nube que dependan de rutas heredadas (`/etc`), se recomienda ejecutar la utilidad de migración justo después de actualizar a la versión 6.5 y utilizar la configuración de nube Touch UI para cualquier trabajo posterior. Si tiene personalizaciones de servicios de nube existentes, continúe usando la IU clásica en la configuración actualizada hasta que las personalizaciones se actualicen para que se alineen con las rutas migradas (`/conf`) y luego ejecute la utilidad de migración.

   Para migrar **Servicios de nube de AEM Forms**, que incluye lo siguiente, pulse Migración de configuración de AEM Forms Cloud (la migración de configuración de nube es independiente del paquete de compatibilidad AEMFD), pulse Migración de configuraciones de AEM Forms Cloud y, a continuación, en la página Migración de configuración, pulse **Iniciar migración**:

   * Servicios de nube del Modelo de datos de formulario

      * Ruta de origen: `/etc/cloudservices/fdm`
      * Ruta de destino: `/conf/global/settings/cloudconfigs/fdm`
   * Recaptcha

      * Ruta de origen: `/etc/cloudservices/recaptcha`
      * Ruta de destino: `/conf/global/settings/cloudconfigs/recaptcha`
   * Adobe Sign

      * Ruta de origen: `/etc/cloudservices/echosign`
      * Ruta de destino: `/conf/global/settings/cloudconfigs/echosign`
   * Servicios de nube de Typekit

      * Ruta de origen: `/etc/cloudservices/typekit`
      * Ruta de destino: `/conf/global/settings/cloudconfigs/typekit`

   La ventana del explorador muestra lo siguiente a medida que se produce el proceso de migración:

   * Cuando se actualizan los recursos: Recursos actualizados correctamente.
   * Una vez completada la migración: Migración de recursos finalizada.

   Cuando se ejecuta, la utilidad Migración hace lo siguiente:

   * **Añade las etiquetas a los recursos**: Agrega la etiqueta &quot;Gestión de correspondencia : Recursos migrados&quot; / &quot;Forms adaptable : Recursos migrados&quot;. a los recursos migrados, de modo que los usuarios puedan identificar los recursos migrados. Al ejecutar la utilidad Migración, todos los recursos existentes en el sistema se marcan como Migrados.
   * **Genera etiquetas**: Las categorías y subcategorías presentes en el sistema anterior se crean como etiquetas y, a continuación, estas etiquetas se asocian a los recursos relevantes de Gestión de Correspondencia en AEM. Por ejemplo, una categoría (reclamaciones) y una subcategoría (reclamaciones) de una plantilla de carta se generan como etiquetas.










1. Una vez que la utilidad de migración haya terminado de ejecutarse, continúe con el [tareas domésticas](#housekeepingtasks).

#### Migración de reglas mediante el editor de reglas {#migrate-rules}

Estos componentes se pueden migrar abriéndolos en el Editor de reglas en el editor de Forms adaptable.

* Para migrar reglas y secuencias de comandos (no es necesario si se actualiza desde la versión 6.3) a los componentes personalizados, pulse Migración de componentes personalizados de Forms adaptable y, en la pantalla siguiente, pulse Iniciar migración. Se migra lo siguiente:

   * Reglas y secuencias de comandos creadas con el editor de reglas (6.1 FP1 y posteriores)

   * Secuencias de comandos creadas con la pestaña Script en la IU de 6.1 y anteriores

* Para migrar plantillas (no es necesario si se actualiza desde la versión 6.3 y 6.4), pulse Migración de plantillas de Forms adaptable y, en la pantalla siguiente, pulse Iniciar migración. Se migra lo siguiente:

   * Plantillas antiguas: plantillas de formularios adaptables creadas en /apps con AEM 6.1 Forms o anterior. Esto incluye las secuencias de comandos definidas en los componentes de la plantilla.

   * Nuevas plantillas : plantillas de formularios adaptables creadas con el editor de plantillas en /conf. Esto incluye la migración de reglas y secuencias de comandos creadas con el editor de reglas.

### Tareas domésticas después de ejecutar la utilidad de migración {#housekeepingtasks}

Después de ejecutar la utilidad de migración, debe encargarse de las siguientes tareas de mantenimiento:

1. Compruebe que la versión XFA de diseños y diseños de fragmento sea 3.3 o posterior. Si utiliza diseños y diseños de fragmento de una versión anterior, podría haber problemas al procesar la carta. Para actualizar la versión de un XFA anterior a la versión más reciente, complete los siguientes pasos:

   1. [Descargar el XFA como archivo zip](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) desde la interfaz de usuario de Forms.
   1. Extraiga el archivo .
   1. Abra el archivo XFA en el último Designer y guárdelo. La versión del XFA se actualiza a la más reciente.
   1. Cargue el XFA en la interfaz de usuario de Forms.

1. Publique todos los recursos publicados en el sistema anterior antes de la migración. La utilidad de migración actualiza los recursos solo en la instancia de autor y para actualizar los recursos en la instancia de publicación es necesario publicar los recursos.

1. En AEM Forms 6.4 y 6.5, se cambian algunos de los derechos de los grupos de usuarios de formularios. Si desea que cualquiera de los usuarios pueda cargar XDP y Adaptive Forms que contengan secuencias de comandos o utilizar el editor de código, debe agregarlos al grupo de usuarios que puedan acceder a formularios. Del mismo modo, los autores de plantillas ya no pueden utilizar el editor de código del Editor de reglas. Para que los usuarios puedan utilizar el editor de código, agréguelos al grupo af-template-script-writers. Para obtener instrucciones sobre cómo agregar usuarios a grupos, consulte [Administración de usuarios y grupos de usuarios](/help/communities/users.md).
