---
title: Endurecimiento y seguridad de los formularios AEM en el entorno OSGi
seo-title: Endurecimiento y seguridad de los formularios AEM en el entorno OSGi
description: Conozca las recomendaciones y prácticas recomendadas para proteger AEM Forms en el servidor OSGi.
seo-description: Conozca las recomendaciones y prácticas recomendadas para proteger AEM Forms en el servidor OSGi.
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 0%

---


# Endurecimiento y seguridad de los formularios AEM en el entorno OSGi {#hardening-and-securing-aem-forms-on-osgi-environment}

Conozca las recomendaciones y prácticas recomendadas para proteger AEM Forms en el servidor OSGi.

La seguridad de un entorno de servidor es de suma importancia para una organización. Este artículo describe las recomendaciones y prácticas recomendadas para proteger los servidores que ejecutan AEM Forms. No se trata de un documento completo de endurecimiento del host para su sistema operativo. En su lugar, este artículo describe varios ajustes de seguridad que debe implementar para mejorar la seguridad de la aplicación implementada. Sin embargo, para garantizar que los servidores de aplicaciones se mantengan seguros, también debe implementar procedimientos de supervisión, detección y respuesta de seguridad, además de las recomendaciones que se proporcionan en este artículo. El documento también contiene las mejores prácticas y directrices para asegurar la información personal identificable.

El artículo está dirigido a consultores, especialistas en seguridad, arquitectos de sistemas y profesionales de TI que son responsables de planificar el desarrollo de aplicaciones o infraestructura y la implementación de AEM Forms. Estas funciones incluyen las siguientes funciones comunes:

* Ingenieros de TI y operaciones que deben implementar aplicaciones web y servidores seguros en sus propias organizaciones o en sus organizaciones de clientes.
* Arquitectos y planificadores que son responsables de planificar los esfuerzos arquitectónicos para los clientes en sus organizaciones.
* Especialistas en seguridad de TI que se centran en proporcionar seguridad en todas las plataformas dentro de sus organizaciones.
* Consultores de Adobes y socios que requieren recursos detallados para clientes y socios.

La siguiente imagen muestra los componentes y protocolos que se utilizan en una implementación típica de AEM Forms, incluida la topología adecuada del cortafuegos:

![arquitectura típica](assets/typical-architecture.png)

AEM Forms es altamente personalizable y puede funcionar en muchos entornos diferentes. Es posible que algunas de las recomendaciones no sean aplicables a su organización.

## Capa de transporte seguro {#secure-transport-layer}

Las vulnerabilidades de seguridad del nivel de transporte están entre las primeras amenazas para cualquier servidor de aplicaciones orientado a Internet o a la intranet. Esta sección describe el proceso de endurecimiento de los hosts de la red contra estas vulnerabilidades. Se ocupa de la segmentación de red, el endurecimiento de la pila del Protocolo de control de transmisión/Protocolo de Internet (TCP/IP) y el uso de firewalls para la protección del host.

### Límite de los extremos abiertos {#limit-open-endpoints}

Una organización puede tener un servidor de seguridad externo para restringir el acceso entre un usuario final y la granja de publicaciones de AEM Forms. La organización también puede tener un servidor de seguridad interno para limitar el acceso entre un conjunto de servidores de publicación y otros elementos de la organización (por ejemplo, instancia de autor, instancia de procesamiento, bases de datos). Permitir servidores de seguridad para habilitar el acceso a un número limitado de direcciones URL de AEM Forms para usuarios finales y dentro de los elementos de la organización:

#### Configurar firewall externo {#configure-external-firewall}

Puede configurar un servidor de seguridad externo para permitir que determinadas direcciones URL de AEM Forms tengan acceso a Internet. Se requiere acceso a estas direcciones URL para rellenar o enviar un formulario adaptable, HTML5, una carta de administración de correspondencia o para iniciar sesión en un servidor de AEM Forms:

