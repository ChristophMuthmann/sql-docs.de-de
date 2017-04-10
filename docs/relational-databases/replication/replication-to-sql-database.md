---
title: "Replikation zu SQL-Datenbank | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL-Datenbank-Replikation"
  - "Replikation, SQL-Datenbank"
ms.assetid: e8484da7-495f-4dac-b38e-bcdc4691f9fa
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Replikation zu SQL-Datenbank
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replikation kann so konfiguriert werden, dass [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
 **Unterstützte Konfigurationen:**  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann eine Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, lokal oder eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in virtuellen Azure-Computer in der Cloud ausgeführt wird. Weitere Informationen finden Sie unter [SQL Server auf Azure Virtual Machines-Übersicht](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] muss ein Abonnent Push von einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
-   Die Verteilungsdatenbank und die Replikations-Agents können nicht platziert werden [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
-   Es werden nur Momentaufnahmen und die unidirektionale Transaktionsreplikation unterstützt. Die Peer-zu-Peer-Transaktionsreplikation und Mergereplikation werden nicht unterstützt.  
  
## Versionen  
 Verleger und Verteiler müssen mindestens eine der folgenden Versionen aufweisen:  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP1 CU3  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] CU10 RTM  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 CU 8  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP3 erwartet  
  
 Zum Konfigurieren der Replikation mit einer älteren Version können Herstellens Fehler MSSQL_REPL20084 (der Prozess konnte nicht an Abonnenten verbinden) und MSSQL_REPL40532 (Server kann nicht geöffnet werden. \< Name> von der Anmeldung angeforderte. Fehler bei der Anmeldung.).  
  
 Die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Abonnenten muss mindestens V12 und können in jeder Region.  
  
 Verwendung aller Funktionen von [!INCLUDE[ssSDS](../../includes/sssds-md.md)] müssen verwenden Sie die neuesten Versionen der [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) und [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx).  
  
## Hinweise  
 Replikation kann konfiguriert werden, mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder durch Ausführen von [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen auf dem Verleger. Konfigurieren der Replikation kann nicht mithilfe der [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Portal.  
  
 Replikation können Sie nur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Benutzernamen für die Authentifizierung für die Verbindung [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Eine replizierte Tabelle muss einen Primärschlüssel haben.  
  
 Sie benötigen ein Azure-Abonnement und eine vorhandene [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.  
  
 Eine einzelne Veröffentlichung auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen sowohl [!INCLUDE[ssSDS](../../includes/sssds-md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (lokale und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einer Azure Virtual Machines) Abonnenten.  
  
 Replikations-Management, Überwachung und Problembehandlung erforderlich, aus dem lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Nur Pushabonnements, [!INCLUDE[ssSDS](../../includes/sssds-md.md)] werden unterstützt.  
  
 Nur `@subscriber_type = 0` wird unterstützt **Sp_addsubscription** für SQL-Datenbank.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] bidirektionale, sofortige, aktualisiert oder Peer-to-Peer-Replikation unterstützt nicht.  
  
## Replikationsarchitektur  
 ![replication-to-sql-database](../../relational-databases/replication/media/replication-to-sql-database.png "replication-to-sql-database")  
  
## Szenarien  
  
#### Typisches Replikationsszenario  
  
1.  Erstellen Sie eine Transaktionsreplikation-Veröffentlichung auf einem lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank.  
  
2.  Auf dem lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden den **Assistenten für neue Abonnements** oder [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen erstellen Sie einen Push für Abonnement [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
3.  Das anfängliche Dataset ist in der Regel eine Momentaufnahme, die vom Momentaufnahme-Agent erstellt und vom Verteilungs-Agent verteilt und angewendet wird. Das ursprüngliche Dataset kann auch angegeben werden über eine Sicherung oder andere Methoden, wie z. B. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
#### Datenmigrationsszenario  
  
1.  Replizieren von Daten aus einer lokalen verwenden Transaktionsreplikation [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
2.  Umleiten der Client- oder mittleren Ebene Applikationen aktualisieren die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] kopieren.  
  
3.  Aktualisiert die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version der Tabelle, und entfernen Sie die Veröffentlichung.  
  
## Einschränkungen  
 Die folgenden Optionen können nicht für [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Abonnements:  
  
-   Kopieren der Dateigruppenzuordnung  
  
-   Kopieren des Tabellenpartitionierungsschemas  
  
-   Kopieren des Indexpartitionierungsschemas  
  
-   Kopieren der benutzerdefinierten Statistiken  
  
-   Kopieren der Standardbindungen  
  
-   Kopieren der Regelbindungen  
  
-   Kopieren von Volltextindizes  
  
-   Kopieren von XML XSD  
  
-   Kopieren von XML-Indizes  
  
-   Kopieren von Berechtigungen  
  
-   Kopieren von räumlichen Indizes  
  
-   Kopieren von gefilterten Indizes  
  
-   Kopieren von Datenkomprimierungsattributen  
  
-   Kopieren von Attributen von Spalten mit geringer Dichte  
  
-   Konvertieren von Filestream- in MAX-Datentypen  
  
-   Konvertieren von hierarchyid- in MAX-Datentypen  
  
-   Konvertieren von räumlichen Datentypen in MAX-Datentypen  
  
-   Kopieren von erweiterten Eigenschaften  
  
-   Kopieren von Berechtigungen  
  
 Zu bestimmende Einschränkungen:  
  
-   Sortierung der Kopien  
  
-   Ausführung in einer serialisierten Transaktion  
  
## Beispiele  
 Erstellen Sie eine Veröffentlichung für ein Pushabonnement. Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Erstellen eines Abonnements Push](../../relational-databases/replication/create-a-push-subscription.md) mithilfe der [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] Namen des logischen Servers als Abonnent (z. B. **N'azuresqldbdns.database.windows.net'**) und die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Name als Zieldatenbank (z. B. **AdventureWorks**).  
  
## Siehe auch  
 [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md)   
 [Erstellen eines Pushabonnements](../../relational-databases/replication/create-a-push-subscription.md)   
 [Replikationstypen](../../relational-databases/replication/types-of-replication.md)   
 [Überwachung & #40; Replikation & #41;](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Initialisieren eines Abonnements](../../relational-databases/replication/initialize-a-subscription.md)  
  
  