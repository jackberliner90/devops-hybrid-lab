# Portfolio: DevOps Hybrid-Cloud Infrastruktur (WIP 🚧)

Dieses Repository dokumentiert den Aufbau meiner Hybrid-Cloud-Laborumgebung. Das Ziel ist die praxisnahe Umsetzung von DevOps-Prinzipien (IaC, Security, CI/CD) und die Vorbereitung auf die Zertifizierungen AZ-104, AZ-400, AZ-800 und AZ-801.

**Status:** In Arbeit. Der Fortschritt wird über [das Projekt-Board](https://github.com/users/jackberliner90/projects/1) getrackt. *(Link ggf. anpassen)*

## Projekt-Architektur (SOLL-Zustand)

Dies ist der logische Netzplan für das finale Setup (Domain: `matzke.lab`):

```text
                                [ ☁️ INTERNET ]
                                      ^
                                      | (Hat öffentliche IP: z.B. 178.254.***.***)
+-------------------------------------+-------------------------------------------------------+
| [ ☁️ 1blu VPS SX (Hub) ]             | [ ☁️ AZURE CLOUD ]                                    |
|   (OS: Ubuntu, Docker, k3s)         |   (Für M365, Cloud Witness, AD Connect, SQL DB)       |
|                                     |                                                       |
|   [ 🐳 Container: WireGuard-Server ] |   • ❗Azure SQL Database (Für RDS-Broker HA)         |
|       (VPN-Netz: 10.200.0.0/24)     |   • Storage (Cloud Witness)                           |
|   [ 🐳 Container: Nginx, osTicket ]  |                                                       |
+-------------------------------------+-------------------------------------------------------+
       ^                                    ^ ^
       | (S2S VPN-Tunnel)                   | | (Quorum)
       |                                    | +---(SQL-Verbindung)
+------+------------------------------------+---+--------------------------------------------+
| [ 🏠 PHYSISCHER HOST-SERVER (i7) @ HOME-LAB ]                                               |
|   Host-OS: Windows Server 2022 + HYPER-V                                                    |
|                                                                                           |
| --- Hyper-V vSwitches ------------------------------------------------------------------ |
|   [ 🌐 vSwitch-Extern ] [ 🔒 vSwitch-Intern (192.168.100.0/24) ]                           |
|                                                                                           |
| --- Hyper-V VMs (Domain: matzke.lab) --------------------------------------------------- |
|                                                                                           |
|   [ 🛡️ VM: ROUTER-VM (Linux, 100.1) ] (Baut S2S-Tunnel ZU 1blu-Hub)                         |
|   [ 🤖 VM: DC01 (100.10) ] --(AD Connect)--> [ ☁️ AZURE CLOUD ]                             |
|   [ 🤖 VM: DC02 (100.11) ]                                                                  |
|   [ 📁 VM: FS01 (100.20) ] --(Quorum)------> [ ☁️ AZURE CLOUD ]                             |
|   [ 📁 VM: FS02 (100.21) ] (Stellt \\FILE-SHARE\Profile bereit)                             |
|   [ 🩹 VM: WSUS (100.40) ]                                                                  |
|   [ 🖥️ VM: RD-GW-WEB (100.50) ]                                                             |
|   [ 🧠 VM: RD-BROKER01 (100.51) ] --(DB)--> [ ☁️ AZURE SQL ]                                 |
|   [ 🧠 VM: RD-BROKER02 (100.52) ] --(DB)--> [ ☁️ AZURE SQL ]                                 |
|   [ 💼 VM: RD-SESSION01 (100.55) ] (Load Balanced)                                          |
|   [ 💼 VM: RD-SESSION02 (100.56) ] (Load Balanced)                                          |
|   [ 👩‍🔬 VM: CLIENT01 (DHCP) ]                                                               |
|                                                                                           |
+-------------------------------------------------------------------------------------------+
