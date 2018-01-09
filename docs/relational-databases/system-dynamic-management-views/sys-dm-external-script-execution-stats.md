---
title: dm_external_script_execution_stats | Microsoft Docs
ms.custom: 
ms.date: 09/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_execution_stats
- sys.dm_external_script_execution_stats_TSQL
- dm_external_script_execution_stats
- dm_external_script_execution_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_external_script_execution_stats dynamic management view
ms.assetid: 2e99f026-ceb2-42a2-a549-c71d31ed0cf4
caps.latest.revision: "5"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a80c26130d5671dd387122930e599a2c33a5db60
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="sysdmexternalscriptexecutionstats"></a>sys.dm_external_script_execution_stats
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]


  Gibt eine Zeile für jeden Typ von externer Skriptanforderung zurück. Die externen Skriptanforderungen werden nach der unterstützten externen Skriptsprache gruppiert. Für jede externe Skriptfunktion wird eine Zeile generiert. Beliebige externe Skriptfunktionen werden nicht aufgezeichnet, sofern sie nicht von einem übergeordneten Prozess wie `rxExec`gesendet werden.

 
  
> [!NOTE]  
>  Diese dynamische Verwaltungssicht ist nur verfügbar, wenn Sie die Funktion installiert und aktiviert haben, die die Ausführung von externen Skripts unterstützt. Informationen zur Vorgehensweise bei R-Skripts finden Sie unter [Einrichten von SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|Sprache|**nvarchar**|Name der registrierten externen Skriptsprache. Jedes externe Skript muss die Sprache in der Skriptanforderung angeben, um das zugehörige Startprogramm zu starten. |  
|counter_name|**nvarchar**|Name einer registrierten externen Skriptfunktion. Lässt keine NULL-Werte zu.|  
|counter_value|**integer**|Gesamtanzahl der Instanzen, die von der registrierten externen Skriptfunktion auf dem Server aufgerufen wurden. Dieser Wert ist kumulativ und beginnt mit dem Zeitpunkt, zu dem das Feature auf der Instanz installiert wurde. Der Wert kann nicht zurückgesetzt werden.|  

  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
> [!NOTE]  
>  Benutzer, die externe Skripts ausführen, müssen die zusätzliche Berechtigung EXECUTE ANY EXTERNAL SCRIPT haben, aber diese dynamische Verwaltungssicht kann von Administratoren ohne diese Berechtigung verwendet werden. 
  
## <a name="remarks"></a>Hinweise  
  Diese dynamische Verwaltungssicht wird für die interne Telemetrie bereitgestellt, um die Gesamtauslastung des neuen Features zur externen Skriptausführung in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] zu überwachen. Der Telemetriedienst wird mit Launchpad gestartet und inkrementiert jedes Mal einen datenträgerbasierten Zähler, wenn eine registrierte externe Skriptfunktion aufgerufen wird.

Leistungsindikatoren sind im Allgemeinen nur so lange gültig, wie der Prozess aktiv ist, der sie generiert hat. Daher kann eine Abfrage für eine DMV keine ausführlichen Daten für Dienste anzeigen, die beendet wurden. Wenn ein Startprogramm z. B. ein externes Skript ausführt und es sehr schnell abschließt, kann eine konventionelle DMV möglicherweise keine Daten anzeigen.

Daher bleiben die von der DMV verfolgten Leistungsindikatoren aktiv und der Status für „sys.dm_external_script_requests“ wird beibehalten, indem Schreibvorgänge auf den Datenträger verwendet werden, auch wenn die Instanz heruntergefahren wird.

   
  
### <a name="r-counter-values"></a>R-Leistungsindikatorwerte
 Derzeit ist R die einzige in [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)] unterstützte externe Skriptsprache. Externe Skriptanforderungen für die Sprache R werden von [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] behandelt. 

Für R verfolgt diese DMV die Anzahl der R-Aufrufe, die vorgenommen werden, auf einer Instanz. Wenn `rxLinMod` z. B. parallel aufgerufen und ausgeführt wird, wird der Leistungsindikator um 1 erhöht.
 
Für die Sprache R stellen die im Feld *counter_name* angezeigten Leistungsindikatorwerte die Namen von registrierten ScaleR-Funktionen dar. Die Werte im Feld *counter_value* stellen die kumulierte Anzahl von Instanzen für die bestimmte ScaleR-Funktion dar. 

Die Zählung beginnt, wenn das Feature für die Instanz installiert und aktiviert wird und bleibt kumulativ, bis die Datei, die den Status verwaltet, von einem Administrator gelöscht oder überschrieben wird. Daher ist es im Allgemeinen nicht möglich, die Werte in *counter_value*zurückzusetzen. Zum Überwachen der Nutzung nach Sitzung, Kalenderzeiten oder anderen Intervallen wird empfohlen, dass Sie die Leistungsindikatoren in einer Tabelle erfassen.

### <a name="registration-of-external-script-functions"></a>Registrierung externer Skriptfunktionen

Die R-Sprache unterstützt beliebige Skripts und die R-Community stellt viele Tausende Pakete bereit, die jeweils eigene Funktionen und Methoden enthalten. Diese DMV überwacht jedoch nur die ScaleR-Funktionen, die mit SQL Server-R Services installiert sind.

Die Registrierung dieser Funktionen wird beim Installieren des Features durchgeführt, und registrierte Funktionen können nicht hinzugefügt oder gelöscht werden.

## <a name="examples"></a>Beispiele  
  
### <a name="viewing-the-number-of-r-scripts-run-on-the-server"></a>Anzeigen der Anzahl der auf dem Server ausgeführten R-Skripts  
 Im folgenden Beispiel wird die kumulative Anzahl von externen Skriptausführungen für die R-Sprache angezeigt.  
  
```  
SELECT counter_name, counter_value   
FROM sys.dm_external_script_execution_stats   
WHERE language = 'R';
```  

  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungssichten und -funktionen im Zusammenhang mit der Ausführung &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md) 
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  

