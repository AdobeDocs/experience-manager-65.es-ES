---
title: Integración de '[!DNL Experience Manager Assets] con [!DNL Adobe Workfront]'
description: Introducción a la integración entre  [!DNL Assets] y [!DNL Workfront]
role: Admin,Leader,Architect
feature: Workfront Integrations and Apps
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
hide: true
solution: Experience Manager, Workfront
source-git-commit: 5ccac0aadce3971e66da052d393cbd33b61e94f7
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 9%

---

# Integración de [!DNL Adobe Experience Manager Assets] con [!DNL Adobe Workfront] {#assets-integration-overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=es) |
| AEM 6.5 | Este artículo |

[!DNL Adobe Workfront] es una aplicación de administración de trabajo que le ayuda a administrar todo el ciclo de vida del trabajo en un solo lugar. La integración entre [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] permite a las organizaciones mejorar la velocidad del contenido y el tiempo de salida al mercado, conectando intrínsecamente el trabajo con la administración de recursos digitales. En el contexto de la administración de su trabajo en Workfront, los usuarios tienen acceso a los documentos e imágenes necesarios.

[!DNL Workfront for Experience Manager enhanced connector] habilita procesos empresariales mejorados con flujos de trabajo de un extremo a otro, y proporciona experiencias de cliente de un extremo a otro personalizadas y almacenamiento central. Adobe ofrece un conector estándar y un conector mejorado para integrar las dos soluciones. Vea las funciones admitidas a continuación para ver una comparación y vea [las novedades de [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] permite a su organización:

* Cree automáticamente carpetas de Experience Manager vinculados en Workfront y organícelas en función de Portfolio, programas y proyectos de Workfront.
* Sincronice los metadatos del proyecto de Workfront con las carpetas de Experience Manager vinculadas.
* Experience Manager de actualizaciones de metadatos con nuevas versiones.
* Establezca los estados de objetos de Workfront en función de condiciones configurables mediante flujos de trabajo de Experience Manager.
* Recursos de Publish para el entorno de publicación de Experience Manager o para Brand Portal.

Consulte los [requisitos previos y compatibilidad con la plataforma para el conector mejorado](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* El Adobe requiere la implementación y configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector] solamente a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y se configura sin un socio certificado o [!DNL Adobe Professional Services], no se admite en el Adobe.
>
>* El Adobe puede publicar actualizaciones para [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hagan redundante este conector; si esto sucede, es posible que los clientes deban realizar la transición desde el uso de este conector.
>
>* El Adobe admite las versiones de conector mejoradas 1.7.4 y posteriores. No se admiten versiones preliminares ni versiones personalizadas anteriores. Para comprobar la versión mejorada del conector, vaya al grupo `digital.hoodoo` disponible en el panel izquierdo de [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es).
>
>* Consulte [Examen de certificación de socio para el conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener información sobre el examen, consulte [Guía para exámenes](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Comparar diferentes integraciones entre [!DNL Assets] y [!DNL Workfront] {#feature-parity-matrix}

A continuación se muestran los detalles de las funcionalidades disponibles a través de varios tipos de integraciones entre [!DNL Assets] y [!DNL Workfront].

| Funcionalidad | Descripción | [!DNL Workfront] y [!DNL Assets Essentials] *Sin conector (predeterminado)* | [!DNL Workfront for Experience Manager enhanced connector] *Requiere Conector* | Workfront y [!DNL Experience Manager as a Cloud Service] *Sin conector (predeterminado)* |
|----|----|----|-----|-----|
| Métodos de implementación | Apropiado para la oferta [!DNL Assets]. | Assets Essentials | Adobe Managed Services, On-Premise | Cloud Service |
| **General** |
| Enviar archivos digitales de [!DNL Workfront] a [!DNL Assets] | La última versión de un documento WF se puede cargar en AEM Assets, que está vinculado como una nueva versión del documento. | ✓ | ✓ | ✓ |
| AEM Vinculación manual de carpetas de recursos a objetos de Workfront | AEM Las carpetas existentes se pueden vincular como carpetas de Workfront y sus recursos secundarios se vinculan como nuevos documentos de Workfront. | ✓ | ✓ | ✓ |
| Vincular [!DNL Assets] a objetos de Workfront | AEM Los recursos existentes en la se pueden vincular a un nuevo documento de Workfront o como una nueva versión de un documento existente. | ✓ | ✓ | ✓ |
| Los Assets AEM que se agreguen a carpetas vinculadas se envían automáticamente a los usuarios de la aplicación de correo electrónico | Si se agrega el documento a una carpeta vinculada, el recurso asociado se cargará automáticamente en AEM Assets como un nuevo recurso. | ✓ | ✓ | ✓ |
| Descargar AEM Assets vinculado desde Workfront | Cuando un recurso está vinculado en Workfront, el usuario puede descargar los bytes del recurso. | ✓ | ✓ | ✓ |
| Busque AEM Assets desde Workfront | El selector de AEM Assets en Workfront permite búsquedas de texto completo para recursos. | ✓ | ✓ | ✓ |
| AEM Buscar carpetas de la desde Workfront | El selector de AEM Assets en Workfront permite búsquedas de texto completo en carpetas. | ✓ | ✓ | ✓ |
| AEM Ver y navegar por la jerarquía de carpetas desde Workfront | El selector de AEM Assets en Workfront permite la exploración de la jerarquía de AEM Assets limitada por el   AEM los controles de acceso y permisos asociados al usuario establecidos en la sección de permisos de la aplicación de la aplicación de la aplicación de. | ✓ | ✓ | ✓ |
| AEM Seguimiento de versiones de recursos en cronologías de | Mantener el historial de versiones del documento entre Workfront AEM y la. | ✓ | ✓ | ✓ |
| Desvincular Assets de AEM Assets en Workfront | AEM Un recurso vinculado existente de la lista de recursos se puede desvincular del documento de Workfront asociado. AEM Esto no elimina el recurso original dentro de la. | ✓ | ✓ | ✓ |
| Añadir recurso con nueva versión a AEM Assets desde Workfront | Cuando se agrega una versión recién agregada a un documento en Workfront AEM, un usuario puede enviar la nueva versión a para que la sustituya, a fin de que se pueda usar la versión existente. | ✓ | ✓ | ✓ |
| Assets enlazado en Workfront AEM al hacer clic en el usuario directo para obtener la | AEM Los usuarios son dirigidos a los recursos para obtener una vista previa de un recurso vinculado desde Workfront. | ✓ | ✓ | Próximamente |
| AEM Crear automáticamente carpetas enlazadas de la en Workfront | AEM Cree automáticamente carpetas de recursos enlazados en Workfront mediante los estados de proyecto. AEM Configuración automática de carpetas de recursos basadas en Portfolio, programas y proyectos de Workfront. | No | ✓ | No |
| AEM Navegue directamente a repositorios de desde Workfront | AEM Permite que los usuarios naveguen a los repositorios de datos disponibles configurados en Workfront. | ✓ | No | ✓ |
| AEM Creación de carpetas de carpetas enlazadas en Workfront | AEM Cree manualmente carpetas de recursos enlazadas en Workfront mediante la opción disponible en la pestaña Documentos. | ✓ | No | ✓ |
| Sincronización de comentarios | Sincronizar automáticamente los comentarios de los recursos de [!DNL Workfront] a [!DNL Assets] | No | ✓ | No |
| Compatibilidad con varios entornos de Workfront AEM que se conectan a un solo entorno de | Los usuarios de varios entornos de Workfront AEM pueden conectarse a un único entorno de. | ✓ | No | ✓ |
| AEM Compatibilidad con varios entornos de que se conectan a un solo entorno de Workfront | Los usuarios dentro de un solo entorno de Workfront AEM pueden enviar o vincular recursos entre varios entornos de. | ✓ | ✓ | ✓ |
| **Metadatos** |
| Asignar metadatos de recursos de Workfront a AEM Assets | Las propiedades de objeto de Workfront AEM y de formulario personalizado se pueden asignar a propiedades de metadatos de recursos de. Los valores se insertan en la carga o el vínculo inicial. | ✓ | ✓ | ✓ |
| Crear automáticamente un documento de Forms personalizado en Workfront | Adjuntar formularios personalizados a documentos, tareas y problemas de Workfront AEM mediante flujos de trabajo de la. | No | ✓ | No |
| Actualización automática bidireccional de metadatos entre AEM Assets y Workfront | Actualizar automáticamente los metadatos entre AEM Assets y Workfront. El recurso debe insertarse inicialmente desde Workfront AEM a la red de recursos, y los metadatos del recurso de Workfront AEM deben asignarse a los recursos de la red de recursos para que las actualizaciones de metadatos bidireccionales funcionen correctamente. | No | ✓ | No |
| Vista en tiempo real en Workfront AEM para metadatos asignados a los usuarios de la red de área de datos | AEM Vea los metadatos asignados actualizados a los paneles Detalles del documento y Resumen del documento de Workfront para su uso. | ✓ | No | ✓ |
| Inserción en tiempo real de metadatos de Workfront AEM actualizados para su | Actualice automáticamente los metadatos de Workfront AEM asignados a sin volver a cargar un recurso o una nueva versión de un recurso. | ✓ | No | ✓ |
| Asignación de metadatos de Workfront a carpetas de AEM Assets | Sincronice los metadatos del proyecto de Workfront AEM con las carpetas enlazadas de la. | No | ✓ | ✓ |
| AEM Actualizaciones de metadatos con nuevas versiones de | AEM Se puede realizar una configuración en la para determinar si un recurso con una nueva versión en Workfront también se inserta junto con los cambios realizados en sus metadatos. | No | ✓ | No |
| AEM Actualizar automáticamente los metadatos de los cambios de los datos de la a Forms personalizada en Workfront | AEM le permite suscribirse a las actualizaciones de los formularios de documentos en Workfront. Como resultado, cualquier actualización de los metadatos del formulario personalizado del documento de Workfront AEM edita los valores de los campos de metadatos de la asignados. | No | ✓ | No |
| **Flujos de trabajo (predeterminados)** |
| Crear nueva versión de revisión en Assets vinculado | Al vincular un recurso en Workfront, se puede generar una prueba automáticamente. | No | Personalizado | No |
| Definir estado en objetos de Workfront | Definición de estados de objetos de Workfront AEM basados en condiciones configurables mediante flujos de trabajo de | No | ✓ | Próximamente |
| Publish Assets AEM a entorno de Publish o Brand Portal de la | Dé a los usuarios de Workfront AEM la opción de publicar automáticamente los recursos vinculados en un entorno de Publish o Brand Portal de la. | No | ✓ | Próximamente |
