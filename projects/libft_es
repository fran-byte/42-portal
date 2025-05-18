## 🔹 1. Fundamentos previos (antes de atacar libft)

### 📌 Objetivo:

Tener **todas las herramientas técnicas y conceptuales** necesarias para empezar Libft **con confianza**, evitando errores comunes y entendiendo **lo que estás haciendo y por qué**.

---

### 🛠️ Cómo compilar en C (`gcc`, flags, `Makefile`)

#### ✅ ¿Qué es compilar?

Es el proceso de transformar tu código fuente `.c` en **código máquina ejecutable**. El compilador más usado en 42 es `gcc`.

#### 🔧 ¿Qué es `gcc` y cómo se usa?

```bash
gcc -Wall -Wextra -Werror archivo.c -o ejecutable
```

* **`-Wall`**: muestra los *warnings* estándar.
* **`-Wextra`**: muestra más advertencias.
* **`-Werror`**: convierte los *warnings* en errores (esto te obliga a escribir código limpio).
* **`-o`**: indica el nombre del archivo ejecutable resultante.

> ⚠️ En los proyectos de 42, **estos flags son obligatorios**, y tu código debe compilar **sin ningún warning**.

---

#### 🧱 ¿Qué es un Makefile?

Un **Makefile** es un script que automatiza el proceso de compilación. En lugar de escribir varios comandos manualmente, defines reglas que lo hacen por ti. Es obligatorio en Libft.

#### 🧪 Ejemplo básico de Makefile para Libft:

```make
NAME = libft.a
SRC = ft_strlen.c ft_isalpha.c
OBJ = $(SRC:.c=.o)

CC = cc
CFLAGS = -Wall -Wextra -Werror

all: $(NAME)

$(NAME): $(OBJ)
	ar rcs $(NAME) $(OBJ)

clean:
	rm -f $(OBJ)

fclean: clean
	rm -f $(NAME)

re: fclean all
```

* **`ar rcs`**: crea la librería estática (`.a`)
* **Reglas obligatorias**: `all`, `clean`, `fclean`, `re`, y `$(NAME)`
* **No debe hacer relink**: no compiles más veces de lo necesario

---

### 📦 Qué es una librería estática (`.a`)

Una **librería estática** es un archivo que **contiene código ya compilado**, listo para reutilizar. En vez de copiar funciones en cada nuevo proyecto, puedes simplemente enlazar tu `libft.a`.

#### 📌 ¿Cómo se usa?

1. La creas con:

```bash
ar rcs libft.a ft_strlen.o ft_isalpha.o ...
```

2. La usas así:

```bash
gcc main.c -L. -lft -o programa
```

* `-L.` le dice a gcc que busque librerías en el directorio actual
* `-lft` busca `libft.a` (se le quita el "lib" y el ".a")

---

### 📚 Uso de `man` y documentación oficial

#### ✅ ¿Qué es `man`?

`man` viene de "manual". Te muestra la documentación de funciones del sistema.

Por ejemplo:

```bash
man strlen
```

Te mostrará:

* El prototipo: `size_t strlen(const char *s);`
* Qué hace: cuenta los caracteres hasta `\0`
* Qué devuelve: un número (`size_t`)
* Qué errores puede devolver: en este caso, ninguno

#### 🧠 ¿Por qué es vital en 42?

Debes **reimplementar funciones estándar**, como `memcpy`, `strchr`, etc. El *man* es la fuente oficial para saber cómo deben comportarse **exactamente**.

---

### 🧬 Anatomía de una función en C

Vamos a desglosar una función paso a paso:

```c
int ft_strlen(const char *s)
{
    int i = 0;
    while (s[i])
        i++;
    return i;
}
```

#### Partes clave:

* `int`: tipo de retorno. La función devuelve un número.
* `ft_strlen`: nombre de la función. Todas tus funciones deben empezar con `ft_`.
* `const char *s`: parámetro de entrada. Es una cadena que **no vas a modificar**.
* `{ ... }`: el cuerpo de la función.
* `while (s[i])`: recorre la cadena hasta encontrar `\0`.
* `return i`: devuelve la longitud.

> ✨ Recomendación: antes de escribir el código, **piensa la lógica en español o pseudocódigo**.

---

### 🧾 Tipos de datos estándar

| Tipo     | Significado                         | Ejemplo               |
| -------- | ----------------------------------- | --------------------- |
| `int`    | Entero (positivo o negativo)        | `int x = -42;`        |
| `char`   | Carácter (letra, número, símbolo)   | `char c = 'A';`       |
| `void`   | Sin tipo / no devuelve nada         | `void ft_print(void)` |
| `size_t` | Tamaño sin signo (usado en strings) | `size_t len = 5;`     |

#### 📌 ¿Qué es `size_t`?

Es un tipo sin signo (positivo) usado para tamaños de memoria y longitudes.

Por ejemplo:

```c
size_t ft_strlen(const char *s);
```

Usarlo te evita errores con valores negativos y te garantiza portabilidad (en 32 o 64 bits).

---

### 🔗 Punteros y arrays básicos

#### ✅ ¿Qué es un puntero?

Un puntero es una variable que **guarda la dirección de otra variable**.

```c
int x = 10;
int *p = &x;  // p apunta a x
```

Puedes acceder al valor de `x` a través del puntero:

```c
printf("%d\n", *p);  // imprime 10
```

---

#### ✅ ¿Y un array?

Un array es una **colección de elementos del mismo tipo en memoria contigua**.

```c
char saludo[] = "Hola";
```

Esto es casi igual a:

```c
char *saludo = "Hola";
```

En ambos casos, `saludo[0]` vale `'H'`, `saludo[1]` vale `'o'`, etc.

---

#### 📌 Relación con Libft:

Muchas funciones de Libft usan punteros:

* `const char *s` → apunta al comienzo de una cadena
* `char *dst, const char *src` → para copiar datos
* `void *b` → para funciones genéricas (como `memset`)

> Entender bien cómo funcionan punteros y arrays es **clave** para no tener errores como segfaults o buffer overflows.

---

### 🧠 Consejos prácticos

* **Haz pruebas pequeñas en archivos separados** antes de integrar en tu libft.
* Usa `valgrind` para detectar errores de memoria (especialmente más adelante con `malloc`).
* Lee los `man` antes de empezar cada función, **aunque creas saber lo que hacen**.
* Empieza implementando funciones **sencillas** (como `ft_isalpha`) para familiarizarte.
* Usa `printf` para depurar. No tengas miedo de imprimir valores para entenderlos.

