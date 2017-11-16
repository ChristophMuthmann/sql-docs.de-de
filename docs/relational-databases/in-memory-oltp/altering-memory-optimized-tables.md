---
title: "Ändern von speicheroptimierten Tabellen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 690b70b7-5be1-4014-af97-54e531997839
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 7d2dbe0bdc4cbd05f11eacf938b35a9c35ace2e7
ms.openlocfilehash: bd27f9755945abf7c09118a5997bb3745e66ab57
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="altering-memory-optimized-tables"></a>Ändern von speicheroptimierten Tabellen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Änderungen des Schemas und des Indizes in speicheroptimierten Tabellen können mithilfe der Anweisung ALTER TABLE durchgeführt werden. In SQL Server 2016 und Azure SQL-Datenbank sind ALTER TABLE-Vorgänge mit speicheroptimierte Tabellen OFFLINE, d.h., dass die Tabelle während des Vorgangs nicht abgefragt werden kann. Die Datenbankanwendung kann weiterhin ausgeführt werden, und jeder Vorgang, der auf die Tabellen zugreift, wird blockiert bis der Änderungsprozess abgeschlossen ist. Es ist mögliche, mehrere ADD-, DROP- und ALTER-Vorgänge in einer einzigen ALTER TABLE-Anweisung zu kombinieren.
  
## <a name="alter-table"></a>ALTER TABLE  
 
Die ALTER TABLE-Syntax wird für die Änderung des Tabellenschemas sowie zum Hinzufügen, Löschen und Neuerstellen von Indizes verwendet. Indizes werden als Teil der Tabellendefinition berücksichtigt:  
  
-   Die Syntax ALTER TABLE... ADD/DROP/ALTER INDEX wird nur für speicheroptimierte Tabelle unterstützt.  
  
-   Wenn keine ALTER TABLE-Anweisung verwendet wird, werden die Anweisungen CREATE INDEX, DROP INDEX und ALTER INDEX *nicht* für Indizes auf speicheroptimierten Tabellen unterstützt.  
  
 Nachfolgend sehen Sie die Syntax für die ADD, DROP und ALTER INDEX-Klauseln auf der Anweisung ALTER TABLE.  
  
```
| ADD   
     {   
        <column_definition>  
      | <table_constraint>  
      | <table_index>    
     } [ ,...n ]  
  
| DROP   
     {  
         [ CONSTRAINT ]   
         {   
              constraint_name   
         } [ ,...n ]  
         | COLUMN   
         {  
              column_name   
         } [ ,...n ]  
         | INDEX   
         {  
              index_name   
         } [ ,...n ]  
     } [ ,...n ]  
  
| ALTER INDEX index_name  
     {   
         REBUILD WITH ( <rebuild_index_option> )     
     }  
}  
```  
  
 Die folgenden Änderungsarten werden unterstützt.  
  
-   Ändern der Bucketanzahl  
  
-   Hinzufügen und Entfernen eines Indexes  
  
-   Ändern, Hinzufügen und Entfernen einer Spalte  
  
-   Hinzufügen und Entfernen einer Einschränkung  
  
 Weitere Informationen zu ALTER TABLE-Funktionen und die vollständige Syntax finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
## <a name="schema-bound-dependency"></a>Schemagebundene Abhängigkeit  
 Systemintern kompilierte gespeicherte Prozeduren müssen schemagebunden sein, d. h., sie haben eine schemagebundene Abhängigkeit zu den speicheroptimierten Tabellen, auf die sie zugreifen, und zu den Spalten, auf die sie verweisen. Eine schemagebundene Abhängigkeit ist eine Beziehung zwischen zwei Entitäten, mit der verhindert wird, dass die Entität, auf die verwiesen wird, gelöscht oder in einer inkompatiblen Art geändert wird, solange die verweisende Entität vorhanden ist.  
  
 Wird beispielsweise in einer schemagebundenen systemintern kompilierten gespeicherten Prozedur auf die Spalte *c1* aus der Tabelle *mytable*verwiesen, kann die Spalte *c1* nicht gelöscht werden. Entsprechend kann, wenn es eine solche Prozedur mit einer INSERT-Anweisung ohne Spaltenliste gibt (z. B. `INSERT INTO dbo.mytable VALUES (...)`) keine Spalte aus der Tabelle gelöscht werden.  
 
