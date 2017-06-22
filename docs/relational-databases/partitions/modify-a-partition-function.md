---
title: "Ändern einer Partitionsfunktion | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-partition
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae5bfc09-f27a-4ea9-9518-485278b11674
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2b55aa8c92aaf469aa2ef7945a84068301124641
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="modify-a-partition-function"></a>Ändern einer Partitionsfunktion
  Sie können Tabellen- oder Indexpartitionen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ändern, indem Sie mit [!INCLUDE[tsql](../../includes/tsql-md.md)]die angegebene Partitionsanzahl in Einerschritten in der Partitionsfunktion der partitionierten Tabelle bzw. des Indexes hinzufügen oder abziehen. Beim Hinzufügen einer Partition "teilen" Sie eine vorhandene Partition "auf" und definieren die Partitionsbegrenzungen erneut. Wenn Sie eine Partition löschen, "führen" Sie die Begrenzungen von zwei Partitionen "zusammen". Diese Aktion füllt eine Partition neu und belässt die andere Partition ohne Zuordnung.  
  
> [!CAUTION]  
>  Mehrere Tabellen oder Indizes können dieselbe Partitionsfunktion verwenden. Wenn Sie eine Partitionsfunktion ändern, wirkt sich dies auf alle Funktionen einer einzigen Transaktion aus. Überprüfen Sie die Abhängigkeiten der Partitionsfunktion, bevor Sie sie ändern.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So ändern Sie eine Partitionsfunktion mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   ALTER PARTITION FUNCTION kann nur verwendet werden, um eine Partition in zwei aufzuteilen bzw. um zwei Partitionen in eine zusammenzuführen. Um die Partitionierung von Tabellen bzw. Indizes zu ändern (beispielsweise von 10 in 5 Partitionen), können Sie eine der folgenden Optionen verwenden:  
  
    -   Erstellen Sie eine neue partitionierte Tabelle mit der gewünschten Partitionsfunktion, und fügen Sie dann die Daten aus der alten Tabelle in die neue Tabelle ein, indem Sie entweder eine INSERT INTO ... SELECT FROM [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder den **Assistenten zum Verwalten von Partitionen** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwenden.  
  
    -   Erstellen Sie einen partitionierten gruppierten Index für einen Heap.  
  
        > [!NOTE]  
        >  Das Löschen eines partitionierten gruppierten Index ergibt einen partitionierten Heap.  
  
    -   Verwenden Sie die CREATE INDEX-Anweisung von [!INCLUDE[tsql](../../includes/tsql-md.md)] mit der DROP EXISTING = ON-Klausel, um einen vorhandenen partitionierten Index zu löschen und neu zu erstellen.  
  
    -   Führen Sie eine Abfolge von ALTER PARTITION FUNCTION-Anweisungen aus.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird die Replikation beim Ändern einer Partitionsfunktion nicht unterstützt. Wenn Sie Änderungen an Partitionsfunktionen in der Veröffentlichungsdatenbank vornehmen möchten, müssen Sie diese manuell in der Abonnementdatenbank durchführen.  
  
-   Alle von ALTER PARTITION FUNCTION betroffenen Dateigruppen müssen online sein.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die folgenden Berechtigungen können zum Ausführen von ALTER PARTITION FUNCTION verwendet werden:  
  
-   ALTER ANY DATASPACE-Berechtigung. Diese Berechtigung gilt standardmäßig für Mitglieder der festen Serverrolle **sysadmin** und für Mitglieder der festen Datenbankrollen **db_owner** und **db_ddladmin** .  
  
-   Die Berechtigung CONTROL oder ALTER für die Datenbank, in der die Partitionsfunktion erstellt wurde.  
  
-   Die Berechtigung CONTROL SERVER oder ALTER ANY DATABASE auf dem Server der Datenbank, in der die Partitionsfunktion erstellt wurde.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 **So ändern Sie eine Partitionsfunktion:**  
  
 Diese spezielle Aktion kann nicht mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ausgeführt werden. Um eine Partitionsfunktion zu ändern, müssen Sie zuerst die Funktion löschen und dann mit dem Assistenten zum Erstellen von Partitionen eine neue Funktion mit den gewünschten Eigenschaften erstellen. Weitere Informationen finden Sie unter  
  
#### <a name="to-delete-a-partition-function"></a>So löschen Sie eine Partitionsfunktion  
  
1.  Erweitern Sie die Datenbank mit der zu löschenden Partitionsfunktion und dann den Ordner **Speicher** .  
  
2.  Erweitern Sie den Ordner **Partitionsfunktionen** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die Partitionsfunktion, die Sie löschen möchten, und klicken Sie dann auf **Löschen**.  
  
4.  Stellen Sie im Dialogfeld **Objekt löschen** sicher, dass die richtige Partitionsfunktion ausgewählt ist, und klicken Sie dann auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-split-a-single-partition-into-two-partitions"></a>So teilen Sie eine einzelne Partition in zwei Partitionen auf  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Look for a previous version of the partition function “myRangePF1” and deletes it if it is found.  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
        DROP PARTITION FUNCTION myRangePF1;  
    GO  
    -- Create a new partition function called “myRangePF1” that partitions a table into four partitions.  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    --Split the partition between boundary_values 100 and 1000  
    --to create two partitions between boundary_values 100 and 500  
    --and between boundary_values 500 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    SPLIT RANGE (500);  
    ```  
  
#### <a name="to-merge-two-partitions-into-one-partition"></a>So führen Sie zwei Partitionen zu einer Partition zusammen  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Look for a previous version of the partition function “myRangePF1” and deletes it if it is found.  
    IF EXISTS (SELECT * FROM sys.partition_functions  
        WHERE name = 'myRangePF1')  
        DROP PARTITION FUNCTION myRangePF1;  
    GO  
    -- Create a new partition function called “myRangePF1” that partitions a table into four partitions.  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES ( 1, 100, 1000 );  
    GO  
    --Merge the partitions between boundary_values 1 and 100  
    --and between boundary_values 100 and 1000 to create one partition  
    --between boundary_values 1 and 1000.  
    ALTER PARTITION FUNCTION myRangePF1 ()  
    MERGE RANGE (100);  
    ```  
  
 Weitere Informationen finden Sie unter [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md).  
  
  
