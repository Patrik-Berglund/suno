# The Complete Suno AI Instruction Guide

**Note:** This guide uses Suno v5 by default unless otherwise specified.

## Suno Creation Modes

### Simple Mode (500 Character Limit)

**Song Description Field:** 500 characters maximum - describe your song in natural language

**What to include:** Pick and mix any combination of:
- Genre/style
- Mood/emotion
- Instruments
- Vocal type/style
- Tempo/energy
- Production style
- Song theme/lyrics idea

**Optimized Formula:**
```
[Genre] + [Mood] + [1-2 Key Instruments] + [Vocal Type] + [Tempo/Energy]
```

**Examples:**

**Concise (78 chars):**
```
Melancholic indie pop, acoustic guitar, female lead, clean mix, mid-tempo 96 BPM
```

**With lyrics idea (156 chars):**
```
Upbeat synthwave, driving bassline, male vocals, 80s nostalgia. Lyrics about late-night drives through neon-lit streets. Explosive chorus, soft verses.
```

**Maximum detail (487 chars):**
```
Dark cinematic R&B with falsetto male vocals and analog 80s synth bass, gated snare, neon club vibe, glossy mix, 104 BPM. Lyrics explore love as a bad habit - can't quit, keeps coming back. Moody verses with ambient pads, explosive chorus with layered harmonies, atmospheric bridge with whispered vocals. Think late-night drive through empty city streets, streetlights reflecting off wet pavement. Reverb-heavy production, tight drums, melodic bass runs. Bittersweet and hypnotic.
```

**Tips for 500-Char Limit:**
- Use natural language - no need for brackets or strict formatting
- Prioritize what matters most to your vision
- Combine descriptors: "warm analog synth" vs "warm, analog, synthesizer"
- Include lyrics themes if space allows
- One sentence per element keeps it readable


### Custom Mode (Full Control)

**Style Field:** 1,000 characters maximum - describe genre, mood, instruments, production
- Examples: "soft beat, explosive chorus, progressive chords"
- Keep concise: 15-30 words optimal for best results
- Most important descriptors first
- No brackets needed

**Lyrics Field:** 5,000 characters maximum - write full lyrics with meta tags in brackets
- Use structure tags: `[Verse]`, `[Chorus]`, `[Bridge]`
- Add section-specific instructions: `[Verse - Introspective, Gentle]`
- Include performance notes: `[Guitar Solo]`, `[Instrumental Break]`

**The 6-Point Prompt Structure (for Style field):**
```
[Mood] + [Genre/Era] + [Key Instruments] + [Vocal Type] + [Mix Tone] + [Tempo/BPM]
```

**Example Style Field:**
```
Melancholic indie pop, acoustic guitar, warm pads, female lead, clean bright mix, 96 BPM
```

**Example Lyrics Field:**
```
[Intro - Atmospheric, Clean Guitar]

[Verse 1 - Introspective, Gentle]
City lights like scattered stars
You and I float past the boulevard

[Chorus - Energetic, Powerful]
Stay with me until the morning light
We'll rewrite every lost goodnight

[Bridge - Sparse, Whispered]
Maybe we were never meant to stay...

[Outro - Fade Out]
```

---

## Core Principles

### What Suno Responds To

1. **Genre/Era** - Starting point for arrangement, tempo, chord progressions
2. **Instrumentation** - Single instruments can completely shift output
3. **Vocal Style** - One of the strongest control levers
4. **Mood/Tone** - Shapes emotional direction
5. **Production/Mix** - Determines final sound texture

### What to Avoid

- ❌ Vague prompts ("make a pop song")
- ❌ Overloaded prompts (too many conflicting descriptors)
- ❌ Artist names (often blocked; use musical descriptors instead)
- ❌ **Copyrighted lyrics** (Suno will block generation; write original lyrics instead)
- ❌ Missing vocal specification
- ❌ No tempo or energy cues

---

## Structure Prompting (Advanced)

### Use Section Tags in Lyrics

```
[INTRO - Pulsing synth bass and clean guitar riff]
(Instrumental)

[VERSE 1 - Vocals calm, clear, intimate over sparse beat]
Walking through this city late at night
Underneath the neon guiding light

[CHORUS - Explosive energy, full band, powerful vocals]
THIS IS THE FIRE BURNING IN ME!
A FLAME THAT NEVER DIES!

[BRIDGE - Atmospheric, synths swell, echoing whisper]
The silence... the waiting...
The world is holding its breath...

[FINAL CHORUS - Full intensity, layered vocals, huge drums]
THIS IS THE FIRE BURNING IN ME!
```

**For Pure Instrumental Tracks:**
Add `[Instrumental]` at the very top of the lyrics field to prevent Suno from attempting to sing section descriptions:

```
[Instrumental]

[Intro - Grand Piano Solo, Dark and Mysterious]

[Verse - Piano Lead, Violin Enters Dramatically]

[Chorus - Full Power, Piano and Violin in Unison]

[Outro - Fade with Haunting Echo]
```

**Why This Works:**
- Gives Suno a narrative "script" to follow
- AI understands build-up and release
- Tags like [CHORUS] and [BRIDGE] are direct signals
- Controls arrangement and instrumentation per section

---

## Lyric Writing Best Practices

### v5 Improvements Over v4.5
- Higher fidelity to user text; better section obedience
- Improved syllable mapping and rhyme cadence
- Longer context reduces cutoffs and drift
- Pronunciation improved, but mispronunciations still occur

### Copyright & Original Content
**IMPORTANT:** Suno blocks copyrighted lyrics and may flag your account.
- ❌ Don't copy existing song lyrics verbatim
- ✅ Write original lyrics inspired by the style/theme
- ✅ Use the same emotional arc and structure, but different words
- ✅ Study the original's syllable patterns and rhyme schemes, then create your own

**Example - Recreating a Classic:**
Instead of copying "Is This Love" by Whitesnake, write original lyrics with:
- Same theme (questioning if love is real)
- Similar structure (verse-pre-chorus-chorus pattern)
- Matching syllable counts and phrasing
- Your own unique words and metaphors

### Formatting Precision
- Use explicit section markers: [VERSE 1], [CHORUS], [BRIDGE]
- Keep verses to 4–6 lines; separate sections with blank lines
- Avoid prose; format like a song sheet for reliable parsing

### Syllable-to-Beat Alignment
Match syllables to the expected beat count.

✅ 8-beat example: "Walk through the fire, I call Your name again"
❌ Mismatch: "In the fire I still walk, I call Your holy name again now"

**Tips:**
- Count syllables per line and keep consistent within sections
- Shorter lines (4–6 words each) improve phrasing
- Break into smaller verse blocks if lyrics cut off mid-verse

