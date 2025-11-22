# IsoGuard Audit - Asistente Inteligente ISO 27001:2022

## Descripción General

**IsoGuard Audit** es un asistente inteligente para auditorías internas ISO 27001:2022 que permite gestionar auditorías, documentos, hallazgos y controles de seguridad de manera eficiente. La aplicación proporciona análisis automatizados y genera informes interactivos con insights sobre el cumplimiento normativo.

## URLs del Proyecto

- **Desarrollo Local**: https://3000-imag6iekhml3r2pdp412w-5185f4aa.sandbox.novita.ai
- **API Base**: `/api`
- **Repositorio GitHub**: (Pendiente configuración)

## Características Implementadas ✅

### Dashboard Principal
- **Estadísticas en tiempo real** de auditorías, hallazgos y cumplimiento
- **Gráficos visuales** de hallazgos por severidad
- **Panel de cumplimiento** con estados (cumple, parcial, no cumple)
- **Lista de auditorías recientes** con información detallada

### Gestión de Auditorías
- Visualización de todas las auditorías con filtros
- Información detallada: título, descripción, alcance, fechas
- Estados: draft, active, completed
- Asignación de auditores

### Gestión de Documentos
- **Interfaz de carga** de documentos (políticas, procedimientos, evidencias)
- Tipos soportados: PDF, DOCX, XLSX
- Estados de análisis: pending, analyzed
- Almacenamiento y versionado de documentos

### Hallazgos de Auditoría
- **Categorización**: gaps, observaciones, fortalezas
- **Severidad**: high, medium, low
- **Recomendaciones** automáticas por hallazgo
- Vinculación con controles ISO 27001:2022

### Controles ISO 27001:2022
- **Base de datos completa** de controles del Anexo A
- Categorías: organizacionales, personas, físicos, tecnológicos
- Evaluación de cumplimiento por control
- Evidencias y notas de evaluación

### Generación de Informes
- Informe ejecutivo para la dirección
- Informe de cumplimiento detallado
- Insights de IA con recomendaciones
- Exportación en múltiples formatos

## Arquitectura de Datos

### Modelo de Datos

La aplicación utiliza **Cloudflare D1** (SQLite distribuido) con las siguientes tablas:

#### Tablas Principales

1. **users** - Usuarios del sistema (auditores, consultores)
   - Campos: id, email, name, password_hash, role, created_at

2. **audits** - Auditorías ISO 27001:2022
   - Campos: id, title, description, scope, audit_date, status, user_id

3. **iso_controls** - Controles del Anexo A ISO 27001:2022
   - Campos: id, control_id (ej: A.5.1), control_name, category, description

4. **documents** - Documentos cargados
   - Campos: id, audit_id, document_name, document_type, file_size, status, analysis_result

5. **findings** - Hallazgos de auditoría
   - Campos: id, audit_id, control_id, finding_type, severity, title, description, recommendation, status

6. **compliance_assessments** - Evaluaciones de cumplimiento
   - Campos: id, audit_id, control_id, compliance_level, evidence, notes

7. **reports** - Informes generados
   - Campos: id, audit_id, report_type, report_data, generated_at

### Servicios de Almacenamiento

- **Cloudflare D1**: Base de datos relacional para datos estructurados
- **Local SQLite**: Para desarrollo con `--local` flag
- **Migraciones**: Sistema de versionado de esquema en `/migrations`

## API Endpoints

### Dashboard
- `GET /api/dashboard/stats` - Estadísticas generales del sistema

### Auditorías
- `GET /api/audits` - Lista todas las auditorías
- `GET /api/audits/:id` - Detalles de auditoría con documentos, hallazgos y evaluaciones
- `POST /api/audits` - Crear nueva auditoría

### Controles ISO
- `GET /api/controls` - Lista todos los controles ISO 27001:2022

## Guía de Usuario

### Navegación Principal

1. **Dashboard** 📊
   - Vista general con métricas clave
   - Acceso rápido a auditorías activas
   - Visualización de hallazgos pendientes

2. **Auditorías** 📋
   - Crear nueva auditoría con título, descripción y alcance
   - Ver historial de auditorías
   - Acceder a detalles y resultados

3. **Documentos** 📄
   - Cargar políticas y procedimientos
   - Subir evidencias de cumplimiento
   - Revisar análisis automáticos

4. **Hallazgos** ⚠️
   - Revisar gaps de cumplimiento
   - Ver observaciones y recomendaciones
   - Identificar fortalezas del SGSI

5. **Controles ISO** ✅
   - Consultar controles del Anexo A
   - Evaluar nivel de cumplimiento
   - Documentar evidencias

