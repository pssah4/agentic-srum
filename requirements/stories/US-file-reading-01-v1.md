# USER STORY: Parse Valid YAML Frontmatter

**ID**: US-file-reading-01  
**Feature**: FEAT-core-property-management-file-reading  
**Status**: Planned  
**Priorität**: Must  
**Effort**: 0.5 PT  
**Version**: v1  

## User Story

**Als** Entwickler  
**möchte ich** YAML Frontmatter aus Markdown-Files parsen können  
**damit** ich auf alle Properties zugreifen kann ohne das File zu modifizieren

## Problem

Standard Obsidian Notes enthalten YAML Frontmatter zwischen `---` Delimitern. Diese Properties müssen zuverlässig extrahiert und in Python-Datenstrukturen umgewandelt werden.

## Acceptance Criteria

```gherkin
Given ein Markdown-File mit korrektem YAML Frontmatter
  ---
  title: "Test Note"
  status: "active"
  tags: ["work", "project"]
  ---
  # Content here
When das File mit parse_frontmatter() gelesen wird
Then erhalte ich ein Dictionary: {"title": "Test Note", "status": "active", "tags": ["work", "project"]}

Given ein File mit komplexem YAML (Listen, nested objects)
When geparst wird
Then werden alle Strukturen korrekt in Python-Datentypen konvertiert

Given ein File mit Standard Obsidian Properties (UID, Typ, etc.)
When geparst wird  
Then sind alle bekannten Property-Typen korrekt verfügbar
```

## Definition of Done

- [ ] Function `parse_frontmatter(file_path)` implementiert
- [ ] Korrekte YAML-Parsing mit Python `yaml` library
- [ ] Frontmatter-Delimiter (`---`) werden korrekt erkannt
- [ ] Alle YAML-Datentypen werden unterstützt (string, int, list, dict)
- [ ] Unit Test mit mindestens 5 verschiedenen YAML-Strukturen
- [ ] Error-Handling falls YAML-Library nicht verfügbar
- [ ] Performance-Test mit Files bis 1MB Größe

## Implementation Notes

```python
# Expected function signature
def parse_frontmatter(file_path: Path) -> dict:
    """Parse YAML frontmatter from markdown file.
    
    Why this approach: We use PyYAML for robust parsing because
    manual string parsing would be error-prone for complex YAML.
    """
    pass
```

## Test Cases

1. **Standard Properties**: title, status, tags, category
2. **Obsidian Specific**: UID, summary, typ
3. **Complex YAML**: nested objects, multi-line strings
4. **Edge Cases**: empty frontmatter, only delimiters
5. **Unicode**: German umlauts, special characters

## Dependencies

- PyYAML library
- pathlib.Path for file handling

## Risks

- **YAML Complexity**: Sehr komplexe YAML-Strukturen könnten Performance-Probleme verursachen
- **Memory**: Große YAML-Blocks könnten Memory-Usage erhöhen

**Mitigation**: Limit auf "reasonable" YAML-Größe, Monitoring in Tests