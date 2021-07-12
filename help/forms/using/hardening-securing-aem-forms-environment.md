---
title: Endurecimiento y seguridad de los formularios AEM en el entorno OSGi
seo-title: Endurecimiento y seguridad de los formularios AEM en el entorno OSGi
description: Conozca las recomendaciones y prácticas recomendadas para proteger AEM Forms en el servidor OSGi.
seo-description: Conozca las recomendaciones y prácticas recomendadas para proteger AEM Forms en el servidor OSGi.
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
role: Admin
exl-id: 5da3cc59-4243-4098-b1e0-438304fcd0c5
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 0%

---

# Endurecimiento y seguridad de los formularios AEM en el entorno OSGi {#hardening-and-securing-aem-forms-on-osgi-environment}

Conozca las recomendaciones y prácticas recomendadas para proteger AEM Forms en el servidor OSGi.

La seguridad de un entorno de servidor es de suma importancia para una organización. En este artículo se describen recomendaciones y prácticas recomendadas para proteger los servidores que ejecutan AEM Forms. Este no es un documento completo que endurezca el host para su sistema operativo. En su lugar, en este artículo se describen varias opciones de configuración para reforzar la seguridad que debe implementar para mejorar la seguridad de la aplicación implementada. Sin embargo, para garantizar que los servidores de aplicaciones permanezcan seguros, también debe implementar procedimientos de supervisión, detección y respuesta de seguridad, además de las recomendaciones que se proporcionan en este artículo. El documento también contiene prácticas recomendadas y directrices para asegurar la información personal identificable (PII).

El artículo está dirigido a consultores, especialistas en seguridad, arquitectos de sistemas y profesionales de TI responsables de planificar la aplicación o el desarrollo de infraestructura y la implementación de AEM Forms. Estas funciones incluyen las siguientes funciones comunes:

* Los ingenieros de TI y de operaciones que deben implementar aplicaciones y servidores web seguros en sus propias organizaciones o en sus organizaciones de clientes.
* Arquitectos y planificadores responsables de planificar los esfuerzos arquitectónicos de los clientes en sus organizaciones.
* Especialistas en seguridad de TI que se centran en proporcionar seguridad en todas las plataformas de sus organizaciones.
* Consultores de Adobe y socios que requieren recursos detallados para clientes y socios.

La siguiente imagen muestra los componentes y protocolos que se utilizan en una implementación típica de AEM Forms, incluida la topología apropiada del cortafuegos:

![arquitectura típica](assets/typical-architecture.png)

AEM Forms es altamente personalizable y puede funcionar en muchos entornos diferentes. Es posible que algunas de las recomendaciones no sean aplicables a su organización.

## Capa de transporte segura {#secure-transport-layer}

Las vulnerabilidades de seguridad de capa de transporte están entre las primeras amenazas para cualquier servidor de aplicaciones orientado a Internet o a la intranet. En esta sección se describe el proceso de endurecimiento de los hosts de la red contra estas vulnerabilidades. Se ocupa de la segmentación de red, el refuerzo de la pila del Protocolo de control de transmisión/Protocolo Internet (TCP/IP) y el uso de cortafuegos para la protección del host.

### Límite de extremos abiertos  {#limit-open-endpoints}

Una organización puede tener un cortafuegos externo para restringir el acceso entre un usuario final y la granja de servidores de publicación de AEM Forms. La organización también puede tener un firewall interno para limitar el acceso entre un conjunto de servidores de publicación y otros dentro de los elementos de organización (por ejemplo, la instancia de autor, la instancia de procesamiento y las bases de datos). Permita que los cortafuegos permitan el acceso a un número limitado de URL de AEM Forms para usuarios finales y dentro de los elementos de la organización:

#### Configuración de cortafuegos externo  {#configure-external-firewall}

Puede configurar un cortafuegos externo para permitir que determinadas URL de AEM Forms accedan a Internet. Se requiere acceso a estas direcciones URL para rellenar o enviar un formulario adaptable, HTML5, carta de administración de correspondencia o para iniciar sesión en un servidor de AEM Forms:

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
     <li>/content/forms/formsets/profiles/</li> 
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

