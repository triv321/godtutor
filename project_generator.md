# 🛠️ PROJECT GENERATOR
## Production-Grade Projects That Can't Be Found in Tutorials

> **Reference File**: Load when assigning projects during `learning_engine.md` phases

---

## 🎯 PROJECT DESIGN PHILOSOPHY

Every project in this database follows these principles:

```
ANTI-TUTORIAL HELL PRINCIPLES:
  
  1. NO COPY-PASTE SOLUTIONS
     Projects are designed so Googling won't give direct answers.
     
  2. PRODUCTION CONTEXT
     Every project is something real companies actually build.
     
  3. FORCED INTERNALS
     Ban common libraries to force understanding of how things work.
     
  4. MEASURABLE SUCCESS
     Clear criteria—no ambiguity about "done."
     
  5. SCALING MINDSET
     Always include "now make it handle 10x load" challenges.
```

---

## 🧠 CRITICAL: LLM PROJECT GENERATION MANDATE

```
⚠️ IMPORTANT FOR THE LLM:

The projects below are EXAMPLES and TEMPLATES, NOT an exhaustive list.

YOU MUST:
  ✓ Generate NEW projects tailored to what the user is learning
  ✓ Use the template structure to create original project ideas
  ✓ Adapt projects to the user's specific learning context
  ✓ Be CREATIVE - match projects to their current skill gaps
  
USE THE DATABASE PROJECTS WHEN:
  ✓ They perfectly match the user's learning goals
  ✓ As inspiration for creating similar projects
  ✓ As reference for quality/difficulty level
  
CREATE NEW PROJECTS WHEN:
  ✓ User is learning something not covered by database
  ✓ User's specific gaps need targeted practice
  ✓ You can create something more relevant to their goals
  ✓ Database projects have been exhausted
  
EXAMPLE:
  If user is learning Go:
    ❌ DON'T force-fit the Node.js rate limiter
    ✅ DO generate: "Build a concurrent web scraper in Go
        (goroutines, channels, sync primitives)"

  If user is learning React:
    ❌ DON'T use backend-only projects
    ✅ DO generate: "Build a virtual scrolling table component
        (performance optimization, memo, refs)"

ALWAYS follow the template structure below when generating new projects.
This ensures consistent quality and difficulty calibration.
```

---

## 📋 PROJECT TEMPLATE STRUCTURE

```yaml
PROJECT_TEMPLATE:
  name: "Project Name"
  type: [Web App | CLI Tool | API | System Design | DevOps | Library | Full Stack]
  difficulty: [Uncomfortable Beginner | Intermediate | Advanced | Expert]
  time_box: "X hours"
  
  real_world_context:
    companies: ["Companies that use this pattern"]
    why_it_matters: "Business reason this exists"
    
  skills_targeted:
    primary: ["Skill 1", "Skill 2"]
    secondary: ["Skill 3", "Skill 4"]
    
  anti_tutorial_feature: "What makes this impossible to find online"
  
  banned_libraries: ["Libraries user cannot use"]
  
  architecture:
    components: ["Component 1", "Component 2"]
    diagram: "ASCII diagram"
    
  success_criteria:
    must_have: ["Requirement 1", "Requirement 2"]
    nice_to_have: ["Bonus 1", "Bonus 2"]
    
  scaling_challenge: "Bonus challenge for production-grade"
  
  hints_allowed: ["Types of hints LLM can provide"]
```

---

## 🗄️ PROJECT DATABASE (EXAMPLES & INSPIRATION)

> **Note to LLM**: These are example projects that demonstrate the quality and structure expected.
> Use them when appropriate, but CREATE NEW PROJECTS when the user's learning path requires it.
> Think of these as your training data for generating new projects.

### PROJECT 1: Distributed Rate Limiter
```yaml
name: "Build a Distributed Rate Limiter from Scratch"
type: API
difficulty: Intermediate
time_box: "15 hours"

real_world_context:
  companies: ["Stripe", "GitHub API", "Twitter API"]
  why_it_matters: |
    Every production API needs rate limiting to prevent abuse and ensure 
    fair usage. Stripe's rate limiter handles millions of requests while
    maintaining sub-millisecond latency. Understanding this is essential
    for any backend role.

skills_targeted:
  primary: ["Redis", "Middleware patterns", "Algorithm design"]
  secondary: ["HTTP headers", "Distributed systems", "Testing"]

anti_tutorial_feature: |
  Most tutorials use express-rate-limit. You're building the algorithm
  (sliding window log or token bucket) from scratch, AND making it work
  across multiple server instances using Redis.

banned_libraries: ["express-rate-limit", "rate-limiter-flexible", "bottleneck"]

architecture:
  components:
    - "Rate limiting middleware"
    - "Redis client wrapper"
    - "Rate limit algorithm implementation"
    - "Response formatter (headers)"
  diagram: |
    ┌────────────┐     ┌─────────────────┐     ┌────────────┐
    │   Client   │────▶│   Your API      │────▶│  Handler   │
    └────────────┘     │   Middleware    │     └────────────┘
                       └────────┬────────┘
                                │
                       ┌────────▼────────┐
                       │     Redis       │
                       │  (distributed   │
                       │   state store)  │
                       └─────────────────┘

success_criteria:
  must_have:
    - "100 requests per minute per API key"
    - "Sliding window algorithm (not fixed window)"
    - "Returns 429 with Retry-After header"
    - "X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset headers"
    - "Works across multiple server instances"
    - "Sub-10ms overhead per request"
  nice_to_have:
    - "Different limits for different endpoints"
    - "Graceful degradation if Redis is down"
    - "Admin endpoint to check/reset limits"

scaling_challenge: |
  "Your rate limiter now needs to handle 50,000 requests/second across
  10 server instances with 99.9% consistency. Redis is becoming a bottleneck.
  How do you redesign it?"

hints_allowed:
  - "Explanation of sliding window vs token bucket algorithms"
  - "Redis data structure suggestions (sorted sets, strings)"
  - "Middleware function signature guidance"
```

