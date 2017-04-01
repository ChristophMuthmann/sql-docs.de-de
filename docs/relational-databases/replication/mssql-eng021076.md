---
title: "MSSQL_ENG021076 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG021076 (Fehler)"
ms.assetid: 612e5c59-ba3e-49c3-a3df-56bac3d850a2
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG021076
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21076|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Die Anfangsmomentaufnahme für den %1!s!-Artikel ist noch nicht verfügbar.|  
  
## Erklärung  
 Der Fehler MSSQL_ENG021076 wird ausgelöst, wenn der Verteilungs-Agent gestartet wird, bevor der Momentaufnahme-Agent mit dem Generieren der Momentaufnahmen fertig ist. Dieser Fehler wird nur ausgelöst, wenn die Veröffentlichung einen einzigen Artikel enthält. Wenn die Veröffentlichung mehr als einen Artikel enthält, wird stattdessen der Fehler MSSQL_ENG021075 ausgelöst. Weitere Informationen finden Sie unter [MSSQL_ENG021075](../../relational-databases/replication/mssql-eng021075.md).  
  
## Benutzeraktion  
 Wenn der Momentaufnahme-Agent für die Veröffentlichung seit der Erstellung des Abonnements oder seit dem letzten erneuten Initialisieren des Abonnements nicht mehr gestartet wurde, starten Sie den Momentaufnahme-Agent, und lassen Sie ihn die Momentaufnahme fertig generieren, bevor Sie den Verteilungs-Agent starten. Weitere Informationen finden Sie unter [Erstellen und Anwenden der Momentaufnahme](../../relational-databases/replication/create-and-apply-the-snapshot.md).  
  
 Wenn der Momentaufnahme-Agent die Momentaufnahme nicht fertig generiert, überprüfen Sie den Verlauf des Momentaufnahme-Agents auf Fehler, und sorgen Sie für deren Behebung. Weitere Informationen zum Anzeigen des Status und zu Fehlerdetails im Replikationsmonitor, finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents verknüpft sind mit einer Publikation & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
 Wenn der Fehler weiterhin auftritt, erhöhen Sie die Protokollierungsstufe des Agents, und geben Sie eine Ausgabedatei für das Protokoll an. Je nach Zusammenhang, in dem der Fehler auftritt, finden Sie hier möglicherweise die Schritte, die zum Fehler führen, und/oder weitere Fehlermeldungen.  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  