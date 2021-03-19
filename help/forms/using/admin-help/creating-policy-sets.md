---
title: Creación y administración de conjuntos de políticas
seo-title: Creación y administración de conjuntos de políticas
description: Los conjuntos de políticas se utilizan para agrupar las políticas que tienen un propósito comercial común. Puede crear, editar y eliminar directivas en un conjunto de directivas.
seo-description: Los conjuntos de políticas se utilizan para agrupar las políticas que tienen un propósito comercial común. Puede crear, editar y eliminar directivas en un conjunto de directivas.
uuid: 11faf67c-b9b7-4394-8672-d43cace131ad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a4fb1a11-8fe3-4092-a036-1c079aea1250
feature: Seguridad de los documentos
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 0%

---


# Creación y administración de conjuntos de directivas {#creating-and-managing-policy-sets}

Los conjuntos de políticas se utilizan para agrupar las políticas que tienen un propósito comercial común. Los conjuntos de políticas se pueden poner a disposición de un subconjunto de usuarios del sistema.

Cada conjunto de políticas tiene al menos un coordinador de conjuntos de políticas asociado. El *coordinador del conjunto de directivas* es un administrador o un usuario que tiene permisos adicionales. El coordinador del conjunto de políticas suele ser un especialista de la organización que puede crear mejor las políticas en un conjunto de políticas determinado.

Los coordinadores de conjuntos de políticas pueden realizar las siguientes tareas:

* Crear nuevas políticas
* Editar y eliminar cualquier directiva del conjunto de directivas
* Editar configuración de conjunto de directivas
* Agregar y quitar coordinadores para el conjunto de directivas
* Ver eventos de directivas y documentos para cualquier directiva o documento dentro del conjunto de directivas
* Revocar el acceso a los documentos
* Cambiar directivas para el documento

Los superusuarios y los coordinadores de conjuntos de directivas que tienen permiso para hacerlo crean y eliminan conjuntos de directivas en la interfaz del administrador de seguridad de documentos.

Al eliminar un conjunto de directivas, las directivas que formaban parte del conjunto no se pueden aplicar a los nuevos documentos. Sin embargo, puede ver la información de la directiva tanto en la consola de administración como en las páginas web del usuario final para las directivas que aún se están utilizando. Puede ver la información de la directiva desde la página de detalles del documento para cualquier documento protegido por la directiva. Las directivas que aún se estén utilizando se pueden editar.

El superusuario o el coordinador de conjuntos de directivas agrega los dominios creados en Administración de usuarios al usuario y grupo visibles para cada conjunto de directivas. Esta lista es visible para el coordinador de conjuntos de políticas y se utiliza para poner límites en los dominios que el coordinador de conjuntos de políticas puede examinar al elegir usuarios para agregar a políticas.

Al crear conjuntos de directivas, se asigna a los usuarios la función de publicador de documentos. El *editor de documentos* es el usuario que protege el documento con una directiva. De forma predeterminada, este usuario siempre se incluye en una directiva con derechos de acceso completos, incluidas las capacidades de revocación y conmutación de políticas. Sin embargo, los administradores pueden cambiar los derechos de acceso del editor del documento para las directivas compartidas. Por ejemplo, el administrador puede desactivar el derecho del editor del documento a revocar el acceso al documento o cambiar la directiva. Si un administrador cambia la directiva adjunta al documento, el nombre del Publicador se actualizará al nombre del propietario de la directiva que se aplicó por última vez al documento.

Tras la instalación de la seguridad del documento, se crea un conjunto de directivas predeterminado denominado *Conjunto de directivas globales*. El administrador que instaló el software o el coordinador del conjunto de directivas designado para este conjunto de directivas es el encargado de administrar este conjunto de directivas.

## Crear un conjunto de directivas {#create-a-policy-set}

Conjunto de directivas globales es el único conjunto de directivas predeterminado que se crea en el momento de la instalación. Puede crear conjuntos de directivas adicionales y agregar directivas, usuarios, coordinadores de conjuntos de políticas y editores de documentos. Después de crear un conjunto de directivas, puede crear directivas dentro del conjunto.

Durante la creación del conjunto de directivas, puede utilizar el botón Atrás para volver a la pantalla anterior y el botón Guardar para guardar el conjunto de directivas en cualquier momento.

1. En la página de seguridad del documento, haga clic en Directivas, en la ficha Conjuntos de directivas y, a continuación, en Nuevo.
1. En el cuadro Nombre, escriba un nombre para el conjunto de directivas, escriba opcionalmente una Descripción y, a continuación, haga clic en Siguiente. El nombre no puede contener dos puntos **:**.

   >[!NOTE]
   >
   >Puede crear un nombre de conjunto de directivas que contenga caracteres extendidos; sin embargo, cuando se realiza una comparación entre dos cadenas, los caracteres acentuados y no acentuados como &quot;e&quot; y &quot;é&quot; se consideran iguales. Cuando alguien crea un conjunto de directivas, se realiza una comparación para comprobar si ya existe un conjunto de directivas con el mismo nombre. La comparación no puede distinguir entre nombres que sean iguales excepto para caracteres acentuados. Se da por hecho que el conjunto de directivas ya se ha agregado a la base de datos y el nuevo no se ha agregado.

