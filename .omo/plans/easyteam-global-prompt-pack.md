# easyteam-global-prompt-pack - Work Plan

## TL;DR (For humans)

I treated this as open-ended and chose best-practice defaults for you: EasyTeam should become a **markdown-first prompt pack for ChatGPT Pro**, not an app. This gives you the fastest useful result with almost no typing: short commands (`0`, `1`, `2`, `ano`, `ne`) and one-question-at-a-time choices.

What you get:
- A clean repo structure for EasyTeam as a reusable prompt-engineering project.
- A full ChatGPT Project Instructions prompt designed for low-typing use.
- Modular role prompts for MODERÁTOR, BÁSNÍK, HUDEBNÍK, PROMPTER, KRITIK, COVERMASTER, and UŽIVATEL.
- AUTO mode and ultra-short command protocol.
- A critic rubric for rhyme, rhythm, grammar, singability, and Suno style prompt quality.
- Example sessions proving the system works with mostly `ano/ne` and numeric choices.
- QA checklists so future prompt changes do not break the workflow.
- GitHub usage docs for versioning prompt changes.

Decisions I made for you:
- **No paid API/model**: only your existing ChatGPT Pro, free/local Ollama, GitHub, and markdown files are allowed.
- **No UI/app v1**: first deliverable is a prompt pack because the current gap is workflow quality, not buttons.
- **Default interaction**: `0` runs AUTO; `ano` and natural variants like `jo`, `jj`, `tak`, `ok`, `dobra`, `yes` accept defaults; `ne` stops or asks for a simple alternative; `1/2/3` selects visible options. Numeric precedence rule: if EasyTeam has just shown numbered choices and is waiting for an answer, a bare number selects that choice; otherwise it is interpreted as a global command.
- **Default workflow**: two improvement rounds, then final Lyrics, Style Prompt, COVERMASTER, and S-cover unless you continue.
- **Default languages**: user-facing Czech/Slovak/Polish/English tolerant, including local dialect `po naszymu`; Suno Style Prompt always English.
- **Copyright safety**: named artist requests are converted into musical attributes, not imitation.
- **Notes/journal**: GitHub is primary. Project decisions, prompt versions, changelog, and reusable documentation live in committed markdown files. `.omo/` is only local scratch/planning state.
- **Privacy**: do not add a personal profile/personality file. Only add generic interaction rules inside project docs/prompts: low typing, yes/no/numeric controls, mixed PL/CZ/EN/`po naszymu` input, and `jo/jj/ok/tak` meaning yes.
- **Review transparency**: if a reviewer finds a hard error, ambiguity, or softer logical nuance, show `CHYBA:` and `NÁVRH OPRAVY:` before applying the fix; for nuance, suggest the better variant.
- **Execution cadence**: downstream worker must do exactly one todo at a time, verify it, report evidence, then continue.

What it will NOT do:
- No web app, desktop app, hosting, database, paid model/API, or pay-per-token service.
- No automatic publishing to external services.
- No copying living artists’ exact style.

Risk: low. This is documentation/prompt architecture. Main risk is prompt verbosity; the plan explicitly tests for low-typing behavior.

## Scope

### In scope

- Work only inside `D:\testyAI\EasyTeam`.
- Preserve the existing EasyTeam concept from `README.md` while expanding it into a complete prompt-pack project.
- Add markdown artifacts under predictable folders:
  - `prompts/`
  - `prompts/roles/`
  - `workflows/`
  - `examples/`
  - `qa/`
  - `docs/`
- Replace or supersede the current basic `easyteam-chatgpt-prompt.md` with a stronger ChatGPT Project Instructions artifact.
- Add low-typing command support and examples.
- Add QA/rubric material that can be manually or agent-tested without paid APIs.

### Out of scope / Must NOT have

