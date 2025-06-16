# Guía Definitiva para Instalar n8n GRATIS

## 📋 Índice
1. [¿Qué es n8n?](#qué-es-n8n)
2. [Opciones de Instalación](#opciones-de-instalación)
3. [n8n Cloud](#n8n-cloud)
4. [Instalación Local](#instalación-local)
   - [Con NPM](#con-npm)
   - [Con Docker](#con-docker)
5. [Alojamiento en la Nube](#alojamiento-en-la-nube)
   - [Plataforma como Servicio (PaaS)](#plataforma-como-servicio-paas)
   - [Infraestructura como Servicio (IaaS)](#infraestructura-como-servicio-iaas)
6. [Configuración Avanzada](#configuración-avanzada)
7. [Comparación de Costos](#comparación-de-costos)

---

## 🤖 ¿Qué es n8n?

n8n es una herramienta de automatización de flujos de trabajo de código abierto que permite conectar diferentes aplicaciones y servicios para automatizar tareas repetitivas. Es perfecta para crear agentes de IA, automatizar procesos empresariales y conectar APIs sin necesidad de programar.

---

## 🚀 Opciones de Instalación

Existen múltiples formas de instalar n8n, cada una con sus ventajas y desventajas:

### 1. **n8n Cloud** 🌐
- **Facilidad**: ⭐⭐⭐⭐⭐
- **Costo**: €€€
- **Control**: ⭐⭐

### 2. **Local (Tu ordenador)** 💻
- **Facilidad**: ⭐⭐⭐⭐
- **Costo**: GRATIS
- **Control**: ⭐⭐⭐⭐⭐

### 3. **Nube (Hosting propio)** ☁️
- **Facilidad**: ⭐⭐⭐
- **Costo**: €
- **Control**: ⭐⭐⭐⭐

---

## 1. n8n Cloud

### ✅ Ventajas
- **Configuración instantánea**: Solo necesitas registrarte
- **Sin mantenimiento**: Todo está gestionado por n8n
- **Escalabilidad automática**: Se adapta a tus necesidades

### ❌ Desventajas
- **Costo elevado**: €20/mes por 5 workflows activos
- **Menos control**: Limitado a las opciones que ofrece la plataforma
- **Dependencia externa**: Dependes del servicio de n8n

### 📋 Planes Disponibles

| Plan | Precio | Workflows Activos | Ejecuciones |
|------|--------|-------------------|-------------|
| Starter | €20/mes | 5 | 2,500 por workflow |
| Pro | €50/mes | 15 | 10,000 por workflow |

### 🔗 Cómo Empezar
1. Visita [n8n.io](https://n8n.io)
2. Regístrate con tu email
3. Selecciona tu plan
4. ¡Comienza a crear workflows!

---

## 2. Instalación Local

### Opción A: Con NPM

#### 📋 Requisitos Previos
- Node.js instalado en tu sistema
- NPM (viene incluido con Node.js)

#### 🛠️ Instalación de Node.js
1. Visita [nodejs.org](https://nodejs.org)
2. Descarga la versión LTS para tu sistema operativo
3. Ejecuta el instalador y sigue las instrucciones

#### ⚙️ Instalación de n8n
```bash
# Verificar instalación de Node.js
node -v

# Verificar instalación de NPM
npm -v

# Instalar n8n globalmente
npm install n8n -g

# Iniciar n8n
n8n start
```

#### 🌐 Acceso
- Abre tu navegador y ve a: `http://localhost:5678`
- Completa el formulario de registro inicial

#### 🔄 Actualización
```bash
# Buscar actualizaciones
npm outdated -g

# Actualizar n8n
npm update n8n -g
```

### Opción B: Con Docker

#### 📋 Requisitos Previos
- Docker Desktop instalado

#### 🛠️ Instalación de Docker
1. Visita [docker.com](https://www.docker.com/products/docker-desktop)
2. Descarga Docker Desktop para tu sistema operativo
3. Instala y reinicia tu ordenador

#### ⚙️ Instalación de n8n con Docker
```bash
# Crear directorio para n8n
mkdir n8n-data

# Ejecutar n8n en Docker
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

#### 🔄 Usando Docker Compose
```yaml
version: '3.8'
services:
  n8n:
    image: docker.n8n.io/n8nio/n8n
    restart: always
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=password
    volumes:
      - ~/.n8n:/home/node/.n8n
```

### 🔐 Exposición para Servicios Externos

Para conectar con servicios como Telegram, Google, etc., necesitas exponer tu n8n local:

#### Con NGROK
1. Instala NGROK desde [ngrok.com](https://ngrok.com)
2. Ejecuta: `ngrok http 5678`
3. Usa la URL HTTPS proporcionada

---

## 3. Alojamiento en la Nube

### Plataforma como Servicio (PaaS)

#### 🚀 Railway (Recomendado)

**Ventajas:**
- Despliegue con un clic
- Gestión automática de la infraestructura
- Escalabilidad automática

**Costos:**
- Plan Hobby: €5/mes + uso
- Plan Pro: €20/mes + uso

**Instalación:**
1. Visita [railway.app](https://railway.app)
2. Regístrate con tu cuenta de GitHub
3. Selecciona "Deploy a template"
4. Busca "n8n with worker"
5. Haz clic en "Deploy"

#### 🔄 Otras Opciones PaaS
- **Render**: Fácil de usar, plan gratuito disponible
- **Vercel**: Excelente para aplicaciones web
- **Heroku**: Clásico, pero más caro
- **Cloudflare Pages**: Rápido y económico

### Infraestructura como Servicio (IaaS)

#### 🏗️ Hostinger VPS + Dokploy

**Ventajas:**
- Costo fijo mensual
- Control total sobre el servidor
- Múltiples aplicaciones en un servidor

**Instalación:**

1. **Contratar VPS en Hostinger**
   - Visita [hostinger.com](https://hostinger.com)
   - Selecciona "VPS Hosting"
   - Elige un plan (recomendado: 8GB RAM)
   - Configura ubicación del servidor (cerca de tu ubicación)
   - Selecciona Ubuntu como sistema operativo

2. **Instalar Dokploy**
   ```bash
   curl -sSL https://dokploy.com/install.sh | sh
   ```

3. **Configurar n8n**
   - Accede a tu panel de Dokploy
   - Crea un nuevo proyecto
   - Selecciona "Template"
   - Busca n8n y despliega

#### 🔧 Configuración de Dominio
- En Hostinger, ve a la sección de DNS
- Apunta tu dominio a la IP de tu VPS
- Configura SSL automáticamente

---

## 4. Configuración Avanzada

### 🔐 Variables de Entorno Importantes

```bash
# Autenticación básica
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=tu_usuario
N8N_BASIC_AUTH_PASSWORD=tu_contraseña

# Base de datos externa
DB_TYPE=postgresdb
DB_POSTGRESDB_HOST=localhost
DB_POSTGRESDB_PORT=5432
DB_POSTGRESDB_DATABASE=n8n
DB_POSTGRESDB_USER=n8n_user
DB_POSTGRESDB_PASSWORD=n8n_password

# Configuración de webhooks
WEBHOOK_URL=https://tu-dominio.com/
```

### 📊 Monitoreo y Mantenimiento

#### Métricas Importantes a Monitorear:
- **CPU**: No debe superar el 80% constantemente
- **RAM**: Mantener un 20% libre
- **Disco**: Limpiar logs regularmente
- **Workflows**: Optimizar los que consumen más recursos

#### Backups Automáticos:
```bash
# Backup de la base de datos
pg_dump n8n > backup_$(date +%Y%m%d).sql

# Backup de archivos de configuración
tar -czf n8n_config_backup.tar.gz ~/.n8n/
```

---

## 5. Comparación de Costos

### 📊 Tabla Comparativa Mensual

| Opción | Costo Mensual | Workflows | Ventajas | Desventajas |
|--------|---------------|-----------|----------|-------------|
| **n8n Cloud** | €20-50 | 5-15 | Sin configuración | Caro, menos control |
| **Local** | €0 | Ilimitado | Gratis, control total | Solo acceso local |
| **Railway** | €5-25 | Ilimitado | Fácil, escalable | Costo variable |
| **Hostinger VPS** | €4-15 | Ilimitado | Costo fijo, múltiples apps | Requiere configuración |

### 💡 Recomendaciones por Caso de Uso

#### Para Principiantes 🔰
- **Empezar con**: Instalación local con NPM
- **Razón**: Gratis, fácil de configurar, perfecto para aprender

#### Para Desarrollo 👨‍💻
- **Empezar con**: Docker local
- **Razón**: Fácil de replicar, aislado del sistema

#### Para Producción (1-2 clientes) 🏢
- **Empezar con**: Railway
- **Razón**: Balance entre facilidad y costo

#### Para Escalar (3+ clientes) 🚀
- **Empezar con**: Hostinger VPS + Dokploy
- **Razón**: Costo fijo, múltiples aplicaciones

---

## 6. Troubleshooting Común

### 🔧 Problemas Frecuentes y Soluciones

#### Error: Puerto 5678 ya en uso
```bash
# Encontrar proceso usando el puerto
lsof -i :5678

# Matar el proceso
kill -9 [PID]

# O usar otro puerto
n8n start --port 5679
```

#### Error: Permisos insuficientes
```bash
# Cambiar propietario de archivos
sudo chown -R $USER:$USER ~/.n8n

# Dar permisos de ejecución
chmod +x ~/.n8n/
```

#### Error: Memoria insuficiente
```bash
# Aumentar memoria para Node.js
export NODE_OPTIONS="--max-old-space-size=4096"
n8n start
```

---

## 7. Próximos Pasos

### 🔗 Configuración de Integraciones

Una vez instalado n8n, los siguientes pasos típicos son:

1. **Configurar credenciales** para servicios como:
   - Google (Gmail, Drive, Sheets)
   - Telegram
   - OpenAI
   - Webhooks

2. **Crear tu primer workflow**
3. **Configurar notificaciones**
4. **Establecer monitoreo**

### 📚 Recursos Adicionales

- **Documentación oficial**: [docs.n8n.io](https://docs.n8n.io)
- **Comunidad**: [community.n8n.io](https://community.n8n.io)
- **Templates**: [n8n.io/workflows](https://n8n.io/workflows)
