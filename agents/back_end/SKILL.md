---
name: Back-end Expert
description: Advanced instruction set for mission-critical back-end development, specializing in distributed systems, high-performance APIs, and cloud-native infrastructure.
---

# ⚙️ Back-end Expert Skill

This skill is designed for engineering high-scale, resilient back-end systems that serve as the foundation for modern enterprise applications.

## 🏗️ Architectural Foundations (2025/2026)

### 1. High-Performance API Protocols
- **Decision Matrix**: Use **gRPC** for internal service-to-service communication, **GraphQL** for client-facing flexibility, and **REST** for public interoperability.
- **OpenAPI**: Maintain live, synchronized documentation (Swagger) that drives front-end type generation.

### 2. Data Persistence & Performance
- **PostgreSQL Mastery**: Implement advanced indexing, window functions, and partitioning for datasets > 1TB.
- **Caching Logic**: Multi-tier caching strategy (Application L1, Redis L2, CDN Edge) with intelligent TTL management.
- **Consistency Models**: Understanding ACID vs. BASE based on business critical path (e.g., Payments vs. Social Feed).

### 3. Distributed Readiness
- **Microservices Architecture**: Implement service mesh, dynamic service discovery, and circuit breakers (Resilience4j/Istio).
- **Event-Driven Design**: Use Kafka or RabbitMQ for asynchronous workflows and eventual consistency.

## 🛠️ Operational Workflow (SOP)

### Phase 1: System Design & Schema
- Define data models and API contracts (Proto/GraphQL Schema) before writing implementation code.
- Conduct a "Load Analysis" to identify potential bottlenecks (CPU vs. I/O bound).

### Phase 2: Development & Infrastructure-as-Code (IaC)
- Manage all infrastructure using Terraform or Pulumi.
- Ensure all deployments are containerized (Docker/Kubernetes).

### Phase 3: Testing & Resilience
- **Test Pyramid**: 80%+ Unit coverage, 100% integration coverage for critical paths.
- **Chaos Engineering**: Test system resilience by simulating network failures and service outages.
- **Security-First**: Enforce OAuth2/OIDC, zero-trust internal networking, and encryption-at-rest.

---
*Authored by Antigravity Back-end Agent.*
