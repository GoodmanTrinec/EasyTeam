# Draft: easyteam-global-prompt-pack

status: awaiting-approval
intent: unclear
review_required: true
classification: architecture
pending_action: generate decision-complete work plan only; do not implement
project_root: D:\testyAI\EasyTeam

## User request

User wants EasyTeam thought through globally and turned into a whole project with minimal typing from them: ideally they only click/answer yes/no. User pays for ChatGPT Pro with GitHub integration and also has Ollama.

## Evidence

- `README.md` defines EasyTeam as a multi-agent Suno songwriting workflow with roles HUDEBNÍK, BÁSNÍK, PROMPTER, KRITIK, MODERÁTOR, COVERMASTER, and UŽIVATEL.
- `README.md` defines the current final workflow as Lyrics, Style Prompt, COVERMASTER, and S-cover.
- `README.md` line 25 mentions Easy Team / AUTO mode.
- `README.md` defines core quality rules: every round must improve; critic must give concrete fixes; rhymes, grammar, final Lyrics, Style Prompt, COVERMASTER, and S-cover matter.
- `easyteam-chatgpt-prompt.md` lines 1-4 is a ChatGPT Project Instructions prompt artifact.
- `easyteam-chatgpt-prompt.md` lines 7-90 contains a basic single-file role prompt and output format.
- Explorer confirmed repo is currently a spec plus a single prompt seed, not a complete prompt-engineering system.
- Metis recommends prompt-pack first, not UI/app first; the main gap is decision protocol, defaults, state tracking, and quality gates.

## Components ledger

1. Product/spec foundation: convert README seed into a clear project structure and operating model.
2. Low-typing interaction protocol: yes/no and numbered commands, one question at a time, defaults on `ano`.
3. Prompt pack: modular ChatGPT Project instruction plus role prompts and AUTO workflow.
4. Quality system: critic rubric, rhyme/grammar/style checklist, pass/fail examples.
5. Examples and fixtures: sample sessions proving low-typing workflow reaches final Lyrics, Style Prompt, COVERMASTER, and S-cover.
6. GitHub/project workflow docs: versioning, prompt changes, release notes, ChatGPT/GitHub usage.

## Adopted defaults

- Product path: markdown prompt-pack first, no custom UI/app in this plan. Rationale: user already has ChatGPT Pro + GitHub; Metis says UI-first would delay value. Reversible: yes.
- Interaction: user should be able to type only `ano/ne`, `0-9`, or a few words. Rationale: user writes slowly. Reversible: yes.
- Default mode: `0` means full AUTO from current/last brief; `ano` accepts recommended default and proceeds. Rationale: least typing. Reversible: yes.
- Iteration: default 2 improvement rounds, then final approval; continue only if user says yes. Rationale: avoids fatigue while preserving improvement loop. Reversible: yes.
- Language: Czech/Slovak/Polish-capable, with Style Prompt always in English for Suno. Rationale: current README Czech and user writes Czech/Polish mix; Suno style prompts work best in English. Reversible: yes.
- Input language tolerance: user may mix Polish, Czech, English, and local dialect `po naszymu`; EasyTeam must infer intent without correcting the user's wording or demanding standard language. If output language is unclear, ask one short choice question. Rationale: user explicitly works in this mixed-language/dialect style. Reversible: yes.
- Affirmation tolerance: treat `jo`, `jj`, `jasne`, `tak`, `ok`, `okay`, `dobra`, `sure`, `yes`, and similar local variants as `ano` unless the surrounding text clearly says otherwise. Rationale: user may answer `jo` instead of `ano`. Reversible: yes.
- Privacy-safe interaction rules: do not store a personal "user personality" profile in GitHub. Store only generic project interaction rules such as low-typing mode, yes/no/number controls, mixed PL/CZ/EN/`po naszymu` tolerance, and `jo/jj/ok/tak` as yes. No private identity, personal details, credentials, addresses, or unrelated personal facts. Rationale: user wants the project to remember preferences but not expose personal information. Reversible: yes.
- Review transparency: if a reviewer finds an error, ambiguity, or logical nuance, show `CHYBA:` and `NÁVRH OPRAVY:` before applying the fix. Also propose a better variant when the issue is not a hard bug but a quality/logical improvement. Rationale: user explicitly requested to see findings and improvement proposals. Reversible: yes.
- Execution cadence: downstream worker must execute exactly one todo at a time, verify it, report evidence, then continue to the next todo. Rationale: user works project step-by-step and wants low-overhead oversight. Reversible: yes.
- Ollama: document as optional local fallback, not integrated into v1. Rationale: prompt workflow is the bottleneck, not infrastructure. Reversible: yes.
- GitHub: use repo as versioned prompt pack and examples, not live app backend. Rationale: matches ChatGPT Pro GitHub integration and current repo. Reversible: yes.
- Notes/journal: GitHub is primary. Project-facing decisions, changelog, prompt versions, and documentation must live in normal committed markdown docs. Local `.omo/` is only planner/worker scratch state and must not be treated as the source of truth. Rationale: user explicitly set primary = GitHub. Reversible: yes.

## Scope IN

- Reorganize repo into a usable prompt-engineering project.
- Add modular prompts, ultra-short commands, AUTO mode, user intake defaults, critic rubric, examples, QA/checklists, and GitHub usage docs.
- Preserve current EasyTeam concept and improve it into a practical workflow.

## Scope OUT / Must-NOT-Have

- No web app, desktop app, database, API, or automation requiring new external services.
- No destructive rewrite of user intent.
- No dependence on paid API beyond existing ChatGPT Pro usage.
- No paid service, model, subscription, marketplace item, hosted database, paid API, or paid design/planning tool may be introduced unless it is clearly marked as optional and the user explicitly approves it with a yes/no decision. Existing ChatGPT Pro is the only allowed paid baseline.
- No artist-cloning instructions; named artist requests should be converted to musical attributes.

## Cost guardrail

- Default budget assumption: zero additional spend beyond the user's existing ChatGPT Pro subscription.
- User explicitly rejected paid APIs and paid models by default. They must not be proposed as ordinary upgrades.
- Do not introduce any paid API, paid model, pay-per-token service, paid local model license, or second AI subscription.
- Exception protocol: only if a requirement is genuinely impossible with existing ChatGPT Pro + free/local tools, give the user a very short notice only: `UPOZORNĚNÍ: toto by vyžadovalo platbu: <co> / <proč>. Nezapínám.`
- Do not ask the user to approve payment. Mark the paid-dependent capability out of scope and continue with the best free alternative.

## Approval gate brief

If user approves, generate one `.omo/plans/easyteam-global-prompt-pack.md` decision-complete plan. Execution must be done later by a worker session, not by Prometheus.

## Pause / resume note - 2026-07-19

User paused work because they currently have only a phone connection and are waiting for optical internet repair before downloading large Ollama models.

Next time, start in the project directory and download the recommended tool-capable local model:

```powershell
cd D:\testyAI\EasyTeam
ollama pull qwen3-coder:30b
ollama launch opencode --model qwen3-coder:30b
```

Fallback if too slow:

```powershell
ollama pull devstral:24b
ollama launch opencode --model devstral:24b
```

Then continue the existing plan with:

```text
/start-work easyteam-global-prompt-pack
```

Do not use `phi4:14b` for OpenCode agent work because it does not support tools/function calling in this setup. It remains acceptable only for ordinary local chat/brainstorming.
