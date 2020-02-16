---
title: 'Usar metadatos en una notificación por correo electrónico '
seo-title: 'Usar metadatos en una notificación por correo electrónico '
description: Utilizar metadatos para rellenar información en una notificación por correo electrónico del flujo de trabajo de formularios
seo-description: Utilizar metadatos para rellenar información en una notificación por correo electrónico del flujo de trabajo de formularios
uuid: 9075b64e-1934-44d5-8b16-aa6e95e93da9
topic-tags: publish
discoiquuid: d48b5137-c866-43cd-925b-7a6a8eac8c0b
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Usar metadatos en una notificación por correo electrónico {#use-metadata-in-an-email-notification}

Puede utilizar el paso Asignar tarea para crear y asignar tareas a un usuario o grupo. Cuando se asigna una tarea a un usuario o grupo, se envía una notificación por correo electrónico al usuario definido o a cada miembro del grupo definido. Una notificación [de](../../forms/using/use-custom-email-template-assign-task-step.md) correo electrónico típica contiene el vínculo de la tarea asignada y la información relacionada con la tarea.

Puede utilizar metadatos en una plantilla de correo electrónico para rellenar dinámicamente la información en una notificación por correo electrónico. Por ejemplo, el valor del título, la descripción, la fecha de vencimiento, la prioridad, el flujo de trabajo y la última fecha de la siguiente notificación por correo electrónico se selecciona de forma dinámica durante la ejecución (cuando se genera una notificación por correo electrónico).

![Plantilla de correo electrónico predeterminada](assets/default_email_template_metadata_new.png)

Los metadatos se almacenan en pares clave-valor. Puede especificar la clave en la plantilla de correo electrónico y sustituirla por un valor en tiempo de ejecución (cuando se genera una notificación por correo electrónico). Por ejemplo, en el ejemplo de código siguiente, &quot;$ {workitem_title}&quot; es una clave. Se sustituye por el valor &quot;Solicitud de préstamo&quot; en tiempo de ejecución.

```xml
subject=Task Assigned - ${workitem_title}

message=<html><body>\n\
 <table style="width: 480px; font-family: Helvetica, Arial, sans-serif; border: 0; padding: 0; vertical-align: top; text-align: left; word-wrap: break-word; margin: 16px auto; color:#323232; background-color:#FFFCF9; border-collapse: collapse;">\n\
  <tbody>\n\
   <tr>\n\
    <td style="height: 100px; width: 480px; background-color: #FFE0CB; border-top: 5pt solid black; font-family: Helvetica, Arial, sans-serif; font-weight: bold; font-size: 15px; line-height: 20px; padding: 12px; color: #707070;">\n\
      Sample Company\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="font-family: Helvetica, Arial, sans-serif; height: auto; background-color: #FFFCF9; padding: 32px 16px 20px 16px; ">\n\
     <pre style="font-size: 13px; font-family: Helvetica, Arial, sans-serif;  font-weight: normal; color: #323232;"> Hello ${workitem_assignee},\n\
 The following task has been assigned to you:</pre>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="width: 480px;">\n\
     <table style="height: auto; width: 480px; background-color:#FFFBF9; font-family: Helvetica, Arial, sans-serif; border-collapse: collapse;">\n\
      <tbody>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> TITLE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_title}</p>\n\
        </td>\n\
       </tr>\n\
                            <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DESCRIPTION</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_description}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DUE DATE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_due_date}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> PRIORITY</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_priority}</p>\n\
        </td>\n\
       </tr>\n\
       <tr>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> WORKFLOW</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_workflow}</p>\n\
        </td>\n\
       </tr>\n\
      </tbody>\n\
     </table>\n\
    </td>\n\
   </tr>\n\
   <tr style = "text-align: center; vertical-align: middle;">\n\
    <td style="padding:48px 0 72px 0;"> \n\
     <a href="${workitem_url}" target="_blank" style="background-color: #1EBBBB; font-size: 18px; line-height: 25px; font-weight: bold; color: #FFFFFF; text-decoration: none; padding: 15px 15px 15px 15px;">Open Task</a>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="border-top: solid 1px #EDEAE7; padding: 16px;">\n\
     <p><span style="font-size: 12px; font-weight: normal; font-style: italic; color: #919191;">This is an automatically generated email. Please do not reply to this email.</code></p>\n\
    </td>\n\
   </tr>\n\
  </tbody>\n\
 </table>\n\
</body>\n\
</html>\n\
```

## Uso de metadatos generados por el sistema en una notificación por correo electrónico {#using-system-generated-metadata-in-an-email-notification}

Una aplicación de AEM Forms proporciona varias variables de metadatos (pares clave-valor) predeterminadas. Puede utilizar estas variables en una plantilla de correo electrónico. El valor de la variable se basa en la aplicación de formularios asociada. En la tabla siguiente se muestran todas las variables de metadatos disponibles de forma predeterminada:

<table>
 <tbody> 
  <tr> 
   <td>Clave</td> 
   <td>Descripción</td> 
  </tr> 
  <tr> 
   <td>workitem_title</td> 
   <td>Título de la aplicación de formularios asociada.</td> 
  </tr> 
  <tr> 
   <td>workitem_url</td> 
   <td>URL para acceder a la aplicación de formularios asociada.</td> 
  </tr> 
  <tr> 
   <td>workitem_description</td> 
   <td>Descripción de la aplicación de formularios asociada.</td> 
  </tr> 
  <tr> 
   <td>workitem_priority</td> 
   <td>Prioridad especificada para la aplicación de formularios asociada.</td> 
  </tr> 
  <tr> 
   <td>workitem_due_date</td> 
   <td>Última fecha para actuar en la aplicación de formularios asociada.</td> 
  </tr> 
  <tr> 
   <td>workitem_workflow</td> 
   <td>Nombre del flujo de trabajo asociado a la aplicación de formularios.</td> 
  </tr> 
  <tr> 
   <td>workitem_assign_timestamp</td> 
   <td>Fecha y hora en que se asignó el elemento de flujo de trabajo al usuario asignado actual.</td> 
  </tr> 
  <tr> 
   <td>workitem_assignee</td> 
   <td>Nombre del cesionario actual.</td> 
  </tr> 
  <tr> 
   <td>host_prefix</td> 
   <td>URL del servidor de creación. Por ejemplo, https://10.41.42.66:4502<br /> </td> 
  </tr> 
  <tr> 
   <td>publish_prefix</td> 
   <td>URL del servidor de publicación. Por ejemplo, https://10.41.42.66:4503</td> 
  </tr> 
 </tbody> 
</table>

## Uso de metadatos personalizados en una notificación por correo electrónico {#using-custom-metadata-in-an-email-notification}

También puede utilizar metadatos personalizados en una notificación por correo electrónico. Los metadatos personalizados contienen información además de los metadatos generados por el sistema. Por ejemplo, los detalles de directivas recuperados de una base de datos. Puede utilizar un paquete ECMAScript o OSGi para agregar metadatos personalizados en crx-repository:

### Usar ECMAScript para agregar metadatos personalizados {#use-ecmascript-to-add-custom-metadata}

[ECMAScript](https://en.wikipedia.org/wiki/ECMAScript) es un lenguaje de secuencias de comandos. Se utiliza para secuencias de comandos de lado del cliente y aplicaciones de servidor. Siga estos pasos para utilizar ECMAScript y agregar metadatos personalizados para una plantilla de correo electrónico:

1. Inicie sesión en CRX DE con una cuenta administrativa. La dirección URL es https://[server]:[port]/crx/de/index.jsp

1. Vaya a /apps/fd/dashboard/scripts/metadataScripts. Cree un archivo con la extensión .ecma. Por ejemplo, usermetadata.ecma

   Si la ruta mencionada no existe, créela.

1. Agregue código al archivo .ecma que tenga la lógica de generar metadatos personalizados en pares clave-valor. Por ejemplo, el siguiente código ECMAScript genera metadatos personalizados para una póliza de seguro:

   ```
   function getUserMetaData()  {
       //Commented lines below provide an overview on how to set user metadata in map and return it.
       var HashMap = Packages.java.util.HashMap;
       var valuesMap = new HashMap();
       valuesMap.put("policyNumber", "2017568972695");
       valuesMap.put("policyHolder", "Adobe Systems");
   
       return valuesMap;
   }
   ```

1. Haga clic en Guardar todo. Ahora, el script está disponible para su selección en el modelo de flujo de trabajo de AEM.

   ![asignar tarea-metadatos](assets/assigntask-metadata.png)

1. (Opcional) Especifique el título de la secuencia de comandos:

   Si no especifica el título, el campo Metadatos personalizados muestra la ruta completa del archivo ECMAScript. Realice los siguientes pasos para especificar un título significativo para la secuencia de comandos:

   1. Expanda el nodo de secuencia de comandos, haga clic con el botón derecho en el nodo **[!UICONTROL jcr:content]** y, a continuación, haga clic en **[!UICONTROL Mezclas]**.
   1. Mezcla de tipos:título en el cuadro de diálogo Editar mezclas y haga clic **+**.
   1. Agregue una propiedad con los valores siguientes.

      | Nombre | jcr:title |
      |---|---|
      | Tipo | Cadena |
      | Value | Especifique el título de la secuencia de comandos. Por ejemplo, metadatos personalizados para el titular de la directiva. El valor especificado se muestra en el paso asignar tarea. |

### Usar un paquete OSGi y una interfaz Java para agregar metadatos personalizados {#use-an-osgi-bundle-and-java-interface-to-add-custom-metadata}

Puede utilizar la interfaz Java WorkitemUserMetadataService para agregar metadatos personalizados a las plantillas de correo electrónico. Puede crear un paquete OSGi que utilice la interfaz Java WorkitemUserMetadataService e implementarla en el servidor de AEM Forms. Permite seleccionar los metadatos en el paso Asignar tarea.

Para crear un paquete OSGi con la interfaz de Java, agregue archivos jar del SDK [del cliente de](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms y archivos jar [de](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) granito como dependencias externas al proyecto del paquete OSGi. Puede utilizar cualquier IDE de Java para crear un paquete OSGi. El siguiente procedimiento proporciona pasos para utilizar Eclipse para crear un paquete OSGi:

1. Abra Eclipse IDE. Vaya a Archivo > Nuevo proyecto.

1. En la pantalla Seleccionar un asistente, seleccione Mover proyecto y haga clic en Siguiente.

1. En el proyecto Nuevo visor, mantenga los valores predeterminados y haga clic en Siguiente. Seleccione un arquetipo y haga clic en Siguiente. Por ejemplo, maven-archetype-quickstart. Especifique el ID de grupo, el ID de artefacto, la versión y el paquete para el proyecto y haga clic en Finalizar. Se crea el proyecto.

1. Abra el archivo pom.xml para editarlo y sustituya todo el contenido del archivo por el siguiente:

   ```
   
   ```

1. Agregue código fuente que utilice la interfaz Java WorkitemUserMetadataService para agregar metadatos personalizados para las plantillas de correo electrónico. A continuación se muestra un código de muestra:

   ```java
   package com.aem.impl;
   
   import com.adobe.fd.workspace.service.external.WorkitemUserMetadataService;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Properties;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.osgi.framework.Constants;
   
   import java.util.HashMap;
   import java.util.Map;
   
   @Component
   @Service
   @Properties({
           @Property(name = Constants.SERVICE_DESCRIPTION, value = "A sample implementation of a user metadata service."),
           @Property(name = WorkitemUserMetadataService.SERVICE_PROPERTY_LABEL, value = "Default User Metadata Service")})
   
   public class WorkitemUserMetadataServiceImpl
     implements WorkitemUserMetadataService
   {
     public WorkitemUserMetadataServiceImpl() {}
   
     public Map<String, String> getUserMetadataMap()
     {
       HashMap<String, String> metadataMap = null;
       metadataMap = new HashMap();
       metadataMap.put("test_metadata", "tested-interface implementation");
       return metadataMap;
     }
   }
   ```

1. Abra un símbolo del sistema y vaya al directorio que contiene el proyecto del paquete OSGi. Utilice el siguiente comando para crear el paquete OSGi:

   `mvn clean install`

1. Cargue el paquete en un servidor de AEM Forms. Puede utilizar AEM Package Manager para importar el paquete al servidor de AEM Forms.

Una vez importado el paquete, puede seleccionar los metadatos en el paso Asignar tarea y utilizarlos en una plantilla de correo electrónico.
