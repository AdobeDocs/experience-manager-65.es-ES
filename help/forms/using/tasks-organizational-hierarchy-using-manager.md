---
title: Administración de tareas en una jerarquía organizativa mediante la vista Administrador
seo-title: Administración de tareas en una jerarquía organizativa mediante la vista Administrador
description: Cómo los administradores y los jefes de organización pueden acceder a las tareas de sus informes directos e indirectos y trabajar en ellas en la ficha Tareas pendientes del espacio de trabajo de AEM Forms.
seo-description: Cómo los administradores y los jefes de organización pueden acceder a las tareas de sus informes directos e indirectos y trabajar en ellas en la ficha Tareas pendientes del espacio de trabajo de AEM Forms.
uuid: c44c55e6-6cc1-417d-8e89-c8d5c32914c8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2e60df86-d8ff-4cf9-b801-9559857b5ff4
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Administración de tareas en una jerarquía organizativa mediante la vista Administrador{#managing-tasks-in-an-organizational-hierarchy-using-manager-view}

En el espacio de trabajo de AEM Forms, los administradores ahora pueden acceder a las tareas asignadas a cualquier persona de su jerarquía (informes directos o indirectos) y realizar varias acciones en ellas. Las tareas están disponibles en la ficha Tareas pendientes del espacio de trabajo de AEM Forms. Las acciones admitidas en las tareas de los informes directos son:

**Reenviar** una tarea desde un informe directo a cualquier usuario.

**Reclamar** una tarea de un informe directo.

**Reclamar y abrir** Reclamar una tarea de un informe directo y abrirlo automáticamente en la lista de tareas pendientes del administrador.

**Rechazar** Rechazar una tarea reenviada a un informe directo por otro usuario. Esta opción está disponible para las tareas reenviadas por otros usuarios a un informe directo.

AEM Forms restringe el acceso de los usuarios únicamente a las tareas para las que el usuario tiene control de acceso (ACL). Esta comprobación garantiza que un usuario solo pueda recuperar las tareas en las que tiene permisos de acceso. Mediante el uso de implementaciones y servicios Web de terceros para definir la jerarquía, una organización puede personalizar la definición de administrador y dirigir informes para adaptarlos a sus necesidades.

1. Crear un DSC. Para obtener más información, consulte el tema &quot;Desarrollo de componentes para AEM Forms&quot; en la guía [Programación con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63) .
1. En DSC, defina un nuevo SPI para la administración de jerarquías a fin de definir jerarquías e informes directos dentro de los usuarios de AEM Forms. A continuación se muestra un fragmento de código Java™ de muestra.

   ```as3
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

1. Cree un archivo component.xml. Asegúrese de que la identificación de especificaciones debe ser la misma que se muestra en el siguiente fragmento de código. A continuación se muestra un fragmento de código de muestra que puede reutilizar.

   ```as3
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

1. Implementar DSC a través de Workbench. Reinicie `ProcessManagementTeamTasksService` el servicio.
1. Es posible que tenga que actualizar el explorador o cerrar la sesión o volver a iniciarla con el usuario.

La siguiente pantalla ilustra el acceso a las tareas de los informes directos y a las acciones disponibles.

![cu_manager_view](assets/cu_manager_view.png)

Acceder a las tareas de los informes directos y actuar en función de las tareas

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
