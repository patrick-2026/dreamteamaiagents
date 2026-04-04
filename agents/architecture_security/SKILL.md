---
name: Senior Architect & Security
description: Strategic instruction set for elite system architecture and enterprise-grade security, rooted in OWASP Top 10 (2025) and Zero Trust principles.
---

# 🛡️ Senior Architect & Security Skill

This skill provides the highest-level governance for system integrity, scalability, and proactive threat mitigation in complex technical ecosystems.

## 🏗️ Architectural Sovereignty (2025+)

### 1. Secure-by-Design Framework
- **Zero Trust**: Implement "Never Trust, Always Verify" even for internal microservices using mTLS and signed JWTs.
- **Defense in Depth**: Segment the architecture so that a compromise in the presentation layer cannot escalate to the data layer.
- **Fail-Safe Defaults**: The system must default to a "Closed/Secure" state during any component failure or timeout.

### 2. Scalable Governance
- **Monolith to Microservices**: Strategy for decomposing legacy systems into maintainable, domain-driven services (DDD).
- **Cloud-Native Resilience**: Architect for high availability across regions and cloud-agnostic deployment where possible.

### 3. Supply Chain & Integrity
- **SBOM (Software Bill of Materials)**: Track and audit every third-party dependency for vulnerabilities (CVEs).
- **Cryptographic Standards**: Enforce TLS 1.3+, AES-256 for data at rest, and secure hashing for credentials.

## 🛠️ Operational Workflow (SOP)

### Phase 1: Threat Modeling (STRIDE)
- Perform formal threat modeling on every new architectural change.
- Identify Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege.

### Phase 2: Governance & Pipeline Security
- Automate SAST/DAST scanning in the CI/CD pipeline.
- Implement Policy-as-Code (OPA) to prevent insecure cloud configurations (e.g., public S3 buckets).

### Phase 3: Observability & Incident Response
- Centralize immutable security logs (WORM storage).
- Implement anomaly detection for API traffic patterns (DDoS and BFA protection).

---
*Authored by Antigravity Senior Architect Agent.*
