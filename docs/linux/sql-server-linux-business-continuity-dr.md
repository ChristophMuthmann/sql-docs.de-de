---
title: "Notfallwiederherstellung für SQL Server on Linux | Microsoft Docs"
description: 
author: mihaelab
ms.author: mihaelab
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: c75717c8-c677-4033-8ca6-d0ac93aee04d
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 86f41971e06efb767dde336cf93f9224a204176d
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="business-continuity-and-database-recovery-sql-server-on-linux"></a>Business Continuity und Database Recovery SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server on Linux können Organisationen eine Vielzahl der Vereinbarung zum Servicelevel-Ziele, um verschiedene geschäftlichen Anforderungen gerecht zu erzielen.

Die einfachsten Lösungen nutzen Virtualisierungstechnologien um ein hohes Maß an Stabilität gegenüber Hostebene-Fehlern vor Hardwarefehlern zu gewährleisten, sowie die Flexibilität und ressourcenmaximierung Fehlertoleranz zu erreichen. Diese Systeme können lokal, in einer privaten oder öffentlichen Cloud und Hybrid-Umgebungen ausführen. Die einfachste Form der Wiederherstellung im Notfall und Schutz ist die datenbanksicherung. Einfache Lösungen, die in SQL Server 2017 RC2 verfügbar sind:

- **VM-Failover**
    - Robusten Schutz vor Gast- und Ebene OS-Fehler
    - Ungeplante und geplante Ereignisse
    - Minimaler Downtime für das Patchen und upgrades
    - RTO in Minuten


- [**Datenbank sichern und Wiederherstellen**](sql-server-linux-backup-and-restore-database.md) 
    - Schutz vor versehentlicher oder böswilliger datenbeschädigung
    - Schutz für die notfallwiederherstellung
    - RTO in Minuten, Stunden

Hohe Verfügbarkeit und Disaster Recovery Standardtechniken bieten Schutz auf Instanzebene, die zusammen mit der Infrastruktur für eine zuverlässige freigegebenen Speicher. Für SQL Server 2017 RC2 standard hoher Verfügbarkeit enthält:

- [**Failovercluster**](sql-server-linux-shared-disk-cluster-configure.md)
    - Instanz-Schutz auf Netzwerkebene
    - Der automatischen fehlererkennung und automatisches failover
    - Stabilität gegenüber Betriebssystem und SQL Server-Fehlern
    - RTO in Sekunden, Minuten


## <a name="summary"></a>Zusammenfassung

SQL Server 2017 RC2 unter Linux enthält Virtualisierung, Sicherung und Wiederherstellung und Failover Cluster, um hohe Verfügbarkeit und notfallwiederherstellung zu unterstützen. 
