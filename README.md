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

## Shared tooling

Big third-party toolkits don't get committed. They live outside the repo, and I symlink them into the root and git-ignore the link.

Right now that's just SecLists:

```sh
ln -s ../SecLists SecLists
```

It points at the [danielmiessler/SecLists](https://github.com/danielmiessler/SecLists) clone.

## Python

Per-box Python work runs on [uv](https://docs.astral.sh/uv/). To rebuild a box's environment from its lockfile:

```sh
cd nexus-lab
uv sync
```
