# HTB Labs

Working notes, scans, and exploit code for Hack The Box machines.

## Layout

```
.
├── <lab-name>/         # one directory per HTB machine / lab
│   ├── nmap/           #   scan output for that box
│   └── ...             #   lab-specific exploits, notes, loot
└── <shared tooling>    # tools reused across every lab live at the repo root
```

### Convention

- **Common tools I always reach for** (shared scripts, helpers, wordlist
  pointers, a shared Python env, etc.) go in the **repo root**.
- **Lab-specific tools** (a PoC for one CVE, a box's nmap scans, per-box notes)
  **stay inside that lab's directory**.

## Shared tooling

Large third-party toolkits live **outside** this repo and are symlinked into the
root for convenience. They are git-ignored — never committed.

- **`SecLists/`** — symlink to `../SecLists` (the
  [danielmiessler/SecLists](https://github.com/danielmiessler/SecLists) clone,
  ~5 GB). Recreate the link on a new machine with:

  ```sh
  ln -s ../SecLists SecLists
  ```

## Labs

- **`cap/`** — nmap scans for the Cap machine. `cap.*` is the working scan
  (ports 21/22/80 open); `cap-initial.*` is an earlier all-filtered scan.
- **`nexus-lab/`** — uv-managed Python project. `cve-exploit.py` is a PoC for
  CVE-2026-38526 (Krayin CRM RCE), specific to this box.

## Python environments

Per-lab Python work uses [uv](https://docs.astral.sh/uv/). Recreate a lab's
environment from its lockfile:

```sh
cd nexus-lab
uv sync
```

`.venv/` directories are git-ignored and regenerated locally — never committed.
