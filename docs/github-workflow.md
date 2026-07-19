# GitHub workflow

Tento dokument popisuje, jak používat GitHub pro versionování EasyTeam prompt packu.

## Princip

GitHub je **primární zdroj pravdy** pro EasyTeam. Všechny prompt soubory, dokumentace a příklady jsou verzovány v git commitech. Lokální `.omo/` adresář je pouze scratch/planovací stav, který není oficiálním zdrojem pravdy.

## ChatGPT Pro + GitHub integrace

ChatGPT Pro umí číst soubory z GitHub repozitáře. To umožňuje:

1. **Číst aktuální prompt** přímo z `prompts/chatgpt-project-instructions.md`
2. **Aktualizovat soubory** přes GitHub (commit přes ChatGPT nebo ručně)
3. **Verzovat změny** — každá úprava promptu je vidět v git historii

## Doporučený workflow

### 1. Příprava nové verze promptu

1. Uprav `prompts/chatgpt-project-instructions.md` nebo jiné soubory.
2. Otestuj změny podle `qa/prompt-regression-checklist.md`.
3. Commitni a pushni.

### 2. Použití v ChatGPT

1. Otevři ChatGPT Project.
2. Do Project Instructions vlož obsah `prompts/chatgpt-project-instructions.md`.
3. Pokud používáš GitHub integraci, ChatGPT může číst soubory přímo z repa.

### 3. Commit naming

Používej jasné zprávy, např.:
- `"Fix critic strictness for weak rhymes"`
- `"Add example for pop ballad workflow"`
- `"Update command table with numeric precedence"`
- `"Fix typo in moderator role prompt"`

### 4. Co nedělat

- **Nepřidávat placená API / modely** do promptů ani dokumentace.
- **Nepřidávat osobní údaje** nebo credentials.
- **Nepoužívat `.omo/` jako oficiální dokumentaci** — všechno důležité patří do committed markdown souborů v `prompts/`, `docs/`, `qa/`, `examples/`.

## Rychlá kontrola před commitem

Před každým commitem spusť:

```powershell
Select-String -Path *.md,docs/*.md,prompts/**/*.md,qa/*.md,examples/*.md -Pattern 'paid API','paid model','pay-per-token'
```

Pokud najdeš match, zkontroluj, zda jde o zakázaný návrh (FAIL) nebo pouze o guardrail (OK).