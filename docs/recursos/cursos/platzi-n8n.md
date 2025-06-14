# Curso de N8N - Platzi

## Información del Curso

- **Plataforma**: Platzi
- **Instructor**: Luis Delgado Corrales
- **Duración**: 1 hora de contenido - 8 horas de práctica
- **Nivel**: Principiante
- **Fecha completado**: 13-06-2025

# Descripción del Curso
Aprende a construir agentes inteligentes con n8n, integrando servicios como OpenAI, Telegram, Google Sheets, Pinecone y Notion. Configurá flujos automáticos, RAGs con bases vectoriales y servidores MCP sin escribir una línea de código. Ideal para quienes buscan aplicar IA en soluciones reales con bajo esfuerzo técnico.


## Contenido del Curso

### Módulo 1: Explorando n8n
- Automatización inteligente con N8N
- Diferencias entre N8N Cloud y N8N Community
- Instalación de N8N en servidor propio con Render.com
- Creación de formularios y conexión con Google Sheets en N8N

### Módulo 2: Construye un Agente AI
- Configuración de bot de Telegram para registro automático de gastos
- Transformación de archivos binarios a texto para procesamiento con IA
- Configuración del agente IA para registrar datos en Google Sheets
- Configuración de agente de IA para procesar comprobantes desde Telegram

### Módulo 3: RAG
- RAG: Combinando IA generativa con fuentes confiables
- Configuración de Google Drive en N8N para RAG
- Vectores y embeddings: bases de datos en Pinecone para IA
- Creación de consultas inteligentes a bases de datos vectoriales en N8N

### Módulo 4: MCP
- Conexión de datos con MCP
- Consulta a base de datos PostgreSQL con lenguaje natural
- Configuración de MCP Client con Chat Trigger en N8N
- Configurando MCP Client

## Mis Notas y Aprendizajes

### Conceptos Clave
1. **Diferencia Cloud vs Self-Hosted**
   - Cloud: Más fácil, limitado en plan gratuito
   - Self-Hosted: Control total, requiere setup

2. **Render.com + Supabase**
   - Combinación ideal para principiantes
   - Costo razonable (~$7/mes)
   - Escalabilidad automática

3. **Docker Best Practices**
   - Usar imagen oficial n8nio/n8n
   - Configurar variables de entorno correctamente

### Proyectos Desarrollados
- [x] Setup básico Render + Supabase
- [x] Workflow de notificaciones
- [ ] Integración con APIs externas
- [ ] Sistema de respaldos

## Recursos Adicionales

- [Repositorio del curso](enlace-si-existe)
- [Dockerfile usado](../deployment/render-com/dockerfile-optimizado.md)
- [Variables de entorno](../deployment/render-com/variables-entorno.md)

## Próximos Pasos
1. Implementar MCP Server
2. Crear workflows más complejos
3. Integrar con Claude Desktop
4. Automatizar procesos de trabajo

## Calificación Personal
⭐⭐⭐⭐⭐ (5/5)

**Recomendado para**: Principiantes que quieren setup completo y funcional de N8N.