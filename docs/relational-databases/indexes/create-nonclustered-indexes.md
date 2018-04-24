---
title: Erstellen nicht gruppierter Indizes | Microsoft Dokumentation
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- index creation [SQL Server], nonclustered indexes
- nonclustered indexes [SQL Server], creating
- nonclustered indexes [SQL Server], UNIQUE constraint
- indexes [SQL Server], nonclustered
- nonclustered indexes [SQL Server], PRIMARY KEY constraint
ms.assetid: 9402029a-1227-46c4-93aa-c2122eb1b943
caps.latest.revision: 41
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 01ad2fc13ed2fba75e4c5971f06b59708868f659
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-nonclustered-indexes"></a>Erstellen nicht gruppierter Indizes
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Sie können nicht gruppierte Indizes in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]erstellen. Ein nicht gruppierter Index ist eine von den in einer Tabelle gespeicherten Daten getrennte Indexstruktur, durch die ausgewählte Spalten neu angeordnet werden. In vielen Fällen können Daten mithilfe von nicht gruppierten Indizes schneller gefunden werden als mit einer Suche in der zugrunde liegenden Tabelle. Mitunter lassen sich Abfragen vollständig mit den Daten im nicht gruppierten Index beantworten, oder der nicht gruppierte Index kann [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf die Zeilen in der zugrunde liegenden Tabelle verweisen. Im Allgemeinen werden nicht gruppierte Indizes erstellt, um die Leistung von häufig verwendeten Abfragen zu verbessern, die nicht vom gruppierten Index abgedeckt werden, oder Zeilen in einer Tabelle ohne gruppierten Index (als Heap bezeichnet) zu suchen. Sie können mehrere nicht gruppierte Indizes für eine Tabelle oder eine indizierte Sicht erstellen.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Implementations"></a> Typische Implementierungen  
 Nicht gruppierte Indizes werden auf folgende Weise implementiert:  
  
-   **UNIQUE-Einschränkungen**  
  
     Wenn Sie eine UNIQUE-Einschränkung erstellen, wird ein eindeutiger nicht gruppierter Index erstellt, um standardmäßig eine UNIQUE-Einschränkung zu erzwingen. Sie können einen eindeutigen gruppierten Index angeben, wenn noch kein gruppierter Index für die Tabelle vorhanden ist. Weitere Informationen finden Sie unter [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).  
  
-   **Index unabhängig von einer Einschränkung**  
  
     Wenn der gruppierte Index nicht angegeben wird, wird standardmäßig ein nicht gruppierter Index erstellt. Die maximale Anzahl nicht gruppierter Indizes, die pro Tabelle erstellt werden können, beträgt 999. Dies schließt alle Indizes ein, die durch PRIMARY KEY- oder UNIQUE-Einschränkungen erstellt wurden, jedoch keine XML-Indizes.  
  
-   **Nicht gruppierter Index für eine indizierte Sicht**  
  
     Nachdem ein eindeutiger gruppierter Index für eine Sicht erstellt wurde, können nicht gruppierte Indizes erstellt werden. Weitere Informationen finden Sie unter [Erstellen von indizierten Sichten](../../relational-databases/views/create-indexed-views.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht. Der Benutzer muss ein Mitglied der festen Serverrolle **sysadmin** bzw. der festen Datenbankrollen **db_ddladmin** und **db_owner** sein.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-create-a-nonclustered-index-by-using-the-table-designer"></a>So erstellen Sie einen nicht gruppierten Index mit dem Tabellen-Designer  
  
1.  Erweitern Sie im Objekt-Explorer die Datenbank mit der Tabelle, für die Sie einen nicht gruppierten Index erstellen möchten.  
  
2.  Erweitern Sie den Ordner **Tabellen** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die Tabelle, für die Sie einen nicht gruppierten Index erstellen möchten, und wählen Sie **Entwurf**aus.  
  
4.  Klicken Sie im Menü **Tabellen-Designer** auf **Indizes/Schlüssel**.  
  
5.  Klicken Sie im Dialogfeld **Indizes/Schlüssel** auf **Hinzufügen**.  
  
6.  Wählen Sie im Textfeld **Ausgewählter Primärschlüssel/eindeutiger Schlüssel oder Index** den neuen Index aus.  
  
7.  Wählen Sie im Raster **Als CLUSTERED erstellen**aus, und wählen Sie in der Dropdownliste rechts neben der Eigenschaft **Nein** aus.  
  
8.  Klicken Sie auf **Schließen**.  
  
9. Klicken Sie im Menü **Datei** auf **Speichern***Tabellenname*.  
  
#### <a name="to-create-a-nonclustered-index-by-using-object-explorer"></a>So erstellen Sie einen nicht gruppierten Index mit dem Objekt-Explorer  
  
1.  Erweitern Sie im Objekt-Explorer die Datenbank mit der Tabelle, für die Sie einen nicht gruppierten Index erstellen möchten.  
  
2.  Erweitern Sie den Ordner **Tabellen** .  
  
3.  Erweitern Sie die Tabelle, für die Sie einen nicht gruppierten Index erstellen möchten.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Ordner **Indizes** , zeigen Sie auf **Neuer Index**, und wählen Sie **Nicht gruppierter Index**aus.  
  
5.  Geben Sie in das Dialogfeld **Neuer Index** auf der Seite **Allgemein** den Namen des neuen Indexes in das Feld **Indexname** ein.  
  
6.  Klicken Sie unter **Indexschlüsselspalten**auf **Hinzufügen…**.  
  
7.  Aktivieren Sie im Dialogfeld **Spalten auswählen aus***Tabellenname* die Kontrollkästchen der Tabellenspalten, die dem nicht gruppierten Index hinzugefügt werden sollen.  
  
8.  Klicken Sie auf **OK**.  
  
9. Klicken Sie im Dialogfeld **Neuer Index** auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-a-nonclustered-index-on-a-table"></a>So erstellen Sie einen nicht gruppierten Index für eine Tabelle  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    -- Find an existing index named IX_ProductVendor_VendorID and delete it if found.   
    IF EXISTS (SELECT name FROM sys.indexes  
                WHERE name = N'IX_ProductVendor_VendorID')   
        DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;   
    GO  
    -- Create a nonclustered index called IX_ProductVendor_VendorID   
    -- on the Purchasing.ProductVendor table using the BusinessEntityID column.   
    CREATE NONCLUSTERED INDEX IX_ProductVendor_VendorID   
        ON Purchasing.ProductVendor (BusinessEntityID);   
    GO  
    ```  
  
## <a name="related-content"></a>Verwandte Inhalte  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
[Handbuch zum SQL Server Indexentwurf](../../relational-databases/sql-server-index-design-guide.md) 
