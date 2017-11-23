---
title: "Leistung bewährte Methoden für SQL Server on Linux | Microsoft Docs"
description: "Dieses Thema enthält Richtlinien und bewährte Methoden für Leistung für die Ausführung von SQL Server-2017 unter Linux."
author: rgward
ms.author: bobward
manager: jhubbard
ms.date: 09/14/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: d6fb9839ee1ba7f583eca9445599422469212083
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-2017-on-linux"></a>Bewährte Methoden für Leistung und Konfigurationsrichtlinien für SQL Server-2017 unter Linux

Dieses Thema enthält bewährte Methoden und Empfehlungen zur Maximierung der Leistung für datenbankanwendungen, die Verbindung mit SQL Server unter Linux. Diese Empfehlungen gelten nur für auf dem Linux-Plattform ausgeführt wird. Alle normale SQL Server-Empfehlungen, wie z. B. Indexentwurf, gelten weiterhin.

Die folgenden Richtlinien enthalten Empfehlungen zum Konfigurieren von SQL Server- und Linux-Betriebssystems.

## <a name="sql-server-configuration"></a>SQL Server-Konfiguration

Es wird empfohlen, die folgenden Konfigurationsaufgaben ausführen, nach der Installation von SQL Server für Linux, um optimale Leistung für Ihre Anwendung zu gewährleisten.

### <a name="best-practices"></a>Bewährte Methoden

- **Verwenden Sie die PROZESSAFFINITÄT für den Knoten und/oder die CPUs**

   Es wird empfohlen, verwenden Sie `ALTER SERVER CONFIGURATION` festzulegende `PROCESS AFFINITY` für alle der **NUMANODEs** und/oder CPUs Sie verwenden nur für SQL Server (in der Regel für alle Knoten und CPUs) auf einem Linux-Betriebssystem. Prozessor-Affinität kann effiziente Linux- und Planen von SQL-Verhalten beibehalten. Mithilfe der **NUMANODE** Option ist die einfachste Methode. Beachten Sie, dass Sie die zu verwendende **PROZESSAFFINITÄT** selbst wenn Sie nur einen einzelnen NUMA-Knoten auf dem Computer haben.  Finden Sie unter der [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) Dokumentation weitere Informationen zum Festlegen **PROZESSAFFINITÄT**.

- **Konfigurieren Sie mehrere Tempdb-Datendateien**

   Da eine SQL Server auf Linux-Installation eine Option zum Konfigurieren von mehrere Tempdb-Dateien nicht bereitstellt, wird empfohlen, dass Sie erwägen, erstellen mehrere Tempdb-Datendateien, nach der Installation. Weitere Informationen finden Sie unter der Anleitung in diesem Artikel [Empfehlungen Zuordnung in SQL Server-Tempdb-Datenbank reduzieren](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d).

### <a name="advanced-configuration"></a>Erweiterte Konfiguration

Die folgenden Empfehlungen sind optionale-Konfigurationseinstellungen, die Sie festlegen, ob möglicherweise nach der Installation von SQL Server on Linux ausführen. Diese Optionen hängen von den Anforderungen Ihrer arbeitsauslastung und Konfiguration von Ihrem Linux-Betriebssystem.

- **Ein Arbeitsspeicherlimit mit Mssql-Conf festlegen**

   Um sicherzustellen, dass genügend freier Arbeitsspeicher für die Linux-Betriebssystem vorhanden ist, wird der SQL Server-Prozess nur 80 % des physischen Arbeitsspeichers standardmäßig verwendet. Für einige Systeme, die große Menge des physischen Arbeitsspeichers 20 % möglicherweise, eine erhebliche Anzahl. Beispielsweise würde auf einem System mit 1 TB RAM, die Standardeinstellung ca. 200 GB RAM nicht verwendete lassen. In diesem Fall empfiehlt es sich um das Arbeitsspeicherlimit auf einen höheren Wert konfigurieren. Finden Sie in der Dokumentation für die **Mssql-Conf** Tool und die [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) festlegen, die steuert, des Arbeitsspeichers für SQL Server (in Einheiten von MB) sichtbar.

   Wenn Sie diese Einstellung zu ändern, achten Sie darauf, dass Sie nicht auf ein zu hoher Wert festgelegt. Wenn Sie nicht genügend Arbeitsspeicher lassen, können Sie bei Problemen mit der Linux-Betriebssystem und andere Linux-Anwendungen auftreten.

## <a name="linux-os-configuration"></a>Linux-Betriebssystem-Konfiguration

Erwägen Sie die folgenden Linux-Betriebssystem-Konfigurationseinstellungen, die beste Leistung für eine SQL Server-Installation zur Verfügung.

