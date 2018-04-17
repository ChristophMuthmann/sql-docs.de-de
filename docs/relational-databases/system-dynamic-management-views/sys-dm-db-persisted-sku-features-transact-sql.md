---
title: Sys. dm_db_persisted_sku_features (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_persisted_sku_features_TSQL
- sys.dm_db_persisted_sku_features
- dm_db_persisted_sku_features_TSQL
- dm_db_persisted_sku_features
dev_langs:
- TSQL
helpviewer_keywords:
- editions [SQL Server], feature restrictions
- sys.dm_db_persisted_sku_features dynamic management view
ms.assetid: b4b29e97-b523-41b9-9528-6d4e84b89e09
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0cbc96b18346f6e55f4029e795c22557f6107e7b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbpersistedskufeatures-transact-sql"></a>sys.dm_db_persisted_sku_features (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Einige Funktionen von der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ändern Sie die Möglichkeit, [!INCLUDE[ssDE](../../includes/ssde-md.md)] Informationen in den Datenbankdateien speichert. Diese Funktionen sind nicht in allen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar. Eine Datenbank, die diese Funktionen enthält, kann nicht in eine Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verschoben werden, die sie nicht unterstützt. Verwenden Sie die dynamische verwaltungssicht Sys. dm_db_persisted_sku_features, um editionsspezifischen Funktionen aufzulisten, die in der aktuellen Datenbank aktiviert sind.
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|feature_name|**sysname**|Externer Name der Funktion, die in der aktuellen Datenbank aktiviert ist, aber nicht in allen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt wird. Diese Funktion muss entfernt werden, bevor die Datenbank zu allen verfügbaren Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] migriert werden kann.|  
|feature_id|**int**|Funktions-ID, die der Funktion zugeordnet ist. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]installiert haben.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung für die Datenbank.  
  
## <a name="remarks"></a>Hinweise  
 Wenn keine Funktionen, die durch eine bestimmte Edition eingeschränkt werden können, die von der Datenbank verwendet werden, gibt die Sicht keine Zeilen zurück.  
  
 Sys. dm_db_persisted_sku_features listet möglicherweise die folgenden Funktionen zur Datenbank verändert wie mit speziellen eingeschränkten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Editionen:  
  
-   **ChangeCapture**: Gibt an, dass eine Datenbank Change Data Capture aktiviert wurde. Um Change Data Capture zu entfernen, verwenden Sie die [sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) gespeicherte Prozedur. Weitere Informationen finden Sie unter [Informationen zu Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md).  
  
-   **ColumnStoreIndex**: Gibt an, über mindestens eine Tabelle verfügt über einen columnstore-Index. So aktivieren Sie eine Datenbank in eine Edition von verschoben werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die diese Funktion nicht unterstützt, verwenden Sie die [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) oder [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) Anweisung, um den columnstore-Index zu entfernen. Weitere Informationen finden Sie unter [columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-overview.md).  
  
    **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
-   **Komprimierung**: Gibt an, dass mindestens eine Tabelle oder ein Index die datenkomprimierung oder das Vardecimal-Speicherformat verwendet. So aktivieren Sie eine Datenbank in eine Edition von verschoben werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die diese Funktion nicht unterstützt, verwenden Sie die [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) oder [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) -Anweisung zum Entfernen von datenkomprimierung. Um das vardecimal-Speicherformat zu entfernen, verwenden Sie die sp_tableoption-Anweisung. Weitere Informationen finden Sie unter [Data Compression](../../relational-databases/data-compression/data-compression.md).  
  
-   **MultipleFSContainers**: Gibt an, dass die Datenbank mehrere FileStream-Container verwendet. Die Datenbank besitzt eine FILESTREAM-Dateigruppe mit mehreren Containern (Dateien). Weitere Informationen finden Sie unter [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
-   **InMemoryOLTP**: Gibt an, dass die Datenbank In-Memory OLTP verwendet. Die Datenbank verfügt über eine MEMORY_OPTIMIZED_DATA-Dateigruppe. Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
  **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]). 
  
-   **Partitionierung.** Gibt an, dass die Datenbank partitionierte Tabellen, partitionierte Indizes, partitionierte Schemas oder Partitionsfunktionen enthält. Damit eine Datenbank in eine andere Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als die Enterprise oder Developer Edition verlagert werden kann, genügt es nicht, die Tabelle dahingehend abzuändern, dass sie sich in einer einzigen Partition befindet. Sie müssen die partitionierte Tabelle entfernen. Wenn die Tabelle Daten enthält, verwenden Sie SWITCH PARTITION, um jede Partition in eine nicht partitionierte Tabelle zu konvertieren. Löschen Sie dann die partitionierte Tabelle, das Partitionsschema und die Partitionsfunktion.  
  
-   **TransparentDataEncryption.** Gibt an, dass eine Datenbank mit transparenter Datenverschlüsselung verschlüsselt wird. Um die transparente Datenverschlüsselung zu entfernen, verwenden Sie die ALTER DATABASE-Anweisung. Weitere Informationen finden Sie unter [Transparente Datenverschlüsselung &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  

> [!NOTE]
> Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Service Pack 1, die diese Funktionen sind verfügbar für mehrere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Editionen und nicht nur auf Enterprise oder Developer Editionen beschränkt.

 Wenn Sie feststellen möchten, ob in einer Datenbank Funktionen verwendet werden, die nur in bestimmten Editionen verfügbar sind, führen Sie die folgende Anweisung in der Datenbank aus:  
  
```sql  
SELECT feature_name FROM sys.dm_db_persisted_sku_features;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Datenbank verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [Editionen und unterstützten Funktionen von SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Editionen und unterstützten Funktionen von SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
