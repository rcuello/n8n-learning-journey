# 🚀 Guía de Instalación y Uso de n8n

## 📋 Requisitos Previos

- **Docker Desktop** instalado y funcionando
- **Docker Compose** incluido con Docker Desktop
- Editor de texto (VS Code, Notepad++, etc.)
- Navegador web moderno

## 📁 1. Preparación del Entorno

### 1.1 Crear Estructura de Carpetas
```bash
mkdir n8n-lab
cd n8n-lab
```

### 1.2 Descargar los Archivos
Crear los siguientes archivos en la carpeta `n8n-lab`:

**Archivo 1: `docker-compose.yml`**
- Descarga el archivo Docker Compose proporcionado por el instructor
- Guárdalo exactamente con el nombre `docker-compose.yml`

**Archivo 2: `.env`**
- Crear archivo `.env` con el contenido proporcionado por el instructor
- ⚠️ **Importante**: El archivo debe llamarse exactamente `.env` (con el punto al inicio)

## ⚙️ 2. Verificación del Archivo .env

Abre el archivo `.env` y verifica que contenga:

```env
# --- Configuración n8n ---
N8N_HOST=localhost
N8N_PORT=5680
N8N_PROTOCOL=http
WEBHOOK_URL=http://localhost:5680/
GENERIC_TIMEZONE=America/Bogota
TZ=America/Bogota

# Autenticación UI
N8N_BASIC_AUTH_ACTIVE=true
N8N_UI_USER=student
N8N_UI_PASSWORD=student123

# Base de datos
POSTGRES_DB=n8n_database
POSTGRES_USER=n8n_user
POSTGRES_PASSWORD=n8n_pass123

# Mitmproxy
NODE_TLS_REJECT_UNAUTHORIZED=0
MITMPROXY_PORT=8080
MITMPROXY_WEB_PORT=8081
MITMPROXY_WEB_PASSWORD=proxy123

HTTP_PROXY=http://mitmproxy:8080
HTTPS_PROXY=http://mitmproxy:8080
NO_PROXY=localhost,127.0.0.1,n8n-db,redis

# Adminer 
ADMINER_PORT=8082

# Redis 
REDIS_PORT=6379
REDIS_PASSWORD=redis123

# Logs
N8N_LOG_LEVEL=debug
N8N_LOG_OUTPUT=console
CODE_ENABLE_STDOUT=true
```

### 🔍 Puntos Clave del .env:
- **Puertos principales**: n8n (5680), Mitmproxy (8080/8081), Adminer (8082)
- **Credenciales de acceso**: usuario `student`, contraseña `student123`
- **Configuración de proxy**: Para interceptar peticiones HTTP

## 🚀 3. Instalación y Puesta en Marcha

### 3.1 Iniciar los Servicios
```bash
# Navegar a la carpeta del proyecto
cd n8n-lab

# Iniciar todos los servicios
docker-compose up -d
```

### 3.2 Verificar que Todo Esté Funcionando
```bash
# Ver el estado de los contenedores
docker-compose ps

# Deberías ver algo como:
# n8n        running   0.0.0.0:5680->5680/tcp
# n8n-db     running   5432/tcp
# adminer    running   0.0.0.0:8082->8080/tcp
# mitmproxy  running   0.0.0.0:8080->8080/tcp, 0.0.0.0:8081->8081/tcp
# redis      running   0.0.0.0:6379->6379/tcp
```

### 3.3 Ver Logs (Si Hay Problemas)
```bash
# Ver logs de todos los servicios
docker-compose logs -f

# Ver logs de un servicio específico
docker-compose logs n8n
```

## 🌐 4. Acceso a n8n

### 4.1 Abrir n8n
- **URL**: http://localhost:5680
- **Usuario**: `student`
- **Contraseña**: `student123`

### 4.2 Primera Exploración de n8n
1. **Crear tu primer workflow**:
   - Clic en "Add first step"
   - Buscar y agregar un nodo "Manual Trigger"
   
2. **Agregar un nodo HTTP Request**:
   - Clic en el "+" después del trigger
   - Buscar "HTTP Request"
   - Configurar: 
     - **Method**: GET
     - **URL**: https://jsonplaceholder.typicode.com/posts/1

3. **Probar el workflow**:
   - Clic en "Test workflow"
   - Clic en "Execute Workflow"

### 4.3 Ejercicios Básicos en n8n
**Ejercicio 1**: Crear workflow con API pública
- Trigger Manual → HTTP Request → Ver resultado

**Ejercicio 2**: Workflow con múltiples peticiones
- Manual → HTTP Request (posts) → HTTP Request (users) → Merge

## 🗄️ 5. Acceso a Adminer (Base de Datos)

### 5.1 Conectarse a Adminer
- **URL**: http://localhost:8082

### 5.2 Datos de Conexión
- **Motor de base de datos**: `PostgreSQL` ⚠️ (¡Cambiar del MySQL por defecto!)
- **Servidor**: `n8n-db`
- **Usuario**: `n8n_user`
- **Contraseña**: `n8n_pass123`
- **Base de datos**: `n8n_database`

### 5.3 Exploración de la Base de Datos
Una vez conectado, explorar estas tablas principales:

**Tabla `execution_entity`**:
```sql
SELECT id, "workflowId", mode, status, "startedAt", "stoppedAt" 
FROM execution_entity 
ORDER BY "startedAt" DESC 
LIMIT 10;
```

**Tabla `workflow_entity`**:
```sql
SELECT id, name, active, "createdAt", "updatedAt"
FROM workflow_entity;
```

**Estadísticas de ejecuciones**:
```sql
SELECT status, COUNT(*) as cantidad 
FROM execution_entity 
GROUP BY status;
```

## 🕵️ 6. Interceptar Peticiones con Mitmproxy

### 6.1 Acceder a Mitmproxy Web
- **URL**: http://localhost:8081
- **Contraseña**: `proxy123`

### 6.2 Configurar n8n para Usar Proxy
Los nodos HTTP de n8n ya están configurados para usar el proxy automáticamente gracias a las variables de entorno.

### 6.3 Monitorear Peticiones HTTP
1. **Abrir Mitmproxy** en http://localhost:8081
2. **Ejecutar un workflow** con nodos HTTP en n8n
3. **Observar las peticiones** en tiempo real en Mitmproxy

### 6.4 Análisis de Peticiones
En Mitmproxy podrás ver:
- **Request Headers**: Cabeceras enviadas
- **Request Body**: Cuerpo de la petición
- **Response Headers**: Cabeceras de respuesta  
- **Response Body**: Contenido de la respuesta
- **Timing**: Tiempos de respuesta

## 🧪 7. Ejercicios Prácticos Integrados

### Ejercicio A: Workflow con Monitoreo Completo
1. **Crear workflow** en n8n con HTTP Request
2. **Ejecutar** y ver logs en n8n
3. **Verificar ejecución** en Adminer
4. **Analizar petición** en Mitmproxy

### Ejercicio B: API Testing
1. **Crear workflow** que consuma diferentes endpoints
2. **Usar Mitmproxy** para analizar diferencias en headers/responses
3. **Consultar en Adminer** las ejecuciones exitosas vs fallidas

### Ejercicio C: Debugging de APIs
1. **Crear workflow** que falle intencionalmente (URL incorrecta)
2. **Usar Mitmproxy** para ver el error HTTP
3. **Revisar en Adminer** el registro del error

## 🛠️ 8. Comandos Útiles

### Gestión del Entorno
```bash
# Detener todos los servicios
docker-compose down

# Reiniciar un servicio específico
docker-compose restart n8n

# Ver uso de recursos
docker-compose ps
docker stats

# Limpiar volúmenes (⚠️ Borra todos los datos)
docker-compose down -v
```

### Troubleshooting
```bash
# Ver logs detallados
docker-compose logs -f [servicio]

# Acceder a un contenedor
docker-compose exec n8n sh
docker-compose exec n8n-db psql -U n8n_user -d n8n_database

# Verificar conectividad
docker-compose exec n8n ping google.com
```

## 📊 9. Puertos y URLs de Referencia

| Servicio | URL | Puerto | Credenciales |
|----------|-----|---------|--------------|
| **n8n UI** | http://localhost:5680 | 5680 | student / student123 |
| **Adminer** | http://localhost:8082 | 8082 | Ver sección 5.2 |
| **Mitmproxy Web** | http://localhost:8081 | 8081 | Contraseña: proxy123 |
| **Mitmproxy Proxy** | localhost:8080 | 8080 | (Proxy HTTP/HTTPS) |
| **Redis** | localhost:6379 | 6379 | Contraseña: redis123 |

## ✅ 10. Checklist de Verificación

- [ ] Docker Desktop está ejecutándose
- [ ] Archivos `docker-compose.yml` y `.env` están en la carpeta
- [ ] Comando `docker-compose up -d` ejecutado exitosamente
- [ ] Todos los servicios muestran status "running"
- [ ] n8n accesible en http://localhost:5680
- [ ] Adminer accesible y conecta a PostgreSQL
- [ ] Mitmproxy web accesible en http://localhost:8081
- [ ] Workflow de prueba ejecutado correctamente

## 🆘 Problemas Comunes

**Error "Connection refused" en Adminer**
- ✅ Verificar que motor sea PostgreSQL (no MySQL)
- ✅ Esperar a que PostgreSQL esté listo (puede tomar 1-2 minutos)

**n8n no carga**
- ✅ Verificar que puerto 5680 no esté en uso
- ✅ Revisar logs: `docker-compose logs n8n`

**Mitmproxy no intercepta peticiones**
- ✅ Verificar variables HTTP_PROXY en .env
- ✅ Algunos nodos pueden ignorar proxy (comportamiento esperado)

---

## 🎯 Objetivos de Aprendizaje

Al completar esta guía, habrás aprendido:
- ✅ Desplegar aplicaciones con Docker Compose
- ✅ Configurar variables de entorno
- ✅ Crear y ejecutar workflows en n8n
- ✅ Consultar bases de datos PostgreSQL
- ✅ Interceptar y analizar tráfico HTTP
- ✅ Integrar múltiples herramientas de desarrollo

¡Buen trabajo explorando el ecosistema n8n! 🚀