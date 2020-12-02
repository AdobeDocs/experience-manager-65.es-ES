---
title: Modelado de datos - Modelo de David Nuescheler
seo-title: Modelado de datos - Modelo de David Nuescheler
description: Recomendaciones de modelado de contenido de David Nuescheler
seo-description: Recomendaciones de modelado de contenido de David Nuescheler
uuid: acb27e81-9143-4e0d-a37a-ba26491a841f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 39546c0a-b72f-42df-859b-98428ee0d5fb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 0%

---


# Modelado de datos - Modelo de David Nuescheler{#data-modeling-david-nuescheler-s-model}

## Origen {#source}

Los siguientes detalles son ideas y comentarios expresados por David Nuescheler.

David fue cofundador y CTO of Day Software AG, un proveedor líder de software de gestor de contenido global e infraestructura de contenido, que fue adquirido por Adobe en 2010. Ahora es socio y vicepresidente de Tecnología empresarial en Adobe y también lidera el desarrollo de JSR-170, la interfaz de programación de aplicaciones (API) de Java Content Repository (JCR), el estándar tecnológico para gestor de contenido.

También se pueden ver más actualizaciones en [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

## Introducción de David {#introduction-from-david}

En varias discusiones he encontrado que los desarrolladores están algo incómodos con las características y funcionalidades presentadas por JCR cuando se trata de modelado de contenido. No hay guía y muy poca experiencia aún en cómo modelar contenido en un repositorio y por qué un modelo de contenido es mejor que el otro.

Mientras que en el mundo relacional la industria del software tiene mucha experiencia en cómo modelar datos, todavía estamos en las primeras etapas del espacio del repositorio de contenido.

Me gustaría inicio llenar este vacío expresando mis opiniones personales sobre cómo se debe modelar el contenido, con la esperanza de que algún día esto pueda convertirse en algo más significativo para la comunidad de desarrolladores, que no es solamente &quot;mi opinión&quot; sino algo que es más generalmente aplicable. Consideremos que esto podría ser el primer golpe que se le dé rápidamente.

>[!NOTE]
>
>Renuncia de responsabilidad: Estas pautas expresan mis vistas personales, a veces controvertidas. Espero con interés debatir estas directrices y perfeccionarlas.

## Siete reglas simples {#seven-simple-rules}

### Regla #1: Primero los datos, estructurar más adelante. Tal vez. {#rule-data-first-structure-later-maybe}

#### Explicación {#explanation-1}

Recomiendo no preocuparse por una estructura de datos declarada en el sentido ERD. Inicialmente.

Aprenda a amar a nt:unestructure ( y amigos) en desarrollo.

Creo que Stefano lo resume bastante bien.

Mis resultados finales: La estructura es cara y en muchos casos es completamente innecesario declarar explícitamente la estructura al almacenamiento subyacente.

Existe un contrato implícito sobre la estructura que la aplicación utiliza de forma inherente. Supongamos que almaceno la fecha de modificación de una entrada de blog en una propiedad lastModified. Mi aplicación sabrá automáticamente leer la fecha de modificación de esa misma propiedad de nuevo, realmente no hay necesidad de declararla explícitamente.

Las restricciones de datos adicionales, como las obligatorias o las restricciones de tipo y valor, solo deben aplicarse cuando sea necesario por motivos de integridad de los datos.

#### Ejemplo {#example-1}

El ejemplo anterior de uso de una propiedad `lastModified` Date en, por ejemplo, un nodo &quot;post blog&quot;, no significa que sea necesario un tipo de nodo especial. Definitivamente usaría `nt:unstructured` para mis nodos de anuncios de blog al menos al principio. Ya que en mi aplicación de blogueo todo lo que voy a hacer es mostrar la fecha de la última modificación de todos modos (posiblemente &quot;ordenar por&quot;) apenas me importa si es una fecha. Dado que confío implícitamente en mi aplicación de escritura de blogs para poner una &quot;fecha&quot; allí de todos modos, realmente no hay necesidad de declarar la presencia de una `lastModified` fecha en la forma de una de nodetype.

### Regla #2: Impulse la jerarquía de contenido, no permita que suceda. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Explicación {#explanation-2}

La jerarquía de contenido es un recurso muy valioso. Así que no dejen que suceda, diseñen. Si no tiene un nombre &quot;bueno&quot; y legible para un nodo, probablemente sea algo que debería reconsiderar. Los números arbitrarios casi nunca son un &quot;buen nombre&quot;.

Si bien puede ser extremadamente fácil poner rápidamente un modelo relacional existente en un modelo jerárquico, se debe reflexionar sobre ello.

En mi experiencia, si uno piensa en el control de acceso y la contención, generalmente buenos controladores para la jerarquía de contenido. Piense en ello como si fuera su sistema de archivos. Quizás incluso utilice archivos y carpetas para modelarlos en el disco local.

Personalmente prefiero las convenciones de jerarquía antes que el sistema de nodemecanografía en muchos casos inicialmente, e introducir la escritura más tarde.

>[!CAUTION]
>
>La forma en que se estructura un repositorio de contenido también puede afectar al rendimiento. Para obtener el mejor rendimiento, el número de nodos secundarios conectados a nodos individuales en un repositorio de contenido generalmente no debe superar los 1.000.
>
>Consulte [ ¿Cuántos datos puede manejar CRX?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html) para obtener más información.

#### Ejemplo {#example-2}

Yo modelaría un simple sistema de blogueo como sigue. Por favor, ten en cuenta que inicialmente ni siquiera me importan los respectivos tipos de nodos que uso en este momento.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Creo que una de las cosas que se hacen evidentes es que todos entendemos la estructura del contenido basado en el ejemplo sin más explicaciones.

Lo que puede ser inesperado inicialmente es por qué no almacenaría los &quot;comentarios&quot; con el &quot;post&quot;, que se debe a un control de acceso que me gustaría que se aplicara de una manera razonablemente jerárquica.

Con el modelo de contenido anterior, puedo permitir fácilmente que el usuario &quot;anónimo&quot; &quot;cree&quot; comentarios, pero mantener al usuario anónimo en base a solo lectura para el resto del espacio de trabajo.

### Regla #3: Los espacios de trabajo son para clone(), merge() y update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Explicación {#explanation-3}

Si no utiliza los métodos `clone()`, `merge()` o `update()` en la aplicación, es probable que un solo espacio de trabajo sea el camino a seguir.

&quot;Nodos correspondientes&quot; es un concepto definido en la especificación JCR. Básicamente, se reduce a nodos que representan el mismo contenido, en diferentes llamados espacios de trabajo.

JCR introduce el concepto muy abstracto de Workspaces, que deja a muchos desarrolladores poco claro qué hacer con ellos. Me gustaría proponer que su uso de espacios de trabajo se ponga a prueba a continuación.

Si tiene una superposición considerable de nodos &quot;correspondientes&quot; (esencialmente los nodos con el mismo UUID) en varias áreas de trabajo, probablemente ponga los espacios de trabajo a buen uso.

Si no hay superposición de nodos con el mismo UUID, probablemente esté abusando de los espacios de trabajo.

Los espacios de trabajo no deben utilizarse para control de acceso. La visibilidad del contenido para un grupo de usuarios en particular no es un buen argumento para separar las cosas en diferentes espacios de trabajo. JCR incluye &quot;Control de acceso&quot; en el repositorio de contenido para proporcionar esto.

Los espacios de trabajo son los límites de las referencias y la consulta.

#### Ejemplo {#example-3}

Utilice espacios de trabajo para cosas como:

* v1.2 de su proyecto frente a v1.3 de su proyecto
* un &quot;desarrollo&quot;, un &quot;control de calidad&quot; y un estado de contenido &quot;publicado&quot;

No utilice espacios de trabajo para cosas como:

* directorios principales de usuario
* diferente contenido para diferentes audiencias de destinatario como pública, privada, local, ...
* bandejas de entrada de correo electrónico para distintos usuarios

### Regla #4: Tenga cuidado con los hermanos del mismo nombre. {#rule-beware-of-same-name-siblings}

#### Explicación {#explanation-4}

Aunque se han introducido en la especificación los Siblings del mismo nombre (SNS) para permitir la compatibilidad con estructuras de datos diseñadas y expresadas a través de XML y, por lo tanto, son extremadamente valiosas para JCR, SNS viene con una sobrecarga y complejidad considerables para el repositorio.

Cualquier ruta al repositorio de contenido que contenga un SNS en uno de sus segmentos de ruta se torna mucho menos estable, si se elimina o se reordena un SNS, tendrá un impacto en las rutas del resto de SNS y sus hijos.

Para la importación de XML o la interacción con los SNS XML existentes puede ser necesaria y útil, pero nunca he utilizado SNS y nunca lo haré en mis modelos de datos de &quot;campo verde&quot;.

#### Ejemplo {#example-4}

Uso

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

en lugar de

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### Regla #5: Referencias consideradas perjudiciales. {#rule-references-considered-harmful}

#### Explicación {#explanation-5}

Las referencias implican integridad referencial. Encuentro importante entender que las referencias no sólo agregan costos adicionales al repositorio que administra la integridad referencial, sino que también son costosas desde la perspectiva de la flexibilidad del contenido.

Personalmente, me aseguro de usar sólo referencias cuando realmente no puedo tratar con una referencia colgante y de otra manera usar una ruta, un nombre o una cadena UUID para hacer referencia a otro nodo.

#### Ejemplo {#example-5}

Supongamos que permito las &quot;referencias&quot; de un documento a) a otro documento b). Si modelo esta relación con propiedades de referencia, significa que los dos documentos están vinculados a nivel de repositorio. No puedo exportar/importar el documento a) individualmente, ya que el destinatario de la propiedad de referencia puede no existir. También se ven afectadas otras operaciones como combinar, actualizar, restaurar o clonar.

