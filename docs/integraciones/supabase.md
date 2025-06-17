# Tutorial: Crear cuenta en Supabase e integrar con N8N

## Introducción

Este tutorial te guiará paso a paso para crear una cuenta en Supabase y configurarla como base de datos para tu instancia de N8N. Supabase es una alternativa open-source a Firebase que ofrece una base de datos PostgreSQL robusta y gratuita, perfecta para proyectos de automatización con N8N.

## ¿Qué es Supabase?

Supabase es una plataforma Backend-as-a-Service (BaaS) que proporciona:
- Base de datos PostgreSQL completamente administrada
- APIs REST y GraphQL automáticas
- Autenticación y autorización integrada
- Almacenamiento de archivos
- Funciones serverless

## Ventajas de usar Supabase con N8N

✅ **Plan gratuito generoso**: 500MB de almacenamiento y 50,000 autenticaciones/mes  
✅ **PostgreSQL nativo**: Compatible directamente con N8N  
✅ **Infraestructura confiable**: Respaldos automáticos y alta disponibilidad  
✅ **Escalabilidad**: Fácil upgrade cuando tu proyecto crezca  
✅ **Dashboard intuitivo**: Gestión visual de datos y configuraciones  
✅ **APIs automáticas**: Acceso directo a tus datos desde N8N workflows  

---

## Parte 1: Creación de cuenta en Supabase

### Paso 1: Registro inicial

