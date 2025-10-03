# Requirements Templates - Übersicht und Prozess

Dieses Verzeichnis enthält die Templates für die drei Ebenen der Requirements-Dokumentation: **Epics**, **Features** und **Issues**.

## 🎯 Template-Hierarchie mit bidirektionaler Verlinkung

```
EPIC (Strategische Ebene)
  ├── verweist auf → FEATURE 1, FEATURE 2, ...
  │
  └── FEATURE (Funktionale Ebene)
      ├── verweist zurück auf → EPIC
      ├── verweist auf → ISSUE 1, ISSUE 2, ...
      │
      └── ISSUE (Implementierungsebene)
          ├── verweist zurück auf → FEATURE
          └── verweist zurück auf → EPIC
```

**Wichtig:** Jede Ebene muss auf ihre Parent- UND Child-Items verweisen!

## 📊 EPIC Template - Strategische Ebene

**Datei:** `EPIC-TEMPLATE.md`  
**Scope:** High-Level Business Capabilities (2-6 Monate, €100k+ Impact)

### Hauptsektionen
```markdown
> Epic: EPIC-XXX
> Status: Backlog | Planning | In Progress | In Review | Done
> Priority: Strategic | High | Medium | Low
> Timeline: Q1 2025
> Total Story Points: [Summe aller Features]

## Business Goal
## Target Personas  
## Business Value & Success Metrics (mit ROI)
## Related Features (3-15 Features)
   - FEATURE-001 ✅ (8 SP)
   - FEATURE-002 🟡 (13 SP)
   - FEATURE-003 🔵 (21 SP)
## Timeline & Milestones
## Dependencies & Risks
## Definition of Done (Epic Level)
```

### Verlinkung
**Epic verweist auf:**
- ✅ Related Features Section mit Status und SP
- ✅ Dependencies zu anderen Epics

**Feature verweist zurück auf:**
- ✅ Epic Referenz im Header: `> **Epic:** EPIC-001 - [Name]`

### Wann verwenden?
- Strategische Initiativen (>2 Monate)
- Multiple Teams involviert
- Mehrere Features zu einem Geschäftsziel
- Portfolio/Roadmap Planning

---

## 🎯 FEATURE Template - Funktionale Ebene

**Datei:** `FEATURE-TEMPLATE.md`  
**Scope:** Konkrete Funktionalitäten (1-4 Wochen, 13-55 SP, €10k-100k Impact)

### Hauptsektionen
```markdown
> Epic: EPIC-XXX - [Epic Name]
> Feature: FEATURE-XXX
> Status: Backlog | Planning | In Progress | In Review | Done
> Priority: High | Medium | Low
> Story Points: [Summe aller Issues]
> Team: [Team Name]

## Overview & Business Value
## User Impact & Personas
## User Stories (Feature Level)
## Related Issues (3-10 Issues)
   ### Core Issues (Must Complete)
   - ISSUE-001: Basic Login ✅ (5 SP)
   - ISSUE-002: OAuth Integration 🟡 (8 SP)
   - ISSUE-003: 2FA 🔵 (5 SP)
## Workflows & Use Cases
## Success Metrics (Feature-Specific KPIs)
## Dependencies & Risks
## Definition of Done (Feature Level)
```

### Verlinkung
**Feature verweist auf:**
- ✅ Epic im Header: `> **Epic:** EPIC-001 - Customer Portal`
- ✅ Related Issues Section mit Status und SP
- ✅ Dependencies zu anderen Features

**Epic verweist auf Feature:**
- ✅ In Related Features Liste

**Issue verweist zurück auf:**
- ✅ Feature im Header: `> **Feature:** FEATURE-001 - Login`

### Wann verwenden?
- Einzelne, in sich geschlossene Funktionalität
- User Value klar kommunizierbar
- 1-4 Wochen Entwicklungszeit
- Sprint Planning Items

---

## ⚙️ ISSUE Template - Implementierungsebene

**Datei:** `ISSUE-TEMPLATE.md`  
**Scope:** Implementierbare Arbeitseinheiten (1-5 Tage, 1-8 SP)

