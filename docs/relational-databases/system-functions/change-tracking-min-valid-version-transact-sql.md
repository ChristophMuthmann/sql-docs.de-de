---
title: CHANGE_TRACKING_MIN_VALID_VERSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_CLEANUP_VERSION
- CHANGE_TRACKING_CLEANUP_VERSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHANGE_TRACKING_MIN_VALID_VERSION
- change tracking [SQL Server], CHANGE_TRACKING_MIN_VALID_VERSION
ms.assetid: 5a43d23f-adcf-4c0b-95ad-07cee03c1f9d
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2c25e58c693602752865016758527bad67ad903b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="changetrackingminvalidversion-transact-sql"></a>CHANGE_TRACKING_MIN_VALID_VERSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die minimale Version auf dem Client, der zum Abrufen von änderungsnachverfolgungsinformationen aus der angegebenen Tabelle, bei der Verwendung gültig ist die [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) Funktion.  
    
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CHANGE_TRACKING_MIN_VALID_VERSION ( table_object_id )  
```  
  
## <a name="arguments"></a>Argumente  
 *table_object_id*  
 Ist die Objekt-ID der Tabelle an. *Table_object_id* ist ein **Int**.  
  
## <a name="return-type"></a>Rückgabetyp  
 **bigint**  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie diese Funktion zur Überprüfung des Werts, der die *Last_sync_version* -Parameters für CHANGETABLE. Wenn *Last_sync_version* ist kleiner als der Wert, der von dieser Funktion gemeldet wird, die Ergebnisse, die von einer späteren Aufruf von CHANGETABLE zurückgegeben werden möglicherweise nicht gültig.  
  
 CHANGE_TRACKING_MIN_VALID_VERSION verwendet die folgenden Informationen, um den Rückgabewert zu bestimmen:  
  
-   Wenn für die Tabelle die Änderungsnachverfolgung aktiviert ist.  
  
-   Wenn der Cleanuptask im Hintergrund ausgeführt wurde, um Änderungsnachverfolgungsinformationen zu entfernen, die älter als die für die Datenbank angegebene Beibehaltungsdauer sind.  
  
-   Wenn die Tabelle abgeschnitten wurde. Dadurch werden alle Änderungsnachverfolgungsinformationen entfernt, die der Tabelle zugeordnet sind.  
  
 Die Funktion gibt einen NULL-Fehler zurück, wenn eine der folgenden Bedingungen zutrifft:  
  
-   Die Änderungsnachverfolgung ist für die Datenbank nicht aktiviert.  
  
-   Die angegebene Tabellen-Objekt-ID ist für die aktuelle Datenbank nicht gültig.  
  
-   Es sind keine ausreichenden Berechtigungen für die von der Objekt-ID angegebene Tabelle vorhanden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ermittelt, ob eine angegebene Version eine gültige Version ist. In diesem Beispiel wird die minimal gültige Version für die Tabelle `dbo.Employees` abgerufen, und dieser Wert wird mit dem Wert der Variable `@last_sync_version` verglichen. Wenn der Wert von `@last_sync_version` kleiner als der Wert von `@min_valid_version` ist, dann ist die Liste der geänderten Zeilen nicht gültig.  
  
> [!NOTE]  
>  Normalerweise wird der Wert aus einer Tabelle oder aus einem anderen Speicherort abgerufen, in der bzw. in dem die letzte Versionsnummer gespeichert wurde, die zum Synchronisieren von Daten verwendet wurde.  
  
```  
-- The tracked change is tagged with the specified context   
DECLARE @min_valid_version bigint, @last_sync_version bigint;  
  
SET @min_valid_version =   
CHANGE_TRACKING_MIN_VALID_VERSION(OBJECT_ID('dbo.Employees'));  
  
SET @last_sync_version = 11  
IF (@last_sync_version < @min_valid_version)  
-- Error � do not obtain changes  
ELSE  
-- Obtain changes using CHANGETABLE(CHANGES ...)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Änderungsnachverfolgungsfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)  
  
  
