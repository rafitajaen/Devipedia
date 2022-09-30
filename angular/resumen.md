# Resumen

### Angular

Angular es una plataforma de desarrollo para facilitar la construcción de aplicaciones multiplataforma.

Es de código abierto, está escrita en Typescript y mantenida por el equipo de Google.

Angular es considerada una plataforma porque integra en una misma solución:&#x20;

* Framework basado en componentes para construir aplicaciones webs escalables.&#x20;
* Colección de librerías bien integradas que cubren una gran variedad de funciones (routing, formularios, cliente-servidor)&#x20;
* Herramientas para ayudar a desarrollar, compilar y testear.

Lo que conocemos hoy como Angular es una versión moderna del framework Angular JS que creó Google para desarrollar principalmente SPAs.

Las ventajas de utilizar Angular frente a AngularJS, son:&#x20;

* Compatibilidad con TS con lo que ello implica (escalabilidad por tipado, evitar errores en tiempo de compilación). &#x20;
* Está diseñada desde los inicios para soportar aplicaciones multiplataforma.

```bash
npm install -g @angular/cli
```

### Typescript

Typescript es un lenguaje de programación de código abierto y desarrollado por Microsoft, que fue concebido para solventar las carencias de JS cuando se crean aplicaciones de gran tamaño.

Comúnmente se dice que Typescript es un superset de JS, ya que este amplía las funcionalidades de JS y al mismo tiempo que mantiene la compatibilidad del código. (todo código de JS lo es de TS, y cualquier código de TS se transpila a JS)

Debemos entender que TS es una capa por encima de JS para facilitar la vida al desarrollador, ya que aporta:

* Tipado estático, para descubrir errores en tiempo de compilación y no durante el runtime.&#x20;
* Permite trabajar con JS como si fuera un lenguaje orientado a objetos, más extendido que la programación basada en prototipos.&#x20;
* Incluye la opción de añadir funcionalidades de versiones modernas de ECMAScript.

Algunas de las funcionalidades que añade TS a JS son Tipos, Interfaces, Decoradores, Enumeradores.

```bash
npm install typescript -D
```

### Angular Building Blocks

{% hint style="info" %}
Componentes Directivas Módulos Servicios Pipes Guards
{% endhint %}

Los bloques no son más que clases de JS, pero para comprenderlas mejor debemos definir qué es un decorador:

Los decoradores son una funcionalidad experimental (ECMAScript ES2015+) que se utiliza para modificar la declaración y el comportamiento de una clase.

Angular utiliza estos decoradores, junto con los metadatos, para aportar una funcionalidad concreta a cada bloque.

```bash
ng new my-new-app
```

### Angular Minimal App

**Raíz del proyecto:**&#x20;

* angular.json : Configuración de angular.&#x20;
* tsconfig.json: Configuración TS.&#x20;
* package.json: Configuración dependencias node.

**src/**&#x20;

* main.ts: incluye bootstrapModule() para cargar el módulo principal de la app.&#x20;
* index.html: template donde se define app-root

**app/**&#x20;

* app.module.ts: Incluye bootstrap que define el componente raíz y lo inserta en el index.html.&#x20;
* app.component.ts&#x20;
* app-routing.module.ts

**assets/**

**environments/**

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
 
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
 
@NgModule({
  declarations: [ AppComponent ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### Components

Un componente es la unidad mínima de construcción de una aplicación de Angular y representa una porción de la interfaz de usuario.

Para definir un componente asociamos el decorador `@Component` a una clase que será la encargada de definir la interacción con el DOM.

Este decorador recibe los siguientes parámetros:

* Selector: Nombre del custom element para renderizarlo en el DOM.
* Template\*: Representa la porción de UI que queremos renderizar en el DOM. HTML + sintaxis Angular que añade funcionalidad (property binding).
* Styles\*: Opcional. Para la apariencia.

\*Angular aporta la opción de declarar los templates Inline y en archivos propios.

Toda aplicación tiene al menos un componente app-root, que es la raíz del árbol de componentes de Angular.

Un componente es una directiva que tiene asociado un template.

```bash
ng generate component hero
```

```typescript
import { Component } from "@angular/core"

@Component({
   selector: 'app-hero',
   templateUrl: './hero.component.html'
   styleUrls: ['./hero.component.scss']
})
export class HeroComponent implements OnInit {

ngOnInit(){}

}
```

### Directivas

Las directivas son clases que añaden o modifican el comportamiento de elementos de una app de Angular.

Diferenciamos dos tipos de directivas:&#x20;

* Directivas de atributo: Modificar apariencia o comportamiento de un elemento HTML o componente. Built in: \[ngClass], \[ngStyle], \[ngModel]
* Directivas Estructurales: Modifican el layout del DOM, añadiendo o eliminando elementos del DOM. Built in: \*ngIf, \*ngFor, \*ngSwitch

Los componentes son directivas de atributo que tienen asociado un template.

Se pueden aplicar varias directivas a un único elemento.

```typescript
import { Directive, ElementRef, Input } from '@angular/core';

@Directive({ selector: '[myHighlight]' })
export class HighlightDirective {
    constructor(el: ElementRef) {
       el.nativeElement.style.backgroundColor = 'yellow';
    }
}
```

```html
<p myHighlight>Highlight me!</p>
```

### Módulos

Los módulos son contenedores para agrupar código en bloques lógicos dentro de una aplicación de Angular.

Toda aplicación de Angular tiene al menos un módulo (AppModule), que es el módulo raíz y el que arranca toda la aplicación.

Su uso es opcional y normalmente implementan una funcionalidad concreta (feature) dentro de la aplicación.

Un módulo puede importar funcionalidades de otros módulos, y exportar las suyas propias.

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

@NgModule({
  imports:      [ BrowserModule ],
  providers:    [ Logger ],
  declarations: [ AppComponent ],
  exports:      [ UserComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

### LyfeCycle Hooks

El ciclo de vida de un componente (o directiva) no es más que las diferentes fases por las que pasa dicho componente dentro de una aplicación de Angular.

El ciclo de vida empieza cuando Angular instancia la clase de dicho componente para renderizarlo en el DOM.

En ciertos puntos de este ciclo de vida Angular llama a unas funciones especiales (Hooks), que podemos implementar para controlar el comportamiento del componente en las diferentes fases del ciclo de vida.

* ngOnchanges: Se llama antes de ngOnInit si el componente tiene inputs y cada vez que los inputs cambian. Tiene impacto en la performance.&#x20;
* ngOnInit: Se llama después del primer ngOnchanges. Lugar donde se setean los inputs. Lugar para fetch.&#x20;
* ngDoCheck: Lugar para detectar y actuar frente a cambios que Angular no puede detectar por sí mismo.&#x20;
* ngOnDestroy: Antes de que Angular destruya la instancia. Lugar para desuscribirse de observables, detach Event-Handlers (Listeners), y evitar memory leaks.

<figure><img src="https://github.com/sudheerj/angular-interview-questions/raw/master/images/lifecycle.png" alt=""><figcaption><p>Angular LyfeCycle Hooks</p></figcaption></figure>