- Do not add an app, executable, backend, package manager setup, database, hosted service, or API integration.
- Do not introduce any paid API, paid model, pay-per-token service, paid local model license, or second AI subscription.
- Do not ask the user to approve payment. If something would require payment, emit only: `UPOZORNĚNÍ: toto by vyžadovalo platbu: <co> / <proč>. Nezapínám.` and continue free.
- Do not make the user type long setup phrases.
- Do not remove the project’s core identity: EasyTeam is a multi-agent Suno songwriting workflow with Lyrics, Style Prompt, COVERMASTER, and S-cover output.
- Do not claim automated Suno integration.
- Do not store private personal data or a named personality profile in GitHub; keep only generic interaction rules needed for the project.

### Evidence references

- `README.md:5-16` defines EasyTeam as a multi-agent song workflow and lists roles.
- `README.md` requires the full final workflow: Lyrics, Style Prompt, COVERMASTER, and S-cover.
- `README.md:25` introduces Easy Team / AUTO mode.
- `README.md:27` says each round must create real improvement.
- `README.md:33-79` defines the critic’s rhyme, rhythm, grammar, and morphology checks.
- `README.md:83-92` lists core rules and final output expectations.
- `easyteam-chatgpt-prompt.md:1-4` is the existing ChatGPT Project Instructions seed.
- `easyteam-chatgpt-prompt.md:7-90` contains the current basic role prompt and output format.

## Verification strategy

Testing strategy: **tests-after / prompt QA fixtures**, because this is a prompt/documentation project, not executable code.

Every implementation todo must include:
- Happy-path QA: a sample low-typing session reaches final Lyrics, Style Prompt, COVERMASTER, and S-cover.
- Failure-path QA: a bad/underspecified input causes EasyTeam to ask one short numbered or yes/no question, not a long form.
- Evidence path: a markdown example or checklist entry under `examples/` or `qa/`.

Global verification commands/checks for the worker:
- `Get-ChildItem -Recurse -File -Include *.md | Select-Object FullName` to enumerate all markdown files.
- `Get-ChildItem -Recurse -File -Include *.md | Select-String -Pattern "paid API","paid model","pay-per-token","OpenAI API","Claude API","Gemini API"` and confirm any matches appear only as prohibited-cost guardrails.
- `Get-ChildItem examples -File -Filter *.md | Select-String -Pattern "MODERÁTOR, zahaj kolo 1"` should return no required-use examples; if it appears, it must be explicitly marked as not required.
- `Get-ChildItem examples -File -Filter *.md | Select-String -Pattern "--- LYRICS ---","--- STYLE PROMPT ---","--- COVERMASTER ---","--- S-COVER ---"` confirms final-output examples include all required sections.
- `Select-String -Path qa/*.md -Pattern "weak rhyme","forced rhyme","low-typing","one short"` confirms QA includes at least one weak-rhyme failure case and one low-typing pass case.

## Execution strategy

Mandatory execution order:

- Execute exactly one todo at a time in numeric order: Todo 1, then Todo 2, then Todo 3, etc.
- Do not start the next todo until the current todo's implementation, QA, evidence path, and commit boundary are complete.
- After each todo, report briefly: `HOTOVO: Todo N`, changed files, QA evidence, and any reviewer findings.
- If a reviewer or QA step finds an error, ambiguity, or logical nuance, show it before fixing:
  - `CHYBA: <what is wrong or weak>`
  - `NÁVRH OPRAVY: <specific fix or better variant>`
- Only after the finding/proposal is visible may the worker apply the fix.

Step order:

1. Create structure and central index first so later files have stable homes.
2. Write the command protocol before rewriting prompts; all prompts must obey it.
3. Split the role prompts into modular files, then assemble the ChatGPT Project Instructions from those decisions.
4. Add the critic rubric and Suno style schema.
5. Add examples and QA fixtures last, using them to validate the prompt pack.
6. Update README and GitHub workflow docs after all artifacts exist.

Dependency matrix:

- Todo 1 blocks all later todos.
- Todo 2 blocks Todos 3, 4, 6, 7.
- Todo 3 blocks Todo 5 and Todo 6.
- Todo 4 blocks Todo 6.
- Todo 5 blocks Todo 6 and Todo 7.
- Todo 6 blocks Todo 8.
- Todo 7 blocks Todo 8.
- Todo 8 is final documentation integration.

