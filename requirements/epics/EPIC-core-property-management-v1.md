# EPIC: Core Property-Management

**ID**: EPIC-core-property-management  
**Status**: Planned  
**Priorität**: Must  
**Version**: v1  

## Problem Statement

Als Obsidian-Nutzer mit 1000+ Markdown-Notes möchte ich Properties (YAML Frontmatter) effizient lesen, verwalten und bearbeiten können, ohne jede Datei einzeln öffnen zu müssen.

## Business Value

- **Zeitersparnis**: Bulk-Operations statt manueller Einzelbearbeitung
- **Konsistenz**: Einheitliche Property-Strukturen über alle Notes
- **Skalierbarkeit**: Effiziente Verarbeitung großer Note-Sammlungen

## Acceptance Criteria

**Given** ein Obsidian Vault mit Markdown-Files  
**When** der Nutzer Properties verwalten möchte  
**Then** kann er einzelne oder mehrere Files auswählen und Properties lesen/bearbeiten

## Epic Goals

1. **File Processing Foundation**: Sichere YAML Frontmatter Parse/Write-Operationen
2. **Property Operations**: Add/Edit/Delete/Rename von Properties
3. **Batch Processing**: Effiziente Verarbeitung multipler Files
4. **File Selection**: Flexible Auswahl (einzeln/multi/folder)

## Out of Scope

- Obsidian Plugin-Integration (MVP fokussiert auf standalone App)
- Property-Validierung (wird später hinzugefügt)
- Undo-Funktionalität

## Features

- FEAT-core-property-management-file-reading
- FEAT-core-property-management-write-operations  
- FEAT-core-property-management-operations-logic
- FEAT-core-property-management-file-selection

## Dependencies

- Robust YAML Parser (Python yaml library)
- File System Access (pathlib)
- UTF-8 Encoding Support

## Risks

- **Performance Risk**: Große Anzahl Files könnte Sequential Processing verlangsamen → Lösung: Async Processing in EPIC 4
- **Data Loss Risk**: YAML-Write-Fehler könnte Files korruptieren → Lösung: Backup System in EPIC 4

## Definition of Done

- Alle Features implementiert und getestet
- Unit Tests für alle Core-Funktionen
- YAML Frontmatter wird korrekt gelesen und geschrieben
- Batch-Operationen funktionieren zuverlässig
- Error-Handling für defekte YAML-Files
- Code dokumentiert mit "Warum"-Kommentaren