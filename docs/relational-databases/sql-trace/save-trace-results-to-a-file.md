---
title: Speichern von Ablaufverfolgungsergebnissen in einer Datei | Microsoft-Dokumentation
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
ms.assetid: 74f80667-62f3-4e14-bb1a-f0c2b6ef3402
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6555bf45840676342a9df3b37fee8830bfed246f
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2018
---
# <a name="save-trace-results-to-a-file"></a>Speichern von Ablaufverfolgungsergebnissen in einer Datei
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Ablaufverfolgungsergebnisse können in einer Datei gespeichert werden. Die Ablaufverfolgungsergebnisse werden in eine Ablaufverfolgungsdatei geschrieben. Eine Ablaufverfolgungsdatei kann in einem lokalen Verzeichnis (z. B.\\*Ordnername*\\*Dateiname.trc*) oder in einem Netzwerkverzeichnis (z. B. \\\Computername\Freigabename\Dateiname.trc) gespeichert sein.  
  
 Die Ablaufverfolgungsdateien können für die folgenden Aufgaben verwendet werden:  
  
-   Wiedergeben von Ablaufverfolgungen  
  
-   Überwachen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Ausführen einer Leistungsanalyse  
  
-   Korrelation von Ablaufverfolgungsereignissen mit Leistungsindikatoren zur Optimierung der Suche nach Problemen  
  
-   Datenbankmodul-Optimierungsratgeber-Analyse  
  
-   Ausführen der Abfrageoptimierung  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speichert Ablaufverfolgungsergebnisse in einer Datei, wenn ein Pfad und ein Dateiname für das Argument **@tracefile** der gespeicherten Prozedur **sp_trace_create**angegeben sind.  
  
> [!NOTE]  
>  Wenn ein Pfad zur gespeicherten Prozedur **sp_trace_create** zum Speichern der Ablaufverfolgungsdatei angegeben ist, muss der Server Zugriff auf das Verzeichnis haben. Achten Sie auch darauf, dass es sich bei Angabe eines lokalen Verzeichnisses für **sp_trace_create**um ein lokales Verzeichnis auf dem Servercomputer handelt.  
  
 Wenn [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] verwendet wird, können Sie Ablaufverfolgungsergebnisse in einer Datei oder Tabelle speichern. Das Speichern von Ablaufverfolgungsergebnissen in einer Tabelle ermöglicht den gleichen Zugriff wie beim Speichern der Ablaufverfolgung in einer Datei. Außerdem können Sie für die Tabelle Abfragen ausführen, um nach bestimmten Ereignissen zu suchen.  
  
 Weitere Informationen zum Speichern von Ablaufverfolgungsergebnissen finden Sie unter [Speichern von Ablaufverfolgungsergebnissen in einer Tabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md) und [Speichern von Ablaufverfolgungsergebnissen in einer Datei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [Erstellen einer Ablaufverfolgung &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [Erstellen einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
