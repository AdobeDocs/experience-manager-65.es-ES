---
title: ¿Cómo se generan y funcionan con hashes en PDF forms dinámicos?
description: Generación y trabajo con hash en PDF forms dinámicos
source-git-commit: 730ae7cd6cd04eb6377b37eafe29db597e93cce3
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# Generación y trabajo con hash en PDF forms dinámicos {#generate-work-with-hashes-dynamic-pdf-forms}


## Conocimientos previos {#prerequisite-knowledge}

Se requiere cierta experiencia con AEM Forms en JEE Designer, así como la capacidad de acceder a funciones y de llamar a ellas en objetos de secuencias de comandos.

## Nivel de usuario {#user-level}

Inicio

Cuando quiera ocultar una contraseña en el formulario PDF y no desee que aparezca en texto sin formato dentro del código fuente o en cualquier otro lugar del documento PDF, es clave saber cómo generar y trabajar con los hash MD4, MD5, SHA-1 y SHA-256.

La idea es confundir la contraseña generando un hash único y almacenando este hash en el documento PDF. Este hash único se puede generar mediante diferentes funciones hash, y en este artículo le mostraré cómo generarlas dentro del formulario PDF y cómo trabajar con ellas.

Una función hash toma una cadena larga (o mensaje) de cualquier longitud como entrada y produce una cadena de longitud fija como salida, a veces denominada compendio de mensaje o huella digital.

AEM Forms en JEE Designer permite implementar las diferentes funciones hash en objetos de secuencia de comandos como JavaScript y ejecutarlos dentro de un documento PDF dinámico. Los PDF de ejemplo que se incluyen con los archivos de muestra para este artículo utilizan implementaciones de código abierto de las siguientes funciones hash:

* MD4 y MD5: diseñado por Ronald Rivest

* SHA-1 y SHA-256 - tal como los define el NIST

La mayor ventaja de utilizar hashes es que no tiene que comparar contraseñas directamente comparando cadenas de texto claras; en su lugar, puede comparar los dos hashes de las dos contraseñas. Como es muy poco probable que dos cadenas diferentes tengan el mismo hash, si ambos hashes son idénticos, entonces puede suponer que las cadenas comparadas (en este caso, las contraseñas) también son idénticas.