### Hauptsektionen
```markdown
> Epic: EPIC-XXX - [Epic Name]
> Feature: FEATURE-XXX - [Feature Name]
> Issue: ISSUE-XXX
> Status: Backlog | Ready | In Progress | In Review | Done
> Priority: High | Medium | Low
> Story Points: 1 | 2 | 3 | 5 | 8 | 13

## Business Context (Contribution to Feature)
## User Story
## Acceptance Criteria
## Gherkin Scenarios (MIN. 2 VOLLSTÄNDIG!)
   Scenario 1: Happy Path
   Scenario 2: Edge/Error Case
   (Scenario 3: Optional)
## Technical Notes (nur Constraints)
## Dependencies
## Definition of Done (Issue Level)
## Test Plan
```

### Verlinkung - KRITISCH!
**Issue verweist auf:**
- ✅ Epic im Header: `> **Epic:** EPIC-001 - Customer Portal`
- ✅ Feature im Header: `> **Feature:** FEATURE-001 - Login`
- ✅ Dependencies zu anderen Issues

**Feature verweist auf Issue:**
- ✅ In Related Issues Liste

**Issue Details:**
- ✅ Business Context erklärt Beitrag zum Feature
- ✅ Gherkin Feature-Name matched Feature-Name

### Wann verwenden?
- Implementierbar in 1 Sprint
- Konkrete Implementierungsarbeit
- Developer Handoff
- Sprint Backlog Items

---

## 🔗 Bidirektionale Verlinkung - Pflichtfelder

### EPIC muss enthalten:

```markdown
## Related Features

### Core Features (Must Have)
1. 🟡 **FEATURE-001**: Login & Authentication
   - **Business Value:** User access to system
   - **Dependencies:** None
   - **Story Points:** 18 SP
   - **Status:** In Progress (3/5 Issues done)

2. 🔵 **FEATURE-002**: Profile Management  
   - **Business Value:** User personalization
   - **Dependencies:** FEATURE-001
   - **Story Points:** 13 SP
   - **Status:** Planned
```

### FEATURE muss enthalten:

```markdown
> **Epic:** EPIC-001 - Customer Self-Service Portal

## Related Issues

### Core Issues (Must Complete)
1. **ISSUE-001** - Basic Email Login ✅ (5 SP)
   - **Status:** Done
   - **Description:** Email/password authentication
   
2. **ISSUE-002** - OAuth Integration 🟡 (8 SP)
   - **Status:** In Progress
   - **Description:** Google/GitHub OAuth
   - **Dependencies:** ISSUE-001
```

### ISSUE muss enthalten:

```markdown
> **Epic:** EPIC-001 - Customer Self-Service Portal  
> **Feature:** FEATURE-001 - Login & Authentication

## Business Context

**Contribution to Feature:**
This issue implements the basic email/password login flow,
which is the foundation for FEATURE-001. Without this,
OAuth (ISSUE-002) and 2FA (ISSUE-003) cannot be built.
```

---

## 📋 Prozess-Workflow

### 1. Top-Down: Epic → Feature → Issue

```
Schritt 1: Requirements Engineer erstellt EPIC
├─ Business Goal definiert
├─ Personas identifiziert
├─ 3-15 Features identifiziert
└─ EPIC-001-customer-portal.md erstellt

Schritt 2: Für jedes Feature
├─ Feature-spezifischen Business Value definiert
├─ 3-10 Issues identifiziert
├─ FEATURE-001-login.md erstellt
└─ Epic-Referenz im Header

Schritt 3: Für jedes Issue
├─ User Story geschrieben
├─ MIN. 2 Gherkin-Szenarien erstellt
├─ ISSUE-001-email-login.md erstellt
├─ Feature-Referenz im Header
└─ Epic-Referenz im Header
```

### 2. Validation: Bottom-Up Check

```
Issue-Validation:
✅ Issue verweist auf Feature?
✅ Feature existiert?
✅ Feature verweist zurück auf Issue in Related Issues?
✅ Issue verweist auf Epic?
✅ Epic existiert?

Feature-Validation:
✅ Feature verweist auf Epic?
✅ Epic existiert?
✅ Epic verweist zurück auf Feature in Related Features?
✅ Feature verweist auf alle Issues?
✅ Alle Issues existieren?

Epic-Validation:
✅ Epic verweist auf alle Features?
✅ Alle Features existieren?
✅ Features verweisen zurück auf Epic?
```

### 3. Status-Synchronisation

