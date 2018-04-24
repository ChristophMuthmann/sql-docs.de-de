---
title: Standardablaufverfolgung aktiviert (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], traces
- traces [SQL Server], logs
- default trace enabled option
ms.assetid: 1322d668-44f4-469e-8fd6-e0d02a81c8f2
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 291101a66e852d2897ad8cee5f36f90b6445872f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="default-trace-enabled-server-configuration-option"></a>Standardablaufverfolgung aktiviert (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Mit der Option **Standardablaufverfolgung aktiviert** können Sie die standardmäßigen Ablaufverfolgungsprotokolldateien aktivieren oder deaktivieren. Mit der Standardablaufverfolgung steht Ihnen ein umfassendes, persistentes Protokoll zu Aktivitäten und primär auf die Konfigurationsoptionen bezogenen Änderungen zur Verfügung.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen erweiterte Ereignisse.  
  
## <a name="purpose"></a>Zweck  
 Die Standardablaufverfolgung vereinfacht Datenbankadministratoren die Problembehandlung, indem die für die Diagnose von erstmalig auftretenden Problemen erforderlichen Protokolldaten zur Verfügung gestellt werden.  
  
## <a name="viewing"></a>Anzeigen  
 Die Standardablaufverfolgungsprotokolle können in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] geöffnet und überprüft werden oder mit [!INCLUDE[tsql](../../includes/tsql-md.md)] mithilfe der `fn_trace_gettable` -Systemfunktion abgefragt werden. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] können die Standard-Ablaufverfolgungsprotokolldateien wie normale Ablaufverfolgungsausgabedateien geöffnet werden. Das Protokoll für die Standardablaufverfolgung wird mithilfe einer Rollover-Ablaufverfolgungsdatei standardmäßig im Verzeichnis `\MSSQL\LOG` gespeichert. Der Basisdateiname für die Protokolldatei der Standardablaufverfolgung lautet `log.trc`. In einer typischen Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist die Standardablaufverfolgung aktiviert und erhält so TraceID 1. Wenn die Standardablaufverfolgung nach der Installation und dem Erstellen von anderen Ablaufverfolgungen aktiviert wird, kann die TraceID eine größere Zahl sein.  
  
 Weitere Informationen zum Anzeigen dieser Ablaufverfolgungsdatei mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler finden Sie unter [Öffnen einer Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md).  
  
### <a name="example"></a>Beispiel:  
 Durch die folgende Anweisung wird das Protokoll für die Standardablaufverfolgung im standardmäßigen Speicherort geöffnet:  
  
```  
SELECT *   
FROM fn_trace_gettable  
('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\LOG\log.trc', default);  
GO  
  
```  
  
## <a name="configuring"></a>Konfiguration  
 Wenn für die Option **Standardablaufverfolgung aktiviert** der Wert 1 festgelegt wird, ist die **Standardablaufverfolgung**aktiviert. Der Standardwert für diese Option ist 1 (EIN). Durch den Wert 0 wird die Ablaufverfolgung deaktiviert.  
  
 Bei der Option **Standardablaufverfolgung aktiviert** handelt es sich um eine erweiterte Option. Wenn Sie die Einstellung mithilfe der gespeicherten Systemprozedur **sp_configure** ändern, können Sie die Option **Standardablaufverfolgung aktiviert** nur ändern, wenn für **Erweiterte Optionen anzeigen** der Wert 1 festgelegt ist. Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