## Todos

### Todo 1: `D:\testyAI\EasyTeam`: Create markdown prompt-pack folders and root index - expect stable project map

References:
- Current repo has only `README.md` and `easyteam-chatgpt-prompt.md` besides `.git`.
- `README.md` defines the full final workflow: Lyrics, Style Prompt, COVERMASTER, and S-cover.

Implementation:
- Create these folders exactly: `prompts/`, `prompts/roles/`, `workflows/`, `examples/`, `qa/`, `docs/`.
- Add `.gitkeep` placeholder files inside each new folder so Git can track the folder structure before later files are added.
- Add `INDEX.md` at repo root mapping every folder and intended artifact.
- `INDEX.md` must explain that EasyTeam is a ChatGPT Pro prompt-pack first, not an app.
- `INDEX.md` must include the payment rule: no paid API/model beyond existing ChatGPT Pro.

Acceptance criteria:
- All listed folders exist.
- Every listed folder contains `.gitkeep` until replaced by real tracked files.
- `INDEX.md` links to every planned artifact path, even if later todos still fill them.
- `INDEX.md` states the default user interaction is low-typing: `0`, `ano/ne`, numeric choices.

QA:
- Happy path commands: `Test-Path INDEX.md`; `Get-Content INDEX.md`; `Select-String -Path INDEX.md -Pattern 'prompts/','workflows/','examples/','qa/','docs/'`; `Test-Path prompts/.gitkeep`; `Test-Path prompts/roles/.gitkeep`; `Test-Path workflows/.gitkeep`; `Test-Path examples/.gitkeep`; `Test-Path qa/.gitkeep`; `Test-Path docs/.gitkeep`. Pass if `INDEX.md` exists, all planned folders are mentioned, and placeholders exist.
- Failure path command: `Select-String -Path INDEX.md -Pattern 'web app','desktop app','backend','database','API integration'`. Pass only if matches are absent or explicitly marked out of scope.
- Evidence path: `INDEX.md`.

Commit line:
- `git add INDEX.md prompts/.gitkeep prompts/roles/.gitkeep workflows/.gitkeep examples/.gitkeep qa/.gitkeep docs/.gitkeep`
- `if ($?) { git commit -m "Structure EasyTeam prompt pack" }`

### Todo 2: `workflows/short-commands.md`: Define ultra-short yes/no control protocol - expect no long trigger required

References:
- User explicitly said `MODERÁTOR, zahaj kolo 1` is too long.
- User writes slowly and wants yes/no or click-like decisions.
- `README.md:25` supports Easy Team / AUTO mode.

Implementation:
- Add `workflows/short-commands.md`.
- Define command table exactly:
  - `0` = AUTO start or continue from current brief.
  - `1` = show 3 short options when no numbered choice list is currently awaiting an answer.
  - `2` = improve lyrics according to KRITIK when no numbered choice list is currently awaiting an answer.
  - `3` = change music/style direction when no numbered choice list is currently awaiting an answer.
  - `4` = make chorus stronger.
  - `5` = shorten.
  - `6` = more emotional.
  - `7` = more commercial/catchy.
  - `8` = show current state.
  - `9` = final Lyrics, Style Prompt, COVERMASTER, and S-cover.
  - `ano` = accept recommended default and continue.
  - `jo`, `jj`, `tak`, `ok`, `dobra`, `yes`, and clear local equivalents = same as `ano`.
  - `ne` = stop current path and offer 3 alternatives.
  - `?` = show command help.
- Include rules: ask one question at a time; prefer 1/2/3 options; never require long prose; if input is incomplete, choose safe defaults and ask only one short question.
- Include numeric precedence rule exactly: if EasyTeam has just shown numbered choices and is waiting for an answer, a bare number selects that choice; otherwise it is interpreted as a global command.

