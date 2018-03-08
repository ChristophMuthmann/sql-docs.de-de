---
title: sp_syscollector_start_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syscollector_start_collection_set_TSQL
- sp_syscollector_start_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_start_collection_set
ms.assetid: d8357180-f51e-4681-99f9-0596fe2d2b53
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 54381b4d9b0baab7d9b726fd209a3cfb598fb8e1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="spsyscollectorstartcollectionset-transact-sql"></a>sp_syscollector_start_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Startet einen Sammlungssatz, wenn der Sammler bereits aktiviert ist und der Sammlungssatz nicht ausgeführt wird. Wenn der Sammler nicht aktiviert ist, aktivieren Sie den Sammler Treiberdienst [Sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md) und verwenden Sie diese gespeicherte Prozedur, um einen Sammlungssatz zu starten.  

  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syscollector_start_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@collection_set_id =** ] *collection_set_id*  
 Der eindeutige lokale Bezeichner für den Sammlungssatz. *Collection_set_id* ist **Int** hat den Standardwert NULL. *Collection_set_id* muss einen Wert aufweisen, wenn *Namen* ist NULL.  
  
 [  **@name =** ] "*Namen*"  
 Ist der Name des Sammlungssatzes. *Namen* ist **Sysname** hat den Standardwert NULL. *Namen* muss einen Wert aufweisen, wenn *Collection_set_id* ist NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 sp_syscollector_create_collection_set muss im Kontext der msdb-Systemdatenbank ausgeführt werden, und SQL Server-Agent muss aktiviert sein.  
  
 Bei dieser Prozedur tritt ein Fehler auf, wenn sie für einen Sammlungssatz ohne Zeitplan ausgeführt wird. Wenn der Sammlungssatz keinen Zeitplan (da der zugehörige Sammlungsmodus ohne Zwischenspeicherung, z. B. festgelegt ist), verwenden Sie die [Sp_syscollector_run_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md) gespeicherte Prozedur, um den Sammlungssatz zu starten.  
  
 Diese Prozedur aktiviert die Sammlungs- und Uploadaufträge für den angegebenen Sammlungssatz und startet umgehend den Auftrag des Sammlungs-Agents, wenn für den Sammlungssatz der zugehörige Sammlungsmodus auf die Zwischenspeicherung (0) festgelegt ist. Weitere Informationen finden Sie unter [Sp_syscollector_create_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
 Wenn der Sammlungssatz keine Sammelelemente enthält, hat dieser Vorgang keine Auswirkungen. Fehler 14685 wird als Warnung zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Damit diese Prozedur ausgeführt werden kann, ist die Mitgliedschaft in der festen Datenbankrolle dc_operator erforderlich. Wenn der Sammlungssatz über kein Proxykonto verfügt, ist die Mitgliedschaft in der festen Serverrolle sysadmin erforderlich.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Sammlungssatz mithilfe seines Bezeichners gestartet.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
