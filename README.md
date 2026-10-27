# labdex plugins

The official Marketplace of [labdex](https://github.com/reykimedev/labdex): a signed
`index.json` at **https://reykimedev.github.io/labdex-plugins/index.json**, which every labdex
trusts out of the box (signed with the labdex project key).

> [!WARNING]
> Built with AI, for home labs only: labdex and its plugins were written largely with an AI
> coding assistant (Claude), directed and reviewed by a human. They haven't had an independent
> security audit and may contain security problems. Run them on a trusted home network.

## How it works

- Every plugin lives in its own repository (`labdex-plugin-<id>`). Publishing a GitHub
  release there (tag `v<version>`) signs the plugin and attaches `<id>-<version>.zip` to it.
- [`plugins.yaml`](plugins.yaml) lists those repositories. The
  [publish workflow](.github/workflows/publish.yml) reads their releases every six hours (or
  when this repository changes), checks each archive's checksum and signature, and publishes
  the index: every release is a version you can install, update to or go back to, with its
  release notes.
- A version is withdrawn by adding `withdrawn: {"1.2": "why"}` to its entry. labdex then warns
  everyone who has it, and updates skip it.

| Plugin | Repository |
| --- | --- |
| Ansible runner | [labdex-plugin-ansible](https://github.com/reykimedev/labdex-plugin-ansible) |
| Backup | [labdex-plugin-backup](https://github.com/reykimedev/labdex-plugin-backup) |
| Beszel | [labdex-plugin-beszel](https://github.com/reykimedev/labdex-plugin-beszel) |
| Certificates | [labdex-plugin-certificates](https://github.com/reykimedev/labdex-plugin-certificates) |
| Docker | [labdex-plugin-docker](https://github.com/reykimedev/labdex-plugin-docker) |
| File exports | [labdex-plugin-exports](https://github.com/reykimedev/labdex-plugin-exports) |
| k3s / Kubernetes | [labdex-plugin-k3s](https://github.com/reykimedev/labdex-plugin-k3s) |
| Login banner & prompt (Ansible) | [labdex-plugin-motd](https://github.com/reykimedev/labdex-plugin-motd) |
| nmap service discovery | [labdex-plugin-nmap](https://github.com/reykimedev/labdex-plugin-nmap) |
| OPNsense | [labdex-plugin-opnsense](https://github.com/reykimedev/labdex-plugin-opnsense) |
| Prometheus service discovery | [labdex-plugin-prometheus-sd](https://github.com/reykimedev/labdex-plugin-prometheus-sd) |
| Proxmox VE | [labdex-plugin-proxmox](https://github.com/reykimedev/labdex-plugin-proxmox) |
| Routing discovery | [labdex-plugin-routing](https://github.com/reykimedev/labdex-plugin-routing) |
| SNMP neighbours | [labdex-plugin-snmp](https://github.com/reykimedev/labdex-plugin-snmp) |
| Tailscale / Headscale | [labdex-plugin-tailscale](https://github.com/reykimedev/labdex-plugin-tailscale) |
| Technitium DNS | [labdex-plugin-technitium](https://github.com/reykimedev/labdex-plugin-technitium) |
| Traefik | [labdex-plugin-traefik](https://github.com/reykimedev/labdex-plugin-traefik) |
| UniFi Network | [labdex-plugin-unifi](https://github.com/reykimedev/labdex-plugin-unifi) |
| Uptime Kuma | [labdex-plugin-uptimekuma](https://github.com/reykimedev/labdex-plugin-uptimekuma) |
| VictoriaMetrics / Prometheus | [labdex-plugin-victoriametrics](https://github.com/reykimedev/labdex-plugin-victoriametrics) |
| YAML mirror | [labdex-plugin-yaml-mirror](https://github.com/reykimedev/labdex-plugin-yaml-mirror) |

## Your own plugins

Plugins signed with your own key go in a Marketplace of your own: copy this repository, list
your plugin repositories in `plugins.yaml` and set `LABDEX_SIGNING_KEY` to your key
(`labdex plugin keygen`). People add your index under Admin › Plugins › Repositories; labdex
pins your key from then on. Start a plugin repository with
`tools/plugin_repo/make_plugin_repo.py` from the labdex repository.
