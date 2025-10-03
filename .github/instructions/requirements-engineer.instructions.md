---
applyTo: "requirements/**/*.md"
description: "Automatische Validierungs- und Qualitätsregeln beim Arbeiten mit Requirements-Dateien"
---

# Requirements Validation & Quality Rules

Diese Instructions werden **automatisch** angewendet, wenn du in `requirements/**/*.md` Dateien arbeitest. Sie ergänzen den Requirements Engineer Chatmode mit spezifischen Validierungs- und Quality-Checks.

> **Hinweis:** Diese Regeln werden zusätzlich zu den Hauptinstruktionen aus `.github/chatmodes/requirements-engineer.chatmode.md` geladen. Dort findest du den kompletten Prozess-Workflow.

## File-System-basierte Validierung

### 1. Automatische Dateinamen-Validierung

**Bei Öffnen/Erstellen einer Requirements-Datei, prüfe automatisch:**

```javascript
// Pseudo-Code für Validation
function validateFilename(filename) {
  const patterns = {
    epic: /^EPIC-\d{3}-[a-z0-9-]+\.md$/,
    feature: /^FEATURE-\d{3}-[a-z0-9-]+\.md$/,
    issue: /^ISSUE-\d{3}-[a-z0-9-]+\.md$/
  };
  
  // Prüfe gegen entsprechendes Pattern
  if (!matchesPattern(filename)) {
    return error("❌ Dateiname entspricht nicht Konvention");
  }
  
  // Prüfe ob Nummer eindeutig ist
  if (numberAlreadyExists(filename)) {
    return error("❌ Nummer bereits vergeben");
  }
  
  return success("✅ Dateiname korrekt");
}
```

**Konventionen:**
```
✅ EPIC-001-customer-portal.md
✅ FEATURE-042-login-system.md
✅ ISSUE-127-oauth-integration.md

❌ epic1.md                          (kein Prefix, keine 3-stellige Nummer)
❌ ISSUE-1-login.md                  (Nummer nicht 3-stellig)
❌ ISSUE-001-User Login.md           (Spaces statt Dashes)
❌ ISSUE-001-LoginFeature.md         (CamelCase statt lowercase)
```

### 2. Hierarchie-Validierung

**Bei Speichern einer Requirements-Datei, prüfe:**

#### Für ISSUE-Dateien:
```
CHECK:
1. Header enthält Epic-Referenz?
   → Prüfe: "> **Epic:** EPIC-XXX" vorhanden
   → Prüfe: EPIC-XXX.md existiert
   → Prüfe: EPIC verweist zurück auf dieses Issue über Feature

2. Header enthält Feature-Referenz?
   → Prüfe: "> **Feature:** FEATURE-XXX" vorhanden
   → Prüfe: FEATURE-XXX.md existiert
   → Prüfe: FEATURE listet dieses Issue in "Related Issues"

3. Business Context erklärt Contribution?
   → Prüfe: "Contribution to Feature" Section vorhanden
   → Prüfe: Inhalt ist nicht leer oder Platzhalter
```

**Fehlermeldungen:**
```
❌ ISSUE-023-user-profile.md

Hierarchie-Fehler:
- Epic-Referenz fehlt im Header
- Feature FEATURE-007 existiert nicht
- Feature FEATURE-007 listet dieses Issue nicht

Actions erforderlich:
1. Füge "> **Epic:** EPIC-XXX" zum Header hinzu
2. Erstelle FEATURE-007.md oder korrigiere Referenz
3. Update FEATURE-007 "Related Issues" Section
```

#### Für FEATURE-Dateien:
```
CHECK:
1. Header enthält Epic-Referenz?
   → Prüfe: "> **Epic:** EPIC-XXX" vorhanden
   → Prüfe: EPIC-XXX.md existiert
   → Prüfe: EPIC listet dieses Feature in "Related Features"

2. Related Issues Section vollständig?
   → Prüfe: Min. 3 Issues gelistet
   → Prüfe: Alle Issues existieren
   → Prüfe: Story Points = Summe aller Issue Story Points

3. Alle Issues verweisen zurück?
   → Für jedes gelistete Issue: Prüfe ISSUE-XXX hat dieses Feature im Header
```

