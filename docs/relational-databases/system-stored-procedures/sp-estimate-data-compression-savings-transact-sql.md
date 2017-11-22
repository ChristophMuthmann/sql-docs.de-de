---
title: Sp_estimate_data_compression_savings (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_estimate_data_compression_savings_TSQL
- sp_estimate_data_compression_savings
dev_langs: TSQL
helpviewer_keywords:
- compression [SQL Server], estimating
- sp_estimate_data_compression_savings
ms.assetid: 6f6c7150-e788-45e0-9d08-d6c2f4a33729
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 80b5cb7fff9bfadd2d1dfe03884d2e723744fe8b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spestimatedatacompressionsavings-transact-sql"></a>sp_estimate_data_compression_savings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die aktuelle Größe des angeforderten Objekts zurück und schätzt die Objektgröße für den angeforderten Komprimierungsstatus. Die Komprimierung kann für ganze Tabellen oder Teile von Tabellen ermittelt werden. Dazu gehören Heaps, gruppierte Indizes, nicht gruppierte Indizes, indizierte Sichten sowie Tabellen- und Indexpartitionen. Die Objekte können mit der Zeilenkomprimierung oder der Seitenkomprimierung komprimiert werden. Wenn die Tabelle, der Index oder die Partition bereits komprimiert ist, können Sie mithilfe dieser Prozedur die Größe der erneut komprimierten Tabelle, des erneut komprimierten Index oder der erneut komprimierten Partition einschätzen.  
  
> [!NOTE]  
>  Komprimierung und **Sp_estimate_data_compression_savings** stehen nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Um die Größe des Objekts bei Verwendung der angeforderten Komprimierungseinstellung einzuschätzen, fragt diese gespeicherte Prozedur das Quellobjekt ab und lädt diese Daten in eine entsprechende Tabelle und einen entsprechenden Index in tempdb. Die Tabelle oder der Index, die bzw. der in tempdb erstellt wurde, wird anschließend entsprechend der angeforderten Einstellung komprimiert, und die Komprimierungseinsparungen werden berechnet.  
  
 So ändern Sie den Komprimierungsstatus der eine Tabelle, Index oder Partition mithilfe der [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) oder [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) Anweisungen. Allgemeine Informationen zur Komprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
> [!NOTE]  
>  Wenn die vorhandenen Daten fragmentiert sind, können Sie ihre Größe möglicherweise ohne Komprimierung verringern, indem Sie den Index neu erstellen. Für Indizes wird der Füllfaktor während der Neuerstellung des Indexes angewendet. Dadurch könnte die Größe des Indexes zunehmen.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_estimate_data_compression_savings   
     [ @schema_name = ] 'schema_name'    
   , [ @object_name = ] 'object_name'   
   , [@index_id = ] index_id   
   , [@partition_number = ] partition_number   
   , [@data_compression = ] 'data_compression'   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @schema_name=] '*Schema_name*"  
 Der Name des Datenbankschemas, das die Tabelle oder die indizierte Sicht enthält. *Schema_name* ist **Sysname**. Wenn *Schema_name* NULL ist, wird das Standardschema des aktuellen Benutzers verwendet.  
  
 [ @object_name=] '*Object_name*"  
 Der Name der Tabelle oder der indizierten Sicht des Indexes. *Object_name* ist **Sysname**.  
  
 [ @index_id=] '*Index_id*"  
 Die ID des Indexes. *Index_id* ist **Int**, und kann einen der folgenden Werte: die ID-Nummer eines Indexes, NULL oder 0, wenn *Object_id* ein Heap ist. Geben Sie NULL an, wenn Informationen zu allen Indizes für eine Basistabelle oder Sicht zurückgegeben werden sollen. Wenn Sie NULL angeben, müssen Sie auch angeben, auf NULL für *Partition_number*.  
  
 [ @partition_number=] '*Partition_number*"  
 Die Partitionsnummer im Objekt. *Partitionsnummer* ist **Int**, und kann einen der folgenden Werte: die Partitionsnummer des Indexes oder Heaps, NULL oder 1 für einen nicht partitionierten Index oder Heap.  
  
 Sie können auch angeben, um die Partition anzugeben, die [$partition](../../t-sql/functions/partition-transact-sql.md) Funktion. Geben Sie NULL an, wenn Informationen zu allen Partitionen des besitzenden Objekts zurückgegeben werden sollen.  
  
 [ @data_compression=] '*Data_compression*"  
 Der Typ der Komprimierung, die ausgewertet werden soll. *DATA_COMPRESSION* kann eine der folgenden Werte: NONE, ROW oder PAGE.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Das folgende Resultset wird zurückgegeben, damit Informationen zur aktuellen und geschätzten Größe von Tabelle, Index oder Partition bereitgestellt werden.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|object_name|**sysname**|Der Name der Tabelle oder indizierten Sicht.|  
