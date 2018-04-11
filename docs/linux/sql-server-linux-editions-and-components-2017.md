---
title: Editionen und unterstützten Funktionen von SQL Server-2017 ~ Linux | Microsoft Docs
ms.custom: sql-linux
ms.date: 09/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: sql-linux
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- default components
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
ms.assetid: ''
caps.latest.revision: 121
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: da867b1125d4ee444a0e04e34d729484bee43514
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="editions-and-supported-features-of-sql-server-2017-on-linux"></a>Editionen und unterstützten Funktionen von SQL Server-2017 unter Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieser Artikel enthält Details zu Features, die von den verschiedenen Editionen von SQL Server-2017 unter Linux unterstützt. Editionen und unterstützten Funktionen von SQL Server unter Windows finden Sie unter [2017 für SQL Server - Windows](../sql-server/editions-and-components-of-sql-server-2017.md).  
  
Die Installationsanforderungen variieren je nach den benötigten Anwendungen. Die verschiedenen Editionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tragen den individuellen Leistungs-, Laufzeit- und Preisanforderungen von Organisationen und Einzelpersonen Rechnung. Welche [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Komponenten Sie installieren, hängt auch von den individuellen Anforderungen ab. In den folgenden Abschnitten erfahren Sie, wie Sie die bestmögliche Auswahl unter den in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]verfügbaren Editionen und Komponenten treffen.  

Die neuesten Versionsanmerkungen und Informationen zu Neuerungen finden Sie über die folgenden Links:
- [SQL Server unter Linux: Anmerkungen zu dieser Version](sql-server-linux-release-notes.md)
- [Neuigkeiten in SQL Server on Linux](sql-server-linux-whats-new.md)

