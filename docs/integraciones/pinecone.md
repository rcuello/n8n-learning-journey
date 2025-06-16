# Tutorial: Configuración de Pinecone para N8N

## Introducción

Este tutorial te guiará paso a paso para crear una cuenta en Pinecone, configurar un índice vectorial y conectarlo con N8N, permitiéndote automatizar operaciones de búsqueda vectorial, almacenamiento de embeddings y recuperación de información semántica en tus workflows de IA.

> **Prerrequisitos**: 
> - Cuenta de correo electrónico activa
> - Acceso a N8N (cloud o self-hosted)
> - Navegador web actualizado
> - Conocimientos básicos de vectores y embeddings (opcional pero recomendado)

## ¿Qué es Pinecone?

Pinecone es una base de datos vectorial completamente administrada que permite realizar búsquedas de similitud a gran escala. Es especialmente útil para aplicaciones de IA como:
- Búsqueda semántica
- Sistemas de recomendación
- Chatbots con memoria
- Análisis de similitud de documentos
- RAG (Retrieval-Augmented Generation)

## Paso 1: Crear Cuenta en Pinecone

### 1.1 Acceso a Pinecone
1. Ve a [Pinecone.io](https://www.pinecone.io/)
2. Haz clic en **Sign Up** o **Get Started Free**
![alt text](assets/pinecone/pinecone-sign-up.png)

3. Se abrirá el formulario de registro

### 1.2 Registro de Nueva Cuenta
1. **Método 1 - Con Google**:
   - Haz clic en **Continue with Google**
   - Selecciona tu cuenta de Google
   - Autoriza los permisos necesarios

2. **Método 2 - Con Email**:
   - Ingresa tu **Email address**
   - Crea una **Password** segura
   - Haz clic en **Sign Up**

![alt text](assets/pinecone/pinecone-register.png)

### 1.3 Verificación de Email
1. Revisa tu correo electrónico
2. Busca el email de Pinecone con el asunto "Verify your email"
3. Haz clic en **Verify Email** en el correo
4. Serás redirigido a la consola de Pinecone

> **💡 Tip**: Si no recibes el email, revisa tu carpeta de spam o correo no deseado.

## Paso 2: Configuración Inicial de la Cuenta

### 2.1 Completar Perfil
1. Una vez verificado el email, accederás al dashboard de Pinecone
2. Es posible que te solicite completar información adicional:
   - **First Name** (Nombre)
   - **Last Name** (Apellido)
   - **Company** (Empresa - opcional)
   - **Use case** (Caso de uso)
![alt text](assets/pinecone/pinecone-create-your-account.png)

3. Selecciona tu caso de uso principal o "Other"
4. Haz clic en **Continue**
![alt text](assets/pinecone/pinecone-customize-your-setup.png)

### 2.2 Generación Automática de API Key
1. Después de hacer clic en **Continue**, aparecerá automáticamente un diálogo modal
2. Verás el mensaje: **"API key generated"**
3. El sistema muestra: *"Your 'default' API key has been generated"*
4. **⚠️ IMPORTANTE**: Aparecerá una advertencia que dice:
   - **"You must copy and save this key immediately"**
   - *"For security reasons, we will not show you this key again after you close this dialog. Please save it somewhere secure for future use."*

5. **Copiar la API Key**:
   - Haz clic en el ícono de **Copy** (📋) junto a la clave enmascarada
   - La clave tiene el formato: `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`
   - **Guarda esta clave inmediatamente** en un lugar seguro (bloc de notas, gestor de contraseñas, etc.)

6. Una vez copiada y guardada, haz clic en **Close**

> **🔒 Seguridad Crítica**: Esta es la única vez que verás la API key completa. Si la pierdes, tendrás que generar una nueva desde la sección API Keys.

![alt text](assets/pinecone/pinecone-api-key-generated.png)

### 2.3 Explorar el Dashboard
Familiarízate con los elementos principales:
- **Indexes**: Donde crearás y gestionarás tus índices vectoriales
- **API Keys**: Para obtener las credenciales de autenticación
- **Usage**: Monitoreo de consumo y límites
- **Billing**: Información de facturación y plan actual

> **💡 Plan Gratuito**: Pinecone ofrece un plan gratuito con 1 índice y hasta 100,000 vectores.

## Paso 3: Crear tu Primer Índice

### 3.1 Navegar a Indexes
1. En el sidebar izquierdo, haz clic en **Indexes**
2. Verás la página de gestión de índices (inicialmente vacía)
3. Haz clic en **Create Index**

![alt text](assets/pinecone/pinecone-create-index.png)

### 3.2 Configurar el Índice
Completa la configuración del índice:

**Información Básica:**
- **Index Name**: Ejemplo: "n8n-embeddings" (solo minúsculas, números y guiones)
- **Dimensions**: Número de dimensiones de tus vectores
  - Para OpenAI text-embedding-3-small, utiliza: **1536**
  - Para otros modelos, consulta su documentación

![alt text](assets/pinecone/pinecone-text-embedding-3-small-dimensions-1536.png)
  
**Configuración Avanzada:**
- **Metric**: Selecciona la métrica de distancia
  - **Cosine** (recomendado para la mayoría de casos)
  - **Euclidean** (distancia euclidiana)
  - **Dotproduct** (producto punto)
  
- **Cloud Provider**: Selecciona el proveedor de nube
  - **AWS** (recomendado para mejor rendimiento)

![alt text](assets/pinecone/pinecone-cloud-provider.png)

- **Region**: Selecciona la región más cercana a tu ubicación
  - Virginia **us-east-1**

![alt text](assets/pinecone/pinecone-region-us-east-1.png)

### 3.3 Crear el Índice
1. Revisa toda la configuración
2. Haz clic en **Create Index**

![alt text](assets/pinecone/pinecone-create-index-confirm.png)

3. El proceso puede tomar 1-2 minutos
4. Una vez creado, verás el estado como "Ready"

![alt text](assets/pinecone/pinecone-index-ready.png)


> **⚠️ Importante**: Las dimensiones del índice no se pueden cambiar después de creado. Asegúrate de usar el número correcto.

## Paso 4: Obtener API Key

### 4.1 Navegar a API Keys
1. En el sidebar izquierdo, haz clic en **API Keys**
2. Verás tu clave API por defecto ya creada
3. La clave tiene un formato similar a: `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`

### 4.2 Copiar API Key
1. Haz clic en el ícono de **Copy** junto a tu API key
2. Guarda esta clave en un lugar seguro
3. **NUNCA** compartas tu API key públicamente

![alt text](assets/pinecone/pinecone-create-api-key.png)

### 4.3 Obtener Environment
1. En la misma página de API Keys, encontrarás tu **Environment**
2. Tiene un formato como: `your-env-12345.svc.pinecone.amazonaws.com`
3. También copia y guarda este valor

> **🔒 Seguridad**: Trata tu API key como una contraseña. No la incluyas en código público o repositorios.

## Paso 5: Configurar Pinecone en N8N

### 5.1 Agregar Nodo Pinecone
1. En tu workflow de N8N, haz clic en **+** para agregar un nodo
2. Busca "Pinecone" en la lista de nodos
3. Selecciona **Pinecone Vector Store**
4. Arrastra el nodo a tu workflow

### 5.2 Crear Nueva Credencial
1. En la configuración del nodo Pinecone
2. En **Credentials**, haz clic en **Create New**
3. Se abrirá el formulario de credenciales de Pinecone



### 5.3 Completar Credenciales
Ingresa la información obtenida de Pinecone:

1. **API Key**: Pega la API key que copiaste de Pinecone


### 5.4 Probar Conexión
1. Haz clic en **Test** para verificar la conexión
2. Si todo está correcto, verás "Connection successful"
3. Haz clic en **Save** para guardar las credenciales

![alt text](assets/pinecone/pinecone-n8n-set-api-key.png)

## Paso 6: Configurar el Nodo Pinecone

### 6.1 Agregar Nodo Pinecone Vector Store
1. En tu workflow de N8N, haz clic en **+** para agregar un nodo
2. Busca "Pinecone" en la lista de nodos
3. Selecciona **Pinecone Vector Store**
4. Arrastra el nodo a tu workflow

![alt text](assets/pinecone/pinecone-n8n-select-vector-store.png)

**Index Name**: Ingresa el nombre del índice que creaste (ej: "n8n-embeddings")

### 6.2 Configurar Credenciales
1. En la pestaña **Parameters** del nodo Pinecone Vector Store
2. En **Credential to connect with**, haz clic en el dropdown
3. Selecciona **Create New Credential** si es tu primera vez
4. Se abrirá el formulario de credenciales **PineconeApi account**

**Completar información de credenciales:**
1. **API Key**: Pega la API key que guardaste de Pinecone
2. **Environment**: Ingresa tu environment de Pinecone (formato: `your-env-xxxxx.svc.pinecone.amazonaws.com`)
3. **Name**: Dale un nombre descriptivo (ej: "Pinecone Production")
4. Haz clic en **Save** para guardar las credenciales

### 6.3 Configurar Operation Mode
En el nodo, configura:
1. **Operation Mode**: Selecciona según tu necesidad:
   - **Get Documents (As Vector Store for Chain/Tool)**: Para recuperar documentos como parte de una cadena
   - **Insert Documents**: Para insertar nuevos documentos
   - **Update Documents**: Para actualizar documentos existentes
   - **Delete Documents**: Para eliminar documentos

### 6.4 Configurar Pinecone Index
1. **Pinecone Index**: Selecciona **From list** 
2. En el dropdown, selecciona el índice que creaste (ej: "n8n-embeddings")
   - Si no aparece, verifica que las credenciales sean correctas

### 6.5 Configurar Options
En la sección **Options**:
1. **Pinecone Namespace**: (Opcional) Ingresa un namespace para organizar tus vectores
   - Ejemplo: "namespacecommerce" para e-commerce
   - Los namespaces ayudan a segmentar datos dentro del mismo índice
2. **Add Option**: Haz clic para agregar opciones adicionales si es necesario

![alt text](assets/pinecone/pinecone-n8n-options.png)

## Paso 8: Integración con OpenAI

### 8.1 Workflow Completo con Embeddings
Para un sistema completo con generación de embeddings:

**Nodos necesarios:**
1. **Webhook/Manual Trigger** - Entrada de datos
2. **OpenAI Node** (Embeddings) - Generar vectores
3. **Pinecone Node** - Almacenar o buscar
4. **Code Node** - Procesamiento adicional

### 8.2 Configuración OpenAI para Embeddings
En el nodo OpenAI:
- **Resource**: Text
- **Operation**: Create Embeddings
- **Model**: text-embedding-ada-002
- **Text**: El texto a convertir en vector

## Resolución de Problemas Comunes

### Error de Dimensiones
- **Problema**: "Vector dimension mismatch"
- **Solución**: Verifica que las dimensiones del vector coincidan con las del índice

### Error de Autenticación
- **Problema**: "Unauthorized" o "Invalid API key"
- **Solución**: 
  - Verifica que la API key sea correcta
  - Asegúrate de que no tenga espacios extra
  - Confirma que el environment sea el correcto

### Error de Índice No Encontrado
- **Problema**: "Index not found"
- **Solución**: 
  - Verifica que el nombre del índice sea exacto (case-sensitive)
  - Asegúrate de que el índice esté en estado "Ready"

### Límites de Plan Gratuito
- **Problema**: "Quota exceeded"
- **Solución**: 
  - Revisa tu uso en el dashboard de Pinecone
  - Considera actualizar a un plan pagado
  - Optimiza el número de vectores almacenados

## Mejores Prácticas

### 9.1 Gestión de Vectores
- **IDs únicos**: Usa identificadores únicos y descriptivos
- **Metadatos útiles**: Incluye información que facilite el filtrado
- **Batch operations**: Procesa múltiples vectores en lotes para mejor rendimiento

### 9.2 Optimización de Búsquedas
- **Top K apropiado**: No solicites más resultados de los necesarios
- **Filtros de metadata**: Usa filtros para reducir el espacio de búsqueda
- **Caché de resultados**: Implementa caché para consultas frecuentes

### 9.3 Monitoreo y Mantenimiento
- **Uso de cuotas**: Monitorea regularmente tu consumo
- **Performance**: Observa los tiempos de respuesta
- **Cleanup**: Elimina vectores obsoletos regularmente

## Casos de Uso Avanzados

### 10.1 Sistema RAG (Retrieval-Augmented Generation)
Combina Pinecone con LLMs para crear sistemas de Q&A:
1. Indexa documentos como vectores en Pinecone
2. Busca documentos relevantes basados en la pregunta
3. Usa los documentos encontrados como contexto para el LLM

### 10.2 Sistema de Recomendaciones
Crea recomendaciones basadas en similitud:
1. Vectoriza preferencias de usuarios
2. Busca usuarios similares en Pinecone
3. Recomienda elementos basados en usuarios similares

### 10.3 Detección de Duplicados
Identifica contenido duplicado o similar:
1. Convierte documentos a vectores
2. Busca vectores con alta similitud
3. Agrupa o elimina duplicados

## Monitoreo y Límites

### 11.1 Plan Gratuito
- **Índices**: 1 índice máximo
- **Vectores**: Hasta 100,000 vectores
- **Queries**: Sin límite específico
- **Almacenamiento**: Incluido en el límite de vectores

### 11.2 Planes Pagados
- **Starter**: $70/mes - Múltiples índices, más vectores
- **Standard**: Facturación por uso
- **Enterprise**: Para necesidades corporativas

### 11.3 Monitoreo de Uso
En el dashboard de Pinecone:
- **Usage**: Vectores almacenados y queries realizadas
- **Performance**: Latencia y throughput
- **Billing**: Costos actuales y proyectados

## Conclusión

Una vez completada esta configuración, tendrás una base de datos vectorial completamente funcional integrada con N8N. Esto te permitirá crear workflows avanzados de IA que incluyan búsqueda semántica, sistemas de recomendación y aplicaciones RAG.

La combinación de Pinecone y N8N abre posibilidades enormes para automatizar procesos que requieren comprensión semántica y búsqueda de similitud, siendo especialmente poderosa cuando se combina con modelos de lenguaje como OpenAI GPT.

## Recursos Adicionales

- [Documentación oficial de Pinecone](https://docs.pinecone.io/)
- [Documentación de N8N para Pinecone](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.vectorstorepinecone/)
- [Pinecone Console](https://app.pinecone.io/)
- [Ejemplos de integración](https://docs.pinecone.io/examples)
- [Guía de embeddings de OpenAI](https://platform.openai.com/docs/guides/embeddings)
- [Tutorial en video - Pinecone + N8N](https://www.youtube.com/results?search_query=pinecone+n8n+tutorial)

## Próximos Pasos

Una vez dominada la configuración básica, considera explorar:
- **Hybrid Search**: Combinando búsqueda vectorial con filtros tradicionales
- **Multi-tenancy**: Separando datos por usuarios o organizaciones
- **Real-time updates**: Actualizando vectores en tiempo real
- **A/B Testing**: Comparando diferentes estrategias de embedding
- **Scaling**: Optimizando para grandes volúmenes de datos