---
layout: default
title: "fran-byte 42 Madrid — Punteros en C"
---

## 🔹 Punteros en C – Recurso de Apoyo para Libft

### 📌 Objetivo

Profundizar en el uso de punteros en C: acceso a memoria, manipulación de datos, arrays, estructuras, casteo y memoria dinámica. Este recurso complementa la comprensión necesaria para enfrentar proyectos como **Libft** o **get\_next\_line**.

---

## 1️⃣ ¿Qué es un puntero?

Un **puntero** es una variable que almacena la **dirección de memoria** de otra variable. En C, cada variable ocupa una posición específica en la memoria, y los punteros permiten acceder directamente a esos espacios, optimizando el rendimiento y permitiendo manejo dinámico de datos.

```c
int *p; // Puntero a entero
char *q; // Puntero a carácter
```

Un puntero que no apunta a una dirección válida se considera "muerto" o nulo (`NULL`).

---

## 2️⃣ Operadores: Referencia y Desreferencia

* `&`: obtiene la dirección de memoria de una variable.
* `*`: accede al contenido de la dirección a la que apunta (desreferencia).

```c
int x = 10;
int *p = &x;

printf("%d\n", x);   // 10
printf("%p\n", &x);  // Dirección de x
printf("%p\n", p);   // Dirección de x (igual que &x)
printf("%d\n", *p);  // 10
```

---

## 3️⃣ Modificación indirecta con punteros

```c
int x = 20;
int *p = &x;
*p = 50;
printf("%d\n", x); // 50
```

---

## 4️⃣ Punteros y Arreglos

Los arreglos en C actúan como punteros al primer elemento:

```c
int arr[] = {10, 20, 30};
int *p = arr;

for (int i = 0; i < 3; i++)
    printf("%d\n", *(p + i));
```

Equivale a `arr[i]`. Esto también explica por qué puedes pasar un arreglo como un puntero a funciones.

---

## 5️⃣ Punteros a Punteros

Puedes tener punteros que apuntan a otros punteros:

```c
int x = 100;
int *p = &x;
int **pp = &p;

printf("%d\n", **pp); // 100
```

Estos niveles de indirección son útiles en estructuras como listas enlazadas.

---

## 6️⃣ Intercambio de valores con punteros

```c
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

Uso:

```c
int x = 5, y = 10;
swap(&x, &y);
```

---

## 7️⃣ Casteo (Type Casting)

```c
int a = 5, b = 2;
float resultado = (float)a / b; // 2.5
```

Sin casteo, el resultado sería `2` (entero). Castear convierte el tipo para garantizar el resultado deseado.

---

## 8️⃣ `malloc` y Memoria Dinámica

`malloc` devuelve un `void *`, que debes convertir al tipo adecuado:

```c
int *puntero = (int *)malloc(sizeof(int));
*puntero = 10;
free(puntero);
```

### 📌 ¿Por qué castear?

```c
struct nodo *ap_nodo = (struct nodo *)malloc(sizeof(struct nodo));
```

* `malloc` no sabe qué tipo usas, así que casteas para indicarlo.

---

## 9️⃣ Ejemplo completo con `malloc`

```c
int *puntero = (int *)malloc(sizeof(int));
if (puntero == NULL) return 1;
*puntero = 25;
printf("Valor: %d\n", *puntero);
free(puntero);
```

---

## 🔟 Punteros y Estructuras (`->`)

```c
struct empleado {
    char nombre[20];
    float sueldo;
};

struct empleado datos = {"Juan", 3500.50};
struct empleado *emp = &datos;
printf("Nombre: %s\n", emp->nombre);
printf("Sueldo: %.2f\n", emp->sueldo);
```

---

## ✅ Resumen

* `*` desreferencia, `&` obtiene dirección
* Arreglos y punteros son equivalentes en muchos casos
* Punteros permiten modificar valores y estructuras dinámicas
* `malloc` reserva memoria, `free` la libera
* `->` accede a miembros de estructuras apuntadas

---

## 📚 Recursos Recomendados

* `man malloc`, `man pointer`, `man struct`
* [cplusplus.com - pointers](https://cplusplus.com/doc/tutorial/pointers/)
* [Valgrind - detectar errores de memoria](https://valgrind.org/)

---