**Regeln:**
- Issue → Done: Update Feature Progress
- Alle Issues in Feature → Done: Feature Status = Done
- Alle Features in Epic → Done: Epic Status = Done

**Status-Werte (konsistent über alle Ebenen):**
```
Backlog     → Noch nicht angefangen
Planning    → Requirements/Design Phase
Ready       → Bereit für Implementierung (nur Issue)
In Progress → Aktiv in Entwicklung
In Review   → Code Review / Testing
Done        → Abgeschlossen und deployed
```

---

## 🎨 Namenskonventionen

### Dateinamen
```bash
# Epics (immer 3-stellig)
EPIC-001-customer-self-service-portal.md
EPIC-042-mobile-app-redesign.md

# Features (immer 3-stellig)
FEATURE-001-login-authentication.md
FEATURE-023-profile-management.md

# Issues (immer 3-stellig)
ISSUE-001-basic-email-login.md
ISSUE-142-oauth-google-integration.md
```

### Slug-Regeln
- ✅ lowercase
- ✅ words separated by dashes
- ✅ descriptive but concise (3-5 words max)
- ❌ NO underscores
- ❌ NO spaces
- ❌ NO special characters

---

## ✅ Quality Checklist für Hierarchie

### Vor dem Commit eines EPIC:

- [ ] ✅ Mindestens 3 Core Features definiert
- [ ] ✅ Jedes Feature in Related Features hat:
  - Status Icon (✅🟡🔵⚪)
  - Story Points
  - Business Value
  - Dependencies
- [ ] ✅ Alle Features existieren als FEATURE-XXX.md Dateien
- [ ] ✅ Jedes Feature referenziert dieses Epic zurück

### Vor dem Commit eines FEATURE:

- [ ] ✅ Epic-Referenz im Header: `> **Epic:** EPIC-XXX`
- [ ] ✅ Epic existiert und listet dieses Feature
- [ ] ✅ Mindestens 3 Core Issues definiert
- [ ] ✅ Jedes Issue in Related Issues hat:
  - Status Icon (✅🟡🔵)
  - Story Points
  - Description
  - Dependencies
- [ ] ✅ Alle Issues existieren als ISSUE-XXX.md Dateien
- [ ] ✅ Jedes Issue referenziert dieses Feature zurück
- [ ] ✅ Story Points = Summe aller Issue Story Points

### Vor dem Commit eines ISSUE:

- [ ] ✅ Epic-Referenz im Header: `> **Epic:** EPIC-XXX`
- [ ] ✅ Feature-Referenz im Header: `> **Feature:** FEATURE-XXX`
- [ ] ✅ Epic existiert
- [ ] ✅ Feature existiert und listet dieses Issue
- [ ] ✅ Business Context erklärt Beitrag zum Feature
- [ ] ✅ Gherkin Feature-Name = Feature-Name aus FEATURE-XXX
- [ ] ✅ MIN. 2 vollständige Gherkin-Szenarien
- [ ] ✅ Keine Platzhalter in Gherkin ([X], TODO, ...)

---

## 🔍 Häufige Fehler vermeiden

### ❌ Fehler 1: Einseitige Verlinkung
```markdown
# FEATURE-001.md
> **Epic:** EPIC-001  ✅

# EPIC-001.md
## Related Features
- FEATURE-002  ❌ FEATURE-001 fehlt!
```

**Lösung:** Beide Richtungen verlinken!

### ❌ Fehler 2: Inkonsistente Story Points
```markdown
# FEATURE-001.md
> Story Points: 21 SP

## Related Issues
- ISSUE-001: 5 SP
- ISSUE-002: 8 SP
- ISSUE-003: 5 SP
Total: 18 SP  ❌ Mismatch!
```

**Lösung:** Story Points = Summe aller Issues

### ❌ Fehler 3: Fehlende Rückverweise
```markdown
# ISSUE-001.md
> **Feature:** FEATURE-001  ✅

# FEATURE-001.md
## Related Issues
[leer]  ❌ Issue fehlt!
```

**Lösung:** Feature muss Issue listen!

### ❌ Fehler 4: Gherkin ohne Feature-Context
```gherkin
# ISSUE-001.md
Feature: Login  ❌ Zu generisch!

Scenario: User logs in
  Given user exists
  When user logs in
  Then success  ❌ Vage!
```

