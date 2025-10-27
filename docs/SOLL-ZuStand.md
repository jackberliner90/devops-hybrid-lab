# SOLL-Zustand (Detaillierter Infrastruktur-Plan)

Dies ist die "Single Source of Truth" für alle IPs, VMs und Dienste.

## 1. IP-Adressplan (Isoliertes Lab-Netz: 192.168.100.0/24)

| Hostname      | VM-Name     | Zweck                   | IP-Adresse | Gateway | DNS 1      | DNS 2   |
| :------------ | :---------- | :---------------------- | :--------- | :------ | :--------- | :------ |
| **ROUTER-VM** | `VM-ROUTER` | Gateway, NAT, S2S-VPN   | `100.1`    | `100.1` | `100.10`   | `100.11`|
| **DC01** | `VM-DC01`   | AD, DNS, DHCP, iSCSI    | `100.10`   | `100.1` | `127.0.0.1`| `100.11`|
| **DC02** | `VM-DC02`   | AD, DNS, DHCP Failover| `100.11`   | `100.1` | `100.10`   | `127.0.0.1`|
| **FS01** | `VM-FS01`   | Cluster-Knoten 1        | `100.20`   | `100.1` | `100.10`   | `100.11`|
| **FS02** | `VM-FS02`   | Cluster-Knoten 2        | `100.21`   | `100.1` | `100.10`   | `100.11`|
| *(Virtuell)* | `CLUSTER-FS`| Cluster-Verwaltung      | `100.25`   | -       | -          | -       |
| *(Virtuell)* | `FILE-SHARE`| Dateiserver-Rolle       | `100.26`   | -       | -          | -       |
| **WEB01** | `VM-WEB01`  | Interner Webserver      | `100.30`   | `100.1` | `100.10`   | `100.11`|
| **WSUS** | `VM-WSUS`   | WSUS Server             | `100.40`   | `100.1` | `100.10`   | `100.11`|
| **RD-GW-WEB** | `VM-RDGW`   | RD-Gateway / Web        | `100.50`   | `100.1` | `100.10`   | `100.11`|
| **RD-BROKER01**| `VM-RDB1`   | RD Broker 1 (HA)        | `100.51`   | `100.1` | `100.10`   | `100.11`|
| **RD-BROKER02**| `VM-RDB2`   | RD Broker 2 (HA)        | `100.52`   | `100.1` | `100.10`   | `100.11`|
| **RD-SESS01** | `VM-RDS1`   | RD Session Host 1       | `100.55`   | `100.1` | `100.10`   | `100.11`|
| **RD-SESS02** | `VM-RDS2`   | RD Session Host 2       | `100.56`   | `100.1` | `100.10`   | `100.11`|
| **CLIENT01** | `VM-CLIENT01`| Test-Client            | `DHCP`     | `DHCP`  | `DHCP`     | `DHCP`  |
| **DHCP-BEREICH**| (Logisch)   | **`matzke.lab` Scope** | `100.100-150`| `100.1` | `100.10`   | `100.11`|

## 2. VM-Inventar (Ressourcenplan)

| VM-Name       | OS             | vCPUs | RAM (Min / Max) | VHDX 1 (OS) | VHDX 2 (Daten) |
| :------------ | :------------- | :---- | :-------------- | :---------- | :------------- |
| `VM-ROUTER`   | Ubuntu 22.04   | 1     | 512MB / 1GB     | 20 GB       | -              |
| `VM-DC01`     | Win Srv 22     | 2     | 2GB / 4GB       | 60 GB       | 50GB (iSCSI)   |
| `VM-DC02`     | Win Srv 22     | 2     | 2GB / 4GB       | 60 GB       | -              |
| `VM-FS01`     | Win Srv 22     | 2     | 2GB / 6GB       | 60 GB       | -              |
| `VM-FS02`     | Win Srv 22     | 2     | 2GB / 6GB       | 60 GB       | -              |
| `VM-WEB01`    | Win Srv 22     | 2     | 1GB / 4GB       | 50 GB       | -              |
| `VM-WSUS`     | Win Srv 22     | 2     | 4GB / 8GB       | 60 GB       | 200GB (WSUS)   |
| `VM-RDGW`     | Win Srv 22     | 2     | 2GB / 4GB       | 60 GB       | -              |
| `VM-RDB1`     | Win Srv 22     | 2     | 2GB / 4GB       | 60 GB       | -              |
| `VM-RDB2`     | Win Srv 22     | 2     | 2GB / 4GB       | 60 GB       | -              |
| `VM-RDS1`     | Win Srv 22     | 4     | 4GB / 8GB       | 60 GB       | -              |
| `VM-RDS2`     | Win Srv 22     | 4     | 4GB / 8GB       | 60 GB       | -              |
| `VM-CLIENT01` | Win 11         | 2     | 2GB / 4GB       | 60 GB       | -              |