---
title: Replikation in die SQL-Datenbank | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 06/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Database replication
- replication, SQL Database
ms.assetid: e8484da7-495f-4dac-b38e-bcdc4691f9fa
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1beb8c0334078c7710568a40339daf05ed0b69e1
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="replication-to-sql-database"></a>Replikation zu SQL-Datenbank
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation kann für [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]konfiguriert werden.  
  
 **Unterstützte Konfigurationen:**  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz sein, der lokal ausgeführt wird. Alternativ kann es sich um eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] handeln, die auf einem virtuellen Azure-Computer in der Cloud ausgeführt wird. Weitere Informationen finden Sie unter [Übersicht zu SQL Server auf virtuellen Azure-Computern](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] muss ein Pushabonnent eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verlegers sein.  
  
-   Die Verteilungsdatenbank und die Replikations-Agents können nicht auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)]platziert werden.  
  
-   Es werden nur Momentaufnahmen und die unidirektionale Transaktionsreplikation unterstützt. Die Peer-zu-Peer-Transaktionsreplikation und Mergereplikation werden nicht unterstützt.  
  
## <a name="versions"></a>Versionen  
 Verleger und Verteiler müssen mindestens eine der folgenden Versionen aufweisen:  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP1 CU3  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] RTM CU10  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 CU8  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] in SP3 erwartet  
  
 Bei dem Versuch, die Replikation mit einer älteren Version zu konfigurieren, können folgende Fehlernummern auftreten: MSSQL_REPL20084 (Der Prozess konnte keine Verbindung zum Abonnenten herstellen.) und MSSQL_REPL40532 (Der von der Anmeldung angeforderte Server \<Name> kann nicht geöffnet werden. Fehler bei der Anmeldung).  
  
 Der [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Abonnent muss mindestens V12 aufweisen und kann sich in jeder Region befinden.  
  
 Sie müssen die neuesten Versionen der [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) und [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) verwenden, um alle Funktionen von [!INCLUDE[ssSDS](../../includes/sssds-md.md)] nutzen zu können.  
  
## <a name="remarks"></a>Hinweise  
 Die Replikation kann mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder durch Ausführen von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen auf dem Verleger konfiguriert werden. Sie können die Replikation nicht mithilfe des [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Portals konfigurieren.  
  
 Die Replikation kann zur Authentifizierung nur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen verwenden, um sich mit [!INCLUDE[ssSDS](../../includes/sssds-md.md)]zu verbinden.  
  
 Eine replizierte Tabelle muss einen Primärschlüssel haben.  
  
 Sie benötigen ein Azure-Abonnement und eine vorhandene [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.  
  
 Eine einzelne Veröffentlichung auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann sowohl [!INCLUDE[ssSDS](../../includes/sssds-md.md)] - als auch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - (lokal und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einer Azure Virtual Machine) Abonnenten unterstützen.  
  
 Die Replikationsverwaltung, -überwachung und -problembehandlung muss auf dem lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt werden.  
  
 Es werden nur Pushabonnements für [!INCLUDE[ssSDS](../../includes/sssds-md.md)] unterstützt.  
  
 In `@subscriber_type = 0` wird für SQL-Datenbank nur **@subscriber_type = 0** unterstützt.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] unterstützt nicht die bidirektionale, sofortige, aktualisierbare oder Peer-to-Peer-Replikation.  
  
## <a name="replication-architecture"></a>Replikationsarchitektur  
 ![replikation-in-die-sql-datenbank](../../relational-databases/replication/media/replication-to-sql-database.png "replication-to-sql-database")  
  
## <a name="scenarios"></a>Szenarien  
  
#### <a name="typical-replication-scenario"></a>Typisches Replikationsszenario  
  
1.  Erstellen Sie eine Transaktionsreplikationsveröffentlichung auf einer lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank.  
  
2.  Verwenden Sie auf dem lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den **Assistenten für neue Abonnements** oder [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen, um einen Push für [!INCLUDE[ssSDS](../../includes/sssds-md.md)]-Abonnements zu erstellen .  
  
3.  Das anfängliche Dataset ist in der Regel eine Momentaufnahme, die vom Momentaufnahme-Agent erstellt und vom Verteilungs-Agent verteilt und angewendet wird. The initial data set can also be supplied through a backup or other means, such as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
#### <a name="data-migration-scenario"></a>Datenmigrationsszenario  
  
1.  Verwenden Sie die Transaktionsreplikation, um Daten aus einer lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank zu [!INCLUDE[ssSDS](../../includes/sssds-md.md)]zu replizieren.  
  
2.  Leiten Sie die Client- oder Middle-Tier-Anwendung um, um die Kopie der [!INCLUDE[ssSDS](../../includes/sssds-md.md)] zu aktualisieren.  
  
3.  Beenden Sie die Aktualisierung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version der Tabelle, und entfernen Sie die Veröffentlichung.  
  
## <a name="limitations"></a>Einschränkungen  
 Die folgenden Optionen werden für [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Abonnements nicht unterstützt:  
  
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
  
## <a name="examples"></a>Beispiele  
 Erstellen Sie eine Veröffentlichung für ein Pushabonnement. Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md) indem Sie den logischen Servernamen [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] als Abonnent (z.B. **N'azuresqldbdns.database.windows.net'**) und den Namen [!INCLUDE[ssSDS](../../includes/sssds-md.md)] als Zieldatenbank verwenden (z.B. **AdventureWorks**).  
  
## <a name="see-also"></a>Siehe auch  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Types of Replication](../../relational-databases/replication/types-of-replication.md)   
 [Überwachen &#40;Replikation&#41;](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Initialize a Subscription](../../relational-databases/replication/initialize-a-subscription.md)  
  
  

