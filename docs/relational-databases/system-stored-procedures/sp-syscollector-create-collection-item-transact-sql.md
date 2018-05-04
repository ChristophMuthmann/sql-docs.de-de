---
title: Sp_syscollector_create_collection_item (Transact-SQL) | Microsoft Docs
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
- sp_syscollector_create_collection_item
- sp_syscollector_create_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_create_collection_item
- data collector [SQL Server], stored procedures
ms.assetid: 60dacf13-ca12-4844-b417-0bc0a8bf0ddb
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f531ab741581379351ca4721e9f3e7db10ab5b7a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spsyscollectorcreatecollectionitem-transact-sql"></a>sp_syscollector_create_collection_item (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt ein Sammelelement in einem benutzerdefinierten Sammlungssatz. Ein Sammelelement definiert die zu sammelnden Daten und die Häufigkeit, mit der die Daten gesammelt werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syscollector_create_collection_item   
      [ @collection_set_id = ] collection_set_id   
    , [ @collector_type_uid = ] 'collector_type_uid'  
    , [ @name = ] 'name'   
    , [ [ @frequency = ] frequency ]  
    , [ @parameters = ] 'parameters'  
    , [ @collection_item_id = ] collection_item_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumente  
 [ @collection_set_id = ] *collection_set_id*  
 Der eindeutige lokale Bezeichner für den Sammlungssatz. *Collection_set_id* ist **Int**.  
  
 [ @collector_type_uid =] '*Collector_type_uid*"  
 Ist die GUID, der dem sammlertyp entspricht, verwenden Sie für dieses Element identifiziert *Collector_type_uid* ist **"uniqueidentifier"** verfügt über keinen Standardwert... Um eine Liste von Sammlertypen zu erhalten, fragen Sie die syscollector_collector_types-Systemsicht ab.  
  
 [ @name =] '*Namen*"  
 Der Name des Sammelelements. *Namen* ist **Sysname** und darf nicht NULL oder eine leere Zeichenfolge sein.  
  
 *Namen* muss eindeutig sein. Wenn Sie eine Liste der aktuellen Namen von Sammelelementen abrufen möchten, fragen Sie die syscollector_collection_items-Systemsicht ab.  
  
 [ @frequency =] *Häufigkeit*  
 Mithilfe dieses Parameters wird angegeben (in Sekunden), wie häufig Daten durch dieses Sammelelement aufgezeichnet werden. *Häufigkeit* ist **Int**, hat den Standardwert 5. Der minimale Wert, der angegeben werden kann, ist 5 Sekunden.  
  
 Wenn der Sammlungssatz auf den Modus ohne Zwischenspeicherung festgelegt ist, wird die Häufigkeit ignoriert, da dieser Modus bewirkt, dass sowohl die Datensammlung als auch der Datenupload dem Zeitplan entsprechend stattfinden, der für den Sammlungssatz angegeben wurde. Um den Sammlungsmodus des Sammlungssatzes anzuzeigen, Fragen Sie die [Syscollector_collection_sets](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md) -Systemsicht.  
  
 [ @parameters =] '*Parameter*"  
 Die Eingabeparameter für den Sammlertyp. *Parameter* ist **Xml** hat den Standardwert NULL. Die *Parameter* Schema muss das Schema für Parameter des sammlertyps entspricht.  
  
 [ @collection_item_id = ] *collection_item_id*  
 Der eindeutige Bezeichner für das Sammlungssatzelement. *Collection_item_id* ist **Int** und erzeugt OUTPUT.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 sp_syscollector_create_collection_item muss im Kontext der msdb-Systemdatenbank ausgeführt werden.  
  
 Der Sammlungssatz, dem das Sammelelement hinzugefügt wird, muss beendet werden, bevor das Sammelelement erstellt wird. Systemsammlungssätzen können keine Sammelelemente hinzugefügt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Damit diese Prozedur ausgeführt werden kann, ist die Mitgliedschaft in der festen Datenbankrolle dc_admin (mit EXECUTE-Berechtigung) erforderlich.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Sammelelement auf Grundlage des Sammlungstyps `Generic T-SQL Query Collector Type` erstellt und dem Sammlungssatz `Simple collection set test 2` hinzugefügt. Zur Erstellung der angegebenen Auflistung von festzulegen, führen Sie Beispiel B in [Sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
```  
USE msdb;  
GO  
DECLARE @collection_item_id int;  
DECLARE @collection_set_id int = (SELECT collection_set_id   
                                  FROM syscollector_collection_sets  
                                  WHERE name = N'Simple collection set test 2');  
DECLARE @collector_type_uid uniqueidentifier =   
    (SELECT collector_type_uid  
     FROM syscollector_collector_types  
     WHERE name = N'Generic T-SQL Query Collector Type');  
DECLARE @params xml =   
    CONVERT(xml, N'\<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
                <Value>SELECT * FROM sys.objects</Value>  
                <OutputTable>MyOutputTable</OutputTable>  
            </Query>  
            <Databases>   
                <Database> UseSystemDatabases = "true"   
                           UseUserDatabases = "true"  
                </Database>  
            </Databases>  
         \</ns:TSQLQueryCollector>');  
  
EXEC sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid,  
    @name = 'My custom TSQL query collector item',  
    @frequency = 6000,  
    @parameters = @params,  
    @collection_item_id = @collection_item_id OUTPUT;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)   
 [Sp_syscollector_update_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)   
 [Sp_syscollector_delete_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)   
 [Syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)   
 [Sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
