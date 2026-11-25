# Gabriel Affonso

**Linux Platform Engineer** · secure infrastructure and AI agent systems · Porto, Portugal

I build and run the infrastructure under my own company, [Esteio](#esteio), and the AI agents that work on top of it. Admin access exists only inside a VPN. Every change goes from Git through Ansible and Docker, with a snapshot first and a tested way back. I treat LLMs the same way I treat servers: I don't trust them to behave, I make the system enforce it. Output format is forced at the decoder, and an agent's permissions are set by the tools it is given, not by what its prompt asks.

Before infrastructure I was an electrical engineer for 5+ years, four of them running my own company. That's where I learned to scope work, manage risk, and explain trade-offs to people who aren't engineers.

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnubash&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat-square&logo=ansible&logoColor=white)
![Traefik](https://img.shields.io/badge/Traefik-24A1C1?style=flat-square&logo=traefikproxy&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![WireGuard](https://img.shields.io/badge/WireGuard-88171A?style=flat-square&logo=wireguard&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=flat-square&logo=cloudflare&logoColor=white)
![Claude](https://img.shields.io/badge/Claude-D97757?style=flat-square&logo=claude&logoColor=white)

---

## Infrastructure

**[zero-trust-vps-platform](https://github.com/gabzaf/zero-trust-vps-platform)**
The production platform that hosts client websites and the Esteio agents, documented as engineering case studies (Situation → Task → Action → Result).
Cloudflare WAF → host firewall (80/443 from Cloudflare only) → Traefik → segmented Docker networks. Admin over WireGuard only, centralised logs in Loki/Grafana, encrypted immutable backups. Every control is mapped to CIS v8 and NIST CSF, with the known gaps listed.
Notable finding: Docker silently bypassed my default-DROP firewall, because published ports go through `FORWARD` and never reach `INPUT`. [Case 02](https://github.com/gabzaf/zero-trust-vps-platform/blob/main/cases/case-02-container-platform-and-traefik-ingress/00-overview.md) covers how I found it and the fail-closed fix.

**[Inception-of-Things](https://github.com/gabzaf/Inception-of-Things)**
A two-node K3s cluster provisioned with Vagrant, host-based routing through Traefik Ingress, and GitOps delivery with Argo CD: the cluster follows the repository.

---

## AI agents

<a id="esteio"></a>
**Esteio: an agent-operated web agency** *(private repos)*
Esteio builds, hosts and maintains websites for small businesses in Portugal. I designed the system that runs it:
- **Lead pipeline in Python + SQLite.** It searches Google Maps and Instagram, audits each business's site, and writes a diagnosis sheet.
- **An AI agent with 8 skills** that scores leads, drafts outreach, prepares and analyses meetings, and keeps the CRM and finances. It runs on the VPS under systemd timers: a morning list and a daily batch on weekdays, and a weekly review.
- **Human in the loop by design.** The agent has no tool to send messages and cannot change its own code, and risky commands need approval. That's for GDPR and marketing rules, and so a person checks every contact.
- **A static site generator** with a content schema and validation, which turns an agent-written brief into a client demo site.

**Automated video production**
A code-driven pipeline that runs an Instagram channel: an agent writes the script, ElevenLabs generates the voice with word-level timing, SVG characters are animated to the narration, HyperFrames renders the video, and a review step approves it before publishing. The channel publishes three videos a day, and post metrics feed a written decision log.

**call_me_maybe**
Reliable function calling from a 0.6B model (Qwen3). Constrained decoding masks every token that would break the JSON schema, so the model picks the function and arguments but can't get the format wrong: **100% schema-valid calls, 91% fully correct.**
<sub>Python · transformers · Pydantic</sub>

**agent-smith**
My own Thought → Code → Observation agent loop, with no orchestration framework. It has a sandbox that limits imports, file paths, time and memory, a custom MCP server for its tools, and fallback across LLM providers with token, retry and latency tracking.

---

## Systems and security

| Project | What it is |
|---|---|
| [ft_transcendence](https://github.com/gabzaf/FT_TRANSCENDENCE) | Real-time web platform, team of 5. I owned infra and security: ModSecurity WAF, Vault, Docker Compose |
| [webserv](https://github.com/gabzaf/42_WebServer) | HTTP/1.1 server from scratch in C++98, single `poll()` event loop |
| [pentest-lab-reports](https://github.com/gabzaf/pentest-lab-reports) | Authorised lab findings: impact, root cause, fix |
| [cybersecurity-officer](https://github.com/gabzaf/cybersecurity-officer) | The Security Officer role under NIS2 (Portugal), mapped to ISO 27001, NIST CSF and CIS |

---

## Background

- **42 Porto**: common core completed (2023–2026), now in the advanced curriculum
- (ISC)² Certified in Cybersecurity · Cybersecurity Officer (CNCS / IPL) · Google Cybersecurity
- BSc Electrical Engineering and MBA in Energy, PUC-Rio
- Portuguese · English · Spanish

[LinkedIn](https://www.linkedin.com/in/affonsogabriel/)
