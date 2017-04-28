---
title: Erweiterte Ereignisse | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- extended events [SQL Server]
- xe
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
caps.latest.revision: 48
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e067f99cb78b96c4a20938b3fb60842bd91b2931
ms.lasthandoff: 04/11/2017

---
# <a name="extended-events"></a>Erweiterte Ereignisse
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

Die Funktion Erweiterte Ereignisse von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] besitzt eine sehr stark skalierbare und konfigurierbare Architektur, mit der Benutzer je nach Bedarf eine entsprechende Menge an Informationen sammeln können, die zum Beheben oder Identifizieren eines Leistungsproblems notwendig ist.  

Weitere Informationen zu erweiterten Ereignissen finden Sie hier:

- [Schnellstart: Erweiterte Ereignisse in SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)
- Blogs: [SQL Server Extended Events](http://blogs.msdn.com/b/extended_events/)(Erweiterte Ereignisse von SQL Server)

  
## <a name="benefits-of-includessnoversionincludesssnoversion-mdmd-extended-events"></a>Vorteile von erweiterten Ereignissen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Erweiterte Ereignisse ist ein Lightweight-Leistungsüberwachungssystem, das sehr wenige Leistungsressourcen verwendet. Die Funktion „Erweiterte Ereignisse“ stellt zwei grafische Benutzeroberflächen (**Assistent für neue Sitzungen** und **Neue Sitzung**) zum Erstellen, Ändern, Anzeigen und Analysieren der Sitzungsdaten bereit.  
  
## <a name="extended-events-concepts"></a>Konzepte für erweiterte Ereignisse  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Die Funktion „Erweiterte Ereignisse“ basiert auf vorhandenen Konzepten, z.B. einem Ereignis oder einem Ereignisconsumer, verwendet Konzepte aus der Ereignisablaufverfolgung für Windows und führt neue Konzepte ein.  
  
 In der folgenden Tabelle werden die Konzepte von "Erweiterte Ereignisse" beschrieben.  
  
|Thema|Description|  
|-----------|-----------------|  
|[Pakete für erweiterte Ereignisse von SQL Server](../../relational-databases/extended-events/sql-server-extended-events-packages.md)|Beschreibt die Pakete für erweiterte Ereignisse, in denen Objekte enthalten sind, mit denen Daten beim Ausführen einer Sitzung für erweiterte Ereignisse abgerufen und verarbeitet werden.|  
|[Ziele für erweiterte Ereignisse von SQL Server](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)|Beschreibt die Ereignisconsumer, die während einer Ereignissitzung Daten empfangen können.|  
|[Modul für erweiterte Ereignisse von SQL Server](../../relational-databases/extended-events/sql-server-extended-events-engine.md)|Beschreibt das Modul, das eine Sitzung für erweiterte Ereignisse implementiert und verwaltet.|  
|[Sitzungen für erweiterte Ereignisse von SQL Server](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)|Beschreibt die Sitzung für erweiterte Ereignisse.|  
  
## <a name="extended-events-architecture"></a>Architektur von erweiterten Ereignissen  
 Erweiterte Ereignisse entsprechen einem allgemeinen Ereignisbehandlungssystem für Serversysteme. Die Infrastruktur für erweiterte Ereignisse unterstützt die Korrelation von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sowie unter bestimmten Umständen die Korrelation von Daten aus dem Betriebssystem und aus Datenbankanwendungen. Im zweiten Fall muss die Ausgabe von erweiterten Ereignissen an die Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW) weitergeleitet werden, damit die Ereignisdaten mit Ereignisdaten aus dem Betriebssystem oder einer Anwendung korreliert werden können.  
  
 Alle Anwendungen weisen Ausführungspunkte auf, die sowohl innerhalb der Anwendung als auch außerhalb nützlich sind. In der Anwendung kann die asynchrone Verarbeitung in die Warteschlange eingereiht werden, wobei Informationen zugrunde gelegt werden, die bei der ersten Ausführung eines Tasks gesammelt wurden. Außerhalb der Anwendung stellen Ausführungspunkte Überwachungshilfsprogrammen Informationen zum Verhalten und zu den Leistungsmerkmalen der überwachten Anwendung zur Verfügung.  
  
 Erweiterte Ereignisse unterstützen die Verwendung von Ereignisdaten außerhalb eines Prozesses. Diese Daten werden i. d. R. folgendermaßen verwendet:  
  
