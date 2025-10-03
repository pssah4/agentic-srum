# ISSUE-[NUMBER]-[short-name]

> **Epic:** [EPIC-XXX] - [Epic Name]  
> **Feature:** [FEATURE-XXX] - [Feature Name]  
> **Status:** Backlog | Ready | In Progress | In Review | Done  
> **Priority:** High | Medium | Low  
> **Story Points:** [1, 2, 3, 5, 8, 13]  
> **Sprint:** [Sprint Number or Backlog]

## Business Context

[1-2 Sätze: Warum brauchen wir dieses Issue? Wie trägt es zum Feature bei?]

**Contribution to Feature:**
[Wie trägt dieses Issue zum übergeordneten Feature bei?]

**Business Value:**
- [Spezifischer Nutzen dieses Issues innerhalb des Features]
- [Messbarer Impact wenn möglich]

**Target Persona:**
- [Welche User-Gruppe profitiert von diesem spezifischen Issue?]

## User Story

```
Als [Rolle]
möchte ich [Ziel/Wunsch]
damit [Nutzen/Begründung]
```

**Beispiel:**
```
Als eingeloggter Benutzer
möchte ich mein Profilbild ändern können
damit ich meine Identität im System personalisieren kann
```

## Acceptance Criteria

### Must Have (Kritisch für Done)

**Gegeben diese Vorbedingungen sind erfüllt:**
1. [Vorbedingung 1]
2. [Vorbedingung 2]

**Wenn diese Aktionen ausgeführt werden:**
1. [Aktion 1]
2. [Aktion 2]

**Dann erwarten wir folgende Ergebnisse:**
1. [Erwartetes Verhalten 1]
2. [Erwartetes Verhalten 2]

### Should Have (Wichtig aber nicht kritisch)
- [Optional: Zusätzliche Criteria die nice-to-have sind]

## Gherkin Scenarios

> **KRITISCH:** Mindestens 2 vollständige Szenarien erforderlich!  
> Jedes Szenario muss Given/When/Then enthalten.  
> Keine Platzhalter wie [X], TODO, oder "..." erlaubt.

### Scenario 1: [Happy Path - Hauptszenario]

```gherkin
Feature: [Feature Name aus FEATURE-XXX]

Scenario: [Beschreibender Name des Szenarios]
  Given [Konkrete Vorbedingung mit spezifischen Werten]
  And [Weitere Vorbedingung falls nötig]
  When [Konkrete Aktion des Users]
  And [Weitere Aktion falls nötig]
  Then [Erwartetes Ergebnis mit konkreten Werten]
  And [Weitere Erwartung]
  And [Weitere Erwartung]
```

**Beispiel:**
```gherkin
Feature: User Profile Management

Scenario: User successfully uploads a new profile picture
  Given a logged-in user with user ID "12345"
  And the user is on the profile settings page
  And the user has not uploaded a profile picture yet
  When the user clicks on "Change Profile Picture"
  And selects a valid JPEG image "portrait.jpg" of 2MB size
  And clicks "Upload"
  Then the profile picture is uploaded successfully
  And a success message "Profile picture updated!" is displayed
  And the new picture is visible on the profile page
  And the picture is resized to 200x200 pixels
  And the old default avatar is replaced
```

### Scenario 2: [Edge Case oder Error Path]

```gherkin
Feature: [Feature Name]

Scenario: [Beschreibender Name des Edge Case]
  Given [Konkrete Vorbedingung für Edge Case]
  And [Weitere Vorbedingung]
  When [Aktion die zum Edge Case führt]
  Then [Erwartetes Verhalten bei Edge Case]
  And [Erwarteter Error oder Warnung]
  And [System-Zustand nach Edge Case]
```

**Beispiel:**
```gherkin
Feature: User Profile Management

Scenario: User attempts to upload an invalid file format
  Given a logged-in user with user ID "12345"
  And the user is on the profile settings page
  When the user clicks on "Change Profile Picture"
  And selects a PDF file "document.pdf" instead of an image
  And clicks "Upload"
  Then the upload is rejected
  And an error message "Please upload a valid image file (JPEG, PNG, GIF)" is displayed
  And the current profile picture remains unchanged
  And the file selection dialog stays open for correction
```

