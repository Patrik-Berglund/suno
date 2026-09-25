# Suno AI Agent Guide: Prompt Crafting & Lyric Writing (v6)

**Purpose:** This guide is for AI assistants helping users craft Suno prompts and write lyrics. Focus on actionable prompt construction and production workflows.

**Version:** Suno v6, current as of Sept 2026. All older models (v4.5, v5, v5.5) are **retired for new generations, with no UI option to pick one** — per Suno's own blog post and help center FAQ, and **directly confirmed by the user on the live Suno web app**. Previously generated songs remain playable; any new generation runs on v6 or its `v6-wild` / `v6-mini` variants (see [Suno v6: Model Variants & New Capabilities](#suno-v6-model-variants--new-capabilities) below). **The pre-v6 version of this guide is preserved as-is at `SUNO-AI-AGENT-GUIDE-V5.5.md`** — that model's character/behavior is gone from the live product, but the old guide's own reasoning and recipes remain a useful reference in their own right, un-diluted by v6-era caveats. Most of the general tag vocabulary below (structure tags, meta tags, lyric-writing mechanics) is carried forward from that older guide since it's mostly model-version-agnostic Suno syntax — but where a v6-specific behavior is documented below, treat that as the current word over anything in the old file.

**⚠️ Source reliability:** This guide is compiled from community testing, blog posts, and inference — not Suno's official documentation or engineers, except where explicitly marked as sourced from Suno's own blog/help articles or official tutorial videos (e.g. the v6 section below). Nobody outside Suno actually knows the model internals; claims here about *why* something works (tag processing, weighting, what the Exclude field does mechanically) are best guesses inferred from observed behavior, not confirmed architecture. Treat every claim as a hypothesis to test against your own generations, not a fact. When something in here contradicts what you're actually hearing back from Suno, trust the audio over the doc — and update the doc.

---

## Suno v6: Model Variants & New Capabilities

Sourced from Suno's official v6 blog post ("Introducing v6"), help center FAQ, and Suno's own "transitioning to v6" tutorial video (official, first-party — treat as more reliable than the community-inferred material elsewhere in this guide). Still light on explicit prompt-syntax/tag detail in places noted below.

**Model variants (replace all prior model versions):**
- **v6** — flagship, Pro/Premier only. Predictable and reliable — start here when you have a clear vision and want to land it directly.
- **v6-wild** — Pro/Premier only. More varied, gives ideas more room to go in unexpected directions. **Confirmed (official tutorial):** this is explicitly the intended replacement for "I keep going back to an older model for the variation/grit/personality" — if that's what you miss, start with v6-wild, not the flagship.
- **v6-mini** — free tier. Faster/lighter than prior free-tier models.

**Recommended workflow across the two paid variants:** you're not locked into one. Use v6-wild to find an interesting idea/direction from a prompt, then carry that same direction into flagship v6 to polish and control it — mirrors the old "explore on one model, finish on another" workflow some users had.

