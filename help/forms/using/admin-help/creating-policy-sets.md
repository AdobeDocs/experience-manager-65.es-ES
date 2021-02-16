---
title: Creación y administración de conjuntos de políticas
seo-title: Creación y administración de conjuntos de políticas
description: Los conjuntos de políticas se utilizan para agrupar directivas que tienen un propósito comercial común. Puede crear, editar y eliminar directivas en un conjunto de políticas.
seo-description: Los conjuntos de políticas se utilizan para agrupar directivas que tienen un propósito comercial común. Puede crear, editar y eliminar directivas en un conjunto de políticas.
uuid: 11faf67c-b9b7-4394-8672-d43cace131ad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a4fb1a11-8fe3-4092-a036-1c079aea1250
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 0%

---


# Creación y administración de conjuntos de políticas {#creating-and-managing-policy-sets}

Los conjuntos de políticas se utilizan para agrupar directivas que tienen un propósito comercial común. Los conjuntos de políticas se pueden poner a disposición de un subconjunto de usuarios del sistema.

Cada conjunto de políticas tiene al menos un coordinador de conjuntos de políticas asociado. El *coordinador de conjuntos de políticas* es un administrador o un usuario que tiene permisos adicionales. El coordinador de conjuntos de políticas suele ser un especialista de la organización que puede crear mejor las políticas en un conjunto de políticas determinado.

Los coordinadores de conjuntos de políticas pueden realizar las siguientes tareas:

* Crear nuevas directivas
* Editar y eliminar cualquier directiva del conjunto de directivas
* Editar la configuración del conjunto de directivas
* Añadir y eliminar coordinadores para el conjunto de directivas
* Eventos de política de vista y documento para cualquier política o documento dentro del conjunto de políticas
* Revocar acceso a documentos
* Cambiar directivas para el documento

Los superusuarios y los coordinadores de conjuntos de políticas que tienen permiso para hacerlo crean y eliminan conjuntos de políticas en la interfaz del administrador de seguridad de documento.

Al eliminar un conjunto de directivas, las directivas que formaban parte del conjunto no se pueden aplicar a documentos nuevos. Sin embargo, puede vista de la información de la política tanto en la consola de administración como en las páginas web del usuario final para las directivas que aún están en uso. Puede vista la información de la política desde la página de detalles del documento para cualquier documento protegido por la política. Las políticas que aún se están utilizando se pueden editar.

El superusuario o coordinador de conjuntos de políticas agrega los dominios creados en Administración de usuarios al usuario y grupo visibles para cada conjunto de políticas. Esta lista es visible para el coordinador de conjuntos de políticas y se utiliza para poner límites en los dominios que el coordinador de conjuntos de políticas puede examinar al elegir usuarios para agregar a las políticas.

Al crear conjuntos de políticas, se asigna a los usuarios la función de publicador de documento. El *editor de documento* es el usuario que protege el documento con una política. De forma predeterminada, este usuario siempre se incluye en una directiva con derechos de acceso completos, incluidas las capacidades de revocación y conmutación de políticas. Sin embargo, los administradores pueden cambiar los derechos de acceso del editor de documento para las directivas compartidas. Por ejemplo, el administrador puede desactivar el derecho del editor de documento a revocar el acceso de documento o cambiar la directiva. Si un administrador cambia la directiva adjunta al documento, el nombre del publicador se actualizará al nombre del propietario de la última directiva aplicada al documento.

Al instalar la seguridad de documento, se crea un conjunto de directivas predeterminado llamado *Conjunto de directivas globales*. Este conjunto de directivas lo administra el administrador que instaló el software o el coordinador de conjuntos de directivas designado para este conjunto de directivas.

## Crear un conjunto de directivas {#create-a-policy-set}

El conjunto de directivas globales es el único conjunto de directivas predeterminado que se crea al realizar la instalación. Puede crear conjuntos de políticas adicionales y agregar políticas, usuarios, coordinadores de conjuntos de políticas y editores de documento. Después de crear un conjunto de directivas, puede crear políticas dentro del conjunto.

Durante la creación del conjunto de directivas, puede utilizar el botón Atrás para volver a la pantalla anterior y el botón Guardar para guardar el conjunto de directivas en cualquier momento.

1. En la página Seguridad de documento, haga clic en Directivas, en la ficha Conjuntos de directivas y, a continuación, en Nuevo.
1. En el cuadro Nombre, escriba un nombre para el conjunto de directivas, escriba opcionalmente una Descripción y, a continuación, haga clic en Siguiente. El nombre no puede contener dos puntos **:**.

   >[!NOTE]
   >
   >Puede crear un nombre de conjunto de directivas que contenga caracteres extendidos; sin embargo, cuando se realiza una comparación entre dos cadenas, los caracteres acentuados y no acentuados como &quot;e&quot; y &quot;é&quot; se consideran iguales. Cuando alguien crea un conjunto de directivas, se realiza una comparación para comprobar si ya existe un conjunto de directivas con el mismo nombre. La comparación no puede distinguir entre nombres que son iguales excepto los caracteres acentuados. Se da por hecho que el conjunto de directivas ya se ha agregado a la base de datos y que no se ha agregado el nuevo.