### Scenario 3: [Optional - Weiteres relevantes Szenario]

```gherkin
Feature: [Feature Name]

Scenario: [Beschreibender Name - z.B. Performance, Security]
  Given [Vorbedingung]
  When [Aktion]
  Then [Erwartung]
  And [Zusätzliche Erwartung]
```

## Technical Notes

> **Hinweis:** Nur Constraints, keine Implementierungsdetails!

### Performance Requirements
- [z.B. "Upload muss <5 Sekunden dauern für Dateien bis 5MB"]
- [z.B. "UI muss responsive sein während Upload"]

### Security Requirements
- [z.B. "Nur authentifizierte User können hochladen"]
- [z.B. "Dateivalidierung gegen Malware erforderlich"]
- [z.B. "Uploaded files müssen in isoliertem Storage"]

### Compliance/Regulatory
- [z.B. "GDPR-konform: User kann Bild jederzeit löschen"]
- [z.B. "Audit Log für alle Upload-Aktionen"]

### Technical Constraints
- [z.B. "Maximale Dateigröße: 5MB"]
- [z.B. "Unterstützte Formate: JPEG, PNG, GIF"]
- [z.B. "Muss mit existierendem CDN kompatibel sein"]

### Integration Points
- **[API/Service Name]:** [Was wird angebunden?]
- **[Database]:** [Welche Tables/Collections?]
- **[External Service]:** [Welche Third-Party Services?]

## Dependencies

### Blocking Dependencies (Must be done first)
> Diese Items müssen **vorher** fertig sein:

- [ ] `ISSUE-[NUMBER]`: [Beschreibung warum blockierend]
  - **Impact:** [Was passiert wenn nicht fertig?]
  - **ETA:** [Erwartetes Fertigstellungsdatum]

- [ ] `FEATURE-[NUMBER]`: [Feature-Dependency]
  - **Impact:** [Auswirkung]

### Blocked By This Issue (Waiting on this)
> Diese Items **warten** auf dieses Issue:

- [ ] `ISSUE-[NUMBER]`: [Beschreibung der Abhängigkeit]
  - **Impact:** [Was wird blockiert?]

### Related Items (Coordination required)
> Koordination erforderlich, aber nicht blockierend:

- [ ] `ISSUE-[NUMBER]`: [Beschreibung der Relation]
  - **Coordination Point:** [Was muss abgestimmt werden?]

### External Dependencies
> Dependencies außerhalb unseres Teams:

- [ ] **[Team/Service Name]:** [Was wird benötigt]
  - **Contact:** [Ansprechpartner]
  - **Status:** [Current status]

## Definition of Done

> **Alle** Punkte müssen erfüllt sein, bevor Issue als "Done" gilt!

### Functional Requirements
- [ ] Alle Must-Have Acceptance Criteria erfüllt
- [ ] Alle Gherkin-Szenarien implementiert und getestet
- [ ] User Story demonstrierbar
- [ ] Feature Owner hat akzeptiert

### Code Quality
- [ ] Code Review durchgeführt und approved
- [ ] Unit Tests geschrieben (Coverage ≥80% für neue/geänderte Zeilen)
- [ ] Integration Tests vorhanden für kritische Pfade
- [ ] Code folgt Team Coding Standards
- [ ] Keine kritischen oder high-priority Bugs offen

### Testing
- [ ] Alle Gherkin-Szenarien haben entsprechende automatisierte Tests
- [ ] Happy Path getestet
- [ ] Edge Cases getestet
- [ ] Error Handling getestet
- [ ] Performance Requirements validiert
- [ ] Security Requirements validiert

### Documentation
- [ ] Code ist dokumentiert (Inline Comments wo nötig)
- [ ] README aktualisiert (falls nötig)
- [ ] API Dokumentation aktualisiert (falls zutreffend)
- [ ] User-Dokumentation erstellt/aktualisiert (falls zutreffend)

