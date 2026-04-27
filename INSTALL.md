# Installation Guide

This guide is the source of truth for installing and validating the `summarize-slides` skill from scratch.
It is intentionally platform-generic, but it does define concrete default paths, concrete download sources, concrete validation states, and concrete runtime capability checks.

Repository:

- `https://github.com/Li-Baichuan-James/summarize-slides-skill`

Raw files for this skill:

- `https://raw.githubusercontent.com/Li-Baichuan-James/summarize-slides-skill/main/SKILL.md`
- `https://raw.githubusercontent.com/Li-Baichuan-James/summarize-slides-skill/main/INSTALL.md`
- `https://raw.githubusercontent.com/Li-Baichuan-James/summarize-slides-skill/main/README.md`
- `https://raw.githubusercontent.com/Li-Baichuan-James/summarize-slides-skill/main/LICENSE`

Companion `pdf` skill source:

- Repository path: `https://github.com/anthropics/skills/tree/main/skills/pdf`
- Required raw files:
  - `https://raw.githubusercontent.com/anthropics/skills/main/skills/pdf/SKILL.md`
  - `https://raw.githubusercontent.com/anthropics/skills/main/skills/pdf/LICENSE.txt`
- Recommended extra raw files:
  - `https://raw.githubusercontent.com/anthropics/skills/main/skills/pdf/forms.md`
  - `https://raw.githubusercontent.com/anthropics/skills/main/skills/pdf/reference.md`

Treat the raw URLs in this guide as the authoritative install source for a direct file-based local install.

State model used in this guide:

- `pdf status` is one of: `discoverability-confirmed`, `path-validated`, `unavailable`
- `latex status` is one of: `xelatex-ready`, `fallback-only`, `unavailable`
- `install result` is one of: `strictly validated`, `path-validated`, `incomplete`

Important naming rule:

- the repository name is `summarize-slides-skill`
- the installed local skill folder must be `summarize-slides`
- do not install this skill into a folder named `summarize-slides-skill`

## For Humans

Copy and paste this prompt to your LLM agent:

```text
Install and validate the `summarize-slides` skill by following this guide exactly:
https://raw.githubusercontent.com/Li-Baichuan-James/summarize-slides-skill/main/INSTALL.md
```

## For LLM Agents

Follow this order exactly.

1. Detect the host agent family.
Use one of these families: `OpenCode`, `Claude Code`, or `.agents/skills style setup`.

Use observable signals rather than guesswork:
- choose `OpenCode` if the environment, docs, or local paths clearly refer to `OpenCode` or `opencode`
- choose `Claude Code` if the environment, docs, or local paths clearly refer to `Claude Code` or `.claude`
- choose `.agents/skills style setup` if the environment uses the `.agents/skills` convention and does not present itself as `OpenCode` or `Claude Code`
- if the signals conflict or no family can be identified, stop and report the blocker instead of guessing

2. Resolve the default local skills directory for that family.
Use these defaults:
- `OpenCode` -> `~/.config/opencode/skills/`
- `Claude Code` -> `~/.claude/skills/`
- `.agents/skills style setup` -> `~/.agents/skills/`

3. Create `<skills-dir>/summarize-slides/`.

4. Install `summarize-slides` from the raw URLs listed in this guide.
Treat the raw URLs in this file as the authoritative install source for the skill contents.

Download these three files into `<skills-dir>/summarize-slides/` with these exact filenames:
- `SKILL.md`
- `README.md`
- `LICENSE`

Do not rename the folder to `summarize-slides-skill`.
Do not rely on repo metadata like `.git/` to make the skill work.

5. Verify that `<skills-dir>/summarize-slides/SKILL.md` exists directly inside the folder.

6. Check the companion `pdf` status.
Treat it as:
- `discoverability-confirmed` if the platform exposes an installed or bundled skill list that includes `pdf`
- `path-validated` if a local file exists at `<skills-dir>/pdf/SKILL.md`
- `unavailable` if neither of the above is true

7. If `pdf` is not available, install it from the companion source listed above.

Create `<skills-dir>/pdf/` and download at least:
- `SKILL.md`
- `LICENSE.txt`

Recommended additional files for fuller compatibility:
- `forms.md`
- `reference.md`

