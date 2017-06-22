---
title: Erstellen gruppierter Indizes | Microsoft Dokumentation
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
- index creation [SQL Server], clustered indexes
- clustered indexes, creating
- clustered indexes, PRIMARY KEY constraint
- clustered indexes, UNIQUE constraint
- indexes [SQL Server], clustered
ms.assetid: 47148383-c2c7-4f08-a9e4-7016bf2d1d13
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 309d0fa2603bfa14dc305b73036867c084eab683
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="create-clustered-indexes"></a>Erstellen gruppierter Indizes
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Sie können gruppierte Indizes für Tabellen mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] erstellen. Abgesehen von wenigen Ausnahmen sollte jede Tabelle über einen gruppierten Index verfügen. Ein gruppierter Index steigert nicht nur die Abfrageleistung, sondern kann bei Bedarf auch neu erstellt oder neu organisiert werden, um die Tabellenfragmentierung zu steuern. Ein gruppierter Index kann auch für eine Sicht erstellt werden. (Gruppierte Indizes sind im Thema [Beschreibung von gruppierten und nicht gruppierten Indizes](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)definiert.)  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Typische Implementierungen](#Implementations)  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **Erstellen eines gruppierten Indexes für eine Tabelle mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Implementations"></a> Typische Implementierungen  
 Gruppierte Indizes werden auf folgende Weise implementiert:  
  
-   **PRIMARY KEY- und UNIQUE-Einschränkungen**  
  
     Wenn Sie eine PRIMARY KEY-Einschränkung erstellen, wird automatisch ein eindeutiger gruppierter Index für die Spalte(n) erstellt, wenn noch kein gruppierter Index für die Tabelle vorhanden ist und Sie keinen eindeutigen nicht gruppierten Index angeben. Die Primärschlüsselspalte darf keine NULL-Werte zulassen.  
  
     Wenn Sie eine UNIQUE-Einschränkung erstellen, wird ein eindeutiger nicht gruppierter Index erstellt, um standardmäßig eine UNIQUE-Einschränkung zu erzwingen. Sie können einen eindeutigen gruppierten Index angeben, wenn noch kein gruppierter Index für die Tabelle vorhanden ist.  
  
     Ein Index, der als Bestandteil der Einschränkung erstellt wird, erhält automatisch denselben Namen wie die Einschränkung. Weitere Informationen finden Sie unter [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md) und [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md).  
  
-   **Index unabhängig von einer Einschränkung**  
  
     Sie können einen gruppierten Index für eine andere Spalte als die Primärschlüsselspalte erstellen, wenn eine nicht gruppierte Primärschlüsseleinschränkung angegeben wurde.  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Beim Erstellen einer gruppierten Indexstruktur wird Speicherplatz sowohl für die alte Struktur (Quelle) als auch für die neue Struktur (Ziel) in den jeweiligen Dateien und Dateigruppen benötigt. Die Speicherzuordnung für die alte Struktur wird erst dann aufgehoben, wenn die vollständige Transaktion abgeschlossen ist. Eventuell wird weiterer Speicherplatz temporär für Sortierzwecke benötigt. Weitere Informationen finden Sie unter [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
-   Wenn ein gruppierter Index in einem Heap mit mehreren nicht gruppierten Indizes erstellt wird, müssen alle nicht gruppierten Indizes neu erstellt werden, damit sie statt der Zeilen-ID (RID) den Gruppierungsschlüsselwert enthalten. Entsprechend gilt, dass beim Löschen eines gruppierten Indexes in einer Tabelle mit mehreren nicht gruppierten Indizes alle nicht gruppierten Indizes beim Ausführen der DROP-Anweisung neu erstellt werden. Dies kann bei umfangreichen Tabellen sehr lange dauern.  
  
     Beim Erstellen von Indizes für umfangreiche Tabellen sollten Sie möglichst mit dem gruppierten Index beginnen und dann die nicht gruppierten Indizes erstellen. Legen Sie gegebenenfalls die ONLINE-Option auf ON fest, wenn Sie Indizes für vorhandene Tabellen erstellen. Beim Wert ON werden keine lang andauernden Tabellensperren aufrechterhalten. Damit wird die Fortsetzung von Abfragen oder Updates für die zugrunde liegende Tabelle ermöglicht. Weitere Informationen finden Sie unter [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
-   Der Indexschlüssel eines gruppierten Indexes kann keine Spalten des Datentyps **varchar** enthalten, bei denen Daten in der Zuordnungseinheit ROW_OVERFLOW_DATA vorhanden sind. Wird ein gruppierter Index für eine **varchar**-Spalte erstellt, bei der in der Zuordnungseinheit IN_ROW_DATA Daten vorhanden sind, erzeugen alle nachfolgenden Einfügungen und Updates der Spalte einen Fehler, bei der diese Daten aus der Zeile entfernt werden. Zum Abrufen von Informationen zu Tabellen, die ggf. Daten mit Zeilenüberlauf enthalten, verwenden Sie die dynamische Verwaltungsfunktion [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht. Der Benutzer muss ein Mitglied der festen Serverrolle **sysadmin** bzw. der festen Datenbankrollen **db_ddladmin** und **db_owner** sein.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-create-a-clustered-index-by-using-object-explorer"></a>So erstellen Sie einen gruppierten Index mit dem Objekt-Explorer  
  
1.  Erweitern Sie im Objekt-Explorer die Tabelle, für die Sie einen gruppierten Index erstellen möchten.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Indizes** , zeigen Sie auf **Neuer Index**, und wählen Sie **Gruppierter Index**aus.  
  
3.  Geben Sie in das Dialogfeld **Neuer Index** auf der Seite **Allgemein** den Namen des neuen Indexes in das Feld **Indexname** ein.  
  
4.  Klicken Sie unter **Indexschlüsselspalten**auf **Hinzufügen…**.  
  
5.  Aktivieren Sie im Dialogfeld **Spalten auswählen aus***table_name* das Kontrollkästchen der Tabellenspalte, die dem gruppierten Index hinzugefügt werden soll.  
  
6.  Klicken Sie auf **OK**.  
  
7.  Klicken Sie im Dialogfeld **Neuer Index** auf **OK**.  
  
#### <a name="to-create-a-clustered-index-by-using-the-table-designer"></a>So erstellen Sie einen gruppierten Index mit dem Tabellen-Designer  
  
1.  Erweitern Sie im Objekt-Explorer die Datenbank, für die Sie eine Tabelle mit einem gruppierten Index erstellen möchten.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Tabellen** , und klicken Sie auf **Neue Tabelle**.  
  
3.  Erstellen Sie eine neue Tabelle. Weitere Informationen finden Sie unter [Verbindungsserver &#40;Datenbankmodul&#41;](../../relational-databases/tables/create-tables-database-engine.md).  
  
4.  Klicken Sie mit der rechten Maustaste auf die neue Tabelle, und klicken Sie auf **Entwurf**.  
  
5.  Klicken Sie im Menü **Tabellen-Designer** auf **Indizes/Schlüssel**.  
  
6.  Klicken Sie im Dialogfeld **Indizes/Schlüssel** auf **Hinzufügen**.  
  
7.  Wählen Sie im Textfeld **Ausgewählter Primärschlüssel/eindeutiger Schlüssel oder Index** den neuen Index aus.  
  
8.  Wählen Sie im Datenblatt **Als CLUSTERED erstellen**aus, und wählen Sie in der Dropdownliste rechts neben der Eigenschaft **Ja** aus.  
  
9. Klicken Sie auf **Schließen**.  
  
10. Klicken Sie im Menü **Datei** auf **Speichern***table_name*.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-a-clustered-index"></a>So erstellen Sie einen gruppierten Index  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Create a new table with three columns.  
    CREATE TABLE dbo.TestTable  
        (TestCol1 int NOT NULL,  
         TestCol2 nchar(10) NULL,  
         TestCol3 nvarchar(50) NULL);  
    GO  
    -- Create a clustered index called IX_TestTable_TestCol1  
    -- on the dbo.TestTable table using the TestCol1 column.  
    CREATE CLUSTERED INDEX IX_TestTable_TestCol1   
        ON dbo.TestTable (TestCol1);   
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Primärschlüsseln](../../relational-databases/tables/create-primary-keys.md)   
 [Erstellen von Unique-Einschränkungen](../../relational-databases/tables/create-unique-constraints.md)  
  
  

