---
title: Asignación de grupos de usuarios personalizados en AEM 6.5
seo-title: Asignación de grupos de usuarios personalizados en AEM 6.5
description: Descubra cómo funciona la asignación de grupos de usuarios personalizados en AEM.
seo-description: Descubra cómo funciona la asignación de grupos de usuarios personalizados en AEM.
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
translation-type: tm+mt
source-git-commit: a268b7046430cc17c8b59b9306cf3533d73bb4a2

---


# Asignación de grupos de usuarios personalizados en AEM 6.5 {#custom-user-group-mapping-in-aem}

## Comparación del contenido de JCR relacionado con CUG {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>Versiones anteriores de AEM</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comentarios</strong></td>
  </tr>
  <tr>
   <td><p>Propiedad: cq:cugEnabled</p> <p>Declarando tipo de nodo: N/D, propiedad residual</p> </td>
   <td><p>Autorización:</p> <p>Nodo: rep:cugPolicy de tipo de nodo rep:CugPolicy</p> <p>Declarando tipo de nodo: rep:CugMixin</p> <p> </p> <p> </p> <p> </p> Autenticación:</p> <p>Tipo de mezcla: granite:AuthenticationRequired</p> </td>
   <td><p>Para restringir el acceso de lectura, se aplica una directiva CUG dedicada al nodo de destino.</p> <p>NOTA: Las directivas solo se pueden aplicar en las rutas configuradas admitidas.</p> <p>Los nodos con el nombre rep:cugPolicy y el tipo rep:CugPolicy están protegidos y no se pueden escribir con llamadas regulares a la API de JCR; utilice la administración de control de acceso JCR en su lugar.</p> <p>Consulte <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">esta página</a> para obtener más información.</p> <p>Para hacer cumplir los requisitos de autenticación en un nodo, basta con agregar el tipo de mezcla granite:AuthenticationRequired.</p> <p>NOTA: Solo se respetan por debajo de las rutas configuradas admitidas.</p> </td>
  </tr>
  <tr>
   <td><p>Propiedad: cq:cugPrincipals</p> <p>Declarando tipo de nodo: NA, propiedad residual</p> </td>
   <td><p>Propiedad: rep:mainNames</p> <p>Declarando tipo de nodo: rep:CugPolicy</p> </td>
   <td><p>La propiedad que contiene los nombres de los principales a los que se permite leer el contenido debajo del CUG restringido está protegida y no se puede escribir mediante llamadas regulares a la API de JCR; utilice la administración de control de acceso JCR en su lugar.</p> <p>Consulte <a href="https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbitapi/src/main/java/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.java">esta página</a> para obtener más detalles sobre la implementación.</p> </td>
  </tr>
  <tr>
   <td><p>Propiedad: cq:cugLoginPage</p> <p>Declarando tipo de nodo: NA, propiedad residual</p> </td>
   <td><p>Propiedad: granite:loginPath (opcional)</p> <p>Declarando tipo de nodo: granite:AuthenticationRequired</p> </td>
   <td><p>Un nodo JCR con el tipo de mezcla granite:AuthenticationRequired definido, puede definir opcionalmente una ruta de inicio de sesión alternativa.</p> <p>NOTA: Solo se respetan por debajo de las rutas configuradas admitidas.</p> </td>
  </tr>
  <tr>
   <td><p>Propiedad: cq:cugRealm</p> <p>Declarando tipo de nodo: NA, propiedad residual</p> </td>
   <td>ND</td>
   <td>Ya no se admite con la nueva implementación.</td>
  </tr>
 </tbody>
</table>

## Comparación de los servicios de OSGi {#comparison-of-osgi-services}

**Versiones anteriores de AEM**

Etiqueta: Compatibilidad con el grupo cerrado de usuarios (CUG) de Adobe Granite

Nombre: com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* Etiqueta: Configuración de Apache Jackrabbit Oak CUG

   Nombre: org.apache.jackrabbit.oak.spi.security.authorized.cug.impl.CugConfiguration

   ConfigurationPolicy = REQUIRED

* Etiqueta: Lista de exclusión de Apache Jackrabbit Oak CUG

   Nombre: org.apache.jackrabbit.oak.spi.security.authorized.cug.impl.CugExcludeImpl

   ConfigurationPolicy = REQUIRED

* Nombre: com.adobe.granite.auth.requirements.impl.RequirementService
* Etiqueta: Requisito de autenticación de Adobe Granite y controlador de ruta de inicio de sesión

   Nombre: com.adobe.granite.auth.requirements.impl.DefaultRequirementHandler

   ConfigurationPolicy = REQUIRED

**Comentarios**

* Configuración de la autorización de CUG y habilitar/deshabilitar la evaluación.
Servicio para configurar la lista de exclusión de los principales que no deben verse afectados por la autorización de CUG.

   >[!NOTE] Si CugExcludeImpl no está configurado, CugConfiguration volverá al valor predeterminado.

   Es posible conectar una implementación personalizada de CugExclude en caso de necesidades especiales.

* Componente OSGi que implementa LoginPathProvider que expone una ruta de inicio de sesión coincidente al elemento LoginSelectorHandler. Tiene una referencia obligatoria a un RequirementHandler que se utiliza para registrar al observador que escucha los requisitos de autenticación modificados almacenados en el contenido mediante el tipo de mezcla granite:AuthenticationRequired.
* Componente OSGi que implementa RequirementHandler que notifica al SlingAuthenticator los cambios en los requisitos de autenticación.

   Dado que la directiva de configuración de este componente es REQUERIDA, solo se activará si se especifica un conjunto de rutas admitidas.

   Al habilitar el servicio, se iniciará RequirementService.

<!-- nested tables not supported - text above is the table>
<table>
 <tbody>
  <tr>
   <td><strong>Older AEM Versions</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comments</strong></td>
  </tr>
  <tr>
   <td><p>Label: Adobe Granite Closed User Group (CUG) Support</p> <p>Name: com.day.cq.auth.impl.CugSupportImpl</p> </td>
   <td><p>Label: Apache Jackrabbit Oak CUG Configuration</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
    <td><p>Label: Apache Jackrabbit Oak CUG Exclude List</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl</p> <p>ConfigurationPolicy = REQUIRED</p> <p> </p> <p> </p> <p> </p> <p> </p> </td>
      </tr>
      <tr>
       <td>Name: com.adobe.granite.auth.requirement.impl.RequirementService</td>
      </tr>
      <tr>
       <td><p>Label: Adobe Granite Authentication Requirement and Login Path Handler</p> <p>Name: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
      </tr>
     </tbody>
    </table> </td>
   <td>
     <tbody>
      <tr>
       <td>Configuration of the CUG authorization and enable/disable the evaluation.</td>
      </tr>
      <tr>
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation in case of special needs.</p> </td>
      </tr>
      <tr>
       <td>OSGi component implementing LoginPathProvider that exposes a matching login path to the LoginSelectorHandler. It has a mandatory reference to a RequirementHandler which is used to register the observer that listens to changed auth requirements stored in the content by the means of the granite:AuthenticationRequired mixin type. </td>
      </tr>
      <tr>
       <td><p>OSGi component implementing RequirementHandler that notifies the SlingAuthenticator about changes to authrequirements.</p> <p>As configuration policy for this component is REQUIRE it will only be activated if a set of supported paths is specified.</p> <p>Enabling the service will launch the RequirementService.</p> </td>
      </tr>
     </tbody>
     </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