The helper scripts mentioned by the `pdf` skill are recommended only if the target environment wants the full Anthropic skill bundle. They are not required for this guide's minimum local `pdf` companion validation.

8. Re-check the `pdf status`.
If it is still `unavailable`, report the `install result` as `incomplete` for full `summarize-slides` use and stop.

9. Check the local LaTeX environment with these commands, in this order:
- `xelatex --version`
- `pdflatex --version`
- `latexmk --version`

10. Interpret the LaTeX check as a capability probe, not as proof that end-to-end PDF compilation is healthy.
Treat it as:
- `xelatex-ready` if `xelatex --version` returns a usable version string
- `fallback-only` if `xelatex` is unavailable but `pdflatex --version` or `latexmk --version` returns a usable version string
- `unavailable` if none of the three commands returns a usable version string

Missing `xelatex` degrades or blocks the preferred Chinese-first compiled PDF path for this skill, because `summarize-slides` explicitly prefers `xelatex` for Chinese text and math.
That does not by itself mean the skill is uninstalled.

If `latex status` is `fallback-only`, report that the preferred `xelatex` path is not validated and Chinese-heavy compiled PDF output may degrade or fail depending on the local TeX setup.

If `latex status` is `unavailable`, report that compiled PDF output is blocked in this environment, even if the skill installation itself is otherwise valid.

11. Verify installation state.
If the platform exposes a skill list or installed-skill view, confirm that `summarize-slides` appears there. That counts as `discoverability-confirmed` installation evidence.

If the platform does not expose such a mechanism, confirm that:
- the selected `<skills-dir>` matches the host-family rule in this guide, and
- `summarize-slides/SKILL.md` is directly inside that directory.

That counts only as `path-validated`, not `discoverability-confirmed`.

12. Report the final result with:
- detected agent family
- resolved skills directory
- installed skill path
- file list in `<skills-dir>/summarize-slides/`
- whether `pdf` is `discoverability-confirmed`, `path-validated`, or `unavailable`
- whether LaTeX is `xelatex-ready`, `fallback-only`, or `unavailable`
- whether the `install result` is `strictly validated`, `path-validated`, or `incomplete`
- any capability warning caused by missing `xelatex`

## Validation Standard

An installation counts as `strictly validated` by this guide only if all of the following are true:

- `<skills-dir>/summarize-slides/SKILL.md` exists
- `<skills-dir>/summarize-slides/README.md` exists
- `<skills-dir>/summarize-slides/LICENSE` exists
- companion `pdf` skill is `discoverability-confirmed`, or is `path-validated` with the required local files present
- if `pdf` was installed locally from this guide, then `<skills-dir>/pdf/SKILL.md` and `<skills-dir>/pdf/LICENSE.txt` both exist
- the installation is discoverability-confirmed under Step 11

If the platform does not expose a skill list or installed-skill view, but all file-placement checks pass, the `install result` may be reported as `path-validated` rather than `strictly validated`.

If the `pdf` companion is missing or still unavailable after Step 8, the `install result` is `incomplete` because `summarize-slides` requires `pdf` as a companion skill.

LaTeX is a runtime capability check, not the installation criterion.
If `xelatex` is missing, do not mark the skill uninstalled for that reason alone.

If `latex status` is `fallback-only`, the installation can still be `strictly validated` or `path-validated`, but the preferred Chinese-first compiled PDF workflow is degraded or unvalidated.

If `latex status` is `unavailable`, the installation can still be `strictly validated` or `path-validated` if all file-placement and `pdf` checks pass, but compiled PDF output is blocked until a TeX environment is installed.

If the raw `LICENSE` URL for this repository does not resolve yet in the published repo snapshot, do not silently ignore that gap. Report the install result as `incomplete` for this guide's full strict-validation standard until the published `LICENSE` file is available.

## Notes

- This guide is intentionally platform-generic in workflow, but not vague: it defines concrete default paths, concrete raw download sources, and concrete validation requirements.
- It does not prescribe platform-specific marketplace or plugin commands when direct file installation is sufficient.
- Runtime native PDF support does not substitute for the required `pdf` skill under this guide.
- The local install folder is `summarize-slides`, not `summarize-slides-skill`.
