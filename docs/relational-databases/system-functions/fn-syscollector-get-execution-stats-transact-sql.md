---
title: Fn_syscollector_get_execution_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_syscollector_get_execution_stats
- fn_syscollector_get_execution_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: fn_syscollector_get_execution_stats function
ms.assetid: 793ad72c-a992-4a8d-8584-bcb6b3b476f1
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6dbdb0794058c51f43fd760096623ded58aee789
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="fnsyscollectorgetexecutionstats-transact-sql"></a>fn_syscollector_get_execution_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt ausführliche Statistiken zum Sammlungssatz oder Paket zurück, einschließlich der vom Datenflusstask eines Pakets protokollierten Anzahl der Fehlerzeilen. Wird von ein Datenflusstask eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Komponente, die Daten verarbeitet. Diese Daten befinden sich in relationalem Format, wodurch sie über ein Eingabe- und ein Ausgabedataset verfügen, die aus Zeilen bestehen.  
  
 Die Statistik wird auf Grundlage von Einträgen in der syscollector_execution_stats-Sicht berechnet.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn_syscollector_get_execution_stats ( log_id )  
```  
  
## <a name="arguments"></a>Argumente  
 *log_id*  
 Der lokale eindeutige Bezeichner für das Ausführungsprotokoll. *log_id* ist **int**  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|avg_row_count_in|**int**|Durchschnittliche Anzahl von Zeilen, die in die Datenflusstasks des Pakets eingetreten sind.<br /><br /> Hinweis: Ein Datenflusstasks ist ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Komponente, die Daten verarbeitet. Diese Daten befinden sich in relationalem Format, wodurch sie über ein Eingabedataset verfügen, das aus Zeilen besteht. Anzahl der Zeilen, die in den Task eingetreten sind. Nachdem die Daten umgewandelt wurden, werden sie als ein Resultset ausgegeben, das aus Zeilen besteht. Der Datenflusstask wandelt die Daten um und gibt ein Resultset aus, das aus Zeilen besteht. Diese Ausgabe entspricht der Anzahl der Zeilen, die den Task verlassen haben.|  
|min_row_count_in|**int**|Minimale Anzahl von Zeilen, die in die Datenflusstasks des Pakets eingetreten sind.|  
|max_row_count_in|**int**|Maximale Anzahl von Zeilen, die in die Datenflusstasks des Pakets eingetreten sind.|  
|avg_row_count_out|**int**|Durchschnittliche Anzahl von Zeilen, die die Datenflusstasks des Pakets verlassen haben.|  
|min_row_count_out|**int**|Minimale Anzahl von Zeilen, die die Datenflusstasks des Pakets verlassen haben.|  
|max_row_count_out|**int**|Maximale Anzahl von Zeilen, die den Datenflusstasks des Pakets verlassen haben.|  
|avg_duration|**int**|Durchschnittliche Verweildauer (in Millisekunden) in der Datenflusskomponente des Pakets.|  
|min_duration|**int**|Minimale Verweildauer (in Millisekunden) in der Datenflusskomponente des Pakets.|  
|max_duration|**int**|Maximale Verweildauer (in Millisekunden) in der Datenflusskomponente des Pakets.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT für **dc_operator**.  
  
## <a name="see-also"></a>Siehe auch  
 [Syscollector_execution_stats &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)  
  
  
