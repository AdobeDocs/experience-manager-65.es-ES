---
title: Visualización del avatar del usuario
seo-title: Visualización del avatar del usuario
description: Cómo personalizar el espacio de trabajo de AEM Forms para mostrar la imagen de un usuario que ha iniciado sesión.
seo-description: Cómo personalizar el espacio de trabajo de AEM Forms para mostrar la imagen de un usuario que ha iniciado sesión.
uuid: 2961dc93-f0d0-4842-80f1-3c239a20e348
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: aec03ea5-17a6-4775-92cb-2ad361895fdf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Visualización del avatar del usuario {#displaying-the-user-avatar}

El avatar del usuario que ha iniciado sesión se muestra en la esquina superior derecha del espacio de trabajo de AEM Forms. Además, los avatares de los informes directos de la jerarquía organizativa se muestran en la vista Administrador. Puede configurar el espacio de trabajo de AEM Forms para que seleccione las imágenes de usuario de la base de datos, por ejemplo, el servidor LDAP.

>[!NOTE]
>
>La proporción de aspecto admitida en las imágenes de usuario es 1:1.

1. Cree una DSC con los detalles mencionados en el paso siguiente. Para obtener más información, consulte el tema &quot;Desarrollo de componentes para AEM Forms&quot; en la guía [Programación con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63) .
1. En DSC, defina un nuevo SPI que exponga los métodos getCurrentUserImageUrl y getUserImageUrl para obtener una URL de imagen para un usuario de AEM Forms. A continuación se muestra un fragmento de código Java™ de muestra:

   ```as3
   public class DemoUserImageURLProviderService {
     public String getCurrentUserImageUrl()
     {
        // return the URL for profile Image of logged in user
     }
     public String getUserImageUrl(String principalOid)
     {
         // return the URL for profile Image for user represented by this principal Oid
      }
   }
   ```

1. Cree un archivo component.xml. Asegúrese de que la identificación de especificaciones es la que se muestra en el siguiente fragmento de código.

   El siguiente fragmento de código es un ejemplo. Personalícelo para adaptarlo a sus necesidades específicas.

   ```as3
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.DemoUsersComponent</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
       <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
       <services>
           <service name="DemoUserImageURLProviderService" title="Demo User ImageURL provider service" orchestrateable="false">
           <auto-deploy service-id="DemoUserImageURLProviderService" category-id="Demo Users Component DSC" major-version="1" minor-version="0" />
           <description>Service for resolving user image url.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.UserImageUrlProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.demousers.DemoUserImageURLProviderService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="false" name="getCurrentUserImageUrl" method="getCurrentUserImageUrl">
                   <output-parameter name="result" type="java.lang.String"/>
               </operation>
               <operation anonymous-access="false" name="getUserImageUrl"
   method="getUserImageUrl">
               <input-parameter name="principalOid" type="java.lang.String"/>
               <output-parameter name="result" type="java.lang.String"/>
               </operation>
           </operations>
           </service>
       </services>
   </component>
   ```

1. Implementar DSC a través de Workbench. Reinicie `ProcessManagementClientSessionService` el servicio.
1. Es posible que tenga que actualizar el explorador o cerrar la sesión o volver a iniciarla con el usuario.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
