---
title: ALTER PARTITION SCHEME (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION SCHEME
- ALTER_PARTITION_SCHEME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PARTITION SCHEME statement
- partition schemes [SQL Server], modifying
- modifying partition schemes
- adding filegroups
- NEXT USED filegroups
ms.assetid: f01d6880-9800-4cfb-8d11-d4be21efc8ca
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f339a83559e565d5046c721657becd6cf6a5940d
ms.sourcegitcommit: 721ad1cbc10e8147c087ae36b36296d72cbb0de8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="alter-partition-scheme-transact-sql"></a>ALTER PARTITION SCHEME (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Fügt einem Partitionsschema eine Dateigruppe hinzu oder ändert die Bezeichnung der NEXT USED-Dateigruppe für das Partitionsschema. 

>[!NOTE]
>In Azure SQL-Datenbank werden nur primäre Dateigruppen unterstützt.  
  
 ![Artikellinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Article link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER PARTITION SCHEME partition_scheme_name   
NEXT USED [ filegroup_name ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *partition_scheme_name*  
 Der Name des Partitionsschemas, das geändert werden soll.  
  
 *filegroup_name*  
 Gibt die Dateigruppe an, die vom Partitionsschema als NEXT USED markiert werden soll. Dies bedeutet, dass die Dateigruppe eine neue Partition akzeptiert, die mithilfe einer [ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md)-Anweisung erstellt wurde.  
  
 In einem Partitionsschema kann nur eine Dateigruppe als NEXT USED bezeichnet werden. Es kann eine Dateigruppe angegeben werden, die nicht leer ist. Wenn *filegroup_name* angegeben wurde und derzeit keine Dateigruppe als NEXT USED markiert ist, wird *filegroup_name* als NEXT USED markiert. Wenn *filegroup_name* angegeben wurde und bereits eine Dateigruppe mit der NEXT USED-Eigenschaft vorhanden ist, wird die NEXT USED-Eigenschaft von der vorhandenen Dateigruppe auf *filegroup_name* übertragen.  
  
 Wenn *filegroup_name* nicht angegeben wurde und bereits eine Dateigruppe mit der NEXT USED-Eigenschaft vorhanden ist, verliert diese Dateigruppe ihren NEXT USED-Status, sodass keine NEXT USED-Dateigruppen in *partition_scheme_name* vorhanden sind.  
  
 Wenn *filegroup_name* nicht angegeben wurde und keine Dateigruppen als NEXT USED markiert sind, gibt ALTER PARTITION SCHEME eine Warnmeldung zurück.  
  
## <a name="remarks"></a>Remarks  
 Jede Dateigruppe, die von ALTER PARTITION SCHEME betroffen ist, muss online sein.  
  
## <a name="permissions"></a>Berechtigungen  
 Die folgenden Berechtigungen können verwendet werden, um ALTER PARTITION SCHEME auszuführen:  
  
-   ALTER ANY DATASPACE-Berechtigung. Diese Berechtigung gilt standardmäßig für Mitglieder der festen Serverrolle **sysadmin** und für Mitglieder der festen Datenbankrollen **db_owner** und **db_ddladmin** .  
  
-   CONTROL- oder ALTER-Berechtigung für die Datenbank, in der das Partitionsschema erstellt wurde.  
  
-   Die CONTROL SERVER-Berechtigung oder ALTER ANY DATABASE-Berechtigung auf dem Server der Datenbank, in der das Partitionsschema erstellt wurde.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird vorausgesetzt, dass das Partitionsschema `MyRangePS1` und die Dateigruppe `test5fg` in der aktuellen Datenbank vorhanden sind.  
  
```  
ALTER PARTITION SCHEME MyRangePS1  
NEXT USED test5fg;  
```  
  
 Als Ergebnis einer ALTER PARTITION FUNCTION-Anweisung erhält die Dateigruppe `test5fg` alle zusätzlichen Partitionen einer partitionierten Tabelle oder eines partitionierten Indexes.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_schemes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [sys.data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
