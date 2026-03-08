# Expresiones EL en Camunda – Referencia

Sintaxis y ejemplos de Expression Language (JUEL) en modelos BPMN.

## Sintaxis básica

Las expresiones se escriben entre `${` y `}`:

```
${ variableDeProceso }
${ beanDeSpring.metodo() }
${ condicion == true }
```

Se evalúan en tiempo de ejecución por el motor.

## Variables de proceso

| Expresión | Significado |
|-----------|-------------|
| `${importe}` | Valor de la variable `importe`. |
| `${solicitante}` | Valor de la variable `solicitante`. |
| `${aprobada == true}` | Expresión booleana (p. ej. en condición de gateway). |

## Uso en el modelo

| Lugar | Ejemplo |
|-------|---------|
| **Nombre de tarea** | Name: `Aprobación para ${solicitante}` |
| **Condición de flujo** | Condition: `${aprobada == true}` |
| **Asignación de tarea** | Assignee: `${asignado}` |
| **Listener / script** | Acceso a variables en expresiones o scripts. |

## Reglas

* La variable debe existir en el momento de evaluar la expresión.
* Si se usa en condiciones de gateway, la expresión debe evaluarse a booleano.
* Se pueden usar beans de Spring: `${miServicio.obtenerUsuario()}` (si el bean está en el contexto).

## Relación con los labs

* **lab06**: variables de proceso, formularios y uso de expresiones EL en nombres y condiciones.
