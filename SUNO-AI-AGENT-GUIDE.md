# Suno AI Agent Guide: Prompt Crafting & Lyric Writing (v5)

**Purpose:** This guide is for AI assistants helping users craft Suno v5 prompts and write lyrics. Focus on actionable prompt construction and production workflows.

**Version:** Suno v5 (December 2025)

---

## Core Prompt Formula

```
[Genre] + [Mood] + [Tempo] + [Instruments] + [Vocals] + [Production Quality] + [Emotion]
```

**Optimal length:** 15-30 words (4-7 descriptors)
**Rule:** Most important descriptors first—Suno weights early words more heavily

**Example:**
```
Melodic techno, emotional and driving, 126 BPM, deep analog bass, ethereal pads, female vocal samples, progressive structure, studio-grade clean mix
```

---

## Two Creation Modes

### Simple Mode (500 chars)
Natural language description in one field. Fast iteration, beginner-friendly.

**Example:**
```
Melancholic indie pop, acoustic guitar, female lead, clean mix, mid-tempo 96 BPM
```

### Custom Mode (Full Control)
- **Style field:** 1,000 chars max (genre, mood, instruments, production)
- **Lyrics field:** 5,000 chars max (full lyrics with meta tags)
- **Additional features:** Gendered vocals toggle, instrumental-only option, audio upload (Pro)

---

## v5 Improvements Over v4.5

**Audio Quality:**
- 44.1 kHz, 16-bit stereo (studio-grade)
- Clearer mix separation, tighter low end
- Up to 8 minutes lossless audio (paid plans)
- Multi-stem export: Free (MP3 mix), Pro (2-stem), Premier (up to 12 stems)

**Prompt Understanding:**
- Better syllable-to-beat mapping
- Longer context window (less cutoff/drift)
- Improved pronunciation and phoneme rendering
- More reliable section obedience

**Creative Control:**
- Weirdness, Style Influence, Audio Influence sliders
- Song Editor: Remake, Rewrite, Extend, Reorder, Delete sections
- Audio uploads with role control (featured vs texture)

---

## Prompt Construction Rules

### Always Include
1. **Vocal type:** male/female/falsetto/choir/duet (or "instrumental only, no vocals")
2. **1-2 hero instruments:** acoustic guitar, Rhodes piano, 808s, brass section
3. **Mood + genre:** melancholic indie pop, aggressive trap, dreamy synthwave
4. **Tempo:** BPM number or descriptor (slow pocket, mid-tempo, driving)
5. **Production quality:** 1-2 cues ("clean mix", "studio-grade", "tape saturation")

### Production Quality Descriptors (Critical for Consistency)

**Clean Production:**
- "clean mix"
- "studio-grade"
- "balanced frequency response"
- "no distortion"
- "professional mastering"

**Lo-Fi/Vintage:**
- "tape saturation"
- "vinyl warmth"
- "analog character"
- "lo-fi aesthetic"

**Specific Issues to Avoid:**
- "no harsh highs"
- "no muddy bass"
- "no clipping"
- "no artifacts"

### Avoid
- ❌ Vague prompts: "make a pop song"
- ❌ Overloaded prompts: too many conflicting descriptors (3+ genres)
- ❌ Artist names: use musical descriptors instead
- ❌ Missing vocal specification
- ❌ Too complex: brand names, specific gear models

---

## Creative Control Sliders (v5)

### Weirdness (Safe → Chaos)
~50% = normal baseline

**By Genre:**
- Radio Pop: 35-50
- Hip-hop/Trap: 40-55
- Worship/Gospel: 25-40
- Orchestral: 55-70
- Experimental: 70-85

**By Section:**
- Chorus: Lower (35-45) for consistent hook
- Verse: Mid (40-55) for clarity
- Bridge: Higher (55-70) for novelty

**Rule:** Change one slider at a time; compare 20-30s regions

### Style Influence (Loose → Strong)
How tightly output follows your style input

**By Genre:**
- Radio Pop: 65-80
- Hip-hop/Trap: 55-70
- Worship/Gospel: 70-85
- Orchestral: 45-60
- Experimental: 35-55

