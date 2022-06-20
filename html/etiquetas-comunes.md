---
description: Enumeración de las etiquetas de HTML más comunes según su tipo.
---

# Etiquetas Comunes

### Basic HTML

```html
<!DOCTYPE>   : Define el documento
<html>       : Defiene el documento HTML
<head>       : Contiene los metadatos e información del documento
<title>      : Título del documento
<body>       : Cuerpo del documento
<h1> a <h6>  : HTML Headings
<p>          : Párrafos
<br />       : Single line break
<hr />       : Horizontal rule
<!-- * -->   : Comentarios

```

### Formularios e inputs

```html
<form>       : Formulario HTML (Contenedor)
<input>      : Input control
<textarea>   : Multiline input control
<button>     : Botón
<select>     : Dropdown list (Contenedor)
<option>     : Dropdown list item
<optgroup>   : Grupo de <option> relacionadas
<label>      : Etiqueta de un <input>
<fieldset>   : Grupo de elementos relacionados en un <form>
<legend>     : Caption de un <fieldset>
```

### Formatos

```html
<abbr>       : Abreviación o acrónimo
<code>       : Pieza de código
<em>         : Texto en cursiva (Emphasis Text)
<mark>       : Highlighted
<pre>        : Texto Preformateado
<small>      : Letra pequeña (Copyright/Texto legal)
<progress>   : Barra de progreso
<blockquote> : Quote from another source.
<b>          : Texto en negrita
<q>          : Inline quotation element
```

#### `<b>` vs `<strong>`

> The `<strong>` element is for content that is of greater importance, while the `<b>` element is used to draw attention to text without indicating that it's more important. - [MDN web docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/strong)

#### `<i>` vs `<em>` vs `<q>` vs `<strong>`

> The `<em>` element is for words that have a stressed emphasis compared to surrounding text, which is often limited to a word or words of a sentence and affects the meaning of the sentence itself.
>
> Typically this element is displayed in italic type. However, it should not be used to apply italic styling; use the CSS [`font-style`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-style) property for that purpose. Use the [`<cite>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/cite) element to mark the title of a work (book, play, song, etc.). Use the [`<i>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/i) element to mark text that is in an alternate tone or mood, which covers many common situations for italics such as scientific names or words in other languages. Use the [`<strong>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/strong) element to mark text that has greater importance than surrounding text. - [MDN web docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/em)

#### `<q>` : The inline quotation element

```html
<p>When Dave asks HAL to open the pod bay door, HAL answers: 
    <q cite="https://www.imdb.com/title/tt0062622/quotes/qt0396921">
    I'm sorry, Dave. 
    I'm afraid I can't do that.
    </q>
</p>
```

> The **`<q>`** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element indicates that the enclosed text is a short inline quotation. Most modern browsers implement this by surrounding the text in quotation marks. This element is intended for short quotations that don't require paragraph breaks; for long quotations use the [`<blockquote>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote) element.

### Imágenes

```html
<img>         : Imagen
<map>         : A set of clickable link Areas
<area>        : Area dentro de un Map
<figure>      : Container de imágenes
<figcaption>  : Pie de foto de una <figure>
<svg>         : SVG
<picture>     : Container para multiples fuentes de imagen
<canvas>      : Use to draw graphics on the fly (via JS)
```
