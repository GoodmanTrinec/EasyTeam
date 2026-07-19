# EasyTeam local diary

## 2026-07-19 - Pause until optical internet is fixed

Status: paused intentionally because the user currently has only a phone connection and does not want to download large Ollama models now.

Project location:

- `D:\testyAI\EasyTeam`

Current durable planning artifacts:

- `.omo/plans/easyteam-global-prompt-pack.md` - approved decision-complete implementation plan.
- `.omo/drafts/easyteam-global-prompt-pack.md` - planning draft and decisions.

Important clarification from this session:

- EasyTeam itself remains a **ChatGPT Pro markdown prompt-pack project**.
- Ollama is only an optional local helper / OpenCode execution model, not part of the EasyTeam product requirements.
- `phi4:14b` failed for agent work because it does **not** support tools/function calling in this setup.
- The next tool-capable Ollama model recommendation for this PC is `qwen3-coder:30b`.

User hardware note:

- GPU: NVIDIA RTX 4070 with 12 GB VRAM.
- RAM: 64 GB.
- User accepts slower execution and is OK with using system RAM.

Recommended model choice next time:

1. Primary: `qwen3-coder:30b`
   - Best fit for local coding/agent work when slower speed is acceptable.
   - Supports tools.
   - Larger than VRAM, so expect partial CPU/RAM offload.
2. Fallback if too slow: `devstral:24b`
   - Also tool-capable and agent/coding oriented.
   - Smaller/faster than `qwen3-coder:30b`.
3. Avoid for OpenCode tools: `phi4:14b`
   - OK for normal chat/brainstorming only.

Next-session exact commands after optical internet returns:

```powershell
cd D:\testyAI\EasyTeam
ollama pull qwen3-coder:30b
ollama launch opencode --model qwen3-coder:30b
```

If `qwen3-coder:30b` is too slow:

```powershell
ollama pull devstral:24b
ollama launch opencode --model devstral:24b
```

After model setup, continue with the existing plan, not a new plan:

```text
/start-work easyteam-global-prompt-pack
```

Critical next-session reminder:

- Start from `D:\testyAI\EasyTeam`, not from `C:\`, otherwise `/start-work` may say no plan was found.
- Do not create a new EasyTeam plan unless the user changes scope.
- Do not add paid APIs, paid models, backend, database, or app UI.
- The implementation target is still the markdown prompt pack described in `.omo/plans/easyteam-global-prompt-pack.md`.
