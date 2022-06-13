---
description: >-
  TS es un superconjunto de JS desarrollado por Microsoft. Nos habilita el
  tipado fuerte de variables, generar enumerados, interfaces, clases.
---

# TS Basics

{% hint style="info" %}
El **tipado fuerte** permite _detectar errores del código en tiempo de desarrollo_, antes de que la aplicación llegue a ejecución.
{% endhint %}

### Tipos primitivos (Built-in types)

Los tipos primitivos son: `number`, `boolean`, `string`, `void`, `null` y `undefined`.

#### Instanciación simple

```typescript
var nombre: string = 'Martin';
const PI: number = 3.1416;
let isTrue: boolean = true;
```

#### Instanciación múltiple

```typescript
let nombre: string, edad: number = 32, isDev: boolean = true;

nombre = 'Martín';
isDev = false;
```

### Arrays

#### Array de tipo único

```typescript
let listaCompra: string[] = ['Lechuga', 'Tomates'];
```

#### Array de tipo múltiple

```typescript
let cajonDesastre: (number | boolean | string)[];

cajonDesastre = [false, 'calcetines', true, 26];
```

### Enumeradores (Enums)

#### Enumerador básico

```typescript
enum Estados {
    'Completo',
    'En progreso',
    'Pendiente'
}
```

#### Enumerador con valores

{% hint style="info" %}
Asignando un valor entero a un enumerado se consigue que el valor de los enumerados siguientes sea una iteración del primero.
{% endhint %}

```typescript
enum Premios{
    'Primero' = 1,
    'Segundo',  // 2 
    'Tercero',  // 3
    'Accessit' = "A"
}
```

###

