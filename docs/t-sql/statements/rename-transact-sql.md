---
title: RENAME (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/21/2018
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 0907cfd9-33a6-4fa6-91da-7d6679fee878
caps.latest.revision: ''
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1766a9e1dbe040ed120aaaf5d35fe0ab858c4e7a
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="rename-transact-sql"></a>RENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Benennt eine vom Benutzer erstellte Tabelle in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] um. Benennt eine vom Benutzer erstellte Tabelle oder Datenbank in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] um.  
  
> [!NOTE]  
>  Verwenden Sie zum Umbenennen einer Datenbank in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] [ALTER DATABASE (Azure SQL Data Warehouse](alter-database-azure-sql-data-warehouse.md).  Um eine Datenbank in Azure SQL-Datenbank umzubenennen, verwenden Sie die Anweisung [ALTER DATABASE (Azure SQL-Datenbank)](alter-database-azure-sql-database.md). Verwenden Sie die gespeicherte Prozedur [sp_renamedb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-renamedb-transact-sql.md), um eine Datenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] umzubenennen.
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for Azure SQL Data Warehouse  
  
-- Rename a table.  
RENAME OBJECT [::] [ [ database_name .  [schema_name ] ] . ] | [schema_name . ] ] table_name TO new_table_name  
[;]  
  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- Rename a table  
RENAME OBJECT [::] [ [ database_name . [ schema_name ] . ] | [ schema_name . ] ] table_name TO new_table_name  
[;]  
  
