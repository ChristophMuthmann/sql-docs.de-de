---
title: Starten, Beenden, Anhalten, Fortsetzen und Neustarten von SQL Server-Diensten | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/26/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Configuration Manager, start and stop services
- stopping SQL Server Agent
- parameters [SQL Server], startup options
- SQL Server, startup options
- Database Engine [SQL Server], starting and stopping services
- pausing SQL Server
- PowerShell [SQL Server], starting and stopping services
- single-user mode [SQL Server], starting in
- SQL Server Management Studio [SQL Server], starting or stopping services
- stopping SQL Server Browser service
- starting SQL Server Agent
- default instances [SQL Server], starting and stopping
- SQL Server Agent, starting and stopping
- command prompt [SQL Server], starting and stopping SQL Server services
- continuing SQL Server
- starting SQL Server Database Engine
- net stop commands [SQL Server]
- command prompt [SQL Server], SQL Browser service
- Configuration Manager, start and stop services
- resuming SQL Server
- startup options [SQL Server]
- named instances [SQL Server], starting and stopping
- net start commands [SQL Server]
- SQL Server, starting and stopping
- stopping SQL Server
- starting SQL Server Browser service
- SQL Server Database Engine setting startup options
- administering SQL Server, starting and stopping services
- Management Studio [SQL Server], starting or stopping services
ms.assetid: 32660a02-e5a1-411a-9e57-7066ca459df6
caps.latest.revision: "20"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3671c010f2c17d4a7c0312a99312f6d0996e5735
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="start-stop-pause-resume-restart-sql-server-services"></a>Starten, Beenden, Anhalten, Fortsetzen und Neustarten von SQL Server-Diensten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > Informationen finden früheren Versionen von SQL Server finden Sie unter [Start Stop Pause Resume Restart the Database Engine SQL Server Agent or SQL Server Browser Service (Starten, Beenden, Anhalten, Fortsetzen und Neustarten von SQL Server-Agent, SQL Server-Browserdienst oder des Datenbankmoduls)](https://msdn.microsoft.com/en-US/library/hh403394(SQL.120).aspx).

  In diesem Thema wird beschrieben, wie das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent oder der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browserdienst mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager, mit  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], **net** -Befehlen von einer Eingabeaufforderung, mit [!INCLUDE[tsql](../../includes/tsql-md.md)]oder mit PowerShell gestartet, beendet, angehalten, fortgesetzt oder neu gestartet werden.  
  