### Structure Tags
Use explicit markers: `[Verse]`, `[Chorus]`, `[Bridge]`, `[Outro]`

### Keep Sections Concise
- 2-6 lines per section works best
- Long lyric dumps cause alignment issues
- Write line breaks where you want musical breaths

### Syllable Control
- Specify syllable targets: "Verse lines: 8–10 syllables each"
- Use hyphens for sustained notes: `lo-ove`, `sooo-long`
- Show phrasing with punctuation: commas = pauses, dashes = staggered delivery

### Rhyme Schemes
State the pattern explicitly:
```
Rhyme scheme: AABB
Example: "sky / high / way / stay"
```

### Prevent Lyric Changes
Add at the top:
```
(Do not change any words inside brackets. Sing exactly as written.)
```

### Stage Directions & Performance Notes
v5 respects these better than v4.5:
- [whisper], [rap verse], [falsetto]
- [sing with power], [breathy]
- [Guitar Solo], [Instrumental Break]

### Call-and-Response (Duets)
```
[VERSE 2]
[male vocal] Who will rise?
[female vocal] I will rise!
```

### Common Pitfalls (and Fixes)
- **Overstuffing lines:** too many words → off-beat phrasing. Fix: shorten lines
- **Over-rhyming:** forced rhymes sound robotic. Fix: rhyme every 2nd or 4th line
- **Ambiguous words:** homographs confuse pronunciation. Fix: phonetic spellings
- **Chorus sounds robotic:** Add repetition ("Shine, shine, shine") or stage directions

---

## Descriptor Library

### Mood Words
- Melancholic, uplifting, nostalgic, moody, anthemic
- Airy, gritty, dreamy, dark, cinematic
- Reflective, spiritual, energetic, heartbroken

### Genre/Era
- 60s soul, 70s funk, 80s synth-pop, 90s grunge
- 2000s indie, modern trap, contemporary R&B
- Gospel, neo-soul, boom-bap, UK drill

### Instruments
- **Keys:** Rhodes piano, Hammond B3 organ, electric piano, analog synth
- **Strings:** Acoustic guitar, electric guitar, upright bass, slap bass
- **Brass:** Brass section, horn stabs, trumpet leads
- **Drums:** Brushed kit, gated drums, 808s, live percussion
- **Other:** Cello, violin section, vocoder, synth pads

### Vocal Types
- Female lead, male lead, falsetto, breathy
- Raspy, smooth, powerhouse gospel lead
- Whispery pop vocals, smoky jazz vocals
- Choir harmonies, stacked harmonies, duet
- Rapped verses + sung chorus

### Mix/Production Tone
- Clean bright, glossy, tape-saturated, lo-fi warmth
- Wide stereo, stadium reverb, live-room acoustics
- Vintage analog, modern radio mix, vinyl crackle
- Tight punchy mix, warm analog, crisp dark production

### Tempo/Energy
- 68–76 BPM (ballad)
- 90–100 BPM (mid-tempo)
- 110–126 BPM (dance/upbeat)
- 140+ BPM (fast/energetic)
- Descriptors: "slow pocket," "driving four-on-the-floor," "swung feel"

---

## Genre-Specific Prompts

### Pop & Indie

**Modern Pop (Taylor Swift-style):**
```
"Modern pop, emotional female vocals, acoustic guitar verse → bright synth chorus, confessional tone, clean mix, 95 BPM."
Lyrics: growing apart but wishing them well.
```

**Indie Pop (The 1975-style):**
```
"Dreamy indie pop, chorus guitars, glossy synth pads, male lead with airy doubles, nostalgic 2000s feel, 118 BPM."
Lyrics: city lights and almost-love.
```

### Hip-Hop & R&B

**Melodic Trap (Drake-style):**
```
"Moody trap, laid-back male vocals, ambient pads, deep 808s, late-night atmosphere, reverb-heavy ad-libs, 80 BPM."
Lyrics: success vs. loneliness.
```

**Neo-Soul (SZA-style):**
```
"Neo-soul groove, silky female lead, stacked harmonies, Rhodes keys, cozy lo-fi warmth, 74 BPM."
Lyrics: boundaries and healing.
```

**Cinematic R&B (The Weeknd-style):**
```
"Dark R&B, falsetto male vocals, analog 80s synth bass, gated snare, neon club vibe, glossy mix, 104 BPM."
Lyrics: love as a bad habit.
```

### Rock & Alternative

**90s Grunge (Nirvana-style):**
```
"Grunge trio, distorted guitars, raw male vocals, quiet-loud-quiet dynamics, tape saturation, 116 BPM."
Lyrics: static on the radio, feeling stuck.
```

**Indie Rock (Arctic Monkeys-style):**
```
"Cool indie rock, tight rhythm guitars, swagger bassline, dry male vocal, club-room realism, 110 BPM."
Lyrics: late-bar observations.
```

### Soul & Jazz

**Retro Soul-Jazz (Amy Winehouse-style):**
```
"Soul-jazz ensemble, smoky female vocal, horn section, upright bass, tape-saturated room, 78 BPM."
Lyrics: vow to quit then one more round.
```

**Gospel-Soul (Aretha Franklin-style):**
```
"Gospel-soul ballad, powerful female lead, Hammond organ, live choir call-and-response, emotional lift, 72 BPM."
Lyrics: finding strength again.
```

### Electronic

**Melodic House (Rüfüs Du Sol-style):**
```
"Atmospheric melodic house, airy male vocal, long-tail reverb, rolling bassline, sunset emotion, 120 BPM."
Lyrics: we'll meet where the light hits water.
```

**French House (Daft Punk-style):**
```
"Funk-house, vocoder hooks, slapped bass, filtered pads, talkbox ad-libs, crisp sidechain, 122 BPM."
Hook: "keep it moving, keep it moving."
```

### Cinematic

**Epic Score (Hans Zimmer-style):**
```
"Orchestral score, string ostinatos, brass swells, taiko hits, massive dynamics, heroic finale, tempo shifts 80–120 BPM."
Cue: from doubt to triumph.
```

**Sadcore Cinema (Lana Del Rey-style):**
```
"Slow cinematic pop, melancholic female vocals, tremolo guitars, vintage plate reverb, 68 BPM."
Lyrics: postcards from a past life.
```

---

## Advanced Techniques

### Three-Pass Method (Layered Prompting)

1. **Idea Pass:** Short prompt for chordal/genre bed and melodic contour
2. **Lyric Pass:** Match lyrical content to the contour's rhythm
3. **Performance Pass:** Feed lyric + contour back with voice, dynamics, production details

### Scene-Based Prompting

Define a visual scene to anchor details:
```
Scene: rainy platform at midnight, ticket clutched in hand.
Instruction: Make metaphors from this scene—avoid generic phrases.
```