#### Für EPIC-Dateien:
```
CHECK:
1. Related Features Section vollständig?
   → Prüfe: Min. 3 Features gelistet
   → Prüfe: Alle Features existieren
   → Prüfe: Total Story Points = Summe aller Feature Story Points

2. Alle Features verweisen zurück?
   → Für jedes gelistete Feature: Prüfe FEATURE-XXX hat dieses Epic im Header
```

### 3. Content-Struktur-Validierung

**Prüfe Required Sections:**

#### EPIC muss haben:
```yaml
required_sections:
  - "Business Goal"
  - "Target Personas"
  - "Business Value & Success Metrics"
  - "Related Features"
  - "Timeline & Milestones"
  - "Dependencies & Risks"
  - "Definition of Done"
  - "Validation Checklist"
  - "Metadata"
```

#### FEATURE muss haben:
```yaml
required_sections:
  - "Overview"
  - "Business Value"
  - "User Impact & Personas"
  - "User Stories"
  - "Related Issues"
  - "Success Metrics"
  - "Dependencies & Risks"
  - "Definition of Done"
  - "Validation Checklist"
  - "Metadata"
```

#### ISSUE muss haben:
```yaml
required_sections:
  - "Business Context"
  - "User Story"
  - "Acceptance Criteria"
  - "Gherkin Scenarios"
  - "Technical Notes"
  - "Dependencies"
  - "Definition of Done"
  - "Test Plan"
  - "Validation Checklist"
  - "Metadata"
```

**Bei fehlenden Sections:**
```
⚠️ FEATURE-012-shopping-cart.md

Fehlende Required Sections:
- "Success Metrics" - erforderlich für Feature
- "Dependencies & Risks" - erforderlich für Feature

Template: requirements/templates/FEATURE-TEMPLATE.md
```

## Gherkin-Qualitäts-Validierung

### Automatische Gherkin-Prüfung für ISSUE-Dateien

**Bei jedem Save/Commit, führe durch:**

```javascript
function validateGherkin(issueContent) {
  // 1. Zähle Scenarios
  const scenarios = extractScenarios(issueContent);
  
  if (scenarios.length < 2) {
    return error("❌ Nur " + scenarios.length + " Scenario(s) gefunden. Min. 2 erforderlich.");
  }
  
  // 2. Prüfe jedes Scenario
  scenarios.forEach((scenario, index) => {
    // 2.1 Hat Given?
    if (!scenario.includes("Given")) {
      return error("❌ Scenario " + (index+1) + ": Missing 'Given'");
    }
    
    // 2.2 Hat When?
    if (!scenario.includes("When")) {
      return error("❌ Scenario " + (index+1) + ": Missing 'When'");
    }
    
    // 2.3 Hat Then?
    if (!scenario.includes("Then")) {
      return error("❌ Scenario " + (index+1) + ": Missing 'Then'");
    }
    
    // 2.4 Enthält Platzhalter?
    const placeholders = ["[X]", "[x]", "TODO", "TBD", "[TBD]", "...", "[...]"];
    placeholders.forEach(ph => {
      if (scenario.includes(ph)) {
        return error("❌ Scenario " + (index+1) + ": Enthält Platzhalter '" + ph + "'");
      }
    });
    
    // 2.5 Ist spezifisch? (hat konkrete Werte in "")
    if (!scenario.match(/"[^"]+"/)) {
      return warning("⚠️ Scenario " + (index+1) + ": Keine konkreten Werte in Anführungszeichen");
    }
  });
  
  // 3. Prüfe Feature-Name
  const featureName = extractFeatureName(issueContent);
  const featureRef = extractFeatureReference(issueContent);
  
  if (!featureName.includes(featureRef)) {
    return warning("⚠️ Gherkin Feature-Name sollte Feature-Referenz enthalten");
  }
  
  return success("✅ Gherkin-Validierung erfolgreich: " + scenarios.length + " Scenarios");
}
```

