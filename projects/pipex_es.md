---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Fundamentos Previos (Antes de Empezar Philosophers)

### 📌 Objetivo:

Este proyecto se centra en la **programación concurrente**. Te desafía a resolver un problema clásico de la informática que enseña cómo gestionar de manera eficiente y segura **recursos compartidos** entre múltiples hilos. Los conceptos clave son **concurrencia**, **sincronización** y el uso de **hilos (threads)** y **mutexes**.

Un grupo de filósofos alterna entre tres actividades: **comer**, **pensar** y **dormir**. Su acceso a los recursos necesarios (tenedores) es limitado, y la solución está en asegurar que cada filósofo pueda completar sus ciclos **sin conflictos ni bloqueos**.

---

## 🔹 2. El Problema de los Filósofos Comensales

Propuesto originalmente por **Edsger Dijkstra**, es una metáfora clásica en la programación concurrente: varios procesos (filósofos) deben coordinarse para acceder a recursos compartidos limitados (tenedores), evitando **interbloqueos**, **inanición** o **condiciones de carrera**.

### 📅 Planteamiento del Problema

* Cinco filósofos están sentados en una mesa redonda.
* Cada uno alterna entre **comer**, **pensar** y **dormir**.
* Hay cinco tenedores, uno entre cada par de filósofos.
* Para comer, un filósofo necesita **el tenedor de la izquierda y el de la derecha**.
* Tras comer, piensan, luego duermen, y repiten el ciclo.

Problemas pueden surgir si no hay una correcta sincronización:

### 🔒 Problemas Clave

* **Interbloqueo (Deadlock)**: Cada filósofo toma un tenedor y espera indefinidamente el otro.
* **Inanición (Starvation)**: Algunos nunca logran comer porque otros acaparan los recursos.
* **Condiciones de carrera (Race conditions)**: Varios intentan acceder al mismo tenedor simultáneamente, generando inconsistencias.

---

## 🔹 3. Conceptos Teóricos

Este proyecto introduce dos herramientas críticas para la concurrencia:

### 🔢 Hilos (Threads)

* Un hilo es la unidad más pequeña de ejecución.
* Comparten memoria/recursos del proceso padre, siendo ligeros pero propensos a conflictos de estado compartido.
* Cada filósofo es un hilo independiente.

En C, usarás **POSIX Threads (pthreads)**:

* `pthread_create` → Crea un nuevo hilo.
* `pthread_join` → Espera a que termine un hilo.
* `pthread_exit` → Finaliza un hilo correctamente.
* Usa `usleep` para simular pausas.

### ⏳ Cambio de Contexto (Context Switching)

* Los hilos no se ejecutan verdaderamente en paralelo (salvo múltiples núcleos).
* El SO alterna entre ellos rápidamente.
* La **sincronización adecuada** es esencial.

### 🔐 Mutexes (Exclusión Mutua)

* Los mutexes previenen el acceso simultáneo a recursos compartidos.
* Cada tenedor está protegido por un mutex.

Funciones clave:

* `pthread_mutex_init`
* `pthread_mutex_lock`
* `pthread_mutex_unlock`
* `pthread_mutex_destroy`

Los filósofos deben:

* Bloquear los mutex de los dos tenedores para comer.
* Liberarlos al terminar.

---

## 🔹 4. Estrategias de Solución

### 🔎 Asignación Ordenada de Recursos

* Algunos filósofos toman primero el tenedor izquierdo, otros el derecho.
* Reduce el riesgo de esperas circulares.

### ❌ Limitar Filósofos Comiendo Concurrentemente

* Solo permite que (N - 1) filósofos intenten comer al mismo tiempo.

### 🔼 Jerarquía de Tenedores

* Asigna un orden a los tenedores.
* Los filósofos deben tomarlos siempre en orden ascendente.

---

## 📃 Estructura del Proyecto

### Descripción:

El proyecto **Philosophers** simula el problema usando hilos y mutexes.

### Estructura de Archivos:

```
philosophers/
├── philo.c               // Entrada principal, validación de argumentos
├── philo_utils.c         // Utilidades de tiempo, atoi, sleep
├── philo_start.c         // Inicialización y arranque de simulación
├── philo_create.c        // Rutina de filósofos (comer, dormir, pensar)
├── philo_monitor_deaths.c // Monitoreo de inanición
├── philo.h               // Header con estructuras, constantes y prototipos
```

---

## 📈 Características Principales

### 📊 Validación de Argumentos

* Requiere 4 o 5 argumentos: número de filósofos, tiempo para morir, para comer, para dormir, \[comidas requeridas]
* Todos deben ser enteros positivos.

### ⚖️ Inicialización de la Simulación

* Se inicializan tenedores (mutexes) y filósofos.
* Se crea un hilo por filósofo.

### 🤔 Ciclo de Vida del Filósofo

* `take_forks`: bloquear tenedores izquierdo y derecho
* Comer → dormir → pensar
* Se maneja especialmente el caso de un solo filósofo.

### 🔎 Monitoreo de Muertes

* `monitor_deaths`: hilo independiente
* Verifica si algún filósofo excedió `time_to_die` sin comer
* Si ocurre, registra e interrumpe la simulación

### ⚖️ Sincronización

* Mutexes aseguran acceso exclusivo a tenedores
* Mensajes en consola también están protegidos con mutex

---

## 🔴 Resumen de `philo_monitor_deaths.c`

### Función: `monitor_deaths`

* Verifica continuamente el tiempo desde la última comida de cada filósofo
* Si `tiempo_desde_ultima_comida > time_to_die`:

  * Imprime mensaje de muerte
  * Detiene la simulación

Mutexes protegen el acceso compartido a `last_meal` para evitar condiciones de carrera.

---

## 📝 Casos de Prueba

Dentro de `philo_start.c`:

```c
// Nadie debería morir:
./philo 5 800 200 200
./philo 5 600 150 150
./philo 4 410 200 200
./philo 100 800 200 200
./philo 105 800 200 200
./philo 200 800 200 200

// Un filósofo debería morir:
./philo 1 800 200 200
./philo 4 310 200 100
./philo 4 200 205 200

// Casos con error:
./philo -5 600 200 200
./philo 4 -5 200 200
./philo 4 600 -5 200
./philo 4 600 200 -5
./philo 4 600 200 200 -5

// Verificación de fugas de memoria:
valgrind --leak-check=full --track-origins=yes --show-leak-kinds=all ./philo
```

---

## 💡 Valgrind

Siempre usa **Valgrind** para detectar fugas de memoria y asegurar el correcto manejo:

```bash
valgrind --leak-check=full --track-origins=yes --show-leak-kinds=all ./philo 5 800 200 200
```

---
