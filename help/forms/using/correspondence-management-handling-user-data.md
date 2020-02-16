---
title: Administración de correspondencia| Gestión de datos de usuario
seo-title: Administración de correspondencia| Gestión de datos de usuario
description: nulo
seo-description: nulo
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Administración de correspondencia| Gestión de datos de usuario {#correspondence-management-handling-user-data}

La gestión de correspondencia de AEM Forms le permite crear, administrar y optimizar correspondencia segura y personalizada con los clientes. Proporciona una interfaz de usuario intuitiva para que los usuarios comerciales creen correspondencias mediante bloques de contenido y elementos multimedia previamente aprobados. Para obtener más información sobre la creación de correspondencias, consulte [Crear correspondencia](/help/forms/using/create-correspondence.md).

Cuando un usuario comercial o un agente guarda una correspondencia como borrador o la envía, se guarda una instancia de carta en el repositorio de AEM. La instancia de carta incluye metadatos y datos de correspondencia.

>[!NOTE]
>
>En AEM 6.5 Forms, la gestión de correspondencia no está disponible de forma predeterminada. Si va a realizar la actualización desde una versión anterior de AEM Forms, instale el paquete de compatibilidad y migre los recursos de gestión de correspondencia para seguir utilizándolos en AEM 6.5 Forms. Para obtener más información, consulte Paquete [de compatibilidad](/help/forms/using/compatibility-package.md).

## Almacenes de datos y datos de usuarios {#data}

La gestión de correspondencia almacena datos para las letras de borrador y enviadas en el repositorio de AEM solo si la instancia de publicación está configurada para administrar instancias de cartas. Para obtener más información acerca de la configuración, consulte Propiedades [de configuración de Administración de](/help/forms/using/cm-configuration-properties.md)correspondencia.

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
   <td><p>Repositorio de AEM de instancias de publicación y creación especificadas en la configuración de replicación inversa</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>Repositorio de AEM de la instancia de creación de procesamiento remoto</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

En la ubicación del repositorio de AEM especificada anteriormente:

* `[yyyy]/[mm]/[dd]` es la estructura de nodos basada en la fecha en que se creó la instancia de carta
* `[node-id]` es el ID asignado a la carpeta que contiene la letra
* `[letter-instance-name]` es el nombre especificado al guardar o enviar una carta

En el nodo [letter-instance-name] , se crea la siguiente estructura de nodos y los datos de cada instancia de letra se almacenan en el repositorio de AEM:

| Nodo | Descripción |
|---|---|
| `extendedProperties` | Almacena las propiedades de metadatos de la instancia de carta. |
| `dataXML` | Almacena un archivo dataXML descargable que contiene los datos de la correspondencia en formato binario. |
| `processedXDP` | Incluye los detalles de la plantilla XDP utilizada para crear la carta enviada. Este nodo solo se crea para las correspondencias enviadas. |
| `submittedLetter` | Almacena los datos de carta enviados en formato binario descargable. Este nodo solo se crea para las correspondencias enviadas. |

## Acceso y eliminación de datos de usuario {#access-and-delete-user-data}

Puede acceder a los datos de envío y borrador de la correspondencia en los almacenes de datos configurados y, si es necesario, eliminarlos.

### Acceso a los datos de usuario {#access-user-data}

La administración de correspondencia proporciona API que puede utilizar para buscar y acceder a instancias de cartas de borrador y envío. Mediante las API, puede buscar y abrir instancias de carta utilizando el ID de instancia de carta o el usuario que guardó o envió la correspondencia. Para obtener más información, consulte [API para acceder a instancias](/help/forms/using/cm-apis-to-access-letter-instances.md)de letras.

También puede desplazarse a la instancia de carta en el repositorio de AEM mediante CRX DELite. Consulte Almacenes [de datos y datos de](/help/forms/using/correspondence-management-handling-user-data.md#data) usuario para obtener información sobre los datos almacenados y la ubicación del repositorio.

### Eliminar datos de usuario {#delete-user-data}

Para buscar una instancia de carta que contenga los datos de un usuario específico, puede:

* Utilice las API de administración de correspondencia si se conoce el nombre de la instancia de carta o el usuario que guardó el borrador o envió la correspondencia
* Utilice la búsqueda del repositorio de AEM utilizando información personal, como el nombre o el ID de correo electrónico, para encontrar el nodo en el que se almacena la información

Para eliminar completamente los datos de usuario de las correspondencias enviadas y borradas de los sistemas AEM, debe eliminar manualmente el nodo de instancia de carta de todas las instancias de AEM aplicables.
