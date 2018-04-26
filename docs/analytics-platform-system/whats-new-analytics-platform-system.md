---
title: Neuheiten bei Analytics Platform System – ein horizontaler Datawarehouse | Microsoft Docs
description: Neuigkeiten in Microsoft® Analytics Platform System angezeigt wird, eine horizontale Skalierung einer lokalen Anwendung, die MPP SQL Server Parallel Data Warehouse hostet.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4beb44ac45d95aa0338dc9dc0be0796a223d3243
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="whats-new-in-analytics-platform-system-2016-a-scale-out-mpp-data-warehouse"></a>Was ist neu in Analytics Platform System 2016, ein horizontaler MPP Datawarehouse
Neuigkeiten Sie in Microsoft® Analytics Platform System (APS) 2016, das neueste Update für die Anwendung für eine horizontale Skalierung lokalen Einheit, die MPP SQL Server Parallel Data Warehouse hostet. 

## <a name="sql-server-2016"></a>SQL Server 2016

APS 2016 wird auf die neueste Version von SQL Server 2016 ausgeführt und verwendet die standardmäßige Datenbank-Kompatibilitätsgrad 130 zur Verfügung.  SQL Server 2016 ermöglicht einige der neuen Features wie z. B. sekundäre Indizes für gruppierte columnstore-Indizes und Kerberos für PolyBase unterstützen. 


## <a name="t-sql"></a>T-SQL
APS-2016 unterstützt diese Verbesserungen der T-SQL-Kompatibilität.  Diese zusätzliche Sprachelemente vereinfachen die Migration von SQL Server und anderen Datenquellen. 

- [SQL-Sortierungen auf Spaltenebene][] werden jetzt zusätzlich zu den Windows-Sortierungen unterstützt.
- [Nicht gruppierte Indizes für gruppierte columnstore-Indizes][] Umfang zur Leistungssteigerung von Abfragen, Suchen nach bestimmten Werten in den gruppierten columnstore-Index. 
- [WÄHLEN SIE... IN][] 
- [sp_spaceused()][] zeigt der Speicherplatz verwendet, oder in einer Tabelle oder Datenbank reserviert.
- [Breite Tabellen][] Unterstützung entspricht dem SQL Server 2016. Das vorherige Limit von 32 KB für die Zeilengröße ist nicht mehr vorhanden. 

### <a name="data-types"></a>Datentypen

- [VARCHAR(max)][], [NVARCHAR(MAX)][] und [VARBINARY(MAX)][]. Diese LOB-Datentypen haben eine Maximalgröße von 2 GB. Laden Sie diese Objekte verwenden [Bcp (Hilfsprogramm)][]. Polybase und Dwloader unterstützen derzeit diese Datentypen. 
- [SYSNAME][]
- ["UNIQUEIDENTIFIER"][]
- [NUMERISCHE][] und dezimaldatentypen verwendet.

### <a name="window-functions"></a>Fensterfunktionen

- [ROWS oder RANGE][] in der OVER-Klausel der SELECT-Anweisung.
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

### <a name="security-functions"></a>Sicherheitsfunktionen (Transact-SQL)

- [CHECKSUM()][] und [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

### <a name="additional-functions"></a>Zusätzliche Funktionen

- [NEWID()][]
- [RAND()][]

## <a name="polybasehadoop-enhancements"></a>PolyBase-Hadoop-Erweiterungen

- Kompatibilität mit Hortonworks HDP 2.4 und HDP 2.5
- Unterstützung für Kerberos über datenbankweit gültige Anmeldeinformationen
- Unterstützung von Anmeldeinformationen mit Azure-Speicher-Blobs

## <a name="install-and-upgrade-enhancements"></a>Installation und Upgrade-Erweiterungen

### <a name="enterprise-architecture-updates"></a>Updates für Enterprise-Architektur
Ein Upgrade Ihrer vorhandene Appliance auf APS 2016 installiert die neuesten Firmware- und Treiberupdates zu erhalten, darunter Sicherheitsupdates. 

Eine neue Einheit von DELL oder HPE enthält die neuesten Updates plus:

- Aktuelle Generation-Prozessor-Unterstützung (Broadwell)
- Aktualisieren auf DDR4 DIMM
- Verbesserte DIMM-Durchsatz

### <a name="integration"></a>Integration

- Vollständig vereinfacht qualifizierten Domänennamen (FQDN)-Unterstützung zum Einrichten einer Vertrauensstellung mit der Einheit. 
- Um FQDN verwenden, müssen Sie führen eine vollständige Aktualisierung und während des Upgrades teilnehmen. 

### <a name="reduced-downtime"></a>Geringere Ausfallzeiten
Installation oder Aktualisierung auf APS 2016 ist schneller und erfordert weniger Ausfallzeiten als in vorherigen Versionen. Reduzieren von Ausfallzeiten, die zum Installieren oder aktualisieren: 

 - Anwenden von WSUS-Updates mithilfe eines Bildes optimiert enthält, die alle Updates bis Juni 2016
 - Wendet Sicherheit wurden Updates mit den Treiber und Firmware-updates
 - Fügt die neuesten Hotfixes und das Dienstprogramm zum Überprüfen der Appliance (PAV) auf Ihrem Gerät, sodass Sie sie bereit zum Installieren von mit nicht erforderlich, um sie herunterzuladen sind.


<!--MSDN references-->
[database compatibility level 130]:https://msdn.microsoft.com/library/bb510680.aspx
[SQL-Sortierungen auf Spaltenebene]:https://msdn.microsoft.com/library/ms143726.aspx
[Nicht gruppierte Indizes für gruppierte columnstore-Indizes]:https://msdn.microsoft.com/library/ms188783.aspx
[VARCHAR(max)]:https://msdn.microsoft.com/library/ms176089.aspx
[NVARCHAR(MAX)]:https://msdn.microsoft.com/library/ms186939.aspx
[VARBINARY(MAX)]:https://msdn.microsoft.com/library/ms188362.aspx
[SYSNAME]:https://msdn.microsoft.com/library/ms188021.aspx
[WÄHLEN SIE... IN]:https://msdn.microsoft.com/library/ms188029.aspx
[sp_spaceused()]:https://msdn.microsoft.com/library/ms188776.aspx
[Breite Tabellen]:https://msdn.microsoft.com/library/ms143432.aspx
[BULK INSERT]:https://msdn.microsoft.com/library/ms188365.aspx
[Bcp (Hilfsprogramm)]:https://msdn.microsoft.com/library/ms162802.aspx
["UNIQUEIDENTIFIER"]:https://msdn.microsoft.com/library/ms187942.aspx
[NUMERISCHE]:https://msdn.microsoft.com/library/ms187746.aspx
[ROWS oder RANGE]:https://msdn.microsoft.com/library/ms189461.aspx
[FIRST_VALUE]:https://msdn.microsoft.com/library/hh213018.aspx
[LAST_VALUE]:https://msdn.microsoft.com/library/hh231517.aspx
[CUME_DIST]:https://msdn.microsoft.com//library/hh231078.aspx
[PERCENT_RANK]:https://msdn.microsoft.com/library/hh213573.aspx
[CHECKSUM()]:https://msdn.microsoft.com/library/ms189788.aspx
[BINARY_CHECKSUM()]:https://msdn.microsoft.com/library/ms173784.aspx
[HAS_PERMS_BY_NAME()]:https://msdn.microsoft.com/library/ms189802.aspx
[NEWID()]:https://msdn.microsoft.com/library/ms190348.aspx
[RAND()]:https://msdn.microsoft.com/library/ms177610.aspx


  

  