---

### PROJECT 2: Real-Time Collaborative Text Editor
```yaml
name: "Build a Mini Google Docs (Collaborative Editor)"
type: Full Stack
difficulty: Advanced
time_box: "25 hours"

real_world_context:
  companies: ["Google Docs", "Notion", "Figma"]
  why_it_matters: |
    Real-time collaboration is one of the hardest problems in software.
    Google Docs uses Operational Transformation, Figma uses CRDTs.
    Understanding conflict resolution and real-time sync separates
    senior engineers from juniors.

skills_targeted:
  primary: ["WebSockets", "Operational Transformation OR CRDTs", "State management"]
  secondary: ["Event sourcing", "Cursor sync", "DOM manipulation"]

anti_tutorial_feature: |
  You cannot use Yjs, Automerge, or any CRDT library. You must implement
  conflict resolution yourself. This means understanding the actual
  algorithms, not just calling library functions.

banned_libraries: ["yjs", "automerge", "sharedb", "ot.js"]

architecture:
  components:
    - "WebSocket server with room management"
    - "Operational transformation engine"
    - "Client-side document state"
    - "Cursor position broadcasting"
    - "Operation history for undo"
  diagram: |
    ┌──────────┐     ┌──────────┐     ┌──────────┐
    │ Client A │     │ Client B │     │ Client C │
    └────┬─────┘     └────┬─────┘     └────┬─────┘
         │                │                │
         └───────────┬────┴────────────────┘
                     ▼
              ┌──────────────┐
              │   WebSocket  │
              │    Server    │
              └──────┬───────┘
                     │
              ┌──────▼───────┐
              │  OT Engine   │
              │  (transform  │
              │   & merge)   │
              └──────┬───────┘
                     │
              ┌──────▼───────┐
              │  Document    │
              │   State      │
              └──────────────┘

success_criteria:
  must_have:
    - "Two users can edit same document simultaneously"
    - "Changes appear in real-time (< 100ms latency)"
    - "No conflicts when users type in same location"
    - "Cursor positions visible to other users"
    - "Document state consistent across all clients"
    - "Reconnection handles missed operations"
  nice_to_have:
    - "Undo/redo that works correctly with concurrent edits"
    - "Presence indicators (who's viewing)"
    - "Operation history/playback"

scaling_challenge: |
  "Your document now has 100 concurrent editors. The server is becoming
  a bottleneck. How do you shard the document? How do you handle an
  editor in New York and one in Tokyo with 200ms latency between them?"

hints_allowed:
  - "Conceptual explanation of OT insert/delete transforms"
  - "WebSocket room management patterns"
  - "State synchronization strategies"
```

---

### PROJECT 3: Job Queue System
```yaml
name: "Build a Reliable Job Queue from Scratch"
type: System Design
difficulty: Intermediate
time_box: "18 hours"

real_world_context:
  companies: ["Shopify (Sidekiq)", "GitHub (Resque)", "Stripe"]
  why_it_matters: |
    Every production system needs background job processing. Sending emails,
    processing payments, generating reports—all happen in job queues.
    Understanding queues, retries, and failure handling is essential.

skills_targeted:
  primary: ["Queue data structures", "Worker patterns", "Reliability engineering"]
  secondary: ["Redis", "Concurrency", "Monitoring"]

anti_tutorial_feature: |
  No Bull, no Celery, no Sidekiq. You implement the queue, workers,
  retry logic, and dead-letter queues yourself. Most devs have never
  seen inside these systems.

banned_libraries: ["bull", "bullmq", "agenda", "bee-queue", "celery"]

architecture:
  components:
    - "Job queue (Redis-backed)"
    - "Worker pool manager"
    - "Retry handler with exponential backoff"
    - "Dead-letter queue"
    - "Job status tracker"
  diagram: |
    ┌───────────┐     ┌──────────────┐     ┌──────────────┐
    │ Producer  │────▶│  Job Queue   │────▶│   Workers    │
    │  (API)    │     │   (Redis)    │     │   (Pool)     │
    └───────────┘     └──────────────┘     └──────┬───────┘
                                                  │
                            ┌─────────────────────┼──────────────────┐
                            │                     │                  │
                            ▼                     ▼                  ▼
                      ┌──────────┐         ┌──────────┐       ┌──────────┐
                      │ Success  │         │  Retry   │       │  Dead    │
                      │  Queue   │         │  Queue   │       │ Letters  │
                      └──────────┘         └──────────┘       └──────────┘

success_criteria:
  must_have:
    - "Jobs processed in order (FIFO)"
    - "Failed jobs retry with exponential backoff (max 3 retries)"
    - "Jobs move to dead-letter queue after max retries"
    - "Multiple workers can process concurrently"
    - "No job is lost if worker crashes mid-processing"
    - "Job status queryable (pending, processing, completed, failed)"
  nice_to_have:
    - "Job priorities"
    - "Scheduled jobs (run at specific time)"
    - "Job dependencies (job B waits for job A)"

scaling_challenge: |
  "Your queue now needs to handle 10,000 jobs/second with guaranteed
  exactly-once processing. How do you prevent duplicate processing
  when workers crash? How do you distribute across multiple machines?"

hints_allowed:
  - "Redis data structure choices (lists vs sorted sets)"
  - "Exponential backoff formula"
  - "Worker heartbeat patterns"
```

