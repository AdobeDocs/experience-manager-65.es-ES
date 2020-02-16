---
title: Migración de recursos y documentos de AEM Forms
seo-title: Migración de recursos y documentos de AEM Forms
description: La utilidad de migración le permite migrar recursos y documentos de AEM Forms desde AEM 6.3 Forms o versiones anteriores a AEM 6.4 Forms.
seo-description: La utilidad de migración le permite migrar recursos y documentos de AEM Forms desde AEM 6.3 Forms o versiones anteriores a AEM 6.4 Forms.
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# Migración de recursos y documentos de AEM Forms{#migrate-aem-forms-assets-and-documents}

La utilidad de migración convierte los recursos [de formularios](../../forms/using/introduction-forms-authoring.md)adaptables, las configuraciones de [nube](/help/sites-developing/extending-cloud-config.md)y los recursos [de administración de](/help/forms/using/cm-overview.md) correspondencia del formato utilizado en las versiones anteriores al formato utilizado en AEM 6.5 Forms. Al ejecutar la utilidad de migración, se migran los elementos siguientes:

* Componentes personalizados para formularios adaptables
* Plantillas de gestión de correspondencia y formularios adaptables
* Configuraciones de nube
* Gestión de correspondencia y recursos de formularios adaptables

>[!NOTE]
>
>En caso de actualización fuera de lugar, en el caso de los recursos de Correspondence Management, puede ejecutar la migración cada vez que importe los recursos. Para la migración de la administración de correspondencia debe tener instalado el paquete de compatibilidad de formularios.

## Enfoque de la migración {#approach-to-migration}

Puede [actualizar](../../forms/using/upgrade.md) a la versión más reciente de AEM Forms 6.5 desde AEM Forms 6.4, 6.3 o 6.2 o realizar una instalación nueva. Según si ha actualizado la instalación anterior o ha realizado una nueva instalación, debe realizar una de las siguientes acciones:

**En caso de actualización in situ**

