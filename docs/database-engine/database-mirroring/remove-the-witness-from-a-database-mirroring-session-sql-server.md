---
title: "Entfernen des Zeugen aus einer Datenbank-Spiegelungssitzung (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Zeuge [SQL Server], deaktivieren"
  - "Zeuge [SQL Server], entfernen"
  - "Datenbankspiegelung [SQL Server], Zeuge"
ms.assetid: f3ce7afc-8936-4d35-80ce-d0f8fbc318d3
caps.latest.revision: 39
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 39
---
# Entfernen des Zeugen aus einer Datenbank-Spiegelungssitzung (SQL Server)
  In diesem Thema wird beschrieben, wie Sie einen Zeugen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]aus einer Datenbankspiegelungssitzung entfernen. Der Datenbankbesitzer kann den Zeugen für eine Datenbank-Spiegelungssitzung jederzeit während einer Datenbank-Spiegelungssitzung deaktivieren.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **Entfernen des Zeugen mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Entfernen des Zeugen](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So entfernen Sie den Zeugen  
  
1.  Stellen Sie eine Verbindung zur Prinzipalserverinstanz her, und klicken Sie im Bereich **Objekt-Explorer** auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**, und wählen Sie die Datenbank aus, deren Zeuge entfernt werden soll.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, wählen Sie **Tasks** aus, und klicken Sie dann auf **Spiegeln**. Dadurch wird die Seite **Spiegelung** im Dialogfeld **Datenbankeigenschaften** geöffnet.  
  
4.  Zum Entfernen des Zeugen löschen Sie seine Servernetzwerkadresse aus dem Feld **Zeuge** .  
  
    > [!NOTE]  
    >  Wenn Sie vom Modus für hohe Sicherheit mit automatischem Failover zum Modus zur hohe Leistung wechseln, wird das **Feld** Zeuge automatisch gelöscht.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So entfernen Sie den Zeugen  
  
1.  Stellen Sie für eine der Partnerserverinstanzen eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)] her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Führen Sie die folgende Anweisung aus:  
  
     [ALTER DATABASE](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md) *Datenbankname* SET WITNESS OFF  
  
     Dabei ist *Datenbankname* der Name der gespiegelten Datenbank.  
  
     Im folgenden Beispiel wird der Zeuge aus der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank entfernt.  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET WITNESS OFF ;  
    ```  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Entfernen des Zeugen  
 Durch das Deaktivieren des Zeugen ändert sich der [Betriebsmodus](../../database-engine/database-mirroring/database-mirroring-operating-modes.md) entsprechend der Einstellung für die Transaktionssicherheit:  
  
-   Wenn die Transaktionssicherheit auf FULL (Standardeinstellung) festgelegt ist, wird in der Sitzung der synchrone Modus für hohe Sicherheit ohne automatisches Failover verwendet.  
  
-   Wenn die Transaktionssicherheit auf OFF festgelegt ist, wird die Sitzung asynchron (im Modus für hohe Leistung) ausgeführt, ohne dass ein Quorum erforderlich ist. Bei deaktivierter Transaktionssicherheit wird stets dringend empfohlen, den Zeugen ebenfalls zu deaktivieren.  
  
> [!TIP]  
>  Die Transaktionssicherheitseinstellung der Datenbank wird auf jedem Partner in der [sys.database_mirroring](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)-Katalogsicht in der **mirroring_safety_level**-Spalte und der **mirroring_safety_level_desc**-Spalte aufgezeichnet.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Hinzufügen eines Zeugen für die Datenbankspiegelung mithilfe der Windows-Authentifizierung &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
-   [Hinzufügen oder Ersetzen eines Datenbank-Spiegelungszeugen &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
## Siehe auch  
 [ALTER DATABASE-Datenbankspiegelung &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md)   
 [Ändern der Transaktionssicherheit in einer Datenbank-Spiegelungssitzung &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)   
 [Hinzufügen eines Zeugen für die Datenbankspiegelung mithilfe der Windows-Authentifizierung &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)   
 [Datenbank-Spiegelungszeuge](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  