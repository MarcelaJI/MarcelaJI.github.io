---
layout: default
title: HTB CBBH notes
---

# JavaScript Obfuscation & Deobfuscation — concise guide

TL;DR: Obfuscation rewrites code so humans (and often detection systems) can’t read it while preserving behavior. Common JavaScript techniques include minification, packing (token dictionaries + runtime unpackers), string/array encodings and extreme forms like JSFuck/JJ/AA encode. Deobfuscation uses beautifiers, unpackers and manual reverse-engineering (plus knowledge of encodings such as Base64/hex/ROT13).

