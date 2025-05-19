# DevCompass: Parte II - Especificación Técnica (Arquitectura)

![DevCompass Logo](https://via.placeholder.com/800x200?text=DevCompass+Logo)

*"Navegando tu carrera en el ecosistema de tu empresa"*

---

## Índice Parte II
1. [Visión General Técnica](#visión-general-técnica)
2. [Modelo de Datos](#modelo-de-datos)
3. [Arquitectura del Sistema](#arquitectura-del-sistema)
4. [Componentes Técnicos de NLP](#componentes-técnicos-de-nlp)

---

## Visión General Técnica

DevCompass se construirá como una aplicación web moderna basada en microservicios, con una clara separación entre frontend y backend. La aplicación utilizará tecnologías cloud-native y seguirá principios de desarrollo ágil.

### Stack Tecnológico Principal

```mermaid
flowchart TD
    subgraph "Frontend"
        React[React + TypeScript]
        Redux[Redux Toolkit]
        MaterialUI[Material UI]
        D3[D3.js / Recharts]
    end
    
    subgraph "Backend"
        Node[Node.js + Express]
        Microservices[Microservicios]
        MQ[Message Queue]
        NLP[Servicio NLP]
    end
    
    subgraph "Datos"
        PostgreSQL[PostgreSQL]
        MongoDB[MongoDB]
        Redis[Redis]
    end
    
    subgraph "DevOps"
        Docker[Docker]
        K8s[Kubernetes]
        CICD[CI/CD Pipeline]
        Monitor[Prometheus + Grafana]
    end
    
    Frontend <--> Backend
    Backend <--> Datos
    DevOps --> Frontend
    DevOps --> Backend
    DevOps --> Datos
```

## Modelo de Datos

El modelo de datos de DevCompass está diseñado para soportar el contexto organizacional, perfiles culturales, mapas de carrera y planes de desarrollo individuales.

### Diagrama Entidad-Relación

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

### Entidades Principales

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

### Estrategia de Persistencia

- **PostgreSQL**: Almacenamiento principal para datos relacionales y transaccionales
- **MongoDB**: Para documentos semiestructurados (perfiles culturales, evidencias)
- **Redis**: Caché, sesiones y datos de alta frecuencia de acceso

## Arquitectura del Sistema

DevCompass utiliza una arquitectura de microservicios para permitir desarrollo, despliegue y escalado independientes de cada componente funcional.

### Diagrama de Arquitectura

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

### Descripción de Componentes Principales

1. **API Gateway**
   - Enrutamiento de solicitudes
   - Autenticación y autorización
   - Rate limiting y seguridad
   - Gestión de versiones de API

2. **Authentication Service**
   - Integración con Google OAuth
   - Gestión de sesiones y tokens
   - Autorización basada en roles

3. **Culture Analysis Service**
   - Gestión de documentos culturales
   - Coordinación con servicio NLP
   - Almacenamiento y consulta de perfiles culturales

4. **Developer Profile Service**
   - Gestión de perfiles técnicos
   - Evaluaciones de competencias
   - Historial de progresión

5. **Career Map Service**
   - Definición de rutas de carrera
   - Gestión de niveles y requisitos
   - Posicionamiento en mapa de carrera

6. **Alignment Engine**
   - Cálculo de alineación cultural-técnica
   - Identificación de brechas
   - Priorización de áreas de desarrollo

7. **Development Plan Service**
   - Generación de planes personalizados
   - Recomendación de recursos
   - Seguimiento de progreso

## Componentes Técnicos de NLP

El servicio NLP para el MVP se implementará con un enfoque híbrido que combina OpenAI GPT API con un sistema de reglas personalizadas, ofreciendo el mejor balance entre velocidad de implementación, precisión y flexibilidad.

### Estrategia NLP para MVP Mínimo

```mermaid
flowchart TD
    Input[Documentos Culturales] --> Preprocessor[Preprocesamiento básico]
    Preprocessor --> GPTService[Servicio OpenAI GPT]
    GPTService --> StructuredParser[Parser JSON estructurado]
    StructuredParser --> RulesEngine[Motor de reglas]
    RulesEngine --> ValidationProcess[Proceso de validación]
    ValidationProcess --> CulturalDB[(Base de datos cultural)]
    CulturalDB --> API[API de consulta]
    ValidationProcess --> AdminUI[Interfaz de administrador]
    AdminUI --> ManualAdjustment[Ajustes manuales]
    ManualAdjustment --> CulturalDB
```

### Arquitectura del Servicio NLP

```mermaid
flowchart TD
    subgraph "API Gateway"
        Gateway[API Gateway]
    end
    
    subgraph "NLP Service"
        Controller[NLP Controller]
        PreProcessor[Preprocessor]
        GPTClient[OpenAI GPT Client]
        ResultParser[Result Parser]
        RulesEngine[Rules Engine]
        ValidationService[Validation Service]
    end
    
    subgraph "Storage"
        MongoDB[(MongoDB - Cultural Documents)]
        Redis[(Redis - Processing Cache)]
    end
    
    Gateway --> Controller
    Controller --> PreProcessor
    PreProcessor --> GPTClient
    GPTClient --> ResultParser
    ResultParser --> RulesEngine
    RulesEngine --> ValidationService
    ValidationService --> MongoDB
    PreProcessor --> Redis
    RulesEngine --> Redis
```

### Componentes Principales

1. **Preprocessor**
   - Extracción de texto de diferentes formatos (PDF, DOCX, HTML)
   - Limpieza básica y normalización
   - Segmentación en bloques procesables
   - Detección de idioma

2. **OpenAI GPT Client**
   - Gestión de prompts optimizados
   - Control de tokens y costos
   - Manejo de reintentos y errores
   - Paralelización de solicitudes

3. **Result Parser**
   - Validación de JSON retornado
   - Normalización de términos
   - Detección de inconsistencias
   - Consolidación de respuestas

4. **Rules Engine**
   - Jerarquización de valores
   - Mapeo de comportamientos a niveles
   - Eliminación de duplicados
   - Enriquecimiento semántico

5. **Validation Service**
   - Interfaz para revisión humana
   - Opciones de edición y ajuste
   - Confirmación de resultados
   - Publicación de perfil finalizado

### Ejemplos de Prompts GPT

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

### Flujo de Procesamiento Completo

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

### Métricas de Rendimiento Objetivo

- **Tiempo de procesamiento**: < 2 minutos para documentos típicos (hasta 50 páginas)
- **Precisión en valores**: > 85% de valores culturales correctamente identificados
- **Precisión en comportamientos**: > 80% de comportamientos correctamente asociados
- **Satisfacción de usuario**: > 4/5 en relevancia de los resultados extraídos
- **Tasa de ajustes manuales**: < 30% de elementos requieren modificación manual