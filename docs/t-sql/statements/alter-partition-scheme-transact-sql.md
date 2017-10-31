---
title: ALTER PARTITION SCHEME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 545fe3da48f0d0c98d72b32e5a82d9fd55579d00
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-partition-scheme-transact-sql"></a>ALTER PARTITION SCHEME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt einem Partitionsschema eine Dateigruppe hinzu oder ändert die Bezeichnung der NEXT USED-Dateigruppe für das Partitionsschema.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER PARTITION SCHEME partition_scheme_name   
NEXT USED [ filegroup_name ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *partition_scheme_name*  
 Der Name des Partitionsschemas, das geändert werden soll.  
  
 *filegroup_name*  
 Gibt die Dateigruppe an, die vom Partitionsschema als NEXT USED markiert werden soll. Dies bedeutet, dass die Dateigruppe akzeptiert eine neue Partition, die erstellt wird ein [ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md) Anweisung.  
  
 In einem Partitionsschema kann nur eine Dateigruppe als NEXT USED bezeichnet werden. Es kann eine Dateigruppe angegeben werden, die nicht leer ist. Wenn *Filegroup_name* angegeben ist und derzeit keine Dateigruppe als NEXT USED, *Filegroup_name* als NEXT USED markiert ist. Wenn *Filegroup_name* angegeben ist, und eine Dateigruppe mit der NEXT USED-Eigenschaft bereits vorhanden ist, wird der NEXT USED-Eigenschaft aus der vorhandenen Dateigruppe auf überträgt *Filegroup_name*.  
  
 Wenn *Filegroup_name* nicht angegeben ist und bereits eine Dateigruppe mit der NEXT USED-Eigenschaft vorhanden ist, verliert diese Dateigruppe die NEXT USED-Status, sodass keine NEXT USED-Dateigruppen in *Partition_scheme_name*.  
  
 Wenn *Filegroup_name* nicht angegeben ist, und es werden keine Dateigruppen als NEXT USED markiert, ALTER PARTITION SCHEME eine Warnmeldung zurück.  
  
## <a name="remarks"></a>Hinweise  
 Jede Dateigruppe, die von ALTER PARTITION SCHEME betroffen ist, muss online sein.  
  
## <a name="permissions"></a>Berechtigungen  
 %Tdas folgende Berechtigungen kann verwendet werden, um ALTER PARTITION SCHEME auszuführen:  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME &#40; Transact-SQL &#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Sys. partition_schemes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [Sys. data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [Sys. destination_data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [Sys.Partitions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  

