---
title: SP6 - Documentation Filtrage
author: Lucas Bidault
date: 11/10/2021
version: 1
---

# SP6 - Documentation Filtrage

[TOC]

## Création de la table de filtrage

### Filtrage-WAN

| N°  | Interface | IP Source | Port Source | IP Dest      | Port Dest | Status      | Protocole | Action |
| --- | --------- | --------- | ----------- | ------------ | --------- | ----------- | --------- | ------ |
| 1   | GE0/1     | **        | NONE        | **           | NONE      | NONE        | ICMP ER   | PERMIT |
| 2   | GE0/1     | **        | **          | **           | **        | ESTABLISHED | **        | PERMIT |
| 3   | GE0/1     | **        | **          | 172.16.19.11 | 1194      | NEW         | TCP       | PERMIT |
| 4   | GE0/1     | **        | **          | **           | **        | **          | **        | DENY   |

### Filtrage-LAN

| N°  | Interface     | IP Source      | Port Source | IP Dest | Port Dest | Status      | Protocole | Action |
| --- | ------------- | -------------- | ----------- | ------- | --------- | ----------- | --------- | ------ |
| 1   | GE0/0.10 - 80 | **             | NONE        | **      | NONE      | NONE        | ICMP E    | PERMIT |
| 2   | GE0/0.10 - 80 | 192.168.5.0/24 | **          | **      | **        | ESTABLISHED | **        | PERMIT |
| 3   | GE0/0.10 - 80 | 192.168.5.0/24 | **          | **      | 53        | NEW         | **        |        |
| 4   | GE0/0.10 - 80 | 192.168.5.0/24 | **          | **      | 21        | NEW         | TCP       |        |
| 5   | GE0/0.10 - 80 | 192.168.5.0/24 | **          | **      | 25        | NEW         | TCP       |        |
| 6   | GE0/0.10 - 80 | 192.168.5.0/24 | **          | **      | 143       | NEW         | TCP       |        |
| 7   | GE0/0.10 - 80 | 192.168.5.0/24 | **          | **      | 3389      | NEW         | TCP       |        |
| 8   | GE0/0.10 - 80 | 192.168.5.0/24 | **          | **      | 80        | NEW         | TCP       |        |
| 9   | GE0/0.10 - 80 | 192.168.5.0/24 | **          | **      | 443       | NEW         | TCP       |        |
| 10  | GE0/0.10 - 80 | **             | **          | **      | **        | **          | **        | DENY   |

### Filtrage-Server

| N°  | Interface     | IP Source      | Port Source | IP Dest | Port Dest | Status      | Protocole | Action |
| --- | ------------- | -------------- | ----------- | ------- | --------- | ----------- | --------- | ------ |
| 1   | GE0/0.10 - 80 | **             | NONE        | **      | NONE      | NONE        | ICMP E    | PERMIT |
| 2   | GE0/0.10 - 80 | 172.16.55.0/24 | **          | **      | **        | ESTABLISHED | **        | PERMIT |
| 3   | GE0/0.10 - 80 | 172.16.55.0/24 | **          | **      | 53        | NEW         | **        |        |
| 4   | GE0/0.10 - 80 | 172.16.55.0/24 | **          | **      | 21        | NEW         | TCP       |        |
| 5   | GE0/0.10 - 80 | 172.16.55.0/24 | **          | **      | 25        | NEW         | TCP       |        |
| 6   | GE0/0.10 - 80 | 172.16.55.0/24 | **          | **      | 143       | NEW         | TCP       |        |
| 7   | GE0/0.10 - 80 | 172.16.55.0/24 | **          | **      | 3389      | NEW         | TCP       |        |
| 8   | GE0/0.10 - 80 | 172.16.55.0/24 | **          | **      | 80        | NEW         | TCP       |        |
| 9   | GE0/0.10 - 80 | 172.16.55.0/24 | **          | **      | 443       | NEW         | TCP       |        |
| 10  | GE0/0.10 - 80 | **             | **          | **      | **        | **          | **        | DENY   |

## Paramétrage du filtrage sur le routeur cisco

### Filtrage-WAN

```
ip access-list extended filtrage-wan
    permit icmp any any echo-reply
    permit tcp any any established
    permit tcp any host 172.16.55.11 eq 1194
    deny ip any any

interface GigabitEthernet0/1
    ip access-group filtrage-wan in
```

### Filtrage-LAN

```
ip access-list extended filtrage-lan
    permit icmp any any echo
    permit udp any any eq 67
    permit udp 192.168.5.0 0.0.0.255 any eq 53 
    permit tcp 192.168.5.0 0.0.0.255 any eq 53 
    permit tcp 192.168.5.0 0.0.0.255 any eq 21 
    permit tcp 192.168.5.0 0.0.0.255 any eq 110 
    permit tcp 192.168.5.0 0.0.0.255 any eq 143 
    permit tcp 192.168.5.0 0.0.0.255 any eq 3389 
    permit tcp 192.168.5.0 0.0.0.255 any eq 80 
    permit tcp 192.168.5.0 0.0.0.255 any eq 443 
    deny ip any any

interface GigabitEthernet0/0.10 - 80
    ip access-group filtrage-lan in
```

### Filtrage-Server

```
ip access-list extended filtrage-serveur
    permit icmp any any echo
    permit udp host 172.16.55.2 any eq 68
    permit udp 172.16.55.0 0.0.0.255 any eq 53 
    permit tcp 172.16.55.0 0.0.0.255 any eq 53 
    permit tcp 172.16.55.0 0.0.0.255 any eq 21 
    permit tcp 172.16.55.0 0.0.0.255 any eq 110 
    permit tcp 172.16.55.0 0.0.0.255 any eq 143 
    permit tcp 172.16.55.0 0.0.0.255 any eq 3389 
    permit tcp 172.16.55.0 0.0.0.255 any eq 80 
    permit tcp 172.16.55.0 0.0.0.255 any eq 443 
    deny ip any any

interface GigabitEthernet0/0.55
    ip access-group filtrage-server in
```