-   Von Ablaufverfolgungstools wie der SQL-Ablaufverfolgung und dem Systemmonitor  
  
-   Von Tools für die Protokollierung wie dem Windows-Ereignisprotokoll oder dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll  
  
-   Von Benutzern, die ein Produkt verwalten oder Anwendungen für ein Produkt entwickeln  
  
 Das Design von erweiterten Ereignissen zeichnet sich durch die folgenden zentralen Aspekte aus:  
  
-   Das Modul für erweiterte Ereignisse ist ereignisagnostisch. Daher kann das Modul jedes beliebige Ereignis an jedes beliebige Ziel binden, da es nicht durch den Ereignisinhalt eingeschränkt wird. Weitere Informationen zum Modul für erweiterte Ereignisse finden Sie unter [SQL Server Extended Events Engine](../../relational-databases/extended-events/sql-server-extended-events-engine.md).  
  
-   Ereignisse werden von Ereignisconsumern getrennt, die in erweiterten Ereignissen als *Ziele* bezeichnet werden. Das bedeutet, dass jedes Ziel jedes Ereignis empfangen kann. Zusätzlich kann jedes ausgelöste Ereignis automatisch vom Ziel verarbeitet werden, das dann wiederum die Protokollierung ausführen oder zusätzlichen Ereigniskontext bereitstellen kann. Weitere Informationen finden Sie unter [SQL Server Extended Events Targets](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384).  
  
-   Ereignisse unterscheiden sich von der Aktion, die ausgeführt werden soll, wenn ein Ereignis auftritt. Dies führt dazu, dass jede beliebige Aktion jedem beliebigen Ereignis zugeordnet werden kann.  
  
-   Mithilfe von Prädikaten kann dynamisch gefiltert werden, wenn Ereignisdaten aufgezeichnet werden sollen. Dadurch wird die Infrastruktur für erweiterte Ereignisse noch flexibler. Weitere Informationen finden Sie unter [SQL Server Extended Events Packages](../../relational-databases/extended-events/sql-server-extended-events-packages.md).  
  
 Erweiterte Ereignisse können Ereignisdaten synchron generieren (und asynchron verarbeiten), wodurch eine flexible Lösung für die Ereignisbehandlung bereitgestellt wird. Außerdem bieten erweiterte Ereignisse die folgenden Funktionen:  
  
-   Eine im gesamten Serversystem einheitliche Methode für die Ereignisbehandlung, wobei die Benutzer dennoch die Möglichkeit haben, einzelne Ereignisse für die Problembehandlung zu isolieren.  
  
-   Integration mit und Unterstützung von vorhandenen ETW-Tools  
  
