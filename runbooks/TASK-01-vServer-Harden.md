# Runbook: TASK 01 - vServer (Hub) absicher**Status: Erledigt.**

Server wurde am 09.11.2025 provisioniert und grundlegend gehärtet.

**Abgeschlossene Aufgaben:**
- [x] vServer bei 1blu (VPS SX, `(Public IP des Hubs)`) angemietet.
- [x] Erster Login als `root` und Passwort geändert.
- [x] Neuer Admin-Benutzer (`patrik`) mit `sudo`-Rechten erstellt.
- [x] SSH-Key-Login für `patrik` eingerichtet.
- [x] SSH-Login für `root` deaktiviert (`PermitRootLogin no`).
- [x] SSH-Passwort-Login deaktiviert (`PasswordAuthentication no`).
- [x] System-Updates (`apt update && apt upgrade`) ausgeführt.
- [x] Firewall (ufw) konfiguriert und `ssh` sowie `51820/udp` (WireGuard) erlaubt.