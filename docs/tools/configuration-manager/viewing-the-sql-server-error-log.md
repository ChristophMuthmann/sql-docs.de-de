---
title: "Anzeigen des SQL Server-Fehlerprotokolls | Microsoft Docs"
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
  - "Durchnummerieren des SQL Server-Fehlerprotokolls"
  - "Ansehen des SQL Server-Fehlerprotokolls"
  - "Fehler [SQL Server], Protokolle"
  - "SQL Server-Fehlerprotokoll"
  - "Anzeigen des SQL Server-Fehlerprotokolls"
  - "Protokolle [SQL Server], SQL Server-Fehlerprotokolle"
ms.assetid: 6908c21a-65e3-458f-a272-fee256d86448
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Anzeigen des SQL Server-Fehlerprotokolls
  Zeigen Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll an, um sicherzustellen, dass bestimmte Prozesse erfolgreich abgeschlossen wurden (z.B. Sicherungs- und Wiederherstellungsvorgänge, Batchbefehle oder andere Skripts und Prozesse). Dies ist hilfreich, um aktuelle oder potenzielle Problembereiche zu ermitteln, einschließlich automatischer Wiederherstellungsmeldungen (insbesondere, wenn eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angehalten und neu gestartet wurde), Kernelmeldungen oder anderer Fehlermeldungen auf Serverebene.  
  
 Um das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll anzuzeigen, können Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder einen beliebigen Text-Editor verwenden. Weitere Informationen zum Anzeigen des Fehlerprotokolls finden Sie unter [Open Log File Viewer](../../relational-databases/logs/open-log-file-viewer.md). Standardmäßig befindet sich das Fehlerprotokoll unter `Program Files\Microsoft SQL Server\MSSQL.`*n*`\MSSQL\LOG\ERRORLOG` und `ERRORLOG.`*n* .  
  
 Es wird immer dann ein neues Fehlerprotokoll erstellt, wenn eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartet wird, obwohl die gespeicherte Systemprozedur [sp_cycle_errorlog](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md) zum Durchlaufen der Fehlerprotokolldateien verwendet werden kann, ohne dass die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu gestartet werden muss. In der Regel behält [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sicherungen der letzten sechs Protokolle bei. Dabei erhält die letzte Sicherung die Erweiterung .1, die zweitletzte Sicherung die Erweiterung .2 usw. Das aktuelle Fehlerprotokoll hat keine Erweiterung.  
  
 Beachten Sie, dass Sie auch das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll zu Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anzeigen können, die offline sind oder nicht gestartet werden können. Weitere Informationen finden Sie unter [Anzeigen von Offlineprotokolldateien](../../relational-databases/logs/view-offline-log-files.md).  
  
  