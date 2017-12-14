---
title: Entfernen der Datenbankspiegelung (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/17/2016
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
- database mirroring [SQL Server], removing
- removing database mirroring [SQL Server]
ms.assetid: bbc4d7f7-3bc7-40d6-a822-af195fe7f8c0
caps.latest.revision: "42"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e4557e1e2d52ebc45b73728b813358b07b8bea19
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="remove-database-mirroring-sql-server"></a>Entfernen der Datenbankspiegelung (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie eine Datenbankspiegelung aus einer Datenbank in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] entfernen.  Der Datenbankbesitzer kann eine Datenbank-Spiegelungssitzung jederzeit manuell beenden, indem er die Spiegelung von der Datenbank entfernt.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **Entfernen einer Datenbankspiegelung mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Entfernen der Datenbankspiegelung](#FollowUp)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-remove-database-mirroring"></a>So entfernen Sie die Datenbankspiegelung  
  
1.  Stellen Sie während einer Datenbank-Spiegelungssitzung eine Verbindung mit der Prinzipalserverinstanz her, und klicken Sie im Objekt-Explorer auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**, und wählen Sie die Datenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, wählen Sie **Tasks**aus, und klicken Sie dann auf **Spiegeln**. Dadurch wird die Seite **Spiegelung** im Dialogfeld **Datenbankeigenschaften** geöffnet.  
  
4.  Klicken Sie im Bereich **Seite auswählen** auf **Spiegelung**.  
  
5.  Zum Entfernen der Spiegelung klicken Sie auf **Spiegeln entfernen**. Es wird eine Bestätigungsaufforderung angezeigt. Wenn Sie auf **Ja**klicken, wird die Sitzung beendet, und die Spiegelung wird aus der Datenbank entfernt.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Zum Entfernen der Datenbankspiegelung verwenden Sie die **Datenbankeigenschaften**. Verwenden Sie die Seite **Spiegelung** im Dialogfeld **Datenbankeigenschaften** .  
  
#### <a name="to-remove-database-mirroring"></a>So entfernen Sie die Datenbankspiegelung  
  
1.  Stellen Sie für einen der Spiegelungspartner eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)] her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Führen Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung aus:  
  
    ```  
    ALTER DATABASE database_name SET PARTNER OFF  
    ```  
  
     wobei *Datenbankname* für die gespiegelte Datenbank steht, deren Sitzung Sie entfernen möchten.  
  
     Im folgenden Beispiel wird die Datenbankspiegelung aus der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank entfernt.  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER OFF;  
    ```  
  
##  <a name="FollowUp"></a> Nachverfolgung: Entfernen der Datenbankspiegelung  
  
> [!NOTE]  
>  Weitere Informationen zu den Auswirkungen des Entfernens der Datenbankspiegelung finden Sie unter [Entfernen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
-   **Wenn Sie die Datenbankspiegelung erneut starten möchten**  
  
     Vor dem erneuten Starten der Spiegelung müssen alle Protokollsicherungen, die nach dem Entfernen der Spiegelung für die Prinzipaldatenbank erstellt wurden, auf die Spiegeldatenbank angewendet werden.  
  
-   **Wenn Sie die Datenbankspiegelung nicht erneut starten möchten**  
  
     Sie haben auch die Möglichkeit, die frühere Spiegeldatenbank wiederherzustellen. Auf der Serverinstanz, die den Spiegelserver darstellte, können Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung ausführen:  
  
    ```  
    RESTORE DATABASE database_name WITH RECOVERY;  
    ```  
  
    > [!IMPORTANT]  
    >  Wenn Sie diese Datenbank wiederherstellen, sind zwei voneinander abweichende Datenbanken mit demselben Namen online. Deshalb müssen Sie sicherstellen, dass Clients nur auf eine der beiden zugreifen können (in der Regel die aktuellere Prinzipaldatenbank).  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Anhalten oder Fortsetzen einer Datenbank-Spiegelungssitzung &#40;SQL Server&#41;](../../database-engine/database-mirroring/pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
-   [Entfernen des Zeugen aus einer Datenbank-Spiegelungssitzung &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
-   [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
  
-   [Beispiel: Einrichten der Datenbankspiegelung mithilfe von Zertifikaten &#40;SQL Server&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Einrichten der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
