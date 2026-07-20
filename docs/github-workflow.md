﻿﻿# GitHub workflow

Tento dokument popisuje, jak používat GitHub pro versionování EasyTeam prompt packu.

## Princip

GitHub je **primární zdroj pravdy** pro EasyTeam. Všechny prompt soubory, dokumentace a příklady jsou verzovány v git commitech. Dočasné agentní scratch soubory a lokální pracovní poznámky nejsou oficiálním zdrojem pravdy.

## ChatGPT Pro, Codex a GitHub

ChatGPT Pro nebo Codex může podle dostupných oprávnění číst soubory z GitHub repozitáře. Zápis do repozitáře není automaticky zaručený a závisí na tom, zda má použitý nástroj práva pro změnu obsahu repa.

1. **Číst aktuální prompt** přímo z `prompts/chatgpt-project-instructions.md`
2. **Aktualizovat soubory** přes Codex, lokální Git/GitHub CLI nebo GitHub integraci s právy zápisu
3. **Verzovat změny** — každá úprava promptu je vidět v git historii

## Doporučený workflow

### 1. Příprava nové verze promptu

1. Uprav `prompts/chatgpt-project-instructions.md` nebo jiné soubory.
2. Otestuj změny podle `qa/prompt-regression-checklist.md`.
3. Commitni a pushni přes dostupný zapisovací nástroj:
   - Codex s GitHub oprávněním pro zápis obsahu,
   - lokální `git`,
   - GitHub CLI (`gh`),
   - nebo GitHub web UI.

### 2. Použití v ChatGPT

1. Otevři ChatGPT Project.
2. Do Project Instructions vlož obsah `prompts/chatgpt-project-instructions.md`.
3. Pokud používáš GitHub integraci, ChatGPT může číst soubory přímo z repa. Zápis vyžaduje samostatné oprávnění pro commit/push.

### 3. Commit naming

Používej jasné zprávy, např.:
- `"Fix critic strictness for weak rhymes"`
- `"Add example for pop ballad workflow"`
- `"Update command table with numeric precedence"`
- `"Fix typo in moderator role prompt"`
- `"Align COVERMASTER across EasyTeam project"`

### 4. Co nedělat

- **Nepřidávat placená API / modely** do promptů ani dokumentace.
- **Nepřidávat osobní údaje** nebo credentials.
- **Nepoužívat dočasné agentní scratch soubory jako oficiální dokumentaci** — všechno důležité patří do committed markdown souborů v `prompts/`, `docs/`, `qa/`, `examples/`.

## Rychlá kontrola před commitem

Před každým commitem spusť:

```powershell
Select-String -Path *.md,docs/*.md,prompts/**/*.md,qa/*.md,examples/*.md -Pattern 'paid API','paid model','pay-per-token'
```

Pokud najdeš match, zkontroluj, zda jde o zakázaný návrh (FAIL) nebo pouze o guardrail (OK).