Acceptance criteria:
- The phrase `MODERÁTOR, zahaj kolo 1` appears only as an example of what is no longer needed, not as a required command.
- `0` is documented as sufficient to start AUTO when context exists.
- `ano`, `ne`, and numeric precedence behavior are unambiguous.
- Affirmation variants like `jo`, `jj`, `tak`, `ok`, `dobra`, and `yes` are documented as equivalent to `ano`.

QA:
- Happy path command: `Select-String -Path workflows/short-commands.md -Pattern 'tema rytir metal cz 3','0','numeric precedence'` confirms compact start and precedence are documented.
- Failure path command: `Select-String -Path workflows/short-commands.md -Pattern 'only 0','one short numbered question','not a long form'` confirms empty-context recovery is documented.
- Evidence path: `workflows/short-commands.md`.

Commit line:
- `git add workflows/short-commands.md`
- `if ($?) { git commit -m "Add low typing command workflow" }`

### Todo 3: `prompts/roles/*.md`: Split all EasyTeam roles into modular prompts - expect reusable role contracts

References:
- `README.md` lists HUDEBNÍK, BÁSNÍK, PROMPTER, KRITIK, MODERÁTOR, COVERMASTER, and UŽIVATEL.
- `easyteam-chatgpt-prompt.md:13-52` contains current combined role descriptions.

Implementation:
- Add these files:
  - `prompts/roles/moderator.md`
  - `prompts/roles/poet.md`
  - `prompts/roles/musician.md`
  - `prompts/roles/prompter.md`
  - `prompts/roles/critic.md`
  - `prompts/roles/covermaster.md`
  - `prompts/roles/user.md`
- Each role file must include: purpose, inputs, outputs, must-do, must-not-do, low-typing behavior.
- Moderator must own state, command interpretation, one-question-at-a-time flow, and final assembly.
- Critic must be strict and concrete; no vague praise-only review.
- PROMPTER must produce English Suno Style Prompt.

Acceptance criteria:
- Every README role has one matching role file.
- Every role file mentions how it behaves when user answers `ano`, `ne`, or a number, including the numeric precedence rule.
- Role files do not contradict `workflows/short-commands.md`.

QA:
- Happy path command: `Select-String -Path prompts/roles/moderator.md -Pattern 'AUTO','0','ano','ne','numeric precedence'` confirms Moderator can drive low-typing AUTO.
- Failure path command: `Select-String -Path prompts/roles/critic.md -Pattern 'weak','fake','concrete line','reject'` or Czech equivalents confirms KRITIK rejects weak/fake rhymes with line-specific fixes.
- Evidence path: `prompts/roles/*.md`.

Commit line:
- `git add prompts/roles`
- `if ($?) { git commit -m "Add modular EasyTeam role prompts" }`

### Todo 4: `qa/critic-rubric.md`: Create strict song-quality rubric - expect concrete pass/fail checks

References:
- `README.md:33-79` defines critic responsibilities for rhyme, rhythm, grammar, morphology, and natural language.
- `README.md` says critic must provide concrete errors and final output must include Lyrics, Style Prompt, COVERMASTER, and S-cover.

Implementation:
- Add `qa/critic-rubric.md`.
- Include sections: rhyme quality, rhythm/singability, grammar/morphology, emotional specificity, chorus strength, Suno suitability, style prompt quality.
- Each section must have pass/fail criteria and examples.
- Include weak-rhyme failure cases and what a concrete KRITIK response looks like.
- Add rule: text cannot pass just because the idea is good; it must sing well.

Acceptance criteria:
- Rubric contains at least 7 categories.
- Rubric has at least one pass and one fail example for rhyme.
- Rubric requires line-specific criticism.

QA:
- Happy path command: `Select-String -Path qa/critic-rubric.md -Pattern 'PASS','couplet','reason'` confirms a good couplet pass example exists.
- Failure path command: `Select-String -Path qa/critic-rubric.md -Pattern 'FAIL','forced rhyme','line pair','required fix'` confirms fake/forced rhyme failure is concrete.
- Evidence path: `qa/critic-rubric.md`.

Commit line:
- `git add qa/critic-rubric.md`
- `if ($?) { git commit -m "Add EasyTeam critic rubric" }`