### Control Chorus Repetition

Be explicit:
```
"Chorus uses same four lines twice, with the second chorus adding stacked harmonies and an extra ad-lib line."
```

### Use TAG Prefix

Start lyrics with style tags:
```
[TAG: STYLE: synth-driven, dreamy, ethereal atmosphere with pulsing bass and shimmering pads]
```

This keeps your style prompt secret when publishing (just edit lyrics data).

---

## Prompt Templates

### Minimal (Fast Iteration)
```
Create a 90-second pop hook with a female soulful voice.
Mood: nostalgic, hopeful.
Lyric: "I keep the light on for you" — make two short lines, then a longer resolving line.
Tempo: 105 BPM. Key: D major.
Produce: clean modern pop with piano and warm synth pad.
```

### Structured (Full Songs)
```
OBJECTIVE: Full song (VERSE / PRE-CHORUS / CHORUS / BRIDGE / OUTRO), 3:20 target.

VOICE: Male, late-20s, intimate pop vocal with slight rasp. Avoid heavy auto-tune.

MOOD & STORY: Introspective, rising to hopeful by chorus. Theme: leaving a small town to pursue a dream.

STRUCTURE:
- Verse 1 (8 bars): set scene, 7–9 syllables per line, internal rhyme on lines 2 & 4
- Pre-chorus (4 bars): increase tension, shorter lines
- Chorus (16 bars): anthem-like, repeated hook "I'll find the map in your smile", strong melody, layered harmonies
- Bridge (8 bars): contrast — sparse instrumentation, spoken-word feel for two bars, then sung resolution

PRODUCTION: organic acoustic guitar, light percussion, electric piano, warm bass. Avoid heavy reverb on lead voice; add tight doubles at chorus.

LYRICS: Write explicit lyrics. Use vivid details (e.g., "train station, ticket stub"). Maintain internal rhymes and natural phrasing.
```

---

## Common Failure Modes & Fixes

### Problem: Garbled lyrics or dropped words
**Cause:** Lines too long, conflicting stage notes, model capacity limits  
**Fix:** Shorten phrases, split into smaller sections, or generate phrase-by-phrase

### Problem: Unnatural phrasing (robotic cadence)
**Cause:** Model defaulting to learned prosody  
**Fix:** Add explicit timing (BPM, bar mapping), use `(breath)` or `(hold)` markers, elongate vowels

### Problem: Melody drift or wrong repetition
**Cause:** Vague structure or missing section markers  
**Fix:** Add `[Chorus]` tags, label repeats as "same melody," or produce sections separately

### Problem: Generic output
**Cause:** Prompt too vague  
**Fix:** Add one unique instrument + one specific mood word

### Problem: Too chaotic
**Cause:** Overloaded prompt  
**Fix:** Reduce to 4–7 descriptors; stick to the formula

### Problem: Wrong genre blend
**Cause:** Conflicting descriptors  
**Fix:** Put primary genre first—Suno weights early words more heavily

---

## Pro Tips

### Specify Everything
- Always include vocal type (male/female/falsetto/choir)
- Add one instrument that defines the genre
- Include BPM or tempo descriptor when rhythm matters

### Generate Multiple Takes
- Create 2–3 versions
- Lower temperature = more predictable
- Higher temperature = more creative but less consistent
- Pick the best and iterate

### Use Punctuation for Phrasing
- Commas = short pauses
- Dashes = extended syllable linkage
- Ellipses = breath or staggered delivery

### Repeat Hooks Exactly
Paste the chorus in full each time rather than relying on "repeat chorus" shorthand

### Keep Prompts 15–30 Words
Sweet spot: 4–7 descriptors. Too few = generic. Too many = confused.

### Combine AI + Human
- Use Suno for instrumentation
- Layer your own vocals or samples
- Edit in a DAW for final polish
- Treat AI as a collaborator, not a replacement

---

## Suno Studio & Song Editor

### Studio vs Song Editor (v5)

| Task | Song Editor | Studio |
|------|-------------|--------|
| Section editing from waveform | ✅ Remake / Rewrite / Extend / Reorder / Delete | ✅ Same, within multitrack context |
| Multi-stem export | ✅ Available (verify stem count in UI) | ✅ Available (verify stem count in UI) |
| Extended uploads | ✅ Long uploads (verify current limits in UI) | ✅ Integrated in project (verify limits in UI) |
| Creative sliders | ✅ Weirdness / Style Influence / Audio Influence* | ✅ Same |
| Multitrack workspace | — | ✅ Track list, timeline, per-track controls |
| MIDI export | — | 🛈 Promoted for Studio — verify availability |

*Audio Influence appears when an upload is present.

**Use Song Editor when:** Fast section edits, quick stems, broad access
**Use Studio when:** Multitrack context, upload-led builds, stem swaps, arrangement lab

### Studio Workflows (blueprints)

**A) Upload-Led Song (featured vocal/riff)**
1. Import clean WAV (trim silence; minimal FX)
2. Set Audio Influence 60–75 so the upload leads
3. Draft base idea; keep Weirdness near 50
4. Lock chorus (Remake only; Weirdness ↓, Style ↑)
5. Rewrite verses for diction and space
6. Extend 1–2 bars for transitions; Export or Get Stems

**B) AI-First, Human Vocal Later**
1. Draft instrumental + guide vox
2. Get Stems
3. Mute AI lead; import human vocal
4. Remake Bridge only; keep chorus frozen
5. Export stems for final mix if needed

**C) Remix / Arrangement Lab**
1. Import full track; extract stems
2. Mute or replace drums/bass; try alternatives
3. Reorder sections; generate a new Bridge
4. Extend tail for a clean outro; export stems

### Stem Strategy
- Solo, then decide: keep, mute, or replace
- Avoid micro-mixing in Studio
- If it's an arrangement issue (too many mids), fix in Suno, then export
- If it's a tone/EQ issue, export stems and finish in a DAW
- Use consistent sample rate/bit depth across exports (match UI settings)

### For Pro Users
- Open Song Editor to rearrange sections
- Split songs into up to 12 stems
- Extract vocals, mute instruments
- Layer your own live instruments or voice

### For Premier Users
- Use Suno Studio as a multitrack DAW
- Edit on timeline
- Export stems and MIDI
- Import into your DAW (FL Studio, Ableton, Logic Pro) for detailed mixing

### Export Options
- **Free:** MP3 (good for demos, social media)
- **Pro/Premier:** WAV (studio quality), video with lyrics
- **Premier:** MIDI exports

---

## Quick Checklist Before Generating

