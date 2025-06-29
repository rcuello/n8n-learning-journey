# Instalación de n8n en Render con Supabase

## Introducción

Esta guía te mostrará cómo desplegar n8n de forma gratuita usando Render como plataforma de hosting y Supabase como base de datos PostgreSQL. Esta combinación es ideal para comenzar con n8n sin costos iniciales.

## Ventajas de esta configuración

- ✅ **Gratuito**: Ambos servicios ofrecen planes gratuitos generosos
- ✅ **Sin código**: Usa la imagen oficial de Docker de n8n
- ✅ **Actualizaciones automáticas**: Siempre tendrás la última versión estable
- ✅ **Escalable**: Fácil upgrade cuando necesites más recursos
- ✅ **Confiable**: Infraestructura profesional y respaldos automáticos
- ✅ **Configuración simple**: Sin necesidad de repositorios o builds

## Requisitos previos

- Cuenta de email válida
- Navegador web actualizado
- Conocimientos básicos de configuración web (opcional)

## Paso 1: Configurar Supabase (Base de datos)

### 1.1 Crear cuenta en Supabase

1. Ve a [supabase.com](https://supabase.com)
2. Haz clic en "Start your project"
3. Regístrate con tu cuenta de GitHub (recomendado)
4. Acepta los términos y condiciones

### 1.2 Crear una organización personal

1. Después del registro, serás dirigido al dashboard principal
2. Si es tu primera vez, Supabase te pedirá crear una organización:
   - **Organization name**: Tu nombre o nombre de tu empresa (ej: "Mi Empresa Automations")
   - **Organization type**: Selecciona **"Personal"** 
   - **Plan**: Automáticamente se asignará el **"Free Plan"**
   - Haz clic en "Create organization"

   ![alt text](assets/supabase-create-org.png)

> 💡 **Nota**: La organización es como una carpeta que contendrá todos tus proyectos. Puedes crear múltiples proyectos dentro de una organización.


### 1.3 Crear un nuevo proyecto

1. Una vez creada la organización, haz clic en "New project"
2. Selecciona tu organización recién creada
3. Configura el proyecto:
   - **Name**: `n8n-database` (o el nombre que prefieras)
   - **Database Password**: Genera una contraseña segura y **guárdala en un lugar seguro**
   - **Region**: `East US (Ohio)`

4. Haz clic en "Create new project"
5. Espera 2-3 minutos mientras se aprovisiona la infraestructura

![alt text](assets/supabase-create-new-project.png)

### 1.4 Verificar la creación del proyecto

Una vez completado, verás:
- ✅ **Database**: Estado "Healthy" 
- ✅ **API**: URLs generadas automáticamente
- ✅ **Authentication**: Configurado y listo
- 📊 **Dashboard**: Con métricas básicas disponibles

![alt text](assets/supabase-project-status.png)

### 1.5 Obtener la cadena de conexión

1. Una vez creado el proyecto, ve a **Connect**
![alt text](assets/supabase-connect.png)

2. En la sección **"Transaction pooler"**, haz clic en **"View parameters"** para expandir las opciones
3. Verás los parámetros de conexión individuales:
   - **Host**: `aws-0-[region].pooler.supabase.com`
   - **Database**: `postgres` 
   - **Port**: `6543` (puerto del pooler, no el estándar 5432)
   - **User**: `postgres.[project-ref]`
   - **Password**: `[la-contraseña-que-creaste]`
![alt text](assets/supabase-connection-string.png)

## Paso 2: Configurar Render (Hosting)

### 2.1 Crear cuenta en Render

1. Ve a [render.com](https://render.com)
2. Haz clic en ["Get started"](https://dashboard.render.com/register)
3. Regístrate con tu email o cuenta de GitHub
4. Verifica tu email si es necesario

![alt text](assets/render-create-account.png)

### 2.2 Crear el servicio web en Render

1. En el dashboard de Render, haz clic en "New +"
2. Selecciona "Web Service"

![alt text](assets/render-new-web-service.png)

3. En la sección "You are deploying a Web Service", selecciona **"Existing image"**
4. En el campo de imagen Docker, ingresa: `docker.n8n.io/n8nio/n8n`

![alt text](assets/render-existing-image.png)

5. Configura el servicio:
   - **Name**: `n8n-app` (o tu nombre preferido)
   - **Project**: Haz clic en "Create new project" si quieres organizar mejor tus servicios
      - **Project name**: `n8n-automation-suite` (o el nombre que prefieras)
      - **Environment name**: `Production`

      ![alt text](assets/render-create-project.png)

   - **Region**: `Oregon (US West)`
   - **Instance Type**: `Free 512 MB (RAM)`
   
     ![alt text](assets/render-instance-type.png)


> 💡 **Nota**: Al usar la imagen oficial de Docker, no necesitas configurar repositorio ni comandos de build. Render descargará y ejecutará directamente la imagen oficial de n8n.

## Paso 3: Configurar Variables de Entorno

![alt text](assets/render-env-variables.png)

En la sección "Environment" de tu servicio en Render, agrega las siguientes variables:

### 3.1 Variables de base de datos (Supabase)

| Variable | Valor | Descripción |
|----------|-------|-------------|
| `DB_TYPE` | `postgresdb` | Tipo de base de datos |
| `DB_POSTGRESDB_DATABASE` | `postgres` | Nombre de la base de datos |
| `DB_POSTGRESDB_HOST` | `db.[PROJECT-REF].supabase.co` | Host de Supabase (obtener de Supabase) |
| `DB_POSTGRESDB_USER` | `postgres` | Usuario de PostgreSQL (obtener de Supabase) |
| `DB_POSTGRESDB_PASSWORD` | `[TU-PASSWORD]` | Contraseña de Supabase |
| `DB_POSTGRESDB_PORT` | `5432` | Puerto PostgreSQL (obtener de Supabase) |
| `DB_POSTGRESDB_SCHEMA` | `public` | Schema de la base de datos |
| `DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED` | `FALSE` | Desactivar validación SSL estricta |

### 3.2 Variables de configuración de n8n

| Variable | Valor | Descripción |
|----------|-------|-------------|
| `N8N_HOST` | `tu-app-name.onrender.com` | Dominio de tu aplicación (sin https://) |
| `N8N_PORT` | `443` | Puerto HTTPS para Render |
| `N8N_PROTOCOL` | `https` | Protocolo de conexión |
| `WEBHOOK_URL` | `https://tu-app-name.onrender.com` | URL completa de webhooks |

### 3.3 Variables de seguridad y encriptación

| Variable | Valor | Descripción |
|----------|-------|-------------|
| `N8N_ENCRYPTION_KEY` | `42072e543214e3ffa40474006d3dbbaa` | Clave de encriptación principal |
| `NON_ENCRYPTION_KEY` | `683ECC56E7BEFA1E5AF5D85C5E43E` | Clave adicional de seguridad |
| `N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS` | `TRUE` | Forzar permisos de archivos |

### 3.4 Variables de configuración regional y funcional

| Variable | Valor | Descripción |
|----------|-------|-------------|
| `GENERIC_TIMEZONE` | `America/Bogota` | Zona horaria principal |
| `TZ` | `America/Bogota` | Zona horaria del sistema |
| `N8N_RUNNERS_ENABLED` | `TRUE` | Habilitar runners para mejor rendimiento |

### 3.5 Cómo obtener valores de Supabase

Para obtener los valores correctos de tu base de datos Supabase:

1. Ve a tu proyecto en Supabase
2. Navega a **Settings** > **Database**
3. En la sección "Connection string", encontrarás:
   - **Host**: `db.[PROJECT-REF].supabase.co`
   - **User**: `postgres` 
   - **Port**: `5432`
   - **Database**: `postgres`
   - **Password**: La que configuraste al crear el proyecto

4. Copia estos valores exactos a las variables correspondientes

### 3.6 Generar claves de encriptación personalizadas (Opcional)

Si prefieres generar tus propias claves de encriptación:

```bash
# Para N8N_ENCRYPTION_KEY (32 bytes)
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"

# Para NON_ENCRYPTION_KEY (16 bytes)  
node -e "console.log(require('crypto').randomBytes(16).toString('hex').toUpperCase())"
```
![alt text](assets/render-enc-key.png)

![alt text](assets/render-n8n-enc-key.png)

> ⚠️ **Importante**: Si cambias las claves de encriptación después de tener workflows guardados, estos podrían volverse ilegibles. Guarda las claves en un lugar seguro.

## Paso 4: Desplegar la aplicación

1. Después de configurar todas las variables, haz clic en "Create Web Service"
2. Render comenzará a construir y desplegar tu aplicación
3. El proceso puede tomar 5-10 minutos la primera vez
4. Una vez completado, obtendrás una URL como: `https://tu-app.onrender.com`

## Paso 5: Configuración inicial de n8n

1. Accede a tu URL de Render
2. Si configuraste autenticación básica, ingresa tus credenciales
3. Completa la configuración inicial:
   - Crea tu cuenta de administrador
   - Configura las preferencias básicas
   - Verifica la conexión a la base de datos

## Paso 6: Configuración adicional

### 6.1 Webhooks y dominios personalizados

1. Actualiza la variable `WEBHOOK_URL` con tu dominio final
2. Si usas un dominio personalizado, configúralo en Render:
   - Ve a Settings > Custom Domains
   - Agrega tu dominio y configura los DNS

### 6.2 Mantener activo el servicio (Plan gratuito)

El plan gratuito de Render "duerme" después de 15 minutos de inactividad:

- **Opción 1**: Configurar un webhook que haga ping cada 10 minutos
- **Opción 2**: Usar un servicio como UptimeRobot
- **Opción 3**: Actualizar a plan pagado ($7/mes)

## Solución de problemas

### Error de conexión a la base de datos

1. Verifica que la URL de conexión esté correcta
2. Confirma que la contraseña no tenga caracteres especiales problemáticos
3. Revisa que todas las variables de entorno estén configuradas

### Error "Service Unavailable" o puerto incorrecto

1. Verifica que `N8N_PORT` esté configurado como `5678`
2. Revisa que Render esté escuchando en el puerto correcto
3. Espera unos minutos para que el contenedor se inicie completamente

### Autenticación no funciona

1. Verifica que `N8N_BASIC_AUTH_ACTIVE` esté en `true`
2. Confirma que usuario y contraseña sean correctos
3. Prueba desactivar la autenticación temporalmente

## Limitaciones del plan gratuito

### Render (Plan gratuito)
- 750 horas/mes de tiempo de ejecución
- Duerme después de 15 min de inactividad
- 512 MB RAM
- 1 CPU compartida

### Supabase (Plan gratuito)
- 500 MB de almacenamiento
- 2 proyectos activos máximo
- 50,000 autenticaciones/mes

## Recursos adicionales

- [Documentación oficial de n8n](https://docs.n8n.io/)
- [Render Documentation](https://render.com/docs)
- [Supabase Documentation](https://supabase.com/docs)
- [n8n Community](https://community.n8n.io/)

---

> 💡 **Tip**: Guarda todas las credenciales y URLs en un gestor de contraseñas seguro. Necesitarás acceso a ellas para futuras configuraciones y mantenimiento.