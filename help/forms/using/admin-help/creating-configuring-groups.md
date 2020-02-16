---
title: Creación y configuración de grupos
seo-title: Creación y configuración de grupos
description: Obtenga información sobre cómo crear grupos de forma manual o dinámica, editar un grupo, ver los detalles de un grupo o eliminarlo.
seo-description: Obtenga información sobre cómo crear grupos de forma manual o dinámica, editar un grupo, ver los detalles de un grupo o eliminarlo.
uuid: 8532d72b-270a-4fcf-b7a5-56fca979a5fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2058b501-65ce-4ad3-8e1b-b2eab896f70f
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# Creación y configuración de grupos{#creating-and-configuring-groups}

La creación de grupos de usuarios permite asignar funciones al grupo en lugar de a usuarios individuales.

Hay dos tipos diferentes de grupos disponibles. Puede crear manualmente un grupo y agregarle usuarios y otros grupos. También puede crear grupos dinámicos que incluyan automáticamente a todos los usuarios que cumplan un conjunto de reglas especificado.

Los usuarios pueden experimentar un tiempo de respuesta más lento si pertenecen a muchos grupos (por ejemplo, 500 o más) o si los grupos están anidados profundamente (por ejemplo, 30 niveles). Si tiene este problema, puede configurar formularios AEM para recuperar previamente información de ciertos dominios. (Consulte [Configuración de formularios AEM para recuperar previamente la información](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information)de dominio).

## Crear un grupo manualmente {#create-a-group-manually}

Cuando crea manualmente un grupo, puede agregarle usuarios y otros grupos y asignar funciones al grupo. También puede asociar el grupo con un grupo principal.

Si está utilizando Content Services (obsoleto), puede seleccionar la opción Seleccionar esta opción para insertar usuarios y grupos en proveedores de almacenamiento externo principal registrados en la página Administración de dominios para insertar la información para cualquier usuario o grupo nuevo que cree en Content Services (obsoleto).

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos y, a continuación, haga clic en Nuevo grupo.
1. Complete la sección Configuración general y haga clic en Siguiente. Nombre canónico y Nombre de grupo son atributos obligatorios.

   El nombre canónico es un identificador único para el grupo. Cada grupo y usuario de un dominio debe tener un nombre canónico único. Seleccione la casilla Generado por el sistema para permitir que la Administración de usuarios asigne un valor único, o bien desactive la casilla de verificación y especifique un valor personalizado para el Nombre canónico.

   Evite utilizar caracteres de subrayado (_) en nombres canónicos, por ejemplo, `sample_group`. Al buscar grupos en función de su nombre canónico, no se devuelven los que contienen caracteres de subrayado.

1. Para agregar usuarios y grupos a este nuevo grupo, haga clic en Buscar usuarios/grupos y realice las siguientes tareas:

   * En el cuadro Buscar, escriba los criterios de búsqueda.
   * En la lista En, seleccione Usuarios, Grupos o Usuarios y grupos.
   * En la lista Uso, seleccione Nombre, Correo electrónico o ID de usuario.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y haga clic en Buscar.
   * En los resultados de la búsqueda, seleccione las casillas de verificación de los usuarios y grupos que desee agregar a este nuevo grupo y haga clic en Aceptar.

1. Haga clic en Siguiente.
1. Para agregar este nuevo grupo a otros grupos existentes, haga clic en Buscar grupos y haga lo siguiente:

   * En el cuadro Buscar, escriba los criterios de búsqueda.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y haga clic en Buscar.
   * En los resultados de la búsqueda, active las casillas de verificación de los grupos a los que pertenece el nuevo grupo y haga clic en Aceptar.

1. Haga clic en Siguiente.
1. Para asignar funciones al grupo, haga clic en Buscar funciones, seleccione las casillas de verificación de cada función que desee asignar al grupo y haga clic en Aceptar. Los usuarios del grupo heredan funciones asignadas a nivel de grupo.
1. Haga clic en Finalizar.

