---
title: Seleccionar dinámicamente un usuario o grupo para los pasos del flujo de trabajo centrado en AEM Forms
seo-title: Seleccionar dinámicamente un usuario o grupo para los pasos del flujo de trabajo centrado en AEM Forms
description: 'Obtenga información sobre cómo seleccionar un usuario o grupo para un flujo de trabajo de AEM Forms en tiempo de ejecución. '
seo-description: 'Obtenga información sobre cómo seleccionar un usuario o grupo para un flujo de trabajo de AEM Forms en tiempo de ejecución. '
uuid: 19dcbda4-61af-40b3-b10b-68a341373410
content-type: troubleshooting
topic-tags: publish
discoiquuid: e6c9f3bb-8f20-4889-86f4-d30578fb1c51
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Seleccionar dinámicamente un usuario o grupo para los pasos del flujo de trabajo centrado en AEM Forms {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

Obtenga información sobre cómo seleccionar un usuario o grupo para un flujo de trabajo de AEM Forms en tiempo de ejecución.

En las organizaciones grandes, existen requisitos para seleccionar usuarios de forma dinámica para un proceso. Por ejemplo, seleccionar un agente de campo para servir a un cliente en función de la proximidad del agente al cliente. En este escenario, el agente se selecciona dinámicamente.

Asignar tarea y los pasos de Adobe Sign de flujos de trabajo centrados en [formularios en OSGi](/help/forms/using/aem-forms-workflow.md) proporcionan opciones para seleccionar dinámicamente un usuario. Puede utilizar paquetes de ECMAScript o OSGi para seleccionar dinámicamente un usuario asignado para el paso Asignar Tarea o para seleccionar firmantes para el paso Firmar Documento.

## Utilice ECMAScript para seleccionar dinámicamente un usuario o grupo {#use-ecmascript-to-dynamically-select-a-user-or-group}

ECMAScript es un lenguaje de secuencias de comandos. Se utiliza para secuencias de comandos de lado del cliente y aplicaciones de servidor. Siga estos pasos para seleccionar dinámicamente un usuario o un grupo mediante ECMAScript:

1. Abra CRXDE Lite. La dirección URL es `https://'[server]:[port]'/crx/de/index.jsp`
1. Cree un archivo con la extensión .ecma en la siguiente ruta. Si la ruta (estructura de nodos) no existe, créela:

   * (Ruta para el paso Asignar Tarea) `/apps/fd/dashboard/scripts/participantChooser`
   * (paso Ruta de firma) `/apps/fd/workflow/scripts/adobesign`

1. Añada ECMAScript, que tiene la lógica de seleccionar dinámicamente un usuario, al archivo .ecma. Haga clic en **[!UICONTROL Guardar todo]**.

   Para ver secuencias de comandos de ejemplo, consulte [Ejemplo de ECMAScripts para seleccionar dinámicamente un usuario o un grupo](/help/forms/using/dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group).

1. Añada el nombre para mostrar de la secuencia de comandos. Este nombre se muestra en los pasos del flujo de trabajo. Para especificar el nombre:

   1. Expanda el nodo de secuencia de comandos, haga clic con el botón derecho en el nodo **[!UICONTROL jcr:content]** y, a continuación, haga clic en **[!UICONTROL Mezclas]**.
   1. Añada la propiedad en el cuadro de diálogo Editar mezclas y haga clic en `mix:title` Aceptar ****.
   1. Añada la siguiente propiedad en el nodo jcr:content de la secuencia de comandos:

      | Nombre | Tipo | Value |
      |--- |--- |--- |
      | jcr:title | Cadena | Especifique el nombre de la secuencia de comandos. Por ejemplo, elija el agente de campo más cercano. Este nombre se muestra en los pasos Asignar Tarea y Firmar Documento. |

   1. Haga clic en **Guardar todo**. La secuencia de comandos está disponible para su selección en los componentes de Flujo de trabajo de AEM.

      ![script](assets/script.png)

### Ejemplo de ECMAScripts para elegir dinámicamente un usuario o un grupo {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

El siguiente ejemplo de ECMAScript selecciona dinámicamente un usuario asignado para el paso Asignar Tarea. En esta secuencia de comandos, se selecciona un usuario en función de la ruta de la carga útil. Antes de utilizar esta secuencia de comandos, asegúrese de que todos los usuarios mencionados en la secuencia de comandos existen en AEM. Si los usuarios mencionados en la secuencia de comandos no existen en AEM, el proceso relacionado puede fallar.

```
function getParticipant() {

var workflowData = graniteWorkItem.getWorkflowData();

if (workflowData.getPayloadType() == "JCR_PATH") { 

var path = workflowData.getPayload().toString(); 
     if (path.indexOf("/content/geometrixx/en") == 0) {
    return "user1";
    } 
   else {
              return "user2";
            }
}
}
```

El siguiente ejemplo de ECMAScript selecciona dinámicamente un usuario asignado para el paso Adobe Sign. Antes de utilizar la siguiente secuencia de comandos, asegúrese de que la información del usuario (direcciones de correo electrónico y números de teléfono) que se menciona en la secuencia de comandos es correcta. Si la información del usuario que se menciona en la secuencia de comandos es incorrecta, el proceso relacionado puede fallar.

>[!NOTE]
>
>Al utilizar ECMAScript para Adobe Sign, la secuencia de comandos debe estar ubicada en crx-repository en /apps/fd/workflow/scripts/adobesign/ y debe tener una función denominada getAdobeSignRecipients para devolver una lista de los usuarios.

```
function getAdobeSignRecipients() {

    var recipientSetInfos = new Packages.java.util.ArrayList();

    var recipientInfoSet = new com.adobe.aem.adobesign.recipient.RecipientSetInfo();
    var recipientInfoList = new Packages.java.util.ArrayList();
    var recipientInfo = new com.adobe.aem.adobesign.recipient.RecipientInfo();

    var email;
    var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.PHONE;  
    //var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.NONE;
    var securityOptions = null;

    var phoneNumber = "123456789";
    var countryCode = "+1";
    var recipientPhoneInfo = new Array();
    recipientPhoneInfo.push(new com.adobe.aem.adobesign.recipient.RecipientPhoneInfo(phoneNumber, countryCode));

     securityOptions = new com.adobe.aem.adobesign.recipient.RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
    
    email = "example@example.com";
    
    recipientInfo.setEmail(email);
    recipientInfo.setSecurityOptions(securityOptions);
    
    recipientInfoList.add(recipientInfo);
    recipientInfoSet.setMemberInfos(recipientInfoList);
    recipientSetInfos.add(recipientInfoSet);

    return recipientSetInfos;

}
```

## Utilizar la interfaz de Java para elegir dinámicamente un usuario o grupo {#use-java-interface-to-dynamically-choose-a-user-or-group}

Puede utilizar la interfaz Java [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) para elegir dinámicamente un usuario o un grupo para Adobe Sign y asignar pasos de Tarea. Puede crear un paquete OSGi que utilice la interfaz Java [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) e implementarla en el servidor de AEM Forms. La opción está disponible para su selección en los componentes Asignar Tarea y Adobe Sign de Flujo de trabajo de AEM.

Para compilar el ejemplo de código que se muestra a continuación, se requieren archivos jar del SDK [del cliente de](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms y archivos jar [de](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) granito. Añada estos archivos jar como dependencias externas al proyecto del paquete OSGi. Puede utilizar cualquier IDE de Java para crear un paquete OSGi. El siguiente procedimiento proporciona pasos para utilizar Eclipse para crear un paquete OSGi:

1. Abra Eclipse IDE. Vaya a **[!UICONTROL Archivo]**> **[!UICONTROL Nuevo proyecto]**.
1. En la pantalla Seleccionar un asistente, seleccione **[!UICONTROL Mover proyecto]** y haga clic en **[!UICONTROL Siguiente]**.
1. En el proyecto Nuevo visor, mantenga los valores predeterminados y haga clic en **[!UICONTROL Siguiente]**. Seleccione un arquetipo y haga clic en **[!UICONTROL Siguiente]**. Por ejemplo, maven-archetype-quickstart. Especifique el ID **** de grupo, el ID **[!UICONTROL de]** artefacto, la **[!UICONTROL versión]** y el **[!UICONTROL paquete]** para el proyecto y haga clic en **[!UICONTROL Finalizar]**. Se crea el proyecto.
1. Abra el archivo pom.xml para editarlo y sustituya todo el contenido del archivo por el siguiente:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>getAgent</groupId>
       <artifactId>assignToAgent</artifactId>
       <version>1.0</version>
       <packaging>bundle</packaging><!-- packaging type bundle is must -->
   
       <name>assignToAgent</name>
       <url>https://maven.apache.org</url>
       <repositories>
           <repository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk-test</artifactId>
               <version>4.0.70</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.granite</groupId>
               <artifactId>com.adobe.granite.workflow.api</artifactId>
               <version>1.0.0</version>
           </dependency>
   
           <dependency>
               <groupId>org.osgi</groupId>
               <artifactId>org.osgi.core</artifactId>
               <version>4.2.0</version>
               <scope>provided</scope>
           </dependency>
   
           <dependency>
               <groupId>org.apache.felix</groupId>
               <artifactId>org.apache.felix.scr.annotations</artifactId>
               <version>1.7.0</version>
   
           </dependency>
   
           <dependency>
               <groupId>org.apache.sling</groupId>
               <artifactId>org.apache.sling.api</artifactId>
               <version>2.2.0</version>
   
           </dependency>
   
       </dependencies>
   
       <!-- ====================================================================== -->
       <!-- B U I L D D E F I N I T I O N -->
       <!-- ====================================================================== -->
       <build>
           <plugins>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-bundle-plugin</artifactId>
                   <extensions>true</extensions>
                   <configuration>
                       <instructions>
                           <Bundle-SymbolicName>com.aem.assigntoAgent-bundle</Bundle-SymbolicName>
                       </instructions>
                   </configuration>
               </plugin>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-scr-plugin</artifactId>
                   <version>1.9.0</version>
                   <executions>
                       <execution>
                           <id>generate-scr-descriptor</id>
                           <goals>
                               <goal>scr</goal>
                           </goals>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

1. Añada el código fuente que utiliza la interfaz Java [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) para elegir dinámicamente un usuario o un grupo para el paso Asignar tarea. Para obtener el código de muestra, consulte [Ejemplo para elegir dinámicamente un usuario o un grupo mediante la interfaz](#-sample-scripts-for)de Java.
1. Abra un símbolo del sistema y vaya al directorio que contiene el proyecto del paquete OSGi. Utilice el siguiente comando para crear el paquete OSGi:

   `mvn clean install`

1. Cargue el paquete en un servidor de AEM Forms. Puede utilizar AEM Package Manager para importar el paquete al servidor de AEM Forms.

Después de importar el paquete, la opción de elegir la interfaz de Java para seleccionar dinámicamente un usuario o un grupo estará disponible en para los pasos de Adobe Sign y Asignar Tarea.

### Ejemplo de código Java para elegir dinámicamente un usuario o un grupo {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

El siguiente código de muestra selecciona dinámicamente un usuario asignado para el paso Adobe Sign. El código se utiliza en un paquete OSGi. Antes de utilizar el código que aparece a continuación, asegúrese de que la información del usuario (direcciones de correo electrónico y números de teléfono) que se menciona en el código sea correcta. Si la información de usuario mencionada en el código es incorrecta, el proceso relacionado puede fallar.

```java
/*************************************************************************

 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2016 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
 
package com.aem.impl;

import java.util.ArrayList;
import java.util.List;

import com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod;
import com.adobe.aem.adobesign.recipient.RecipientInfo;
import com.adobe.aem.adobesign.recipient.RecipientPhoneInfo;
import com.adobe.aem.adobesign.recipient.RecipientSecurityOption;
import com.adobe.aem.adobesign.recipient.RecipientSetInfo;
import com.adobe.fd.workflow.adobesign.api.RecipientInfoSpecifier;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

/**
 * <code>DummyRecipientInfoSpecifier implementation. A sample code to write implementation of RecipientInfoSpecifier to choose recipients/code>...
 */
@Service

@Component(metatype = false)
public class DummyRecipientChoser implements RecipientInfoSpecifier {
    public List<RecipientSetInfo> getAdobeSignRecipients(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {

        List<RecipientSetInfo> recipientSetInfos = new ArrayList<RecipientSetInfo>();

                //First Recipient

                RecipientSetInfo recipientInfoSet1 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList = new ArrayList<RecipientInfo>();
                RecipientInfo recipientInfo1 = new RecipientInfo();//Member to first recipient

                String email;

                RecipientAuthenticationMethod recipientAuthenticationMethod = RecipientAuthenticationMethod.WEB_IDENTITY;
                RecipientSecurityOption securityOptions = null;

                String phoneNumber = "123456789";
                String countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo = new RecipientPhoneInfo[1];  //if multiple phone numbers, size>1
                recipientPhoneInfo[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
                 
                email = "example@example.com";

                recipientInfo1.setEmail(email);
                recipientInfo1.setSecurityOptions(securityOptions);

                recipientInfoList.add(recipientInfo1);  //Add member

                recipientInfoSet1.setMemberInfos(recipientInfoList);

                //Second Recipient

                RecipientSetInfo recipientInfoSet2 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList2 = new ArrayList<RecipientInfo>();

                recipientAuthenticationMethod = RecipientAuthenticationMethod.PHONE;
                securityOptions = null;
                 
                phoneNumber = "987654321";//"0123456789";

                countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo_1 = new RecipientPhoneInfo[1];
                recipientPhoneInfo_1[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo_1 , null);
                 
                email = "example2@example.com";//"dummymail2@domain.com";

                RecipientInfo recipientInfo2  = new RecipientInfo();
                recipientInfo2.setEmail(email);
                recipientInfo2.setSecurityOptions(securityOptions);

                recipientInfoList2.add(recipientInfo2);  //Add member

                recipientInfoSet2.setMemberInfos(recipientInfoList2);

                //*********************************

                recipientSetInfos.add(recipientInfoSet1); 
                recipientSetInfos.add(recipientInfoSet2);

        return recipientSetInfos;

    }

}
```

