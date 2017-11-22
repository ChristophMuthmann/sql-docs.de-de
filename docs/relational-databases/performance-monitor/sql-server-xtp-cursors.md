---
title: SQL Server-XTP-Cursor | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 84bf4654-3ef7-4d7f-a269-c8bb4ed4acad
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ce11b76c47faa36406452c707c8246a3dfd1d7b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-xtp-cursors"></a>SQL Server-XTP-Cursor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Das Leistungsobjekt für SQL Server-XTP-Cursor enthält Leistungsindikatoren für interne Cursor des In-Memory-OLTP-Moduls. Cursor sind die Bausteine auf unterer Ebene, die das In-Memory-OLTP-Modul zur Verarbeitung von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragen verwendet. Daher können Sie diese in der Regel nicht direkt steuern.  
  
 In dieser Tabelle werden die Leistungsindikatoren für **SQL Server-XTP-Cursor** beschrieben.  
  
|Leistungsindikator|Beschreibung|  
|-------------|-----------------|  
|**Cursorlöschvorgänge/s**|Die durchschnittliche Anzahl der pro Sekunde erfolgten Cursorlöschvorgänge.|  
|**Cursoreinfügevorgänge/s**|Die durchschnittliche Anzahl der pro Sekunde erfolgten Cursoreinfügevorgänge.|  
|**Gestartete Cursorscans/s**|Die durchschnittliche Anzahl der pro Sekunde gestarteten Cursorscans.|  
|**Cursor-UNIQUE-Verstöße/s**|Die durchschnittliche Anzahl der pro Sekunde erfolgten Verstöße gegen die UNIQUE-Einschränkung.|  
|**Cursorupdates/s**|Die durchschnittliche Anzahl der pro Sekunde erfolgten Cursorupdates.|  
|**Cursorschreibkonflikte/s**|Die durchschnittliche Anzahl der pro Sekunde erfolgten Write-Write-Konflikte in dieselbe Zeilenversion.|  
|**Dusty-Corner-Scanwiederholungen/s (durch den Benutzer ausgegeben)**|Die durchschnittliche Anzahl von Scanwiederholungen aufgrund von Schreibkonflikten während Dusty-Corner-Sweep-Vorgängen, die pro Sekunde durch vollständige Tabellenscans eines Benutzers ausgegeben werden. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|  
|**Entfernte abgelaufene Zeilen/s**|Die durchschnittliche Anzahl abgelaufener Zeilen, die pro Sekunde von Cursorn entfernt werden.|  
|**Berührte abgelaufene Zeilen/s**|Die durchschnittliche Anzahl abgelaufener Zeilen, die pro Sekunde von Cursorn berührt werden.|  
|**Zurückgegebene Zeilen/s**|Die durchschnittliche Anzahl von Zeilen, die pro Sekunde von Cursorn zurückgegeben werden.|  
|**Berührte Zeilen/s**|Die durchschnittliche Anzahl von Zeilen, die pro Sekunde von Cursorn berührt werden.|  
|**Berührte vorläufig gelöschte Zeilen/s**|Die durchschnittliche Anzahl ablaufender Zeilen, die pro Sekunde von Cursorn berührt werden. Eine Zeile läuft ab, wenn die Transaktion, durch die sie gelöscht wurde, immer noch aktiv ist (d. h., es wurde noch kein Commit ausgeführt bzw. sie wurde nicht abgebrochen).|  
  
## <a name="see-also"></a>Siehe auch  
 [Leistungsindikatoren für SQL Server XTP &#40;In-Memory OLTP&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
