---
title: Erstellen manueller Ablaufverfolgungen mit gespeicherten Prozeduren | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f6f47fa2-7c17-41d4-9f69-9be144d56832
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1ee7ef604dc518fb4765ca5bd944c7fe01500035
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="create-manual-traces-using-stored-procedures"></a>Erstellen manueller Ablaufverfolgungen mit gespeicherten Prozeduren
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
  
  
