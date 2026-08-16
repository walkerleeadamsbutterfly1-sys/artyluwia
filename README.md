# artyluwia

A small repository containing three obfuscated Lua script files: `script`, `v2`, and `v3`. Each file appears to have been produced with the "wearedevs" obfuscator and contains encoded/escaped byte sequences rather than readable source.

> WARNING: These files are obfuscated. They may contain unknown scripts or secrets this is very safe to use.

## Contents

- `script` — obfuscated Lua code (wearedevs obfuscator header).
- `v2` — obfuscated Lua code (wearedevs obfuscator header).
- `v3` — obfuscated Lua code (wearedevs obfuscator header).
- (No README or license present in the repository — consider adding one and documenting the source and purpose of these files.)

## Purpose

This README assumes the repository currently stores obfuscated Lua artifacts. If the repo's intent is different (examples, payloads, distribution), please update this README to reflect the project's goals, licensing, and provenance.

## Quick analysis / how to inspect safely

1. Do not execute the scripts on your production machine.
2. Use an isolated sandbox or container (example using Docker):
   - Create a disposable container or VM and analyze there.
   - Example (Alpine + Lua):
     - docker run --rm -it -v "$(pwd)":/work --workdir /work alpine:latest sh
     - apk add --no-cache lua5.3 coreutils
     - Inspect files with `head`, `strings`, `sed`, etc.

3. Useful local commands to gather quick info:
   - file script
   - head -n 30 script
   - strings script | head -n 50
   - sed -n '1,120p' script

4. Static analysis suggestions:
   - Search for patterns of runtime string-decoding or `load`/`loadstring`/`loadfile` calls that evaluate decoded text.
   - If the code contains only byte escapes, look for code that converts those escapes into real bytes and then executes them.
   - Compare versions (`script`, `v2`, `v3`) to see what changed between them.

5. Deobfuscation:
   - There is no universal deobfuscator. Deobfuscation often requires understanding the decoding routine implemented in the obfuscated file, then writing a translator to reproduce the decoding and dump the resulting plaintext.
   - If you are not comfortable reverse-engineering, ask the original author for the unobfuscated source or consult a trusted security analyst.

## Usage

This repository does not contain human-readable source. If your goal is to use or modify these scripts, request or restore the original (unobfuscated) source. If these files are intentionally distributed obfuscated, document:
- What the scripts do
- Any runtime dependencies (Lua version, libraries)
- How to configure and run them (in a sandbox)

## Contributing

- If you are the repository owner, please add:
  - A clear project description.
  - The original source (or explain why obfuscated artifacts are stored).
  - A license (see below).
  - Any tests or examples that show intended behavior.

- If you want to contribute deobfuscated/annotated versions, include:
  - A separate directory (e.g., `deobfuscated/`) with the recovered source.
  - A write-up of the deobfuscation method you used (for reproducibility and education).

## Security

- Treat these files as untrusted code until reviewed.
- Analyze in an isolated environment.
- Avoid running them with network access or elevated privileges.

## License

No license is present in this repository. If you own these files, add a LICENSE file to clarify reuse, distribution, and liability.

## Next steps / checklist for repo owner

- [ ] Add a short project description in README.
- [ ] Add a license file.
- [ ] Include unobfuscated source or documentation explaining why obfuscated artifacts are stored.
- [ ] Add analysis notes or a deobfuscation trace if you want to preserve a readable history.
