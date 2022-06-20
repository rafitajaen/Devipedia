---
description: Lista de los tipos de selectores en CSS
---

# Selectores

### Selector Universal

```css
* { color: black; }
```

### Selector de elementos

```css
button { font-size: 12px; } 
```

### Lista de selectores

```css
h1, h2, h3 { color: magenta; }
```

### Selector de IDs

```css
#signup { background-color: cyan; }
```

### Selector de Clases

```css
.tag {  }
```

### Selector de Descendientes

```css
li a {  }
```

### Selector de Adyacentes

```css
/* Paragraphs that come immediately after any image */
img + p { font-weight: bold; }
```

### Selector Hijo Directo

```css
div > li {  } 
```

### Selector de atributos

```css
/* <a> elements with a title attribute */
a[title] { color: purple; }

/* <a> elements with an href matching "https://example.org" */
a[href="https://example.org"] { color: green; }

/* <a> elements with an href containing "example" */
a[href*="example"] { font-size: 2em; }

/* <a> elements with an href ending ".org" */
a[href$=".org"] { font-style: italic; }

/* <a> elements whose class attribute contains the word "logo" */
a[class~="logo"] { padding: 2px; }

input[type="text"] {   }
```

### Otros Selectores

```css
/*Sections with a class="post" */
section.post {  }
```
