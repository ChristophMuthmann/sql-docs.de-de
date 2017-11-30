---
title: Sys. dm_db_objects_disabled_on_compatibility_level_change (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_objects_disabled_on_compatibility_level_change
- dm_db_objects_disabled_on_compatibility_level_change_TSQL
- sys.dm_db_objects_disabled_on_compatibility_level_change
- sys.dm_db_objects_disabled_on_compatibility_level_change_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_objects_disabled_on_compatibility_level_change catalog view
ms.assetid: a5d70064-0330-48b9-b853-01eba50755d0
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bafca706c9fa8aa1f90bfb38b16df067c317a475
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spatial-data---sysdmdbobjectsdisabledoncompatibilitylevelchange"></a>Räumliche Daten - Sys. dm_db_objects_disabled_on_compatibility_level_change
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Führt die Indizes und Einschränkungen, die als Ergebnis der Änderung des Kompatibilitätsgrads in deaktiviert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Indizes und Einschränkungen, die persistierte berechnete Spalten enthalten, deren Ausdrücke räumliche UDTs verwenden, werden nach einem Upgrade oder einer Änderung des Kompatibilitätsgrads deaktiviert. Bestimmen Sie die Auswirkungen einer Änderung des Kompatibilitätsgrads mithilfe dieser dynamischen Verwaltungsfunktion.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
sys.dm_db_objects_disabled_on_compatibility_level_change ( compatibility_level )   
```  
  
##  <a name="Arguments"></a> Argumente  
 *COMPATIBILITY_LEVEL*  
 **Int** , die den Kompatibilitätsgrad angibt, die Sie festlegen möchten.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Klasse**|**int**|1 = Einschränkungen<br /><br /> 7 = Indizes und Heaps|  
|**class_desc**|**nvarchar(60)**|OBJECT oder COLUMN für Einschränkungen<br /><br /> INDEX für Indizes und Heaps|  
|**major_id**|**int**|OBJECT ID der Einschränkungen<br /><br /> OBJECT ID der Tabelle, die Indizes und Heaps enthält|  
|**minor_id**|**int**|NULL für Einschränkungen<br /><br /> Index_id für Indizes und Heaps|  
|**Abhängigkeit**|**nvarchar(60)**|Beschreibung der Abhängigkeit, die bewirkt, dass die Einschränkung oder der Index deaktiviert wird. Die gleichen Werte werden auch in den Warnungen verwendet, die während des Upgrades ausgelöst werden. Einige Beispiele dafür sind:<br /><br /> "space" für eine systeminterne Funktion<br /><br /> "geometry" für einen System-UDT<br /><br /> "geography::Parse" für eine Methode eines System-UDTs|  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Persistente berechnete Spalten, die systeminterne Funktionen verwenden, werden bei einer Änderung des Kompatibilitätsgrads deaktiviert. Darüber hinaus werden persistierte berechnete Spalten, die eine Geometry-Methode oder Geography-Methode verwenden, beim Upgrade einer Datenbank deaktiviert.  
  
### <a name="which-functions-cause-persisted-computed-columns-to-be-disabled"></a>Welcher Funktionen haben eine Deaktivierung von persistierten berechneten Spalten zur Folge?  
 Wenn die folgenden Funktionen im Ausdruck einer persistierten berechneten Spalte verwendet werden, bewirken sie, dass Indizes und Einschränkungen, die auf diese Spalten verweisen, bei einer Änderung des Kompatibilitätsgrads von 80 auf 90 deaktiviert werden:  
  
-   **IsNumeric**  
  
 Wenn die folgenden Funktionen im Ausdruck einer persistierten berechneten Spalte verwendet werden, bewirken sie, dass Indizes und Einschränkungen, die auf diese Spalten verweisen, bei einer Änderung des Kompatibilitätsgrads von 100 auf 110 oder höher deaktiviert werden:  
  
-   **SOUNDEX**  
  
-   **Geografie:: GeomFromGML**  
  
-   **Geografie:: STGeomFromText**  
  
-   **Geografie:: STLineFromText**  
  
-   **Geografie:: STPolyFromText**  
  
-   **Geografie:: STMPointFromText**  
  
-   **Geografie:: STMLineFromText**  
  
-   **Geografie:: STMPolyFromText**  
  
-   **Geografie:: STGeomCollFromText**  
  
-   **Geografie:: STGeomFromWKB**  
  
-   **Geografie:: STLineFromWKB**  
  
-   **Geografie:: STPolyFromWKB**  
  
-   **Geografie:: STMPointFromWKB**  
  
-   **Geografie:: STMLineFromWKB**  
  
-   **Geografie:: STMPolyFromWKB**  
  
-   **Geografie:: STUnion**  
  
-   **Geografie:: STIntersection**  
  
-   **Geografie:: STDifference**  
  
-   **Geografie:: STSymDifference**  
  
-   **Geografie:: STBuffer**  
  
-   **Geografie:: BufferWithTolerance**  
  
-   **Geography:: Parse**  
  
-   **Geografie:: reduzieren**  
  
### <a name="behavior-of-the-disabled-objects"></a>Verhalten der deaktivierten Objekte  
 **Indizes**  
  
 Wenn der gruppierte Index deaktiviert ist, oder ein nicht gruppierter Index erzwungen wird, wird der folgende Fehler ausgelöst: "der Abfrageprozessor kann keinen Plan erstellen, da der Index ' %. \*ls für die Tabelle oder Sicht ' %. \*ls deaktiviert ist. " Um diese Objekte erneut zu aktivieren, erstellen Sie die Indizes nach dem Upgrade durch Aufruf **ALTER INDEX ON... REBUILD**.  
  
 **Heaps**  
  
 Wenn eine Tabelle mit einem deaktivierten Heap verwendet wird, wird der folgende Fehler ausgelöst. Um diese Objekte erneut zu aktivieren, erstellen Sie nach dem Upgrade durch Aufruf **ALTER INDEX alle ON... REBUILD**.  
  
```  
// ErrorNumber: 8674  
// ErrorSeverity: EX_USER  
// ErrorFormat: The query processor is unable to produce a plan because the table or view '%.*ls' is disabled.  
// ErrorCause: The table has a disabled heap.   
// ErrorCorrectiveAction: Rebuild the disabled heap to enable it.   
// ErrorInserts: table or view name   
// ErrorOwner: mtintor   
// ErrorFirstProduct: SQL11  
```  
  
 Wenn Sie versuchen, die während eines Onlinevorgangs den Heap neu zu erstellen, wird ein Fehler ausgelöst.  
  
 **CHECK-Einschränkungen und Fremdschlüssel**  
  
 Deaktivierte CHECK-Einschränkungen und Fremdschlüssel lösen keinen Fehler aus. Die Einschränkungen werden jedoch nicht erzwungen, wenn Zeilen geändert werden. Um diese Objekte erneut zu aktivieren, überprüfen Sie die Einschränkungen nach der Aktualisierung durch Aufrufen von **ALTER TABLE... CHECK-Einschränkung**.  
  
 **Persistente berechnete Spalten**  
  
 Da eine Deaktivierung einzelner Spalten nicht möglich ist, wird die gesamte Tabelle deaktiviert, indem der gruppierte Index oder der Heap deaktiviert wird.  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird eine Abfrage für **sys.dm_db_objects_disabled_on_compatibility_level_change** angezeigt, durch die Objekte gesucht werden, auf die sich eine Änderung des Kompatibilitätsgrads in 120 auswirkt.  
  
```tsql  
SELECT * FROM sys.dm_db_objects_disabled_on_compatibility_level_change(120);  
GO  
  
```  
  
  
