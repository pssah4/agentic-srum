# USER STORY: Handle Files Without Frontmatter

**ID**: US-file-reading-02  
**Feature**: FEAT-core-property-management-file-reading  
**Status**: Planned  
**Priorität**: Must  
**Effort**: 0.5 PT  
**Version**: v1  

## User Story

**Als** Nutzer  
**möchte ich** auch Markdown-Files ohne YAML Frontmatter verarbeiten können  
**damit** ich sie später mit Properties erweitern kann

## Problem

Nicht alle Markdown-Files haben YAML Frontmatter. Die App muss graceful mit solchen Files umgehen und sie nicht als "Fehler" behandeln, sondern als Kandidaten für Property-Hinzufügung.

## Acceptance Criteria

```gherkin
Given ein Markdown-File ohne Frontmatter
  # Just a title
  Some content here
When das File mit parse_frontmatter() gelesen wird
Then erhalte ich ein leeres Dictionary: {}
And der Content bleibt verfügbar

Given ein File das mit Content startet (keine --- Delimiter)
When geparst wird
Then wird erkannt dass keine Frontmatter vorhanden ist
And es wird kein Fehler geworfen

Given ein File mit nur einem --- Delimiter
When geparst wird
Then wird das File als "kein Frontmatter" behandelt
```

## Definition of Done

- [ ] Files ohne `---` Delimiter werden korrekt erkannt
- [ ] Rückgabe ist immer ein Dictionary (leer wenn kein Frontmatter)
- [ ] Kein Exception/Error für frontmatter-lose Files
- [ ] Content-Extraktion funktioniert auch ohne Frontmatter
- [ ] Unit Tests für verschiedene "No-Frontmatter"-Szenarien
- [ ] Logging Info-Message: "No frontmatter found in {filename}"

## Implementation Notes

```python
def parse_frontmatter(file_path: Path) -> dict:
    """Parse YAML frontmatter, return empty dict if none found.
    
    Why this approach: Returning empty dict instead of None
    allows consistent downstream processing without null-checks.
    Callers can use if properties: to check for content.
    """
    # Check for --- delimiters first
    # Return {} if not found, parsed dict if found
    pass
```

## Test Cases

1. **Pure Markdown**: File startet direkt mit `# Title`
2. **Empty File**: Komplett leere `.md` Datei
3. **Single Delimiter**: File mit nur einem `---` am Anfang
4. **Content Only**: Nur Text, keine Markdown-Header
5. **Whitespace**: File mit Leerzeilen vor Content

## Dependencies

- Keine zusätzlichen Dependencies
- Nutzt dieselbe File-Reading-Logic wie US-file-reading-01

## Risks

- **False Positives**: `---` im Content könnte fälschlich als Delimiter erkannt werden

**Mitigation**: Nur `---` am Dateianfang (erste 10 Zeilen) als Delimiter behandeln