>[!NOTE]
>
>Hay algunos problemas de seguridad conocidos (llamados conflictos de hash) con MD4 o MD5. Debido a esos conflictos de hash y otros hacks SHA-1 (incluyendo tablas de arco iris), decidí concentrarme en la función hash SHA-256 en la segunda muestra.  Para obtener más información, consulte las páginas [Collision](https://en.wikipedia.org/wiki/Hash_collision) y [Rainbow Table](https://en.wikipedia.org/wiki/Rainbow_table) de Wikipedia.

## Examen de los objetos de secuencia de comandos {#examining-script-objects}

Cuando abra uno de los dos ejemplos proporcionados en AEM Forms en JEE Designer, encontrará los cuatro objetos de secuencia de comandos en la paleta Jerarquía (consulte la figura siguiente).

![Variables](assets/variables.jpg)

Para ver la implementación JavaScript de las funciones hash dentro de estos objetos de secuencia de comandos, seleccione el objeto de secuencia de comandos y explore el código en el Editor de secuencias de comandos.  Puede ver cómo se ha implementado cada una de las siguientes funciones hash:

* soHASHING_MD4.hex_md4()
* soHASHING_MD4.b64_md4()
* soHASHING_MD4.str_md4()
* soHASHING_MD5.hex_md5()
* soHASHING_MD5.b64_md5()
* soHASHING_MD5.str_md5()
* soHASHING_SHA1.hex_sha1()
* soHASHING_SHA1.b64_sha1( )
* soHASHING_SHA1.str_sha1( )
* soHASHING_SHA256.hex_sha256()
* soHASHING_SHA256.b64_sha256()
* soHASHING_SHA256.str_sha256()

Como puede ver en esta lista, hay diferentes funciones disponibles para los diferentes tipos de salida del hash. Puede elegir entre `hex_` para dígitos hexadecimales, `b64_` para salida codificada Base64 o `str_` para codificación de cadenas sencilla.

Según la función hash que elija, la longitud del hash variará:

* MD4: 128 bits
* MD5: 128 bits
* SHA-1: 160 bits
* SHA-256: 256 bits

## Prueba de los PDF forms de muestra {#try-sample-pdf-forms}

Los archivos de ejemplo para este artículo incluyen dos PDF forms. El primer ejemplo le permite escribir una cadena y luego generar valores hash MD4, MD5, SHA-1 y SHA-256 para la cadena.  El segundo ejemplo es un formulario sencillo que desbloquea los campos de texto si se introduce una contraseña correcta.

### Ejemplo 1:  generación de hashes {#generating-dashes}

Siga los pasos a continuación para probar la primera muestra:

1. Después de descargar y descomprimir los archivos de ejemplo, abra hashing_forms_sample1.pdf con AEM Forms en JEE Designer. También puede utilizar Adobe Reader o Adobe Acrobat Professional para abrir y ver el ejemplo, pero no podrá ver el código fuente.
1. En el campo de texto etiquetado [!UICONTROL borrar texto] escriba una contraseña o cualquier otro mensaje que desee que tenga hash.
1. Haga clic en uno de los cuatro botones para generar el hash MD4, MD5, SHA-1 o SHA-256. Dependiendo del botón que haya pulsado, se llama a una de las cuatro funciones hash que producen salida hexadecimal y se coloca en hash la cadena o el mensaje.

El resultado de la operación hash se muestra en el campo etiquetado [!UICONTROL hash]. La longitud del hash variará según la función de hash que elija.

Todos los ejemplos utilizan dígitos hexadecimales como tipo de salida. Puede utilizar el Editor de secuencias de comandos para modificar los ejemplos y cambiar el tipo de salida a Base64 o a String simple.

### Ejemplo 2:  contraseñas coincidentes {#matching-passwords}

El segundo ejemplo muestra cómo se comparan los hashes en segundo plano, sin tener que revelar la contraseña real. La contraseña que introduzca tendrá un cifrado hash. La contraseña real, que se almacena en un campo invisible, también está almacenada con hash. La contraseña es segura, no porque sea invisible, sino porque se ha cifrado en hash. Debido a que es imposible reconstruir la contraseña desde el valor con hash, es seguro exponer la contraseña con hash. La comparación se realiza únicamente entre los hashes, no entre las contraseñas en texto sin formato. Si ambos hashes son iguales, puede suponer que las contraseñas son idénticas.

Siga los pasos a continuación para probar la segunda muestra:

1. Abra `hashing_forms_sample2.pdf` con AEM Forms en JEE Designer. También puede utilizar Adobe Reader o Adobe Acrobat Professional para abrir y ver el ejemplo, pero no podrá ver el código fuente.
1. Elija uno de los dos campos de contraseña etiquetados como [!UICONTROL Password MAN] o [!UICONTROL Password WOMAN] y escriba las contraseñas:
   1. La contraseña del hombre es `bob`
   1. La contraseña de la mujer es `alice`
1. Al sacar el enfoque de los campos de contraseña o pulsar la tecla Intro, el hash de la contraseña que ha introducido se genera automáticamente y se compara con el hash almacenado de la contraseña correcta en segundo plano. Las contraseñas correctas con hash se almacenan en los campos de texto invisibles etiquetados como `passwd_man_hashed` y `passwd_woman_hashed`. Si escribe la contraseña correcta para el hombre, los campos de texto etiquetados como `Man 1` y `Man 2` se hacen accesibles para que pueda escribir texto en ellos. El mismo comportamiento se aplica a los campos de mujer.
1. De forma opcional, puede hacer clic en el botón denominado &quot;eliminar contraseñas&quot;, que desactivará los campos de texto y cambiará su borde.

El código para comparar los dos valores con hash y habilitar los campos de texto es sencillo:

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## Dónde ir desde aquí {#next-steps}

¿Dónde necesitarían algo como esto? Considere un formulario PDF que tenga campos que solo deben rellenarlos personas autorizadas. Al asegurar esos campos con una contraseña, que no se pueden ver en texto claro en ningún lugar del documento como en Sample_2.pdf, puede asegurarse de que esos campos solo sean accesibles para los usuarios que conocen la contraseña.

Le animo a seguir explorando los dos archivos PDF de muestra.  Puede generar nuevos valores hash con Sample_1.pdf y utilizar los valores generados para cambiar la contraseña o la función hash utilizada en Sample_2.pdf.  Los recursos enumerados en la sección Atribuciones también proporcionan información adicional sobre el hash y las implementaciones JavaScript específicas utilizadas en este artículo.

## Atribuciones {#attributions}

* [Ronald Rivest](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [Conflicto de hash](https://en.wikipedia.org/wiki/Hash_collision)
* [Tabla arco iris](https://en.wikipedia.org/wiki/Rainbow_table)
* [Página de inicio del proyecto MD5 de JavaScript](http://pajhome.org.uk/crypt/md5/)
* [página de inicio del proyecto jsSHA2](https://anmar.eu.org/projects/jssha2/)


