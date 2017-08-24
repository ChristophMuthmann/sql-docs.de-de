---
title: "Always On-verfügbarkeitsgruppe für SQL Server on Linux | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c5c7e602ac1beedb028072b4c82578e9948af43d
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="availability-groups-for-sql-server-on-linux"></a>Verfügbarkeitsgruppen für SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

Eine SQL Server Always On-verfügbarkeitsgruppe ist eine hohe Verfügbarkeit (HA), Wiederherstellung im Notfall (DR) und die Lösung mit horizontaler Skalierung. Es bietet hohe Verfügbarkeit für Gruppen von Datenbanken auf direkt angeschlossener Speicher. Unterstützt mehrere sekundäre Replikate für integrierte hohe Verfügbarkeit und DR, automatische fehlererkennung schnell transparentes Failover und Lastenausgleich lesen. Diese Breite Palette von Funktionen können Sie eine optimale SLAs für Ihre arbeitsauslastungen Verfügbarkeit zu erzielen.

SQL Server-Verfügbarkeitsgruppen in SQL Server 2012 eingeführt wurden und wurden mit jeder Version verbessert. Diese Funktion ist nun unter Linux verfügbar. Um SQL Server-arbeitsauslastungen mit strengen Business Continuity Anforderungen zu berücksichtigen, Verfügbarkeitsgruppen, führen Sie auf allen unterstützten [Linux-Distributionen](sql-server-linux-release-notes.md). Darüber hinaus sind auch alle Funktionen, die Verfügbarkeitsgruppen eine flexible und effiziente Integrierte HA-DR-Lösung machen auf Linux verfügbar. Dazu gehören: 

- **Mit mehreren datenbankfailover** eine verfügbarkeitsgruppe unterstützt eine Failoverumgebung für einen Satz von Benutzerdatenbanken, die auch als verfügbarkeitsdatenbanken bezeichnet.
- **Schnelle fehlererkennung und Failover** als Ressource in einem Cluster mit hoher Verfügbarkeit, eine verfügbarkeitsgruppe, profitieren Sie von integrierten Cluster Intelligence für sofortige failovererkennung und failoveraktion.
- **Transparent Failover, die mithilfe von virtuellen IP-Adressressource** ermöglicht Client einzelnen Verbindungszeichenfolge zum primären im Falle eines Failovers zu verwenden. Erfordert die Integration mit einem Cluster-Manager.
- **Mehrere synchrone und asynchrone sekundäre Replikate** eine verfügbarkeitsgruppe unterstützt bis zu acht sekundäre Replikate. Mit synchronen Replikaten wartet, das primäre Replikat beim commit einer Transaktion, die das primäre Replikat für Transaktionen auf den Datenträger geschrieben werden, auf das Transaktionsprotokoll wartet. Das primäre Replikat wartet nicht für Schreibvorgänge auf asynchrone synchronen Replikaten.  
- **Manuelles oder automatisches Failover** Failover auf ein sekundäres Replikat kann ausgelöst werden automatisch vom Cluster oder bei Bedarf durch den Datenbankadministrator.
- **Aktive sekundäre Replikate, die gelesen und backup-Arbeitslasten zur** ein oder mehrere sekundäre Replikate können so konfiguriert werden, um schreibgeschützten Zugriff auf sekundäre Datenbanken unterstützen zudem werden mit Sicherungen auf sekundären Datenbanken zuzulassen.
- **Automatisches seeding** SQL Server erstellt automatisch die sekundären Replikate für jede Datenbank in der verfügbarkeitsgruppe.
- **Schreibgeschütztes routing** SQL-Server leitet eingehende Verbindungen an einen verfügbarkeitsgruppenlistener an ein sekundäres Replikat, das für schreibgeschützte Arbeitslasten konfiguriert ist. 
- **Integrität auf Datenbankebene Überwachung und Failover Datenbanktrigger** verbesserte datenbanküberwachung und Diagnose. 
- **Notfallwiederherstellungskonfigurationen** mit verteilte Verfügbarkeitsgruppen oder multisubnetz-Verfügbarkeit Gruppe eingerichtet. 
- **Skalieren von Lesevorgängen Funktionen** In SQL Server 2017 können eine verfügbarkeitsgruppe mit oder ohne hohe Verfügbarkeit für horizontale Skalierung nur-Lese Vorgänge. 


