---
title: "Von den SQL Server 2016-Editionen unterstützte Funktionen | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- sql edition
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
caps.latest.revision: 175
author: sabotta
ms.author: carlasab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b9b9db3ca911b8fd8eed6304b9d3a8f51e9e9ba2
ms.lasthandoff: 04/11/2017

---
# <a name="editions-and-supported-features-for-sql-server-2016"></a>Von den SQL Server 2016-Editionen unterstützte Funktionen
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Dieses Thema bietet detaillierte Informationen zu den von verschiedenen [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]-Versionen unterstützten Funktionen.  
  
 Die SQL Server Evaluation Edition steht für einen Testzeitraum von 180 Tagen zur Verfügung.  
  
 Die neuesten Versionsanmerkungen und Informationen zu Neuerungen finden Sie über die folgenden Links:
- [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
- [Neuerungen in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

    
 **Probieren Sie SQL Server 2016 aus!**    
    
 > [![Download from Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Download SQL Server 2016  from the Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure Virtual Machine small](../analysis-services/media/azure-virtual-machine-small.png) **[Spin up a Virtual Machine with SQL Server 2016 already installed](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.SQL2016SP1-WS2016?tab=Overview?wt.mc_id=sqL16_vm)**    
    
**Developer und Evaluation-Editionen**  
 Von Developer und Evaluation-Editionen unterstützte Funktionen finden Sie unter Funktionen für die SQL Server Enterprise Edition in den folgenden Tabellen.
Eine Liste der Funktionen der Developer Edition für [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 finden Sie unter [SQL Server 2016 SP1 editions (Editionen von SQL Server 2016 SP1)](https://aka.ms/uw6cw4).   
  
##  <a name="Cross-BoxScaleLimits"></a> Scale Limits  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|Maximale von einer einzelnen Instanz verwendete Rechenkapazität ( [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Maximum des Betriebssystems|Beschränkt auf weniger als 4 Sockets oder 24 Kerne|Beschränkt auf weniger als 4 Sockets oder 16 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne| 
|Maximale von einer einzelnen Instanz verwendete Rechenkapazität ( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oder [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)])|Maximum des Betriebssystems|Beschränkt auf weniger als 4 Sockets oder 24 Kerne|Beschränkt auf weniger als 4 Sockets oder 16 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne|  
|Maximaler Arbeitsspeicher für den Pufferpool pro Instanz von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Maximum des Betriebssystems|128 GB|64 GB|1410 MB|1410 MB|
|Maximaler Arbeitsspeicher für Columnstore-Segmentcache pro Instanz von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Unbegrenzter Arbeitsspeicher| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|Maximale speicheroptimierte Datengröße pro Datenbank in [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Unbegrenzter Arbeitsspeicher| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|Maximaler genutzter Arbeitsspeicher pro Instanz von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Maximum des Betriebssystems|Tabellarisch: 16 GB<br /><br /> MOLAP: 64 GB|–|–|–|  
|Maximaler genutzter Arbeitsspeicher pro Instanz von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Maximum des Betriebssystems|64 GB|64 GB|4 GB|–|
|Maximale relationale Datenbankgröße|524 PB|524 PB|524 PB|10 GB|10 GB|  
  
<sup>1</sup> Die Enterprise Edition mit einer Lizenzierung auf der Grundlage von Serverlizenz + Clientzugriffslizenz (CAL) (für neue Verträge nicht verfügbar) ist auf maximal 20 Kerne pro SQL Server-Instanz beschränkt. Für das auf Prozessorkernen basierende Serverlizenzierungsmodell gelten keine Beschränkungen. Weitere Informationen finden Sie unter [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
<sup>2</sup> Gilt für [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. 

##  <a name="RDBMSHA"></a> RDBMS High Availability  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Server Core-Unterstützung <sup>1</sup>|ja|ja|ja|ja|ja|  
|Protokollversand|ja|ja|ja|Nein|Nein|  
|Datenbankspiegelung|ja|ja<br /><br /> Nur vollständige Sicherheit|Nur WITNESS|Nur WITNESS|Nur WITNESS| 
|Sicherungskomprimierung|ja|ja|Nein|Nein|Nein| 
|Datenbankmomentaufnahme|ja|Ja <sup>3</sup>|Ja <sup>3</sup>|Ja <sup>3</sup>|Ja <sup>3</sup>|
|AlwaysOn-Failoverclusterinstanzen|ja<br /><br /> Anzahl der Knoten ist das Maximum des Betriebssystems|ja<br /><br /> Unterstützung für 2 Knoten|Nein|Nein|Nein|  
|AlwaysOn-Verfügbarkeitsgruppen|ja<br /><br /> Bis zu 8 sekundäre Replikate, einschließlich 2 synchronen sekundären Replikaten|Nein|Nein|Nein|Nein|
|Basis-Verfügbarkeitsgruppen <sup>2</sup>|Nein|ja<br /><br /> Unterstützung für 2 Knoten|Nein|Nein|Nein|
|Onlineseiten- und Onlinedateiwiederherstellung|ja|Nein|Nein|Nein|Nein|
|Online-Indizierung|ja|Nein|Nein|Nein|Nein|
|Onlineschemaänderung|ja|Nein|Nein|Nein|Nein|
|Schnelle Wiederherstellung|ja|Nein|Nein|Nein|Nein|
|Gespiegelte Sicherungen|ja|Nein|Nein|Nein|Nein|
|Hinzufügen von Speicher im laufenden Systembetrieb und CPU|ja|Nein|Nein|Nein|Nein|
|Datenbankwiederherstellungsberater|ja|ja|ja|ja|ja|
|Verschlüsselte Sicherung|ja|ja|Nein|Nein|Nein|
|Hybridsicherung in Windows Azure (Sicherung über URL)|ja|ja|Nein|Nein|Nein|  
  
 <sup>1</sup> Weitere Informationen zum Installieren von SQL Server 2016 unter Server Core finden Sie unter [Installieren von SQL Server 2016 unter Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md). 

<sup>2</sup> Weitere Informationen über Basis-Verfügbarkeitsgruppen finden Sie unter [Basis-Verfügbarkeitsgruppen](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).  

<sup>3</sup> Gilt für [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.
  
##  <a name="RDBMSSP"></a> RDBMS Scalability and Performance  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Columnstore <sup>1</sup>|ja|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja<sup>2</sup>|Ja<sup>2</sup>|  
|In-Memory-OLTP <sup>1</sup>|ja|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>, <sup>3</sup>|Ja <sup>2</sup>|
|Stretch-Datenbank|ja|ja|ja|ja|ja|
|Persistenter Hauptspeicher|ja|ja|ja|ja|ja|
|Unterstützung mehrerer Instanzen|50|50|50|50|50|
|Tabellen- und Indexpartitionierung|ja|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>|  
|Datenkomprimierung|ja|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>|
|Resource Governor|ja|Nein|Nein|Nein|Nein|  
|Parallelverarbeitung für partitionierte Tabellen|ja|Nein|Nein|Nein|Nein|
|Mehrere FILESTREAM-Container|ja|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>|
|NUMA-basierter und großer Arbeitsspeicher für umfangreiche Seiten und Zuordnung von Pufferarrays|ja|Nein|Nein|Nein|Nein|
|Pufferpoolerweiterung|ja|ja|Nein|Nein|Nein|
|Ressourcenkontrolle für E/A-Vorgänge|ja|Nein|Nein|Nein|Nein|  
|Verzögerte Dauerhaftigkeit|ja|ja|ja|ja|ja|

<sup>1</sup> Die Größe der In-Memory OLTP-Daten und des Columnstore-Segmentcaches sind auf die Größe des Arbeitsspeichers beschränkt, die von der Edition im Bereich Kapazitätsgrenzen festgelegt wird. Den maximale Grad an Parallelität ist beschränkt. Der Grad an Prozessparallelität (Degree of Parallelism, DOP) für eine Indexerstellung ist auf 2 DOP für die Standard Edition und auf 1 DOP für die Web und die Express Edition beschränkt. Dies gilt für Columnstore-Indizes, die über datenträgerbasierte Tabellen und speicheroptimierte Tabellen erstellt wurden.

<sup>2</sup> Gilt für [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. 

<sup>3</sup> Dieses Feature ist in der LocalDB-Installationsoption nicht enthalten.
##  <a name="RDBMSS"></a> RDBMS Security  
  
|Funktion|Enterprise|Standard|Web|Express|Express mit Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|Sicherheit auf Zeilenebene|ja|ja|Ja <sup>1</sup>|Ja <sup>1</sup>|Ja <sup>1</sup>|  
|Always Encrypted|ja|Ja <sup>1</sup>|Ja <sup>1</sup>|Ja <sup>1</sup>|Ja <sup>1</sup>| 
|Dynamische Datenmaskierung|ja|ja|Ja <sup>1</sup>|Ja <sup>1</sup>|Ja <sup>1</sup>|   
|Allgemeine Überwachung|ja|ja|ja|ja|ja| 
|Feine Überwachung|ja|Ja <sup>1</sup>|Ja <sup>1</sup>|Ja <sup>1</sup>|Ja <sup>1</sup>| 
|Transparente Datenbankverschlüsselung|ja|Nein|Nein|Nein|Nein|   
|Erweiterbare Schlüsselverwaltung|ja|Nein|Nein|Nein|Nein| 
|Benutzerdefinierte Rollen|ja|ja|ja|ja|ja| 
|Eigenständige Datenbanken|ja|ja|ja|ja|ja| 
|Verschlüsselung von Sicherungen|ja|ja|Nein|Nein|Nein|  

<sup>1</sup> Gilt für [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.  
##  <a name="Replication"></a> Replication  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Heterogene Abonnenten|ja|ja|Nein|Nein|Nein|  
|Mergereplikation|ja|ja|Ja (Nur Abonnent)|Ja (Nur Abonnent)|Ja (Nur Abonnent)|   
|Veröffentlichungen mit Oracle|ja|Nein|Nein|Nein|Nein| 
|Peer-zu-Peer-Transaktionsreplikation|ja|Nein|Nein|Nein|Nein|   
|Momentaufnahmereplikation|ja|ja|Ja (Nur Abonnent)|Ja (Nur Abonnent)|Ja (Nur Abonnent)|   
|SQL Server-Änderungsnachverfolgung|ja|ja|ja|ja|ja| 
|Transaktionsreplikation|ja|ja|Ja (Nur Abonnent)|Ja (Nur Abonnent)|Ja (Nur Abonnent)|   
|Transaktionsreplikation zu Azure|ja|ja|Nein|Nein|Nein|   
|Aktualisierbares Abonnement für Transaktionsreplikation|ja|Nein|Nein|Nein|Nein|  
  
##  <a name="SSMS"></a> Management Tools  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Management Objects (SMO)|ja|ja|ja|ja|ja|  
|SQL-Konfigurations-Manager|ja|ja|ja|ja|ja|   
|SQL CMD (Command Prompt Tool – Eingabeaufforderungstool)|ja|ja|ja|ja|ja|      
|Distributed Replay – Administratortool|ja|ja|ja|ja|Nein|  
|Distributed Replay – Client|ja|ja|ja|Nein|Nein|  
|Distributed Replay - Controller|Ja (bis zu 16 Clients)|Ja (1 Client)|Ja (1 Client)|Nein|Nein|   
|SQL Profiler|ja|ja|Nein <sup>1</sup>|Nein <sup>1</sup>|Nein <sup>1</sup>|  
|SQL Server-Agent|ja|ja|ja|Nein|Nein| 
|Microsoft System Center Operations Manager Management Pack|ja|ja|ja|Nein|Nein|  
|Datenbankoptimierungsratgeber (DTA)|ja|Ja <sup>2</sup>|Ja <sup>2</sup>|Nein|Nein|      
  
 <sup>1</sup> SQL Server Web, SQL Server Express, SQL Server Express mit Tools und SQL Server Express mit Advanced Services können mit der SQL Server Standard- und SQL Server Enterprise-Edition profiliert werden.  
  
 <sup>2</sup> Optimierung ist nur in Funktionen der Standard Edition aktiviert.  
  
##  <a name="RDBMSM"></a> RDBMS Manageability  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Benutzerinstanzen|Nein|Nein|Nein|ja|ja| 
|LocalDB|Nein|Nein|Nein|Ja|Nein| 
|Dedizierte Administratorverbindung|ja|ja|ja|Ja, mit Ablaufverfolgungsflag|Ja, mit Ablaufverfolgungsflag|   
|PowerShell-Skriptunterstützung|ja|ja|ja|ja|ja| 
|SysPrep-Unterstützung <sup>1</sup>|ja|ja|ja|ja|ja| 
|Unterstützung für Komponentenvorgänge der Datenschichtanwendung – Extrahieren, Bereitstellen, Aktualisieren, Löschen|ja|ja|ja|ja|ja| 
|Richtlinienautomatisierung (Überprüfung nach Zeitplan und Änderungen)|ja|ja|ja|Nein|Nein|   
|Sammler von Leistungsdaten|ja|ja|ja|Nein|Nein| 
|Fähigkeit zur Registrierung als verwaltete Instanz in einer Mehrfachinstanzverwaltung|ja|ja|ja|Nein|Nein|   
|Standardleistungsberichte|ja|ja|ja|Nein|Nein| 
|Planhinweislisten und Planeinfrierung für Planhinweislisten|ja|ja|ja|Nein|Nein|   
|Direkte Abfrage von indizierten Sichten (mittels NOEXPAND-Hinweis)|ja|ja|ja|ja|ja| 
|Automatische Wartung für indizierte Sichten|ja|ja|ja|Nein|Nein| 
|Verteilte partitionierte Sichten|ja|Nein|Nein|Nein|Nein| 
|Parallele Indexvorgänge|ja|Nein|Nein|Nein|Nein|  
|Automatische Verwendung indizierter Sichten mittels Abfrageoptimierer|ja|Nein|Nein|Nein|Nein| 
|Parallele Konsistenzprüfung|ja|Nein|Nein|Nein|Nein| 
|SQL Server-Steuerungspunkt für das Hilfsprogramm|ja|Nein|Nein|Nein|Nein|    
|Pufferpoolerweiterung|ja|ja|Nein|Nein|Nein| 
  
 <sup>1</sup> Weitere Informationen finden Sie unter [Überlegungen zur Installation von SQL Server mit SysPrep](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
 
<sup>2</sup> Gilt für [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1. 
  
##  <a name="DevTools"></a> Development Tools  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Integration in Microsoft Visual Studio|ja|ja|ja|ja|ja| 
|IntelliSense (Transact-SQL und MDX)|ja|ja|ja|ja|ja| 
|SQL Server Data Tools (SSDT)|ja|ja|ja|ja|Nein|    
|MDX-Bearbeitungs-, MDX-Debug- und MDX-Entwurfstools|ja|ja|Nein|Nein|Nein|   
  
##  <a name="Programmability"></a> Programmability  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Grundlegende Integration von R|ja|ja|ja|ja|Nein|   
|Erweiterte Integration von R|ja|Nein|Nein|Nein|Nein| 
|R-Server (eigenständig)|ja|Nein|Nein|Nein|Nein|   
|PolyBase-Computeknoten|ja|Ja <sup>1</sup>|Ja <sup>1</sup>, <sup>2</sup>|Ja <sup>1</sup>, <sup>2</sup>|Ja <sup>1</sup>, <sup>2</sup>| 
|PolyBase-Hauptknoten|ja|Nein|Nein|Nein|Nein| 
|JSON|ja|ja|ja|ja|ja|   
|Abfragespeicher|ja|ja|ja|ja|ja|   
|Temporal|ja|ja|ja|ja|ja|   
|Common Language Runtime (CLR)-Integration|ja|ja|ja|ja|ja|   
|Systemeigene XML-Unterstützung|ja|ja|ja|ja|ja| 
|XML-Indizierung|ja|ja|ja|ja|ja| 
|MERGE & UPSERT-Funktionen|ja|ja|ja|ja|ja|   
|FILESTREAM-Unterstützung|ja|ja|ja|ja|ja| 
|FileTable|ja|ja|ja|ja|ja| 
|Datums- und Uhrzeitdatentypen|ja|ja|ja|ja|ja|  
|Internationalisierungsunterstützung|ja|ja|ja|ja|ja| 
|Volltextsuche und semantische Suche|ja|ja|ja|ja|Nein| 
|Angabe der Sprache in einer Abfrage|ja|ja|ja|ja|Nein|   
|Service Broker (Messaging)|ja|ja|Nein (nur Client)|Nein (nur Client)|Nein (nur Client)|   
|Transact-SQL-Endpunkte|ja|ja|ja|Nein|Nein| 

<sup>1</sup> Horizontale Skalierung mit mehreren Computeknoten erfordert einen Hauptknoten.

<sup>2</sup> Gilt für [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.
  
## <a name="IS"></a> Integration Services

Informationen über die Features von Integration Services (SSIS), die von den einzelnen Editionen von [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] unterstützt werden, finden Sie unter [Von den SQL Server-Editionen unterstützte Integration Services-Funktionen](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="MDS"></a> Master Data Services  
 Informationen über die [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] - und Data Quality Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Master Data Services- und Data Quality Services-Features](../master-data-services/master-data-services-and-data-quality-services-features-support.md). 

  
##  <a name="DW"></a> Data Warehouse  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Erstellen von Cubes ohne Datenbank|ja|ja|Nein|Nein|Nein |   
|Automatisches Generieren von Staging- und Data Warehouse-Schemas|ja|ja|Nein|Nein|Nein| 
|Change Data Capture|ja|Ja <sup>1</sup>|Nein|Nein|Nein| 
|Optimierung von Sternjoin-Abfragen|ja|Nein|Nein|Nein|Nein| 
|Skalierbare schreibgeschützte Analysis Services-Konfiguration|ja|Nein|Nein|Nein|Nein| 
|Parallele Abfrageverarbeitung bei partitionierten Tabellen und Indizes|ja|Nein|Nein|Nein|Nein|   
|Globale Batchaggregation|ja|Nein|Nein|Nein|Nein| 

<sup>1</sup> Gilt für [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] SP1.  
##  <a name="SSAS"></a> Analysis Services  
  
Informationen über die Analysis Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Analysis Services-Features](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md). 
  
##  <a name="BIMD"></a> BI Semantic Model (Multi Dimensional)  
  
Informationen über die Analysis Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Analysis Services-Features](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
   
##  <a name="BIT"></a> BI Semantic Model (Tabular)  
  
Informationen über die Analysis Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Analysis Services-Features](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="PPSP"></a> Power Pivot for SharePoint  
  
Informationen über die Power Pivot for SharePoint-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Analysis Services-Features](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="DM"></a> Data Mining  
  
Informationen über die Data Mining-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Analysis Services-Features](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="SSRS"></a> Reporting Services  
  
Informationen über die Reporting Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Reporting Services-Features](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).

##  <a name="BIC"></a> Business Intelligence Clients  

Informationen über die Business Intelligence-Clientfeatures, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Analysis Services Features](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) oder [Von den Editionen von SQL Server 2016 unterstützte Reporting Services Features](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="SLS"></a> Spatial and Location Services  
  
|Funktionsname|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Räumlichkeitsindizes|ja|ja|ja|ja|ja|   
|Planarer und geodätischer Datentyp|ja|ja|ja|ja|ja| 
|Erweiterte räumliche Bibliotheken|ja|ja|ja|ja|ja|   
|Importieren/Exportieren räumlicher Industriestandard-Datenformate|ja|ja|ja|ja|ja|   
  
##  <a name="ADS"></a> Additional Database Services  
  
|Funktionsname|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|ja|ja|ja|ja|ja|   
|Datenbank-E-Mail|ja|ja|ja|Nein|Nein| 
  
##  <a name="Other"></a> Other Components  
  
|Funktionsname|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium-Edition|StreamInsight Standard-Edition|StreamInsight Standard-Edition|Nein|Nein| 
|StreamInsight HA|StreamInsight Premium-Edition|Nein|Nein|Nein|Nein|   
  
> [![Herunterladen von SSMS](../analysis-services/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx) Laden Sie die neueste Version von **[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) herunter.**    
  
## <a name="see-also"></a>Siehe auch  
 [Produktspezifikationen für SQL Server 2016](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [Installation für SQLServer 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)  
  
  

