---
title: Administración de tareas en una jerarquía organizativa mediante la vista Administrador
seo-title: Managing tasks in an organizational hierarchy using Manager View
description: Cómo los administradores y los jefes de organización pueden acceder y trabajar en las tareas de sus informes directos e indirectos en la pestaña Tareas pendientes del espacio de trabajo de AEM Forms.
seo-description: How managers and organization heads can access and work on the tasks of their direct and indirect reports in the To-do tab in AEM Forms workspace.
uuid: c44c55e6-6cc1-417d-8e89-c8d5c32914c8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2e60df86-d8ff-4cf9-b801-9559857b5ff4
docset: aem65
exl-id: e50974a7-01ac-4a08-bea2-df9cc975c69e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Administración de tareas en una jerarquía organizativa mediante la vista Administrador{#managing-tasks-in-an-organizational-hierarchy-using-manager-view}

En el espacio de trabajo de AEM Forms, los administradores ahora pueden acceder a las tareas asignadas a cualquier persona de su jerarquía (informes directos o indirectos) y realizar diversas acciones en ellas. Las tareas están disponibles en la ficha Tareas pendientes del espacio de trabajo de AEM Forms. Las acciones compatibles con las tareas de los informes directos son:

**Adelante** Reenviar una tarea desde un informe directo a cualquier usuario.

**Reclamación** Reclama una tarea de un informe directo.

**Reclamar y abrir** Reclame una tarea de un informe directo y ábrala automáticamente en la lista de tareas pendientes del administrador.

**Rechazar** Rechace una tarea reenviada a un informe directo por otro usuario. Esta opción está disponible para las tareas reenviadas por otros usuarios a un informe directo.

AEM Forms restringe el acceso de los usuarios solo a aquellas tareas para las que el usuario tiene control de acceso (ACL). Esta comprobación garantiza que un usuario solo pueda recuperar las tareas en las que tiene permisos de acceso. Mediante servicios web e implementaciones de terceros para definir la jerarquía, una organización puede personalizar la definición de administrador y dirigir informes para adaptarlos a sus necesidades.

1. Crear un DSC. Para obtener más información, consulte el tema &quot;Desarrollo de componentes para AEM Forms&quot; en [Programación con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63) guía.
1. En el DSC, defina un nuevo SPI para la administración de jerarquías a fin de definir jerarquías e informes directos dentro de los usuarios de AEM Forms. A continuación se muestra un fragmento de código Java™ de muestra.

   ```java
   public class MyHierarchyMgmtService
   {
        /*
       Input : Principal Oid for a livecycle user
       Output : Returns true when the user is either the service invoker OR his direct/indirect report.
       */
       boolean isInHierarchy(String principalOid) {
   
       }
   
       /*
       Input : Principal Oid for a livecycle user
       Output : List of principal Oids for direct reports of the livecycle user
       A user may get direct reports only for himself OR his direct/indirect reports.
       So the API is functionally equivalent to -
       isInHierarchy(principalOid) ? <return direct reports> : <return empty list>
       */
       List<String> getDirectReports(String principalOid) {
   
       }
   
       /*
       Returns whether a livecycle user has direct reports or not.
       It's functionally equivalent to -
       getDirectReports(principalOid).size()>0
       */
       boolean isManager(String principalOid) {
   
       }
   }
   ```

1. Cree un archivo component.xml. Asegúrese de que spec-id debe ser el mismo que se muestra en el fragmento de código siguiente. A continuación se muestra un fragmento de código de ejemplo que puede reutilizar.

   ```xml
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.SampleDSC</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
         <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
         <services>
           <service name="MyHierarchyMgmtService" title="My hierarchy management service" orchestrateable="false">
           <auto-deploy service-id="MyHierarchyMgmtService" category-id="Sample DSC" major-version="1" minor-version="0" />
           <description>Service for resolving hierarchy management.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.HierarchyManagementProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.hierarchymanagement.MyHierarchyMgmtService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="true" name="isInHierarchy" method="isInHierarchy">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.lang.Boolean"/>
               </operation>
               <operation anonymous-access="true" name="getDirectReports" method="getDirectReports">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.util.List"/>
               </operation>
               <operation anonymous-access="true" name="isManager" method="isManager">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.lang.Boolean"/>
               </operation>
               </operations>
               </service>
         </services>
   </component>
   ```

1. Implementar DSC a través de Workbench. Restart `ProcessManagementTeamTasksService` servicio.
1. Es posible que tenga que actualizar su navegador o cerrar la sesión/iniciar sesión con el usuario de nuevo.

La siguiente pantalla ilustra el acceso a las tareas de los informes directos y a las acciones disponibles.

![cu_manager_view](assets/cu_manager_view.png)

Acceso a tareas de informes directos y realización de tareas