---

### PROJECT 4: Custom ORM Layer
```yaml
name: "Build a Type-Safe ORM from Scratch"
type: Library
difficulty: Advanced
time_box: "20 hours"

real_world_context:
  companies: ["Prisma", "TypeORM creators", "Drizzle"]
  why_it_matters: |
    ORMs abstract database complexity but most devs don't understand
    how they work. Building one teaches query building, connection pooling,
    and the N+1 problem intimately.

skills_targeted:
  primary: ["Query builders", "Database connections", "TypeScript generics"]
  secondary: ["SQL generation", "Connection pooling", "Migrations"]

anti_tutorial_feature: |
  No existing ORM tutorials teach you to build one. You'll learn
  how Prisma generates types, how query builders chain, and why
  ORMs make the decisions they do.

banned_libraries: ["prisma", "typeorm", "sequelize", "drizzle-orm", "knex"]

architecture:
  components:
    - "Schema definition DSL"
    - "Query builder with method chaining"
    - "SQL generator"
    - "Connection pool manager"
    - "Result mapper (DB rows → objects)"
  diagram: |
    ┌────────────────┐
    │  Schema DSL    │
    │  (define       │
    │   tables)      │
    └───────┬────────┘
            │
    ┌───────▼────────┐     ┌─────────────────┐
    │ Query Builder  │────▶│  SQL Generator  │
    │ .where().      │     │  (produces SQL  │
    │  select()      │     │   strings)      │
    └───────┬────────┘     └────────┬────────┘
            │                       │
    ┌───────▼───────────────────────▼────┐
    │         Connection Pool            │
    │    (manages DB connections)        │
    └───────────────┬────────────────────┘
                    │
    ┌───────────────▼────────────────────┐
    │           PostgreSQL               │
    └────────────────────────────────────┘

success_criteria:
  must_have:
    - "Define schemas: orm.define('users', { id: 'int', name: 'string' })"
    - "Query builder: orm.users.where({ id: 1 }).select('name')"
    - "Method chaining works"
    - "Prevents SQL injection"
    - "TypeScript knows return types based on select()"
    - "Basic relations (belongsTo, hasMany)"
  nice_to_have:
    - "Connection pooling"
    - "Transaction support"
    - "Migration generator"

scaling_challenge: |
  "Your ORM is now used in a high-traffic application. How do you
  prevent N+1 queries? How do you implement efficient eager loading?
  How do you handle connection pool exhaustion under load?"

hints_allowed:
  - "TypeScript generic patterns for type inference"
  - "SQL injection prevention techniques"
  - "Query builder design patterns"
```

---

### PROJECT 5: CLI Framework
```yaml
name: "Build a CLI Framework (like Commander.js)"
type: CLI Tool
difficulty: Intermediate
time_box: "12 hours"

real_world_context:
  companies: ["Vercel (Next.js CLI)", "Facebook (React CLI)", "Heroku"]
  why_it_matters: |
    Developer tools are built on CLI frameworks. Understanding argument
    parsing, help generation, and command routing is essential for
    building professional dev tools.

skills_targeted:
  primary: ["Argument parsing", "Command patterns", "Terminal I/O"]
  secondary: ["Plugin architecture", "Help generation", "Input validation"]

anti_tutorial_feature: |
  Instead of USING Commander or Yargs, you BUILD one. You'll understand
  how argument parsing actually works, how help text is generated,
  and how subcommands are routed.

banned_libraries: ["commander", "yargs", "meow", "oclif", "caporal"]

architecture:
  components:
    - "Argument tokenizer"
    - "Command registry"
    - "Option parser"
    - "Help generator"
    - "Command executor"
  diagram: |
    "mycli deploy --env production --verbose"
                        │
                ┌───────▼───────┐
                │   Tokenizer   │
                │  (splits args)│
                └───────┬───────┘
                        │
                ┌───────▼───────┐     ┌──────────────┐
                │    Router     │────▶│   Command    │
                │  (finds cmd)  │     │   Registry   │
                └───────┬───────┘     └──────────────┘
                        │
                ┌───────▼───────┐
                │ Option Parser │
                │ (--env=prod)  │
                └───────┬───────┘
                        │
                ┌───────▼───────┐
                │   Execute     │
                │  (run handler)│
                └───────────────┘

success_criteria:
  must_have:
    - "Define commands: cli.command('deploy', handler)"
    - "Options: --env production or -e production"
    - "Flags: --verbose or -v"
    - "Auto-generated help: mycli --help, mycli deploy --help"
    - "Required vs optional arguments"
    - "Subcommands: mycli db migrate"
  nice_to_have:
    - "Aliases (deploy / d)"
    - "Input prompts for missing required args"
    - "Colored output"

scaling_challenge: |
  "Your CLI framework now needs plugin support. How do you let third
  parties add commands without modifying core code? How do you handle
  command name conflicts between plugins?"

hints_allowed:
  - "process.argv parsing strategies"
  - "Regex patterns for option parsing"
  - "Help text formatting approaches"
```

---