#### Configuración del cortafuegos interno  {#configure-internal-firewall}

Puede configurar el cortafuegos interno para permitir que ciertos componentes de AEM Forms (por ejemplo, instancia de autor, instancia de procesamiento, bases de datos) se comuniquen con el conjunto de servidores de publicación y otros componentes internos mencionados en el diagrama de topología:

<table> 
 <tbody>
  <tr>
   <td>Host<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Publicar granja (nodos de publicación)</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>Servidor de procesamiento</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Servidor de complementos del Forms Workflow (AEM Forms en el servidor JEE)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### Configuración de permisos del repositorio y listas de control de acceso (ACL) {#setup-repository-permissions-and-access-control-lists-acls}

De forma predeterminada, los recursos disponibles en los nodos de publicación son accesibles para todos. El acceso de solo lectura está habilitado para todos los recursos. Es necesario para habilitar el acceso anónimo. Si planea restringir la vista del formulario y enviar el acceso solo a usuarios autenticados, utilice un grupo común para permitir que solo los usuarios autenticados tengan acceso de solo lectura a los recursos disponibles en los nodos de publicación. Las siguientes ubicaciones/directorios contienen recursos de formulario que requieren refuerzo (acceso de solo lectura para usuarios autenticados):

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## Administrar de forma segura los datos de los formularios  {#securely-handle-forms-data}

AEM Forms almacena datos en ubicaciones predefinidas y carpetas temporales. Debe proteger los datos para evitar un uso no autorizado.

### Configuración de la limpieza periódica de la carpeta temporal {#setup-periodic-cleanup-of-temporary-folder}

Cuando se configuran formularios para archivos adjuntos, se verifican o se previsualizan componentes, los datos correspondientes se almacenan en los nodos de publicación en /tmp/fd/. Los datos se depuran periódicamente. Puede modificar el trabajo de depuración de datos predeterminado para que sea más agresivo. Para modificar el trabajo programado para purgar datos, abra AEM consola web, abra Tarea de limpieza temporal de almacenamiento de AEM Forms y modifique la expresión Cron.

En las situaciones mencionadas anteriormente, los datos solo se guardan para usuarios autenticados. Además, los datos están protegidos con listas de control de acceso (ACL). Por lo tanto, modificar la depuración de datos es un paso adicional para asegurar la información.

### Datos seguros guardados por la acción de envío del portal de formularios {#secure-data-saved-by-forms-portal-submit-action}

De forma predeterminada, la acción de envío de formularios del portal de formularios adaptables guarda los datos en el repositorio local del nodo de publicación. Los datos se guardan en /content/forms/fp. **No se recomienda almacenar datos en instancias de publicación.**

Puede configurar el servicio de almacenamiento para que envíe mensajes por cable al clúster de procesamiento sin guardar nada localmente en el nodo de publicación. El clúster de procesamiento reside en una zona segura detrás del firewall privado y los datos siguen siendo seguros.

Utilice las credenciales del servidor de procesamiento para AEM servicio de configuración de DS para publicar datos del nodo de publicación en el servidor de procesamiento. Se recomienda utilizar las credenciales de un usuario no administrativo restringido con acceso de lectura y escritura al repositorio del servidor de procesamiento. Para obtener más información, consulte [Configuración de servicios de almacenamiento para borradores y envíos](/help/forms/using/configuring-draft-submission-storage.md).

### Datos seguros gestionados por el modelo de datos de formulario (FDM) {#secure-data-handled-by-form-data-model-fdm}

Utilice cuentas de usuario con privilegios mínimos requeridos para configurar orígenes de datos para el modelo de datos de formulario (FDM). El uso de cuentas administrativas puede proporcionar acceso abierto a entidades de esquema y metadatos a usuarios no autorizados.\
La integración de datos también proporciona métodos para autorizar solicitudes de servicio de FDM. Puede insertar mecanismos de autorización antes y después de la ejecución para validar una solicitud. Las solicitudes de servicio se generan marcando el prefijo de un formulario, enviando un formulario e invocando servicios a través de una regla.

