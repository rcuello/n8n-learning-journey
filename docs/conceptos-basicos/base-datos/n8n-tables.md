# 🗄️ Guía de las Tablas de la Base de Datos de n8n

## 📊 Introducción

[n8n](https://docs.n8n.io/hosting/architecture/database-structure/#database-and-query-technology) utiliza una base de datos relacional para almacenar toda la información sobre workflows, ejecuciones, usuarios, credenciales y configuraciones.
Por defecto, n8n usa **SQLite**, pero también es compatible con **PostgreSQL** y **MySQL/MariaDB**.
El acceso a la base de datos y las migraciones se gestionan mediante **[TypeORM](https://github.com/typeorm/typeorm)**.

Para explorar la base de datos puedes usar herramientas como [DBeaver](https://dbeaver.io).

---

## 🚀 Tablas de Workflows y Ejecuciones

### 📝 `workflow_entity`

Contiene la definición completa de todos los workflows creados en la instancia.

### 📜 `workflow_history`

Guarda versiones anteriores de workflows para permitir recuperación o auditoría.

### 🔄 `execution_entity`

Almacena las ejecuciones de workflows. Dependiendo de la configuración, n8n puede guardar todas las ejecuciones o solo las fallidas/exitosas.

### 📦 `execution_data`

Registra el workflow en el momento de la ejecución y los datos procesados.

### 📊 `execution_metadata`

Contiene metadatos personalizados asociados a ejecuciones.

### 📈 `workflow_statistics`

Guarda métricas y conteos sobre la ejecución de workflows.

---

## 🔐 Tablas de Seguridad y Acceso

### 🗝️ `credentials_entity`

Almacena credenciales encriptadas usadas para conectarse con servicios externos.

### 🔒 `shared_credentials`

Mapea credenciales a usuarios con diferentes roles (propietario, colaborador, etc.).

### 🤝 `shared_workflow`

Define qué usuarios tienen acceso a workflows y en qué nivel (editor, lector, etc.).

---

## 👥 Tablas de Usuarios y Autenticación

### 👤 `user`

Contiene los datos de usuarios registrados en la instancia.

### 🔑 `auth_identity`

Almacena identidades externas de autenticación (por ejemplo, cuando se usa SAML).

### 📜 `auth_provider_sync_history`

Historial de sincronizaciones con proveedores de autenticación (como SAML).

### 🚫 `invalid_auth_token`

Registra tokens de autenticación que han sido invalidados.

### 🛠️ `role`

Actualmente no se utiliza, reservado para futuras funciones de roles personalizados.

---

## 🌐 Tablas de Triggers y Webhooks

### 🎣 `webhook_entity`

Registra todos los webhooks activos en workflows. Incluye no solo los nodos Webhook, sino también cualquier nodo disparador que use webhooks.

### 📅 `event_destinations`

Configura destinos para streaming de logs y otros eventos del sistema.

---

## 📁 Tablas de Organización

### 🏷️ `tag_entity`

Lista de tags creados en la instancia.

### 🔗 `workflows_tags`

Mapea tags a workflows.

### 📁 `project`

Representa proyectos que agrupan recursos dentro de la instancia.

### 🔗 `project_relation`

Define relaciones entre proyectos y usuarios, incluyendo roles.

---

## 🛠️ Tablas de Configuración y Extensiones

### ⚙️ `settings`

Contiene configuraciones globales de la instancia que no dependen de variables de entorno, como:

* Estado del propietario de la instancia
* Opciones de autenticación habilitadas (SAML, LDAP, etc.)
* Clave de licencia

### 🧩 `installed_nodes`

Lista los nodos de la comunidad instalados en la instancia.

### 📦 `installed_packages`

Detalla los paquetes npm instalados. Un paquete puede contener uno o más nodos.

### 🔄 `migrations`

Registro de todas las migraciones de base de datos aplicadas.

### 🔧 `variables`

Almacena variables globales definidas en la instancia.

---

## 🧪 Tablas de Testing

### 🧪 `test_case_execution`

Registra las ejecuciones de casos de prueba.

### 🏃 `test_run`

Almacena la ejecución de conjuntos de pruebas.

---

## 🗺️ Visión General de Relaciones

n8n mantiene un esquema relacional donde:

* **Workflows** (`workflow_entity`) se conectan con **ejecuciones** (`execution_entity`) y **webhooks** (`webhook_entity`).
* **Usuarios** (`user`) se relacionan con **workflows** y **credenciales** mediante tablas de compartición (`shared_workflow`, `shared_credentials`).
* **Tags** (`tag_entity`) y **proyectos** (`project`) permiten organizar workflows y recursos.
* **Configuraciones**, **variables** y **nodos instalados** permiten personalizar la instancia.

👉 La documentación oficial incluye un **[diagrama entidad-relación (ERD)](https://docs.n8n.io/hosting/architecture/database-structure/#database-and-query-technology)** que muestra gráficamente estas relaciones.

![Modelo entidad-relacion de n8n](./modelo-er.png)

---

## ⚠️ Recomendaciones

* Evita modificar directamente los datos en la base sin entender las consecuencias.
* Realiza **backups periódicos** antes de cualquier cambio estructural.
* Considera que algunas tablas, como `execution_data`, pueden crecer rápidamente y afectar el rendimiento.
* Usa índices o herramientas de análisis solo en entornos de prueba antes de aplicar en producción.

---

✅ Con esta guía tienes una visión consolidada de la estructura de la base de datos de n8n, alineada con la documentación oficial y organizada por categorías prácticas.