**Lock-First Protocol:**
- Lock Chorus: Weirdness ↓, Style ↑
- Freeze when it lands
- Then shape other sections

### Audio Influence (with uploads)
Appears when audio is uploaded

- **60-75:** Featured vocal/riff (lead)
- **20-40:** Ambient texture (background)

---

## Audio Upload Workflow (v5)

### Prepare Audio
1. Export clean mono/stereo WAV at 44.1kHz
2. Trim silence from start/end
3. Avoid heavy FX (reverb, delay, compression)
4. Use dry, isolated stems for best results

### Upload & Prompt
State role explicitly in prompt:
```
Featured vocal, 100 BPM, D minor, keep natural vocal tone
```

Set Audio Influence slider:
- High (60-75) if upload should lead
- Low (20-40) for ambient texture

### Structure Sections
Guide arrangement with section tags:
```
[VERSE] - Sparse, vocal-focused
[CHORUS] - Full arrangement around upload
[BRIDGE] - Atmospheric variation
```

### Troubleshooting Uploads

| Symptom | Cause | Fix |
|---------|-------|-----|
| Vocal sounds metallic | AI overprocessing | Add "keep natural vocal tone" |
| Instrument bleed | Noisy/effected upload | Use dry, isolated stem |
| Off-beat sync | Unclear/variable BPM | State exact BPM in prompt |
| Wrong-key harmonies | Key misdetected | Specify key (e.g., "C minor") |
| Upload ignored | Too long/noisy format | Pre-trim; resample to 44.1kHz WAV |
| Timing drift | BPM/key mismatch | Restate BPM; remake only off section |

### Advanced Upload Techniques
- **Double tracking:** Upload lead; ask for harmonies/doubles in chorus
- **Instrument anchors:** Build orchestration around your riff
- **Remix:** Upload legacy stems; modernize style via prompt
- **Sound collage:** Field recordings → harmonized pads or percussion

---

## Song Editor Workflow (v5)

The Song Editor allows section-level control without re-rolling the entire track.

### Section Tools

| Tool | Function | When to Use |
|------|----------|-------------|
| **Rewrite** | Keep role/intent; change phrasing/lyrics | Fix diction, adjust melody within form |
| **Remake** | New musical idea (respects prompt + sliders) | Try different arrangement for section |
| **Extend** | Append bars at tail; existing audio unchanged | Add transition bars, extend outro |
| **Reorder** | Move blocks on timeline; content unchanged | Rearrange song structure |
| **Delete** | Remove region; crossfades handled | Cut weak sections |

### Lock-First Protocol (Professional Workflow)

1. **Lock Chorus First**
   - Remake Chorus only
   - Weirdness ↓ (35-45), Style ↑ (70-85)
   - Freeze when it lands

2. **Shape Verses**
   - Use Rewrite for diction/phrasing
   - Keep arrangement sparse
   - Weirdness mid (40-55)

3. **Explore Bridge**
   - Remake here
   - Raise Weirdness one notch (55-70)
   - Keep other sections frozen

4. **Extend for Transitions**
   - Add 1-2 bars before/after chorus
   - Smooth section changes

### Standard Section Map
```
[INTRO 4] [VERSE 1 8] [PRE 4] [CHORUS 8]
[VERSE 2 8] [PRE 4] [CHORUS 8]
[BRIDGE 8] [CHORUS 8] [OUTRO 4]
```
Numbers = target bar counts

### Editor Troubleshooting

| Symptom | Root Cause | Editor Fix |
|---------|-----------|------------|
| Chorus not memorable | Variation too high | Lower Weirdness; Remake Chorus; shorten lyric |
| Verse too busy | Too many mid parts | Rewrite; reduce instrument tags |
| Abrupt cuts | Zero-tail regions | Extend 1-2 bars at transitions |
| Hook lost after edits | Later remake overwrote | Revert to saved Chorus version |

---

## Stem Export Strategy (v5)

### Export Tiers
- **Free:** MP3 full mix only
- **Pro:** 2-stem (vocals + instrumental)
- **Premier:** Up to 12 stems (verify in UI)

