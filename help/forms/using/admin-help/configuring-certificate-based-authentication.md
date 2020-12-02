---
title: Configuración de la autenticación basada en certificados
seo-title: Configuración de la autenticación basada en certificados
description: Importe un certificado de entidad emisora de certificados (CA) en el almacén de confianza y cree una asignación de certificados para la autenticación basada en certificados.
seo-description: Importe un certificado de entidad emisora de certificados (CA) en el almacén de confianza y cree una asignación de certificados para la autenticación basada en certificados.
uuid: 9802a969-6d29-4b80-a4ed-06eb6e66e046
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d958ae65-3008-4d68-9e11-4346e149827f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---


# Configuración de la autenticación basada en certificados {#configuring-certificate-based-authentication}

Normalmente, la Administración de usuarios realiza la autenticación con un nombre de usuario y una contraseña. La administración de usuarios también admite la autenticación basada en certificados, que puede utilizar para autenticar usuarios a través de Acrobat o para autenticar usuarios mediante programación. Para obtener más información sobre la autenticación de usuarios mediante programación, consulte [Programación con formularios AEM](https://www.adobe.com/go/learn_aemforms_programming_63).

Para utilizar la autenticación basada en certificados, importe un certificado de entidad emisora de certificados (CA) en el almacén de confianza y, a continuación, cree una asignación de certificados.

## Importar el certificado de CA {#import-the-ca-certificate}

Al importar el certificado, seleccione las opciones Confiar en la autenticación de certificado y Confiar en la identidad, así como cualquier otra opción que necesite. Para obtener más información sobre la importación de certificados, consulte [Administración de certificados](/help/forms/using/admin-help/certificates.md#managing-certificates).

## Configuración de la asignación de certificados {#configuring-certificate-mapping}

Para habilitar la autenticación basada en certificados para los usuarios, cree una asignación de certificados. Una *asignación de certificados* define un mapa entre los atributos de un certificado y los atributos de los usuarios de un dominio. Puede asignar más de un certificado al mismo dominio.

Al probar un certificado, Administración de usuarios carga las comprobaciones de certificado para asegurarse de que cumple los siguientes requisitos:

* El certificado es válido.
* El emisor especificado puede verificar el certificado.
* El certificado contiene el atributo necesario para la asignación.
* La asignación especificada asigna el certificado a un solo usuario de la base de datos de formularios AEM. Los usuarios actuales y los usuarios obsoletos (eliminados) se comprueban para determinar si coinciden con los criterios de asignación. Por lo tanto, la prueba de certificado falla si más de un usuario, incluidos los usuarios obsoletos, tiene en cuenta el valor de atributo.

>[!NOTE]
>
>No se puede editar una asignación de certificado existente.

**Añadir una asignación de certificado**

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Asignación de certificados.
1. Haga clic en Asignación de certificado nuevo y, en la lista Para emisor, seleccione el alias de certificado tal como está configurado en Administración de almacén de confianza.
1. Asigne uno de los atributos del certificado al atributo de un usuario. Por ejemplo, puede asignar el nombre común del certificado al ID de inicio de sesión del usuario.

   Si el contenido del atributo del certificado es diferente del contenido del atributo del usuario en la base de datos de Administración de usuarios, puede utilizar una Expresión de Java Regular (regex) para coincidir con los dos atributos. Por ejemplo, si los nombres comunes de los certificados son *Alex Pink (Authentication)* y *Alex Pink (Signing)* y el nombre común en la base de datos User Management es *Alex Pink*, utilice un regex para extraer la parte requerida del atributo de certificado (en este ejemplo, *Alex Pink&lt;a 7/>.)* La expresión regular que especifique debe ajustarse a la especificación de Java regex.

   Puede transformar la expresión especificando el orden de los grupos en el cuadro Orden personalizado. El orden personalizado se utiliza con el método `java.util.regex.Matcher.replaceAll()`. El comportamiento que se ve se corresponderá con el comportamiento de ese método y la cadena de entrada (el orden personalizado) se debe especificar en consecuencia.

   Para probar el regex, introduzca un valor en el cuadro Parámetro de prueba y haga clic en Prueba.

   Puede utilizar los siguientes caracteres en el regex:

   * . (cualquier carácter)
   * &amp;ast; (0 o más ocurrencias)
   * () (especifique el grupo entre corchetes)
   * \ (utilizado para escapar de un carácter regex a un carácter normal)
   * $n (utilizado para hacer referencia al grupo n)

   Ejemplos de expresiones regulares:

   * Para extraer &quot;Alex Pink&quot; de &quot;Alex Pink (Autenticación)&quot;

      **Regex:** (.&amp;ast;) \(Autenticación\)

   * Para extraer &quot;Alex Pink&quot; de &quot;Alex (Authentication) Pink&quot;

      **Regex:** (.&amp;ast;)\(Autenticación\) (.&amp;ast;)

   * Para extraer &quot;Alex Rosa&quot; de &quot;Alex (Autenticación) Rosa&quot;

      **Regex:** (.&amp;ast;)\(Autenticación\) (.&amp;ast;)

      Orden personalizado: $2 $1 (devuelve el segundo grupo, concatenado al primer grupo, capturado con un carácter de espacio en blanco)

   * Para extraer &quot;apink@sampleorg.com&quot; de &quot;smtp:apink@sampleorg.com&quot;

      **Regex:** smtp:(.&amp;ast;)
   Para obtener más información sobre el uso de expresiones regulares, consulte [Tutorial de Java sobre expresiones regulares](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. En la lista Para dominio, seleccione el dominio del usuario.
1. Para probar esta configuración, haga clic en Examinar para cargar un certificado de usuario de muestra, haga clic en Probar certificado y, si la configuración es correcta, haga clic en Aceptar.

**Editar una asignación de certificado existente**

1. En la Consola de administración, haga clic en Configuración > Administración de usuarios > Configuración.
1. Haga clic en Asignación de certificados.
1. Seleccione la asignación de certificados para editar y editar su configuración. Puede actualizar la expresión normal y el orden personalizado.
1. Para probar los cambios, haga clic en Examinar para cargar un certificado de muestra, haga clic en Probar certificado y, a continuación, haga clic en Aceptar.

**Eliminar una asignación de certificado**

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Asignación de certificados.
1. Seleccione la casilla de verificación de la asignación de certificados que desea eliminar, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

