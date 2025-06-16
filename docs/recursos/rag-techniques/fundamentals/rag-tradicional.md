# RAG Tradicional - Fundamentos

## 🎯 Introducción

RAG (Retrieval-Augmented Generation) Tradicional es la base de todos los sistemas de recuperación de información moderna. Antes de explorar técnicas avanzadas como Late Chunking o Contextual Retrieval, es fundamental entender cómo funciona el RAG tradicional, sus fortalezas y sus limitaciones.

Esta guía te llevará paso a paso a través de todo el proceso, desde la importación de documentos hasta la generación de respuestas, con ejemplos prácticos para implementar en N8N.


---

## 🔍 ¿Qué es RAG Tradicional?

### Definición

RAG Tradicional es un sistema que combina **recuperación de información** con **generación de texto** para crear respuestas precisas y contextualizadas basadas en una base de conocimiento específica.

### El Problema que Resuelve

Los modelos de lenguaje grandes (LLMs) tienen limitaciones:
- **Conocimiento estático**: Entrenados hasta una fecha específica
- **Alucinaciones**: Pueden inventar información
- **Falta de especialización**: No conocen datos específicos de tu empresa/dominio
- **Sin fuentes**: No pueden citar de dónde viene la información

RAG resuelve estos problemas **conectando el LLM con tu base de conocimiento**.

---

## 🏗️ Arquitectura del RAG Tradicional

### Visión General del Proceso

```
📄 DOCUMENTOS → 🔀 CHUNKING → 🧠 EMBEDDING → 💾 VECTOR DB → 🔍 QUERY → 📝 RESPUESTA
```

![alt text](../assets/fundamentals/tradicional-rag.png)


### Los 6 Pasos Fundamentales

1. **Importación de Datos** 📥
2. **Fragmentación (Chunking)** ✂️
3. **Generación de Embeddings** 🧠
4. **Almacenamiento Vectorial** 💾
5. **Recuperación (Retrieval)** 🔍
6. **Generación de Respuesta** 📝

---

## 📥 Paso 1: Importación de Datos

### Tipos de Documentos Soportados

| Tipo | Formato | Casos de Uso | Complejidad |
|------|---------|--------------|-------------|
| **PDF** | .pdf | Manuales, reportes, documentos oficiales | Media |
| **Texto** | .txt, .md | Documentación, artículos | Baja |
| **Word** | .docx | Políticas, procedimientos | Media |
| **Web** | HTML | Páginas web, wikis | Alta |
| **Datos estructurados** | .csv, .json | Bases de datos, catálogos | Media |



---

## ✂️ Paso 2: Fragmentación (Chunking)

### ¿Por qué Fragmentar?

Los modelos de embedding tienen **limitaciones de tokens**:
- La mayoría acepta **máximo 512 tokens** (~400 palabras)
- Documentos largos deben dividirse en fragmentos manejables
- Cada fragmento debe contener **información coherente y completa**

### Estrategias de Chunking
1. Fixed-Size Chunking (Más Común)
2. Semantic Chunking (Recomendado)
3. Document Structure Chunking

---

## 🧠 Paso 3: Generación de Embeddings

### ¿Qué son los Embeddings?

Los embeddings son **representaciones numéricas** de texto que capturan su significado semántico en un espacio vectorial de alta dimensión.

```
"El gato está en la mesa" → [0.1, -0.3, 0.8, 0.2, -0.1, ...] (1536 dimensiones)
```

### Modelos de Embedding Populares

| Modelo | Dimensiones | Contexto | Precio | Casos de Uso |
|--------|-------------|----------|--------|--------------|
| **OpenAI text-embedding-3-small** | 1536 | 8191 tokens | $0.02/1M | General, económico |
| **OpenAI text-embedding-3-large** | 3072 | 8191 tokens | $0.13/1M | Alta precisión |
| **Jina AI v2** | 768 | 8192 tokens | $0.02/1M | Multilingüe |
| **Cohere Embed v3** | 1024 | 512 tokens | $0.10/1M | Clasificación |

---

## 💾 Paso 4: Almacenamiento Vectorial

### ¿Qué es una Base de Datos Vectorial?