### <a name="kernel-settings-for-high-performance"></a>Kernel-Einstellungen für hohe Leistung

Dies sind die empfohlenen Linux-Betriebssystem Einstellungen im Zusammenhang mit hoher Leistung und den Durchsatz für eine SQL Server-Installation. Finden Sie in Ihrem Linux-Betriebssystem-Dokumentation für den Prozess zum Konfigurieren dieser Einstellungen.



> [!Note]
> Für Benutzer von Red Hat Enterprise Linux (RHEL) wird der Durchsatz Leistungsprofil diese Einstellungen automatisch (mit Ausnahme von C-Status) konfigurieren.

Die folgende Tabelle enthält Empfehlungen für die CPU-Einstellungen:

| Einstellung | Wert | Weitere Informationen |
|---|---|---|
| CPU-Häufigkeit Ressourcenkontrolle | Leistung | Finden Sie unter der **Cpupower** Befehl |
| ENERGY_PERF_BIAS | Leistung | Finden Sie unter der **x86_energy_perf_policy** Befehl |
| min_perf_pct | 100 | Finden Sie in der Dokumentation auf Intel-p-Status |
| C-Status | Nur C1 | Finden Sie in Ihrem Linux oder System-Dokumentation zum Sicherstellen der C-Status nur auf C1 festgelegt ist |

Die folgende Tabelle enthält Empfehlungen für die datenträgereinstellungen:

| Einstellung | Wert | Weitere Informationen |
|---|---|---|
| Datenträger-Read-Aheads | 4096 | Finden Sie unter der **Blockdev** Befehl |
| Sysctl-Einstellungen | Kernel.sched_min_granularity_ns = 10000000<br/>Kernel.sched_wakeup_granularity_ns = 15000000<br/>VM.dirty_ratio = 40<br/>VM.dirty_background_ratio = 10<br/>VM.swappiness=10 | Finden Sie unter der **Sysctl** Befehl |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>Kernel-Einstellung Auto Numa Lastenausgleich für NUMA-Systemen mit mehreren Knoten

Bei der Installation von SQL Server auf mehreren Knoten **NUMA** Systeme, die folgenden **kernel.numa_balancing** Kernel-Einstellung ist standardmäßig aktiviert. SQL Server auf einen Betrieb mit maximaler Effizienz ermöglichen eine **NUMA** System, deaktivieren Sie automatische Numa Lastenausgleich in einem NUMA-System mit mehreren Knoten:

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>Kernel-Einstellungen für virtuellen Adressraum

Die Standardeinstellung von **vm.max_map_count** (dies 65536 ist) möglicherweise nicht hoch genug für eine SQL Server-Installation. Ändern Sie diesen Wert (das eine Obergrenze festgelegt ist), um 256 KB.

```bash
sysctl -w vm.max_map_count 262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>Deaktivieren des letzten Zugriffs auf Datum/Uhrzeit auf Dateisystemen, für die SQL Server-Daten und Protokolldateien

Verwenden der **Noatime** Attribut mit einem beliebigen Dateisystem, der zum Speichern von SQL Server-Daten und Protokolldateien verwendet wird. Finden Sie in Ihrem Linux-Dokumentation zum Festlegen dieses Attributs.

### <a name="leave-transparent-huge-pages-thp-enabled"></a>Lassen Sie Transparent große Seiten (THP) aktiviert

Die meisten Linux-Installationen sollten diese Option standardmäßig befinden sich auf. Es wird empfohlen, die meisten konsistente Leistung zu erzielen, um diese Konfigurationsoption aktiviert zu lassen.

### <a name="swapfile"></a>Auslagerungsdatei

Stellen Sie sicher, dass Sie auf einer ordnungsgemäß konfigurierten Swapfile zur Vermeidung einer unzureichenden Arbeitsspeicher verfügen. Wenden Sie sich an Ihre Linux-Dokumentation für das Erstellen und streamingbedarf eine Auslagerungsdatei.

### <a name="virtual-machines-and-dynamic-memory"></a>Virtuelle Computer und dynamischer Arbeitsspeicher

Wenn Sie SQL Server on Linux auf einem virtuellen Computer ausführen, stellen Sie sicher, dass Sie Optionen auswählen, korrigieren Sie die Größe des Arbeitsspeichers für den virtuellen Computer reserviert. Verwenden Sie keine Funktionen wie Hyper-V Dynamic Memory.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu SQL Server-Funktionen, die Leistung verbessern, finden Sie unter [erste Schritte mit Leistungsfunktionen](sql-server-linux-performance-get-started.md).

Weitere Informationen zu SQL Server unter Linux finden Sie unter [Übersicht über die von SQL Server on Linux](sql-server-linux-overview.md).
