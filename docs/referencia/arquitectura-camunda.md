# Arquitectura de Camunda – Referencia

Componentes principales del motor y flujo de ejecución.

## Esquema general

```
┌─────────────────────────────────────────────────────────┐
│                  Aplicación (Spring Boot)                │
│  ┌─────────────┐  ┌──────────────┐  ┌─────────────────┐ │
│  │ Código Java │  │ Modelos BPMN │  │ Camunda Engine  │ │
│  │ (Delegates) │  │ (desplegados)│  │ (Process Engine)│ │
│  └──────┬──────┘  └──────┬───────┘  └────────┬────────┘ │
│         │                │                    │         │
│         └────────────────┴────────────────────┘         │
│                          │                               │
└──────────────────────────┼───────────────────────────────┘
                           ▼
                  ┌─────────────────┐
                  │   Base de datos  │
                  │ (estado, historial)│
                  └─────────────────┘
```

## Componentes principales

| Componente | Función |
|------------|--------|
| **Process Engine** | Ejecuta los procesos BPMN, gestiona instancias, tareas y jobs. |
| **Repository Service** | Despliegue y consulta de definiciones de proceso (BPMN). |
| **Runtime Service** | Inicio de procesos, mensajes, variables de instancias activas. |
| **Task Service** | Consulta y completado de tareas de usuario. |
| **History Service** | Consulta del historial de instancias y tareas completadas. |
| **Base de datos** | Persistencia del estado del motor (tablas `ACT_*` en H2/Postgres/etc.). |

## Mensajes típicos al arrancar

* `Process Engine default created` → motor inicializado.
* Referencias a H2, Flyway o esquema de BD → persistencia configurada.

## Relación con los labs

* **lab02**: identificar estos componentes en el arranque de la aplicación.
* **lab03**: configuración del motor en Spring Boot y acceso a Cockpit/Tasklist.
