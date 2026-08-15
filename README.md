# HTB Labs

My Hack The Box work. Scans, notes, and whatever exploit code I end up writing.

## How it's organized

Each box gets its own folder. Anything I reuse across boxes sits at the repo root.

```
.
├── <lab-name>/         # one folder per HTB machine
│   ├── nmap/           #   scans for that box
│   └── ...             #   exploits, notes, loot for that box
└── <shared tooling>    # reused across boxes, lives at the root
```

The rule is simple. If I only need it for one box, it stays in that box's folder. If I reach for it on every box (a helper script, a wordlist, a shared Python env), it goes in the root.

## Shared tooling

Big third-party toolkits don't get committed. They live outside the repo, and I symlink them into the root and git-ignore the link.

Right now that's just SecLists:

```sh
ln -s ../SecLists SecLists
```

It points at the [danielmiessler/SecLists](https://github.com/danielmiessler/SecLists) clone, which is around 5 GB. Run that command to recreate the link on a new machine.

## Labs

**cap/** has the nmap scans for Cap. `cap.*` is the real one, with ports 21, 22, and 80 open. `cap-initial.*` was an earlier run that came back all-filtered. I kept both.

**nexus-lab/** is a uv Python project. Its `cve-exploit.py` is a proof-of-concept for CVE-2026-38526, a Krayin CRM RCE, and it only matters for that box.

## Python

Per-box Python work runs on [uv](https://docs.astral.sh/uv/). To rebuild a box's environment from its lockfile:

```sh
cd nexus-lab
uv sync
```

I don't commit `.venv/`. It's git-ignored and I just rebuild it locally when I need it.
