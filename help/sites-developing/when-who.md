---
title: 'Pruebas: ¿cuándo y con quién?'
description: Se pueden desempeñar diversas funciones en las pruebas y en diversas etapas del desarrollo del proyecto.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 5a16be40-eede-4a47-b03b-3993e285232e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Pruebas: ¿cuándo y con quién?{#testing-when-and-with-whom}

Se pueden desempeñar diversas funciones en las pruebas y en diversas etapas del desarrollo del proyecto.

<table>
 <tbody>
  <tr>
   <td>Equipo de prueba</td>
   <td>Responsable de... </td>
   <td>Cuando...</td>
  </tr>
  <tr>
   <td>Equipo de desarrollo</td>
   <td>El equipo de desarrollo es responsable de las pruebas unitarias y de algunas pruebas de integración.</td>
   <td>Estas pruebas son las primeras en la cadena, aunque se repiten / se extienden durante el desarrollo.</td>
  </tr>
  <tr>
   <td>Equipo de control de calidad</td>
   <td><p>Necesita un equipo de control de calidad (del tamaño que corresponda) para realizar pruebas funcionales y de rendimiento.</p> <p>Estos son probadores neutrales y dedicados; una regla de oro del software siempre establece que un desarrollador nunca debe probar su propio trabajo.</p> <p>Los miembros de este equipo pueden proceder del equipo del proyecto del día, del socio y/o de su equipo de clientes.</p> </td>
   <td><p>La primera versión de la función debe ponerse a disposición de los probadores (cuando sea posible). Aunque una versión provisional anticipada puede generar muchos errores, puede proporcionar comentarios anticipados sobre problemas críticos.</p> </td>
  </tr>
  <tr>
   <td>Equipo de prueba del cliente</td>
   <td><p>Según el modelo de proyecto seleccionado, se puede planificar la participación de miembros del equipo del cliente en las pruebas, en particular autores del sitio del cliente.</p> <p>Esto es ventajoso porque:</p>
    <ul>
     <li><p>Se proporciona al cliente la experiencia del proyecto que se está desarrollando.</p> </li>
     <li><p>Proporciona comentarios anticipados del cliente.</p> </li>
     <li><p>Los usuarios suelen expresar sus requisitos en términos de experiencia previa; involucrar a los clientes en las pruebas lo antes posible aumenta su experiencia del nuevo proyecto en términos de <i>práctico</i> experiencia.</p> </li>
    </ul> </td>
   <td><p>De nuevo, la participación temprana es buena, aunque cualquier versión que utilicen los clientes debería ser estable y tener una funcionalidad razonable.</p> <p>Las primeras impresiones siempre son importantes.</p> </td>
  </tr>
 </tbody>
</table>
