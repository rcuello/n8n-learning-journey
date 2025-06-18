# Guía para generar API Key de Google Gemini

## Introducción
Esta guía te ayudará a obtener una API key de Google Gemini para usar con n8n y otros servicios. La API key te permitirá acceder a los modelos de inteligencia artificial de Google Gemini.

## Pasos para obtener la API Key

### 1. Acceder a Google AI Studio
- Ve a [Google AI Studio](https://aistudio.google.com/)
- Inicia sesión con tu cuenta de Google

![alt text](assets/google-gemini/google-gemini-dashboard.png)

### 2. Crear o seleccionar un proyecto
- Una vez en Google AI Studio, busca el botón **"Create API key"**
- Si no tienes un proyecto de Google Cloud, necesitarás crear uno:
  - Ve a [Google Cloud Console](https://console.cloud.google.com/)
  - Crea un nuevo proyecto o selecciona uno existente
  - Asegúrate de que la API de Gemini esté habilitada para tu proyecto

### 3. Generar la API Key
- En Google AI Studio, haz clic en [**"Create API key"**](https://aistudio.google.com/apikey)
- Selecciona el proyecto de Google Cloud que deseas usar
- Sigue los pasos del asistente para generar tu clave
- Una vez generada, **copia la API key inmediatamente** (no podrás verla nuevamente)

![alt text](assets/google-gemini/google-gemini-create-api-key.png)

### 4. Guardar la API Key de forma segura
- Guarda la API key en un lugar seguro
- **Nunca compartas esta clave públicamente**
- Considera usar un gestor de contraseñas para almacenarla

## Configuración en n8n

### 1. Crear credencial en n8n
- Ve a tu instancia de n8n
- Navega a **Credentials** → **Add Credential**
- Busca **"Gemini"** o **"Gemini Palm API"**
- Haz clic en **"Continue"**

### 2. Configurar la credencial
- **Host**: Deja el valor por defecto (generalmente no necesitas cambiarlo)
- **API Key**: Pega la API key que copiaste de Google AI Studio
- **Nombre**: Asigna un nombre descriptivo a tu credencial
- Haz clic en **"Save"**

### 3. Verificar la configuración
- Deberías ver un mensaje verde confirmando que la credencial se guardó correctamente
- Copia el **Credential ID** que se genera (lo necesitarás para tus workflows)

## Uso en workflows de n8n

1. **Agregar nodo Gemini**: En tu workflow, agrega un nodo de Google Gemini
2. **Seleccionar credencial**: En la configuración del nodo, selecciona la credencial que acabas de crear
3. **Configurar parámetros**: Ajusta los parámetros según tus necesidades (modelo, prompt, etc.)

## Consejos importantes

### Seguridad
- ⚠️ **Nunca expongas tu API key en código público**
- 🔒 Usa variables de entorno o sistemas de gestión de secretos
- 🔄 Regenera la clave periódicamente por seguridad

### Límites y costos
- 📊 Revisa los límites de uso de la API en tu proyecto de Google Cloud
- 💰 Monitorea el uso para evitar costos inesperados
- 📈 Configura alertas de facturación si es necesario

### Solución de problemas
- **Error de autenticación**: Verifica que la API key esté correcta y el proyecto esté activo
- **Límites excedidos**: Revisa las cuotas en Google Cloud Console
- **API deshabilitada**: Asegúrate de que la API de Gemini esté habilitada en tu proyecto

## Recursos adicionales

- [Documentación oficial de Google AI Studio](https://ai.google.dev/)
- [Documentación de n8n para Google Gemini](https://docs.n8n.io/)
- [Google Cloud Console](https://console.cloud.google.com/)

## Notas finales

Una vez que tengas tu API key configurada correctamente, podrás usar Google Gemini en tus workflows de n8n para tareas como:
- Generación de texto
- Análisis de contenido
- Procesamiento de lenguaje natural
- Y muchas otras aplicaciones de IA

¡Recuerda siempre mantener tus credenciales seguras y monitorear el uso de tu API!