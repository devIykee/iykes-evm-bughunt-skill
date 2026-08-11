# Changelog

## [v0.2.1] - 2026-08-10

### Added

- **Coverage tracking (mandatory):** maintain `coverage.md` during every hunt/audit
  with files opened, code paths traced (not just files touched), coverage %
  (X/Y files), and explicitly excluded areas with one-line reasons.
- Running table format plus top summary line `Coverage: X/Y files (Z%)`.
- Incremental update rule (as files are read, not only at the end).
- Low-coverage honesty gate before final report / user summary.
- Operating rule 10 and token-budget rule 9; Step 3 inventory sets Y; Step 9 and
  multi-finding packs include coverage.md.

## [v0.2.0] - 2026-08-10

### Added

- **Step 5 foundation map** before deep findings: state who-writes, external call
  order, token paths, access gates, structured PASS/FAIL first-pass checklist.
- **Step 5.5 multi-angle adversarial pass** for complex logic: malicious drain/freeze,
  economic/math, state/AC/reentrancy, edges, external integrations. Chunked prompts
  (one mechanism at a time).
- **Step 5.6 dual-ledger / multi-strategy vault hunt**: principal book vs NAV vs cash
  returned; forced questions (gross vs supplied, unrealizable NAV, phantom zero
  withdraw, maxWithdraw lie, view/pull asymmetry, epoch coupling, lastPass over-pull).
- **PRODUCT_TYPE** `multi-strategy-vault` and expanded vault attack questions.
- **Bug classes 8–12**: unrealizable NAV preferential exit; gross book vs supplied;
  phantom zero-return withdraw; view/pull asymmetry; compromised-agent churn without
  external send.
- **Severity second-opinion gate** (gas, AC, reachability, mitigations, temporary vs
  persistent). Temporary restore sandwich must be killed before claiming bank-run theft.
- **Optional companion skills** (forefy/.context): smart-contract-audit, tiny-auditor,
  foundry-poc. This playbook remains lead for intake/disclosure.
- **Slither triage rule**: no Critical from static High without a working PoC.
- **PoC quality bar** and Appendix B adversarial prompt pack; Appendix C hunt hygiene.
- Token-budget rule: chunk analysis, do not full-repo dump.

### Changed

- Operating rules: honest bounds, trust-root vs permissionless, temporary vs persistent.
- Step 3: source-only / pre-deploy repo audits allowed with local unit PoCs.
- Step 9: master findings table + multi-finding private pack guidance.
- Description frontmatter updated for new steps and dual-ledger focus.

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
