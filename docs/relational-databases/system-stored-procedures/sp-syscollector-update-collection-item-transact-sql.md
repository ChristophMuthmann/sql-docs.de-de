---
title: Sp_syscollector_update_collection_item (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_item
- sp_syscollector_update_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_update_collection_item
ms.assetid: 7a0d36c8-c6e9-431d-a5a4-6c1802bce846
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 79232a6bdbc4c56bc52b559a715efb1b9f63e6b9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spsyscollectorupdatecollectionitem-transact-sql"></a>sp_syscollector_update_collection_item (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wird verwendet, um die Eigenschaften eines benutzerdefinierten Sammelelements zu ändern oder um ein benutzerdefiniertes Sammelelement umzubenennen.  
  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syscollector_update_collection_item   
      [ [ @collection_item_id = ] collection_item_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @frequency = ] frequency ]  
    , [ [ @parameters = ] 'parameters' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @collection_item_id = ] *collection_item_id*  
 Ist der eindeutige Bezeichner, der das sammelelement identifiziert. *Collection_item_id* ist **Int** hat den Standardwert NULL. *Collection_item_id* muss einen Wert aufweisen, wenn *Namen* ist NULL.  
  
 [ @name =] '*Namen*"  
 Der Name des Sammelelements. *Namen* ist **Sysname** hat den Standardwert NULL. *Namen* muss einen Wert aufweisen, wenn *Collection_item_id* ist NULL.  
  
 [ @new_name =] '*New_name*"  
 Der neue Name für das Sammelelement. *New_name* ist **Sysname**, und kann nicht verwendet, eine leere Zeichenfolge sein.  
  
 *New_name* muss eindeutig sein. Wenn Sie eine Liste der aktuellen Namen von Sammelelementen abrufen möchten, fragen Sie die syscollector_collection_items-Systemsicht ab.  
  
 [ @frequency =] *Häufigkeit*  
 Die Häufigkeit (in Sekunden), mit der Daten durch dieses Sammelelement aufgezeichnet werden. *Häufigkeit* ist **Int**, hat den Standardwert 5. Dies ist der Minimalwert, der angegeben werden können.  
  
 [ @parameters =] '*Parameter*"  
 Die Eingabeparameter für das Sammelelement. *Parameter* ist **Xml** hat den Standardwert NULL. Die *Parameter* Schema muss das Schema für Parameter des sammlertyps entspricht.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Sammlungssatz auf den Modus ohne Zwischenspeicherung festgelegt ist, werden Änderungen der Häufigkeit ignoriert, da dieser Modus bewirkt, dass sowohl die Datensammlung als auch der Datenupload dem Zeitplan entsprechend stattfinden, der für den Sammlungssatz angegeben wurde. Zum Anzeigen des Status des Sammlungssatzes führen Sie die folgende Abfrage aus. Ersetzen Sie `<collection_item_id>` durch die ID des zu aktualisierenden Sammelelements.  
  
```  
USE msdb;  
GO  
SELECT cs.collection_set_id, collection_set_uid, cs.name   
    ,'is running' = CASE WHEN is_running =  0 THEN 'No' ELSE 'Yes' END  
    ,'cache mode' = CASE WHEN collection_mode = 0 THEN 'Cached mode' ELSE 'Non-cached mode' END  
FROM syscollector_collection_sets AS cs  
JOIN syscollector_collection_items AS ci   
ON ci.collection_set_id = cs.collection_set_id  
WHERE collection_item_id = <collection_item_id>;  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Damit dieser Vorgang ausgeführt werden kann, ist die Mitgliedschaft in der festen Datenbankrolle dc_admin oder dc_operator (mit EXECUTE-Berechtigung) erforderlich. Obwohl die dc_operator-Rolle diese gespeicherte Prozedur ausführen kann, können die Eigenschaften von den Mitgliedern dieser Rolle nur begrenzt geändert werden. Die folgenden Eigenschaften können nur von dc_admin geändert werden:  
  
-   @new_name  
  
-   @parameters  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele basieren auf dem sammelelement, das im Beispiel definiert erstellten [Sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md).  
  
### <a name="a-changing-the-collection-frequency"></a>A. Ändern der Sammlungshäufigkeit  
 Im folgenden Beispiel wird die Sammlungshäufigkeit für das angegebene Sammelelement geändert.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@frequency = 3000;  
GO  
```  
  
### <a name="b-renaming-a-collection-item"></a>B. Umbenennen eines Sammelelements  
 Im folgenden Beispiel wird ein Sammelelement umbenannt.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@new_name = N'My modified TSQL item';  
GO  
```  
  
### <a name="c-changing-the-parameters-of-a-collection-item"></a>C. Ändern der Parameter eines Sammelelements  
 Im folgenden Beispiel werden die dem Sammelelement zugeordneten Parameter geändert. Die im `<Value>`-Attribut definierte Anweisung wird geändert, und das `UseSystemDatabases`-Attribut wird auf false festgelegt. Wenn Sie die aktuellen Parameter für dieses Element anzeigen möchten, fragen Sie die Parameter-Spalte in der syscollector_collection_items-Systemsicht ab. Möglicherweise müssen Sie den Wert für `@collection_item_id` ändern.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@collection_item_id = 9,   
@parameters = '  
    \<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
        <Query>  
            <Value>SELECT * FROM sys.dm_db_index_usage_stats</Value>  
            <OutputTable>MyOutputTable</OutputTable>  
        </Query>  
        <Databases>  
            <Database> UseSystemDatabases = "false"   
                       UseUserDatabases = "true"</Database>  
        </Databases>  
    \</ns:TSQLQueryCollector>';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)   
 [Sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
