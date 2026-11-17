# Network overview (lab addressing)

All addresses and VLAN IDs are placeholders from the plan. Real values stay in the private repo.

```mermaid
flowchart TB
  ISP((Internet)) --> UDM[UDM Pro Max<br/>gateway for every VLAN]
  UDM --> SW[Switching]
  SW --> DEF[Default 10.0.1.0/24<br/>network equipment]
  SW --> HOUSE[Household VLANs<br/>cameras .30, iot .40, adults .50, kids .60,<br/>printers .70, media players .80, guest .90]
  SW --> MGMT[IT_Mgmt 10.0.10.0/24]
  SW --> SERVERS[Servers 10.0.20.0/24]
  SW --> SOC[VLAN 100 SOC 10.0.100.0/24<br/>Wazuh, Greenbone, n8n, ntfy, IRIS]
  SW --> TEST[Testing 10.0.110.0/24<br/>bench devices]
  SW --> AI[VLAN 120 AI 10.0.120.0/24<br/>no internet<br/>Ollama, Whisper, Piper]
  SERVERS --- PVE[Proxmox host<br/>Home Assistant OS VM]
  SOC --- PVE
  AI --- PVE
  HOUSE -. "syslog UDP 514" .-> SOC
  PVE -. "Wazuh agents TCP 1514/1515" .-> SOC
  SOC -- "Ollama 11434" --> AI
  PVE -- "HA to Whisper 10300, Piper 10200" --> AI
```

## Data flow in one line

Endpoints and network devices send logs to Wazuh. Wazuh and Greenbone raise alerts. n8n asks a local LLM to summarize them, then waits for a phone approval on ntfy before it acts.
