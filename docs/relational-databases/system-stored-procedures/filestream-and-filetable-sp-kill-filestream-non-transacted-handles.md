---
title: Sp_kill_filestream_non_transacted_handles (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
- sp_kill_filestream_non_transacted_handles_TSQL
- sp_kill_filestream_non_transacted_handles
dev_langs: TSQL
helpviewer_keywords: sp_kill_filestream_non_transacted_handles
ms.assetid: 7188353e-ab29-49a0-8f25-7fb8ab122589
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7958e7a6513363030d8962774a28992bd055661d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="filestream-and-filetable---spkillfilestreamnontransactedhandles"></a>FileStream- und FileTable - sp_kill_filestream_non_transacted_handles
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Schließt nicht transaktionale Dateihandles für FileTable-Daten.  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
sp_kill_filestream_non_transacted_handles [[ @table_name = ] ‘table_name’, [[ @handle_id = ] @handle_id]]  
```  
  
## <a name="arguments"></a>Argumente  
 *table_name*  
 Der Name der Tabelle, in der nicht transaktionale Handles zu schließen sind.  
  
 Sie können übergeben *Table_name* ohne *Handle_id* um zu schließen, um alle geöffneten nicht transaktionalen Handles für die FileTable.  
  
 Sie können NULL übergeben, für den Wert des *Table_name* um zu schließen, um alle geöffneten nicht transaktionalen Handles für alle FileTables in der aktuellen Datenbank. NULL, ist der Standardwert.  
  
 *handle_id*  
 Die optionale ID des einzelnen Handles, der geschlossen werden soll. Sie erhalten die *Handle_id* aus der [dm_filestream_non_transacted_handles &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md) -verwaltungssicht. Jede ID ist in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz eindeutig. Bei Angabe von *Handle_id*, müssen Sie auch einen Wert für *Table_name*.  
  
 Sie können NULL übergeben, für den Wert des *Handle_id* um zu schließen, um alle geöffneten nicht transaktionalen Handles für die FileTable gemäß *Table_name*. NULL, ist der Standardwert.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-set"></a>Resultset  
 Keine.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Die *Handle_id* erforderlich **Sp_kill_filestream_non_transacted_handles** ist nicht im Zusammenhang mit der Session_id oder Arbeitseinheit, die in anderen dient **kill** Befehle.  
  
 Weitere Informationen finden Sie unter [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md).  
  
## <a name="metadata"></a>Metadaten  
 Informationen zu geöffneten nicht transaktionalen Dateihandles, Fragen Sie die dynamische verwaltungssicht [dm_filestream_non_transacted_handles &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md).  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Sie benötigen **VIEW DATABASE STATE** über die Berechtigung zum Abrufen von Dateihandles aus der **dm_filestream_non_transacted_handles** -verwaltungssicht und zum Ausführen von **Sp_kill_filestream_non_ Transacted_handles**.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele zeigen, wie Aufrufen **Sp_kill_filestream_non_transacted_handles** nicht transaktionale Dateihandles für FileTable-Daten zu schließen.  
  
```tsql  
-- Close all open handles in the current database.  
sp_kill_filestream_non_transacted_handles  
  
-- Close all open handles in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = ’myFileTable’  
  
-- Close a specific handle in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = ’myFileTable’, @handle_id = 0xFFFAAADD  
```  
  
 Im folgende Beispiel wird gezeigt, wie ein Skript verwenden, zum Abrufen einer *Handle_id* und schließen Sie sie.  
  
```tsql  
DECLARE @handle_id varbinary(16);  
DECLARE @table_name sysname;  
  
SELECT TOP 1 @handle_id = handle_id, @table_name = Object_name(table_id)  
FROM sys.dm_FILESTREAM_non_transacted_handles;  
  
EXEC sp_kill_filestream_non_transacted_handles @dbname, @table_name, @handle_id;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
