# Elementos BPMN – Referencia rápida

Resumen de los elementos básicos de BPMN 2.0 usados en el curso.

## Eventos

| Elemento | Símbolo | Uso |
|----------|---------|-----|
| **Evento de inicio** | Círculo simple (verde en Camunda) | Punto donde comienza el proceso. Todo proceso tiene uno. |
| **Evento de fin** | Círculo con borde grueso (rojo en Camunda) | Final de un flujo. Puede haber varios. |
| **Evento intermedio** | Círculo con doble borde | Mensaje, temporizador, señal, etc. |

## Actividades

| Elemento | Símbolo | Uso |
|----------|---------|-----|
| **Tarea** | Rectángulo con bordes redondeados | Una unidad de trabajo (manual o automática). |
| **User Task** | Rectángulo con icono de persona | Tarea que realiza un usuario en Tasklist. |
| **Service Task** | Rectángulo con icono de engranaje | Tarea ejecutada por el motor (delegación a Java, etc.). |

## Flujo y decisiones

| Elemento | Símbolo | Uso |
|----------|---------|-----|
| **Flujo de secuencia** | Flecha continua | Orden de ejecución entre elementos. |
| **Gateway (genérico)** | Rombo | Punto de divergencia o convergencia del flujo. |

## Convenciones en Camunda Modeler

* **Pool**: rectángulo que engloba el proceso. El **Process Id** y **Executable = true** son necesarios para que el motor ejecute el proceso.
* **Name** vs **Id**: el nombre se muestra en el diagrama; el id se usa en código y despliegue.

## Relación con los labs

* **lab01**: identificar estos elementos en un diagrama existente.
* **lab04**: crear y configurar eventos de inicio/fin, User Tasks y Service Tasks en Camunda Modeler.