**New creation capabilities:**
- **Partial song editing** — change one section via plain-language instruction while the rest of the track is preserved untouched. Overlaps with the existing [Song Editor Workflow](#song-editor-workflow) tools (Rewrite/Remake/Extend); still unclear if this is a new surface or a rebrand — verify in the current UI.
- **Multi-source mashups** — combine elements from different songs in one request (e.g. "vocals from X, drums from Y").
- **Sample-to-beat workflow** — isolate/extract a specific section of an existing track to build a new arrangement around.
- **Vibe-based creation** — generate from a feeling/atmosphere alone ("a song that feels like midnight on a rooftop") rather than requiring explicit genre/instrument/tempo descriptors. Suno's copy frames this as improved natural-language understanding of mood and reference, not just literal keyword matching — worth testing whether the keyword-dense [Core Prompt Formula](#core-prompt-formula) is still the more reliable default or whether vibe-style prompts now compete with it.
- **Multimodal input** — text, audio, image, and video can now all be creative starting points (not just audio upload as in the earlier [Audio Upload Workflow](#audio-upload-workflow)).
- **Lyric refinement** — change a single word or line without triggering a full regeneration of the vocal take.

**New/changed controls:**
- **Variety slider** — **confirmed mechanism, quoting Suno's own V6 FAQ (relayed via a third-party writeup that quotes it verbatim, so treat the quote itself as first-party, the writeup's interpretation around it as community-tier):** Variety works by "adjusting and updating your style prompts" — it literally rewrites/expands the text of your style field before generation, and setting it to 0 lets you "retain full control of your style tags." That's a sharper, more mechanical claim than "explores different directions" (from the official tutorial video, [above](#suno-v6-model-variants--new-capabilities)) — the two aren't necessarily contradictory (rewriting the prompt is plausibly *how* two takes end up diverging), but the practical implication is bigger than it first looked: at any Variety above 0, Suno may rewrite a style prompt you spent real time crafting before it ever generates. If you're doing careful keyword-formula or narrative-prose prompting per this guide, **set Variety to 0** or the model may not be reading the prompt you wrote. "Normal" is the default for v6/v6-mini. If **My Taste**/Personalize is enabled, Variety can also pull on your taste profile — but turning Personalize *off* does **not** stop Variety from rewriting; they're separate controls, and community reports describe users assuming otherwise and being wrong.
- **First-party confirmation of the rewrite mechanism (this project, Sept 2026) — directly observed in the UI, not inferred:** the user can see the actual rewritten style text Suno produces at Variety >0, and it doesn't just reorder your existing words — it swaps in new descriptors that weren't in your prompt and drops some that were. This is stronger evidence than a round-trip audio re-upload/auto-caption diff (below), since it's the literal rewritten prompt text, not a reconstruction from the audio — and it's a direct, concrete confirmation of the FAQ's "adjusting and updating your style prompts" language at the content level, not just a word-order shuffle. Practical implication: at Variety >0, treat your style field as a *starting point* Suno edits, not the literal text it generates from — don't assume a descriptor survived just because you wrote it, don't assume an unwanted element in the output came from a bad prompt rather than a swapped-in addition, and check the actual rewritten style text in the UI after generating rather than guessing. Variety 0 remains the only way to guarantee the literal text you wrote is what's used.
- **Confirmed: Weirdness and Style Influence still exist as separate sliders alongside Variety on v6** — the [Creative Control Sliders](#creative-control-sliders) section below still applies. Community-reported pairing for **obedience** (reproduce exactly what you asked for): Variety 0, Weirdness low (~20), Style Influence high (~75-85) — note V6 is reported to obey a given Style Influence value more literally than v5.5 did, so you may not need to push it as high as old habits suggest. Community-reported pairing for **surprise** (chase the old models' unpredictability): Weirdness high, Style Influence loose, Variety above 0, ideally on **v6-wild** rather than flagship v6. **Confirmed to do nothing:** typing slider values as text into the style field ("weirdness 20%, style influence 80%") — the sliders are a separate UI control under Advanced Options; words in the style field are just words to the model, and several viral prompt templates that include this are just carrying dead text.
- **Max Mode** — optional paid add-on (extra credits). **Confirmed use case (official tutorial + Suno FAQ):** most relevant when the song has an audio influence (a cover, or a custom voice) — it reduces stylistic/vocal *drift* as the track progresses, especially past the 2-minute mark, and helps keep the musical style consistent as the song develops. It is a switch, not a slider, and doesn't fix a rewritten prompt or a bad arrangement — reach for it on the take you intend to keep, not while exploring.

**Field note — obedience vs. surprise, confirmed against this project's own generations (Sept 2026):** after ~50 v6 generations, the user reports v6 "follows the instructions more closely, which surprisingly has led to less interesting results... generates less surprising and more mainstream results" compared to v5.5, though prompting technique may also be a factor. This matches the dominant community theme across launch-week reports (see below) almost word for word: "better fidelity, worse feel." Treat this as the default hypothesis for any v6 session that feels flat — before assuming a bad prompt, try the surprise-pairing above (Weirdness high, Style Influence loose, Variety >0, v6-wild) rather than writing a longer, more careful prompt, since a *more* careful/literal prompt is likely to push v6 further toward safe and mainstream, not away from it.

**Cross-checked against real user reports (comments on Suno's own official "Transitioning to v6" YouTube video, Sept 2026 — anecdotal per-user reports, not aggregated data, but numerous and independent, and they converge on the same complaints across many separate commenters):** the "generic/bland/sterile/radio-friendly" complaint is the single most repeated theme, echoing this project's own finding above almost exactly — one commenter's summary of the new Variety slider was "I had variety before. What I don't have now is consistency," a pointed complaint that the thing renamed "Variety" doesn't feel like it delivers variety in practice. Other recurring, more concrete complaints worth treating as open risks rather than settled facts: style-field instructions reportedly sometimes ignored outright ("does not follow my style prompts and adds crap I do not want" — plausibly the Variety-rewrites-your-prompt mechanism above surfacing as "ignored my prompt" to the user), and increased background artifacts/noise in some generations. Take all of this as convergent-but-unverified sentiment, exactly like the rest of this guide's community-tier material — but convergence across independent official-tutorial claims, third-party blog testing, real user comments, and this project's own generations is stronger signal than any one source alone.

**A recommended starting recipe, independently convergent across four separate sources (official tutorial's "start from defaults," the Undetectr blog's Variety/Weirdness/Style Influence explainer, an independent Redditor's own tested numbers, and that Redditor's commenters confirming similar numbers worked for them):** for **obedience/control** — Variety 0, Weirdness under 50% (one source's finer scale: 0-30% controlled/clean, 30-50% "creative sweet spot," 50-60% adventurous, 60%+ experimental), Style Influence 80-95%. Skip Max Mode during early calibration generations — save it for the take you're keeping. This isn't a magic universal preset (no source claims that, and this guide agrees with that caution) but the fact that multiple independent people landed on roughly the same numbers by their own separate testing is more convincing than any single source's claim would be alone.

**⚠️ Important counter-signal — some users report prompting doesn't move the needle at all:** not everyone agrees the structured-prompting approach above actually works. Direct quotes from real users on the same Reddit thread this recipe came from: "No matter if I do a one sentence prompt or a clearly structured one telling it exactly what to do structure and mix-wise, it defaults to the generic v6 sound. Literally no difference in the mix between the two approaches." And: "It's not the user, it's how the model was trained." A separate, credible-sounding technical complaint from the same thread: a user says they ran an actual EQ analysis on downloaded v6 tracks and concluded v6 "does not know how to mix. At all. It defaults to a shitty, unbalanced EQ" — unverified methodology, but worth taking as a data point that some of the muddiness/dullness reported under [Cause 3: the render itself](#suno-v6-community-reported-issues--fixes) may not be prompt-fixable for every account or genre, no matter how carefully the guide's own advice is followed. **Practical implication:** treat every fix in this guide's v6 sections as "worth trying first," not as a guarantee — if several genuinely different, careful attempts produce no audible difference at all, that's itself useful information (the problem may be the model/genre combination, not your prompt), not a sign to keep iterating indefinitely.

**Mixed reports on Cover preserving character from older-model songs:** the Undetectr duet guide (above) reports v6 Covers hold the original melody/vocal character well. At least one independent Reddit user reports the opposite for their own songs: "I can't for the life of me get it to produce anything close to the musical styles of my old songs. Even cover of the old v5/v5.5 just sounds like the AI is tired." Treat Cover fidelity as unresolved/inconsistent rather than reliable, and test it on the specific song you care about before assuming it will carry the character forward.

**⚠️ Reported discrepancy — Voices may not survive migration cleanly despite official claims:** multiple commenters report that a custom Voice profile cloned under v5.5 no longer resembles their actual voice after the v6 migration — one specifically reported their voice profile now produces "a different accent" entirely (going in as their own voice, coming out as what they described as "an Argentine lady that I am not"), and noted v5.5 had been the documented required model for that Voice profile. This directly contradicts the official tutorial's claim (below) that existing voices/custom models "keep working" unchanged under v6. **Practical implication:** if you have a saved custom Voice from before the v6 migration, verify it still sounds like itself with a fresh test generation before relying on it for real work — don't assume automatic-carryover claims held up for your specific voice.

**Working with songs already generated (Remaster vs. Cover):** two distinct post-generation operations, easy to conflate:
- **Remaster** — improves audio quality/acoustic detail of a track you already have; does not reinterpret it. Use when you like the song as-is and just want cleaner audio.
- **Cover** — lets the new model reinterpret the song (arrangement, texture, performance) while following the original melody. Use when you want the *idea* carried forward but re-rendered through v6, not just cleaned up.

**Custom models:** if you built a custom model on an older generation, it does not need to be rebuilt — Suno's official claim is that it's automatically updating the underlying engine so existing custom models keep working under v6. Covers, voices, and "inspo" tools also all remain available in the UI; only the model generation powering them changed. **See the reported discrepancy immediately above** — verify against your own account rather than assuming this claim held up perfectly.

**Getting new-model defaults right:** when first testing v6/v6-wild, start from default slider settings — Suno tunes these as the intended starting point — generate a few songs, listen to what the model is actually doing, then adjust from what you hear rather than pre-emptively cranking settings.

**Migrating a workflow built around an older model — don't chase the model, chase the quality:** the official guidance is explicit here — don't try to force v6 to behave like an old model by model choice alone. Instead identify the *specific quality* you liked and write it directly into the prompt as a descriptor: "imperfect vocals" if you liked vocal imperfection, "rougher production" if you liked grit, or the actual instrumentation/recording-quality/performance characteristics if you were chasing a specific older aesthetic. Model choice (v6 vs. v6-wild) plus the Variety slider gets you *unpredictability*; explicit descriptors get you the *specific texture* — use both together rather than expecting either alone to reproduce an old model's feel.

**Unchanged per the FAQ:** credit cost (10 credits per dual-song generation); Simple Mode still auto-selects tools on your behalf.

**Why old prompts reportedly don't transfer:** per Suno's own launch messaging, v6 was built with label partners (Warner, BMG, Believe) on a different, licensed dataset — not a fine-tune continuing from v4.5/v5/v5.5's training data. If a prompt that reliably worked on v5.5 does nothing on v6, that's a plausible reason why, not just a sign you need to add more descriptors. Community reports (below) suggest the practical fallout skews by genre: mainstream pop/rock/folk/country reportedly hold up well or improve; heavily distorted/extreme genres (metal, drum & bass, other bass-heavy electronic) reportedly got worse. Unconfirmed by Suno directly, but consistent across independent reports — treat the [Genre Confidence Tiers](#genre-confidence-tiers) table below as needing its own v6-era re-verification, not an inherited given.

---

## Suno v6: Community-Reported Issues & Fixes

**Reliability of this section:** everything below is other people's inference from launch-week testing and Reddit threads — the same tier as the rest of this guide's community-sourced material, not Suno documentation, regardless of how confidently any source states it. Treat every fix here as a hypothesis to test on your own generation, exactly per this guide's standing rule. Where a source directly quotes Suno's own help text verbatim, that quoted fragment is called out as such; the surrounding interpretation is not.

**Vocals reading lyrics instead of singing them:** the most common early complaint. Reported cause: v6 performs the syllables you actually wrote, literally and at whatever density they're written, rather than the older models' habit of dropping/stretching syllables to fit the beat. A dense lyric with no delivery instruction gets performed as flat, rushed text.
- Count syllables against tempo before writing a delivery cue: roughly 6-8 syllables per verse line, 4-6 per chorus line for a ballad-paced song, with the last word of chorus lines landing on an open vowel (ay/oh/oo/ah) so there's something to hold.
- Write the hold directly into the lyric text, not just as an instruction: stretching the vowel on the page ("sta-a-ay") is reported as more effective than telling the model to sustain a note in the style field alone.
- Separate the singer (identity: range/texture/age, stays constant) from the performance (pacing/holds/breath/dynamics, changes per section) as two different clauses rather than one adjective doing both jobs.
- Make verse and chorus different **on the page**, not just in adjectives — same line length + same instructions in both sections reportedly gets sung identically. Vary pace, energy, holds, and breathing per section deliberately.
- A sung/hummed reference (even a rough phone recording) is reported as more reliable than any text description for phrasing — see the audio-seed note below.
- Reported ordering tip (unconfirmed mechanism, costs nothing to try): Genre → Vocals → Drums/Guitars/Bass → Arrangement/energy → Production → Ending instruction, i.e. vocal description early, right after genre.

**Band/arrangement drops out under the vocal (especially rock/metal):** reported cause: an adjective-only prompt ("big riffs, punchy drums") is a complete instruction for an intro with no vocal, but says nothing about what instruments should do once a voice enters — and v6 reportedly fills gaps by having instruments get out of the singer's way, rather than the older models' habit of just continuing anyway.
- Build a per-section instrument map before writing the style field: for each of guitar/drums/bass (add more rows as needed), specify verse/chorus/bridge behavior explicitly — e.g. "guitar: intro riff continues under the verse vocal, palm-muted and lower, never stops."
- Use jobs/verbs, not adjectives, per instrument per section ("answers the vocal," "drives," "drops out," "holds") rather than describing a static sound.
- Restate the same instruction as a short bracketed cue at the top of each lyric section — reported to be read at the moment that section renders, so it reinforces the style-field instruction rather than duplicating it uselessly. Keep the two in agreement; a contradiction between style field and section tag reportedly gets resolved by the model thinning the arrangement.
- Heavy/distorted genres (metal, hard rock) are reported as a harder case the map alone won't fully fix — distorted guitars and drums allegedly sound synthetic/over-compressed on v6 regardless of prompt. Try v6-wild for these before concluding the prompt is at fault.

**Vocals sound muffled/buried/dull:** reported as three distinct causes needing different fixes, worth diagnosing before changing anything:
1. **Arrangement too dense** — too many instruments crowding the vocal's frequency range. Fix: specify per-section what's *not* playing under the vocal ("verse: only acoustic guitar and bass, no drums, no pads, no strings"), paired with Exclude entries for the worst offenders (pads, strings, synth layers).
2. **Vocal never placed** — arrangement is fine but nothing told the model where the voice sits. Fix: use placement language, not quality adjectives — "in front of the band, close-miked and dry, the loudest element in the mix" is reported as actionable; "crisp, clear, professional mix" is reported as not (the model has nothing to act on).
3. **Dull render** — a genuine model-level lack of high-frequency content on some generations, independent of prompt. Reported not fixable by prompting at all. Mitigations: regenerate the same prompt (render quality reportedly varies generation-to-generation more than prompt-to-prompt), try v6-wild, keep songs under ~3.5 minutes (degradation is reported concentrated in the back half of longer tracks), or fix in post (a high shelf ~8kHz, a cut ~200-400Hz) rather than in the prompt.

**Duet vocals randomly swap between singers:** reported cause: without an explicit assignment, v6 has to guess who sings each line and guesses differently each generation — worse than older models, which reportedly drifted into a "good enough" default on their own.
- Name both singers once in the style field ("Singer A: male baritone... Singer B: female alto...") and reuse those exact names as section tags (`[Verse 1 - Singer A]`) and inline for traded lines (`(Singer B)`).
- Pick one structure deliberately rather than mixing: **alternating** (one singer per whole section — easiest to control), **call-and-response** (traded lines within a section — keep each traded line to ~6 syllables or fewer, since a longer line reportedly gives room for a mid-line swap), or **harmony** (both singers on the *same words* at once — reported reliable; different words sung simultaneously is reported as not).
- If a solid solo version already exists, Cover it with a duet-style-field addition rather than generating fresh — reported to hold the original melody more reliably, though it tends to give both singers the same tune (fine for alternating/harmony, not for a bridge needing two different melodies).

**Unwanted intro vocals/humming, or overlong/cut-off endings:** reported cause: an unspecified song edge is an invitation for the model to improvise there, and it improvises with a vocal texture at the start and a vamp at the end.
- State what the intro/outro *is* in positive terms with an explicit bar count in both the style field and a lyric tag (e.g. "8 bar instrumental intro, piano only, no vocal of any kind" + `[Intro - piano, 8 bars, no vocal]`), rather than only saying what it isn't.
- **Never name the unwanted element in the style field** — reported (and consistent with this guide's existing [Negative Prompting](#negative-prompting-exclusions) advice) that writing "no humming" can reinforce humming, since the word is now in the prompt regardless of "no." Put unwanted elements in the **Exclude field** as short categories (`humming, vocal intro, spoken intro, ad-libs, fade out`), and put the positive instruction in the style field instead.
- Give the ending a stated length ("4 bar instrumental outro, fade to silence by the end of bar four" or "hard stop after the last chorus, no outro") — "outro" alone with no bound is reported to reliably run long.
- Cut-off final lyric lines are reported as usually a lyric-length problem (too many words for the space) rather than a tagging problem — trim a verse, end on a short final line, and follow it with an explicit `[End]` tag before assuming the arrangement is broken.
- **Safety-buffer technique (independent Reddit source, Sept 2026, unconfirmed but a clever, cheap-to-try idea):** rather than ending the lyric on the final sung line, deliberately add a disposable `[Instrumental Outro]` + `[Hard Stop]` + `[End]` block *after* the final chorus. The idea: if v6 decides to end the song a beat early, it reportedly "spends" that decision on the disposable instrumental buffer instead of cutting off the vocalist mid-word. Explicitly reported as a **prompting aid, not a guaranteed technical fix** — worth trying before assuming the arrangement itself is broken, but don't treat `[Hard Stop]`/`[End]` tags as hard guarantees.
- **Keep bracket/section tags short.** The same source reports that long paragraphs written inside a bracket tag can be partially ignored or misinterpreted piecemeal — put the detailed direction in the style field instead, and use the bracket tag only as a short label/cue (consistent with this guide's existing per-section tag advice elsewhere, but worth stating as an explicit caution here: brevity in tags, detail in the style field, not the reverse).
- For a take that's otherwise good except the intro/outro, partial editing or the Song Editor's trim/replace tools are reported cheaper and more reliable than a full regeneration — though plain-language single-line edits are also reported as inconsistent this early (see caveat under [New creation capabilities](#suno-v6-model-variants--new-capabilities) above).

**Can't get a solo instrument without a full backing band:** reported cause — a long-standing confusion predating v6 between two different requests. **"Instrumental"** means no vocals (drums/bass/pads are still fair game). **"Solo"** is ambiguous, since in training data it often means a lead break *within* a band arrangement, not a single unaccompanied performer.
- Describe a single performer in a situation, not a genre tag: "one acoustic guitarist, alone in a quiet room, fingerstyle" is reported more reliable than "solo acoustic guitar."
- Exclude every other instrument category explicitly (`drums, percussion, bass, synth, pads, strings, vocals`) — reported as more load-bearing on v6 than on older models for this specific problem.
- Tag every section, not just the intro, as solo-only — an untagged later section is reportedly where the band reappears.
- If prompting still fails: stem separation works when the target instrument is prominent in a sparse mix and reportedly degrades in dense mixes; Suno Studio (a distinct multi-track surface) is the reported fallback for reliably isolating one part.

**Audio-seed workflow (voice memo / hummed melody → song):** consistent with and extending this guide's existing [Audio Upload Workflow](#audio-upload-workflow) section — reported specifically strong on v6.
- Melody, rhythm/phrasing, and (if you say "matches the uploaded recording") key/tempo are reported to survive into the generation reliably. Tone/timbre does not — the model's singer performs your melody, not in your voice, unless combined with a saved custom voice.
- With audio attached, write the style field to describe *everything except* the hook — the recording already is the hook. State explicitly that the upload defines a specific part ("the uploaded audio is the chorus melody, keep that melody exactly for every chorus") and let the style field describe the band/arrangement/instruments around it.
- Audio Influence appears once audio is attached; change it on its own between generations, not simultaneously with Style Influence/Weirdness/Variety, per this guide's existing one-change-at-a-time debugging principle.
- A rough 20-40 second phone recording (hummed or played) is reported as sufficient — steady tempo and clear pitch matter more than recording quality.

**Vocal identity drifting mid-song (first-party observation, this project, Sept 2026, unconfirmed elsewhere):** one generation started on a female vocal and gradually morphed into a male vocal over the course of the track, with no such instruction in the prompt. Not reported in any of the sources above, so treat as an anecdotal single-occurrence data point, not a known pattern — but plausibly connected to the broader "consistency" complaints in this section (the same instability that lets a vocal/style drift or a duet swap singers could manifest as a slow within-take timbre morph rather than a hard swap). If you want to deliberately reproduce or avoid this: it's untested whether it's tied to Variety >0 (which rewrites the prompt and could destabilize identity over a long generation), a longer song length (this guide's other v6 notes above link degradation/consistency loss to the back half of longer tracks), or something else entirely. Worth a deliberate test — hold everything else constant and vary song length and Variety to see which one reproduces it — before relying on or ruling out the effect.

---

## Core Prompt Formula

```
[Genre] + [Mood] + [Tempo] + [Instruments] + [Vocals] + [Production Quality] + [Emotion]
```

**Optimal length:** 15-30 words (4-7 descriptors) as a floor for fast iteration — not a hard ceiling. See [Two Valid Prompt Styles](#two-valid-prompt-styles) below for when longer narrative prose outperforms this.
**Rule:** Most important descriptors first—Suno weights early words more heavily

**Example:**
```
Melodic techno, emotional and driving, 126 BPM, deep analog bass, ethereal pads, female vocal samples, progressive structure, studio-grade clean mix
```

---

## Two Valid Prompt Styles

The formula above is a **keyword-dense** style: pack the essentials into 15-30 words for fast iteration and easy A/B testing of single descriptors. It's not the only style that works.

**Narrative prose style** — sourced from official Suno docs (not community inference, so weight it at least as reliable as the keyword formula): the Style field can also be written as flowing descriptive paragraphs covering genre feel, instrumentation, and arrangement dynamics in full sentences, with Tempo and Mood broken out as their own labeled beats.

Official example (90s-inspired hip-hop track):
```
I want a 90s-inspired hip-hop track that feels upbeat, funky, and full of live energy. Think warm vinyl textures, syncopated drums, and jazzy chord progressions. The beat should swing — not rigid — with crisp snare hits, layered hi-hats, and a deep, rounded bassline that drives the groove.

Add electric piano chords, upright bass, muted trumpet accents, and percussive fills for that live jam feel. The mix should sound open and dynamic, like a live band recording with analog warmth.

Tempo: Around 102–106 BPM — quick enough to feel danceable but still relaxed and rhythmic. Slight tempo lift during the chorus for momentum.

Mood: Confident, playful, and intelligent. It should sound like a jam session among skilled MCs and musicians — rhythmic, soulful, and contagious in energy.
```

**When to use which:**
- **Keyword formula:** early exploration, fast iteration, testing individual descriptors
- **Narrative prose:** once the direction is set and you want to lock in arrangement/dynamics detail — especially useful for describing *how* elements interact ("swing — not rigid," "slight tempo lift during the chorus") rather than just listing them

Both fit inside the Style field's 1,000-char budget (see below). The "15-30 words" guidance is a starting point for iteration speed, not evidence that longer prompts underperform — see the revised [Prompt Complexity Balance](#prompt-complexity-balance) note for how this reconciles with the "Too Complex" warning elsewhere in this guide.

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

## Prompt Construction Rules

### Always Include
1. **Vocal type:** male/female/falsetto/choir/duet (or instrumental — Instrumental toggle + `vocals` in the Exclude field)
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
- ⚠️ Conflicting descriptors: e.g. "aggressive" + "gentle", or a genre stack with no clear lead — put the main genre first (stacking many genres is fine to test, see [Genre Fusion](#genre-fusion))
- ⚠️ Artist names: can pull generation strongly toward that artist's real catalog, overriding other descriptors in the same prompt — including in a reused instrument/style list not written with that artist in mind. Sometimes desirable, sometimes not — use deliberately, decide per-track. Also risks an outright generation block for copyright-flagged names (inconsistent, not a reliable list); intentionally misspelling the name is an unconfirmed workaround for that block, may stop working without notice
- ❌ Missing vocal specification
- ❌ Too complex: brand names, specific gear models
- ⚠️ "Live" as a descriptor (e.g. "live-sounding drums," "live band feel"): repeatedly observed across separate sessions to get interpreted literally as a concert/stadium performance — audience noise, arena ambience — rather than the intended "recorded with an organic, in-the-room feel." Consistent enough to treat as a known trap, not a one-off. Use "natural," "organic," "real drum kit," or the `[Live-Room Acoustics]` tag instead; if you need the word "live" itself, back it up with `crowd noise, audience, stadium reverb` in the Exclude field

---

## Creative Control Sliders

Sliders shape *how* the model interprets your text prompt, not *what* to generate. Mental model: the Style/Lyrics prompt defines the vocabulary; the sliders define the grammar — the same "jazz" prompt at low Weirdness produces a conventional jazz standard, at high Weirdness produces jazz that breaks its own conventions. Available in Custom Mode below the Lyrics field (V4.5+ through v5.5, **confirmed still present on v6**). v6 adds a third slider, Variety, alongside these two rather than replacing them — Variety rewrites your style text before generation (confirmed; this is also plausibly why the two takes diverge from each other), rather than changing how conventionally the model reads a fixed prompt. Keep it at 0 whenever the exact wording of your style field matters. See [Suno v6: Model Variants & New Capabilities](#suno-v6-model-variants--new-capabilities).

**Unconfirmed mechanism hypothesis:** Weirdness plausibly works like a sampling-probability control — low values favor the most probable next musical event at each step (conventional, predictable), high values let lower-probability events through more often (surprising, less coherent). Suno hasn't documented the actual mechanism; treat this as a hypothesis, not fact, same as other internals claims in this guide.

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

## Audio Upload Workflow

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

## Song Editor Workflow

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

### Lock-a-Take Workflow (Taming Non-Determinism)

Every full generation re-rolls the whole song, even with identical input and Variety 0 — so the more you pile into one prompt, the harder it is to tell whether a change helped or you just got a lucky roll. This project's working approach (Sept 2026):

1. **Get a good base take first.** Run a deliberately simple baseline prompt a few times, unchanged, until one take has the core right (intro, hook, drops — whatever the track lives on). Leave fragile, hard-to-prompt requests (tempo shifts, precise timing, specific motifs recurring later) *out* of the baseline.
2. **Keep that take and stop re-rolling the whole song.** Everything you like about it is now fixed. A new full generation throws it away and starts from scratch.
3. **Change one section at a time on the kept take.** Use v6 partial editing, or Remake/Extend in the Song Editor, on just the section you want to change. Each attempt is still random, but only inside that section; the rest stays as it was.

**Why:** it narrows the randomness from the whole track down to one section at a time, and it gives fragile ideas (e.g. a real BPM change on the final drop, via Remake/Extend with a different BPM in the prompt) a fair test without risking the parts that already work. This is the general form of the chorus-first [Lock-First Protocol](#lock-first-protocol-professional-workflow) above: lock whatever works, experiment on the rest.

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

## Stem Export Strategy

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

**Reportedly** the Exclude field works better than the Style field for exclusions — this is community-reported, not confirmed by Suno. Multiple sources claim negative instructions written into the Style field ("no drums", "no vocals") are unreliable, and that the **Exclude field under Advanced Options** is the more dependable place for unwanted instruments/elements. Worth A/B testing yourself before fully trusting it.

### Instrumental Tracks (No Vocals)
There is no dedicated `[no vocals]` meta tag, and "no vocals" in the Style field is unreliable. The dependable combination:
1. Toggle **Instrumental** on in Custom Mode
2. Add `[Instrumental]` in the Lyrics field (or `[Instrumental Break]` for a vocal-free section inside a song that otherwise has vocals)
3. Put `vocals` in the **Exclude field**

### Effective Syntax (Style field — positive framing still works well)
```
"Upbeat pop with drums and bass" + Exclude: guitars
"Trap beat with piano and synths" + Exclude: 808s
"Acoustic guitar focus, clear vocals" + Exclude: distortion
```

### Ineffective Syntax
```
❌ "Without singing unless background only"
❌ "No sounds that are bad"
❌ "Not like rock"
❌ Relying on Style-field "no X" phrasing for anything you actually need excluded
```

### Common Uses
- Pure instrumental: Instrumental toggle + `[Instrumental]` tag + Exclude field (see above) — do not rely on "no vocals" text alone
- Remove instrument: Exclude field, `"electric guitar"` (keeps other guitars)
- Clear mix: Exclude field, `"synth pads"` (reduces midrange clutter)
- Precision stacking: Exclude field, `"lead guitar solo"` (keeps rhythm guitars)

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

## Multilingual & Pronunciation

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

**UI features carried forward from v4.5/v5.5 (don't change tag vocabulary; unverified as still current on v6):**
- **Lyrics Editor structure labels** — the web Lyrics Editor lets you label sections Verse/Chorus/Outro from a UI control instead of typing bracket tags. Same underlying job as `[Verse]`/`[Chorus]`/`[Outro]`; use whichever surface you're actually composing in.
- **My Taste** — biases defaults only when a prompt is underspecified. Explicit Style-field descriptors and Lyrics-field meta tags still override it — it doesn't compete with anything you've deliberately written.
- **Style Augmentation (magic wand icon)** — generates personalized *style* text for you; it does not generate or modify structural meta tags.

v6 adds **partial editing** and **lyric refinement** (change one section/word/line via plain language without a full regeneration) and **multi-source mashups** — see [Suno v6: Model Variants & New Capabilities](#suno-v6-model-variants--new-capabilities). Whether these are new UI surfaces or extensions of the existing Song Editor tools (Rewrite/Remake/Extend) isn't confirmed by the source material — check the current UI.

### Song Structure Tags

```
[Intro] - Lead-in / scene setting
[Verse] / [Verse 1] / [Verse 2] - Lyrical development
[Pre-Chorus] - Build-up before chorus
[Chorus] / [Chorus x2] - Main hook / emotional core
[Post-Chorus] - After chorus section
[Bridge] - Contrast / pivot
[Breakdown] - Stripped-back section, reduced instrumentation, creates space
[Build] / [Build-Up] - Progressive intensity increase (common in EDM)
[Drop] - Beat-driven instrumental focus, max instrumentation, follows a Build
[Hook] - Catchy part emphasis
[Interlude] - Instrumental break connecting sections, palette cleanser
[Break] / [Instrumental Break] - Break in the song
[Solo Section] - Featured instrument spotlight
[Outro] - Closure or fade-out
[Fade Out] / [Fade In] - Volume transitions
[End] - Hard stop; signals the song should end (prevents trailing audio)
```

**Note:** Tags are case-insensitive (`[VERSE]`, `[Verse]`, `[verse]` are equivalent).

### Vocal Tags

**Avoiding the generic "Suno voice":** a bare "male vocal" or "female vocal" tag with one adjective tends to produce Suno's default timbre, recognizable across many different songs. Stack 2-3 specific descriptors (tone + technique/texture + style) to get something distinctive:
```
Raspy male vocals with subtle vibrato, lo-fi warmth
Ethereal female vocals, breathy and reverb-heavy, choir harmonies
Deep baritone, smooth jazz delivery, minimal processing
```
For per-section control (e.g. a chorus that needs to sound markedly different from the verse), use [Parameterized Metatags](#parameterized-metatags-colon-syntax) instead of only setting this once in the Style field.

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
[Vocal Fry] - Low, gravelly vibration at the start of a phrase; builds intimacy
[Crying Tone] / [Whimper] - Subtle raspy break conveying vulnerability or pain, without full grit/distortion
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
[Scream] - Screamed/shouted delivery (metal, punk)
[Ad-lib] - Improvised vocal phrases
[Vocal Run] - Quick succession of notes, often improvised
[Crooning] - Soft, intimate singing style
[Conversational] - Rhythmic, almost-spoken delivery; crisp diction grounds storytelling before the melody expands
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
- Echo ad-lib: repeat the last word/phrase of a line in parentheses immediately after — `I'm caught up in a fever dream (fever dream)`. Reinforces the hook with a call-and-response feel without needing a second vocalist; works well stacked with `[Layered]`/`[Backup Vocals]` tags on the section.

### Vocal Technique Vocabulary (Pedagogy-Level)

These are vocal-*pedagogy* terms — more technical than the tone/texture/style lists above — describing *how* a vocal is physically produced rather than just its overall vibe. Most useful when a section needs to sound distinctly different from another in a controllable way (an intimate, dry verse vs. a strained, urgent chorus belt), stacked 2-4 at a time inside a section tag rather than dropped in alone.

**Placement & Resonance:**
```
[Pharyngeal Twang] / Bright pharyngeal twang - Bright, brassy, cutting quality from pharyngeal constriction; reads as loud/present without needing volume
[Forward Nasal Placement] - Resonance pushed into the mask/nasal cavity; brighter, more forward-sitting tone
[Chest-Dominant] - Weight and resonance centered in chest voice; grounded, powerful low-effort loudness
[Mixed-Voice] / Tight mixed-voice belt - Blend of chest and head voice; keeps a belt controlled at the top of the range instead of flipping to pure head voice
```

**Delivery & Texture:**
```
[Breathy Lower-Mid Register] - Airy, breath-mixed tone sitting in the lower-middle of the vocal range
[Vocal Fry Onset] - Creaky, low-vibration fry specifically at the start of a phrase, not sustained through it; builds intimacy without committing to full fry throughout
[Rapid Speech-Level Delivery] - Fast, conversational cadence locked rhythmically to a named instrument, e.g. "locking into the guitar"
[Dry-Forward Mix] / [Close-Mic Intimate Vocal] - Minimal reverb/space, sitting forward and present; contrasts deliberately against a reverb-drenched instrumental section (e.g. intro piano) to make the vocal entrance feel close and grounded
[Chest-Dominant Crying Edge] - An emotional, break-like rasp riding on top of a chest-dominant belt; conveys urgency/desperation on a peak note without going full scream
[Strained / Pushed High] - Intentional vocal strain at the top of the range, read as urgency rather than a mixing flaw
```

**Half-time/full-time layering:** `Tempo: 83 BPM half-time pulse, four-on-the-floor underneath` describes a perceived half-time feel (the vocal/melody phrasing feels like half the BPM) layered over an actually-doubled rhythmic pulse underneath. State both explicitly — a single BPM number alone won't communicate the layered feel.

**Evocative/personified production language:** describing an effect by what it sounds like doing, not just its technical name — e.g. `sidechain-pumping pads gasping for air` (audible sidechain compression), `cavernous, ungrounded` (heavy reverb/delay on a sparse intro), `massive wide stereo`, `pitched vocal chops panned hard left/right`. Pair with the literal effect name (`[Sidechain Compression]`, `[Wide Stereo]`) rather than relying on the metaphor alone.

See [Repeated vs. Arrangement-Aware Section Descriptor Blocks](#repeated-vs-arrangement-aware-section-descriptor-blocks) below for how to apply these per-section, and [Labeled Hybrid Style Field Format](#labeled-hybrid-style-field-format) for folding them into the Style field.

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
[Silence] - Brief pause in the audio
```

**Classical Dynamics Markings** (from Suno's own glossary):
```
[Forte] - Loud
[Piano] - Soft (dynamics sense, not the instrument — context disambiguates)
[Fortissimo] - Very loud
[Pianissimo] - Very soft
[Accent] - Emphasis on a particular note or beat
[Tremolo] - Rapid repetition of a note or alternation between notes
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

**Solo & Passage Tags:**
```
[Guitar Solo] - Guitar-focused instrumental passage
[Piano Solo] - Piano-focused passage
[Drum Solo] - Percussion-focused passage
[Bass Solo] - Bass-focused passage
[Saxophone Solo] - Sax-focused passage
[Synth Solo] - Synthesizer lead passage
[Strings Rise] - String section swell
[Percussion Break] - Rhythm-focused breakdown
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

**Classical Tempo Terms** (from Suno's own glossary — an alternative vocabulary to plain BPM/descriptor tags):
```
[Adagio] - Slow, "at ease" (66-76 BPM)
[Andante] - Moderate walking pace (76-108 BPM)
[Allegro] - Fast, lively (120-168 BPM)
[Presto] - Very fast (168-200 BPM)
[Rubato] - Flexible tempo; performer speeds up/slows down expressively
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
⚠️ **Reportedly unreliable at generation time.** Community reports suggest time signature is primarily an editing-surface control (Studio grid + metronome after generation), not a generation-time directive — but nobody outside Suno has confirmed the actual mechanism. If an odd-meter track matters, verify with your own test generations rather than assuming the tag does nothing.

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
[Key Change] - Harmonic modulation to a new key
```

**Advanced Theory Terms** (from Suno's own glossary — useful for orchestral/classical/jazz prompting):
```
[Cadence] - Harmonic/melodic formula creating a sense of resolution or pause
[Ostinato] - A repeated musical pattern or phrase
[Pedal Point] - A sustained/repeated note while harmonies change above it
[Suspension] - Holding a note from one chord into the next, creating tension
[Augmentation] - Lengthening the rhythmic values of a melody
[Diminution] - Shortening the rhythmic values of a melody
[Anacrusis] - Pickup notes occurring before the first full measure
[Coda] - A concluding section that brings a piece to an end
[Arpeggio] - Playing chord notes in sequence rather than simultaneously
[Interval] / [Octave] - The distance between two pitches / the interval of double frequency
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

### Learning From Suno's Own Output (Audio Upload → Auto-Caption)

Uploading a reference track (game soundtrack, old demo, found sound, or one of your own past generations) lets Suno auto-generate its own style + lyric caption from the audio. Read back what it calls the elements — its own vocabulary for a sound is more reliable than guessing descriptors from outside.

Two format notes for writing prompts around this:
- For dense production/instrumental material, the style field can be full technical prose (decay, resonance, filter movement), not just a short keyword list — denser than the 15-30 word rule elsewhere in this guide, and the model can parse it back.
- Instrumental arrangement doesn't need named sections. It can be a sequence of short, standalone event tags under generic labels instead of `[Verse]`/`[Chorus]`, e.g. `[Section A][distorted resonant kick drum, 4/4 pulse][metallic percussion loop enters]` — describing what happens moment-to-moment rather than what kind of section it is. Useful for instrumental intros/breaks/outros inside otherwise vocal tracks.

### Round-Trip Debugging (Diagnosing Style/Lyric Prompt Drift)

To check whether a prompt actually landed: **generate** → **download** the audio → **re-upload** it back into Suno → **diff** the fresh auto-caption against your original prompt, line by line.

Reading the diff:
- Descriptor in your prompt, missing from the re-caption → likely didn't survive generation. Try moving it earlier in the prompt (early words weight more heavily), making it more specific, raising Style Influence, or dropping it if it's consistently lost.
- Descriptor in the re-caption you never asked for → shows what Suno defaulted to filling the gap with.
- Generic vocal wording in the re-caption ("male vocal," no texture) → the voice rendered as default/generic; not just a matter of your perception.
- Numbers/keys in the re-caption (BPM, key) are stated as flat fact even when your original prompt never specified them — don't assume a number in a re-caption was actually in your input; check line by line.

**Non-determinism:** one re-caption only diagnoses that one take, not the prompt in general. Generate the same unchanged prompt 3 times before touching anything — 3 takes tells "consistently missing" apart from "one unlucky roll." Budget 5-10 generations total (3 unchanged + tweaks) before concluding a prompt does or doesn't work.

**Reused style/instrument lists:** if a base list carrying artist-name vocal references gets reused across tracks for sonic-family cohesion, treat those artist names as an active competing force on the outcome, not neutral shared DNA — they can pull toward that artist's real sound regardless of the rest of the list. Decide per track whether to keep that pull or swap in a fresh musical descriptor.

### Parameterized Metatags (Colon Syntax)

The most reliable way to give a single section unique instrumentation or vocal character without changing the global Style field: add descriptors after a colon inside the bracket tag.

```
[Verse: whispered vocals, acoustic guitar only]
Walking through the morning mist
The world still sleeping, still

[Chorus: full band, powerful vocals]
But I'm awake, I'm alive
And every sound is a sign
```

**Why this matters for vocal distinctiveness:** stacking a generic "male vocal" / "female vocal" tag with only one adjective in the Style field tends to produce Suno's default vocal timbre — the same voice shows up across many songs. Parameterized section tags let you stack 2-3 unusual, specific descriptors per section instead:

```
[Verse: gritty, slightly nasal male vocal, worn and weathered grain]
[Chorus: cracked upper register on the belt, raspy and imperfect]
```

This combines with — doesn't replace — the dash-style descriptive headers already used in this guide's lyric examples (`[Verse 1 - Introspective, Gentle]`); colon syntax is the more precisely-controlled form when a section's vocal character needs to diverge sharply from the rest of the song.

### Repeated vs. Arrangement-Aware Section Descriptor Blocks

Beyond single-word colon tags (`[Chorus: full band, powerful vocals]`), a section header can carry a full comma-separated technical block combining instrumentation and [vocal-technique terms](#vocal-technique-vocabulary-pedagogy-level) together. There are two ways to reuse that block across repeated sections of the same type, and which one to pick depends on what you want the repeat to feel like:

**Identical repeat (for hook-level consistency):** every occurrence of a section type carries the exact same block, word for word — reinforces that Verse 1 and Verse 2 (or every Chorus) should sound like the same idea recurring, not evolve.
```
[Verse 1: breathy lower-mid register, vocal fry onset on opening phrases, dry-forward vocal, rapid speech-level delivery locking into guitar, staccato syncopated guitar, sparse low end]
...
[Verse 2: breathy lower-mid register, vocal fry onset on opening phrases, dry-forward vocal, rapid speech-level delivery locking into guitar, staccato syncopated guitar, sparse low end]
...
```

**Arrangement-aware repeat (for a felt narrative progression):** the block describes what changed since the last occurrence — what dropped out, what returned, what's different this time — rather than restating the same words. Use this when the song should feel like it's moving through stages, not looping.
```
[Verse 1: dry, close-mic intimate vocal, four-on-the-floor kick enters, steady heartbeat pulse]
...
[Verse 2: synths drop out, close intimate vocal returns, driving bass and kick keep momentum]
...
```

Both are valid; pick per song based on whether the repeat should read as "the same moment again" or "the same section type, later in the story."

### Labeled Hybrid Style Field Format

A third valid Style field format, alongside the [keyword formula](#core-prompt-formula) and [narrative prose](#two-valid-prompt-styles): dense comma-separated technical description of verse/chorus contrast, capped off with explicit labeled clauses — `Tempo:`, `Key:`, `Production:`, `Mood:` — stated as their own beats at the end, the way narrative prose breaks out Tempo/Mood. Combines keyword density with narrative prose's labeled precision.

```
[Genre + fusion description], [Verse character: instrumentation + vocal technique], [Chorus character: instrumentation + vocal technique], Tempo: [BPM + feel], Key: [key], [chord progression], Production: [quality descriptors], Mood: [emotional core]
```

Example (reggae-pop/radio-pop fusion):
```
Mid-tempo acoustic-driven pop anthem, radio pop with singer-songwriter texture, staccato syncopated acoustic guitar with reggae-pop lean for danceable momentum, Verses sparse and tight, low end stripped, lyric tenor vocal with bright pharyngeal twang and forward nasal placement, breathy lower-mid register with vocal fry onset on phrase openings, dry forward mix, rapid speech-level delivery locking into guitar, Chorus thickens with heavy kick, deep sub-bass synth, octave-doubled unison vocal stacks, tight mixed-voice belt pushed high and strained, bright nasal twang, urgent chest-dominant crying edge on the high note, crisp and cleanly separated not muddy, Tempo: 83 BPM half-time pulse, four-on-the-floor underneath, Key: B♭ minor, vi-V-IV-I progression, Production: clean mix, studio-grade mastering, balanced frequency response, no muddy bass, no harsh highs, Mood: urgent, melancholic beneath danceable energy, unrequited longing and frustration
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

### Genre Fusion

**No hard limit on how many genres you stack.** The old "two genres max, three or more is chaos" rule is unverified community lore from the v4/v5 era, not something Suno has stated or anyone has measured. Any combination is worth testing — Styles.md is the pool to draw from, single genres and fusions alike.

**Working heuristics (hypotheses, not rules):**
- **Order still reportedly matters:** Suno appears to weight early words more, so lead with the genre you want as the main identity and list supporting influences after it.
- **One dominant identity helps when a stack comes out muddled** — a v6 community write-up (Reddit, Sept 2026, one person's testing in metalcore/post-hardcore/electronic-rock) reports good results with **one main musical identity + two or three supporting influences**, e.g. "modern metalcore, California skater pop-punk, emo-pop hooks, darkwave synth textures."
- **If a fusion sounds like mush, shorten the stack or reorder it** before concluding the combination can't work — and per the [iteration principle](#key-principles-for-ai-agents), give it a few generations first, since one take doesn't diagnose a prompt.

**Two-genre fusions that are commonly reported to land easily** (starting points, not a ceiling): R&B Trap, Jazz House, Gospel Soul, Reggae Afrobeat, Lo-fi Hip Hop, Synthwave Pop.

### Genre Confidence Tiers

Nobody outside Suno actually knows the training data composition or model internals — the tiers below are inferred by outside observers from output consistency, not published by Suno. Treat as "commonly reported difficulty," not measured fact. Genre accuracy anecdotally tracks toward Global North genres (guitar/piano/drums-heavy) over regional/non-Western ones. Pick descriptors with this in mind, especially for anything pulled from Styles.md's World & Regional section — and expect this table itself to need correction as you generate.

**⚠️ v6 caveat — this table predates v6 and may no longer hold:** this table was built from v4.5/v5.5-era testing. Per Suno's own announcement, v6 trained on a different, licensed dataset (label partners, not the older broad dataset) rather than continuing the old one — see [why old prompts reportedly don't transfer](#suno-v6-model-variants--new-capabilities) above. Community reports since the v6 launch specifically call out heavily distorted/extreme genres (metal, especially guitar distortion; drum & bass and other bass-heavy electronic) as *worse* on v6 than on v5.5, while mainstream pop/rock/folk/country are reported as steady-to-improved. Re-verify any genre here against fresh v6 generations rather than trusting this table's tier placement as still current — it's now two different models' worth of behavior layered into one list.

**High-confidence (reliable):** pop, synth-pop, indie pop, dream pop, rock, indie rock, alt-rock, punk rock, hip-hop, trap, boom bap, lo-fi hip-hop, EDM, house, techno, trance, drum and bass, R&B, neo-soul, country, folk, indie folk, Americana, jazz, swing, bebop

**Medium-confidence (usable, expect to iterate):** metal (extreme vocals — growls/screams — are hit-or-miss), classical/orchestral (complex counterpoint is weak), reggaeton, salsa, bossa nova, cumbia, bachata, afrobeats, afropop, K-pop, J-pop, city pop

**Low-confidence (requires heavy iteration, approximate results):** avant-garde/experimental/noise, non-Western traditional forms (gamelan, raga, Tuvan throat singing, and most of Styles.md's African/Middle Eastern/Asian regional entries), pure sound design/ambient drone (Suno optimizes for song structure, not soundscape)

**How to apply:** for a low-confidence genre fusion, budget for more generations and treat the result as "inspired by" rather than an authentic recreation — don't chase precision the training data can't support.

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

For pure instrumentals, be explicit — Instrumental toggle on, `vocals` in the Exclude field (see [Instrumental Tracks](#instrumental-tracks-no-vocals)), and describe the arrangement per section:

```
Style: Melodic techno, 126 BPM, deep analog bass, ethereal pads, progressive structure, studio-grade clean mix, instrumental
Exclude: vocals

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

**Optimal (keyword style):** "Upbeat indie pop, 110 BPM, jangly guitars, warm bass, female vocals, clean bright mix"
- Result: Clear direction, good consistency

**Too Complex:** "Upbeat indie pop with jangly Rickenbacker 12-string guitars, Fender Precision bass with flatwound strings, Ludwig drum kit with Zildjian cymbals, female soprano vocals with Neumann U87 microphone, SSL console mixing..."
- Result: Confusion, missed elements, artifacts

**Note the difference:** the "Too Complex" failure here isn't length — it's stacking specific gear/brand names (see [Prompt Construction Rules → Avoid](#always-include): "brand names, specific gear models" is its own listed pitfall). Long narrative prose describing sound, feel, and arrangement in plain language is a different thing and works well — see [Two Valid Prompt Styles](#two-valid-prompt-styles).

**Rule:** 15-30 words / 4-7 key descriptors for keyword-style prompts; narrative prose can run longer as long as it stays in plain descriptive language rather than named gear.

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
Tech House, energetic, 128 BPM, drum machine, electric piano, punchy kicks, synth pads, 4/4 time, club-ready mix, instrumental
Exclude: vocals
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
Synthwave, nostalgic, 120 BPM, analog synths, gated drums, arpeggiators, retro bass, cinematic pads, 80s production, instrumental
Exclude: vocals
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
Sliders apply to the whole generation, not per section. For a full-song generation:
- **Variety: 0** — otherwise Suno rewrites the style text you just built
- Weirdness and Style Influence per the [v6 starting recipe](#suno-v6-model-variants--new-capabilities) (obedience: Weirdness under 50, Style Influence 80-95), then adjust from what you hear

Per-section values only come into play when you Remake a single section in the Song Editor (see [Lock-First Protocol](#lock-first-protocol-professional-workflow)):
- Chorus/Hook: Weirdness ↓ (35-45), Style ↑ (70-85)
- Verse: Weirdness mid (40-55), Style mid (55-70)
- Bridge: Weirdness ↑ (55-70), Style mid (45-60)

### Step 5: Add Exclusions (if needed)
Use the **Exclude field**, not "no X" in the style field (see [Negative Prompting](#negative-prompting-exclusions)):
- Instrumental? → Instrumental toggle + `[Instrumental]` tag + Exclude: `vocals`
- Avoid specific instrument? → Exclude: `[instrument]`
- Clear muddy mix? → Exclude: `synth pads` or `rhythm guitar`

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
| Output too chaotic | Conflicting or unanchored descriptors | Put primary genre first; lower Weirdness to 35-45; trim or reorder the stack | Test a shorter version side by side |
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
- [ ] Vocal type specified (or Instrumental toggle + Exclude: vocals)
- [ ] 1-2 hero instruments named
- [ ] Mood + genre clear
- [ ] Tempo set (BPM or descriptor)
- [ ] Production quality descriptor included
- [ ] 15-30 words total (4-7 descriptors) — or narrative prose if using that style (see [Two Valid Prompt Styles](#two-valid-prompt-styles))
- [ ] Most important elements first
- [ ] Lyrics: 4-6 lines per section
- [ ] Lyrics: structure tags present
- [ ] Lyrics: checked for homographs
- [ ] Variety at 0 (unless deliberately letting Suno rewrite the style)
- [ ] Unwanted elements in the Exclude field, not as "no X" in the style field

### Pre-Export QA
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

## Title Suggestions (Always Include)

Every prompt/lyric response must end with a list of 5–8 suggested song titles that match the mood, genre, and narrative of the track. Mark one as the recommended pick with a short reason.

**Format:**
```
**Suggested Titles:**
- Title One
- Title Two
- Title Three
- Title Four
- Title Five

**Pick:** *Title Two* — brief reason.
```

**Rules:**
- Titles should be evocative, not generic (avoid "The Song", "Untitled")
- Match register: a trap song and a cinematic score need different title styles
- Prefer specific, image-rich phrasing over abstract words
- 1–5 words each works best

---

## Key Principles for AI Agents

1. **Always ask clarifying questions** if genre, mood, or vocal type unclear
2. **Start with the formula:** Genre + Mood + Tempo + Instruments + Vocals + Production Quality
3. **Keyword prompts: 15-30 words** (4-7 descriptors) for fast iteration; narrative prose can run longer — see [Two Valid Prompt Styles](#two-valid-prompt-styles)
4. **Most important first:** Suno weights early words more
5. **Include production quality:** Always add 1-2 quality descriptors
6. **Lyrics: 4-6 lines per section** maximum
7. **Check for homographs:** read, live, lead, bass, tear, wind
8. **Add performance tags** for dynamic delivery
9. **Variety 0 by default;** per-section slider values (Chorus conservative, Bridge experimental) apply only when Remaking a single section
10. **Use the Exclude field** for unwanted elements, not "no X" in the style field
11. **Lock chorus first** in Song Editor workflow
12. **For uploads:** State BPM/key explicitly; set Audio Influence appropriately
13. **Multilingual:** One language per section; add "no English" if needed
14. **Export strategy:** Fix arrangement in Suno, tone/EQ in DAW
15. **Iterate:** Suno is non-deterministic — the same prompt produces different results each time. Real-world workflow on this project: generate the *same unchanged prompt* 3 times first to sample the variance before touching anything, then start making small tweaks if none of those 3 land — landing a take that actually works often takes 5-10 generations total between the unchanged batch and the tweaked follow-ups. Don't conclude a prompt "doesn't work" from a single generation, or even from one changed variant — the prompt is only one input; the roll is the other. Once a take lands, stop re-rolling the whole song and edit it section by section instead — see [Lock-a-Take Workflow](#lock-a-take-workflow-taming-non-determinism).

---

## Final Notes

- **Treat Suno like a producer:** Give clear direction, not vague inspiration
- **Simple structure > complex chaos:** Clear sections beat overloaded prompts
- **Strong keywords > generic descriptions:** "Spanish nylon guitar" beats "guitar"
- **v6 tools:** Use Song Editor for section control, Audio Uploads for collaboration, Stems for DAW finishing
- **Lock-first workflow:** Perfect the chorus, then build around it
- **Production quality matters:** Always include quality descriptors for consistency
- **Iterate fast:** Test variations, use sliders strategically
- **Generate multiple takes:** non-deterministic model — expect 5-10 generations per track to land the one that actually works, not 2-3; pick best, refine in Song Editor

This guide prioritizes actionable prompt construction and v6 production workflows. Focus on helping users craft precise, effective prompts, leverage v6 features, and achieve professional results.
