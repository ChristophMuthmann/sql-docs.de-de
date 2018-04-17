---
title: Sp_mergemetadataretentioncleanup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_mergemetadataretentioncleanup
- sp_mergemetadataretentioncleanup_TSQL
helpviewer_keywords:
- sp_mergemetadataretentioncleanup
ms.assetid: 4e8d6343-2a38-421d-a3f3-c37d437a0f88
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 32a8e2654428569f189efd111839fbde7c6258f0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spmergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt ein manuelles Cleanup von Metadaten in die [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_ Zuordnungen](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md), und [MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md) Systemtabellen. Diese gespeicherte Prozedur wird auf jedem Verleger und Abonnenten in der Topologie durchgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@num_genhistory_rows=** ] *Num_genhistory_rows* Ausgabe  
 Gibt die Anzahl der Zeilen bereinigt aus dem [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md) Tabelle. *Num_genhistory_rows* ist **Int**, hat den Standardwert **0**.  
  
 [  **@num_contents_rows=** ] *Num_contents_rows* Ausgabe  
 Gibt die Anzahl der Zeilen bereinigt aus dem [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) Tabelle. *Num_contents_rows* ist **Int**, hat den Standardwert **0**.  
  
 [  **@num_tombstone_rows=** ] *Num_tombstone_rows* Ausgabe  
 Gibt die Anzahl der Zeilen bereinigt aus dem [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) Tabelle. *Num_tombstone_rows* ist **Int**, hat den Standardwert **0**.  
  
 [  **@aggressive_cleanup_only=** ] *Aggressive_cleanup_only*  
 Nur interne Verwendung.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
  
> [!IMPORTANT]  
>  Wenn mehrere Veröffentlichungen in einer Datenbank vorhanden sind, und eine für diese Veröffentlichungen eine unbegrenzte Aufbewahrungsdauer für Veröffentlichungen verwendet, die Ausführung **Sp_mergemetadataretentioncleanup** keinen Cleanup der Merge-Replikation-änderungsnachverfolgung die Metadaten für die Datenbank. Aus diesem Grund sollten Sie die unbegrenzte Aufbewahrungsdauer für Veröffentlichungen mit Vorsicht verwenden. Um festzustellen, ob eine Veröffentlichung eine unbegrenzte Beibehaltungsdauer besitzt, führen Sie [Sp_helpmergepublication &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) auf dem Verleger und der Hinweis Festlegen aller Veröffentlichungen im Resultset mit einem Wert von **0** für **Aufbewahrung**.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Db_owner** festen Datenbankrolle oder Benutzer in der veröffentlichungszugriffsliste für eine veröffentlichte Datenbank kann **Sp_mergemetadataretentioncleanup**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
