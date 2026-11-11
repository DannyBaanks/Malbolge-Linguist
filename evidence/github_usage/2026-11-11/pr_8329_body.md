Hi Linguist maintainers!

I've prepared a Malbolge language definition, a TextMate grammar, a real Classic Malbolge sample, and a reproducible test environment.

I want to be transparent: **this proposal does not currently meet Linguist's usage threshold**. My latest search found only 37 `.malbolge` files. I understand the published requirements and the guidance already provided in Discussion #8164.

I'm submitting this as an explicit request for an exception or reconsideration, not as a claim that the requirements have been satisfied.

Malbolge has a long history and an existing ecosystem of interpreters, compilers, educational tools, and research projects. I believe there may be value in considering that context, even though it does not substitute for measured source-file usage.

The implementation and supporting evidence are available here:

https://github.com/DannyBaanks/Malbolge-Linguist

I understand if the maintainers decide to close this PR under the current policy. I appreciate your time and the guidance you've already provided.

Thank you!

## Checklist:

- [x] **I am adding a new language.**
  - [ ] The extension of the new language is used in hundreds of repositories on GitHub.com.
    - Search results for each extension:
      - https://github.com/search?type=code&q=NOT+is%3Afork+path%3A*.malbolge
      - Not met: 37 files via the code search API on 2026-11-11 (42 on 2026-09-02).
  - [x] I have included a real-world usage sample for all extensions added in this PR:
    - Sample source(s):
      - `samples/Malbolge/truth_machine.malbolge`: written by me for this PR. It is a Classic Malbolge truth machine (input `0` halts, input `1` loops), not a Hello World.
    - Sample license(s): MIT (I am happy for it to be included under Linguist's MIT license)
  - [x] I have included a syntax highlighting grammar: https://github.com/DannyBaanks/malbolge-syntax (MIT, `source.malbolge`, added with `script/add-grammar`)
  - [x] I have added a color
    - Hex value: `#1D1A2F`
    - Rationale: a near-black deep violet, chosen by me. Malbolge has no official branding. The color is meant to stay readable in the language bar on light and dark themes.
  - [ ] I have updated the heuristics to distinguish my language from others using the same extension.
    - Not needed: no other language in Linguist uses `.malbolge`. `.mal` and `.mb` are not claimed.

🤖 Generated with [Claude Code](https://claude.com/claude-code)
