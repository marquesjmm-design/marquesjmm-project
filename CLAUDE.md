# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this directory is

`D:\Claude marquesjmm` is a personal workspace, **not a single project**. The top level itself is not under version control; it holds two independent git repos and one loose file, all unrelated to each other:

| Item | What it is |
|---|---|
| `Petrotec/` | Own git repo, local only — no remote. Holds the Petrotec deliverables, currently the 5-slide deck for executive management. Content is internal and sensitive (turnover, commercial pressure), so any remote must be private and explicitly confirmed by the user. |
| `pr-practice/` | Own git repo with a GitHub remote. The only code project. |
| `sporting-leoes-em-campo.html` | Standalone single-file page (inline CSS/JS, Google Fonts). Opens directly in a browser; no build step. Not in any repo. |

Do not look for shared architecture, a common build, or cross-references between these — there are none. Treat each as its own task. `git` commands only work from inside one of the two repo directories; the top level is not a repo.

The user works in **European Portuguese (PT-PT, not PT-BR)**. Write deliverables and prose in PT-PT unless asked otherwise.

## Toolchain

Installed and verified working (2026-08-26):

| Tool | Version | Notes |
|---|---|---|
| Node / npm | 24.19.0 LTS / 11.17.0 | `C:\Program Files\nodejs` |
| Python / pip | 3.13.15 / 26.2.1 | User install; correctly shadows the Microsoft Store stub |
| LibreOffice | 26.2.5.2 | **Not on PATH** — invoke `"$env:ProgramFiles\LibreOffice\program\soffice.exe"` |
| Microsoft PowerPoint | Office16 | `C:\Program Files\Microsoft Office\root\Office16\POWERPNT.EXE` |
| `gh` | authenticated as `marquesjmm-design` | |

The Node/Python toolchain the `pptx`, `docx`, and `xlsx` skills document (pptxgenjs, markitdown, `validate.py`, `soffice`) now runs here — use it rather than hand-rolling OOXML.

**The one remaining gap: `pdftoppm` (Poppler) is not installed.** The skills' render step is `soffice --convert-to pdf` followed by `pdftoppm`, so that second half will fail. Export slide images directly from PowerPoint COM instead — faster and a more faithful render than the LibreOffice path anyway:

```powershell
$ppt = New-Object -ComObject PowerPoint.Application
$pres = $ppt.Presentations.Open($file, $true, $false, $false)  # ReadOnly, no window
$pres.Export($outDir, 'PNG', 1920, 1080)                       # -> DiapositivoN.PNG
```

This doubles as the strongest validity check available: if PowerPoint opens a generated file without offering to repair it, the package is sound.

## PowerShell 5.1 gotchas

This shell is Windows PowerShell 5.1, and two of its behaviours will mislead you here:

**Native stderr is wrapped as an error and flips `$?` to false even on exit code 0.** Both `npm` (update notices) and `soffice` (a harmless "Could not find platform independent libraries" message) write to stderr on success, and PowerShell renders that as a red `NativeCommandError` block. Judge these commands by `$LASTEXITCODE`, not by appearance or `$?` — and do not report a run as failed on the strength of that block alone.

**A `.ps1` saved without a BOM is read as ANSI, corrupting every Portuguese accent in its output.** When writing a script that emits PT-PT text, prepend a UTF-8 BOM before running it:

```bash
printf '\xEF\xBB\xBF' > build_bom.ps1 && cat build.ps1 >> build_bom.ps1
```

## pr-practice

A deliberately tiny math-utils library whose purpose is **practising the GitHub pull request workflow** — the code is a pretext, the git/PR mechanics are the point. Expect work here to be about branches, PRs, and reviews rather than about features.

```bash
npm test          # runs `node mathUtils.test.js`; prints "add: ok" / "multiply: ok"
```

The test file is a plain `node` script with no framework, so there is no single-test runner or filter flag — to run one case, edit or comment out calls in `mathUtils.test.js`.

`main` is the default branch and work happens on feature branches (e.g. `fix/readme-typo-and-missing-test`), which already have upstreams on `origin`.
