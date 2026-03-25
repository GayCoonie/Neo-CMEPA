# Neo-CMEPA 2.1

**Neo-CMEPA** is a deliberately nonstandard phonetic control orthography for converting IPA into a form that generative singing systems such as **Suno** are more likely to pronounce consistently than raw IPA.

It began as a reboot of older CMEPA versions after repeated practical failures with direct IPA input. The guiding principle is **not** elegance, linguistic purity, or internal neatness. The guiding principle is:

> **If a symbol produces better sung output, it wins.**

As a result, Neo-CMEPA is:

- **phonologically informed**
- **historically aware**
- **empirically tuned**
- and often **orthographically cursed**

This repository contains a converter from IPA to **Neo-CMEPA 2.1**.

---

## Core Philosophy

Neo-CMEPA is **not IPA** and is **not intended to replace IPA**.

It is a **control alphabet** designed for a specific hostile environment:

- IPA is often ignored, misread, or partially treated as gibberish by generative singing models.
- Ordinary spelling invites unwanted English-default pronunciation.
- Beautifully systematic orthographies often fail in practice.
- Mixed-script, selectively unnatural orthography can outperform both IPA and normal spelling.

So Neo-CMEPA prioritizes:

1. **Pronunciation stability in TTS / music models**
2. **Reliable handling of Middle English-oriented material**
3. **Explicit syllable control**
4. **Practical approximation for messy real-world IPA**
5. **Empirical success over theoretical elegance**

---

## Version

This README describes **Neo-CMEPA 2.1**.

Notable traits of 2.1 include:

- contextual handling of **/s/**
- **/w/ -> `w`**
- **/ʍ/ -> `hw`**
- **/r/ -> `ρ`**
- **/θ/ -> `θ`**
- explicit historical handling for initial **kn -> k'n** and **gn -> g'n**

---

# Alphabet

## Consonants

### Core consonants

| IPA | Neo-CMEPA |
|---|---|
| /p/ | `p` |
| /b/ | `b` |
| /t/ | `t` |
| /d/ | `d` |
| /k/ | `k` |
| /g/ | `g` |
| /f/ | `f` |
| /v/ | `v` |
| /m/ | `m` |
| /n/ | `n` |
| /l/ | `l` |
| /r/ | `ρ` |
| /w/ | `w` |
| /j/ | `y` |
| /z/ | `z` |
| /h/ | `h` |

### Special consonants

| IPA | Neo-CMEPA | Notes |
|---|---|---|
| /θ/ | `θ` | chosen for output behavior, not aesthetics |
| /ð/ | `δ` | stable voiced dental |
| /ʃ/ | `ш` | stable `sh` |
| /tʃ/ | `ч` | also used for tied/untied affricate variants |
| /dʒ/ | `џ` | explicit separate representation |
| /ŋ/ | `ң` | velar nasal |
| /x/, /ç/ | `kh` | intentionally merged for stability |
| /ʍ/ | `hw` | explicit voiceless `w` |

---

## The `/s/` Rule in 2.1

