---
title: DBCC CHECKCONSTRAINTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/14/2017
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
- DBCC CHECKCONSTRAINTS
- DBCC_CHECKCONSTRAINTS_TSQL
- CHECKCONSTRAINTS
- CHECKCONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC CHECKCONSTRAINTS statement
- consistency [SQL Server], constraints
- checking constraint consistency
- constraints [SQL Server], consistency checks
- integrity [SQL Server], constraints
ms.assetid: da6c9cee-6687-46e8-b504-738551f9068b
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2ff75ba3c32d138d9124eba5cfe170cf146d5778
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-checkconstraints-transact-sql"></a>DBCC CHECKCONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Überprüft die Integrität einer angegebenen Einschränkung oder aller Einschränkungen einer angegebenen Tabelle in der aktuellen Datenbank.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC CHECKCONSTRAINTS  
[   
    (   
    table_name | table_id | constraint_name | constraint_id   
    )  
]  
    [ WITH   
    [ { ALL_CONSTRAINTS | ALL_ERRORMSGS } ]  
    [ , ] [ NO_INFOMSGS ]   
    ]  
```  
  
## <a name="arguments"></a>Argumente  
 *table_name* | *table_id* | *constraint_name* | *constraint_id*  
 Die zu überprüfende Tabelle oder Einschränkung. Wenn *Table_name* oder *Table_id* wird angegeben, werden alle aktivierte Einschränkungen der Tabelle überprüft. Wenn *Constraint_name* oder *Constraint_id* wird angegeben, wird nur diese Einschränkung überprüft. Wenn weder ein Tabellenbezeichner noch ein Einschränkungsbezeichner angegeben ist, werden alle aktivierten Einschränkungen für alle Tabellen in der aktuellen Datenbank überprüft.  
 Durch den Einschränkungsnamen wird die zugehörige Tabelle eindeutig identifiziert. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 mit  
 Aktiviert anzugebende Optionen.  
  
 ALL_CONSTRAINTS  
 Überprüft alle aktivierten und deaktivierten Einschränkungen der Tabelle, wenn der Tabellenname angegeben ist oder wenn alle Tabellen überprüft werden. Andernfalls wird nur die aktivierte Einschränkung überprüft. ALL_CONSTRAINTS hat keine Wirkung, wenn ein Einschränkungsname angegeben ist.  
  
 ALL_ERRORMSGS  
 Gibt alle Zeilen zurück, die den Einschränkungen der überprüften Tabelle nicht entsprechen. Standardmäßig sind dies die ersten 200 Zeilen.  
  
 NO_INFOMSGS  
 Alle Informationsmeldungen werden unterdrückt.  
  
## <a name="remarks"></a>Hinweise  
DBCC CHECKCONSTRAINTS erstellt für alle FOREIGN KEY- und CHECK-Einschränkungen einer Tabelle eine Abfrage und führt sie aus.
  
Eine FOREIGN KEY-Abfrage sieht beispielsweise folgendermaßen aus:
  
```sql
SELECT <columns>  
FROM <table_being_checked> LEFT JOIN <referenced_table>  
    ON <table_being_checked.fkey1> = <referenced_table.pkey1>   
    AND <table_being_checked.fkey2> = <referenced_table.pkey2>  
WHERE <table_being_checked.fkey1> IS NOT NULL   
    AND <referenced_table.pkey1> IS NULL  
    AND <table_being_checked.fkey2> IS NOT NULL  
    AND <referenced_table.pkey2> IS NULL  
