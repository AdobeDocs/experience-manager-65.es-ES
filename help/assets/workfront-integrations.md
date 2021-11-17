---
title: '[!DNL Experience Manager Assets] integration with [!DNL Adobe Workfront]'
description: Introducción a la integración entre [!DNL Assets] y [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
source-git-commit: 8d39e1c86e5185a181400f10b7822a57c9d3aeae
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager Assets] integración con [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] es una aplicación de administración de trabajo que le ayuda a administrar todo el ciclo de vida del trabajo en un solo lugar. La integración entre [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] permite a las organizaciones mejorar la velocidad de contenido y el tiempo de comercialización conectando intrínsecamente el trabajo con la administración de recursos digitales. En el contexto de la administración de su trabajo en Workfront, los usuarios tienen acceso a los documentos e imágenes necesarios.

La variable [!DNL Workfront for Experience Manager enhanced connector] permite procesos empresariales mejorados con flujos de trabajo end-to-end y proporciona experiencias personalizadas de cliente end-to-end y almacenamiento de información central. Para obtener más información sobre las capacidades y características de la variable [!DNL enhanced connector], consulte [novedades de [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] permite a su organización:

* Cree automáticamente carpetas de Experience Manager vinculadas en Workfront y organice las carpetas en función de Portfolio, programas y proyectos de Workfront.
* Sincronice los metadatos del proyecto de Workfront con las carpetas de Experience Manager vinculadas.
* Actualizaciones de metadatos de Experience Manager con nuevas versiones.
* Defina los estados de los objetos de Workfront en función de condiciones configurables mediante flujos de trabajo de Experience Manager.
* Publique recursos en el entorno de publicación de Experience Manager o en Brand Portal.

Consulte la compatibilidad con la plataforma y [requisitos previos para el conector mejorado](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>El Adobe requiere la implementación y la configuración del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y se configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con Adobe.
>
>Adobe puede publicar actualizaciones en [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hacen que este conector sea redundante; si esto ocurre, es posible que se requiera a los clientes que pasen del uso de este conector.

## Comparar distintas integraciones entre [!DNL Assets] y [!DNL Workfront] {#feature-parity-matrix}

A continuación se detallan las funcionalidades disponibles a través de varios tipos de integraciones entre [!DNL Assets] y [!DNL Workfront].

| Función | Descripción | [!DNL Workfront] y [!DNL Assets Essentials] | [!DNL Workfront] para [!DNL Experience Manager] connector | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| Métodos de implementación | Apropiado para el cual [!DNL Assets] oferta. | Assets Essentials | Cloud Service, Adobe Managed Services, On-Premise | Cloud Service, Adobe Managed Services, On-Premise |
| Enviar archivos digitales desde [!DNL Workfront] a [!DNL Assets] | La última versión de un documento WF se puede cargar en AEM Assets, que se vinculará como una nueva versión del documento. | ✓ | ✓ | ✓ |
| Vincular manualmente AEM carpetas a objetos de Workfront | Las carpetas de AEM existentes se pueden vincular como una carpeta de Workfront y sus recursos secundarios se vinculan como nuevos documentos de Workfront. | ✓ | ✓ | ✓ |
| Vínculo [!DNL Assets] a objetos de Workfront | Los recursos existentes en AEM pueden vincularse a un nuevo documento de Workfront o como una nueva versión de un documento existente. | ✓ | ✓ | ✓ |
| Los recursos añadidos a carpetas vinculadas se envían automáticamente a AEM | Si el documento se agrega a una carpeta vinculada, el recurso asociado se carga automáticamente en AEM Assets como nuevo recurso. | ✓ | ✓ | ✓ |
| Descargar AEM Assets vinculado desde Workfront | Cuando un recurso está vinculado en Workfront, el usuario puede descargar los bytes del recurso. | ✓ | ✓ | ✓ |
| Buscar AEM Assets desde Workfront | El selector de AEM Assets en Workfront permite realizar búsquedas de texto completo de los recursos. | ✓ | ✓ | ✓ |
| Ver y navegar AEM jerarquía de carpetas desde Workfront | El selector de AEM Assets en Workfront permite examinar la jerarquía de AEM Assets limitada por los controles de acceso asociados al usuario y los permisos establecidos en AEM. | ✓ | ✓ | ✓ |
| Desvincular recursos de AEM Assets en Workfront | Un recurso vinculado existente de AEM se puede desvincular del documento de Workfront asociado. Esto no elimina el recurso original dentro de AEM. | ✓ | ✓ | ✓ |
| Añadir recursos de versiones recientes a AEM Assets desde Workfront | Cuando se añade una versión recién añadida a un documento en Workfront, un usuario puede enviar la nueva versión a AEM para reemplazar la versión existente. | ✓ | ✓ | ✓ |
| Recursos vinculados en Workfront cuando se hace clic en Direccionar usuario a AEM | Los usuarios son dirigidos a AEM para obtener una vista previa de un recurso vinculado desde Workfront. | ✓ | ✓ | Personalizado |
| Crear automáticamente carpetas de AEM vinculadas en Workfront | Crear automáticamente carpetas de AEM vinculadas en Workfront mediante estados de objetos. Organizar automáticamente AEM carpetas en función de los Portfolio, programas y proyectos de Workfront. | No | No | ✓ |
| Sincronización de comentarios | Sincronizar automáticamente los comentarios de los recursos [!DNL Workfront] a [!DNL Assets] | No | ✓ | ✓ |
| Asignación de metadatos de recursos de Workfront a AEM Assets | El objeto Workfront y las propiedades de formulario personalizadas pueden asignarse a propiedades de metadatos de AEM recurso. Los valores se insertan en el enlace o la carga inicial. | ✓ | ✓ | ✓ |
| Crear automáticamente Forms personalizado de documento en Workfront | Adjunte formularios personalizados a documentos, tareas y problemas de Workfront mediante flujos de trabajo AEM. | No | Agregue manualmente el formulario personalizado y la sincronización automatizada funcione | ✓ |
| Actualización automática bidireccional de metadatos entre AEM Assets y Workfront | Actualice automáticamente los metadatos entre AEM Assets y Workfront. | No | ✓ | ✓ |
| Asignación de metadatos de Workfront a carpetas de AEM Assets | Sincronice los metadatos del proyecto de Workfront con las carpetas de AEM vinculadas. | No | No | ✓ |
| Actualizaciones de metadatos de AEM con nuevas versiones | Se puede realizar una configuración en AEM para determinar si un recurso con una nueva versión en Workfront también inserta cambios en sus metadatos. | No | No | ✓ |
| Actualizar automáticamente AEM metadatos sobre los cambios en el Forms personalizado en Workfront | Workfront está configurado de tal manera que las propiedades de metadatos de AEM de recursos especificadas se asignan a un formulario personalizado de documento. Cuando un recurso está inicialmente vinculado o cuando se actualiza, los valores de estas propiedades de metadatos se copian en el campo de formulario personalizado del documento de Workfront correspondiente. Se debe tener cuidado para evitar que el cambio se AEM de vuelta a AEM como si fuera un cambio originado en Workfront. | No | ✓ | ✓ |
| Crear una nueva versión de prueba en recursos vinculados | Al vincular un recurso en Workfront, se puede generar una prueba automáticamente. | No | ✓ | Personalizado |
| Definir estado en objetos de Workfront | Definir estados de objetos de Workfront basados en condiciones configurables mediante flujos de trabajo AEM | No | No | ✓ |
| Publicar recursos en AEM Publish Environment o Brand Portal | Proporcione a los usuarios de Workfront la opción de publicar automáticamente los recursos vinculados en un entorno de publicación de AEM o Brand Portal. | No | No | ✓ |
