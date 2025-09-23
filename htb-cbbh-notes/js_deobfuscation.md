---
layout: default
title: HTB CBBH notes
---

# JavaScript Obfuscation & Deobfuscation — concise guide 🔎

TL;DR: Obfuscation rewrites code so humans (and often detection systems) can’t read it while preserving behavior. Common JavaScript techniques include minification, packing (token dictionaries + runtime unpackers), string/array encodings and extreme forms like JSFuck/JJ/AA encode. Deobfuscation uses beautifiers, unpackers and manual reverse-engineering (plus knowledge of encodings such as Base64/hex/ROT13).

---

## Intro 

Obfuscation makes code hard to read but still executable. It’s widely used in benign contexts (protecting IP, reducing reuse) and maliciously (evading detection). Understanding obfuscation is a prerequisite for deobfuscation.

---


### What is obfuscation?

- Transforms source into a harder-to-read form while preserving function.
- Often automated by obfuscator tools.
- Examples: replacing identifiers with indices, building dictionaries of tokens and reconstructing at runtime, encoding strings.




