---
title: CHANGETABLE (Transact-SQL) | Microsoft Docs
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
- CHANGETABLE_TSQL
- CHANGETABLE
dev_langs:
- TSQL
helpviewer_keywords:
- CHANGETABLE
- change tracking [SQL Server], CHANGETABLE
ms.assetid: d405fb8d-3b02-4327-8d45-f643df7f501a
caps.latest.revision: 34
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5023989a36f6118532dad0b110d03aaabf381242
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="changetable-transact-sql"></a>CHANGETABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Änderungsnachverfolgungsinformationen für eine Tabelle zurück. Sie können diese Anweisung verwenden, um alle Änderungen für eine Tabelle oder die Änderungsnachverfolgungsinformationen für eine bestimmte Zeile abzurufen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CHANGETABLE (  
    { CHANGES table , last_sync_version  
    | VERSION table , <primary_key_values> } )  
[AS] table_alias [ ( column_alias [ ,...n ] )  
  
<primary_key_values> ::=  
( column_name [ , ...n ] ) , ( value [ , ...n ] )  
```  
  
## <a name="arguments"></a>Argumente  
 ÄNDERUNGEN *Tabelle* , *Last_sync_version*  
 Gibt Nachverfolgungsinformationen für alle Änderungen an einer Tabelle, die seit der Version vorgenommen wurden, die angegebenen *Last_sync_version*.  
  
 *table*  
 Die benutzerdefinierte Tabelle, von der nachverfolgte Änderungen abgerufen werden sollen. Die Änderungsnachverfolgung muss für die Tabelle aktiviert sein. Es kann ein Tabellenname verwendet werden, der aus ein, zwei, drei oder vier Teilen besteht. Der Tabellenname kann synonym mit der Tabelle sein.  
  
 *last_sync_version*  
 Wenn Änderungen abgeufen werden, muss die aufrufende Anwendung den Punkt angeben, ab dem Änderungen erforderlich sind. Die last_sync_version gibt diesen Punkt an. Die Funktion gibt Informationen für alle Zeilen zurück, die ab dieser Version geändert worden sind. Die Anwendung fragt Änderungen mit einer größeren Versionsnummer als last_sync_version ab.  
  
 In der Regel, bevor sie Änderungen abruft, ruft die Anwendung **change_tracking_current_version()-Funktion** um die Version zu erhalten, die verwendet werden, die nächsten Mal Änderungen erforderlich sind. Deshalb muss die Anwendung den tatsächlichen Wert nicht interpretieren oder verstehen.  
  
 Da last_sync_version von der aufrufenden Anwendung abgerufen wird, muss die Anwendung den Wert persistent speichern. Wenn die Anwendung diesen Wert verliert, müssen Daten erneut initialisiert werden.  
  
 *Last_sync_version* ist **"bigint"**. Der Wert muss skalar sein. Ein Ausdruck verursacht einen Syntaxfehler.  
  
 Wenn der Wert NULL ist, werden alle nachverfolgten Änderungen zurückgegeben.  
  
 *Last_sync_version* , um sicherzustellen, dass es nicht zu alt ist, da einige oder alle Änderungsinformationen entsprechend der für die Datenbank konfigurierten Beibehaltungsdauer bereinigt wurden möglicherweise überprüft werden soll. Weitere Informationen finden Sie unter [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41; ](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md) und [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 VERSION *Tabelle*, {< Primary_key_values >}  
 Gibt die letzten Änderungsnachverfolgungsinformationen für eine angegebene Zeile zurück. Primärschlüsselwerte müssen die Zeile identifizieren. <primary_key_values> identifiziert die Primärschlüsselspalten und gibt die Werte an. Die Namen der Primärschlüsselspalten können in beliebiger Reihenfolge angegeben werden.  
  
 *Tabelle*  
 Die benutzerdefinierte Tabelle, von der Änderungsnachverfolgungsinformationen abgerufen werden sollen. Die Änderungsnachverfolgung muss für die Tabelle aktiviert sein. Es kann ein Tabellenname verwendet werden, der aus ein, zwei, drei oder vier Teilen besteht. Der Tabellenname kann synonym mit der Tabelle sein.  
  
 *column_name*  
 Gibt den Namen der Primärschlüsselspalte oder der Spalten an. Es können mehrere Spaltennamen in beliebiger Reihenfolge angegeben werden.  
  
 *Wert*  
 Der Wert des Primärschlüssels. Wenn mehrere Primärschlüsselspalten vorhanden sind, die Werte müssen angegeben werden in der gleichen Reihenfolge wie die Spalten angezeigt, in werden der *Column_name* Liste.  
  
 [AS] *Table_alias* [(*Spaltenalias* [,... *n* ])]  
 Stellt Namen für die Ergebnisse bereit, die von CHANGETABLE zurückgegeben werden.  
  
 *table_alias*  
 Der Aliasname der Tabelle, der von CHANGETABLE zurückgegeben wird. *Table_alias* ist erforderlich und muss ein gültiger [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 *column_alias*  
 Ein optionaler Spaltenalias oder eine Liste von Spaltenaliasnamen für die Spalten, die von CHANGETABLE zurückgegeben werden. Hierdurch können Spaltennamen angepasst werden, falls die Ergebnisse doppelte Namen aufweisen.  
  
## <a name="return-types"></a>Rückgabetypen  
 **table**  
  
## <a name="return-values"></a>Rückgabewerte  
  
### <a name="changetable-changes"></a>CHANGETABLE CHANGES  
 Wenn CHANGES angegeben wird, werden 0 oder mehr Zeilen, die die folgenden Spalten aufweisen, zurückgegeben.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|SYS_CHANGE_VERSION|**bigint**|Versionswert, der der letzten Änderung an der Zeile zugeordnet ist.|  
|SYS_CHANGE_CREATION_VERSION|**bigint**|Versionswerte, die dem letzten Einfügevorgang zugeordnet sind.|  
|SYS_CHANGE_OPERATION|**NCHAR(1)-Wert**|Gibt den Typ der Änderung an:<br /><br /> **U** = aktualisieren<br /><br /> **Ich** = einfügen<br /><br /> **D** = löschen|  
|SYS_CHANGE_COLUMNS|**varbinary(4100)**|Listet die Spalten auf, die sich seit last_sync_version (der Baseline) geändert haben. Beachten Sie, dass berechnete Spalten nie als geändert aufgelistet sind.<br /><br /> Der Wert ist NULL, wenn eine der folgenden Bedingungen zutrifft:<br /><br /> Die Änderungsnachverfolgung für Spalten ist nicht aktiviert.<br /><br /> Der Vorgang ist ein Einfüge- oder Löschvorgang.<br /><br /> Alle Nicht-Primärschlüsselspalten wurden in einem Vorgang aktualisiert. Dieser Binärwert sollte nicht direkt interpretiert werden. Verwenden Sie stattdessen zum Interpretieren [CHANGE_TRACKING_IS_COLUMN_IN_MASK()](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md).|  
|SYS_CHANGE_CONTEXT|**varbinary(128)**|Änderungskontextinformationen, die Sie optional angeben können, mit der [WITH](../../relational-databases/system-functions/with-change-tracking-context-transact-sql.md) -Klausel als Teil einer INSERT-, Update- oder DELETE-Anweisung.|  
|\<Wert der Primärschlüsselspalte >|Identisch mit den Benutzertabellenspalten.|Die Primärschlüsselwerte für die nachverfolgte Tabelle. Diese Werte identifizieren jede Zeile in der Benutzertabelle eindeutig.|  
  
### <a name="changetable-version"></a>CHANGETABLE VERSION  
 Wenn VERSION angegeben wird, wird eine Zeile, die die folgenden Spalten aufweist, zurückgegeben.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|SYS_CHANGE_VERSION|**bigint**|Wert der aktuellen Änderungsversion, der mit der Zeile verknüpft ist.<br /><br /> Der Wert ist NULL, wenn für einen längeren Zeitraum als der Beibehaltungsdauer für die Änderungsnachverfolgung keine Änderung vorgenommen wurde oder wenn die Zeile seit Aktivierung der Änderungsnachverfolgung nicht geändert wurde.|  
|SYS_CHANGE_CONTEXT|**varbinary(128)**|Änderungskontextinformationen, die optional angegeben werden können, indem Sie die WITH-Klausel als Teil einer INSERT-, UPDATE- oder DELETE-Anweisung verwenden.|  
|\<Wert der Primärschlüsselspalte >|Identisch mit den Benutzertabellenspalten.|Die Primärschlüsselwerte für die nachverfolgte Tabelle. Diese Werte identifizieren jede Zeile in der Benutzertabelle eindeutig.|  
  
## <a name="remarks"></a>Hinweise  
 Die CHANGETABLE-Funktion wird in der Regel in der FROM-Klausel einer Abfrage verwendet, so als handele es sich um eine Tabelle.  
  
## <a name="changetablechanges"></a>CHANGETABLE(CHANGES...)  
 Um Zeilendaten für neue oder geänderte Zeilen zu erhalten, verbinden Sie das Resultset mit der Benutzertabelle, indem Sie die Primärschlüsselspalten verwenden. Für jede Zeile in der Benutzertabelle, die geändert wurde, wird nur eine Zeile zurückgegeben, auch wenn es mehrere Änderungen an derselben Zeile seit wurden der *Last_sync_version* Wert.  
  
 Änderungen von Primärschlüsselspalten werden nie als Updates markiert. Wenn sich ein Primärschlüsselwert ändert, wird dies als Löschung des alten Werts und Einfügung des neuen Werts betrachtet.  
  
 Wenn Sie eine Zeile löschen und dann eine Zeile mit dem alten Primärschlüssel einfügen, wir die Änderung als Aktualisierung aller Spalten in der Zeile betrachtet.  
  
 Die Werte, die für die sys_change_operation-Spalte und SYS_CHANGE_COLUMNS-Spalte zurückgegeben werden, sind relativ zum Baseline (Last_sync_version), die angegeben wird. Z. B. wenn ein Einfügevorgang auf Version 10 und bei Version 15 ein Updatevorgang vorgenommen wurde und der Basislinie *Last_sync_version* 12 ist, wird ein Update gemeldet. Wenn die *Last_sync_version* -Wert 8 beträgt, wird eine Einfügung gemeldet. SYS_CHANGE_COLUMNS meldet berechnete Spalten nie als aktualisiert.  
  
 Im Allgemeinen werden alle Vorgänge, bei denen Daten in Benutzertabellen eingefügt, aktualisiert oder gelöscht werden, nachverfolgt, einschließlich der MERGE-Anweisung.  
  
 Die folgenden Vorgänge, die sich auf Benutzertabellendaten auswirken, werden nicht nachverfolgt:  
  
-   Ausführen der UPDATETEXT-Anweisung  
  
     Diese Anweisung ist veraltet und wird in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt. Es werden jedoch Änderungen nachverfolgt, die durch die Verwendung der .WRITE-Klausel der UPDATE-Anweisung vorgenommen werden.  
  
-   Löschen von Zeilen mit TRUNCATE TABLE  
  
     Wenn eine Tabelle abgeschnitten ist, werden die mit der Tabelle verknüpften Versionsinformationen der Änderungsnachverfolgung zurückgesetzt, als ob die Änderungsnachverfolgung gerade erst für die Tabelle aktiviert wurde. Eine Clientanwendung sollte immer die zuletzt synchronisierte Version überprüfen. Die Überprüfung schlägt fehl, wenn die Tabelle abgeschnitten wurde.  
  
## <a name="changetableversion"></a>CHANGETABLE(VERSION...)  
 Ein leeres Resultset wird zurückgegeben, wenn ein nicht vorhandener Primärschlüssel angegeben wird.  
  
 Der Wert von SYS_CHANGE_VERSION kann NULL sein, wenn für einen längeren Zeitraum als der Beibehaltungsdauer keine Änderung vorgenommen wurde (z. B. wenn die Änderungsinformationen durch ein Cleanup entfernt wurden) oder wenn die Zeile seit Aktivierung der Änderungsnachverfolgung für die Tabelle nicht geändert wurde.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die folgenden Berechtigungen für die Tabelle, die von angegeben wird die *Tabelle* Wert um änderungsnachverfolgungsinformationen abzurufen:  
  
-   SELECT-Berechtigung für die Primärschlüsselspalten  
  
-   VIEW CHANGE TRACKING  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-rows-for-an-initial-synchronization-of-data"></a>A. Zurückgeben von Zeilen für eine Erstsynchronisierung der Daten  
 Im folgenden Beispiel wird gezeigt, wie Daten für eine Erstsynchronisierung der Tabellendaten abgerufen werden. Die Abfrage gibt alle Zeilendaten und ihre zugehörigen Versionen zurück. Sie können diese Daten dann einfügen oder dem System hinzufügen, das die synchronisierten Daten enthalten soll.  
  
```sql  
-- Get all current rows with associated version  
SELECT e.[Emp ID], e.SSN, e.FirstName, e.LastName,  
    c.SYS_CHANGE_VERSION, c.SYS_CHANGE_CONTEXT  
FROM Employees AS e  
CROSS APPLY CHANGETABLE   
    (VERSION Employees, ([Emp ID], SSN), (e.[Emp ID], e.SSN)) AS c;  
```  
  
### <a name="b-listing-all-changes-that-were-made-since-a-specific-version"></a>B. Auflisten aller Änderungen, die seit einer bestimmten Version vorgenommen wurden  
 Im folgenden Beispiel werden alle Änderungen aufgelistet, die seit der angegebenen Version (`@last_sync_version)`) in der Tabelle vorgenommen wurden. [Emp-ID] und SSN ist Spalten in einem zusammengesetzten Primärschlüssel.  
  
```sql  
DECLARE @last_sync_version bigint;  
SET @last_sync_version = <value obtained from query>;  
SELECT [Emp ID], SSN,  
    SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION,  
    SYS_CHANGE_COLUMNS, SYS_CHANGE_CONTEXT   
