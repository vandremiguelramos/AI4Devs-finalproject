# DevCompass: Parte III - Especificación Técnica (Implementación Simplificada para MVP)

![DevCompass Logo](https://via.placeholder.com/800x200?text=DevCompass+Logo)

*"Navegando tu carrera en el ecosistema de tu empresa"*

---

## Índice Parte III
1. [API y Servicios](#api-y-servicios)
2. [Frontend](#frontend)
3. [Seguridad e Integración con Google](#seguridad-e-integración-con-google)
4. [Infraestructura Simplificada](#infraestructura-simplificada)
5. [Plan de Implementación MVP](#plan-de-implementación-mvp)
6. [Consideraciones Futuras](#consideraciones-futuras)

---

## API y Servicios

Para el MVP de DevCompass, se implementará una API REST simplificada con Express.js que abarque todas las funcionalidades esenciales.

### Estructura de API Simplificada

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

### Endpoints Principales

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

### Implementación API Simple

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

module.exports = app;
```

## Frontend

La interfaz de usuario de DevCompass se desarrollará con React y TypeScript, siguiendo un enfoque simple pero funcional para el MVP.

### Estructura de Componentes

```mermaid
flowchart TD
    App --> Router
    Router --> AuthPages
    Router --> AdminPages
    Router --> DeveloperPages
    
    subgraph "Componentes Auth"
        AuthPages --> Login
        AuthPages --> GoogleCallback
    end
    
    subgraph "Componentes Admin"
        AdminPages --> Dashboard
        AdminPages --> CultureManager
        AdminPages --> UsersManager
        AdminPages --> CareerPathEditor
    end
    
    subgraph "Componentes Developer"
        DeveloperPages --> DevDashboard
        DeveloperPages --> ProfileView
        DeveloperPages --> CareerMapView
        DeveloperPages --> DevelopmentPlanView
    end
    
    subgraph "Componentes Compartidos"
        SharedComps[Shared Components]
        SharedComps --> Navbar
        SharedComps --> FormComponents
        SharedComps --> DataVisualizers
    end
    
    App --> SharedComps
    AdminPages --> SharedComps
    DeveloperPages --> SharedComps
    AuthPages --> SharedComps
```

### Principales Vistas MVP

#### Vista de Administrador

1. **Dashboard Cultural**
   - Resumen del perfil cultural
   - Métricas de alineación global
   - Estado de usuarios

2. **Gestor Cultural**
   - Subida de documentos
   - Visualización de valores extraídos
   - Editor de comportamientos esperados
   - Validación de perfil cultural

#### Vista de Desarrollador

1. **Dashboard Personal**
   - Resumen de perfil y posición
   - Indicadores de alineación
   - Próximos objetivos

2. **Autodiagnóstico**
   - Evaluación de competencias técnicas
   - Evaluación de competencias blandas
   - Visualización de resultados

3. **Mapa de Carrera y Plan**
   - Visualización de ruta profesional
   - Plan de desarrollo personalizado
   - Recursos recomendados

### Tecnologías Frontend para MVP

- **Framework**: React con TypeScript
- **Estado**: Context API o Redux simple
- **Routing**: React Router
- **UI**: Material UI para componentes base
- **Visualización**: Recharts para gráficos
- **Formularios**: Formik + Yup
- **HTTP**: Axios o fetch API

## Seguridad e Integración con Google

La seguridad es prioritaria incluso en el MVP, especialmente para la protección de datos culturales y personales.

### Flujo de Autenticación OAuth

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

### Implementación OAuth con Google (Simplificada)

```javascript
// Configuración del servidor de autenticación
const passport = require('passport');
const GoogleStrategy = require('passport-google-oauth20').Strategy;
const jwt = require('jsonwebtoken');
const User = require('../models/User');
const Organization = require('../models/Organization');

// Configuración de Google OAuth
passport.use(new GoogleStrategy({
    clientID: process.env.GOOGLE_CLIENT_ID,
    clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    callbackURL: '/api/auth/google/callback',
    scope: ['profile', 'email']
  },
  async (accessToken, refreshToken, profile, done) => {
    try {
      // Verificar si el usuario existe
      let user = await User.findOne({ googleId: profile.id });
      
      if (!user) {
        // Crear usuario nuevo
        const email = profile.emails[0].value;
        const domain = email.split('@')[1];
        
        // Buscar organización por dominio
        const organization = await Organization.findOne({ domain });
        
        // Determinar si es primer usuario de organización (admin)
        const isAdmin = organization ? 
          (await User.countDocuments({ organizationId: organization.id })) === 0 : 
          false;
        
        user = await User.create({
          googleId: profile.id,
          email,
          name: profile.displayName,
          profilePicture: profile.photos[0].value,
          organizationId: organization?.id,
          roleId: isAdmin ? 'admin' : 'developer'
        });
      }
      
      // Generar token JWT
      const token = jwt.sign(
        { id: user.id, email: user.email, role: user.roleId },
        process.env.JWT_SECRET,
        { expiresIn: '1h' }
      );
      
      return done(null, { user, token });
    } catch (error) {
      return done(error);
    }
  }
));

// Middleware de autenticación JWT
const authenticateJwt = (req, res, next) => {
  const authHeader = req.headers.authorization;
  
  if (authHeader) {
    const token = authHeader.split(' ')[1];
    
    jwt.verify(token, process.env.JWT_SECRET, (err, user) => {
      if (err) {
        return res.sendStatus(403);
      }
      
      req.user = user;
      next();
    });
  } else {
    res.sendStatus(401);
  }
};

module.exports = { passport, authenticateJwt };
```

### Medidas de Seguridad para MVP

1. **Autenticación**
   - OAuth 2.0 con Google
   - JWT para sesiones
   - Middleware de autorización por rol

2. **Protección de Datos**
   - Cifrado en tránsito (HTTPS)
   - Validación de entradas
   - Sanitización de datos

3. **Seguridad Básica**
   - Headers de seguridad (Helmet)
   - CORS configurado
   - Manejo seguro de errores

## Infraestructura Simplificada

Para el MVP de DevCompass, se utilizará una infraestructura simplificada pero robusta, enfocada en rápido desarrollo y validación.

### Arquitectura Simplificada

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

### Stack Tecnológico Simplificado

1. **Frontend**
   - React + TypeScript
   - Material UI
   - Recharts para visualizaciones
   - Alojado en Vercel/Netlify/Heroku

2. **Backend**
   - Node.js + Express.js
   - Passport.js para autenticación
   - Knex.js/Sequelize como ORM
   - Alojado en Heroku/Railway/Render

3. **Base de Datos**
   - PostgreSQL único
   - Migraciones con Knex/Sequelize
   - Alojado en servicio gestionado (Heroku Postgres)

4. **Servicios Externos**
   - OpenAI API para procesamiento NLP
   - Google OAuth para autenticación
   - Almacenamiento S3 para documentos (opcional)

### Configuración de Desarrollo Local

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

## Plan de Implementación MVP

### Backlog de Tickets Simplificado

Para el desarrollo del MVP, se ha creado un backlog de tickets enfocado en las funcionalidades esenciales con una infraestructura simplificada:

#### Épica 1: Configuración de Proyecto e Infraestructura Simplificada
- DCM-001: Configuración del repositorio y estructura de proyecto
- DCM-002: Configuración de entorno de desarrollo simple (Docker)
- DCM-003: Implementación del modelo de datos inicial
- DCM-004: Configuración de despliegue simple

#### Épica 2: Autenticación y Gestión de Usuarios
- DCM-005: Implementación de autenticación con Google OAuth
- DCM-006: Implementación de roles de usuario (Admin/Developer)
- DCM-007: Perfil de usuario y gestión de cuenta

#### Épica 3: Módulo de Análisis Cultural (NLP)
- DCM-008: Servicio de procesamiento NLP con OpenAI GPT
- DCM-009: Preprocesamiento de documentos culturales
- DCM-010: Motor de reglas para post-procesamiento
- DCM-011: Interfaz de administrador para gestión cultural

#### Épica 4: Evaluación de Perfiles Técnicos
- DCM-012: Implementación de autodiagnóstico para desarrolladores
- DCM-013: Calibración de nivel técnico
- DCM-014: Implementación del mapa de carrera básico

#### Épica 5: Motor de Alineación y Plan de Desarrollo
- DCM-015: Implementación del motor de alineación cultural-técnica
- DCM-016: Dashboard de alineación para desarrolladores
- DCM-017: Generación de plan de desarrollo personalizado

#### Épica 6: API y Routing
- DCM-018: Implementación de estructura de API básica
- DCM-019: Implementación de endpoints para gestión cultural
- DCM-020: Implementación de endpoints para perfiles y evaluación
- DCM-021: Implementación de endpoints para alineación y planes

#### Épica 7: Frontend y Experiencia de Usuario
- DCM-022: Implementación de componentes compartidos
- DCM-023: Implementación de vistas de administrador
- DCM-024: Implementación de vistas de desarrollador
- DCM-025: Visualizaciones de datos con Recharts

#### Épica 8: Integración y Pruebas
- DCM-026: Integración de componentes front-end y back-end
- DCM-027: Pruebas del flujo principal
- DCM-028: Despliegue de MVP en ambiente de producción

### Planificación de Sprints

```mermaid
gantt
    title Plan de Implementación DevCompass MVP
    dateFormat  YYYY-MM-DD
    section Sprint 0
    Configuración del repositorio                  :a1, 2025-06-01, 1w
    Configuración de entorno dev                   :a2, 2025-06-01, 1w
    Implementación modelo de datos                 :a3, 2025-06-08, 1w
    
    section Sprint 1
    Configuración de despliegue                    :b1, 2025-06-15, 1w
    Autenticación con Google                       :b2, 2025-06-15, 2w
    Implementación de roles                        :b3, 2025-06-22, 1w
    Estructura API básica                          :b4, 2025-06-22, 1w
    
    section Sprint 2
    Perfil y gestión de usuario                    :c1, 2025-06-29, 1w
    Endpoints gestión cultural                     :c2, 2025-06-29, 1w
    Endpoints perfiles                             :c3, 2025-07-06, 1w
    Componentes compartidos                        :c4, 2025-07-06, 1w
    
    section Sprint 3
    Servicio NLP con OpenAI                        :d1, 2025-07-13, 2w
    Preprocesamiento documentos                    :d2, 2025-07-13, 1w
    Motor de reglas                                :d3, 2025-07-20, 1w
    
    section Sprint 4
    Interfaz gestión cultural                      :e1, 2025-07-27, 2w
    Vistas de administrador                        :e2, 2025-07-27, 2w
    Visualizaciones (parte 1)                      :e3, 2025-08-03, 1w
    
    section Sprint 5
    Autodiagnóstico desarrolladores                :f1, 2025-08-10, 2w
    Calibración nivel técnico                      :f2, 2025-08-10, 1w
    Mapa de carrera básico                         :f3, 2025-08-17, 1w
    
    section Sprint 6
    Motor de alineación                            :g1, 2025-08-24, 2w
    Dashboard de alineación                        :g2, 2025-08-24, 1w
    Endpoints alineación y planes                  :g3, 2025-08-31, 1w
    Vistas de desarrollador                        :g4, 2025-08-31, 1w
    
    section Sprint 7
    Plan de desarrollo personalizado               :h1, 2025-09-07, 1w
    Visualizaciones (parte 2)                      :h2, 2025-09-07, 1w
    Integración de componentes                     :h3, 2025-09-14, 1w
    Pruebas y despliegue                           :h4, 2025-09-14, 1w
```

### Resumen del Plan

- **Total de tickets**: 28
- **Puntos de historia totales**: 175
- **Duración estimada**: 14 semanas (7 sprints de 2 semanas + Sprint 0)
- **Equipo recomendado**: 5 personas (1 Tech Lead, 2 Desarrolladores Full Stack, 1 Especialista NLP, 1 UX/UI Designer)

## Consideraciones Futuras

### Evolución Post-MVP

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

### Integraciones Futuras

```mermaid
flowchart LR
    DevCompass[DevCompass] --> HR[HR Systems]
    DevCompass --> LMS[Learning Platforms]
    DevCompass --> PM[Project Management]
    DevCompass --> Git[Git Platforms]
    
    HR --> HRIS[HRIS Systems]
    HR --> ATS[Applicant Tracking]
    
    LMS --> Udemy[Udemy]
    LMS --> Coursera[Coursera]
    LMS --> LinkedIn[LinkedIn Learning]
    
    PM --> Jira[Jira]
    PM --> Asana[Asana]
    PM --> Monday[Monday.com]
    
    Git --> GitHub[GitHub]
    Git --> GitLab[GitLab]
```

Las integraciones se priorizarán según el feedback de usuarios y la dirección que tome el producto después de la validación del MVP.

---

© 2025 DevCompass | *"Navegando tu carrera en el ecosistema de tu empresa"*