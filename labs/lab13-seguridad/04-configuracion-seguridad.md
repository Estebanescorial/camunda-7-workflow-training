# Configuración básica de seguridad

## 🎯 Objetivo

Configurar la **seguridad básica del motor Camunda** utilizando autenticación integrada y comprobar cómo afecta al acceso a Cockpit, Tasklist y Admin.

---

## 🧠 Contexto

Camunda incluye un sistema de autenticación integrado basado en:

```id="t6d03l"
usuarios
grupos
autorizaciones
```

Cuando la seguridad está activada:

```id="y7s31p"
los usuarios deben autenticarse
los permisos se verifican en cada acción
las aplicaciones web aplican control de acceso
```

Las aplicaciones afectadas son:

```id="c2r9lj"
Cockpit
Tasklist
Admin
```

---

# Verificar la autenticación

Arrancar la aplicación:

```bash id="n4a5jd"
cd backend
mvn spring-boot:run
```

Abrir el navegador:

```id="p8e3kq"
http://localhost:8081/camunda
```

La aplicación mostrará una pantalla de login.

---

# Crear un usuario administrador

Abrir:

```id="a9j0nt"
http://localhost:8081/camunda/app/admin
```

Ir a:

```id="b6c1sw"
Users
```

Seleccionar:

```id="z4l1xp"
Create New User
```

Introducir:

```id="r0y3c4"
User ID: admin
First Name: Admin
Last Name: User
Password: admin
Email: admin@workflow.local
```

Guardar el usuario.

---

# Crear grupo de administradores

Ir a:

```id="4p6t4m"
Groups
```

Seleccionar:

```id="1s1k1p"
Create New Group
```

Configurar:

```id="v3b5d7"
Group ID: administrators
Name: Administrators
Type: SYSTEM
```

Guardar el grupo.

---

# Añadir usuario al grupo

Abrir el grupo:

```id="b7h9l3"
administrators
```

Seleccionar:

```id="1s7h1q"
Add Member
```

Añadir el usuario:

```id="z7t7k5"
admin
```

---

# Conceder permisos administrativos

Ir a:

```id="2m8o8v"
Authorizations
```

Crear una nueva autorización.

Configurar:

```id="t7j4n4"
Type: Grant
Group: administrators
Resource: All
Permissions: ALL
```

Guardar la autorización.

---

# Verificar acceso

Cerrar sesión.

Abrir nuevamente:

```id="o6s3g3"
http://localhost:8081/camunda
```

Iniciar sesión con:

```id="f3g8f2"
usuario: admin
password: admin
```

El usuario debería poder acceder a:

```id="y2h7p9"
Cockpit
Tasklist
Admin
```

---

# Qué ocurre internamente

Cuando un usuario accede a la plataforma:

```id="p5t3e4"
usuario se autentica
        │
        ▼
Camunda identifica sus grupos
        │
        ▼
se verifican autorizaciones
        │
        ▼
se permite o bloquea el acceso
```

Esto garantiza que solo usuarios autorizados puedan interactuar con el sistema.

---

# Comprobación

El ejercicio se considera completado cuando:

* se crea un usuario administrador
* se crea el grupo `administrators`
* el usuario pertenece al grupo
* el usuario puede acceder a Cockpit, Tasklist y Admin.
# Testing de procesos

## 🎯 Objetivo

Crear un **test automatizado** que verifique la ejecución de un proceso BPMN utilizando **JUnit y el motor Camunda**.

---

## 🧠 Contexto

Los procesos BPMN pueden probarse igual que cualquier otro componente de software.

Un test puede verificar:

```id="7a6n8p"
que un proceso se inicia correctamente
qué tareas se ejecutan
qué variables se generan
si el proceso termina correctamente
```

Camunda permite ejecutar estos tests utilizando el motor embebido dentro del test.

---

# Crear el archivo de test

Crear el archivo:

```id="g9k2o1"
backend/src/test/java/com/example/workflow/ProcesoApprovalTest.java
```

---

# Añadir el test básico

Añadir el siguiente código:

```java id="f1q2z9"
package com.example.workflow;

import org.camunda.bpm.engine.RuntimeService;
import org.camunda.bpm.engine.runtime.ProcessInstance;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

import static org.assertj.core.api.Assertions.assertThat;

@SpringBootTest
public class ProcesoApprovalTest {

    @Autowired
    private RuntimeService runtimeService;

    @Test
    void iniciarProceso() {

        ProcessInstance instance = runtimeService.startProcessInstanceByKey("approval-process");

        assertThat(instance).isNotNull();
        assertThat(instance.isEnded()).isFalse();

    }
}
```

Este test verifica que el proceso puede iniciarse correctamente.

---

# Ejecutar los tests

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Ejecutar los tests:

```bash id="f0h6c8"
mvn test
```

El test debería ejecutarse correctamente.

---

# Añadir variables al test

Modificar el test para iniciar el proceso con variables.

```java id="t3v5j7"
@Test
void iniciarProcesoConVariables() {

    ProcessInstance instance = runtimeService.startProcessInstanceByKey(
            "approval-process",
            java.util.Map.of(
                    "solicitante", "juan",
                    "importe", 1000,
                    "tipoSolicitud", "COMPRA"
            )
    );

    assertThat(instance).isNotNull();
}
```

Esto permite probar distintos escenarios del proceso.

---

# Qué ocurre durante el test

Durante la ejecución del test:

```id="b9e0k1"
Spring Boot inicia el contexto
        │
        ▼
Camunda arranca el motor
        │
        ▼
se despliega el proceso BPMN
        │
        ▼
el test ejecuta el proceso
```

Esto permite validar el comportamiento del workflow automáticamente.

---

# Ventajas del testing de procesos

El testing permite:

```id="y2v4d6"
detectar errores en modelos BPMN
validar reglas de negocio
probar diferentes escenarios
evitar regresiones
```

---

# Comprobación

El ejercicio se considera completado cuando:

* se crea un test para el proceso
* el test inicia el proceso BPMN
* el test se ejecuta correctamente con `mvn test`.
