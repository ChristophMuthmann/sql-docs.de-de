---
title: "SQL Server-Konfiguration (R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# SQL Server-Konfiguration (R Services)
Die Informationen in diesem Abschnitt liefert eine allgemeine Anleitung für die Hardware und Netzwerk-Konfiguration des Computers, der verwendet wird, um den Host [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Es sollte berücksichtigt werden, zusätzlich zu den allgemeinen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Angaben für die Optimierung der [Performance-Zentrum für SQL Server-Datenbankmodul und Azure SQL-Datenbank](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## Prozessor

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] können parallele Aufgaben mithilfe der verfügbaren Kerne auf dem Computer; die größeren Anzahl von Kernen, die verfügbar sind, desto besser die Leistung. Da [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] normalerweise gleichzeitig von mehreren Benutzern verwendet, sollte der Datenbankadministrator die ideale Anzahl von Kernen, die erforderlich sind, um die maximale Auslastung Berechnungen unterstützen bestimmen. Die Anzahl der Kerne für IO Operations gebundenen nicht helfen kann, CPU-bezogener Algorithmen von schnelleren CPUs mit vielen Kernen profitieren.

## Speicher

Die Menge des verfügbaren Speichers auf dem Computer haben einen großen Einfluss auf die Leistung der erweiterte analytische Algorithmen. Nicht genügend Arbeitsspeicher kann den Grad der Parallelität beeinflussen, wenn den SQL Server-Kontext. Sie können auch beeinflussen die Segmentgröße (Zeilen pro Lesevorgang), die verarbeitet werden kann und die Anzahl gleichzeitiger Sitzungen, die unterstützt werden können.

Mindestens 32GB wird dringend empfohlen. Wenn Sie mehr als 32 GB zur Verfügung haben, können Sie die SQL-Datenquelle, um weitere Zeilen in jedem Lesevorgang verwenden, zur Verbesserung der Leistung konfigurieren.

## Energieoptionen

Auf dem Windows-Betriebssystem die __hohe Leistung__ Power-Option sollte verwendet werden. Mithilfe einer anderen Power-Einstellung führt zu verringerter oder inkonsistente Leistung bei Verwendung [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

## Datenträger-e/a

Training und Vorhersage Aufträge mithilfe von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] sind von Natur aus e gebunden, und hängen von der Geschwindigkeit der Datenträger, die auf die Datenbank gespeichert ist. Schnellere Laufwerke, z. B. solid-State-Laufwerke (SSD) können Ihnen helfen. 

Datenträger-e/a wird auch von einer anderen Anwendung, die Zugriff auf die Festplatte beeinflusst: z. B. Lesevorgänge für eine Datenbank durch andere Clients. Datenträger-e/a-Leistung kann auch beeinflusst werden, wird durch das Dateisystem verwendet wird, z. B. die Blockgröße, die durch das Dateisystem verwendet. Wenn mehrere Laufwerke verfügbar sind, speichern Sie die Datenbanken auf einem anderen Laufwerk als [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] desjenigen, der für [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] angesteuert werden nicht den gleichen Datenträger wie Anforderungen für Daten, die in der Datenbank gespeichert.

Datenträger-e/a kann die Leistung erheblich beeinträchtigen, RevoScaleR analytische Funktionen ausführen, die mehrere Iterationen während des Trainings verwendet. Z. B. `rxLogit`, `rxDTree`, `rxDForest` und `rxBTrees` alle verwenden mehrere Iterationen. Wenn die Datenquelle ist [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], diese Algorithmen verwenden Sie temporäre Dateien, die optimiert werden, um die Daten zu erfassen. Diese Dateien werden automatisch bereinigt, wenn die Sitzung abgeschlossen ist. Müssen einen hochleistungsfähigen Datenträger für Lese-/Schreibvorgänge kann die insgesamt verstrichene Zeit für diese Algorithmen erheblich verbessern.

> [!NOTE]
> [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] erfordert die 8.3-Dateiname-Unterstützung auf Windows-Betriebssystemen. Sie können fsutil.exe verwenden, um zu bestimmen, ob ein Laufwerk 8.3-Dateinamen unterstützt, oder um Unterstützung zu aktivieren, wenn dies nicht der Fall. Weitere Informationen zur Verwendung von fsutil.exe mit 8.3-Dateinamen finden Sie unter [Fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).

### Tabellenkomprimierung

E/a-Leistung kann oft mit Komprimierung oder Columstore Indizes verbessert werden. Im Allgemeinen ist Daten oft wiederholt in verschiedenen Spalten in einer Tabelle mit einem columnstore-Index diese Wiederholungen nutzt, wenn die Daten komprimiert.

Ein columnstore-Index ist möglicherweise nicht so effizient, wenn eine von Einfügevorgängen in der Tabelle Vielzahl, jedoch ist eine gute Wahl, wenn die Daten statisch oder nur selten geändert werden. Wenn ein einspaltiger Speicher nicht geeignet ist, kann die Aktivierung der Komprimierung bei einer großen Tabelle Zeilen verwendet werden, zur Verbesserung der e/a.

Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md)

