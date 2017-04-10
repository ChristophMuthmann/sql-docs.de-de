---
title: "&#220;berwachen der Fehlerprotokolle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Protokolle [SQL Server]"
  - "Datenbankleistung [SQL Server], Fehler"
  - "Windows-Anwendungsprotokolle [SQL Server]"
  - "Überwachen der Leistung [SQL Server], Fehler"
  - "Serverleistung [SQL Server], Fehler"
  - "Vergleichen der Ausgabe des Fehler- und Anwendungsprotokolls"
  - "Fehler [SQL Server], Protokolle"
  - "Optimieren von Datenbanken [SQL Server], Fehler"
  - "Datenbanküberwachung [SQL Server], Fehler"
  - "SQL Server-Fehlerprotokoll"
  - "Protokolle [SQL Server], SQL Server-Fehlerprotokolle"
  - "Fehlerprotokolle [SQL Server]"
  - "Protokolle [SQL Server], Windows-Anwendungsprotokolle"
ms.assetid: e250336b-0695-44f6-a42f-23222f94e377
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# &#220;berwachen der Fehlerprotokolle
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] protokolliert bestimmte Systemereignisse und benutzerdefinierte Ereignisse im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll und im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anwendungsprotokoll. Beide Protokolle versehen alle aufgezeichneten Ereignisse automatisch mit einem Zeitstempel. Sie können die Informationen im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll für die Problembehandlung bezüglich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwenden.  
  
 Das Windows-Anwendungsprotokoll bietet eine Gesamtübersicht der Ereignisse, die im Windows-Betriebssystem auftreten, sowie der Ereignisse in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents. Verwenden Sie die Windows-Ereignisanzeige, um das Windows-Anwendungsprotokoll anzuzeigen und die Informationen zu filtern. So können Sie beispielsweise Ereignisse, wie Informationen, Warnung, Fehler, Erfolgsüberwachung und Fehlerüberwachung, filtern.  
  
## Vergleichen der Ausgaben des Fehler- und Anwendungsprotokolls  
 Sie können sowohl das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll als auch das Windows-Anwendungsprotokoll verwenden, um die Ursache von Problemen zu identifizieren. Möglicherweise erhalten Sie während der Überwachung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokolls Fehlermeldungen, die keine Informationen zu den Ursachen enthalten. Durch Vergleichen der Daten und Zeiten der Ereignisse zwischen diesen Protokollen können Sie die Liste der wahrscheinlichen Ursachen eingrenzen. Der Protokolldatei-Viewer von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ermöglicht die Integration von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents und des Windows-Protokolls in eine einzelne Liste. Auf diese Weise können Sie zugehörige Serverereignisse und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ereignisse besser nachvollziehen. Weitere Informationen finden Sie im Thema zum Protokolldatei-Viewer in der SQL Server-Onlinedokumentation.  
  
## In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Anzeigen des SQL Server-Fehlerprotokolls](../../tools/configuration-manager/viewing-the-sql-server-error-log.md)|Enthält Informationen zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll und beschreibt das Anzeigen dieses Fehlerprotokolls.|  
|[Anzeigen des Windows-Anwendungsprotokolls](../../tools/configuration-manager/viewing-the-windows-application-log.md)|Enthält Informationen zum Windows-Fehlerprotokoll und beschreibt das Anzeigen dieses Fehlerprotokolls.|  
  
  