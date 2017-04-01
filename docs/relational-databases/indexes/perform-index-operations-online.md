---
title: "Ausf&#252;hren von Onlineindexvorg&#228;ngen | Microsoft Docs"
ms.custom: ""
ms.date: "02/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-indexes"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Onlineindexvorgänge [SQL Server]"
  - "Onlineindexvorgänge"
  - "ONLINE (Option)"
ms.assetid: 1e43537c-bf67-4db3-9908-3cb45c6fdaa1
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Ausf&#252;hren von Onlineindexvorg&#228;ngen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie Indizes in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]online erstellen, neu erstellen oder löschen. Die ONLINE-Option ermöglicht, dass Benutzer während dieser Indexvorgänge gleichzeitig auf die dem Index zugrunde liegende Tabelle oder auf Daten eines gruppierten Indexes sowie auf alle eventuell damit verbundenen nicht gruppierten Indizes zugreifen können. Während beispielsweise ein gruppierter Index von einem Benutzer neu erstellt wird, kann dieser Benutzer – und alle anderen Benutzer – weiterhin die dem Index zugrunde liegenden Daten aktualisieren oder abfragen. Wenn Sie DDL-Vorgänge (Datendefinitionssprache) wie das Erstellen oder Neuerstellen eines gruppierten Indexes offline ausführen, richten diese Vorgänge exklusive Sperren für die dem Index zugrunde liegenden Daten und damit verbundene Indizes ein. Damit werden Änderungen und Abfragen der zugrunde liegenden Daten verhindert, bis der Indexvorgang abgeschlossen ist.  
  
> [!NOTE]  
>  Onlineindexvorgänge sind nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar. Weitere Informationen finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **Onlineneuerstellung eines Indexes mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Onlineindexvorgänge werden in Geschäftsumgebungen empfohlen, die rund um die Uhr und 7 Tage die Woche aktiv sind, für die also eine gleichzeitige Benutzeraktivität während Indexvorgängen unabdingbar ist.  
  
-   Die ONLINE-Option ist in folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen verfügbar:  
  
    -   [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)  
  
    -   [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)  
  
    -   [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)  
  
    -   [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) (zum Hinzufügen oder Löschen von UNIQUE- oder PRIMARY KEY-Einschränkungen mit der CLUSTERED-Indexoption)  
  
-   Weitere Einschränkungen und Einschränkungen im Zusammenhang mit der Onlineerstellung, -neuerstellung und -löschung von Indizes finden Sie unter [Richtlinien für Onlineindexvorgänge](../../relational-databases/indexes/guidelines-for-online-index-operations.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### Sie erstellen Sie einen Index online neu  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um die Datenbank mit der Tabelle zu erweitern, in der Sie einen Index online neu erstellen möchten.  
  
2.  Erweitern Sie den Ordner **Tabellen** .  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, für die Sie einen Index online neu erstellen möchten.  
  
4.  Erweitern Sie den Ordner **Indizes** .  
  
5.  Klicken Sie mit der rechten Maustaste auf den Index, den Sie online neu erstellen möchten, und wählen Sie **Eigenschaften** aus.  
  
6.  Wählen Sie unter **Seite auswählen**die Option **Optionen**aus.  
  
7.  Wählen Sie **DML-Onlineverarbeitung zulassen**aus, und wählen Sie dann in der Liste **True** aus.  
  
8.  Klicken Sie auf **OK**.  
  
9. Klicken Sie mit der rechten Maustaste auf den Index, den Sie online neu erstellen möchten, und wählen Sie **Neu erstellen** aus.  
  
10. Überprüfen Sie im Dialogfeld **Indizes neu erstellen** , dass der richtige Index im Raster **Neu zu erstellende Indizes** ausgewählt ist, und klicken sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So können Sie einen Index online erstellen, neu erstellen oder löschen  
  
1.  Stellen Sie im Objekt-Explorer ** **eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Im folgenden Beispiel wird ein vorhandener Index online neu erstellt.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER INDEX AK_Employee_NationalIDNumber ON HumanResources.Employee  
    REBUILD WITH (ONLINE = ON);  
    GO  
    ```  
  
     Im folgenden Beispiel wird ein gruppierter Index online gelöscht, und die daraus resultierende Tabelle (Heap) wird in die Dateigruppe `NewGroup` verschoben, wofür die `MOVE TO`-Klausel verwendet wird. Die Katalogsichten `sys.indexes`, `sys.tables`und `sys.filegroups` werden abgefragt, um die Platzierung von Index und Tabelle in den Dateigruppen vor und nach der Verschiebung zu prüfen.  
  
     [!code-sql[IndexDDL#DropIndex4](../../relational-databases/indexes/codesnippet/tsql/perform-index-operations_1.sql)]  
  
 Weitere Informationen finden Sie unter [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
  