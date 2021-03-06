---
layout: tutorials
title: Styles
---
<h2 class="tutorials-content__sub-title">Styles</h2>

<h3 class="tutorials-content__sub-title">Estilo en linea</h3>

<p class="tutorials-content__text">Los estilos en línea son estilos que están presentes en el HTML en el atributo de estilo.<code class="tutorials__code">.style</code> nos permite tener acceso al estilo en linea de elementos y poder cambiarlos o modificarlo.</p>

<pre>
  <code class="language-html">
  &#60;section class="section" id="section" style="color:red;"&#62;Section Content&#60;/section&#62;
  </code>
</pre>

<pre>
  <code class="language-javascript">
  let element = document.querySelector('#section');

  let fontColor = element.style.color;

  console.log(fontColor); //-> red
  
  element.style.color = 'blue';
  </code>
</pre>

<h3 class="tutorials-content__sub-title">Estilo calculados</h3>

<p class="tutorials-content__text">Dado que el estilo de un elemento puede modificarse desde un bloque de declaración de estilo CSS ubicado en otro archivo o en el archivo HTML donde se declara el elemento, no podemos confiar solo en <code class="tutorials__code">HTMLElement.style</code> para acceder a todas sus propiedades de estilo.</p>

<pre>
  <code class="language-html">
  &#60;section class="section" id="section"&#62;Section Content&#60;/section&#62;
  </code>
</pre>

<pre>
  <code class="language-javascript">
  let element = document.querySelector('#section');

  let fontColor = window.getComputedStyle(element).getPropertyValue('color');

  console.log(fontColor); //-> rgb(255, 0, 0)
  </code>
</pre>
