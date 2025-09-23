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

### Spot & decode common encodings

- **Base64** — alphanumerics plus +/ and padding =.
    - Encode: ```echo text | base64```
    - Decode: ``` echo text | base64 -d```
- **Hex** — hex digits 0-9a-f.
    - Encode: ```echo text | xxd -p```
    - Decode: ```echo HEX | xxd -p -r```
- **Caesar / ROT13** — simple letter shifts; decode with tr.
    - ```echo text | tr 'A-Za-z' 'N-ZA-Mn-za-m'```

Tip: automated tools (e.g., cipher identifier pages) can help detect encoding types.

---

### Deobfuscation workflow (practical)


1. Beautify / Pretty-print

    - Use browser DevTools (Pretty Print / {}), Prettier, Beautifier to restore newlines and formatting.

2. Automated unpackers

    - Run tools like UnPacker / JSNice / other online unpackers to remove common packer layers.

3. Inspect runtime output instead of executing

    - Replace eval with console.log or otherwise print the unpacked return value to examine source safely.

4. Manual reverse engineering

    - When custom obfuscators are used, read and trace the unpacker, decode embedded strings, and understand the reassembly logic. This may require stepping through code in DevTools.

5. Reproduce functionality

    - Replicate important client actions with curl or other HTTP tools (e.g., POST to /serial.php) to confirm behavior without running obfuscated client-side code.

Quick curl examples

#### GET
```bash
curl http://SERVER_IP:PORT/
```


#### POST (no data)

```
curl -s http://SERVER_IP:PORT/ -X POST
```


#### POST (with data)

```
curl -s http://SERVER_IP:PORT/ -X POST -d "param1=sample"
```

----


### Useful commands (condensed)

```
echo text | base64 — base64 encode

echo b64 | base64 -d — base64 decode

echo text | xxd -p — hex encode

echo hex | xxd -p -r — hex decode

echo text | tr 'A-Za-z' 'N-ZA-Mn-za-m' — rot13 encode/decode

ctrl+u (Firefox) — view page source

```

----

### Tools & resources (short list)

- Run / debug / quick console: JS Console — https://jsconsole.com/

- Beautify / pretty print: Prettier — https://prettier.io/playground/, Beautifier — https://beautifier.io/

- Unpackers / deobfuscators: UnPacker — https://matthewfl.com/unPacker.html, JSNice — http://www.jsnice.org/

- Experiment / run snippets: playcode — https://playcode.io/javascript

- Special encoders: JSFuck, JJEncode, AAEncode (use sparingly — performance hit)

---

### Final notes / best practices

- Always prefer understanding unpacker logic rather than blindly running obfuscated code.

- Automated tools help but aren’t sufficient for custom obfuscation; manual analysis may be required.

- Avoid performing security/cryptographic logic client-side — it’s easy to bypass or extract keys.

- When publishing analyses/examples, strip any sensitive endpoints or secrets before posting.




