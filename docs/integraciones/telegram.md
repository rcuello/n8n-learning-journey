# Tutorial: Integración de Telegram con N8N

## Introducción

Este tutorial te guiará paso a paso para configurar un bot de Telegram y conectarlo con N8N, permitiéndote automatizar mensajes, crear chatbots interactivos y responder a eventos de Telegram de manera automática.

> **Prerrequisitos**: 
> - Cuenta de Telegram activa
> - Acceso a N8N (cloud o self-hosted)
> - Aplicación de Telegram instalada (móvil o desktop)

## Paso 1: Crear un Bot de Telegram

### 1.1 Iniciar Chat con BotFather
1. Abre Telegram en tu dispositivo
2. Busca [**@BotFather**](https://telegram.me/BotFather) en el buscador de Telegram

![Buscar BotFather](assets/telegram/telegram-search-botfather.png)

3. Haz clic en el usuario verificado **BotFather** (tiene una marca azul de verificación)
4. Inicia una conversación haciendo clic en **Start** o enviando `/start`

![alt text](assets/telegram/telegram-start-botfather.png)

> **💡 Tip**: BotFather es el bot oficial de Telegram para crear y gestionar otros bots.

### 1.2 Crear Nuevo Bot
1. En el chat con BotFather, envía el comando: `/newbot`

![Crear nuevo bot](assets/telegram/telegram-newbot-command.png)

2. BotFather te responderá: *"Alright, a new bot. How are we going to call it? Please choose a name for your bot."*
3. Envía el **nombre** de tu bot (puede contener espacios y caracteres especiales)
   - Ejemplo: "Mi N8NBot Automatizado"



### 1.3 Configurar Username del Bot
1. BotFather te pedirá un username: *"Good. Now let's choose a username for your bot. It must end in `bot`. Like this, for example: TetrisBot or tetris_bot."*
2. Envía el **username** de tu bot siguiendo estas reglas:
   - Debe terminar en `bot`
   - Entre 5 y 32 caracteres
   - Solo letras latinas, números y guiones bajos
   - No se puede cambiar después
   - Ejemplo: `mi_n8n_bot_automatizado_bot`

![Configurar username](assets/telegram/telegram-bot-username.png)

### 1.4 Obtener el Token de Acceso
1. Si todo está correcto, BotFather te enviará un mensaje de confirmación con:
   - Confirmación de creación del bot
   - **Token de acceso** (una cadena larga como: `723456789:ABCdefGHIjklMNOpqrsTUVwxyz`)
   - Enlace directo a tu bot
2. **Copia y guarda el token** en un lugar seguro

![Token de acceso](assets/telegram/telegram-bot-token.png)

> **⚠️ Importante**: El token es como una contraseña. No lo compartas públicamente y guárdalo de forma segura.

## Paso 2: Configurar Credenciales en N8N

### 2.1 Acceder a Credenciales
1. En N8N, crea un nuevo workflow o abre uno existente
2. Agrega un nodo **Telegram** o **Telegram Trigger**
3. En la configuración del nodo, busca el campo **Credentials**
4. Haz clic en **Create New**

![alt text](assets/telegram/n8n-telegram-create-trigger.png)

![Crear credenciales N8N](assets/telegram/n8n-telegram-create-credentials.png)



### 2.2 Configurar Token de Acceso
1. Selecciona **Telegram API** del menú desplegable
2. En el campo **Access Token**, pega el token que obtuviste de BotFather
3. Dale un nombre descriptivo a la credencial: Ejemplo: "Mi Bot Telegram"
4. Haz clic en **Save**

![Configurar token](assets/telegram/n8n-telegram-access-token.png)


### 2.3 Probar la Conexión
1. Después de guardar, N8N debería mostrar "Connected" o similar
2. Si hay algún error, verifica que el token esté correcto y completo

## Paso 3: Iniciar y Probar el Bot

### 3.1 Acceder a tu Bot
1. Una vez creado el bot, BotFather te proporcionará un enlace directo como: `https://t.me/tu_bot_username_bot`
2. Haz clic en el enlace o busca tu bot por su username en Telegram
3. Verás el perfil de tu bot recién creado
![alt text](assets/telegram/telegram-start-bot-chat.png)

### 3.2 Iniciar el Bot
1. En el chat de tu bot, haz clic en **Start** o envía `/start`

![Iniciar bot boton](assets/telegram/telegram-start-02-bot-chat.png)
![Iniciar bot comando](assets/telegram/telegram-start-03-bot-chat.png)

2. Si el bot no responde aún, es normal - necesita estar configurado en N8N primero
3. Puedes enviar algunos mensajes de prueba para tener datos cuando configures N8N

> **💡 Tip**: Es recomendable iniciar el bot antes de configurar N8N para asegurar que la comunicación funcione correctamente.


### 3.3 Verificar Estado del Bot
1. El bot aparecerá como "online" pero no responderá hasta que configures N8N
2. Puedes verificar que el token funciona probando la conexión en N8N
3. Los mensajes que envíes ahora aparecerán cuando configures el Telegram Trigger

## Paso 4: Configurar el Bot para Recibir Mensajes

### 4.1 Usando Telegram Trigger
1. Agrega un nodo **Telegram Trigger** a tu workflow
2. Selecciona las credenciales que configuraste
3. En **Trigger On**, selecciona qué tipo de eventos quieres escuchar:
   - **message** - Mensajes de texto

![Configurar Telegram Trigger](assets/telegram/n8n-telegram-trigger-config.png)

### 4.2 Obtener Chat ID
Para enviar mensajes a usuarios específicos, necesitas sus Chat IDs:

1. Envíe un mensaje a tu bot
2. Usa el nodo Telegram Trigger para capturar el mensaje
3. En la salida del nodo, encontrarás el `chat.id`
4. Guarda este ID para enviar mensajes devuelta

![Obtener Chat ID](assets/telegram/n8n-telegram-chat-id.png)

## Paso 5: Enviar Mensajes desde N8N

### 5.1 Configurar Nodo Telegram
1. Agrega un nodo **Telegram** después del trigger

![alt text](assets/telegram/n8n-telegram-set-send-message.png)

2. Selecciona la operación **Send Text Message**

![alt text](assets/telegram/n8n-telegram-select-option-send-message.png)

3. Completa los campos:
   - **Chat ID**: ID del chat donde enviar el mensaje `{{ $json.message.chat.id }}`
   - **Text**: Contenido del mensaje
   - **Parse Mode**: Opcional (HTML, Markdown, etc.)

![alt text](assets/telegram/n8n-telegram-send-message.png)

![alt text](assets/telegram/n8n-telegram-basic-send-message-workflow.png)

![alt text](assets/telegram/n8n-telegram-basic-send-message-workflow-result.png)

4. Para remover la atribución agrega un nuevo campo `Add Field`
5. Selecciona `Append n8n Attribution` y desactivalo.

![alt text](assets/telegram/n8n-telegram-basic-send-message-remove-attribution.png)

6. Envia un nuevo mensaje y notarás que ya no se envia la atribución de n8n.

![alt text](assets/telegram/n8n-telegram-basic-send-message-remove-attribution-sucess.png)

### 5.2 Usar Variables Dinámicas
Puedes usar datos del trigger en tus mensajes:
```
Hola  {{ $json.message.from.first_name }}, 
recibi tu mensaje : {{ $json.message.text }}
```

![alt text](assets/telegram/n8n-telegram-dynamic-variables.png)

![alt text](assets/telegram/n8n-telegram-dynamic-variables-check-response.png)

## Paso 6: Crear un Bot Interactivo

### 6.1 Bot de Respuesta Automática

### Agregar el Nodo AI Agent
1. En tu workflow, entre el **Telegram Trigger** y el nodo **Telegram** de respuesta, agrega un nodo **AI Agent**

![alt text](assets/telegram/n8n-telegram-add-node-ai-agent.png)

2. Arrastra una conexión desde el Telegram Trigger hacia el AI Agent
3. Conecta la salida del AI Agent al nodo Telegram para enviar la respuesta

![Workflow con AI Agent](assets/telegram/n8n-telegram-ai-workflow.png)

#### Seleccionar el Modelo OpenAI
1. En el nodo **AI Agent**, configura el **Chat Model**
2. Selecciona **OpenAI Chat Model** del menú desplegable

![alt text](assets/telegram/n8n-telegram-ai-select-openai-chat-model.png)

3. Crea nuevas credenciales para OpenAI:
   - Ve a [OpenAI Platform](https://platform.openai.com/api-keys)
   - Genera una nueva API Key
   - En N8N, pega la API Key en las credenciales de OpenAI

#### Configurar el Modelo
- **Model**: Selecciona `gpt-3.5-turbo` o `gpt-4o-mini` según tu preferencia y presupuesto

![alt text](assets/telegram/n8n-telegram-openai-config-chat-model.png)

![alt text](assets/telegram/n8n-telegram-openai-workflow-with-model.png)

### 6.3 Configurar la Memory (Memoria)
#### Agregar Simple Memory

1. En el AI Agent, configura el componente **Memory**
2. Selecciona **Simple Memory** para mantener el contexto de la conversación
3. Esto permite que el bot recuerde mensajes anteriores en la misma sesión

![alt text](assets/telegram/n8n-telegram-add-simple-memory.png)

#### Configuración de Memory
- **Session ID**: Para usar el id de sesión de Telegram usa `{{ $('Telegram Trigger').item.json.message.chat.id }}`

![alt text](assets/telegram/n8n-telegram-simple-memory-config.png)

![alt text](assets/telegram/n8n-telegram-openai-workflow-with-memory.png)

> **💡 Tip**: Si usas el chat integrado por N8N usa `{{ $json.message.chat.id }}` para mantener conversaciones separadas por usuario.

### 6.4 Definir el System Prompt

#### Personalizar la Personalidad del Bot
1. En el AI Agent agrega la opción **System Message**

![alt text](assets/telegram/n8n-telegram-add-system-message.png)

2. configura el **System Message** para definir cómo debe comportarse:

```
Eres un asistente virtual útil y amigable integrado en Telegram. 

Características:
- Respondes en español de forma clara y concisa
- Eres profesional pero cercano
- Si no sabes algo, lo admites honestamente
- Mantienes conversaciones naturales y fluidas

Instrucciones:
- Responde directamente sin mencionar que eres un AI
- No excedas más de 200 carácteres en tu respuesta
- Usa emojis ocasionalmente para hacer las conversaciones más amigables
- Si te piden algo que no puedes hacer, explica alternativas útiles
```

![alt text](assets/telegram/n8n-telegram-system-message.png)

3. configura el **User Message** que proviene de telegram

![alt text](assets/telegram/n8n-telegram-user-message.png)

### 6.5 Configurar la Respuesta de Telegram

#### Configurar el Nodo Telegram de Salida
1. **Chat ID**: `{{ $('Telegram Trigger').item.json.message.chat.id }}`

![alt text](assets/telegram/n8n-telegram-config-user-message-chat-id.png)

2. **Text**: `{{ $json.output }}` (la respuesta generada por el AI Agent)

3. **Parse Mode**: `Markdown` (para formato enriquecido si el AI lo usa)
4. **Disable n8n Attribution**: Activado (para respuestas más limpias)

![alt text](assets/telegram/n8n-telegram-config-user-message-disable-n8n-attribution.png)


### 6.6 Workflow Completo

#### Estructura del Flujo
```
Telegram Trigger → AI Agent → Telegram Send Message
                     ↓
                Chat Model (OpenAI)
                     ↓
                Memory (Simple)
                     
```

![alt text](assets/telegram/n8n-telegram-ai-agent-full-workflow.png)

![alt text](assets/telegram/n8n-telegram-ai-agent-full-workflow-result.png)

## Conclusión

Con esta configuración, tendrás un bot de Telegram inteligente que puede:

✅ Mantener conversaciones naturales  
✅ Recordar el contexto de la conversación  
✅ Responder preguntas complejas  
✅ Realizar cálculos y tareas específicas  
✅ Adaptarse al tono y necesidades del usuario  
✅ Proporcionar respuestas coherentes y útiles  


### Recursos Adicionales
- [Documentación oficial de Telegram Bot API](https://core.telegram.org/bots/api)
- [Documentación de N8N para Telegram](https://docs.n8n.io/integrations/builtin/trigger-nodes/n8n-nodes-base.telegramtrigger/)
- [BotFather - Documentación de funciones](https://core.telegram.org/bots/features)
- [Telegram Bot Features](https://core.telegram.org/bots#6-botfather)
- [Guía de mejores prácticas para bots](https://core.telegram.org/bots#3-how-do-i-create-a-bot)