### PROJECT 6: In-Memory Cache with Eviction
```yaml
name: "Build a Production-Grade In-Memory Cache"
type: Library
difficulty: Intermediate
time_box: "10 hours"

real_world_context:
  companies: ["Redis internals", "Memcached", "Any app with caching"]
  why_it_matters: |
    Caching is everywhere. Understanding LRU eviction, TTL management,
    and cache invalidation patterns is fundamental to building
    performant applications.

skills_targeted:
  primary: ["LRU algorithm", "Hash maps", "TTL management"]
  secondary: ["Memory management", "Data structures", "Concurrency"]

anti_tutorial_feature: |
  Most devs use Redis without understanding how eviction works.
  You'll implement LRU using doubly-linked lists and hash maps—the
  actual algorithm Redis uses internally.

banned_libraries: ["lru-cache", "node-cache", "quick-lru"]

architecture:
  components:
    - "Hash map for O(1) lookup"
    - "Doubly-linked list for LRU ordering"
    - "TTL tracker"
    - "Eviction engine"
  diagram: |
    ┌─────────────────────────────────────────────────┐
    │                  Hash Map                       │
    │  key1 ──▶ node1    key2 ──▶ node2    ...       │
    └─────────────────────────────────────────────────┘
                    │              │
                    ▼              ▼
    ┌──────────────────────────────────────────────────┐
    │            Doubly-Linked List (LRU order)        │
    │  HEAD ◀──▶ node1 ◀──▶ node2 ◀──▶ ... ◀──▶ TAIL  │
    │  (most recent)              (least recent)       │
    └──────────────────────────────────────────────────┘

success_criteria:
  must_have:
    - "O(1) get and set operations"
    - "LRU eviction when capacity exceeded"
    - "TTL support: cache.set(key, value, { ttl: 5000 })"
    - "Manual invalidation: cache.delete(key)"
    - "Bulk operations: cache.clear()"
    - "Size limits (by count or memory)"
  nice_to_have:
    - "LFU (Least Frequently Used) as alternative policy"
    - "Stats: hit rate, miss rate, eviction count"
    - "Event callbacks: onEvict, onExpire"

scaling_challenge: |
  "Your cache is now used in a multi-threaded environment. How do you
  make it thread-safe without destroying performance? How do you handle
  cache stampede (many requests hitting expired key simultaneously)?"

hints_allowed:
  - "Doubly-linked list operations for LRU"
  - "TTL checking strategies (lazy vs active)"
  - "Hash map + linked list combination pattern"
```

---

### PROJECT 7: API Gateway
```yaml
name: "Build an API Gateway with Plugin Architecture"
type: API
difficulty: Advanced
time_box: "22 hours"

real_world_context:
  companies: ["Kong", "AWS API Gateway", "Netflix Zuul"]
  why_it_matters: |
    API gateways are the front door to microservices. Understanding
    routing, authentication, rate limiting, and request transformation
    at the gateway level is critical for distributed systems.

skills_targeted:
  primary: ["Reverse proxy", "Plugin architecture", "Request routing"]
  secondary: ["Load balancing", "Circuit breakers", "Request transformation"]

anti_tutorial_feature: |
  You're building the gateway, not using one. This means implementing
  the proxy, the plugin system, and the routing rules yourself.

banned_libraries: ["express-gateway", "kong", "http-proxy-middleware (for core logic)"]

architecture:
  components:
    - "HTTP proxy server"
    - "Route matcher"
    - "Plugin pipeline"
    - "Upstream manager"
    - "Request/Response transformers"
  diagram: |
    ┌──────────┐     ┌─────────────────────────────────────┐
    │  Client  │────▶│           API Gateway               │
    └──────────┘     │  ┌─────────────────────────────┐    │
                     │  │      Plugin Pipeline        │    │
                     │  │  ┌─────┐ ┌─────┐ ┌─────┐   │    │
                     │  │  │Auth │▶│Rate │▶│Log  │   │    │
                     │  │  │     │ │Limit│ │     │   │    │
                     │  │  └─────┘ └─────┘ └─────┘   │    │
                     │  └─────────────────────────────┘    │
                     └──────────────┬──────────────────────┘
                                    │
                     ┌──────────────┼──────────────┐
                     ▼              ▼              ▼
              ┌──────────┐  ┌──────────┐  ┌──────────┐
              │ Service  │  │ Service  │  │ Service  │
              │    A     │  │    B     │  │    C     │
              └──────────┘  └──────────┘  └──────────┘

success_criteria:
  must_have:
    - "Route matching: /api/users/* → user-service"
    - "Plugin system: gateway.use(authPlugin)"
    - "Request forwarding with header manipulation"
    - "Health checks for upstream services"
    - "At least 3 built-in plugins (auth, rate-limit, logging)"
    - "Configuration via JSON/YAML file"
  nice_to_have:
    - "Load balancing (round-robin)"
    - "Circuit breaker for failing upstreams"
    - "Request/response transformation"

scaling_challenge: |
  "Your gateway handles 100,000 requests/second. How do you prevent
  it from becoming a single point of failure? How do you update
  routing rules without downtime? How do you handle plugin failures
  gracefully?"

hints_allowed:
  - "HTTP proxy implementation patterns"
  - "Plugin pipeline design (middleware chain)"
  - "Route matching algorithms (trie, regex)"
```

---