Eine Liste der SQL Server-Funktionen unter Linux nicht verfügbar, finden Sie unter [nicht unterstützte Funktionen und Dienstleistungen](sql-server-linux-release-notes.md#Unsupported).

### <a name="try-sql-server"></a>Testen Sie SQL Server!    
    
[Herunterladen von SQLServer 2017](http://www.microsoft.com/sql-server/sql-server-2017)

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Editionen  
 In der folgenden Tabelle werden die Editionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]beschrieben. 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Edition|Definition|  
|---------------------------------------|----------------|  
|Enterprise|Das Premium-Angebot [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise Edition bietet eine umfassende hochwertige datencenterfunktionen mit blitzschneller Performance hohe Servicelevel für unternehmenswichtige Arbeitslasten.|  
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard Edition bietet grundlegende datenverwaltung für Abteilungen und kleinere Unternehmen ihre Anwendungen ausführen und unterstützt allgemeine Entwicklungstools für lokale und Cloud – ermöglicht eine effektive datenbankverwaltung mit minimalen IT-Ressourcen.|  
|Web|Die[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition ist eine mit geringen Anschaffungs- und Betriebskosten verbundene Option für Webhoster und Web-VAPs, die kostengünstige Skalierbarkeit und Verwaltungsfunktionen für Webpräsenzen jeder Größe bietet.|  
|Entwickler|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer Edition ermöglicht Entwicklern das Erstellen beliebiger Anwendungen auf der Basis von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Sämtliche Funktionen der Enterprise Edition stehen zur Verfügung. Die Lizenz bezieht sich jedoch auf die Verwendung als Entwicklungs- und Testsystem und nicht als Produktionsserver. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer ist eine ideale Option zum Erstellen und Testen von Anwendungen.|  
|Express Edition|Die Express Edition ist eine kostenlose Datenbank auf Einstiegsebene und eignet sich ideal zum Üben und zum Erstellen von datengesteuerten Anwendungen für Desktopcomputer und kleine Server. Dies ist die beste Wahl für unabhängige Softwareanbieter, Entwickler und Tüftler, die Clientanwendungen erstellen. Wenn Sie erweiterte Datenbankfunktionen benötigen, können Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express nahtlos auf höhere Endversionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]aktualisieren.|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>Verwenden von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mit Client-/Server-Anwendungen  

Sie können auch nur die Clientkomponenten von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf einem Computer mit Client-/Serveranwendungen installieren und so eine direkte Verbindung mit einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz herstellen. Die Installation der Clientkomponenten ist auch dann eine gute Wahl, wenn Sie eine Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf einem Datenbankserver verwalten, oder wenn Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Anwendungen entwickeln möchten.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-components"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Komponenten  

SQL Server-2017 unter Linux unterstützt die SQL Server-Datenbankmodul. Die folgende Tabelle beschreibt die Funktionen im Datenbankmodul.   
  
|Serverkomponenten|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] enthält die [!INCLUDE[ssDE](../includes/ssde-md.md)], den Kerndienst zum Speichern, verarbeiten und Sichern von Daten, Replikation, Volltextsuche, Tools zum Verwalten von relationalen und XML-Daten, und klicken Sie in der Datenbank Analytics-Integration.|  

**Developer, Enterprise Core und Evaluation Edition**  
Von der Developer, Enterprise Core und Evaluation-Editionen unterstützte Funktionen finden Sie unter Funktionen für die SQL Server Enterprise Edition in den folgenden Tabellen aufgeführt.

Die Developer Edition unterstützt weiterhin nur einen Client für [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md). 
  
##  <a name="Cross-BoxScaleLimits"></a> Skalierungsgrenzen  
  
|Funktion|Enterprise|Standard|Web|Express| 
|-------------|----------------|--------------|---------|------------------------|
|Maximale von einer einzelnen Instanz verwendete Rechenkapazität ( [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Maximum des Betriebssystems|Beschränkt auf weniger als 4 Sockets oder 24 Kerne|Beschränkt auf weniger als 4 Sockets oder 16 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne| 
|Maximale von einer einzelnen Instanz verwendete Rechenkapazität ( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oder [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)])|Maximum des Betriebssystems|Beschränkt auf weniger als 4 Sockets oder 24 Kerne|Beschränkt auf weniger als 4 Sockets oder 16 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne|
|Maximaler Arbeitsspeicher für den Pufferpool pro Instanz von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Maximum des Betriebssystems|128 GB|64 GB|1410 MB|
|Maximaler Arbeitsspeicher für Columnstore-Segmentcache pro Instanz von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Unbegrenzter Arbeitsspeicher| 32 GB| 16 GB| 352 MB|  
|Maximale speicheroptimierte Datengröße pro Datenbank in [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Unbegrenzter Arbeitsspeicher| 32 GB| 16 GB| 352 MB|
|Maximale relationale Datenbankgröße|524 PB|524 PB|524 PB|10 GB|  
  
<sup>1</sup> Enterprise Edition mit Server + Client Clientzugriffslizenz (CAL) basierte Lizenzierung (für neue Verträge nicht verfügbar) ist auf maximal 20 Kerne pro SQL Server-Instanz beschränkt. Für das auf Prozessorkernen basierende Serverlizenzierungsmodell gelten keine Beschränkungen. Weitere Informationen finden Sie unter [Kapazitätsgrenzen zu berechnen, indem Sie SQL Server-Edition](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
 
##  <a name="RDBMSHA">
            </a> RDBMS: Hochverfügbarkeit  
  
|Funktion|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|Protokollversand|ja|ja|ja|nein|  
|Sicherungskomprimierung|ja|ja|Nein|nein| 
|Datenbankmomentaufnahme|ja|Nein|Nein|nein|
|Always On-Failoverclusterinstanz<sup>1</sup>|ja|ja|Nein|nein| 
|Always On-Verfügbarkeitsgruppen<sup>2</sup>|ja|Nein|Nein|nein|
|Basis-Verfügbarkeitsgruppen <sup>3</sup>|nein|Ja|Nein|nein|
|Mindestreplikate für Commitverfügbarkeitsgruppen|ja|ja|Nein|nein|
|Verfügbarkeitsgruppe ohne Cluster|ja|ja|Nein|nein|
|Onlineseiten- und Onlinedateiwiederherstellung|ja|Nein|Nein|nein|
|Online-Indizierung|ja|Nein|Nein|nein|
|Fortsetzbare Neuerstellung von online geschalteten Indizes|ja|Nein|Nein|nein|
|Onlineschemaänderung|ja|Nein|Nein|nein|
|Schnelle Wiederherstellung|ja|Nein|Nein|nein|
|Gespiegelte Sicherungen|ja|Nein|Nein|nein|
|Hinzufügen von Speicher im laufenden Systembetrieb und CPU|ja|Nein|Nein|nein|
|Verschlüsselte Sicherung|ja|ja|Nein|nein|
|Hybridsicherung in Windows Azure (Sicherung über URL)|ja|ja|Nein|nein|
  
<sup>1</sup> auf Enterprise Edition verwendet wird, wird die Anzahl der Knoten das maximum des Betriebssystems. Bei der Standard Edition werden nur zwei Knoten unterstützt. 

<sup>2</sup> auf Enterprise Edition bietet Unterstützung für bis zu 8 sekundäre Replikate - einschließlich 2 synchronen sekundären Replikaten. 

<sup>3</sup> standard Edition unterstützt die Basis-Verfügbarkeitsgruppen. Eine Basis-Verfügbarkeitsgruppe unterstützt zwei Replikate mit einer Datenbank. Weitere Informationen über Basis-Verfügbarkeitsgruppen finden Sie unter [Basis-Verfügbarkeitsgruppen](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).    

##  <a name="RDBMSSP"></a> RDBMS: Skalierbarkeit und Leistung  
  
|Funktion|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------| 
|Columnstore <sup>1</sup>|ja|ja|ja|ja|  
|Große Objektbinärdateien in gruppierten Columnstore-Indizes|ja|ja|ja|ja|  
|Onlineneuerstellung für nicht gruppierten Columnstore-Index|ja|Nein|Nein|nein|
|In-Memory-OLTP <sup>1</sup>|ja|ja|ja|ja|
|Persistenter Hauptspeicher|ja|ja|ja|ja|
|Tabellen- und Indexpartitionierung|ja|ja|ja|ja|  
|Datenkomprimierung|ja|ja|ja|ja|
|Ressourcenkontrolle|ja|Nein|Nein|nein|  
|Parallelverarbeitung für partitionierte Tabellen|ja|Nein|Nein|nein|
|NUMA-basierter und großer Arbeitsspeicher für umfangreiche Seiten und Zuordnung von Pufferarrays|ja|Nein|Nein|nein|
|Ressourcenkontrolle für E/A-Vorgänge|ja|Nein|Nein|nein|  
|Verzögerte Dauerhaftigkeit|ja|ja|ja|ja|
|Automatische Optimierung|ja|Nein|Nein|nein|
|Adaptive Joins im Batchmodus|ja|Nein|Nein|nein|
|Feedback zur Speicherzuweisung im Batchmodus|ja|Nein|Nein|nein|
|Verschachtelte Ausführung mit Tabellenwertfunktionen mit mehreren Anweisungen|ja|ja|ja|ja|
|Verbesserungen beim massenhaften Einfügen|ja|ja|ja|ja|


<sup>1</sup> Die Größe der In-Memory OLTP-Daten und des Columnstore-Segmentcaches sind auf die Größe des Arbeitsspeichers beschränkt, die von der Edition im Bereich Kapazitätsgrenzen festgelegt wird. Den maximale Grad an Parallelität ist beschränkt. Der Grad der prozessparallelität (DOP) für einen Index Buildvorgang ist auf 2 DOP für die Standard Edition und 1 DOP für die Web und Express-Editionen beschränkt. Dies gilt für Columnstore-Indizes, die über datenträgerbasierte Tabellen und speicheroptimierte Tabellen erstellt wurden.

##  <a name="RDBMSS"></a> RDBMS: Sicherheit  
  
|Funktion|Enterprise|Standard|Web|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|Sicherheit auf Zeilenebene|ja|ja|ja|ja|  
|Always Encrypted|ja|ja|ja|ja| 
|Dynamische Datenmaskierung|ja|ja|ja|ja|   
|Allgemeine Überwachung|ja|ja|ja|ja| 
|Feine Überwachung|ja|ja|ja|ja| 
|Transparente Datenbankverschlüsselung|ja|Nein|Nein|nein|   
|Benutzerdefinierte Rollen|ja|ja|ja|ja| 
|Eigenständige Datenbanken|ja|ja|ja|ja| 
|Verschlüsselung von Sicherungen|ja|ja|Nein|nein|  

##  <a name="RDBMSM"></a> RDBMS: Verwaltbarkeit  
  
|Funktion|Enterprise|Standard|Web|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|Dedizierte Administratorverbindung|ja|ja|ja|Ja, mit Ablaufverfolgungsflag|Ja, mit Ablaufverfolgungsflag|   
|PowerShell-Skriptunterstützung|ja|ja|ja|ja| 
|Unterstützung für Komponentenvorgänge der Datenschichtanwendung: Extrahieren, Bereitstellen, Aktualisieren, Löschen|ja|ja|ja|ja| 
|Richtlinienautomatisierung (Überprüfung nach Zeitplan und Änderungen)|ja|ja|ja|Nein|nein|   
|Sammler von Leistungsdaten|ja|ja|ja|Nein|nein| 
|Standardleistungsberichte|ja|ja|ja|Nein|nein| 
|Planhinweislisten und Planeinfrierung für Planhinweislisten|ja|ja|ja|Nein|nein|   
|Direkte Abfrage von indizierten Sichten (mittels NOEXPAND-Hinweis)|ja|ja|ja|ja| 
|Automatische Wartung für indizierte Sichten|ja|ja|ja|Nein|nein| 
|Verteilte partitionierte Sichten|ja|Nein|Nein|nein| 
|Parallele Indexvorgänge|ja|Nein|Nein|nein|  
|Automatische Verwendung indizierter Sichten mittels Abfrageoptimierer|ja|Nein|Nein|nein| 
|Parallele Konsistenzprüfung|ja|Nein|Nein|nein| 
|SQL Server-Steuerungspunkt für das Hilfsprogramm|ja|Nein|Nein|nein|    

##  <a name="Programmability"></a> Programmability  
  
|Funktion|Enterprise|Standard|Web|Express 
|-------------|----------------|--------------|---------|------------------------|  
|JSON|ja|ja|ja|ja|   
|Abfragespeicher|ja|ja|ja|ja|   
|Temporal|ja|ja|ja|ja|   
|Systemeigene XML-Unterstützung|ja|ja|ja|ja| 
|XML-Indizierung|ja|ja|ja|ja| 
|MERGE- und UPSERT-Funktionen|ja|ja|ja|ja|   
|Datums- und Uhrzeitdatentypen|ja|ja|ja|ja|  
|Internationalisierungsunterstützung|ja|ja|ja|ja| 
|Volltextsuche und semantische Suche|ja|ja|ja|ja|nein| 
|Angabe der Sprache in einer Abfrage|ja|ja|ja|ja|nein|   
|Service Broker (Messaging)|ja|ja|Nein (nur Client)|Nein (nur Client)|Nein (nur Client)|   
|Transact-SQL-Endpunkte|ja|ja|ja|Nein|nein| 
|Diagramm|ja|ja|ja|ja|  


<sup>1</sup> Horizontale Skalierung mit mehreren Computeknoten erfordert einen Hauptknoten.

## <a name="IS"></a> Integration Services

Informationen zu Integration Services (SSIS)-Funktionen, die von den Editionen unterstützt [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], finden Sie unter [Integration Services-Funktionen, die von den Editionen von SQL Server unterstützte](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="SLS"></a> Räumliche und ortsbezogene Dienste  
  
|Funktionsname|Enterprise|Standard|Web|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Räumlichkeitsindizes|ja|ja|ja|ja|   
|Planarer und geodätischer Datentyp|ja|ja|ja|ja| 
|Erweiterte räumliche Bibliotheken|ja|ja|ja|ja|   
|Importieren/Exportieren räumlicher Industriestandard-Datenformate|ja|ja|ja|ja|   

  
## <a name="next-steps"></a>Nächste Schritte 
 [Editionen und unterstützten Funktionen für SQL Server-2017 – Windows](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [Editionen und unterstützten Funktionen für SQL Server 2016 – Windows](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [Editionen und unterstützten Funktionen für SQL Server 2014 - Windows](http://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)  
 [Installation for SQL Server (Installation für SQLServer 2016)](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 [Produktspezifikationen für SQLServer](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb) 

  
  