Así que podría modelar esas referencias como &quot;referencias débiles&quot; (en JCR v1.0 esto esencialmente se reduce a propiedades de cadena que contienen el uuid del nodo de destinatario) o simplemente usar una ruta. A veces la ruta es más significativa para empezar.

Creo que hay casos de uso en los que un sistema realmente no puede funcionar si una referencia está colgando, pero simplemente no puedo encontrar un buen ejemplo &quot;real&quot; pero simple de mi experiencia directa.

### Regla #6: Los archivos son archivos. {#rule-files-are-files}

#### Explicación {#explanation-6}

Si un modelo de contenido expone algo que huele *de forma remota, incluso* como un archivo o una carpeta que intento utilizar (o ampliar desde) `nt:file`, `nt:folder` y `nt:resource`.

En mi experiencia, muchas aplicaciones genéricas permiten interactuar implícitamente con nt:folder y nt:files, y saben cómo manejar y mostrar ese evento si se enriquecen con información meta adicional. Por ejemplo, una interacción directa con implementaciones de servidores de archivos como CIFS o WebDAV que se encuentran sobre JCR se convierte en implícita.

Creo que como buena regla general uno podría usar lo siguiente: Si necesita almacenar el nombre de archivo y el tipo mime, entonces `nt:file`/ `nt:resource` es una muy buena coincidencia. Si puede tener varios &quot;archivos&quot;, una carpeta nt:es un buen lugar para almacenarlos.