### Workflow
1. **Solo each stem** → decide keep/mute/replace
2. **Avoid micro-mixing in Suno** → fix arrangement issues in Suno, tone/EQ in DAW
3. **Export for DAW** if tone/EQ issues persist
4. **Use consistent sample rate/bit depth** across exports

### DAW Finishing
- Import stems into Audacity, GarageBand, Reaper, etc.
- Trim and crossfade between sections
- Balance vocal/instrument levels
- Light EQ and reverb as needed
- Export final WAV/MP3

---

## Negative Prompting (Exclusions)

v5 handles negative prompting more reliably than v4.5.

### Effective Syntax
```
"Instrumental only, no vocals"
"Upbeat pop with drums and bass, no guitars"
"Trap beat with piano and synths, no 808s"
"Acoustic guitar focus, no distortion, clear vocals"
```

### Ineffective Syntax
```
❌ "Without singing unless background only"
❌ "No sounds that are bad"
❌ "Not like rock"
```

### Common Uses
- Pure instrumental: `"no vocals"` or `"instrumental only"`
- Remove instrument: `"no electric guitar"` (keeps other guitars)
- Clear mix: `"no synth pads"` (reduces midrange clutter)
- Precision stacking: `"no lead guitar solo"` (keeps rhythm guitars)

### Troubleshooting Negatives
```
Still hearing vocals?
  → Try "instrumental only"
     → If persists → Export stems → Remove vocals in DAW

Mix feels too empty?
  → Reduce exclusions (1-2 max)
     → Add clear positives (what you DO want)
```

---

## Multilingual & Pronunciation (v5)

### Non-English Best Practices
- Keep prompts simple: "Emotional ballad in Spanish, piano and strings"
- Write full sentences in custom lyrics to preserve syntax
- Use phonetic spelling for tricky names/words
- **One language per section** to avoid fallback to English
- Add "all lyrics in <language>, no English" to prevent drift

### Language-Specific Tips

**Spanish:**
```
Latin pop with romantic Spanish lyrics, passionate vocal delivery
```

**French:**
```
Chanson française ballad, poetic French lyrics, soft piano
```

**Japanese:**
```
J-pop upbeat song in Japanese, female vocal, bright synths
```

### Troubleshooting Multilingual
```
Song drifts into English?
  → Add "all lyrics in <language>, no English" to prompt
  
Slang/names misread?
  → Spell them as they sound (phonetic)
```

---

## Lyric Writing

### Structure Tags (Required)
```
[Verse 1]
[Pre-Chorus]
[Chorus]
[Verse 2]
[Bridge]
[Outro]
```

### Formatting Rules
- **4-6 lines per section** (not more)
- **Blank line between sections**
- **2-6 words per line** for best phrasing
- **Consistent syllable count** within sections

### Syllable-to-Beat Alignment
✅ Good (8 beats): "Walk through the fire, I call Your name again"
❌ Bad (too many): "In the fire I still walk, I call Your holy name again now"

**Tip:** Count syllables per line and keep consistent within each section type.

### Pronunciation Fixes (Homographs)

| Word | Problem | Fix |
|------|---------|-----|
| read | reed/red | Use "reed" (present) or "red" (past) |
| live | liv/laiv | Use "lyve" for concert/live show |
| lead | leed/led | Use "led" for metal; "leed" for verb |
| bass | base/bass | Use "basss" or "bahss" for instrument |
| tear | teer/tare | Use "teer" (cry) or "tare" (rip) |
| wind | wind/wined | Use "wynd" (air) or "winnd" (turn) |

### Performance Tags (in lyrics)
```
[Verse 1 - Introspective, Gentle]
[Chorus - Energetic, Powerful]
[Bridge - Sparse, Whispered]
```

**Inline tags:**
```
City lights like scattered stars (breathy)
Stay with me until the morning light (belt)
(Whispered) Maybe we were never meant to stay
```

