## Projekt-Architektur (SOLL-Zustand)

Das Netzwerk-Design folgt dem **Bastion-Host-Prinzip** ("Defense in Depth").
Der Zugang erfolgt ausschließlich über den gehärteten VPN-Gateway.

```text
      [ ☁️ INTERNET (Angriffsfläche) ]
             |
             | (Nur Port 51820/UDP offen)
             v
+----------------------------------+      (Sicherer Tunnel)     +------------------------+
| [ 🛡️ VPS SX (Bastion / Hub) ]    | <========================> | [ 🏠 HOME-LAB (Spoke) ]|
|   • OS: Ubuntu 22.04             |      (WireGuard VPN)       |   • Router-VM          |
|   • Rolle: Security Gateway      |                            |   • AD / Hyper-V       |
|   • Keine Apps, nur VPN          |                            |   • RDS Farm           |
+----------------------------------+                            +------------------------+
      ^      |
      |      | (Sicherer Tunnel)
      |      v
      |    +--------------------------+
      |    | [ ⚙️ VPS RX16 (Worker) ]  |
      |    |   • OS: Ubuntu 22.04     |
      |    |   • Rolle: App-Server    |
      |    |   • Docker / k3s         |
      |    |   • osTicket / Nginx     |
      |    +--------------------------+
      |
      +--- (Admin-Zugriff via VPN)