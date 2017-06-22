---
title: MSSQLSERVER_14421 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 14421 (Database Engine error)
ms.assetid: 03e76d4a-d463-4673-8843-08e4ecaefe27
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cc4a06f7b9b27884ac0a5998d43ef056368dcc73
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver14421"></a>MSSQLSERVER_14421
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|14421|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SQLErrorNum14421|  
|Meldungstext|Die sekundäre Datenbank für den Protokollversand, %s.%s, weist eine Wiederherstellungsschwelle von %d Minuten auf und ist nicht mehr synchronisiert. Während %d Minuten wurde keine Wiederherstellung ausgeführt. Die Wiederherstellungslatenzzeit beträgt %d Minuten. Überprüfen Sie das Agentprotokoll und die Informationen des Protokollversandmonitors.|  
  
## <a name="explanation"></a>Erklärung  
Mit dieser Meldung wird angegeben, dass der Protokollversand außerhalb der Wiederherstellungsschwelle nicht mehr synchronisiert ist. Bei der Wiederherstellungsschwelle handelt es sich um eine Zeit in Minuten, die zwischen den Wiederherstellungsvorgängen vergehen kann, bevor eine Meldung erzeugt wird.  
  
### <a name="possible-causes"></a>Mögliche Ursachen  
Mit dieser Meldung wird nicht unbedingt ein Problem beim Protokollversand angegeben. Stattdessen wird mit dieser Meldung eines der folgenden Probleme angegeben:  
  
-   Der Wiederherstellungsauftrag wird nicht ausgeführt.  
  
    Folgende mögliche Ursachen können vorliegen, dass der Auftrag nicht ausgeführt wird: Der SQL Server-Agent-Dienst in der sekundären Serverinstanz wird nicht ausgeführt, der Auftrag wurde deaktiviert, oder der Zeitplan für den Auftrag wurde geändert.  
  
-   Fehler beim Wiederherstellungsauftrag.  
  
    Folgende mögliche Ursachen können für den Fehler beim Auftrag vorliegen: Der Pfad des Wiederherstellungsordners ist nicht gültig, der Datenträger ist voll, oder es liegt ein anderer Grund vor, wonach ein Fehler bei der RESTORE-Anweisung auftritt.  
  
## <a name="user-action"></a>Benutzeraktion  
So beheben Sie das mit dieser Meldung angegebene Problem:  
  
-   Stellen Sie sicher, dass der SQL Server-Agent-Dienst in der sekundären Serverinstanz ausgeführt wird, dass der Wiederherstellungsauftrag für diese sekundäre Datenbank aktiviert ist und dass er so geplant ist, dass er in der entsprechenden Häufigkeit ausgeführt wird.  
  
-   Möglicherweise tritt beim Wiederherstellungsauftrag auf dem sekundären Server ein Fehler auf. Überprüfen Sie in diesem Fall den Auftragsverlauf für den Wiederherstellungsauftrag, und suchen Sie nach der Ursache.  
  
-   Für den in der sekundären Serverinstanz ausgeführten Wiederherstellungsauftrag des Protokollversands kann möglicherweise keine Verbindung mit der Überwachungsserverinstanz hergestellt werden, um die **log_shipping_monitor_secondary**-Tabelle zu aktualisieren. Dies beruht möglicherweise auf einem Authentifizierungsproblem zwischen der Überwachungsserverinstanz und der sekundären Serverinstanz.  
  
-   Die Sicherungswarnschwelle weist möglicherweise einen falschen Wert auf. Im Idealfall ist dieser Wert auf den dreifachen Wert der Häufigkeit festgelegt, mit der der Wiederherstellungsauftrag ausgeführt wird. Wenn Sie die Häufigkeit für den Wiederherstellungsauftrag ändern, nachdem der Protokollversand konfiguriert und ausgeführt wurde, müssen Sie den Wert für die Sicherungswarnschwelle entsprechend aktualisieren.  
  
-   Wenn die Überwachungsserverinstanz offline geschaltet und anschließend wieder online geschaltet wird, wird die **log_shipping_monitor_secondary**-Tabelle erst dann mit den aktuellen Werten aktualisiert, wenn der Warnmeldungsauftrag ausgeführt wurde. Der Fehler 14421 kann ausgelöst werden, wenn ein Wiederherstellungsauftrag mit folgender Meldung erfolgreich ausgeführt wurde: "Für die sekundäre Datenbank wurde keine anwendbare Protokollsicherungsdatei gefunden." Wenn dieser Fehler auftritt, wird der Speicherzeitpunkt nicht aktualisiert. Möglicherweise beruht der Fehler in diesem Fall auf einem Problem mit dem Kopierauftrag.  
  
    Wenn Sie die Überwachungstabellen mit den neuesten Daten für die sekundäre Datenbank aktualisieren möchten, führen Sie **sp_refresh_log_shipping_monitor** in der sekundären Serverinstanz aus.  
  
-   Das Datum oder die Uhrzeit in der sekundären Serverinstanz oder in der Überwachungsserverinstanz ist nicht richtig. Dadurch werden möglicherweise Warnmeldungen generiert. Möglicherweise wurde das Systemdatum oder die Systemuhrzeit für eine der Instanzen geändert.  
  
    > [!NOTE]  
    > Unterschiedliche Zeitzonen für die beiden Serverinstanzen sollten kein Problem darstellen.  
  
## <a name="see-also"></a>Siehe auch  
[log_shipping_monitor_secondary &#40;Transact-SQL&#41;](~/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql.md)  
[Informationen zum Protokollversand &#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
[sp_help_log_shipping_monitor_secondary &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)  
[sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql.md)  
[Informationen zum Protokollversand &#40;SQL Server&#41;](~/database-engine/log-shipping/about-log-shipping-sql-server.md)  
  