## <a name="logging-of-alter-table-on-memory-optimized-tables"></a>Protokollieren von ALTER TABLE bei speicheroptimierten Tabellen
Bei einer speicheroptimierten Tabelle werden die meisten ALTER TABLE-Szenarios nun parallel ausgeführt und tragen zu einer Optimierung der Schreibvorgänge in das Transaktionsprotokoll bei. Zur Optimierung werden nur die Metadatenänderungen in das Transaktionsprotokoll geschrieben. Die folgenden ALTER TABLE-Vorgänge werden als Singlethread ausgeführt und sind nicht protokolloptimiert.

Die Singlethreadvorgänge schreiben in diesem Fall den gesamten Inhalt der geänderten Tabelle in das Transaktionsprotokoll. Im Folgenden finden Sie eine Liste der Singlethread-Vorgänge:

- Ändern oder Hinzufügen einer Spalte, um einen LOB-Typ (Large Object) zu verwenden: nvarchar(max), varchar(max) oder varbinary(max).

- Hinzufügen oder Löschen eines Columnstore-Indexes.

- Fast jeder Vorgang, der sich auf eine [zeilenüberragende Spalte (off-row column)](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)auswirkt.

    - Sorgen Sie dafür, dass eine Spalte in der Zeile aus der Zeile verschoben wird.

    - Sorgen Sie dafür, dass eine Spalte außerhalb der Zeile in die Zeile verschoben wird.

    - Erstellen Sie eine neue Spalte außerhalb der Zeile.

    - *Ausnahme:* Ein Verlängern einer bereits zeilenüberragenden Spalte wird in der optimierten Weise protokolliert. 
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel ändert sich die Bucketanzahl eines vorhandenen Hashindexes. Dadurch wird der Hashindex mit der neuen Bucketanzahl neu erstellt, während andere Eigenschaften des Hashindexes unverändert bleiben.  
  
```tsql
ALTER TABLE Sales.SalesOrderDetail_inmem   
       ALTER INDEX imPK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID  
              REBUILD WITH (BUCKET_COUNT=67108864);  
GO
```
  
 Im folgenden Beispiel wird eine Spalte mit der Einschränkung NOT NULL und einer DEFAULT-Definition hinzugefügt, und WITH VALUES wird verwendet, um Werte für jede vorhandene Zeile der Tabelle bereitzustellen. Ohne WITH VALUES hat jede Zeile in der neuen Spalte den Wert NULL.  
  
```tsql  
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD Comment NVARCHAR(100) NOT NULL DEFAULT N'' WITH VALUES;  
GO
```  
  
 Im folgenden Beispiel wird einer vorhandenen Spalte eine Primärschlüsseleinschränkung hinzugefügt.  
  
```tsql
CREATE TABLE dbo.UserSession (   
   SessionId int not null,   
   UserId int not null,   
   CreatedDate datetime2 not null,   
   ShoppingCartId int,   
   index ix_UserId nonclustered hash (UserId) with (bucket_count=400000)   
)   
WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_ONLY) ;  
GO  
  
ALTER TABLE dbo.UserSession  
       ADD CONSTRAINT PK_UserSession PRIMARY KEY NONCLUSTERED (SessionId);  
GO
```  
  
 Im folgenden Beispiel wird ein Index entfernt.  
  
```tsql
ALTER TABLE Sales.SalesOrderDetail_inmem  
       DROP INDEX ix_ModifiedDate;  
GO
```  
  
 Im folgenden Beispiel wird ein Index hinzugefügt.  
  
```tsql  
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD INDEX ix_ModifiedDate (ModifiedDate);  
GO  
```  
  
 Im folgenden Beispiel werden mehrere Spalten hinzugefügt, mit einem Index und Einschränkungen.  
  
```tsql
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD    CustomerID int NOT NULL DEFAULT -1 WITH VALUES,  
              ShipMethodID int NOT NULL DEFAULT -1 WITH VALUES,  
              INDEX ix_Customer (CustomerID);  
GO  
```


<a name="logging-of-alter-table-on-memory-optimized-tables-124"></a>


## <a name="see-also"></a>Siehe auch  

[Speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  