### Todo 5: `prompts/chatgpt-project-instructions.md`: Build final ChatGPT Project Instructions - expect paste-ready prompt

References:
- `easyteam-chatgpt-prompt.md:1-90` is the current basic version.
- `workflows/short-commands.md` will define the required low-typing protocol.
- `prompts/roles/*.md` will define role contracts.
- `qa/critic-rubric.md` will define quality gates.

Implementation:
- Add `prompts/chatgpt-project-instructions.md` as the canonical paste-ready ChatGPT Project prompt.
- It must include:
  - EasyTeam identity.
  - Low-typing command protocol.
  - State model: brief, current lyrics, current style, round number, open decision, final status.
  - Role choreography.
  - AUTO mode.
  - Quality gates from critic rubric.
  - Mixed-language input tolerance: understand Polish/Czech/English and `po naszymu`; never force the user to rewrite in standard language.
  - Privacy-safe interaction rules: user-facing controls should support slow typing and casual yes variants, but must not store or expose private personal details.
  - Final output format: `--- LYRICS ---`, `--- STYLE PROMPT ---`, optional `--- AVOID / NEGATIVE PROMPT ---`.
  - Payment guardrail notice: no paid API/model; if needed, only warn and do not enable.
- It must instruct ChatGPT to ask at most one short question when required.
- It must prefer defaults over asking whenever safe.
- If the desired output language is unclear because the user mixed languages/dialect, ask one short numbered choice such as `Jazyk výstupu: 1) česky 2) polsky 3) po naszymu?`.
- It must define numeric precedence: if numbered choices are visible and awaiting a reply, `1/2/3` selects one option; otherwise numeric global commands apply.

Acceptance criteria:
- A user can paste the file into ChatGPT Project Instructions directly.
- `0` starts AUTO when enough context exists.
- If context is missing, the prompt asks one short numbered question.
- Final output is Suno-ready and split into Lyrics, Style Prompt, COVERMASTER, and S-cover.

QA:
- Happy path manual ChatGPT check: create/use a ChatGPT Project with `prompts/chatgpt-project-instructions.md` pasted into Project Instructions, submit `tema rytir metal cz 3` then `0`; expected assertion: response starts EasyTeam/AUTO round without requiring `MODERÁTOR, zahaj kolo 1`.
- Failure path manual ChatGPT check: in a fresh chat with the same Project Instructions, submit only `0`; expected assertion: response asks one short numbered question, e.g. `Vyber téma: 1) láska 2) boj 3) smutek`, and does not show a long intake form.
- Static command: `Select-String -Path prompts/chatgpt-project-instructions.md -Pattern 'numeric precedence','one short','0','STYLE PROMPT'` confirms the core instructions are present.
- Evidence path: `prompts/chatgpt-project-instructions.md`. Do not require `examples/` fixtures here; behavior examples are created and validated in Todo 6.

Commit line:
- `git add prompts/chatgpt-project-instructions.md`
- `if ($?) { git commit -m "Add paste ready ChatGPT project prompt" }`

### Todo 6: `examples/*.md`: Add low-typing worked sessions - expect proof user can mostly answer yes/no

References:
- User wants to only click/answer yes/no as much as possible.
- `README.md:25` establishes AUTO mode.
- `README.md:20-24` establishes final output shape.

Implementation:
- Add at least three examples:
  - `examples/czech-folk-metal-low-typing.md`
  - `examples/pop-ballad-yes-no.md`
  - `examples/empty-zero-recovery.md`
- Each example must show input transcript and expected behavior.
- At least one example must start with a compact brief plus `0`.
- At least one example must show mostly `ano/ne` and numeric choices.
- At least one example must show only `0` in an empty context and the one-question recovery behavior.
- Each example must end with `Lyrics`, `Style Prompt`, `COVERMASTER`, and `S-cover` or explain why it is an intermediate state.

Acceptance criteria:
- There are at least 3 example files.
- No example requires typing `MODERÁTOR, zahaj kolo 1`.
- Examples demonstrate both success and recovery behavior.

