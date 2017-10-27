---
title: "Aktivieren von Indizes und Einschränkungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- indexes [SQL Server], enabling
- nonclustered indexes [SQL Server], enabling a disabled index
- index enabling [SQL Server]
- disabled indexes [SQL Server], how to enable
- constraints [SQL Server], enabling
- clustered indexes, enabling disabled indexes
ms.assetid: c55c8865-322e-4ab0-ba04-ea1f56735353
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2e0e171e2cf2bdc35a3e9c3c7e5ed1077aabe4dc
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="enable-indexes-and-constraints"></a>Aktivieren von Indizes und Einschränkungen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie ein deaktivierter Index in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]aktiviert wird. Nach dem Deaktivieren eines Indexes bleibt er deaktiviert, bis er neu erstellt oder gelöscht wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So aktivieren Sie einen deaktivierten Index mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Nachdem der Index neu erstellt wurde, müssen alle Einschränkungen, die aufgrund der Deaktivierung des Indexes deaktiviert wurden, manuell aktiviert werden. PRIMARY KEY- und UNIQUE-Einschränkungen werden durch Neuerstellen des zugehörigen Indexes aktiviert. Dieser Index muss neu erstellt (aktiviert) werden, bevor Sie FOREIGN KEY-Einschränkungen aktivieren können, die auf die PRIMARY KEY- oder UNIQUE-Einschränkung verweisen. FOREIGN KEY-Einschränkungen werden mithilfe der ALTER TABLE CHECK CONSTRAINT-Anweisung aktiviert.  
  
-   Das Neuerstellen eines deaktivierten gruppierten Indexes kann nicht ausgeführt werden, wenn die Option ONLINE auf ON festgelegt wurde.  
  
-   Wenn der gruppierte Index deaktiviert oder aktiviert und der nicht gruppierte Index deaktiviert ist, besitzt die Aktion des gruppierten Indexes die folgenden Auswirkungen auf den deaktivierten nicht gruppierten Index.  
  
    |Gruppierte Index-Aktion|Deaktivierter nicht gruppierter Index ...|  
    |----------------------------|-----------------------------------|  
    |ALTER INDEX REBUILD|Bleibt deaktiviert.|  
    |ALTER INDEX ALL REBUILD.|Wird neu erstellt und aktiviert.|  
    |DROP INDEX.|Bleibt deaktiviert.|  
    |CREATE INDEX WITH DROP_EXISTING.|Bleibt deaktiviert.|  
  
     Beim Erstellen eines neuen gruppierten Index tritt das gleiche Verhalten auf wie bei ALTER INDEX ALL REBUILD.  
  
-   Zulässige Aktionen für nicht gruppierte Indizes, die einem gruppierten Index zugeordnet sind, hängen vom Status (deaktiviert oder aktiviert) der beiden Indextypen ab. In der folgenden Tabelle werden die zulässigen Aktionen für nicht gruppierte Indizes zusammengefasst.  
  
    |Nicht gruppierte Index-Aktion|Wenn der gruppierte und der nicht gruppierte Index deaktiviert sind.|Wenn der gruppierte Index aktiviert ist und der nicht gruppierte Index einen beliebigen Zustand aufweist.|  
    |-------------------------------|--------------------------------------------------------------------|----------------------------------------------------------------------------------------|  
    |ALTER INDEX REBUILD|Die Aktion erzeugt einen Fehler.|Die Aktion ist erfolgreich.|  
    |DROP INDEX.|Die Aktion ist erfolgreich.|Die Aktion ist erfolgreich.|  
    |CREATE INDEX WITH DROP_EXISTING.|Die Aktion erzeugt einen Fehler.|Die Aktion ist erfolgreich.|  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht. Bei der Verwendung von DBCC DBREINDEX muss der Benutzer die Tabelle besitzen oder Mitglied der festen Serverrolle **sysadmin** oder der festen Datenbankrollen **db_ddladmin** und **db_owner** sein.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-enable-a-disabled-index"></a>So aktivieren Sie einen deaktivierten Index  
  
1.  Klicken Sie in Objekt-Explorer auf das Pluszeichen, um die Datenbank zu erweitern, die die Tabelle enthält, auf der Sie einen Index aktivieren möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, in der Sie einen Index aktivieren möchten.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Indizes** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf den Index, den Sie aktivieren möchten, und wählen Sie **Neu erstellen**aus.  
  
6.  Überprüfen Sie im Dialogfeld **Indizes neu erstellen** , dass der richtige Index im Raster **Neu zu erstellende Indizes** ausgewählt ist, und klicken sie auf **OK**.  
  
#### <a name="to-enable-all-indexes-on-a-table"></a>So aktivieren Sie alle Indizes auf einer Tabelle  
  
1.  Klicken Sie in Objekt-Explorer auf das Pluszeichen, um die Datenbank zu erweitern, die die Tabelle enthält, in der Sie die Indizes aktivieren möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, in der Sie die Indizes aktivieren möchten.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Ordner **Indizes** , und wählen Sie **Alle neu erstellen**.  
  
5.  Überprüfen Sie im Dialogfeld **Indizes neu erstellen** , dass die richtigen Indizes im Raster **Neu zu erstellende Indizes** ausgewählt sind, und klicken sie auf **OK**. Um einen Index aus dem Raster **Neu zu erstellende Indizes** zu entfernen, wählen Sie den Index aus, und drücken Sie die ENTF-Taste.  
  
 Die folgenden Informationen sind im Dialogfeld **Indizes neu erstellen** verfügbar:  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-enable-a-disabled-index-using-alter-index"></a>So aktivieren Sie einen deaktivierten Index mit ALTER INDEX  
  
1.  Stellen **Sie im Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Enables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table.  
  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    REBUILD;   
    GO  
    ```  
  
#### <a name="to-enable-a-disabled-index-using-create-index"></a>So aktivieren Sie einen deaktivierten Index mit CREATE INDEX  
  
1.  Stellen **Sie im Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- re-creates the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    -- using the OrganizationLevel and OrganizationNode columns  
    -- and then deletes the existing IX_Employee_OrganizationLevel_OrganizationNode index  
    CREATE INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
       (OrganizationLevel, OrganizationNode)  
    WITH (DROP_EXISTING = ON);  
    GO  
    ```  
  
#### <a name="to-enable-a-disabled-index-using-dbcc-dbreindex"></a>So aktivieren Sie einen deaktivierten Index mit DBCC DBREINDEX  
  
1.  Stellen **Sie im Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- enables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    DBCC DBREINDEX ("HumanResources.Employee", IX_Employee_OrganizationLevel_OrganizationNode);  
    GO  
    ```  
  
#### <a name="to-enable-all-indexes-on-a-table-using-alter-index"></a>So aktivieren Sie alle Indizes auf einer Tabelle mit ALTER INDEX  
  
1.  Stellen **Sie im Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- enables all indexes  
    -- on the HumanResources.Employee table  
    ALTER INDEX ALL ON HumanResources.Employee  
    REBUILD;  
    GO  
    ```  
  
#### <a name="to-enable-all-indexes-on-a-table-using-dbcc-dbreindex"></a>So aktivieren Sie alle Indizes auf einer Tabelle mit DBCC DBREINDEX  
  
1.  Stellen **Sie im Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- enables all indexes  
    -- on the HumanResources.Employee table  
    DBCC DBREINDEX ("HumanResources.Employee", " ");  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md), [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md) und [DBCC DBREINDEX &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md).  
  
  

