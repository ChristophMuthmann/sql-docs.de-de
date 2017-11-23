---
title: sp_rda_get_rpo_duration (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_get_rpo_duration
- sys.sp_rda_get_rpo_duration_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.sp_rda_get_rpo_duration stored procedure
ms.assetid: 35882067-3072-47ff-9024-ca453c0f49a7
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4a36d1b1e04e53098710a1cacc8c463653f82710
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="syssprdagetrpoduration-transact-sql"></a>sp_rda_get_rpo_duration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Ruft die Anzahl von Stunden für migrierte Daten, die von SQL Server beibehalten in eine Stagingtabelle für Hilfe eine vollständige Wiederherstellung der Azure-Remotedatenbank, stellen Sie sicher, wenn eine zeitpunktwiederherstellung erforderlich ist. 
  
  Weitere Informationen finden Sie unter [Stretch-Datenbank reduziert das Risiko eines Verlusts Ihrer Azure-Daten, indem migrierte Zeilen vorübergehend beibehalten](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO).  
    
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Syntax    
    
```    
    
sp_rda_get_rpo_duration @durationinhours output    
    
```    
    
## <a name="output-parameter"></a>Output-parameter    
 *@durationinhours*    
  Die Anzahl der Stunden (eine ganze Zahl ungleich Null-Wert) der migrierten Daten, die von SQL Server für die aktuelle aktivierter Funktion Stretch-Datenbank beibehalten.    
    
## <a name="permissions"></a>Berechtigungen    
 Erfordert Db_owner-Berechtigungen.    
    
## <a name="remarks"></a>Hinweise    
 Ändern Sie den Wert durch Ausführen von [Sys. sp_rda_set_rpo_duration &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md).    
    
## <a name="see-also"></a>Siehe auch    
 [Sys. sp_rda_set_rpo_duration &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)     
 [Wiederherstellen von Stretch-aktivierten Datenbanken (Stretch-Datenbank)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)    
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