1. (Opcional) Para establecer los dominios que son visibles para los editores de documentos cuando agregan usuarios a una directiva, haga clic en Agregar dominios, seleccione los dominios para que se puedan buscar, haga clic en Agregar y, después, haga clic en Aceptar.
1. En la página Agregar usuarios y grupos visibles , haga clic en Siguiente.
1. (Opcional) Para agregar un coordinador de conjuntos de directivas, haga clic en Agregar usuarios y grupos en la página Agregar coordinadores de conjuntos de directivas (paso 3 de 4) y realice estas tareas:

   * En el cuadro Buscar, escriba el nombre o la dirección de correo electrónico.
   * En la lista Uso, seleccione la opción adecuada.
   * En la lista Tipo, seleccione Usuario y, en la lista En, seleccione un dominio en el que buscar.
   * En la lista Mostrar, seleccione el número de resultados que desea mostrar por página y, a continuación, haga clic en Buscar.
   * Seleccione la casilla de verificación del usuario o grupo que desea agregar y haga clic en Siguiente.
   * Seleccione los permisos del coordinador del conjunto de directivas y haga clic en Agregar. Se pueden configurar los siguientes permisos:

      * Ver eventos
      * Administrar documentos (revocar y restablecer el acceso a los documentos y cambiar las políticas de los documentos)
      * Administrar directivas (crear, editar y eliminar directivas)
      * Administración de publicadores de documentos (agregar y quitar publicadores de documentos)
      * Delegar (agregar y quitar coordinadores de conjuntos de directivas)

1. Repita el paso 5 para agregar más coordinadores de conjuntos de políticas.
1. Revise la configuración del coordinador del conjunto de directivas y haga clic en Siguiente.
1. Haga clic en Agregar usuarios y grupos para agregar editores de documentos que puedan usar las directivas dentro del conjunto de directivas para proteger documentos.
1. En la página Agregar editores de documentos , realice estas tareas:

   * En el cuadro Buscar, escriba el nombre o la dirección de correo electrónico.
   * En la lista Uso, seleccione la opción adecuada.
   * En la lista Tipo, seleccione Usuario y, en la lista En, seleccione un dominio en el que buscar.
   * En la lista Mostrar, seleccione el número de resultados que desea mostrar por página y, a continuación, haga clic en Buscar.
   * Seleccione las casillas de verificación de los usuarios y grupos que desee agregar, haga clic en Agregar y, a continuación, haga clic en Aceptar.

1. Haga clic en Guardar.

Ahora puede agregar directivas al conjunto de directivas. (Consulte [Creación y edición de directivas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies)).

## Editar un conjunto de directivas {#edit-a-policy-set}

1. En la página de seguridad del documento, haga clic en Directivas, en la ficha Conjuntos de directivas y, a continuación, en el conjunto de directivas que desea editar.
1. Haga clic en la ficha adecuada y edítela según sea necesario:

   * **Detalle:** edite el nombre y la descripción del conjunto de directivas.
   * **Directivas:** cree, habilite, edite y elimine directivas dentro del conjunto de directivas.
   * **Usuarios y grupos visibles:** agregue y elimine usuarios y grupos visibles que se puedan incluir en una directiva.
   * **Coordinadores de conjuntos de políticas:** agregue, elimine y cambie permisos para los coordinadores.
   * **Publicadores de documentos:** agregue y elimine usuarios que puedan publicar documentos mediante las políticas del conjunto.

1. Para eliminar un usuario o grupo visible, un coordinador de conjuntos de directivas o un publicador de documentos, haga clic en la ficha correspondiente, seleccione la casilla de verificación de la entrada, haga clic en Eliminar y, a continuación, haga clic en Aceptar.
1. Para agregar usuarios o grupos visibles, un coordinador de conjuntos de políticas o editores de documentos, haga clic en la ficha adecuada, haga clic en Agregar usuarios o grupos, busque el usuario o grupo que desee agregar, seleccione la entrada, haga clic en Agregar y, después, haga clic en Aceptar.
1. En la pestaña Directivas , busque las directivas que desea agregar al conjunto de directivas y cree nuevas directivas:

   * Para buscar una directiva, seleccione ID de directiva o Nombre de directiva, escriba el valor correspondiente, seleccione el número de elementos que desea mostrar y haga clic en Buscar.
   * Para obtener más información sobre la creación de una nueva directiva, consulte [Creación y edición de directivas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).

## Eliminar un conjunto de directivas {#delete-a-policy-set}

Al eliminar un conjunto de directivas, las directivas que formaban parte del conjunto no se pueden aplicar a los nuevos documentos. Sin embargo, puede ver la información de la directiva tanto en la consola de administración como en las páginas web del usuario final para las directivas que aún se están utilizando. Puede ver la información de la directiva desde la página de detalles del documento para cualquier documento protegido por la directiva. Las directivas que aún se estén utilizando se pueden editar.

1. Haga clic en Directivas y en la ficha Conjuntos de directivas .
1. Seleccione la casilla de verificación del conjunto de directivas que desea eliminar.
1. Haga clic en Eliminar y, a continuación, en Aceptar.

