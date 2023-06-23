---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6,5
description: Encuentre información de la versión, novedades, instrucciones de instalación y una lista de cambios detallada para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: fed4e110-9415-4740-aba1-75da522039a9
source-git-commit: 316b93575d9cbbc2c5a64bc5030b036a2ade5b92
workflow-type: tm+mt
source-wordcount: '3777'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager] Notas de la versión del paquete de servicio más reciente de 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=7yhrWb&nav=MTVfe0U0RjdDQUM3LTZCQ0EtNDk1Qy04Mjc1LTM2MUJEMzE1OEVGN30 -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, June 1, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.17.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del paquete de servicio |
| Fecha | jueves, 25 de mayo de 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## ¿Qué incluye? [!DNL Experience Manager] 6.5.17.0 {#what-is-included-in-aem-6517}

[!DNL Experience Manager] 6.5.17.0 incluye nuevas funciones, mejoras clave solicitadas por el cliente, correcciones de errores y mejoras de rendimiento, estabilidad y seguridad que se han publicado desde la publicación inicial de 6.5 en abril de 2019. [Instalar este Service Pack](#install) el [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Algunas de las funciones y mejoras clave de esta versión son las siguientes:

* **Mejoras en la experiencia de búsqueda** : Ahora puede realizar rápidamente las siguientes operaciones en los recursos que se muestran en los resultados de búsqueda:
   * Creación de un flujo de trabajo
   * Crear una versión
   * Relacionar o desrelacionar recursos

  No es necesario desplazarse a la ubicación del recurso y ver sus propiedades para realizar estas operaciones.
* **Dynamic Media _Instantánea_**: Experimente con imágenes de prueba o URL de Dynamic Media para ver la salida de diferentes modificadores de imagen y optimizaciones de imágenes inteligentes para el tamaño de archivo (con entrega WebP y AVIF), el ancho de banda de la red y la proporción de píxeles del dispositivo. Consulte [Instantánea Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).
* **Streaming DASH con Dynamic Media** - Se ha lanzado la compatibilidad con el nuevo protocolo (DASH - Dynamic Adaptive Streaming over HTTP) para el streaming adaptable en la entrega de vídeo de Dynamic Media (con CMAF habilitado). Disponible ahora para todas las regiones, [habilitado mediante un ticket de asistencia](/help/assets/video.md#enable-dash-on-your-account-enable-dash).
* **Integración de Experience Manager Sites y fragmentos de contenido con Dynamic Media de próxima generación de recursos** : Los usuarios de Experience Manager Assets as a Cloud Service Next-Generation Dynamic Media ahora pueden utilizar esos recursos alojados en la nube para la creación y el envío con instancias on-premise o Managed Services de Experience Manager Sites 6.5.

**AEM Forms**

* **[Forms AEM adaptable en el editor de páginas de la](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)** AEM : ahora puede utilizar el Editor de páginas de para crear y agregar rápidamente varios formularios a las páginas de Sites. Esta capacidad permite a los autores de contenido crear experiencias de captura de datos sin problemas dentro de las páginas de Sites mediante la potencia de los componentes de los formularios adaptables, incluido el comportamiento dinámico, las validaciones, la integración de datos, la generación de documentos de registro y la automatización de los procesos empresariales. Puede hacer lo siguiente:
   * Cree un formulario adaptable arrastrando y soltando componentes de formulario en el componente Contenedor de Forms adaptable en el editor de AEM Sites o en los fragmentos de experiencias.
   * Utilice el asistente de Forms adaptable dentro del editor de AEM Sites para poder crear formularios independientes de cualquier página de Sites, lo que le proporciona la libertad de reutilizar dichos formularios en varias páginas.
   * Agregue varios formularios a una página de Sites, lo que optimizará la experiencia del usuario y proporcionará la buena flexibilidad.
* **[Compatibilidad con reCAPTCHA Enterprise en Experience Manager Forms](/help/forms/using/captcha-adaptive-forms.md)**: Se ha añadido compatibilidad con reCAPTCHA Enterprise en Experience Manager Forms, que proporciona una protección mejorada contra actividades fraudulentas y spam, además de la compatibilidad con reCAPTCHA v2 de Google.
* **[Compatibilidad con Adobe Acrobat Sign para Administración Pública con Experience Manager Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**: AEM Forms ahora se integra con Adobe Acrobat Sign para Administración Pública (compatible con FedRAMP). Esta integración proporciona un nivel avanzado de cumplimiento y seguridad para las firmas electrónicas con envíos de formularios adaptables para cuentas asociadas con el gobierno (departamentos y agencias gubernamentales). La integración con Adobe Acrobat Sign para Administración Pública permite a los socios de Adobe y a los clientes gubernamentales utilizar firmas electrónicas en Forms adaptable para algunas de las líneas de negocio más importantes y sensibles. Este nivel adicional de seguridad garantiza que todas las firmas electrónicas cumplan plenamente con la normativa FedRAMP Moderate, lo que proporciona tranquilidad a los clientes gubernamentales de Adobe.
* **[Habilitar la integración de Salesforce con Experience Manager Forms para el intercambio de datos](/help/forms/using/oauth2-client-credentials-flow-for-server-to-server-integration.md)**: configure la integración entre Experience Manager Forms y la aplicación Salesforce mediante el flujo de credenciales del cliente OAuth 2.0. Esta capacidad permite la autenticación y autorización seguras y directas de la aplicación y permite una comunicación fluida sin la participación del usuario.
* **Optimización y funcionalidad mejorada del motor de flujo de trabajo**: aumente el rendimiento de los motores de flujo de trabajo minimizando el número de instancias de flujo de trabajo. Además de `COMPLETED` y `RUNNING` valores de estado, el flujo de trabajo también admite tres nuevos valores de estado: `ABORTED`, `SUSPENDED`, y `FAILED`.


<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets]{#assets-6517}

* Cuando publica más de 40 PDF simultáneamente, [!DNL Experience Manager] deja de responder y deja de estar disponible durante un tiempo. (ASSETS-21789)
* Si ha iniciado sesión como usuario de prueba, no puede ver los recursos relacionados con un recurso concreto al hacer clic en las propiedades de un recurso. (ASSETS-21648)
* Al editar Recursos mediante `Desktop Actions`, si intenta registrar más de cinco recursos a la vez, `Limit Reached` se muestra el error y se retiran los recursos seleccionados. (ASSETS-21121)
* No se pueden ordenar los recursos por su nombre en una colección. (ASSETS-20924)
* No se pueden establecer dimensiones en Recursos de un tipo de formato de imagen. (ASSETS-20835)
* El texto de la información del objeto y su fondo en el campo Buscar/agregar dirección de correo electrónico no muestran la relación de contraste adecuada al compartir un vínculo. (ASSETS-17347)
* Cuando expanda `Notifications`Sin embargo, el texto no se muestra correctamente debido al espaciado de párrafo. (ASSETS-17345)
* Cuando copia un recurso en la colección, `Public Collection` La casilla de verificación no se muestra correctamente. (ASSETS-17343)
* Los elementos utilizan atributos ARIA sin una función. (ASSETS-17325,ASSETS-17323)
* El vínculo no es descriptivo al expandir `Notifications`. (ASSETS-17283)
* Cuando navegue y expanda el [!DNL Smart Crop] , el contenido aparece como una lista, pero no se marca como una lista sin ordenar. Como resultado, el lector de pantalla no reconoce la lista sin ordenar y la lee como texto sin formato. (ASSETS-17247)
* El `Sort By` La etiqueta no está asociada a su lista desplegable correspondiente. Como resultado, el lector de pantalla no reconoce las opciones desplegables. (ASSETS-17239)
* No se puede mover hacia adelante o hacia atrás con las teclas de tabulación o flecha del teclado cuando intenta agregar un usuario mediante la función `Add user` cuadro combinado. (ASSETS-17233)
* El lector de pantalla no transmite correctamente la información del paso Flujos de trabajo (ASSETS-17285).
* Cuando navegue a `Saved Searches` Cuadro combinado, ni el nombre ni la función tienen etiquetas asignadas. (ASSETS-17329)
* Al navegar `Collection` y coloque el puntero sobre el texto *Miembros*, el texto no aparece como marcado. Como resultado, el lector de pantalla no reconoce el texto del encabezado y lo lee como texto sin formato. (ASSETS-17245)
* No se puede acceder `View Settings` opción que utiliza las teclas de desplazamiento hacia abajo o hacia arriba desde el teclado. (ASSETS-17257)
* No se puede almacenar en déclencheur un flujo de trabajo para varios recursos seleccionados que se encuentran en filtros de búsqueda. (ASSETS-7689)
* Al seleccionar un recurso (o varios) en los resultados de búsqueda, la opción relacionar o no relacionar no está visible. Pero la opción está disponible, de lo contrario. (ASSETS-7679)
* El panel Filtros de búsqueda se abre solo una vez después de iniciar sesión y no se abre si sale de la página de búsqueda y vuelve a ejecutar la búsqueda. (ASSETS-7671)
* El cuadro combinado de correo electrónico no muestra la relación de contraste adecuada al compartir un vínculo. (ASSETS-17349)

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST 
* When you select any file in a Collection and click `Download`, and then navigate to the email checkbox and expand it, regular text and email link is not recognizable due to background color. (ASSETS-17349) 
* When you navigate to `Smart Crop` option, the screen reader does not announce the expand or collapse state of the button. (ASSETS-17335)-->

## [!DNL Assets] - [!DNL Dynamic Media]{#dm-6517}

* La conexión con Dynamic Media se interrumpe cuando ya existe una configuración de nube de Dynamic Media. (ASSETS-23057)
* Rendimiento mejorado al examinar las carpetas con muchos vídeos de Dynamic Media y problema resuelto que no se puede cargar en la vista de la tarjeta de carpetas. (ASSETS-23016)
* Los tokens de vista previa se eliminan de `error.log` que se puede utilizar para solicitar contenido seguro desde los servidores de prueba seguros. (ASSETS-22685)
* Representación de la miniatura del PDF añadiendo una sombra. Se ha actualizado la versión 4.0.1680232194 de Gibson lib para resolver el problema de procesamiento de miniaturas del PDF. (ASSETS-22585)
* El modo híbrido de Dynamic Media ahora es compatible con la versión 8.0.1 de New Relic Agent (ASSETS-22578).
* Ahora se respetan las ACL del Experience Manager (Listas de control de acceso) al previsualizar archivos Dynamic Media en el Experience Manager. (ASSETS-21628)
* Los lectores de pantalla no navegan a elementos ocultos cuando el usuario intenta navegar con la tecla de flecha abajo o Tab. (ASSETS-5617)
* Interfaz de usuario de perfil de imagen restringida para cultivos inteligentes con el mismo nombre, la misma dimensión o ambos. (ASSETS-16997)
* La anchura y altura predeterminadas ahora se establecen en 50 píxeles para los recortes inteligentes en la interfaz de usuario del perfil de imagen. (ASSETS-16997)

## [!DNL Commerce]{#commerce-6517}

* Las etiquetas que se mueven son residuos recogidos pero los productos siguen haciendo referencia a ellas en `/var`. (CQ-4351337)

## [!DNL Forms]{#forms-6517}

* AEM Después de actualizar a Paquete de servicio de 6.5.15.0, los formularios de HTML5 no funcionan o no se cargan correctamente en el explorador Edge con el modo de compatibilidad con IE. (FORMS-8526, FORMS-8523)
* AEM Cuando un usuario aplica el paquete de servicio 6.5.16.0 de, el editor de reglas no se abre. (FORMS-8290)
* Cuando se aplica el número máximo de dígitos de validación a un componente Cuadro numérico, se produce un error. (FORMS-7938)
* Al crear instrucciones de comunicación interactivas, el componente de gráfico del PDF no se genera correctamente. (FORMS-7827, FORMS-8297)
* La recolección de basura de Java™ no puede borrar el montón de generación antigua en un servidor OSGi de Experience Manager Forms. (FORMS-8207)
* Cuando un usuario actualiza al paquete de servicio del Experience Manager 6.5.16.0, las propiedades de metadatos CRX faltan después del envío. (FORMS-8205)
* Cuando un usuario deshabilita el componente Selector de fecha en un formulario adaptable, aún se puede editar. (FORMS-7804)
* En Experience Manager 6.5.16.0 Forms Service Pack, cuando un usuario intenta editar los coordinadores de conjuntos de directivas, la opción Administrador de documentos siempre permanece sin marcar. (FORMS-7775, FORMS-8599)
* Cuando un usuario actualiza al paquete de servicio de Experience Manager 6.5.16.0, el método &quot;GuideNode.externalize&quot; que gestiona las cadenas que deben traducirse deja de funcionar. (FORMS-7709)
* En el `Assign task` Paso, cuando un usuario selecciona &quot;Enviar correo electrónico de notificación&quot; e invoca el flujo de trabajo, el texto no se muestra correctamente en el correo electrónico recibido. Se reciben los signos de interrogación en lugar del texto del correo electrónico recibido. (FORMS-7675)
* El documento de registro se está localizando parcialmente. (FORMS-7674, FORMS-7573)
* Un usuario no puede editar conjuntos de directivas aunque se le asignen permisos específicos. (FORMS-7665)
* Cuando un usuario en la `forms-users` El grupo intenta crear un formulario, la instancia de Experience Manager Forms se bloquea. (FORMS-7629)
* Cuando el usuario hace clic en los botones Restablecer, Guardar o Enviar de un formulario adaptable, no se muestra ningún mensaje en la pantalla. (FORMS-7524)
* Para mejorar el rendimiento de la conversión de PDF Generator en un paquete de servicio de Experience Manager 6.5.16.0, el intervalo de suspensión se puede configurar. (FORMS-6752)
* La opción de alternancia sigue siendo la misma, pero la visibilidad del campo cambia incluso cuando un usuario arrastra el cursor ligeramente. (FORMS-6728)
* Cuando el usuario actualiza al paquete de servicio del Experience Manager 6.5.15.0, la redirección deja de funcionar cuando se procesa un formulario adaptable en Internet Explorer. (FORMS-6725)
* La herramienta PAC 2021 para todos los objetos de fondo de un formulario de PDF creado por un Diseñador de Experience Manager devuelve un error como `Path object not tagged`. (FORMS-6707)
* Cuando un usuario aplica un filtro en la bandeja de entrada, genera un `NullPointerException` error. (FORMS-6706)
* Cuando un usuario importa un archivo de plantilla (.tds) con fragmentos a los que se hace referencia, se bloquea un Diseñador de Experience Manager. (FORMS-6702)
* En caso de que el usuario cree un PDF estático mediante el servicio Output en un Experience Manager Forms Designer 6.5, se produce un error como `OCCD (optional content configuration dictionary) contains AS key`. (FORMS-6691)
* Cuando el usuario crea un flujo de trabajo simple y añade una variable simple, `set variable mapping` se produce un error. (FORMS-5819)
* Cuando un usuario intenta generar un PDF mediante el servicio Output, aunque esté marcado como `PDF/A-1a`, una comprobación de conformidad mediante el`Preflight` falla el servicio. (LC-3920837)
* Después de instalar un paquete de servicio de Experience Manager 6.5.16.0, no se puede abrir un diseñador de Experience Manager. (LC-3921000)
* Cuando un usuario agrega una casilla de verificación y un botón de radio, la estructura de un árbol de etiquetas no se genera según los estándares del PDF. (LC-3920838)
* En caso de que un usuario genere un PDF estático utilizando la incrustación y el subconjunto de fuentes a través del servicio de salida, el PDF resultante contendrá solo las fuentes incrustadas. (LC-3920963)
* El texto en hebreo se muestra incorrectamente en formato RTL. (LC-3919632)
* Cuando un usuario actualiza al paquete de servicio de Experience Manager 6.5.16.0 en un servidor JBoss® Turnkey, el servicio Signature no invoca. El error encontrado es: `java.lang.ClassCastException: com.adobe.xfa.TextNode cannot be cast to com.adobe.xfa.Element`. (FORMS-7833)
* Después de actualizar al paquete de servicio del Experience Manager 6.5.14.0, los procesos de Workbench para mover un nodo CRX de una ubicación a otra no funcionan. El error se produce como `ALC-CRX-30000-000: com.adobe.ep.crx.client.exceptions.CRCException: ALC-CRX-030-000-[Internal Server Error]`. (FORMS-7713)
* Cuando un usuario actualiza al paquete de servicio de Experience Manager 6.5.16.0, la variable `Usage Rights` no se puede aplicar. (FORMS-7892)
* Cuando un usuario intenta generar un documento de PDF, la validación de PDF/A-1b falla. (FORMS-7615)
* Cuando un usuario hace clic en `Configure` para la opción `Form Container` , el explorador deja de responder. (FORMS-7605)
* Cuando un usuario actualiza al paquete de servicio de Experience Manager Forms 6.5.16.0 e intenta cambiar el `LicenseType` hasta `Production`Sin embargo, los cambios no se reflejan. (FORMS-7594)
* Cuando un usuario intenta invocar un proceso LCA con un PDF que incluye el `Chinese Full Width Characters`, se produce un problema con el `ValidateForm` proceso. (FORMS-7464)
* En Experience Manager Forms Designer, XMLFM genera una salida ZPL con diferentes tamaños de papel, como carta, A4 y A5, para plantillas basadas en XDP. (FORMS-7898)


## Integraciones{#integrations-6517}

* Al convertir una configuración de Adobe Target IMS a una credencial de usuario en configuraciones de nube heredadas, la variable `connectedWhen` La propiedad no cambia. Este problema hace que todas las llamadas pasen como si la configuración aún estuviera basada en IMS. (CQ-4352810)
* Agregando `modifyProperties` permiso para `fd-cloudservice` usuario del sistema para la configuración de Adobe Sign. (FORMS-6164)
* Con Experience Manager integrado con Adobe Target, al crear una actividad de prueba A/B, no se sincronizan las audiencias asociadas con ella, sino con Target. (NPR-40085)

## Oak{#oak-6517}

En Service Pack 13 y versiones posteriores, ha comenzado a aparecer el siguiente registro de errores que afecta a la caché de persistencia:

```shell
org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
    at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
    at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
    at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
    at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
    at org.h2.mvstore.db.Store.<init>(Store.java:129)
```

O bien

```shell
org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
```

Para resolver esta excepción, haga lo siguiente:

1. Elimine las dos carpetas siguientes de `crx-quickstart/repository/`

   * `cache`
   * `diff-cache`

1. Instale el Service Pack o reinicie el Experience Manager as a Cloud Service.
Nuevas carpetas de `cache` y `diff-cache` se crean automáticamente y ya no experimenta una excepción relacionada con lo siguiente `mvstore` en el `error.log`.

## Plataforma{#platform-6517}

* En la interfaz de usuario de Experience Manager Tag Management (/aem/tags/), los espacios de nombres y las etiquetas aparecen en el orden en que se crean. Sin embargo, cuando hay muchas áreas de nombres y etiquetas, la capacidad de verlas y administrarlas es difícil. Este problema se debe a que no se pueden ordenar de ninguna otra manera. (NPR-39620)
* Se necesita la actualización de la versión del cierre de Google porque Minification js no funciona para algunas bibliotecas de cliente. (NPR-40043)

## [!DNL Sites]{#sites-6517}

* Disminución de rendimiento en LinkCheckerTransformer. (SITES-11661)
* Las copias de idioma de una página no se actualizaban según lo esperado. (SITES-11191)
* Llamada para abrir páginas que no sean de campaña `targeteditor.html` innecesariamente. Retire el `targeteditor` llame a cuando no sea necesario. (SITES-12469)
* No se pueden crear Live Copies para páginas con anotaciones. (SITES-12154)
* El despliegue de páginas no funciona en Experience Manager 6.5.16. (SITES-12008)
* Memoria insuficiente; alta actividad de recolección de elementos no utilizados debido a `NotificationManagerImpl`. `NotificationManager` actualización del paquete a Experience Manager 6.5. (SITES-11440)
* Se han corregido las pruebas de TI de WCM que bloqueaban el Service Pack 17. (SITES-13089)
* La recuperación de referencias de sitios falla en el servlet. (SITES-10901)

### [!DNL Sites] - Interfaz de usuario de administrador{#sites-adminui-6517}

* No se puede cerrar la ventana de vista previa del selector de imágenes en miniatura. (SITES-10459)

### [!DNL Sites] - [!DNL Content Fragments]{#sites-contentfragments-6517}

* Configuración para conectarse al objeto del servicio Polaris (URL, credenciales, devolución de llamada, etc.). (SITES-12149)
* Uso de `SemanticDataType.REFERENCE` debe admitir &quot;Remote-Asset-IDs&quot;. (SITES-12127)
* Integre el Selector de recursos de Polaris en el editor de fragmentos de contenido. (SITES-12125)
* Se necesitaba un encabezado http obligatorio para acceder al extremo del servicio de metadatos. (SITES-13068)
* La implementación de GraphQL de 6.5 no estaba a la par con el Cloud Service (principal); se solucionaron los problemas identificados. (SITES-13096)
* La paginación/ordenación y el filtrado híbrido de GraphQL deberían estar disponibles en Experience Manager 6.5/AMS. (SITES-9154)

### [!DNL Sites] - Componentes principales{#sites-core-components-6517}

* La propiedad `cq-msm-lockable` tiene el valor de redirección incorrecto en el componente de página de base. (SITES-10904)
* El Selector de recursos remoto siempre redirige al entorno de ensayo de IMS. (SITES-13433)

### [!DNL Sites] - [!DNL Experience Fragments]{#sites-experiencefragments-6517}

* Al seleccionar una configuración de externalizador en un fragmento de experiencia al exportar a Adobe Target, se envía la URL externalizada incorrecta. (SITES-12402)
* Eliminar términos no inclusivos; aplicar directrices de términos inclusivos. (SITES-11244)

### [!DNL Sites] - Editor de página{#sites-pageeditor-6517}

* No se muestra ninguna miniatura para un carrusel establecido en el carril lateral del buscador de contenido de Experience Manager. (SITES-8593)

## Sling{#sling-6517}

* Sling `ResourceMerger` consume una gran cantidad de CPU cuando se le proporciona una ruta ficticia, lo que provoca una denegación de servicio. (NPR-40338)

## Proyectos de traducción{#translation-6517}

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST * The `translationrules.xml` is sorted poorly when adding a rule to a property by way of the translation configuration user interface. (NPR-40431) -->
* La copia de idioma no se crea cuando el usuario no está configurando campos no obligatorios. (NPR-40036)

## Interfaz de usuario{#ui-6517}

* El botón Cancelar de Propiedades de página está inactivo; debería llevar a la interfaz de usuario de Administración del sitio. (NPR-40501)

<!-- ## WCM{#wcm-6517}

* TEXT -->

## Flujo de trabajo{#workflow-6517}

* Cambios de la consola de flujo de trabajo. (NPR-40502)
* `SegmentNotfound errors` en los registros de una instancia de creación de producción, provocada por una resolución de recursos sin cerrar en la clase `com.day.cq.workflow.impl.email.EMailNotificationServic`. (NPR-40187)
* A cerrado no cerrado `ResourceResolver` excepción que se está registrando. (ASSETS-22495)
* El autor del Experience Manager se bloquea cuando el PSD/PDF con un `DocumentAncestors` atributos de metadatos cargados. (ASSETS-22966)
* Filtrado de sesión en clase `InboxSharingCache` con `user-reader-service`. (CQ-4352513)
* La lista de usuarios y grupos incompleta se muestra cuando el paso &quot;Selector de participantes de iniciador de flujo de trabajo&quot; enumera los usuarios y grupos para el paso de participante. Este problema ocurría cuando un grupo era también miembro de otro grupo. (NPR-40055)
* Depuración mejorada de flujos de trabajo. (NPR-40459)

## Instalar [!DNL Experience Manager] 6.5.17.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.17.0 requiere [!DNL Experience Manager] 6.5. Véase [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en el Adobe [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip).
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.17.0 en una de las instancias de autor mediante el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> El Adobe no recomienda quitar ni desinstalar el [!DNL Experience Manager] Paquete de 6.5.17.0. Como tal, antes de instalar el paquete, debe crear una copia de seguridad del `crx-repository` en caso de que deba revertirlo. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instalación del Service Pack en [!DNL Experience Manager] 6,5{#install-service-pack}

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de realizar la instalación, tome una instantánea o realice una copia de seguridad nueva de su [!DNL Experience Manager] ejemplo.

1. Descargue el Service Pack desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el Administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y luego seleccione **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de la instalación del Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del Administrador de paquetes a veces existe durante la instalación del Service Pack. El Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete actualizador antes de asegurarse de que las instalaciones se hayan realizado correctamente. Normalmente, este problema se produce en [!DNL Safari] explorador, pero puede producirse de forma intermitente en cualquier explorador.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar automáticamente [!DNL Experience Manager] 6.5.17.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en `../crx-quickstart/install` cuando el servidor está disponible en línea. El paquete se instala automáticamente.
* Utilice el [API HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para instalar los paquetes anidados.

>[!NOTE]
>
>Experience Manager 6.5.17.0 no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validación de la instalación**

Para conocer las plataformas certificadas para trabajar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.17.0)` bajo [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi son **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web): `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.15 o posterior de (utilice la consola web: `/system/console/bundles`). <!-- NPR-40398 for 6.5.17.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Instalar Service Pack para [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obtener instrucciones para instalar el Service Pack en Experience Manager Forms, consulte [Instrucciones de instalación del Service Pack de Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Instalación del paquete de índice de GraphQL para fragmentos de contenido de Experience Manager{#install-aem-graphql-index-add-on-package}

Los clientes que utilicen GraphQL deben instalar [Fragmento de contenido de Experience Manager con el paquete de índice 1.1.1 de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Al hacerlo, puede añadir la definición de índice necesaria en función de las funciones que utilizan realmente.

Si no se instala este paquete, las consultas de GraphQL pueden ser lentas o dar error.

>[!NOTE]
>
>Instale este paquete solo una vez por instancia; no es necesario reinstalarlo con cada Service Pack.

### UberJar{#uber-jar}

UberJar para [!DNL Experience Manager] 6.5.17.0 está disponible en la [Repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.17/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.17</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar y los demás artefactos relacionados están disponibles en el Repositorio de Maven Central en lugar del Repositorio de Maven público de Adobe (`repo.adobe.com`). El nombre del archivo principal de UberJar cambia a `uber-jar-<version>.jar`. Así que no hay `classifier`, con `apis` como el valor, para el `dependency` etiqueta.

## Funciones en desuso{#removed-deprecated-features}

A continuación, se muestra una lista de las funciones que se han marcado como obsoletas con [!DNL Experience Manager] 6.5.7.0. Las funciones se marcan como obsoletas inicialmente y posteriormente se eliminan en una versión futura. Se proporciona una opción alternativa.

Revise si utiliza una función o una capacidad en una implementación. Además, planifique cambiar la implementación para utilizar una opción alternativa.

| Área | Funcionalidad | Reemplazo |
|---|---|---|
| Integraciones | La pantalla **[!UICONTROL Inclusión de Experience Manager Cloud Services]** está obsoleto debido a que [!DNL Experience Manager] y [!DNL Adobe Target] La integración de se actualiza en [!DNL Experience Manager] 6.5. La integración es compatible con la API de Adobe Target Standard. La API utiliza la autenticación mediante Adobe IMS y [!DNL Adobe I/O Runtime]. Apoya el creciente papel de Adobe Launch en instrumentación [!DNL Experience Manager] en el caso de las páginas de analytics y personalización, el asistente de inclusión es irrelevante desde el punto de vista funcional. | Configurar conexiones del sistema, autenticación IMS de Adobe y [!DNL Adobe I/O Runtime] integraciones a través de las respectivas [!DNL Experience Manager] cloud services. |
| Conectores | El conector JCR de Adobe para Microsoft® SharePoint 2010 y Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/D |

## Problemas conocidos{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* Actualice las consultas de GraphQL que puedan haber utilizado un nombre de API personalizado para el modelo de contenido a con el nombre predeterminado del modelo de contenido en su lugar.

* Una consulta de GraphQL puede utilizar el complemento `damAssetLucene` índice en lugar de `fragments` índice. Esta acción puede dar como resultado consultas de GraphQL que fallan o que tardan mucho tiempo en ejecutarse.

  Para corregir el problema, `damAssetLucene` debe configurarse para incluir las dos propiedades siguientes:

   * `contentFragment`
   * `model`

  Una vez cambiada la definición del índice, es necesario volver a indexar (`reindex` = `true`).

  Después de estos pasos, las consultas de GraphQL deberían funcionar más rápido.

* Como [!DNL Microsoft® Windows Server 2019] no admite [!DNL MySQL 5.7] y [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] no admite instalaciones llave en mano para [!DNL Experience Manager Forms 6.5.10.0].

* Si actualiza su [!DNL Experience Manager] instancia de 6.5.0 a 6.5.4 al Service Pack más reciente de Java™ 11, verá lo siguiente `RRD4JReporter` excepciones en la `error.log` archivo. Para detener las excepciones, reinicie la instancia de [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Los usuarios pueden cambiar el nombre de una carpeta en una jerarquía en [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el Explorador de propiedades. El problema se resuelve seleccionando la configuración de otro campo del formulario adaptable en el mismo editor.

* Durante la instalación de, pueden mostrarse los siguientes errores y mensajes de advertencia [!DNL Experience Manager] 6.5.x.x:
   * &quot;Cuando la integración de Adobe Target está configurada en [!DNL Experience Manager] Si se utiliza la API de Target Standard (autenticación IMS) y se exportan los fragmentos de experiencias a Target, se crean tipos de ofertas incorrectos. En lugar de &quot;Fragmento de experiencia&quot;/fuente &quot;Adobe Experience Manager&quot;, Target crea varias ofertas con el tipo &quot;HTML&quot;/fuente &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: No se han encontrado ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor de formularios adaptables falla cuando se utilizan funciones de agregado como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - No hay ventanas de mantenimiento en granite/operations/maintenance.
   * El punto interactivo de una imagen interactiva de Dynamic Media no está visible al obtener una vista previa del recurso mediante el visor de titulares de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : tiempo de espera hasta que se completó el cambio de registro sin registrar.

* Al intentar mover, eliminar o publicar fragmentos de contenido, sitios o páginas, hay un problema cuando se recuperan las referencias de fragmentos de contenido, ya que la consulta en segundo plano falla. Es decir, la funcionalidad no funciona.
Para garantizar un funcionamiento correcto, debe agregar las siguientes propiedades al nodo de definición del índice `/oak:index/damAssetLucene` (no se requiere reindexación):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* En la plataforma JBoss® 7.1.4, cuando el usuario instala el Service Pack de Experience Manager 6.5.16.0 o posterior, `adobe-livecycle-jboss.ear` la implementación falla.
* La versión de JDK superior a 1.8.0_281 no es compatible con el servidor JEE de WebLogic.
* AEM A partir de la versión 6.5.15, el motor JavaScript de Rhino proporcionado por el ```org.apache.servicemix.bundles.rhino``` El paquete tiene un nuevo comportamiento de elevación. Scripts que utilizan el modo estricto (```use strict;```) deben declarar correctamente sus variables, de lo contrario, no se ejecutarán, lo que generará un error de tiempo de ejecución.

## Paquetes de contenido y paquetes OSGi incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.17.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.17.0](/help/release-notes/assets/65170_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.17.0](/help/release-notes/assets/65170_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos{#restricted-sites}

Estos sitios web solo están disponibles para los clientes de. Si es cliente de y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe de.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* [Contactar con Atención al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
>* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)