FROM CHANGETABLE (CHANGES Employees, @last_sync_version) AS C;  
```  
  
### <a name="c-obtaining-all-changed-data-for-a-synchronization"></a>C. Abrufen aller geänderten Daten für eine Synchronisierung  
 Im folgenden Beispiel wird gezeigt, wie Sie alle geänderten Daten abrufen können. Diese Abfrage führt die Änderungsnachverfolgungsinformationen mit der Benutzertabelle zusammen, sodass Benutzertabelleninformationen zurückgegeben werden. Ein `LEFT OUTER JOIN` wird verwendet, damit eine Zeile für gelöschte Zeilen zurückgegeben wird.  
  
```sql  
-- Get all changes (inserts, updates, deletes)  
DECLARE @last_sync_version bigint;  
SET @last_sync_version = <value obtained from query>;  
SELECT e.FirstName, e.LastName, c.[Emp ID], c.SSN,  
    c.SYS_CHANGE_VERSION, c.SYS_CHANGE_OPERATION,  
    c.SYS_CHANGE_COLUMNS, c.SYS_CHANGE_CONTEXT   
FROM CHANGETABLE (CHANGES Employees, @last_sync_version) AS c  
    LEFT OUTER JOIN Employees AS e  
        ON e.[Emp ID] = c.[Emp ID] AND e.SSN = c.SSN;  