### Stage Directions
- `[whisper]`, `[rap verse]`, `[falsetto]`
- `[Guitar Solo]`, `[Instrumental Break]`
- `[sing with power]`, `[breathy]`

### Call-and-Response (Duets)
```
[Verse 2]
[male vocal] Who will rise?
[female vocal] I will rise!
```

### Common Lyric Pitfalls
- **Overstuffed lines:** Too many words → off-beat. Fix: shorten to 4-6 words
- **Robotic chorus:** Add repetition ("Shine, shine, shine") or vary delivery tags
- **Cutoff mid-verse:** Break into smaller blocks (4-6 lines max)
- **Forced rhymes:** Rhyme every 2nd or 4th line, not every line

---

## Section-Aware Prompting

### Energy Curve (1-5 scale)

| Section | Energy | Instrumentation Strategy |
|---------|--------|--------------------------|
| Intro | 1-2 | Sparse; no lead yet |
| Verse | 2-3 | Lyric clarity; few midrange parts |
| Pre-Chorus | 3-4 | Riser/percussion detail |
| Chorus | 4-5 | Hook instruments + backing vocals |
| Bridge | 3-4 | Contrast or new motif |
| Outro | 1-2 | Taper; remove leads |

### Section-Specific Prompting
```
[VERSE] acoustic guitar arpeggios + soft bass + light percussion
[CHORUS] full band: brass stabs + gospel choir + synth pad
[BRIDGE] solo piano, atmospheric pads
[OUTRO] guitar fade with strings
```

**Why this works:** Section blocks produce clearer builds and payoffs than flat prompts.

---

## Instrumentation Strategy

### Be Specific
✅ "Spanish nylon guitar arpeggio, funk slap bass, lo-fi Rhodes keys"
❌ "guitar, bass, keyboard"

### Instrument Tiers
- **Core:** bass, drums, guitar, piano, strings
- **Expanded:** Rhodes, Hammond organ, sitar, 808, Moog synth
- **Specialty:** muted trumpet, steel pan, kalimba, taiko drums

### Limit Midrange Clutter
- **2-3 midrange instruments max** (guitar, keys, pads)
- Add contrast: airy pad (high) + deep sub (low)
- If muddy: use negative prompting to remove one mid instrument

### Genre Fusion
- Reggae beat + orchestral strings
- Trap drums + gospel choir
- Lo-fi hip hop + kalimba + muted trumpet
- Synthwave pads + flamenco guitar

**Add tempo/genre markers:** "90 BPM," "synthwave" for tighter execution

---

## Complete Meta Tags Reference

### What Are Meta Tags?

Meta tags are keyword markers that steer structure, style, and production. Most impactful in the first 20–30 words and around section changes.

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

## Advanced Techniques

### TAG Prefix Method (Keep Style Secret)

You can embed your entire style prompt at the top of the lyrics field using the TAG prefix. This keeps your style secret when publishing (just edit the lyrics data before sharing).

**Format:**
```
[TAG: STYLE: synth-driven, dreamy, ethereal atmosphere with pulsing bass and shimmering pads]

[Verse 1]
Your lyrics here...
```

**Why this works:**
- Suno reads the TAG line as style instructions
- You can delete the TAG line before publishing
- Keeps your production secrets private
- Allows more granular control per section

**Example:**
```
[TAG: STYLE: dark trap, 140 BPM, sliding 808s, atmospheric pads, aggressive male vocals]

[Verse 1]
Walking through the shadows...
```

### Two-Layer Prompting System

**Layer 1 (The "What"):** Structure in lyrics box
```
[Verse], [Chorus], [Bridge]
```
This defines the architecture.

**Layer 2 (The "How"):** Sonic character in style prompt
```
...with a sparse, vocal-heavy verse that builds into an explosive, guitar-driven chorus...
```
This suggests the instrumentation and production within that structure.

**Combined Example:**

**Style:** Energetic pop song with sparse verse that builds to euphoric chorus, atmospheric bridge, powerful final chorus

**Lyrics:**
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

### Narrative Arc Prompting

Instead of just describing sound, describe the **journey** of the song.

**Basic:** "An energetic pop song"
**Result:** Often flat, single-level energy

