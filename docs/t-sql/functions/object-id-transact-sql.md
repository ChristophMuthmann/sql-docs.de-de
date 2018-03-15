---
title: OBJECT_ID (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECT_ID
- OBJECT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], IDs
- identification numbers [SQL Server], database objects
- checking object exists
- IDs [SQL Server], database objects
- OBJECT_ID function
- database objects [SQL Server], IDs
- displaying object IDs
- viewing object IDs
- verifying object exists
ms.assetid: f89286db-440f-4218-a828-30881ce3077a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4978a07401fa33e0244a61181e29cfd6146b695e
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="objectid-transact-sql"></a>OBJECT_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Datenbankobjekt-ID eines Objekts mit Schemabereich zurück.  
  
> [!IMPORTANT]  
>  Objekte, die keine Schemas als Bereiche besitzen, z. B. DDL-Trigger, können nicht mit OBJECT_ID abgefragt werden. Rufen Sie für Objekte, die nicht in der [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)-Katalogsicht gefunden werden, die Objekt-IDs ab, indem Sie die entsprechende Katalogsicht abfragen. Verwenden Sie z.B. `SELECT OBJECT_ID FROM sys.triggers WHERE name = 'DatabaseTriggerLog``'`, um die Objekt-ID eines DDL-Triggers zurückzugeben.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
OBJECT_ID ( '[ database_name . [ schema_name ] . | schema_name . ]   
  object_name' [ ,'object_type' ] )  
```  
  
## <a name="arguments"></a>Argumente  
 **'** *object_name* **'**  
 Das zu verwendende Objekt. *object_name* entspricht entweder dem Typ **varchar** oder **nvarchar**. Wenn *object_name* dem Typ **varchar** entspricht, wird eine implizite Konvertierung in **nvarchar** vorgenommen. Die Angabe des Datenbank- und des Schemanamens ist optional.  
  
 **'** *object_type* **'**  
 Der Objekttyp mit Schemabereich. *object_type* entspricht entweder dem Typ **varchar** oder **nvarchar**. Wenn *object_type* dem Typ **varchar** entspricht, wird eine implizite Konvertierung in **nvarchar** vorgenommen. Eine Liste von Objekttypen finden Sie in der Spalte **Typ** unter [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="exceptions"></a>Ausnahmen  
 Für einen räumlichen Index gibt OBJECT_ID den Wert NULL zurück.  
  
 Gibt bei einem Fehler NULL zurück.  
  
 Ein Benutzer kann nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass integrierte Funktionen (z. B. OBJECT_ID), die Metadaten ausgeben, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Remarks  
 Wenn der Parameter für eine Systemfunktion optional ist, wird von der aktuellen Datenbank, dem aktuellen Hostcomputer, dem aktuellen Serverbenutzer oder dem aktuellen Datenbankbenutzer ausgegangen. Auf integrierte Funktionen müssen immer runde Klammern folgen.  
  
 Wenn der Name einer temporären Tabelle angegeben wird, muss der Datenbankname vor diesem angegeben werden, es sei denn, die aktuelle Datenbank ist **tempdb**. Beispiel: `SELECT OBJECT_ID('tempdb..#mytemptable')`.  
  
 Systemfunktionen können in der SELECT-Liste, in einer WHERE-Klausel und überall dort verwendet werden, wo ein Ausdruck zulässig ist. Weitere Informationen finden Sie unter [Expressions &#40;Transact-SQL&#41; (Ausdrücke &#40;Transact-SQL&#41;)](../../t-sql/language-elements/expressions-transact-sql.md) und [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-object-id-for-a-specified-object"></a>A. Zurückgeben der Objekt-ID für ein angegebenes Objekt  
 Das folgende Beispiel gibt die Objekt-ID für die `Production.WorkOrder`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurück.  
  
```  
USE master;  
GO  
SELECT OBJECT_ID(N'AdventureWorks2012.Production.WorkOrder') AS 'Object ID';  
GO  
```  
  
### <a name="b-verifying-that-an-object-exists"></a>B. Überprüfen, ob ein Objekt vorhanden ist  
 Das folgende Beispiel überprüft das Vorhandensein einer angegebenen Tabelle, indem überprüft wird, ob die Tabelle eine Objekt-ID besitzt. Wenn die Tabelle vorhanden ist, wird sie gelöscht. Ist die Tabelle nicht vorhanden, wird die `DROP TABLE`-Anweisung nicht ausgeführt.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'dbo.AWBuildVersion', N'U') IS NOT NULL  
DROP TABLE dbo.AWBuildVersion;  
GO  
```  
  
### <a name="c-using-objectid-to-specify-the-value-of-a-system-function-parameter"></a>C. Angeben des Werts eines Systemfunktionsparameters mithilfe von OBJECT_ID  
 Im folgenden Beispiel werden Informationen zu allen Indizes und Partitionen der `Person.Address`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben. Dazu wird die [sys.dm_db_index_operational_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)-Funktion verwendet.  
  
> [!IMPORTANT]  
>  Wenn Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen DB_ID und OBJECT_ID zum Zurückgeben eines Parameterwerts verwenden, sollten Sie immer sicherstellen, dass eine gültige ID zurückgegeben wird. Wenn der Datenbank- oder Objektname nicht gefunden werden kann, wenn sie z. B. nicht vorhanden oder fehlerhaft geschrieben sind, geben beide Funktionen NULL zurück. Die **sys.dm_db_index_operational_stats**-Funktion interpretiert NULL als Platzhalterwert, der alle Datenbanken oder alle Objekte angibt. Da dies ein versehentlicher Vorgang sein kann, veranschaulichen die Beispiele in diesem Abschnitt, wie Sie auf sichere Weise Datenbank- und Objekt-IDs bestimmen.  
  
```  
DECLARE @db_id int;  
DECLARE @object_id int;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
IF @db_id IS NULL   
  BEGIN;  
    PRINT N'Invalid database';  
  END;  
ELSE IF @object_id IS NULL  
  BEGIN;  
    PRINT N'Invalid object';  
  END;  
ELSE  
  BEGIN;  
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);  
  END;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="d-returning-the-object-id-for-a-specified-object"></a>D: Zurückgeben der Objekt-ID für ein angegebenes Objekt  
 Das folgende Beispiel gibt die Objekt-ID für die `FactFinance`-Tabelle in der [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]-Datenbank zurück.  
  
```  
SELECT OBJECT_ID('AdventureWorksPDW2012.dbo.FactFinance') AS 'Object ID';  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Metadata Functions &#40;Transact-SQL&#41; (Metadatenfunktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)  
  
  

