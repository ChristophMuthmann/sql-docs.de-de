---
title: TRUNCATE TABLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRUNCATE
- TRUNCATE TABLE
- TRUNCATE_TSQL
- TRUNCATE_TABLE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- row removal [SQL Server], TRUNCATE TABLE statement
- table truncating [SQL Server]
- removing rows
- TRUNCATE TABLE statement
- deleting rows
- dropping rows
ms.assetid: 3d544eed-3993-4055-983d-ea334f8c5c58
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 71f05b47a4a070e5d797a6f9ff6b5f4d88e585c5
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="truncate-table-transact-sql"></a>TRUNCATE TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entfernt alle Zeilen aus einer Tabelle oder die angegebenen Partitionen einer Tabelle ohne Protokollierung der einzelnen Zeilen löschen. TRUNCATE TABLE entspricht DELETE ohne WHERE-Klausel. TRUNCATE TABLE ist jedoch schneller und verwendet weniger Systemressourcen und Ressourcen für die Transaktionsprotokollierung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
TRUNCATE TABLE   
    [ { database_name .[ schema_name ] . | schema_name . } ]  
    table_name  
    [ WITH ( PARTITIONS ( { <partition_number_expression> | <range> }   
    [ , ...n ] ) ) ]  
[ ; ]  
  
