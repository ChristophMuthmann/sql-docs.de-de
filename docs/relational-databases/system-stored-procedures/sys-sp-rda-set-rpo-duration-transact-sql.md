---
title: Sys. sp_rda_set_rpo_duration (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_rpo_duration
- sys.sp_rda_set_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_rpo_duration stored procedure
ms.assetid: 95c80c5b-9252-4612-9ea7-544c48834fd2
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5b59b63e3691b3a8d164c2cb99c3bb3e971237b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="syssprdasetrpoduration-transact-sql"></a>Sys. sp_rda_set_rpo_duration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Legt die Anzahl von Stunden für migrierte Daten, die von SQL Server beibehalten in eine Stagingtabelle für Hilfe eine vollständige Wiederherstellung der Azure-Remotedatenbank, stellen Sie sicher, wenn eine zeitpunktwiederherstellung erforderlich ist.    
    
 Weitere Informationen finden Sie unter [Stretch-Datenbank reduziert das Risiko eines Verlusts Ihrer Azure-Daten, indem migrierte Zeilen vorübergehend beibehalten](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO).  
   
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
     
## <a name="syntax"></a>Syntax    
    
```    
    
sp_rda_set_rpo_duration [ @duration_hrs = ] duration_hrs    
    
```    
    
## <a name="arguments"></a>Argumente    
 [ @duration_hrs =] *Duration_hrs*    
 Die Anzahl der Stunden (eine ganze Zahl ungleich Null-Wert) der migrierten Daten, die Sie für die aktuelle Datenbank für Stretch-aktivierten SQL Server beibehalten soll. Der Standardwert und der Mindestwert beträgt 8 Stunden.    
 
 > [!NOTE]
 > Bei höheren Werten wird mehr Speicherplatz auf SQL Server erforderlich.
    
## <a name="permissions"></a>Berechtigungen    
 Erfordert Db_owner-Berechtigungen.    
    
## <a name="remarks"></a>Hinweise    
 Rufen Sie den aktuellen Wert Treiberdienst [sp_rda_get_rpo_duration &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md).    
    
## <a name="see-also"></a>Siehe auch    
 [sp_rda_get_rpo_duration &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)     
 [Wiederherstellen von Stretch-aktivierten Datenbanken (Stretch-Datenbank)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)     
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
