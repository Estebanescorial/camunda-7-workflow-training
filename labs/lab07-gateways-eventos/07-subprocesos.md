# Subprocesos en BPMN

## 🎯 Objetivo

Usar **subprocesos embebidos** y **Call Activity** en el proceso de aprobación para agrupar pasos reutilizables o invocar otros procesos.

---

## 🧠 Contexto

**Subproceso embebido (Embedded Subprocess)**: un bloque dentro del mismo diagrama que agrupa varias tareas. El flujo entra al subproceso, ejecuta todas las actividades internas (secuencia, gateways, etc.) y sale por un único punto. Las variables del proceso padre son visibles dentro del subproceso.

**Call Activity**: invoca **otro proceso** (definido en otro BPMN) por su key. La instancia del proceso hijo se ejecuta; al terminar, el proceso padre continúa. Sirve para reutilizar flujos (ej. "Validar datos", "Notificar") en varios procesos.

| Tipo | Contenido | Reutilización |
|------|-----------|----------------|
| Subproceso embebido | Mismo archivo BPMN | No; solo agrupa en este proceso |
| Call Activity | Otro proceso (.bpmn) | Sí; varios procesos pueden llamarlo |

---

## 📋 Subproceso embebido en Camunda Modeler

1. En la **paleta de la izquierda** busca **Subprocess** (rectángulo con un signo +). Arrástralo al canvas y colócalo en el flujo donde deba ejecutarse el bloque (por ejemplo entre dos tareas).
2. Para **meter actividades dentro**: haz **doble clic** sobre el subproceso; se abrirá su interior y verás la paleta y el canvas como siempre. Añade ahí las actividades, gateways o eventos que quieras (ejemplo: una tarea "Validar datos" y, si hace falta, un gateway). Una sola conexión de entrada y una de salida; el flujo sale cuando termina el último elemento interno.
3. Para volver al nivel del proceso principal, usa el breadcrumb o la navegación que muestre el Modeler arriba (suele decir algo como el nombre del proceso o "Subprocess").

Las variables del proceso están disponibles en las expresiones y en los delegates dentro del subproceso.

---

## 📋 Call Activity

1. **Crear el proceso hijo:** Crea otro archivo BPMN (por ejemplo `validacion.bpmn` en `model/`). Ábrelo en Camunda Modeler, haz clic en el **canvas** (en una zona vacía, fuera de cualquier elemento) para seleccionar el proceso; en el **panel de propiedades a la derecha** asigna el **process key** (por ejemplo `validacion`). Guárdalo.
2. **En el proceso principal:** Abre el BPMN que uses como proceso de aprobación en este lab (por ejemplo el que tengas en **model/**). En la **paleta de la izquierda** busca **Call Activity** y arrástrala al flujo donde deba invocarse el subproceso.
3. **Selecciona** la Call Activity; en el panel de **propiedades a la derecha** busca el campo **Called element** (o "Called process") y escribe ahí el **process key** del proceso hijo (ej. `validacion`).
4. **Despliega ambos procesos** (según tu proyecto: al arrancar la aplicación si el despliegue es automático, o desde la consola/API de Camunda si lo tienes configurado así). Al ejecutar el padre, el motor crea una instancia del hijo y, al completarla, sigue en el padre.

Opcional: en las propiedades de la Call Activity puedes configurar **Input/Output mapping** para pasar variables al hijo o mapear variables del hijo al padre.

---

## 📌 Comprobación

* Con subproceso embebido: ejecutar el proceso y verificar en Cockpit que la instancia recorre las actividades dentro del subproceso.
* Con Call Activity: ver en Cockpit dos instancias (padre e hijo) y que el padre continúa tras completar el hijo.

---

## 📌 Conclusión

Los subprocesos embebidos organizan el diagrama en bloques; las Call Activity reutilizan procesos completos y mantienen modelos más simples y mantenibles.