Ausführliche Informationen zu SQL Server-Verfügbarkeitsgruppen finden Sie unter [SQL Server Always On-Verfügbarkeitsgruppen](http://msdn.microsoft.com/library/hh510230.aspx).

## <a name="availability-group-terminology"></a>Availability Group-Terminologie

Eine verfügbarkeitsgruppe unterstützt eine Failoverumgebung für einen diskreten Satz von Benutzerdatenbanken – auch bezeichnet als verfügbarkeitsdatenbanken -, die zusammen ein Failover ausführen. Eine verfügbarkeitsgruppe unterstützt einen Satz primärer Datenbanken mit Lese-/ Schreibzugriff und einen bis acht Sätze entsprechender sekundärer Datenbanken. Optional können sekundäre Datenbanken für schreibgeschützten Zugriff und/oder einige Sicherungsvorgänge verfügbar gemacht werden. Eine verfügbarkeitsgruppe definiert einen Satz von zwei oder mehr failoverpartnern, bekannt als verfügbarkeitsreplikate. Verfügbarkeitsreplikate sind Komponenten der verfügbarkeitsgruppe. Weitere Informationen finden Sie [(Übersicht) der Always On-Verfügbarkeitsgruppen (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).

Die folgenden Begriffe Beschreiben der Hauptkomponenten von einer SQL Server-Lösung für die Verfügbarkeit Gruppe:

 Verfügbarkeitsgruppe  
 Ein Container für eine Gruppe von Datenbanken ( *Verfügbarkeitsdatenbanken*), für die zusammen ein Failover ausgeführt wird.  
  
 Verfügbarkeitsdatenbank  
 Eine Datenbank, die zu einer Verfügbarkeitsgruppe gehört. Für jede Verfügbarkeitsdatenbank verwaltet die Verfügbarkeitsgruppe eine einzelne Lese-/Schreibkopie (die *primäre Datenbank*) und eine bis acht schreibgeschützte Kopien (*sekundäre Datenbanken*).  
  
 primäre Datenbank  
 Die Lese-/Schreibkopie einer Verfügbarkeitsdatenbank.  
  
 Sekundäre Datenbank  
 Eine schreibgeschützte Kopie einer Verfügbarkeitsdatenbank.  
  
 Verfügbarkeitsreplikat  
 Eine Instanziierung einer verfügbarkeitsgruppe, die von einer bestimmten Instanz von SQL Server gehostet und verwaltet eine lokale Kopie jeder verfügbarkeitsdatenbank, die zur verfügbarkeitsgruppe gehört. Zwei Typen von Verfügbarkeitsreplikaten sind vorhanden: ein einzelnes *primäres Replikat* und ein bis acht *sekundäre Replikate*.  
  
 primäres Replikat  
 Das Verfügbarkeitsreplikat, das die primären Datenbanken für Lese-/Schreibverbindungen von Clients verfügbar macht und darüber hinaus Transaktionsprotokoll-Datensätze für jede primäre Datenbank an jedes sekundäre Replikat sendet.  
  
 Sekundäres Replikat  
 Ein Verfügbarkeitsreplikat, das eine sekundäre Kopie jeder Verfügbarkeitsdatenbank beibehält und als potenzielles Failoverziel für die Verfügbarkeitsgruppe dient. Optional kann ein sekundäres Replikat schreibgeschützten Zugriff auf sekundäre Datenbanken und das Erstellen von Sicherungen für sekundäre Datenbanken unterstützen.  
  
 Verfügbarkeitsgruppenlistener  
 Ein Servername, mit dem Clients eine Verbindung herstellen können, um auf eine Datenbank in einem primären Replikat einer Verfügbarkeitsgruppe zuzugreifen. Verfügbarkeitsgruppenlistener leiten eingehende Verbindungen an das primäre Replikat oder ein schreibgeschütztes sekundäres Replikat weiter.  


## <a name="new-in-sql-server-2017-for-availability-groups"></a>Neu in SQL Server-2017 für Verfügbarkeitsgruppen

SQL Server-2017 verfügt über neue Funktionen für Verfügbarkeitsgruppen.

**CLUSTER_TYPE** verwenden mit `CREATE AVAILABILITY GROUP`. Identifiziert den Typ des Server-Cluster-Managers, die eine verfügbarkeitsgruppe verwaltet. Einer der folgenden Typen kann sein:

   - **WSFC** Winows Server-Failovercluster. Unter Windows ist es der Standardwert für CLUSTER_TYPE.
   - **EXTERNE** einen, die unter Linux mit Schrittmacher ist beispielsweise nicht Windows Server-Failovercluster - Manager.
   - **KEINE** keine Cluster-Manager. Für eine verfügbarkeitsgruppe Skalieren von Lesevorgängen verwendet.

Weitere Informationen zu diesen Optionen finden Sie unter [CREATE AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878399.aspx) oder [ALTER AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878601.aspx).

**Garantiert ein Commit ausgeführt wird auf synchrone sekundäre Replikate**

Use `required_synchronized_secondaries_to_commit`with `CREATE AVAILABILITY GROUP` or `ALTER AVAILABILITY GROUP`. Wenn `required_synchronized_secondaries_to_commit` auf einen höheren Wert als 0 (null) auf dem primären Replikat Datenbanken gewartet werden, bis die Transaktion, auf die angegebene Anzahl von ausgeführt wird Transaktionen festgelegt **synchronen sekundären Replikat** Datenbankprotokolle Replikat. Wenn nicht genügend synchrone sekundäre Replikate online sind, werden alle Verbindungen mit dem primären Replikat, bis die Kommunikation mit ausreichend sekundären Replikate fortgesetzt, zurückgewiesen.

**Skalieren von Lesevorgängen Verfügbarkeitsgruppen**

Erstellen einer verfügbarkeitsgruppe ohne einen Cluster zum Skalieren von Lesevorgängen arbeitsauslastungen zu unterstützen. Finden Sie unter [Skalieren von Lesevorgängen Verfügbarkeitsgruppen](../database-engine/availability-groups/windows/read-scale-availability-groups.md).

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren der verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)

[Konfigurieren Sie Skalieren von Lesevorgängen verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-rs.md)

[Verfügbarkeitsgruppe-Clusterressource auf RHEL hinzufügen](sql-server-linux-availability-group-cluster-rhel.md)

[Verfügbarkeitsgruppe-Clusterressource auf SLES hinzufügen](sql-server-linux-availability-group-cluster-sles.md)

[Verfügbarkeitsgruppe-Clusterressource auf Ubuntu hinzufügen](sql-server-linux-availability-group-cluster-ubuntu.md)