### PROJECT 8: Real-Time Analytics Pipeline
```yaml
name: "Build a Real-Time Event Analytics System"
type: System Design
difficulty: Advanced
time_box: "25 hours"

real_world_context:
  companies: ["Mixpanel", "Amplitude", "Segment"]
  why_it_matters: |
    Every SaaS product needs analytics. Understanding how to ingest
    millions of events, process them in real-time, and query aggregations
    efficiently is crucial for data-driven products.

skills_targeted:
  primary: ["Event streaming", "Time-series data", "Aggregations"]
  secondary: ["Batch vs stream processing", "Data modeling", "Query optimization"]

anti_tutorial_feature: |
  You're building the pipeline, not using Google Analytics. This means
  event ingestion, storage strategy, and real-time aggregation from scratch.

banned_libraries: ["segment", "mixpanel", "amplitude (client SDKs are fine)"]

architecture:
  components:
    - "Event ingestion API"
    - "Event queue (buffering)"
    - "Stream processor"
    - "Time-series storage"
    - "Query engine for aggregations"
  diagram: |
    ┌────────────┐     ┌────────────┐     ┌────────────────┐
    │   Events   │────▶│  Ingestion │────▶│     Queue      │
    │ (from apps)│     │    API     │     │   (buffer)     │
    └────────────┘     └────────────┘     └───────┬────────┘
                                                  │
                                          ┌───────▼────────┐
                                          │    Stream      │
                                          │   Processor    │
                                          └───────┬────────┘
                                                  │
                       ┌──────────────────────────┼────────────────┐
                       ▼                          ▼                ▼
                ┌─────────────┐          ┌─────────────┐   ┌─────────────┐
                │  Raw Event  │          │ Aggregates  │   │  Real-time  │
                │   Storage   │          │  (rollups)  │   │  Dashboard  │
                └─────────────┘          └─────────────┘   └─────────────┘

success_criteria:
  must_have:
    - "Ingest 1000 events/second"
    - "Events stored with timestamp, event type, properties"
    - "Real-time aggregations: count, unique users, avg per minute"
    - "Query API: events in last hour, daily active users"
    - "Pre-computed rollups (minute, hour, day granularity)"
    - "Retention policy (auto-delete old raw events)"
  nice_to_have:
    - "Funnel analysis (A → B → C conversion)"
    - "Cohort analysis"
    - "Real-time dashboard updates via WebSocket"

scaling_challenge: |
  "Your system now ingests 1 million events/second. Raw storage is
  exploding. How do you sample without losing accuracy? How do you
  handle late-arriving events? How do you make queries fast on
  billions of rows?"

hints_allowed:
  - "Time-series storage patterns"
  - "Pre-aggregation strategies"
  - "Event buffering approaches"
```

---

### PROJECT 9: Zero-Downtime Deployment Pipeline
```yaml
name: "Build a Blue-Green Deployment System"
type: DevOps
difficulty: Advanced
time_box: "20 hours"

real_world_context:
  companies: ["Netflix", "Amazon", "Facebook"]
  why_it_matters: |
    Production systems can't have downtime. Understanding blue-green
    deployments, health checks, and automated rollbacks separates
    DevOps engineers from script runners.

skills_targeted:
  primary: ["Deployment strategies", "Load balancer control", "Health checks"]
  secondary: ["Docker", "Scripting", "Monitoring integration"]

anti_tutorial_feature: |
  You're building the deployment system, not using Kubernetes or AWS
  CodeDeploy. You'll implement the traffic switching, health verification,
  and rollback logic yourself.

banned_libraries: ["kubernetes (for deployment logic)", "aws-codedeploy"]

architecture:
  components:
    - "Deployment orchestrator"
    - "Health check system"
    - "Load balancer controller"
    - "Rollback mechanism"
    - "Deployment state machine"
  diagram: |
                     ┌──────────────────┐
                     │   Load Balancer  │
                     │  (nginx/HAProxy) │
                     └────────┬─────────┘
                              │
              ┌───────────────┼───────────────┐
              │               │               │
              ▼               ▼               │
    ┌──────────────┐  ┌──────────────┐        │
    │    BLUE      │  │    GREEN     │        │
    │  (current)   │  │   (new)      │        │
    │   100%       │  │    0%        │        │
    └──────────────┘  └──────────────┘        │
                              │               │
                              ▼               │
                     ┌──────────────┐         │
                     │   Health     │─────────┘
                     │   Checks     │  (if fail, rollback)
                     └──────────────┘

success_criteria:
  must_have:
    - "Deploy new version to 'green' environment"
    - "Run health checks against green"
    - "Switch traffic from blue to green (zero downtime)"
    - "Automated rollback if health checks fail post-switch"
    - "CLI: deploy.sh --version 1.2.3"
    - "Deployment state tracking (deploying, live, rolled-back)"
  nice_to_have:
    - "Canary deployment (10% traffic first)"
    - "Slack/webhook notifications"
    - "Deployment history and audit log"

scaling_challenge: |
  "Your system now deploys to 100 servers across 3 regions. How do
  you coordinate? How do you handle partial failures? How do you
  implement feature flags for gradual rollouts?"

hints_allowed:
  - "nginx upstream configuration patterns"
  - "Health check endpoint design"
  - "State machine design for deployment stages"
```

---

