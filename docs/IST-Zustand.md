# IST-Zustand (Ausgangslage)

Dies dokumentiert die physische und Netzwerk-Infrastruktur vor Projektbeginn am 27.10.2025.

## 1. Physische Infrastruktur (Home-Lab Server)

* **Server-Typ:** Eigenbau-Server
* **CPU:** Intel i7-8700 (6 Kerne / 12 Threads)
* **RAM:** 64 GB DDR4
* **Speicher:** 1.5 TB SSD 
* **Host-OS:** Windows Server 2022 Datacenter (Basis-Installation, noch keine Rollen konfiguriert)
* **IP-Adresse (Statisch):** `192.168.178.100` 

## 2. Admin-Arbeitsplatz

* **PC-Typ:** Separater Arbeitsplatz-PC
* **CPU:** Intel i5-13400
* **RAM:** 32 GB DDR5
* **Zweck:** Wird für Management (VS Code, Git, RDP, SSH, Browser-Zugriff auf Cloud-Portale) und den Zugriff auf das Lab über das geplante VPN genutzt.
* **Hinweis:** Dieser PC ist *nicht* Teil der zu bauenden SOLL-Infrastruktur, sondern das Management-Werkzeug.

## 3. Physisches Netzwerk (Heimnetz)

* **Router:** AVM FritzBox 7490
* **Netzwerk-ID:** `192.168.178.0/24`
* **Router/Gateway IP:** `192.168.178.1` 
* **Internet-Zugang:** Vorhanden.

## 4. Cloud-Konten & Software

* **Cloud-Konten:** Azure Test-Konto, M365 Developer Tenant (müssen erstellt bzw. aktiviert werden).
* **Management-Software:** VS Code, Git, Windows Terminal (auf Admin-Arbeitsplatz installiert).
