---
title: sp_rda_reconcile_batch (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_batch
- sys.sp_rda_reconcile_batch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_batch stored procedure
ms.assetid: 6d21eac3-7b6c-4fe0-8bc4-bf503f3948a6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1df76c9b3107b5fbd45eb8a99eab1ec5baf5f4ee
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="syssprdareconcilebatch-transact-sql"></a>sys.sp_rda_reconcile_batch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Gleicht die Batch-ID, die in der Stretch-aktivierten SQL Server-Tabelle gespeichert sind, mit der Batch-ID, die in der remote-Azure-Tabelle gespeichert.  
  
 In der Regel haben nur auszuführende **Sp_rda_reconcile_batch** Wenn Sie kürzlich die meisten migrierten Daten manuell aus der Remotetabelle gelöscht haben. Wenn Sie Remotedaten, die den aktuellen Batch enthält manuell löschen, die Batch-IDs sind nicht synchronisiert, und Migration angehalten wird.  
 
 Um Daten zu löschen, die bereits in Azure migriert wurden, finden Sie unter den Hinweisen auf dieser Seite.
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>Syntax  
  
```  
  
sp_rda_reconcile_batch @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>Argumente  
 @objname = '*@objname*'  
 Der Name der SQL Server Stretch-aktivierte Tabelle.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert Db_owner-Berechtigungen.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie möchten Daten löschen, die bereits in Azure migriert wurden, führen Sie folgende Schritte aus.  
  
1.  Anhalten der Datenmigration. Weitere Informationen finden Sie unter [anhalten und Fortsetzen der Datenmigration &#40; Stretch-Datenbank &#41; ](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
2.  Löschen der Daten aus der Stagingtabelle für SQL Server durch Ausführen eines DELETE-Befehls mit dem Hinweis stage_only durch. Weitere Informationen finden Sie unter [durchführen administrativer Aktualisierungs- und Löschvorgänge](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md#adminHints).
  
3.  Löschen Sie diese Daten aus der Remotetabelle Azure durch Ausführen eines DELETE-Befehls mit dem REMOTE_ONLY-Hinweis.  
  
4.  Run **sp_rda_reconcile_batch**.  
  
5.  Fortsetzen der Datenmigration. Weitere Informationen finden Sie unter [anhalten und Fortsetzen der Datenmigration &#40; Stretch-Datenbank &#41; ](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
## <a name="example"></a>Beispiel  
 Wenn der Batch-IDs abstimmen möchten, führen Sie die folgende Anweisung aus.  
  
```sql  
EXEC sp_rda_reconcile_batch @objname = N'StretchEnabledTableName';  
```  
  
  
