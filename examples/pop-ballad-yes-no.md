﻿# Example: Pop ballad — yes/no workflow

Ukázka, jak UŽIVATEL pracuje převážně s `ano`/`ne` a číselnými volbami.

## Vstupní transcript

```
UŽIVATEL: topic love pop en 2

EasyTeam: Love pop ballad, English, 2 rounds. Start AUTO? 0) yes 1) change topic 2) change style
UŽIVATEL: 0
```

## Průběh

### Round 1
```
Moderator: Round 1/2. Topic: love, pop ballad, English.
Musician: Soft pop ballad, 80 BPM, piano, strings, female vocal, intimate night atmosphere.
Poet:
[Verse 1]
The rain keeps falling on my window
I sit alone, the lights are low
Your face is fading like a photo
From seasons we no longer know

[Chorus]
And I still hear your name
Echoing like a flame
Burning through the silent night
Till morning brings the light

Critic: PASS — rhymes are natural (window/photo, low/know), rhythm is consistent, good imagery.

Moderator: Round 1 complete. Continue to round 2? (0 = yes, 1 = more changes)
User: 0
```

### Round 2
```
Moderator: Round 2/2. Strengthening the chorus.
Musician: Add backing vocals in chorus, slight tempo increase to 85 BPM.
Poet:
[Verse 2]
The streets are empty, cold december
A faded scarf, a word I remember
You walked away without a warning
I count the seconds till the morning

[Chorus]
And I still hear your name
Echoing like a flame
Burning through the silent night
Till morning brings the light (hold)

[Bridge]
Maybe in another life
I would not have caused this strife
Maybe time will heal the scar
And bring me back to who you are

Critic: PASS. Verse 2 is strong, bridge adds emotional depth. One suggestion: "strife" is slightly formal for pop. Consider "Maybe I would not have cut the knife" or "Maybe I'd have stayed the night".
User: ne

Moderator: Alternatives: 1) keep "strife" 2) use "Maybe I'd have stayed the night" 3) rewrite bridge entirely
User: 2

Poet: (revised bridge)
[Bridge]
Maybe in another life
I would have stayed with you tonight
Maybe time will heal the scar
And bring me back to who you are

Critic: PASS. Clean, natural, emotional.
Moderator: Finalize? 0 = yes, 1 = another round
User: 0
```

## Final output

```
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
Echoing like a flame
Burning through the silent night
Till morning brings the light

[Verse 2]
The streets are empty, cold december
A faded scarf, a word I remember
You walked away without a warning
I count the seconds till the morning

[Chorus]
And I still hear your name
Echoing like a flame
Burning through the silent night
Till morning brings the light

[Bridge]
Maybe in another life
I would have stayed with you tonight
Maybe time will heal the scar
And bring me back to who you are

[Outro]
Your name... (fade)

--- STYLE PROMPT ---

Soft pop ballad, piano and strings, gentle female vocals, 80 BPM, intimate night atmosphere with emotional crescendo in the bridge.

--- COVERMASTER ---

COVERMASTER reads the title "Still Hear Your Name", the English lyrics, the intimate pop ballad style, rain/window imagery, memory, regret and an unresolved emotional ending. The cover should stay melancholic and should not turn the story into a happy reunion.

--- S-COVER ---

Size: 543 × 807 px
Aspect ratio: 543:807
Simplified ratio: 181:269
Text: Still Hear Your Name
Prompt: Vertical Suno song cover, rainy night window, soft reflected city lights, a faded photo and scarf on a piano, intimate melancholic pop ballad atmosphere, gentle cinematic lighting, no cheerful reunion scene.
```

## Shrnutí

- User typed `topic love pop en 2`, then `0`, then `0`, then `ne`, then `2`, then `0`
- Only **6 short inputs** for a complete song
- Mostly `0` (yes) and one `ne` with a numeric choice
