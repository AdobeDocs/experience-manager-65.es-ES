---
title: Gestión de correspondencia | Gestión de datos de usuario
seo-title: Gestión de correspondencia | Gestión de datos de usuario
description: Gestión de correspondencia | Gestión de datos de usuario
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
role: Admin
exl-id: a0c6a02c-47a3-4e70-a14c-953ee016b8e4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Gestión de correspondencia | Gestión de datos de usuario {#correspondence-management-handling-user-data}

La gestión de correspondencia de AEM Forms le permite crear, administrar y optimizar las correspondencias de clientes seguras y personalizadas. Proporciona una interfaz de usuario intuitiva para que los usuarios empresariales creen correspondencias utilizando bloques de contenido y elementos multimedia previamente aprobados. Para obtener más información sobre la creación de correspondencia, consulte [Crear correspondencia](/help/forms/using/create-correspondence.md).

Cuando un usuario empresarial o un agente guarda una correspondencia como borrador o la envía, se guarda una instancia de carta en el repositorio de AEM. La instancia de carta incluye datos de correspondencia y metadatos.

>[!NOTE]
>
>En AEM 6.5 Forms, la administración de correspondencia no está disponible de forma predeterminada. Si está actualizando desde una versión anterior de AEM Forms, instale el paquete de compatibilidad y migre los recursos de administración de correspondencia para seguir usándolos en AEM 6.5 Forms. Para obtener más información, consulte [Paquete de compatibilidad](/help/forms/using/compatibility-package.md).

## Almacenamiento de datos y datos de usuarios {#data}

La gestión de correspondencia almacena datos para cartas en borrador y enviadas en AEM repositorio solo si la instancia de publicación está configurada para administrar instancias de carta. Para obtener más información sobre la configuración, consulte [Propiedades de configuración de Gestión de correspondencia](/help/forms/using/cm-configuration-properties.md).

Según la persistencia del almacén de datos configurada para la implementación de AEM, los borradores y los datos de correspondencia enviados se almacenan en las siguientes ubicaciones.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo de persistencia</strong></p> </td>
   <td><p><strong>Almacén de datos</strong></p> </td>
   <td><p><strong>Lugar de residencia</strong></p> </td>
  </tr>
  <tr>
   <td><p>Predeterminado</p> </td>
   <td><p>AEM repositorio de instancias de publicación y de autor especificado en la configuración de replicación inversa</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>AEM repositorio de la instancia de autor del procesamiento remoto</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

En la ubicación del repositorio AEM especificada arriba:

* `[yyyy]/[mm]/[dd]` es la estructura del nodo basada en la fecha en la que se creó la instancia de letra
* `[node-id]` es el ID asignado a la carpeta que contiene la carta
* `[letter-instance-name]` es el nombre especificado al guardar o enviar una carta

En el nodo [letter-instance-name], se crea la siguiente estructura de nodos y los datos de cada instancia de letra se almacenan en el repositorio de AEM:

| Nodo | Descripción |
|---|---|
| `extendedProperties` | Almacena las propiedades de metadatos de la instancia de carta. |
| `dataXML` | Almacena un archivo dataXML descargable que contiene los datos de correspondencia en formato binario. |
| `processedXDP` | Incluye los detalles de la plantilla XDP utilizada para crear la carta enviada. Este nodo solo se crea para las correspondencias enviadas. |
| `submittedLetter` | Almacena los datos de la carta enviada en formato binario descargable. Este nodo solo se crea para las correspondencias enviadas. |

## Acceso y eliminación de datos de usuario {#access-and-delete-user-data}

Puede acceder a los datos de correspondencia en borrador y enviados en los almacenes de datos configurados y, si es necesario, eliminarlos.

### Acceso a los datos de usuario {#access-user-data}

La gestión de correspondencia proporciona API que puede utilizar para buscar y acceder a instancias de carta en borrador y enviadas. Con las API, puede encontrar y abrir instancias de carta utilizando el ID de instancia de la carta o el usuario que guardó o envió la correspondencia. Para obtener más información, consulte [APIs para acceder a instancias de carta](/help/forms/using/cm-apis-to-access-letter-instances.md).

Alternativamente, puede navegar a la instancia de carta en AEM repositorio utilizando CRX DELite. Consulte [Almacenamiento de datos y datos de usuario](/help/forms/using/correspondence-management-handling-user-data.md#data) para obtener información sobre los datos almacenados y la ubicación del repositorio.

### Eliminar datos de usuario {#delete-user-data}

Para buscar una instancia de carta que contenga los datos de un usuario específico, puede:

* Utilice las API de gestión de correspondencia si se conoce el nombre de la instancia de carta o el usuario que guardó el borrador o envió la correspondencia
* Utilice AEM búsqueda del repositorio utilizando información personal, como el ID de correo electrónico o el nombre, para encontrar el nodo en el que se almacena la información

Para eliminar por completo los datos de usuario de las correspondencias en borrador y enviadas desde AEM sistemas, debe eliminar manualmente el nodo de instancia de letra de todas las instancias de AEM aplicables.
