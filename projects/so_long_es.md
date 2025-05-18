---
layout: default
title: "fran-byte 42 Madrid — so\_long"
---

## 🔹 so\_long — Introducción al desarrollo 2D con MiniLibX

### 📌 Objetivo

Desarrollar un videojuego 2D sencillo en lenguaje C utilizando la biblioteca **MiniLibX**, consolidando conceptos clave como manejo de archivos, representación de mapas, gráficos en 2D, interacción con el teclado, validación de datos y estructuras dinámicas.

---

## 🎮 Descripción General del Proyecto

| Elemento           | Detalle                                                                      |
| ------------------ | ---------------------------------------------------------------------------- |
| Tipo de Proyecto   | Juego 2D con desplazamiento de personaje y recogida de objetos               |
| Biblioteca gráfica | MiniLibX                                                                     |
| Entrada de datos   | Archivo `.ber` que representa el mapa                                        |
| Elementos del mapa | `1`: muro, `0`: espacio vacío, `P`: jugador, `C`: coleccionable, `E`: salida |
| Objetivo del juego | Recolectar todos los `C` y llegar al `E`                                     |
| Requisitos clave   | Validación de mapa, gestión de eventos, renderizado, limpieza de memoria     |

---

## 🗂️ Estructura del Proyecto

| Archivo            | Descripción                                                             |
| ------------------ | ----------------------------------------------------------------------- |
| `so_long.c`        | Punto de entrada: lectura del mapa, inicialización principal            |
| `map_validation.c` | Comprobaciones del mapa: rectangularidad, bordes, cantidad de elementos |
| `graphics.c`       | Renderización de sprites y actualización de pantalla                    |
| `events.c`         | Interacción con el jugador: teclas, cierre de ventana                   |
| `player.c`         | Lógica de movimiento, colisiones, recogida de coleccionables            |
| `utils.c`          | Funciones auxiliares: errores, liberación de memoria, strings           |

---

## 🎨 MiniLibX: Conceptos Fundamentales

### 🔧 Inicialización y Ventana

```c
void *mlx_ptr = mlx_init();
void *win_ptr = mlx_new_window(mlx_ptr, 800, 600, "so_long");
```

### 🎨 Renderizado de Gráficos

* `mlx_xpm_file_to_image()` para cargar sprites `.xpm`
* `mlx_put_image_to_window()` para dibujar en pantalla

```c
void *img = mlx_xpm_file_to_image(mlx_ptr, "wall.xpm", &w, &h);
mlx_put_image_to_window(mlx_ptr, win_ptr, img, x * 64, y * 64);
```

### 🕹️ Gestión de Eventos

* `mlx_key_hook()` para entradas del teclado
* `mlx_loop()` inicia el bucle principal

```c
mlx_key_hook(win_ptr, &key_handler, game);
mlx_loop(mlx_ptr);
```

---

## 📏 Reglas de Validación del Mapa

1. **Rectangularidad**: todas las filas deben tener igual longitud
2. **Bordes de paredes**: todo el borde debe estar compuesto por `1`
3. **Elementos mínimos**:

   * Un solo `P`
   * Al menos un `C`
   * Al menos una `E`
4. **Ruta válida**: Debe existir camino entre `P`, todos los `C` y la `E`

💡 Tip: usa flood fill para verificar si el mapa es transitable.

---

## 🧠 Conceptos Técnicos Reforzados

### 📚 Manejo de archivos

* `open`, `read`, `close` para cargar el `.ber`
* Validación de extensión, lectura línea por línea, construcción del mapa

### 🧱 Matriz bidimensional (mapa)

* Representación del mapa como `char **map`
* Conversión del contenido del archivo en una estructura navegable

### 🎮 Movimiento del jugador

* Actualizar posición si no es muro
* Verificar si se recoge un `C`
* Verificar si se puede entrar en la `E`

### 📦 Imágenes y assets

* Formato `.xpm` obligatorio
* Una imagen para cada elemento (`wall`, `floor`, `player`, `exit`, `collectible`)

### 🧼 Limpieza de memoria

* Liberar mapa, imágenes y punteros de MiniLibX
* Implementar `free_map`, `exit_game`, y hooks para cerrar con `ESC`

---

## 🧪 Validación del Juego

```plaintext
1111111111
100100E001
101100C001
10P0010001
1111111111
```

Este mapa es válido si:

* `P` tiene camino a todos los `C`
* Hay camino desde el último `C` a `E`

---

## 🚦 Flujo General del Programa

1. **Leer y validar el mapa**
2. **Inicializar MiniLibX y cargar sprites**
3. **Renderizar el mapa**
4. **Esperar input del usuario y actualizar el juego**
5. **Verificar condiciones de victoria**
6. **Cerrar el juego limpiamente**

---

## 🧩 Recomendaciones Técnicas

* Usa estructuras para mantener el estado del juego (`t_game`, `t_map`)
* Divide la lógica de movimiento, renderizado y eventos en archivos separados
* Usa `valgrind` para comprobar fugas de memoria
* Documenta cada función en el `.h`

---

## 📚 Recursos y Lecturas Sugeridas

* [MiniLibX Linux (42Docs)](https://harm-smits.github.io/42docs/libs/minilibx)
* [Fundamentos de juegos 2D con C](https://www.gamedev.net/)

---

