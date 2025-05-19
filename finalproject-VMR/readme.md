# claude-3.7-sonnet
# Proyecto: DevCompass

## Índice

0. [Ficha del proyecto](#0-ficha-del-proyecto)
1. [Descripción general del producto](#1-descripción-general-del-producto)
2. [Arquitectura del sistema](#2-arquitectura-del-sistema)
3. [Modelo de datos](#3-modelo-de-datos)
4. [Especificación de la API](#4-especificación-de-la-api)
5. [Historias de usuario](#5-historias-de-usuario)
6. [Tickets de trabajo](#6-tickets-de-trabajo)
7. [Pull requests](#7-pull-requests)

---

## 0. Ficha del proyecto

### **0.1. Tu nombre completo:**
Vandré Miguel Ramos

### **0.2. Nombre del proyecto:**
DevCompass

### **0.3. Descripción breve del proyecto:**
DevCompass es una plataforma innovadora que alinea el desarrollo profesional de especialistas en tecnología con la cultura y valores de su empresa. El sistema traduce la cultura organizacional en un mapa de desarrollo personalizado, permitiendo a los profesionales IT navegar su carrera desde Junior hasta Tech Leader de manera eficiente y culturalmente alineada.

### **0.4. URL del proyecto:**
Work in Progress

### 0.5. URL o archivo comprimido del repositorio
Work in Progress

---

## 1. Descripción general del producto

### **1.1. Objetivo:**

DevCompass tiene como objetivo principal facilitar el desarrollo profesional de especialistas en tecnología, alineando sus competencias técnicas y objetivos de carrera con la cultura y valores de su organización.

El producto aporta valor a dos grupos principales:

**Para desarrolladores:** Proporciona un camino claro de progresión profesional personalizado que refleja no solo las competencias técnicas necesarias, sino también los comportamientos y valores que su empresa específica valora, aumentando así sus posibilidades de crecimiento y satisfacción profesional.

**Para organizaciones:** Ofrece una herramienta para asegurar que el desarrollo de su talento técnico está alineado con su cultura organizacional única, facilitando la retención, el engagement y la coherencia cultural a través de los diferentes niveles de la jerarquía técnica.

El producto soluciona la desconexión habitual entre el desarrollo técnico y la cultura organizacional, que suele resultar en planes de carrera genéricos que no reflejan los valores específicos de cada empresa.

### **1.2. Características y funcionalidades principales:**

1. **Análisis cultural mediante NLP:** Utiliza procesamiento de lenguaje natural para analizar documentos de cultura organizacional y extraer automáticamente valores corporativos, comportamientos esperados y expectativas por nivel jerárquico.

2. **Autodiagnóstico técnico contextualizado:** Sistema de evaluación para desarrolladores que mide tanto competencias técnicas como alineación con comportamientos valorados culturalmente.

3. **Mapa de carrera personalizado:** Visualización del camino de desarrollo desde Junior hasta Tech Leader, adaptado a los valores y expectativas específicas de cada organización.

4. **Motor de alineación cultural-técnica:** Algoritmo que analiza el grado de coincidencia entre el perfil del desarrollador y las expectativas culturales de la organización, identificando brechas y fortalezas.

5. **Plan de desarrollo accionable:** Generación de roadmaps personalizados con objetivos priorizados según la alineación cultural y técnica, incluyendo recomendación de recursos relevantes.

6. **Seguimiento de evolución:** Sistema para registrar evidencias de progreso, actualizar métricas de desarrollo y generar reportes periódicos compartibles con líderes y mentores.

7. **Autenticación con Google:** Integración con Google para un inicio de sesión simplificado y detección automática de dominio corporativo para asociación con perfil cultural.

### **1.3. Diseño y experiencia de usuario:**

Work in Progress

### **1.4. Instrucciones de instalación:**

Work in Progress

---

## 2. Arquitectura del Sistema

### **2.1. Diagrama de arquitectura:**

DevCompass se construirá como una aplicación web moderna basada en microservicios, con clara separación entre frontend y backend, siguiendo principios de desarrollo ágil y utilizando tecnologías cloud-native.

```mermaid
flowchart TD
    Client[Cliente Web] --> Gateway[API Gateway]
    
    subgraph "Servicios Core"
        Gateway --> AuthService[Authentication Service]
        Gateway --> CultureService[Culture Analysis Service]
        Gateway --> ProfileService[Developer Profile Service]
        Gateway --> CareerService[Career Map Service]
        Gateway --> AlignmentService[Alignment Engine]
        Gateway --> DevPlanService[Development Plan Service]
    end
    
    subgraph "Servicios NLP"
        CultureService <--> NLPProcessor[NLP Processor]
        NLPProcessor <--> GPTService[OpenAI GPT Service]
        NLPProcessor <--> RulesEngine[Rules Engine]
    end
    
    subgraph "Almacenamiento"
        AuthService --> Redis[(Redis)]
        AuthService --> PostgreSQL[(PostgreSQL)]
        
        CultureService --> MongoDB[(MongoDB)]
        CultureService --> PostgreSQL
        
        ProfileService --> PostgreSQL
        CareerService --> PostgreSQL
        AlignmentService --> PostgreSQL
        AlignmentService --> MongoDB
        DevPlanService --> PostgreSQL
    end
```

Para el MVP, se utilizará una versión simplificada de esta arquitectura:

```mermaid
flowchart TD
    User[Usuario] --> Frontend[Frontend React]
    Frontend --> Backend[Backend Express.js]
    Backend --> DB[(PostgreSQL)]
    Backend --> OpenAI[OpenAI API]
    
    subgraph "Entorno de Desarrollo"
        Docker[Docker Compose] --> DevDB[(PostgreSQL Dev)]
        Docker --> DevBackend[Express Dev]
        Docker --> DevFrontend[React Dev]
    end
    
    subgraph "Entorno de Producción"
        AppHosting[Heroku/Vercel] --> ProdBackend[Express Prod]
        AppHosting --> ProdFrontend[React Prod Build]
        DBHosting[DB Hosting] --> ProdDB[(PostgreSQL Prod)]
        ProdBackend --> ProdDB
        ProdBackend --> OpenAI
    end
```

### **2.2. Descripción de componentes principales:**

**Frontend:**
- **Framework**: React con TypeScript
- **Estado**: Redux Toolkit o Context API
- **UI**: Material UI para componentes base
- **Visualización**: D3.js/Recharts para gráficos
- **Routing**: React Router

**Backend:**
- **Framework**: Node.js con Express.js
- **Autenticación**: Integración con Google OAuth
- **Microservicios**: Servicios independientes por dominio funcional
- **Message Queue**: Para comunicación asíncrona entre servicios
- **NLP**: Servicio especializado para procesamiento de lenguaje natural

**Datos:**
- **PostgreSQL**: Para datos relacionales y transaccionales
- **MongoDB**: Para documentos semiestructurados (perfiles culturales, evidencias)
- **Redis**: Caché, sesiones y datos de alta frecuencia de acceso

**DevOps:**
- **Contenedores**: Docker
- **Orquestación**: Kubernetes
- **CI/CD**: Pipeline automatizado
- **Monitoreo**: Prometheus + Grafana

**Componentes Principales del Servicio NLP:**
1. **Preprocessor**: Limpieza y preparación de documentos en diversos formatos
2. **OpenAI GPT Client**: Comunicación optimizada con la API de OpenAI
3. **Result Parser**: Validación y normalización de respuestas JSON
4. **Rules Engine**: Procesamiento post-NLP y aplicación de reglas de negocio 
5. **Validation Service**: Interfaz para revisión y ajuste humano de resultados

### **2.3. Descripción de alto nivel del proyecto y estructura de ficheros**

Work in Progress

### **2.4. Infraestructura y despliegue**

Para el MVP, se utilizará una infraestructura simplificada enfocada en rápido desarrollo y validación:

**Entorno de desarrollo:**
- Docker Compose con contenedores para:
  - PostgreSQL (única base de datos para MVP)
  - Backend Express.js
  - Frontend React

**Configuración local con Docker:**
```yaml
# docker-compose.yml para entorno de desarrollo local
version: '3'

services:
  postgres:
    image: postgres:14
    environment:
      POSTGRES_USER: devcompass
      POSTGRES_PASSWORD: devcompass
      POSTGRES_DB: devcompass
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
  
  backend:
    build:
      context: ./backend
    volumes:
      - ./backend:/app
      - /app/node_modules
    ports:
      - "3001:3001"
    environment:
      - NODE_ENV=development
      - DATABASE_URL=postgres://devcompass:devcompass@postgres:5432/devcompass
      - PORT=3001
      - JWT_SECRET=development_secret
      - GOOGLE_CLIENT_ID=${GOOGLE_CLIENT_ID}
      - GOOGLE_CLIENT_SECRET=${GOOGLE_CLIENT_SECRET}
      - OPENAI_API_KEY=${OPENAI_API_KEY}
    depends_on:
      - postgres
  
  frontend:
    build:
      context: ./frontend
    volumes:
      - ./frontend:/app
      - /app/node_modules
    ports:
      - "3000:3000"
    environment:
      - REACT_APP_API_URL=http://localhost:3001/api
    depends_on:
      - backend

volumes:
  postgres_data:
```

**Entorno de producción (MVP):**
- Frontend: Vercel/Netlify/Heroku
- Backend: Heroku/Railway/Render
- Base de datos: Servicio gestionado (Heroku Postgres)

**Stack tecnológico simplificado para MVP:**
1. **Frontend**: React + TypeScript, Material UI, Recharts
2. **Backend**: Node.js + Express.js, Passport.js, Knex.js/Sequelize
3. **Base de datos**: PostgreSQL único
4. **Servicios externos**: OpenAI API, Google OAuth

### **2.5. Seguridad**

El sistema implementará las siguientes medidas de seguridad para el MVP:

1. **Autenticación**:
   - OAuth 2.0 con Google
   - JWT para gestión de sesiones
   - Middleware de autorización por rol

2. **Protección de datos**:
   - Cifrado en tránsito (HTTPS)
   - Validación de entradas
   - Sanitización de datos

3. **Seguridad básica**:
   - Headers de seguridad (Helmet)
   - CORS configurado
   - Manejo seguro de errores

**Flujo de autenticación OAuth:**
```mermaid
sequenceDiagram
    actor User
    participant App as DevCompass App
    participant API as API Express
    participant Google as Google OAuth
    
    User->>App: Clic en "Login with Google"
    App->>Google: Redirección a OAuth
    Google->>User: Pantalla de consentimiento
    User->>Google: Autoriza acceso
    Google->>App: Redirección a callback con código
    App->>API: POST /auth/google/callback con código
    API->>Google: Intercambia código por tokens
    Google->>API: Devuelve tokens
    API->>Google: Solicita info de usuario
    Google->>API: Devuelve perfil
    API->>API: Crea/actualiza usuario
    API->>API: Genera JWT
    API->>App: Devuelve JWT y datos
    App->>App: Almacena JWT
    App->>API: Solicitudes autenticadas
```

### **2.6. Tests**

Work in Progress

---

## 3. Modelo de Datos

### **3.1. Diagrama del modelo de datos:**

```mermaid
erDiagram
    Organization ||--o{ User : "has"
    Organization ||--|| CultureProfile : "has"
    User ||--o| DeveloperProfile : "has"
    User }|--|| Role : "has"
    CultureProfile ||--o{ CultureValue : "contains"
    CultureProfile ||--o{ ExpectedBehavior : "defines"
    CareerPath ||--o{ CareerLevel : "contains"
    CareerLevel ||--o{ RequiredSkill : "requires"
    DeveloperProfile ||--o{ SkillAssessment : "contains"
    DeveloperProfile ||--|| CareerPosition : "has"
    CareerPosition }|--|| CareerLevel : "references"
    DeveloperProfile ||--o{ DevelopmentGoal : "has"
    DevelopmentGoal ||--o{ LearningResource : "uses"
    DevelopmentGoal ||--o{ ProgressEvidence : "tracks"
    RequiredSkill }o--|| Skill : "references"
    SkillAssessment }o--|| Skill : "references"
    ExpectedBehavior }o--|| CareerLevel : "applies_to"
```

### **3.2. Descripción de entidades principales:**

#### Organization
```json
{
  "id": "string (UUID)",
  "name": "string",
  "domain": "string (dominio de correo)",
  "created_at": "timestamp",
  "active": "boolean"
}
```

#### CultureProfile
```json
{
  "id": "string (UUID)",
  "organization_id": "string (UUID, FK)",
  "raw_documents": "jsonb (documentos originales)",
  "last_processed": "timestamp",
  "processing_confidence": "float",
  "created_at": "timestamp",
  "updated_at": "timestamp"
}
```

#### User
```json
{
  "id": "string (UUID)",
  "email": "string",
  "name": "string",
  "google_id": "string",
  "profile_picture": "string (URL)",
  "last_login": "timestamp",
  "organization_id": "string (UUID, FK)",
  "role_id": "string (UUID, FK)"
}
```

#### DeveloperProfile
```json
{
  "id": "string (UUID)",
  "user_id": "string (UUID, FK)",
  "last_assessment": "timestamp",
  "career_goals": "json",
  "created_at": "timestamp",
  "updated_at": "timestamp"
}
```

#### CareerLevel
```json
{
  "id": "string (UUID)",
  "career_path_id": "string (UUID, FK)",
  "name": "string (ej: Junior, Mid, Senior)",
  "description": "string",
  "level_order": "integer",
  "progression_criteria": "json"
}
```

### **3.3. Estrategia de Persistencia**

- **PostgreSQL**: Almacenamiento principal para datos relacionales y transaccionales
- **MongoDB**: Para documentos semiestructurados (perfiles culturales, evidencias)
- **Redis**: Caché, sesiones y datos de alta frecuencia de acceso

---

## 4. Especificación de la API

### **4.1. Estructura de API Simplificada**

```mermaid
flowchart TD
    Client[Cliente Web] --> API[API Express.js]
    
    API --> AuthRoutes[/auth]
    API --> OrgRoutes[/organizations]
    API --> CultureRoutes[/culture]
    API --> ProfileRoutes[/profiles]
    API --> CareerRoutes[/career]
    API --> AlignmentRoutes[/alignment]
    API --> PlanRoutes[/development-plans]
```

### **4.2. Endpoints Principales**

#### Autenticación
- `GET /api/auth/google`: Inicio del flujo OAuth
- `GET /api/auth/google/callback`: Callback de Google
- `POST /api/auth/refresh-token`: Renovación de tokens
- `POST /api/auth/logout`: Cierre de sesión

#### Cultura
- `GET /api/culture/:orgId`: Obtiene perfil cultural
- `POST /api/culture/:orgId/documents`: Sube documentos
- `POST /api/culture/:orgId/process`: Inicia procesamiento
- `GET /api/culture/:orgId/values`: Obtiene valores
- `GET /api/culture/:orgId/behaviors`: Obtiene comportamientos
- `PUT /api/culture/:orgId`: Actualiza perfil cultural

#### Perfiles
- `GET /api/profiles/:userId`: Obtiene perfil de desarrollador
- `POST /api/profiles`: Crea nuevo perfil
- `PUT /api/profiles/:userId`: Actualiza perfil
- `GET /api/profiles/:userId/skills`: Lista evaluaciones de habilidades
- `PUT /api/profiles/:userId/skills/:skillId`: Actualiza evaluación

#### Alineación y Plan
- `GET /api/alignment/:userId`: Obtiene análisis de alineación
- `POST /api/alignment/:userId/calculate`: Calcula alineación
- `GET /api/alignment/:userId/gaps`: Obtiene brechas prioritarias
- `GET /api/development-plans/:userId`: Obtiene plan actual
- `POST /api/development-plans/:userId/generate`: Genera plan

### **4.3. Implementación API Simple (Ejemplo)**

```javascript
// app.js - Aplicación Express simplificada para MVP
const express = require('express');
const cors = require('cors');
const morgan = require('morgan');
const helmet = require('helmet');
const passport = require('passport');

// Importar rutas
const authRoutes = require('./routes/auth');
const organizationRoutes = require('./routes/organizations');
const cultureRoutes = require('./routes/culture');
const profileRoutes = require('./routes/profiles');
const careerRoutes = require('./routes/career');
const alignmentRoutes = require('./routes/alignment');
const planRoutes = require('./routes/development-plans');

const app = express();

// Middleware
app.use(helmet());
app.use(cors());
app.use(morgan('dev'));
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(passport.initialize());

// Rutas de API
app.use('/api/auth', authRoutes);
app.use('/api/organizations', organizationRoutes);
app.use('/api/culture', cultureRoutes);
app.use('/api/profiles', profileRoutes);
app.use('/api/career', careerRoutes);
app.use('/api/alignment', alignmentRoutes);
app.use('/api/development-plans', planRoutes);

// Middleware para errores
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({
    error: true,
    message: process.env.NODE_ENV === 'production' 
      ? 'Error interno del servidor' 
      : err.message
  });
});

module.exports = app;);
app.use('/api/culture', cultureRoutes);
app.use('/api/profiles', profileRoutes);
app.use('/api/career', careerRoutes);
app.use('/api/alignment', alignmentRoutes);
app.use('/api/development-plans', planRoutes);

// Middleware para errores
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({
    error: true,
    message: process.env.NODE_ENV === 'production' 
      ? 'Error interno del servidor' 
      : err.message
  });
});

module.exports = app;
```

### **4.4. Ejemplos de Prompts GPT para API NLP**

#### Prompt para Extracción de Valores

```
Analiza el siguiente texto de cultura organizacional y extrae los 5-10 valores fundamentales de la empresa. Para cada valor, proporciona:
1. Nombre del valor (una palabra o frase corta)
2. Descripción breve que contextualiza el valor
3. Nivel de importancia percibida (del 1-10)
4. Términos o conceptos relacionados

Responde ÚNICAMENTE en formato JSON estructurado siguiendo exactamente este esquema:
{
  "valores": [
    {
      "nombre": "nombre del valor",
      "descripcion": "descripción breve",
      "importancia": número del 1-10,
      "terminosRelacionados": ["término1", "término2"]
    }
  ]
}

Texto a analizar:
[TEXTO CULTURAL DE LA EMPRESA]
```

#### Prompt para Comportamientos Esperados

```
Analiza el siguiente texto de cultura organizacional y extrae los comportamientos específicos que la empresa espera de sus empleados. Para cada comportamiento:
1. Descripción clara del comportamiento
2. Valores asociados a este comportamiento
3. Niveles jerárquicos a los que aplica (Junior, Mid, Senior, Lead)

Responde ÚNICAMENTE en formato JSON estructurado siguiendo exactamente este esquema:
{
  "comportamientos": [
    {
      "descripcion": "descripción del comportamiento",
      "valoresAsociados": ["valor1", "valor2"],
      "nivelesAplicables": ["Junior", "Mid", "Senior", "Lead"]
    }
  ]
}

Texto a analizar:
[TEXTO CULTURAL DE LA EMPRESA]
```

### **4.5. Flujo de Procesamiento NLP**

```mermaid
sequenceDiagram
    actor Admin as Administrador
    participant UI as Frontend Admin
    participant API as API Gateway
    participant NLP as NLP Service
    participant GPT as OpenAI GPT
    participant DB as MongoDB
    
    Admin->>UI: Sube documentos culturales
    UI->>API: POST /api/culture/:orgId/documents
    API->>NLP: Procesar documentos
    NLP->>NLP: Preprocesar texto
    
    loop Para cada segmento de texto
        NLP->>GPT: Solicitud con prompt de valores
        GPT-->>NLP: Respuesta JSON (valores)
        NLP->>GPT: Solicitud con prompt de comportamientos
        GPT-->>NLP: Respuesta JSON (comportamientos)
    end
    
    NLP->>NLP: Aplicar reglas de negocio
    NLP->>NLP: Consolidar resultados
    NLP->>DB: Almacenar resultados preliminares
    NLP-->>API: Devolver análisis completado
    API-->>UI: Mostrar resultados para validación
    
    Admin->>UI: Valida y ajusta resultados
    UI->>API: PUT /api/culture/:orgId
    API->>NLP: Procesar ajustes
    NLP->>DB: Actualizar perfil cultural
    NLP-->>API: Confirmar actualización
    API-->>UI: Mostrar perfil finalizado
```

---

## 5. Historias de usuario

A continuación se presentan algunas historias de usuario clave para el MVP:

### Módulo 1: Captura y Análisis Cultural

**Historia 1: Ingreso de información cultural empresarial**
**Como** representante de RRHH/Liderazgo
**Quiero** ingresar información sobre la cultura organizacional
**Para** crear un perfil cultural que guíe el desarrollo de los profesionales IT

**Criterios de aceptación**:
- Puedo acceder al módulo de cultura empresarial
- Puedo completar campos estructurados (valores, misión, visión)
- Puedo proporcionar texto libre describiendo comportamientos valorados
- Puedo cargar documentos relevantes (código de conducta, manuales)
- El sistema confirma la recepción de la información

**Historia 2: Visualización del ADN cultural**
**Como** administrador/desarrollador
**Quiero** visualizar el perfil cultural de la organización
**Para** comprender los valores y comportamientos esperados

**Criterios de aceptación**:
- Puedo acceder al dashboard cultural
- Puedo ver representación gráfica de valores centrales
- Puedo explorar comportamientos esperados por nivel
- Puedo acceder a recomendaciones de alineación cultural

### Módulo 2: Evaluación Técnica Contextualizada

**Historia 3: Autodiagnóstico inicial del desarrollador**
**Como** desarrollador
**Quiero** realizar una autoevaluación de mis competencias
**Para** establecer mi perfil técnico actual

**Criterios de aceptación**:
- Puedo acceder al módulo de autodiagnóstico
- Puedo completar evaluación técnica basada en mi nivel
- Puedo evaluar mis habilidades blandas
- Puedo indicar mis objetivos de carrera
- Puedo guardar parcialmente y continuar después
- Recibo un resumen visual de mi perfil al finalizar

**Historia 4: Benchmark contra expectativas organizacionales**
**Como** desarrollador
**Quiero** comparar mi perfil con las expectativas para mi nivel
**Para** identificar brechas de desarrollo

**Criterios de aceptación**:
- El sistema muestra indicadores de alineación por categoría
- Puedo identificar claramente mis fortalezas
- Puedo ver las brechas más importantes
- Recibo un informe personalizado de benchmark

### Módulo 3: Plan de Desarrollo Accionable

**Historia 5: Generación del roadmap personalizado**
**Como** desarrollador
**Quiero** recibir un plan de desarrollo personalizado
**Para** progresar en mi carrera de manera alineada con la cultura

**Criterios de aceptación**:
- El sistema traduce brechas en objetivos de desarrollo
- Los objetivos están secuenciados según prioridad
- Se establecen tiempos estimados para cada objetivo
- Puedo visualizar el roadmap completo

**Historia 6: Registro de evidencias de desarrollo**
**Como** desarrollador
**Quiero** registrar evidencias de mi progreso
**Para** documentar mi evolución profesional

**Criterios de aceptación**:
- Puedo seleccionar el objetivo en el que he avanzado
- Puedo registrar evidencia (descripción, enlaces, adjuntos)
- Puedo autoevaluar mi nivel de dominio alcanzado
- El sistema registra la evidencia con timestamp

---

## 6. Tickets de trabajo

### Épica 1: Configuración de Proyecto e Infraestructura Simplificada

#### DCM-001: Configuración del repositorio y estructura de proyecto
**Tipo**: Tarea Técnica  
**Prioridad**: Alta  
**Estimación**: 3 puntos  
**Descripción**: Crear repositorio en GitHub/GitLab y configurar estructura de carpetas básica para el proyecto.  
**Criterios de aceptación**:
- Repositorio creado con estructura de carpetas
- Configuración de ESLint, Prettier y TypeScript
- Inicialización de proyecto con React (frontend) y Express (backend)
- README con instrucciones de instalación y desarrollo

#### DCM-002: Configuración de entorno de desarrollo simple
**Tipo**: Tarea Técnica  
**Prioridad**: Alta  
**Estimación**: 3 puntos  
**Descripción**: Configurar un entorno de desarrollo simple con Docker para facilitar el desarrollo local.  
**Criterios de aceptación**:
- Docker Compose para el entorno de desarrollo
- Contenedores para base de datos (PostgreSQL)
- Scripts para iniciar el entorno completo
- Variables de entorno configuradas para desarrollo

#### DCM-003: Implementación del modelo de datos inicial
**Tipo**: Tarea Técnica  
**Prioridad**: Alta  
**Estimación**: 8 puntos  
**Descripción**: Implementar el esquema de base de datos inicial con las entidades principales requeridas para el MVP.  
**Criterios de aceptación**:
- Esquemas de PostgreSQL para entidades principales
- Migraciones de base de datos
- Scripts de inicialización para datos de prueba
- Configuración de ORM

### Épica 2: Autenticación y Gestión de Usuarios

#### DCM-005: Implementación de autenticación con Google OAuth
**Tipo**: Historia de Usuario  
**Prioridad**: Alta  
**Estimación**: 8 puntos  
**Descripción**: Como usuario, quiero poder iniciar sesión con mi cuenta de Google para acceder a la plataforma de manera segura y sin tener que crear credenciales adicionales.  
**Criterios de aceptación**:
- Flujo completo de login con Google OAuth 2.0
- Redirección a callback y procesamiento de tokens
- Generación y validación de JWT
- Manejo de sesiones
- UI para botón de login con Google

#### DCM-006: Implementación de roles de usuario (Admin/Developer)
**Tipo**: Historia de Usuario  
**Prioridad**: Alta  
**Estimación**: 5 puntos  
**Descripción**: Como sistema, necesito distinguir entre usuarios administradores y desarrolladores para proporcionar acceso diferenciado a las funcionalidades.  
**Criterios de aceptación**:
- Detección automática de rol basado en dominio de correo y primer usuario
- Middleware de autorización basado en roles
- Limitación de acceso a endpoints según rol
- Interfaz de usuario adaptada al rol del usuario

### Épica 3: Módulo de Análisis Cultural (NLP)

#### DCM-008: Servicio de procesamiento NLP con OpenAI GPT
**Tipo**: Tarea Técnica  
**Prioridad**: Alta  
**Estimación**: 13 puntos  
**Descripción**: Implementar el servicio de NLP para el análisis de documentos culturales utilizando OpenAI GPT API.  
**Criterios de aceptación**:
- Cliente para comunicación con OpenAI API
- Implementación de prompts optimizados para extracción de valores y comportamientos
- Manejo de reintentos y errores
- Control de costos y límites de tokens
- Pruebas unitarias con casos de texto real

#### DCM-009: Preprocesamiento de documentos culturales
**Tipo**: Tarea Técnica  
**Prioridad**: Alta  
**Estimación**: 8 puntos  
**Descripción**: Implementar la capa de preprocesamiento para documentos culturales en diferentes formatos.  
**Criterios de aceptación**:
- Extracción de texto de documentos PDF, DOCX y HTML
- Limpieza y normalización de texto
- Segmentación para procesamiento modular
- Detección de idioma

### Épica 7: Frontend y UX

#### DCM-022: Implementación de componentes compartidos
**Tipo**: Tarea Técnica  
**Prioridad**: Alta  
**Estimación**: 5 puntos  
**Descripción**: Desarrollar los componentes compartidos de UI que se utilizarán en toda la aplicación.  
**Criterios de aceptación**:
- Navbar y sidebar responsivos
- Componentes de formulario reutilizables
- Componentes de visualización de datos
- Tema y estilos unificados

#### DCM-023: Implementación de vistas de administrador
**Tipo**: Historia de Usuario  
**Prioridad**: Alta  
**Estimación**: 8 puntos  
**Descripción**: Como administrador, quiero acceder a un dashboard que me permita gestionar el perfil cultural y usuarios de mi organización.  
**Criterios de aceptación**:
- Dashboard principal con métricas
- Vista de gestión cultural
- Vista de gestión de usuarios
- Editor de mapa de carrera organizacional

### Planificación de Sprints

```mermaid
gantt
    title Plan de Implementación DevCompass MVP
    dateFormat  YYYY-MM-DD
    section Sprint 0
    Configuración inicial                          :a1, 2025-06-01, 2w
    
    section Sprint 1
    Autenticación y API Base                       :b1, 2025-06-15, 2w
    
    section Sprint 2
    Perfiles y Frontend Base                       :c1, 2025-06-29, 2w
    
    section Sprint 3
    Procesamiento NLP                              :d1, 2025-07-13, 2w
    
    section Sprint 4
    Interfaz de Administrador                      :e1, 2025-07-27, 2w
    
    section Sprint 5
    Perfiles de Desarrollador                      :f1, 2025-08-10, 2w
    
    section Sprint 6
    Alineación y Vistas                            :g1, 2025-08-24, 2w
    
    section Sprint 7
    Finalización MVP                               :h1, 2025-09-07, 2w
```

### Resumen del Plan

- **Total de tickets**: 28
- **Puntos de historia totales**: 175
- **Duración estimada**: 14 semanas (7 sprints de 2 semanas + Sprint 0)
- **Equipo recomendado**: 5 personas (1 Tech Lead, 2 Desarrolladores Full Stack, 1 Especialista NLP, 1 UX/UI Designer)

### Consideraciones Futuras

Después de validar el MVP con usuarios reales, se puede considerar la evolución hacia una arquitectura más robusta y escalable:

1. **Migración a Microservicios**
   - Separación de componentes en servicios independientes
   - Implementación de API Gateway más completo
   - Comunicación asíncrona entre servicios

2. **Mejoras de Escalabilidad**
   - Implementación de Kubernetes para orquestación
   - Implementación de bases de datos especializadas (MongoDB, Redis)
   - Arquitectura multi-región

3. **Enriquecimiento de NLP**
   - Fine-tuning de modelos específicos para contexto cultural
   - Implementación de ML para mejora continua
   - Procesamiento batch para análisis masivo

---

## 7. Pull requests

Work in Progress