## Crear un grupo dinámico {#create-a-dynamic-group}

En un grupo dinámico, no se seleccionan individualmente los usuarios que pertenecen al grupo. En su lugar, se especifica un conjunto de reglas y todos los usuarios que las cumplan se agregan automáticamente al grupo dinámico.

Utilice una de estas dos formas de crear grupos dinámicos:

* Habilite la creación automática de grupos dinámicos basados en dominios de correo electrónico, como @adobe.com. Al habilitar esta función, Administración de usuarios crea un grupo dinámico para cada dominio de correo electrónico único en la base de datos de formularios de AEM. Utilice una expresión cron para especificar la frecuencia con la que Administración de usuarios busca en la base de datos de formularios AEM nuevos dominios de correo electrónico. Estos grupos dinámicos se agregan al dominio local DefaultDom y se denominan &quot;Todos los usuarios con un ID de *`[email domain]`* correo electrónico&quot;.
* Cree un grupo dinámico según criterios específicos, incluidos el dominio de correo electrónico, la descripción, el nombre canónico y el nombre de dominio del usuario. Para pertenecer al grupo dinámico, un usuario debe cumplir todos los criterios especificados. Para configurar una condición &quot;o&quot;, cree dos grupos dinámicos independientes y agréguelos a un grupo local. Por ejemplo, utilice ese método para crear un grupo de usuarios que pertenezcan al dominio de correo electrónico @adobe.com o cuyo nombre canónico contenga ou=adobe.com. Sin embargo, los usuarios no necesariamente deben cumplir ambas condiciones.

Un grupo dinámico solo contiene usuarios. No puede contener otros grupos. Sin embargo, un grupo dinámico puede pertenecer a un grupo principal.

### Crear automáticamente grupos dinámicos basados en dominios de correo electrónico {#automatically-create-dynamic-groups-based-on-email-domains}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Configurar atributos avanzados del sistema.
1. En Creación automática de grupos dinámicos, active la casilla de verificación.
1. Especifique cuándo el Administrador de usuarios comprueba si hay nuevos dominios de correo electrónico. Esta hora debe ser posterior al tiempo de sincronización del dominio, ya que la creación de grupos dinámicos solo es lógica si se ha completado la sincronización del dominio.

   * Para habilitar la sincronización automática diariamente, escriba la hora en el formato de 24 horas en el cuadro Ocurre diariamente en. Al guardar la configuración, este valor se convierte en una expresión cron, que se muestra en el cuadro de abajo.
   * Para programar la sincronización en un día concreto de la semana o mes, o en un mes concreto, seleccione escribir la expresión cron adecuada en el cuadro. El valor predeterminado es `0 00 4 ? * *`(lo que significa que marcar 4 A.M. todos los días).

      El uso de la expresión cron se basa en el sistema de programación de trabajos de código abierto Quartz, versión 1.4.0.

1. Haga clic en Guardar.

### Crear un grupo dinámico basado en criterios especificados {#create-a-dynamic-group-based-on-specified-criteria}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. Haga clic en Nuevo grupo dinámico.
1. Complete la sección Configuración general. Nombre del grupo es un atributo obligatorio. Puede asignar el grupo a cualquier dominio configurado.
1. En Criterios de grupo dinámico, especifique uno o varios atributos utilizados para rellenar el grupo dinámico.

   >[!NOTE]
   >
   >Los atributos Correo electrónico, Descripción y Nombre canónico distinguen entre mayúsculas y minúsculas al utilizar el operador Igual a. No distinguen entre mayúsculas y minúsculas con los operadores Empieza por, Termina por o Contiene.

   **** Correo electrónico: Dominio de correo electrónico del usuario, como `@adobe.com`.

   **** Descripción: Descripción del usuario, como &quot;Informático científico&quot;

   **** Nombre canónico: Nombre canónico del usuario, como `ou=adobe.com`

   **** Nombre de dominio: El nombre del dominio al que pertenece el usuario, como `DefaultDom`. El atributo Nombre de dominio distingue entre mayúsculas y minúsculas al utilizar el operador Contiene. No distingue entre mayúsculas y minúsculas con los operadores Empieza por, Termina por o Igual a.

