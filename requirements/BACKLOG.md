# BACKLOG: Obsidian Properties Manager

**Projekt**: Obsidian Properties Manager  
**Version**: 1.0.0-MVP  
**Erstellt**: 2025-09-27  
**Status**: Intake abgeschlossen, Ready for Implementation Planning  

## Projekt-Übersicht

Python-App (CLI + Streamlit UI) zur Verwaltung von YAML Frontmatter Properties in Obsidian Markdown Notes mit optionaler LLM-generierter Summary-Funktionalität.

**Zielgruppe**: Obsidian-Nutzer mit 1000+ Notes  
**MVP-Scope**: Standalone App (später Plugin-Potential)  

## Epics Übersicht

| Epic ID | Name | Priorität | Status | Features | 
|---------|------|-----------|--------|----------|
| [EPIC-core-property-management](epics/EPIC-core-property-management-v1.md) | Core Property-Management | Must | Planned | 4 Features |
| [EPIC-llm-integration](epics/EPIC-llm-integration-v1.md) | LLM-Integration | Should | Planned | 2 Features |
| [EPIC-user-interface](epics/EPIC-user-interface-v1.md) | User Interface | Must | Planned | 4 Features |
| [EPIC-data-safety-performance](epics/EPIC-data-safety-performance-v1.md) | Data Safety & Performance | Must | Planned | 3 Features |
| [EPIC-quality-reliability](epics/EPIC-quality-reliability-v1.md) | Quality & Reliability | Must | Planned | 2 Features |

## Features Übersicht

### EPIC 1: Core Property-Management
| Feature ID | Name | Priorität | Status | Stories |
|------------|------|-----------|--------|---------|
| [FEAT-core-property-management-file-reading](features/FEAT-core-property-management-file-reading-v1.md) | Markdown File Reading | Must | Planned | 5 Stories |
| FEAT-core-property-management-write-operations | Property Write Operations | Must | Planned | TBD |
| FEAT-core-property-management-operations-logic | Property Operations Logic | Must | Planned | TBD |
| FEAT-core-property-management-file-selection | File Selection & Batch Processing | Must | Planned | TBD |

### EPIC 2: LLM-Integration
| Feature ID | Name | Priorität | Status | Stories |
|------------|------|-----------|--------|---------|
| FEAT-llm-integration-openai-api | OpenAI API Integration | Should | Planned | TBD |
| FEAT-llm-integration-summary-workflow | Summary Generation Workflow | Should | Planned | TBD |

### EPIC 3: User Interface  
| Feature ID | Name | Priorität | Status | Stories |
|------------|------|-----------|--------|---------|
| FEAT-user-interface-action-selection | UI Action Selection | Must | Planned | TBD |
| FEAT-user-interface-dynamic-forms | UI Dynamic Forms | Must | Planned | TBD |
| FEAT-user-interface-file-management | UI File Management | Must | Planned | TBD |
| FEAT-user-interface-cli | CLI Interface | Must | Planned | TBD |

### EPIC 4: Data Safety & Performance
| Feature ID | Name | Priorität | Status | Stories |
|------------|------|-----------|--------|---------|
| FEAT-data-safety-performance-backup-system | Backup System | Must | Planned | TBD |
| FEAT-data-safety-performance-output-management | Output Management | Must | Planned | TBD |
| FEAT-data-safety-performance-async-processing | Async Processing | Must | Planned | TBD |

### EPIC 5: Quality & Reliability
| Feature ID | Name | Priorität | Status | Stories |
|------------|------|-----------|--------|---------|
| FEAT-quality-reliability-error-handling-logging | Error Handling & Logging | Must | Planned | TBD |
| FEAT-quality-reliability-testing-documentation | Testing & Documentation | Must | Planned | TBD |

## User Stories (Beispiel - erstes Feature)

| Story ID | Name | Feature | Priorität | Effort | Status |
|----------|------|---------|-----------|--------|--------|
| [US-file-reading-01](stories/US-file-reading-01-v1.md) | Parse Valid YAML Frontmatter | File Reading | Must | 0.5 PT | Planned |
| [US-file-reading-02](stories/US-file-reading-02-v1.md) | Handle Files Without Frontmatter | File Reading | Must | 0.5 PT | Planned |
| US-file-reading-03 | Handle Invalid YAML Gracefully | File Reading | Must | 0.5 PT | TBD |
| US-file-reading-04 | Extract Content Separate From Properties | File Reading | Must | 0.5 PT | TBD |
| US-file-reading-05 | Support UTF-8 Encoding | File Reading | Must | 0.5 PT | TBD |

## Technische Anforderungen

**Sprachen**: Python  
**UI**: Streamlit + Click (CLI)  
**APIs**: OpenAI GPT-4.1  
**Plattformen**: Windows, Linux (WSL)  
**File-Typen**: .md (UTF-8)  

## Next Steps

1. **Implementation Plan Agent**: Nutze `/requirements/manifest.json` + alle Markdown-Files für detaillierte Implementierungsplanung
2. **Vervollständigung**: Restliche Features und User Stories ausarbeiten  
3. **Priorisierung**: MoSCoW-Priorisierung für MVP-Release verfeinern

## Artefakte

- **Manifest**: [manifest.json](manifest.json)
- **Templates**: [templates/](templates/)
- **Epics**: [epics/](epics/)  
- **Features**: [features/](features/)
- **Stories**: [stories/](stories/)

---
**Generiert von**: Requirements Engineer Agent  
**Bereit für**: Implementation Plan Agent