# Essential Core

### ¿Cuáles son los componentes básicos de Angular?

i. Component: Bloques de construcción básico que componen una aplicación.

ii. Modules: Colecciones de código con el objetivo de empaquetar y proporcionar un ámbito común a funcionalidades concretas.

iii. Templates: Representa la vista de un componente. Son secciones de código HTML que incluye código de Angular que pueden modificar los elementos HTML antes de que sean mostrados.

iiii. Services: Se utiliza para la lógica que no está asociada a la vista y que necesita ser utilizada por varios componentes. Tienen el objetivo de modularizar y reutilizar. Utilizado para fetching data, validate user inputs or logging.

v. Metadata: Información que se añade a través los decoradores para configurar el comportamiento de una clase (metodo, propiedad o parámetro) en Angular.

### ¿Qué son los componentes?

Es la unidad mínima de construcción en una aplicación de Angular. Está compuesta de:

* Template (código HTML que describe como se renderizará).
* Styles (CSS para la apariencia)
* Typescript Class con decorador de tipo Componente. Encargado de definir la interacción del template con el DOM.

Los componentes son directivas que tienen un template asociado.

### ¿Qué es una directiva?

Existen dos tipos de directivas diferentes:

* Estructurales
* De atributo

Las directivas de atributo añaden o modifican el comportamiento de un elemento del DOM o una instancia de un componente existente. Se diferencia de los componentes en que no tienen un template asociado.

Puede haber varias directivas asociadas a un único elemento del DOM.

### ¿Qué es un template?

Un template es un fragmento de la interfaz de usuario de una aplicación. Cada componente se asocia con un template, y están compuesto básicamente de código HTML que puede mezclarse con sintaxis de Angular.

### ¿Qué es un decorador?

Es una función que se usa para asociar metadatos a determinadas clases, métodos, propiedades o parámetros, aportándole una funcionalidad concreta dentro de Angular y que es una característica únicamente presente en Typescript.

### ¿Tipos de decoradores?

Class decorator: @NgModule, @Component, @Injectable, @Directive, @Pipe&#x20;

Property Decorator: @Input, @Output, @ContentChild, @ContentChildren, @ViewChild, @ViewChildren, @HostBinding&#x20;

Method Decorator: @HostListener&#x20;

Parameter Decorator: @Inject, @Host, @Self, @SkipSelf, @Optional&#x20;

Custom Decorators

### ¿Qué es un módulo?

Son una agrupación de código que normalmente implementa una característica completa dentro de la aplicación. Su uso es optativo. Pueden importar funcionalidades que se haya importado de otros módulos.