* [Aktivieren der Komprimierung für eine Tabelle oder einen Index](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [Beschreibung von Columnstore-Indizes](Columnstore%20Indexes%20Guide.md)

## Auslagerungsdatei

Windows-Betriebssystem verwendet eine Auslagerungsdatei, Absturzabbilder verwalten und zum Speichern von Seiten des virtuellen Speichers. Wenn Sie feststellen, übermäßiges Auslagern dass, erhöhen Sie den physischen Speicher auf dem Computer. Obwohl eine weitere physische Speicherkapazität Paging nicht beseitigt werden, wird es die Notwendigkeit für das Paging reduziert.

Die Geschwindigkeit des Datenträgers, die die Auslagerungsdatei auf kann auch die Leistung beeinträchtigen. Speichern die Auslagerungsdatei auf eine SSD oder über mehrere Auslagerungsdateien über mehrere SSDs kann die Leistung verbessern.

Finden Sie unter [Bestimmen der geeigneten Auslagerungsdateigröße für 64-Bit-Versionen von Windows](https://support.microsoft.com/en-us/kb/2860880) Informationen zum Ändern der Größe der Auslagerungsdatei.

## Ressourcenkontrolle

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] unterstützt die Ressourcenkontrolle zur Steuerung der verschiedenen von verwendeten Ressourcen [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Der Standardwert für Speicherbedarf von R ist z. B. 20 % des insgesamt verfügbaren Arbeitsspeichers auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Dies geschieht, um sicherzustellen, dass [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Workflows von R-Aufträge mit langer Ausführung nicht ernsthaft beeinträchtigt werden. Diese Grenzen können jedoch durch den Datenbankadministrator geändert werden. 

Die Ressourcen beschränkt sind __MAX_CPU_PERCENT__, __MAX_MEMORY_PERCENT__, und __MAX_PROCESSES__. Um die aktuellen Einstellungen anzuzeigen, verwenden Sie diese [!INCLUDE[tsql_md](../../includes/tsql-md.md)] Anweisung:

```T-SQL
SELECT * FROM sys.resource_governor_external_resource_pools
``` 

Wenn [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ist in erster Linie für R-Dienste verwendet, es kann hilfreich sein, MAX_CPU_PERCENT 60 % und 40 % zu erhöhen. Wenn es viele R-Sitzungen, die mit dem gleichen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] zur gleichen Zeit, alle drei erhöht werden. Verwenden Sie zum Ändern der Werte zugeordnete Ressource [!INCLUDE[tsql_md](../../includes/tsql-md.md)] Anweisungen. 

In diesem Beispiel wird die Auslastung des Speichers auf 40 %:

```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)
```
Im folgenden Beispiel wird alle drei konfigurierbaren Werte:
```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`
``` 

> [!NOTE]
> Um Änderungen an diesen Einstellungen sofort wirksam zu machen, führen Sie die Anweisung `ALTER RESOURCE GOVERNOR RECONFIGURE` nach dem Ändern einer Arbeitsspeicher, CPU oder max Prozess festlegen. 

## Siehe auch
[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)

[EXTERNE RESSOURCEN-POOL ERSTELLEN](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [SQL Server-R Services Performance Tuning Guide](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 
 [Fallstudie zur Leistung](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R und Datenoptimierung](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)