- [ ] 1 vocal type specified?
- [ ] 1–2 hero instruments named?
- [ ] Mood + era/genre clear?
- [ ] Mix tone added (clean/lo-fi/glossy/tape)?
- [ ] Tempo set (BPM or "mid-tempo/slow pocket")?
- [ ] Structure tags in lyrics ([Verse], [Chorus], [Bridge])?
- [ ] Lyrics 2–6 lines per section?
- [ ] Checked for homographs (read, live, lead, bass, tear, wind)?
- [ ] If using uploads: BPM and key specified?
- [ ] Sliders set appropriately for section type?

---

## Example: Complete Prompt

```
STYLE: Melancholic indie pop, acoustic guitar + warm synth pads, female mid-range breathy vocal with close harmonies, intimate late-night vibe, clean bright mix, 96 BPM.

LYRICS:

[Verse 1]
City lights like scattered stars (breathy)
You and I float past the boulevard
Every word we didn't say
Hangs between us, fades away

[Chorus]
Stay with me until the morning light (belt)
We'll rewrite every lost goodnight
Hold the silence, let it breathe
Find the truth in what we need

[Verse 2]
Coffee shops and empty streets
Memories in every heartbeat
I'm learning how to let you go
Even when I miss you so

[Chorus]
Stay with me until the morning light
We'll rewrite every lost goodnight
Hold the silence, let it breathe
Find the truth in what we need

[Bridge - Atmospheric, sparse instrumentation]
(Whispered)
Maybe we were never meant to stay...
Maybe love is learning to walk away...

[Final Chorus - Full intensity, stacked harmonies]
Stay with me until the morning light
We'll rewrite every lost goodnight
Hold the silence, let it breathe
Find the truth in what we need
```

---

## Final Thoughts

Suno is at its best when you treat it like a producer—not a mind reader.

**The single best habit:** Write a one-line top-anchor at the very top of your prompt:
- Vocal role
- BPM
- Structure

Then add your labeled lyric blocks.

This small discipline yields disproportionately better and more repeatable results.

**Remember:**
- Clear direction > vague inspiration
- Simple structure > complex chaos
- Strong musical keywords > generic descriptions
- Iterate fast, test variations, humanize the output

Generate. Listen. Tweak. Repeat.

---

## Meta Tags Reference

### What Are Meta Tags?

Meta tags are keyword markers in square brackets that steer structure, style, and production. Most impactful in the first 20–30 words and around section changes.

**Format:** `[Tag: Value]` or `[Tag]`

**Where to use:**
- **Lyrics field:** Use with brackets `[Verse]`, `[Chorus]`
- **Style field:** Use without brackets as descriptions
- **Top of lyrics:** Front-load control tags in first 3–5 lines

### Song Structure Tags

```
[Intro] - Lead-in / scene setting
[Verse] / [Verse 1] / [Verse 2] - Lyrical development
[Pre-Chorus] - Build-up before chorus
[Chorus] / [Chorus x2] - Main hook / emotional core
[Post-Chorus] - After chorus section
[Bridge] - Contrast / pivot
[Drop] - Beat-driven instrumental focus
[Hook] - Catchy part emphasis
[Break] / [Instrumental Break] - Break in the song
[Solo Section] - Featured instrument spotlight
[Outro] - Closure or fade-out
[Fade Out] / [Fade In] - Volume transitions
```

### Vocal Tags

**Important Note:** Many voice tags are hit-or-miss. A proven strategy:
1. Upload a vocal sample from Splice
2. Extend the song with different lyrics or use Cover option
3. Use voice tags to manipulate the vocal
4. Layer more styles by repeating with different prompts
5. Extract stems and delete unwanted vocals

**Vocal Type:**
```
[Male Vocal] / [Female Vocal]
[Duet] - Two voices
[Choir] - Group vocals
[Harmonies] - Multiple vocal parts
[Backup Vocals] - Supporting voices
```

**Vocal Tone:**
```
[Airy] - Light, floating quality
[Breathy] - Breath-heavy delivery
[Crisp] - Sharp, clear articulation
[Deep] - Low, resonant
[Gritty] - Rough, textured
[Smooth] - Silky, polished
[Soft] - Gentle, delicate
[Warm] - Rich, inviting
[Raw] - Unpolished, emotional
[Sharp] - Cutting, piercing
[Muffled] - Dampened, distant
[Bright] - Clear, present
[Mellow] - Relaxed, easy
[Raspy] - Scratchy, rough
[Clear] - Pure, clean
[Thin] - Light, delicate
[Dense] - Heavy, thick
```

**Vocal Effects:**
```
[Auto-tuned] - Pitch correction
[Distorted] - Overdriven, harsh
[Reverbed] - Spacious echo
[Echoed] - Distinct repetitions
[Layered] - Multiple vocal tracks
[Chopped] - Cut and rearranged
[Pitch-shifted] - Up or down
[Filtered] - EQ manipulation
[Vocoder] - Robotic voice
[Robotized] - Mechanical quality
[Phased] - Phase-shifted
[Flanged] - Sweeping effect
[Time-stretched] - Tempo-altered
[Lo-fi] - Degraded quality
[Bit-crushed] - Digital distortion
[Glitched] - Digital artifacts
[Stuttered] - Rhythmic repetition
[Modulated] - Varying effect
[Panned] - Left/right stereo
[Granular] - Microscopic sampling
[Doubled] - Double-tracked
[Auto-harmonized] - Automatic harmony
[Saturated] - Warm distortion
[Ring-modulated] - Metallic effect
[Detuned] - Slightly off-pitch
[Reverse] - Backward-sounding
```

**Pitch & Range:**
```
[Low-pitched] - Below normal range
[High-pitched] - Above normal range
[Mid-range] - Standard range
[Sub-bass vocals] - Very low
[Falsetto] - High, breathy
[Baritone] - Low male
[Soprano] - High female
[Tenor] - High male
[Contralto] - Low female
[Whispered falsetto] - Soft high
[Harmonized layers] - Multiple pitches
[Dissonant harmonies] - Clashing pitches
[Octave shift] - Up or down octave
[Pitch-bent] - Sliding pitch
[Modulated pitch] - Varying pitch
[Subtle detune] - Slight off-pitch
[Formant-shifted] - Character change
```

**Vocal Texture:**
```
[Whispered] - Very soft, intimate
[Gravelly] - Rough, textured
[Velvety] - Smooth, luxurious
[Dreamy] - Ethereal, floating
[Resonant] - Full, rich
[Nasal] - Nose-focused
[Brassy] - Bold, metallic
[Metallic] - Cold, industrial
[Saturated] - Warm, full
[Smoky] - Dark, sultry
[Chilled] - Cool, relaxed
[Rough-edged] - Unpolished
[Shimmery] - Bright, sparkling
[Glassy] - Clear, fragile
[Crunchy] - Distorted texture
[Liquid-like] - Flowing, smooth
[Breathy exhale] - Breath-focused
```