Una base de datos especializada en almacenar y consultar vectores de alta dimensión de manera eficiente.

### Bases de Datos Vectoriales Populares

| Base de Datos | Tipo | Escalabilidad | Facilidad | Precio |
|---------------|------|---------------|-----------|--------|
| **Pinecone** | Cloud | Alta | Muy fácil | Desde $70/mes |
| **Qdrant** | Self-hosted/Cloud | Alta | Fácil | Desde $25/mes |
| **Weaviate** | Self-hosted/Cloud | Media | Media | Gratis/Pago |
| **ChromaDB** | Local/Self-hosted | Baja | Muy fácil | Gratis |
| **FAISS** | Local | Media | Difícil | Gratis |



---

## ⚠️ Limitaciones del RAG Tradicional

### Problemas Principales

#### 1. **Pérdida de Contexto**
```
Problema: Chunks aislados pierden el contexto del documento completo

Ejemplo:
Chunk 1: "La empresa reportó crecimiento."
Chunk 2: "El crecimiento fue del 15%."

Consulta: "¿Cuánto creció la empresa?"
Resultado: Solo se recupera Chunk 2, sin contexto de qué empresa.
```

#### 2. **Fragmentación Subóptima**
```
Problema: División arbitraria puede separar información relacionada

Documento: "El nuevo producto A cuesta $100. Sus características incluyen..."
Chunking: Separa precio de características
Resultado: Respuestas incompletas sobre el producto
```

#### 3. **Ranking Impreciso**
```
Problema: Similitud semántica no siempre = relevancia real

Consulta: "¿Cómo instalar el software?"
Recuperado: Chunks sobre "desinstalar" (semánticamente similar)
Resultado: Información incorrecta o confusa
```

### Casos Donde Falla RAG Tradicional

| Escenario | Problema | Ejemplo |
|-----------|----------|---------|
| **Información distribuida** | Datos en múltiples chunks | Calcular totales, comparaciones |
| **Dependencias temporales** | Orden cronológico importante | Procesos paso a paso |
| **Referencias cruzadas** | Menciones a otras secciones | "Como se mencionó anteriormente" |
| **Contexto implícito** | Información asumida | Pronouns, acrónimos sin definir |


---



## 🎯 Conclusiones

### Fortalezas del RAG Tradicional

✅ **Simplicidad**: Fácil de entender e implementar
✅ **Eficiencia**: Procesamiento rápido y económico
✅ **Escalabilidad**: Funciona bien hasta cierto punto
✅ **Flexibilidad**: Compatible con múltiples fuentes de datos
✅ **Madurez**: Herramientas y librerías bien establecidas

### Cuándo Usar RAG Tradicional

- **Documentos simples** con estructura clara
- **Presupuesto limitado** para implementación
- **Prototipado rápido** de sistemas RAG
- **Casos de uso básicos** de Q&A
- **Equipos con experiencia limitada** en IA

### Cuándo Considerar Alternativas

- Documentos con **información interrelacionada**
- Necesidad de **alta precisión** crítica
- **Consultas complejas** que requieren múltiples fuentes
- **Contexto distribuido** a través del documento
- **Presupuesto disponible** para técnicas avanzadas

### El Camino Hacia Técnicas Avanzadas

RAG Tradicional es el **punto de partida perfecto** para:
1. Entender los fundamentos
2. Identificar limitaciones específicas de tu caso de uso
3. Evaluar si necesitas técnicas más avanzadas
4. Establecer métricas de rendimiento base

Una vez que domines RAG Tradicional y identifiques sus limitaciones en tu contexto específico, estarás listo para explorar técnicas avanzadas como Late Chunking y Contextual Retrieval.

---

## 📚 Recursos Adicionales

### Documentación Oficial
- [OpenAI Embeddings API](https://platform.openai.com/docs/guides/embeddings)
- [Qdrant Documentation](https://qdrant.tech/documentation/)
- [N8N RAG Workflows](https://docs.n8n.io/integrations/)

### Herramientas Recomendadas
- **Evaluación**: LangSmith, Weights & Biases
- **Monitoring**: LangFuse, Phoenix
- **Testing**: RAGAS, TruLens