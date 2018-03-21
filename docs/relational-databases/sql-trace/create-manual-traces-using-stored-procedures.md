---
title: Erstellen manueller Ablaufverfolgungen mit gespeicherten Prozeduren | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-trace
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f6f47fa2-7c17-41d4-9f69-9be144d56832
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 563a34e49fb7361245cf5b7365632688bf5af87b
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2018
---
# <a name="create-manual-traces-using-stored-procedures"></a>Erstellen manueller Ablaufverfolgungen mit gespeicherten Prozeduren
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt zum Erstellen von Ablaufverfolgungen für eine Instanz von [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Systemprozeduren zur Verfügung. Sie können aus Ihren Anwendungen heraus diese gespeicherten Systemprozeduren verwenden, um Ablaufverfolgungen statt mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]manuell zu erstellen. Dadurch können Sie benutzerdefinierte Anwendungen schreiben, die den speziellen Anforderungen Ihres Unternehmens entsprechen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 In der folgenden Tabelle werden die gespeicherten Systemprozeduren für die Ablaufverfolgung einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]aufgelistet.  
  
|Gespeicherte Prozedur|Ausgeführter Task|  
|----------------------|--------------------|  
|[sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)|Gibt die Informationen zu in einer Ablaufverfolgung enthaltenen Ereignisse zurück.|  
|[sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)|Gibt Informationen zu einer angegebene Ablaufverfolgung oder zu alle vorhandenen Ablaufverfolgungen zurück.|  
|[sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)|Erstellt eine Ablaufverfolgungsdefinition. Die neue Ablaufverfolgung weist einen beendeten Status auf.|  
|[sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)|Erstellt ein benutzerdefiniertes Ereignis.|  
|[sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)|Fügt einer Ablaufverfolgung eine Ereignisklasse oder eine Datenspalte hinzu oder entfernt eine Ereignisklasse oder eine Datenspalte aus einer Ablaufverfolgung.|  
|[sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)|Startet, beendet oder schließt eine Ablaufverfolgung.|  
|[sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)|Gibt Informationen über für eine Ablaufverfolgung angewendete Filter zurück.|  
|[sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)|Wendet einen neuen oder geänderten Filter für eine Ablaufverfolgung an.|  
  
 **So definieren Sie eine eigene Ablaufverfolgung mithilfe von gespeicherten Prozeduren**  
  
1.  Geben Sie die Ereignisse, die aufgezeichnet werden sollen, mit **sp_trace_setevent**an.  
  
2.  Geben Sie Ereignisfilter an. Weitere Informationen finden Sie unter [Festlegen eines Ablaufverfolgungsfilters &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md).  
  
3.  Geben Sie das Ziel für die aufgezeichneten Ereignisdaten mit **sp_trace_create** an.  
  
 Ein Beispiel zum Verwenden gespeicherter Prozeduren der Ablaufverfolgung finden Sie unter [Erstellen einer Ablaufverfolgung &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
 **So legen Sie die Standardeinstellungen für Ablaufverfolgungsdefinitionen fest**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
 **So legen Sie die Standardeinstellungen für die Ablaufverfolgungsanzeige fest**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **So erstellen Sie eine Ablaufverfolgung**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
 [Transact-SQL](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)  
  
 **So fügen Sie einer Ablaufverfolgungsvorlage Ereignisse hinzu bzw. entfernen sie**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Transact-SQL](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
