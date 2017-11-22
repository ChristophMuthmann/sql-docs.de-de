---
title: Sys. dm_db_objects_impacted_on_version_change (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_objects_impacted_on_version_change_TSQL
- dm_db_objects_impacted_on_version_change
- dm_db_objects_impacted_on_version_change_TSQL
- sys.dm_db_objects_impacted_on_version_change
dev_langs: TSQL
helpviewer_keywords:
- dm_db_objects_impacted_on_version_change
- sys.dm_db_objects_impacted_on_version_change
ms.assetid: b94af834-c4f6-4a27-80a6-e8e71fa8793a
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ab63b177449c0648f033773197ee32b48ec0d3f5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbobjectsimpactedonversionchange-azure-sql-database"></a>sys.dm_db_objects_impacted_on_version_change (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Diese datenbankbezogene Systemsicht wurde entworfen, um ein Frühwarnsystem bereitzustellen, mit dem Objekte ermittelt werden sollen, die von einem Upgrade der Hauptversion in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] betroffen sein werden. Sie können die Sicht entweder vor oder nach dem Upgrade verwenden, um eine vollständige Enumeration der betroffenen Objekte abzurufen. Sie müssen diese Sicht in jeder Datenbank abfragen, damit der gesamte Server berücksichtigt wird.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|class|**Int** NOT NULL|Die Klasse des Objekts, das betroffen sein wird:<br /><br /> **1** = Einschränkung<br /><br /> **7** = Indizes und Heaps|  
|class_desc|**nvarchar(60)** NOT NULL|Beschreibung der Klasse:<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **INDEX**|  
|major_id|**Int** NOT NULL|Objekt-ID der Einschränkung oder Objekt-ID der Tabelle, die den Index oder Heap enthält.|  
|minor_id|**Int** NULL|**NULL** für Einschränkungen<br /><br /> Index_id für Indizes und Heaps|  
|Abhängigkeit|**nvarchar(60)** NOT NULL|Beschreibung der Abhängigkeit, die bewirkt, dass die Einschränkung oder der Index betroffen sind. Derselbe Wert wird auch für Warnungen verwendet, die während des Upgrades generiert werden.<br /><br /> Beispiele:<br /><br /> **Speicherplatz** (für systeminterne)<br /><br /> **Geometrie** (für System-UDT)<br /><br /> **Geography:: Parse** (für System-UDT-Methode)|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung.  
  
## <a name="example"></a>Beispiel  
 Im folgende Beispiel wird eine Abfrage für **Sys. dm_db_objects_impacted_on_version_change** Suchen der Objekte, die ein Upgrade auf die nächstgrößeren Serverversion betroffen  
  
```  
SELECT * FROM sys.dm_db_objects_disabled_on_version_change;  
GO  
```  
  
```  
class  class_desc        major_id    minor_id    dependency                       
------ ----------------- ----------- ----------- ----------   
1      OBJECT_OR_COLUMN  181575685   NULL        geometry                        
7      INDEX             37575172    1           geometry                        
7      INDEX             2121058592  1           geometry                        
1      OBJECT_OR_COLUMN  101575400   NULL        geometry     
```  
  
## <a name="remarks"></a>Hinweise  
  
### <a name="how-to-update-impacted-objects"></a>Aktualisieren betroffener Objekte  
 Die folgenden Schritte beschreiben die Korrekturmaßnahmen, die Sie nach dem bevorstehenden Serviceupgrade im Juni durchführen sollten.  
  
|Order|Betroffenes Objekt|Korrekturmaßnahme|  
|-----------|---------------------|-----------------------|  
|1|**Indizes**|Alle identifizierten Index neu erstellen **Sys. dm_db_objects_impacted_on_version_change** zum Beispiel:`ALTER INDEX ALL ON <table> REBUILD`<br />oder<br />`ALTER TABLE <table> REBUILD`|  
|2|**Objekt**|Alle Einschränkungen, die durch **Sys. dm_db_objects_impacted_on_version_change** muss erneut überprüft werden, nachdem die Geometrie und Geografie-Daten in der zugrunde liegenden Tabelle neu berechnet werden. Führen Sie die erneute Überprüfung für Einschränkungen mithilfe von ALTER TABLE durch. <br />Beispiel: <br />`ALTER TABLE <tab> WITH CHECK CHECK CONSTRAINT <constraint name>`<br />oder<br />`ALTER TABLE <tab> WITH CHECK CONSTRAINT ALL`|  
  
  
