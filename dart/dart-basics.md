# Dart Basics

### Type Inference

Dart es un lenguaje de tipado estático e inferido. Podemos utilizar `var` para que Dart infiera el tipo de la variable.

```
void main () {
		var name = 'Andrea'; // String Type
		var age = 34; // int Type

		// Una variable no puede cambiar de Type una vez que es asignada
		age = "Asignar este String a una variable tipo int dará error";

}
```

### Variable Interpolation

La interpolación sirve para incluir una variable en una cadena

```dart
void main() {
		String name = 'Andrea';
		int age = 34;

		print("Hello I'm $name");
		print("My name has ${name.length} letters");

		print("I'm $age years old");
}
```

### Inmutabilidad

Siempre que sea posible, utilizaremos variables `final` para declarar constantes

```dart
void main () 
{
	
		// Variables mutables
		int age = 30;
		var height = 2.9;

		// Correcto
		age = 22; // Variable mutable => Puede cambiar de estado

		// Variables inmutables
		final int edad = 40;
		final altura = 1.9;

		// Error
		altura = 2.1 // Variable inmutable => Solo puede inicializarse una vez
}
```

### Variables Dinámicas

Con la keyword `dynamic` podemos declarar variables dinámicas. Aunque Dart brinda esta posibilidad es una opción que debe utilizarse en casos muy concretos.

```dart
void main () {
		
		dynamic altura = 3;
		altura = "No dará error de compilación, pero debe usarse en casos muy concretos"
}
```

### Funciones

#### Función básica con parámetros obligatorios y posicionales

```dart
void describe(String name, int age, double height){
		print("Hello I'm $name");
		print ("I'm $age years old");
}
```
