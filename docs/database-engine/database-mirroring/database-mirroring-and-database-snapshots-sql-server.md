---
title: Datenbankspiegelung und Datenbankmomentaufnahmen (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- snapshots [SQL Server database snapshots], database mirroring
- database snapshots [SQL Server], database mirroring
ms.assetid: 0bf1be90-7ce4-484c-aaa7-f8a782f57c5f
caps.latest.revision: "41"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: db1c0902b2de0a761e1a7558e9bbb71c946afe5b
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="database-mirroring-and-database-snapshots-sql-server"></a>Datenbankspiegelung und Datenbankmomentaufnahmen (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Sie können die Vorteile einer Spiegeldatenbank, die aus Gründen der Verfügbarkeit verwaltet wird, auch für die ausgelagerte Berichterstellung ausnutzen. Wenn Sie für die Berichterstellung eine Spiegeldatenbank verwenden möchten, können Sie eine Datenbankmomentaufnahme für die Spiegeldatenbank erstellen und die Clientverbindungsanforderungen an die zuletzt erstellte Momentaufnahme weiterleiten. Eine Datenbankmomentaufnahme ist eine statische, schreibgeschützte, hinsichtlich der Transaktionen konsistente Momentaufnahme des Zustands einer Quelldatenbank, in dem sich diese zum Zeitpunkt der Erstellung der Momentaufnahme befand. Zum Erstellen einer Datenbankmomentaufnahme für die Spiegeldatenbank muss sich die Datenbank im synchronisierten Spiegelungsstatus befinden.  
  
 Im Gegensatz zur eigentlichen Spiegeldatenbank ist eine Datenbankmomentaufnahme auch für Clients zugreifbar. Solange der Spiegelserver mit dem Prinzipalserver kommuniziert, können Sie Berichtsclients an eine Verbindung mit einer Momentaufnahme weiterleiten. Da Datenbankmomentaufnahmen statisch sind, sind neue Daten nicht verfügbar. Sie müssen in regelmäßigen Abständen eine neue Datenbankmomentaufnahme erstellen und sicherstellen, dass Anwendungen eingehende Clientverbindungen an die neueste Momentaufnahme weiterleiten, um den Benutzern relativ neue Daten zur Verfügung zu stellen.  
  
 Eine neue Datenbankmomentaufnahme ist fast leer. Er nimmt jedoch im Laufe der Zeit an Größe zu, wenn immer mehr Datenbankseiten zum ersten Mal aktualisiert werden. Da jede Momentaufnahme für eine Datenbank auf diese Weise schrittweise größer wird, verbraucht jede einzelne Datenbankmomentaufnahme genauso viele Ressourcen wie eine normale Datenbank. Abhängig von der Konfiguration des Spiegelservers und des Prinzipalservers kann sich bei Vorhandensein einer übermäßig hohen Anzahl von Datenbankmomentaufnahmen auf einer Spiegeldatenbank die Leistung der Prinzipaldatenbank verringern. Sie sollten daher nur einige wenige, relativ neue Momentaufnahmen auf den Spiegeldatenbanken behalten. Nachdem Sie eine Ersatzmomentaufnahme erstellt haben, sollten Sie eingehende Abfragen an die neue Momentaufnahme weiterleiten und die frühere Momentaufnahme löschen, sobald alle aktuellen Abfragen abgeschlossen sind.  
  
> [!NOTE]  
>  Weitere Informationen zu Datenbankmomentaufnahmen finden Sie unter [Datenbank-Momentaufnahmen &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
 Wenn ein Rollenwechsel stattfindet, werden die Datenbank und die zugehörigen Momentaufnahmen neu gestartet, wobei die Verbindung mit den Benutzern vorübergehend getrennt wird. Anschließend verbleiben die Datenbankmomentaufnahmen auf der Serverinstanz, auf der sie erstellt wurden und die zur neuen Prinzipaldatenbank geworden ist. Die Momentaufnahmen können nach dem Failover weiter verwendet werden. Dies bedeutet für den neuen Prinzipalserver jedoch eine zusätzliche Belastung. Falls in Ihrer Umgebung die Leistung eine wichtige Überlegung ist, sollten Sie auf der neuen Spiegeldatenbank eine Momentaufnahme erstellen, sobald diese verfügbar ist, die Clients zu der neuen Momentaufnahme umleiten und alle Datenbankmomentaufnahmen aus der früheren Spiegeldatenbank löschen.  
  
> [!NOTE]  
>  Wenn Sie eine dedizierte, gut skalierte Berichterstellung bevorzugen, sollten Sie eine Replikation in Betracht ziehen. Weitere Informationen finden Sie unter [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md).  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel werden Momentaufnahmen für eine gespiegelte Datenbank erstellt.  
  
 Angenommen, die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank wird in einer Datenbank-Spiegelungssitzung verwendet. In diesem Beispiel werden drei Datenbankmomentaufnahmen für die Spiegelkopie der `AdventureWorks` -Datenbank erstellt, die sich auf Laufwerk `F` befindet. Die Momentaufnahmen werden mit `AdventureWorks_0600`, `AdventureWorks_1200`und `AdventureWorks_1800` bezeichnet, um den ungefähren Zeitpunkt ihrer Erstellung anzugeben.  
  
1.  Erstellen Sie die erste Datenbankmomentaufnahm für den Spiegel von [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
    ```  
    CREATE DATABASE AdventureWorks_0600  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_0600.SNP')  
       AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
2.  Erstellen Sie die zweite Datenbankmomentaufnahme für den Spiegel von [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Benutzer, die noch immer `AdventureWorks_0600` verwenden, können diese auch weiterhin verwenden.  
  
    ```  
    CREATE DATABASE AdventureWorks_1200  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_1200.SNP')  
       AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
     Die neuen Clientverbindungen können nun programmgesteuert an die zuletzt erstellte Momentaufnahme weitergeleitet werden.  
  
3.  Erstellen Sie die dritte Momentaufnahme für den Spiegel von [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Benutzer, die immer noch `AdventureWorks_0600` oder `AdventureWorks_1200` verwenden, können diese auch weiterhin verwenden.  
  
    ```  
    CREATE DATABASE AdventureWorks_1800  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_1800.SNP')  
        AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
     Die neuen Clientverbindungen können nun programmgesteuert an die zuletzt erstellte Momentaufnahme weitergeleitet werden.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Erstellen einer Datenbankmomentaufnahme &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Anzeigen einer Datenbankmomentaufnahme &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [Löschen einer Datenbankmomentaufnahme &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenbank-Momentaufnahmen &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [Verbinden von Clients mit einer Datenbank-Spiegelungssitzung &#40;SQL Server&#41;](../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)  
  
  