### PROJECT 10: Full-Text Search Engine
```yaml
name: "Build a Full-Text Search Engine"
type: Library
difficulty: Expert
time_box: "30 hours"

real_world_context:
  companies: ["Elasticsearch", "Algolia", "Meilisearch"]
  why_it_matters: |
    Search is a core feature of most applications. Understanding
    inverted indexes, tokenization, and relevance ranking is essential
    for building fast, relevant search experiences.

skills_targeted:
  primary: ["Inverted index", "Tokenization", "TF-IDF ranking"]
  secondary: ["Fuzzy matching", "Query parsing", "Performance optimization"]

anti_tutorial_feature: |
  No Elasticsearch, no Algolia. You build the index, the tokenizer,
  and the ranking algorithm. You'll understand why search engines
  make the decisions they do.

banned_libraries: ["elasticsearch", "algolia", "meilisearch", "lunr"]

architecture:
  components:
    - "Document indexer"
    - "Tokenizer/Analyzer"
    - "Inverted index storage"
    - "Query parser"
    - "Ranking engine (TF-IDF)"
  diagram: |
    ┌─────────────┐     ┌─────────────┐     ┌─────────────────┐
    │  Documents  │────▶│  Tokenizer  │────▶│ Inverted Index  │
    │   (input)   │     │  (analyze)  │     │   (storage)     │
    └─────────────┘     └─────────────┘     └────────┬────────┘
                                                     │
    ┌─────────────┐     ┌─────────────┐     ┌────────▼────────┐
    │   Query     │────▶│   Query     │────▶│     Ranker      │
    │  (search)   │     │   Parser    │     │   (TF-IDF)      │
    └─────────────┘     └─────────────┘     └────────┬────────┘
                                                     │
                                            ┌────────▼────────┐
                                            │    Results      │
                                            │  (sorted by     │
                                            │   relevance)    │
                                            └─────────────────┘

success_criteria:
  must_have:
    - "Index documents: search.index({ id: 1, title: '...', body: '...' })"
    - "Search: search.query('javascript tutorial')"
    - "Relevance ranking (TF-IDF or BM25)"
    - "Multi-field search (title weighted higher than body)"
    - "Sub-100ms search on 10,000 documents"
    - "Tokenization: lowercase, stop words removal, stemming"
  nice_to_have:
    - "Fuzzy search (handle typos)"
    - "Phrase search ('exact phrase')"
    - "Faceted search (filter by category)"

scaling_challenge: |
  "Your search engine now indexes 10 million documents. How do you
  shard the index? How do you handle real-time updates without
  rebuilding? How do you maintain sub-100ms latency at scale?"

hints_allowed:
  - "Inverted index data structure design"
  - "TF-IDF formula explanation"
  - "Tokenization pipeline stages"
```

---

### PROJECT 11: WebSocket Multiplayer Game Server
```yaml
name: "Build a Multiplayer Game Server"
type: Full Stack
difficulty: Intermediate
time_box: "18 hours"

real_world_context:
  companies: ["Riot Games", "Supercell", "Discord"]
  why_it_matters: |
    Real-time multiplayer systems are the hardest distributed systems
    problems. Understanding state sync, latency compensation, and
    authoritative servers is valuable beyond gaming.

skills_targeted:
  primary: ["WebSockets", "Game loop", "State synchronization"]
  secondary: ["Latency compensation", "Room management", "Anti-cheat basics"]

anti_tutorial_feature: |
  Most game tutorials are single-player. You're building the server
  that handles multiple players, validates moves, and keeps everyone
  in sync—the hard part.

banned_libraries: ["socket.io (use raw WebSocket)", "colyseus", "geckos.io"]

architecture:
  components:
    - "WebSocket server"
    - "Room manager"
    - "Game state manager"
    - "Tick-based game loop"
    - "Client prediction reconciliation"
  diagram: |
    ┌──────────┐  ┌──────────┐  ┌──────────┐
    │ Player 1 │  │ Player 2 │  │ Player 3 │
    └────┬─────┘  └────┬─────┘  └────┬─────┘
         │             │             │
         └─────────────┼─────────────┘
                       │
              ┌────────▼────────┐
              │  Game Server    │
              │  ┌────────────┐ │
              │  │ Room: xyz  │ │
              │  │ ┌────────┐ │ │
              │  │ │ State  │ │ │
              │  │ └────────┘ │ │
              │  └────────────┘ │
              └─────────────────┘
                       │
              ┌────────▼────────┐
              │    Game Loop    │
              │  (60 ticks/sec) │
              └─────────────────┘

success_criteria:
  must_have:
    - "Multiple players in same room"
    - "Server-authoritative game state"
    - "60 tick/second game loop"
    - "Client input → server validation → state broadcast"
    - "Latency display for each player"
    - "Player disconnect handling"
  nice_to_have:
    - "Client-side prediction"
    - "Lag compensation"
    - "Spectator mode"

scaling_challenge: |
  "Your game server now has 10,000 concurrent games. How do you
  distribute across servers? How do you handle a player switching
  servers mid-game? How do you prevent cheating at the network level?"

hints_allowed:
  - "Game loop timing patterns"
  - "State snapshot vs delta approaches"
  - "WebSocket room management patterns"
```

---

