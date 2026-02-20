# 🐝 OpenCode Multi-Agent System — Proyecto de Prueba

> **Autor:** Josue (Jotures)
> **Fecha:** 2026-02-20
> **Herramienta:** [OpenCode](https://opencode.ai) (SST) con GitHub Copilot
> **Repositorio:** [Jotures/opencode-prueba](https://github.com/Jotures/opencode-prueba)

---

## 📋 Descripción del Proyecto

Este proyecto implementa un **sistema de 95 agentes especializados** para OpenCode, una herramienta CLI de desarrollo asistido por IA. Cada agente funciona como un **modo experto** con instrucciones detalladas (system prompts) que guían al modelo de IA para responder como un especialista en un dominio específico.

Los agentes fueron adaptados de la colección [jbeck018/agents-opencode](https://github.com/jbeck018/agents-opencode) (originalmente diseñada para Claude Code de Anthropic) y **convertidos al formato compatible con OpenCode (SST)**.

---

## 🏗️ Estructura del Proyecto

```
opencode-prueba/
├── .gitignore                    # Archivos ignorados por Git
├── .opencode/                    # Configuración de OpenCode
│   ├── agent/                    # 95 agentes especializados (.md)
│   │   ├── ai-engineer.md
│   │   ├── backend-architect.md
│   │   ├── code-reviewer.md
│   │   ├── python-pro.md
│   │   ├── security-auditor.md
│   │   ├── hive-queen-strategic.md
│   │   └── ... (95 archivos en total)
│   └── command/                  # Comandos personalizados
│       └── multi.md              # Comando /multi para orquestación
├── AGENTS-GUIDE.md               # Guía completa del sistema Hive-Mind (documentación original)
└── README.md                     # Este archivo
```

---

## 🔧 Problema Resuelto

### Situación Inicial
Los archivos de agentes estaban en formato **Claude Code** (Anthropic), que es incompatible con OpenCode (SST):

```yaml
# ❌ Formato original (Claude Code) - NO funcionaba en OpenCode
---
description: Elite code review expert...
mode: subagent
model: anthropic/claude-opus-4-20250514
temperature: 0.1
tools:
  write: false
  edit: false
  bash: false
  read: true
  grep: true
  glob: true
---
```

**Resultado:** OpenCode ignoraba los 95 agentes y solo mostraba los predeterminados ("Plan" y "Built") más un "README" que se leía erróneamente como agente.

### Solución Aplicada
Se migró el frontmatter YAML de cada archivo al formato compatible con OpenCode:

```yaml
# ✅ Formato corregido (OpenCode) - FUNCIONA
---
name: code-reviewer
description: Elite code review expert...
---
```

**Cambios realizados (PR #1):**
- ✅ Agregado campo `name:` derivado del nombre del archivo
- ✅ Eliminado `mode: subagent` (OpenCode no lo usa)
- ✅ Eliminado `model: anthropic/...` (usa el modelo por defecto del usuario)
- ✅ Eliminado `temperature:` (no soportado por OpenCode en agentes)
- ✅ Eliminado `tools:` en formato anidado de Claude Code
- ✅ Movido `README.md` de `.opencode/agent/` a `AGENTS-GUIDE.md` en la raíz
- ✅ Contenido de los system prompts **preservado intacto**

---

## 📦 Catálogo de los 95 Agentes

### 🐝 Hive-Mind y Orquestación (8 agentes)
| Agente | Descripción |
|--------|-------------|
| `hive-queen-strategic` | Planificación de alto nivel y descomposición de objetivos |
| `hive-queen-tactical` | Coordinación de ejecución en tiempo real |
| `hive-queen-adaptive` | Optimización continua y aprendizaje de patrones |
| `swarm-coordinator` | Spawning distribuido de agentes y agregación de resultados |
| `consensus-builder` | Toma de decisiones multi-agente y resolución de conflictos |
| `memory-archivist` | Memoria compartida persistente entre sesiones |
| `task-router` | Asignación inteligente de tareas según capacidades |
| `agent-spawner` | Creación y gestión del ciclo de vida de agentes |

### 🏗️ Desarrollo y Arquitectura (10 agentes)
| Agente | Descripción |
|--------|-------------|
| `backend-architect` | Diseño de APIs RESTful, microservicios y schemas de BD |
| `frontend-developer` | Componentes React, layouts responsivos, state management |
| `ui-ux-designer` | Diseño de interfaces, wireframes y design systems |
| `ui-visual-validator` | Validación visual de UI mediante análisis de screenshots |
| `mobile-developer` | Desarrollo React Native/Flutter con integraciones nativas |
| `graphql-architect` | Schemas GraphQL, resolvers y federation |
| `architect-review` | Revisión de consistencia arquitectónica |
| `database-architect` | Diseño de BD escalables y arquitectura de datos distribuidos |
| `event-sourcing-architect` | Event sourcing, CQRS y patrones event-driven |
| `monorepo-architect` | Estrategia monorepo con Nx, Turborepo y Bazel |

### 💻 Especialistas en Lenguajes (19 agentes)
| Agente | Descripción |
|--------|-------------|
| `python-pro` | Python idiomático con features avanzados |
| `javascript-pro` | JavaScript moderno con ES6+, async y Node.js |
| `typescript-pro` | TypeScript avanzado con generics y type safety |
| `golang-pro` | Go idiomático con goroutines, channels e interfaces |
| `rust-pro` | Rust con ownership, lifetimes y trait implementations |
| `c-pro` | C eficiente con gestión de memoria y system calls |
| `cpp-pro` | C++ moderno con RAII, smart pointers y STL |
| `java-pro` | Java moderno con streams, concurrencia y JVM |
| `csharp-pro` | C# moderno con .NET optimization |
| `php-pro` | PHP moderno con features avanzados |
| `ruby-pro` | Ruby con metaprogramming y Rails patterns |
| `elixir-pro` | Elixir con OTP patterns y Phoenix |
| `scala-pro` | Scala enterprise con programación funcional |
| `haskell-pro` | Programación funcional pura con type systems avanzados |
| `sql-pro` | SQL complejo, optimización de queries y schemas |
| `flutter-expert` | Flutter con Dart, widgets y platform integrations |
| `unity-developer` | Desarrollo de juegos Unity con C# |
| `minecraft-bukkit-pro` | Desarrollo de plugins Minecraft con Bukkit/Spigot/Paper |
| `ios-developer` | Desarrollo nativo iOS con Swift/SwiftUI |

### ⚙️ Infraestructura y Operaciones (14 agentes)
| Agente | Descripción |
|--------|-------------|
| `devops-troubleshooter` | Debug de producción, análisis de logs |
| `deployment-engineer` | CI/CD pipelines, Docker y cloud deployments |
| `cloud-architect` | Infraestructura AWS/Azure/GCP y optimización de costos |
| `hybrid-cloud-architect` | Infraestructura híbrida multi-cloud y on-premises |
| `kubernetes-architect` | Infraestructura cloud-native con K8s y GitOps |
| `database-optimizer` | Optimización de queries SQL e indexación |
| `database-admin` | Operaciones de BD, backups, replicación |
| `terraform-specialist` | Módulos Terraform avanzados e IaC |
| `incident-responder` | Respuesta a incidentes de producción |
| `network-engineer` | Conectividad de red, load balancers, SSL/TLS |
| `dx-optimizer` | Developer Experience: tooling, setup y workflows |
| `service-mesh-expert` | Istio, Linkerd, Envoy y traffic management |
| `observability-engineer` | OpenTelemetry, métricas, logging y tracing |
| `arm-cortex-expert` | Sistemas embebidos con ARM Cortex-M y RTOS |

### 🔒 Calidad y Seguridad (8 agentes)
| Agente | Descripción |
|--------|-------------|
| `code-reviewer` | Code review experto con foco en seguridad y confiabilidad |
| `security-auditor` | Auditoría de vulnerabilidades y compliance OWASP |
| `test-automator` | Suites de tests: unit, integration y e2e |
| `performance-engineer` | Profiling, optimización y caching |
| `debugger` | Especialista en debugging de errores y fallos |
| `error-detective` | Búsqueda de patrones de error en logs y código |
| `search-specialist` | Investigación web avanzada y síntesis |
| `tdd-orchestrator` | Workflows de Test-Driven Development |

### 🤖 Data e IA (7 agentes)
| Agente | Descripción |
|--------|-------------|
| `data-scientist` | Análisis de datos, SQL, BigQuery e insights |
| `data-engineer` | Pipelines ETL, data warehouses y streaming |
| `ai-engineer` | Aplicaciones LLM, sistemas RAG y prompt pipelines |
| `ml-engineer` | Pipelines ML, model serving y feature engineering |
| `mlops-engineer` | Infraestructura ML, experiment tracking |
| `prompt-engineer` | Optimización de prompts para LLMs |
| `vector-database-engineer` | Pinecone, Qdrant, Weaviate y búsqueda semántica |

### 📚 Documentación (4 agentes)
| Agente | Descripción |
|--------|-------------|
| `docs-architect` | Documentación técnica integral desde codebases |
| `mermaid-expert` | Diagramas Mermaid: flowcharts, ERDs, secuencias |
| `reference-builder` | Referencias técnicas exhaustivas y documentación API |
| `tutorial-engineer` | Tutoriales paso a paso y contenido educativo |

### 💼 Negocio y Marketing (6 agentes)
| Agente | Descripción |
|--------|-------------|
| `business-analyst` | Métricas, reportes y KPIs |
| `content-marketer` | Blog posts, social media y newsletters |
| `hr-pro` | Hiring, onboarding, PTO, performance |
| `sales-automator` | Cold emails, follow-ups y templates |
| `customer-support` | Tickets de soporte, FAQs y emails |
| `legal-advisor` | Políticas de privacidad, términos de servicio |

### 🔍 SEO y Contenido (10 agentes)
| Agente | Descripción |
|--------|-------------|
| `seo-content-auditor` | Auditoría de contenido para E-E-A-T y SEO |
| `seo-meta-optimizer` | Meta titles, descriptions y URLs optimizados |
| `seo-keyword-strategist` | Densidad de keywords y variaciones semánticas |
| `seo-structure-architect` | Estructura de contenido y schema markup |
| `seo-snippet-hunter` | Formateo para featured snippets |
| `seo-content-refresher` | Actualización de contenido desactualizado |
| `seo-cannibalization-detector` | Detección de canibalización de keywords |
| `seo-authority-builder` | Señales E-E-A-T e indicadores de confianza |
| `seo-content-writer` | Escritura de contenido SEO-optimizado |
| `seo-content-planner` | Outlines, topic clusters y calendarios |

### 🏢 Dominios Especializados (7 agentes)
| Agente | Descripción |
|--------|-------------|
| `api-documenter` | Specs OpenAPI/Swagger y documentación de APIs |
| `payment-integration` | Integración Stripe, PayPal y procesadores de pago |
| `quant-analyst` | Modelos financieros y backtesting de estrategias |
| `risk-manager` | Monitoreo de riesgo de portafolio |
| `legacy-modernizer` | Refactorización de codebases legacy |
| `context-manager` | Gestión de contexto entre agentes y tareas |
| `blockchain-developer` | Smart contracts, DeFi, Web3 y Solidity |

---

## ⚠️ Alcances y Limitaciones — Lo que Funciona vs Lo que No

### ✅ Funciona Completamente
| Funcionalidad | Descripción |
|---|---|
| **95 modos expertos** | Cada agente tiene un system prompt especializado de ~100-170 líneas |
| **Cambiar entre agentes** | Presionar `Tab` en OpenCode muestra todos los agentes disponibles |
| **Respuestas especializadas** | Cada agente responde con expertise profundo en su dominio |
| **Comando `/multi`** | Comando personalizado para simular coordinación multi-agente |

### ⚠️ Funciona Parcialmente
| Funcionalidad | Realidad |
|---|---|
| **`@mention` de agentes** | Depende de la versión de OpenCode instalada |
| **Sub-agentes automáticos** | OpenCode tiene soporte básico; requiere cambio manual con Tab |
| **Orquestación `/multi`** | Es un prompt que le pide al agente simular coordinación, no ejecución paralela real |

### ❌ No Funciona (Limitaciones de OpenCode actual)
| Funcionalidad | Realidad |
|---|---|
| **Hive-Mind real** (Queens→Workers) | Solo son system prompts descriptivos. No hay orquestación automática |
| **Multi-modelo** (GPT + Claude + Gemini) | Todos los agentes usan el mismo modelo (GitHub Copilot) |
| **Ejecución paralela real** | OpenCode ejecuta un agente a la vez |

---

## 🚀 Cómo Usar

### Prerrequisitos
- [OpenCode](https://opencode.ai) instalado (`npm i -g opencode`)
- Proveedor de IA configurado (GitHub Copilot, Anthropic, OpenAI, etc.)

### Instalación

```bash
git clone https://github.com/Jotures/opencode-prueba.git
cd opencode-prueba
opencode
```

### Uso Básico

1. **Abrir OpenCode** en la carpeta del proyecto:
   ```bash
   opencode
   ```

2. **Presionar `Tab`** para ver la lista de agentes disponibles.

3. **Seleccionar un agente** y escribir tu consulta:
   ```
   # Con code-reviewer seleccionado:
   Revisa este archivo para vulnerabilidades de seguridad

   # Con python-pro seleccionado:
   Escribe un script para procesar archivos CSV en paralelo

   # Con backend-architect seleccionado:
   Diseña una API REST para un sistema de e-commerce
   ```

### Formato de los Agentes

Cada agente sigue esta estructura:

```yaml
---
name: nombre-del-agente
description: Descripción breve de las capacidades del agente
---
```

---

## 📊 Historial del Proyecto

| Fecha | Evento |
|-------|--------|
| 2026-02-19 | Creación del repositorio y subida inicial de agentes (formato Claude Code) |
| 2026-02-20 | Diagnóstico: agentes incompatibles con OpenCode |
| 2026-02-20 | PR #1: Migración de 95 agentes al formato OpenCode + mover README.md |
| 2026-02-20 | Merge del PR #1 — Agentes funcionando correctamente |

---

## 📚 Documentación Adicional

- **[AGENTS-GUIDE.md](./AGENTS-GUIDE.md)** — Guía completa del sistema Hive-Mind, workflows multi-agente, y documentación detallada de cada agente
- **[OpenCode Docs](https://opencode.ai/docs/)** — Documentación oficial de OpenCode
- **[Repo original de agentes](https://github.com/jbeck018/agents-opencode)** — Colección original de donde se adaptaron los agentes

---

## 📄 Licencia

Los agentes están basados en la colección de [wshobson/agents](https://github.com/wshobson/agents) bajo licencia MIT.