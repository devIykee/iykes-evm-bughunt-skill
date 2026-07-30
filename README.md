# Iyke's Web3 Bughunt Skill

**Status: personal research tool, not accepting external contributions.**

End-to-end EVM smart-contract bug-hunting playbook (researcher: **deviykee** / **Iyke**).
Fill the INTAKE block in `SKILL.md`, then run Steps 1–10: ground-truth the chain, locate
core contracts, map the surface, triage auth, hunt by product type and bug class, fork-prove
findings, score severity honestly, write the report, and disclose privately. Mechanical
probes live in `tools/`; judgment stays in the playbook.

Skill id: `iykes-web3-bughunt-skill` (formerly `duke-web3-bug-hunting` as a skill name only).

## Folder structure

```text
.
├── SKILL.md           # Playbook: INTAKE, rules, Steps 1–10, templates
├── LICENSE            # MIT — Copyright (c) 2026 Iyke / deviykee
├── CHANGELOG.md
├── README.md          # This file
└── tools/
    ├── README.md      # Per-script usage + exit codes
    ├── selftest.sh    # Graceful-failure smoke test
    ├── step1_ground_truth.sh
    ├── step2_creator_trace.sh
    ├── step2_bundle_grep.sh
    ├── step3_surface_map.sh
    ├── step4_auth_triage.sh
    ├── step7_poc_scaffold.sh
    ├── step9_report_skeleton.py
    └── step10_dm_skeleton.py
```

This repo is pure tooling. Do not commit filled INTAKE blocks, live hunt addresses,
draft reports/DMs, or `poc/` artifacts. Keep hunt work elsewhere (e.g. a private workspace).

## Prerequisites

Install commands (Linux/macOS-style):

```bash
# Foundry (provides forge + cast)
curl -L https://foundry.paradigm.xyz | bash
foundryup
# ensure on PATH, e.g.:
export PATH="$HOME/.foundry/bin:$PATH"

# Python 3
# Debian/Ubuntu:
sudo apt-get update && sudo apt-get install -y python3 curl
# macOS:
# brew install python3 curl

# GitHub CLI (optional; Step 10 private disclosure repo only)
# Debian/Ubuntu: see https://github.com/cli/cli#installation
# macOS: brew install gh
# then: gh auth login

# jq is optional and not required by these scripts
```

### Versions tested in this packaging environment

| Tool | Version |
|---|---|
| `forge` | 1.7.1 |
| `cast` | 1.7.1 |
| `python3` | 3.13.13 |
| `gh` | 2.96.0 |
| `curl` | system |

```bash
forge --version   # forge Version: 1.7.1
cast --version    # cast Version: 1.7.1
```

After clone:

```bash
chmod +x tools/*.sh tools/*.py
./tools/selftest.sh
```

## Quickstart

1. Open `SKILL.md` and fill **INTAKE** (only fields you know; omit unknowns).
2. Set shell vars: `RPC=...; CID=...; BS=<EXPLORER>/api/v2`.
3. Run steps in order:
   - Step 1: `./tools/step1_ground_truth.sh "$RPC" "$CID"`
   - Step 2: creator-trace and/or bundle-grep until you have a core address
   - Step 3: `./tools/step3_surface_map.sh "$RPC" "$CID" "0x..." "$BS"`
   - Step 4: `./tools/step4_auth_triage.sh "$RPC" "0x..."`
   - Steps 5–6: read with attack questions + bug-class playbook (manual)
   - Step 7: `./tools/step7_poc_scaffold.sh "$RPC" "0x..." poc` then fill and fork-test
   - Step 8: honest severity (manual)
   - Step 9: `python3 ./tools/step9_report_skeleton.py ... -o reports/...`
   - Step 10: `python3 ./tools/step10_dm_skeleton.py ... -o reports/dm-...` then private DM
4. Follow operating rules in `SKILL.md` on every hunt.

## Tools

| Script | Step | Inputs | Outputs / gates | Why this exists |
|---|---|---|---|---|
| `step1_ground_truth.sh` | 1 | RPC, chain id | PASS/STOP on chain | Avoid hours on dead/scam RPCs |
| `step2_creator_trace.sh` | 2A | explorer API, token | creator address | Reliable factory/core discovery |
| `step2_bundle_grep.sh` | 2B | website URL | role-labeled 0x hits | Find hidden frontend config addrs |
| `step3_surface_map.sh` | 3 | RPC, chain, contract, [API] | balance, Sourcify, selectors | Verified vs unverified path |
| `step4_auth_triage.sh` | 4 | RPC, contract, [sigs] | guarded / OPEN | Free-win missing-auth check |
| `step7_poc_scaffold.sh` | 7 | RPC, target, [dir] | Foundry PoC + forge cmd | Repeatable fork-only proof setup |
| `step9_report_skeleton.py` | 9 | INTAKE + severity fields | report markdown | Same report shape every hunt |
| `step10_dm_skeleton.py` | 10 | project/severity/impact | first DM text | Consistent private first contact |
| `selftest.sh` | — | none | pass/fail smoke | Catch broken tools before a hunt |

Full usage strings, examples, and exit codes: [`tools/README.md`](tools/README.md).

## Responsible disclosure

From the playbook operating rules (substance unchanged):

1. **Fork / `eth_call` verification only. Never move real funds on mainnet.**
2. **Honest severity.** State the bound. A Medium is a Medium.
3. **Ask, never threaten.** No "pay or I release/exploit".
4. **Kill your own finding if it doesn't hold up.**
5. **Never publish a live, unpatched bug.** Private channel + private repo until fixed.

Researcher identity for reports: **deviykee**. First DM voice: **Iyke** (http://x.com/deviykee).

## License

MIT — Copyright (c) 2026 Iyke / deviykee. See [LICENSE](LICENSE).