```  
  
Die Abfragedaten werden in einer temporären Tabelle gespeichert. Wenn alle geforderten Tabellen oder Einschränkungen überprüft wurden, wird das Resultset zurückgegeben.
DBCC CHECKCONSTRAINTS prüft die Integrität von FOREIGN KEY- und CHECK-Einschränkungen, aber nicht die Integrität der auf dem Datenträger gespeicherten Datenstrukturen einer Tabelle. Solche können ausgeführt werden, mithilfe von [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) und [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md).
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
Wenn *Table_name* oder *Table_id* angegeben ist und es für die versionsverwaltung durch das System aktiviert ist, führt DBCC CHECKCONSTRAINTS außerdem konsistenzprüfungen temporaler Daten für die angegebene Tabelle. Wenn *NO_INFOMSGS* nicht angegeben ist, wird dieser Befehl wird jeder Verstoß Konsistenz in der Ausgabe in einer separaten Zeile zurück. Das Format der Ausgabe werden ([pkcol1], [pkcol2]..) = (\<pkcol1_value >, \<pkcol2_value >...) UND \<Schwachpunkte durch temporale Tabellendatensatz >.
  
|Check|Zusätzliche Informationen in der Ausgabe, wenn Fehler bei der Überprüfung|  
|-----------|-----------------------------------------------|  
|PeriodEndColumn ≥ PeriodStartColumn (aktuell)|[sys_end] = '{0}' AND MAX(DATETIME2) = '9999-12-31 23:59:59.99999'|  
|PeriodEndColumn ≥ PeriodStartColumn (aktuell sind, Verlauf)|[sys_start] = '{0}' AND [sys_end] = '{1}'|  
|PeriodStartColumn < Current_utc_time (aktuell)|[Sys_start] = '{0}' und SYSUTCTIME|  
|PeriodEndColumn < Current_utc_time (Verlauf)|[sys_end] = '{0}' AND SYSUTCTIME|  
|(überlappungen)|(sys_start1 sys_end1), (sys_start2 sys_end2) für zwei überlappende Datensätze.<br /><br /> Wenn mehr als 2 überlappende Datensätze sind, müssen Ausgabe mehrere Zeilen jeder mit ein Paar von überlappt.|  
  
Es gibt keine Möglichkeit Constraint_name oder Constraint_id angeben, um nur temporale konsistenzprüfungen ausgeführt.
  
## <a name="result-sets"></a>Resultsets  
DBCC CHECKCONSTRAINTS gibt ein Rowset mit folgenden Spalten zurück.
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|Tabellenname|**varchar**|Der Name der Tabelle.|  
|Constraint Name|**varchar**|Name der verletzten Einschränkung.|  
|Erläuterungen|**varchar**|Spaltenwertzuweisungen, die die Zeile bzw. die Zeilen, die die Einschränkung verletzen, identifizieren.<br /><br /> Der Wert in dieser Spalte kann in einer WHERE-Klausel einer SELECT-Anweisung verwendet werden, die hinsichtlich Zeilen abfragt, die die Einschränkung verletzen.|  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner** .
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-checking-a-table"></a>A. Überprüfen einer Tabelle  
Im folgenden Beispiel wird die Einschränkungsintegrität der `Table1`-Tabelle in der `AdventureWorks`-Datenbank überprüft.
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE Table1 (Col1 int, Col2 char (30));  
GO  
INSERT INTO Table1 VALUES (100, 'Hello');  
GO  
ALTER TABLE Table1 WITH NOCHECK ADD CONSTRAINT chkTab1 CHECK (Col1 > 100);  
GO  
DBCC CHECKCONSTRAINTS(Table1);  
GO  
```  
  
### <a name="b-checking-a-specific-constraint"></a>B. Überprüfen einer bestimmten Einschränkung  
Im folgenden Beispiel wird die Integrität der `CK_ProductCostHistory_EndDate`-Einschränkung überprüft.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC CHECKCONSTRAINTS ('Production.CK_ProductCostHistory_EndDate');  
GO  
```  
  
### <a name="c-checking-all-enabled-and-disabled-constraints-on-all-tables"></a>C. Überprüfen aller aktivierten und deaktivierten Einschränkungen für alle Tabellen  
 Im folgenden Beispiel wird die Integrität aller aktivierten und deaktivierten Einschränkungen für alle Tabellen in der aktuellen Datenbank überprüft.  
  
```sql  
DBCC CHECKCONSTRAINTS WITH ALL_CONSTRAINTS;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
[DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
