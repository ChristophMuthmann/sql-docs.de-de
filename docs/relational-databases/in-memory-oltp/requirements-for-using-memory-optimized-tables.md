---
title: "Anforderungen für die Verwendung speicheroptimierter Tabellen | Microsoft-Dokumentation"
ms.custom: SQL2016_New_Updated
ms.date: 11/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
caps.latest.revision: "65"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: de8c79ca45f7b02e25a893afd017c38c25340f2d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="requirements-for-using-memory-optimized-tables"></a>Anforderungen für die Verwendung von speicheroptimierten Tabellen
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Informationen zum Verwenden von In-Memory-OLTP in Azure-Datenbanken finden Sie unter [Erste Schritte mit In-Memory in SQL-Datenbanken](http://azure.microsoft.com/documentation/articles/sql-database-in-memory/).  
  
 Zusätzlich zu den [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)gilt für die Verwendung von In-Memory-OLTP Folgendes:  
  
-   SQL Server 2016 SP1( oder höher), jede Edition. Für SQL Server 2014 und SQL Server 2016 RTM (vor SP1) benötigen Sie die Enterprise, Developer oder Evaluation Edition.
    - Hinweis: In-Memory-OLTP erfordert die 64-Bit-Version von SQL Server.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] benötigt ausreichend Arbeitsspeicher, um die Daten in speicheroptimierten Tabellen und Indizes aufzunehmen. Des Weiteren wird zusätzlicher Speicherplatz für die Unterstützung der Online-Arbeitsauslastung benötigt. Weitere Informationen finden Sie unter [Schätzen der Arbeitsspeicheranforderungen speicheroptimierter Tabellen](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) .  

-   Stellen Sie bei der Ausführung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem virtuellen Computer (VM) sicher, dass genügend Arbeitsspeicher dem virtuellen Computer zugewiesen ist, sodass der Arbeitsspeicher unterstützt wird, der für speicheroptimierte Tabellen und Indizes benötigt wird. Abhängig von der VM-Hostanwendung wird die Konfigurationsoption zum Garantieren von Speicherbelegung für die VM „reservierter Speicher“ genannt, oder „Mindestarbeitsspeicher“ bei Verwendung von dynamischer Arbeitsspeicherverwaltung. Stellen Sie sicher, dass diese Einstellungen für die Anforderungen der Datenbanken in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausreichend sind.
  
-   Geben Sie Speicherplatz frei, der zweimal der Größe der dauerhaften speicheroptimierten Tabellen entspricht.  
  
-   Der Prozessor muss die **cmpxchg16b** -Anweisung unterstützen, um In-Memory-OLTP verwenden zu können. Alle modernen 64-Bit-Prozessoren unterstützen **cmpxchg16b**.  
  
     Wenn Sie eine VM-Hostanwendung verwenden und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler anzeigt, der von einem älteren Prozessor verursacht wird, sollten Sie überprüfen, ob die Anwendung eine Konfigurationsoption zum Aktivieren von **cmpxchg16b**enthält. Andernfalls können Sie Hyper-V verwenden, das **cmpxchg16b** ohne Änderung einer Konfigurationsoption unterstützt.  
  
-   In-Memory-OLTP wird als Teil von **Database Engine Services**installiert.  
  
     Zum Installieren der Berichtgenerierung ([Bestimmen, ob eine Tabelle oder eine gespeicherte Prozedur zu In-Memory-OLTP portiert werden soll](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (um In-Memory-OLTP über den Objekt-Explorer von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zu verwalten) gehen Sie unter [Herunterladen von SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).   
  
## <a name="important-notes-on-using-includehek2includeshek-2-mdmd"></a>Wichtige Anmerkungen zur Verwendung von [!INCLUDE[hek_2](../../includes/hek-2-md.md)]  
  
-   Beim Start von SQL Server 2016 ist die Größe für speicheroptimierte Tabellen unbeschränkt. Dies gilt jedoch nicht für den verfügbaren Arbeitsspeicher. Die Gesamtgröße aller dauerhaften Tabellen in einer Datenbank in SQL Server 2014 sollte im Arbeitsspeicher maximal 250 GB für SQL Server 2014-Datenbanken betragen. Weitere Informationen finden Sie unter [Schätzen der Arbeitsspeicheranforderungen speicheroptimierter Tabellen](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md).  
    - Hinweis: Ab SQL Server 2016 SP1 unterstützen Standard und Express Edition In-Memory OLTP, aber sie bedingen Kontingente für die Menge an Arbeitsspeicher, die Sie für speicheroptimierte Tabellen in einer bestimmten Datenbank verwenden können. In Standard Edition sind dies 32 GB pro Datenbank. In Express Edition sind dies 352 MB pro Datenbank. 
  
-   Wenn Sie eine oder mehrere Datenbanken mit speicheroptimierten Tabellen erstellen, sollten Sie die sofortige Dateiinitialisierung für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz aktivieren (also dem Dienststartkonto für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das Benutzerrecht SE_MANAGE_VOLUME_NAME erteilen). Ohne die sofortige Dateiinitialisierung werden speicheroptimierte Speicherdateien (Daten- und Änderungsdateien) bei der Erstellung initialisiert, was sich negativ auf die Leistung der Arbeitsauslastung auswirken kann. Weitere Informationen zur sofortigen Dateiinitialisierung finden Sie unter [Datenbankdatei-Initialisierung](http://msdn.microsoft.com/library/ms175935\(SQL.105\).aspx). Informationen dazu, wie die sofortige Dateiinitialisierung aktiviert wird, finden Sie unter [Wie und warum die sofortige Dateiinitialisierung aktiviert werden sollte](http://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx).  
  
## <a name="see-also"></a>Siehe auch  
 [In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
