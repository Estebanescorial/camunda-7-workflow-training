# Estructura del proyecto Spring Boot

## 🎯 Objetivo

Explorar la estructura de una aplicación **Spring Boot** identificando dónde se encuentran:

* el código Java
* los recursos del proyecto
* los procesos BPMN
* la configuración de la aplicación

Además se verificará que **Spring Boot carga automáticamente los recursos del directorio `resources`**.

---

## 🧠 Contexto

Las aplicaciones Spring Boot siguen una estructura estándar de directorios.

Esta estructura permite que el framework encuentre automáticamente:

* clases Java
* archivos de configuración
* recursos del proyecto
* modelos BPMN

Camunda aprovecha esta estructura para **localizar automáticamente los procesos BPMN**.

---

# Explorar el proyecto backend

Abre una **terminal** en VS Code (menú **Terminal** → **New Terminal**). Desde la **raíz del repositorio** (donde están **labs**, **backend** y el **README**), ejecuta:

```bash
cd backend
```

Para ver la estructura del proyecto ejecuta:

```bash
tree src
```

La estructura debería ser similar a:

```
src
├── main
│   ├── java
│   └── resources
└── test
```

---

# Identificar el código de la aplicación

En el **explorador de archivos** de VS Code (barra lateral izquierda), entra en **backend** → **src** → **main** → **java** y localiza la **clase principal** de la aplicación (suele estar en un paquete raíz, por ejemplo `com.example.workflow`). Abre el archivo **WorkflowAppApplication.java** (o el nombre que tenga tu proyecto). Si no lo encuentras, usa **Ctrl+P** y escribe `WorkflowApp` o `Application.java`.

Dentro del archivo busca la anotación:

```java
@SpringBootApplication
```

Esta anotación indica que esta clase es **el punto de arranque de Spring Boot**.

---

# Identificar los recursos del proyecto

En el explorador de VS Code, dentro de **backend**, entra en **src** → **main** → **resources**. Ahí están los recursos que carga la aplicación (configuración, estáticos, etc.).

Por ejemplo:

* configuración
* archivos estáticos
* modelos BPMN

---

# Ver dónde se almacenan los procesos BPMN

Dentro de **backend/src/main/resources** puede haber una carpeta **processes** (o similar); ahí se almacenan los modelos BPMN que Camunda despliega. Si no existe aún, la crearás al añadir procesos en labs posteriores.

Por ejemplo:

```
approval.bpmn
```

---

# Verificar que Spring Boot carga los recursos

En el explorador, dentro de **backend/src/main/resources**, **clic derecho** → **New File** (o crea el archivo desde el menú). Nombre: **test-resource.txt**. Abre el archivo y escribe en la primera línea: `Spring Boot resources test`. Guarda con **Ctrl+S**.

---

# Verificar que el archivo está en el classpath

En la **terminal**, asegúrate de estar en **backend** (si no, `cd backend` desde la raíz del repo). Ejecuta:

```bash
mvn clean package
```

Cuando termine, el archivo de prueba se habrá copiado a **target/classes**. Para comprobarlo, ejecuta:

```bash
ls target/classes
```

Debería aparecer el archivo:

```
test-resource.txt
```

Esto demuestra que **Spring Boot copia automáticamente los recursos al classpath durante la compilación**.

---

# Qué significa esto para Camunda

El motor Camunda utiliza este mismo mecanismo para localizar los procesos BPMN.

Cuando la aplicación arranca:

1. Spring Boot carga los recursos del classpath
2. Camunda escanea el directorio `processes`
3. los archivos BPMN encontrados se despliegan automáticamente

---

# Comprobación

El ejercicio se considera completado cuando:

* se ha identificado la estructura del proyecto
* se ha localizado el directorio `resources`
* se ha creado un recurso de prueba
* se ha comprobado que el archivo aparece en `target/classes`.