-   **Vorbereitungen:**  
  
    -   [Was ist die Funktion dieser Dienste?](#Services)  
  
    -   [Zusätzliche Informationen](#MoreInformation)  
  
    -   [Security](#Security)  
  
-   **Anweisungen mit:**  
  
    -   [SQL Server-Konfigurations-Manager](#SSCMProcedure)  
  
    -   [SQL Server Management Studio](#SSMSProcedure)  
  
    -   [Net-Befehle von einem Eingabeaufforderungsfenster](#CommandPrompt)  
  
    -   [Transact-SQL](#TsqlProcedure)  
  
    -   [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Services"></a> Was ist die Funktion des [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Diensts, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Diensts und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browserdiensts?  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten sind ausführbare Programme, die als Windows-Dienst ausgeführt werden. Programme, die als Windows-Dienst ausgeführt werden, lassen sich ohne Anzeige von Aktivitäten auf dem Computerbildschirm weiterhin ausführen.  
  
 **[!INCLUDE[ssDE](../../includes/ssde-md.md)] Dienst**  
 Der ausführbare Prozess, der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]entspricht. [!INCLUDE[ssDE](../../includes/ssde-md.md)] kann der Standardinstanz (eine pro Computer) oder einer von vielen benannten Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)]entsprechen. Verwenden Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager, um zu bestimmen, welche Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf dem Computer installiert werden. Die Standardinstanz wird im Fall der Installation als **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)** aufgelistet. Benannte Instanzen werden im Fall der Installation als **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (<Instanzname>)** aufgelistet. Standardmäßig wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express als **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLEXPRESS)**installiert.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent-Dienst**  
 Entspricht einem Windows-Dienst, der geplante administrative Tasks ausführt, die als Aufträge und Warnungen bezeichnet werden. Weitere Informationen finden Sie unter [SQL Server Agent](http://msdn.microsoft.com/library/8d1dc600-aabb-416f-b3af-fbc9fccfd0ec). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent ist nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browserdienst**  
 Ein Windows-Dienst, der auf eingehende Anforderungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ressourcen lauscht und Clientinformationen zu den auf dem Computer installierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen bereitstellt. Eine einzelne Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browserdiensts wird für alle auf dem Computer installierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen verwendet.  
  
###  <a name="MoreInformation"></a> Zusätzliche Informationen  
  
-   Durch das Anhalten des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Diensts wird verhindert, dass neue Benutzer eine Verbindung mit [!INCLUDE[ssDE](../../includes/ssde-md.md)]herstellen. Benutzer, die bereits verbunden sind, können jedoch ihre Arbeit fortsetzen, bis die jeweilige Verbindung unterbrochen wird. Halten Sie den Dienst an, wenn Benutzer zuerst ihre Arbeit abschließen sollen, bevor Sie den Dienst beenden. Dadurch können sie Transaktionen abschließen, die gerade verarbeitet werden. Mit der Funktion zum Fortsetzen kann [!INCLUDE[ssDE](../../includes/ssde-md.md)] neue Verbindungen wieder zulassen. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst kann nicht angehalten oder fortgesetzt werden.  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zeigen den aktuellen Dienststatus an. Dazu werden folgende Symbole verwendet.  
  
     **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager**  
  
    -   Ein grüner Pfeil im Symbol neben dem Dienstnamen gibt an, dass der Dienst gestartet wurde.  
  
    -   Ein rotes Quadrat im Symbol neben dem Dienstnamen gibt an, dass der Dienst beendet wurde.  
  
    -   Zwei vertikale blaue Linien im Symbol neben dem Dienstnamen geben an, dass der Dienst angehalten wurde.  
  
    -   Beim Neustart von [!INCLUDE[ssDE](../../includes/ssde-md.md)]weist ein rotes Quadrat darauf hin, dass der Dienst beendet wurde. Ein grüner Pfeil gibt daraufhin an, dass der Dienst erfolgreich gestartet wurde.  
  
     **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
    -   Ein weißer Pfeil in einem grünen Kreis neben dem Dienstnamen gibt an, dass der Dienst gestartet wurde.  
  
    -   Ein weißes Quadrat in einem roten Kreis neben dem Dienstnamen gibt an, dass der Dienst beendet wurde.  
  
    -   Zwei vertikale weiße Linien in einem blauen Kreis neben dem Dienstnamen geben an, dass der Dienst angehalten wurde.  
  
-   Bei Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers oder bei Verwendung von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]sind nur mögliche Optionen verfügbar. Wurde der Dienst beispielsweise bereits gestartet, ist die Option **Start** nicht verfügbar.  
  
-   Im Fall der Ausführung auf einem Cluster lässt sich der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Dienst am besten mittels Clusterverwaltung verwalten.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Standardmäßig können nur Mitglieder der lokalen Administratorgruppe einen Dienst starten, beenden, anhalten, fortsetzen oder neu starten. Informationen dazu, wie Sie es Nichtadministratoren ermöglichen, Dienste zu verwalten, finden Sie unter [How to grant users rights to manage services in Windows Server 2003](http://support.microsoft.com/kb/325349)(So erteilen Sie Benutzern die Berechtigung zum Verwalten von Diensten in Windows Server 2003). (Dieser Vorgang ist bei anderen Versionen von Windows ähnlich.)  
  
 Das Beenden von [!INCLUDE[ssDE](../../includes/ssde-md.md)] unter Verwendung des [!INCLUDE[tsql](../../includes/tsql-md.md)]**SHUTDOWN** -Befehls erfordert die Mitgliedschaft in den festen **sysadmin** - oder **serveradmin** -Serverrollen. Diese Mitgliedschaft ist nicht übertragbar.  
  
##  <a name="SSCMProcedure"></a> Verwenden des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers  
  
#### <a name="starting-includessnoversionincludesssnoversion-mdmd-configuration-manager"></a>Starten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, dann auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], danach auf **Konfigurationstools**, und klicken Sie auf **SQL Server-Konfigurations-Manager**.  
  
     Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager ein Snap-In für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console und kein eigenständiges Programm ist, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager in neueren Versionen von Windows nicht als Anwendung angezeigt. Nachfolgend sind die Pfade der letzten vier Versionen aufgeführt (unter der Annahme, dass Windows auf Laufwerk C installiert wurde).  
  
    |||  
    |-|-|  
    |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|  
    |[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|C:\Windows\SysWOW64\SQLServerManager10.msc|  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-includessdenoversionincludesssdenoversion-mdmd"></a>So wird eine [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager mithilfe der oben genannten Anweisungen.  
  
2.  Wenn das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, klicken Sie auf **Ja**.  
  
3.  Klicken Sie im linken Bereich des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers auf **SQL Server-Dienste**.  
  
4.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf **SQL Server (MSSQLServer)** oder auf eine benannte Instanz, und klicken Sie anschließend auf **Starten**, **Beenden**, **Anhalten**, **Fortsetzen**oder **Neu starten**.  
  
5.  Klicken Sie auf **OK** , um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager zu schließen.  
  
> [!NOTE]  
>  Weitere Informationen zum Starten einer [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Instanz mit Startoptionen finden Sie unter [Konfigurieren von Serverstartoptionen &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-includessnoversionincludesssnoversion-mdmd-browser-or-an-instance-of-the-includessnoversionincludesssnoversion-mdmd-agent"></a>So wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Browser oder eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Instanz gestartet, beendet, angehalten, fortgesetzt oder neu gestartet  
  
1.  Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager mithilfe der oben genannten Anweisungen.  
  
2.  Wenn das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, klicken Sie auf **Ja**.  
  
3.  Klicken Sie im linken Bereich des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers auf **SQL Server-Dienste**.  
  
4.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Browser**, **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent (MSSQLServer)** oder **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent (<Instanzname>)** für eine benannte Instanz, und klicken Sie anschließend auf **Starten**, **Beenden**, **Anhalten**, **Fortsetzen** oder **Neu starten**.  
  
5.  Klicken Sie auf **OK** , um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager zu schließen.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent kann nicht angehalten werden.  
  
##  <a name="SSMSProcedure"></a> Verwenden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-includessdenoversionincludesssdenoversion-mdmd"></a>So wird eine [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her, klicken Sie mit der rechten Maustaste auf die zu startende [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz und anschließend auf **Starten**, **Beenden**, **Anhalten**, **Fortsetzen**oder **Neu starten**.  
  
     Klicken Sie alternativ im Bereich „Registrierte Server“ mit der rechten Maustaste auf die zu startende [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz, zeigen Sie auf die Option **Dienstkontrolle**, und klicken Sie anschließend auf **Starten**, **Beenden**, **Anhalten**, **Fortsetzen**oder **Neu starten**.  
  
2.  Wenn das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, klicken Sie auf **Ja**.  
  
3.  Klicken Sie bei der Frage, ob die Aktion ausgeführt werden soll, auf **Ja**.  
  
#### <a name="to-start-stop-or-restart-the-an-instance-of-the-includessnoversionincludesssnoversion-mdmd-agent"></a>So wird eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Instanz gestartet, beendet oder neu gestartet  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her, klicken Sie mit der rechten Maustaste auf **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent**, und klicken Sie anschließend auf **Starten**, **Beenden**oder **Neu starten**.  
  
2.  Wenn das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, klicken Sie auf **Ja**.  
  
3.  Klicken Sie bei der Frage, ob die Aktion ausgeführt werden soll, auf **Ja**.  
  
##  <a name="CommandPrompt"></a> Über das Eingabeaufforderungsfenster mit Net-Befehlen  
 Die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste können anhand von [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Befehlen von **-Befehlen von** Windows gestartet, beendet oder angehalten werden.  
  
###  <a name="dbDefault"></a> So starten Sie die Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   Geben Sie an einer Eingabeaufforderung einen der folgenden Befehle ein:  
  
     **net start "SQL Server (MSSQLSERVER)"**  
  
     -oder-  
  
     **net start MSSQLSERVER**  
  
###  <a name="dbNamed"></a> So starten Sie eine benannte Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   Geben Sie an einer Eingabeaufforderung einen der folgenden Befehle ein. Ersetzen Sie *\<Instanzname>* durch den Namen der Instanz, die Sie verwalten möchten.  
  
     **net start "SQL Server (** *Instanzname* **)"**  
  
     -oder-  
  
     **net start MSSQL$** *Instanzname*  
  
###  <a name="dbStartup"></a> So starten Sie [!INCLUDE[ssDE](../../includes/ssde-md.md)] mit Startoptionen  
  
-   Fügen Sie Startoptionen am Ende der Anweisung **net start "SQL Server (MSSQLSERVER)"** hinzu (durch ein Leerzeichen getrennt). Beim Starten mithilfe von **net start**wird ein Schrägstrich (/) anstelle eines Bindestriches (-) für die Startoptionen verwendet.  
  
     **net start "SQL Server (MSSQLSERVER)" /f /m**  
  
     -oder-  
  
     **net start MSSQLSERVER /f /m**  
  
    > [!NOTE]  
    >  Weitere Informationen finden Sie unter [Startoptionen für den Datenbankmoduldienst](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
###  <a name="agDefault"></a> So starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent auf der Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Geben Sie an einer Eingabeaufforderung einen der folgenden Befehle ein:  
  
     **net start "SQL Server-Agent (MSSQLSERVER)"**  
  
     -oder-  
  
     **net start SQLSERVERAGENT**  
  
###  <a name="agNamed"></a> So starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent auf einer benannten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Geben Sie an einer Eingabeaufforderung einen der folgenden Befehle ein. Ersetzen Sie *Instanzname* durch den Namen der Instanz, die Sie verwalten möchten.  
  
     **net start "SQL Server-Agent(** *Instanzname* **)"**  
  
     -oder-  
  
     **net start SQLAgent$** *Instanzname*  
  
 Informationen zum Ausführen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents im ausführlichen Modus zur Problembehandlung finden Sie unter [sqlagent90 (Anwendung)](../../tools/sqlagent90-application.md).  
  
###  <a name="Browser"></a> So starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser  
  
-   Geben Sie an einer Eingabeaufforderung einen der folgenden Befehle ein:  
  
     **net start "SQL Server Browser"**  
  
     -oder-  
  
     **net start SQLBrowser**  
  
###  <a name="pauseStop"></a> So werden Dienste über das Eingabeaufforderungsfenster angehalten oder beendet  
  
-   Ändern Sie zum Anhalten oder Beenden von Diensten die Befehle wie folgt.  
  
    -   Um einen Dienst anzuhalten, ersetzen Sie **net start** durch **net pause**.  
  
    -   Um einen Dienst zu beenden, ersetzen Sie **net start** durch **net stop**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] lässt sich mit der **SHUTDOWN** -Anweisung beenden.  
  
#### <a name="to-stop-the-includessdeincludesssde-mdmd-using-includetsqlincludestsql-mdmd"></a>So beenden Sie [!INCLUDE[ssDE](../../includes/ssde-md.md)] mit [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
-   Um nach der vollständigen Ausführung von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen und gespeicherten Prozeduren [!INCLUDE[ssDE](../../includes/ssde-md.md)]zu beenden, führen Sie die folgende Anweisung aus.  
  
    ```sql  
    SHUTDOWN;   
    ```  
  
-   Um [!INCLUDE[ssDE](../../includes/ssde-md.md)] sofort zu beenden, führen Sie die folgende Anweisung aus.  
  
    ```sql  
    SHUTDOWN WITH NOWAIT;   
    ```  
  
 Weitere Informationen zur **SHUTDOWN**-Anweisung finden Sie unter [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md).  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
  
#### <a name="to-start-and-stop-includessdeincludesssde-mdmd-services"></a>So starten und beenden Sie [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Dienste  
  
1.  Starten Sie in einem Eingabeaufforderungsfenster [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell durch das Ausführen des folgenden Befehls.  
  
    ```ms-dos  
    sqlps  
    ```  
  
2.  Führen Sie an einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Eingabeaufforderung den folgenden Befehl aus. Ersetzen Sie `computername` durch den Namen des Computers.  
  
    ```powershell  
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\computername  
    $Wmi = (get-item .).ManagedComputer  
  
    ```  
  
3.  Identifizieren Sie den Dienst, den Sie beenden oder starten möchten. Wählen Sie eine der folgenden Zeilen aus. Ersetzen Sie `instancename` durch den Namen der benannten Instanz.  
  
    -   Abrufen eines Verweises auf die Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQLSERVER']  
        ```  
  
    -   Abrufen eines Verweises auf die benannte Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQL$instancename']  
        ```  
  
    -   Abrufen eines Verweises auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst auf der Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLSERVERAGENT']  
        ```  
  
    -   Abrufen eines Verweises auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst auf einer benannten Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLAGENT$instancename']  
        ```  
  
    -   Abrufen eines Verweises auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browserdienst.  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLBROWSER']  
        ```  
  
4.  Starten Sie anhand des Beispiels den ausgewählten Dienst, und beenden Sie ihn anschließend.  
  
    ```powershell  
    # Display the state of the service.  
    $DfltInstance  
    # Start the service.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über die SQL Server-Setupdokumentation](http://msdn.microsoft.com/library/2620439a-f9d3-4b3c-9968-48f60b4bb9a5)   
 [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [SQL Server-Konfigurations-Manager](../../relational-databases/sql-server-configuration-manager.md)   
 [Starten von SQL Server mit Minimalkonfiguration](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md)   
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)  
  
  