Si necesita agregar metainformación para su recurso, digamos una propiedad &quot;author&quot; o &quot;description&quot;, extienda `nt:resource` no la `nt:file`. Rara vez extiendo nt:file y extendo frecuentemente `nt:resource`.

#### Ejemplo {#example-6}

Supongamos que a alguien le gustaría subir una imagen a una entrada de blog en:

```xml
/content/myblog/posts/iphone_shipping
```

y tal vez la reacción intestinal inicial sería agregar una propiedad binaria que contenga la imagen.

Aunque ciertamente hay buenos casos de uso para usar solamente una propiedad binaria (digamos que el nombre es irrelevante y el tipo mime está implícito) en este caso, recomendaría la siguiente estructura para mi ejemplo de blog.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Regla #7: Las identificaciones son malas. {#rule-ids-are-evil}

#### Explicación {#explanation-7}

En las bases de datos relacionales, los ID son un medio necesario para expresar las relaciones, por lo que las personas tienden a utilizarlas también en modelos de contenido. Principalmente por razones equivocadas.

Si el modelo de contenido está lleno de propiedades que finalizan en &quot;Id&quot;, probablemente no esté aprovechando la jerarquía correctamente.

Es cierto que algunos nodos necesitan una identificación estable durante todo su ciclo de vida. Mucho menos de lo que pensarías. mix:referceable proporciona un mecanismo de este tipo integrado en el repositorio, por lo que realmente no hay necesidad de encontrar un medio adicional para identificar un nodo de manera estable.

También tenga en cuenta que los elementos se pueden identificar por ruta, y por mucho que los &quot;enlaces simbólicos&quot; tengan más sentido para la mayoría de los usuarios que los enlaces duros en un sistema de archivos unix, una ruta tiene sentido para que la mayoría de las aplicaciones hagan referencia a un nodo destinatario.

Lo que es más importante, es **mix**:referceable, lo que significa que se puede aplicar a un nodo en el momento en que realmente necesite hacer referencia a él.

Digamos que sólo porque le gustaría poder hacer referencia a un nodo de tipo &quot;Documento&quot; no significa que el tipo de nodo &quot;Documento&quot; tenga que extenderse desde mix:referenciable de manera estática, ya que se puede agregar a cualquier instancia del &quot;Documento&quot; dinámicamente.

#### Ejemplo {#example-7}

Uso:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

en lugar de:

```xml
[Blog]
-- blogId
-- author
[Post]
-- postId
-- blogId
-- title
-- text
-- date
[Attachment]
-- attachmentId
-- postId
-- filename
+ resource (nt:resource)
```

