# Changelog

## [v0.1.0] - 2026-07-30

### Added

- Initial packaging of **Iyke's Web3 Bughunt Skill** (`iykes-web3-bughunt-skill`).
- Renamed skill from `duke-web3-bug-hunting` (skill id only; researcher identity remains deviykee / Iyke).
- Extracted mechanical Steps 1–4 and 7 into `tools/` CLI scripts:
  - `step1_ground_truth.sh`
  - `step2_creator_trace.sh`
  - `step2_bundle_grep.sh`
  - `step3_surface_map.sh`
  - `step4_auth_triage.sh`
  - `step7_poc_scaffold.sh`
- Template fillers for Step 9 report and Step 10 first DM:
  - `step9_report_skeleton.py`
  - `step10_dm_skeleton.py`
- `tools/selftest.sh` smoke-checks graceful failure (usage message, non-zero exit, no hang).
- `tools/README.md` with purpose, usage, examples, and exit codes per script.
- Top-level README, MIT LICENSE, `.gitignore` for Foundry/hunt artifacts.
- Standalone git repo (separate from the broader `secres` workspace).
