# EPIC: LLM-Integration

**ID**: EPIC-llm-integration  
**Status**: Planned  
**Priorität**: Should  
**Version**: v1  

## Problem Statement

Als Obsidian-Nutzer möchte ich fehlende Summaries in meinen Notes automatisch durch LLM generieren lassen können, um schnell zu verstehen worum es in einer Note geht, ohne sie vollständig lesen zu müssen.

## Business Value

- **Schnelle Übersicht**: 2-Satz-Summaries ermöglichen schnelle Inhalts-Orientierung
- **Zeitersparnis**: Automatische Summary-Generierung statt manueller Erstellung
- **Selektive Anwendung**: Nutzer kann gezielt Notes für Summary-Generierung auswählen

## Acceptance Criteria

**Given** Markdown-Files ohne Summary-Property  
**When** der Nutzer LLM-Summary-Generierung auswählt  
**Then** werden max. 2-Satz-Summaries generiert und als Property hinzugefügt

**Given** Files mit bestehenden Summaries  
**When** LLM-Summary läuft  
**Then** werden bestehende Summaries nicht überschrieben (außer explizit gewählt)

## Epic Goals

1. **OpenAI Integration**: Stabile GPT-4.1 API-Verbindung
2. **Content Analysis**: Markdown-Inhalt für Summary-Prompting aufbereiten
3. **User Control**: Nutzer entscheidet welche Files Summary bekommen
4. **Quality Assurance**: Max. 2 Sätze, inhaltlich relevante Zusammenfassung

## Out of Scope

- Andere LLM-Provider (nur OpenAI im MVP)
- Summary-Validierung/Qualitätsprüfung
- Custom Prompt-Templates
- Automatische Summary-Updates bei Content-Änderungen

## Features

- FEAT-llm-integration-openai-api
- FEAT-llm-integration-summary-workflow

## Dependencies

- OpenAI API Key (vom Nutzer bereitgestellt)
- Stabile Internet-Verbindung
- OpenAI Python SDK
- API-Kosten-Management (serverseitig bei OpenAI)

## Risks

- **API Rate Limits**: Zu viele parallele Requests → Lösung: Request-Throttling
- **API Costs**: Unerwartete Kosten bei großen Batches → Nutzer ist informiert über serverseitige Limits
- **Content Privacy**: Sensitive Notes werden an OpenAI gesendet → Nutzer-Verantwortung, bewusste Auswahl
- **API Failures**: Network/Service-Ausfälle → Robust Error-Handling

## Definition of Done

- OpenAI GPT-4.1 API erfolgreich integriert
- Summary-Generierung produziert max. 2 Sätze
- Bestehende Summaries werden nur auf Nutzer-Wunsch überschrieben
- API-Fehler werden korrekt behandelt und geloggt
- Nutzer kann Summary-Operation selektiv anwenden
- Unit Tests für API-Integration und Prompt-Handling