**Narrative Arc:** "An energetic pop song that builds to an euphoric chorus, features an atmospheric bridge that breaks the intensity, and ends with a powerful final chorus. Energy starts medium, explodes in chorus, drops in bridge, peaks at end."
**Result:** Dynamic, professional structure

### Inline Performance Direction

Use parentheses for performance notes within lyrics:

```
[Verse 1]
City lights like scattered stars (breathy)
You and I float past the boulevard (intimate)
Every word we didn't say (building)
Hangs between us, fades away (soft)

[Chorus]
Stay with me until the morning light (belt, powerful)
We'll rewrite every lost goodnight (stacked harmonies)
```

### Spoken Word & Theatrical Elements

For creative/experimental tracks:

```
[Intro - Spoken Word, Confident but Curious]
Hi there. Welcome to the show.
This is not a performance — it's a proof of life.

[Tag: Soft Orchestral Build]

[Verse - Calm, Technical, Hypnotic]
Every sound begins as an instruction
Every emotion starts as code

[Tag: Glitch Beat with Orchestral Choir]
```

### Genre Fusion Rules

**Two genres max:** "Jazz Trap" or "Gospel Drill" works
**Three or more:** Chaos and confusion

**Effective fusions:**
- R&B Trap
- Jazz House
- Gospel Soul
- Reggae Afrobeat
- Lo-fi Hip Hop
- Synthwave Pop

**Ineffective:**
- "Funk Jazz Reggae Drumstep Gospel" (too many)

### BPM Guidelines by Genre

| Genre | BPM Range |
|-------|-----------|
| House / Techno | 120-130 |
| Drum & Bass | 170-175 |
| Pop | 100-115 |
| Lo-Fi / Chill | 70-95 |
| Drill / Grime | 135-145 |
| Trap | 130-150 |
| Hip Hop | 80-110 |
| Ballad | 60-80 |

### Production Quality Descriptors

Always include 1-2 quality cues for consistency:

**Clean Production:**
- "clean mix"
- "studio-grade"
- "balanced frequency response"
- "no distortion"
- "professional mastering"

**Lo-Fi/Vintage:**
- "tape saturation"
- "vinyl warmth"
- "analog character"
- "lo-fi aesthetic"

**Specific Issues to Avoid:**
- "no harsh highs"
- "no muddy bass"
- "no clipping"
- "no artifacts"

### Emotional Arc Mapping

Map energy levels across sections (1-5 scale):

```
[Intro] - Energy 1-2
[Verse 1] - Energy 2-3
[Pre-Chorus] - Energy 3-4
[Chorus] - Energy 4-5
[Verse 2] - Energy 2-3
[Bridge] - Energy 3-4 (contrast)
[Final Chorus] - Energy 5
[Outro] - Energy 1-2
```

Include this in your narrative arc description for better dynamics.

### Instrumental-Only Best Practices

For pure instrumentals, be explicit:

```
Style: Melodic techno, 126 BPM, deep analog bass, ethereal pads, progressive structure, studio-grade clean mix, no vocals, instrumental only

Lyrics:
[Intro]
[Steady kick drum build]

[Drop]
[Full percussion, driving bassline]

[Break]
[Filtered synths, sparse drums]

[Build]
[Add melodic elements, rising tension]

[Final Drop]
[Full energy, all elements]

[Outro]
[Gradual fade]
```

### The Golden Formula

```
Genre + Mood + Tempo + Instruments + Vocals + Production Quality + Emotion
```

**Example:**
"Melodic techno, emotional and driving, 126 BPM, deep analog bass, ethereal pads, female vocal samples, progressive structure, studio-grade clean mix"

### Prompt Complexity Balance

**Too Simple:** "Make a pop song"
- Result: Generic, unpredictable

**Optimal:** "Upbeat indie pop, 110 BPM, jangly guitars, warm bass, female vocals, clean bright mix"
- Result: Clear direction, good consistency

