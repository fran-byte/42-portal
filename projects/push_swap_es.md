---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Fundamentos previos (antes de atacar push_swap)

### 📌 Objetivo:

Diseñar e implementar un algoritmo eficiente de ordenación utilizando un **conjunto limitado de operaciones sobre pilas**, con el objetivo de ordenar números usando la **menor cantidad de movimientos posible**.

---

### 🧱 ¿Qué es `push_swap`?

- Recibe una lista de números desordenados como argumentos por línea de comandos.
- Imprime por `stdout` una **serie de instrucciones** que ordenan los números utilizando únicamente las operaciones permitidas.
- ✅ **No debe imprimir los números**, solo las instrucciones.

---

## 🛠️ Operaciones permitidas

Solo puedes usar las siguientes operaciones (estilo assembler):

| **Instrucción** | **Descripción**                                                                     |
|-----------------|--------------------------------------------------------------------------------------|
| `sa`            | Intercambia los dos primeros elementos de la pila A.                                |
| `sb`            | Intercambia los dos primeros elementos de la pila B.                                |
| `ss`            | Aplica `sa` y `sb` al mismo tiempo.                                                 |
| `pa`            | Mueve el primer elemento de B al principio de A.                                    |
| `pb`            | Mueve el primer elemento de A al principio de B.                                    |
| `ra`            | Rota todos los elementos de A una posición hacia arriba.                            |
| `rb`            | Rota todos los elementos de B una posición hacia arriba.                            |
| `rr`            | Aplica `ra` y `rb` simultáneamente.                                                 |
| `rra`           | Rota todos los elementos de A una posición hacia abajo.                             |
| `rrb`           | Rota todos los elementos de B una posición hacia abajo.                             |
| `rrr`           | Aplica `rra` y `rrb` al mismo tiempo.                                               |

---

## 🎯 Objetivo final

Debes construir un algoritmo de ordenación que:

* ✅ Ordene correctamente cualquier lista de **enteros únicos**.
* ✅ Use **solo** las operaciones permitidas.
* ✅ Sea **eficiente** (menos de 700 movimientos para 100 números).
* ✅ Sea **robusto** (control de errores, entradas inválidas, etc.).

---

## ⚙️ Estructura del algoritmo de ordenación

El algoritmo puede dividirse en **tres fases principales**:

---

### 🔁 Fase 1: Mover elementos de A a B

1. **Preparación inicial:**
   - Mueve los dos primeros elementos de A a B sin condiciones.

2. **Nodo objetivo en B:**
   - Para cada número en A, encuentra un “nodo objetivo” en B: el número más pequeño en B que sea mayor que el actual.
   - Si no existe, el nodo objetivo es el número más grande en B.

3. **Cálculo de coste:**
   - Para cada número en A, calcula cuántas operaciones requiere llevarlo a la cima de A y al nodo objetivo a la cima de B.

4. **Seleccionar el nodo más barato:**
   - Mueve el número con el **menor coste de inserción** de A a B.

5. **Repetir:**
   - Continúa hasta que **solo queden tres elementos en A**.

---

### 🧮 Fase 2: Ordenar los 3 elementos restantes en A

1. **Algoritmo de 3 números:**
   - Si los tres elementos no están ordenados:
     - Mueve el número más grande al fondo con rotaciones.
     - Intercambia los dos primeros si es necesario.

---

### 🔁 Fase 3: Mover elementos de B a A

1. **Encontrar el nodo objetivo en A:**
   - Para cada número en B, busca el mayor número en A que sea menor.
   - Si no hay ninguno, el nodo objetivo es el más pequeño de A.

2. **Cálculo de coste:**
   - Calcula los movimientos necesarios para llevar el número y su objetivo a la cima de sus respectivas pilas.

3. **Mover el más barato:**
   - Mueve de B a A el número con el **menor coste**.

4. **Repetir:**
   - Hasta que B esté vacío.

---

### 🔄 Fase final: Rotar hasta el menor

- Cuando todos los números estén en A, **rota A** hasta que el número más pequeño esté arriba.

---

## 🧪 Ejemplo de ejecución

### Entrada inicial:
```bash
./push_swap 2 7 5 4 3 6 1
````

### Paso a paso:

1. **Pila A:**

```
A (de arriba a abajo):
2
7
5
4
3
6
1
```

2. **Mover 2 a B:**

```
A       B
7       2
5
4
3
6
1
```

3. **Mover 7 a B:**

```
A       B
5       7
4       2
3
6
1
```

4. **Repetir hasta que queden 3 en A**

5. **Ordenar los 3 en A**

6. **Mover de B a A usando el algoritmo de coste mínimo**

7. **Rotar A hasta que el más pequeño esté arriba**

Resultado final:

```
A (ordenada):
1
2
3
4
5
6
7

B: (vacía)
```

---

### 📚 Recursos útiles

* `man 3 atoi`
* `man 2 write`
* `man 3 malloc`
* [Wikipedia: Pila (estructura de datos)](https://es.wikipedia.org/wiki/Pila_%28inform%C3%A1tica%29)
* [Push\_swap visualizer (GitHub)](https://github.com/o-reo/push_swap_visualizer)

---

### 🧠 Consejos prácticos

* Comienza manejando la entrada y validando argumentos (sin duplicados, solo números).
* Usa una estructura `t_stack` con punteros (`prev`/`next`) para controlar las pilas.
* Implementa funciones auxiliares como `is_sorted`, `stack_len`, `get_min` cuanto antes.
* Imprime las pilas durante el desarrollo para depurar.
* Separa bien las responsabilidades: coste, nodo objetivo, mejor movimiento.
* Crea scripts de test para 3, 5 y 100+ elementos.
* Primero haz que funcione. Luego optimiza.

---

