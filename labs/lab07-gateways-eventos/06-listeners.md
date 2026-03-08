# Listeners en BPMN

## 🎯 Objetivo

Configurar **listeners** (execution y task) en elementos del proceso para ejecutar lógica en momentos concretos del ciclo de vida (inicio/fin de actividad o proceso), sin modificar el flujo principal.

---

## 🧠 Contexto

Los **listeners** permiten reaccionar a eventos del motor:

* **Execution Listener**: se ejecuta en eventos de un flujo (start, end) en actividades, gateways o el proceso. Útil para logging, setear variables, auditoría o notificaciones.
* **Task Listener**: solo en **User Tasks**; eventos como create, complete, assignment. Útil para asignar candidatos, enviar notificaciones al crear la tarea o registrar quién la completó.

Cada listener puede ser:

* **Expression**: expresión EL (ej. `${logger.info(execution.id)}`).
* **Delegate Expression**: bean de Spring (ej. `${miExecutionListener}`).
* **Class**: clase Java que implemente `ExecutionListener` o `TaskListener`.
* **Script**: script (JavaScript, Groovy, etc.) inline o externo.

---

## 📋 Execution Listener en Camunda Modeler

1. **Selecciona** en el diagrama un nodo (una actividad, un gateway o el propio proceso): haz clic en él.
2. A la **derecha** de la ventana suele estar el panel **Properties** (Propiedades). Si no lo ves, prueba con el menú **Window** → **Show Properties** o similar. Ese panel muestra las opciones del elemento seleccionado.
3. Dentro del panel Properties busca la sección **Listeners**. Ahí se configuran los execution y task listeners.
4. Pulsa **Add** (o "Añadir") y elige **Execution Listener**. Tendrás que elegir:
   * **Event**: start o end (cuándo se ejecuta: al entrar o al salir del nodo).
   * **Type**: Expression, Delegate Expression, Class o Script.
   * El **valor** según el tipo (por ejemplo, la expresión o el nombre del bean).

Ejemplo con expresión (solo para ver un log):

* Event: **start**
* Type: **Expression**
* Expression: `${logger.info("Nodo ejecutado: " + execution.getCurrentActivityId())}`

Para usar una clase Java: crea una clase que implemente `org.camunda.bpm.engine.delegate.ExecutionListener` (método `notify`) y referénciala con **Delegate Expression** (ej. `${miListener}`) registrando el bean en Spring.

---

## 📋 Task Listener en User Task

1. En el diagrama, **haz clic** en una **User Task** (la tarea de usuario que quieras).
2. En el panel **Properties** (a la derecha), entra en la misma sección **Listeners**.
3. Añade un **Task Listener** (no Execution Listener). Los eventos que suelen usarse son **create**, **complete** y **assignment** (cuando se asigna la tarea a alguien).
4. Elige evento, tipo (expression, delegate, class, script) y el valor. Por ejemplo: al **create**, con una expresión, puedes asignar una variable (ej. fecha de creación); al **complete**, puedes guardar en una variable el `assignee` (está disponible en el contexto de la expresión).

---

## 📌 Comprobación

Después de añadir un execution listener en una actividad del **proceso que estés usando en este lab** (por ejemplo el proceso de aprobación que tengas en **model/**): arranca la aplicación, inicia una instancia del proceso y revisa los logs. Al pasar por ese nodo debería aparecer el mensaje o el efecto del listener (log o variable). Si no ves nada, comprueba que el listener está en el nodo correcto y que el evento (start/end) es el que esperas.

---

## 📌 Conclusión

Los listeners permiten desacoplar lógica transversal (logging, variables, notificaciones, auditoría) del flujo BPMN y de las tareas de servicio, manteniendo el diagrama más limpio y la lógica reutilizable.