-   Einen vollständig konfigurierbaren Ereignisbehandlungsmechanismus auf Grundlage von [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Die Möglichkeit zur dynamischen Überwachung aktiver Prozesse mit minimaler Beeinträchtigung dieser Prozesse.  
  
-   Eine standardmäßige Systemintegritätssitzung, die ohne merkliche Auswirkungen auf die Leistung ausgeführt wird. In der Sitzung werden Systemdaten erfasst, mit deren Hilfe Sie Leistungsprobleme beheben können. Weitere Informationen finden Sie unter [Verwenden der system_health-Sitzung](../../relational-databases/extended-events/use-the-system-health-session.md).  
  
## <a name="extended-events-tasks"></a>Tasks für erweiterte Ereignisse  

Durch Verwenden von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] zum Ausführen von [!INCLUDE[tsql](../../includes/tsql-md.md)] -DDL-Anweisungen (Data Definition Language), dynamischen Verwaltungssichten und -funktionen oder Katalogsichten können Sie einfache oder komplexe Problembehandlungslösungen für erweiterte Ereignisse von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für Ihre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Umgebung erstellen.  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Verwenden Sie den **Objekt-Explorer** , um Ereignissitzungen zu verwalten.|[Verwalten von Ereignissitzungen im Objektexplorer](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)|  
|Beschreibt, wie Sie eine Sitzung für erweiterte Ereignisse erstellen.|[Erstellen einer Sitzung für erweiterte Ereignisse](http://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74)|  
|Beschreibt, wie Sie Zieldaten anzeigen und aktualisieren.| [Erweiterte Ansicht von Zieldaten aus erweiterten Ereignissen in SQL Server](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)|  
|Beschreibt, wie Sie die folgenden Tools von erweiterten Ereignissen zum Erstellen und Verwalten von erweiterten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ereignissitzungen verwenden:|[Tools für erweiterte Ereignisse](../../relational-databases/extended-events/extended-events-tools.md)|  
|Beschreibt, wie Sie eine Sitzung für erweiterte Ereignisse ändern.|[Ändern einer Sitzung für erweiterte Ereignisse](../../relational-databases/extended-events/alter-an-extended-events-session.md)|  
|Beschreibt, wie Sie Informationen zu den den Ereignissen zugeordneten Feldern abrufen.|[Abrufen der Felder für alle Ereignisse](http://msdn.microsoft.com/library/4e4ee03f-5bca-42ed-a37c-db1c82e3aad2)|  
|Beschreibt, wie Sie herausfinden, welche Ereignisse in den registrierten Paketen verfügbar sind.|[Anzeigen der Ereignisse für registrierte Pakete](http://msdn.microsoft.com/library/9a90b1a2-aa69-43f6-bdeb-cc5f57a26c6f)|  
|Beschreibt, wie Sie ermitteln, welche Ziele für erweiterte Ereignisse in den registrierten Paketen verfügbar sind.|[Anzeigen der Ziele von erweiterten Ereignissen für registrierte Pakete](http://msdn.microsoft.com/library/4985aa5f-ac99-49f6-852c-9d25916549e9)|  
|Beschreibt, wie Sie die Ereignisse und Aktionen für erweiterte Ereignisse anzeigen, die den einzelnen SQL-Ablaufverfolgungsereignissen und deren zugeordneten Spalten entsprechen.|[Anzeigen der Entsprechungen von erweiterten Ereignissen für SQL-Ablaufverfolgungsklassen](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|Beschreibt, wie Sie die Parameter suchen, die sich festlegen lassen, wenn Sie das ADD TARGET-Argument in CREATE EVENT SESSION oder ALTER EVENT SESSION verwenden.|[Abrufen der konfigurierbaren Parameter für das ADD TARGET-Argument](http://msdn.microsoft.com/library/08454543-c5c8-4ca3-9af9-f1d82264471c)|  
|Beschreibt, wie Sie ein vorhandenes SQL-Ablaufverfolgungsskript in eine Sitzung für erweiterte Ereignisse konvertieren.|[Konvertieren eines vorhandenen SQL-Ablaufverfolgungsskripts in eine Sitzung für erweiterte Ereignisse](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|Beschreibt die Ermittlung der gesperrten Abfragen, des Plans der Abfrage und des [!INCLUDE[tsql](../../includes/tsql-md.md)] -Stapels zum Zeitpunkt der Sperrung.|[Feststellen, welche Abfragen Sperren enthalten](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)|  
|Beschreibt, wie Sie die Quelle von Sperren identifizieren, die die Datenbankleistung beeinträchtigen.|[Suchen der Objekte, die über die meisten Sperren verfügen](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|Beschreibt, wie Sie anhand von erweiterten Ereignissen mit der Ereignisablaufverfolgung für Windows die Systemaktivität überwachen.|[Überwachen der Systemaktivität mit erweiterten Ereignisses](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)|  
| Verwenden der Katalogsichten und dynamischen Verwaltungssichten für erweiterte Ereignisse | [SELECT- und JOIN-Anweisungen von Systemsichten für erweiterte Ereignisse in SQL Server](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) |

  
## <a name="see-also"></a>Siehe auch  
 [Datenebenenanwendungen](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [DAC-Unterstützung für SQL Server-Objekte und -Versionen](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)   
 [Bereitstellen einer Datenebenenanwendung](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [Überwachen von Datenebenenanwendungen](../../relational-databases/data-tier-applications/monitor-data-tier-applications.md)   
 [Dynamische Verwaltungssichten für erweiterte Ereignisse](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [Katalogsichten für erweiterte Ereignisse &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)  
  
  