**Vocal Style:**
```
[Staccato] - Short, detached
[Legato] - Smooth, connected
[Vibrato-heavy] - Tremolo-rich
[Monotone] - Single pitch
[Melismatic] - Multi-note syllables
[Syncopated] - Off-beat rhythm
[Operatic] - Classical dramatic
[Chanting] - Repetitive, rhythmic
[Spoken-word] - Speech-like
[Growling] - Guttural, aggressive
[Belting] - Powerful, loud
[Yodeling] - Rapid pitch changes
[Humming] - Closed-mouth singing
[Rapping] - Rhythmic speech
[Scatting] - Jazz improvisation
[Falsetto runs] - High melodic lines
[Yelping] - Sharp, sudden
[Grunting] - Low, forceful
[Call-and-response] - Back-and-forth
```

**Dynamics & Volume:**
```
[Soft-spoken] - Quiet, gentle
[Shouted] - Loud, forceful
[Crescendo] - Gradually louder
[Decrescendo] - Gradually softer
[Sudden stop] - Abrupt ending
[Building intensity] - Increasing power
[Explosive] - Sudden burst
[Subtle] - Understated
[Whispered vocals] - Very quiet
[Breathy build-up] - Gradual increase
[Intense climax] - Peak moment
[Dynamic shifts] - Varying volume
[Fading vocals] - Gradual decrease
[Echoing softly] - Quiet repetition
[Reverb swell] - Growing space
[Silent break] - Dramatic pause
```

**Emotional & Mood:**
```
[Sultry] - Seductive, smooth
[Ethereal] - Otherworldly, floating
[Melancholic] - Sad, reflective
[Playful] - Light, fun
[Aggressive] - Forceful, intense
[Haunting] - Eerie, memorable
[Euphoric] - Extremely happy
[Mysterious] - Enigmatic, dark
[Hypnotic] - Trance-like
[Dreamy] - Floating, surreal
[Confident] - Assured, strong
[Desperate] - Urgent, pleading
[Tranquil] - Calm, peaceful
[Emotive] - Emotionally expressive
[Longing] - Yearning, wistful
[Angsty] - Troubled, intense
[Triumphant] - Victorious, proud
[Introspective] - Thoughtful, inward
[Detached] - Distant, cool
```

**Vocal Timing & Rhythm:**
```
[Off-beat] - Syncopated timing
[Syncopated] - Rhythmically displaced
[On-beat] - Steady timing
[Fast-paced] - Quick delivery
[Laid-back] - Relaxed timing
[Polyrhythmic] - Multiple rhythms
[Triplets] - Three-note groupings
[Slow-drawled] - Extended, lazy
[Quick stabs] - Short, sharp
[Rolling] - Flowing, continuous
[Freeform] - Unstructured timing
[Rapid-fire] - Very fast
[Loose phrasing] - Relaxed timing
[Tight rhythm] - Precise timing
```

**Vocal Techniques in Lyrics:**
- Backup vocals: `sing me a song (sing me a song)`
- Melody sounds: `ou ou la la la` or `dee dee doo doo`
- Shouting: `ALL CAPS FOR EMPHASIS`

### Mood & Atmosphere Tags

**Emotional Moods:**
```
[Melancholic] - Sad, reflective
[Euphoric] - Extremely happy, uplifting
[Nostalgic] - Wistful, remembering
[Dreamy] - Ethereal, floating
[Aggressive] - Intense, forceful
[Peaceful] - Calm, serene
[Mysterious] - Enigmatic, intriguing
[Introspective] - Thoughtful, inward
[Uplifting] - Inspiring, elevating
[Dark] - Brooding, ominous
[Joyful] - Happy, celebratory
[Somber] - Serious, grave
[Playful] - Light, fun
[Tense] - Anxious, strained
[Serene] - Tranquil, calm
```

**Atmospheric Tags:**
```
[Dark Atmosphere] - Brooding, ominous
[Bright Atmosphere] - Light, cheerful
[Ambient Atmosphere] - Spacious, atmospheric
[Intimate Atmosphere] - Close, personal
[Cinematic] - Film-like, epic
[Haunting] - Eerie, ghostly
[Warm] - Cozy, inviting
[Cold] - Distant, sterile
```

**Special Atmosphere:**
```
[Eerie Whispers] - Unsettling background vocals
[Ghostly Echoes] - Reverb-heavy, ethereal
[Ominous Drone] - Low, continuous tension
[Spectral Melody] - Otherworldly melody
```

### Energy & Intensity Tags

**Energy Levels:**
```
[High Energy] - Pumping, driving
[Medium Energy] - Steady, moderate
[Low Energy] - Calm, relaxed
[Building Energy] / [Building Intensity] - Gradually increasing
[Explosive Energy] - Sudden bursts
[Driving] - Forward momentum
```

**Intensity Modifiers:**
```
[Intense] - Maximum power
[Gentle] - Soft approach
[Powerful] - Strong presence
[Subtle] - Understated
[Dynamic] - Varying levels
[Anthemic] - Stadium-worthy
[Epic] - Grand, heroic
```

**Dynamic Progression:**
```
[Crescendo] - Gradually louder
[Diminuendo] / [Decrescendo] - Gradually softer
[Climactic] - Musical high point
[Emotional Swell] - Gradual emotional build
[Sudden Break] - Abrupt change
```

### Instrument Tags

**Guitars:**
```
[Electric Guitar] - Modern, amplified
[Acoustic Guitar] - Natural, organic
[Distorted Electric Guitar] - Heavy, overdriven
[Clean Electric Guitar] - Clear, undistorted
[Lead Guitar] - Solo lines
[Rhythm Guitar] - Chord accompaniment
[Bass Guitar] / [Slap Bass] - Low-end foundation
[Fingerpicking] - Acoustic technique
```

**Keys & Synths:**
```
[Piano] - Classic acoustic
[Electric Piano] / [Rhodes Piano] - Vintage electric
[Hammond Organ] / [Organ] - Church or Hammond
[Synthesizer] / [Synth] - Electronic sounds
[Synth Lead] - Lead synthesizer
[Synth Bass] - Bass synthesizer
[Synth Pad] / [Ambient Pads] - Atmospheric layers
[Warm Rhodes] - Specific vintage sound
[Clavinet] - Funk keyboard
```

**Strings:**
```
[Violin] - Classical elegance
[Cello] - Deep, rich tones
[Strings Section] / [String Section] - Orchestral strings
[Upright Bass] - Acoustic bass
```

**Brass & Woodwinds:**
```
[Saxophone] - Jazz sophistication
[Trumpet] / [Muted Trumpet] - Bright, bold
[Brass Section] / [Horn Section] - Full brass ensemble
[Brass Stabs] - Short brass hits
[Flute] - Light, airy
[Clarinet] - Smooth, woody
```