QA:
- Happy path command: `Select-String -Path examples/czech-folk-metal-low-typing.md -Pattern 'tema rytir metal cz 3','0','--- LYRICS ---','--- STYLE PROMPT ---'` confirms compact input reaches final output.
- Failure path command: `Select-String -Path examples/empty-zero-recovery.md -Pattern 'only 0','one short','1)','2)','3)'` confirms empty `0` recovers with one numbered question.
- Evidence path: `examples/*.md`.

Commit line:
- `git add examples`
- `if ($?) { git commit -m "Add EasyTeam low typing examples" }`

### Todo 7: `qa/prompt-regression-checklist.md`: Add regression checklist for future prompt changes - expect stable behavior

References:
- Prompt projects drift when role instructions are edited without tests.
- Existing repo has no acceptance checks or fixtures.

Implementation:
- Add `qa/prompt-regression-checklist.md`.
- Include checks for:
  - Low-typing compliance.
  - Role separation.
  - Critic strictness.
  - Lyrics/Style Prompt/COVERMASTER/S-cover separation.
  - English Style Prompt.
  - No paid API/model suggestion.
  - No artist cloning.
  - One-question-at-a-time behavior.
- Include exact manual test prompts and expected outcomes.

Acceptance criteria:
- Checklist can be run by an agent or human without external paid services.
- Checklist includes at least 8 checks.
- Checklist includes at least one negative test for payment suggestions.
- Checklist includes a language/dialect test proving mixed Polish/Czech/English/`po naszymu` input does not trigger a long correction request.

QA:
- Happy path command: `Select-String -Path qa/prompt-regression-checklist.md -Pattern 'low-typing','role separation','critic strictness','pass condition'` confirms concrete checks exist.
- Failure path command: `Select-String -Path qa/prompt-regression-checklist.md -Pattern 'paid API','paid model','FAIL'` confirms payment suggestions fail the checklist.
- Evidence path: `qa/prompt-regression-checklist.md`.

Commit line:
- `git add qa/prompt-regression-checklist.md`
- `if ($?) { git commit -m "Add prompt regression checklist" }`

### Todo 8: `README.md`, `docs/github-workflow.md`, and `docs/decision-log.md`: Update public docs for ChatGPT Pro + GitHub usage - expect GitHub to be the project source of truth

References:
- Current `README.md` is conceptual and does not explain setup/use.
- User has ChatGPT Pro with GitHub integration.
- User rejects paid APIs/models beyond existing ChatGPT Pro.

Implementation:
- Update `README.md` to include:
  - What EasyTeam is.
  - Fast setup: paste `prompts/chatgpt-project-instructions.md` into ChatGPT Project Instructions.
  - Short commands table summary.
  - Minimal examples.
  - Link to QA and examples.
  - Cost policy: no paid API/model; ChatGPT Pro + free/local tools only.
- Add `docs/github-workflow.md` explaining:
  - How to use ChatGPT Pro GitHub connection to read/update prompt files.
  - Suggested prompt versioning workflow.
  - Commit naming recommendations.
  - How to avoid accidental paid API/model additions.
- Add `docs/decision-log.md` explaining:
  - GitHub/committed markdown is primary source of truth.
  - Local `.omo/` is only scratch/planning state, not the official project diary.
  - Project-facing decisions, prompt versions, release notes, and reusable docs are recorded in normal docs and committed to GitHub.

Acceptance criteria:
- README is usable as first-time setup documentation.
- README links to canonical prompt, command workflow, examples, and QA.
- `docs/github-workflow.md` is specific to this repo and ChatGPT Pro workflow.
- `docs/decision-log.md` clearly states GitHub is primary and `.omo/` is non-authoritative local scratch state.

QA:
- Happy path command: `Select-String -Path README.md -Pattern 'ChatGPT Project','prompts/chatgpt-project-instructions.md','0','docs/decision-log.md'` confirms setup and GitHub-primary memory are documented.
- Failure path command: `Select-String -Path README.md,docs/*.md -Pattern 'paid API','paid model','pay-per-token','source of truth'`; paid terms may appear only as prohibited items, and docs must not describe `.omo/` as official source of truth.
- Evidence path: `README.md`, `docs/github-workflow.md`, `docs/decision-log.md`.