**Too Complex:** "Upbeat indie pop with jangly Rickenbacker 12-string guitars, Fender Precision bass with flatwound strings, Ludwig drum kit with Zildjian cymbals, female soprano vocals with Neumann U87 microphone, SSL console mixing..."
- Result: Confusion, missed elements, artifacts

**Rule:** 15-30 words, 4-7 key descriptors

---

## Copy-Ready Prompt Templates

### Modern Pop
```
Modern pop, emotional female vocals, acoustic guitar verse → bright synth chorus, confessional tone, clean mix, 95 BPM
```

### Melodic Trap
```
Moody trap, laid-back male vocals, ambient pads, deep 808s, late-night atmosphere, reverb-heavy ad-libs, 80 BPM
```

### Neo-Soul
```
Neo-soul groove, silky female lead, stacked harmonies, Rhodes keys, cozy lo-fi warmth, 74 BPM
```

### Cinematic R&B
```
Dark R&B, falsetto male vocals, analog 80s synth bass, gated snare, neon club vibe, glossy mix, 104 BPM
```

### 90s Grunge
```
Grunge trio, distorted guitars, raw male vocals, quiet-loud-quiet dynamics, tape saturation, 116 BPM
```

### Gospel-Soul
```
Gospel-soul ballad, powerful female lead, Hammond organ, live choir call-and-response, emotional lift, 72 BPM
```

### Melodic House
```
Atmospheric melodic house, airy male vocal, long-tail reverb, rolling bassline, sunset emotion, 120 BPM
```

### Orchestral Score
```
Orchestral score, string ostinatos, brass swells, taiko hits, massive dynamics, heroic finale, tempo shifts 80-120 BPM
```

### Tech House / EDM
```
Tech House, energetic, 128 BPM, drum machine, electric piano, punchy kicks, synth pads, 4/4 time, club-ready mix, no vocals
```

### UK Drill
```
UK Drill, dark, aggressive, 140 BPM, TR-808 drums, massive sub-bass, sliding 808 bassline, fast hi-hat rolls, raw male vocals
```

### Deep House
```
Deep House, smooth, soulful, 122 BPM, warm bassline, Rhodes piano, vinyl crackle, atmospheric pads, gentle female vocals, lo-fi texture
```

### Liquid Drum and Bass
```
Liquid Drum and Bass, melodic, 174 BPM, breakbeat drums, deep sub-bass, lush pads, female vocal samples, atmospheric
```

### Synthwave
```
Synthwave, nostalgic, 120 BPM, analog synths, gated drums, arpeggiators, retro bass, cinematic pads, 80s production, no vocals
```

---

## Prompt Construction Workflow

### Step 1: Identify Core Elements
Ask user:
- Genre/style?
- Mood/emotion?
- Vocal type (or instrumental)?
- Key instruments?
- Tempo feel?

### Step 2: Build Foundation (15-30 words)
```
[Genre] + [Mood] + [1-2 Instruments] + [Vocal Type] + [Tempo]
```

### Step 3: Add Production Detail (if needed)
```
+ [Mix Tone] + [Specific Production Element]
```

### Step 4: Set Sliders
- Chorus/Hook: Weirdness ↓ (35-45), Style ↑ (70-85)
- Verse: Weirdness mid (40-55), Style mid (55-70)
- Bridge: Weirdness ↑ (55-70), Style mid (45-60)

### Step 5: Add Exclusions (if needed)
- Instrumental? → "no vocals"
- Avoid specific instrument? → "no [instrument]"
- Clear muddy mix? → "no synth pads" or "no rhythm guitar"

---

## Lyric Writing Workflow

### Step 1: Structure Planning
```
[Verse 1] - 4-6 lines
[Chorus] - 4-6 lines (repeatable hook)
[Verse 2] - 4-6 lines
[Chorus] - repeat exact same lines
[Bridge] - 4-6 lines (contrast)
[Chorus] - repeat exact same lines
```

### Step 2: Syllable Consistency
- Count syllables in first verse line
- Match that count for other verse lines
- Chorus can have different count, but keep it consistent across all choruses