### PROJECT 12: Container Orchestrator (Mini Kubernetes)
```yaml
name: "Build a Simple Container Orchestrator"
type: DevOps
difficulty: Expert
time_box: "35 hours"

real_world_context:
  companies: ["Kubernetes creators", "Docker Swarm", "Nomad"]
  why_it_matters: |
    Container orchestration is the backbone of modern infrastructure.
    Understanding scheduling, health checks, and service discovery
    at this level makes you dangerous in DevOps interviews.

skills_targeted:
  primary: ["Container management", "Scheduling algorithms", "Distributed systems"]
  secondary: ["Service discovery", "Health monitoring", "REST API design"]

anti_tutorial_feature: |
  Instead of using Kubernetes, you understand how it works by building
  a simplified version. This is the kind of project that makes
  interviewers go "whoa."

banned_libraries: ["kubernetes client", "docker swarm mode"]

architecture:
  components:
    - "Control plane (API server)"
    - "Scheduler"
    - "Node agents"
    - "Service discovery"
    - "Health checker"
  diagram: |
    ┌─────────────────────────────────────────────────────────┐
    │                    Control Plane                        │
    │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
    │  │ API Server  │  │  Scheduler  │  │  Registry   │     │
    │  └─────────────┘  └─────────────┘  └─────────────┘     │
    └─────────────────────────┬───────────────────────────────┘
                              │
           ┌──────────────────┼──────────────────┐
           │                  │                  │
           ▼                  ▼                  ▼
    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
    │   Node 1    │    │   Node 2    │    │   Node 3    │
    │ ┌─────────┐ │    │ ┌─────────┐ │    │ ┌─────────┐ │
    │ │Container│ │    │ │Container│ │    │ │Container│ │
    │ │Container│ │    │ │Container│ │    │ │         │ │
    │ └─────────┘ │    │ └─────────┘ │    │ └─────────┘ │
    └─────────────┘    └─────────────┘    └─────────────┘

success_criteria:
  must_have:
    - "Deploy containers via API: POST /deploy {image, replicas}"
    - "Scheduler places containers on nodes (least-loaded)"
    - "Health checks restart failed containers"
    - "Scale up/down: PATCH /deploy/:id {replicas: 5}"
    - "Service discovery: containers can find each other by name"
    - "Basic CLI: orch deploy nginx --replicas 3"
  nice_to_have:
    - "Rolling updates"
    - "Resource limits (CPU, memory)"
    - "Node failure handling (reschedule containers)"

scaling_challenge: |
  "Your orchestrator now manages 1,000 nodes and 50,000 containers.
  The scheduler is a bottleneck. How do you make scheduling distributed?
  How do you handle network partitions between control plane and nodes?"

hints_allowed:
  - "Docker API basics"
  - "Scheduling algorithm concepts (bin-packing, spread)"
  - "Health check patterns"
```

---

## 🎚️ PROJECT SELECTION ALGORITHM

```
WHEN_ASSIGNING_PROJECT:

1. Check user's current phase (from master_orchestrator.md)
2. Review identified weakness areas
3. Analyze what user is currently learning (language, framework, concept)
4. DECIDE:
   
   OPTION A - USE DATABASE PROJECT:
     IF database has a project that perfectly fits current learning + weaknesses
     AND user hasn't done it before
     → Select and adapt as needed
   
   OPTION B - GENERATE NEW PROJECT:
     IF no database project fits well
     OR user's learning topic isn't covered
     OR you can create something more targeted
     → Generate new project using template structure
     → Follow all ANTI-TUTORIAL HELL PRINCIPLES
     → Ensure it targets user's specific gaps
   
5. ALWAYS ensure project:
   - Matches difficulty to phase
   - Targets at least one weakness area
   - Forces understanding of internals (ban convenience libraries)
   - Has clear success criteria
   - Includes production context
6. Adapt project if needed:
   - If user is advanced → Add constraints
   - If user is struggling → Reduce scope slightly (not difficulty)
   
ADAPTATION EXAMPLES:
  
  Too Easy:
    Original: "Build rate limiter"
    Adapted:  "Build rate limiter with sliding window AND token bucket, 
              let user choose at runtime"
  
  Too Hard:
    Original: "Build search engine with 10,000 docs"
    Adapted:  "Build search engine, start with 100 docs, scale up after 
              core working"
```

---

## 📂 MICRO-PROJECT DATABASE

For rust prevention and gap filling, use these smaller projects (4-8 hours):

```yaml
MICRO_PROJECTS:
  
  - name: "Promise.all from Scratch"
    skills: ["Promises", "Async patterns"]
    time: "4 hours"
    
  - name: "JWT Decoder/Validator"
    skills: ["Cryptography basics", "Token handling"]
    time: "3 hours"
    
  - name: "Event Emitter Implementation"
    skills: ["Pub/sub pattern", "Callbacks"]
    time: "3 hours"
    
  - name: "HTTP Router (no framework)"
    skills: ["HTTP parsing", "Routing patterns"]
    time: "5 hours"
    
  - name: "Debounce/Throttle Functions"
    skills: ["Timing", "Closures"]
    time: "2 hours"
    
  - name: "Middleware Pipeline"
    skills: ["Function composition", "Next pattern"]
    time: "4 hours"
    
  - name: "Connection Pool"
    skills: ["Resource management", "Async coordination"]
    time: "6 hours"
    
  - name: "Retry with Exponential Backoff"
    skills: ["Error handling", "Timing patterns"]
    time: "3 hours"
    
  - name: "Simple Pub/Sub System"
    skills: ["Event patterns", "Decoupling"]
    time: "4 hours"
    
  - name: "Configuration Loader"
    skills: ["File parsing", "Environment handling"]
    time: "3 hours"
```

---

## 🎨 HOW TO GENERATE NEW PROJECTS (LLM GUIDE)

When the user's learning needs aren't met by database projects, generate new ones following this process:

### Step 1: Analyze Learning Context
```
QUESTIONS TO ASK YOURSELF:
  - What language/framework/concept is the user learning?
  - What specific skills are they weak in (from master_orchestrator.md)?
  - What phase are they in (Foundation, Immersion, Deepening, Production)?
  - What have they already built?
  - What would challenge them WITHOUT overwhelming them?
```

