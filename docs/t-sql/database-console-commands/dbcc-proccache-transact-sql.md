---
title: DBCC PROCCACHE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC PROCCACHE
- DBCC_PROCCACHE_TSQL
- PROCCACHE_TSQL
- PROCCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- procedure cache [SQL Server]
- displaying procedure cache information
- DBCC PROCCACHE statement
ms.assetid: 7a4f9f8a-13ff-4bf2-ba29-c17012a23659
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 97e617e7867c90bf1e66c5e64e37b9039087d463
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-proccache-transact-sql"></a>DBCC PROCCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Zeigt Informationen zum Prozedurcache in tabellarischer Form an.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC PROCCACHE [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumente  
 WITH  
 Lässt die Angabe von Optionen zu.  
  
 NO_INFOMSGS  
 Unterdrückt alle Informationsmeldungen mit einem Schweregrad von 0 bis 10.  
  
## <a name="remarks"></a>Hinweise  
Mit dem Prozedurcache werden kompilierte und ausführbare Pläne zwischengespeichert, um die Ausführung von Batches zu beschleunigen. Die Einträge in einem Prozedurcache erfolgen auf Batchebene. Der Prozedurcache schließt die folgenden Einträge ein:
-   Kompilierte Pläne  
-   Ausführungsplan  
-   Algebraisierungsststruktur  
-   Erweiterte Prozeduren  
  
## <a name="result-sets"></a>Resultsets  
In der folgenden Tabelle werden die Spalten des Resultsets beschrieben.
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**NUM Proc beliebt**|Gesamtanzahl von Seiten, die von allen Einträgen im Prozedurcache verwendet werden.|  
|**NUM Proc beliebt verwendet**|Gesamtanzahl von Seiten, die von allen zurzeit verwendeten Einträgen verwendet werden.|  
|**NUM Proc beliebt active**|Nur aus Gründen der Abwärtskompatibilität beibehalten Gesamtanzahl von Seiten, die von allen zurzeit verwendeten Einträgen verwendet werden.|  
|**Proc-Cachegröße**|Gesamtanzahl von Einträgen im Prozedurcache.|  
|**Proc-Caches**|Gesamtanzahl von Einträgen, die zurzeit verwendet werden.|  
|**Proc Cache aktiv**|Nur aus Gründen der Abwärtskompatibilität beibehalten Gesamtanzahl von Einträgen, die zurzeit verwendet werden.|  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner** .
  
## <a name="see-also"></a>Siehe auch  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