### Deployment & Operations
- [ ] Feature Flag konfiguriert (falls nötig)
- [ ] Monitoring/Logging implementiert
- [ ] Alerts konfiguriert (falls kritische Operation)
- [ ] Deployed auf Staging-Umgebung
- [ ] Smoke Tests auf Staging erfolgreich
- [ ] Rollback-Plan dokumentiert

### Feature Integration
- [ ] Issue integriert mit übergeordnetem Feature
- [ ] Feature Owner informiert über Completion
- [ ] Keine Regressions in anderen Issues des Features
- [ ] Feature-Level Tests noch passing

## Test Plan

### Unit Tests
**Scope:**
- [Welche Units/Components getestet werden]

**Test Cases:**
1. [Test Case 1]
2. [Test Case 2]

### Integration Tests
**Scope:**
- [Welche Integrationen getestet werden]

**Test Cases:**
1. [Integration Test 1]
2. [Integration Test 2]

### Manual Test Cases
**Scenario 1: [Name]**
- **Steps:** [1, 2, 3...]
- **Expected Result:** [Was erwartet wird]

**Scenario 2: [Name]**
- **Steps:** [1, 2, 3...]
- **Expected Result:** [Was erwartet wird]

## Validation Checklist

> **Vor Commit:** Alle Punkte müssen ✅ sein!

### File & Naming
- [ ] ✅ Dateiname folgt Konvention: `ISSUE-[3-stellig]-[slug].md`
- [ ] ✅ Issue Number ist eindeutig
- [ ] ✅ Slug ist beschreibend und lowercase mit dashes

### Hierarchy & Links
- [ ] ✅ Epic verlinkt (EPIC-XXX) - muss existieren
- [ ] ✅ Feature verlinkt (FEATURE-XXX) - muss existieren
- [ ] ✅ Feature enthält dieses Issue in seiner Related Issues Liste

### Content Completeness
- [ ] ✅ Alle Required Sections vorhanden
- [ ] ✅ Mindestens 2 vollständige Gherkin-Szenarien
- [ ] ✅ Keine Platzhalter in Gherkin-Szenarien ([X], TODO, ...)
- [ ] ✅ Business Context erklärt Beitrag zum Feature
- [ ] ✅ Acceptance Criteria sind testbar und messbar

### Quality Standards
- [ ] ✅ Story Points geschätzt (Fibonacci: 1,2,3,5,8,13)
- [ ] ✅ Priority zugewiesen
- [ ] ✅ Dependencies dokumentiert (falls vorhanden)
- [ ] ✅ Definition of Done vollständig
- [ ] ✅ Technical Notes enthalten nur Constraints, keine Implementierung

### Gherkin Quality
- [ ] ✅ Jedes Scenario hat Given/When/Then
- [ ] ✅ Scenarios sind spezifisch mit konkreten Werten
- [ ] ✅ Scenarios sind voneinander unterschiedlich
- [ ] ✅ Mindestens 1 Happy Path + 1 Edge/Error Case

## Metadata

**Created:** [YYYY-MM-DD]  
**Last Updated:** [YYYY-MM-DD]  
**Created By:** [Name]  
**Assigned To:** [Developer Name or Team]  
**Reviewed By:** [Reviewer Name]  
**Epic:** [EPIC-XXX] - [Epic Name]  
**Feature:** [FEATURE-XXX] - [Feature Name]  
**Labels:** `type:issue`, `priority:[high|medium|low]`, `sprint:[number]`, `feature:[feature-number]`, `epic:[epic-number]`

## Estimates

**Original Estimate:** [X] Story Points  
**Time Spent:** [X] hours  
**Remaining:** [X] Story Points

## Notes & Comments

[Optional: Zusätzliche Notizen, Design-Entscheidungen, Diskussionen]

**Design Decisions:**
- [Decision 1 and rationale]

**Open Questions:**
- [ ] [Question 1]
- [ ] [Question 2]

**Related Links:**
- [Link zu Design Mock]
- [Link zu Technical Spike]
- [Link zu Related Discussion]

---

**Template Version:** 2.0  
**Last Template Update:** 2025-10-02  
**Compliance:** Requirements Engineer Process v2.0
