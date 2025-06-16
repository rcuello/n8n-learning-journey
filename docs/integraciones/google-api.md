# Tutorial: Configuración de APIs de Google para N8N

## Introducción

Este tutorial te guiará paso a paso para configurar las APIs de Google Cloud y conectarlas con N8N, permitiéndote automatizar servicios como Google Sheets, Google Drive, Google Docs, Google Calendar y otros servicios de Google.

> **Prerrequisitos**: 
> - Cuenta de Google activa
> - Acceso a N8N (cloud o self-hosted)
> - Navegador web actualizado

## Paso 1: Configuración Inicial en Google Cloud Console

### 1.1 Acceso y Aceptación de Términos
1. Accede a [Google Cloud Console](https://console.cloud.google.com/)
2. Si es tu primera vez, verás una pantalla de bienvenida
3. **Acepta los Términos de Servicio** marcando la casilla correspondiente
4. Haz clic en **Aceptar y continuar**

![alt text](assets/gcp/gcp-accept-continue.png)

### 1.2 Cambiar Idioma (Recomendado)
1. En la esquina superior derecha, busca el selector de **Preferencias**
![alt text](assets/gcp/gcp-menu-preference.png)

2. Cambia a **English** para seguir la documentación oficial
3. Haz clic en **Save** o **Guardar**

![alt text](assets/gcp/gcp-language.png)


> **💡 Tip**: Usar inglés facilita seguir la documentación oficial y resolver problemas.

## Paso 2: Crear un Nuevo Proyecto

### 2.1 Crear Proyecto
1. En la parte superior de la consola, haz clic en el **selector de proyectos** (junto al logo de Google Cloud)
2. En la ventana emergente, haz clic en **New Project** (Nuevo Proyecto)
![alt text](assets/gcp/gcp-new-project.png)
3. Completa la información del proyecto:
   - **Project name**: Ejemplo: "N8N Google Integration"
   - **Project ID**: Se genera automáticamente (puedes modificarlo si quieres)
   - **Location**: Selecciona tu organización si tienes una, o deja "No organization"
4. Haz clic en **Create** (Crear)

![alt text](assets/gcp/gcp-create-project.png)

### 2.2 Seleccionar el Proyecto
1. Espera a que se cree el proyecto (puede tomar unos segundos)
2. Una vez creado, asegúrate de que esté seleccionado en el selector de proyectos
3. Verás el nombre del proyecto en la barra superior

> **⚠️ Importante**: Siempre verifica que tengas el proyecto correcto seleccionado antes de continuar.

## Paso 3: Habilitar APIs de Google

### 3.1 Acceder a la Biblioteca de APIs
1. En el menú hamburguesa (☰) de la izquierda
2. Ve a **APIs & Services** > **Library**
3. Se abrirá la biblioteca de APIs disponibles

![alt text](assets/gcp/gcp-api-library.png)

### 3.2 Habilitar APIs Específicas

#### Para Google Sheets:
1. En el buscador, escribe "Google Sheets API"
2. Haz clic en **Google Sheets API**
![alt text](assets/gcp/gcp-search-sheets-api.png)
3. Haz clic en **Enable** (Habilitar)
4. Espera a que se habilite (verás una confirmación)
![alt text](assets/gcp/gcp-enable-sheets-api.png)


#### Para otros servicios (repite según necesites):
- **Google Drive API** - Para gestión de archivos
- **Google Docs API** - Para documentos de texto
- **Google Calendar API** - Para eventos de calendario
- **Google Slides API** - Para presentaciones
- **Gmail API** - Para correo electrónico
- **Google Analytics API** - Para análisis web
- **Google Ads API** - Para publicidad

> **💡 Tip**: Solo habilita las APIs que realmente vas a usar para mantener tu proyecto organizado.

## Paso 4: Configurar OAuth Consent Screen

### 4.1 Pantalla Inicial de Configuración
1. Ve a **APIs & Services** > **OAuth consent screen**
![alt text](assets/gcp/gcp-oauth-consent.png)

2. Verás la pantalla: **"Google Auth Platform not configured yet"**
3. Con el mensaje: *"Get started to configure your application's identity and manage credentials for calling Google APIs and Sign-in with Google"*
4. Haz clic en **"Get started"**

![alt text](assets/gcp/gcp-oauth-plat-not-configured.png)


### 4.2 App Information
Completa los campos requeridos:

**Información Básica:**
- **App name**: "N8N Workflow Connector" (o el nombre que prefieras)
- **User support email**: Selecciona tu dirección de correo electrónico del dropdown

![alt text](assets/gcp/gcp-oauth-consent-app-information.png)

### 4.3 Seleccionar Audience (Audiencia)
Se te presentarán dos opciones:

**External** (Recomendado para la mayoría de casos):
- Para cuentas de Google personales
- Para uso con cualquier cuenta de Google
- Requiere proceso de verificación para publicar (pero no para desarrollo)

**Internal** (Solo si tienes Google Workspace):
- Solo disponible si tu cuenta pertenece a una organización Google Workspace
- Solo usuarios de tu organización pueden usar la app

![alt text](assets/gcp/gcp-oauth-consent-audience.png)

> **💡 Recomendación**: Selecciona **External** a menos que tengas Google Workspace y solo necesites acceso interno.

### 4.4 Contact Information
**Developer contact information:**
- **Email addresses**: Agrega tu correo electrónico principal
- Puedes agregar correos adicionales separados por comas
- Este contacto es para que Google se comunique contigo sobre la app

### 4.5 Finalizar Configuración Inicial
1. Revisa toda la información ingresada
2. Haz clic en **Continue** y luego **Create**

![alt text](assets/gcp/gcp-oauth-consent-finish.png)

## Paso 5: Audience

### 5.1 Test Users
1. Ve a **APIs & Services** > **OAuth consent screen** 
2. En la sección **Audience**, busca la opción **Test Users**
3. Haz clic en **+ Add Users**
4. Agrega tu dirección de correo electrónico principal
5. Agrega cualquier otro correo que necesite acceso durante las pruebas
6. Haz clic en **Add** para cada correo
7. Haz clic en **Save**

![alt text](assets/gcp/gcp-oauth-consent-test-users.png)

> **⚠️ Importante**: Solo los usuarios agregados aquí podrán autorizar la aplicación mientras esté en modo de desarrollo.


## Paso 6: Crear Credenciales OAuth

### 6.1 Crear OAuth Client ID
1. Ve a **APIs & Services** > **Credentials**
2. Haz clic en **Create Credentials**

![alt text](assets/gcp/gcp-oauth-consent-create-credentials.png)

3. Selecciona **OAuth client ID**

![alt text](assets/gcp/gcp-oauth-consent-oauth-client-id.png)

4. Elige **Web application**
5. Dale un nombre: Ejemplo: "N8N Web Client"

![alt text](assets/gcp/gcp-oauth-consent-web-application.png)

### 6.2 Configurar URIs de Redirección
1. En **Authorized redirect URIs**, necesitas agregar la URL de tu instancia N8N
2. Para obtener la URI correcta:
   - Ve a tu instancia de N8N
   - Crea un nuevo workflow
   - Agrega un nodo de Google (ej: Google Drive)
   - En la configuración de credenciales, copia la URI que aparece
   
![alt text](assets/gcp/gcp-n8n-google-drive-callback-url.png)

3. Pega esta URI en Google Cloud Console

![alt text](assets/gcp/gcp-client-auth-redirect-uri.png)

4. Haz clic en **Create**

### 4.3 Guardar Credenciales
- Google Cloud te proporcionará:
  - **Client ID**
  - **Client Secret**

![alt text](assets/gcp/gcp-oauth-consent-save-credentials.png)

> **⚠️ Importante**: Guarda estos valores, los necesitarás en N8N.

## Paso 7: Configurar Credenciales en N8N

### 7.1 Crear Nueva Credencial
1. En N8N, ve al nodo de Google que quieres configurar
2. En **Credentials**, selecciona **Create New**
3. Selecciona el tipo de credencial de Google apropiado

### 7.2 Completar Información
1. **Client ID**: Pega el Client ID de Google Cloud
2. **Client Secret**: Pega el Client Secret de Google Cloud
3. Haz clic en **Sign in with Google**

![alt text](assets/gcp/gcp-n8n-google-set-credentials.png)

### 5.3 Autorización
1. Se abrirá una ventana de Google
2. Selecciona la cuenta de Google que configuraste
![alt text](assets/gcp/gcp-n8n-google-select-account.png)

3. Haz clic en **Continue**

![alt text](assets/gcp/gcp-n8n-google-continue.png)

4. Acepta todos los permisos solicitados
![alt text](assets/gcp/gcp-n8n-google-grant-all-access.png)

5. La ventana se cerrará y verás "Connected" en N8N

![alt text](assets/gcp/gcp-n8n-google-connected.png)

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
- [Video Tutorial](https://www.youtube.com/watch?v=_5q0TOkZkIk&ab_channel=KevinBelier%7CAutomatizacionIA)