**Lösung:**
```gherkin
Feature: Email/Password Authentication (FEATURE-001)

Scenario: User successfully logs in with valid credentials
  Given a registered user with email "user@example.com"
  And the user has password "SecurePass123"
  When the user enters credentials and clicks "Login"
  Then the user is redirected to dashboard
  And a session token is created with 24h expiry
```

---

## 🛠️ Tools & Automatisierung

### Mit Requirements Engineer Mode

```bash
# Epic mit Features erstellen
@requirements-engineer Erstelle Epic für Customer Portal mit Login, Profile, Settings Features

# Feature mit Issues erstellen
@requirements-engineer Breche FEATURE-001 in implementierbare Issues herunter

# Hierarchie validieren
@requirements-engineer Validiere Hierarchie von EPIC-001

# Backlog generieren
@requirements-engineer Generiere BACKLOG.md aus allen Requirements
```

### Validation Script (Beispiel)
```bash
# Prüft ob alle Verlinkungen konsistent sind
./scripts/validate-hierarchy.sh

# Output:
✅ EPIC-001: All 5 features linked correctly
✅ FEATURE-001: All 3 issues linked correctly
❌ FEATURE-002: Missing back-reference in EPIC-001
❌ ISSUE-007: Feature FEATURE-003 does not exist
```

---

## 📚 Beispiel: Vollständige Hierarchie

### EPIC-001-ecommerce-platform.md
```markdown
> Status: In Progress
> Total Story Points: 89 SP

## Related Features

### Core Features (Must Have)
1. 🟡 **FEATURE-001**: Product Catalog (21 SP) - In Progress
2. ✅ **FEATURE-002**: Shopping Cart (13 SP) - Done
3. 🔵 **FEATURE-003**: Checkout (34 SP) - Planning
4. 🔵 **FEATURE-004**: User Accounts (21 SP) - Backlog
```

### FEATURE-001-product-catalog.md
```markdown
> **Epic:** EPIC-001 - eCommerce Platform
> Story Points: 21 SP

## Related Issues

### Core Issues
1. **ISSUE-001** - Product Listing Page ✅ (5 SP) - Done
2. **ISSUE-002** - Product Detail Page 🟡 (5 SP) - In Progress
3. **ISSUE-003** - Product Search 🔵 (8 SP) - Ready
4. **ISSUE-004** - Product Filters 🔵 (3 SP) - Backlog
```

### ISSUE-002-product-detail-page.md
```markdown
> **Epic:** EPIC-001 - eCommerce Platform
> **Feature:** FEATURE-001 - Product Catalog
> Story Points: 5 SP

## Business Context

**Contribution to Feature:**
This issue implements the product detail page which is critical
for FEATURE-001 Product Catalog. It displays full product information
and enables the "Add to Cart" action needed for FEATURE-002.

## Gherkin Scenarios

### Scenario 1: User views product details
```gherkin
Feature: Product Catalog (FEATURE-001)

Scenario: User successfully views complete product information
  Given a product with SKU "PROD-123" exists in the catalog
  And the product has name "Wireless Mouse"
  And the product has price "$29.99"
  And the product has 5 images
  When the user navigates to "/products/PROD-123"
  Then the product name "Wireless Mouse" is displayed
  And the price "$29.99" is prominently shown
  And all 5 product images are loaded
  And the "Add to Cart" button is enabled
  And related products section shows 4 similar items
```

### Scenario 2: User views out-of-stock product
```gherkin
Feature: Product Catalog (FEATURE-001)

Scenario: User views product that is currently unavailable
  Given a product with SKU "PROD-456" exists
  And the product stock quantity is 0
  When the user navigates to "/products/PROD-456"
  Then the product details are displayed
  And an "Out of Stock" badge is shown
  And the "Add to Cart" button is disabled
  And a "Notify When Available" button is displayed
  And estimated restock date "March 15, 2025" is shown
```
```

---

## 📖 Weitere Dokumentation

- **Chatmode:** `.github/chatmodes/requirements-engineer.chatmode.md`
- **Instructions:** `.github/instructions/requirements-engineer.instructions.md`
- **Korrekturen:** `CORRECTIONS-SUMMARY.md`

---

**Template Package Version:** 2.1  
**Process Compliance:** Requirements Engineer Process v2.0  
**Last Updated:** 2025-10-02