**Drums & Percussion:**
```
[Drums] - Full drum kit
[Electronic Drums] / [Drum Machine] - Digital percussion
[TR-808] / [808s] - Classic drum machine
[Acoustic Drums] - Natural drum kit
[Hand Percussion] - Organic rhythms
[Timpani] - Orchestral drums
[Handclaps] - Percussive claps
[Brushed Kit] - Jazz brushes
[Gated Drums] - 80s gated reverb
```

### Production & Effects Tags

**Reverb & Space:**
```
[Reverb] / [Reverb Heavy]
[Hall Reverb] - Large space echo
[Room Reverb] - Intimate space
[Plate Reverb] - Vintage metallic
[Spring Reverb] - Surf guitar classic
[No Reverb] - Dry, close sound
[Long Reverb] - Extended decay
[Natural Reverb] - Organic space
[Stadium Reverb] - Arena sound
```

**Delay & Echo:**
```
[Echo] - Distinct repetitions
[Delay] - Time-based repetition
[Tape Delay] - Vintage analog delay
[Slapback Delay] - Short, snappy
[Ping Pong Delay] - Stereo bouncing
```

**Distortion & Saturation:**
```
[Distortion] - Heavy clipping
[Overdrive] - Warm saturation
[Fuzz] - Vintage distortion
[Clean] - No distortion
[Tape-Saturated] - Analog warmth
[Raw Production] - Unpolished sound
```

**Modulation:**
```
[Chorus] - Pitch modulation
[Flanger] - Sweeping effect
[Phaser] / [Phaser Effect] - Phase shifting
[Tremolo] - Amplitude modulation
```

**Compression & Dynamics:**
```
[Compressed] / [Heavy Compression] - Controlled dynamics
[Sidechain Compression] - Pumping effect
[Punchy] - Tight, impactful
[Wide Stereo] / [Wide Stereo Image] - Spacious mix
[Wall of Sound] - Dense, layered production
```

**Mix Characteristics:**
```
[Clean Production] / [Clean Mix] - Polished, clear
[Modern Production] - Contemporary sound
[Vintage] - Retro character
[Lo-fi] / [Lo-fi Warmth] - Degraded, nostalgic
[Glossy] - Shiny, polished
[Tight Mix] - Controlled, focused
[Live-Room Acoustics] - Natural space
[Studio-Grade Fidelity] - High quality
```

**Special Effects:**
```
[Vinyl Crackle] - Vintage texture
[Tape Hiss] - Analog warmth
[Record Scratch] - Hip-hop classic
[Reverse Reverb] - Ethereal buildup
[Glitch] / [Glitch Effects] - Digital artifacts
[Bitcrushing] - Lo-fi digital distortion
[Stutter Edits] - Rhythmic repetition
[Granular] - Microscopic sampling
[Filter Sweep] / [Low-Pass Filter Sweep] - Sweeping filter
[High-Pass Filter] - Remove low frequencies
[Creative Panning] - Stereo movement
```

### Rhythm & Tempo Tags

**Tempo:**
```
[Slow Tempo] - 60-80 BPM
[Medium Tempo] / [Mid-Tempo] - 90-120 BPM
[Fast Tempo] - 130-180 BPM
[Very Fast] - 180+ BPM
Specific: [90 BPM], [120 BPM], etc.
```

**Rhythmic Feel:**
```
[Straight Feel] - Even eighth notes
[Swing Feel] - Uneven eighths
[Shuffle Feel] - Triplet-based
[Syncopated] - Off-beat emphasis
[Driving Rhythm] - Forward momentum
[Backbeat] - Emphasis on 2 and 4
[Off-beat] - Syncopated emphasis
[Polyrhythm] - Multiple rhythms
```

**Time Signatures:**
```
[4/4 Time] - Standard four beats
[3/4 Time] - Waltz time
[6/8 Time] - Compound duple
[5/4 Time] / [7/8 Time] - Odd meters
```

### Harmony & Chord Tags

**Chord Progressions:**
```
[I-V-vi-IV] - Pop progression (C-G-Am-F)
[vi-IV-I-V] - Alternative pop
[I-vi-IV-V] - 50s progression
[ii-V-I] - Jazz standard
```

**Harmonic Qualities:**
```
[Major Harmony] - Bright, happy
[Minor Harmony] - Dark, sad
[Modal Harmony] - Ancient scales
[Jazz Harmony] - Extended chords
[Dissonant Harmony] - Tension, clash
[Suspended Chords] - Unresolved tension
[Extended Chords] - 7ths, 9ths, 11ths
[Power Chords] - Rock fifths
```

**Scales & Modes:**
```
[Dorian Mode] / [Dorian Harmony] - Minor with raised 6th
[Mixolydian Mode] - Major with lowered 7th
[Lydian Mode] / [Lydian Harmony] - Major with raised 4th
[Phrygian Mode] - Minor with lowered 2nd
[Pentatonic Scale] - Five-note scale
[Blues Scale] - Pentatonic with blue note
```

**Keys:**
```
[C Major], [G Major], [D Major], [A Major], [E Major]
[A Minor], [E Minor], [B Minor], [F# Minor]
[Major Key] / [Minor Key]
```

### Sound Effects Tags

**Natural Sounds:**
```
[Rain] - Weather atmosphere
[Thunder] - Dramatic impact
[Wind] - Atmospheric movement
[Ocean Waves] - Peaceful nature
[Fire Crackling] - Warm ambiance
[Field Recording] - Natural environment
```

**Urban Sounds:**
```
[Traffic] - City atmosphere
[Footsteps] - Human presence
[Crowd Noise] / [Cheering] - Audience sounds
[Machinery] - Industrial texture
```

**Musical Effects:**
```
[Risers] - Building tension
[Impacts] - Dramatic punctuation
[Whoosh] - Transition sound
[White Noise] - Textural element
```

### Advanced Technique Tags

**Arrangement:**
```
[Call and Response] - Musical conversation
[Counterpoint] - Independent melodies
[Layering] / [Layered Arrangement] - Multiple parts
[Unison] - Same melody, multiple instruments
[Canon] - Overlapping repetitions
[Stripped Back] - Minimal instrumentation
[Orchestral Build] - Gradual orchestral introduction
```

**Texture:**
```
[Minimalist] - Sparse, repetitive
[Maximalist] - Dense, complex
[Monophonic] - Single melody line
[Homophonic] - Melody with accompaniment
[Polyphonic] - Multiple independent melodies
[Organic] - Natural, acoustic
[Synthetic] - Electronic, artificial
```