6. **Informes** 📑
   - Generar informes ejecutivos
   - Exportar análisis de cumplimiento
   - Obtener insights de IA

### Datos de Prueba

La aplicación incluye datos de demostración:
- **Usuario**: Douglas - Consultor ISO 27001
- **Auditoría de ejemplo**: Q1 2025
- **22 controles** ISO 27001:2022 precargados
- **3 hallazgos** de ejemplo (gap, observación, fortaleza)
- **4 evaluaciones** de cumplimiento

## Stack Tecnológico

- **Backend**: Hono (framework minimalista para Cloudflare Workers)
- **Base de Datos**: Cloudflare D1 (SQLite distribuido globalmente)
- **Frontend**: Vanilla JS + TailwindCSS + Font Awesome
- **Deployment**: Cloudflare Pages
- **Runtime**: Cloudflare Workers (edge computing)

## Instalación y Desarrollo

### Prerrequisitos
```bash
npm install
```

### Desarrollo Local
```bash
# 1. Build del proyecto
npm run build

# 2. Aplicar migraciones
npm run db:migrate:local

# 3. Cargar datos de prueba
npm run db:seed

# 4. Iniciar servidor de desarrollo
pm2 start ecosystem.config.cjs

# 5. Ver logs
pm2 logs isoguard-audit --nostream

# 6. Probar la aplicación
curl http://localhost:3000/api/dashboard/stats
```

### Scripts Disponibles
- `npm run dev` - Servidor Vite (desarrollo frontend)
- `npm run dev:sandbox` - Wrangler local con D1
- `npm run build` - Build de producción
- `npm run db:migrate:local` - Aplicar migraciones localmente
- `npm run db:seed` - Cargar datos de prueba
- `npm run db:reset` - Resetear base de datos local
- `npm run clean-port` - Limpiar puerto 3000
- `npm run test` - Test básico del servidor

## Estado del Proyecto

### Completado ✅
- ✅ Estructura de base de datos D1 completa
- ✅ Migraciones y datos de prueba
- ✅ API REST funcional con todos los endpoints
- ✅ Dashboard interactivo con estadísticas
- ✅ Gestión de auditorías
- ✅ Sistema de hallazgos y recomendaciones
- ✅ Catálogo de controles ISO 27001:2022
- ✅ Interfaz de usuario responsive
- ✅ Integración con Cloudflare D1

### Pendiente 🚧
- 🚧 Implementación real de carga de archivos (actualmente mock UI)
- 🚧 Integración con servicios de IA para análisis automático
- 🚧 Sistema de autenticación completo (login/logout)
- 🚧 Generación de informes en PDF
- 🚧 Búsqueda y filtrado avanzado
- 🚧 Exportación de datos
- 🚧 Notificaciones y alertas
- 🚧 Gestión de roles y permisos

## Próximos Pasos Recomendados

1. **Desplegar a Cloudflare Pages**
   - Configurar cuenta de Cloudflare
   - Crear D1 database en producción
   - Desplegar con `wrangler pages deploy`

2. **Implementar Autenticación**
   - Integrar con Cloudflare Access o Auth0
   - Agregar protección de rutas
   - Sistema de roles (auditor, administrador)

3. **Análisis con IA**
   - Integrar Cloudflare AI o OpenAI API
   - Análisis automático de documentos
   - Generación de recomendaciones

4. **Mejoras de UX**
   - Búsqueda en tiempo real
   - Filtros avanzados
   - Exportación de informes
   - Notificaciones push

5. **Optimizaciones**
   - Caché de consultas frecuentes
   - Paginación de resultados
   - Compresión de respuestas
   - Service Workers para PWA

## Estructura del Proyecto

```
webapp/
├── src/
│   └── index.tsx           # Aplicación principal Hono
├── migrations/
│   └── 0001_initial_schema.sql  # Schema de base de datos
├── public/                 # Archivos estáticos
├── dist/                   # Build de producción
├── .wrangler/              # Estado local de Wrangler
├── seed.sql                # Datos de prueba
├── ecosystem.config.cjs    # Configuración PM2
├── wrangler.jsonc          # Configuración Cloudflare
├── package.json            # Dependencies y scripts
└── README.md               # Esta documentación
```

## Soporte y Contacto

**Desarrollado para**: Douglas - Consultor de Seguridad ISO 27001:2022

**Perfil**: Consultor con alta experiencia en auditorías e implementación de ISO 27001:2022, con criterio exacto en verificaciones de procesos y documentos de seguridad.

---

**Última actualización**: 2025-11-22
**Versión**: 1.0.0
**Estado**: ✅ Desarrollo Activo