### Gherkin-Quality-Patterns

**Erkenne und verhindere schlechte Patterns:**

#### ❌ Anti-Pattern: Vage Scenarios
```gherkin
Scenario: User logs in
  Given user exists
  When user logs in
  Then success
```

**Feedback:**
```
⚠️ Gherkin-Qualitätswarnung:

Scenario ist zu vage. Verbessere durch:
1. Konkrete Werte: "user@example.com" statt "user"
2. Spezifische Actions: "enters email and clicks Login" statt "logs in"
3. Messbare Outcomes: "redirected to /dashboard" statt "success"

Siehe ISSUE-TEMPLATE.md für Beispiele.
```

#### ❌ Anti-Pattern: Copy-Paste Scenarios
```javascript
// Erkenne duplizierte Scenarios
function detectDuplicateScenarios() {
  const allIssues = loadAllIssues();
  const scenarioHashes = new Map();
  
  allIssues.forEach(issue => {
    issue.scenarios.forEach(scenario => {
      const hash = hashScenario(scenario);
      if (scenarioHashes.has(hash)) {
        return warning(
          "⚠️ " + issue.filename + ": Scenario identisch zu " + 
          scenarioHashes.get(hash)
        );
      }
      scenarioHashes.set(hash, issue.filename);
    });
  });
}
```

#### ❌ Anti-Pattern: Missing Feature Context
```gherkin
Feature: Login

Scenario: ...
```

**Feedback:**
```
⚠️ Feature-Name zu generisch.

Empfohlen: Feature: [Feature Name] ([FEATURE-XXX])
Beispiel: Feature: Login & Authentication (FEATURE-001)

Dies stellt klare Verbindung zum übergeordneten Feature her.
```

## Business-Value-Validierung

### Quantifizierung prüfen

**Für EPIC und FEATURE:**

```javascript
function validateBusinessValue(content) {
  const valueSection = extractSection(content, "Business Value");
  
  // Suche nach quantifizierbaren Metriken
  const patterns = {
    revenue: /\$[\d,]+|\€[\d,]+|revenue.*\d+/i,
    percentage: /\d+%/,
    time: /\d+\s*(hours?|days?|weeks?|months?)/i,
    users: /\d+\s*users?/i,
    reduction: /(reduc|decreas|sav).*\d+/i
  };
  
  let foundMetrics = 0;
  Object.entries(patterns).forEach(([type, pattern]) => {
    if (pattern.test(valueSection)) {
      foundMetrics++;
    }
  });
  
  if (foundMetrics === 0) {
    return warning(
      "⚠️ Business Value nicht quantifiziert. " +
      "Füge messbare Metriken hinzu:\n" +
      "  - Revenue Impact (€X)\n" +
      "  - Time Savings (X hours/week)\n" +
      "  - User Adoption (X%)\n" +
      "  - Cost Reduction (X%)"
    );
  }
  
  return success("✅ Business Value quantifiziert: " + foundMetrics + " Metriken");
}
```

## Story-Points-Konsistenz

### Automatische Aggregation-Prüfung