-- Rename a database  
RENAME DATABASE [::] database_name TO new_database_name  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 RENAME OBJECT [::] [ [*database_name* . [ *schema_name* ] . ] | [ *schema_name* . ] ]*table_name* TO *new_table_name*  
 **GILT FÜR:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Ändern Sie den Namen einer vom Benutzer erstellten Tabelle. Geben Sie die Tabelle an, die mit einem ein-, zwei-, oder dreiteiligen Namen umbenannt werden soll.    Geben Sie die neue Tabelle *new_table_name* als einteiligen Namen an.  
  
 RENAME DATABASE [::] [ *database_name* TO *new_database_name*  
 **GILT FÜR:**  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Ändern Sie den Namen einer benutzerdefinierten Datenbank von *database_name* in *new_database_name*.  Sie können bei der Umbenennung der Datenbank keine der folgenden reservierten [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Datenbanknamen verwenden:  
  
-   master  
  
-   model  
  
-   msdb  
  
-   tempdb  
  
-   pdwtempdb1  
  
-   pdwtempdb2  
  
-   DWConfiguration  
  
-   DWDiagnostics  
  
-   DWQueue  
  
## <a name="permissions"></a>Berechtigungen  
 Zur Ausführung dieses Befehls benötigen Sie folgende Berechtigung:  
  
-   **ALTER**-Berechtigung für die Tabelle  
   
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
  
### <a name="cannot-rename-an-external-table-indexes-or-views"></a>Externe Tabellen, Indizes oder Sichten können nicht umbenannt werden
Sie können keine externen Tabellen, Indizes oder Sichten umbenennen. Anstatt sie umzubenennen können Sie die externe Tabelle, den Index oder die Sicht löschen und dann mit dem neuen Namen erneut erstellen.

### <a name="cannot-rename-a-table-in-use"></a>Verwendete Tabelle kann nicht umbenannt werden  
 Sie können keine Tabellen oder Datenbanken umbenennen, während diese verwendet werden. Das Umbenennen einer Tabelle erfordert eine exklusive Sperre für die Tabelle. Wenn die Tabelle verwendet wird, müssen Sie möglicherweise die Sitzungen beenden, die die Tabelle verwenden. Zum Beenden einer Sitzung können Sie den KILL-Befehl nutzen. Verwenden Sie den KILL-Befehl mit Bedacht, da für nicht per Commit festgeschriebene Arbeit ein Rollback ausgeführt wird, wenn eine Sitzung beendet wird. Sitzungen in SQL Data Warehouse wird die „SID“ vorangestellt. Geben Sie 'SID' und die Sitzungsnummer ein, wenn Sie den KILL-Befehl aufrufen. Dieses Beispiel zeigt eine Liste der aktiven oder im Leerlauf befindlichen Sitzungen an und beendet dann die Sitzung „SID1234“.  
  
### <a name="views-are-not-updated"></a>Sichten werden nicht aktualisiert  
 Wenn Sie eine Datenbank umbenennen, werden alle Sichten ungültig, die den vorherigen Datenbanknamen verwenden. Dieses Verhalten gilt für Sichten innerhalb und außerhalb der Datenbank. Wenn z.B. die Sales-Datenbank umbenannt wird, wird eine Sicht ungültig, die `SELECT * FROM Sales.dbo.table1` enthält. Sie können dieses Problem beheben, indem Sie entweder keine dreiteiligen Namen in Sichten verwenden oder die Sichten aktualisieren, damit diese auf den neuen Datenbanknamen verweisen.  
  
 Beim Umbenennen einer Tabelle werden Sichten nicht aktualisiert, damit diese auf den neuen Tabellennamen verweisen. Jede Sicht (innerhalb oder außerhalb der Datenbank), die auf den vorherigen Tabellennamen verweist, wird ungültig. Zum Beheben dieses Problems können Sie alle Sichten aktualisieren, damit sie auf den neuen Tabellennamen verweisen.  
  
## <a name="locking"></a>Sperren  
 Das Umbenennen einer Tabelle erfordert eine gemeinsame Sperre für das DATABASE-Objekt und das SCHEMA-Objekt sowie eine exklusive Sperre für die Tabelle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-rename-a-database"></a>A. Umbenennen einer Datenbank  
 **GILT NUR FÜR:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 In diesem Beispiel wird die benutzerdefinierte Datenbank AdWorks in AdWorks2 umbenannt.  
  
```  
-- Rename the user defined database AdWorks  
RENAME DATABASE AdWorks to AdWorks2;  
  
```  
  
 Beim Umbenennen einer Tabelle werden alle Objekte und Eigenschaften aktualisiert, die der Tabelle zugeordnet sind, damit diese auf den neuen Tabellennamen verweisen. Es werden z.B. Tabellendefinitionen, Indizes, Einschränkungen und Berechtigungen aktualisiert. Sichten werden nicht aktualisiert.  
  
### <a name="b-rename-a-table"></a>B. Umbenennen einer Tabelle  
 **GILT FÜR:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 In diesem Beispiel wird die Tabelle Customer in Customer1 umbenannt.  
  
```  
-- Rename the customer table  
RENAME OBJECT Customer TO Customer1;  
  
RENAME OBJECT mydb.dbo.Customer TO Customer1;  
```  
  
 Beim Umbenennen einer Tabelle werden alle Objekte und Eigenschaften aktualisiert, die der Tabelle zugeordnet sind, damit diese auf den neuen Tabellennamen verweisen. Es werden z.B. Tabellendefinitionen, Indizes, Einschränkungen und Berechtigungen aktualisiert. Sichten werden nicht aktualisiert.  
   
  
### <a name="c-move-a-table-to-a-different-schema"></a>C. Verschieben einer Tabelle in ein anderes Schema  
 **GILT FÜR:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Wenn Sie beabsichtigen, das Objekt in ein anderes Schema zu verschieben, verwenden Sie [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md). Durch die folgende Anweisung wird z.B. das Tabellenelement aus dem product-Schema in das dbo-Schema verschoben.  
  
```  
ALTER SCHEMA dbo TRANSFER OBJECT::product.item;  
```  
  
### <a name="d-terminate-sessions-before-renaming-a-table"></a>D. Beenden von Sitzungen vor dem Umbenennen einer Tabelle  
 **GILT FÜR:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
 Es ist wichtig, zu beachten, dass Sie eine Tabelle nicht umbenennen können, während diese verwendet wird. Das Umbenennen einer Tabelle erfordert eine exklusive Sperre für die Tabelle. Wenn die Tabelle verwendet wird, müssen Sie möglicherweise die Sitzung beenden, die die Tabelle verwendet. Zum Beenden einer Sitzung können Sie den KILL-Befehl nutzen. Verwenden Sie den KILL-Befehl mit Bedacht, da für nicht per Commit festgeschriebene Arbeit ein Rollback ausgeführt wird, wenn eine Sitzung beendet wird. Sitzungen in SQL Data Warehouse wird die „SID“ vorangestellt. Sie müssen beim Aufruf des KILL-Befehls 'SID' und die Sitzungsnummer eingeben. Dieses Beispiel zeigt eine Liste der aktiven oder im Leerlauf befindlichen Sitzungen an und beendet dann die Sitzung „SID1234“.  
  
```  
-- View a list of the current sessions  
SELECT session_id, login_name, status   
FROM sys.dm_pdw_exec_sessions   
WHERE status='Active' OR status='Idle';  
  
-- Terminate a session using the session_id.  
KILL 'SID1234';  
```  
  
  
