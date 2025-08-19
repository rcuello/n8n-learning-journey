# 🗄️ Guía de las Tablas de la Base de Datos de n8n

## 📊 Introducción

n8n utiliza **PostgreSQL** para almacenar toda la información sobre workflows, ejecuciones, credenciales y configuraciones.
Esta guía describe las tablas más importantes y su propósito dentro de la plataforma.

---

## 🚀 Tablas Principales (Core)

### 📝 `workflow_entity`

**Propósito**: Contiene la definición completa de todos los workflows creados en n8n, incluyendo nodos, conexiones y configuraciones.

### 🔄 `execution_entity`

**Propósito**: Registra cada ejecución de workflows, guardando información sobre el estado, las fechas, los datos procesados y un snapshot del workflow ejecutado.

---

## 🔐 Tablas de Seguridad

### 🗝️ `credentials_entity`

**Propósito**: Almacena credenciales encriptadas para conexiones externas.

> ⚠️ Importante: los datos están encriptados; no se exponen contraseñas en texto plano.

### 🔒 `shared_credentials`

**Propósito**: Gestiona qué usuarios tienen acceso a credenciales específicas y bajo qué rol.

### 🤝 `shared_workflow`

**Propósito**: Define los permisos de usuarios sobre workflows compartidos (propietario, editor, lector).

---

## 🌐 Tablas de Triggers y Webhooks

### 🎣 `webhook_entity`

**Propósito**: Registra los webhooks activos, incluyendo la ruta, el método HTTP y el nodo que los gestiona.

### 📅 `event_destinations`

**Propósito**: Configuración de destinos donde se envían eventos generados por n8n.

---

## 📈 Tablas de Metadatos y Análisis

### 📊 `execution_metadata`

**Propósito**: Almacena metadatos adicionales asociados a las ejecuciones.

### 🏷️ `execution_annotation_tags`

**Propósito**: Permite etiquetar ejecuciones para organización o clasificación.

### 📝 `execution_annotations`

**Propósito**: Guarda comentarios y anotaciones sobre ejecuciones específicas.

### 📈 `workflow_statistics`

**Propósito**: Contiene estadísticas de rendimiento y métricas de workflows.

---

## 👥 Tablas de Usuarios y Autenticación

### 👤 `user`

**Propósito**: Información básica de los usuarios del sistema, incluyendo datos de identificación y autenticación.

### 🔑 `auth_identity`

**Propósito**: Relaciona usuarios con identidades de autenticación.

### 📜 `auth_provider_sync_history`

**Propósito**: Historial de sincronización con proveedores de identidad externos.

### 🚫 `invalid_auth_token`

**Propósito**: Lista tokens de autenticación que fueron invalidados.

---

## 🛠️ Tablas de Configuración

### ⚙️ `settings`

**Propósito**: Configuraciones globales del sistema.

### 🧩 `installed_nodes`

**Propósito**: Registra nodos personalizados que fueron instalados en la plataforma.

### 📦 `installed_packages`

**Propósito**: Guarda información de los paquetes npm instalados en el entorno.

### 🔄 `migrations`

**Propósito**: Controla el estado de las migraciones de base de datos aplicadas.

---

## 📁 Tablas de Organización

### 🏷️ `tag_entity`

**Propósito**: Almacena tags para clasificar workflows.

### 🔗 `workflow_tag_mapping`

**Propósito**: Relación entre workflows y sus tags correspondientes.

---

## 📂 Tablas de Proyectos y Variables

### 📁 `project`

**Propósito**: Representa proyectos como contenedores de organización.

### 🔗 `project_relation`

**Propósito**: Define relaciones entre proyectos y recursos.

### 🔧 `variables`

**Propósito**: Contiene variables globales definidas en el sistema.

---

## 🧪 Tablas de Testing

### 🧪 `test_case_execution`

**Propósito**: Guarda los resultados de ejecuciones de casos de prueba.

### 🏃 `test_run`

**Propósito**: Almacena la información de ejecuciones de conjuntos de pruebas.

---

## 💡 Tips y Mejores Prácticas

* Para debugging, las tablas más útiles son: `execution_entity`, `execution_metadata` y `workflow_entity`.
* Para análisis, combina información de `workflow_entity`, `execution_entity` y `workflow_statistics`.
* En seguridad, nunca intentes desencriptar credenciales directamente en `credentials_entity`.
* Antes de modificar cualquier dato en estas tablas, considera los riesgos y realiza respaldos.

---

## ⚠️ Precauciones

* No modificar registros directamente sin comprender las implicaciones.
* Hacer backups periódicos de la base de datos.
* Tener cuidado con el tamaño de campos como `data` en `execution_entity`, ya que pueden ser muy grandes.
* Evitar consultas complejas sobre tablas de gran tamaño sin índices adecuados.

---

✅ Con esta guía tendrás una visión clara de cómo n8n organiza y almacena la información en PostgreSQL, sin depender de columnas específicas que puedan cambiar en futuras versiones.


