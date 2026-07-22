# Example: Pop ballad — plné AUTO po `GO`

Ukázka, jak krátký brief čeká na `GO` a potom AUTO provede dvě plná kola bez dalšího dotazu.

## Inicializace

```text
UŽIVATEL: topic love pop en 2
EasyTeam: Brief načten: love / pop / English / 2 rounds. Spustit AUTO? Napiš GO.
UŽIVATEL: GO
```

AUTO po `GO` provede obě kola, final gate a COVERMASTER bez otázek mezi etapami.

## Round 1/2

```text
MODERATOR: Round 1/2. TITLE, Lyrics and Style are empty. Goal: establish a concrete memory, chorus hook, musical direction and working title.
MUSICIAN: 80 BPM piano ballad with soft strings and intimate female lead. POET: use rain and a faded photo as recurring images. PROMPTER: keep the arrangement sparse and nocturnal.
POET: Proposes TITLE `Still Hear Your Name` and returns the complete Lyrics version 1 with Verse 1 and Chorus.
PROMPTER: Intimate pop ballad at 80 BPM with soft piano, restrained strings and close female vocals. Sparse nocturnal production with a gentle emotional lift in the chorus.
CRITIC: PASS
MODERATOR: Saves TITLE, complete Lyrics version 1 and Style version 1. Round 1 is complete; AUTO continues immediately.
```

## Round 2/2

```text
MODERATOR: Round 2/2. TITLE is `Still Hear Your Name`; the story uses rain, a photo and unresolved regret. Goal: add Verse 2 and Bridge, strengthen the chorus and refine the final arrangement.
MUSICIAN: Keep 80 BPM, add low strings in Verse 2 and backing vocals only in the final chorus. POET: preserve the unresolved ending. PROMPTER: describe the crescendo without production notes in Lyrics.
POET: Keeps TITLE and returns the complete Lyrics version 2 with Verse 1, Chorus, Verse 2, Bridge, final Chorus and Outro.
PROMPTER: Intimate pop ballad at 80 BPM with soft piano, low strings and close female lead vocals. Sparse rainy-night verses grow into restrained backing harmonies and an emotional final chorus without turning triumphant.
CRITIC: PASS
MODERATOR: Saves the complete final TITLE, Lyrics and Style. Both requested rounds are complete.
```

## Final check

```text
MODERATOR: TITLE matches the unresolved memory, Lyrics is complete, Style is English and all brief requirements are met. Starting the separate final gate.
CRITIC: FAIL | RESPONSIBLE ROLE: PROMPTER | ERROR: STYLE does not explicitly state the vocal delivery in the bridge | FIX: add breathy, restrained delivery without changing the atmosphere.
PROMPTER: Intimate pop ballad at 80 BPM with soft piano, low strings and close, breathy female lead vocals. Sparse rainy-night verses grow into restrained backing harmonies and an emotional final chorus without turning triumphant.
CRITIC: PASS
MODERATOR: `final_gate: pass`. COVERMASTER may now start.
```

## Final output

```text
--- TITLE ---

Still Hear Your Name

--- LYRICS ---

[Verse 1]
The rain keeps falling on my window
I sit alone, the lights are low
Your face is fading like a photo
From seasons we no longer know

[Chorus]
And I still hear your name
Returning with the rain
It crosses every quiet room
And fades before the morning bloom

[Verse 2]
The street is empty in December
Your scarf still hangs beside the door
I trace the words I still remember
Then fold the note inside the drawer

[Bridge]
Maybe in another life
I would have stayed with you that night
But every clock repeats the same
And leaves me listening for your name

[Outro]
Your name returns, then slips away

--- STYLE PROMPT ---

Intimate pop ballad at 80 BPM with soft piano, low strings and close, breathy female lead vocals. Sparse rainy-night verses grow into restrained backing harmonies and an emotional final chorus without turning triumphant.

--- COVERMASTER ---

COVERMASTER reads the title `Still Hear Your Name`, the rainy-night story, memory, regret and the unresolved ending. The visual specification remains melancholic and does not invent a reunion.

--- S-COVER ---

Size: 543 × 807 px
Aspect ratio: 543:807
Simplified ratio: 181:269
Text: Still Hear Your Name
Prompt: Vertical Suno song cover, rainy night window, soft reflected city lights, a faded photo and scarf beside a piano, intimate melancholic atmosphere, no cheerful reunion scene.
```

## Ověřené vlastnosti

- Brief sám nespustil AUTO; EasyTeam počkal na samostatné `GO`.
- Brief s číslem `2` způsobil přesně 2 plná kola.
- PROMPTER byl v každém kole.
- Finalní `FAIL` spustil opravu a opakovanou kontrolu.
- COVERMASTER se aktivoval až po `PASS`.
