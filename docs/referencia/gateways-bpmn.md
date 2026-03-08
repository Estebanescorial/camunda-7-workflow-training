# Gateways BPMN – Referencia

Tipos de gateways y cuándo usar cada uno.

## Exclusive Gateway (XOR)

| Aspecto | Descripción |
|---------|-------------|
| **Símbolo** | Rombo con X en el centro. |
| **Comportamiento** | El flujo toma **una sola** de las ramas de salida. La primera condición que se evalúa a `true` se ejecuta. |
| **Uso típico** | Decisiones sí/no, estados (aprobado/rechazado), rutas mutuamente excluyentes. |
| **Condiciones** | En cada flujo de salida se define una condición (p. ej. `${aprobada == true}`). |

## Parallel Gateway (AND)

| Aspecto | Descripción |
|---------|-------------|
| **Símbolo** | Rombo con signo +. |
| **Comportamiento** | Todas las ramas de salida se activan en paralelo; el flujo espera a que **todas** las ramas lleguen al gateway de convergencia. |
| **Uso típico** | Tareas que pueden hacerse a la vez; reunión de ramas paralelas. |

## Inclusive Gateway (OR)

| Aspecto | Descripción |
|---------|-------------|
| **Símbolo** | Rombo con círculo. |
| **Comportamiento** | Se activan **una o más** ramas cuya condición sea verdadera. |
| **Uso típico** | Revisiones opcionales, caminos que pueden combinarse. |

## Resumen rápido

* **Una sola ruta** → Exclusive Gateway.
* **Varias rutas a la vez (todas)** → Parallel Gateway.
* **Una o varias rutas** → Inclusive Gateway.

## Relación con los labs

* **lab07**: uso de Exclusive Gateway en el proceso de aprobación; condiciones sobre variables (p. ej. `aprobada`).