### Step 3: Rhyme Scheme
- AABB (couplets): sky/high, way/stay
- ABAB (alternating): night/day, light/way
- ABCB (2nd & 4th): stars/boulevard, say/away

### Step 4: Check for Homographs
Scan for: read, live, lead, bass, tear, wind
Replace with phonetic spellings if needed

### Step 5: Add Performance Tags
- Verse: `[Verse 1 - Introspective, Gentle]`
- Chorus: `[Chorus - Energetic, Powerful]`
- Bridge: `[Bridge - Sparse, Whispered]`
- Inline: `(breathy)`, `(belt)`, `(whispered)`

---

## Troubleshooting Common Issues

### Quick Reference Matrix

| Symptom | Cause | Fix | Additional Action |
|---------|-------|-----|-------------------|
| Output too generic | Vague descriptors | Add unique instrument + specific mood; increase Style Influence to 70-80 | Be more specific: "Spanish nylon guitar" not "guitar" |
| Output too chaotic | Too many descriptors | Reduce to 4-7 descriptors; lower Weirdness to 35-45 | Put primary genre first |
| Wrong genre blend | Genre order/conflict | Put primary genre first; remove conflicting descriptors | Use negative prompting |
| Lyrics cut off mid-verse | Lines too long | Shorten to 4-6 words per line; break into smaller blocks (4-6 lines max) | Reduce total lyric length |
| Mispronounced words | Homographs | Replace with phonetic spelling (see table) | Try different vocal persona |
| Chorus sounds robotic | No variation | Add repetition ("Shine, shine, shine"); use stage directions | Vary delivery: (belt) or (breathy) |
| Muddy mix | Too many mids | Limit to 2-3 midrange instruments; use negative prompting | Add contrast: airy pad (high) + deep sub (low) |
| Off-tempo drums | Ambiguous BPM | State exact BPM: "tight funk drums, 90 BPM" | Add tempo descriptor: "driving," "laid-back" |
| Hook inconsistent | Weirdness too high | Lower Weirdness; Remake chorus only | Freeze chorus when it lands |
| Verse crowded | Too many parts | Rewrite; remove 1-2 mid tags | Keep 2-3 mids only |
| Upload ignored | Audio Influence low | Raise Audio Influence; mark "featured" | Trim/denoise upload |
| Timing drift (uploads) | BPM/key mismatch | Add BPM/key; Remake only off section | Align stems in DAW |
| Vocal sounds metallic | AI overprocessing | Add "keep natural vocal tone" | Lower Audio Influence |
| Abrupt section cuts | Zero-tail regions | Extend 1-2 bars at transitions | Add short fades in DAW |

### "Output is too generic"
- Add one unique instrument + one specific mood word
- Increase Style Influence to 70-80
- Be more specific: "Spanish nylon guitar" not "guitar"

### "Output is too chaotic"
- Reduce to 4-7 descriptors max
- Lower Weirdness to 35-45
- Put primary genre first

### "Wrong genre blend"
- Put primary genre first (Suno weights early words more)
- Remove conflicting descriptors
- Use negative prompting to exclude unwanted elements

### "Lyrics cut off mid-verse"
- Shorten lines to 4-6 words each
- Break into smaller verse blocks (4-6 lines max)
- Reduce total lyric length

### "Mispronounced words"
- Replace with phonetic spelling (see homograph table)
- Try different vocal persona
- Add pronunciation guide in parentheses

### "Chorus sounds robotic"
- Add repetition: "Shine, shine, shine"
- Use stage directions: `[sing with power]`
- Vary delivery: `(belt)` or `(breathy)`

### "Muddy mix"
- Limit to 2-3 midrange instruments
- Use negative prompting: "no synth pads"
- Add contrast: airy pad (high) + deep sub (low)

### "Off-tempo drums"
- State exact BPM: "tight funk drums, 90 BPM"
- Repeat BPM in section tags if needed
- Add tempo descriptor: "driving," "laid-back," "swung feel"

---

## Quick Checklist

