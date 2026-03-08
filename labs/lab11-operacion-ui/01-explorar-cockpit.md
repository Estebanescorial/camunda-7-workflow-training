# Explorar Camunda Cockpit

## 🎯 Objetivo

Aprender a utilizar **Camunda Cockpit** para inspeccionar procesos, instancias y el estado del motor.

---

## 🧠 Contexto

**Camunda Cockpit** es la herramienta principal para **operar y monitorizar el motor de procesos**.

Permite:

```
visualizar procesos desplegados
inspeccionar instancias activas
analizar errores e incidentes
ver variables de ejecución
inspeccionar jobs del motor
```

Es la herramienta que utilizarán normalmente los **operadores o administradores del sistema**.

---

# Arrancar la aplicación

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Arrancar la aplicación:

```bash
mvn spring-boot:run
```

Esperar a que el servidor arranque correctamente.

---

# Abrir Cockpit

Abre el **navegador** y en la barra de direcciones escribe: **http://localhost:8081/camunda** (usa el puerto que indique tu aplicación al arrancar; puede ser 8080 u 8081). Inicia sesión si lo pide. Entrarás en la interfaz de Camunda; **Cockpit** suele ser la vista por defecto o un enlace/pestaña visible.

---

# Explorar los procesos

En la **barra lateral izquierda** o el **menú** de Cockpit haz clic en **Processes** (o "Procesos"). Ahí se listan los procesos desplegados.

Busca en la lista el proceso **approval-process** y **haz clic** en él para ver su detalle.

---

# Inspeccionar el diagrama del proceso

Cockpit mostrará el **modelo BPMN interactivo**.

En el diagrama se puede observar:

```
instancias activas
actividades en ejecución
historial de ejecución
```

Las actividades activas se muestran resaltadas.

---

# Ver instancias del proceso

En la parte inferior aparece la sección:

```
Process Instances
```

Aquí se pueden ver todas las instancias activas del proceso.

Seleccionar una instancia para explorarla.

---

# Explorar la instancia

Dentro de la instancia se pueden ver:

```
diagrama de ejecución
variables del proceso
historial de actividades
jobs activos
```

Esto permite analizar exactamente **en qué punto del proceso se encuentra la ejecución**.

---

# Ver variables del proceso

Dentro de la instancia abrir la pestaña:

```
Variables
```

Aquí se pueden observar todas las variables del proceso.

Por ejemplo:

```
solicitante
importe
tipoSolicitud
estadoSolicitud
aprobada
```

Estas variables representan los datos de negocio del proceso.

---

# Ver el historial del proceso

Abrir la pestaña:

```
History
```

Aquí se muestra:

```
actividades ejecutadas
duración de cada tarea
estado final del proceso
```

Esto permite analizar cómo se ha ejecutado el flujo.

---

# Qué se ha aprendido

Con Cockpit se puede:

```
visualizar el estado del proceso
analizar ejecuciones
identificar errores
inspeccionar variables
```

Esto convierte a Cockpit en la principal herramienta de **operación del motor**.

---

# Comprobación

El ejercicio se considera completado cuando:

* se accede a **Camunda Cockpit**
* se abre el proceso `approval-process`
* se inspecciona una instancia del proceso
* se visualizan las variables y el historial del proceso.