**Special Techniques:**
```
[Morphing] - Gradual transformation
[Building Tension] - Increasing suspense
[Emotional Bridge] - Intense bridge section
[Catchy Hook] - Memorable hook
[Powerful Outro] - Strong ending
[Soft Intro] - Gentle beginning
[Melodic Interlude] - Melodic break
[Percussion Break] - Percussion-focused section
```

---

## Suno V5 Advanced Parameters

### Creative Control Sliders

**Weirdness (Safe → Chaos)**
- ~50% ≈ "normal" baseline
- Higher: more exploration and risk
- Lower: safer, more expected takes

**Safe Starting Points by Genre:**
- Radio Pop: 35–50
- Hip-hop/Trap: 40–55
- Worship/Gospel: 25–40
- Orchestral: 55–70
- Ambient/Experimental: 70–85

**Style Influence (Loose → Strong)**
- How tightly output follows your style input
- Higher: stricter adherence to genre/description
- Lower: looser, more open interpretation

**Recommended Ranges:**
- Radio Pop: 65–80
- Hip-hop/Trap: 55–70
- Worship/Gospel: 70–85
- Orchestral: 45–60
- Ambient/Experimental: 35–55

**Audio Influence (appears with uploads)**
- How strongly your uploaded audio guides generation
- 60–75: Featured vocal/riff (lead)
- 20–40: Ambient texture (background)

**Section-Specific Strategy:**
- Chorus: Lower Weirdness (35-45), raise Style Influence (70-85) for consistent hook
- Bridge: Raise Weirdness one step (55-70) for novelty
- Verse: Keep conservative (40-55 Weirdness); focus lyric clarity

**Move one slider at a time and compare 20–30s sections**

### Negative Prompting (Exclude Styles)

**What it does:** Exclude specific elements you DON'T want

**Effective Syntax:**
```
"Instrumental only, no vocals"
"Upbeat pop with drums and bass, no guitars"
"Trap beat with piano and synths, no 808s"
```

**Ineffective Syntax:**
```
❌ "Without singing unless background only"
❌ "No sounds that are bad"
❌ "Not like rock"
```

**Common Use Cases:**
- Pure instrumentals: `"Cinematic orchestral build, no vocals, wide reverb"`
- Remove problem instrument: `"Reggae groove with bass and percussion, no electric guitar"`
- Clear muddy mix: `"Lo-fi hip hop with piano and vinyl crackle, no synth pads"`

**Advanced Strategies:**
- Layer negatives with positives: `"Acoustic guitar focus, no distortion, clear vocals"`
- Precision stacking: `"No lead guitar solo"` (keeps rhythm guitars)
- Genre-aware exclusions: EDM `"no hi-hats"`; Rock `"no distortion"`; Hip hop `"no 808s"`

**Troubleshooting:**
```
Still hearing vocals?
  → Try "instrumental only"
     → If persists → Export stems → Remove vocals in DAW

Mix feels too empty?
  → Reduce exclusions (1–2 max)
     → Add clear positives (what you DO want)
```

### Vocal Gender

**Direct control:** Male | Female

**Combine with tags:**
```
Vocal Gender: Female
Style: Powerful Vocals, Soulful Vocals, R&B
Result: Powerful female voice in R&B style
```

### Professional Combination Formula

```
1. Define precise meta tags (15-20 tags)
2. Set Style Influence high (70-80%) for control
3. Add moderate Weirdness (40-60%) for creativity
4. Use Exclude Styles to eliminate unwanted elements
5. Test and refine based on results
```

**Example - Maximum Control:**
```
Style: Pop, Piano, Female Vocal, Emotional, Ballad
Vocal Gender: Female
Weirdness: 30%
Style Influence: 80%
Exclude: Male Vocal, Electric Guitar
```

**Example - Balanced Creativity:**
```
Style: [same tags]
Weirdness: 50%
Style Influence: 60%
Exclude: [same]
```

---

## Audio Uploads & Hybrid Workflow

### Why Audio Uploads Matter
Uploads turn Suno from a generator into a collaborator. Your voice or riff leads; the model arranges around it. v5 is stable enough to use as a pre-production partner.

### How v5 Integrates Your Audio
- **Input normalization:** RMS leveling and DC offset removal
- **Embedding fusion:** audio mapped into the same latent space as text prompts for blend, not overwrite
- **Onset detection:** percussion transients guide beat alignment
- **Key/scale estimation:** tonal center guess reduces clashes
- **Spectral masking:** AI avoids masking the upload's frequencies

### Best Practices: End-to-End Workflow
1. **Prepare audio:** export clean mono/stereo WAV, 44.1kHz; trim silence; avoid heavy FX
2. **Upload & prompt:** "Featured vocal, 100 BPM, D minor, keep natural tone." State role, BPM, key
3. **Structure sections:** guide arrangement with [VERSE], [CHORUS], [BRIDGE]
4. **Refine in passes:** if sync drifts, regenerate sections, not the entire song
5. **Post-process in DAW:** light EQ/comp/reverb; bounce final WAV/MP3

### Troubleshooting Audio Uploads

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Vocal sounds metallic | AI overprocessing | Add "keep natural vocal tone" |
| Instrument bleed | Noisy/effected upload | Use dry, isolated stem |
| Off-beat sync | Unclear/variable BPM | State exact BPM in prompt and sections |
| Wrong-key harmonies | Key misdetected | Specify key (e.g., "C minor") |
| Upload ignored | Too long/noisy format | Pre-trim; resample to 44.1kHz WAV |

### Advanced Hybrid Techniques
- **Double tracking:** upload lead; ask for harmonies/doubles in chorus
- **Instrument anchors:** build orchestration around your riff or motif
- **Remix:** upload legacy stems; modernize style via prompt
- **Sound collage:** field recordings → harmonized pads or percussion
- **Live looping:** 4-bar loop → extended arrangement with evolving sections

---

## Song Editor & Section Workflow

### Section Tools — When to Use Which

**Rewrite:** keep section role/intent; adjust melody/lyrics within the form
**Remake:** generate a new musical idea for that section (respects prompt + sliders)
**Extend:** append bars at the tail; existing bars stay the same
**Reorder:** move sections on the timeline; audio content unchanged
**Delete:** remove weak regions; transitions are engine-handled

### Lock-First Protocol

1. **Lock Chorus:** Remake only the Chorus; Weirdness ↓, Style Influence ↑
2. **Freeze Chorus:** stop remaking it once it lands
3. **Shape Verses:** use Rewrite for diction/phrasing; keep arrangement sparse
4. **Explore Bridge:** Remake here; raise Weirdness one notch
5. **Extend only** for pre-chorus lifts and outros