1. **Navega a Supabase**
   - Ve a [https://supabase.com](https://supabase.com)
   - Haz clic en **"Start your project"**

2. **Método de registro recomendado**
   - Selecciona **"Continue with GitHub"** (más rápido y seguro)
   - Alternativamente, puedes usar **"Sign up with email"**

3. **Autorización con GitHub**
   - Autoriza a Supabase para acceder a tu cuenta de GitHub
   - Solo necesita acceso básico a tu perfil público

4. **Verificación de email** (si usas email)
   - Revisa tu bandeja de entrada
   - Haz clic en el enlace de verificación

### Paso 2: Configuración de organización

Una vez dentro del dashboard, Supabase te pedirá crear una organización:

1. **Datos de la organización**
   - **Organization name**: `Mi Empresa Automations` (o tu nombre preferido)
   - **Organization type**: Selecciona **"Personal"**
   - **Plan**: Automáticamente se asigna **"Free Plan"**

2. **Confirmar creación**
   - Haz clic en **"Create organization"**
   - Espera 1-2 minutos para la configuración inicial

![alt text](assets/supabase/supabase-create-org.png)

> 💡 **Nota**: La organización funciona como un contenedor para todos tus proyectos. Puedes crear múltiples proyectos dentro de una organización.

---

## Parte 2: Creación del proyecto para N8N

### Paso 3: Configuración del proyecto

1. **Iniciar nuevo proyecto**
   - Haz clic en **"New project"**
   - Selecciona tu organización recién creada

2. **Configuración del proyecto**
   - **Name**: `n8n-production-db` (nombre descriptivo)
   - **Database Password**: 
     - Usa el generador automático de Supabase
     - **⚠️ IMPORTANTE**: Copia y guarda esta contraseña en un lugar seguro
     - No podrás recuperarla después
   - **Region**: Selecciona **"East US (N. Virginia)"** para mejor rendimiento

3. **Confirmación y espera**
   - Haz clic en **"Create new project"**
   - El proceso toma aproximadamente 2-3 minutos
   - Verás una barra de progreso con el estado del aprovisionamiento

![alt text](assets/supabase/supabase-create-new-project.png)

### Paso 4: Verificación del proyecto

Una vez completado, deberías ver:

- ✅ **Project Status**: "Active"
- ✅ **Database**: "Healthy" 
- ✅ **API**: URLs generadas automáticamente
- ✅ **Auth**: Configurado y funcionando
- 📊 **Dashboard**: Con métricas básicas disponibles

![alt text](assets/supabase/supabase-project-status.png)

---

## Parte 3: Obtener datos de conexión

### Paso 5: Acceder a la información de conexión

1. **Navegar a configuraciones**
   - En tu proyecto, ve a **Settings** (⚙️) en la barra lateral
   - Selecciona **"Database"**

2. **Sección de Connection info**
   - Busca la sección **"Connection info"**
   - Aquí encontrarás todos los parámetros necesarios

![alt text](assets/supabase/supabase-connect.png)

3. **Datos para N8N**
   ```
   Host: db.[PROJECT-REF].supabase.co
   Database: postgres
   Username: postgres
   Port: 5432
   Password: [la-contraseña-que-guardaste]
   ```

![alt text](assets/supabase/supabase-connection-string.png)

### Paso 6: Configurar Connection Pooling (Recomendado)

Para mejor rendimiento con N8N:

1. **Activar Connection Pooling**
   - En **Settings** > **Database**
   - Busca **"Connection pooling"**
   - Activa **"Enable connection pooling"**

2. **Obtener datos del pooler**
   ```
   Host: aws-0-[region].pooler.supabase.com
   Database: postgres
   Username: postgres.[project-ref]
   Port: 6543
   Password: [la-misma-contraseña]
   ```

> 💡 **Tip**: El connection pooling mejora el rendimiento al reutilizar conexiones de base de datos, especialmente útil para N8N que puede hacer múltiples consultas simultáneas.

---

## Parte 4: Uso avanzado con N8N

### Paso 1: Usar Supabase Node en workflows

N8N incluye un nodo nativo para Supabase que te permite:

1. **Operaciones disponibles**
   - Insertar registros
   - Actualizar datos
   - Eliminar registros
   - Consultar con filtros avanzados
   - Ejecutar funciones RPC

2. **Configuración del nodo**
   - **Supabase URL**: `https://[PROJECT-REF].supabase.co`
   - **Service Role Key**: Obtener desde **Settings** > **API**
   - **Table**: Nombre de tu tabla


### Paso 10: Crear tablas personalizadas

1. **Acceder al editor SQL**
   - En Supabase, ve a **SQL Editor**
   - Haz clic en **"New query"**

2. **Ejemplo de tabla para logs de N8N**
   ```sql
   CREATE TABLE workflow_logs (
     id BIGSERIAL PRIMARY KEY,
     workflow_id TEXT NOT NULL,
     execution_id TEXT NOT NULL,
     status TEXT NOT NULL,
     started_at TIMESTAMP WITH TIME ZONE DEFAULT now(),
     finished_at TIMESTAMP WITH TIME ZONE,
     error_message TEXT,
     input_data JSONB,
     output_data JSONB
   );
   
   -- Índices para mejor rendimiento
   CREATE INDEX idx_workflow_logs_workflow_id ON workflow_logs(workflow_id);
   CREATE INDEX idx_workflow_logs_status ON workflow_logs(status);
   CREATE INDEX idx_workflow_logs_started_at ON workflow_logs(started_at);
   ```

3. **Ejecutar query**
   - Haz clic en **"Run"** para crear la tabla
   - Verifica en **Table Editor** que se creó correctamente

---

## Solución de problemas comunes

### Error: "Connection refused"

**Causa**: Configuración incorrecta de host o puerto  
**Solución**:
1. Verifica que el host sea exactamente: `db.[PROJECT-REF].supabase.co`
2. Confirma que el puerto sea `5432` (o `6543` si usas pooling)
3. Revisa que no haya espacios extra en las variables

### Error: "Authentication failed"

**Causa**: Contraseña incorrecta o usuario mal configurado  
**Solución**:
1. Verifica que la contraseña sea exactamente la que guardaste
2. Confirma que el usuario sea `postgres`
3. Si tienes caracteres especiales en la contraseña, puede ser necesario codificarlos en URL

### Error: "SSL connection required"

**Causa**: Configuración SSL faltante  
**Solución**:
1. Agrega: `DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED=false`
2. Si persiste, configura: `DB_POSTGRESDB_SSL_MODE=require`

### Performance lento

**Causa**: Sin connection pooling o región distante  
**Solución**:
1. Activa connection pooling en Supabase
2. Usa los parámetros del pooler en lugar de la conexión directa
3. Considera cambiar la región si está muy lejos de tu servidor N8N

---

## Mejores prácticas

### Seguridad
- 🔐 **Nunca compartas tu contraseña de base de datos**
- 🔐 **Usa variables de entorno para todas las credenciales**
- 🔐 **Configura Row Level Security (RLS) para tablas sensibles**
- 🔐 **Usa Service Role Key solo para operaciones de backend**

### Rendimiento
- ⚡ **Activa connection pooling siempre**
- ⚡ **Crea índices en columnas que consultes frecuentemente**
- ⚡ **Usa consultas específicas en lugar de SELECT \***
- ⚡ **Implementa paginación para datasets grandes**

### Monitoreo
- 📊 **Revisa regularmente el dashboard de Supabase**
- 📊 **Configura alertas para uso de recursos**
- 📊 **Monitorea logs de errores**
- 📊 **Mantén backup de workflows críticos**

---

## Recursos adicionales

### Documentación oficial
- [Supabase Database Guide](https://supabase.com/docs/guides/database)
- [N8N Database Configuration](https://docs.n8n.io/hosting/configuration/configuration-methods/)
- [PostgreSQL Best Practices](https://supabase.com/docs/guides/database/postgres/configuration)

### Herramientas útiles
- [Supabase CLI](https://supabase.com/docs/reference/cli) - Para gestión local
- [pgAdmin](https://www.pgadmin.org/) - Cliente visual para PostgreSQL
- [DBeaver](https://dbeaver.io/) - Editor SQL multiplataforma

### Comunidad
- [Supabase Discord](https://discord.supabase.com/)
- [N8N Community](https://community.n8n.io/)
- [Supabase GitHub](https://github.com/supabase/supabase)

---

## Próximos pasos

Una vez que tengas Supabase configurado con N8N:

1. **Explora el nodo de Supabase** en tus workflows
2. **Crea tablas personalizadas** para tus casos de uso específicos
3. **Implementa logging avanzado** de tus automatizaciones
4. **Configura webhooks** para notificaciones en tiempo real
5. **Escala tu configuración** según crezcan tus necesidades

---

> 🎉 **¡Felicidades!** Ahora tienes una base de datos robusta y gratuita para impulsar tus automatizaciones con N8N. La combinación de Supabase + N8N te permite crear workflows poderosos con persistencia de datos confiable.