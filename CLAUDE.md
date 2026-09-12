# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project context

This is "Taller 1" for MINE-4101 (Ciencia de Datos Aplicada, Universidad de los Andes): an EDA of
Colombian public procurement contracts for goods (SECOP II, 2019–2025). Full assignment brief is
in `Taller 1.pdf`. The deliverable is a self-contained, sequentially-runnable notebook (or notebooks)
plus a README that together cover:

1. Initial data understanding (dimensions, dtypes, top 5 attributes with univariate analysis, data
   quality issues found and how they were treated).
2. A stated analysis strategy (a paragraph or two) for identifying which contracts warrant closer
   supervision — spanning basic statistics through hypothesis tests and multivariate visualization.
3. Implementation of that strategy: explicit data processing, statistical/visualization techniques,
   and interpreted insights. Hypotheses must be explicit and contrasted, reporting both significant
   and non-significant results.
4. An executive-facing set of targeting criteria for the control office (contract value, modality,
   destino del gasto, sector, etc.), plus explicit limitations of the analysis.

There is no README yet — one is required by the assignment (team members, objective, scope,
insights/conclusions, repo organization, run instructions, dependencies). No `environment.yml`
or dependency manifest exists yet either, despite being gitignored (suggesting one is expected but
not yet created).

## Data

- `secop_bienes.parquet` is the working dataset (~196k rows × 36 cols). It is gitignored (as are
  `*.csv` and `environment.yml`) — **never commit it**, and don't assume it exists in a fresh clone.
- Loaded via `pandas.read_parquet`. Known issue already flagged in the notebook: several column
  names have broken encoding from a lost `ó`/`ó`/`ón` (mojibake), e.g. `duraci_n_del_contrato`,
  `g_nero_representante_legal`, `liquidaci_n`, `obligaci_n_ambiental` — treat this as a data quality
  issue to document/fix, not a schema to preserve as-is.
- Money columns (`valor_del_contrato`, `valor_pagado`, `valor_facturado`, `valor_pendiente_de_pago`)
  and date columns (`fecha_de_firma`, `fecha_de_inicio_del_contrato`, `fecha_de_fin_del_contrato`)
  are central to the supervision-targeting analysis (deviations = plazo adicionado, presupuesto no
  ejecutado, cierre sin liquidar).
- The brief explicitly calls out that the 2019–2025 range may not be fully comparable across years —
  picking and justifying an analysis window is part of the task, not a given.

## Environment

- No dependency manifest currently exists. `.vscode/settings.json` points at a conda environment
  (`ms-python.python:conda`) for the Jupyter kernel. If adding dependencies, create the
  `environment.yml` the `.gitignore` already anticipates (or ask before assuming pip/venv instead).
- No test suite, linter, or build step in this repo — it's a single analysis notebook. "Correctness"
  here means the notebook runs top-to-bottom without errors (a hard delivery requirement) and its
  statistical claims are sound, not passing CI.

## Working conventions

- Keep analysis in the notebook; markdown cells should carry the interpretation/insight next to the
  code that produced it, per the assignment's "implementation + interpretation" requirement.
- The notebook already has a running "Pendientes de limpieza detectados" markdown cell tracking
  known data quality issues — extend it as new issues are found rather than scattering TODOs.
- When editing the notebook, use the NotebookEdit tool rather than hand-editing the `.ipynb` JSON.