<range> ::=  
<partition_number_expression> TO <partition_number_expression>  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
TRUNCATE TABLE [ { database_name . [ schema_name ] . | schema_name . ] table_name  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Tabelle gehört.  
  
 *table_name*  
 Der Name der Tabelle, die gekürzt werden soll oder aus der alle Zeilen entfernt werden. *TABLE_NAME* muss ein Literal sein. *TABLE_NAME* nicht mit der **OBJECT_ID()** -Funktion oder eine Variable.  
  
 MIT (PARTITIONEN ({ \< *Partition_number_expression*> | \< *Bereich*>} [,... ...n]))  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Gibt die Partitionen an, die abgeschnitten oder aus denen alle Zeilen entfernt werden sollen. Wenn die Tabelle nicht partitioniert ist, die **mit PARTITIONEN** Argument wird ein Fehler generiert. Wenn die **mit PARTITIONEN** -Klausel nicht angegeben ist, wird die gesamte Tabelle abgeschnitten werden.  
  
 *\<Partition_number_expression >* kann auf folgende Weise angegeben werden: 
  
-   Geben Sie die Nummer einer Partition, zum Beispiel:`WITH (PARTITIONS (2))`  
  
-   Geben Sie die Partitionsnummern mehrerer einzelner Partitionen durch Trennzeichen getrennt:`WITH (PARTITIONS (1, 5))`  
  
-   Geben Sie sowohl Bereiche als auch einzelne Partitionen an, beispielsweise:`WITH (PARTITIONS (2, 4, 6 TO 8))`  
  
-   *\<Bereich >* kann durch das Wort getrennte Partitionsnummern angegeben werden **TO**, beispielsweise:`WITH (PARTITIONS (6 TO 8))`  
  
 Um eine partitionierte Tabelle abschneiden, müssen die Tabelle und Indizes (für die gleiche Partitionsfunktion partitioniert) ausgerichtet werden.  
  
## <a name="remarks"></a>Hinweise  
 TRUNCATE TABLE bietet im Vergleich zur DELETE-Anweisung die folgenden Vorteile:  
  
-   Es wird weniger Speicherplatz für die Transaktionsprotokolle verwendet.  
  
     Die DELETE-Anweisung entfernt jede Zeile einzeln und protokolliert jede Löschung einzeln im Transaktionsprotokoll. Beim Entfernen der Daten mit TRUNCATE TABLE wird die Zuordnung der zur Speicherung der Tabellendaten verwendeten Datenseiten aufgehoben, und nur die Zuordnungsaufhebungen der Datenseiten werden im Transaktionsprotokoll aufgezeichnet.  
  
-   In der Regel werden weniger Sperren verwendet.  
  
     Wenn die DELETE-Anweisung mithilfe einer Zeilensperre ausgeführt wird, wird jede Zeile in der Tabelle zum Löschen gesperrt. Durch TRUNCATE TABLE werden immer die Tabelle (einschließlich einer Schemasperre (Sch-M)) und Seite, aber nicht jede Zeile gesperrt.  
  
-   Nullseiten verbleiben ausnahmslos in der Tabelle.  
  
     Nach dem Ausführen einer DELETE-Anweisung kann die Tabelle weiterhin leere Seiten enthalten. Die Zuordnung von leeren Seiten in einem Heap kann z. B. nur aufgehoben werden, wenn mindestens eine exklusive (LCK_M_X) Tabellensperre vorhanden ist. Wenn der Löschvorgang keine Tabellensperre verwendet, enthält die Tabelle (der Heap) viele leere Seiten. In Bezug auf Indizes können durch den Löschvorgang leere Seiten verbleiben, obwohl die Zuordnung dieser Seiten durch einen Cleanupprozess im Hintergrund schnell aufgehoben wird.  
  
 TRUNCATE TABLE entfernt alle Zeilen aus einer Tabelle, die Tabellenstruktur (Spalten, Einschränkungen, Indizes usw.) dagegen bleibt erhalten. Verwenden Sie die DROP TABLE-Anweisung, um neben den dazugehörigen Daten auch die Tabellendefinition zu entfernen.  
  
 Wenn die Tabelle eine Identitätsspalte enthält, wird der Zähler für diese Spalte auf den Ausgangswert zurückgesetzt, der für die Spalte definiert ist. Wenn kein Ausgangswert definiert wurde, wird der Standardwert 1 verwendet. Falls Sie den Wert des Identitätszählers erhalten möchten, verwenden Sie stattdessen DELETE.  
  
## <a name="restrictions"></a>Restrictions  
 Sie können TRUNCATE TABLE nicht für Tabellen verwenden, für die Folgendes gilt:  
  
-   Auf die Tabelle wird mit einer FOREIGN KEY-Einschränkung verwiesen. (Sie können eine Tabelle abschneiden, die einen Fremdschlüssel mit einem Verweis auf sich aufweist.)  
  
-   Die Tabelle ist an einer indizierten Sicht beteiligt.  
  
-   Die Veröffentlichung wird mithilfe einer Transaktionsreplikation oder Mergereplikation vorgenommen.  
  
 Verwenden Sie für Tabellen, die ein oder mehrere dieser Eigenschaften aufweisen, stattdessen die DELETE-Anweisung.  
  
 TRUNCATE TABLE kann keinen Trigger aktivieren, da der Vorgang keine einzelnen Zeilenlöschungen protokolliert. Weitere Informationen finden Sie unter [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md). 
 
 In [!INCLUDE[sssdwfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[sspdw](../../includes/sspdw-md.md)]:

- TRUNCATE TABLE ist in der EXPLAIN-Anweisung nicht zulässig.

- TRUNCATE TABLE kann nicht innerhalb einer Transaktion ausgeführt werden.
  
## <a name="truncating-large-tables"></a>Abschneiden von großen Tabellen  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügt über die Berechtigung zum Löschen oder Abschneiden von Tabellen, die mehr als 128 Blöcke haben, ohne simultane Sperren für alle für das Löschen erforderlichen Blöcke aufrechtzuerhalten.  
  
## <a name="permissions"></a>Berechtigungen  
 Die mindestens erforderliche Berechtigung ist ALTER für *Table_name*. Die Berechtigungen für TRUNCATE TABLE liegen standardmäßig beim Tabellenbesitzer, bei Mitgliedern der festen Serverrolle sysadmin und der festen Datenbankrollen db_owner und db_ddladmin. Die Berechtigungen sind nicht übertragbar. Sie können jedoch die TRUNCATE TABLE-Anweisung innerhalb eines Moduls einbinden, z. B. eine gespeicherte Prozedur, und mit der EXECUTE AS-Klausel für das Modul die passenden Berechtigungen erteilen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-truncate-a-table"></a>A. Abschneiden einer Tabelle  
 Im folgenden Beispiel werden alle Daten aus der `JobCandidate`-Tabelle entfernt. `SELECT`-Anweisungen werden vor und nach der `TRUNCATE TABLE`-Anweisung eingeschlossen, um die Ergebnisse zu vergleichen.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT COUNT(*) AS BeforeTruncateCount   
FROM HumanResources.JobCandidate;  
GO  
TRUNCATE TABLE HumanResources.JobCandidate;  
GO  
SELECT COUNT(*) AS AfterTruncateCount   
FROM HumanResources.JobCandidate;  
GO  
```  
  
### <a name="b-truncate-table-partitions"></a>B. Tabellenpartition abschneiden  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Im folgende Beispiel werden die angegebenen Partitionen einer partitionierten Tabelle abgeschnitten. Mit der Syntax `WITH (PARTITIONS (2, 4, 6 TO 8))` werden die Partitionen 2, 4, 6, 7 und 8 abgeschnitten.  
  
```sql  
TRUNCATE TABLE PartitionTable1   
WITH (PARTITIONS (2, 4, 6 TO 8));  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [DROP TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [IDENTITY &#40;Property&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
  
  

