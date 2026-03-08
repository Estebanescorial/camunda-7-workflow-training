# Lab 07 — Gateways y eventos

## 🎯 Objetivo

Aprender a controlar el flujo de ejecución de un proceso BPMN utilizando **gateways y eventos**.

En este laboratorio se aprenderá a:

* crear decisiones en el flujo del proceso
* definir condiciones basadas en variables
* utilizar eventos temporizadores
* utilizar eventos de mensaje
* configurar listeners (execution y task)
* usar subprocesos embebidos y Call Activity
* probar distintos caminos del proceso

---

# 🧠 Contexto

Hasta ahora los procesos BPMN ejecutaban actividades de forma secuencial.

Sin embargo, en procesos reales es necesario:

```text id="c1q9e6"
tomar decisiones
esperar eventos
reaccionar a mensajes externos
```

BPMN proporciona distintos mecanismos para controlar el flujo del proceso.

Los más utilizados son:

```text id="y6f3g2"
Gateways
Events
```

---

# 🔀 Gateways

Los **gateways** permiten tomar decisiones dentro del proceso.

Por ejemplo:

```text id="x7k4p5"
si importe > 5000 → revisión especial
si importe <= 5000 → aprobación normal
```

Este comportamiento se modela mediante un **Exclusive Gateway**.

---

# ⏱ Eventos

Los **eventos** permiten que el proceso reaccione a situaciones externas.

Ejemplos:

```text id="s8z2h1"
esperar un temporizador
recibir un mensaje
reaccionar a un error
```

Esto permite que los procesos sean **reactivos**.

---

# 🔎 Qué vamos a hacer en este laboratorio

Se ampliará el proceso de aprobación para introducir:

```text id="t0w3p7"
decisiones basadas en variables
eventos temporizadores
eventos de mensaje
```

Esto permitirá crear flujos más complejos y cercanos a escenarios reales.

---

# 📘 Ejercicios del laboratorio

### 01 — Exclusive Gateway

Crear una decisión dentro del proceso utilizando un gateway.

Archivo:

```text id="d6k9y4"
01-exclusive-gateway.md
```

---

### 02 — Condiciones del flujo

Configurar condiciones en los flujos del proceso basadas en variables.

Archivo:

```text id="r4v1z8"
02-condiciones-flujo.md
```

---

### 03 — Eventos temporizador

Crear un evento que haga que el proceso espere un tiempo determinado.

Archivo:

```text id="m2f7x9"
03-eventos-temporizador.md
```

---

### 04 — Eventos de mensaje

Crear un evento que permita reactivar el proceso cuando se reciba un mensaje.

Archivo:

```text id="p5n8w1"
04-eventos-mensaje.md
```

---

### 05 — Pruebas del flujo

Ejecutar el proceso con distintos valores de variables para comprobar cómo cambia el flujo.

Archivo:

```text id="z1t6g3"
05-pruebas-flujo.md
```

---

### 06 — Listeners

Configurar execution listeners y task listeners para logging, variables y auditoría.

Archivo:

```
06-listeners.md
```

---

### 07 — Subprocesos

Usar subprocesos embebidos y Call Activity para agrupar pasos e invocar otros procesos.

Archivo:

```
07-subprocesos.md
```

---

# 🧪 Resultado esperado

Al finalizar este laboratorio el proceso será capaz de:

```text id="v8y0k4"
tomar decisiones basadas en variables
esperar eventos temporales
reaccionar a mensajes externos
```

Esto permitirá modelar procesos más complejos y dinámicos.

---

# 🔜 Próximo laboratorio

En el siguiente laboratorio se estudiará cómo **desplegar y versionar procesos BPMN**, permitiendo actualizar procesos en producción sin interrumpir instancias existentes.
