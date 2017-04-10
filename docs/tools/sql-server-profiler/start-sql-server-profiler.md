---
title: "Starten von SQL Server Profiler | Microsoft Docs"
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
  - "Profiler [SQL Server Profiler], starten"
  - "SQL Server Profiler, starten"
  - "Starten von SQL Server Profiler"
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# Starten von SQL Server Profiler
  Sie können [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] in einer Reihe von Szenarien auf verschiedene Arten starten, um das Erfassen der Ablaufverfolgungsausgabe zu unterstützen. Sie können [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] auf unterschiedliche Weise starten: über das Menü **Start** , über das Menü **Extras** im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber und über verschiedene Positionen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Wenn Sie [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zum ersten Mal starten und im Menü **Datei** die Option **Neue Ablaufverfolgung** auswählen, zeigt die Anwendung das Dialogfeld **Verbindung mit Server herstellen** an, in dem Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angeben können, mit der eine Verbindung hergestellt werden soll.  
  
### So starten Sie SQL Server Profiler aus dem Startmenü  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], zeigen Sie auf **Leistungstools**, und klicken Sie dann auf **SQL Server Profiler**.  
  
### So starten Sie SQL Server Profiler im Datenbankmodul-Optimierungsratgeber  
  
1.  Klicken Sie im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber im Menü **Extras** auf **SQL Server Profiler**.  
  
## So starten Sie SQL Server Profiler in Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] startet jede Profilersitzung in einer eigenen Instanz und wird weiterhin ausgeführt, wenn Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]herunterfahren.  
  
 Sie können [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] von mehreren Positionen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aus starten, wie in den folgenden Prozeduren erläutert. Wenn [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] gestartet wird, lädt es den Verbindungskontext, die Ablaufverfolgungsvorlage und den Filterkontext seines Startpunkts.  
  
#### So starten Sie SQL Server Profiler über das Menü "Extras"  
  
1.  Klicken Sie im [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Extras** auf **SQL Server Profiler**.  
  
#### So starten Sie SQL Server Profiler über den Abfrage-Editor  
  
1.  Klicken Sie in der [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] -Menüleiste auf **Neue Abfrage**.  
  
2.  Klicken Sie im Abfrage-Editor mit der rechten Maustaste, und wählen Sie dann **Ablaufverfolgungsabfrage in SQL Server Profiler** aus.  
  
    > [!NOTE]  
    >  Der Verbindungskontext ist die Editor-Verbindung, die Ablaufverfolgungsvorlage lautet TSQL_SPs, und der angewendete Filter ist SPID = Abfragefenster-SPID.  
  
#### So starten Sie SQL Server Profiler über den Aktivitätsmonitor  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und klicken Sie dann auf **Aktivitätsmonitor**.  
  
2.  Klicken Sie auf den Bereich **Prozesse**, klicken Sie mit der rechten Maustaste auf den Prozess, für den Sie ein Profil erstellen möchten, und klicken Sie dann auf **Ablaufverfolgungsprozess in SQL Server Profiler**.  
  
    > [!NOTE]  
    >  Wenn ein Prozess ausgewählt ist, ist der Verbindungskontext die Verbindung für den Objekt-Explorer, und zwar so, wie sie war, als der Aktivitätsmonitor geöffnet wurde. Die Ablaufverfolgungsvorlage ist der auf dem Servertyp basierende Standard, und die SPID entspricht der SPID für den ausgewählten Prozess.  
  
## .NET Framework-Sicherheit  
 Im Windows-Authentifizierungsmodus muss das Benutzerkonto, das zum Ausführen von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] verwendet wird, die Berechtigung haben, eine Verbindung zu einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herzustellen.  
  
 Zum Ausführen der Ablaufverfolgung mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] müssen die Benutzer außerdem die ALTER TRACE-Berechtigung haben.  
  
## Siehe auch  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [Verwenden von SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
  
  