<table> 
 <tbody>
  <tr>
   <td>Componente</td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Formularios adaptables</td> 
   <td>
    <ul> 
     <li>/content/dam/formsanddocuments/AF_PATH/jcr:content</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Formularios HTML5</td> 
   <td>
    <ul> 
     <li>/content/forms/formsets/perfiles/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Gestión de correspondencia </td> 
   <td>
    <ul> 
     <li>/aem/forms/createcorrespondence* </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Forms Portal </td> 
   <td>
    <ul> 
     <li>/content/forms/portal/</li> 
     <li>/libs/cq/ui/widgets*</li> 
     <li>/libs/cq/security/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td> Aplicación de AEM Forms</td> 
   <td>
    <ul> 
     <li>/j_security_check*</li> 
     <li>/soap/services/AuthenticationManagerService</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

#### Configurar firewall interno {#configure-internal-firewall}

Puede configurar el cortafuegos interno para permitir que determinados componentes de AEM Forms (por ejemplo, instancia de autor, instancia de procesamiento, bases de datos) se comuniquen con el conjunto de servidores de publicación y otros componentes internos mencionados en el diagrama de topología:

<table> 
 <tbody>
  <tr>
   <td>Host<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Publicar granja (nodos de publicación)</td> 
   <td>/bin/received</td> 
  </tr>
  <tr>
   <td>Servidor de procesamiento</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Forms Workflow Add-on server (AEM Forms en el servidor JEE)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### Configurar permisos del repositorio y listas de control de acceso (ACL) {#setup-repository-permissions-and-access-control-lists-acls}

De forma predeterminada, los recursos disponibles en los nodos de publicación son accesibles para todos. El acceso de solo lectura está habilitado para todos los recursos. Se requiere para habilitar el acceso anónimo. Si tiene pensado restringir la vista de formularios y enviar el acceso solo a usuarios autenticados, utilice un grupo común para permitir que solo los usuarios autenticados tengan acceso de solo lectura a los recursos disponibles en los nodos de publicación. Las siguientes ubicaciones/directorios contienen recursos de formulario que requieren endurecimiento (acceso de solo lectura para usuarios autenticados):

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## Administrar de forma segura los datos de formularios {#securely-handle-forms-data}

AEM Forms almacena datos en ubicaciones predefinidas y carpetas temporales. Debe proteger los datos para evitar un uso no autorizado.

### Configurar la limpieza periódica de la carpeta temporal {#setup-periodic-cleanup-of-temporary-folder}

Cuando se configuran formularios para archivos adjuntos, componentes de verificación o previsualización, los datos correspondientes se almacenan en los nodos de publicación en /tmp/fd/. Los datos se purgan periódicamente. Puede modificar el trabajo de depuración de datos predeterminado para que sea más agresivo. Para modificar el trabajo programado para depurar datos, abra AEM consola web, abra la Tarea de limpieza temporal de Almacenamientos de AEM Forms y modifique la expresión Cron.

En los casos mencionados, los datos se guardan únicamente para usuarios autenticados. Además, los datos están protegidos con listas de control de acceso (ACL). Por lo tanto, modificar la depuración de datos es un paso adicional para asegurar la información.

### Datos seguros guardados por la acción de envío del portal de formularios {#secure-data-saved-by-forms-portal-submit-action}

De forma predeterminada, la acción de envío del portal de formularios de formularios adaptables guarda los datos en el repositorio local del nodo de publicación. Los datos se guardan en /content/forms/fp. **No se recomienda almacenar datos en una instancia de publicación.**

Puede configurar el servicio de almacenamiento para que envíe mensajes a través del cable al clúster de procesamiento sin guardar nada localmente en el nodo de publicación. El clúster de procesamiento reside en una zona segura detrás del servidor de seguridad privado y los datos siguen siendo seguros.

Utilice las credenciales del servidor de procesamiento para AEM servicio de configuración de DS para enviar datos desde el nodo de publicación al servidor de procesamiento. Se recomienda utilizar las credenciales de un usuario restringido no administrativo con acceso de lectura y escritura en el repositorio del servidor de procesamiento. Para obtener más información, consulte [Configuración de los servicios de almacenamiento para borradores y envíos](/help/forms/using/configuring-draft-submission-storage.md).

### Datos seguros gestionados por el modelo de datos de formulario (FDM) {#secure-data-handled-by-form-data-model-fdm}

