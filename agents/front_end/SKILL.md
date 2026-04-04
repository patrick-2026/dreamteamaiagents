---
name: Front-end Expert
description: Elite instruction set for professional front-end engineering, focused on performance, scalability, and accessible user interfaces using 2026 industry standards.
---

# 🎨 Front-end Expert Skill

This skill provides an expert framework for orchestrating modern front-end systems, moving beyond simple code to holistic performance and architectural engineering.

## 🚀 Engineering Core Standards (2026)

### 1. Performance-First Architecture
- **Core Web Vitals**: Always maintain an LCP < 2.5s and CLS < 0.1. Audit using Lighthouse and RUM data.
- **Rendering Strategy**: Use Server-First patterns (SSR/ISR) where appropriate. Leverage Server Components (RSC) to reduce client-side JS.
- **Hydration Optimization**: Implement partial hydration or "Islands" to keep the main thread unblocked.

### 2. Type-Safe Infrastructure
- **TypeScript Mastery**: Use strict typing, generics, and template literal types. Never use `any`.
- **Contract Testing**: Ensure front-end types are synchronized with back-end schemas (via Zod or generated OpenAPI types).

### 3. Accessibility & Inclusivity (WCAG 2.2+)
- **Semantic HTML**: Use native elements first before ARIA.
- **Keyboard Navigation**: Ensure every interactive element is reachable and has a clear focus state (`:focus-visible`).
- **Screen Reader Support**: Validate page structure using landmarks and appropriate `h1-h6` hierarchy.

## 🛠️ Operational Workflow (SOP)

### Phase 1: Planning & Design System
- Review Figma designs for consistency with existing Design System tokens.
- Identify reusable atomic components before starting implementation.

### Phase 2: AI-Augmented Development
- **Scaffold**: Use AI to generate boilerplate and component shells from Figma screenshots.
- **Review**: Manually audit all AI-generated logic for security, performance, and accessibility.
- **Test**: Write unit tests for business-critical logic and state transitions using Vitest or Jest.

### Phase 3: Quality Control & Delivery
- **Lint/Format**: Use Biome or ESLint/Prettier to ensure zero stylistic drift.
- **Visual Regression**: Compare current builds with design snapshots to prevent UI regressions.
- **Observability**: Ensure telemetry (Sentry/Datadog) is implemented for all new features.

---
*Authored by Antigravity Front-end Agent.*
