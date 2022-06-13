# Iteraciones

### for

```javascript
let listaTareas: string[] = ['a', 'b', 'c'];

for (let index = 0; index < listaTareas.length; index++) {
    const tarea = listaTareas[index];
    console.log(`${index} - ${tarea}`);
}
```

### forEach

```javascript
let listaTareas: string[] = ['a', 'b', 'c'];

listaTareas.forEach(
    (tarea, index) => {
        console.log(`${index} - ${tarea}`);
    }
);
```

### for in

```javascript
for (const key in miTareaUno) {

    if (Object.prototype.hasOwnProperty.call(miTareaUno, key)) {
        const element = miTareaUno[key];
    }
}
```