**Autorización previa al proceso:** puede utilizar la autorización previa al proceso para validar la autenticidad de una solicitud antes de ejecutarla. Puede utilizar entradas, servicios y detalles de solicitud para permitir o detener la ejecución de la solicitud. Puede devolver una excepción de integración de datos OPERATION_ACCESS_DENIED si se detiene la ejecución. También puede modificar la solicitud del cliente antes de enviarla para su ejecución. Por ejemplo, cambiar la entrada y añadir información adicional.

**Autorización posterior al proceso:**  puede utilizar la autorización posterior al proceso para validar y controlar los resultados antes de devolver los resultados al solicitante. También puede filtrar, recortar e insertar datos adicionales en los resultados.

### Limitar el acceso de los usuarios {#limit-user-access}

Se requiere un conjunto diferente de personalidades de usuario para las instancias de autor, publicación y procesamiento. No ejecute ninguna instancia con credenciales de administrador.

**En una instancia de publicación:**

* Solo los usuarios de un grupo de usuarios de formularios pueden obtener una vista previa, crear borradores y enviar formularios.
* Solo los usuarios del grupo cm-user-agent pueden obtener una vista previa de las cartas de gestión de correspondencia.
* Deshabilite todos los accesos anónimos no esenciales.

**En una instancia de autor:**

* Hay un conjunto diferente de grupos predefinidos con privilegios específicos para cada persona. Asignar usuarios al grupo.

   * Usuario de un grupo de usuarios de formularios:

      * puede crear, rellenar, publicar y enviar un formulario.
      * no se puede crear un formulario adaptable basado en XDP.
      * no tienen permisos para escribir secuencias de comandos para formularios adaptables.
      * no se puede importar XDP o cualquier paquete que contenga XDP
   * Un usuario de grupos de usuarios avanzados de formularios puede crear, rellenar, publicar y enviar todo tipo de formularios, escribir secuencias de comandos para formularios adaptables e importar paquetes que contengan XDP.
   * Un usuario de template-authors y template-power-user pueden obtener una vista previa y crear una plantilla.
   * Un usuario de fdm-authors puede crear y modificar un modelo de datos de formulario.
   * Un usuario del grupo cm-user-agent puede crear, previsualizar y publicar cartas de gestión de correspondencia.
   * Un usuario del grupo de editores de flujos de trabajo puede crear una aplicación de bandeja de entrada y un modelo de flujo de trabajo.


**Al procesar el autor:**

* Para casos de uso de almacenamiento y envío remotos, cree un usuario con permisos de lectura, creación y modificación en la ruta content/form/fp del repositorio crx.
* Agregue un usuario al grupo de usuarios del flujo de trabajo para permitir que un usuario utilice AEM aplicaciones de bandeja de entrada.

## Elementos de intranet seguros de un entorno de AEM Forms {#secure-intranet-elements-of-an-aem-forms-environment}

En general, los clústeres de procesamiento y el complemento de Forms Workflow (AEM Forms en JEE) se ejecutan detrás de un servidor de seguridad. Así que se consideran seguros. Puede seguir realizando algunos pasos para endurecer estos entornos:

### Clúster de procesamiento seguro {#secure-processing-cluster}

Un clúster de procesamiento se ejecuta en modo de autor, pero no lo utiliza para actividades de desarrollo. No permita que se incluya a un usuario normal en los grupos de autores de contenido y usuarios de formularios de un clúster de procesamiento.

### Usar AEM prácticas recomendadas para proteger un entorno de AEM Forms {#use-aem-best-practices-to-secure-an-aem-forms-environment}

Este documento proporciona instrucciones específicas para el entorno de AEM Forms. Debe asegurarse de que la instalación de AEM subyacente sea segura cuando se implemente. Para obtener instrucciones detalladas, consulte la documentación [AEM Security Checklist](/help/sites-administering/security-checklist.md).
