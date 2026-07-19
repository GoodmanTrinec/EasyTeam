# EasyTeam next-session resume note

## Goal

Resume EasyTeam after the user's optical internet is fixed. The next session should start by downloading a tool-capable local Ollama model, then execute the already-created EasyTeam work plan.

## Start here

```powershell
cd D:\testyAI\EasyTeam
ollama pull qwen3-coder:30b
ollama launch opencode --model qwen3-coder:30b
```

Then run:

```text
/start-work easyteam-global-prompt-pack
```

## If too slow

```powershell
ollama pull devstral:24b
ollama launch opencode --model devstral:24b
```

## Existing plan

- Plan path: `.omo/plans/easyteam-global-prompt-pack.md`
- Draft path: `.omo/drafts/easyteam-global-prompt-pack.md`
- Project path: `D:\testyAI\EasyTeam`

## Key decisions to preserve

- EasyTeam is a ChatGPT Pro markdown prompt-pack, not an app.
- No paid API/model beyond existing ChatGPT Pro.
- Low-typing workflow: `0`, `ano/ne`, and numeric choices.
- Accept mixed PL/CZ/EN/`po naszymu` input.
- Do not store personal profile/personality data in GitHub.
- GitHub markdown files are the project source of truth; `.omo/` is local planning/resume scratch.