1. (Opcional) Para establecer los dominios que son visibles para los editores de Documento cuando agregan usuarios a una política, haga clic en Añadir dominios, seleccione los dominios en los que se puede buscar, haga clic en Añadir y, a continuación, haga clic en Aceptar.
1. En la página Añadir usuarios y grupos visibles, haga clic en Siguiente.
1. (Opcional) Para agregar un coordinador de conjuntos de políticas, haga clic en Añadir usuarios y grupos en la página Añadir coordinadores de conjuntos de políticas (Paso 3 de 4) y realice estas tareas:

   * En el cuadro Buscar, escriba el nombre o la dirección de correo electrónico.
   * En la lista Uso, seleccione la opción adecuada.
   * En la lista Tipo, seleccione Usuario y, en la lista En, seleccione un dominio para buscar.
   * En la lista Mostrar, seleccione el número de resultados que se mostrarán por página y, a continuación, haga clic en Buscar.
   * Seleccione la casilla de verificación del usuario o grupo que desee agregar y haga clic en Siguiente.
   * Seleccione los permisos del coordinador de conjuntos de políticas y haga clic en Añadir. Se pueden establecer los siguientes permisos:

      * Eventos de vista
      * Administrar documentos (revocar y restablecer el acceso a documentos y cambiar las políticas en documentos)
      * Administrar políticas (crear, editar y eliminar políticas)
      * Administración de editores de Documento (agregar y quitar editores de Documento)
      * Delegar (agregar y quitar coordinadores de conjuntos de directivas)

1. Repita el paso 5 para agregar más coordinadores de conjuntos de políticas.
1. Revise la configuración del coordinador de conjuntos de políticas y haga clic en Siguiente.
1. Haga clic en Añadir usuarios y grupos para agregar editores de documento que pueden utilizar las directivas del conjunto de directivas para proteger documentos.
1. En la página Añadir publicadores de Documento, realice las siguientes tareas:

   * En el cuadro Buscar, escriba el nombre o la dirección de correo electrónico.
   * En la lista Uso, seleccione la opción adecuada.
   * En la lista Tipo, seleccione Usuario y, en la lista En, seleccione un dominio para buscar.
   * En la lista Mostrar, seleccione el número de resultados que se mostrarán por página y, a continuación, haga clic en Buscar.
   * Seleccione las casillas de verificación para los usuarios y grupos que desee agregar, haga clic en Añadir y, a continuación, haga clic en Aceptar.

1. Haga clic en Guardar.

Ahora puede agregar directivas al conjunto de directivas. (Consulte [Creación y edición de políticas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies)).

## Editar un conjunto de directivas {#edit-a-policy-set}

1. En la página Seguridad de documento, haga clic en Directivas, en la ficha Conjuntos de directivas y, a continuación, en el conjunto de políticas que desea editar.
1. Haga clic en la ficha correspondiente y edite según sea necesario:

   * **Detalle:** edite el nombre y la descripción del conjunto de directivas.
   * **Directivas:** Crear, habilitar, editar y eliminar directivas dentro del conjunto de directivas.
   * **Usuarios y grupos visibles:** Añada y elimine usuarios y grupos visibles que se pueden incluir en una política.
   * **Coordinadores de conjuntos de políticas:** Añada, elimine y cambie los permisos de los coordinadores.
   * **Publicadores de documento:** Añada y elimine usuarios que puedan publicar documentos mediante las políticas del conjunto.

1. Para eliminar un usuario o grupo visible, un coordinador de conjuntos de políticas o un publicador de Documentos, haga clic en la ficha correspondiente, seleccione la casilla de verificación de la entrada, haga clic en Eliminar y, a continuación, haga clic en Aceptar.
1. Para agregar usuarios o grupos visibles, un coordinador de conjuntos de políticas o editores de Documento, haga clic en la ficha correspondiente, haga clic en Añadir usuarios o grupos, busque el usuario o grupo que desee agregar, seleccione la entrada, haga clic en Añadir y, a continuación, haga clic en Aceptar.
1. En la ficha Directivas, busque directivas para agregarlas al conjunto de directivas y cree nuevas directivas:

   * Para buscar una directiva, seleccione ID de directiva o Nombre de directiva, escriba el valor correspondiente, seleccione el número de elementos que desea mostrar y haga clic en Buscar.
   * Para obtener más información sobre la creación de una nueva directiva, consulte [Creación y edición de directivas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).

## Eliminar un conjunto de directivas {#delete-a-policy-set}

Al eliminar un conjunto de directivas, las directivas que formaban parte del conjunto no se pueden aplicar a documentos nuevos. Sin embargo, puede vista de la información de la política tanto en la consola de administración como en las páginas web del usuario final para las directivas que aún se están utilizando. Puede vista la información de la política desde la página de detalles del documento para cualquier documento protegido por la política. Las políticas que aún se están utilizando se pueden editar.

1. Haga clic en Directivas y, a continuación, en la ficha Conjuntos de directivas.
1. Seleccione la casilla de verificación del conjunto de directivas que desea eliminar.
1. Haga clic en Eliminar y, a continuación, en Aceptar.

