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


### 🕵️ What is obfuscation?

- Transforms source into a harder-to-read form while preserving function.
- Often automated by obfuscator tools.
- Examples: replacing identifiers with indices, building dictionaries of tokens and reconstructing at runtime, encoding strings.

---

### Common use cases

- Protect intellectual property / prevent copy-paste.
- Add a thin layer of security (note: client-side auth/encryption is insecure).
- Malicious actors hide payloads to bypass IDS/IPS and human review.

---

### Common obfuscation techniques

1. Minification
    - Removes whitespace/newlines and shortens names. Usually .min.js.
    - Preserves logic; mainly reduces readability and file size.
2. Packing
    - Encodes tokens into arrays/dictionaries and uses a runtime unpacker like function(p,a,c,k,e,d) to rebuild code.
    - Recognizable by the (p,a,c,k,e,d) pattern.
3. String/array encoding & runtime decoding
    - Stores important strings encoded (Base64, hex, custom) and decodes them at runtime.
4. Extreme encoders
    - JSFuck, JJEncode, AAEncode — produce valid JS using only limited characters; very slow and hard to read.

---








