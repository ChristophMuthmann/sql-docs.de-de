---
title: sp_xtp_merge_checkpoint_files (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2016
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
- sys.sp_xtp_merge_checkpoint_files_TSQL
- sys.sp_xtp_merge_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_merge_checkpoint_files
ms.assetid: da04df2a-f7a1-41e7-a1ef-2d5d68919892
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2d5c65c7ca692f341f2fba488254a06cdce3d57e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysspxtpmergecheckpointfiles-transact-sql"></a>sys.sp_xtp_merge_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  **sp_xtp_merge_checkpoint_files** führt alle Daten- und Änderungsdateien Dateien im angegebenen Transaktionsbereich zusammen.  
  
 Weitere Informationen finden Sie unter [erstellen und Verwalten von Speicher für arbeitsspeicheroptimierte Objekte](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**Hinweis**: Diese gespeicherte Prozedur ist in veraltet [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Es wird nicht mehr benötigt und kann nicht verwendet werden, beginnend [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].|  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_xtp_merge_checkpoint_files database_name, @transaction_lower_bound, @transaction_upper_bound  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank, für die die Zusammenführung aufgerufen werden soll. Wenn die Datenbank keine Tabellen im Arbeitsspeicher aufweist, gibt diese Prozedur einen Benutzerfehler zurück. Falls die Datenbank offline ist, wird ein Fehler zurückgegeben.  
  
 *lower_bound_Tid*  
 Die Untergrenze (Bigint), der Transaktionen für eine Datendatei entsprechend [dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) entsprechend der prüfpunktstartdatei der Zusammenführung. Bei einem ungültigen transactionId-Wert wird ein Fehler generiert.  
  
 *upper_bound_Tid*  
 Die Obergrenze (Bigint) von Transaktionen für eine Datendatei entsprechend [dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md). Bei einem ungültigen transactionId-Wert wird ein Fehler generiert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="cursors-returned"></a>Zurückgegebene Cursor  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die feste Serverrolle sysadmin und die feste Datenbankrolle db_owner.  
  
## <a name="remarks"></a>Hinweise  
 Führt alle Daten und Änderungsdateien innerhalb des gültigen Bereichs zusammen, um eine einzelne Daten- und Änderungsdatei zu erstellen. Die Mergerichtlinie wird von dieser Prozedur nicht berücksichtigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