```javascript
function validateStoryPoints(type, content, filename) {
  const declaredSP = extractStoryPoints(content);
  
  if (type === "FEATURE") {
    // Berechne Summe aller Issues
    const issues = extractRelatedIssues(content);
    const calculatedSP = issues.reduce((sum, issue) => {
      return sum + getIssueStoryPoints(issue);
    }, 0);
    
    if (declaredSP !== calculatedSP) {
      return error(
        "❌ " + filename + ": Story Points Mismatch\n" +
        "  Declared: " + declaredSP + " SP\n" +
        "  Calculated: " + calculatedSP + " SP (sum of issues)\n" +
        "  Action: Update Feature Story Points to " + calculatedSP + " SP"
      );
    }
  }
  
  if (type === "EPIC") {
    // Berechne Summe aller Features
    const features = extractRelatedFeatures(content);
    const calculatedSP = features.reduce((sum, feature) => {
      return sum + getFeatureStoryPoints(feature);
    }, 0);
    
    if (declaredSP !== calculatedSP) {
      return error(
        "❌ " + filename + ": Total Story Points Mismatch\n" +
        "  Declared: " + declaredSP + " SP\n" +
        "  Calculated: " + calculatedSP + " SP (sum of features)\n" +
        "  Action: Update Epic Total Story Points to " + calculatedSP + " SP"
      );
    }
  }
  
  return success("✅ Story Points konsistent");
}
```

## Pre-Commit Validation

### Vollständiger Check vor Commit

**Wenn User versucht Requirements-Datei zu commiten:**

```bash
#!/bin/bash
# pre-commit-validation.sh

echo "🔍 Requirements Validation läuft..."

# 1. Dateinamen-Check
validate_filenames

# 2. Hierarchie-Check
validate_hierarchy

# 3. Content-Struktur-Check
validate_required_sections

# 4. Gherkin-Check (nur für Issues)
if [[ $filename == ISSUE-* ]]; then
  validate_gherkin
fi

# 5. Business-Value-Check (für Epics/Features)
if [[ $filename == EPIC-* ]] || [[ $filename == FEATURE-* ]]; then
  validate_business_value
fi

# 6. Story-Points-Check
validate_story_points

# 7. Platzhalter-Check
check_for_placeholders

if [ $ERRORS -gt 0 ]; then
  echo "❌ Validation fehlgeschlagen: $ERRORS Fehler"
  echo "Bitte behebe die Fehler bevor du commitest."
  exit 1
fi

echo "✅ Alle Validierungen erfolgreich!"
exit 0
```

## Automatische Metriken-Berechnung

### Für BACKLOG.md Generierung

```javascript
function calculateMetrics() {
  const allFiles = loadAllRequirements();
  
  return {
    overview: {
      totalEpics: countByType(allFiles, 'EPIC'),
      totalFeatures: countByType(allFiles, 'FEATURE'),
      totalIssues: countByType(allFiles, 'ISSUE'),
      totalStoryPoints: sumStoryPoints(allFiles)
    },
    
    quality: {
      requirementsCompleteness: calculateCompleteness(allFiles),
      gherkinCoverage: calculateGherkinCoverage(allFiles),
      businessValueScore: calculateBusinessValueScore(allFiles),
      hierarchyIntegrity: checkHierarchyIntegrity(allFiles)
    },
    
    status: {
      backlog: countByStatus(allFiles, 'Backlog'),
      planning: countByStatus(allFiles, 'Planning'),
      inProgress: countByStatus(allFiles, 'In Progress'),
      inReview: countByStatus(allFiles, 'In Review'),
      done: countByStatus(allFiles, 'Done')
    },
    
    dependencies: {
      blocked: countBlockedItems(allFiles),
      blocking: countBlockingItems(allFiles),
      critical: identifyCriticalPath(allFiles)
    }
  };
}

function calculateGherkinCoverage(allFiles) {
  const issues = allFiles.filter(f => f.type === 'ISSUE');
  const issuesWithValidGherkin = issues.filter(issue => {
    const scenarios = extractScenarios(issue.content);
    return scenarios.length >= 2 && 
           scenarios.every(s => hasGivenWhenThen(s) && !hasPlaceholders(s));
  });
  
  return (issuesWithValidGherkin.length / issues.length * 100).toFixed(1) + '%';
}
```

## Quality-Gate-Check

### Automatische QG1-Prüfung

