---
title: Object_id (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECT_ID
- OBJECT_ID_TSQL
dev_langs: TSQL
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
caps.latest.revision: "63"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: e9abb4a4556ca8ab83e638768ac95b9d7d637935
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="objectid-transact-sql"></a>OBJECT_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Datenbankobjekt-ID eines Objekts mit Schemabereich zurück.  
  
> [!IMPORTANT]  
>  Objekte, die keine Schemas als Bereiche besitzen, z. B. DDL-Trigger, können nicht mit OBJECT_ID abgefragt werden. Für Objekte, die in nicht gefunden werden die [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) Katalogsicht, die Objekt-IDs abrufen, indem Sie die entsprechende Katalogsicht Abfragen. Um die Objekt-ID eines DDL-Triggers zurückzugeben, verwenden Sie z. B. `SELECT OBJECT_ID FROM sys.triggers WHERE name = 'DatabaseTriggerLog``'`.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
OBJECT_ID ( '[ database_name . [ schema_name ] . | schema_name . ]   
  object_name' [ ,'object_type' ] )  
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Object_name* **"**  
 Ist das Objekt verwendet werden. *Object_name* handelt es sich um **Varchar** oder **Nvarchar**. Wenn *Object_name* ist **Varchar**, wird es implizit in konvertiert **Nvarchar**. Die Angabe des Datenbank- und des Schemanamens ist optional.  
  
 **"** *Object_type* **"**  
 Der Objekttyp mit Schemabereich. *Object_type* handelt es sich um **Varchar** oder **Nvarchar**. Wenn *Object_type* ist **Varchar**, wird es implizit in konvertiert **Nvarchar**. Eine Liste der Objekttypen, finden Sie unter der **Typ** Spalte [sys.objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="exceptions"></a>Ausnahmen  
 Für einen räumlichen Index gibt OBJECT_ID den Wert NULL zurück.  
  
 Gibt NULL zurück, bei einem Fehler.  
  
 Ein Benutzer kann nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass integrierte Funktionen (z. B. OBJECT_ID), die Metadaten ausgeben, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Parameter für eine Systemfunktion optional ist, wird von der aktuellen Datenbank, dem aktuellen Hostcomputer, dem aktuellen Serverbenutzer oder dem aktuellen Datenbankbenutzer ausgegangen. Auf integrierte Funktionen müssen immer runde Klammern folgen.  
  
 Wenn ein temporären Tabellennamen angegeben wird, muss der Datenbankname vor den Namen der temporären Tabelle stammen, wenn die aktuelle Datenbank ist **Tempdb**. Beispiel: `SELECT OBJECT_ID('tempdb..#mytemptable')`  
  
 Systemfunktionen können in der SELECT-Liste, in einer WHERE-Klausel und überall dort verwendet werden, wo ein Ausdruck zulässig ist. Weitere Informationen finden Sie unter [Ausdrücke &#40; Transact-SQL &#41; ](../../t-sql/language-elements/expressions-transact-sql.md) und [, auf dem &#40; Transact-SQL &#41; ](../../t-sql/queries/where-transact-sql.md).  
  
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
 Das folgende Beispiel gibt Informationen für alle Indizes und Partitionen der `Person.Address` -Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank mithilfe der [Sys. dm_db_index_operational_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md) Funktion.  
  
> [!IMPORTANT]  
>  Wenn Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen DB_ID und OBJECT_ID zum Zurückgeben eines Parameterwerts verwenden, sollten Sie immer sicherstellen, dass eine gültige ID zurückgegeben wird. Wenn der Datenbank- oder Objektname nicht gefunden werden kann, wenn sie z. B. nicht vorhanden oder fehlerhaft geschrieben sind, geben beide Funktionen NULL zurück. Die **Sys. dm_db_index_operational_stats** -Funktion interpretiert NULL als Platzhalterwert, der alle Datenbanken oder alle Objekte angibt. Da dies ein versehentlicher Vorgang sein kann, veranschaulichen die Beispiele in diesem Abschnitt, wie Sie auf sichere Weise Datenbank- und Objekt-IDs bestimmen.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-returning-the-object-id-for-a-specified-object"></a>D: Zurückgeben der ObjectID für ein angegebenes Objekt  
 Das folgende Beispiel gibt die Objekt-ID für die `FactFinance`-Tabelle in der [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]-Datenbank zurück.  
  
```  
SELECT OBJECT_ID(AdventureWorksPDW2012.dbo.FactFinance') AS 'Object ID';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys. dm_db_index_operational_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [Object_name &#40; Transact-SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)  
  
  