Neo-CMEPA 2.1 uses **contextual allography** for **/s/**.

This is intentional.

### Rule

- **syllable-initial /s/ before a vowel** -> `σ`
- **syllable-initial /s/ before a consonant** -> `с`
- **all other /s/** -> `ß`

### Examples

| IPA | Output | Reason |
|---|---|---|
| /sa/ | `σа` | syllable-initial before vowel |
| /sta/ | `ста` | syllable-initial before consonant |
| /musə/ | `mу'ßă` | non-initial /s/ |
| /hɔrs/ | `hoρß` | final /s/ |

This rule is driven by model behavior, not by any claim that these are linguistically “correct” spellings of /s/.

---

## Vowels

### Short vowels

| IPA | Neo-CMEPA |
|---|---|
| /a/ | `а` |
| /ɛ/ | `э` |
| /ɪ/ | `і` |
| /ɔ/ | `o` |
| /ʊ/ | `у` |
| /ə/ | `ă` |

### Long open vowels

| IPA | Neo-CMEPA |
|---|---|
| /aː/ | `α` |
| /ɛː/ | `αι` |
| /ɔː/ | `ò` |

### Long close / tense vowels

| IPA | Neo-CMEPA |
|---|---|
| /eː/ | `é` |
| /iː/ | `í` |
| /oː/ | `ó` |
| /uː/ | `ú` |

---

## Diphthongs

Diphthongs are written compositionally according to the mapped vowel symbols and glides.

Typical examples:

| IPA | Neo-CMEPA |
|---|---|
| /aɪ/ | `аі` |
| /aʊ/ | `ау` |
| /ɔɪ/ | `oі` |

Nonsyllabic vowel diacritics may be approximated to `y` or `w` depending on frontness/backness.

---

# Syllable Marking

## Universal syllable boundary rule

Neo-CMEPA places an apostrophe:

> **between every syllable**

This applies whether the IPA already marks syllables or not.

### Examples

| IPA | Neo-CMEPA |
|---|---|
| /faː.dər/ | `fα'dăρ` |
| /rɔː.tə/ | `ρò'tă` |
| /dʒeː.nə.ra.li/ | `џé'nă'ρа'li` |

The apostrophe is used for **syllable structure control**, not stress marking.

---

# Historical Initial Consonant Handling

Neo-CMEPA 2.1 explicitly forces apostrophes in some initial clusters that are notorious in modern English for losing the first consonant.

## Rule

- `kn` -> `k'n`
- `gn` -> `g'n`

This is done even if a naive syllabifier might otherwise keep them together.

### Examples

| IPA | Neo-CMEPA |
|---|---|
| /knixt/ | `k'níkht` or equivalent mapped output |
| /gnat/ | `g'nаt` |

This rule exists to preserve historically intended consonants that modern-English-biased models often suppress.

---

# IPA Intake Rules

When the input is already in IPA, the converter treats it as the source of truth and converts it directly.

## The converter will:

- strip IPA framing such as `/.../` and `[...]`
- ignore primary and secondary stress marks
- preserve whitespace, line breaks, and stanza breaks
- preserve punctuation
- respect explicit IPA syllable marks where present
- infer syllable boundaries when absent
- convert tied and untied affricates equivalently
- approximate unsupported IPA symbols to the nearest useful Neo-CMEPA value where possible
- report warnings for approximations and unhandled symbols

---

# Affricates

These are explicitly recognized in both tied and untied forms.

| IPA input | Neo-CMEPA |
|---|---|
| `tʃ`, `t͡ʃ`, `t͜ʃ`, `ʧ` | `ч` |
| `dʒ`, `d͡ʒ`, `d͜ʒ`, `ʤ` | `џ` |
| `t͡s`, `t͜s`, `ʦ` | `ts` |
| `d͡z`, `d͜z`, `ʣ` | `dz` |

---

# Approximation Policy

Neo-CMEPA 2.1 is intentionally forgiving.

If the IPA contains symbols that are not directly represented in the core Neo-CMEPA inventory, the converter approximates them to the nearest supported value whenever possible.

## Examples of approximations

| IPA | Approximation |
|---|---|
| /ɡ/ | normalized to `g` |
| /ɹ ɾ ɽ ʀ ʁ/ | approximated to `ρ` |
| /ɲ ɳ/ | approximated to `n` |
| /ɬ/ | approximated to `/s/` territory |
| /ɮ/ | approximated to `z` |
| /ɫ ʎ ʟ ɭ/ | approximated to `l` |
| /β/ | approximated to `v` |
| /ɸ/ | approximated to `f` |
| /ʋ/ | approximated to `w` |
| /ɦ/ | approximated to `h` |
| /ʔ/ | approximated to `h` |
| /χ ħ ʜ ɧ ɣ/ | approximated toward `kh` |
| syllabic consonants | rendered as `ă + consonant` |
| nonsyllabic front vowels | approximated to `y` |
| nonsyllabic back vowels | approximated to `w` |

If a symbol still cannot be handled, it is marked explicitly rather than silently deleted.

---

# Why Neo-CMEPA Looks Like This

Because raw IPA often fails in the target environment.

Neo-CMEPA is the product of repeated practical discoveries such as:

- the “correct” symbol often performs worse than the ugly one
- certain scripts are overinterpreted by the model
- some symbols become whole syllables instead of consonants
- some letters carry unwanted language priors
- positional variants can outperform one-symbol-fits-all mapping

So Neo-CMEPA should be understood as:

> **a hostile-environment phonetic control orthography**

not as a normal phonetic alphabet.

---

# Design Notes

## Why mixed scripts?

Because mixed scripts often reduce English-default guessing and force the model into more controlled segmental behavior.

## Why not just use IPA?

Because in practice, models such as Suno often read IPA inconsistently or partially ignore it.

## Why not make the system fully elegant and systematic?

Because elegance is not the main goal.

The main goal is:

- **stable sung pronunciation**
- **predictable phonetic steering**
- **usable output on real model behavior**

If a bizarre grapheme performs better, it is preferred.

---

# Example

## Input IPA

```text
/swɛt sɔŋ knixt gnat ʍeːl wɔːrd rɛːd rɔːtə faːdər θaŋk/
```

## Example Neo-CMEPA-style output

```text
сwэт сoң k'níkht g'nаt hwé'l ρwòrd ραιd ρò'tă fα'dăρ θаңk
```

Exact output may vary depending on approximation decisions and syllabification behavior in the current script version.

---

# Usage

Open the notebook in Colab, paste IPA into the input cell, and run it.

The notebook will:

1. convert the input into Neo-CMEPA
2. print the result
3. save the result to `neo_cmepa_output.txt`
4. print warnings for approximations or unsupported IPA

---

# Scope

Neo-CMEPA 2.1 is primarily tuned for:

- Middle English-oriented pronunciation work
- lyric preparation for TTS / singing models
- IPA cleanup into a more behaviorally reliable orthography

It may also be useful more broadly, but it is **not** intended as a universal phonetic standard.

---

# Final Principle

Neo-CMEPA is built on one practical belief:

> **A symbol is good if the model sings it correctly.**

Everything else is secondary.
