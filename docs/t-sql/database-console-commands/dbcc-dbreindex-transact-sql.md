---
title: DBCC DBREINDEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC DBREINDEX
- DBREINDEX_TSQL
- DBREINDEX
- DBCC_DBREINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- index rebuilding [SQL Server]
- rebuilding indexes
- dynamic index rebuilding [SQL Server]
- DBCC DBREINDEX statement
ms.assetid: 6e929d09-ccb5-4855-a6af-b616022bc8f6
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 991c16eea9a651270ca299e72cafbc822465a9b3
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-dbreindex-transact-sql"></a>DBCC DBREINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Erstellt ein oder mehrere Indizes einer Tabelle in der angegebenen Datenbank neu.
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Verwendung [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) stattdessen.  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC DBREINDEX   
(   
    table_name   
    [ , index_name [ , fillfactor ] ]  
)  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>Argumente  
 *table_name*  
 Der Name der Tabelle, die den angegebenen Index oder die Indizes enthält, die neu zu erstellen sind. Tabellennamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md)*.*  
  
 *index_name*  
 Der Name des neu zu erstellenden Indexes. Indexnamen müssen den Regeln für Bezeichner entsprechen. Wenn *index_name* angegeben wird, muss auch *table_name* angegeben werden. Wenn *index_name* nicht oder als " " angegeben wird, werden alle Indizes für die Tabelle neu erstellt.  
  
 *fillfactor*  
 Der Prozentsatz an Speicherplatz auf jeder Indexseite, der beim Erstellen oder Neuerstellen des Indexes zum Speichern von Daten verwendet werden soll. *fillfactor* ersetzt den ursprünglichen Füllfaktor als neuer Standardwert für den Index und für alle nicht gruppierten Indizes, die neu erstellt werden, weil ein gruppierter Index neu erstellt wird.  
 Wenn *fillfactor* 0 ist, verwendet DBCC DBREINDEX den für den Index zuletzt angegebenen Füllfaktorwert. Dieser Wert wird in der **sys.indexes** -Katalogsicht gespeichert.   
 Wenn *fillfactor* angegeben wird, müssen auch *table_name* und *index_name* angegeben werden. Wenn *fillfactor* nicht angegeben wird, wird der Standardfüllfaktor, 100, verwendet. Weitere Informationen finden Sie unter [Angeben des Füllfaktors für einen Index](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
 WITH NO_INFOMSGS  
 Unterdrückt alle Informationsmeldungen mit einem Schweregrad von 0 bis 10.  
  
## <a name="remarks"></a>Hinweise  
Die DBCC DBREINDEX-Anweisung erstellt einen Index oder alle Indizes für eine Tabelle neu. Aufgrund der Möglichkeit, Indizes dynamisch neu zu erstellen, können Indizes mit PRIMARY KEY- oder UNIQUE-Einschränkungen neu erstellt werden, ohne diese Einschränkungen zu löschen und neu zu erstellen. Das heißt, ein Index kann neu erstellt werden, ohne die Struktur einer Tabelle oder deren Einschränkungen zu kennen. Dies kann nach dem Massenkopieren von Daten in die Tabelle der Fall sein.

DBCC DBREINDEX kann alle Indizes für eine Tabelle in einer einzelnen Anweisung neu erstellen. Dies ist einfacher, als mehrere DROP INDEX- und CREATE INDEX-Anweisungen zu codieren. Da die Arbeit von einer Anweisung ausgeführt wird, ist DBCC DBREINDEX automatisch atomar. Einzelne DROP INDEX- und CREATE INDEX-Anweisungen müssen dagegen in eine Transaktion eingebunden werden, um atomar zu sein. Außerdem bietet DBCC DBREINDEX mehr Optimierungen, als bei einzelnen DROP INDEX- und CREATE INDEX-Anweisungen möglich wären.

Im Gegensatz zu DBCC INDEXDEFRAG, oder ALTER INDEX mit der Option REORGANIZE, ist DBCC DBREINDEX ein Offlinevorgang. Wenn ein nicht gruppierter Index neu erstellt wird, wird für die Dauer des Vorgangs eine freigegebene Sperre für die betreffende Tabelle eingerichtet. Dadurch werden Änderungen an der Tabelle verhindert. Falls der gruppierte Index neu erstellt wird, wird eine exklusive Tabellensperre eingerichtet. Dadurch wird jeglicher Tabellenzugriff verhindert, wodurch die Tabelle offline ist. Verwenden Sie die ALTER INDEX REBUILD-Anweisung mit der Option ONLINE, um eine Indexneuerstellung online auszuführen, oder um den Grad an Parallelität während des Indexneuerstellungsvorgangs zu steuern.

Weitere Informationen zum Auswählen einer Methode zum Neuerstellen oder Neuorganisieren eines Indexes finden Sie unter [Neuorganisieren und Neuerstellen von Indizes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md) .
  
## <a name="restrictions"></a>Einschränkungen  
Die Verwendung von DBCC DBREINDEX wird für die folgenden Objekte nicht unterstützt.
-   Systemtabellen  
-   Räumlichkeitsindizes  
-   Speicheroptimierte xVelocity-columnstore-Indizes  
  
## <a name="result-sets"></a>Resultsets  
Unabhängig davon, ob NO_INFOMSGS angegeben wurde oder nicht (der Tabellenname muss angegeben werden), gibt DBCC DBREINDEX immer Folgendes zurück:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Berechtigungen  
Bei dem Aufrufer muss es sich um den Besitzer der Tabelle oder um ein Mitglied der festen Serverrolle **sysadmin** , der festen Datenbankrolle **db_owner** oder der festen Datenbankrolle **db_ddladmin** handeln.
  
## <a name="examples"></a>Beispiele  
### <a name="a-rebuilding-an-index"></a>A. Neuerstellen eines Index  
Im folgenden Beispiel wird der gruppierte Index `Employee_EmployeeID` mit einem Füllfaktor von `80` in der `Employee` -Tabelle der `AdventureWorks` -Datenbank neu erstellt.
  
```sql  
USE AdventureWorks2012;   
GO  
DBCC DBREINDEX ('HumanResources.Employee', PK_Employee_BusinessEntityID,80);  
GO  
```  
  
### <a name="b-rebuilding-all-indexes"></a>B. Neuerstellen aller Indizes  
Im folgenden Beispiel werden alle Indizes für die `Employee` -Tabelle der `AdventureWorks` -Datenbank mit dem Füllfaktorwert `70`neu erstellt.
  
```sql
USE AdventureWorks2012;   
GO  
DBCC DBREINDEX ('HumanResources.Employee', ' ', 70);  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
  