Commit line:
- `git add README.md docs/github-workflow.md docs/decision-log.md`
- `if ($?) { git commit -m "Document EasyTeam ChatGPT workflow" }`

## Final verification wave

Run these after all todos are complete. All must pass before claiming done.

### F1 Plan compliance audit

- Verify every planned file exists.
- Verify every todo acceptance criterion has evidence.
- Verify no app/backend/API/payment scope was added.
- Commands: `Test-Path` for every planned file; `Get-ChildItem -Recurse -File -Include *.md | Select-String -Pattern 'paid API','paid model','pay-per-token','backend','database'`; inspect matches and allow only prohibited-scope mentions.
- Evidence path: `qa/final-plan-compliance.md` created by the worker.

### F2 Prompt quality review

- Review `prompts/chatgpt-project-instructions.md` against `qa/critic-rubric.md` and `qa/prompt-regression-checklist.md`.
- Confirm command `0`, `ano`, `ne`, `1/2/3`, and `9` are unambiguous, including the precedence rule: visible numbered choices beat global numeric commands.
- Commands: `Select-String -Path prompts/chatgpt-project-instructions.md,workflows/short-commands.md -Pattern 'numeric precedence','0','ano','ne','9'`; manually verify the documented precedence rule is present in both files.
- Evidence path: `qa/final-prompt-quality-review.md`.

### F3 Low-typing manual simulation

- Simulate at least two sessions from `examples/` using only the transcript and expected behavior.
- Confirm each reaches or correctly approaches Lyrics, Style Prompt, COVERMASTER, and S-cover.
- Commands: `Get-Content examples/czech-folk-metal-low-typing.md`; `Get-Content examples/empty-zero-recovery.md`; compare transcript steps to expected assertions in each file and record pass/fail.
- Optional ChatGPT Pro check, if available without payment/API: paste `prompts/chatgpt-project-instructions.md` into a ChatGPT Project and run the same two example inputs; record screenshots or copied transcript snippets in the evidence file.
- Evidence path: `qa/final-low-typing-simulation.md`.

### F4 Scope fidelity / cost guardrail review

- Grep all markdown for paid API/model suggestions.
- Confirm paid options are not recommended and the project remains ChatGPT Pro + free/local tools only.
- Confirm named-artist cloning is disallowed or converted into attributes.
- Evidence path: `qa/final-scope-fidelity.md`.

## Commit strategy

- Use small commits aligned to the todos above.
- Use Windows PowerShell-safe commit commands: run `git add ...` on one line, then `if ($?) { git commit -m "..." }` on the next line. Do not use `&&`.
- Do not rely on Git tracking empty directories; add `.gitkeep` placeholders when a folder must exist before it contains real files.
- Do not squash until the user asks.
- Commit messages should be clear and conventional enough for repo history:
  - `Structure EasyTeam prompt pack`
  - `Add low typing command workflow`
  - `Add modular EasyTeam role prompts`
  - `Add EasyTeam critic rubric`
  - `Add paste ready ChatGPT project prompt`
  - `Add EasyTeam low typing examples`
  - `Add prompt regression checklist`
  - `Document EasyTeam ChatGPT workflow`
- Before each commit, verify no unrelated files outside `D:\testyAI\EasyTeam` are staged.

## Success criteria

- User can open README, copy one prompt into ChatGPT Project Instructions, and start with compact input plus `0`.
- User can continue with mostly `ano/ne` or numbers.
- EasyTeam produces the full final workflow: Lyrics, English Style Prompt, COVERMASTER, and S-cover.
- KRITIK remains strict about rhymes, rhythm, grammar, and singability.
- No paid API/model is introduced, recommended, or required beyond the user’s existing ChatGPT Pro.
- Repo contains reusable prompt artifacts, examples, QA checklists, and GitHub workflow docs.
- Final verification wave evidence files exist and show all checks passed.
