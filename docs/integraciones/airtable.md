# Tutorial Completo: Conectar Airtable con n8n

## Parte 1: Crear una cuenta en Airtable

### Paso 1: Registro en Airtable
1. Ve a [airtable.com](https://airtable.com)
2. Haz clic en "Sign up for free" (Registrarse gratis)

![alt text](assets/airtable/at-signup-free.png)

3. Aparecerá la página de registro con varias opciones:
   - **Opción recomendada**: Haz clic en "Continue with Google" para usar tu cuenta de Google
   - **Alternativa con email**: Ingresa tu email de trabajo en el campo "Work email" y haz clic en "Continue with email"
   - También puedes usar "Continue with Single Sign On" o "Continue with Apple ID"
4. Si usas Google, autoriza el acceso a Airtable
5. Si usas email, verifica tu correo siguiendo el enlace que recibirás

### Paso 2: Configuración inicial del perfil
Después de autenticarte con Google, aparecerá una página "Tell us about yourself" para personalizar tu experiencia:

1. **Organización**: Completa el campo "I work at" con el nombre de tu empresa u organización
2. **Industria**: En "We're in the" selecciona el tipo de industria de tu empresa
3. **Tipo de equipo**: En "I am on" elige el tipo de equipo al que perteneces (Marketing, IT, Operations, etc.)
4. Haz clic en "Continue" para proceder

![alt text](assets/airtable/at-setup-profile.png)

> **⚠️ Nota**: Esta información ayuda a Airtable a personalizar tu experiencia, pero puedes completarla con información general si prefieres.

### Paso 3: Configurar tu primera aplicación
Después de completar tu perfil, Airtable te mostrará la página "Build your app" con el asistente Cobuilder:

![alt text](assets/airtable/at-build-app.png)

#### Opción 1: Usar plantillas predefinidas
1. **Start with your idea**: Selecciona una de las opciones predeterminadas:
   - Project Management
   - Data Analysis  
   - Resource Allocation
   - Collaboration Hub
   - Automated Reporting
   - O haz clic en "..." para ver más opciones

2. Al seleccionar una opción, aparecerá una descripción automática de lo que puede hacer esa aplicación

#### Opción 2: Importar datos existentes
En la sección "Or, start with your data" puedes:
- **Import spreadsheets**: Subir archivos CSV, Excel o Google Sheets
- **Import documents**: Subir contratos, presentaciones y otros documentos

#### Para este tutorial:
1. Haz clic en **"Project Management"** como ejemplo
2. Haz clic en **"Next"** para continuar
3. Airtable creará automáticamente una base con estructura predefinida

*Alternativamente, puedes hacer clic en "Import spreadsheets" si ya tienes datos que quieres usar.*

### Ejemplo de estructura básica:
- **Nombre**: Campo de texto para nombres
- **Email**: Campo de email
- **Fecha**: Campo de fecha
- **Estado**: Campo de selección única

### Paso 4: Crear una nueva base manualmente (Alternativo)
Si prefieres crear una base desde cero en cualquier momento:

1. **Desde el workspace**: En tu workspace principal ("My First Workspace"), haz clic en el botón **"Create"** (aparece tanto en el centro como en la barra lateral izquierda)

2. **Seleccionar tipo**: Aparecerán opciones para crear:
   - Una nueva base desde cero
   - Usar una plantilla
   - Importar datos

![alt text](assets/airtable/at-create-base.png)

3. **Configurar la base**: 
   - Asigna un nombre descriptivo a tu base
![alt text](assets/airtable/at-set-base-name.png)
   - Renombre la tabla creada por defecto
![alt text](assets/airtable/at-rename-table.png) 
   - Agrega las columnas/campos que necesites
   - Define los tipos de datos (Texto, Número, Fecha, etc.)
![alt text](assets/airtable/at-create-columns.png)
---


## Parte 2: Conectar Airtable con n8n

### Paso 1: Configurar el workflow en n8n
1. Abre tu instancia de n8n
2. Crea un nuevo workflow
3. Agrega un nodo "Manual Trigger" o "Click to Execute"
4. Haz clic en el botón "+" para agregar un nuevo nodo
5. Busca "Airtable" y selecciona el nodo que necesites:
   - **Create Record**: Para crear nuevos registros
   - **Get All Records**: Para obtener todos los registros
   - **Update Record**: Para actualizar registros existentes
   - **Delete Record**: Para eliminar registros

### Paso 2: Crear el token de acceso en Airtable
1. Ve a [airtable.com/create/tokens](https://airtable.com/create/tokens)
2. Aparecerá la página "Personal access tokens" con el mensaje "You have no personal access tokens"
3. Verás la explicación: "Personal access tokens grant permission to read and write data via the Airtable API"
4. Haz clic en el botón "Create token"

![alt text](assets/airtable/at-create-token.png)

**Nota sobre la navegación**: Puedes llegar aquí también desde el menú lateral:
- Developers → Personal access tokens

### Paso 3: Configurar el token de acceso
Aparecerá el formulario "Create personal access token" con las siguientes secciones:

#### 1. Nombre del token
- En el campo "Name", escribe un nombre descriptivo (ej. "n8n Integration" o "Automatización n8n")
- Nota: El nombre será visible en el historial de revisiones de registros

#### 2. Configurar permisos (Scopes)
Haz clic en "+ Add a scope" y agrega los siguientes permisos:
- **data.records:read** - Para leer registros de la base
- **data.records:write** - Para escribir/crear/actualizar registros  
- **schema.bases:read** - Para leer la estructura de la base

#### 3. Configurar acceso a bases
En la sección "Access", tienes dos opciones:
- **"Add all resources"** - Da acceso a todas tus bases (no recomendado por seguridad)
- **"Add a base"** - Selecciona bases específicas (recomendado)

**Recomendación**: Haz clic en "+ Add a base" y selecciona únicamente la base que vas a usar con n8n

#### 4. Crear el token
Una vez configurado todo, haz clic en "Create token" (botón azul en la esquina inferior derecha)

![alt text](assets/airtable/at-create-token.png)
![alt text](assets/airtable/at-create-token-2.png)

![alt text](assets/airtable/at-create-token-success.png)

### ⚠️ Importante sobre seguridad:
- **Copia el token inmediatamente** y guárdalo en un lugar seguro
- **Nunca compartas este token** con nadie
- Si el token se compromete, revócalo y crea uno nuevo

### Paso 5: Configurar la credencial en n8n
1. En el nodo de Airtable, ve a "Credentials to connect with"
2. Haz clic en "Create New Credential"
3. Selecciona "Access Token" como método de autenticación
4. Pega el token que copiaste de Airtable
5. Haz clic en "Save"

![alt text](assets/airtable/at-n8n-set-create-access-token.png)

### Paso 6: Configurar el nodo de Airtable
1. **Resource**: Selecciona "Record"
2. **Operation**: Elige la operación que necesites:
   - **Get All**: Para obtener todos los registros
   - **Create**: Para crear un nuevo registro
   - **Update**: Para actualizar un registro existente
   - **Delete**: Para eliminar un registro
3. **Base**: Selecciona tu base de Airtable
4. **Table**: Selecciona la tabla específica dentro de tu base

![alt text](assets/airtable/at-n8n-set-create-record.png)


### Paso 7: Probar la conexión
1. Haz clic en "Execute Workflow" o "Test Step"
2. Si todo está configurado correctamente, deberías ver:
   - Una marca verde de éxito
   - Los datos de tu tabla de Airtable en el output
   - Información adicional como IDs de registros y timestamps

![alt text](assets/airtable/at-n8n-test-success.png)

![alt text](assets/airtable/at-create-record-success.png)
---

## Casos de uso comunes

### 1. Sincronizar formularios web con Airtable
- Usar un webhook para recibir datos de formularios
- Procesar los datos en n8n
- Crear registros automáticamente en Airtable

### 2. Automatizar reportes
- Obtener datos de Airtable periódicamente
- Procesar y formatear la información
- Enviar reportes por email o Slack

### 3. Integrar con otras herramientas
- Conectar Airtable con CRMs
- Sincronizar con hojas de cálculo de Google
- Integrar con herramientas de marketing

---

## Solución de problemas comunes

### Error de autenticación
- Verifica que el token esté copiado correctamente
- Confirma que los scopes estén configurados apropiadamente
- Asegúrate de que la base esté incluida en el token

### No se encuentran registros
- Verifica el nombre de la base y tabla
- Confirma que la tabla contenga datos
- Revisa los filtros si estás usando alguno

### Permisos insuficientes
- Agrega los scopes necesarios al token
- Regenera el token si es necesario
- Verifica que la base esté incluida en el token