```  
  
### <a name="d-detecting-conflicts-by-using-changetableversion"></a>D. Erkennen von Konflikten mit CHANGETABLE(VERSION...)  
 Im folgenden Beispiel wird gezeigt, wie eine Zeile nur dann aktualisiert wird, wenn sie sich seit der letzten Synchronisierung nicht geändert hat. Die Versionsnummer der betreffenden Zeile wird mit `CHANGETABLE` abgerufen. Wenn die Zeile aktualisiert wurde, werden keine Änderungen vorgenommen, und die Abfrage gibt Informationen über die aktuelle Änderung der Zeile zurück.  
  
```sql  
-- @last_sync_version must be set to a valid value  
UPDATE  
    SalesLT.Product  
SET  
    ListPrice = @new_listprice  
FROM  
    SalesLT.Product AS P  
WHERE  
    ProductID = @product_id AND  
    @last_sync_version >= ISNULL (  
        (SELECT CT.SYS_CHANGE_VERSION FROM   
            CHANGETABLE(VERSION SalesLT.Product,  
            (ProductID), (P.ProductID)) AS CT),  
        0);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Änderungsnachverfolgungsfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [Nachverfolgen von Datenänderungen &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [CHANGE_TRACKING_IS_COLUMN_IN_MASK &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)   
 [CHANGE_TRACKING_CURRENT_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-current-version-transact-sql.md)   
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)  
  
  
