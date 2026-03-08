# Configurar dependencias de Camunda

## 🎯 Objetivo

Identificar la dependencia que permite integrar **Camunda con Spring Boot** y comprobar qué componentes se añaden al proyecto cuando se incluye.

---

## 🧠 Contexto

Camunda se integra con Spring Boot mediante **starter dependencies**.

Un *starter* es una dependencia que instala automáticamente:

* el motor Camunda
* la configuración básica
* la integración con Spring
* las aplicaciones web de Camunda

En este proyecto se utiliza el **starter oficial de Camunda para Spring Boot**.

---

# Localizar las dependencias del proyecto

En el **explorador de archivos** (izquierda), entra en la carpeta **backend** y haz clic en **pom.xml** para abrirlo. O usa **Ctrl+P** y escribe `pom.xml`. Dentro del archivo busca el bloque:

```xml
<dependencies>
```

Localizar la dependencia de Camunda:

```xml
<dependency>
    <groupId>org.camunda.bpm.springboot</groupId>
    <artifactId>camunda-bpm-spring-boot-starter-webapp</artifactId>
    <version>7.19.0</version>
</dependency>
```

---

# Qué añade esta dependencia

Esta dependencia instala automáticamente varios componentes:

```
Camunda Process Engine
Camunda Cockpit
Camunda Tasklist
Camunda Admin
REST API del motor
Integración con Spring Boot
```

No es necesario instalar cada componente por separado.

---

# Explorar las dependencias descargadas

Para ver qué dependencias instala Maven ejecutar:

```bash
mvn dependency:tree
```

Este comando muestra todas las dependencias utilizadas por el proyecto.

Buscar en la salida elementos relacionados con Camunda, por ejemplo:

```
camunda-engine
camunda-webapp
camunda-engine-spring
```

Esto confirma que el motor Camunda se ha añadido al proyecto.

---

# Identificar otras dependencias importantes

Dentro del `pom.xml` también aparecen otras dependencias relevantes.

Por ejemplo:

```
spring-boot-starter-web
```

Permite crear aplicaciones web con Spring Boot.

```
spring-boot-starter-data-jpa
```

Permite trabajar con persistencia de datos mediante JPA.

```
h2
```

Base de datos embebida utilizada durante el desarrollo.

---

# Verificar que Maven descarga las dependencias

Ejecutar nuevamente la compilación:

```bash
mvn clean install
```

Durante la compilación Maven descargará las dependencias que aún no estén en el repositorio local.

---

# Comprobación

El ejercicio se considera completado cuando:

* se localiza la dependencia de Camunda en el `pom.xml`
* se ejecuta `mvn dependency:tree`
* se identifican las librerías relacionadas con Camunda en el árbol de dependencias.