1. Haga clic en Prueba. Una página de prueba muestra los primeros 200 usuarios que cumplen los criterios definidos. Haga clic en Cerrar.
1. Si la prueba ha devuelto los resultados esperados, haga clic en Siguiente. De lo contrario, edite los criterios del grupo dinámico y vuelva a realizar la prueba.
1. Para agregar el grupo dinámico a un grupo principal, haga clic en Buscar grupos y realice las siguientes tareas:

   * En el cuadro Buscar, escriba los criterios de búsqueda.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y haga clic en Buscar.
   * En los resultados de la búsqueda, active las casillas de verificación de los grupos a los que pertenece el grupo dinámico y haga clic en Aceptar.

1. Haga clic en Siguiente.
1. Para asignar funciones al grupo dinámico, haga clic en Buscar funciones, seleccione las casillas de verificación de cada función que desee asignar al grupo y, a continuación, haga clic en Aceptar. Los usuarios del grupo heredan funciones asignadas a nivel de grupo.
1. Haga clic en Finalizar.

## Ver detalles sobre un grupo {#view-details-about-a-group}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. En la lista En, seleccione Agrupar y, a continuación, haga clic en Buscar. Los resultados de la búsqueda se enumeran en la parte inferior de la página. Puede ordenar la lista haciendo clic en cualquiera de los encabezados de columna.
1. Haga clic en el nombre del grupo para mostrar los detalles. Aparece la página Detalles del grupo.
1. Para ver los miembros directos del grupo, haga clic en Principios secundarios.

## Editar un grupo {#edit-a-group}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. Para buscar el grupo que se va a editar, realice las siguientes tareas:

   * En el cuadro Buscar, escriba los criterios de búsqueda.
   * En la lista Uso, seleccione Nombre o Correo electrónico.
   * En la lista En, seleccione Grupos.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y haga clic en Buscar.
   * En los resultados de búsqueda, haga clic en el nombre del grupo que desee editar.

1. En la ficha Detalles, edite la configuración general y haga clic en Guardar.
1. Para editar los grupos asociados, haga clic en la ficha Grupos principales y realice las siguientes tareas:

   * Para buscar grupos que agregar a la asociación, haga clic en Buscar grupos y complete la información de búsqueda.
   * Para agregar grupos, active la casilla de verificación de los grupos que desee agregar, haga clic en Aceptar y, a continuación, haga clic en Guardar.
   * Para eliminar un grupo asociado, seleccione la casilla de verificación del grupo que desea eliminar, haga clic en Eliminar, en Aceptar y, a continuación, en Guardar.

1. Para editar los usuarios y grupos del grupo, haga clic en la ficha Principios secundarios y realice las siguientes tareas:

   * Para encontrar usuarios y grupos que agregar, haga clic en Buscar usuarios/grupos y complete la información de búsqueda.
   * Para agregar un usuario o grupo, seleccione la casilla de verificación del usuario o grupo, haga clic en Aceptar y, a continuación, en Guardar.
   * Para eliminar un usuario o grupo, seleccione la casilla de verificación del usuario o grupo, haga clic en Eliminar, en Aceptar y, a continuación, en Guardar.

1. Para editar las asignaciones de funciones, haga clic en la ficha Asignaciones de funciones y realice las siguientes tareas:

   * Para buscar roles que asignar al grupo, haga clic en Buscar roles.
   * Para agregar una función, active la casilla de verificación de la función, haga clic en Aceptar y, a continuación, en Guardar.
   * Para anular la asignación de una función, seleccione la casilla de verificación de la función, haga clic en Desasignar y, a continuación, haga clic en Guardar.

## Eliminar un grupo {#delete-a-group}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. En la lista Buscar, seleccione Grupos y, a continuación, haga clic en Buscar.
1. Seleccione la casilla de verificación del grupo que desea eliminar, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

