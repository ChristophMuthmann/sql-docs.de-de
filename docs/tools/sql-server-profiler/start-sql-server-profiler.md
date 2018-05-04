---
title: Führen Sie SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 7/7/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
- Profiler [SQL Server Profiler], running
- SQL Server Profiler, running
- running SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0179f93aa874667098d6f8ba2550129dec281ada
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="run-sql-server-profiler"></a>Ausführen von SQL Server Profiler
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Sie können [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] in einer Reihe von Szenarios auf verschiedene Arten ausführen, um das Erfassen der Ablaufverfolgungsausgabe zu unterstützen. Sie können [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] auf unterschiedliche Arten starten: über das **Startmenü** von Windows 10, über das Menü **Extras** im [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Optimierungsratgeber und über verschiedene Speicherorte in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
Wenn Sie [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zum ersten Mal starten und im Menü **Datei** die Option **Neue Ablaufverfolgung** auswählen, zeigt die Anwendung das Dialogfeld **Verbindung mit Server** herstellen an, in dem Sie eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angeben können, mit der eine Verbindung hergestellt wird.  
## <a name="to-start-sql-server-profiler-from-the-windows-10-start-menu"></a>So starten Sie SQL Server Profiler über das Startmenü von Windows 10  
-  Klicken Sie auf der Windows **starten** Symbol oder drücken Sie die Windows-Taste und damit beginnen, geben Sie "SQL Server Profiler 17". Wenn die **SQL Server Profiler 17** Kachel angezeigt wird, klicken Sie darauf.   

## <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>So starten Sie SQL Server Profiler im Datenbankmodul-Optimierungsratgeber  
-  Klicken Sie im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Optimierungsratgeber im Menü **Extras** auf **SQL Server Profiler**.  

## <a name="to-start-sql-server-profiler-in-sql-server-management-studio"></a>So starten SQL Server Profiler in SQL Server Management Studio  
 Sie können starten [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] über verschiedene Positionen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Wenn [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] gestartet wird, lädt er den Verbindungskontext, die Ablaufverfolgungsvorlage und den Filterkontext seines Startpunkts. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] startet jede profilersitzung in SQL Server in einer eigenen Instanz und Profiler wird weiterhin ausgeführt, wenn Sie Herunterfahren [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>So starten Sie SQL Server Profiler über das Menü "Extras"  
-  Klicken Sie im [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Extras** auf **SQL Server Profiler**.  

### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>So starten Sie SQL Server Profiler über den Abfrage-Editor  
- Klicken Sie im Abfrage-Editor mit der rechten Maustaste, und wählen Sie dann **Ablaufverfolgungsabfrage in SQL Server Profiler**aus.  

  > [!NOTE]  
  >  Der Verbindungskontext ist die Editor-Verbindung, die Ablaufverfolgungsvorlage lautet TSQL_SPs, und der angewendete Filter ist SPID = Abfragefenster-SPID.  
    
### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>So starten Sie SQL Server Profiler über den Aktivitätsmonitor  
- Klicken Sie im Aktivitätsmonitor auf den Bereich **Prozesse**, klicken Sie mit der rechten Maustaste auf den Prozess, für den Sie ein Profil erstellen möchten, und klicken Sie anschließend auf **Ablaufverfolgungsprozess in SQL Server Profiler**.  

    > [!NOTE]  
    >  Wenn ein Prozess ausgewählt ist, ist der Verbindungskontext die Verbindung für den Objekt-Explorer, und zwar so, wie sie war, als der Aktivitätsmonitor geöffnet wurde. Die Ablaufverfolgungsvorlage ist der auf dem Servertyp basierende Standard, und die SPID entspricht der SPID für den ausgewählten Prozess.  
    
## <a name="net-framework-security"></a>.NET Framework-Sicherheit  
- Im Windows-Authentifizierungsmodus muss das Benutzerkonto, das zum Ausführen von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] verwendet wird, die Berechtigung haben, eine Verbindung zur Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]herzustellen.  
- Zum Ausführen der Ablaufverfolgung mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]müssen die Benutzer außerdem die ALTER TRACE-Berechtigung haben.  

## <a name="next-steps"></a>Nächste Schritte  
 [Übersicht über die SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [Verwenden von SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
