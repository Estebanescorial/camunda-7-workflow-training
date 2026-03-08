# APIs Java de Camunda – Referencia

Servicios principales del motor accesibles desde Java (Spring Boot).

## RuntimeService

Gestiona **instancias de proceso** (procesos en ejecución).

| Método / uso | Descripción |
|--------------|-------------|
| `startProcessInstanceByKey("process-id")` | Inicia una instancia por clave del proceso. |
| `startProcessInstanceByKey("id", variables)` | Inicia pasando variables. |
| `createMessageCorrelation("mensaje").correlate()` | Correlaciona un mensaje con instancias esperando. |
| `getVariable(executionId, "nombreVar")` | Obtiene variable de una ejecución. |
| `setVariable(executionId, "nombreVar", valor)` | Establece variable. |

Inyectar en Spring: `@Autowired RuntimeService runtimeService;`

## TaskService

Gestiona **tareas de usuario** (human tasks).

| Método / uso | Descripción |
|--------------|-------------|
| `createTaskQuery().taskAssignee("usuario").list()` | Lista tareas asignadas a un usuario. |
| `createTaskQuery().processInstanceBusinessKey("key").list()` | Tareas por business key. |
| `complete(taskId)` | Completa la tarea (y avanza el flujo). |
| `complete(taskId, variables)` | Completa pasando variables. |
| `setAssignee(taskId, "usuario")` | Asigna la tarea a un usuario. |

Inyectar en Spring: `@Autowired TaskService taskService;`

## RepositoryService

Consultas sobre **definiciones de proceso** (BPMN desplegados).

| Método / uso | Descripción |
|--------------|-------------|
| `createProcessDefinitionQuery().processDefinitionKey("id").latestVersion().singleResult()` | Obtiene la última versión de un proceso. |
| `createDeployment().addClasspathResource("...").deploy()` | Despliega un recurso (p. ej. BPMN). |

## HistoryService

Consultas sobre **historial** (instancias y tareas ya finalizadas).

| Método / uso | Descripción |
|--------------|-------------|
| `createHistoricProcessInstanceQuery()...` | Busca instancias históricas. |
| `createHistoricTaskInstanceQuery()...` | Busca tareas históricas. |

## Relación con los labs

* **lab09**: uso de RuntimeService para iniciar procesos y de TaskService para listar y completar tareas desde Java.