|schema_name|**sysname**|Das Schema der Tabelle oder indizierten Sicht.|  
|index_id|**int**|Index-ID eines Index:<br /><br /> 0 = Heap<br /><br /> 1 = Gruppierter Index<br /><br /> > 1 = Nicht gruppierter Index|  
|partition_number|**int**|Partitionsnummer. Gibt 1 für eine nicht partitionierte Tabelle oder einen Index zurück.|  
|size_with_current_compression_setting (KB)|**bigint**|Die Größe der angeforderten, vorhandenen Tabelle, des Indexes oder der Partition.|  
|size_with_requested_compression_setting (KB)|**bigint**|Die geschätzte Größe der Tabelle, des Indexes oder der Partition, die bzw. der die angeforderte Komprimierungseinstellung verwendet, und der vorhandene Füllfaktor (sofern zutreffend). Zudem wird vorausgesetzt, dass keine Fragmentierung vorliegt.|  
|sample_size_with_current_compression_setting (KB)|**bigint**|Die Größe der Stichprobe mit der aktuellen Komprimierungseinstellung. Dies beinhaltet jegliche Fragmentierung.|  
|sample_size_with_requested_compression_setting (KB)|**bigint**|Die Größe der Stichprobe, die mithilfe der angeforderten Komprimierungseinstellung erstellt wird, mit vorhandenem Füllfaktor (sofern zutreffend) und ohne Fragmentierung.|  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie sp_estimate_data_compression_savings, um die Einsparungen beim Aktivieren einer Tabelle oder einer Partition für die Zeilen- oder Seitenkomprimierung einzuschätzen. Wenn beispielsweise die durchschnittliche Größe der Zeile um 40 Prozent verringert werden kann, können Sie die Größe des Objekts potenziell um 40 Prozent verringern. Möglicherweise erzielen Sie keine Platzeinsparung, weil dies vom Füllfaktor und von der Zeilengröße abhängt. Wenn eine Zeile beispielsweise 8000 Bytes lang ist und Sie die Größe um 40 Prozent verringern, passt weiterhin nur eine Zeile auf eine Datenseite. Daher werden keine Einsparungen erzielt.  
  
 Wenn die Ergebnisse der Ausführung von sp_estimate_data_compression_savings darauf hindeuten, dass sich die Tabelle vergrößert, bedeutet dies, dass für viele Zeilen in der Tabelle fast die gesamte Genauigkeit der Datentypen verwendet wird, und der geringe zusätzliche Verarbeitungsaufwand für das komprimierte Format ist größer als die Einsparungen durch die Komprimierung. Aktivieren Sie in diesem seltenen Fall die Komprimierung nicht.  
  
 Wenn eine Tabelle für eine Komprimierung aktiviert ist, verwenden Sie sp_estimate_data_compression_savings, um die durchschnittliche Größe der Zeile bei nicht komprimierter Tabelle einzuschätzen.  
  
 Eine (IS)-Sperre wird während dieses Vorgangs für die Tabelle abgerufen. Wenn keine (IS)-Sperre abgerufen werden kann, wird die Prozedur blockiert. Die Tabelle wird unter der Read Committed-Isolationsstufe gescannt.  
  
 Wenn die angeforderte Komprimierungseinstellung mit der aktuellen Komprimierungseinstellung identisch ist, gibt die gespeicherte Prozedur die geschätzte Größe ohne Fragmentierung und mit dem vorhandenen Füllfaktor zurück.  
  
 Wenn die Index- oder die Partitions-ID nicht vorhanden ist, werden keine Ergebnisse zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die SELECT-Berechtigung für die Tabelle.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Da diese Prozedur nicht auf columnstore-Tabellen anwendbar ist, werden die Datenkomprimierungsparameter COLUMNSTORE und COLUMNSTORE_ARCHIVE nicht akzeptiert.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Größe der `Production.WorkOrderRouting`-Tabelle geschätzt, wenn sie mit der `ROW`-Komprimierung komprimiert wird.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimate_data_compression_savings 'Production', 'WorkOrderRouting', NULL, NULL, 'ROW' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [Sys.Partitions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Implementierung von Unicode-Komprimierung](../../relational-databases/data-compression/unicode-compression-implementation.md)  
  
  
