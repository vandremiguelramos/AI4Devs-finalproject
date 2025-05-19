# DevCompass: Parte I - Documento Funcional

![DevCompass Logo](https://via.placeholder.com/800x200?text=DevCompass+Logo)

*"Navegando tu carrera en el ecosistema de tu empresa"*

---

## Índice Parte I
1. [Descripción General](#descripción-general)
2. [Valor Agregado](#valor-agregado)
3. [Ventajas Competitivas](#ventajas-competitivas)
4. [Módulos del MVP](#módulos-del-mvp)
5. [Casos de Uso](#casos-de-uso)
6. [Sistema de Autenticación](#sistema-de-autenticación)
7. [Flujo del Usuario](#flujo-del-usuario)
8. [Procesamiento de Lenguaje Natural (NLP)](#procesamiento-de-lenguaje-natural-nlp)

---

## Descripción General

DevCompass es una plataforma innovadora que alinea el desarrollo profesional de especialistas en tecnología con la cultura y valores de su empresa. El sistema traduce la cultura organizacional en un mapa de desarrollo personalizado, permitiendo a los profesionales IT navegar su carrera desde Junior hasta Tech Leader de manera eficiente y culturalmente alineada.

## Valor Agregado

DevCompass transforma el desarrollo profesional tradicional al integrar tres dimensiones clave que normalmente permanecen desconectadas:

1. **Alineación cultural-técnica:** Convierte la cultura empresarial abstracta en rutas de desarrollo concretas y accionables.

2. **Personalización contextual:** Adapta el camino de aprendizaje a las necesidades específicas del profesional y su entorno organizacional.

3. **Visibilidad bidireccional:** Permite tanto al profesional como a la empresa visualizar el progreso y alineación, facilitando decisiones basadas en datos.

## Ventajas Competitivas

1. **Enfoque integrado:** A diferencia de plataformas de aprendizaje técnico genéricas, DevCompass personaliza el desarrollo según el contexto cultural específico.

2. **Procesamiento de cultura:** Capacidad única para transformar descripciones textuales de cultura en parámetros accionables de desarrollo.

3. **Mapeo dinámico:** Actualización continua del plan de desarrollo basada en el progreso del usuario y cambios organizacionales.

4. **Orientación específica al sector IT:** Diseñado exclusivamente para el desarrollo de carrera en tecnología, abordando sus desafíos únicos.

5. **Medición de alineación:** Métricas concretas del grado de sincronización entre desarrollo personal y expectativas organizacionales.

## Módulos del MVP

### 1. Captura y análisis cultural
- Formulario estructurado para input de texto libre sobre cultura empresarial
- Extracción automática de valores y comportamientos esperados
- Visualización del "ADN cultural" de la organización

### 2. Evaluación técnica contextualizada
- Autodiagnóstico de competencias técnicas por nivel
- Evaluación de habilidades blandas relevantes por etapa
- Benchmark respecto a expectativas de la posición actual

### 3. Mapa de carrera personalizado
- Visualización del camino Junior → Tech Leader
- Hitos y competencias necesarias por nivel
- Indicadores de posición actual y próximos objetivos

### 4. Motor de alineación
- Dashboard de coincidencia entre perfil actual y expectativas
- Identificación de brechas prioritarias
- Recomendaciones personalizadas basadas en análisis cultural-técnico

### 5. Plan de desarrollo accionable
- Generación de roadmap con prioridades claras
- Recursos recomendados filtrados por relevancia cultural
- Sistema de seguimiento de progreso con indicadores visuales

### 6. Seguimiento de evolución
- Registro de evidencias de desarrollo
- Métricas de progreso técnico y alineación cultural
- Reportes periódicos de avance compartibles con mentores/líderes

## Casos de Uso

### Módulo 1: Captura y Análisis Cultural

#### CU-1.1: Ingreso de información cultural empresarial
**Actor principal:** Representante de RRHH/Liderazgo
- **Descripción:** El representante ingresa información sobre la cultura organizacional mediante texto libre y formularios estructurados.
- **Precondición:** Usuario con rol administrativo autenticado en el sistema.
- **Flujo básico:**
  1. El usuario accede al módulo de cultura empresarial.
  2. Completa campos estructurados (valores corporativos, misión, visión).
  3. Proporciona texto libre describiendo comportamientos valorados.
  4. Carga documentos relevantes (código de conducta, manuales de cultura).
  5. El sistema confirma la recepción de la información.
- **Flujo alternativo:** Si ya existe información cultural previa, el sistema ofrece actualizar o reemplazar.
- **Postcondición:** Información cultural almacenada y lista para análisis.

#### CU-1.2: Procesamiento y extracción de valores culturales
**Actor principal:** Sistema
- **Descripción:** El sistema analiza la información cultural para extraer valores clave y expectativas comportamentales.
- **Precondición:** Información cultural ingresada en el sistema.
- **Flujo básico:**
  1. El sistema aplica NLP para identificar valores centrales.
  2. Categoriza los comportamientos esperados por nivel jerárquico.
  3. Identifica competencias valoradas culturalmente.
  4. Crea un perfil cultural de la organización.
- **Postcondición:** Perfil cultural indexado y disponible para referencia.

#### CU-1.3: Visualización del ADN cultural
**Actor principal:** Administrador/Desarrollador
- **Descripción:** El usuario visualiza el perfil cultural de la organización.
- **Precondición:** Análisis cultural completado.
- **Flujo básico:**
  1. El usuario accede al dashboard cultural.
  2. Visualiza representación gráfica de valores centrales.
  3. Explora comportamientos esperados por nivel.
  4. Accede a recomendaciones de alineación cultural.
- **Postcondición:** Usuario comprende el perfil cultural de la organización.

### Módulo 2: Evaluación Técnica Contextualizada

#### CU-2.1: Autodiagnóstico inicial del desarrollador
**Actor principal:** Desarrollador
- **Descripción:** El desarrollador realiza una autoevaluación de sus competencias técnicas y blandas.
- **Precondición:** Usuario registrado con perfil de desarrollador.
- **Flujo básico:**
  1. El desarrollador accede al módulo de autodiagnóstico.
  2. Completa evaluación técnica basada en su nivel actual.
  3. Evalúa sus habilidades blandas.
  4. Indica sus objetivos de carrera.
  5. El sistema registra las respuestas.
- **Flujo alternativo:** El desarrollador puede guardar parcialmente y continuar después.
- **Postcondición:** Perfil técnico del desarrollador creado.

#### CU-2.2: Calibración de nivel técnico
**Actor principal:** Sistema/Líder técnico (opcional)
- **Descripción:** El sistema evalúa el nivel técnico del desarrollador y opcionalmente un líder puede validarlo.
- **Precondición:** Autodiagnóstico completado.
- **Flujo básico:**
  1. El sistema analiza las respuestas del autodiagnóstico.
  2. Asigna un nivel técnico preliminar (Junior/Mid/Senior/Tech Lead).
  3. Opcionalmente notifica al líder para validación.
  4. El líder revisa y ajusta si es necesario.
- **Postcondición:** Nivel técnico validado asignado al desarrollador.

#### CU-2.3: Benchmark contra expectativas organizacionales
**Actor principal:** Sistema
- **Descripción:** El sistema compara el perfil del desarrollador con las expectativas para su nivel en la organización.
- **Precondición:** Nivel técnico asignado y perfil cultural disponible.
- **Flujo básico:**
  1. El sistema cruza competencias del desarrollador con expectativas culturales.
  2. Calcula indicadores de alineación por categoría.
  3. Identifica fortalezas y brechas.
  4. Genera informe de benchmark personalizado.
- **Postcondición:** Análisis de brechas disponible para el plan de desarrollo.

### Módulo 3: Mapa de Carrera Personalizado

#### CU-3.1: Generación del mapa de carrera
**Actor principal:** Sistema
- **Descripción:** El sistema genera un mapa visual del camino de desarrollo desde Junior hasta Tech Leader.
- **Precondición:** Perfil cultural y evaluación técnica completos.
- **Flujo básico:**
  1. El sistema combina el modelo genérico de carrera IT con el contexto cultural.
  2. Personaliza hitos según expectativas organizacionales.
  3. Adapta competencias requeridas por nivel.
  4. Crea visualización del camino completo.
- **Postcondición:** Mapa de carrera personalizado disponible.

#### CU-3.2: Posicionamiento en el mapa de carrera
**Actor principal:** Desarrollador/Sistema
- **Descripción:** El sistema posiciona al desarrollador en el mapa de carrera según su evaluación.
- **Precondición:** Mapa de carrera generado y evaluación técnica completada.
- **Flujo básico:**
  1. El sistema identifica la posición actual basada en la evaluación.
  2. Marca visualmente esta posición en el mapa.
  3. Calcula la distancia a hitos próximos.
  4. Indica competencias dominadas y pendientes.
- **Postcondición:** Desarrollador visualiza su posición en el mapa de carrera.

#### CU-3.3: Identificación de próximos objetivos
**Actor principal:** Desarrollador/Sistema
- **Descripción:** El sistema identifica y propone los siguientes objetivos de desarrollo.
- **Precondición:** Posicionamiento en mapa completado.
- **Flujo básico:**
  1. El sistema identifica competencias prioritarias a desarrollar.
  2. Sugiere próximo nivel a alcanzar.
  3. Estima tiempo aproximado para alcanzar hitos.
  4. El desarrollador confirma objetivos de interés.
- **Postcondición:** Objetivos próximos definidos para el plan de desarrollo.

### Módulo 4: Motor de Alineación

#### CU-4.1: Análisis de coincidencia cultural-técnica
**Actor principal:** Sistema
- **Descripción:** El sistema analiza el grado de alineación entre el perfil del desarrollador y las expectativas culturales.
- **Precondición:** Perfil cultural y evaluación técnica completos.
- **Flujo básico:**
  1. El sistema aplica algoritmos de coincidencia entre perfiles.
  2. Calcula puntuación de alineación por dimensión.
  3. Identifica áreas de alta y baja alineación.
  4. Genera informe detallado.
- **Postcondición:** Índice de alineación calculado y disponible.

#### CU-4.2: Visualización de dashboard de alineación
**Actor principal:** Desarrollador/Líder
- **Descripción:** El usuario visualiza el dashboard que muestra el grado de alineación.
- **Precondición:** Análisis de coincidencia completado.
- **Flujo básico:**
  1. El usuario accede al dashboard de alineación.
  2. Visualiza gráficos de puntuación por dimensión.
  3. Explora detalles de áreas específicas.
  4. Accede a explicaciones sobre cálculos de alineación.
- **Postcondición:** Usuario comprende su nivel de alineación cultural-técnica.

#### CU-4.3: Identificación de brechas prioritarias
**Actor principal:** Sistema
- **Descripción:** El sistema identifica y prioriza brechas a abordar.
- **Precondición:** Análisis de coincidencia completado.
- **Flujo básico:**
  1. El sistema evalúa el impacto de cada brecha.
  2. Prioriza según importancia cultural y técnica.
  3. Genera lista ordenada de áreas a desarrollar.
  4. Asigna niveles de urgencia.
- **Postcondición:** Lista priorizada de brechas disponible para plan de desarrollo.

### Módulo 5: Plan de Desarrollo Accionable

#### CU-5.1: Generación del roadmap personalizado
**Actor principal:** Sistema
- **Descripción:** El sistema crea un plan de desarrollo personalizado basado en brechas identificadas.
- **Precondición:** Análisis de brechas completado.
- **Flujo básico:**
  1. El sistema traduce brechas en objetivos de desarrollo.
  2. Secuencia objetivos según prioridad y dependencias.
  3. Establece tiempos estimados para cada objetivo.
  4. Genera visualización del roadmap completo.
- **Postcondición:** Plan de desarrollo disponible para el usuario.

#### CU-5.2: Recomendación de recursos de aprendizaje
**Actor principal:** Sistema
- **Descripción:** El sistema recomienda recursos específicos para cada objetivo de desarrollo.
- **Precondición:** Roadmap generado.
- **Flujo básico:**
  1. El sistema identifica recursos relevantes para cada objetivo.
  2. Filtra por relevancia cultural y técnica.
  3. Prioriza según efectividad y accesibilidad.
  4. Presenta catálogo de recursos personalizado.
- **Flujo alternativo:** Si hay recursos internos de la empresa, se priorizan apropiadamente.
- **Postcondición:** Recursos de aprendizaje asociados a cada objetivo.

#### CU-5.3: Configuración de seguimiento de progreso
**Actor principal:** Desarrollador
- **Descripción:** El desarrollador configura su sistema de seguimiento de progreso.
- **Precondición:** Plan de desarrollo generado.
- **Flujo básico:**
  1. El desarrollador accede a configuración de seguimiento.
  2. Establece frecuencia de check-ins.
  3. Selecciona indicadores a monitorear.
  4. Configura notificaciones.
  5. Opcionalmente invita mentores/líderes al seguimiento.
- **Postcondición:** Sistema de seguimiento configurado.

### Módulo 6: Seguimiento de Evolución

#### CU-6.1: Registro de evidencias de desarrollo
**Actor principal:** Desarrollador
- **Descripción:** El desarrollador registra evidencias de su progreso en objetivos específicos.
- **Precondición:** Plan de desarrollo activo.
- **Flujo básico:**
  1. El desarrollador accede al módulo de seguimiento.
  2. Selecciona objetivo en el que ha avanzado.
  3. Registra evidencia (descripción, enlaces, adjuntos).
  4. Autoevalúa nivel de dominio alcanzado.
  5. El sistema registra la evidencia con timestamp.
- **Postcondición:** Evidencia registrada y asociada al objetivo correspondiente.

#### CU-6.2: Actualización de métricas de progreso
**Actor principal:** Sistema
- **Descripción:** El sistema actualiza las métricas de progreso basado en evidencias registradas.
- **Precondición:** Evidencias registradas.
- **Flujo básico:**
  1. El sistema procesa las evidencias nuevas.
  2. Actualiza porcentajes de avance por objetivo.
  3. Recalcula métricas de alineación.
  4. Actualiza visualizaciones de progreso.
- **Postcondición:** Métricas de progreso actualizadas.

#### CU-6.3: Generación de reportes de avance
**Actor principal:** Desarrollador/Líder
- **Descripción:** El usuario genera reportes de avance para períodos específicos.
- **Precondición:** Métricas de progreso disponibles.
- **Flujo básico:**
  1. El usuario accede al módulo de reportes.
  2. Selecciona período de interés.
  3. Configura elementos a incluir en el reporte.
  4. Genera el reporte en el formato deseado.
  5. Opcionalmente comparte con stakeholders relevantes.
- **Flujo alternativo:** Generación automática de reportes según periodicidad configurada.
- **Postcondición:** Reporte de avance generado y distribuido según configuración.

#### CU-6.4: Ajuste dinámico del plan de desarrollo
**Actor principal:** Sistema/Desarrollador
- **Descripción:** El sistema o el desarrollador ajustan el plan según el progreso y cambios contextuales.
- **Precondición:** Seguimiento de progreso activo durante cierto período.
- **Flujo básico:**
  1. El sistema detecta desviaciones significativas del plan.
  2. Sugiere ajustes al roadmap y prioridades.
  3. El desarrollador revisa y confirma cambios propuestos.
  4. El sistema actualiza el plan de desarrollo.
- **Flujo alternativo:** El desarrollador inicia manualmente el proceso de ajuste.
- **Postcondición:** Plan de desarrollo actualizado según avance real y contexto actual.

## Sistema de Autenticación

### Requisitos de Autenticación con Google

#### Descripción General
DevCompass implementará un sistema de autenticación basado en cuentas de Google (Google Sign-In) que permitirá dos perfiles de usuario diferenciados: administradores y desarrolladores. Este enfoque simplifica el proceso de registro, mejora la seguridad y facilita la gestión de accesos en entornos corporativos donde Google Workspace es ampliamente utilizado.

#### Tecnología y Configuración
- **Protocolo**: OAuth 2.0 con OpenID Connect
- **Alcance de permisos**: 
  - Información básica del perfil
  - Correo electrónico verificado
  - Opcional: acceso a Google Calendar para integración de planes de desarrollo (versiones futuras)
- **Método de implementación**: Google Identity Services SDK
- **Seguridad**: Tokens JWT con firma y validación del lado del servidor

### Perfiles de Usuario

#### 1. Perfil Administrador
**Descripción**: Usuarios con capacidad para configurar el sistema a nivel organizacional y gestionar perfiles culturales.

**Características**:
- Acceso completo al módulo de Captura y Análisis Cultural
- Capacidad para definir y actualizar el perfil cultural de la empresa
- Gestión de dominios permitidos para el registro (ej. @tuempresa.com)
- Visualización de dashboards agregados de alineación cultural
- Configuración de niveles de carrera y expectativas por nivel
- Gestión de usuarios internos

**Proceso de asignación**:
- Primer usuario registrado con un dominio corporativo específico
- Asignación manual por administradores existentes
- Verificación opcional por correo electrónico corporativo con nivel de gerencia

#### 2. Perfil Desarrollador
**Descripción**: Usuarios finales que utilizan el sistema para evaluar y desarrollar su carrera profesional.

**Características**:
- Acceso a su perfil técnico personal
- Visualización del mapa de carrera personalizado
- Autodiagnóstico de competencias
- Plan de desarrollo y seguimiento de evolución
- Registro de evidencias de progreso
- Generación de reportes personales

**Proceso de asignación**:
- Registro automático como desarrollador para cualquier usuario que se autentique con Google
- Verificación opcional de correo corporativo para vincular automáticamente con perfil cultural

### Flujo de Autenticación

#### Primer Ingreso - Administrador
1. Usuario visita DevCompass y selecciona "Iniciar sesión con Google"
2. Se autentica en Google y autoriza permisos básicos
3. Al detectar primer usuario de un dominio corporativo, el sistema ofrece configuración inicial
4. Usuario confirma rol de administrador y completa información organizacional básica
5. Sistema habilita módulo de Captura Cultural para configuración inicial

#### Primer Ingreso - Desarrollador
1. Usuario visita DevCompass y selecciona "Iniciar sesión con Google"
2. Se autentica en Google y autoriza permisos básicos
3. Sistema verifica dominio de correo y lo asocia a perfil cultural (si existe)
4. Usuario es dirigido al proceso de onboarding y autodiagnóstico inicial
5. Sistema genera perfil inicial y mapa de carrera preliminar

#### Accesos Posteriores
1. Usuario visita DevCompass y selecciona "Iniciar sesión con Google"
2. Sistema reconoce al usuario y carga su perfil y preferencias
3. Interfaz se adapta automáticamente según el rol (administrador/desarrollador)
4. Usuario accede directamente a su dashboard personalizado

## Flujo del Usuario

1. La empresa carga información cultural (texto libre)
2. El sistema procesa y crea un perfil cultural de la organización
3. El desarrollador completa su evaluación inicial
4. El sistema genera un mapa de posicionamiento y alineación
5. Se crea un plan de desarrollo personalizado
6. El usuario registra su progreso periódicamente
7. Dashboard muestra la evolución y alineación cultural-técnica

## Procesamiento de Lenguaje Natural (NLP)

El componente de NLP es un diferenciador clave de DevCompass que permite transformar descripciones textuales de cultura organizacional en parámetros accionables para el desarrollo profesional.

### Arquitectura del Sistema NLP

El sistema NLP de DevCompass se estructura en cinco capas principales:

1. **Capa de Ingesta y Preprocesamiento**
   - Recepción de textos culturales de diversas fuentes (documentos, formularios, etc.)
   - Limpieza y normalización textual (eliminación de stopwords, lematización)
   - Segmentación por secciones temáticas (valores, comportamientos, expectativas)
   - Generación de corpus procesable para análisis

2. **Capa de Análisis Semántico**
   - Identificación de valores corporativos mediante reconocimiento de entidades y análisis semántico
   - Extracción de verbos de acción que denotan comportamientos valorados
   - Detección de patrones lingüísticos asociados a expectativas
   - Mapeo de términos técnicos específicos de la organización

3. **Capa de Categorización y Estructuración**
   - Clasificación de valores extraídos en categorías predefinidas (innovación, colaboración, etc.)
   - Asociación de comportamientos a niveles jerárquicos específicos
   - Agrupación de expectativas por áreas de competencia
   - Generación de taxonomía cultural específica de la empresa

4. **Capa de Correlación Técnica**
   - Asociación entre elementos culturales y competencias técnicas
   - Ponderación de valores según relevancia para diferentes roles IT
   - Mapeo entre comportamientos culturales y habilidades de desarrollo de software
   - Identificación de alineaciones y discrepancias potenciales

5. **Capa de Visualización y API**
   - Generación de representaciones visuales del "ADN cultural"
   - Exposición de endpoints para consumo por otros módulos
   - Interfaz de consulta para búsquedas contextuales
   - Exportación de resultados en formatos estructurados

### Implementación en el MVP

Para el MVP, el sistema NLP se implementará con las siguientes consideraciones:

1. **Alcance Inicial**
   - Enfoque en extracción precisa de 5-10 valores corporativos clave
   - Identificación de comportamientos esperados para 3 niveles básicos (Junior, Mid, Senior)
   - Mapeo inicial a competencias técnicas fundamentales
   - Visualización simplificada pero informativa del perfil cultural

2. **Limitaciones Controladas**
   - Procesamiento optimizado para documentos en español, inglés y portugués
   - Enfoque en industria tecnológica con posibilidad de expansión
   - Capacidad de procesamiento para documentos de hasta 50 páginas
   - Tiempo de análisis acotado (menos de 1 minuto para documentos típicos)

3. **Métricas de Rendimiento**
   - Precisión > 80% en identificación de valores corporativos
   - Recall > 75% en extracción de comportamientos relevantes
   - Tiempo de procesamiento < 30 segundos para documentos estándar
   - Satisfacción de usuario > 4/5 en relevancia de resultados