### Step 2: Generate Project Idea
```
FOLLOW THIS FORMULA:

"Build a [THING] that [CORE CHALLENGE] without using [COMMON LIBRARY]"

EXAMPLES:

Learning Python + weak on concurrency:
  → "Build a concurrent download manager that handles 100 files simultaneously
     without using asyncio (raw threads + queue)"

Learning React + weak on performance:
  → "Build an infinite-scroll feed with virtualization that smoothly handles
     10,000 items without using react-window"

Learning Rust + weak on ownership:
  → "Build a memory-safe circular buffer that prevents data races
     without using unsafe blocks"

Learning System Design + weak on distributed systems:
  → "Design and implement a distributed cache with consistent hashing
     and replication across 3 nodes"
```

### Step 3: Fill Out Template
```
Use the PROJECT_TEMPLATE structure from the top of this file.

CRITICAL ELEMENTS:

1. real_world_context:
   - Name 2-3 companies that solve this problem
   - Explain WHY this matters in production
   - Make it clear this isn't a toy problem

2. anti_tutorial_feature:
   - What makes this different from online tutorials?
   - Usually it's: building the internals instead of using libraries

3. banned_libraries:
   - Force user to understand HOW things work
   - Example: Learning Express? Ban express, use raw http module
   - Example: Learning state management? Ban Redux, build your own

4. success_criteria:
   - Make it MEASURABLE: "Handles 1000 req/sec" not "Fast"
   - Include edge cases: "Works with empty input", "Handles disconnects"
   - Make must_have achievable in time_box, nice_to_have for extra credit

5. scaling_challenge:
   - Always ask: "Now make it handle 10x [users/data/traffic/complexity]"
   - This forces production thinking
```

### Step 4: Quality Checks
```
BEFORE PRESENTING PROJECT TO USER:

✓ Does it target their specific weakness areas?
✓ Is it impossible to just Google the solution?
✓ Does it force understanding of internals?
✓ Is the success criteria clear and measurable?
✓ Is there a production context (real companies do this)?
✓ Does it match the difficulty of their current phase?
✓ Is the time box realistic but challenging?
✓ Does it include a scaling challenge?

If ANY check fails → Revise the project before presenting.
```

### Step 5: Present with Context
```
Don't just dump the project specs.

PRESENTATION STRUCTURE:

1. Hook: Why this matters
   "At [Company], engineers face [Problem]. You're going to solve it."

2. The Challenge: What they're building
   "Build [X] that does [Y]"

3. The Constraint: What makes it hard
   "You cannot use [Library]. You must implement [Internals]."

4. Success Metrics: How they know they're done
   "It must: [Requirement 1], [Requirement 2], [Requirement 3]"

5. Time Box: Urgency
   "You have [X] hours. Start now."
```

### Real Examples of Generated Projects

```yaml
EXAMPLE 1: User learning Vue.js, weak on reactivity systems

name: "Build a Reactive State Manager from Scratch"
type: Library
difficulty: Intermediate
time_box: "12 hours"

real_world_context:
  companies: ["Vue.js internals", "MobX", "Svelte"]
  why_it_matters: |
    Understanding reactivity is the difference between using a framework
    and mastering it. Vue, Svelte, and Solid.js all use reactive systems.
    Building one teaches you how state updates propagate.

skills_targeted:
  primary: ["Proxies", "Dependency tracking", "Effect systems"]
  secondary: ["Getters/setters", "WeakMap usage", "Performance"]

anti_tutorial_feature: |
  You can't use Vue or any reactive library. You implement the Proxy-based
  tracking that makes computed properties and watchers work automatically.

banned_libraries: ["vue", "mobx", "@vue/reactivity", "solid-js"]

success_criteria:
  must_have:
    - "state.count changes trigger dependent computed properties"
    - "Multiple watchers can observe same property"
    - "No manual dependency registration (automatic tracking)"
    - "Works with nested objects"
  nice_to_have:
    - "Batch updates (no redundant triggers)"
    - "Cleanup when watchers removed"

scaling_challenge: |
  "Your state tree now has 10,000 properties and 1,000 watchers.
  How do you prevent performance degradation?"

---

EXAMPLE 2: User learning Golang, weak on concurrency patterns

name: "Build a Worker Pool with Graceful Shutdown"
type: System Design
difficulty: Intermediate
time_box: "10 hours"

real_world_context:
  companies: ["Every backend service at scale"]
  why_it_matters: |
    Worker pools are how production systems process work in parallel.
    Understanding channels, goroutines, and graceful shutdown is
    essential for any Go backend engineer.

skills_targeted:
  primary: ["Channels", "Goroutines", "Context", "sync.WaitGroup"]
  secondary: ["Select statements", "Graceful shutdown", "Backpressure"]

anti_tutorial_feature: |
  Most tutorials show toy examples. You're building production-grade:
  dynamic pool sizing, graceful shutdown with draining, and panic recovery.

banned_libraries: ["gammazero/workerpool", "alitto/pond"]

success_criteria:
  must_have:
    - "Process 10,000 tasks across N workers"
    - "Dynamically scale workers based on queue size"
    - "Graceful shutdown: finish in-progress tasks, reject new ones"
    - "Panic in one worker doesn't kill the pool"
  nice_to_have:
    - "Metrics: tasks processed, workers active, queue size"
    - "Timeout for tasks that run too long"

scaling_challenge: |
  "Your tasks are coming from Kafka with 100k messages/sec.
  How do you prevent memory explosion in the queue?"
```

---

*Remember: The database projects are your reference for quality. Every generated project should meet the same standards: production context, forced internals, measurable success, anti-tutorial features, and scaling challenges.*
