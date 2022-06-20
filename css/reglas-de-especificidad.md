---
description: >-
  Cuando existen conflictos entre estilos se aplican las reglas de especificidad
  para ver cual tiene prioridad.
---

# Reglas de especificidad

### Prioridad

!important > Inline style > ID > Class > Elementos

### Especificidad

|       +      | <---SPECIFIC---> |         -        |
| :----------: | :--------------: | :--------------: |
| ID Selectors |       Class      |     Elementos    |
|              |     Atributo     | Pseudo-elementos |
|              |   Pseudo-clases  |                  |
|              |                  |                  |