### Standard Section Map (copy/paste)
```
[INTRO 4] [VERSE 1 8] [PRE 4] [CHORUS 8]
[VERSE 2 8] [PRE 4] [CHORUS 8]
[BRIDGE 8] [CHORUS 8] [OUTRO 4]
```
Numbers = target bar counts. Keep counts stable while you test remakes.

### Energy Curve Rubric

| Section | Energy (1–5) | Notes |
|---------|--------------|-------|
| Intro | 1–2 | Sparse; no lead yet |
| Verse | 2–3 | Lyric clarity; few midrange parts |
| Pre | 3–4 | Riser/perc detail |
| Chorus | 4–5 | Hook instruments + BGV |
| Bridge | 3–4 | Contrast or new motif |
| Outro | 1–2 | Taper; remove leads |

### Editor + Sliders Quick Matrix

| Goal | Editor action | Sliders | Prompt/Edit note |
|------|---------------|---------|------------------|
| Lock a hook | Remake Chorus | Weirdness ↓, Style ↑ | Short, repeatable chorus lyric |
| Fix weak verse | Rewrite Verse | Mid Weirdness/Style | Add concrete instrument tags |
| Add lift into chorus | Extend pre-chorus 1–2 bars | Weirdness +1 | "riser/transition" |
| Try new bridge idea | Remake Bridge | Weirdness ↑ | Keep other sections frozen |
| Smooth transitions | Reorder / Extend tails | Style mid | "soft transition / no hard stop" |
| Upload leads | Remake sections around upload | Audio ↑ | Mark upload "featured"; restate BPM/key |

---

## Pronunciation & Multilingual Guide

### English Pronunciation Pitfalls (Homographs)

Even in v5, guide words that have multiple pronunciations.

| Word | Risk | Likely Misread | Fix (Optimized Spelling) |
|------|------|----------------|--------------------------|
| read | reed/red | Random tense | Use "reed" (present) or "red" (past) |
| live | liv/laiv | Often "liv" | Use "lyve" for concert/live show |
| lead | leed/led | Often "leed" | Use "led" for the metal |
| bass | base/bass | Often "base" | Use "basss" or "bahss" |
| tear | teer/tare | Guesses | Use "teer" (cry) or "tare" (rip) |
| wind | wind/wined | Guesses | Use "wynd" (air) or "winnd" (turn) |

### Best Practices for English Lyrics
- Preview generated lyrics and scan for homographs
- Use phonetic spellings to lock pronunciation
- Shorter lines improve phrasing and stress
- Test multiple personas; some render English stress more cleanly

### Best Practices for Non-English Prompts
- Keep prompts simple: "Emotional ballad in Spanish, piano and strings"
- Write full sentences in custom lyrics to preserve syntax
- Use phonetic spelling for tricky names/words
- One language per section: avoid unintended fallback to English

### Troubleshooting Pronunciation
```
Wrong English pronunciation?
  → Replace with phonetic spelling in lyrics

Song drifts into English?
  → Add "all lyrics in <language>, no English" to prompt

Slang/names misread?
  → Spell them as they sound (phonetic)
```

---

## Instrumentation & Arrangement (v5 Improvements)

### Section-Aware Arrangement

Structure by section for clearer builds:
```
[VERSE] guitar arpeggios + soft bass + light percussion
[CHORUS] full band: brass stabs + gospel choir + synth pad
[BRIDGE] solo piano, atmospheric pads
[OUTRO] guitar fade with strings
```

Section blocks produce clearer builds and payoffs than a single flat prompt.

### Instrument Tagging Guide

Be specific. Type, style, and context matter.

**Core:** bass, drums, guitar, piano, strings
**Expanded:** Rhodes, Hammond organ, sitar, 808, Moog synth
**Specialty:** muted trumpet, steel pan, kalimba, taiko drums

✅ "Spanish nylon guitar arpeggio, funk slap bass, lo-fi Rhodes keys"
❌ "guitar, bass, keyboard"

### Genre Fusion Examples
- Reggae beat + orchestral strings
- Trap drums + gospel choir
- Lo-fi hip hop + kalimba + muted trumpet
- Synthwave pads + flamenco guitar

Add tempo or genre markers for tighter execution (e.g., "90 BPM," "synthwave")

### Troubleshooting Instrumentation

| Problem | Cause | Fix | Extra Tip |
|---------|-------|-----|-----------|
| Muddy mix | Too many mid instruments | Limit to 2–3 mids | Add airy pad or deep sub for contrast |
| Drums off-tempo | Ambiguous tags | "Tight funk drums, 90 BPM" | Repeat BPM in each section |
| Harsh synths | No genre context | "Warm analog" or "lo-fi" | Add "low-pass filtered" or "soft" |
| Missing guitar solo | Vague tag/location | "Featured solo guitar in bridge" | Place solo in a [BRIDGE] block |
| Overstuffed chorus | All parts at once | Stagger entry of layers | Emulate producer workflow |

---

## Tag Combination Strategies

### Layering Approach

**Foundation Layer:** Genre + Tempo + Key instrument
```
Rock + Electric Guitar + Male Vocal
```

**Emotional Layer:** Mood + Atmosphere + Energy
```
+ Dark + Aggressive + Intense
```

**Technical Layer:** Production + Effects + Arrangement
```
+ Raw Production + Reverb Heavy
```

**Structure Layer:** Song sections
```
+ Intro + Verse + Chorus
```

### Dynamic Progression

Vary tags during sections for storytelling:
```
[Intro]: Atmospheric, Mysterious, Clean Electric Guitar
[Verse]: Introspective, Gentle, Acoustic Guitar
[Chorus]: Energetic, Powerful, Distorted Electric Guitar
[Bridge]: Dramatic, Cinematic, String Section
[Outro]: Peaceful, Fade Out
```

### Creative Contrasts

Unite opposite elements for unique results:
```
Gentle + Distorted Electric Guitar = Interesting contrast
Electronic + Acoustic Drum Kit = Organic/digital fusion
Dark + Uplifting = Bittersweet emotion
Classical + Modern = Timeless innovation
```

### Tag Placement Best Practices

**In Lyrics Field (with brackets):**
- Structure tags: `[Verse]`, `[Chorus]`, `[Bridge]`
- Section-specific moods: `[Verse - Introspective]`
- Instrument cues: `[Guitar Solo]`

**In Style Field (no brackets):**
- Genre, mood, instruments, production
- Keep to 15-30 words
- Most important tags first

**At Top of Lyrics (with TAG prefix):**
```
[TAG: STYLE: synth-driven, dreamy, ethereal atmosphere with pulsing bass]
```
This keeps your style secret when publishing (edit lyrics before sharing).

---

*This guide synthesizes best practices from Suno v5 documentation, community testing, and hundreds of prompt experiments. Always verify licensing and platform policies before monetizing AI-generated content.*