Utilice cuentas de usuario con privilegios mínimos requeridos para configurar orígenes de datos para el modelo de datos de formulario (FDM). El uso de una cuenta administrativa puede proporcionar acceso abierto a los metadatos y a las entidades de esquema a usuarios no autorizados.\
La integración de datos también proporciona métodos para autorizar solicitudes de servicio FDM. Puede insertar mecanismos de autorización previa y posterior a la ejecución para validar una solicitud. Las solicitudes de servicio se generan anteponiendo un formulario, enviando un formulario e invocando servicios a través de una regla.

**Autorización previa al proceso:** puede utilizar la autorización previa al proceso para validar la autenticidad de una solicitud antes de ejecutarla. Puede utilizar entradas, servicios y detalles de solicitud para permitir o detener la ejecución de la solicitud. Puede devolver una excepción de integración de datos OPERATION_ACCESS_DENIED si se detiene la ejecución. También puede modificar la solicitud del cliente antes de enviarla para su ejecución. Por ejemplo, cambiar la entrada y agregar información adicional.

**Autorización posterior al proceso:** puede utilizar la autorización posterior al proceso para validar y controlar los resultados antes de devolverlos al solicitante. También puede filtrar, eliminar e insertar datos adicionales en los resultados.

### Limitar el acceso del usuario {#limit-user-access}

Se requiere un conjunto diferente de usuarios para crear, publicar y procesar instancias. No ejecute ninguna instancia con credenciales de administrador.

**En una instancia de publicación:**

* Solo los usuarios del grupo de usuarios de formularios pueden crear previsualizaciones, crear borradores y enviar formularios.
* Sólo los usuarios del grupo cm-user-agent pueden previsualización cartas de gestión de correspondencia.
* Deshabilite todos los accesos anónimos no esenciales.

**En una instancia de autor:**

* Hay un conjunto diferente de grupos predefinidos con privilegios específicos para cada persona. Asignar usuarios al grupo.

   * Un usuario del grupo de usuarios de formularios:

      * puede crear, rellenar, publicar y enviar un formulario.
      * no se puede crear un formulario adaptable basado en XDP.
      * no tiene permisos para escribir secuencias de comandos para formularios adaptables.
      * no se puede importar XDP o cualquier paquete que contenga XDP
   * Un usuario de grupos de usuarios avanzados de formularios puede crear, rellenar, publicar y enviar todos los tipos de formularios, escribir secuencias de comandos para formularios adaptables e importar paquetes que contengan XDP.
   * Un usuario de generadores de plantillas y de plantilla y usuario avanzado puede crear una previsualización y crear una plantilla.
   * Un usuario de fdm-author puede crear y modificar un modelo de datos de formulario.
   * Un usuario del grupo cm-user-agent puede crear, previsualización y publicar cartas de gestión de correspondencia.
   * Un usuario del grupo de editores de flujo de trabajo puede crear una aplicación de bandeja de entrada y un modelo de flujo de trabajo.


**Al procesar el autor:**

* Para casos de uso de almacenamiento y envío remotos, cree un usuario con permisos de lectura, creación y modificación en la ruta de contenido/formulario/fp del repositorio crx.
* Añada el usuario a un grupo de usuarios de flujo de trabajo para permitir que un usuario utilice AEM aplicaciones de bandeja de entrada.

## Elementos de intranet seguros de un entorno de AEM Forms {#secure-intranet-elements-of-an-aem-forms-environment}

En general, los clústeres de procesamiento y el complemento Forms Workflow (AEM Forms en JEE) se ejecutan detrás de un servidor de seguridad. Así que se consideran seguros. Puede seguir realizando algunos pasos para endurecer estos entornos:

### Clúster de procesamiento seguro {#secure-processing-cluster}

Un clúster de procesamiento se ejecuta en el modo de creación, pero no lo utiliza para actividades de desarrollo. No permita que un usuario normal se incluya en los grupos de autores de contenido y usuarios de formularios de un clúster de procesamiento.

### UTILICE AEM prácticas recomendadas para asegurar un entorno de AEM Forms {#use-aem-best-practices-to-secure-an-aem-forms-environment}

Este documento proporciona instrucciones específicas para AEM Forms entorno. Debe asegurarse de que la instalación de AEM subyacente es segura cuando se implementa. Para obtener instrucciones detalladas, consulte la documentación de [AEM Security Checklist](/help/sites-administering/security-checklist.md).
