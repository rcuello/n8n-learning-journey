# Tutorial: Configuración de APIs de Google para N8N

## Introducción

Este tutorial te guiará paso a paso para configurar las APIs de Google Cloud y conectarlas con N8N, permitiéndote automatizar servicios como Google Sheets, Google Drive, Google Docs, Google Calendar y otros servicios de Google.

> **Prerrequisito**: Necesitas tener una cuenta de Google Cloud activa y acceso a N8N.

## Paso 1: Configuración Inicial en Google Cloud

### 1.1 Cambiar Idioma a Inglés
1. Accede a tu consola de Google Cloud
2. Ve a configuración de idioma
3. Selecciona **English (United States)**
4. Guarda los cambios

> **Nota**: Es recomendable usar inglés ya que toda la documentación oficial está en este idioma.

## Paso 2: Habilitar APIs de Google

### 2.1 Acceder a APIs & Services
1. En el menú hamburguesa de Google Cloud Console
2. Ve a **APIs & Services**
3. Selecciona **Library**

### 2.2 Habilitar Google Sheets API (Ejemplo)
1. En la biblioteca de APIs, busca "Google Sheets"
2. Selecciona **Google Sheets API**
3. Haz clic en **Enable**

## Paso 3: Configurar OAuth Consent Screen

### 3.1 Configuración Básica
1. Ve a **APIs & Services** > **OAuth consent screen**
2. Completa los campos requeridos:
   - **App name**: Ejemplo: "Google N8N Integration"
   - **User support email**: Tu correo electrónico
   - **Developer contact**: El mismo correo electrónico
3. Haz clic en **Save and Continue**

### 3.2 Scopes
- En la sección **Scopes**, puedes dejarlo como está por defecto
- Haz clic en **Save and Continue**

### 3.3 Test Users
- Agrega tu correo electrónico como usuario de prueba
- Haz clic en **Add Users**
- Guarda y continúa

## Paso 4: Crear Credenciales OAuth

### 4.1 Crear OAuth Client ID
1. Ve a **APIs & Services** > **Credentials**
2. Haz clic en **Create Credentials**
3. Selecciona **OAuth client ID**
4. Elige **Web application**
5. Dale un nombre: Ejemplo: "N8N Google Integration"

### 4.2 Configurar URIs de Redirección
1. En **Authorized redirect URIs**, necesitas agregar la URL de tu instancia N8N
2. Para obtener la URI correcta:
   - Ve a tu instancia de N8N
   - Crea un nuevo workflow
   - Agrega un nodo de Google (ej: Google Sheets)
   - En la configuración de credenciales, copia la URI que aparece
3. Pega esta URI en Google Cloud Console
4. Haz clic en **Create**

### 4.3 Guardar Credenciales
- Google Cloud te proporcionará:
  - **Client ID**
  - **Client Secret**
- **Importante**: Guarda estos valores, los necesitarás en N8N

## Paso 5: Configurar Credenciales en N8N

### 5.1 Crear Nueva Credencial
1. En N8N, ve al nodo de Google que quieres configurar
2. En **Credentials**, selecciona **Create New**
3. Selecciona el tipo de credencial de Google apropiado

### 5.2 Completar Información
1. **Client ID**: Pega el Client ID de Google Cloud
2. **Client Secret**: Pega el Client Secret de Google Cloud
3. Haz clic en **Connect my account**

### 5.3 Autorización
1. Se abrirá una ventana de Google
2. Selecciona la cuenta de Google que configuraste
3. Haz clic en **Continue**
4. Acepta todos los permisos solicitados
5. La ventana se cerrará y verás "Connected" en N8N

## Paso 6: Prueba de Funcionamiento

### 6.1 Crear un Test Simple
1. Configura un nodo de Google Sheets para crear un documento
2. Dale un nombre: "Test N8N"
3. Ejecuta el nodo
4. Verifica en tu Google Drive que se haya creado el documento

## Paso 7: Habilitar Servicios Adicionales

### 7.1 Para Otros Servicios de Google
Para cada servicio adicional que quieras usar (Google Drive, Google Docs, etc.):

1. **Habilitar la API**:
   - Ve a **APIs & Services** > **Library**
   - Busca el servicio (ej: "Google Drive API")
   - Haz clic en **Enable**

2. **Usar las Mismas Credenciales**:
   - En N8N, puedes usar las mismas credenciales OAuth
   - Solo necesitas el mismo Client ID y Client Secret
   - El proceso de autorización se repite para cada servicio

### 7.2 Servicios Comunes de Google
- **Google Drive API**
- **Google Docs API**
- **Google Calendar API**
- **Google Slides API**
- **Gmail API**
- **Google Analytics API**
- **Google Ads API**

## Resolución de Problemas Comunes

### Error de URI de Redirección
- **Problema**: "redirect_uri_mismatch"
- **Solución**: Verifica que la URI en Google Cloud coincida exactamente con la de N8N

### Error de Permisos
- **Problema**: "insufficient_permissions"
- **Solución**: Revisa que hayas habilitado la API específica en Google Cloud

### Error de Autenticación
- **Problema**: No se puede conectar la cuenta
- **Solución**: Verifica que el Client ID y Client Secret sean correctos

## Mejores Prácticas

### Seguridad
- Mantén tus credenciales seguras
- No compartas Client ID y Client Secret públicamente
- Revisa regularmente los permisos otorgados

### Organización
- Usa nombres descriptivos para tus aplicaciones OAuth
- Documenta qué servicios has habilitado
- Mantén un registro de tus credenciales

### Limitaciones y Cuotas
- Cada API de Google tiene límites de uso
- Monitorea tu consumo en Google Cloud Console
- Considera implementar manejo de errores para límites de tasa

## Conclusión

Una vez completada esta configuración, tendrás acceso completo a los servicios de Google desde N8N. Esta configuración inicial te permitirá crear automatizaciones potentes integrando múltiples servicios de Google en tus workflows.


### Recursos Adicionales
- [Documentación oficial de N8N para Google](https://docs.n8n.io/integrations/builtin/credentials/google/)
- [Google Cloud Console](https://console.cloud.google.com/)
- [APIs de Google disponibles](https://developers.google.com/apis-explorer)
- [Video Tutorial](https://www.youtube.com/watch?v=miUnVwkndbM)
