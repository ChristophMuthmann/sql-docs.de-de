---
title: "&#196;ndern des Dienststartkontos f&#252;r SQL Server (SQL Server-Konfigurations-Manager) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/06/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server-Dienste, Startkontoänderungen"
  - "Startkonten [SQL Server]"
  - "Ändern von Startkonten für Dienste"
ms.assetid: d721c796-0397-46a7-901b-1a9a3c3fb385
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# &#196;ndern des Dienststartkontos f&#252;r SQL Server (SQL Server-Konfigurations-Manager)
  In diesem Thema wird die Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers zum Ändern der Startoptionen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste und zum Ändern der von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent, vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser, von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]verwendeten Dienstkonten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] oder PowerShell beschrieben. Weitere Informationen zum Auswählen eines geeigneten Dienstkontos finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
> [!IMPORTANT]  
>  Wenn Sie das Dienststartkonto für den [!INCLUDE[ssDE](../../includes/ssde-md.md)]- und den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent ändern, muss der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienst ([!INCLUDE[ssDE](../../includes/ssde-md.md)]) neu gestartet werden, damit die Änderung wirksam wird. Beim Neustart des Diensts stehen sämtliche dieser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz zugeordneten Datenbanken erst dann wieder zur Verfügung, wenn der Dienst erfolgreich neu gestartet wird. Wenn Sie das Dienststartkonto für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent ändern müssen, sollten Sie dies während regelmäßig geplanter Wartungen vornehmen oder wenn die Datenbank offline geschaltet werden kann, ohne dass dabei die Ausführung täglicher Vorgänge unterbrochen wird.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Gruppierte Server  
  
     Die Änderung des Dienstkontos für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]- oder den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent muss über den aktiven Knoten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Clusters ausgeführt werden.  
  
     Bei Ausführung unter Windows Server 2008 (in einer nicht dem Standard entsprechenden Konfiguration mit Domänengruppen) ist zum Ändern des Dienstkontos für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager erforderlich, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anzuhalten, indem die Ressourcengruppen offline geschaltet werden.  
  
-   SKU-Upgrade ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] auf andere SKU als Express)  
  
     Während der [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]-Installation wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Dienst für die Verwendung des Netzwerkdienstkontos konfiguriert. Dieser wird jedoch deaktiviert. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager kann das dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst zugewiesene Konto ändern, jedoch kann der Dienst nicht aktiviert oder gestartet werden. Nach einem SKU-Upgrade von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] auf eine andere SKU als Express wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Dienst nicht automatisch aktiviert. Dieser kann stattdessen bei Bedarf aktiviert werden, indem im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager der Dienststartmodus auf "Manuell" oder "Automatisch" festgelegt wird.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### So ändern Sie das Dienststartkonto für SQL Server  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, dann auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], danach auf **Konfigurationstools**, und klicken Sie auf **SQL Server-Konfigurations-Manager**.  
  
    > [!NOTE]  
    >  Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager ein Snap-In für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console und kein eigenständiges Programm ist, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager in neueren Versionen von Windows nicht als Anwendung angezeigt.  
    >   
    >  -   **Windows 10**:  
    >          Geben Sie zum Öffnen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Managers auf der **Startseite** Folgendes ein: SQLServerManager13.msc (für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Ersetzen Sie für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 13 durch eine kleinere Zahl. Durch Klicken auf „SQLServerManager13.msc“ wird der Konfigurations-Manager geöffnet. Um den Konfigurations-Manager an die Startseite oder Taskleiste anzuheften, klicken Sie mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **Dateispeicherort öffnen**. Klicken Sie im Windows-Explorer mit der rechten Maustaste auf „SQLServerManager13.msc“, und klicken Sie dann auf **An Startmenü anheften** oder **An Taskleiste anheften**.  
    > -   **Windows 8**:  
    >          Um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager zu öffnen, geben Sie im Charm **Suchen** unter **Apps** die Zeichenfolge **SQLServerManager\<Version>.msc** ein, z.B. **SQLServerManager13.msc**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Klicken Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager auf **SQL Server-Dienste**.  
  
3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf den Namen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz, dessen Dienststartkonto Sie ändern möchten, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie im Dialogfeld **Eigenschaften von SQL Server \<***Instanzname***>** auf die Registerkarte **Anmelden**, und wählen Sie einen **Anmelden als**-Kontotyp aus.  
  
5.  Klicken Sie nach Auswahl des neuen Dienststartkontos auf **OK**.  
  
     In einem Meldungsfenster werden Sie gefragt, ob Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst neu starten möchten.  
  
6.  Klicken Sie auf **Ja**, und schließen Sie dann den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager.  
  
## Siehe auch  
 [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../database-engine/configure-windows/start, stop, pause, resume, restart sql server services.md)   
 [Konfigurieren von WMI zum Anzeigen des Serverstatus in SQL Server-Tools](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  