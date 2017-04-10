---
title: "Von den SQL Server 2016-Editionen unterst&#252;tzte Funktionen | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
keywords: 
  - "sql edition"
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
caps.latest.revision: 175
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
---
# Von den SQL Server 2016-Editionen unterst&#252;tzte Funktionen
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Dieses Thema bietet detaillierte Informationen zu den von verschiedenen [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]-Versionen unterstützten Funktionen.  
  
 Die SQL Server Evaluation Edition steht für einen Testzeitraum von 180 Tagen zur Verfügung.  
  
 Die neuesten Versionsanmerkungen und Informationen zu Neuerungen finden Sie über die folgenden Links:
- [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
- [Neuerungen in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

    
 **Probieren Sie SQL Server 2016 aus!**    
    
 > [![Download aus dem Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Virtueller Azure-Computer (klein)](../analysis-services/media/azure-virtual-machine-small.png) **[Starten eines virtuellen Computers, auf dem SQL Server 2016 bereits installiert ist](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    
    
  
 Informationen über Funktionen, die von den Evaluation- und Developer-Editionen unterstützt werden, finden Sie unter „SQL Server Enterprise Edition“.  
  
##  <a name="a-namecross-boxscalelimitsa-scale-limits"></a><a name="Cross-BoxScaleLimits"></a> Kapazitätsgrenzen  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|Maximale von einer einzelnen Instanz verwendete Rechenkapazität ([!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>)|Maximum des Betriebssystems|Beschränkt auf weniger als 4 Sockets oder 24 Kerne|Beschränkt auf weniger als 4 Sockets oder 16 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne| 
|Maximale von einer einzelnen Instanz verwendete Rechenkapazität ([!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oder [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)])|Maximum des Betriebssystems|Beschränkt auf weniger als 4 Sockets oder 24 Kerne|Beschränkt auf weniger als 4 Sockets oder 16 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne|  
|Maximaler Arbeitsspeicher für den Pufferpool pro Instanz von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Maximum des Betriebssystems|128 GB|64 GB|1410 MB|1410 MB|
|Maximaler Arbeitsspeicher für Columnstore-Segmentcache pro Instanz von [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Unbegrenzter Arbeitsspeicher| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|Maximale speicheroptimierte Datengröße pro Datenbank in [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Unbegrenzter Arbeitsspeicher| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|Maximaler genutzter Arbeitsspeicher pro Instanz von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Maximum des Betriebssystems|Tabellarisch: 16 GB<br /><br /> MOLAP: 64 GB|–|–|–|  
|Maximaler genutzter Arbeitsspeicher pro Instanz von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Maximum des Betriebssystems|64 GB|64 GB|4 GB|Nicht zutreffend|
|Maximale relationale Datenbankgröße|524 PB|524 PB|524 PB|10 GB|10 GB|  
  
 1. Die Enterprise Edition mit einer Lizenzierung auf der Grundlage von Serverlizenz + Clientzugriffslizenz (CAL) (für neue Verträge nicht verfügbar) ist auf maximal 20 Kerne pro SQL Server-Instanz beschränkt. Für das auf Prozessorkernen basierende Serverlizenzierungsmodell gelten keine Beschränkungen. Weitere Informationen finden Sie unter [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
<sup>2</sup> Gilt für [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. 

##  <a name="a-namerdbmshaa-rdbms-high-availability"></a><a name="RDBMSHA"></a> RDBMS – Hohe Verfügbarkeit  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Server Core-Unterstützung <sup>1</sup>|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|  
|Protokollversand|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein|  
|Datenbankspiegelung|ja|ja<br /><br /> Nur vollständige Sicherheit|Nur WITNESS|Nur WITNESS|Nur WITNESS| 
|Sicherungskomprimierung|ja|Benutzerkontensteuerung|Nein|Nein|Nein| 
|Datenbankmomentaufnahme|ja|Ja <sup>3</sup>|Ja <sup>3</sup>|Ja <sup>3</sup>|Ja <sup>3</sup>|
|AlwaysOn-Failoverclusterinstanzen|ja<br /><br /> Anzahl der Knoten ist das Maximum des Betriebssystems|ja<br /><br /> Unterstützung für 2 Knoten|Nein|Nein|Nein|  
|AlwaysOn-Verfügbarkeitsgruppen|ja<br /><br /> Bis zu 8 sekundäre Replikate, einschließlich 2 synchronen sekundären Replikaten|Nein|Nein|Nein|Nein|
|Basis-Verfügbarkeitsgruppen <sup>2</sup>|Nein|Ja<br /><br /> Unterstützung für 2 Knoten|Nein|Nein|Nein|
|Connection Director|ja|Nein|Nein|Nein|Nein|
|Onlineseiten- und Onlinedateiwiederherstellung|ja|Nein|Nein|Nein|Nein|
|Online-Indizierung|ja|Nein|Nein|Nein|Nein|
|Onlineschemaänderung|Ja|Nein|Nein|Nein|Nein|
|Schnelle Wiederherstellung|ja|Nein|Nein|Nein|Nein|
|Gespiegelte Sicherungen|ja|Nein|Nein|Nein|Nein|
|Hinzufügen von Speicher im laufenden Systembetrieb und CPU|Ja|Nein|Nein|Nein|Nein|
|Datenbankwiederherstellungsberater|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|
|Verschlüsselte Sicherung|ja|Benutzerkontensteuerung|Nein|Nein|Nein|
|Hybridsicherung in Windows Azure (Sicherung über URL)|Ja|Benutzerkontensteuerung|Nein|Nein|Nein|  
  
 <sup>1</sup> Weitere Informationen zum Installieren von SQL Server 2016 unter Server Core finden Sie unter [Installieren von SQL Server 2016 unter Server Core](../database-engine/install-windows/install-sql-server-2016-on-server-core.md). 

<sup>2</sup> Weitere Informationen über Basis-Verfügbarkeitsgruppen finden Sie unter [Basis-Verfügbarkeitsgruppen](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).  

<sup>3</sup> Gilt für [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.
  
##  <a name="a-namerdbmsspa-rdbms-scalability-and-performance"></a><a name="RDBMSSP"></a> RDBMS – Skalierbarkeit und Leistung  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Columnstore <sup>1</sup>|Ja|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja<sup>2</sup>|Ja<sup>2</sup>|  
|In-Memory-OLTP <sup>1</sup>|Ja|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>, <sup>3</sup>|Ja <sup>2</sup>|
|Stretch-Datenbank|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|
|Persistenter Hauptspeicher|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Ja|
|Unterstützung mehrerer Instanzen|50|50|50|50|50|
|Tabellen- und Indexpartitionierung|ja|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>|  
|Datenkomprimierung|ja|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>|
|Resource Governor|Ja|Nein|Nein|Nein|Nein|  
|Parallelverarbeitung für partitionierte Tabellen|Ja|Nein|Nein|Nein|Nein|
|Mehrere FILESTREAM-Container|ja|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>|Ja <sup>2</sup>|
|NUMA-basierter und großer Arbeitsspeicher für umfangreiche Seiten und Zuordnung von Pufferarrays|Ja|Nein|Nein|Nein|Nein|
|Pufferpoolerweiterung|ja|Benutzerkontensteuerung|Nein|Nein|Nein|
|Ressourcenkontrolle für E/A-Vorgänge|ja|Nein|Nein|Nein|Nein|  
|Verzögerte Dauerhaftigkeit|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Ja|

<sup>1</sup> Die Größe der In-Memory OLTP-Daten und des Columnstore-Segmentcaches sind auf die Größe des Arbeitsspeichers beschränkt, die von der Edition im Bereich Kapazitätsgrenzen festgelegt wird. Den maximale Grad an Parallelität ist beschränkt. Der Grad an Prozessparallelität (Degree of Parallelism, DOP) für eine Indexerstellung ist auf 2 DOP für die Standard Edition und auf 1 DOP für die Web und die Express Edition beschränkt. Dies gilt für Columnstore-Indizes, die über datenträgerbasierte Tabellen und speicheroptimierte Tabellen erstellt wurden.

<sup>2</sup> Gilt für [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. 

<sup>3</sup> Dieses Feature ist in der LocalDB-Installationsoption nicht enthalten.
##  <a name="a-namerdbmssa-rdbms-security"></a><a name="RDBMSS"></a> RDBMS – Sicherheit  
  
|Funktion|Enterprise|Standard|Web|Express|Express mit Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|Sicherheit auf Zeilenebene|ja|ja|Ja <sup>1</sup>|Ja <sup>1</sup>|Ja <sup>1</sup>|  
|Always Encrypted|Ja|Ja <sup>1</sup>|Ja <sup>1</sup>|Ja <sup>1</sup>|Ja <sup>1</sup>| 
|Dynamische Datenmaskierung|ja|ja|Ja <sup>1</sup>|Ja <sup>1</sup>|Ja <sup>1</sup>|   
|Allgemeine Überwachung|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|Feine Überwachung|ja|Ja <sup>1</sup>|Ja <sup>1</sup>|Ja <sup>1</sup>|Ja <sup>1</sup>| 
|Transparente Datenbankverschlüsselung|Ja|Nein|Nein|Nein|Nein|   
|Erweiterbare Schlüsselverwaltung|ja|Nein|Nein|Nein|Nein| 
|Benutzerdefinierte Rollen|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|Eigenständige Datenbanken|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|Verschlüsselung von Sicherungen|ja|Benutzerkontensteuerung|Nein|Nein|Nein|  

<sup>1</sup> Gilt für [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.  
##  <a name="a-namereplicationa-replication"></a><a name="Replication"></a> Replikation  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Heterogene Abonnenten|ja|Benutzerkontensteuerung|Nein|Nein|Nein|  
|Mergereplikation|ja|ja|Ja (Nur Abonnent)|Ja (Nur Abonnent)|Ja (Nur Abonnent)|   
|Veröffentlichungen mit Oracle|Ja|Nein|Nein|Nein|Nein| 
|Peer-zu-Peer-Transaktionsreplikation|Ja|Nein|Nein|Nein|Nein|   
|Momentaufnahmereplikation|ja|ja|Ja (Nur Abonnent)|Ja (Nur Abonnent)|Ja (Nur Abonnent)|   
|SQL Server-Änderungsnachverfolgung|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|Transaktionsreplikation|ja|ja|Ja (Nur Abonnent)|Ja (Nur Abonnent)|Ja (Nur Abonnent)|   
|Transaktionsreplikation zu Azure|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein|   
|Aktualisierbares Abonnement für Transaktionsreplikation|Ja|Nein|Nein|Nein|Nein|  
  
##  <a name="a-namessmsa-management-tools"></a><a name="SSMS"></a> Verwaltungstools  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Management Objects (SMO)|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|  
|SQL-Konfigurations-Manager|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|   
|SQL CMD (Command Prompt Tool – Eingabeaufforderungstool)|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Ja|      
|Distributed Replay – Administratortool|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|  
|Distributed Replay – Client|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein|  
|Distributed Replay - Controller|Ja (bis zu 16 Clients)|Ja (1 Client)|Ja (1 Client)|Nein|Nein|   
|SQL Profiler|ja|Ja|Nein <sup>1</sup>|Nein <sup>1</sup>|Nein <sup>1</sup>|  
|SQL Server-Agent|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein| 
|Microsoft System Center Operations Manager Management Pack|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein|  
|Datenbankoptimierungsratgeber (DTA)|Ja|Ja <sup>2</sup>|Ja <sup>2</sup>|Nein|Nein|      
  
 <sup>1</sup> SQL Server Web, SQL Server Express, SQL Server Express mit Tools und SQL Server Express mit Advanced Services können mit der SQL Server Standard- und SQL Server Enterprise-Edition profiliert werden.  
  
 <sup>2</sup> Optimierung ist nur in Funktionen der Standard Edition aktiviert.  
  
##  <a name="a-namerdbmsma-rdbms-manageability"></a><a name="RDBMSM"></a> RDBMS-Verwaltbarkeit  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Benutzerinstanzen|Nein|Nein|Nein|Benutzerkontensteuerung|ja| 
|LocalDB|Nein|Nein|Nein|Ja|Nein| 
|Dedizierte Administratorverbindung|ja|Benutzerkontensteuerung|ja|Ja, mit Ablaufverfolgungsflag|Ja, mit Ablaufverfolgungsflag|   
|PowerShell-Skriptunterstützung|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|SysPrep-Unterstützung <sup>1</sup>|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Ja| 
|Unterstützung für Komponentenvorgänge der Datenschichtanwendung – Extrahieren, Bereitstellen, Aktualisieren, Löschen|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|Richtlinienautomatisierung (Überprüfung nach Zeitplan und Änderungen)|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein|   
|Sammler von Leistungsdaten|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein| 
|Fähigkeit zur Registrierung als verwaltete Instanz in einer Mehrfachinstanzverwaltung|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein|   
|Standardleistungsberichte|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein| 
|Planhinweislisten und Planeinfrierung für Planhinweislisten|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein|   
|Direkte Abfrage von indizierten Sichten (mittels NOEXPAND-Hinweis)|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|Automatische Wartung für indizierte Sichten|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein| 
|Verteilte partitionierte Sichten|Ja|Nein|Nein|Nein|Nein| 
|Parallele Indexvorgänge|ja|Nein|Nein|Nein|Nein|  
|Automatische Verwendung indizierter Sichten mittels Abfrageoptimierer|Ja|Nein|Nein|Nein|Nein| 
|Parallele Konsistenzprüfung|Ja|Nein|Nein|Nein|Nein| 
|SQL Server-Steuerungspunkt für das Hilfsprogramm|Ja|Nein|Nein|Nein|Nein|    
|Pufferpoolerweiterung|ja|Benutzerkontensteuerung|Nein|Nein|Nein| 
  
 <sup>1</sup> Weitere Informationen finden Sie unter [Überlegungen zur Installation von SQL Server mit SysPrep](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
 
<sup>2</sup> Gilt für [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1. 
  
##  <a name="a-namedevtoolsa-development-tools"></a><a name="DevTools"></a> Entwicklungstools  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Integration in Microsoft Visual Studio|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Ja| 
|IntelliSense (Transact-SQL und MDX)|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Ja| 
|SQL Server Data Tools (SSDT)|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|    
|MDX-Bearbeitungs-, MDX-Debug- und MDX-Entwurfstools|ja|Benutzerkontensteuerung|Nein|Nein|Nein|   
  
##  <a name="a-nameprogrammabilitya-programmability"></a><a name="Programmability"></a> Programmierbarkeit  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Grundlegende Integration von R|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|   
|Erweiterte Integration von R|ja|Nein|Nein|Nein|Nein| 
|R-Server (eigenständig)|Ja|Nein|Nein|Nein|Nein|   
|PolyBase-Computeknoten|Ja|Ja <sup>1</sup>|Ja <sup>1</sup>, <sup>2</sup>|Ja <sup>1</sup>, <sup>2</sup>|Ja <sup>1</sup>, <sup>2</sup>| 
|PolyBase-Hauptknoten|ja|Nein|Nein|Nein|Nein| 
|JSON|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|   
|Abfragespeicher|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|   
|Temporal|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Ja|   
|Common Language Runtime (CLR)-Integration|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|   
|Systemeigene XML-Unterstützung|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|XML-Indizierung|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|MERGE & UPSERT-Funktionen|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|   
|FILESTREAM-Unterstützung|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|FileTable|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|Datums- und Uhrzeitdatentypen|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|  
|Internationalisierungsunterstützung|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|Volltextsuche und semantische Suche|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein| 
|Angabe der Sprache in einer Abfrage|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|   
|Service Broker (Messaging)|ja|ja|Nein (nur Client)|Nein (nur Client)|Nein (nur Client)|   
|Transact-SQL-Endpunkte|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein| 

<sup>1</sup> Horizontale Skalierung mit mehreren Computeknoten erfordert einen Hauptknoten.

<sup>2</sup> Gilt für [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.
  
## <a name="a-nameisa-integration-services"></a><a name="IS"></a> Integration Services

Informationen über die Features von Integration Services (SSIS), die von den einzelnen Editionen von [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Integration Services-Funktionen](Integration%20Services%20Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).

##  <a name="a-namemdsa-master-data-services"></a><a name="MDS"></a> Master Data Services  
 Informationen über die [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]- und Data Quality Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Master Data Services- und Data Quality Services-Features](../master-data-services/master data services and data quality services features support.md). 

  
##  <a name="a-namedwa-data-warehouse"></a><a name="DW"></a> Data Warehouse  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Erstellen von Cubes ohne Datenbank|ja|Benutzerkontensteuerung|Nein|Nein|Nein |   
|Automatisches Generieren von Staging- und Data Warehouse-Schemas|ja|Benutzerkontensteuerung|Nein|Nein|Nein| 
|Change Data Capture|ja|Ja <sup>1</sup>|Ja <sup>1</sup>|Nein|Nein| 
|Optimierung von Sternjoin-Abfragen|ja|Nein|Nein|Nein|Nein| 
|Skalierbare schreibgeschützte Analysis Services-Konfiguration|Ja|Nein|Nein|Nein|Nein| 
|Parallele Abfrageverarbeitung bei partitionierten Tabellen und Indizes|Ja|Nein|Nein|Nein|Nein|   
|Globale Batchaggregation|ja|Nein|Nein|Nein|Nein| 

<sup>1</sup> Gilt für [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] SP1.  
##  <a name="a-namessasa-analysis-services"></a><a name="SSAS"></a> Analysis Services  
  
Informationen über die Analysis Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Analysis Services-Features](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md). 
  
##  <a name="a-namebimda-bi-semantic-model-multi-dimensional"></a><a name="BIMD"></a> BI-Semantikmodell (mehrdimensional)  
  
Informationen über die Analysis Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Analysis Services-Features](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
   
##  <a name="a-namebita-bi-semantic-model-tabular"></a><a name="BIT"></a> BI-Semantikmodell (tabellarisch)  
  
Informationen über die Analysis Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Analysis Services-Features](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="a-nameppspa-power-pivot-for-sharepoint"></a><a name="PPSP"></a> PowerPivot für SharePoint  
  
Informationen über die Power Pivot for SharePoint-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Analysis Services-Features](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="a-namedma-data-mining"></a><a name="DM"></a> Data Mining  
  
Informationen über die Data Mining-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Analysis Services-Features](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="a-namessrsa-reporting-services"></a><a name="SSRS"></a> Reporting Services  
  
Informationen über die Reporting Services-Features, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Reporting Services-Features](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).

##  <a name="a-namebica-business-intelligence-clients"></a><a name="BIC"></a> Business Intelligence-Clients  

Informationen über die Business Intelligence-Clientfeatures, die von den einzelnen Editionen von [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] unterstützt werden, finden Sie unter [Von den Editionen von SQL Server 2016 unterstützte Analysis Services Features](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) oder [Von den Editionen von SQL Server 2016 unterstützte Reporting Services Features](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="a-nameslsa-spatial-and-location-services"></a><a name="SLS"></a> Räumliche und ortsbezogene Dienste  
  
|Funktionsname|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Räumlichkeitsindizes|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|   
|Planarer und geodätischer Datentyp|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja| 
|Erweiterte räumliche Bibliotheken|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|   
|Importieren/Exportieren räumlicher Industriestandard-Datenformate|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Ja|   
  
##  <a name="a-nameadsa-additional-database-services"></a><a name="ADS"></a> Weitere Datenbankdienste  
  
|Funktionsname|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|ja|   
|Datenbank-E-Mail|ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Nein|Nein| 
  
##  <a name="a-nameothera-other-components"></a><a name="Other"></a> Andere Komponenten  
  
|Funktionsname|Enterprise|Standard|Web|Express mit Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium-Edition|StreamInsight Standard-Edition|StreamInsight Standard-Edition|Nein|Nein| 
|StreamInsight HA|StreamInsight Premium-Edition|Nein|Nein|Nein|Nein|   
  
> [![Herunterladen von SSMS](../analysis-services/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx) Laden Sie die neueste Version von **[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) herunter.**    
  
## <a name="see-also"></a>Siehe auch  
 [Produktspezifikationen für SQL Server 2016](../Topic/Product%20Specifications%20for%20SQL%20Server%202016.md)   
 [Installation für SQLServer 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)  
  
  