Si ha realizado una actualización in situ, la instancia actualizada ya tiene los recursos y documentos. Sin embargo, antes de poder utilizar los recursos y documentos, deberá instalar el paquete [de compatibilidad](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEMFD (incluye el paquete de compatibilidad de gestión de correspondencia)

A continuación, debe actualizar los recursos y documentos [ejecutando la utilidad](#runningmigrationutility)Migración.

**En caso de instalación fuera de lugar**

Si se trata de una instalación fuera de lugar (nueva), antes de poder utilizar los recursos y documentos, deberá instalar el paquete [de compatibilidad](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEMFD (incluye el paquete de compatibilidad de gestión de correspondencia).

A continuación, debe importar el paquete de recursos (zip o cmp) en la nueva configuración y, a continuación, actualizar los recursos y documentos [ejecutando la utilidad](#runningmigrationutility)Migración. Adobe recomienda crear nuevos recursos en la nueva configuración solo después de ejecutar la utilidad de migración.

Debido a los cambios relacionados con [la compatibilidad](/help/sites-deploying/backward-compatibility.md) con versiones anteriores, se han cambiado las ubicaciones de algunas carpetas en el repositorio crx. Exporte e importe dependencias manualmente (bibliotecas y recursos personalizados) desde la configuración anterior a un entorno nuevo.

## Lea esto antes de continuar con la migración {#prerequisites}

Para los recursos de Correspondencia:

* Para los recursos importados de la plataforma anterior, se agrega una propiedad: **fd:version=1.0**.
* Desde AEM 6.1 Forms, los comentarios no están disponibles de forma predeterminada. Los comentarios que se agregaron anteriormente están disponibles en los recursos pero no son visibles en la interfaz automáticamente. Debe personalizar la propiedad expandedProperties en la interfaz de usuario de AEM Forms para que los comentarios estén visibles.
* En algunas de las versiones anteriores, como LiveCycle ES4, el texto se editaba con Flex RichTextEditor, pero desde AEM 6.1 Forms se utiliza el editor HTML. Debido a esta representación y al aspecto de las fuentes, los tamaños de fuente y los márgenes de fuente pueden ser diferentes de los de las versiones anteriores en la interfaz de usuario de Autor. Sin embargo, las letras se ven iguales cuando se procesan.
* Las listas de los módulos de texto se han mejorado y ahora se representan de forma diferente. Puede haber diferencias visuales. Le recomendamos que procese y vea las letras donde está utilizando listas en módulos de texto.
* Dado que los módulos de contenido de imagen se convierten en recursos DAM y que los diseños y fragmentos se agregan a los formularios durante la migración, la propiedad Actualizado por de estos módulos cambia a admin.
* El historial de versiones de los recursos no se migra y no está disponible tras la migración. Se mantiene el historial de versiones posterior a la migración.
* El estado Listo para publicar está en desuso desde AEM 6.1 Forms, por lo que todos los recursos del estado Listo para publicar se han cambiado al estado Modificado.
* Dado que la interfaz de usuario se actualiza en AEM Forms 6.3, los pasos para realizar las personalizaciones también son diferentes. Debe rehacer la personalización si está migrando de una versión anterior a la 6.3.
* Los fragmentos de diseño pasan de /content/apps/cm/layouts/fragmentlayouts/1001 a /content/apps/cm/module/fragmentlayouts. La referencia del diccionario de datos en los recursos muestra la ruta del diccionario de datos en lugar de su nombre.
* Los espacios de tabulación que se utilizan para la alineación en los módulos de texto deben reajustarse. Para obtener más información, consulte Gestión de [correspondencia - Uso del espaciado de tabulación para organizar el texto](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* Las configuraciones del compositor de recursos cambian a las configuraciones de Correspondence Management.
* Los recursos se mueven en carpetas con nombres como Texto existente y Lista existente.

## Uso de la utilidad Migración {#using-the-migration-utility}

### Ejecución de la utilidad Migración {#runningmigrationutility}

Ejecute la utilidad de migración antes de realizar cambios en los recursos o crear recursos. Se recomienda no ejecutar la utilidad después de realizar cambios o crear recursos. Asegúrese de que la interfaz de usuario de Administración de correspondencia o Recursos de formularios adaptables no esté abierta mientras se esté ejecutando el proceso de migración.

Al ejecutar la Utilidad de migración por primera vez, se crea un registro con la siguiente ruta y nombre: \[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log. Este registro se actualiza constantemente con la información de migración de Correspondencia y formularios adaptables, como mover recursos.

>[!NOTE]
>
>Antes de ejecutar la utilidad de migración, asegúrese de haber realizado una copia de seguridad del repositorio crx.

1. En una sesión de navegador, inicie sesión en la instancia de creación de AEM como administrador.

1. Abra la siguiente URL en el explorador:

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   El explorador muestra cuatro opciones:

   * Migración de recursos de AEM Forms
   * Migración de componentes personalizados de formularios adaptables
   * Migración de plantillas de formularios adaptables
   * Migración de configuraciones en la nube de AEM Forms

1. Para realizar la migración, haga lo siguiente:

   * Para migrar **recursos**, toque Migración de recursos de AEM Forms y, en la pantalla siguiente, toque **Iniciar migración**. Se migrará lo siguiente:

      * Formularios adaptables
      * Fragmentos de documento
      * Temas
      * Cartas
      * Diccionarios de datos
   >[!NOTE]
   >
   >Durante la migración de recursos, puede encontrar mensajes de advertencia como &quot;Conflicto encontrado para...&quot;. Estos mensajes indican que no se pudieron migrar las reglas de algunos de los componentes de los formularios adaptables. Por ejemplo, si el componente tiene un evento que tenga reglas y secuencias de comandos, si las reglas se producen después de cualquier secuencia de comandos, no se migrará ninguna de las reglas del componente. Sin embargo, estas reglas se pueden migrar abriendo el editor de reglas en la creación de formularios adaptables.
   >
   >
   >Estos componentes se pueden migrar abriéndolos en el Editor de reglas en el editor de formularios adaptables.
   >
   >
   >
   >    * Para migrar reglas y secuencias de comandos (no es necesario si se actualiza desde 6.3) en componentes personalizados, toque Migración de componentes personalizados de formularios adaptables y, en la siguiente pantalla, toque Iniciar migración. Se migrará lo siguiente: >
      >
      >
      >        

      * Reglas y secuencias de comandos creadas con el editor de reglas (6.1 FP1 y posterior)
      >        * Secuencias de comandos creadas con la ficha Secuencia de comandos en la interfaz de usuario de 6.1 y versiones anteriores
   >
   >
   >    * Para migrar plantillas (no es necesario si se actualiza desde 6.3 y 6.4), toque Migración de plantillas de formularios adaptables y, en la siguiente pantalla, toque Iniciar migración. Se migrará lo siguiente:
      >
      >
      >
      >        


      * Plantillas antiguas: plantillas de formularios adaptables creadas en /apps con AEM 6.1 Forms o versiones anteriores. Esto incluye las secuencias de comandos que se definieron en los componentes de la plantilla.
      >        * Plantillas nuevas: plantillas de formularios adaptables creadas con el editor de plantillas en /conf. Esto incluye la migración de reglas y secuencias de comandos creadas con el editor de reglas.


   * Para migrar componentes personalizados de formularios adaptables, toque Migración **de componentes personalizados de formularios** adaptables y, en la página Migración de componentes personalizados, toque **Iniciar migración**. Se migrará lo siguiente:

      * Componentes personalizados escritos para formularios adaptables
      * Superposiciones de componentes, si las hay.
   * Para migrar plantillas de formulario adaptables, toque Migración **de plantillas de formularios** adaptables y, en la página Migración de componentes personalizados, toque **Iniciar migración**. Se migrará lo siguiente:

      * Plantillas de formulario adaptables creadas en /apps o /conf con el Editor de plantillas de AEM.
   * Migre los servicios de configuración de nube de AEM Forms para aprovechar el nuevo paradigma de servicio en la nube contextual, que incluye la IU táctil habilitada (en /conf). Al migrar los servicios de configuración de nube de AEM Forms, los servicios en la nube de /etc se mueven a /conf. Si no tiene personalizaciones de servicios en la nube que dependan de las rutas heredadas (/etc.), se recomienda ejecutar la utilidad de migración inmediatamente después de actualizar a 6.5 y utilizar la IU táctil de configuración en la nube para cualquier otro trabajo. Si ya tiene personalizaciones de servicios en la nube, continúe utilizando la IU clásica en la configuración actualizada hasta que las personalizaciones se actualicen para alinearse con las rutas migradas (/conf) y, a continuación, ejecute la utilidad de migración.
   Para migrar los servicios **de nube de** AEM Forms, que incluyen lo siguiente, toque Migración de configuración de nube de AEM Forms (la migración de configuración de nube es independiente del paquete de compatibilidad AEMFD), toque Migración de configuraciones de nube de AEM Forms y, a continuación, en la página Migración de configuración, toque **Iniciar migración**:

   * Servicios de nube del modelo de datos de formulario

      * Ruta de origen: /etc/cloudservices/fdm
      * Ruta de destino: /conf/global/settings/cloudconfigs/fdm
   * Recaptcha

      * Ruta de origen: /etc/cloudservices/recaptcha
      * Ruta de destino: /conf/global/settings/cloudconfigs/recaptcha
   * Adobe Sign

      * Ruta de origen: /etc/cloudservices/echosign
      * Ruta de destino: /conf/global/settings/cloudconfigs/echosign
   * Servicios de nube de Typekit

      * Ruta de origen: /etc/cloudservices/typekit
      * Ruta de destino: /conf/global/settings/cloudconfigs/typekit
   La ventana del explorador muestra lo siguiente a medida que se produce el proceso de migración:

   * Al actualizar los recursos: Los recursos se actualizaron correctamente.
   * Una vez completada la migración: Finalizó la migración de recursos.
   Cuando se ejecuta, la utilidad Migración hace lo siguiente:

   * **Agrega las etiquetas a los recursos**: Agrega la etiqueta &quot;Gestión de correspondencia: Recursos migrados&quot; / &quot;Formularios adaptables: Recursos migrados&quot;. a los recursos migrados, para que los usuarios puedan identificar los recursos migrados. Al ejecutar la utilidad de migración, todos los recursos existentes en el sistema se marcan como Migrados.
   * **Genera etiquetas**: Las categorías y subcategorías presentes en el sistema anterior se crean como etiquetas y, a continuación, estas etiquetas se asocian a los recursos de Correspondence Management relevantes en AEM. Por ejemplo, una categoría (Reclamaciones) y una subcategoría (Reclamaciones) de una plantilla de carta se generan como etiquetas.

















1. Una vez que la utilidad de migración haya terminado de ejecutarse, continúe con las tareas [de mantenimiento](#housekeepingtasks).

### Tareas domésticas después de ejecutar la utilidad de migración {#housekeepingtasks}

Después de ejecutar la utilidad de migración, tenga en cuenta las siguientes tareas de mantenimiento: [](../../forms/using/import-export-forms-templates.md)

1. Asegúrese de que la versión XFA de diseños y diseños de fragmento es 3.3 o posterior. Si está utilizando diseños y maquetaciones de fragmentos de una versión anterior, podría haber problemas al procesar la carta. Para actualizar la versión de un XFA anterior a la versión más reciente, siga los pasos siguientes:

   1. [Descargue el archivo](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) XFA como zip desde la interfaz de usuario de Forms.
   1. Extraiga el archivo.
   1. Abra el archivo XFA en el último Designer y guárdelo. La versión del XFA se actualiza a la más reciente.
   1. Cargue el XFA en la interfaz de usuario de Forms.

1. Publique todos los recursos publicados en el sistema anterior antes de la migración. La utilidad de migración actualiza los recursos solo en la instancia de autor y, para actualizar los recursos en las instancias de publicación, es necesario publicarlos.
1. En AEM Forms 6.4 y 6.5, se cambian algunos de los derechos de los grupos de usuarios de formularios. Si desea que cualquiera de los usuarios pueda cargar archivos XDP y formularios adaptables que contengan secuencias de comandos o utilice el editor de código, deberá agregarlos al grupo de usuarios con capacidad para formularios. Del mismo modo, los autores de plantillas ya no pueden utilizar el editor de código en el Editor de reglas. Para que los usuarios puedan utilizar el editor de código, agréguelos al grupo af-template-script-writers. Para obtener instrucciones sobre cómo agregar usuarios a grupos, consulte [Administración de usuarios y grupos](/help/communities/users.md)de usuarios.