### Before Generating
- [ ] Vocal type specified (or "no vocals")
- [ ] 1-2 hero instruments named
- [ ] Mood + genre clear
- [ ] Tempo set (BPM or descriptor)
- [ ] Production quality descriptor included
- [ ] 15-30 words total (4-7 descriptors)
- [ ] Most important elements first
- [ ] Lyrics: 4-6 lines per section
- [ ] Lyrics: structure tags present
- [ ] Lyrics: checked for homographs
- [ ] Sliders set for section type

### Pre-Export QA (v5)
- [ ] Chorus repeats identically; no drift
- [ ] Verse intelligible in mono
- [ ] Transitions smooth; tails extended where needed
- [ ] Uploads in tune/time; BPM/key consistent
- [ ] Stems test-imported; alignment confirmed (if using stems)

---

## Example: Complete Prompt Construction

**User request:** "Sad indie song about a breakup, female voice"

**AI Agent Process:**

1. **Identify elements:**
   - Genre: indie pop
   - Mood: melancholic, reflective
   - Vocal: female, breathy
   - Instruments: acoustic guitar, warm pads
   - Tempo: slow-mid (96 BPM)

2. **Build prompt:**
   ```
   Melancholic indie pop, acoustic guitar, warm synth pads, female breathy vocal, intimate late-night vibe, clean bright mix, 96 BPM
   ```

3. **Set sliders:**
   - Weirdness: 40 (slightly conservative for radio-friendly)
   - Style Influence: 70 (clear adherence to indie pop)

4. **Write lyrics:**
   ```
   [Verse 1]
   City lights like scattered stars
   You and I float past the boulevard
   Every word we didn't say
   Hangs between us, fades away

   [Chorus]
   Stay with me until the morning light
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

   [Bridge - Sparse, Whispered]
   Maybe we were never meant to stay
   Maybe love is learning to walk away

   [Chorus - Full intensity]
   Stay with me until the morning light
   We'll rewrite every lost goodnight
   Hold the silence, let it breathe
   Find the truth in what we need
   ```

5. **Final check:**
   - ✅ Vocal type: female breathy
   - ✅ Instruments: acoustic guitar, warm pads
   - ✅ Mood: melancholic, intimate
   - ✅ Tempo: 96 BPM
   - ✅ Lyrics: 4 lines per section
   - ✅ Structure tags present
   - ✅ No homographs detected

---

## Key Principles for AI Agents (v5)

1. **Always ask clarifying questions** if genre, mood, or vocal type unclear
2. **Start with the formula:** Genre + Mood + Tempo + Instruments + Vocals + Production Quality
3. **Keep prompts 15-30 words** (4-7 descriptors)
4. **Most important first:** Suno weights early words more
5. **Include production quality:** Always add 1-2 quality descriptors
6. **Lyrics: 4-6 lines per section** maximum
7. **Check for homographs:** read, live, lead, bass, tear, wind
8. **Add performance tags** for dynamic delivery
9. **Set sliders by section type:** Chorus (conservative), Bridge (experimental)
10. **Use negative prompting** to exclude unwanted elements
11. **Lock chorus first** in Song Editor workflow
12. **For uploads:** State BPM/key explicitly; set Audio Influence appropriately
13. **Multilingual:** One language per section; add "no English" if needed
14. **Export strategy:** Fix arrangement in Suno, tone/EQ in DAW
15. **Iterate:** Generate 2-3 versions, pick best, refine

---

## Final Notes

- **Treat Suno like a producer:** Give clear direction, not vague inspiration
- **Simple structure > complex chaos:** Clear sections beat overloaded prompts
- **Strong keywords > generic descriptions:** "Spanish nylon guitar" beats "guitar"
- **v5 advantages:** Use Song Editor for section control, Audio Uploads for collaboration, Stems for DAW finishing
- **Lock-first workflow:** Perfect the chorus, then build around it
- **Production quality matters:** Always include quality descriptors for consistency
- **Iterate fast:** Test variations, use sliders strategically
- **Generate multiple takes:** 2-3 versions, pick best, refine in Song Editor

This guide prioritizes actionable prompt construction and v5 production workflows. Focus on helping users craft precise, effective prompts, leverage v5 features, and achieve professional results.
