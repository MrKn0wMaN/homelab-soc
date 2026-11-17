# homelab-soc

A home security operations center built on a single Proxmox server and UniFi network: Wazuh as SIEM and endpoint protection, Greenbone for vulnerability scanning, n8n as SOAR with phone approvals through ntfy, DFIR-IRIS for cases, and a local, air-gapped LLM (Ollama) that triages alerts but never acts on its own.

Everything here is sanitized: addresses, names and keys are placeholders.

## Layout

| Folder | What |
| --- | --- |
| `docs/sessions/` | One write-up per build session |
| `configs/` | Wazuh rules and decoders, n8n workflow JSON, Docker Compose files |
| `scripts/` | Bridge scripts and Ansible playbooks |
| `diagrams/` | Architecture and network diagrams |
| `blog/` | Source for the GitHub Pages blog |

## Status

Build started November 2026. See `docs/sessions/` for progress.
