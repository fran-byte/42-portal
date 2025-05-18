---
layout: default
title: "fran-byte 42 Madrid — so_long"
---

## 🔹 so_long — Introduction to 2D Game Development with MiniLibX

### 📌 Objective

Develop a simple 2D video game in C using the **MiniLibX** graphics library, consolidating key concepts such as file handling, map representation, 2D graphics, keyboard interaction, data validation, and dynamic structure management.

---

## 🎮 Project Overview

| Element                | Description                                                                  |
|------------------------|------------------------------------------------------------------------------|
| Project Type           | 2D game with player movement and object collection                           |
| Graphics Library       | MiniLibX                                                                     |
| Input Data             | `.ber` file representing the map                                             |
| Map Elements           | `1`: wall, `0`: empty space, `P`: player, `C`: collectible, `E`: exit        |
| Game Objective         | Collect all `C` and reach the `E`                                            |
| Key Requirements       | Map validation, event handling, rendering, memory cleanup                    |

---

## 🗂️ Project Structure

| File                  | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| `so_long.c`           | Entry point: map reading, main initialization                              |
| `map_validation.c`    | Map checks: rectangular shape, borders, element count                      |
| `graphics.c`          | Sprite rendering and screen updates                                        |
| `events.c`            | Player interaction: key presses, window close                             |
| `player.c`            | Movement logic, collisions, collectibles                                  |
| `utils.c`             | Helper functions: errors, memory management, strings                      |

---

## 🎨 MiniLibX: Core Concepts

### 🔧 Initialization and Window

```c
void *mlx_ptr = mlx_init();
void *win_ptr = mlx_new_window(mlx_ptr, 800, 600, "so_long");
````

### 🎨 Graphics Rendering

* `mlx_xpm_file_to_image()` to load `.xpm` sprites
* `mlx_put_image_to_window()` to draw on the screen

```c
void *img = mlx_xpm_file_to_image(mlx_ptr, "wall.xpm", &w, &h);
mlx_put_image_to_window(mlx_ptr, win_ptr, img, x * 64, y * 64);
```

### 🕹️ Event Handling

* `mlx_key_hook()` for key input
* `mlx_loop()` starts the main loop

```c
mlx_key_hook(win_ptr, &key_handler, game);
mlx_loop(mlx_ptr);
```

---

## 📏 Map Validation Rules

1. **Rectangular shape**: all rows must be the same length
2. **Wall borders**: all outer borders must be made of `1`
3. **Minimum required elements**:

   * Exactly one `P`
   * At least one `C`
   * At least one `E`
4. **Valid path**: a path must exist from `P` to all `C` and to `E`

💡 Tip: use flood fill to check if the map is traversable.

---

## 🧠 Reinforced Technical Concepts

### 📚 File Handling

* Use `open`, `read`, `close` to load the `.ber` file
* Validate extension, read line by line, convert to in-memory map

### 🧱 2D Matrix (Map)

* Represent the map as `char **map`
* Build it from the file contents for traversal and rendering

### 🎮 Player Movement

* Update player position if the destination is not a wall
* Check for collectible pickup
* Check if the player can enter the exit

### 📦 Images and Assets

* Only `.xpm` format allowed
* One sprite per map element: `wall`, `floor`, `player`, `exit`, `collectible`

### 🧼 Memory Management

* Free map, images, and MiniLibX pointers
* Implement `free_map`, `exit_game`, and use key hooks to handle ESC exit

---

## 🧪 Valid Game Map Example

```plaintext
1111111111
100100E001
101100C001
10P0010001
1111111111
```

This map is valid if:

* `P` can reach all `C`
* There is a path from the last `C` to `E`

---

## 🚦 General Program Flow

1. **Read and validate the map**
2. **Initialize MiniLibX and load sprites**
3. **Render the map**
4. **Wait for user input and update the game**
5. **Check win conditions**
6. **Exit the game cleanly**

---

## 🧩 Technical Recommendations

* Use structures to maintain game state (`t_game`, `t_map`)
* Split logic into separate files: rendering, movement, events
* Use `valgrind` to check for memory leaks
* Comment and prototype all functions in a `.h` file

---

## 📚 Suggested Resources

* [MiniLibX Linux (42Docs)](https://harm-smits.github.io/42docs/libs/minilibx)
* [Fundamentals of 2D Game Development in C](https://www.gamedev.net/)
  
---