```javascript
function checkQualityGate1() {
  const checks = [
    checkAllEpicsValid(),
    checkAllFeaturesValid(),
    checkAllIssuesValid(),
    checkHierarchyIntegrity(),
    checkGherkinCoverage100(),
    checkNoPlaceholders(),
    checkBusinessValueQuantified(),
    checkDependenciesDocumented()
  ];
  
  const passed = checks.filter(c => c.passed).length;
  const total = checks.length;
  const percentage = (passed / total * 100);
  
  if (percentage === 100) {
    return {
      status: "QG1_READY",
      message: "✅ QG1 erreicht! Alle " + total + " Checks passed.",
      action: "Setze Label 'requirements:approved' und erstelle HANDOVER.md"
    };
  } else {
    return {
      status: "QG1_FAILED",
      message: "❌ QG1 nicht erreicht: " + passed + "/" + total + " Checks passed (" + percentage.toFixed(1) + "%)",
      failedChecks: checks.filter(c => !c.passed),
      action: "Behebe die fehlgeschlagenen Checks"
    };
  }
}
```

## Feedback-Format

### Strukturierte Validation-Messages

**Erfolg:**
```
✅ ISSUE-023-user-registration.md

Validierung erfolgreich:
  ✅ Dateiname korrekt
  ✅ Hierarchie vollständig (Epic + Feature referenziert)
  ✅ 3 Gherkin-Szenarien vorhanden
  ✅ Keine Platzhalter
  ✅ Business Context erklärt Contribution
  ✅ Story Points: 5 SP

Status: Bereit für Commit
```

**Fehler:**
```
❌ ISSUE-023-user-registration.md

Validierungsfehler:
  ❌ Nur 1 Gherkin-Scenario (min. 2 erforderlich)
  ❌ Scenario 1: Enthält Platzhalter "[email address]"
  ⚠️ Business Context ist leer

Actions erforderlich:
  1. Füge min. 1 weiteres Scenario hinzu (z.B. Edge Case)
  2. Ersetze "[email address]" mit konkretem Wert
  3. Beschreibe Beitrag zum Feature in Business Context

Siehe ISSUE-TEMPLATE.md für Beispiele.
```

**Warning:**
```
⚠️ FEATURE-007-shopping-cart.md

Qualitäts-Warnungen:
  ⚠️ Business Value nicht quantifiziert (keine Metriken)
  ⚠️ Story Points (21 SP) != Summe Issues (18 SP)

Empfehlungen:
  1. Füge messbare Business Value Metriken hinzu
  2. Update Story Points auf 18 SP oder prüfe Issue-Schätzungen

Status: Commit möglich, aber Verbesserungen empfohlen
```

## Integration mit Requirements Engineer Mode

Diese Validierungsregeln werden **automatisch** angewendet wenn:

1. **Du arbeitest in requirements/**/*.md Dateien** → Instructions laden automatisch
2. **Du nutzt Requirements Engineer Chatmode** → Chatmode referenziert diese Rules
3. **Du commitest Requirements** → Pre-Commit Hook nutzt diese Rules

**Du musst nichts manuell aufrufen** - die Regeln sind immer aktiv wenn relevant!

## Zusammenfassung

Diese Instructions bieten:

✅ **Automatische Validierung** beim Arbeiten mit Requirements  
✅ **File-System-basierte Checks** für Namenskonventionen und Hierarchie  
✅ **Gherkin-Quality-Checks** für testbare Szenarien  
✅ **Business-Value-Validierung** für Quantifizierung  
✅ **Story-Points-Konsistenz** für korrekte Aggregation  
✅ **Pre-Commit-Validation** für fehlerfreie Commits  
✅ **QG1-Check** für Requirements-Approval  

**Ziel:** Stelle sicher dass JEDE Requirements-Datei dem Quality-Standard entspricht - automatisch, ohne dass der User daran denken muss!
